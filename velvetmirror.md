# WebLink Collective Archive

WebLink Collective Archive 是一个面向技术研究者、信息分析人员和数据归档工作者的结构化外链资源汇总系统。该项目专注于对分散于互联网各处的新闻资讯类外部链接进行统一收集、分类存储与元数据标注，解决个人收藏夹式管理带来的检索困难、失效链接无法追踪以及缺乏上下文描述等核心问题。系统以轻量级 Markdown 文档作为数据载体，配合自动化校验脚本，为中小规模的信息整理团队提供一套可离线运行、可版本控制的链接管理基线方案。

## 功能概览

**批量链接导入与去重**：支持从纯文本列表或 CSV 文件批量导入 URL，系统自动识别重复条目并生成导入报告。

**结构化元数据标注**：每条链接可附加来源域名、抓取时间、内容摘要、所属专题分类与重要等级标签。

**失效链接周期性探测**：内置基于 HTTP 状态码的链接存活检测模块，支持每日定时任务与手动触发两种模式。

**多维度筛选与导出**：按域名、标签、存活状态、导入批次等条件组合筛选，结果可导出为 JSON、CSV 或纯 URL 列表。

**版本变更追踪**：每次增删改操作均记录操作日志，支持回溯任意时间点的链接集合状态。

**自动化报告生成**：每周生成链接健康度报告，包含存活率、响应时间分布、高频失效域名统计。

**本地离线全文检索**：基于 SQLite FTS5 扩展构建的轻量级全文检索引擎，支持对摘要和备注字段的快速关键词匹配。

## 应用场景

**技术博客与资讯的长期归档**：技术团队可将日常阅读中积累的行业分析、漏洞公告、版本发布等外部链接统一纳入系统，避免重要参考资料因原网页下线而永久丢失。

**舆情素材的快速整理**：市场调研或媒体监测人员需要将来自不同信源的新闻报道链接归类整理，配合标签与摘要功能构建可检索的事件素材库。

**开源项目依赖文档溯源**：开源项目维护者可将项目所引用的设计文档、协议规范、第三方库主页等外链集中管理，当上游链接变动时能够第一时间感知并更新项目文档。

**学术论文参考链接管理**：研究人员在文献调研阶段产生的大量预印本、数据集、工具仓库链接可通过该系统统一标注状态（已读、待读、已引用），提升文献管理效率。

## 快速开始

以下命令演示了从克隆仓库到启动本地服务的完整流程。

```bash
git clone https://github.com/weblink-collective/archive.git
cd archive
pip install -r requirements.txt
python scripts/init_db.py
python scripts/import_urls.py --input data/seed_urls.txt --batch 45
python app.py --port 8080
```

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|---|---|---|
| Python | 3.9 或更高 | 核心运行环境，用于 CLI 工具与 Web 服务 |
| SQLite | 3.35.0 或更高 | 内置数据库引擎，需支持 FTS5 扩展 |
| requests | 2.28.0 或更高 | 用于链接存活探测与 HTTP 请求处理 |
| markdown | 3.4.0 或更高 | 用于解析和渲染项目内 Markdown 文档 |
| pytest | 7.2.0 或更高 | 单元测试与集成测试框架（开发依赖） |
| flask | 2.2.0 或更高 | Web 可视化界面服务框架（可选） |
| cron | 系统级 | 用于定时任务调度（生产环境推荐） |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|---|---|---|
| 用户手册 | docs/user-guide.md | 如何导入链接、打标签、导出数据、配置探测策略 |
| 运维手册 | docs/operations.md | 如何部署服务、配置定时任务、迁移数据库、备份恢复 |
| 开发者指南 | docs/developer.md | 如何扩展导入器、自定义筛选器、编写新的报告模块 |
| API 参考 | docs/api-reference.md | 各 Python 模块的函数签名、参数说明与返回值结构 |
| 变更日志 | CHANGELOG.md | 每个版本的新增功能、修复缺陷与破坏性变更列表 |
| 行为准则 | CODE_OF_CONDUCT.md | 贡献者之间的沟通规范与冲突处理原则 |

## 资源列表

- http://m.wap.uliejh.cn/bnews/224412.htm
- http://m.wap.uliejh.cn/bnews/37987.htm
- http://m.wap.uliejh.cn/bnews/33914.htm
- http://m.wap.uliejh.cn/bnews/148842.htm
- http://m.wap.uliejh.cn/bnews/568465.htm
- http://m.wap.uliejh.cn/bnews/7359.htm
- http://m.wap.uliejh.cn/bnews/677291.htm
- http://m.wap.uliejh.cn/bnews/3959.htm
- http://m.wap.uliejh.cn/bnews/6003333.htm
- http://m.wap.uliejh.cn/bnews/77267.htm
- http://m.wap.uliejh.cn/bnews/44268.htm
- http://m.wap.uliejh.cn/bnews/411261.htm
- http://m.wap.uliejh.cn/bnews/3104199.htm
- http://m.wap.uliejh.cn/bnews/049926.htm
- http://m.wap.uliejh.cn/bnews/26735.htm
- http://m.wap.uliejh.cn/bnews/38232.htm
- http://m.wap.uliejh.cn/bnews/009571.htm
- http://m.wap.uliejh.cn/bnews/5851.htm
- http://m.wap.uliejh.cn/bnews/528484.htm
- http://m.wap.uliejh.cn/bnews/95868.htm
- http://m.wap.uliejh.cn/bnews/3314.htm
- http://m.wap.uliejh.cn/bnews/0348.htm
- http://m.wap.uliejh.cn/bnews/3955.htm
- http://m.wap.uliejh.cn/bnews/21491.htm
- http://m.wap.uliejh.cn/bnews/993428.htm
- http://m.wap.uliejh.cn/bnews/12173.htm
- http://m.wap.uliejh.cn/bnews/2073862.htm
- http://m.wap.uliejh.cn/bnews/53441.htm
- http://m.wap.uliejh.cn/bnews/3791344.htm
- http://m.wap.uliejh.cn/bnews/5800296.htm
- http://m.wap.uliejh.cn/bnews/48369.htm
- http://m.wap.uliejh.cn/bnews/964032.htm
- http://m.wap.uliejh.cn/bnews/0516817.htm
- http://m.wap.uliejh.cn/bnews/8377060.htm
- http://m.wap.uliejh.cn/bnews/1729737.htm
- http://m.wap.uliejh.cn/bnews/462746.htm
- http://m.wap.uliejh.cn/bnews/3578.htm
- http://m.wap.uliejh.cn/bnews/987023.htm
- http://m.wap.uliejh.cn/bnews/81414.htm
- http://m.wap.uliejh.cn/bnews/905612.htm
- http://m.wap.uliejh.cn/bnews/44427.htm
- http://m.wap.uliejh.cn/bnews/7906139.htm
- http://m.wap.uliejh.cn/bnews/510319.htm
- http://m.wap.uliejh.cn/bnews/9850.htm
- http://m.wap.uliejh.cn/bnews/1836.htm
- http://m.wap.uliejh.cn/bnews/90909.htm
- http://m.wap.uliejh.cn/bnews/6057.htm
- http://m.wap.uliejh.cn/bnews/9281.htm
- http://m.wap.uliejh.cn/bnews/1618.htm
- http://m.wap.uliejh.cn/bnews/40632.htm
- http://m.wap.uliejh.cn/bnews/95944.htm
- http://m.wap.uliejh.cn/bnews/0012328.htm
- http://m.wap.uliejh.cn/bnews/21686.htm
- http://m.wap.uliejh.cn/bnews/44985.htm
- http://m.wap.uliejh.cn/bnews/6286350.htm
- http://m.wap.uliejh.cn/bnews/1945080.htm
- http://m.wap.uliejh.cn/bnews/798467.htm
- http://m.wap.uliejh.cn/bnews/5129.htm
- http://m.wap.uliejh.cn/bnews/59851.htm
- http://m.wap.uliejh.cn/bnews/9167235.htm
- http://m.wap.uliejh.cn/bnews/684689.htm
- http://m.wap.uliejh.cn/bnews/33389.htm
- http://m.wap.uliejh.cn/bnews/45540.htm
- http://m.wap.uliejh.cn/bnews/3664802.htm
- http://m.wap.uliejh.cn/bnews/20698.htm
- http://m.wap.uliejh.cn/bnews/609087.htm
- http://m.wap.uliejh.cn/bnews/170759.htm
- http://m.wap.uliejh.cn/bnews/19072.htm
- http://m.wap.uliejh.cn/bnews/705609.htm
- http://m.wap.uliejh.cn/bnews/7259.htm
- http://m.wap.uliejh.cn/bnews/437532.htm
- http://m.wap.uliejh.cn/bnews/3104941.htm
- http://m.wap.uliejh.cn/bnews/79883.htm
- http://m.wap.uliejh.cn/bnews/30966.htm
- http://m.wap.uliejh.cn/bnews/144674.htm
- http://m.wap.uliejh.cn/bnews/9436544.htm
- http://m.wap.uliejh.cn/bnews/43364.htm
- http://m.wap.uliejh.cn/bnews/54235.htm
- http://m.wap.uliejh.cn/bnews/41900.htm
- http://m.wap.uliejh.cn/bnews/0567201.htm
- http://m.wap.uliejh.cn/bnews/645573.htm
- http://m.wap.uliejh.cn/bnews/35026.htm
- http://m.wap.uliejh.cn/bnews/618355.htm
- http://m.wap.uliejh.cn/bnews/4095.htm
- http://m.wap.uliejh.cn/bnews/2785.htm
- http://m.wap.uliejh.cn/bnews/3274281.htm
- http://m.wap.uliejh.cn/bnews/7067.htm
- http://m.wap.uliejh.cn/bnews/2551.htm
- http://m.wap.uliejh.cn/bnews/95669.htm
- http://m.wap.uliejh.cn/bnews/43068.htm
- http://m.wap.uliejh.cn/bnews/99079.htm
- http://m.wap.uliejh.cn/bnews/3362950.htm
- http://m.wap.uliejh.cn/bnews/4650.htm
- http://m.wap.uliejh.cn/bnews/8297.htm
- http://m.wap.uliejh.cn/bnews/3520851.htm
- http://m.wap.uliejh.cn/bnews/9300738.htm
- http://m.wap.uliejh.cn/bnews/97530.htm
- http://m.wap.uliejh.cn/bnews/63419.htm
- http://m.wap.uliejh.cn/bnews/170577.htm
- http://m.wap.uliejh.cn/bnews/70017.htm
- http://m.wap.uliejh.cn/bnews/8766728.htm
- http://m.wap.uliejh.cn/bnews/259322.htm
- http://m.wap.uliejh.cn/bnews/1674.htm
- http://m.wap.uliejh.cn/bnews/6846.htm
- http://m.wap.uliejh.cn/bnews/5857905.htm
- http://m.wap.uliejh.cn/bnews/6127571.htm
- http://m.wap.uliejh.cn/bnews/26804.htm
- http://m.wap.uliejh.cn/bnews/226926.htm
- http://m.wap.uliejh.cn/bnews/30311.htm
- http://m.wap.uliejh.cn/bnews/941422.htm
- http://m.wap.uliejh.cn/bnews/3644.htm
- http://m.wap.uliejh.cn/bnews/28007.htm
- http://m.wap.uliejh.cn/bnews/154894.htm
- http://m.wap.uliejh.cn/bnews/71457.htm
- http://m.wap.uliejh.cn/bnews/1166214.htm
- http://m.wap.uliejh.cn/bnews/34371.htm
- http://m.wap.uliejh.cn/bnews/452444.htm
- http://m.wap.uliejh.cn/bnews/06498.htm
- http://m.wap.uliejh.cn/bnews/068566.htm
- http://m.wap.uliejh.cn/bnews/59485.htm
- http://m.wap.uliejh.cn/bnews/7909.htm
- http://m.wap.uliejh.cn/bnews/7634168.htm
- http://m.wap.uliejh.cn/bnews/8690397.htm
- http://m.wap.uliejh.cn/bnews/862606.htm
- http://m.wap.uliejh.cn/bnews/6041859.htm
- http://m.wap.uliejh.cn/bnews/63404.htm
- http://m.wap.uliejh.cn/bnews/52639.htm
- http://m.wap.uliejh.cn/bnews/1331.htm
- http://m.wap.uliejh.cn/bnews/0706732.htm
- http://m.wap.uliejh.cn/bnews/65507.htm
- http://m.wap.uliejh.cn/bnews/234083.htm
- http://m.wap.uliejh.cn/bnews/0951.htm
- http://m.wap.uliejh.cn/bnews/9099.htm
- http://m.wap.uliejh.cn/bnews/912721.htm
- http://m.wap.uliejh.cn/bnews/0575.htm
- http://m.wap.uliejh.cn/bnews/7114.htm
- http://m.wap.uliejh.cn/bnews/01027.htm
- http://m.wap.uliejh.cn/bnews/95853.htm
- http://m.wap.uliejh.cn/bnews/75118.htm
- http://m.wap.uliejh.cn/bnews/6262856.htm
- http://m.wap.uliejh.cn/bnews/242359.htm
- http://m.wap.uliejh.cn/bnews/77602.htm
- http://m.wap.uliejh.cn/bnews/883470.htm
- http://m.wap.uliejh.cn/bnews/566749.htm
- http://m.wap.uliejh.cn/bnews/31453.htm
- http://m.wap.uliejh.cn/bnews/35126.htm
- http://m.wap.uliejh.cn/bnews/1345497.htm
- http://m.wap.uliejh.cn/bnews/95156.htm
- http://m.wap.uliejh.cn/bnews/02999.htm
- http://m.wap.uliejh.cn/bnews/3786775.htm
- http://m.wap.uliejh.cn/bnews/975380.htm
- http://m.wap.uliejh.cn/bnews/7103.htm
- http://m.wap.uliejh.cn/bnews/6935.htm
- http://m.wap.uliejh.cn/bnews/3953877.htm
- http://m.wap.uliejh.cn/bnews/1864.htm
- http://m.wap.uliejh.cn/bnews/80172.htm
- http://m.wap.uliejh.cn/bnews/9499.htm
- http://m.wap.uliejh.cn/bnews/05224.htm
- http://m.wap.uliejh.cn/bnews/4016604.htm
- http://m.wap.uliejh.cn/bnews/763592.htm
- http://m.wap.uliejh.cn/bnews/3063787.htm
- http://m.wap.uliejh.cn/bnews/914281.htm
- http://m.wap.uliejh.cn/bnews/081857.htm
- http://m.wap.uliejh.cn/bnews/1190.htm
- http://m.wap.uliejh.cn/bnews/735485.htm
- http://m.wap.uliejh.cn/bnews/28564.htm
- http://m.wap.uliejh.cn/bnews/49828.htm
- http://m.wap.uliejh.cn/bnews/9877880.htm
- http://m.wap.uliejh.cn/bnews/834878.htm
- http://m.wap.uliejh.cn/bnews/88980.htm
- http://m.wap.uliejh.cn/bnews/94340.htm
- http://m.wap.uliejh.cn/bnews/5513202.htm
- http://m.wap.uliejh.cn/bnews/3628717.htm
- http://m.wap.uliejh.cn/bnews/3001.htm
- http://m.wap.uliejh.cn/bnews/4604.htm
- http://m.wap.uliejh.cn/bnews/6500283.htm
- http://m.wap.uliejh.cn/bnews/7540284.htm
- http://m.wap.uliejh.cn/bnews/575521.htm
- http://m.wap.uliejh.cn/bnews/53219.htm
- http://m.wap.uliejh.cn/bnews/1724.htm
- http://m.wap.uliejh.cn/bnews/66055.htm
- http://m.wap.uliejh.cn/bnews/89361.htm
- http://m.wap.uliejh.cn/bnews/9492.htm
- http://m.wap.uliejh.cn/bnews/764491.htm
- http://m.wap.uliejh.cn/bnews/69613.htm
- http://m.wap.uliejh.cn/bnews/1278069.htm
- http://m.wap.uliejh.cn/bnews/9168365.htm
- http://m.wap.uliejh.cn/bnews/335464.htm
- http://m.wap.uliejh.cn/bnews/639680.htm
- http://m.wap.uliejh.cn/bnews/3403407.htm
- http://m.wap.uliejh.cn/bnews/239865.htm
- http://m.wap.uliejh.cn/bnews/31486.htm
- http://m.wap.uliejh.cn/bnews/986769.htm
- http://m.wap.uliejh.cn/bnews/99488.htm
- http://m.wap.uliejh.cn/bnews/5366.htm
- http://m.wap.uliejh.cn/bnews/177487.htm
- http://m.wap.uliejh.cn/bnews/491595.htm
- http://m.wap.uliejh.cn/bnews/4008041.htm
- http://m.wap.uliejh.cn/bnews/1751165.htm
- http://m.wap.uliejh.cn/bnews/78454.htm
- http://m.wap.uliejh.cn/bnews/6805450.htm
- http://m.wap.uliejh.cn/bnews/4296779.htm
- http://m.wap.uliejh.cn/bnews/49475.htm
- http://m.wap.uliejh.cn/bnews/396908.htm
- http://m.wap.uliejh.cn/bnews/9771.htm
- http://m.wap.uliejh.cn/bnews/2071945.htm
- http://m.wap.uliejh.cn/bnews/757405.htm
- http://m.wap.uliejh.cn/bnews/738289.htm
- http://m.wap.uliejh.cn/bnews/84683.htm
- http://m.wap.uliejh.cn/bnews/08328.htm
- http://m.wap.uliejh.cn/bnews/8909552.htm
- http://m.wap.uliejh.cn/bnews/0473071.htm
- http://m.wap.uliejh.cn/bnews/79315.htm
- http://m.wap.uliejh.cn/bnews/5619288.htm
- http://m.wap.uliejh.cn/bnews/315688.htm
- http://m.wap.uliejh.cn/bnews/88422.htm
- http://m.wap.uliejh.cn/bnews/4877742.htm
- http://m.wap.uliejh.cn/bnews/5753848.htm
- http://m.wap.uliejh.cn/bnews/143616.htm
- http://m.wap.uliejh.cn/bnews/156265.htm
- http://m.wap.uliejh.cn/bnews/823177.htm
- http://m.wap.uliejh.cn/bnews/87999.htm
- http://m.wap.uliejh.cn/bnews/420154.htm
- http://m.wap.uliejh.cn/bnews/5959769.htm
- http://m.wap.uliejh.cn/bnews/4821706.htm
- http://m.wap.uliejh.cn/bnews/629659.htm
- http://m.wap.uliejh.cn/bnews/06469.htm
- http://m.wap.uliejh.cn/bnews/6776167.htm
- http://m.wap.uliejh.cn/bnews/907863.htm
- http://m.wap.uliejh.cn/bnews/704445.htm
- http://m.wap.uliejh.cn/bnews/7303753.htm
- http://m.wap.uliejh.cn/bnews/89314.htm
- http://m.wap.uliejh.cn/bnews/9021.htm
- http://m.wap.uliejh.cn/bnews/3880918.htm
- http://m.wap.uliejh.cn/bnews/584380.htm
- http://m.wap.uliejh.cn/bnews/67966.htm
- http://m.wap.uliejh.cn/bnews/2034.htm
- http://m.wap.uliejh.cn/bnews/4376996.htm
- http://m.wap.uliejh.cn/bnews/9342.htm
- http://m.wap.uliejh.cn/bnews/2852.htm
- http://m.wap.uliejh.cn/bnews/0413.htm
- http://m.wap.uliejh.cn/bnews/3815798.htm
- http://m.wap.uliejh.cn/bnews/1999857.htm
- http://m.wap.uliejh.cn/bnews/374574.htm
- http://m.wap.uliejh.cn/bnews/19737.htm
- http://m.wap.uliejh.cn/bnews/7623.htm
- http://m.wap.uliejh.cn/bnews/10188.htm
- http://m.wap.uliejh.cn/bnews/77573.htm
- http://m.wap.uliejh.cn/bnews/55066.htm
- http://m.wap.uliejh.cn/bnews/210690.htm

## 项目结构

项目采用分层模块化设计，核心逻辑与用户界面分离，便于独立演进和替换。

```
archive/
├── app.py                      # Flask Web 服务入口，提供可视化界面与 REST API
├── cli.py                      # 命令行工具主入口，支持导入、探测、导出等子命令
├── requirements.txt            # 生产环境依赖列表，包含 requests、flask、markdown 等
├── config/
│   ├── default.yaml            # 默认配置项：数据库路径、探测超时、重试策略等
│   └── schema.json             # 链接元数据结构的 JSON Schema 校验规则
├── core/
│   ├── __init__.py
│   ├── database.py             # SQLite 数据库连接池管理与基础 CRUD 操作
│   ├── importer.py             # 批量导入器，支持 txt、csv 格式解析与去重逻辑
│   ├── probe.py                # 链接存活探测器，并发请求与状态码记录
│   ├── indexer.py              # FTS5 全文索引构建与查询接口
│   └── exporter.py             # 结果导出器，支持 JSON、CSV、纯文本三种格式
├── scripts/
│   ├── init_db.py              # 初始化数据库表结构与 FTS5 虚拟表
│   ├── import_urls.py          # 命令行导入脚本，接受 --input 与 --batch 参数
│   ├── daily_probe.py          # 每日探测任务，由 cron 调用的无界面脚本
│   └── generate_report.py      # 周报生成器，输出 Markdown 格式健康度报告
├── tests/
│   ├── unit/                   # 单元测试：覆盖导入器、探测器、索引器核心逻辑
│   ├── integration/            # 集成测试：端到端导入-探测-导出流程验证
│   └── fixtures/               # 测试固定数据：示例 URL 列表与预期结果
├── docs/
│   ├── user-guide.md           # 用户手册：安装、配置、日常操作说明
│   ├── operations.md           # 运维手册：部署拓扑、备份恢复、性能调优
│   ├── developer.md            # 开发者指南：模块设计、扩展点、编码规范
│   └── api-reference.md        # API 参考：各模块公共函数的签名与文档字符串
├── data/
│   ├── batches/                # 按批次存放原始导入文件，命名格式 batch_XXX.txt
│   ├── reports/                # 生成的周报与自定义报告存储目录
│   └── archive.db              # SQLite 主数据库文件（运行时生成，不纳入版本控制）
└── CHANGELOG.md                # 版本变更记录，遵循 Keep a Changelog 格式
```

## 贡献指南

1. 在 GitHub Issues 中查阅现有任务列表，认领未被分配的 issue 或在提出新建议前搜索是否有重复议题。对于缺陷报告，请附带完整的错误日志和可复现的输入样本。

2. 派生项目仓库至个人账户，在派生副本中创建以 `feature/` 或 `fix/` 为前缀的分支，分支名称应简要概括改动内容，例如 `feature/add-json-export-format`。

3. 遵循项目已定义的代码风格（PEP 8 对于 Python 文件，每行不超过 88 字符），并在提交前运行 `pytest tests/` 确保所有现有测试通过。对于新增功能，需在 `tests/` 下补充对应的测试用例。

4. 提交变更时使用规范化的提交信息格式：`<类型>: <简短描述>`，类型可选 `feat`、`fix`、`docs`、`refactor`、`test`、`chore`。提交信息正文应说明改动的原因和影响范围。

5. 通过 Pull Request 提交合并请求，在请求描述中关联对应的 Issue 编号，并简述测试覆盖情况与手动验证步骤。PR 需要至少一位项目维护者审阅后方可合并。

## 常见问题

**Q: 导入的链接数量很大时，如何避免重复条目占用存储空间？**

A: 系统在导入阶段会基于 URL 的规范化形式（移除末尾斜杠、统一协议为小写）计算哈希指纹，并与数据库中已有条目对比。您可以通过 `--strict` 参数控制去重策略，默认模式下仅跳过完全相同的 URL，严格模式下会忽略查询参数差异。此外，导入完成后会生成一份去重报告，列出被跳过的重复条目及其首次导入批次号。

**Q: 链接存活探测的结果是否会影响已有数据？**

A: 探测模块仅更新 `last_status`、`last_response_time` 和 `last_probed_at` 三个字段，不会删除或修改任何链接记录。如果某链接连续多次探测均为失效状态，系统会在周报中标记为 "stale"，但保留该条目供用户手动复查。您也可以通过 Web 界面或 CLI 命令手动剔除确认已永久失效的链接。

**Q: 项目是否支持分布式部署或多用户协同操作？**

A: 当前版本设计为单机离线运行模式，数据库文件基于 SQLite，不支持网络并发写入。如果团队需要多用户协同，建议将数据库文件放置在共享存储（如 NFS）上，并确保同一时间仅有一个写入进程运行。对于高并发写入需求，可参考 `docs/operations.md` 中的外部 PostgreSQL 迁移指南，社区已提供实验性的迁移脚本。

## 许可证

MIT

> 外链数量: 250 | 生成时间: 2026-08-24 23:40:21
