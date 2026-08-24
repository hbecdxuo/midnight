# NewsLink Hub

NewsLink Hub 是一个面向数据采集、内容聚合与历史存档场景的轻量级新闻外链管理平台。该项目定位于为研究人员、数据分析师以及内容运营人员提供稳定、可回溯、可批处理的新闻页面引用源集合。项目本身不存储新闻内容，仅维护指向第三方新闻页面的标准化 URL 列表，并通过元数据索引机制实现高效检索与状态监控。

目标用户包括需要构建新闻语料库的自然语言处理工程师、进行舆情分析的社会科学研究者、以及需要定期抓取特定新闻来源的内容管理开发者。NewsLink Hub 通过提供统一的 URL 清单、批次划分说明和访问状态记录模板，帮助用户降低外链管理成本，避免链接散落在脚本或文档中导致维护困难。

## 功能概览

**批量 URL 清单管理**：项目以批次为单位组织新闻外链，每批次包含 250 个独立新闻页面链接，覆盖不同域名与路径结构，便于用户按批次执行采集任务。

**链接状态标记系统**：提供在线、失效、重定向三种状态标记字段，用户可根据实际访问结果更新每条链接的状态，形成历史可用性记录。

**基础元数据索引**：每条链接关联发布时间、新闻类型、来源域名三个索引字段，支持按这些维度进行快速筛选与统计。

**多格式导出支持**：内置脚本支持将 URL 清单导出为 CSV、JSON 和纯文本格式，方便导入第三方采集工具或数据分析环境。

**访问日志记录**：项目提供访问日志模板，记录每次批量检查的时间戳、成功数和失败数，便于追溯采集任务执行情况。

**批次版本管理**：每批次配备独立的版本号与更新日期，用户可通过 Git 标签追踪不同批次的链接变化，确保实验可复现。

**轻量级本地服务器**：附带基于 Python 内置模块的简易 HTTP 服务，可在本地启动用于预览链接清单或提供内部 API 接口。

**与主流采集框架兼容**：项目输出的 URL 列表可直接用于 Scrapy、Playwright、Requests 等常见采集工具的种子文件格式。

## 应用场景

舆情分析系统种子构建：舆情监测团队可将本项目的 URL 清单作为采集系统的初始种子，定期抓取指定新闻页面内容，进行情感分析与热点识别。每批次 250 条链接的设计便于分布式任务分配。

新闻语料库历史回溯：自然语言处理研究团队需要按时间维度构建新闻语料。本项目链接中包含数字编号，可用于模拟不同时间段的新闻分布，辅助模型训练中的时间泛化测试。

链接生命周期监测：内容聚合平台可使用本项目定期检查每条外链的可访问性，统计域名失效比例，为内容缓存策略提供数据支撑。项目内置的状态标记系统支持这一流程。

采集任务编排教学：作为教学示例，本项目提供结构清晰的 URL 资源列表，适合用于演示 Web 采集课程中的任务队列管理、请求频率控制和异常处理等知识点。

## 快速开始

```bash
# 克隆项目仓库
git clone https://github.com/example/newslink-hub.git
cd newslink-hub

# 安装 Python 依赖（需 Python 3.8 及以上）
pip install -r requirements.txt

# 运行本地预览服务（默认端口 8080）
python serve.py --port 8080

# 执行链接状态检查（仅检查前 50 条）
python check_links.py --limit 50 --output status_report.json
```

## 安装要求

| 依赖 | 必需版本 | 说明 |
|------|----------|------|
| Python | 3.8 及以上 | 核心运行环境，用于执行脚本与启动服务 |
| pip | 21.0 及以上 | Python 包管理工具，用于安装项目依赖 |
| requests | 2.28.0 及以上 | 用于发送 HTTP 请求以检查链接状态 |
| beautifulsoup4 | 4.11.0 及以上 | 可选依赖，用于解析新闻页面标题与摘要 |
| pandas | 1.5.0 及以上 | 可选依赖，用于导出 CSV 与 JSON 格式数据 |
| git | 2.25.0 及以上 | 用于克隆仓库和版本管理 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|------|------|------------|
| 用户手册 | docs/user-guide.md | 如何下载、安装、运行本项目以及管理 URL 清单 |
| 开发者指南 | docs/developer-guide.md | 如何扩展链接检查逻辑、添加新的导出格式 |
| 批次说明 | docs/batch-9.md | 第 9 批次的链接数量、编号范围与更新记录 |
| API 参考 | docs/api-reference.md | 本地服务器提供的 HTTP 接口定义与调用示例 |

## 资源列表

- http://m.3g.uliejh.cn/nnews/80903.htm
- http://m.3g.uliejh.cn/nnews/1289312.htm
- http://m.3g.uliejh.cn/nnews/5832997.htm
- http://m.3g.uliejh.cn/nnews/74531.htm
- http://m.3g.uliejh.cn/nnews/69138.htm
- http://m.3g.uliejh.cn/nnews/42578.htm
- http://m.3g.uliejh.cn/nnews/39770.htm
- http://m.3g.uliejh.cn/nnews/121834.htm
- http://m.3g.uliejh.cn/nnews/31530.htm
- http://m.3g.uliejh.cn/nnews/01535.htm
- http://m.3g.uliejh.cn/nnews/67325.htm
- http://m.3g.uliejh.cn/nnews/0945694.htm
- http://m.3g.uliejh.cn/nnews/70189.htm
- http://m.3g.uliejh.cn/nnews/8710921.htm
- http://m.3g.uliejh.cn/nnews/4891.htm
- http://m.3g.uliejh.cn/nnews/90413.htm
- http://m.3g.uliejh.cn/nnews/6339.htm
- http://m.3g.uliejh.cn/nnews/140702.htm
- http://m.3g.uliejh.cn/nnews/848918.htm
- http://m.3g.uliejh.cn/nnews/8104.htm
- http://m.3g.uliejh.cn/nnews/7951722.htm
- http://m.3g.uliejh.cn/nnews/649558.htm
- http://m.3g.uliejh.cn/nnews/692051.htm
- http://m.3g.uliejh.cn/nnews/5425.htm
- http://m.3g.uliejh.cn/nnews/086692.htm
- http://m.3g.uliejh.cn/nnews/510701.htm
- http://m.3g.uliejh.cn/nnews/7659.htm
- http://m.3g.uliejh.cn/nnews/2588277.htm
- http://m.3g.uliejh.cn/nnews/7881215.htm
- http://m.3g.uliejh.cn/nnews/473935.htm
- http://m.3g.uliejh.cn/nnews/16795.htm
- http://m.3g.uliejh.cn/nnews/29727.htm
- http://m.3g.uliejh.cn/nnews/82410.htm
- http://m.3g.uliejh.cn/nnews/4542622.htm
- http://m.3g.uliejh.cn/nnews/9383.htm
- http://m.3g.uliejh.cn/nnews/723191.htm
- http://m.3g.uliejh.cn/nnews/7174374.htm
- http://m.3g.uliejh.cn/nnews/16865.htm
- http://m.3g.uliejh.cn/nnews/847956.htm
- http://m.3g.uliejh.cn/nnews/3816.htm
- http://m.3g.uliejh.cn/nnews/89779.htm
- http://m.3g.uliejh.cn/nnews/55777.htm
- http://m.3g.uliejh.cn/nnews/7510760.htm
- http://m.3g.uliejh.cn/nnews/7576.htm
- http://m.3g.uliejh.cn/nnews/1651787.htm
- http://m.3g.uliejh.cn/nnews/9991663.htm
- http://m.3g.uliejh.cn/nnews/9020.htm
- http://m.3g.uliejh.cn/nnews/4938.htm
- http://m.3g.uliejh.cn/nnews/569826.htm
- http://m.3g.uliejh.cn/nnews/802955.htm
- http://m.3g.uliejh.cn/nnews/442536.htm
- http://m.3g.uliejh.cn/nnews/91716.htm
- http://m.3g.uliejh.cn/nnews/43670.htm
- http://m.3g.uliejh.cn/nnews/34260.htm
- http://m.3g.uliejh.cn/nnews/3237168.htm
- http://m.3g.uliejh.cn/nnews/1993546.htm
- http://m.3g.uliejh.cn/nnews/1168.htm
- http://m.3g.uliejh.cn/nnews/16132.htm
- http://m.3g.uliejh.cn/nnews/8468.htm
- http://m.3g.uliejh.cn/nnews/93170.htm
- http://m.3g.uliejh.cn/nnews/635729.htm
- http://m.3g.uliejh.cn/nnews/336628.htm
- http://m.3g.uliejh.cn/nnews/2060592.htm
- http://m.3g.uliejh.cn/nnews/201428.htm
- http://m.3g.uliejh.cn/nnews/876462.htm
- http://m.3g.uliejh.cn/nnews/26173.htm
- http://m.3g.uliejh.cn/nnews/092178.htm
- http://m.3g.uliejh.cn/nnews/4294.htm
- http://m.3g.uliejh.cn/nnews/373774.htm
- http://m.3g.uliejh.cn/nnews/5644604.htm
- http://m.3g.uliejh.cn/nnews/566785.htm
- http://m.3g.uliejh.cn/nnews/643675.htm
- http://m.3g.uliejh.cn/nnews/62065.htm
- http://m.3g.uliejh.cn/nnews/7935353.htm
- http://m.3g.uliejh.cn/nnews/566723.htm
- http://m.3g.uliejh.cn/nnews/94311.htm
- http://m.3g.uliejh.cn/nnews/3311105.htm
- http://m.3g.uliejh.cn/nnews/9217.htm
- http://m.3g.uliejh.cn/nnews/270565.htm
- http://m.3g.uliejh.cn/nnews/6464.htm
- http://m.3g.uliejh.cn/nnews/977166.htm
- http://m.3g.uliejh.cn/nnews/94503.htm
- http://m.3g.uliejh.cn/nnews/6077.htm
- http://m.3g.uliejh.cn/nnews/9846.htm
- http://m.3g.uliejh.cn/nnews/81337.htm
- http://m.3g.uliejh.cn/nnews/55094.htm
- http://m.3g.uliejh.cn/nnews/311431.htm
- http://m.3g.uliejh.cn/nnews/53715.htm
- http://m.3g.uliejh.cn/nnews/65806.htm
- http://m.3g.uliejh.cn/nnews/5423.htm
- http://m.3g.uliejh.cn/nnews/6990.htm
- http://m.3g.uliejh.cn/nnews/2638561.htm
- http://m.3g.uliejh.cn/nnews/4083183.htm
- http://m.3g.uliejh.cn/nnews/62951.htm
- http://m.3g.uliejh.cn/nnews/057417.htm
- http://m.3g.uliejh.cn/nnews/441593.htm
- http://m.3g.uliejh.cn/nnews/6994971.htm
- http://m.3g.uliejh.cn/nnews/723257.htm
- http://m.3g.uliejh.cn/nnews/33991.htm
- http://m.3g.uliejh.cn/nnews/8213953.htm
- http://m.3g.uliejh.cn/nnews/02959.htm
- http://m.3g.uliejh.cn/nnews/1686990.htm
- http://m.3g.uliejh.cn/nnews/2144.htm
- http://m.3g.uliejh.cn/nnews/4487330.htm
- http://m.3g.uliejh.cn/nnews/1045774.htm
- http://m.3g.uliejh.cn/nnews/324560.htm
- http://m.3g.uliejh.cn/nnews/66741.htm
- http://m.3g.uliejh.cn/nnews/0007.htm
- http://m.3g.uliejh.cn/nnews/11612.htm
- http://m.3g.uliejh.cn/nnews/8441703.htm
- http://m.3g.uliejh.cn/nnews/690314.htm
- http://m.3g.uliejh.cn/nnews/8714.htm
- http://m.3g.uliejh.cn/nnews/92249.htm
- http://m.3g.uliejh.cn/nnews/00056.htm
- http://m.3g.uliejh.cn/nnews/616338.htm
- http://m.3g.uliejh.cn/nnews/2877.htm
- http://m.3g.uliejh.cn/nnews/3776999.htm
- http://m.3g.uliejh.cn/nnews/8006.htm
- http://m.3g.uliejh.cn/nnews/793701.htm
- http://m.3g.uliejh.cn/nnews/5416121.htm
- http://m.3g.uliejh.cn/nnews/133167.htm
- http://m.3g.uliejh.cn/nnews/548314.htm
- http://m.3g.uliejh.cn/nnews/647789.htm
- http://m.3g.uliejh.cn/nnews/237815.htm
- http://m.3g.uliejh.cn/nnews/6857111.htm
- http://m.3g.uliejh.cn/nnews/17564.htm
- http://m.3g.uliejh.cn/nnews/4577.htm
- http://m.3g.uliejh.cn/nnews/69329.htm
- http://m.3g.uliejh.cn/nnews/239818.htm
- http://m.3g.uliejh.cn/nnews/6566445.htm
- http://m.3g.uliejh.cn/nnews/660475.htm
- http://m.3g.uliejh.cn/nnews/23707.htm
- http://m.3g.uliejh.cn/nnews/713355.htm
- http://m.3g.uliejh.cn/nnews/33779.htm
- http://m.3g.uliejh.cn/nnews/562317.htm
- http://m.3g.uliejh.cn/nnews/2258432.htm
- http://m.3g.uliejh.cn/nnews/62276.htm
- http://m.3g.uliejh.cn/nnews/47633.htm
- http://m.3g.uliejh.cn/nnews/8840570.htm
- http://m.3g.uliejh.cn/nnews/571430.htm
- http://m.3g.uliejh.cn/nnews/467116.htm
- http://m.3g.uliejh.cn/nnews/6595.htm
- http://m.3g.uliejh.cn/nnews/3823295.htm
- http://m.3g.uliejh.cn/nnews/1118.htm
- http://m.3g.uliejh.cn/nnews/24914.htm
- http://m.3g.uliejh.cn/nnews/2101941.htm
- http://m.3g.uliejh.cn/nnews/6998603.htm
- http://m.3g.uliejh.cn/nnews/901765.htm
- http://m.3g.uliejh.cn/nnews/673117.htm
- http://m.3g.uliejh.cn/nnews/2149.htm
- http://m.3g.uliejh.cn/nnews/254629.htm
- http://m.3g.uliejh.cn/nnews/4635.htm
- http://m.3g.uliejh.cn/nnews/789397.htm
- http://m.3g.uliejh.cn/nnews/8281.htm
- http://m.3g.uliejh.cn/nnews/59377.htm
- http://m.3g.uliejh.cn/nnews/042686.htm
- http://m.3g.uliejh.cn/nnews/931469.htm
- http://m.3g.uliejh.cn/nnews/89636.htm
- http://m.3g.uliejh.cn/nnews/1855.htm
- http://m.3g.uliejh.cn/nnews/53928.htm
- http://m.3g.uliejh.cn/nnews/45052.htm
- http://m.3g.uliejh.cn/nnews/22039.htm
- http://m.3g.uliejh.cn/nnews/5124.htm
- http://m.3g.uliejh.cn/nnews/6400.htm
- http://m.3g.uliejh.cn/nnews/793268.htm
- http://m.3g.uliejh.cn/nnews/9943.htm
- http://m.3g.uliejh.cn/nnews/2490249.htm
- http://m.3g.uliejh.cn/nnews/53025.htm
- http://m.3g.uliejh.cn/nnews/690284.htm
- http://m.3g.uliejh.cn/nnews/680233.htm
- http://m.3g.uliejh.cn/nnews/7289.htm
- http://m.3g.uliejh.cn/nnews/2829.htm
- http://m.3g.uliejh.cn/nnews/4421.htm
- http://m.3g.uliejh.cn/nnews/39097.htm
- http://m.3g.uliejh.cn/nnews/4484279.htm
- http://m.3g.uliejh.cn/nnews/5321.htm
- http://m.3g.uliejh.cn/nnews/322968.htm
- http://m.3g.uliejh.cn/nnews/1534.htm
- http://m.3g.uliejh.cn/nnews/8201.htm
- http://m.3g.uliejh.cn/nnews/51223.htm
- http://m.3g.uliejh.cn/nnews/9069.htm
- http://m.3g.uliejh.cn/nnews/660523.htm
- http://m.3g.uliejh.cn/nnews/2747.htm
- http://m.3g.uliejh.cn/nnews/95281.htm
- http://m.3g.uliejh.cn/nnews/218138.htm
- http://m.3g.uliejh.cn/nnews/4986.htm
- http://m.3g.uliejh.cn/nnews/5463922.htm
- http://m.3g.uliejh.cn/nnews/7415.htm
- http://m.3g.uliejh.cn/nnews/4276591.htm
- http://m.3g.uliejh.cn/nnews/11150.htm
- http://m.3g.uliejh.cn/nnews/5097208.htm
- http://m.3g.uliejh.cn/nnews/95765.htm
- http://m.3g.uliejh.cn/nnews/509522.htm
- http://m.3g.uliejh.cn/nnews/2745911.htm
- http://m.3g.uliejh.cn/nnews/4771299.htm
- http://m.3g.uliejh.cn/nnews/07803.htm
- http://m.3g.uliejh.cn/nnews/2398.htm
- http://m.3g.uliejh.cn/nnews/2787.htm
- http://m.3g.uliejh.cn/nnews/7521.htm
- http://m.3g.uliejh.cn/nnews/1295065.htm
- http://m.3g.uliejh.cn/nnews/030541.htm
- http://m.3g.uliejh.cn/nnews/5335089.htm
- http://m.3g.uliejh.cn/nnews/9485253.htm
- http://m.3g.uliejh.cn/nnews/30952.htm
- http://m.3g.uliejh.cn/nnews/329166.htm
- http://m.3g.uliejh.cn/nnews/06726.htm
- http://m.3g.uliejh.cn/nnews/85901.htm
- http://m.3g.uliejh.cn/nnews/85282.htm
- http://m.3g.uliejh.cn/nnews/1992.htm
- http://m.3g.uliejh.cn/nnews/542972.htm
- http://m.3g.uliejh.cn/nnews/9873753.htm
- http://m.3g.uliejh.cn/nnews/5341091.htm
- http://m.3g.uliejh.cn/nnews/2674514.htm
- http://m.3g.uliejh.cn/nnews/0654943.htm
- http://m.3g.uliejh.cn/nnews/7424.htm
- http://m.3g.uliejh.cn/nnews/9290.htm
- http://m.3g.uliejh.cn/nnews/69062.htm
- http://m.3g.uliejh.cn/nnews/23442.htm
- http://m.3g.uliejh.cn/nnews/15389.htm
- http://m.3g.uliejh.cn/nnews/55207.htm
- http://m.3g.uliejh.cn/nnews/615392.htm
- http://m.3g.uliejh.cn/nnews/6938.htm
- http://m.3g.uliejh.cn/nnews/78944.htm
- http://m.3g.uliejh.cn/nnews/9014429.htm
- http://m.3g.uliejh.cn/nnews/03712.htm
- http://m.3g.uliejh.cn/nnews/18311.htm
- http://m.3g.uliejh.cn/nnews/88543.htm
- http://m.3g.uliejh.cn/nnews/81960.htm
- http://m.3g.uliejh.cn/nnews/4480299.htm
- http://m.3g.uliejh.cn/nnews/71667.htm
- http://m.3g.uliejh.cn/nnews/2290232.htm
- http://m.3g.uliejh.cn/nnews/5906621.htm
- http://m.3g.uliejh.cn/nnews/766416.htm
- http://m.3g.uliejh.cn/nnews/820289.htm
- http://m.3g.uliejh.cn/nnews/03533.htm
- http://m.3g.uliejh.cn/nnews/9622292.htm
- http://m.3g.uliejh.cn/nnews/6171.htm
- http://m.3g.uliejh.cn/nnews/815939.htm
- http://m.3g.uliejh.cn/nnews/5853988.htm
- http://m.3g.uliejh.cn/nnews/5050.htm
- http://m.3g.uliejh.cn/nnews/9686.htm
- http://m.3g.uliejh.cn/nnews/03467.htm
- http://m.3g.uliejh.cn/nnews/2035.htm
- http://m.3g.uliejh.cn/nnews/26224.htm
- http://m.3g.uliejh.cn/nnews/50201.htm
- http://m.3g.uliejh.cn/nnews/2654720.htm
- http://m.3g.uliejh.cn/nnews/6270.htm
- http://m.3g.uliejh.cn/nnews/848238.htm
- http://m.3g.uliejh.cn/nnews/7699.htm
- http://m.3g.uliejh.cn/nnews/035755.htm

## 项目结构

```
newslink-hub/
├── README.md                     # 项目说明文档（本文件）
├── LICENSE                       # MIT 许可证文件
├── requirements.txt              # Python 依赖清单
├── serve.py                      # 轻量级本地 HTTP 服务启动脚本
├── check_links.py                # 链接状态检查与报告生成脚本
├── export.py                     # 多格式导出工具（CSV/JSON/TXT）
├── config/
│   ├── settings.yaml             # 全局配置文件（端口、超时、重试次数）
│   └── batch_9.yaml              # 第 9 批次元数据（链接数、日期、来源域）
├── data/
│   ├── raw/
│   │   └── batch_9_urls.txt      # 第 9 批次原始 URL 列表（纯文本）
│   ├── reports/
│   │   └── status_report.json    # 链接状态检查结果输出目录
│   └── exports/
│       ├── batch_9.csv           # CSV 格式导出文件
│       └── batch_9.json          # JSON 格式导出文件
├── docs/
│   ├── user-guide.md             # 用户操作手册
│   ├── developer-guide.md        # 开发者扩展指南
│   ├── batch-9.md                # 第 9 批次详细说明
│   └── api-reference.md          # 本地 HTTP 服务 API 文档
├── tests/
│   ├── test_checker.py           # 链接检查模块单元测试
│   └── test_exporter.py          # 导出模块单元测试
└── scripts/
    ├── validate_urls.py          # URL 格式校验脚本
    └── generate_summary.py       # 生成批次统计摘要脚本
```

## 贡献指南

1. 在 GitHub 仓库中提交 Issue 说明您希望新增的功能或修复的问题，等待维护者确认后开始工作。

2. Fork 本仓库，在您的分支上按照项目代码风格进行修改，确保所有现有测试用例通过。新增功能需附带对应的单元测试。

3. 提交代码前运行 `scripts/validate_urls.py` 确保 URL 格式正确，并执行 `pytest tests/` 验证测试覆盖率不低于 80%。

4. 提交 Pull Request 时请参照 `docs/developer-guide.md` 中的提交信息模板，清晰描述变更内容、影响范围以及测试结果。

5. 若您希望新增一批 URL 资源，请按照 `config/batch_9.yaml` 的格式创建新的批次配置文件，并更新 `data/raw/` 目录下的对应 URL 列表文件。

## 常见问题

**问：如何检查所有链接的可用性？**

答：运行 `check_links.py` 脚本，加上 `--output` 参数指定报告输出路径。该脚本使用 `requests` 库发送 HEAD 请求，默认超时时间为 5 秒，失败或超时的链接会记录在报告中。您可以通过 `config/settings.yaml` 调整超时和重试次数。

**问：我能否将本项目用于商业采集项目？**

答：可以。本项目采用 MIT 许可证，您可以自由使用、修改、分发和商业化，但需保留原始许可证声明。请注意，本项目的 URL 指向第三方网站，采集时需遵守目标网站的 robots.txt 及服务条款。

**问：如何处理已失效的链接？**

答：`check_links.py` 运行后会生成 `status_report.json`，其中 `status` 字段标记为 `dead` 的链接即为失效链接。您可以将该报告中的失效链接导入 `data/reports/dead_urls.log`，并根据需要决定是否从清单中移除。项目不提供自动删除功能，以免意外移除重要资源。

## 许可证

MIT

> 外链数量: 250 | 生成时间: 2026-08-24 23:40:21
