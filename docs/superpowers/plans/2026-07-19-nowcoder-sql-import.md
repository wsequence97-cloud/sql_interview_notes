# 牛客 SQL 大厂真题导入 Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** 将公开可核验、难度为中等及以上、与现有题型匹配且不重复的牛客 SQL 大厂真题导入当前六段式 Hive SQL 题库。

**Architecture:** 先对 15 道高价值候选题执行来源完整性和语义去重门禁，再按核心题型分批生成单题 Markdown。最后统一更新题型总结、README 和检查报告，并通过结构、编号、来源及 Hive 语法静态检查。

**Tech Stack:** Markdown、Hive SQL、PowerShell、ripgrep、牛客公开题目页

---

### Task 1: 建立候选题来源与去重审计

**Files:**
- Read: `SQL题目生成格式规范.md`
- Read: `docs/superpowers/specs/2026-07-19-nowcoder-sql-import-design.md`
- Read: `01_连续登录/*.md`
- Read: `02_lead_lag_first_last/*.md`
- Read: `03_排序窗口函数/*.md`
- Read: `04_累计汇总/*.md`
- Read: `06_关联应用/*.md`
- Read: `07_留存计算/*.md`
- Read: `09_合并区间/*.md`
- Modify: `generation_check_report.md`

**候选来源：**

牛客公开题单共 118 道。先按难度排除入门和简单题，再对所有中等、较难、困难题执行标题与查询目标初筛；下表是进入详情核验的 15 道高价值候选。其余中等及以上题目也必须在检查报告中按“普通聚合、与现有题重复、核心题型不匹配、公开内容不足”记录排除原因，不能只记录下表题目。

| 题号 | 题目 | 难度 | 目标目录 | 公开题目页 |
|---|---|---|---|---|
| SQL40 | 每个月 Top3 的周杰伦歌曲 | 较难 | `03_排序窗口函数` | `https://www.nowcoder.com/practice/4ab6d198ea8447fe9b6a1cad1f671503` |
| SQL62 | 支付间隔平均值 | 中等 | `02_lead_lag_first_last` | `https://www.nowcoder.com/practice/847431ad931e45348eb1ab5657144c28` |
| SQL63 | 网易云音乐推荐 | 较难 | `06_关联应用` | `https://www.nowcoder.com/practice/048ed413ac0e4cf4a774b906fc87e0e7` |
| SQL78 | 商品销售总额分布 | 中等 | `04_累计汇总` | `https://www.nowcoder.com/practice/62909494cecd4eab8c2501167e825566` |
| SQL80 | 每个部门薪资排名前两名员工 | 中等 | `03_排序窗口函数` | `https://www.nowcoder.com/practice/89329eadd4a64126b1cd326ea0b7eff7` |
| SQL100 | 各类别销售额前三且利润率达标商品 | 中等 | `03_排序窗口函数` | `https://www.nowcoder.com/practice/3d70132f4c14442cada25fec0198e743` |
| SQL117 | 产品年度销售额与竞品年度对比 | 中等 | `02_lead_lag_first_last` | `https://www.nowcoder.com/practice/99cc7f1798a84645a6aca5bdfd163fdb` |
| SQL129 | 近 7 天骑手履约时效看板 | 中等 | `04_累计汇总` | `https://www.nowcoder.com/practice/25af5a3296c747f5b01fc589f1568514` |
| SQL140 | 找出补位班次 | 较难 | `09_合并区间` | `https://www.nowcoder.com/practice/ed828b0385a84e0db95f1513f43076d4` |
| SQL146 | 潮鞋新品发售后 N 日复购留存矩阵 | 中等 | `07_留存计算` | `https://www.nowcoder.com/practice/1a4a359d3a524cc0830c52985888bd38` |
| SQL150 | 连续进步潜水员评选 | 较难 | `01_连续登录` | `https://www.nowcoder.com/practice/05994083a6184554947aac96c568baaf` |
| SQL151 | 核心营位帕累托分析 | 较难 | `04_累计汇总` | `https://www.nowcoder.com/practice/77f924a37530406ca86455381b6d1a5a` |
| SQL153 | 漏斗 | 较难 | `07_留存计算` | `https://www.nowcoder.com/practice/f97762a1c1c44f5ab5e4b6d6a1f42066` |
| SQL158 | 反洗钱三跳资金链路追踪 | 困难 | `06_关联应用` | `https://www.nowcoder.com/practice/e5d1ebc285c14d7eb3980aa32b4b4cee` |
| SQL159 | 信用卡逾期滚动迁徙矩阵 | 困难 | `07_留存计算` | `https://www.nowcoder.com/practice/1e3a3dad8fb64a48924eb28d5abf2b86` |

- [ ] **Step 1: 核对现有题目的标题和查询目标**

Run:

```powershell
rg -n "^# |要求查询|查询目标|本题口径" -g "*.md" -g "!topic_summary.md" -g "!README.md" -g "!generation_check_report.md"
```

Expected: 输出已有单题标题与查询目标，用于识别 SQL40、SQL80 等候选题是否与已有题目实质重复。

- [ ] **Step 2: 完成 118 道题的难度和题型初筛**

从官方题单逐项记录题号、标题和难度。入门、简单题统一标记“难度过低”；中等及以上题目必须给出进入详情核验或排除的明确原因，确保筛选范围不是只看下表 15 道题。

- [ ] **Step 3: 逐题核验公开内容完整性**

对表中每个公开题目页确认五项内容：题目描述、字段结构、样例输入、样例输出、公开 MySQL 解法依据。任何一项因登录、会员或页面缺失而无法核验时，将该题标记为“公开内容不足”，不得创建单题文件。

- [ ] **Step 4: 完成语义去重与最终归类**

按“查询目标 + 关键口径 + 核心 SQL 技法”比较。SQL40 与 SQL80 虽都使用排名窗口，但业务粒度和并列规则不同，可以分别保留；与现有“最大连续登录天数”同口径的候选题必须跳过。

- [ ] **Step 5: 在检查报告记录筛选结果**

在 `generation_check_report.md` 中增加“牛客 SQL 大厂真题筛选”表，字段固定为：题号、难度、筛选结果、目标目录或跳过原因、来源链接。

- [ ] **Step 6: 提交来源审计**

```powershell
git add -- generation_check_report.md
git commit -m "docs: audit Nowcoder SQL candidates"
```

### Task 2: 生成排序窗口函数题目

**Files:**
- Create when source audit passes: `03_排序窗口函数/001_每月播放量前三歌曲.md`
- Create when source audit passes: `03_排序窗口函数/002_每个部门薪资前两名员工.md`
- Create when source audit passes: `03_排序窗口函数/003_各类别销售额前三商品.md`

- [ ] **Step 1: 生成 SQL40 六段式题目**

标准答案流程固定为：三个样例数据 CTE -> 年龄、年份和歌手过滤 -> 按月与歌曲聚合播放量 -> `row_number()` 按播放量降序、`song_id` 升序排名 -> 过滤前三名。并列次序必须遵守原题 `song_id` 规则。

- [ ] **Step 2: 生成 SQL80 六段式题目**

标准答案使用样例数据 CTE 和部门内薪资排名；根据原题对并列薪资的输出口径选择 `rank()` 或 `dense_rank()`，只保留排名前两名员工。

- [ ] **Step 3: 生成 SQL100 六段式题目**

标准答案先按商品聚合销售额和利润率，再过滤利润率超过 20% 的商品，最后在商品类别内按销售额排名并保留前三名；过滤和排名先后以原题公开答案为准。

- [ ] **Step 4: 检查三个文件结构**

Run:

```powershell
rg -n "^## [1-6]\." "03_排序窗口函数/00[1-3]_*.md"
```

Expected: 每个文件恰好输出六个章节标题。

- [ ] **Step 5: 提交排序窗口题目**

```powershell
git add -- 03_排序窗口函数
git commit -m "docs: add Nowcoder ranking SQL problems"
```

### Task 3: 生成前后行比较题目

**Files:**
- Create when source audit passes: `02_lead_lag_first_last/004_计算平均支付间隔.md`
- Create when source audit passes: `02_lead_lag_first_last/005_产品年度销售额同比.md`

- [ ] **Step 1: 生成 SQL62 六段式题目**

标准答案按用户和支付时间排序，使用 `lag()` 取得上一次支付时间，再使用 Hive `unix_timestamp()` 计算间隔并按原题口径求平均值；首笔支付记录不得进入间隔均值。

- [ ] **Step 2: 生成 SQL117 六段式题目**

标准答案先聚合产品年度销售额，再使用 `lag()` 取得上一年度销售额，按原题要求计算同比或竞品对比指标；年份排序和空值处理必须来自公开口径。

- [ ] **Step 3: 静态检查 MySQL 时间函数残留**

Run:

```powershell
rg -n -i "timestampdiff|interval [0-9]+|date_add\([^,]+,\s*interval" "02_lead_lag_first_last/004_计算平均支付间隔.md" "02_lead_lag_first_last/005_产品年度销售额同比.md"
```

Expected: 无匹配。

- [ ] **Step 4: 提交前后行题目**

```powershell
git add -- 02_lead_lag_first_last
git commit -m "docs: add Nowcoder lead lag SQL problems"
```

### Task 4: 生成累计与滚动窗口题目

**Files:**
- Create when source audit passes: `04_累计汇总/006_商品销售总额分布.md`
- Create when source audit passes: `04_累计汇总/007_近7天骑手履约看板.md`
- Create when source audit passes: `04_累计汇总/008_核心营位帕累托分析.md`

- [ ] **Step 1: 生成 SQL78 六段式题目**

根据公开题意先聚合商品销售总额，再完成原题要求的分布分组或累计占比计算；若原题只是普通分组统计而不涉及累计窗口，则在来源审计阶段将其移出本目录或跳过。

- [ ] **Step 2: 生成 SQL129 六段式题目**

标准答案以自然日为窗口口径，先聚合每日骑手指标，再使用日期范围自连接或 Hive 可表达的日期窗口计算近 7 天指标；不得把“前 6 行”误写成“前 6 天”。

- [ ] **Step 3: 生成 SQL151 六段式题目**

标准答案先按营位汇总旺季贡献，按贡献降序计算累计贡献与总贡献，得到累计占比并按原题阈值识别核心营位；累计窗口显式写 `rows between unbounded preceding and current row`。

- [ ] **Step 4: 检查累计窗口边界**

Run:

```powershell
rg -n "rows between|datediff|date_sub|date_add" "04_累计汇总/006_商品销售总额分布.md" "04_累计汇总/007_近7天骑手履约看板.md" "04_累计汇总/008_核心营位帕累托分析.md"
```

Expected: 累计题显式出现窗口边界，7 天题明确出现日期范围逻辑。

- [ ] **Step 5: 提交累计汇总题目**

```powershell
git add -- 04_累计汇总
git commit -m "docs: add Nowcoder cumulative SQL problems"
```

### Task 5: 生成关联与递归链路题目

**Files:**
- Create when source audit passes: `06_关联应用/004_网易云音乐推荐.md`
- Create when source audit passes: `06_关联应用/005_三跳资金链路追踪.md`

- [ ] **Step 1: 生成 SQL63 六段式题目**

标准答案按公开题意构造用户收藏、好友关系和歌曲信息 CTE，使用连接及反连接排除用户已听或已收藏内容；去重粒度必须与原题输出一致。

- [ ] **Step 2: 生成 SQL158 六段式题目**

标准答案使用三层显式自连接追踪固定三跳资金链路，并在每一跳保留原题要求的时间、金额、账户和风险条件；Hive 标准答案不使用未确认可用的递归 CTE。

- [ ] **Step 3: 检查连接过滤条件**

Run:

```powershell
rg -n -i "join|left join|not exists|is null" "06_关联应用/004_网易云音乐推荐.md" "06_关联应用/005_三跳资金链路追踪.md"
```

Expected: 推荐题包含排除已存在记录的逻辑，资金链路题包含三跳连接逻辑。

- [ ] **Step 4: 提交关联应用题目**

```powershell
git add -- 06_关联应用
git commit -m "docs: add Nowcoder join SQL problems"
```

### Task 6: 生成留存、漏斗与迁徙题目

**Files:**
- Create when source audit passes: `07_留存计算/002_新品N日复购留存矩阵.md`
- Create when source audit passes: `07_留存计算/003_业务漏斗转化分析.md`
- Create when source audit passes: `07_留存计算/004_信用卡逾期滚动迁徙矩阵.md`

- [ ] **Step 1: 生成 SQL146 六段式题目**

标准答案先确定新品首购用户及首购日，再关联后续复购行为，按原题 N 日区间和用户分层计算留存矩阵；分母必须固定为对应首购 cohort。

- [ ] **Step 2: 生成 SQL153 六段式题目**

标准答案按原题事件顺序识别漏斗各阶段，明确每阶段用户集合和转化分母；不得使用会提前过滤未转化用户的内连接口径。

- [ ] **Step 3: 生成 SQL159 六段式题目**

标准答案按月份和账户排序，使用前后期逾期状态构造迁徙方向，再按滚动窗口和原题分母统计迁徙矩阵；首期无前态记录按公开口径处理。

- [ ] **Step 4: 检查分母与日期条件**

Run:

```powershell
rg -n "分母|首购|cohort|lag\(|datediff|迁徙" "07_留存计算/00[2-4]_*.md"
```

Expected: 三道题的题目口径或标准答案明确分母、时间关联和状态来源。

- [ ] **Step 5: 提交留存题目**

```powershell
git add -- 07_留存计算
git commit -m "docs: add Nowcoder retention SQL problems"
```

### Task 7: 生成连续状态与区间题目

**Files:**
- Create when source audit passes: `01_连续登录/008_连续进步潜水员评选.md`
- Create when source audit passes: `09_合并区间/002_找出补位班次.md`

- [ ] **Step 1: 生成 SQL150 六段式题目**

标准答案按潜水员和日期排序，使用 `lag()` 判断相邻成绩是否满足“连续进步”，对断点累计分组后统计连续段；连续日期是否为必要条件必须遵循公开题目口径。

- [ ] **Step 2: 生成 SQL140 六段式题目**

标准答案按公开题意识别班次空档与可补位区间，明确端点是否相接、区间是否允许重叠以及补位优先级，再使用 `lag()`、`lead()` 或区间关联完成匹配。

- [ ] **Step 3: 检查连续与区间口径**

Run:

```powershell
rg -n "本题口径|连续日期|端点|重叠|lag\(|lead\(" "01_连续登录/008_连续进步潜水员评选.md" "09_合并区间/002_找出补位班次.md"
```

Expected: 两道题均明确断点或区间边界规则。

- [ ] **Step 4: 提交连续和区间题目**

```powershell
git add -- 01_连续登录 09_合并区间
git commit -m "docs: add Nowcoder sequence and interval SQL problems"
```

### Task 8: 更新题型总结和项目索引

**Files:**
- Modify: `01_连续登录/topic_summary.md`
- Modify: `02_lead_lag_first_last/topic_summary.md`
- Modify: `03_排序窗口函数/topic_summary.md`
- Modify: `04_累计汇总/topic_summary.md`
- Modify: `06_关联应用/topic_summary.md`
- Modify: `07_留存计算/topic_summary.md`
- Modify: `09_合并区间/topic_summary.md`
- Modify: `README.md`
- Modify: `generation_check_report.md`

- [ ] **Step 1: 更新对应题型清单**

每个 `topic_summary.md` 仅加入实际创建成功的题目，记录题目名称、核心考点以及“是否有我的解答 = 否”。不为跳过题目预留编号。

- [ ] **Step 2: 重新计算 README 题目数量**

Run:

```powershell
Get-ChildItem -Directory | Where-Object Name -Match '^\d{2}_' | ForEach-Object { [pscustomobject]@{ Directory=$_.Name; Count=(Get-ChildItem -LiteralPath $_.FullName -Filter '*.md' | Where-Object Name -NE 'topic_summary.md').Count } }
```

Expected: 得到 10 个目录的真实单题数量；用结果替换 README 中已过期的计数，并增加 2026-07-19 更新记录。

- [ ] **Step 3: 完成 generation_check_report**

报告列出实际新增文件、跳过题目及原因、六段结构检查、缺少用户解答清单和 Hive 静态检查结果。

- [ ] **Step 4: 提交索引更新**

```powershell
git add -- README.md generation_check_report.md 01_连续登录/topic_summary.md 02_lead_lag_first_last/topic_summary.md 03_排序窗口函数/topic_summary.md 04_累计汇总/topic_summary.md 06_关联应用/topic_summary.md 07_留存计算/topic_summary.md 09_合并区间/topic_summary.md
git commit -m "docs: update SQL topic indexes"
```

### Task 9: 全量验证

**Files:**
- Verify: all newly created single-question Markdown files
- Verify: `README.md`
- Verify: `generation_check_report.md`

- [ ] **Step 1: 检查六段结构**

Run:

```powershell
$files = git diff HEAD~8 --name-only --diff-filter=A -- '*.md' | Where-Object { $_ -match '^\d{2}_' -and $_ -notmatch 'topic_summary\.md$' }; foreach ($file in $files) { $sections = (Select-String -LiteralPath $file -Pattern '^## [1-6]\.').Count; "$file`t$sections" }
```

Expected: 每个新增单题文件的章节数均为 `6`。

- [ ] **Step 2: 检查缺省个人内容**

Run:

```powershell
rg -L "本题暂未提供我的解答。" $files
rg -L "本题暂未补充个人复盘要点，后续复盘时更新。" $files
```

Expected: 两条命令均无输出。

- [ ] **Step 3: 检查来源与难度**

Run:

```powershell
rg -L "牛客题号.*SQL|难度.*(中等|较难|困难)|https://www\.nowcoder\.com/practice/" $files
```

Expected: 无输出。

- [ ] **Step 4: 检查 MySQL 专有语法残留**

Run:

```powershell
rg -n -i "timestampdiff|date_format\(|str_to_date|interval [0-9]+ (day|month|year)|ifnull\(" $files
```

Expected: 无未解释的 MySQL 专有语法；题目原文或复盘中提到的函数不计入标准答案残留。

- [ ] **Step 5: 检查格式与工作区状态**

Run:

```powershell
git diff --check
git status --short
```

Expected: `git diff --check` 无输出；工作区只包含本计划产生且尚未提交的预期文件，或在最后一次提交后保持干净。
