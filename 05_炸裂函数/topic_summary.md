# 炸裂函数

## 1. 题型定义

炸裂函数题主要考察字符串、数组、集合字段的拆分与展开，例如一行多值拆成多行。

## 2. 核心套路

* 用 `split()` 把字符串拆成数组。
* 用 `lateral view explode()` 展开数组。
* 展开后再做过滤、关联或聚合。

## 3. 常用 Hive 函数

* `split()`
* `explode()`
* `lateral view explode()`
* `posexplode()`
* `concat_ws()`
* `collect_set()`

## 4. 通用解题模板

```sql
with data as (
    select 1 as id, 'a,b,c' as tags
),
exploded_data as (
    select
        id,
        tag
    from data
    lateral view explode(split(tags, ',')) t as tag
)
select *
from exploded_data;
```

## 5. 已收录题目

| 序号 | 文件名 | 题目标题 | 核心考点 | 是否有我的解答 | 是否已分析 |
|---|---|---|---|---|---|
| - | - | 当前暂无题目 | - | - | - |

## 6. 本题型高频易错点

* 忘记 `lateral view` 语法。
* 分隔符没有转义。
* 展开后行数变多，后续聚合口径需要重新确认。

## 7. 面试表达模板

这类题我会先把多值字段用 `split` 拆成数组，再用 `lateral view explode` 展开成多行，最后基于展开后的明细继续做过滤、聚合或关联。
