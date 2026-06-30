# 合并区间

## 1. 题型定义

合并区间类题目主要考察时间区间的重叠、相邻、包含、交集和合并。

## 2. 核心套路

* 按开始时间排序。
* 用 `lag()` 或累计最大结束时间判断是否开启新区间。
* 对新区间标记累计求和生成区间组。
* 按区间组聚合得到合并结果。

## 3. 常用 Hive 函数

* `lag()`
* `max() over()`
* `sum() over()`
* `date_add()`
* `date_sub()`
* `greatest()`
* `least()`

## 4. 通用解题模板

```sql
with data as (
    select 1 as id, '2023-01-01' as start_date, '2023-01-03' as end_date union all
    select 1 as id, '2023-01-02' as start_date, '2023-01-05' as end_date
),
base as (
    select
        id,
        to_date(start_date) as start_date,
        to_date(end_date) as end_date
    from data
),
ordered_data as (
    select
        id,
        start_date,
        end_date,
        max(end_date) over(partition by id order by start_date rows between unbounded preceding and 1 preceding) as prev_max_end_date
    from base
)
select *
from ordered_data;
```

## 5. 已收录题目

| 序号 | 文件名 | 题目标题 | 核心考点 | 是否有我的解答 | 是否已分析 |
|---|---|---|---|---|---|
| - | - | 当前暂无题目 | - | - | - |

## 6. 本题型高频易错点

* 只比较上一行结束时间，忽略前面区间的最大结束时间。
* 没有区分重叠区间和相邻区间。
* 区间边界是否闭区间没有说明。

## 7. 面试表达模板

这类题我会先按开始时间排序，再判断当前区间是否和前面已经合并的最大结束时间相连或重叠。如果不能合并，就打新组标记；最后累计求和生成组号并按组聚合。
