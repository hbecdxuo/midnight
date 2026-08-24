# LinkVault Resource Aggregator

LinkVault is a lightweight, schema-agnostic resource indexing and navigation system designed for developers, technical researchers, and content curators who need to manage large volumes of external hyperlinks with minimal overhead. The project addresses the common problem of link rot, disorganized bookmarks, and the lack of machine-readable metadata in plain HTML bookmark files. LinkVault provides a structured, version-controlled, and queryable repository of categorized external resources, enabling users to maintain a durable, self-documenting collection of references that can be integrated into CI/CD pipelines, documentation generators, or personal knowledge bases. This project is particularly suited for open-source maintainers who need to track dependencies, technical writers who manage reference lists, and researchers who collect large corpora of web-based sources across multiple batches.

The current release, Batch 32 of 120, comprises 250 curated resource links focused on news, technical bulletins, and reference materials sourced from the uliejh.cn domain. LinkVault does not host or proxy content; it provides a normalized index with validation hooks, duplicate detection, and availability checking to ensure that every entry remains accessible and accurately represented. The system is built with extensibility in mind, supporting custom tag schemas, expiration policies, and export filters for JSON, YAML, and Markdown output formats.

## 功能概览

- **批量资源导入**：支持从 CSV、JSON Lines 和 plaintext 清单批量导入 URL，自动解析查询参数并提取域名、路径深度、文件扩展名等结构性特征。

- **链接可用性探测**：内置异步 HTTP 健康检查器，支持 HEAD 和 GET 请求，可配置超时、重试策略和状态码白名单，定期生成可用性报告。

- **元数据标签系统**：每个资源可附加自由标签、优先级标记和分类注释，支持按标签组合进行布尔过滤和全文检索。

- **版本化变更追踪**：所有资源条目的增删改操作均记录时间戳和操作哈希，支持回滚至任意历史快照，便于审计和协作。

- **多格式导出管道**：提供 Markdown 列表、HTML 目录页、JSON API 端点以及 sitemap.xml 生成器，适配静态站点生成器和文档框架。

- **资源关系图谱**：基于共享域名、路径前缀和引用频率构建轻量级关联图，输出 Graphviz DOT 格式，帮助用户发现隐性连接。

- **定时巡检与通知**：可配置 cron 表达式执行周期性检查，当链接失效或响应时间超过阈值时，通过 Webhook 或日志输出告警。

- **去重与规范化引擎**：自动识别 URL 编码差异、尾部斜杠、协议变体（http/https）及常见跟踪参数，合并重复条目并保留首次出现时间。

## 应用场景

**技术文档库维护**：技术写作团队在维护 API 文档或教程时，需要引用大量外部规范、博客和工具站。LinkVault 可作为官方参考列表的后端，每次构建文档时自动验证所有引用链接，避免发布后出现死链，同时支持按模块导出相关资源到特定章节。

**开源项目依赖追踪**：开源项目通常依赖多个第三方服务、镜像源和补丁站点。维护者可使用 LinkVault 记录每个依赖项的官方地址、备用地址和归档链接，通过定时巡检及时发现域名过期或证书变更，减少因外部资源不可用导致的构建失败。

**研究数据管理**：科研人员在文献综述或数据采集阶段会收集数百个数据源、统计门户和新闻聚合页。LinkVault 为每个资源提供稳定的本地标识符，支持批注阅读状态和重要性评分，并能将资源列表直接导出为论文附录或数据集说明文件。

**个人知识库外链整理**：知识管理爱好者使用 Obsidian、Notion 或 Logseq 时，常遇到链接散落、格式混乱的问题。LinkVault 提供标准化的导入导出接口，可将零散书签整合为结构化仓库，配合标签系统实现按主题、项目或时效性分类检索。

**运营监控仪表盘**：运维团队可将内部监控面板、日志查看器和报警管理页的 URL 集中托管于 LinkVault，利用可用性探测功能快速定位故障入口，结合关系图谱分析服务依赖链，辅助故障根因定位。

## 快速开始

以下命令演示了如何获取 LinkVault 源代码、安装依赖并启动本地开发服务器。请确保系统已安装 Git 和 Node.js 18.0 及以上版本。

```bash
git clone https://github.com/linkvault/linkvault-core.git
cd linkvault-core
npm install --production=false
npm run build
npm run dev
```

执行完毕后，访问控制台输出的本地地址（默认为 http://localhost:5173 ）即可进入资源管理面板。首次启动会自动创建内存数据库并加载示例数据。若需持久化存储，请参考配置章节设置 SQLite 或 PostgreSQL 连接字符串。

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|---------|---------|------|
| Node.js | 18.0.0 或更高 | 运行时环境，推荐使用 LTS 版本 |
| npm | 8.0.0 或更高 | 包管理器，用于安装第三方库 |
| SQLite3 | 3.35.0 或更高 | 默认轻量级数据库，生产环境可换为 PostgreSQL |
| Git | 2.25.0 或更高 | 版本控制，用于克隆仓库和提交变更 |
| curl | 7.68.0 或更高 | 用于外部链接健康检查的可选命令行工具 |
| OpenSSL | 1.1.1 或更高 | 用于生成操作哈希和签名验证 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|-----|------|----------|
| 入门指南 | docs/getting-started.md | 如何安装、配置首次运行、导入第一批资源？ |
| 操作手册 | docs/usage/import-export.md | 支持哪些导入格式？如何导出为不同模板？标签系统如何使用？ |
| 运维参考 | docs/administration/health-checks.md | 如何调整超时参数？如何配置 Webhook 告警？巡检日志存在哪里？ |
| 架构设计 | docs/architecture/data-model.md | 数据库表结构如何设计？资源关系图如何构建？扩展点在哪里？ |

## 资源列表

- http://m.3g.uliejh.cn/nnews/9375077.htm
- http://m.3g.uliejh.cn/nnews/6593.htm
- http://m.3g.uliejh.cn/nnews/54056.htm
- http://m.3g.uliejh.cn/nnews/105766.htm
- http://m.3g.uliejh.cn/nnews/4516.htm
- http://m.3g.uliejh.cn/nnews/04839.htm
- http://m.3g.uliejh.cn/nnews/40774.htm
- http://m.3g.uliejh.cn/nnews/0795306.htm
- http://m.3g.uliejh.cn/nnews/4705832.htm
- http://m.3g.uliejh.cn/nnews/48119.htm
- http://m.3g.uliejh.cn/nnews/232460.htm
- http://m.3g.uliejh.cn/nnews/4947532.htm
- http://m.3g.uliejh.cn/nnews/2123761.htm
- http://m.3g.uliejh.cn/nnews/5771858.htm
- http://m.3g.uliejh.cn/nnews/7152.htm
- http://m.3g.uliejh.cn/nnews/4820613.htm
- http://m.3g.uliejh.cn/nnews/20434.htm
- http://m.3g.uliejh.cn/nnews/49620.htm
- http://m.3g.uliejh.cn/nnews/88941.htm
- http://m.3g.uliejh.cn/nnews/78014.htm
- http://m.3g.uliejh.cn/nnews/941293.htm
- http://m.3g.uliejh.cn/nnews/3515.htm
- http://m.3g.uliejh.cn/nnews/44315.htm
- http://m.3g.uliejh.cn/nnews/63749.htm
- http://m.3g.uliejh.cn/nnews/0730.htm
- http://m.3g.uliejh.cn/nnews/9129103.htm
- http://m.3g.uliejh.cn/nnews/948017.htm
- http://m.3g.uliejh.cn/nnews/4463.htm
- http://m.3g.uliejh.cn/nnews/53858.htm
- http://m.3g.uliejh.cn/nnews/009962.htm
- http://m.3g.uliejh.cn/nnews/6230.htm
- http://m.3g.uliejh.cn/nnews/85218.htm
- http://m.3g.uliejh.cn/nnews/9334874.htm
- http://m.3g.uliejh.cn/nnews/3149.htm
- http://m.3g.uliejh.cn/nnews/959598.htm
- http://m.3g.uliejh.cn/nnews/461670.htm
- http://m.3g.uliejh.cn/nnews/32923.htm
- http://m.3g.uliejh.cn/nnews/01357.htm
- http://m.3g.uliejh.cn/nnews/4615178.htm
- http://m.3g.uliejh.cn/nnews/6646.htm
- http://m.3g.uliejh.cn/nnews/3949.htm
- http://m.3g.uliejh.cn/nnews/0048484.htm
- http://m.3g.uliejh.cn/nnews/8715638.htm
- http://m.3g.uliejh.cn/nnews/69645.htm
- http://m.3g.uliejh.cn/nnews/0699695.htm
- http://m.3g.uliejh.cn/nnews/5599145.htm
- http://m.3g.uliejh.cn/nnews/4559627.htm
- http://m.3g.uliejh.cn/nnews/2299534.htm
- http://m.3g.uliejh.cn/nnews/52621.htm
- http://m.3g.uliejh.cn/nnews/24259.htm
- http://m.3g.uliejh.cn/nnews/13646.htm
- http://m.3g.uliejh.cn/nnews/517406.htm
- http://m.3g.uliejh.cn/nnews/356346.htm
- http://m.3g.uliejh.cn/nnews/3889.htm
- http://m.3g.uliejh.cn/nnews/7510992.htm
- http://m.3g.uliejh.cn/nnews/1694608.htm
- http://m.3g.uliejh.cn/nnews/8580.htm
- http://m.3g.uliejh.cn/nnews/08905.htm
- http://m.3g.uliejh.cn/nnews/5054.htm
- http://m.3g.uliejh.cn/nnews/7430903.htm
- http://m.3g.uliejh.cn/nnews/2495.htm
- http://m.3g.uliejh.cn/nnews/26359.htm
- http://m.3g.uliejh.cn/nnews/9751.htm
- http://m.3g.uliejh.cn/nnews/911615.htm
- http://m.3g.uliejh.cn/nnews/24226.htm
- http://m.3g.uliejh.cn/nnews/5238283.htm
- http://m.3g.uliejh.cn/nnews/8630926.htm
- http://m.3g.uliejh.cn/nnews/886420.htm
- http://m.3g.uliejh.cn/nnews/725299.htm
- http://m.3g.uliejh.cn/nnews/02251.htm
- http://m.3g.uliejh.cn/nnews/282197.htm
- http://m.3g.uliejh.cn/nnews/810292.htm
- http://m.3g.uliejh.cn/nnews/1605495.htm
- http://m.3g.uliejh.cn/nnews/7082847.htm
- http://m.3g.uliejh.cn/nnews/4846525.htm
- http://m.3g.uliejh.cn/nnews/005176.htm
- http://m.3g.uliejh.cn/nnews/88603.htm
- http://m.3g.uliejh.cn/nnews/8870390.htm
- http://m.3g.uliejh.cn/nnews/30811.htm
- http://m.3g.uliejh.cn/nnews/1826964.htm
- http://m.3g.uliejh.cn/nnews/0200.htm
- http://m.3g.uliejh.cn/nnews/205941.htm
- http://m.3g.uliejh.cn/nnews/9185211.htm
- http://m.3g.uliejh.cn/nnews/2848.htm
- http://m.3g.uliejh.cn/nnews/0526983.htm
- http://m.3g.uliejh.cn/nnews/0211886.htm
- http://m.3g.uliejh.cn/nnews/153421.htm
- http://m.3g.uliejh.cn/nnews/54244.htm
- http://m.3g.uliejh.cn/nnews/9530.htm
- http://m.3g.uliejh.cn/nnews/96580.htm
- http://m.3g.uliejh.cn/nnews/929744.htm
- http://m.3g.uliejh.cn/nnews/6479.htm
- http://m.3g.uliejh.cn/nnews/11768.htm
- http://m.3g.uliejh.cn/nnews/630748.htm
- http://m.3g.uliejh.cn/nnews/36679.htm
- http://m.3g.uliejh.cn/nnews/0604.htm
- http://m.3g.uliejh.cn/nnews/55595.htm
- http://m.3g.uliejh.cn/nnews/48122.htm
- http://m.3g.uliejh.cn/nnews/3719.htm
- http://m.3g.uliejh.cn/nnews/7227270.htm
- http://m.3g.uliejh.cn/nnews/8260.htm
- http://m.3g.uliejh.cn/nnews/359080.htm
- http://m.3g.uliejh.cn/nnews/90474.htm
- http://m.3g.uliejh.cn/nnews/9822449.htm
- http://m.3g.uliejh.cn/nnews/45792.htm
- http://m.3g.uliejh.cn/nnews/229927.htm
- http://m.3g.uliejh.cn/nnews/11924.htm
- http://m.3g.uliejh.cn/nnews/03176.htm
- http://m.3g.uliejh.cn/nnews/3301622.htm
- http://m.3g.uliejh.cn/nnews/5524.htm
- http://m.3g.uliejh.cn/nnews/6352633.htm
- http://m.3g.uliejh.cn/nnews/150534.htm
- http://m.3g.uliejh.cn/nnews/0708754.htm
- http://m.3g.uliejh.cn/nnews/5869.htm
- http://m.3g.uliejh.cn/nnews/5668.htm
- http://m.3g.uliejh.cn/nnews/3163.htm
- http://m.3g.uliejh.cn/nnews/55833.htm
- http://m.3g.uliejh.cn/nnews/310139.htm
- http://m.3g.uliejh.cn/nnews/57221.htm
- http://m.3g.uliejh.cn/nnews/719909.htm
- http://m.3g.uliejh.cn/nnews/1641657.htm
- http://m.3g.uliejh.cn/nnews/9850271.htm
- http://m.3g.uliejh.cn/nnews/9932040.htm
- http://m.3g.uliejh.cn/nnews/0103.htm
- http://m.3g.uliejh.cn/nnews/7836.htm
- http://m.3g.uliejh.cn/nnews/313982.htm
- http://m.3g.uliejh.cn/nnews/0374.htm
- http://m.3g.uliejh.cn/nnews/7837.htm
- http://m.3g.uliejh.cn/nnews/676202.htm
- http://m.3g.uliejh.cn/nnews/36513.htm
- http://m.3g.uliejh.cn/nnews/5832.htm
- http://m.3g.uliejh.cn/nnews/04476.htm
- http://m.3g.uliejh.cn/nnews/14227.htm
- http://m.3g.uliejh.cn/nnews/0083220.htm
- http://m.3g.uliejh.cn/nnews/0108184.htm
- http://m.3g.uliejh.cn/nnews/77916.htm
- http://m.3g.uliejh.cn/nnews/1359449.htm
- http://m.3g.uliejh.cn/nnews/7129467.htm
- http://m.3g.uliejh.cn/nnews/5933.htm
- http://m.3g.uliejh.cn/nnews/2097.htm
- http://m.3g.uliejh.cn/nnews/6570237.htm
- http://m.3g.uliejh.cn/nnews/5907.htm
- http://m.3g.uliejh.cn/nnews/0052500.htm
- http://m.3g.uliejh.cn/nnews/9930497.htm
- http://m.3g.uliejh.cn/nnews/358302.htm
- http://m.3g.uliejh.cn/nnews/85379.htm
- http://m.3g.uliejh.cn/nnews/4448715.htm
- http://m.3g.uliejh.cn/nnews/8593460.htm
- http://m.3g.uliejh.cn/nnews/69475.htm
- http://m.3g.uliejh.cn/nnews/511733.htm
- http://m.3g.uliejh.cn/nnews/16926.htm
- http://m.3g.uliejh.cn/nnews/2030777.htm
- http://m.3g.uliejh.cn/nnews/176574.htm
- http://m.3g.uliejh.cn/nnews/1943.htm
- http://m.3g.uliejh.cn/nnews/4307.htm
- http://m.3g.uliejh.cn/nnews/1459.htm
- http://m.3g.uliejh.cn/nnews/5051.htm
- http://m.3g.uliejh.cn/nnews/9679.htm
- http://m.3g.uliejh.cn/nnews/3845.htm
- http://m.3g.uliejh.cn/nnews/32956.htm
- http://m.3g.uliejh.cn/nnews/38765.htm
- http://m.3g.uliejh.cn/nnews/360076.htm
- http://m.3g.uliejh.cn/nnews/2868.htm
- http://m.3g.uliejh.cn/nnews/735391.htm
- http://m.3g.uliejh.cn/nnews/2796.htm
- http://m.3g.uliejh.cn/nnews/7547163.htm
- http://m.3g.uliejh.cn/nnews/825138.htm
- http://m.3g.uliejh.cn/nnews/44488.htm
- http://m.3g.uliejh.cn/nnews/213049.htm
- http://m.3g.uliejh.cn/nnews/596063.htm
- http://m.3g.uliejh.cn/nnews/250923.htm
- http://m.3g.uliejh.cn/nnews/417371.htm
- http://m.3g.uliejh.cn/nnews/3968129.htm
- http://m.3g.uliejh.cn/nnews/8788186.htm
- http://m.3g.uliejh.cn/nnews/1294643.htm
- http://m.3g.uliejh.cn/nnews/8000.htm
- http://m.3g.uliejh.cn/nnews/7972.htm
- http://m.3g.uliejh.cn/nnews/0360940.htm
- http://m.3g.uliejh.cn/nnews/3961164.htm
- http://m.3g.uliejh.cn/nnews/5254787.htm
- http://m.3g.uliejh.cn/nnews/09684.htm
- http://m.3g.uliejh.cn/nnews/2919520.htm
- http://m.3g.uliejh.cn/nnews/6171732.htm
- http://m.3g.uliejh.cn/nnews/94541.htm
- http://m.3g.uliejh.cn/nnews/033466.htm
- http://m.3g.uliejh.cn/nnews/84320.htm
- http://m.3g.uliejh.cn/nnews/145079.htm
- http://m.3g.uliejh.cn/nnews/9758618.htm
- http://m.3g.uliejh.cn/nnews/1494.htm
- http://m.3g.uliejh.cn/nnews/6560703.htm
- http://m.3g.uliejh.cn/nnews/68544.htm
- http://m.3g.uliejh.cn/nnews/5434936.htm
- http://m.3g.uliejh.cn/nnews/53867.htm
- http://m.3g.uliejh.cn/nnews/4320.htm
- http://m.3g.uliejh.cn/nnews/77859.htm
- http://m.3g.uliejh.cn/nnews/7378.htm
- http://m.3g.uliejh.cn/nnews/4265.htm
- http://m.3g.uliejh.cn/nnews/8491.htm
- http://m.3g.uliejh.cn/nnews/42571.htm
- http://m.3g.uliejh.cn/nnews/38865.htm
- http://m.3g.uliejh.cn/nnews/2268720.htm
- http://m.3g.uliejh.cn/nnews/8150306.htm
- http://m.3g.uliejh.cn/nnews/2706753.htm
- http://m.3g.uliejh.cn/nnews/3853140.htm
- http://m.3g.uliejh.cn/nnews/9431.htm
- http://m.3g.uliejh.cn/nnews/5188.htm
- http://m.3g.uliejh.cn/nnews/4378.htm
- http://m.3g.uliejh.cn/nnews/9148.htm
- http://m.3g.uliejh.cn/nnews/798537.htm
- http://m.3g.uliejh.cn/nnews/05274.htm
- http://m.3g.uliejh.cn/nnews/55914.htm
- http://m.3g.uliejh.cn/nnews/69873.htm
- http://m.3g.uliejh.cn/nnews/12867.htm
- http://m.3g.uliejh.cn/nnews/253928.htm
- http://m.3g.uliejh.cn/nnews/8606.htm
- http://m.3g.uliejh.cn/nnews/7239.htm
- http://m.3g.uliejh.cn/nnews/8623869.htm
- http://m.3g.uliejh.cn/nnews/9304025.htm
- http://m.3g.uliejh.cn/nnews/1818200.htm
- http://m.3g.uliejh.cn/nnews/065597.htm
- http://m.3g.uliejh.cn/nnews/5315367.htm
- http://m.3g.uliejh.cn/nnews/53862.htm
- http://m.3g.uliejh.cn/nnews/048901.htm
- http://m.3g.uliejh.cn/nnews/366873.htm
- http://m.3g.uliejh.cn/nnews/9743745.htm
- http://m.3g.uliejh.cn/nnews/242793.htm
- http://m.3g.uliejh.cn/nnews/0675696.htm
- http://m.3g.uliejh.cn/nnews/15503.htm
- http://m.3g.uliejh.cn/nnews/6968860.htm
- http://m.3g.uliejh.cn/nnews/910854.htm
- http://m.3g.uliejh.cn/nnews/0055.htm
- http://m.3g.uliejh.cn/nnews/019308.htm
- http://m.3g.uliejh.cn/nnews/74804.htm
- http://m.3g.uliejh.cn/nnews/870227.htm
- http://m.3g.uliejh.cn/nnews/2251.htm
- http://m.3g.uliejh.cn/nnews/771730.htm
- http://m.3g.uliejh.cn/nnews/0944.htm
- http://m.3g.uliejh.cn/nnews/7958.htm
- http://m.3g.uliejh.cn/nnews/081075.htm
- http://m.3g.uliejh.cn/nnews/77108.htm
- http://m.3g.uliejh.cn/nnews/1034.htm
- http://m.3g.uliejh.cn/nnews/9224.htm
- http://m.3g.uliejh.cn/nnews/3082.htm
- http://m.3g.uliejh.cn/nnews/18044.htm
- http://m.3g.uliejh.cn/nnews/0870.htm
- http://m.3g.uliejh.cn/nnews/16430.htm
- http://m.3g.uliejh.cn/nnews/0287.htm
- http://m.3g.uliejh.cn/nnews/641144.htm
- http://m.3g.uliejh.cn/nnews/1273.htm
- http://m.3g.uliejh.cn/nnews/03436.htm

## 项目结构

```
linkvault-core/
├── src/
│   ├── core/                       # 核心数据模型与业务逻辑
│   │   ├── resource.ts             # Resource 实体类，包含 URL 解析、哈希生成方法
│   │   ├── collection.ts           # Collection 管理器，处理批次、标签和查询
│   │   └── validator.ts            # URL 规范化与重复检测引擎
│   ├── checker/                    # 链接可用性探测模块
│   │   ├── http-client.ts          # 基于 undici 的异步 HTTP 检查器
│   │   ├── scheduler.ts            # 基于 cron 的巡检任务调度器
│   │   └── reporter.ts             # 生成可用性报告（JSON/Markdown）
│   ├── storage/                    # 持久化适配器
│   │   ├── sqlite-adapter.ts       # SQLite3 实现，用于开发和小规模部署
│   │   ├── postgres-adapter.ts     # PostgreSQL 实现，用于生产环境
│   │   └── migrations/             # 数据库迁移脚本（按版本递增）
│   ├── api/                        # RESTful API 端点（Express 路由）
│   │   ├── resources.ts            # CRUD 操作：导入、更新、删除、查询
│   │   ├── batches.ts              # 批次管理：创建批次、列出批次、导出批次
│   │   └── health.ts               # 健康检查状态查询与手动触发
│   ├── export/                     # 导出管道
│   │   ├── markdown-renderer.ts    # 生成 Markdown 列表及目录
│   │   ├── json-serializer.ts      # 输出 JSON API 响应
│   │   └── sitemap-generator.ts    # 生成 sitemap.xml 供搜索引擎索引
│   ├── cli/                        # 命令行接口
│   │   ├── import.ts               # 从文件或 stdin 导入资源
│   │   ├── check.ts                # 手动触发全量或增量检查
│   │   └── export.ts               # 按格式和过滤条件导出数据
│   └── utils/                      # 工具函数库
│       ├── logger.ts               # 结构化日志（pino 实现）
│       ├── config.ts               # 环境变量和配置文件加载器
│       └── crypto.ts               # 哈希生成、签名与编码工具
├── tests/                          # 单元测试与集成测试（Jest 框架）
│   ├── unit/                       # 模块级单元测试
│   └── integration/                # 数据库与 API 集成测试
├── docs/                           # 完整文档（Markdown 格式）
├── examples/                       # 示例数据与导入模板
│   ├── sample-batch.csv            # CSV 格式示例批次
│   └── sample-tags.json            # 预定义标签方案
├── .env.example                    # 环境变量模板（数据库连接、超时参数）
├── package.json                    # npm 项目清单与脚本定义
├── tsconfig.json                   # TypeScript 编译配置（严格模式）
└── README.md                       # 本文件
```

## 贡献指南

1. 查阅 issues 列表，选择带有 good-first-issue 或 help-wanted 标签的任务，在评论中声明认领以避免重复工作。对于新功能提议，请先创建一个 issue 描述动机、使用场景和初步设计思路，等待维护者反馈后再开始编码。

2. 从主分支 fork 仓库到个人账户，在本地新建一个描述性的分支名称，例如 feature/add-json-export-filter 或 fix/sqlite-connection-pool。确保分支基于最新的 main 分支，并定期从上游同步变更。

3. 编写代码时遵循项目已配置的 ESLint 和 Prettier 规则。所有新增功能必须包含对应的单元测试，测试覆盖率不得低于 80%。对于涉及外部 HTTP 请求的代码，请使用 nock 或 sinon 进行模拟，避免测试依赖真实网络。

4. 提交信息采用 Conventional Commits 规范，格式为 type(scope): subject，例如 feat(checker): add retry backoff policy。每个提交应保持原子性，即一次提交只解决一个问题或实现一个特性。提交前运行 npm run test 确保所有现有测试通过。

5. 推送分支后，在 GitHub 上创建一个 pull request 到 main 分支。PR 描述中请链接相关的 issue 编号，并提供测试截图或手动验证步骤。至少需要一位维护者批准后方可合并。合并后贡献者信息将自动纳入 release notes。

## 常见问题

**问：LinkVault 是否支持代理或 VPN 环境下的链接检查？**  
答：支持。您可以在 .env 文件中设置 HTTP_PROXY 和 HTTPS_PROXY 环境变量，http-client 模块会自动读取这些变量并路由所有出站请求。对于需要身份验证的代理，支持基本认证格式（如 http://user:pass@proxy.example.com:8080）。若代理需要自定义 CA 证书，可在配置中指定 certPath 选项。

**问：如何迁移已有的浏览器书签或 Pocket 收藏夹到 LinkVault？**  
答：LinkVault 未内置直接解析浏览器书签 HTML 文件的功能，但您可以使用以下流程：将书签导出为 HTML，然后使用命令行工具如 `pup` 或 `htmlq` 提取所有 href 属性值，整理成每行一个 URL 的纯文本文件。最后使用 `npm run import -- --format=plain --file=bookmarks.txt` 导入，系统会自动去重并分配默认标签。若您需要自动解析书签文件夹层级作为标签，可参考 `examples/import-bookmarks.sh` 辅助脚本。

**问：资源列表数量很多时，性能表现如何？**  
答：LinkVault 在设计之初就考虑了大规模资源管理。使用 SQLite 时，单表可稳定支持 10 万条记录，查询响应时间在 50ms 以内（带索引）。异步检查器默认并发数为 16，可根据机器性能在配置中调整 maxConcurrency 参数。对于超过 5000 个资源的批次导出，建议使用流式接口或分页查询，避免一次性加载全部数据到内存。生产环境推荐使用 PostgreSQL，配合连接池和物化视图可进一步提升复杂查询效率。

## 许可证

MIT

> 外链数量: 250 | 生成时间: 2026-08-24 23:40:21
