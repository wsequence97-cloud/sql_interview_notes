# 数据展开与收缩

## 1. 题型定义

数据展开与收缩类题目主要考察行列转换、列转行、行转列、集合聚合与字符串拼接。

## 2. 核心套路

* 列转行可用 `union all` 或 `stack()`。
* 行转列常用条件聚合。
* 多行收缩为一行可用 `collect_set()` 和 `concat_ws()`。

## 3. 常用 Hive 函数

* `stack()`
* `union all`
* `case when`
* `max()`
* `sum()`
* `collect_set()`
* `concat_ws()`

## 4. 通用解题模板

```sql
with data as (
    select 1 as user_id, 'math' as subject, 90 as score union all
    select 1 as user_id, 'english' as subject, 80 as score
)
select
    user_id,
    max(case when subject = 'math' then score end) as math_score,
    max(case when subject = 'english' then score end) as english_score
from data
group by user_id;
```

## 5. 已收录题目

| 序号 | 文件名 | 题目标题 | 核心考点 | 是否有我的解答 | 是否已分析 |
|---|---|---|---|---|---|
| - | - | 当前暂无题目 | - | - | - |

## 6. 本题型高频易错点

* 行转列时聚合函数选择不当。
* 多值拼接前没有去重或排序。
* 列转行后字段类型不一致。

## 7. 面试表达模板

这类题我会先判断是展开还是收缩。展开时把宽表字段拆成多行；收缩时用条件聚合或集合函数把多行合并成一行。
