# 状态标记与填补缺失值

## 1. 题型定义

状态标记与填补缺失值类题目主要考察如何识别状态变化、生成分组标记，以及把缺失值用前值或后值填补。

## 2. 核心套路

* 用 `lag()` 判断状态变化。
* 用累计求和生成状态段编号。
* 用窗口函数辅助填补缺失值。
* 根据业务口径决定向前填补还是向后填补。

## 3. 常用 Hive 函数

* `lag()`
* `lead()`
* `sum() over()`
* `max() over()`
* `first_value()`
* `last_value()`
* `coalesce()`
* `case when`
* `collect_set()`
* `array_contains()`
* `date_format()`

## 4. 通用解题模板

```sql
with data as (
    select 1 as user_id, '2023-01-01' as dt, 'A' as status union all
    select 1 as user_id, '2023-01-02' as dt, 'A' as status union all
    select 1 as user_id, '2023-01-03' as dt, 'B' as status
),
marked_data as (
    select
        user_id,
        dt,
        status,
        case
            when lag(status) over(partition by user_id order by dt) = status then 0
            else 1
        end as is_new_group
    from data
)
select *
from marked_data;
```

## 5. 已收录题目

| 序号 | 文件名 | 题目标题 | 核心考点 | 是否有我的解答 | 是否已分析 |
|---|---|---|---|---|---|
| 001 | `001_统计原创文章被引用次数.md` | 统计原创文章被引用次数 | collect_set 状态集合、array_contains、条件聚合 | 否 | 是 |
| 002 | `002_用前后非空均值填补缺失值.md` | 用前后非空均值填补缺失值 | first_value、last_value、忽略空值、窗口边界 | 否 | 是 |
| 003 | `003_递归顺延差值转累计窗口.md` | 递归顺延差值转累计窗口 | 累计窗口、顺延差值、负数归零 | 否 | 是 |

## 6. 本题型高频易错点

* 状态变化题没有明确排序字段。
* 填补缺失值时窗口边界写错。
* 没有区分连续状态段和全局同状态。
* 用集合状态判断引用关系时，忘记过滤 `oid = 0` 的原创文章本身。
* 用前后非空值填补时，窗口边界没有覆盖到当前行之前和之后的完整范围。
* 看到“上一行不足顺延到下一行”就想写递归，忽略了累计金额差值可以直接表达顺延效果。

## 7. 面试表达模板

这类题我会先按业务主键和时间排序，用 `lag` 判断当前状态是否和上一行一致，再把变化点打标。对于缺失值填补，则会根据题目要求选择前向或后向窗口逻辑。
