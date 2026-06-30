# 留存计算

## 1. 题型定义

留存计算类题目主要考察用户首日、次日、N 日回访，以及分子分母口径的定义。

## 2. 核心套路

* 先确定用户的基准日期。
* 再关联后续活跃日期。
* 用 `datediff()` 判断 N 日留存。
* 最后按日期或 cohort 聚合。

## 3. 常用 Hive 函数

* `to_date()`
* `min()`
* `datediff()`
* `count(distinct ...)`
* `left join`
* `case when`

## 4. 通用解题模板

```sql
with data as (
    select 1 as user_id, '2023-01-01' as login_date union all
    select 1 as user_id, '2023-01-02' as login_date
),
first_login as (
    select
        user_id,
        min(to_date(login_date)) as first_date
    from data
    group by user_id
),
active_data as (
    select distinct
        user_id,
        to_date(login_date) as active_date
    from data
)
select
    f.first_date,
    count(distinct f.user_id) as user_cnt,
    count(distinct case when datediff(a.active_date, f.first_date) = 1 then f.user_id end) as retained_user_cnt
from first_login f
left join active_data a
    on f.user_id = a.user_id
group by f.first_date;
```

## 5. 已收录题目

| 序号 | 文件名 | 题目标题 | 核心考点 | 是否有我的解答 | 是否已分析 |
|---|---|---|---|---|---|
| - | - | 当前暂无题目 | - | - | - |

## 6. 本题型高频易错点

* 分母口径不清晰。
* 忘记按用户和日期去重。
* 用 inner join 导致未留存用户丢失。
* N 日留存的日期差方向写反。

## 7. 面试表达模板

这类题我会先定义 cohort，也就是每个用户的基准日期；然后把用户后续活跃日期关联回来，用 `datediff` 判断是否满足 N 日留存，最后按 cohort 日期统计分子和分母。
