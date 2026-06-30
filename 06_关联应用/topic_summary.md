# 关联应用

## 1. 题型定义

关联应用类题目主要考察多表 join、自关联、半连接、反连接，以及不同 join 条件对结果行数的影响。

## 2. 核心套路

* 明确主表和保留口径。
* 根据是否保留未匹配记录选择 `inner join` 或 `left join`。
* 反关联用 `left join ... where right_key is null`。
* 自关联要给表起清晰别名。

## 3. 常用 Hive 函数

* `inner join`
* `left join`
* `left semi join`
* `case when`
* `coalesce()`

## 4. 通用解题模板

```sql
with users as (
    select 1 as user_id, 'A' as user_name
),
orders as (
    select 1 as user_id, 100 as amount
)
select
    u.user_id,
    u.user_name,
    o.amount
from users u
left join orders o
    on u.user_id = o.user_id;
```

## 5. 已收录题目

| 序号 | 文件名 | 题目标题 | 核心考点 | 是否有我的解答 | 是否已分析 |
|---|---|---|---|---|---|
| 001 | `001_查询每门课都大于60分的学生成绩.md` | 查询每门课都大于60分的学生成绩 | 多表关联、分组过滤后回表取明细 | 是 | 是 |

## 6. 本题型高频易错点

* 把 `left join` 写成 `inner join` 导致主表记录丢失。
* join 条件不完整导致数据膨胀。
* 过滤右表字段时把外连接变成内连接。

## 7. 面试表达模板

这类题我会先确定哪张表是主表、哪些记录必须保留，再选择 join 类型。写完关联后要检查 join 条件是否唯一，避免重复匹配导致指标膨胀。
