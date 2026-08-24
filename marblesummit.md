# LinkHub Crawler Aggregator

LinkHub Crawler Aggregator 是一个面向技术内容聚合与结构化检索的开源工具集，定位于帮助开发者、技术博主、数据分析师以及自动化运维人员从分散的移动端新闻源、技术公告站点和行业动态页面中批量提取、归一化存储并建立可检索的本地资源索引。该项目的核心目标不是替代搜索引擎，而是针对特定域名下的半结构化内容进行定向抓取、元数据抽取和版本化归档，从而为内部知识库、舆情监控系统或技术情报看板提供稳定、可复用的数据底座。

目标用户包括需要监控特定信源的技术团队、希望构建个人阅读存档的独立开发者、以及需要将外部新闻数据导入自有分析平台的数据工程师。项目通过模块化的下载器、解析器、管道过滤器与导出适配器，将原始 HTML 内容转化为结构化的 JSON 记录，并支持输出为 SQLite、CSV 或 Parquet 格式，便于下游系统消费。当前版本针对 uliejh.cn 移动端新闻路径结构进行了专用适配，同时保留了泛用型抓取框架，可快速扩展至其他同类站点。

## 功能概览

批量并发下载器：基于 aiohttp 构建的异步 HTTP 客户端，支持可配置的并发连接数（默认 16）、重试策略（指数退避）以及请求头轮换，可稳定处理数千级别的 URL 列表。

移动端 HTML 解析器：针对 uliejh.cn 的移动端页面结构开发专用提取规则，能够从正文中剥离标题、发布时间、正文段落、分类标签及内链列表，并自动过滤广告与无关区块。

增量存储与去重机制：使用 SQLite 作为本地存储后端，记录每次抓取的任务 ID、URL 哈希、状态码、内容摘要和抓取时间戳，支持基于 URL 或内容哈希的增量更新，避免重复处理。

多格式导出适配器：内置 CSV、JSON Lines、Parquet 三种导出格式，可分别用于 Excel 查看、日志式追加存储和列式存储分析场景，导出字段可配置。

任务调度与断点续爬：支持从文件或数据库读取待处理 URL 列表，任务中断后可通过记录的状态表恢复未完成的请求，适用于长周期或高波动网络环境。

内容变更检测：通过对比两次抓取的内容摘要（MD5）和字符长度差异，生成变更报告，仅输出有更新的记录，降低下游存储压力。

代理与重定向处理：支持 HTTP/HTTPS 代理配置，自动跟随 301/302 重定向，并可限制最大跳转次数，防止无限循环。

## 应用场景

技术团队内部舆情监控：技术管理者可配置每日定时任务，抓取指定域名下的新闻列表，通过内容变更检测模块仅推送新增或修改的条目至企业微信或钉钉机器人，实现低成本的舆情感知。

个人知识库素材采集：独立开发者或研究者可将该工具作为个人阅读器的上游，定期抓取感兴趣的专栏文章并导出为 CSV 或 JSON，再导入 Obsidian、Notion 或 Logseq 等工具进行二次整理与批注。

行业趋势分析的数据准备：数据分析师可批量导出抓取结果至 Parquet 格式，结合 Pandas、DuckDB 或 Apache Superset 进行词频统计、热度趋势分析和发布时间分布可视化，辅助撰写行业周报。

存档与合规审计：法务或合规团队可通过工具对特定域名下的公开内容进行定期全量存档，生成带时间戳的审计记录，用于满足内部合规审查或外部证据留存需求。

## 快速开始

以下命令演示了从克隆仓库到首次运行完整抓取任务的标准流程：

```bash
# 克隆项目仓库至本地
git clone https://github.com/your-org/linkhub-crawler.git

# 进入项目根目录
cd linkhub-crawler

# 创建并激活 Python 虚拟环境（推荐）
python3 -m venv venv
source venv/bin/activate  # Windows 系统请使用 venv\Scripts\activate

# 安装项目核心依赖及开发依赖
pip install -r requirements.txt

# 使用内置示例 URL 列表运行抓取任务（将输出结果保存在 data/output/ 目录下）
python run_crawler.py --input examples/uliejh_seed.txt --output data/output/ --format json
```

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|---|---|---|
| Python | 3.9 或更高 | 所有核心代码基于 Python 实现，低于此版本将导致异步语法错误 |
| aiohttp | 3.8.0 或更高 | 异步 HTTP 客户端库，负责所有网络请求与连接池管理 |
| beautifulsoup4 | 4.11.0 或更高 | HTML 解析库，用于从移动端页面中抽取结构化内容 |
| lxml | 4.9.0 或更高 | 作为 beautifulsoup4 的解析器后端，提供更快的 XPath 支持 |
| sqlite3 | 系统自带（3.35+） | 本地任务状态存储与去重数据库，无需额外安装 |
| pandas | 1.5.0 或更高 | 仅当需要导出 Parquet 格式或进行数据分析时必需 |
| pyarrow | 10.0.0 或更高 | Parquet 格式的编解码依赖，与 pandas 配合使用 |
| aiohttp-socks | 0.7.0 或更高 | 可选依赖，用于支持 SOCKS 代理协议 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|---|---|---|
| 入门指南 | docs/getting_started.md | 如何安装、配置第一个抓取任务并成功导出结果 |
| 配置参考 | docs/configuration.md | 所有可用的命令行参数、环境变量和配置文件格式说明 |
| 解析器开发 | docs/parser_development.md | 如何为新的站点编写自定义解析规则并注册到解析器工厂 |
| 存储与导出 | docs/storage_and_export.md | 本地数据库表结构、数据生命周期管理以及各导出格式的字段映射 |
| API 参考 | docs/api_reference.md | 核心类、函数和装饰器的详细签名与使用示例 |
| 常见工作流 | docs/workflows.md | 定时任务配置、增量抓取策略和变更报告解读 |

## 资源列表

- http://m.3g.uliejh.cn/nnews/5894.htm
- http://m.3g.uliejh.cn/nnews/03146.htm
- http://m.3g.uliejh.cn/nnews/709333.htm
- http://m.3g.uliejh.cn/nnews/6526844.htm
- http://m.3g.uliejh.cn/nnews/975025.htm
- http://m.3g.uliejh.cn/nnews/8121520.htm
- http://m.3g.uliejh.cn/nnews/3567.htm
- http://m.3g.uliejh.cn/nnews/51675.htm
- http://m.3g.uliejh.cn/nnews/2957117.htm
- http://m.3g.uliejh.cn/nnews/59890.htm
- http://m.3g.uliejh.cn/nnews/858253.htm
- http://m.3g.uliejh.cn/nnews/60009.htm
- http://m.3g.uliejh.cn/nnews/4496.htm
- http://m.3g.uliejh.cn/nnews/8085938.htm
- http://m.3g.uliejh.cn/nnews/4762166.htm
- http://m.3g.uliejh.cn/nnews/711386.htm
- http://m.3g.uliejh.cn/nnews/6067672.htm
- http://m.3g.uliejh.cn/nnews/19546.htm
- http://m.3g.uliejh.cn/nnews/8263.htm
- http://m.3g.uliejh.cn/nnews/9963.htm
- http://m.3g.uliejh.cn/nnews/6895.htm
- http://m.3g.uliejh.cn/nnews/76010.htm
- http://m.3g.uliejh.cn/nnews/7856.htm
- http://m.3g.uliejh.cn/nnews/16703.htm
- http://m.3g.uliejh.cn/nnews/82123.htm
- http://m.3g.uliejh.cn/nnews/78940.htm
- http://m.3g.uliejh.cn/nnews/3812.htm
- http://m.3g.uliejh.cn/nnews/442208.htm
- http://m.3g.uliejh.cn/nnews/596967.htm
- http://m.3g.uliejh.cn/nnews/16353.htm
- http://m.3g.uliejh.cn/nnews/9316222.htm
- http://m.3g.uliejh.cn/nnews/951180.htm
- http://m.3g.uliejh.cn/nnews/68566.htm
- http://m.3g.uliejh.cn/nnews/6751476.htm
- http://m.3g.uliejh.cn/nnews/20658.htm
- http://m.3g.uliejh.cn/nnews/28196.htm
- http://m.3g.uliejh.cn/nnews/350585.htm
- http://m.3g.uliejh.cn/nnews/7724795.htm
- http://m.3g.uliejh.cn/nnews/343219.htm
- http://m.3g.uliejh.cn/nnews/2415.htm
- http://m.3g.uliejh.cn/nnews/78439.htm
- http://m.3g.uliejh.cn/nnews/1480.htm
- http://m.3g.uliejh.cn/nnews/8748523.htm
- http://m.3g.uliejh.cn/nnews/3427672.htm
- http://m.3g.uliejh.cn/nnews/8252.htm
- http://m.3g.uliejh.cn/nnews/67768.htm
- http://m.3g.uliejh.cn/nnews/095495.htm
- http://m.3g.uliejh.cn/nnews/2642.htm
- http://m.3g.uliejh.cn/nnews/9622.htm
- http://m.3g.uliejh.cn/nnews/6411.htm
- http://m.3g.uliejh.cn/nnews/2772.htm
- http://m.3g.uliejh.cn/nnews/61215.htm
- http://m.3g.uliejh.cn/nnews/400556.htm
- http://m.3g.uliejh.cn/nnews/3944270.htm
- http://m.3g.uliejh.cn/nnews/92316.htm
- http://m.3g.uliejh.cn/nnews/47187.htm
- http://m.3g.uliejh.cn/nnews/47098.htm
- http://m.3g.uliejh.cn/nnews/0031472.htm
- http://m.3g.uliejh.cn/nnews/52469.htm
- http://m.3g.uliejh.cn/nnews/7113.htm
- http://m.3g.uliejh.cn/nnews/004746.htm
- http://m.3g.uliejh.cn/nnews/276888.htm
- http://m.3g.uliejh.cn/nnews/7195166.htm
- http://m.3g.uliejh.cn/nnews/79848.htm
- http://m.3g.uliejh.cn/nnews/3622798.htm
- http://m.3g.uliejh.cn/nnews/133631.htm
- http://m.3g.uliejh.cn/nnews/86272.htm
- http://m.3g.uliejh.cn/nnews/726583.htm
- http://m.3g.uliejh.cn/nnews/8689340.htm
- http://m.3g.uliejh.cn/nnews/167070.htm
- http://m.3g.uliejh.cn/nnews/06909.htm
- http://m.3g.uliejh.cn/nnews/45189.htm
- http://m.3g.uliejh.cn/nnews/581046.htm
- http://m.3g.uliejh.cn/nnews/0668.htm
- http://m.3g.uliejh.cn/nnews/04022.htm
- http://m.3g.uliejh.cn/nnews/807375.htm
- http://m.3g.uliejh.cn/nnews/3144990.htm
- http://m.3g.uliejh.cn/nnews/883992.htm
- http://m.3g.uliejh.cn/nnews/5029827.htm
- http://m.3g.uliejh.cn/nnews/46115.htm
- http://m.3g.uliejh.cn/nnews/7463.htm
- http://m.3g.uliejh.cn/nnews/9701.htm
- http://m.3g.uliejh.cn/nnews/75958.htm
- http://m.3g.uliejh.cn/nnews/7045883.htm
- http://m.3g.uliejh.cn/nnews/218932.htm
- http://m.3g.uliejh.cn/nnews/468851.htm
- http://m.3g.uliejh.cn/nnews/439473.htm
- http://m.3g.uliejh.cn/nnews/4026938.htm
- http://m.3g.uliejh.cn/nnews/60365.htm
- http://m.3g.uliejh.cn/nnews/0324.htm
- http://m.3g.uliejh.cn/nnews/7483760.htm
- http://m.3g.uliejh.cn/nnews/08402.htm
- http://m.3g.uliejh.cn/nnews/1896.htm
- http://m.3g.uliejh.cn/nnews/49094.htm
- http://m.3g.uliejh.cn/nnews/4274273.htm
- http://m.3g.uliejh.cn/nnews/74863.htm
- http://m.3g.uliejh.cn/nnews/34273.htm
- http://m.3g.uliejh.cn/nnews/96246.htm
- http://m.3g.uliejh.cn/nnews/7672.htm
- http://m.3g.uliejh.cn/nnews/25660.htm
- http://m.3g.uliejh.cn/nnews/214621.htm
- http://m.3g.uliejh.cn/nnews/8532991.htm
- http://m.3g.uliejh.cn/nnews/629688.htm
- http://m.3g.uliejh.cn/nnews/87809.htm
- http://m.3g.uliejh.cn/nnews/56694.htm
- http://m.3g.uliejh.cn/nnews/560783.htm
- http://m.3g.uliejh.cn/nnews/8118084.htm
- http://m.3g.uliejh.cn/nnews/352014.htm
- http://m.3g.uliejh.cn/nnews/6331337.htm
- http://m.3g.uliejh.cn/nnews/031039.htm
- http://m.3g.uliejh.cn/nnews/8254910.htm
- http://m.3g.uliejh.cn/nnews/01564.htm
- http://m.3g.uliejh.cn/nnews/2767.htm
- http://m.3g.uliejh.cn/nnews/931542.htm
- http://m.3g.uliejh.cn/nnews/02947.htm
- http://m.3g.uliejh.cn/nnews/4610490.htm
- http://m.3g.uliejh.cn/nnews/82279.htm
- http://m.3g.uliejh.cn/nnews/5092334.htm
- http://m.3g.uliejh.cn/nnews/57856.htm
- http://m.3g.uliejh.cn/nnews/566821.htm
- http://m.3g.uliejh.cn/nnews/845761.htm
- http://m.3g.uliejh.cn/nnews/306047.htm
- http://m.3g.uliejh.cn/nnews/0012358.htm
- http://m.3g.uliejh.cn/nnews/4625.htm
- http://m.3g.uliejh.cn/nnews/4827985.htm
- http://m.3g.uliejh.cn/nnews/4058009.htm
- http://m.3g.uliejh.cn/nnews/00576.htm
- http://m.3g.uliejh.cn/nnews/31434.htm
- http://m.3g.uliejh.cn/nnews/63228.htm
- http://m.3g.uliejh.cn/nnews/7242709.htm
- http://m.3g.uliejh.cn/nnews/917113.htm
- http://m.3g.uliejh.cn/nnews/480443.htm
- http://m.3g.uliejh.cn/nnews/4349618.htm
- http://m.3g.uliejh.cn/nnews/1294346.htm
- http://m.3g.uliejh.cn/nnews/8985.htm
- http://m.3g.uliejh.cn/nnews/23978.htm
- http://m.3g.uliejh.cn/nnews/4725.htm
- http://m.3g.uliejh.cn/nnews/9713742.htm
- http://m.3g.uliejh.cn/nnews/7493450.htm
- http://m.3g.uliejh.cn/nnews/72570.htm
- http://m.3g.uliejh.cn/nnews/858840.htm
- http://m.3g.uliejh.cn/nnews/3950896.htm
- http://m.3g.uliejh.cn/nnews/6527496.htm
- http://m.3g.uliejh.cn/nnews/6991.htm
- http://m.3g.uliejh.cn/nnews/1786929.htm
- http://m.3g.uliejh.cn/nnews/5963037.htm
- http://m.3g.uliejh.cn/nnews/17281.htm
- http://m.3g.uliejh.cn/nnews/3177.htm
- http://m.3g.uliejh.cn/nnews/68099.htm
- http://m.3g.uliejh.cn/nnews/55298.htm
- http://m.3g.uliejh.cn/nnews/471671.htm
- http://m.3g.uliejh.cn/nnews/1240.htm
- http://m.3g.uliejh.cn/nnews/0513.htm
- http://m.3g.uliejh.cn/nnews/787807.htm
- http://m.3g.uliejh.cn/nnews/60231.htm
- http://m.3g.uliejh.cn/nnews/844774.htm
- http://m.3g.uliejh.cn/nnews/23373.htm
- http://m.3g.uliejh.cn/nnews/03835.htm
- http://m.3g.uliejh.cn/nnews/06334.htm
- http://m.3g.uliejh.cn/nnews/149741.htm
- http://m.3g.uliejh.cn/nnews/28182.htm
- http://m.3g.uliejh.cn/nnews/85886.htm
- http://m.3g.uliejh.cn/nnews/34330.htm
- http://m.3g.uliejh.cn/nnews/33731.htm
- http://m.3g.uliejh.cn/nnews/638054.htm
- http://m.3g.uliejh.cn/nnews/29291.htm
- http://m.3g.uliejh.cn/nnews/0998177.htm
- http://m.3g.uliejh.cn/nnews/2874.htm
- http://m.3g.uliejh.cn/nnews/621164.htm
- http://m.3g.uliejh.cn/nnews/248059.htm
- http://m.3g.uliejh.cn/nnews/1514.htm
- http://m.3g.uliejh.cn/nnews/0352.htm
- http://m.3g.uliejh.cn/nnews/80747.htm
- http://m.3g.uliejh.cn/nnews/1193.htm
- http://m.3g.uliejh.cn/nnews/36542.htm
- http://m.3g.uliejh.cn/nnews/41881.htm
- http://m.3g.uliejh.cn/nnews/9874018.htm
- http://m.3g.uliejh.cn/nnews/61749.htm
- http://m.3g.uliejh.cn/nnews/07261.htm
- http://m.3g.uliejh.cn/nnews/304129.htm
- http://m.3g.uliejh.cn/nnews/14648.htm
- http://m.3g.uliejh.cn/nnews/6462.htm
- http://m.3g.uliejh.cn/nnews/3839672.htm
- http://m.3g.uliejh.cn/nnews/22905.htm
- http://m.3g.uliejh.cn/nnews/22901.htm
- http://m.3g.uliejh.cn/nnews/9510342.htm
- http://m.3g.uliejh.cn/nnews/806228.htm
- http://m.3g.uliejh.cn/nnews/1902201.htm
- http://m.3g.uliejh.cn/nnews/85206.htm
- http://m.3g.uliejh.cn/nnews/26850.htm
- http://m.3g.uliejh.cn/nnews/6979.htm
- http://m.3g.uliejh.cn/nnews/136221.htm
- http://m.3g.uliejh.cn/nnews/52093.htm
- http://m.3g.uliejh.cn/nnews/533293.htm
- http://m.3g.uliejh.cn/nnews/6584.htm
- http://m.3g.uliejh.cn/nnews/663549.htm
- http://m.3g.uliejh.cn/nnews/743882.htm
- http://m.3g.uliejh.cn/nnews/74282.htm
- http://m.3g.uliejh.cn/nnews/4050598.htm
- http://m.3g.uliejh.cn/nnews/9764243.htm
- http://m.3g.uliejh.cn/nnews/2769.htm
- http://m.3g.uliejh.cn/nnews/67522.htm
- http://m.3g.uliejh.cn/nnews/371636.htm
- http://m.3g.uliejh.cn/nnews/8177131.htm
- http://m.3g.uliejh.cn/nnews/4932572.htm
- http://m.3g.uliejh.cn/nnews/90030.htm
- http://m.3g.uliejh.cn/nnews/038733.htm
- http://m.3g.uliejh.cn/nnews/2470.htm
- http://m.3g.uliejh.cn/nnews/94603.htm
- http://m.3g.uliejh.cn/nnews/9771916.htm
- http://m.3g.uliejh.cn/nnews/1017.htm
- http://m.3g.uliejh.cn/nnews/67904.htm
- http://m.3g.uliejh.cn/nnews/500447.htm
- http://m.3g.uliejh.cn/nnews/7062539.htm
- http://m.3g.uliejh.cn/nnews/743958.htm
- http://m.3g.uliejh.cn/nnews/6386.htm
- http://m.3g.uliejh.cn/nnews/0842015.htm
- http://m.3g.uliejh.cn/nnews/2443.htm
- http://m.3g.uliejh.cn/nnews/6513.htm
- http://m.3g.uliejh.cn/nnews/81469.htm
- http://m.3g.uliejh.cn/nnews/30546.htm
- http://m.3g.uliejh.cn/nnews/866432.htm
- http://m.3g.uliejh.cn/nnews/1993334.htm
- http://m.3g.uliejh.cn/nnews/76627.htm
- http://m.3g.uliejh.cn/nnews/6210.htm
- http://m.3g.uliejh.cn/nnews/10890.htm
- http://m.3g.uliejh.cn/nnews/5392524.htm
- http://m.3g.uliejh.cn/nnews/265969.htm
- http://m.3g.uliejh.cn/nnews/4440530.htm
- http://m.3g.uliejh.cn/nnews/882060.htm
- http://m.3g.uliejh.cn/nnews/012420.htm
- http://m.3g.uliejh.cn/nnews/9268.htm
- http://m.3g.uliejh.cn/nnews/72783.htm
- http://m.3g.uliejh.cn/nnews/002377.htm
- http://m.3g.uliejh.cn/nnews/470148.htm
- http://m.3g.uliejh.cn/nnews/5040.htm
- http://m.3g.uliejh.cn/nnews/221538.htm
- http://m.3g.uliejh.cn/nnews/7615198.htm
- http://m.3g.uliejh.cn/nnews/786340.htm
- http://m.3g.uliejh.cn/nnews/656301.htm
- http://m.3g.uliejh.cn/nnews/8147065.htm
- http://m.3g.uliejh.cn/nnews/7595420.htm
- http://m.3g.uliejh.cn/nnews/9888039.htm
- http://m.3g.uliejh.cn/nnews/47004.htm
- http://m.3g.uliejh.cn/nnews/9337.htm
- http://m.3g.uliejh.cn/nnews/344301.htm
- http://m.3g.uliejh.cn/nnews/8254523.htm
- http://m.3g.uliejh.cn/nnews/3320168.htm
- http://m.3g.uliejh.cn/nnews/903012.htm
- http://m.3g.uliejh.cn/nnews/1763870.htm

## 项目结构

```
linkhub-crawler/
├── run_crawler.py                 # 项目主入口，解析命令行参数并驱动整个抓取流程
├── requirements.txt               # 生产环境依赖列表，包含核心库版本锁定
├── dev-requirements.txt           # 开发与测试环境额外依赖（pytest, flake8, mypy 等）
├── config/
│   ├── default.yaml               # 默认配置参数（并发数、超时时间、重试策略等）
│   └── parser_rules.json          # 针对 uliejh.cn 的专用解析规则（CSS 选择器与字段映射）
├── src/
│   ├── __init__.py
│   ├── http_client.py             # 基于 aiohttp 的异步请求封装，含连接池与重试逻辑
│   ├── parser.py                  # 通用 HTML 解析基类及工厂方法，支持注册新站点解析器
│   ├── parsers/
│   │   ├── __init__.py
│   │   ├── base_parser.py         # 解析器抽象基类，定义 extract 接口
│   │   └── uliejh_parser.py       # uliejh.cn 专用解析器，实现标题、正文、时间抽取
│   ├── storage/
│   │   ├── __init__.py
│   │   ├── sqlite_store.py        # SQLite 存储实现，含建表语句与 CRUD 操作
│   │   └── dedup.py               # 基于 URL 哈希和内容摘要的去重逻辑
│   ├── exporter/
│   │   ├── __init__.py
│   │   ├── csv_exporter.py        # CSV 格式导出器，使用 csv.DictWriter
│   │   ├── jsonl_exporter.py      # JSON Lines 格式导出器，逐行写入 JSON 对象
│   │   └── parquet_exporter.py    # Parquet 格式导出器，依赖 pandas + pyarrow
│   ├── scheduler/
│   │   ├── __init__.py
│   │   └── task_manager.py        # 任务队列调度，支持断点续爬与进度持久化
│   └── utils/
│       ├── __init__.py
│       ├── logger.py              # 统一日志配置，支持文件和控制台输出
│       └── validators.py          # URL 校验、哈希计算和字段清洗工具
├── tests/
│   ├── unit/                      # 单元测试，覆盖解析器、存储和导出模块
│   ├── integration/               # 端到端集成测试，使用测试服务器模拟响应
│   └── fixtures/                  # 测试用样本 HTML 文件和预期输出 JSON
├── examples/
│   ├── uliejh_seed.txt            # 示例种子 URL 列表（包含本批 250 条链接）
│   └── custom_parser_demo.py      # 演示如何编写自定义解析器并注册
├── docs/                          # 完整文档目录，内容详见上文文档导航
└── data/
    ├── input/                     # 存放外部传入的待处理 URL 列表文件
    ├── output/                    # 抓取结果导出目录，按任务时间戳子目录归档
    └── cache/                     # SQLite 数据库文件及临时缓存文件
```

## 贡献指南

1. 阅读项目文档中的开发指引（docs/parser_development.md 和 docs/api_reference.md），了解核心抽象类与扩展接口的设计约定，确保新增代码与现有架构风格一致。

2. 在 GitHub 上 fork 本仓库，创建以 feature/ 或 fix/ 为前缀的分支，并在本地完成开发与自测。所有新增功能必须包含对应的单元测试，测试覆盖率不得低于 80%。

3. 提交代码前运行完整的测试套件（pytest tests/）和代码风格检查（flake8 src/ tests/），确保无回归缺陷且符合 PEP 8 规范。建议使用 pre-commit 钩子自动格式化。

4. 发起 Pull Request 至主仓库的 main 分支，在 PR 描述中清晰说明变更动机、影响范围以及手动测试步骤。若涉及配置变更或新增依赖，需同步更新 requirements.txt 和默认配置文件。

5. 项目维护者将在 3 个工作日内进行 Code Review，并根据反馈进行修改或合并。重大功能变更或架构调整需提前在 issue 中讨论并获得共识。

## 常见问题

Q: 抓取过程中出现大量 HTTP 429 或 503 错误，如何解决？

A: 这类错误通常表示目标服务器实施了频率限制或临时过载。建议采取以下措施：降低并发连接数（通过 --concurrency 参数设置为 4 或 8）；增加请求间隔（在配置文件中设置 request_delay 为 1.5 秒以上）；启用代理轮换（通过 --proxy-list 参数传入代理池文件）。此外，任务管理器支持断点续爬，中断后重新运行相同命令将自动跳过已成功抓取的记录。

Q: 解析器无法正确提取某些字段，返回空值，如何调试？

A: 首先检查原始 HTML 结构是否与预期一致，可在 parser_rules.json 中调整 CSS 选择器或 XPath 表达式。项目提供了交互式调试工具（python -m src.parsers.debug --url <目标URL>），该工具会输出解析后的原始 DOM 树片段和每个字段的匹配过程。若页面结构发生较大改版，建议使用浏览器开发者工具重新定位目标元素，并更新规则文件后重新运行测试。

Q: 导出为 Parquet 格式时提示缺少 pyarrow 模块，是否必须安装？

A: Parquet 导出为可选功能，仅当需要与数据分析工具（如 Apache Spark、DuckDB 或 Power BI）直接集成时才需要使用。如果仅使用 CSV 或 JSON Lines 格式，无需安装 pyarrow 和 pandas。若要启用 Parquet 支持，请执行 pip install -r requirements.txt 安装完整依赖组，或单独安装 pandas 和 pyarrow 并确保版本符合要求。

## 许可证

MIT

> 外链数量: 250 | 生成时间: 2026-08-24 23:40:21
