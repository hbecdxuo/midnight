# WebLink Archive Batch Processor

WebLink Archive Batch Processor 是一个面向技术文档归档、外链资源归集与历史页面快照管理的轻量级批处理工具。该项目定位于需要批量采集、清洗、分类和持久化存储大量 URL 资源的开发者、数据研究员与运维工程师。通过声明式的配置和可扩展的管道架构，用户能够将分散的短链、动态参数链接或纯数字 ID 链接转化为结构化元数据记录，并支持后续的可用性检测、内容摘要提取与标签化检索。

本项目不提供爬虫框架或浏览器自动化能力，而是专注于 URL 规范化、批处理队列调度、失败重试策略与结果导出接口。目标用户包括需要整理历史新闻链接的档案维护者、构建外部资源镜像站点的系统管理员，以及进行链接生命周期分析的数据分析人员。

## 功能概览

批量 URL 导入与校验：支持从纯文本文件、CSV 或标准输入流中读取链接列表，自动识别协议头、域名格式与路径结构，过滤非法或重复条目。

可配置的请求管道：每个 URL 经过用户定义的中间件链，包括 User-Agent 轮换、延迟控制、超时设置与状态码白名单过滤。

分布式任务队列：基于 Redis 或内存队列实现生产者-消费者模型，支持多进程并发处理，可横向扩展至多台工作节点。

结构化元数据提取：从响应头、HTML 标题、Meta 描述及 Open Graph 标签中抽取关键字段，输出为 JSON Lines 或 Parquet 格式。

失败重试与死信队列：自动记录永久失败请求至死信存储，支持人工复核后重新入队，并生成详细的失败原因分类统计。

实时进度仪表盘：通过内置 Web 终端或导出 Prometheus 指标，观察每秒请求数、平均响应时间、成功率和队列积压量。

插件化输出适配器：内置文件系统、AWS S3、MinIO 与标准 SQL 数据库（PostgreSQL / SQLite）写入器，用户可自行扩展至其他存储后端。

## 应用场景

历史新闻站点链接可用性审计：针对大量带有数字 ID 的旧闻链接，定期发起 HEAD 或 GET 请求，检测目标页面是否仍返回 200 OK，并记录重定向链变化，用于判断内容是否迁移或下架。

外部资源镜像站点的增量同步：当源站链接遵循固定路径模式（如 /bnews/{id}.htm）时，使用批处理器按 ID 区间或列表生成完整 URL，并发拉取页面正文，保存为本地静态 HTML 存档，供内部搜索或离线阅读。

SEO 外链健康度监控：运营人员将友链或推广链接导入系统，每周自动检查各链接的可访问性、页面标题是否变更、是否存在 nofollow 标记，生成周报供决策参考。

数据中台原始链接清洗层：在大数据流水线中，将杂乱无章的外部 URL 统一经过本工具的规范化、去重和存活验证，再将干净结果写入下游数据湖，减少后续 ETL 作业的异常处理负担。

## 快速开始

以下命令演示了从克隆仓库到运行一次标准批处理任务的全过程。

```bash
# 克隆项目仓库
git clone https://github.com/weblink-archive/batch-processor.git
cd batch-processor

# 安装 Python 虚拟环境与依赖
python3 -m venv venv
source venv/bin/activate  # Windows 使用 venv\Scripts\activate
pip install --upgrade pip
pip install -r requirements.txt

# 准备输入文件 urls.txt，每行一个 URL
# 执行批处理，输出结果至 ./output 目录
python main.py \
  --input urls.txt \
  --output ./output \
  --concurrency 5 \
  --timeout 10 \
  --retry 3 \
  --format json
```

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|---------|---------|------|
| Python | 3.9 及以上 | 核心解释器，低于 3.9 将无法使用类型注解与异步特性 |
| aiohttp | 3.9.0 及以上 | 异步 HTTP 客户端，负责所有网络请求发送与连接池管理 |
| redis-py | 4.5.0 及以上 | 仅在启用分布式队列模式时需要，用于任务代理与结果暂存 |
| sqlalchemy | 2.0.0 及以上 | 提供数据库无关的 ORM 层，用于 SQL 输出适配器 |
| pyarrow | 14.0.0 及以上 | 仅在输出 Parquet 格式时需要，用于列式数据序列化 |
| tqdm | 4.66.0 及以上 | 提供命令行进度条，用于实时显示批处理完成百分比 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|-----|------|----------|
| 入门指南 | docs/getting_started.md | 如何安装、配置第一个任务、理解输入输出格式 |
| 配置参考 | docs/configuration.md | 所有环境变量、配置文件字段及命令行参数的详细说明 |
| 中间件开发 | docs/middleware.md | 如何编写自定义请求拦截器、响应处理器和钩子函数 |
| 性能调优 | docs/performance.md | 并发数选择、超时搭配、连接池大小与内存占用优化建议 |

## 资源列表

- http://m.wap.uliejh.cn/bnews/6158275.htm
- http://m.wap.uliejh.cn/bnews/144651.htm
- http://m.wap.uliejh.cn/bnews/3146.htm
- http://m.wap.uliejh.cn/bnews/267214.htm
- http://m.wap.uliejh.cn/bnews/054461.htm
- http://m.wap.uliejh.cn/bnews/019943.htm
- http://m.wap.uliejh.cn/bnews/693794.htm
- http://m.wap.uliejh.cn/bnews/7916.htm
- http://m.wap.uliejh.cn/bnews/3359228.htm
- http://m.wap.uliejh.cn/bnews/95842.htm
- http://m.wap.uliejh.cn/bnews/351229.htm
- http://m.wap.uliejh.cn/bnews/1985323.htm
- http://m.wap.uliejh.cn/bnews/185628.htm
- http://m.wap.uliejh.cn/bnews/02844.htm
- http://m.wap.uliejh.cn/bnews/033674.htm
- http://m.wap.uliejh.cn/bnews/4515917.htm
- http://m.wap.uliejh.cn/bnews/308886.htm
- http://m.wap.uliejh.cn/bnews/940195.htm
- http://m.wap.uliejh.cn/bnews/5452264.htm
- http://m.wap.uliejh.cn/bnews/345089.htm
- http://m.wap.uliejh.cn/bnews/938846.htm
- http://m.wap.uliejh.cn/bnews/2532668.htm
- http://m.wap.uliejh.cn/bnews/64621.htm
- http://m.wap.uliejh.cn/bnews/6988627.htm
- http://m.wap.uliejh.cn/bnews/062660.htm
- http://m.wap.uliejh.cn/bnews/7964565.htm
- http://m.wap.uliejh.cn/bnews/043800.htm
- http://m.wap.uliejh.cn/bnews/346923.htm
- http://m.wap.uliejh.cn/bnews/697143.htm
- http://m.wap.uliejh.cn/bnews/7592.htm
- http://m.wap.uliejh.cn/bnews/7708679.htm
- http://m.wap.uliejh.cn/bnews/33546.htm
- http://m.wap.uliejh.cn/bnews/68912.htm
- http://m.wap.uliejh.cn/bnews/851719.htm
- http://m.wap.uliejh.cn/bnews/63901.htm
- http://m.wap.uliejh.cn/bnews/562605.htm
- http://m.wap.uliejh.cn/bnews/246205.htm
- http://m.wap.uliejh.cn/bnews/4704.htm
- http://m.wap.uliejh.cn/bnews/1582.htm
- http://m.wap.uliejh.cn/bnews/4318.htm
- http://m.wap.uliejh.cn/bnews/2598.htm
- http://m.wap.uliejh.cn/bnews/23842.htm
- http://m.wap.uliejh.cn/bnews/7555.htm
- http://m.wap.uliejh.cn/bnews/6789.htm
- http://m.wap.uliejh.cn/bnews/3906.htm
- http://m.wap.uliejh.cn/bnews/111398.htm
- http://m.wap.uliejh.cn/bnews/8507.htm
- http://m.wap.uliejh.cn/bnews/262614.htm
- http://m.wap.uliejh.cn/bnews/095129.htm
- http://m.wap.uliejh.cn/bnews/672906.htm
- http://m.wap.uliejh.cn/bnews/7741.htm
- http://m.wap.uliejh.cn/bnews/58959.htm
- http://m.wap.uliejh.cn/bnews/5963.htm
- http://m.wap.uliejh.cn/bnews/5862582.htm
- http://m.wap.uliejh.cn/bnews/9297995.htm
- http://m.wap.uliejh.cn/bnews/030228.htm
- http://m.wap.uliejh.cn/bnews/66499.htm
- http://m.wap.uliejh.cn/bnews/491260.htm
- http://m.wap.uliejh.cn/bnews/7216.htm
- http://m.wap.uliejh.cn/bnews/8151.htm
- http://m.wap.uliejh.cn/bnews/7463107.htm
- http://m.wap.uliejh.cn/bnews/35616.htm
- http://m.wap.uliejh.cn/bnews/30134.htm
- http://m.wap.uliejh.cn/bnews/4145.htm
- http://m.wap.uliejh.cn/bnews/098811.htm
- http://m.wap.uliejh.cn/bnews/6866241.htm
- http://m.wap.uliejh.cn/bnews/65306.htm
- http://m.wap.uliejh.cn/bnews/078672.htm
- http://m.wap.uliejh.cn/bnews/371386.htm
- http://m.wap.uliejh.cn/bnews/76194.htm
- http://m.wap.uliejh.cn/bnews/4575.htm
- http://m.wap.uliejh.cn/bnews/9619.htm
- http://m.wap.uliejh.cn/bnews/4786.htm
- http://m.wap.uliejh.cn/bnews/83521.htm
- http://m.wap.uliejh.cn/bnews/5132.htm
- http://m.wap.uliejh.cn/bnews/70498.htm
- http://m.wap.uliejh.cn/bnews/607169.htm
- http://m.wap.uliejh.cn/bnews/9111.htm
- http://m.wap.uliejh.cn/bnews/926434.htm
- http://m.wap.uliejh.cn/bnews/0784269.htm
- http://m.wap.uliejh.cn/bnews/3525795.htm
- http://m.wap.uliejh.cn/bnews/205036.htm
- http://m.wap.uliejh.cn/bnews/2661800.htm
- http://m.wap.uliejh.cn/bnews/943774.htm
- http://m.wap.uliejh.cn/bnews/531465.htm
- http://m.wap.uliejh.cn/bnews/1599269.htm
- http://m.wap.uliejh.cn/bnews/2018672.htm
- http://m.wap.uliejh.cn/bnews/4166.htm
- http://m.wap.uliejh.cn/bnews/8455470.htm
- http://m.wap.uliejh.cn/bnews/1277298.htm
- http://m.wap.uliejh.cn/bnews/519012.htm
- http://m.wap.uliejh.cn/bnews/6718.htm
- http://m.wap.uliejh.cn/bnews/91175.htm
- http://m.wap.uliejh.cn/bnews/004963.htm
- http://m.wap.uliejh.cn/bnews/225374.htm
- http://m.wap.uliejh.cn/bnews/1959.htm
- http://m.wap.uliejh.cn/bnews/1055.htm
- http://m.wap.uliejh.cn/bnews/061254.htm
- http://m.wap.uliejh.cn/bnews/32907.htm
- http://m.wap.uliejh.cn/bnews/904528.htm
- http://m.wap.uliejh.cn/bnews/40915.htm
- http://m.wap.uliejh.cn/bnews/0583.htm
- http://m.wap.uliejh.cn/bnews/790867.htm
- http://m.wap.uliejh.cn/bnews/90001.htm
- http://m.wap.uliejh.cn/bnews/6480.htm
- http://m.wap.uliejh.cn/bnews/154078.htm
- http://m.wap.uliejh.cn/bnews/3105.htm
- http://m.wap.uliejh.cn/bnews/56116.htm
- http://m.wap.uliejh.cn/bnews/350559.htm
- http://m.wap.uliejh.cn/bnews/7167.htm
- http://m.wap.uliejh.cn/bnews/2215877.htm
- http://m.wap.uliejh.cn/bnews/86792.htm
- http://m.wap.uliejh.cn/bnews/2956.htm
- http://m.wap.uliejh.cn/bnews/757135.htm
- http://m.wap.uliejh.cn/bnews/152592.htm
- http://m.wap.uliejh.cn/bnews/479262.htm
- http://m.wap.uliejh.cn/bnews/6899824.htm
- http://m.wap.uliejh.cn/bnews/2043597.htm
- http://m.wap.uliejh.cn/bnews/58454.htm
- http://m.wap.uliejh.cn/bnews/550104.htm
- http://m.wap.uliejh.cn/bnews/59110.htm
- http://m.wap.uliejh.cn/bnews/4126.htm
- http://m.wap.uliejh.cn/bnews/08155.htm
- http://m.wap.uliejh.cn/bnews/0610538.htm
- http://m.wap.uliejh.cn/bnews/46688.htm
- http://m.wap.uliejh.cn/bnews/153024.htm
- http://m.wap.uliejh.cn/bnews/5884.htm
- http://m.wap.uliejh.cn/bnews/0301.htm
- http://m.wap.uliejh.cn/bnews/5501.htm
- http://m.wap.uliejh.cn/bnews/124735.htm
- http://m.wap.uliejh.cn/bnews/55294.htm
- http://m.wap.uliejh.cn/bnews/5040.htm
- http://m.wap.uliejh.cn/bnews/898879.htm
- http://m.wap.uliejh.cn/bnews/003262.htm
- http://m.wap.uliejh.cn/bnews/3748575.htm
- http://m.wap.uliejh.cn/bnews/6404.htm
- http://m.wap.uliejh.cn/bnews/4863388.htm
- http://m.wap.uliejh.cn/bnews/60705.htm
- http://m.wap.uliejh.cn/bnews/02464.htm
- http://m.wap.uliejh.cn/bnews/6877115.htm
- http://m.wap.uliejh.cn/bnews/6273.htm
- http://m.wap.uliejh.cn/bnews/05394.htm
- http://m.wap.uliejh.cn/bnews/16344.htm
- http://m.wap.uliejh.cn/bnews/478847.htm
- http://m.wap.uliejh.cn/bnews/16114.htm
- http://m.wap.uliejh.cn/bnews/122672.htm
- http://m.wap.uliejh.cn/bnews/455750.htm
- http://m.wap.uliejh.cn/bnews/842839.htm
- http://m.wap.uliejh.cn/bnews/176106.htm
- http://m.wap.uliejh.cn/bnews/00386.htm
- http://m.wap.uliejh.cn/bnews/5973799.htm
- http://m.wap.uliejh.cn/bnews/44260.htm
- http://m.wap.uliejh.cn/bnews/3764.htm
- http://m.wap.uliejh.cn/bnews/3695.htm
- http://m.wap.uliejh.cn/bnews/738801.htm
- http://m.wap.uliejh.cn/bnews/5197.htm
- http://m.wap.uliejh.cn/bnews/6060.htm
- http://m.wap.uliejh.cn/bnews/2977.htm
- http://m.wap.uliejh.cn/bnews/543950.htm
- http://m.wap.uliejh.cn/bnews/7469.htm
- http://m.wap.uliejh.cn/bnews/9203075.htm
- http://m.wap.uliejh.cn/bnews/61444.htm
- http://m.wap.uliejh.cn/bnews/1888880.htm
- http://m.wap.uliejh.cn/bnews/515931.htm
- http://m.wap.uliejh.cn/bnews/95453.htm
- http://m.wap.uliejh.cn/bnews/2387.htm
- http://m.wap.uliejh.cn/bnews/3279179.htm
- http://m.wap.uliejh.cn/bnews/1503364.htm
- http://m.wap.uliejh.cn/bnews/288173.htm
- http://m.wap.uliejh.cn/bnews/6340.htm
- http://m.wap.uliejh.cn/bnews/0686.htm
- http://m.wap.uliejh.cn/bnews/117756.htm
- http://m.wap.uliejh.cn/bnews/2432828.htm
- http://m.wap.uliejh.cn/bnews/0066436.htm
- http://m.wap.uliejh.cn/bnews/4544776.htm
- http://m.wap.uliejh.cn/bnews/8669.htm
- http://m.wap.uliejh.cn/bnews/333609.htm
- http://m.wap.uliejh.cn/bnews/39972.htm
- http://m.wap.uliejh.cn/bnews/4244062.htm
- http://m.wap.uliejh.cn/bnews/973860.htm
- http://m.wap.uliejh.cn/bnews/39708.htm
- http://m.wap.uliejh.cn/bnews/187485.htm
- http://m.wap.uliejh.cn/bnews/4154886.htm
- http://m.wap.uliejh.cn/bnews/5801.htm
- http://m.wap.uliejh.cn/bnews/33094.htm
- http://m.wap.uliejh.cn/bnews/9075.htm
- http://m.wap.uliejh.cn/bnews/1167273.htm
- http://m.wap.uliejh.cn/bnews/3759.htm
- http://m.wap.uliejh.cn/bnews/53659.htm
- http://m.wap.uliejh.cn/bnews/08339.htm
- http://m.wap.uliejh.cn/bnews/128890.htm
- http://m.wap.uliejh.cn/bnews/8456.htm
- http://m.wap.uliejh.cn/bnews/1188.htm
- http://m.wap.uliejh.cn/bnews/16381.htm
- http://m.wap.uliejh.cn/bnews/98708.htm
- http://m.wap.uliejh.cn/bnews/65693.htm
- http://m.wap.uliejh.cn/bnews/672862.htm
- http://m.wap.uliejh.cn/bnews/43750.htm
- http://m.wap.uliejh.cn/bnews/2423304.htm
- http://m.wap.uliejh.cn/bnews/4441.htm
- http://m.wap.uliejh.cn/bnews/35757.htm
- http://m.wap.uliejh.cn/bnews/8543.htm
- http://m.wap.uliejh.cn/bnews/1219307.htm
- http://m.wap.uliejh.cn/bnews/66314.htm
- http://m.wap.uliejh.cn/bnews/0608896.htm
- http://m.wap.uliejh.cn/bnews/6271.htm
- http://m.wap.uliejh.cn/bnews/543340.htm
- http://m.wap.uliejh.cn/bnews/071410.htm
- http://m.wap.uliejh.cn/bnews/6106.htm
- http://m.wap.uliejh.cn/bnews/2797041.htm
- http://m.wap.uliejh.cn/bnews/9665.htm
- http://m.wap.uliejh.cn/bnews/289213.htm
- http://m.wap.uliejh.cn/bnews/113223.htm
- http://m.wap.uliejh.cn/bnews/9275.htm
- http://m.wap.uliejh.cn/bnews/538501.htm
- http://m.wap.uliejh.cn/bnews/908028.htm
- http://m.wap.uliejh.cn/bnews/736272.htm
- http://m.wap.uliejh.cn/bnews/7529000.htm
- http://m.wap.uliejh.cn/bnews/2472.htm
- http://m.wap.uliejh.cn/bnews/99697.htm
- http://m.wap.uliejh.cn/bnews/7016.htm
- http://m.wap.uliejh.cn/bnews/457650.htm
- http://m.wap.uliejh.cn/bnews/041367.htm
- http://m.wap.uliejh.cn/bnews/681571.htm
- http://m.wap.uliejh.cn/bnews/45507.htm
- http://m.wap.uliejh.cn/bnews/98872.htm
- http://m.wap.uliejh.cn/bnews/2596.htm
- http://m.wap.uliejh.cn/bnews/7685631.htm
- http://m.wap.uliejh.cn/bnews/0892601.htm
- http://m.wap.uliejh.cn/bnews/2381.htm
- http://m.wap.uliejh.cn/bnews/95428.htm
- http://m.wap.uliejh.cn/bnews/50594.htm
- http://m.wap.uliejh.cn/bnews/30179.htm
- http://m.wap.uliejh.cn/bnews/667186.htm
- http://m.wap.uliejh.cn/bnews/4700932.htm
- http://m.wap.uliejh.cn/bnews/1943.htm
- http://m.wap.uliejh.cn/bnews/17590.htm
- http://m.wap.uliejh.cn/bnews/72050.htm
- http://m.wap.uliejh.cn/bnews/18035.htm
- http://m.wap.uliejh.cn/bnews/98009.htm
- http://m.wap.uliejh.cn/bnews/8564115.htm
- http://m.wap.uliejh.cn/bnews/9960.htm
- http://m.wap.uliejh.cn/bnews/31022.htm
- http://m.wap.uliejh.cn/bnews/272770.htm
- http://m.wap.uliejh.cn/bnews/940125.htm
- http://m.wap.uliejh.cn/bnews/9941.htm
- http://m.wap.uliejh.cn/bnews/373248.htm
- http://m.wap.uliejh.cn/bnews/8104.htm
- http://m.wap.uliejh.cn/bnews/14694.htm
- http://m.wap.uliejh.cn/bnews/0754868.htm

## 项目结构

```
batch-processor/
├── main.py                          # 程序入口，解析命令行参数并启动调度器
├── config/
│   ├── default.yaml                 # 默认配置（并发数、超时、重试、日志级别）
│   └── schema.json                  # 配置文件的 JSON Schema 校验定义
├── core/
│   ├── loader.py                    # 输入加载器，支持 txt、csv、stdin 读取
│   ├── queue.py                     # 任务队列抽象，内存 / Redis 两种后端实现
│   ├── worker.py                    # 异步工作单元，执行单 URL 的请求与解析
│   └── dispatcher.py                # 调度器，管理生产者、消费者与进度汇总
├── middleware/
│   ├── headers.py                   # User-Agent 轮换及自定义请求头注入
│   ├── retry.py                     # 指数退避重试策略与状态码判定
│   └── extractor.py                 # 从响应中提取标题、描述、标签等元数据
├── adapters/
│   ├── file_writer.py               # 输出到本地 JSON / CSV / Parquet 文件
│   ├── s3_writer.py                 # 上传结果至 S3 兼容对象存储
│   └── sql_writer.py                # 写入 PostgreSQL 或 SQLite 关系表
├── utils/
│   ├── logger.py                    # 结构化日志（JSON 格式，支持 ELK 接入）
│   └── validator.py                 # URL 规范化、去重与黑名单过滤
├── tests/                           # 单元测试与集成测试，覆盖率达 92%
├── docs/                            # 完整文档，含 API 参考与示例教程
├── scripts/                         # 运维脚本，如 Docker 构建、数据迁移
├── requirements.txt                 # 生产环境依赖列表
├── requirements-dev.txt             # 开发环境额外依赖（pytest, black, mypy）
├── Dockerfile                       # 多阶段构建镜像，基于 Alpine 精简体积
├── Makefile                         # 常用命令封装（install, test, lint, run）
└── README.md                        # 本文件
```

## 贡献指南

1. 在 GitHub 上 Fork 本仓库，并克隆到本地开发环境。创建新分支时使用 `feature/` 或 `fix/` 前缀，名称简要描述改动内容，例如 `feature/add-retry-backoff` 或 `fix/queue-leak`。

2. 安装开发依赖并启用 pre-commit 钩子，确保代码风格、类型注解和文档字符串符合项目规范。运行 `make install-dev` 完成环境准备，使用 `make lint` 检查语法问题。

3. 编写或修改代码后，补充对应的单元测试，测试文件放置于 `tests/` 目录下，命名与源文件对应。执行 `make test` 确保全部用例通过且覆盖率不低于 90%。

4. 更新相关文档，包括 `docs/` 下的用户手册、配置说明和示例。如果引入新的依赖项，需同步修改 `requirements.txt` 并在 `README.md` 的安装要求表格中补充。

5. 提交 Pull Request 至主仓库的 `dev` 分支，描述中注明解决的问题、测试结果和文档变更。等待至少两名维护者审阅后合并。

## 常见问题

**Q: 批处理过程中遇到大量 SSL 证书验证失败或连接超时，应如何调整？**

A: 可以在配置文件或命令行中关闭 SSL 验证（`--no-ssl-verify`），但仅建议在内网或受信环境使用。对于超时，可通过 `--timeout` 参数增大单次请求的超时阈值，同时配合 `--retry` 增加重试次数。若目标站点有反爬机制，建议在中间件中配置更长的延迟间隔（`--delay`）并轮换 User-Agent。

**Q: 输出结果中部分 URL 返回 404 或 5xx，但手动访问浏览器可以正常打开，是什么原因？**

A: 常见原因包括目标站点对程序请求做了 User-Agent 或 Headers 校验，以及缺少某些 Cookie 或 Referer 字段。请检查中间件配置，尝试复制浏览器完整的请求头（包括 Accept-Language 和 Sec-Fetch-* 系列头）。另外，某些站点会返回动态加载内容，本工具仅获取初始 HTML，不执行 JavaScript，若页面依赖客户端渲染，则需配合无头浏览器方案。

**Q: 如何处理超过 10 万条 URL 的超大批次任务？**

A: 建议启用 Redis 分布式队列模式，并将输出适配器设置为 S3 或数据库流式写入，避免内存溢出。同时根据机器性能调整并发数，一般推荐并发数不超过 CPU 核心数的 4 倍。可将输入文件拆分为多个分片，在多台机器上并行运行，最终结果通过 `--merge` 参数合并。另外，务必配置日志滚动策略，防止磁盘被大量调试日志占满。

## 许可证

MIT

> 外链数量: 250 | 生成时间: 2026-08-24 23:40:21
