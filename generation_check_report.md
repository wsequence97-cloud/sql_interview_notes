# SQL 题库生成检查报告

## 1. 本次处理范围

本次按 `SQL题目生成格式规范.md`，将当前已有单题 Markdown 文件统一改造成新版 6 段格式。

已处理题目文件：

| 文件 | 处理结果 |
|---|---|
| `01_连续登录/001_查询连续登陆3天以上的用户.md` | 已改为新版 6 段格式 |
| `01_连续登录/002_查询每个用户最大连续登录天数.md` | 已改为新版 6 段格式 |
| `01_连续登录/003_日期连续区间合并.md` | 已改为新版 6 段格式 |
| `01_连续登录/004_查询每个选手最长连胜数.md` | 已改为新版 6 段格式 |
| `01_连续登录/005_查询每个用户可间隔一天的最大连续登录天数.md` | 新增题目，已使用新版 6 段格式 |
| `01_连续登录/006_找出UV增长率连续超过30%的日期.md` | 新增题目，已使用新版 6 段格式 |
| `01_连续登录/007_日期有断区间合并.md` | 新增题目，已使用新版 6 段格式 |
| `02_lead_lag_first_last/001_查询股票波峰波谷.md` | 新增题目，已使用新版 6 段格式 |
| `02_lead_lag_first_last/002_查询前后开市日期.md` | 新增题目，已使用新版 6 段格式 |
| `02_lead_lag_first_last/003_按状态连续段累计计数.md` | 新增题目，已使用新版 6 段格式 |
| `04_累计汇总/001_统计每个用户累计访问次数.md` | 新增题目，已使用新版 6 段格式 |
| `04_累计汇总/002_统计直播间最大同时在线人数.md` | 新增题目，已使用新版 6 段格式 |
| `04_累计汇总/003_统计每小时同时在线人数.md` | 新增题目，已使用新版 6 段格式 |
| `04_累计汇总/004_求最小达到累计金额日期.md` | 新增题目，已使用新版 6 段格式 |
| `04_累计汇总/005_查询历史新低的商品ID.md` | 新增题目，已使用新版 6 段格式 |
| `05_炸裂函数/001_按学生恢复班级和分数列表.md` | 新增题目，已使用新版 6 段格式 |

## 2. 新版固定结构检查

每道题均只保留以下 6 个部分：

1. 题目描述
2. 期望结果
3. 标准答案
4. 我的解答
5. 我的解答正确版本
6. 我的复盘要点

| 文件 | 题目描述 | 期望结果 | 标准答案 | 我的解答 | 我的解答正确版本 | 我的复盘要点 |
|---|---|---|---|---|---|---|
| `001_查询连续登陆3天以上的用户.md` | 通过 | 通过 | 通过 | 通过 | 通过 | 通过 |
| `002_查询每个用户最大连续登录天数.md` | 通过 | 通过 | 通过 | 通过 | 通过 | 通过 |
| `003_日期连续区间合并.md` | 通过 | 通过 | 通过 | 通过 | 通过 | 通过 |
| `004_查询每个选手最长连胜数.md` | 通过 | 通过 | 通过 | 通过 | 通过 | 通过 |
| `005_查询每个用户可间隔一天的最大连续登录天数.md` | 通过 | 通过 | 通过 | 通过 | 通过 | 通过 |
| `006_找出UV增长率连续超过30%的日期.md` | 通过 | 通过 | 通过 | 通过 | 通过 | 通过 |
| `007_日期有断区间合并.md` | 通过 | 通过 | 通过 | 通过 | 通过 | 通过 |
| `001_查询股票波峰波谷.md` | 通过 | 通过 | 通过 | 通过 | 通过 | 通过 |
| `002_查询前后开市日期.md` | 通过 | 通过 | 通过 | 通过 | 通过 | 通过 |
| `003_按状态连续段累计计数.md` | 通过 | 通过 | 通过 | 通过 | 通过 | 通过 |
| `001_统计每个用户累计访问次数.md` | 通过 | 通过 | 通过 | 通过 | 通过 | 通过 |
| `002_统计直播间最大同时在线人数.md` | 通过 | 通过 | 通过 | 通过 | 通过 | 通过 |
| `003_统计每小时同时在线人数.md` | 通过 | 通过 | 通过 | 通过 | 通过 | 通过 |
| `004_求最小达到累计金额日期.md` | 通过 | 通过 | 通过 | 通过 | 通过 | 通过 |
| `005_查询历史新低的商品ID.md` | 通过 | 通过 | 通过 | 通过 | 通过 | 通过 |
| `001_按学生恢复班级和分数列表.md` | 通过 | 通过 | 通过 | 通过 | 通过 | 通过 |

## 3. 删除旧版多余内容

单题文件中已删除旧版冗余章节，包括：

- 题目信息
- 输入表结构
- 标准答案拆解
- 我的解答分析
- 易错点与注意事项
- 面试口述版
- 关联题型与模板

## 4. 我的解答保留情况

| 文件 | 保留情况 |
|---|---|
| `001_查询连续登陆3天以上的用户.md` | 已保留原始 SQL，并补充修正版本 |
| `002_查询每个用户最大连续登录天数.md` | 已保留原始 SQL，并补充修正版本 |
| `003_日期连续区间合并.md` | 原题未提供我的解答，已按规范写明 |
| `004_查询每个选手最长连胜数.md` | 已保留原始 SQL，并补充修正版本 |
| `005_查询每个用户可间隔一天的最大连续登录天数.md` | 已保留用户提供的原始 SQL，并补充修正版本 |
| `006_找出UV增长率连续超过30%的日期.md` | 已保留用户提供的原始 SQL，并补充修正版本 |
| `007_日期有断区间合并.md` | 原题未提供我的解答，已按规范写明 |
| `02_lead_lag_first_last/001_查询股票波峰波谷.md` | 已保留用户提供的原始 SQL，并补充修正版本 |
| `02_lead_lag_first_last/002_查询前后开市日期.md` | 已保留用户提供的原始 SQL，并补充修正版本 |
| `02_lead_lag_first_last/003_按状态连续段累计计数.md` | 已保留用户提供的原始 SQL，并补充修正版本 |
| `04_累计汇总/001_统计每个用户累计访问次数.md` | 已保留用户提供的原始 SQL，并补充修正版本 |
| `04_累计汇总/002_统计直播间最大同时在线人数.md` | 原题未提供我的解答，已按规范写明 |
| `04_累计汇总/003_统计每小时同时在线人数.md` | 已保留用户提供的原始 SQL，并补充修正版本 |
| `04_累计汇总/004_求最小达到累计金额日期.md` | 已保留用户提供的原始 SQL，并补充修正版本 |
| `04_累计汇总/005_查询历史新低的商品ID.md` | 已保留用户提供的原始 SQL，并补充修正版本 |
| `05_炸裂函数/001_按学生恢复班级和分数列表.md` | 已保留用户提供的原始 SQL，并补充修正版本 |

## 5. SQL 方言检查

标准答案均保留为 Hive SQL CTE 完整版，包含：

- 样例数据 CTE
- 解题过程 CTE
- 最终查询 SQL

用户原始解答中的错误写法已原样保留在“我的解答”中，并在“我的解答正确版本”和“我的复盘要点”中给出修正口径。

## 6. 牛客 SQL 大厂真题筛选

- 来源范围：牛客 SQL 大厂真题官方题单的三个列表页
- 采集日期：2026-07-19

| 题号 | 题目 | 难度 | 初筛结果 | 目标目录或跳过原因 | 来源链接 |
|---|---|---|---|---|---|
| SQL40 | 23年蚂蚁-每个月Top3的周杰伦歌曲 | 较难 | 进入详情核验 | `03_排序窗口函数` | https://www.nowcoder.com/practice/4ab6d198ea8447fe9b6a1cad1f671503 |
| SQL41 | 23年蚂蚁-最长连续登录天数 | 困难 | 跳过 | 与现有题重复 | https://www.nowcoder.com/practice/cb8bc687046e4d32ad38de62c48ad79b |
| SQL42 | 23年蚂蚁-分析客户逾期情况 | 中等 | 跳过 | 普通聚合 | https://www.nowcoder.com/practice/22633632da344e2492973ecf555e10c9 |
| SQL43 | 23年蚂蚁-获取指定客户每月的消费额 | 中等 | 跳过 | 普通聚合 | https://www.nowcoder.com/practice/ed04f148b63e469e8f62e051d06a46f5 |
| SQL44 | 23年蚂蚁-查询连续入住多晚的客户信息？ | 中等 | 跳过 | 与现有题重复 | https://www.nowcoder.com/practice/5b4018c47dfd401d87a5afb5ebf35dfd |
| SQL45 | 23年蚂蚁-统计所有课程参加培训人次 | 中等 | 跳过 | 普通聚合 | https://www.nowcoder.com/practice/98aad5807cf34a3b960cc8a70ce03f53 |
| SQL46 | 23年蚂蚁-查询培训指定课程的员工信息 | 简单 | 跳过 | 难度过低 | https://www.nowcoder.com/practice/a0ef4574056e4a219ee7d651ba82efef |
| SQL47 | 23年蚂蚁-推荐内容准确的用户平均评分 | 中等 | 跳过 | 普通聚合 | https://www.nowcoder.com/practice/2dcac73b647247f0aef0b261ed76b47e |
| SQL48 | 23年携程-每个商品的销售总额 | 中等 | 跳过 | 普通聚合 | https://www.nowcoder.com/practice/6d796e885ee44a9cb599f47b16a02ea4 |
| SQL49 | 22年携程-统计各岗位员工平均工作时长 | 简单 | 跳过 | 难度过低 | https://www.nowcoder.com/practice/b7220791a95a4cd092801069aefa1cae |
| SQL50 | 22年携程-查询连续登陆的用户 | 较难 | 跳过 | 与现有题重复 | https://www.nowcoder.com/practice/9944210610ec417e94140ac09512a3f5 |
| SQL51 | 23年携程-统计商家不同会员每日访问人次及访问人数 | 简单 | 跳过 | 难度过低 | https://www.nowcoder.com/practice/0017dc22426b495889da3304dcf254d1 |
| SQL52 | 23年携程-统计各等级会员用户下订单总额 | 简单 | 跳过 | 难度过低 | https://www.nowcoder.com/practice/48dd35a3dd8c4e1494db36b097a03300 |
| SQL53 | 23年携程-查询下订单用户访问次数？ | 中等 | 跳过 | 普通聚合 | https://www.nowcoder.com/practice/32bc1e0fce2343ad934b76a025e09fc5 |
| SQL54 | 23年携程-统计用户从访问到下单的转化率 | 较难 | 跳过 | 普通聚合 | https://www.nowcoder.com/practice/eaff8684aed74e208300f2737edbb083 |
| SQL55 | 23年携程-统计员工薪资扣除比例 | 简单 | 跳过 | 难度过低 | https://www.nowcoder.com/practice/08db6f0135664ca598b579f8d53dc486 |
| SQL56 | 24年交银金科-统计用户获得积分 | 简单 | 跳过 | 难度过低 | https://www.nowcoder.com/practice/22ed0cd240824bb597b3130fef389cea |
| SQL57 | 22年携程-更新用户积分信息？ | 中等 | 跳过 | 核心题型不匹配 | https://www.nowcoder.com/practice/ef1f2fda4338460b948810f3f7e7a68e |
| SQL58 | 22年携程-查询单日多次下订单的用户信息？ | 简单 | 跳过 | 难度过低 | https://www.nowcoder.com/practice/9958aed1e74a49b795dfe2cb9d54ee12 |
| SQL59 | 22年携程-统计各个部门平均薪资 | 简单 | 跳过 | 难度过低 | https://www.nowcoder.com/practice/4722fdf89a4c43eebb58d61a19ccab31 |
| SQL60 | 22年携程-统计加班员工占比 | 中等 | 跳过 | 普通聚合 | https://www.nowcoder.com/practice/6c0a521c36e14c7599eaef858f6f8233 |
| SQL61 | 22年携程-每天登陆最早的用户的内容喜好 | 中等 | 跳过 | 核心题型不匹配 | https://www.nowcoder.com/practice/24bb13a28267486ba86c1d21459fa90a |
| SQL62 | 22年携程-支付间隔平均值 | 中等 | 进入详情核验 | `02_lead_lag_first_last` | https://www.nowcoder.com/practice/847431ad931e45348eb1ab5657144c28 |
| SQL63 | 22年网易-网易云音乐推荐 | 较难 | 进入详情核验 | `06_关联应用` | https://www.nowcoder.com/practice/048ed413ac0e4cf4a774b906fc87e0e7 |
| SQL64 | 22年网易-商品交易 | 简单 | 跳过 | 难度过低 | https://www.nowcoder.com/practice/f257dfc1b55e42e19eec004aa3cb4174 |
| SQL65 | 23年知乎-请写出计算粉丝ctr的sql语句 | 中等 | 跳过 | 普通聚合 | https://www.nowcoder.com/practice/853a6567cf524f63bab0879b8d0bfe62 |
| SQL66 | 23年掌阅-查询成绩 | 简单 | 跳过 | 难度过低 | https://www.nowcoder.com/practice/ef30689ae065434c89c129e9dfe1b4cd |
| SQL67 | 24年OPPO-被重复观看次数最多的3个视频 | 中等 | 跳过 | 与现有题重复 | https://www.nowcoder.com/practice/b75fa2412659422c96369976ee1f9504 |
| SQL68 | 24年OPPO-短视频直播间晚上11-12点之间各直播间的在线人数 | 中等 | 跳过 | 与现有题重复 | https://www.nowcoder.com/practice/38f5febc9dac4e9e84ed5891a3e4ca05 |
| SQL69 | 23年阿里-淘宝店铺的实际销售额与客单价 | 简单 | 跳过 | 难度过低 | https://www.nowcoder.com/practice/ce116419a1f141568094b5eab70e5ce8 |
| SQL70 | 23年阿里-完成员工考核试卷突出的非领导员工 | 较难 | 跳过 | 核心题型不匹配 | https://www.nowcoder.com/practice/422dcd6ae72c49c9bbec1aff90d69806 |
| SQL71 | 23年京东-查询产生理赔费用的快递信息 | 简单 | 跳过 | 难度过低 | https://www.nowcoder.com/practice/d22eab8a0001443fba7c5757e7cbcaea |
| SQL72 | 23年京东-统计快递运输时长 | 中等 | 跳过 | 普通聚合 | https://www.nowcoder.com/practice/bb4196936f15424dbabe76a501186d91 |
| SQL73 | 23年京东-统计快递从创建订单到发出间隔时长 | 简单 | 跳过 | 难度过低 | https://www.nowcoder.com/practice/be3e56c950724b27aa79b79309147443 |
| SQL74 | 23年京东-下单最多的商品 | 简单 | 跳过 | 难度过低 | https://www.nowcoder.com/practice/d7c93e3a3d5b4087896539121d32d367 |
| SQL75 | 23年京东-用户购买次数前三 | 简单 | 跳过 | 难度过低 | https://www.nowcoder.com/practice/e359c071d29c4fb7bac6d346f0cfe1d0 |
| SQL76 | 23年京东-商品价格排名 | 中等 | 跳过 | 与现有题重复 | https://www.nowcoder.com/practice/119f5b8cfe5b45779a3e1b3f4d83b341 |
| SQL77 | 23年京东-商品销售排名 | 简单 | 跳过 | 难度过低 | https://www.nowcoder.com/practice/79c6c3d6d66946f79387bca73c0a29f4 |
| SQL78 | 23年京东-商品销售总额分布 | 中等 | 进入详情核验 | `04_累计汇总` | https://www.nowcoder.com/practice/62909494cecd4eab8c2501167e825566 |
| SQL79 | 24年京东-每个客户的账户总金额 | 简单 | 跳过 | 难度过低 | https://www.nowcoder.com/practice/19f0bc2b8cad44b6986ad9a51ed43def |
| SQL80 | 24年京东-每个部门薪资排名前两名员工 | 中等 | 进入详情核验 | `03_排序窗口函数` | https://www.nowcoder.com/practice/89329eadd4a64126b1cd326ea0b7eff7 |
| SQL82 | 24年京东-查询订单 | 简单 | 跳过 | 难度过低 | https://www.nowcoder.com/practice/5ae7f48dc94f4a76b0ade40b70caf308 |
| SQL83 | 24年京东-商品id数据清洗统计 | 简单 | 跳过 | 难度过低 | https://www.nowcoder.com/practice/c985ecbd820b46e6bafa858f6600126d |
| SQL84 | 24年京东-每个顾客最近一次下单的订单信息 | 中等 | 跳过 | 与现有题重复 | https://www.nowcoder.com/practice/4762ea22b0eb42ceb4f0a972c56d24c4 |
| SQL85 | 24年阿里-统计每个产品的销售情况 | 困难 | 跳过 | 普通聚合 | https://www.nowcoder.com/practice/d431aa7bf72c4fd7b048ec639bc83ad2 |
| SQL86 | 24年京东-各个部门实际平均薪资和男女员工实际平均薪资 | 较难 | 跳过 | 普通聚合 | https://www.nowcoder.com/practice/e8272685d07347cc88667f31f7989231 |
| SQL87 | 24年京东-每个顾客购买的最新产品名称 | 中等 | 跳过 | 与现有题重复 | https://www.nowcoder.com/practice/6ff37adae90f490aafa313033a2dcff7 |
| SQL88 | 24年京东-输出播放量最高的视频 | 中等 | 跳过 | 与现有题重复 | https://www.nowcoder.com/practice/9e9cb264e1f64e28846975d5a32ba8e4 |
| SQL89 | 24年京东-返回顾客名称和相关订单号以及每个订单的总价 | 简单 | 跳过 | 难度过低 | https://www.nowcoder.com/practice/4dda66e385c443d8a11570a70807d250 |
| SQL90 | 24年京东-未下单用户统计 | 简单 | 跳过 | 难度过低 | https://www.nowcoder.com/practice/3433aee5c7824255b2dd2879b30df090 |
| SQL92 | 24年京东-用户订单信息查询 | 简单 | 跳过 | 难度过低 | https://www.nowcoder.com/practice/dccec8456d774169925c0d50843ea076 |
| SQL93 | 24年京东-未下单用户登陆渠道统计 | 简单 | 跳过 | 难度过低 | https://www.nowcoder.com/practice/5090553d7854458987997a5c91c30975 |
| SQL94 | 24年京东-更新员工信息表 | 中等 | 跳过 | 核心题型不匹配 | https://www.nowcoder.com/practice/1eb20d4bf7c5443da7b84105372c9070 |
| SQL95 | 24年京东-最受欢迎的top3课程 | 中等 | 跳过 | 与现有题重复 | https://www.nowcoder.com/practice/b9b33659559c46099aa3257da0374a48 |
| SQL96 | 24年京东-对商品的销售情况进行深度分析 | 中等 | 跳过 | 普通聚合 | https://www.nowcoder.com/practice/d6ced1b60af64a4998169ae717672e8e |
| SQL97 | 24年京东-电商平台需要对商家的销售业绩、退款情况和客户满意度进行综合评估 | 中等 | 跳过 | 普通聚合 | https://www.nowcoder.com/practice/48a236567617449eb6010274b30b29e8 |
| SQL98 | 24年京东-电商平台想要了解不同商品在不同月份的销售趋势 | 中等 | 跳过 | 普通聚合 | https://www.nowcoder.com/practice/a3fab87aca9347c28f406088cf601c7b |
| SQL99 | 24年京东-分析每个商品在不同时间段的销售情况 | 中等 | 跳过 | 普通聚合 | https://www.nowcoder.com/practice/eec7a93e1ab24233bd244e04e910d2f9 |
| SQL100 | 24年京东-查询出不同类别商品中，销售金额排名前三且利润率超过20%的商品信息 | 中等 | 进入详情核验 | `03_排序窗口函数` | https://www.nowcoder.com/practice/3d70132f4c14442cada25fec0198e743 |
| SQL101 | 24年京东-分析每个员工在不同项目中的绩效情况 | 中等 | 跳过 | 普通聚合 | https://www.nowcoder.com/practice/fa64fd2eb40d4639bc23dfb1ffae2163 |
| SQL102 | 24年京东-查询出每个品牌在特定时间段内的退货率以及平均客户满意度评分 | 中等 | 跳过 | 普通聚合 | https://www.nowcoder.com/practice/39f4ccb8ac1b47a89d092b4d8ed08bc8 |
| SQL103 | 24年京东-物流公司想要分析快递小哥的薪资构成和绩效情况 | 中等 | 跳过 | 普通聚合 | https://www.nowcoder.com/practice/4be55ba954bf4f928a2d6ff840f23d1b |
| SQL104 | 24年京东-查询出每个品牌在不同月份的总销售额以及购买该品牌商品的用户的平均年龄 | 中等 | 跳过 | 普通聚合 | https://www.nowcoder.com/practice/a50c67d3374f4d0e85869d3e48e02c0a |
| SQL105 | 24年京东-电商平台需要对各行业销售情况综合评估 | 中等 | 跳过 | 普通聚合 | https://www.nowcoder.com/practice/120cbc6f87214886bbba80d2b5414786 |
| SQL106 | 24年京东-电商平台想要查询出每个商品在2024年上半年的总销售额 | 中等 | 跳过 | 普通聚合 | https://www.nowcoder.com/practice/e190c019dabe4622ae719cca64437a47 |
| SQL107 | 24年京东-电商平台需要对商品的销售和评价情况进行综合分析 | 中等 | 跳过 | 普通聚合 | https://www.nowcoder.com/practice/ccb441966a0342f2ab5fa8e76c33a3e6 |
| SQL108 | 24年京东-评估2023年不同品牌商品的销售趋势和客户满意度 | 中等 | 跳过 | 普通聚合 | https://www.nowcoder.com/practice/a32c7ff803054a919e2b65334463002f |
| SQL109 | 24年京东-查询出每个运输方式在不同城市的平均运输时长以及总运输费用 | 中等 | 跳过 | 普通聚合 | https://www.nowcoder.com/practice/673bf7b17e7c4962bcde889980eec872 |
| SQL110 | 24年京东-分析员工在不同项目中的绩效表现以及所属部门的平均绩效情况 | 中等 | 跳过 | 普通聚合 | https://www.nowcoder.com/practice/20c76a1181004965a3106524fd3ab583 |
| SQL111 | 24年京东-物流公司想要分析快递小哥的收入情况 | 中等 | 跳过 | 普通聚合 | https://www.nowcoder.com/practice/749ba0168f014c639b516258c0ed6c5d |
| SQL112 | 24年京东-分析不同门店各类商品的库存情况和销售情况 | 中等 | 跳过 | 普通聚合 | https://www.nowcoder.com/practice/5b9262a36724466ea1ae1f58187197d6 |
| SQL113 | 24年京东-评估不同供应商提供的零部件质量和成本情况 | 中等 | 跳过 | 普通聚合 | https://www.nowcoder.com/practice/dc44fdd330e8429db8271efc38ce1922 |
| SQL114 | 24年京东-了解2023年全年所有商品的盈利情况 | 中等 | 跳过 | 普通聚合 | https://www.nowcoder.com/practice/05cbbb8662c14b46a15cbcb8993d9277 |
| SQL115 | 24年京东-哪些产品在特定时间段内表现最为出色 | 中等 | 跳过 | 普通聚合 | https://www.nowcoder.com/practice/866a4614615b43a29750537ede4bf0c8 |
| SQL116 | 24年饿了么-分析配送员的配送效率 | 中等 | 跳过 | 普通聚合 | https://www.nowcoder.com/practice/e27ba25e7722478eb86c832fab96fc1a |
| SQL117 | 24年OPPO-深入分析各款产品年总销售额与竞品的年度对比 | 中等 | 进入详情核验 | `02_lead_lag_first_last` | https://www.nowcoder.com/practice/99cc7f1798a84645a6aca5bdfd163fdb |
| SQL118 | 24年OPPO-分析各产品线在特定时间段内的销售情况 | 中等 | 跳过 | 普通聚合 | https://www.nowcoder.com/practice/8a002dd7888b4247b6ac9228577bdbc3 |
| SQL119 | 25年携程-查询高价值旅行套餐客户的支出与套餐详情 | 中等 | 跳过 | 核心题型不匹配 | https://www.nowcoder.com/practice/957e8ab30e2745b48d2f79046df73a23 |
| SQL120 | 24年蚂蚁-贷款情况 | 较难 | 跳过 | 核心题型不匹配 | https://www.nowcoder.com/practice/2817d353f0634208bcf0de74f56ca8f0 |
| SQL121 | 24年美团-统计借阅量 | 困难 | 跳过 | 普通聚合 | https://www.nowcoder.com/practice/280ed56ab3ee49a4b2a4595d38e1d565 |
| SQL122 | 24年美团-统计骑手信息 | 较难 | 跳过 | 核心题型不匹配 | https://www.nowcoder.com/practice/704de2445ed943c6bf65cfd77bd69ff4 |
| SQL123 | 24年小红书-内容社区用户活跃度、转化与广告归因分析 | 较难 | 跳过 | 核心题型不匹配 | https://www.nowcoder.com/practice/e491704f99ed4affb1d42127bf16a4a9 |
| SQL124 | 24年阿里-下单复盘 | 较难 | 跳过 | 核心题型不匹配 | https://www.nowcoder.com/practice/85cece6c8e11434783e9e18da2bddd45 |
| SQL125 | 24年阿里-医院门诊复诊率与抗生素用药占比统计 | 较难 | 跳过 | 普通聚合 | https://www.nowcoder.com/practice/7adcef0b1fb741fbba255870422cdb43 |
| SQL126 | 24年阿里-最畅销的SKU | 较难 | 跳过 | 与现有题重复 | https://www.nowcoder.com/practice/356a64a402864b27a9ab47d0c032756d |
| SQL127 | 24年腾讯-统计每个班级的关键指标 | 较难 | 跳过 | 普通聚合 | https://www.nowcoder.com/practice/07beee54ac62455586016ea1b018d371 |
| SQL128 | 24年字节-统计创作者 | 中等 | 跳过 | 核心题型不匹配 | https://www.nowcoder.com/practice/5f0155102879494c8707f749156f9af3 |
| SQL129 | 24年美团-近7天骑手履约时效看板 | 中等 | 进入详情核验 | `04_累计汇总` | https://www.nowcoder.com/practice/25af5a3296c747f5b01fc589f1568514 |
| SQL130 | 24年字节-目标月份的品类销售简报 | 较难 | 跳过 | 普通聚合 | https://www.nowcoder.com/practice/d5693e529a514ed390f097d395ad481d |
| SQL131 | 25年字节-智能家居设备高能耗异常监控分析 | 中等 | 跳过 | 核心题型不匹配 | https://www.nowcoder.com/practice/d66ad4fcf3d54852832099d1674fe1c3 |
| SQL132 | 25年字节-在线教育平台活跃学员课程评价分析 | 中等 | 跳过 | 普通聚合 | https://www.nowcoder.com/practice/fc255da3eb464571a757980951ff4e79 |
| SQL133 | 25年字节-SaaS平台企业客户新功能采纳度分析 | 中等 | 跳过 | 普通聚合 | https://www.nowcoder.com/practice/7b4b67320dde405c8ffdea850467a92d |
| SQL134 | 25年字节-游戏平台新玩家消费与进阶行为分析 | 中等 | 跳过 | 核心题型不匹配 | https://www.nowcoder.com/practice/dff4543dbf684133b971bb570ce42660 |
| SQL135 | 25年字节-SaaS产品高价值用户活跃度分析 | 中等 | 跳过 | 普通聚合 | https://www.nowcoder.com/practice/439f6de3254143e7b3673ed0259d98b0 |
| SQL136 | 26年小红书-微服务架构下的深层依赖链路漏洞影响面分析 | 中等 | 跳过 | 核心题型不匹配 | https://www.nowcoder.com/practice/a8416ddac26b427c97d8a8c6a7d14779 |
| SQL137 | 26年字节-宠物猫繁育族谱追溯与遗传病风险评估 | 中等 | 跳过 | 核心题型不匹配 | https://www.nowcoder.com/practice/b81457c7327e4a17960804f3ef1a4fd3 |
| SQL138 | 26年阿里-全民健身季推荐网络与积分衰减计算 | 中等 | 跳过 | 核心题型不匹配 | https://www.nowcoder.com/practice/520e2c69f75247bbb05b36fc11d1df67 |
| SQL139 | 26年字节-播客精彩片段裂变传播链统计 | 较难 | 跳过 | 核心题型不匹配 | https://www.nowcoder.com/practice/c67a5e17dd474032aa5eac5dcffca317 |
| SQL140 | 26年携程-找出补位班次 | 较难 | 进入详情核验 | `09_合并区间` | https://www.nowcoder.com/practice/ed828b0385a84e0db95f1513f43076d4 |
| SQL141 | 26年阿里-超充站故障派单链路统计 | 较难 | 跳过 | 核心题型不匹配 | https://www.nowcoder.com/practice/0995ab4acb05404591cfab71df3d11e4 |
| SQL142 | 26年京东-电竞赛事战队近期战绩查询 | 简单 | 跳过 | 难度过低 | https://www.nowcoder.com/practice/7dda27e223a94184a3269ed99ac42fbe |
| SQL143 | 26年字节-骑行运动社区路线个人最佳排名 | 中等 | 跳过 | 与现有题重复 | https://www.nowcoder.com/practice/9a7bde8872dd41268e0c69b2d5cd4c42 |
| SQL144 | 26年阿里-SaaS产品租户核心功能模块用量及占比分析 | 中等 | 跳过 | 普通聚合 | https://www.nowcoder.com/practice/baeb3d368c3b467b8d8dd7f68c39bef4 |
| SQL145 | 26年字节-精品咖啡连锁门店王牌产品及其最忠实顾客分析 | 较难 | 跳过 | 核心题型不匹配 | https://www.nowcoder.com/practice/618a45ec484e45d6a18135586e272152 |
| SQL146 | 25年得物-潮鞋新品发售后N日复购留存矩阵 | 中等 | 进入详情核验 | `07_留存计算` | https://www.nowcoder.com/practice/1a4a359d3a524cc0830c52985888bd38 |
| SQL147 | 25年美团-骑手配送履约分层留存与时段热力矩阵 | 较难 | 跳过 | 与现有题重复 | https://www.nowcoder.com/practice/aca3e6f51a264f5db6a2f876b5f75ef0 |
| SQL148 | 25年网易云音乐-歌手新歌首发后听众分层次日留存与时段活跃矩阵 | 较难 | 跳过 | 与现有题重复 | https://www.nowcoder.com/practice/084ae898ce9a4bc9866700cc9b4616e5 |
| SQL149 | 25年美团-剧本杀门店主题局年度复盘 | 较难 | 跳过 | 核心题型不匹配 | https://www.nowcoder.com/practice/dacd24d66e11464699a4ad4160098241 |
| SQL150 | 25年携程-海岛潜水基地连续进步潜水员评选 | 较难 | 进入详情核验 | `01_连续登录` | https://www.nowcoder.com/practice/05994083a6184554947aac96c568baaf |
| SQL151 | 25年携程-露营地旺季核心营位帕累托分析 | 较难 | 进入详情核验 | `04_累计汇总` | https://www.nowcoder.com/practice/77f924a37530406ca86455381b6d1a5a |
| SQL152 | 25年京东-山地车锦标赛 | 较难 | 跳过 | 核心题型不匹配 | https://www.nowcoder.com/practice/a54df84e7a8a4615b5103b65b7ee5c3b |
| SQL153 | 25年京东-漏斗 | 较难 | 进入详情核验 | `07_留存计算` | https://www.nowcoder.com/practice/f97762a1c1c44f5ab5e4b6d6a1f42066 |
| SQL154 | 26年牛客-Tracker团队活动贡献分拆 | 困难 | 跳过 | 核心题型不匹配 | https://www.nowcoder.com/practice/c26de322cef647ea9304e8ed007e7347 |
| SQL155 | 26年牛客-Tracker技能树卡点诊断 | 困难 | 跳过 | 核心题型不匹配 | https://www.nowcoder.com/practice/8573af8d415e4032ad1f505d477b88e7 |
| SQL156 | 26年牛客-AI Coding活动全链路转化分析 | 困难 | 跳过 | 与现有题重复 | https://www.nowcoder.com/practice/1a698f70475945688ab50619487991d1 |
| SQL157 | 26年牛客-AI Coding模型误导事件识别 | 困难 | 跳过 | 核心题型不匹配 | https://www.nowcoder.com/practice/1df52fcf2e7045c4bf3bd23f86253c60 |
| SQL158 | 26年某银行-反洗钱三跳资金链路追踪 | 困难 | 进入详情核验 | `06_关联应用` | https://www.nowcoder.com/practice/e5d1ebc285c14d7eb3980aa32b4b4cee |
| SQL159 | 26年某银行-信用卡逾期滚动迁徙矩阵 | 困难 | 进入详情核验 | `07_留存计算` | https://www.nowcoder.com/practice/1e3a3dad8fb64a48924eb28d5abf2b86 |

筛选汇总：共 118 道；进入详情核验 15 道；跳过 103 道。
