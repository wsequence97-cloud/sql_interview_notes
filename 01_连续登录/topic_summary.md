# 连续登录

## 1. 题型定义

连续登录类题目主要考察如何在时间序列中识别连续区间、连续状态或连续行为，并进一步统计连续天数、筛选满足条件的连续段，或合并相邻状态区间。

## 2. 核心套路

* 日期连续：先按用户和日期去重，再用 `row_number()` 编号。
* 连续分组：用 `date_sub(date, rn)` 得到稳定分组标记。
* 最大连续天数：先统计每段连续天数，再按用户取 `max()`。
* 允许间隔一天：用 `lag()` 取上次登录日期，若 `datediff(dt, last_dt) > 2` 则开启新连续段。
* 状态连续：用 `lag()` 判断状态是否变化，再用累计求和生成连续段编号。
* 日期区间连续：如果题目要求严格日期连续，用 `lag(end_date)` 判断 `date_add(prev_end_date, 1) = start_date` 是否延续上一段。
* 相邻状态区间合并：如果期望结果不要求日期连续，就用 `lag(type)` 判断相邻状态是否变化，再累计新段标记。
* 连续命中条件：先筛出满足条件的日期，再用 `date_sub(dt, row_number)` 判断命中日期是否连续。
* 区间合并：按连续段编号聚合，取最小开始时间和最大结束时间。
* 累计打标：用 `rows between ... and ...` 明确窗口函数每一行的计算范围。

## 3. 常用 Hive 函数

* `to_date()`
* `date_sub()`
* `date_add()`
* `datediff()`
* `date_format()`
* `row_number()`
* `lag()`
* `sum() over()`
* `rows between ... and ...`
* `count()`
* `max()`
* `min()`

## 4. 通用解题模板

```sql
with data as (
    select 1 as user_id, '2023-01-01 00:00:00' as login_time union all
    select 1 as user_id, '2023-01-02 00:00:00' as login_time
),
login_distinct as (
    select distinct
        user_id,
        to_date(login_time) as login_date
    from data
),
login_ranked as (
    select
        user_id,
        login_date,
        row_number() over(partition by user_id order by login_date) as rn
    from login_distinct
),
login_grouped as (
    select
        user_id,
        login_date,
        date_sub(login_date, cast(rn as int)) as group_date
    from login_ranked
)
select
    user_id,
    group_date,
    count(*) as day_cnt
from login_grouped
group by user_id, group_date;
```

### 4.1 `rows between` 窗口范围理解

`rows between` 用来限定窗口函数每一行的计算范围。它不是只能表示“从第一行到当前行”，而是可以控制当前行向前、向后看多少行。

通用语法：

```sql
聚合函数(...) over(
    partition by 分组字段
    order by 排序字段
    rows between 起点 and 终点
)
```

常见边界含义：

| 写法 | 含义 |
|---|---|
| `unbounded preceding` | 当前分组的第一行 |
| `n preceding` | 当前行往前第 n 行 |
| `current row` | 当前行 |
| `n following` | 当前行往后第 n 行 |
| `unbounded following` | 当前分组的最后一行 |

常见窗口范围：

| 写法 | 作用 | 常见场景 |
|---|---|---|
| `rows between unbounded preceding and current row` | 从第一行累计到当前行 | 累计和、累计打标、连续段编号 |
| `rows between 2 preceding and current row` | 当前行和前 2 行，共 3 行 | 最近 3 条记录滚动统计 |
| `rows between 6 preceding and current row` | 当前行和前 6 行，共 7 行 | 最近 7 条记录滚动统计 |
| `rows between 1 preceding and 1 following` | 前一行、当前行、后一行 | 当前点附近窗口统计 |
| `rows between current row and unbounded following` | 当前行累计到最后一行 | 反向累计、剩余量统计 |
| `rows between unbounded preceding and unbounded following` | 整个分组所有行 | 组内总量、组内最大最小 |

例 1：从第一行累计到当前行

连续状态题里最常见的是：

```sql
sum(is_new_group) over(
    partition by user_id
    order by event_date
    rows between unbounded preceding and current row
) as group_id
```

这表示每个用户内部按时间排序，从第一条记录一直累计到当前行。

如果 `is_new_group = 1` 表示“新连续段开始”，`is_new_group = 0` 表示“延续上一段”，那么累计求和后就能得到连续段编号：

| 日期 | 状态 | is_new_group | group_id |
|---|---|---:|---:|
| 01 | a | 1 | 1 |
| 05 | a | 0 | 1 |
| 10 | b | 1 | 2 |
| 14 | b | 0 | 2 |
| 18 | a | 1 | 3 |

记忆方式：

```text
is_new_group：当前行是不是新段
sum(is_new_group) over(rows between ... current row)：当前行属于第几段
```

例 2：最近 3 行滚动求和

```sql
sum(amount) over(
    partition by user_id
    order by event_date
    rows between 2 preceding and current row
) as recent_3_amount
```

这一行会统计：

```text
前 2 行 + 当前行
```

适合“最近 3 次消费金额”“最近 3 条记录平均值”这类题。

例 3：前后各 1 行的窗口

```sql
avg(score) over(
    partition by class_id
    order by exam_date
    rows between 1 preceding and 1 following
) as around_avg_score
```

这一行会统计：

```text
上一行 + 当前行 + 下一行
```

适合平滑分数、局部均值这类场景。

例 4：整个分组窗口

```sql
max(score) over(
    partition by class_id
    rows between unbounded preceding and unbounded following
) as class_max_score
```

这一行会在班级内所有行中取最大值，结果不会把多行压成一行，每个学生行都会带上班级最高分。

`rows` 和普通 `group by` 的区别：

```text
group by：多行聚合成一行
rows between + over：每行仍然保留，只是给每行补一个窗口计算结果
```

## 5. 已收录题目

| 序号 | 文件名 | 题目标题 | 核心考点 | 是否有我的解答 | 是否已分析 |
|---|---|---|---|---|---|
| 001 | `001_查询连续登陆3天以上的用户.md` | 查询连续登录 3 天以上的用户 | 日期去重、row_number、连续分组、having 筛选 | 是 | 是 |
| 002 | `002_查询每个用户最大连续登录天数.md` | 查询每个用户最大连续登录天数 | 日期去重、连续分组、每段计数、取最大值 | 是 | 是 |
| 003 | `003_日期连续区间合并.md` | 日期连续区间合并 | lag、状态变化打标、累计求和、区间合并 | 否 | 是 |
| 004 | `004_查询每个选手最长连胜数.md` | 查询每个选手最长连胜数 | 连续状态、非 Win 打断、累计分组、取最大值 | 是 | 是 |
| 005 | `005_查询每个用户可间隔一天的最大连续登录天数.md` | 查询每个用户可间隔一天的最大连续登录天数 | lag、允许间隔一天、累计分组、日期跨度 | 是 | 是 |
| 006 | `006_找出UV增长率连续超过30%的日期.md` | 找出 UV 增长率连续超过 30% 的日期 | lag、增长率、连续命中分组、having 筛选 | 是 | 是 |
| 007 | `007_日期有断区间合并.md` | 日期有断区间合并 | lag、状态变化打标、日期断开但相邻状态合并 | 否 | 是 |

## 6. 本题型高频易错点

* 忘记先按用户和日期去重。
* 只按用户分组，没有按连续段标记分组。
* Hive 中误写 MySQL 的 `interval n day`。
* 没有区分“连续日期”和“相邻状态连续”；要以期望结果为准，严格日期连续才判断上一段 `end_date + 1 天` 是否等于当前 `start_date`。
* 日期有断但期望仍然合并时，不能用 `date_add(lag(end_date), 1) = start_date` 做打断条件。
* 状态区间合并时直接按状态分组，导致前后两段同状态被错误合并。
* 连胜类题目不能先过滤 `Win` 再分组，否则会丢失 `Draw` / `Lose` 这些打断点。
* Hive 字符串比较要注意大小写，样例是 `Win` 时不要误写成 `win`。
* 只统计胜场段时，要确认题目是否要求返回从未赢过的选手；如果要求返回，需要先保留全量选手再左连接。
* 不写 `rows between ...` 时，要确认 Hive 默认窗口范围是否符合当前题意。
* “累计到当前行”用 `unbounded preceding and current row`；“滚动最近 N 行”用 `N-1 preceding and current row`。
* 允许间隔一天时，每段长度应按日期跨度算 `datediff(max(dt), min(dt)) + 1`，不是简单 `count(*)`。
* 计算每段跨度时要按 `uid, flag` 分组，不能只按 `uid` 分组。
* 计算增长率时要转成 double，避免整数除法；连续增长题要先筛出命中日期，再判断命中日期是否连续。

## 7. 面试表达模板

这类题我一般先把时间字段标准化成日期，并处理重复数据。对于日期连续问题，可以用 `row_number()` 编号，再用日期减行号生成连续段标记；对于状态连续问题，可以用 `lag()` 判断前后状态是否变化，再对变化标记做累计求和生成连续段编号。最后按连续段聚合，得到连续天数或合并后的时间区间。
