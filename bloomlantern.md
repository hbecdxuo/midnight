# NewsLink Aggregator

NewsLink Aggregator 是一个面向技术资讯聚合与外部资源索引的开源工具集，定位于帮助开发者、技术研究人员与内容策展人批量采集、整理和归档来自移动端新闻源的结构化数据。该项目不依赖特定商业平台，通过可配置的抓取策略与标准化输出格式，将零散的新闻链接转换为可用于数据分析、知识图谱构建或自定义订阅源的基础数据集。目标用户包括需要定期跟踪特定域名发布动态的运维工程师、从事网络内容分析的学术研究者以及希望建立个人新闻档案库的独立开发者。

## 功能概览

- **批量链接采集**：支持基于域名前缀与路径模式的递归扫描，自动发现指定根路径下的全部新闻条目链接。
- **增量更新机制**：通过本地缓存记录已处理的链接指纹，仅对新出现的条目执行内容拉取，避免重复请求。
- **结构化元数据提取**：从链接路径中解析发布时间、文章编号与分类标签，生成统一的 JSON 元数据清单。
- **自定义过滤规则**：允许用户通过正则表达式或关键词列表筛选链接，排除广告页、评论页或非正文页面。
- **多格式导出**：内置 CSV、JSON Lines 与 Markdown 列表三种导出模板，适配数据分析工具、静态站点生成器与纯文本阅览场景。
- **请求频率控制**：提供可调节的并发数与请求间隔参数，降低对目标服务器造成的访问压力。
- **错误重试与日志**：对超时或返回 5xx 状态的请求自动执行指数退避重试，并将全部操作记录写入分级日志文件。
- **镜像校验**：支持对已下载内容计算校验和，确保归档文件的完整性与一致性。

## 应用场景

**个人技术新闻库构建**：开发者可将每日关注的移动端新闻源链接纳入聚合流程，结合定时任务自动拉取正文内容，在本地搭建轻量级全文检索系统，避免依赖第三方 RSS 服务。

**网络内容演化分析**：研究人员利用该工具定期抓取特定域名下的历史链接，通过对比链接数量、路径模式变化与发布时间分布，分析新闻站点的内容生产节奏与栏目调整趋势。

**数据迁移辅助**：在更换内容管理系统或静态站点生成器时，通过导出链接清单与元数据表格，快速完成文章映射关系的核对，降低人工整理错误率。

**离线阅读准备**：用户可在网络条件良好时执行批量拉取，将内容保存为 Markdown 或纯文本文件，同步至移动设备供无网络环境下的阅读与批注。

## 快速开始

以下指令适用于 Linux 与 macOS 环境，Windows 用户可通过 WSL 或 Git Bash 执行。

```bash
# 克隆项目仓库
git clone https://github.com/example/newslink-aggregator.git
cd newslink-aggregator

# 安装依赖（Python 3.9+ 环境）
pip install -r requirements.txt

# 运行基础采集示例（使用内置的测试源）
python cli.py collect --source config/sources.example.json --output ./output
```

## 安装要求

| 依赖 | 必需版本 | 说明 |
|------|----------|------|
| Python | 3.9 或更高 | 解释器运行时，低于 3.9 将导致类型注解语法错误 |
| requests | 2.28.0 及以上 | HTTP 请求库，用于执行链接抓取与内容下载 |
| beautifulsoup4 | 4.11.0 及以上 | HTML 解析库，仅在启用正文提取功能时需要 |
| lxml | 4.9.0 及以上 | 高性能 XML/HTML 解析器，作为 beautifulsoup4 的底层加速器 |
| jsonschema | 4.17.0 及以上 | 用于校验输出 JSON 文件的结构合法性 |
| pytest | 7.0.0 及以上 | 仅开发测试时需要，生产环境可不安装 |
| loguru | 0.6.0 及以上 | 日志记录增强库，提供结构化日志输出与自动轮转 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|------|------|------------|
| 入门 | docs/quickstart.md | 如何在一分钟内跑通采集流程并生成首批输出文件？ |
| 配置 | docs/configuration.md | 链接源、过滤规则、并发参数与存储路径分别如何设置？ |
| 输出 | docs/output-format.md | 每种导出格式的字段定义、示例数据及二次加工建议是什么？ |
| 进阶 | docs/custom-parser.md | 如何为新的新闻源编写自定义路径解析器与元数据映射函数？ |

## 资源列表

- http://m.3g.uliejh.cn/nnews/65554.htm
- http://m.3g.uliejh.cn/nnews/9233.htm
- http://m.3g.uliejh.cn/nnews/66623.htm
- http://m.3g.uliejh.cn/nnews/977970.htm
- http://m.3g.uliejh.cn/nnews/0366.htm
- http://m.3g.uliejh.cn/nnews/4263868.htm
- http://m.3g.uliejh.cn/nnews/1991653.htm
- http://m.3g.uliejh.cn/nnews/4232.htm
- http://m.3g.uliejh.cn/nnews/8112.htm
- http://m.3g.uliejh.cn/nnews/3759606.htm
- http://m.3g.uliejh.cn/nnews/6095595.htm
- http://m.3g.uliejh.cn/nnews/8608917.htm
- http://m.3g.uliejh.cn/nnews/34924.htm
- http://m.3g.uliejh.cn/nnews/6090.htm
- http://m.3g.uliejh.cn/nnews/6143892.htm
- http://m.3g.uliejh.cn/nnews/5223.htm
- http://m.3g.uliejh.cn/nnews/166441.htm
- http://m.3g.uliejh.cn/nnews/818706.htm
- http://m.3g.uliejh.cn/nnews/1093409.htm
- http://m.3g.uliejh.cn/nnews/1630891.htm
- http://m.3g.uliejh.cn/nnews/86496.htm
- http://m.3g.uliejh.cn/nnews/098661.htm
- http://m.3g.uliejh.cn/nnews/7645561.htm
- http://m.3g.uliejh.cn/nnews/6429597.htm
- http://m.3g.uliejh.cn/nnews/68086.htm
- http://m.3g.uliejh.cn/nnews/364921.htm
- http://m.3g.uliejh.cn/nnews/252922.htm
- http://m.3g.uliejh.cn/nnews/943080.htm
- http://m.3g.uliejh.cn/nnews/806612.htm
- http://m.3g.uliejh.cn/nnews/90896.htm
- http://m.3g.uliejh.cn/nnews/5457.htm
- http://m.3g.uliejh.cn/nnews/52070.htm
- http://m.3g.uliejh.cn/nnews/67281.htm
- http://m.3g.uliejh.cn/nnews/17876.htm
- http://m.3g.uliejh.cn/nnews/2721836.htm
- http://m.3g.uliejh.cn/nnews/8494747.htm
- http://m.3g.uliejh.cn/nnews/13726.htm
- http://m.3g.uliejh.cn/nnews/51129.htm
- http://m.3g.uliejh.cn/nnews/6318.htm
- http://m.3g.uliejh.cn/nnews/1845770.htm
- http://m.3g.uliejh.cn/nnews/1418108.htm
- http://m.3g.uliejh.cn/nnews/550326.htm
- http://m.3g.uliejh.cn/nnews/81966.htm
- http://m.3g.uliejh.cn/nnews/1054674.htm
- http://m.3g.uliejh.cn/nnews/38804.htm
- http://m.3g.uliejh.cn/nnews/1559561.htm
- http://m.3g.uliejh.cn/nnews/6256744.htm
- http://m.3g.uliejh.cn/nnews/1155716.htm
- http://m.3g.uliejh.cn/nnews/8855.htm
- http://m.3g.uliejh.cn/nnews/598451.htm
- http://m.3g.uliejh.cn/nnews/97236.htm
- http://m.3g.uliejh.cn/nnews/37638.htm
- http://m.3g.uliejh.cn/nnews/79687.htm
- http://m.3g.uliejh.cn/nnews/7941.htm
- http://m.3g.uliejh.cn/nnews/33102.htm
- http://m.3g.uliejh.cn/nnews/010128.htm
- http://m.3g.uliejh.cn/nnews/1798287.htm
- http://m.3g.uliejh.cn/nnews/643818.htm
- http://m.3g.uliejh.cn/nnews/72849.htm
- http://m.3g.uliejh.cn/nnews/210946.htm
- http://m.3g.uliejh.cn/nnews/7506872.htm
- http://m.3g.uliejh.cn/nnews/4610225.htm
- http://m.3g.uliejh.cn/nnews/96636.htm
- http://m.3g.uliejh.cn/nnews/0948768.htm
- http://m.3g.uliejh.cn/nnews/858690.htm
- http://m.3g.uliejh.cn/nnews/40297.htm
- http://m.3g.uliejh.cn/nnews/547628.htm
- http://m.3g.uliejh.cn/nnews/74669.htm
- http://m.3g.uliejh.cn/nnews/25643.htm
- http://m.3g.uliejh.cn/nnews/26817.htm
- http://m.3g.uliejh.cn/nnews/86737.htm
- http://m.3g.uliejh.cn/nnews/05017.htm
- http://m.3g.uliejh.cn/nnews/5558212.htm
- http://m.3g.uliejh.cn/nnews/3984537.htm
- http://m.3g.uliejh.cn/nnews/8478210.htm
- http://m.3g.uliejh.cn/nnews/30355.htm
- http://m.3g.uliejh.cn/nnews/606925.htm
- http://m.3g.uliejh.cn/nnews/9280983.htm
- http://m.3g.uliejh.cn/nnews/2535.htm
- http://m.3g.uliejh.cn/nnews/5655196.htm
- http://m.3g.uliejh.cn/nnews/661577.htm
- http://m.3g.uliejh.cn/nnews/42403.htm
- http://m.3g.uliejh.cn/nnews/9399.htm
- http://m.3g.uliejh.cn/nnews/062270.htm
- http://m.3g.uliejh.cn/nnews/310994.htm
- http://m.3g.uliejh.cn/nnews/546468.htm
- http://m.3g.uliejh.cn/nnews/875194.htm
- http://m.3g.uliejh.cn/nnews/724550.htm
- http://m.3g.uliejh.cn/nnews/1276.htm
- http://m.3g.uliejh.cn/nnews/1770.htm
- http://m.3g.uliejh.cn/nnews/2553.htm
- http://m.3g.uliejh.cn/nnews/94625.htm
- http://m.3g.uliejh.cn/nnews/99622.htm
- http://m.3g.uliejh.cn/nnews/2695.htm
- http://m.3g.uliejh.cn/nnews/6737.htm
- http://m.3g.uliejh.cn/nnews/502240.htm
- http://m.3g.uliejh.cn/nnews/6503655.htm
- http://m.3g.uliejh.cn/nnews/4073121.htm
- http://m.3g.uliejh.cn/nnews/333570.htm
- http://m.3g.uliejh.cn/nnews/5250.htm
- http://m.3g.uliejh.cn/nnews/375551.htm
- http://m.3g.uliejh.cn/nnews/6081.htm
- http://m.3g.uliejh.cn/nnews/94980.htm
- http://m.3g.uliejh.cn/nnews/7775.htm
- http://m.3g.uliejh.cn/nnews/7536151.htm
- http://m.3g.uliejh.cn/nnews/9927.htm
- http://m.3g.uliejh.cn/nnews/0737.htm
- http://m.3g.uliejh.cn/nnews/162185.htm
- http://m.3g.uliejh.cn/nnews/01998.htm
- http://m.3g.uliejh.cn/nnews/2989.htm
- http://m.3g.uliejh.cn/nnews/46796.htm
- http://m.3g.uliejh.cn/nnews/5187.htm
- http://m.3g.uliejh.cn/nnews/89894.htm
- http://m.3g.uliejh.cn/nnews/3053326.htm
- http://m.3g.uliejh.cn/nnews/96820.htm
- http://m.3g.uliejh.cn/nnews/3273.htm
- http://m.3g.uliejh.cn/nnews/8293317.htm
- http://m.3g.uliejh.cn/nnews/609501.htm
- http://m.3g.uliejh.cn/nnews/7135259.htm
- http://m.3g.uliejh.cn/nnews/80388.htm
- http://m.3g.uliejh.cn/nnews/5272791.htm
- http://m.3g.uliejh.cn/nnews/67617.htm
- http://m.3g.uliejh.cn/nnews/5116.htm
- http://m.3g.uliejh.cn/nnews/4698475.htm
- http://m.3g.uliejh.cn/nnews/5928.htm
- http://m.3g.uliejh.cn/nnews/948244.htm
- http://m.3g.uliejh.cn/nnews/05605.htm
- http://m.3g.uliejh.cn/nnews/653866.htm
- http://m.3g.uliejh.cn/nnews/147902.htm
- http://m.3g.uliejh.cn/nnews/1994.htm
- http://m.3g.uliejh.cn/nnews/880298.htm
- http://m.3g.uliejh.cn/nnews/545861.htm
- http://m.3g.uliejh.cn/nnews/4673356.htm
- http://m.3g.uliejh.cn/nnews/109677.htm
- http://m.3g.uliejh.cn/nnews/4363914.htm
- http://m.3g.uliejh.cn/nnews/19752.htm
- http://m.3g.uliejh.cn/nnews/04278.htm
- http://m.3g.uliejh.cn/nnews/68388.htm
- http://m.3g.uliejh.cn/nnews/126185.htm
- http://m.3g.uliejh.cn/nnews/413683.htm
- http://m.3g.uliejh.cn/nnews/4393.htm
- http://m.3g.uliejh.cn/nnews/750265.htm
- http://m.3g.uliejh.cn/nnews/671511.htm
- http://m.3g.uliejh.cn/nnews/5609616.htm
- http://m.3g.uliejh.cn/nnews/6105.htm
- http://m.3g.uliejh.cn/nnews/66316.htm
- http://m.3g.uliejh.cn/nnews/673738.htm
- http://m.3g.uliejh.cn/nnews/28284.htm
- http://m.3g.uliejh.cn/nnews/285467.htm
- http://m.3g.uliejh.cn/nnews/486024.htm
- http://m.3g.uliejh.cn/nnews/744002.htm
- http://m.3g.uliejh.cn/nnews/54102.htm
- http://m.3g.uliejh.cn/nnews/4936050.htm
- http://m.3g.uliejh.cn/nnews/30459.htm
- http://m.3g.uliejh.cn/nnews/87120.htm
- http://m.3g.uliejh.cn/nnews/7431852.htm
- http://m.3g.uliejh.cn/nnews/77539.htm
- http://m.3g.uliejh.cn/nnews/455494.htm
- http://m.3g.uliejh.cn/nnews/28507.htm
- http://m.3g.uliejh.cn/nnews/720991.htm
- http://m.3g.uliejh.cn/nnews/74471.htm
- http://m.3g.uliejh.cn/nnews/77794.htm
- http://m.3g.uliejh.cn/nnews/962795.htm
- http://m.3g.uliejh.cn/nnews/826618.htm
- http://m.3g.uliejh.cn/nnews/7425877.htm
- http://m.3g.uliejh.cn/nnews/9516948.htm
- http://m.3g.uliejh.cn/nnews/2548.htm
- http://m.3g.uliejh.cn/nnews/8078202.htm
- http://m.3g.uliejh.cn/nnews/503315.htm
- http://m.3g.uliejh.cn/nnews/7323.htm
- http://m.3g.uliejh.cn/nnews/034557.htm
- http://m.3g.uliejh.cn/nnews/55520.htm
- http://m.3g.uliejh.cn/nnews/4406.htm
- http://m.3g.uliejh.cn/nnews/698853.htm
- http://m.3g.uliejh.cn/nnews/1099789.htm
- http://m.3g.uliejh.cn/nnews/882380.htm
- http://m.3g.uliejh.cn/nnews/41608.htm
- http://m.3g.uliejh.cn/nnews/9836.htm
- http://m.3g.uliejh.cn/nnews/97167.htm
- http://m.3g.uliejh.cn/nnews/836665.htm
- http://m.3g.uliejh.cn/nnews/405078.htm
- http://m.3g.uliejh.cn/nnews/2329742.htm
- http://m.3g.uliejh.cn/nnews/9788.htm
- http://m.3g.uliejh.cn/nnews/48274.htm
- http://m.3g.uliejh.cn/nnews/154715.htm
- http://m.3g.uliejh.cn/nnews/8867293.htm
- http://m.3g.uliejh.cn/nnews/1149.htm
- http://m.3g.uliejh.cn/nnews/1533.htm
- http://m.3g.uliejh.cn/nnews/91438.htm
- http://m.3g.uliejh.cn/nnews/53473.htm
- http://m.3g.uliejh.cn/nnews/2785389.htm
- http://m.3g.uliejh.cn/nnews/7153718.htm
- http://m.3g.uliejh.cn/nnews/943657.htm
- http://m.3g.uliejh.cn/nnews/635136.htm
- http://m.3g.uliejh.cn/nnews/71226.htm
- http://m.3g.uliejh.cn/nnews/381724.htm
- http://m.3g.uliejh.cn/nnews/4532901.htm
- http://m.3g.uliejh.cn/nnews/25392.htm
- http://m.3g.uliejh.cn/nnews/6836802.htm
- http://m.3g.uliejh.cn/nnews/8403.htm
- http://m.3g.uliejh.cn/nnews/638119.htm
- http://m.3g.uliejh.cn/nnews/37793.htm
- http://m.3g.uliejh.cn/nnews/5978275.htm
- http://m.3g.uliejh.cn/nnews/7008312.htm
- http://m.3g.uliejh.cn/nnews/2073783.htm
- http://m.3g.uliejh.cn/nnews/63122.htm
- http://m.3g.uliejh.cn/nnews/994448.htm
- http://m.3g.uliejh.cn/nnews/1810.htm
- http://m.3g.uliejh.cn/nnews/3564.htm
- http://m.3g.uliejh.cn/nnews/865076.htm
- http://m.3g.uliejh.cn/nnews/92726.htm
- http://m.3g.uliejh.cn/nnews/210465.htm
- http://m.3g.uliejh.cn/nnews/4051562.htm
- http://m.3g.uliejh.cn/nnews/2348.htm
- http://m.3g.uliejh.cn/nnews/4997469.htm
- http://m.3g.uliejh.cn/nnews/1678.htm
- http://m.3g.uliejh.cn/nnews/0898553.htm
- http://m.3g.uliejh.cn/nnews/2729950.htm
- http://m.3g.uliejh.cn/nnews/4128.htm
- http://m.3g.uliejh.cn/nnews/1822018.htm
- http://m.3g.uliejh.cn/nnews/23902.htm
- http://m.3g.uliejh.cn/nnews/7834018.htm
- http://m.3g.uliejh.cn/nnews/9361.htm
- http://m.3g.uliejh.cn/nnews/2318.htm
- http://m.3g.uliejh.cn/nnews/1658.htm
- http://m.3g.uliejh.cn/nnews/9508393.htm
- http://m.3g.uliejh.cn/nnews/284869.htm
- http://m.3g.uliejh.cn/nnews/86829.htm
- http://m.3g.uliejh.cn/nnews/37307.htm
- http://m.3g.uliejh.cn/nnews/707377.htm
- http://m.3g.uliejh.cn/nnews/4431.htm
- http://m.3g.uliejh.cn/nnews/27133.htm
- http://m.3g.uliejh.cn/nnews/97478.htm
- http://m.3g.uliejh.cn/nnews/62525.htm
- http://m.3g.uliejh.cn/nnews/338838.htm
- http://m.3g.uliejh.cn/nnews/444176.htm
- http://m.3g.uliejh.cn/nnews/7746.htm
- http://m.3g.uliejh.cn/nnews/2656015.htm
- http://m.3g.uliejh.cn/nnews/24430.htm
- http://m.3g.uliejh.cn/nnews/217393.htm
- http://m.3g.uliejh.cn/nnews/846449.htm
- http://m.3g.uliejh.cn/nnews/9309078.htm
- http://m.3g.uliejh.cn/nnews/3061.htm
- http://m.3g.uliejh.cn/nnews/7937031.htm
- http://m.3g.uliejh.cn/nnews/2454527.htm
- http://m.3g.uliejh.cn/nnews/8601133.htm
- http://m.3g.uliejh.cn/nnews/9644147.htm
- http://m.3g.uliejh.cn/nnews/2363.htm
- http://m.3g.uliejh.cn/nnews/697487.htm
- http://m.3g.uliejh.cn/nnews/4779.htm

## 项目结构

```
newslink-aggregator/
├── cli.py                      # 命令行入口，整合 collect、export、validate 子命令
├── requirements.txt            # 生产环境依赖锁定文件
├── pyproject.toml              # 项目元数据与构建配置（PEP 621）
├── src/
│   ├── core/
│   │   ├── __init__.py
│   │   ├── collector.py        # 核心采集引擎，管理请求队列与去重
│   │   └── parser.py           # 路径解析与元数据抽取逻辑
│   ├── filters/
│   │   ├── __init__.py
│   │   ├── regex.py            # 基于正则表达式的链接过滤实现
│   │   └── whitelist.py        # 白名单与黑名单管理模块
│   ├── exporters/
│   │   ├── __init__.py
│   │   ├── jsonl.py            # JSON Lines 格式导出器
│   │   ├── csv.py              # 表格化导出器
│   │   └── markdown.py         # 纯文本列表导出器
│   ├── utils/
│   │   ├── __init__.py
│   │   ├── http.py             # 请求包装、重试、超时控制
│   │   ├── logger.py           # 日志初始化与分级输出
│   │   └── cache.py            # 本地指纹缓存读写操作
│   └── models/
│       ├── __init__.py
│       ├── link.py             # Link 数据类定义
│       └── manifest.py         # 采集任务清单结构
├── tests/
│   ├── unit/                   # 单元测试覆盖核心函数
│   └── integration/            # 集成测试使用模拟服务端
├── config/
│   ├── sources.example.json    # 示例源配置文件
│   └── filters.example.json    # 示例过滤规则文件
├── docs/
│   ├── quickstart.md
│   ├── configuration.md
│   ├── output-format.md
│   └── custom-parser.md
└── output/                     # 默认输出目录（运行后自动创建）
    ├── raw/                    # 原始响应体存储
    └── exported/               # 格式化导出文件存放处
```

## 贡献指南

1. 阅读项目代码风格文档（位于 docs/contributing/style-guide.md），确保新增代码遵循 PEP 8 规范，并使用 black 与 isort 进行格式化。
2. 在 issue 列表中认领或创建新的功能提议，简要描述拟解决的问题与实现思路，等待维护者确认后再开始编码。
3. 基于 main 分支创建特性分支，命名格式为 feature/功能简述 或 fix/问题简述，避免在主干分支上直接提交。
4. 提交代码时附上清晰的 commit message，说明变更原因与影响范围，并确保所有已有单元测试通过，新增功能需补充对应测试用例。
5. 发起 pull request 至 main 分支，等待代码审查；审查通过后由维护者合并，合并后自动触发 CI 流程进行构建与发布。

## 常见问题

**问：采集过程中遇到 403 或 429 状态码应如何处理？**

答：该工具内置指数退避重试机制，默认对 429、500、502、503 状态码执行最多 3 次重试。若持续返回 403，通常表示目标站点启用了反爬策略，建议调整请求头中的 User-Agent 字段，或增加请求间隔（通过 --delay 参数设置，单位秒）。对于严格限制的站点，可启用代理池模块（需自行配置代理列表）。

**问：如何将采集结果集成到静态站点生成器（如 Hugo 或 Jekyll）中？**

答：使用内置的 markdown 导出器可将链接列表生成为标准的无序列表文件，将其放置在站点内容目录下即可直接渲染。若需要包含正文内容，可启用 --with-content 参数，此时导出器会将每条链接对应的正文摘要一同写入，生成适配短代码模板的 Markdown 片段。

**问：项目是否支持增量采集，避免每次全量扫描？**

答：支持。采集器会在首次运行时于 output/cache/ 目录下创建指纹文件，记录已处理链接的路径与最后修改时间。后续执行时会自动跳过指纹匹配的条目，仅对新链接或内容有更新的链接发起请求。该功能默认启用，可通过 --no-cache 禁用。

## 许可证

MIT

> 外链数量: 250 | 生成时间: 2026-08-24 23:40:21
