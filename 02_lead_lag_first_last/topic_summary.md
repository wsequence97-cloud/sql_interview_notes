# lead_lag_first_last

## 1. 题型定义

本题型主要考察在同一分组内访问前后行或首尾值，常用于环比、相邻记录比较、状态变化识别、首末状态判断等问题。

## 2. 核心套路

* 用 `lag()` 取上一行。
* 用 `lead()` 取下一行。
* 相邻行比较：同一分组内同时取前一行和后一行，再用 `case when` 判断当前行类型。
* 前后有效值填充：用窗口范围向前或向后寻找最近满足条件的记录。
* 用 `first_value()` 取窗口内第一行。
* 用 `last_value()` 时注意窗口边界。
* 结合 `case when` 做状态变化判断。

## 3. 常用 Hive 函数

* `lag()`
* `lead()`
* `first_value()`
* `last_value()`
* `row_number()`
* `sum() over()`
* `case when`
* `max() over()`
* `min() over()`
* `coalesce()`

## 4. 通用解题模板

```sql
with data as (
    select 1 as user_id, '2023-01-01' as event_date, 'A' as status union all
    select 1 as user_id, '2023-01-02' as event_date, 'B' as status
),
ordered_data as (
    select
        user_id,
        event_date,
        status,
        lag(status) over(partition by user_id order by event_date) as prev_status,
        lead(status) over(partition by user_id order by event_date) as next_status
    from data
)
select *
from ordered_data;
```

## 5. 已收录题目

| 序号 | 文件名 | 题目标题 | 核心考点 | 是否有我的解答 | 是否已分析 |
|---|---|---|---|---|---|
| 001 | `001_查询股票波峰波谷.md` | 查询股票波峰波谷 | lag、lead、相邻价格比较、case when 打标 | 是 | 是 |
| 002 | `002_查询前后开市日期.md` | 查询前后开市日期 | 前后有效值、窗口范围、max/min over、first_value/last_value | 是 | 是 |
| 003 | `003_按状态连续段累计计数.md` | 按状态连续段累计计数 | lag、状态变化打标、累计分组、段内 row_number | 是 | 是 |

## 6. 本题型高频易错点

* `lag()` 和 `lead()` 没有写 `order by`。
* 有分组对象时忘记写 `partition by`，导致不同股票之间互相比较。
* 原始数据不是有序输入时，直接按输入顺序比较会出错，必须按日期字段排序。
* `last_value()` 忘记设置窗口边界，导致只能看到当前行。
* 没有处理第一行或最后一行的空值。
* 计算前后有效值时，要确认是否包含当前行；本题的 `pre_date` 和 `next_date` 都不包含当前行。
* `first_value(expr, true)` / `last_value(expr, true)` 可以忽略空值，但必须配合正确窗口边界。
* 直接按状态值分组会把不相邻的同状态合并，连续段题必须先生成段编号。

## 7. 面试表达模板

这类题我会先明确分组字段和排序字段，再用 `lag` 或 `lead` 取相邻记录。拿到前后行之后，用 `case when` 判断是否发生变化，最后根据题目要求筛选、打标或聚合。
