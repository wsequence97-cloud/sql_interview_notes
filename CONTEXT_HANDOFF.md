# CONTEXT_HANDOFF

## 1. Current task goal

维护并持续扩展 `D:\WorkSpace\AA_da\leetcode\sql_interview_notes` SQL 面试题笔记库。每道题一份 Markdown 文件，放入对应题型目录，并严格遵守 `SQL题目生成格式规范.md` 的新版 6 段结构。

## 2. User requirements and preferences

- 中文输出，内容面向 SQL 面试刷题和个人错题复盘。
- 每道单题 Markdown 只保留 6 个部分：
  1. 题目描述
  2. 期望结果
  3. 标准答案
  4. 我的解答
  5. 我的解答正确版本
  6. 我的复盘要点
- 标准答案默认使用 Hive SQL CTE 完整版，包含样例数据 CTE、解题过程 CTE、最终查询。
- 如果用户给出自己的 SQL，必须原样保留在 `## 4. 我的解答`，不要擅自修正。
- `## 5. 我的解答正确版本` 基于用户原始 SQL 修正，重点关注能否运行、思路是否正确、口径是否正确，不要纠缠别名美观、排版、是否加 `as`。
- `## 6. 我的复盘要点` 要像用户自己的错题本，优先使用 `【我的卡点】`、`【错误原因】`、`【修正记法】`、`【下次先想】`、`【本题坑点】`。
- 不要编造用户没有写过的解答或没有讨论过的个人感悟。
- 新增题目后通常同步更新对应 `topic_summary.md`、根目录 `README.md`、`generation_check_report.md`。

## 3. Current phase and progress

当前处于 SQL 题库持续维护阶段。最近主要在 `04_累计汇总` 目录新增和完善题目，并把旧的第 6 段 `题目所需注意要点` 全部重构为 `我的复盘要点`。

当前单题数量：

| 目录 | 单题数量 |
|---|---:|
| `01_连续登录` | 6 |
| `02_lead_lag_first_last` | 3 |
| `03_排序窗口函数` | 0 |
| `04_累计汇总` | 5 |
| `05_炸裂函数` | 0 |
| `06_关联应用` | 1 |
| `07_留存计算` | 0 |
| `08_数据展开与收缩` | 0 |
| `09_合并区间` | 0 |
| `10_状态标记与填补缺失值` | 0 |

## 4. Completed changes

已完成全库单题格式重构：

- 13 个既有单题文件全部改为新版 6 段结构。
- 新增检查报告 `refactor_check_report.md`。
- 旧标题 `## 6. 题目所需注意要点` 已替换为 `## 6. 我的复盘要点`。

近期新增/完善的 `04_累计汇总` 题目：

- `04_累计汇总/001_统计每个用户累计访问次数.md`
  - 已保留用户原始解答。
  - 重点：日期字符串转月份、先月度小计再累计。
- `04_累计汇总/002_统计直播间最大同时在线人数.md`
  - 已补用户解答。
  - 重点：登录 `+1`、退出 `-1` 的扫描线。
- `04_累计汇总/003_统计每小时同时在线人数.md`
  - 已保留用户原始解答。
  - 重点复盘：在线区间展开到整点小时、`split(space(...))`、`lateral view posexplode`。
- `04_累计汇总/004_求最小达到累计金额日期.md`
  - 原始数据已改成用户解答里的 2025-03 数据。
  - 已保留用户原始解答。
  - 重点：`rows` 是前 N 行，`range` 才适合日期范围；先筛达标行再按用户取 `min(dt)`。
- `04_累计汇总/005_查询历史新低的商品ID.md`
  - 已保留用户原始解答。
  - 修正版修正了 `strat_price` -> `start_price`、`rank = 1` -> `rank_ts = 1`、`<` vs `<=` 口径。

其他已存在题目：

- `01_连续登录/001_查询连续登陆3天以上的用户.md`
- `01_连续登录/002_查询每个用户最大连续登录天数.md`
- `01_连续登录/003_日期连续区间合并.md`
- `01_连续登录/004_查询每个选手最长连胜数.md`
- `01_连续登录/005_查询每个用户可间隔一天的最大连续登录天数.md`
- `01_连续登录/006_找出UV增长率连续超过30%的日期.md`
- `02_lead_lag_first_last/001_查询股票波峰波谷.md`
- `02_lead_lag_first_last/002_查询前后开市日期.md`
- `02_lead_lag_first_last/003_按状态连续段累计计数.md`
- `06_关联应用/001_查询每门课都大于60分的学生成绩.md`

## 5. Key files, functions, and configuration

Core specification:

- `SQL题目生成格式规范.md`

Root tracking/index files:

- `README.md`
- `generation_check_report.md`
- `refactor_check_report.md`
- `CONTEXT_HANDOFF.md`

Topic summaries:

- `01_连续登录/topic_summary.md`
- `02_lead_lag_first_last/topic_summary.md`
- `04_累计汇总/topic_summary.md`
- `06_关联应用/topic_summary.md`

Recent key problem file:

- `04_累计汇总/005_查询历史新低的商品ID.md`

## 6. Commands run and results

- `Get-Content -LiteralPath 'SQL题目生成格式规范.md' -Encoding UTF8`
  - Confirmed current fixed 6 sections use `## 6. 我的复盘要点`.
- Scanned topic directories with PowerShell.
  - Counts found: `01=6`, `02=3`, `03=0`, `04=5`, `05=0`, `06=1`, `07=0`, `08=0`, `09=0`, `10=0`.
- `git status --short`
  - Returned `fatal: not a git repository (or any of the parent directories): .git`.
  - Do not rely on git status in this workspace.
- Multiple `rg -n ...` checks confirmed newly edited files have correct section headings.

## 7. Current errors or blockers

- No active blocker.
- Workspace is not a git repository according to `git status --short`.
- Some root/report files may still be incremental rather than perfectly regenerated, but current recent updates have been recorded in `README.md`, `topic_summary.md`, and `generation_check_report.md`.

## 8. Important decisions and reasons

- Standard answers should not stack multiple alternatives. If the prompt image gives two possible answers, choose the best one for `## 3. 标准答案` and put contrast/limitations in `## 6. 我的复盘要点`.
- For `04_累计汇总/004_求最小达到累计金额日期.md`, user wanted original data replaced with their own sample. The file now uses user IDs `1001/1002/1003` and dates in `2025-03`.
- For “达到 1W”, the current file uses `>= 10000` because the user's own data/comments used this口径, even though the screenshot answer had `> 10000`. The复盘 notes mention confirming threshold口径.
- For “历史新低商品”, current口径 follows screenshot: latest `after_price <= history_lowest_price` counts as historical low. If strict new low is required, change to `<`.

## 9. Next plan

If user continues with a new SQL problem:

1. Read or rely on `SQL题目生成格式规范.md` if not recently read.
2. Determine target topic directory.
3. Find next sequence number in that directory.
4. Create one Markdown file with exactly the 6 required sections.
5. Use Hive SQL CTE full standard answer.
6. Preserve user SQL exactly in `## 4. 我的解答`.
7. Write a corrected Hive version in `## 5. 我的解答正确版本`.
8. Write 3-5 concise personal复盘 points in `## 6. 我的复盘要点`.
9. Update relevant `topic_summary.md`, `README.md`, and `generation_check_report.md`.
10. Verify with `rg`/PowerShell that headings and tracking files are correct.

## 10. Things not to repeat

- Do not use old section title `题目所需注意要点` in new single-question files.
- Do not add old sections such as `核心步骤解释`、`记忆点`、`面试口述版`、`关联题型`.
- Do not silently “beautify” the user's original SQL in `## 4. 我的解答`.
- Do not write復盤 points about pure formatting unless it causes a runtime error or logic ambiguity.
- Do not assume `rows between N preceding` means “近 N 天”; it means previous N rows.
- Do not rely on git status for change tracking in this workspace.

## 11. Recovery instructions after compact

After compact, first read:

- `CONTEXT_HANDOFF.md`
- `SQL题目生成格式规范.md`
- Recent file if the user references one, especially under `04_累计汇总`

Then restate:

- Current goal
- Completed work
- Current blockers
- Next plan

Do not edit files immediately after compact until state is confirmed, unless the user explicitly asks to proceed.

## 12. Known context usage and compact recovery instructions

This thread is long and the user explicitly invoked `context-compact-handoff`. A durable handoff has been written.

If compacting, run:

```text
/compact
```

Recommended first post-compact user message:

```text
Read CONTEXT_HANDOFF.md first. Restate the current goal, completed work, blockers, and next plan. Do not edit code yet; continue only after the state is confirmed.
```
