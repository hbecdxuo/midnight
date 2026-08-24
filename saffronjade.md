# LinkVault Core

LinkVault Core 是一个面向技术内容聚合与结构化外链管理的开源工具集。该项目定位于为开发者、技术博主、知识库维护者以及自动化采集流程提供一套标准化的外链收录、校验、分类与批量导出方案。其核心能力在于将大量分散的原始 URL 资源（例如来自博客站点的分页或动态生成链接）转化为可维护、可审计、可追溯的结构化数据资产，并配套生成对应的导航页面或 Markdown 文档，特别适用于中大型技术文档站点、API 参考聚合页或社区资源导航站。

目标用户包括需要批量处理外部链接的数据工程师、负责维护技术文档站点的开发者关系团队，以及个人技术博主。LinkVault Core 通过严格的协议保留策略、去重校验、状态码检测和元数据提取，解决多源异构链接难以统一管理、原始 URL 信息丢失以及人工整理效率低下的核心问题。项目采用 Python 3 实现，依赖轻量，可无缝集成至现有 CI/CD 流水线或静态站点生成器（如 Hugo、VuePress）的构建流程中，作为预处理层对原始链接进行标准化清洗和富化。

## 功能概览

- **协议与域名严格透传** 逐条校验并保留用户输入的完整协议前缀和域名层级，不主动补全、不强制跳转 HTTPS，确保链接原始性不受破坏。

- **批量去重与脏数据清洗** 自动识别并移除重复 URL、无效空格、大小写变体及尾部斜杠差异，输出纯净链接集合。

- **元数据自动提取** 对每个 URL 执行异步 HEAD 请求，获取响应状态码、内容类型、最后修改时间及页面标题，丰富链接属性。

- **分类标签体系** 支持基于域名模式、路径关键词或正则表达式的规则引擎，为链接自动打上技术栈、文档类型或内容主题标签。

- **多格式导出器** 内置 Markdown 列表导出、JSON 结构化输出、CSV 表格导出以及静态 HTML 导航页生成器，适配不同发布场景。

- **增量更新与变更日志** 对比历史版本，识别新增、删除或状态变化的链接，生成差异报告，便于审核。

- **命令行与 API 双模式** 提供 CLI 工具用于快速处理本地文件，同时暴露 RESTful API 供远程调用或集成至 Web 服务。

## 应用场景

- **技术文档站点外链审计** 当文档团队需要定期检查站点内所有引用的外部链接是否仍然可访问、是否被重定向或返回错误状态码时，LinkVault Core 可定期爬取并生成链接健康报告，辅助运维人员及时修复失效引用。

- **开源项目资源汇总页构建** 开源社区维护者使用本工具将分散于 issue 评论、邮件列表或社交媒体的推荐资源链接统一收集，经过清洗分类后自动生成 README 中的资源列表章节，保持文档同步更新且无需手动排版。

- **数据采集管道预处理环节** 数据工程师在抓取第三方内容之前，先使用 LinkVault Core 对种子 URL 列表进行去重和协议归一化检查，过滤掉明显无效的条目，降低下游爬虫的无效请求开销，提高采集效率。

- **知识库迁移与 URL 映射** 当企业知识库从旧平台迁移至新系统时，LinkVault Core 可批量校验历史文章中的外部引用链接，生成映射表并标记已失效或变更的地址，辅助内容迁移决策。

- **个人技术博客文章备份整理** 博主导出博客所有文章后，通过本工具提取文中所有外链，快速检查哪些链接已过期，并一键生成新的外链列表用于更新文章附录或友情链接页面。

## 快速开始

以下命令在 Linux / macOS / Windows WSL 环境下均可执行。确保已安装 Git 及 Python 3.8 以上版本。

```bash
# 克隆代码仓库
git clone https://github.com/linkvault/linkvault-core.git
cd linkvault-core

# 创建并激活虚拟环境（推荐）
python3 -m venv venv
source venv/bin/activate      # Linux/macOS
# venv\Scripts\activate       # Windows

# 安装核心依赖
pip install -r requirements.txt

# 使用样例数据运行批量处理
python cli.py process --input sample_links.txt --output report.md

# 启动本地 API 服务（可选）
python api.py --port 8000
```

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|---------|---------|------|
| Python | 3.8, 3.9, 3.10, 3.11 | 核心运行环境，不支持 3.7 及以下版本 |
| requests | 2.28.0 或更高 | 用于发送 HTTP 请求获取链接状态及元数据 |
| click | 8.1.0 或更高 | 命令行交互框架，用于解析 CLI 参数 |
| python-dotenv | 1.0.0 或更高 | 管理环境变量，如 API 密钥或代理配置 |
| pytest | 7.2.0 或更高 | 仅开发测试需要，生产环境可不安装 |
| black | 23.0.0 或更高 | 代码格式化工具，贡献代码时用于风格统一 |
| flask | 2.2.0 或更高 | 可选依赖，仅在启用 API 服务模式时需要 |
| gunicorn | 20.1.0 或更高 | 生产环境部署 API 服务时的 WSGI 服务器 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|------|------|-----------|
| 用户指南 | docs/user_guide.md | 如何安装、配置、运行基础命令以及理解输出格式 |
| 规则引擎手册 | docs/rules_engine.md | 如何编写自定义标签规则、正则表达式模板及优先级控制 |
| API 参考 | docs/api_reference.md | RESTful 接口的鉴权方式、请求参数、响应结构及错误码定义 |
| 贡献者指南 | CONTRIBUTING.md | 开发环境搭建、测试用例编写、提交规范及 PR 流程 |

## 资源列表

- http://m.blog.uliejh.cn/snews/265691.htm
- http://m.blog.uliejh.cn/snews/599652.htm
- http://m.blog.uliejh.cn/snews/05803.htm
- http://m.blog.uliejh.cn/snews/78107.htm
- http://m.blog.uliejh.cn/snews/08483.htm
- http://m.blog.uliejh.cn/snews/9857.htm
- http://m.blog.uliejh.cn/snews/4684.htm
- http://m.blog.uliejh.cn/snews/07201.htm
- http://m.blog.uliejh.cn/snews/736988.htm
- http://m.blog.uliejh.cn/snews/031777.htm
- http://m.blog.uliejh.cn/snews/9422326.htm
- http://m.blog.uliejh.cn/snews/62309.htm
- http://m.blog.uliejh.cn/snews/351157.htm
- http://m.blog.uliejh.cn/snews/3378939.htm
- http://m.blog.uliejh.cn/snews/17407.htm
- http://m.blog.uliejh.cn/snews/406092.htm
- http://m.blog.uliejh.cn/snews/011288.htm
- http://m.blog.uliejh.cn/snews/7303.htm
- http://m.blog.uliejh.cn/snews/3173852.htm
- http://m.blog.uliejh.cn/snews/57701.htm
- http://m.blog.uliejh.cn/snews/848614.htm
- http://m.blog.uliejh.cn/snews/352705.htm
- http://m.blog.uliejh.cn/snews/39539.htm
- http://m.blog.uliejh.cn/snews/6970593.htm
- http://m.blog.uliejh.cn/snews/3896257.htm
- http://m.blog.uliejh.cn/snews/9595782.htm
- http://m.blog.uliejh.cn/snews/7258.htm
- http://m.blog.uliejh.cn/snews/02379.htm
- http://m.blog.uliejh.cn/snews/63882.htm
- http://m.blog.uliejh.cn/snews/5579.htm
- http://m.blog.uliejh.cn/snews/2182.htm
- http://m.blog.uliejh.cn/snews/099060.htm
- http://m.blog.uliejh.cn/snews/9924757.htm
- http://m.blog.uliejh.cn/snews/077348.htm
- http://m.blog.uliejh.cn/snews/15783.htm
- http://m.blog.uliejh.cn/snews/40302.htm
- http://m.blog.uliejh.cn/snews/6483.htm
- http://m.blog.uliejh.cn/snews/391135.htm
- http://m.blog.uliejh.cn/snews/179212.htm
- http://m.blog.uliejh.cn/snews/986123.htm
- http://m.blog.uliejh.cn/snews/4942.htm
- http://m.blog.uliejh.cn/snews/38751.htm
- http://m.blog.uliejh.cn/snews/2743420.htm
- http://m.blog.uliejh.cn/snews/228475.htm
- http://m.blog.uliejh.cn/snews/0575209.htm
- http://m.blog.uliejh.cn/snews/692524.htm
- http://m.blog.uliejh.cn/snews/17291.htm
- http://m.blog.uliejh.cn/snews/48860.htm
- http://m.blog.uliejh.cn/snews/0588550.htm
- http://m.blog.uliejh.cn/snews/170058.htm
- http://m.blog.uliejh.cn/snews/0052892.htm
- http://m.blog.uliejh.cn/snews/64459.htm
- http://m.blog.uliejh.cn/snews/019881.htm
- http://m.blog.uliejh.cn/snews/8187540.htm
- http://m.blog.uliejh.cn/snews/0024.htm
- http://m.blog.uliejh.cn/snews/0276.htm
- http://m.blog.uliejh.cn/snews/80259.htm
- http://m.blog.uliejh.cn/snews/94250.htm
- http://m.blog.uliejh.cn/snews/46601.htm
- http://m.blog.uliejh.cn/snews/7635.htm
- http://m.blog.uliejh.cn/snews/51295.htm
- http://m.blog.uliejh.cn/snews/7334862.htm
- http://m.blog.uliejh.cn/snews/49378.htm
- http://m.blog.uliejh.cn/snews/3011633.htm
- http://m.blog.uliejh.cn/snews/7623.htm
- http://m.blog.uliejh.cn/snews/04708.htm
- http://m.blog.uliejh.cn/snews/2637322.htm
- http://m.blog.uliejh.cn/snews/9044263.htm
- http://m.blog.uliejh.cn/snews/2145.htm
- http://m.blog.uliejh.cn/snews/12999.htm
- http://m.blog.uliejh.cn/snews/7463125.htm
- http://m.blog.uliejh.cn/snews/911567.htm
- http://m.blog.uliejh.cn/snews/1813332.htm
- http://m.blog.uliejh.cn/snews/9939.htm
- http://m.blog.uliejh.cn/snews/6929146.htm
- http://m.blog.uliejh.cn/snews/6804916.htm
- http://m.blog.uliejh.cn/snews/798944.htm
- http://m.blog.uliejh.cn/snews/8929259.htm
- http://m.blog.uliejh.cn/snews/8772726.htm
- http://m.blog.uliejh.cn/snews/901427.htm
- http://m.blog.uliejh.cn/snews/20503.htm
- http://m.blog.uliejh.cn/snews/25277.htm
- http://m.blog.uliejh.cn/snews/8815651.htm
- http://m.blog.uliejh.cn/snews/139286.htm
- http://m.blog.uliejh.cn/snews/17541.htm
- http://m.blog.uliejh.cn/snews/6381.htm
- http://m.blog.uliejh.cn/snews/644517.htm
- http://m.blog.uliejh.cn/snews/5685746.htm
- http://m.blog.uliejh.cn/snews/1291.htm
- http://m.blog.uliejh.cn/snews/6355373.htm
- http://m.blog.uliejh.cn/snews/7460584.htm
- http://m.blog.uliejh.cn/snews/820704.htm
- http://m.blog.uliejh.cn/snews/6157.htm
- http://m.blog.uliejh.cn/snews/173016.htm
- http://m.blog.uliejh.cn/snews/69778.htm
- http://m.blog.uliejh.cn/snews/9705283.htm
- http://m.blog.uliejh.cn/snews/911244.htm
- http://m.blog.uliejh.cn/snews/1867236.htm
- http://m.blog.uliejh.cn/snews/8187.htm
- http://m.blog.uliejh.cn/snews/9364.htm
- http://m.blog.uliejh.cn/snews/52584.htm
- http://m.blog.uliejh.cn/snews/3944.htm
- http://m.blog.uliejh.cn/snews/99359.htm
- http://m.blog.uliejh.cn/snews/0950.htm
- http://m.blog.uliejh.cn/snews/7469.htm
- http://m.blog.uliejh.cn/snews/3812511.htm
- http://m.blog.uliejh.cn/snews/9980.htm
- http://m.blog.uliejh.cn/snews/012643.htm
- http://m.blog.uliejh.cn/snews/473135.htm
- http://m.blog.uliejh.cn/snews/6127235.htm
- http://m.blog.uliejh.cn/snews/1413072.htm
- http://m.blog.uliejh.cn/snews/56306.htm
- http://m.blog.uliejh.cn/snews/330348.htm
- http://m.blog.uliejh.cn/snews/514454.htm
- http://m.blog.uliejh.cn/snews/1294.htm
- http://m.blog.uliejh.cn/snews/493912.htm
- http://m.blog.uliejh.cn/snews/5279742.htm
- http://m.blog.uliejh.cn/snews/350076.htm
- http://m.blog.uliejh.cn/snews/3971.htm
- http://m.blog.uliejh.cn/snews/981734.htm
- http://m.blog.uliejh.cn/snews/51801.htm
- http://m.blog.uliejh.cn/snews/2604967.htm
- http://m.blog.uliejh.cn/snews/2816.htm
- http://m.blog.uliejh.cn/snews/80896.htm
- http://m.blog.uliejh.cn/snews/5820864.htm
- http://m.blog.uliejh.cn/snews/7899487.htm
- http://m.blog.uliejh.cn/snews/80596.htm
- http://m.blog.uliejh.cn/snews/00665.htm
- http://m.blog.uliejh.cn/snews/0985.htm
- http://m.blog.uliejh.cn/snews/7144.htm
- http://m.blog.uliejh.cn/snews/9499064.htm
- http://m.blog.uliejh.cn/snews/8680.htm
- http://m.blog.uliejh.cn/snews/00006.htm
- http://m.blog.uliejh.cn/snews/3672.htm
- http://m.blog.uliejh.cn/snews/13793.htm
- http://m.blog.uliejh.cn/snews/2121636.htm
- http://m.blog.uliejh.cn/snews/678210.htm
- http://m.blog.uliejh.cn/snews/349002.htm
- http://m.blog.uliejh.cn/snews/0311650.htm
- http://m.blog.uliejh.cn/snews/05943.htm
- http://m.blog.uliejh.cn/snews/7465.htm
- http://m.blog.uliejh.cn/snews/339398.htm
- http://m.blog.uliejh.cn/snews/7939779.htm
- http://m.blog.uliejh.cn/snews/9554862.htm
- http://m.blog.uliejh.cn/snews/887068.htm
- http://m.blog.uliejh.cn/snews/34139.htm
- http://m.blog.uliejh.cn/snews/3470.htm
- http://m.blog.uliejh.cn/snews/50352.htm
- http://m.blog.uliejh.cn/snews/9981.htm
- http://m.blog.uliejh.cn/snews/1511.htm
- http://m.blog.uliejh.cn/snews/8184.htm
- http://m.blog.uliejh.cn/snews/644823.htm
- http://m.blog.uliejh.cn/snews/7590173.htm
- http://m.blog.uliejh.cn/snews/8560.htm
- http://m.blog.uliejh.cn/snews/83631.htm
- http://m.blog.uliejh.cn/snews/3735.htm
- http://m.blog.uliejh.cn/snews/4610962.htm
- http://m.blog.uliejh.cn/snews/6218.htm
- http://m.blog.uliejh.cn/snews/6876558.htm
- http://m.blog.uliejh.cn/snews/10649.htm
- http://m.blog.uliejh.cn/snews/43798.htm
- http://m.blog.uliejh.cn/snews/19853.htm
- http://m.blog.uliejh.cn/snews/7483479.htm
- http://m.blog.uliejh.cn/snews/881248.htm
- http://m.blog.uliejh.cn/snews/79265.htm
- http://m.blog.uliejh.cn/snews/674131.htm
- http://m.blog.uliejh.cn/snews/89497.htm
- http://m.blog.uliejh.cn/snews/1265011.htm
- http://m.blog.uliejh.cn/snews/2230930.htm
- http://m.blog.uliejh.cn/snews/3960370.htm
- http://m.blog.uliejh.cn/snews/9822.htm
- http://m.blog.uliejh.cn/snews/6574902.htm
- http://m.blog.uliejh.cn/snews/1053072.htm
- http://m.blog.uliejh.cn/snews/58552.htm
- http://m.blog.uliejh.cn/snews/759668.htm
- http://m.blog.uliejh.cn/snews/5068.htm
- http://m.blog.uliejh.cn/snews/13222.htm
- http://m.blog.uliejh.cn/snews/8859.htm
- http://m.blog.uliejh.cn/snews/4260107.htm
- http://m.blog.uliejh.cn/snews/335278.htm
- http://m.blog.uliejh.cn/snews/951531.htm
- http://m.blog.uliejh.cn/snews/2895885.htm
- http://m.blog.uliejh.cn/snews/8199.htm
- http://m.blog.uliejh.cn/snews/70175.htm
- http://m.blog.uliejh.cn/snews/8189.htm
- http://m.blog.uliejh.cn/snews/3818.htm
- http://m.blog.uliejh.cn/snews/811800.htm
- http://m.blog.uliejh.cn/snews/9573961.htm
- http://m.blog.uliejh.cn/snews/70491.htm
- http://m.blog.uliejh.cn/snews/251062.htm
- http://m.blog.uliejh.cn/snews/9158.htm
- http://m.blog.uliejh.cn/snews/9296353.htm
- http://m.blog.uliejh.cn/snews/7557829.htm
- http://m.blog.uliejh.cn/snews/69716.htm
- http://m.blog.uliejh.cn/snews/03700.htm
- http://m.blog.uliejh.cn/snews/539639.htm
- http://m.blog.uliejh.cn/snews/807780.htm
- http://m.blog.uliejh.cn/snews/7016563.htm
- http://m.blog.uliejh.cn/snews/2543250.htm
- http://m.blog.uliejh.cn/snews/42134.htm
- http://m.blog.uliejh.cn/snews/8032.htm
- http://m.blog.uliejh.cn/snews/75036.htm
- http://m.blog.uliejh.cn/snews/555718.htm
- http://m.blog.uliejh.cn/snews/497713.htm
- http://m.blog.uliejh.cn/snews/561816.htm
- http://m.blog.uliejh.cn/snews/3102969.htm
- http://m.blog.uliejh.cn/snews/9441.htm
- http://m.blog.uliejh.cn/snews/3469.htm
- http://m.blog.uliejh.cn/snews/2488.htm
- http://m.blog.uliejh.cn/snews/912385.htm
- http://m.blog.uliejh.cn/snews/96073.htm
- http://m.blog.uliejh.cn/snews/8993406.htm
- http://m.blog.uliejh.cn/snews/132756.htm
- http://m.blog.uliejh.cn/snews/2648.htm
- http://m.blog.uliejh.cn/snews/6889895.htm
- http://m.blog.uliejh.cn/snews/19759.htm
- http://m.blog.uliejh.cn/snews/2356.htm
- http://m.blog.uliejh.cn/snews/4625.htm
- http://m.blog.uliejh.cn/snews/118255.htm
- http://m.blog.uliejh.cn/snews/45912.htm
- http://m.blog.uliejh.cn/snews/48103.htm
- http://m.blog.uliejh.cn/snews/8526278.htm
- http://m.blog.uliejh.cn/snews/871368.htm
- http://m.blog.uliejh.cn/snews/3638.htm
- http://m.blog.uliejh.cn/snews/2808.htm
- http://m.blog.uliejh.cn/snews/527104.htm
- http://m.blog.uliejh.cn/snews/4913.htm
- http://m.blog.uliejh.cn/snews/240983.htm
- http://m.blog.uliejh.cn/snews/6909054.htm
- http://m.blog.uliejh.cn/snews/5900.htm
- http://m.blog.uliejh.cn/snews/9630926.htm
- http://m.blog.uliejh.cn/snews/504486.htm
- http://m.blog.uliejh.cn/snews/85999.htm
- http://m.blog.uliejh.cn/snews/775550.htm
- http://m.blog.uliejh.cn/snews/0168418.htm
- http://m.blog.uliejh.cn/snews/754973.htm
- http://m.blog.uliejh.cn/snews/75651.htm
- http://m.blog.uliejh.cn/snews/462506.htm
- http://m.blog.uliejh.cn/snews/13275.htm
- http://m.blog.uliejh.cn/snews/19197.htm
- http://m.blog.uliejh.cn/snews/5314253.htm
- http://m.blog.uliejh.cn/snews/1180.htm
- http://m.blog.uliejh.cn/snews/8663.htm
- http://m.blog.uliejh.cn/snews/48616.htm
- http://m.blog.uliejh.cn/snews/3106535.htm
- http://m.blog.uliejh.cn/snews/7859.htm
- http://m.blog.uliejh.cn/snews/5033610.htm
- http://m.blog.uliejh.cn/snews/291364.htm
- http://m.blog.uliejh.cn/snews/493804.htm
- http://m.blog.uliejh.cn/snews/9725495.htm

## 项目结构

```
linkvault-core/
├── cli.py                      # 命令行入口，集成所有子命令
├── api.py                      # Flask API 服务启动脚本
├── requirements.txt            # 生产环境依赖列表
├── .env.example                # 环境变量模板（代理、超时、日志级别）
├── pytest.ini                  # pytest 配置文件
├── README.md                   # 项目说明文档（本文件）
├── LICENSE                     # MIT 许可证文件
├── docs/                       # 用户与开发者文档目录
│   ├── user_guide.md           # 完整用户手册，含命令详解
│   ├── rules_engine.md         # 规则引擎设计文档与示例
│   ├── api_reference.md        # RESTful API 端点与参数说明
│   └── architecture.md         # 整体架构设计与数据流图
├── src/                        # 核心源代码目录
│   ├── __init__.py
│   ├── loader.py               # 原始链接加载器（支持文件、stdin、数据库）
│   ├── cleaner.py              # 去重、空格清理、协议归一化（但保留原始输入）
│   ├── validator.py            # 状态码检测、重定向跟踪与超时控制
│   ├── extractor.py            # HTML 元数据提取（标题、描述、关键词）
│   ├── classifier.py           # 基于规则的标签分类引擎
│   ├── exporter.py             # 多格式导出器（Markdown / JSON / CSV / HTML）
│   ├── differ.py               # 版本对比与增量报告生成
│   └── utils/                  # 工具函数子模块
│       ├── http_client.py      # 异步请求池与连接复用
│       ├── logger.py           # 日志记录与轮转策略
│       └── config.py           # 配置解析（支持 YAML 与环境变量）
├── tests/                      # 单元测试与集成测试目录
│   ├── test_loader.py
│   ├── test_cleaner.py
│   ├── test_validator.py
│   ├── test_extractor.py
│   ├── test_classifier.py
│   ├── test_exporter.py
│   └── fixtures/               # 测试固定数据（样例链接与预期输出）
│       ├── sample_links.txt
│       └── expected_report.md
├── scripts/                    # 运维与辅助脚本
│   ├── batch_process.sh        # 批量处理多批次文件的 Shell 封装
│   └── migrate_db.py           # 数据库迁移工具（SQLite 与 PostgreSQL）
└── data/                       # 数据存储目录（默认 SQLite 数据库与缓存）
    ├── linkvault.db
    └── cache/                  # 请求结果缓存，避免重复网络调用
```

## 贡献指南

1. 从 GitHub 仓库 Fork 项目至个人账户，克隆本地后创建新的功能分支，分支命名遵循 `feature/描述` 或 `fix/描述` 格式，例如 `feature/add-timeout-param`。

2. 安装开发依赖：执行 `pip install -r requirements-dev.txt` 安装 pytest、black、flake8 及 mypy。每次提交前运行 `black src/ tests/` 自动格式化代码，并执行 `flake8 src/` 检查风格问题。

3. 编写或修改功能后，需在 `tests/` 对应模块下补充单元测试用例，确保测试覆盖率达到 85% 以上。运行 `pytest -v --cov=src/` 查看覆盖率报告。

4. 提交 Pull Request 前，请更新 `docs/` 目录下相关的用户文档或 API 文档，并在 PR 描述中明确说明变更类型（新特性、修复、重构或文档更新），同时关联对应的 Issue 编号。

5. 项目维护者会在 5 个工作日内审核 PR，如有修改意见会通过评论标注。合并前需通过所有 CI 检查（包括测试、代码风格和构建）。

## 常见问题

**Q1: 为什么工具不自动将 HTTP 链接升级为 HTTPS？**

A1: LinkVault Core 的设计原则之一是最大限度尊重用户输入的原始性。很多内部系统、测试环境或历史存档站点可能仅支持 HTTP，强制升级会导致访问失败。如果需要批量升级，用户可以在导出阶段使用外部脚本或配置规则引擎中的“协议转换”插件，但核心管线保持透传。

**Q2: 处理数千个链接时，如何防止被目标服务器封禁？**

A2: 工具内置了可配置的请求延迟（`--delay` 参数）和随机 User-Agent 轮换。建议生产环境中设置 `--delay 0.5` 至 `1.0` 秒，并启用 `--respect-robots` 标志自动遵守目标站点的 robots.txt 规则。同时支持代理链配置，可通过环境变量 `HTTP_PROXY` 和 `HTTPS_PROXY` 指定代理服务器。

**Q3: 导出的 Markdown 列表能否直接用于我的 Hugo 站点？**

A3: 可以。默认的 Markdown 导出器生成的是纯无序列表，且不包含 HTML 标签。若 Hugo 站点需要特定 front matter 或分类格式，建议使用 JSON 导出器，然后通过 Hugo 的数据模板或短代码进行渲染。我们也提供了自定义 Jinja2 模板的功能，用户可参考 `docs/user_guide.md` 中的模板变量说明进行调整。

## 许可证

MIT

> 外链数量: 250 | 生成时间: 2026-08-24 23:41:17
