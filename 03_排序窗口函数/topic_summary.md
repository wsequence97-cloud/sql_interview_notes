# 排序窗口函数

## 1. 题型定义

排序窗口函数题主要考察在分组内排序、取 TopN、处理并列名次，以及区分 `row_number`、`rank`、`dense_rank` 的使用场景。

## 2. 核心套路

* 每组取唯一 Top1：优先 `row_number()`。
* 需要保留并列名次：使用 `rank()` 或 `dense_rank()`。
* 排序字段必须明确升序或降序。
* 外层根据排名字段筛选。

## 3. 常用 Hive 函数

* `row_number()`
* `rank()`
* `dense_rank()`
* `sum() over()`
* `count() over()`

## 4. 通用解题模板

```sql
with data as (
    select 10 as dept_id, 'A' as emp_name, 1000 as salary union all
    select 10 as dept_id, 'B' as emp_name, 1200 as salary
),
ranked_data as (
    select
        dept_id,
        emp_name,
        salary,
        row_number() over(partition by dept_id order by salary desc) as rn
    from data
)
select
    dept_id,
    emp_name,
    salary
from ranked_data
where rn = 1;
```

## 5. 已收录题目

| 序号 | 文件名 | 题目标题 | 核心考点 | 是否有我的解答 | 是否已分析 |
|---|---|---|---|---|---|
| - | - | 当前暂无题目 | - | - | - |

## 6. 本题型高频易错点

* 分不清 `row_number()`、`rank()`、`dense_rank()` 对并列的处理。
* 排序方向写反。
* 需要保留并列第一时误用 `row_number()`。

## 7. 面试表达模板

这类题我会先确定分组维度和排序指标，再根据是否需要处理并列选择窗口函数。如果只要每组一条记录，用 `row_number`；如果并列都要保留，用 `rank` 或 `dense_rank`。
