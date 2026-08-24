# WebLink Catalog Aggregator

WebLink Catalog Aggregator 是一个面向技术文档整理、外链资源归集与批量 URL 治理的开源工具集。该项目定位于解决开发者在文档建设、知识库维护、网站迁移和 SEO 审计场景中面临的大量散乱链接难以结构化管理的痛点，提供从链接抓取、分类标注、状态检测到 Markdown 目录生成的全链路命令行解决方案。

目标用户包括技术文档工程师、开源项目维护者、知识库管理员、SEO 工程师以及需要定期整理浏览器收藏夹或书签库的开发者。项目不依赖图形界面，可在服务器或本地终端中直接运行，输出结果与 Git 工作流、静态站点生成器、CI/CD 流水线天然兼容。

## 功能概览

**批量链接导入与去重**：支持从纯文本文件、CSV、JSON 和浏览器书签 HTML 导出文件中批量导入 URL，自动识别并移除重复条目，保留首次出现顺序。

**递归域名聚类与分组**：依据 URL 的协议、主域名、子域名路径深度自动生成层级标签，支持按域名归属、文件类型、发布时间等维度进行二次归类。

**链接状态批量探测**：并发发送 HEAD 请求检测每个 URL 的可访问性，返回 HTTP 状态码、响应时间、重定向链长度和最终落地地址，支持超时与重试策略配置。

**Markdown 目录自动生成**：将结构化链接数据渲染为符合常见开源项目 README 风格的资源列表，支持自定义表格列、分组标题和注释字段，输出可直接粘贴至文档中使用。

**差量更新与变更追踪**：对比两次运行结果，输出新增、删除、状态变更的链接清单，便于在版本控制中追踪外链资源的演变历史。

**过滤规则引擎**：支持使用正则表达式或通配符模式对 URL 进行批量允许或拒绝过滤，可屏蔽特定域名、路径前缀或文件扩展名，适用于企业内网或内容安全策略。

**元数据提取与补全**：从 HTML 页面标题、meta description 和 Open Graph 标签中抽取页面描述信息，补充至链接清单的注释字段，减少手工录入工作量。

**多格式导出适配**：支持输出为 Markdown 列表、JSON 结构化数据、CSV 表格、HTML 目录页和纯文本清单，满足不同下游工具的数据消费需求。

## 应用场景

技术文档站点的外链生命周期管理：当项目文档中包含数百个外部参考链接时，使用本工具定期扫描所有链接的有效性，自动标记失效链接并生成报告，避免用户访问死链影响阅读体验。

浏览器书签库的迁移与清洗：用户从多个浏览器或设备导出书签 HTML 文件后，通过本工具合并去重、按域名分类、检测重复书签，最终生成一个经过整理的 Markdown 资源导航页，便于在团队内分享。

静态博客或 Hugo/VuePress 站点的友情链接维护：将友链页面中的 URL 列表导入工具，配置过滤规则屏蔽非技术类站点，自动提取每个站点的标题和描述，生成格式统一的友链表格，减少手工维护成本。

开源项目 README 中的资源附录生成：维护者将项目依赖的文档、教程、工具站、API 参考等链接整理为原始列表，由工具自动生成符合规范格式的「资源列表」章节，确保每个链接原样输出且无格式污染。

SEO 审计中的外链现状盘点：配合网站日志或爬虫结果，将网站引用的所有外部 URL 导入工具，分析域名分布、协议使用情况、状态码比例，为外链策略调整提供数据依据。

## 快速开始

以下命令可在 Linux、macOS 或 Windows WSL 环境中完成工具的克隆、安装与首次运行。

```bash
git clone https://github.com/webcat-io/weblink-catalog-aggregator.git
cd weblink-catalog-aggregator
pip install -r requirements.txt
python -m weblink_catalog.cli --input sample_links.txt --output catalog.md --format markdown
```

若使用 Docker 运行，可执行：

```bash
docker build -t weblink-catalog .
docker run --rm -v $(pwd)/data:/data weblink-catalog --input /data/links.txt --output /data/out.md
```

首次运行前建议修改配置文件 `config/default.yaml` 中的并发数、超时阈值和过滤规则。完成后可在输出目录中获取生成的 Markdown 文件及 JSON 格式的完整元数据备份。

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|---------|---------|------|
| Python | 3.9 及以上 | 核心运行环境，建议使用 3.11 或 3.12 以获得最佳性能 |
| requests | 2.31.0 及以上 | 用于发送 HTTP HEAD/GET 请求进行链接状态探测 |
| beautifulsoup4 | 4.12.0 及以上 | 解析 HTML 页面标题和 meta 标签，提取页面描述信息 |
| pandas | 2.0.0 及以上 | 处理 CSV 与 Excel 格式的链接数据导入和导出 |
| pyyaml | 6.0 及以上 | 读写 YAML 格式的配置文件与规则定义 |
| tqdm | 4.65.0 及以上 | 显示批量链接处理的进度条，提升终端交互体验 |
| lxml | 4.9.0 及以上 | 作为 beautifulsoup4 的解析器后备，提高 HTML 解析速度 |
| urllib3 | 2.0.0 及以上 | 底层连接池与重试机制，与 requests 协同工作 |

以上依赖可通过 `pip install -r requirements.txt` 一键完成安装。操作系统方面，项目已在 Ubuntu 22.04、macOS Ventura 及 Windows 11（WSL2 Ubuntu 环境）上通过测试。建议使用至少 2 GB 内存以支持高并发探测任务，磁盘空间需求小于 50 MB。

## 文档导航

| 层面 | 目录 | 回答的问题 |
|-----|------|-----------|
| 入门指南 | docs/getting-started.md | 如何安装、首次配置以及运行第一个链接导入任务 |
| 配置手册 | docs/configuration.md | 所有 YAML 配置项的含义、默认值和调优建议 |
| 过滤规则语法 | docs/filter-syntax.md | 正则表达式和通配符规则的写法，以及排除特定链接的示例 |
| 导出格式参考 | docs/output-formats.md | Markdown、JSON、CSV、HTML 各格式的字段说明与模板自定义 |
| 常见工作流 | docs/workflows.md | 定时检测、CI 集成、增量更新等典型使用场景的完整脚本 |
| API 接口 | docs/api-reference.md | 若以库模式导入时提供的公开函数、类和异常定义 |
| 故障排除 | docs/troubleshooting.md | 常见错误码含义、网络代理设置、SSL 证书处理等问题解决方案 |

文档按从浅入深的顺序组织，新用户建议从入门指南开始，阅读时间约 15 分钟即可完成首次跑通。

## 资源列表

- http://m.3g.uliejh.cn/nnews/128032.htm
- http://m.3g.uliejh.cn/nnews/95915.htm
- http://m.3g.uliejh.cn/nnews/5134.htm
- http://m.3g.uliejh.cn/nnews/22464.htm
- http://m.3g.uliejh.cn/nnews/10244.htm
- http://m.3g.uliejh.cn/nnews/6956121.htm
- http://m.3g.uliejh.cn/nnews/342122.htm
- http://m.3g.uliejh.cn/nnews/82970.htm
- http://m.3g.uliejh.cn/nnews/6602.htm
- http://m.3g.uliejh.cn/nnews/1665.htm
- http://m.3g.uliejh.cn/nnews/4928061.htm
- http://m.3g.uliejh.cn/nnews/3815.htm
- http://m.3g.uliejh.cn/nnews/23306.htm
- http://m.3g.uliejh.cn/nnews/5526173.htm
- http://m.3g.uliejh.cn/nnews/1762285.htm
- http://m.3g.uliejh.cn/nnews/11845.htm
- http://m.3g.uliejh.cn/nnews/58958.htm
- http://m.3g.uliejh.cn/nnews/8413013.htm
- http://m.3g.uliejh.cn/nnews/2282.htm
- http://m.3g.uliejh.cn/nnews/00721.htm
- http://m.3g.uliejh.cn/nnews/341881.htm
- http://m.3g.uliejh.cn/nnews/7310975.htm
- http://m.3g.uliejh.cn/nnews/9358151.htm
- http://m.3g.uliejh.cn/nnews/855578.htm
- http://m.3g.uliejh.cn/nnews/05386.htm
- http://m.3g.uliejh.cn/nnews/2101117.htm
- http://m.3g.uliejh.cn/nnews/211542.htm
- http://m.3g.uliejh.cn/nnews/862946.htm
- http://m.3g.uliejh.cn/nnews/4382896.htm
- http://m.3g.uliejh.cn/nnews/0830.htm
- http://m.3g.uliejh.cn/nnews/2064334.htm
- http://m.3g.uliejh.cn/nnews/0385.htm
- http://m.3g.uliejh.cn/nnews/235528.htm
- http://m.3g.uliejh.cn/nnews/457961.htm
- http://m.3g.uliejh.cn/nnews/559517.htm
- http://m.3g.uliejh.cn/nnews/195931.htm
- http://m.3g.uliejh.cn/nnews/577635.htm
- http://m.3g.uliejh.cn/nnews/2009.htm
- http://m.3g.uliejh.cn/nnews/6518099.htm
- http://m.3g.uliejh.cn/nnews/6263.htm
- http://m.3g.uliejh.cn/nnews/73407.htm
- http://m.3g.uliejh.cn/nnews/638041.htm
- http://m.3g.uliejh.cn/nnews/441161.htm
- http://m.3g.uliejh.cn/nnews/46085.htm
- http://m.3g.uliejh.cn/nnews/277794.htm
- http://m.3g.uliejh.cn/nnews/6120835.htm
- http://m.3g.uliejh.cn/nnews/850124.htm
- http://m.3g.uliejh.cn/nnews/59641.htm
- http://m.3g.uliejh.cn/nnews/711168.htm
- http://m.3g.uliejh.cn/nnews/395000.htm
- http://m.3g.uliejh.cn/nnews/782121.htm
- http://m.3g.uliejh.cn/nnews/568340.htm
- http://m.3g.uliejh.cn/nnews/9205.htm
- http://m.3g.uliejh.cn/nnews/9802.htm
- http://m.3g.uliejh.cn/nnews/625674.htm
- http://m.3g.uliejh.cn/nnews/7643.htm
- http://m.3g.uliejh.cn/nnews/3580.htm
- http://m.3g.uliejh.cn/nnews/1744.htm
- http://m.3g.uliejh.cn/nnews/133805.htm
- http://m.3g.uliejh.cn/nnews/2436525.htm
- http://m.3g.uliejh.cn/nnews/735497.htm
- http://m.3g.uliejh.cn/nnews/5342.htm
- http://m.3g.uliejh.cn/nnews/55908.htm
- http://m.3g.uliejh.cn/nnews/2477883.htm
- http://m.3g.uliejh.cn/nnews/76394.htm
- http://m.3g.uliejh.cn/nnews/834815.htm
- http://m.3g.uliejh.cn/nnews/445648.htm
- http://m.3g.uliejh.cn/nnews/4154609.htm
- http://m.3g.uliejh.cn/nnews/8210.htm
- http://m.3g.uliejh.cn/nnews/3998.htm
- http://m.3g.uliejh.cn/nnews/217357.htm
- http://m.3g.uliejh.cn/nnews/590691.htm
- http://m.3g.uliejh.cn/nnews/9977.htm
- http://m.3g.uliejh.cn/nnews/5975.htm
- http://m.3g.uliejh.cn/nnews/716825.htm
- http://m.3g.uliejh.cn/nnews/7828072.htm
- http://m.3g.uliejh.cn/nnews/35809.htm
- http://m.3g.uliejh.cn/nnews/3742.htm
- http://m.3g.uliejh.cn/nnews/3084681.htm
- http://m.3g.uliejh.cn/nnews/73630.htm
- http://m.3g.uliejh.cn/nnews/57103.htm
- http://m.3g.uliejh.cn/nnews/49541.htm
- http://m.3g.uliejh.cn/nnews/406507.htm
- http://m.3g.uliejh.cn/nnews/0434557.htm
- http://m.3g.uliejh.cn/nnews/2529764.htm
- http://m.3g.uliejh.cn/nnews/686792.htm
- http://m.3g.uliejh.cn/nnews/1364.htm
- http://m.3g.uliejh.cn/nnews/0751412.htm
- http://m.3g.uliejh.cn/nnews/8580929.htm
- http://m.3g.uliejh.cn/nnews/8047680.htm
- http://m.3g.uliejh.cn/nnews/2143518.htm
- http://m.3g.uliejh.cn/nnews/2071.htm
- http://m.3g.uliejh.cn/nnews/12458.htm
- http://m.3g.uliejh.cn/nnews/784535.htm
- http://m.3g.uliejh.cn/nnews/2714432.htm
- http://m.3g.uliejh.cn/nnews/9927806.htm
- http://m.3g.uliejh.cn/nnews/473533.htm
- http://m.3g.uliejh.cn/nnews/8961.htm
- http://m.3g.uliejh.cn/nnews/076773.htm
- http://m.3g.uliejh.cn/nnews/35008.htm
- http://m.3g.uliejh.cn/nnews/1486644.htm
- http://m.3g.uliejh.cn/nnews/3275.htm
- http://m.3g.uliejh.cn/nnews/721639.htm
- http://m.3g.uliejh.cn/nnews/5738621.htm
- http://m.3g.uliejh.cn/nnews/9567253.htm
- http://m.3g.uliejh.cn/nnews/044763.htm
- http://m.3g.uliejh.cn/nnews/0079595.htm
- http://m.3g.uliejh.cn/nnews/888168.htm
- http://m.3g.uliejh.cn/nnews/927092.htm
- http://m.3g.uliejh.cn/nnews/14243.htm
- http://m.3g.uliejh.cn/nnews/89313.htm
- http://m.3g.uliejh.cn/nnews/515905.htm
- http://m.3g.uliejh.cn/nnews/8582883.htm
- http://m.3g.uliejh.cn/nnews/233644.htm
- http://m.3g.uliejh.cn/nnews/616141.htm
- http://m.3g.uliejh.cn/nnews/525657.htm
- http://m.3g.uliejh.cn/nnews/223164.htm
- http://m.3g.uliejh.cn/nnews/563259.htm
- http://m.3g.uliejh.cn/nnews/42171.htm
- http://m.3g.uliejh.cn/nnews/80005.htm
- http://m.3g.uliejh.cn/nnews/894006.htm
- http://m.3g.uliejh.cn/nnews/767470.htm
- http://m.3g.uliejh.cn/nnews/64818.htm
- http://m.3g.uliejh.cn/nnews/3396.htm
- http://m.3g.uliejh.cn/nnews/9854919.htm
- http://m.3g.uliejh.cn/nnews/5641.htm
- http://m.3g.uliejh.cn/nnews/418095.htm
- http://m.3g.uliejh.cn/nnews/0973.htm
- http://m.3g.uliejh.cn/nnews/85506.htm
- http://m.3g.uliejh.cn/nnews/0143233.htm
- http://m.3g.uliejh.cn/nnews/18403.htm
- http://m.3g.uliejh.cn/nnews/888868.htm
- http://m.3g.uliejh.cn/nnews/63050.htm
- http://m.3g.uliejh.cn/nnews/0954.htm
- http://m.3g.uliejh.cn/nnews/0288085.htm
- http://m.3g.uliejh.cn/nnews/785276.htm
- http://m.3g.uliejh.cn/nnews/1384637.htm
- http://m.3g.uliejh.cn/nnews/6974757.htm
- http://m.3g.uliejh.cn/nnews/37762.htm
- http://m.3g.uliejh.cn/nnews/4244.htm
- http://m.3g.uliejh.cn/nnews/792156.htm
- http://m.3g.uliejh.cn/nnews/2531.htm
- http://m.3g.uliejh.cn/nnews/273632.htm
- http://m.3g.uliejh.cn/nnews/5269957.htm
- http://m.3g.uliejh.cn/nnews/31780.htm
- http://m.3g.uliejh.cn/nnews/9578.htm
- http://m.3g.uliejh.cn/nnews/519196.htm
- http://m.3g.uliejh.cn/nnews/881288.htm
- http://m.3g.uliejh.cn/nnews/8820.htm
- http://m.3g.uliejh.cn/nnews/55278.htm
- http://m.3g.uliejh.cn/nnews/041880.htm
- http://m.3g.uliejh.cn/nnews/4445.htm
- http://m.3g.uliejh.cn/nnews/2297170.htm
- http://m.3g.uliejh.cn/nnews/4940452.htm
- http://m.3g.uliejh.cn/nnews/3000.htm
- http://m.3g.uliejh.cn/nnews/69420.htm
- http://m.3g.uliejh.cn/nnews/84698.htm
- http://m.3g.uliejh.cn/nnews/686873.htm
- http://m.3g.uliejh.cn/nnews/41518.htm
- http://m.3g.uliejh.cn/nnews/982676.htm
- http://m.3g.uliejh.cn/nnews/1368.htm
- http://m.3g.uliejh.cn/nnews/4757.htm
- http://m.3g.uliejh.cn/nnews/5701383.htm
- http://m.3g.uliejh.cn/nnews/8869294.htm
- http://m.3g.uliejh.cn/nnews/468304.htm
- http://m.3g.uliejh.cn/nnews/7906.htm
- http://m.3g.uliejh.cn/nnews/669721.htm
- http://m.3g.uliejh.cn/nnews/2053628.htm
- http://m.3g.uliejh.cn/nnews/05475.htm
- http://m.3g.uliejh.cn/nnews/4026041.htm
- http://m.3g.uliejh.cn/nnews/4868085.htm
- http://m.3g.uliejh.cn/nnews/4357260.htm
- http://m.3g.uliejh.cn/nnews/1112294.htm
- http://m.3g.uliejh.cn/nnews/4749865.htm
- http://m.3g.uliejh.cn/nnews/9363497.htm
- http://m.3g.uliejh.cn/nnews/8061.htm
- http://m.3g.uliejh.cn/nnews/1636.htm
- http://m.3g.uliejh.cn/nnews/7214152.htm
- http://m.3g.uliejh.cn/nnews/2324200.htm
- http://m.3g.uliejh.cn/nnews/6598.htm
- http://m.3g.uliejh.cn/nnews/145957.htm
- http://m.3g.uliejh.cn/nnews/3023099.htm
- http://m.3g.uliejh.cn/nnews/0731173.htm
- http://m.3g.uliejh.cn/nnews/291947.htm
- http://m.3g.uliejh.cn/nnews/65097.htm
- http://m.3g.uliejh.cn/nnews/247880.htm
- http://m.3g.uliejh.cn/nnews/22722.htm
- http://m.3g.uliejh.cn/nnews/30533.htm
- http://m.3g.uliejh.cn/nnews/1548163.htm
- http://m.3g.uliejh.cn/nnews/0923950.htm
- http://m.3g.uliejh.cn/nnews/66243.htm
- http://m.3g.uliejh.cn/nnews/62758.htm
- http://m.3g.uliejh.cn/nnews/2124932.htm
- http://m.3g.uliejh.cn/nnews/4706755.htm
- http://m.3g.uliejh.cn/nnews/657350.htm
- http://m.3g.uliejh.cn/nnews/1040656.htm
- http://m.3g.uliejh.cn/nnews/210828.htm
- http://m.3g.uliejh.cn/nnews/7434573.htm
- http://m.3g.uliejh.cn/nnews/27996.htm
- http://m.3g.uliejh.cn/nnews/6126090.htm
- http://m.3g.uliejh.cn/nnews/2857.htm
- http://m.3g.uliejh.cn/nnews/717320.htm
- http://m.3g.uliejh.cn/nnews/11738.htm
- http://m.3g.uliejh.cn/nnews/769987.htm
- http://m.3g.uliejh.cn/nnews/285943.htm
- http://m.3g.uliejh.cn/nnews/297206.htm
- http://m.3g.uliejh.cn/nnews/0054966.htm
- http://m.3g.uliejh.cn/nnews/4642.htm
- http://m.3g.uliejh.cn/nnews/76507.htm
- http://m.3g.uliejh.cn/nnews/304196.htm
- http://m.3g.uliejh.cn/nnews/50598.htm
- http://m.3g.uliejh.cn/nnews/2430.htm
- http://m.3g.uliejh.cn/nnews/81529.htm
- http://m.3g.uliejh.cn/nnews/36384.htm
- http://m.3g.uliejh.cn/nnews/4770072.htm
- http://m.3g.uliejh.cn/nnews/21708.htm
- http://m.3g.uliejh.cn/nnews/5215480.htm
- http://m.3g.uliejh.cn/nnews/6477.htm
- http://m.3g.uliejh.cn/nnews/51266.htm
- http://m.3g.uliejh.cn/nnews/69354.htm
- http://m.3g.uliejh.cn/nnews/816160.htm
- http://m.3g.uliejh.cn/nnews/388457.htm
- http://m.3g.uliejh.cn/nnews/0750.htm
- http://m.3g.uliejh.cn/nnews/1992466.htm
- http://m.3g.uliejh.cn/nnews/070903.htm
- http://m.3g.uliejh.cn/nnews/52272.htm
- http://m.3g.uliejh.cn/nnews/6501.htm
- http://m.3g.uliejh.cn/nnews/553316.htm
- http://m.3g.uliejh.cn/nnews/722855.htm
- http://m.3g.uliejh.cn/nnews/5645.htm
- http://m.3g.uliejh.cn/nnews/484564.htm
- http://m.3g.uliejh.cn/nnews/32815.htm
- http://m.3g.uliejh.cn/nnews/69026.htm
- http://m.3g.uliejh.cn/nnews/3553.htm
- http://m.3g.uliejh.cn/nnews/18156.htm
- http://m.3g.uliejh.cn/nnews/3553725.htm
- http://m.3g.uliejh.cn/nnews/924722.htm
- http://m.3g.uliejh.cn/nnews/57287.htm
- http://m.3g.uliejh.cn/nnews/3826937.htm
- http://m.3g.uliejh.cn/nnews/9528162.htm
- http://m.3g.uliejh.cn/nnews/6534686.htm
- http://m.3g.uliejh.cn/nnews/751002.htm
- http://m.3g.uliejh.cn/nnews/96481.htm
- http://m.3g.uliejh.cn/nnews/972094.htm
- http://m.3g.uliejh.cn/nnews/36505.htm
- http://m.3g.uliejh.cn/nnews/7876425.htm
- http://m.3g.uliejh.cn/nnews/75310.htm
- http://m.3g.uliejh.cn/nnews/480241.htm
- http://m.3g.uliejh.cn/nnews/6860365.htm
- http://m.3g.uliejh.cn/nnews/6885355.htm

## 项目结构

```
weblink-catalog-aggregator/
├── weblink_catalog/                 # 核心 Python 包
│   ├── __init__.py                  # 包版本与导出声明
│   ├── cli.py                       # 命令行入口，解析参数并调度任务
│   ├── config.py                    # 配置加载器，合并默认与用户配置
│   ├── exceptions.py                # 自定义异常类（配置错误、网络超时等）
│   ├── link_loader/                 # 链接导入子模块
│   │   ├── __init__.py
│   │   ├── file_parser.py           # 解析 txt, csv, json, html 书签
│   │   └── deduplicator.py          # 基于哈希和规则的去重逻辑
│   ├── probe/                       # 链接探测子模块
│   │   ├── __init__.py
│   │   ├── http_client.py           # 封装 requests 会话与重试策略
│   │   ├── status_checker.py        # 并发执行 HEAD 请求，收集状态码
│   │   └── meta_extractor.py        # 从响应体中解析 title/description
│   ├── filter/                      # 过滤规则引擎
│   │   ├── __init__.py
│   │   ├── rule_compiler.py         # 编译正则与通配符为匹配函数
│   │   └── policy.py                # 允许/拒绝策略的评估流水线
│   ├── aggregator/                  # 聚类与分组逻辑
│   │   ├── __init__.py
│   │   ├── domain_cluster.py        # 按注册域名和路径深度分组
│   │   └── tag_generator.py         # 根据协议、文件类型生成标签
│   ├── renderer/                    # 输出渲染子模块
│   │   ├── __init__.py
│   │   ├── markdown.py              # 生成 Markdown 列表与表格
│   │   ├── json_exporter.py         # 导出完整结构化 JSON
│   │   ├── csv_writer.py            # 写入 CSV 格式
│   │   └── html_template.py         # 生成可浏览的 HTML 目录页
│   └── utils/                       # 通用工具函数
│       ├── __init__.py
│       ├── logger.py                # 日志配置与分级输出
│       └── timer.py                 # 运行耗时统计与进度条包装
├── config/                          # 配置目录
│   ├── default.yaml                 # 默认配置（并发数 50，超时 10s）
│   └── example.custom.yaml          # 用户自定义配置示例
├── tests/                           # 单元测试与集成测试
│   ├── test_loader.py
│   ├── test_probe.py
│   ├── test_filter.py
│   └── fixtures/                    # 测试用的样例输入文件
│       ├── sample_links.txt
│       └── bookmarks_export.html
├── docs/                            # 完整文档源码
│   ├── getting-started.md
│   ├── configuration.md
│   ├── filter-syntax.md
│   ├── output-formats.md
│   ├── workflows.md
│   ├── api-reference.md
│   └── troubleshooting.md
├── scripts/                         # 运维脚本
│   ├── ci_run.sh                    # CI 中执行全量测试
│   └── docker_entrypoint.sh         # Docker 容器入口脚本
├── .github/                         # GitHub Actions 工作流
│   └── workflows/
│       └── test_and_publish.yml
├── requirements.txt                 # 生产依赖
├── requirements-dev.txt             # 开发与测试额外依赖
├── setup.py                         # 安装打包配置
├── README.md                        # 本文件
└── LICENSE                          # MIT 许可证文本
```

## 贡献指南

1. 在 GitHub 仓库中 fork 项目到个人账户，然后 clone 到本地开发环境。建议使用 Python 3.11 及以上版本，并创建独立的虚拟环境来隔离依赖。

2. 安装开发依赖包，运行测试套件确保当前主分支全部通过。新增功能或修复缺陷时，需在 tests 目录下补充对应的测试用例，覆盖率为 90% 以上。

3. 提交变更前请执行代码格式化工具 black 和 isort，并运行 flake8 进行风格检查。所有函数和类必须包含 docstring，复杂逻辑处添加行内注释。

4. 提交 pull request 时，请描述变更动机、实现方案以及是否影响现有配置或输出格式。若涉及新增依赖，需在 requirements.txt 和 setup.py 中同步更新并说明必要性。

5. 文档类贡献可直接修改 docs 目录下的 Markdown 文件，中文内容遵循 中文文案排版指北 的基本规范，英文与数字前后保留一个空格。

## 常见问题

问：探测过程中大量链接返回超时或 SSL 错误，应该如何处理？

答：首先检查网络环境是否可正常访问目标域名，必要时配置代理。其次在 config/default.yaml 中调高 timeout 值（例如 15 秒）和重试次数（例如 3 次）。对于 SSL 证书验证失败的情况，可在配置中设置 verify_ssl: false（不推荐在生产环境使用）。若仍存在大量超时，可降低并发数 max_workers 至 10 或 5。

问：导入的链接中混杂了非技术类站点或广告域名，如何批量过滤？

答：在配置文件的 filter 段落中添加 deny 规则，支持正则表达式。例如屏蔽包含 "adservice" 或 "doubleclick" 的 URL，可设置 pattern: .*(adservice|doubleclick).* 。也支持按顶级域名批量屏蔽，如 pattern: .*\.(ru|cn)$ 会拒绝所有俄语和中文国家顶级域名的链接（请根据实际需求调整）。

问：生成的 Markdown 列表中，每个链接都带有编号或额外符号，如何只保留纯 URL 列表？

答：在输出配置中将 markdown.bullet_style 设为 "plain"，将 add_index 设为 false，并将 wrap_with_tag 设为 false。此外也可以选择输出为 JSON 或 CSV 格式，再自行转换为所需的纯文本形式。具体字段说明请参考 docs/output-formats.md 中的渲染参数章节。

## 许可证

MIT

> 外链数量: 250 | 生成时间: 2026-08-24 23:40:21
