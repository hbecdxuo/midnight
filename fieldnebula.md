# LinkVault Resource Aggregator

LinkVault is a production-grade structured resource aggregation and external link management system designed for technical content curation, batch link processing, and knowledge base construction. It targets developers, technical writers, data analysts, and research engineers who need to systematically organize, validate, and serve large volumes of external reference links from mobile-optimized content sources.

Unlike generic bookmark managers or simple link dump repositories, LinkVault provides automated metadata extraction, link health monitoring, categorical tagging, and export pipelines. The project processes raw URL batches—such as those from mobile news syndication networks—and transforms them into queryable, version-controlled, and dependency-aware resource collections suitable for integration into documentation portals, internal knowledge bases, or CI-driven data pipelines.

## 功能概览

- **批量链接摄入与规范化**: 接受原始 URL 列表（含协议、域名、路径及查询参数），自动去重、格式校验，并生成持久化存储标识。

- **元数据自动补全**: 对每个资源链接发起轻量级 HEAD/GET 请求，提取内容类型、内容长度、最后修改时间、服务器类型等 HTTP 头信息，并计算响应体哈希以追踪变更。

- **分类标签与全文检索**: 基于 URL 路径模式、域名分段和可配置的正则规则库自动打标；支持标题、描述及自定义注释的全文搜索。

- **健康检查与死链检测**: 按可调度周期（每日/每周）重新验证所有链接的可访问性，记录状态码、响应时间和重定向链，生成失效链接报表。

- **多格式导出与集成**: 输出为 JSON、CSV、Markdown 表格或静态 HTML 索引页；提供 RESTful API 和 Webhook 触发更新，便于嵌入现有工作流。

- **审计追踪与版本历史**: 每次链接集合变更（新增、删除、元数据更新）均记录操作日志与快照，支持回滚至任意历史状态。

## 应用场景

**技术文档中心的引用源管理**: 大型开源项目或企业内部文档系统通常引用数百个外部规范、博客、API 参考和社区讨论。LinkVault 可定期抓取并验证这些引用，确保文档中的外部链接始终有效，并在链接失效时自动向维护者发送告警。

**数据挖掘与舆情分析管道预处理**: 研究团队从移动内容平台采集大量新闻、公告或用户生成内容链接。LinkVault 作为预处理层，清洗 URL 格式、抽取域名分布、识别重复条目，并将结构化元数据写入 Parquet 文件供后续分析。

**知识库构建与课程资料汇编**: 教育机构或技术培训团队需要为学员整理补充阅读材料。通过 LinkVault 维护按主题、难度或来源分类的链接池，支持快速生成课程讲义附录或在线阅读清单。

**CI/CD 中的外部依赖锁定**: 在软件构建或部署流程中，若依赖外部配置文件、脚本或资源包，LinkVault 可存储这些资源的永久快照链接及校验和，当外部资源变更时阻断构建并提示人工介入。

## 快速开始

以下指令适用于 Linux/macOS 环境，Windows 用户可通过 WSL2 或 Git Bash 执行。

```bash
# 1. 克隆仓库
git clone https://github.com/your-org/linkvault.git
cd linkvault

# 2. 安装 Python 依赖（建议使用虚拟环境）
python3 -m venv venv
source venv/bin/activate
pip install --upgrade pip
pip install -r requirements.txt

# 3. 初始化数据库并运行摄入示例（使用项目自带测试数据）
python manage.py migrate
python manage.py ingest --source data/sample_batch_60.csv --tag batch60
python manage.py serve --host 0.0.0.0 --port 8080
```

访问 http://localhost:8080 可查看 Web 仪表板；API 文档位于 http://localhost:8080/api/docs。

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|---------|---------|------|
| Python | 3.9 - 3.11 | 核心运行环境，低于 3.9 不支持类型注解语法 |
| PostgreSQL | 13.x 或更高 | 生产数据库，用于存储链接元数据与审计日志；不支持 SQLite 用于生产 |
| Redis | 6.2 或更高 | 缓存层与任务队列后端，用于健康检查调度 |
| Celery | 5.2.7 | 异步任务处理器，与 Redis 配合执行定时验证 |
| httpx | 0.24.0 或更高 | 异步 HTTP 客户端，用于并发链接探测；替代 requests 以支持 HTTP/2 |
| PyYAML | 6.0 | 解析配置文件（config.yaml），支持环境变量插值 |
| alembic | 1.9.0 | 数据库迁移管理，用于 schema 版本升级 |
| pytest | 7.2.0 | 单元测试与集成测试框架（开发依赖） |
| pre-commit | 3.0.0 | Git 钩子管理，用于代码格式化与 lint（开发依赖） |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|------|------|-----------|
| 用户入门 | /docs/getting-started.md | 如何下载、配置、首次运行并摄入第一批链接？ |
| 操作指南 | /docs/operations/scheduling.md | 如何设置周期性健康检查、调整并发数、配置告警规则？ |
| 开发者参考 | /docs/development/api.md | RESTful 端点定义、请求/响应格式、鉴权方式及错误码含义？ |
| 运维手册 | /docs/administration/deployment.md | 支持哪些部署方式（Docker、K8s、systemd）？环境变量如何配置？ |

完整文档树包含 12 个 Markdown 文件，建议从 getting-started.md 开始，按顺序阅读。

## 资源列表

- http://m.wap.uliejh.cn/bnews/728914.htm
- http://m.wap.uliejh.cn/bnews/609897.htm
- http://m.wap.uliejh.cn/bnews/52308.htm
- http://m.wap.uliejh.cn/bnews/2989692.htm
- http://m.wap.uliejh.cn/bnews/064717.htm
- http://m.wap.uliejh.cn/bnews/7005.htm
- http://m.wap.uliejh.cn/bnews/46406.htm
- http://m.wap.uliejh.cn/bnews/4560.htm
- http://m.wap.uliejh.cn/bnews/2283389.htm
- http://m.wap.uliejh.cn/bnews/4269.htm
- http://m.wap.uliejh.cn/bnews/471549.htm
- http://m.wap.uliejh.cn/bnews/246618.htm
- http://m.wap.uliejh.cn/bnews/79811.htm
- http://m.wap.uliejh.cn/bnews/74010.htm
- http://m.wap.uliejh.cn/bnews/0857738.htm
- http://m.wap.uliejh.cn/bnews/15583.htm
- http://m.wap.uliejh.cn/bnews/4416813.htm
- http://m.wap.uliejh.cn/bnews/4569.htm
- http://m.wap.uliejh.cn/bnews/2035350.htm
- http://m.wap.uliejh.cn/bnews/21607.htm
- http://m.wap.uliejh.cn/bnews/6009759.htm
- http://m.wap.uliejh.cn/bnews/4424088.htm
- http://m.wap.uliejh.cn/bnews/1661581.htm
- http://m.wap.uliejh.cn/bnews/119983.htm
- http://m.wap.uliejh.cn/bnews/5734833.htm
- http://m.wap.uliejh.cn/bnews/891224.htm
- http://m.wap.uliejh.cn/bnews/7626.htm
- http://m.wap.uliejh.cn/bnews/2785953.htm
- http://m.wap.uliejh.cn/bnews/1613.htm
- http://m.wap.uliejh.cn/bnews/87838.htm
- http://m.wap.uliejh.cn/bnews/95892.htm
- http://m.wap.uliejh.cn/bnews/4371633.htm
- http://m.wap.uliejh.cn/bnews/36994.htm
- http://m.wap.uliejh.cn/bnews/1478.htm
- http://m.wap.uliejh.cn/bnews/595936.htm
- http://m.wap.uliejh.cn/bnews/832167.htm
- http://m.wap.uliejh.cn/bnews/086312.htm
- http://m.wap.uliejh.cn/bnews/05104.htm
- http://m.wap.uliejh.cn/bnews/003762.htm
- http://m.wap.uliejh.cn/bnews/65821.htm
- http://m.wap.uliejh.cn/bnews/2104969.htm
- http://m.wap.uliejh.cn/bnews/899249.htm
- http://m.wap.uliejh.cn/bnews/204734.htm
- http://m.wap.uliejh.cn/bnews/1517573.htm
- http://m.wap.uliejh.cn/bnews/06068.htm
- http://m.wap.uliejh.cn/bnews/812958.htm
- http://m.wap.uliejh.cn/bnews/675729.htm
- http://m.wap.uliejh.cn/bnews/34287.htm
- http://m.wap.uliejh.cn/bnews/4623615.htm
- http://m.wap.uliejh.cn/bnews/2097378.htm
- http://m.wap.uliejh.cn/bnews/968293.htm
- http://m.wap.uliejh.cn/bnews/256473.htm
- http://m.wap.uliejh.cn/bnews/5347932.htm
- http://m.wap.uliejh.cn/bnews/624099.htm
- http://m.wap.uliejh.cn/bnews/2111015.htm
- http://m.wap.uliejh.cn/bnews/163655.htm
- http://m.wap.uliejh.cn/bnews/0999509.htm
- http://m.wap.uliejh.cn/bnews/744302.htm
- http://m.wap.uliejh.cn/bnews/045235.htm
- http://m.wap.uliejh.cn/bnews/467867.htm
- http://m.wap.uliejh.cn/bnews/017672.htm
- http://m.wap.uliejh.cn/bnews/4662.htm
- http://m.wap.uliejh.cn/bnews/9237831.htm
- http://m.wap.uliejh.cn/bnews/70770.htm
- http://m.wap.uliejh.cn/bnews/92919.htm
- http://m.wap.uliejh.cn/bnews/6008.htm
- http://m.wap.uliejh.cn/bnews/154041.htm
- http://m.wap.uliejh.cn/bnews/64997.htm
- http://m.wap.uliejh.cn/bnews/2556014.htm
- http://m.wap.uliejh.cn/bnews/4582.htm
- http://m.wap.uliejh.cn/bnews/09552.htm
- http://m.wap.uliejh.cn/bnews/105197.htm
- http://m.wap.uliejh.cn/bnews/41556.htm
- http://m.wap.uliejh.cn/bnews/6782761.htm
- http://m.wap.uliejh.cn/bnews/6662274.htm
- http://m.wap.uliejh.cn/bnews/3880235.htm
- http://m.wap.uliejh.cn/bnews/23440.htm
- http://m.wap.uliejh.cn/bnews/704023.htm
- http://m.wap.uliejh.cn/bnews/67287.htm
- http://m.wap.uliejh.cn/bnews/26099.htm
- http://m.wap.uliejh.cn/bnews/7656149.htm
- http://m.wap.uliejh.cn/bnews/6565621.htm
- http://m.wap.uliejh.cn/bnews/87188.htm
- http://m.wap.uliejh.cn/bnews/79424.htm
- http://m.wap.uliejh.cn/bnews/113007.htm
- http://m.wap.uliejh.cn/bnews/834949.htm
- http://m.wap.uliejh.cn/bnews/2651868.htm
- http://m.wap.uliejh.cn/bnews/020141.htm
- http://m.wap.uliejh.cn/bnews/3922308.htm
- http://m.wap.uliejh.cn/bnews/3031.htm
- http://m.wap.uliejh.cn/bnews/933717.htm
- http://m.wap.uliejh.cn/bnews/3771.htm
- http://m.wap.uliejh.cn/bnews/657555.htm
- http://m.wap.uliejh.cn/bnews/8353007.htm
- http://m.wap.uliejh.cn/bnews/076657.htm
- http://m.wap.uliejh.cn/bnews/4214.htm
- http://m.wap.uliejh.cn/bnews/91246.htm
- http://m.wap.uliejh.cn/bnews/3289.htm
- http://m.wap.uliejh.cn/bnews/0399.htm
- http://m.wap.uliejh.cn/bnews/7851.htm
- http://m.wap.uliejh.cn/bnews/58418.htm
- http://m.wap.uliejh.cn/bnews/0929800.htm
- http://m.wap.uliejh.cn/bnews/701544.htm
- http://m.wap.uliejh.cn/bnews/9827731.htm
- http://m.wap.uliejh.cn/bnews/80231.htm
- http://m.wap.uliejh.cn/bnews/73679.htm
- http://m.wap.uliejh.cn/bnews/99190.htm
- http://m.wap.uliejh.cn/bnews/30747.htm
- http://m.wap.uliejh.cn/bnews/18086.htm
- http://m.wap.uliejh.cn/bnews/9257978.htm
- http://m.wap.uliejh.cn/bnews/7076226.htm
- http://m.wap.uliejh.cn/bnews/12979.htm
- http://m.wap.uliejh.cn/bnews/775410.htm
- http://m.wap.uliejh.cn/bnews/0622289.htm
- http://m.wap.uliejh.cn/bnews/4390932.htm
- http://m.wap.uliejh.cn/bnews/8083.htm
- http://m.wap.uliejh.cn/bnews/05661.htm
- http://m.wap.uliejh.cn/bnews/66478.htm
- http://m.wap.uliejh.cn/bnews/4203.htm
- http://m.wap.uliejh.cn/bnews/4663053.htm
- http://m.wap.uliejh.cn/bnews/03825.htm
- http://m.wap.uliejh.cn/bnews/86921.htm
- http://m.wap.uliejh.cn/bnews/94415.htm
- http://m.wap.uliejh.cn/bnews/5552268.htm
- http://m.wap.uliejh.cn/bnews/459231.htm
- http://m.wap.uliejh.cn/bnews/3378328.htm
- http://m.wap.uliejh.cn/bnews/39758.htm
- http://m.wap.uliejh.cn/bnews/49174.htm
- http://m.wap.uliejh.cn/bnews/31520.htm
- http://m.wap.uliejh.cn/bnews/268837.htm
- http://m.wap.uliejh.cn/bnews/66731.htm
- http://m.wap.uliejh.cn/bnews/7617953.htm
- http://m.wap.uliejh.cn/bnews/111501.htm
- http://m.wap.uliejh.cn/bnews/26002.htm
- http://m.wap.uliejh.cn/bnews/19707.htm
- http://m.wap.uliejh.cn/bnews/463614.htm
- http://m.wap.uliejh.cn/bnews/3989.htm
- http://m.wap.uliejh.cn/bnews/56103.htm
- http://m.wap.uliejh.cn/bnews/25568.htm
- http://m.wap.uliejh.cn/bnews/58514.htm
- http://m.wap.uliejh.cn/bnews/361575.htm
- http://m.wap.uliejh.cn/bnews/0050.htm
- http://m.wap.uliejh.cn/bnews/86712.htm
- http://m.wap.uliejh.cn/bnews/47300.htm
- http://m.wap.uliejh.cn/bnews/48188.htm
- http://m.wap.uliejh.cn/bnews/844907.htm
- http://m.wap.uliejh.cn/bnews/7519011.htm
- http://m.wap.uliejh.cn/bnews/88359.htm
- http://m.wap.uliejh.cn/bnews/32972.htm
- http://m.wap.uliejh.cn/bnews/0492984.htm
- http://m.wap.uliejh.cn/bnews/313758.htm
- http://m.wap.uliejh.cn/bnews/370620.htm
- http://m.wap.uliejh.cn/bnews/41252.htm
- http://m.wap.uliejh.cn/bnews/028245.htm
- http://m.wap.uliejh.cn/bnews/1076282.htm
- http://m.wap.uliejh.cn/bnews/4110367.htm
- http://m.wap.uliejh.cn/bnews/5062.htm
- http://m.wap.uliejh.cn/bnews/4866.htm
- http://m.wap.uliejh.cn/bnews/2459858.htm
- http://m.wap.uliejh.cn/bnews/6133512.htm
- http://m.wap.uliejh.cn/bnews/652743.htm
- http://m.wap.uliejh.cn/bnews/623628.htm
- http://m.wap.uliejh.cn/bnews/610379.htm
- http://m.wap.uliejh.cn/bnews/8149.htm
- http://m.wap.uliejh.cn/bnews/1900845.htm
- http://m.wap.uliejh.cn/bnews/1354.htm
- http://m.wap.uliejh.cn/bnews/10270.htm
- http://m.wap.uliejh.cn/bnews/70083.htm
- http://m.wap.uliejh.cn/bnews/4934.htm
- http://m.wap.uliejh.cn/bnews/47134.htm
- http://m.wap.uliejh.cn/bnews/5015068.htm
- http://m.wap.uliejh.cn/bnews/9633.htm
- http://m.wap.uliejh.cn/bnews/27854.htm
- http://m.wap.uliejh.cn/bnews/95640.htm
- http://m.wap.uliejh.cn/bnews/94649.htm
- http://m.wap.uliejh.cn/bnews/65559.htm
- http://m.wap.uliejh.cn/bnews/4706.htm
- http://m.wap.uliejh.cn/bnews/1020406.htm
- http://m.wap.uliejh.cn/bnews/09215.htm
- http://m.wap.uliejh.cn/bnews/6102.htm
- http://m.wap.uliejh.cn/bnews/7737.htm
- http://m.wap.uliejh.cn/bnews/12192.htm
- http://m.wap.uliejh.cn/bnews/26204.htm
- http://m.wap.uliejh.cn/bnews/8304.htm
- http://m.wap.uliejh.cn/bnews/947082.htm
- http://m.wap.uliejh.cn/bnews/463601.htm
- http://m.wap.uliejh.cn/bnews/6037.htm
- http://m.wap.uliejh.cn/bnews/0666.htm
- http://m.wap.uliejh.cn/bnews/5584198.htm
- http://m.wap.uliejh.cn/bnews/1594760.htm
- http://m.wap.uliejh.cn/bnews/202638.htm
- http://m.wap.uliejh.cn/bnews/7286465.htm
- http://m.wap.uliejh.cn/bnews/926525.htm
- http://m.wap.uliejh.cn/bnews/3609.htm
- http://m.wap.uliejh.cn/bnews/37160.htm
- http://m.wap.uliejh.cn/bnews/8535.htm
- http://m.wap.uliejh.cn/bnews/8302.htm
- http://m.wap.uliejh.cn/bnews/477802.htm
- http://m.wap.uliejh.cn/bnews/165319.htm
- http://m.wap.uliejh.cn/bnews/3233153.htm
- http://m.wap.uliejh.cn/bnews/12079.htm
- http://m.wap.uliejh.cn/bnews/9024.htm
- http://m.wap.uliejh.cn/bnews/95621.htm
- http://m.wap.uliejh.cn/bnews/3512.htm
- http://m.wap.uliejh.cn/bnews/8286993.htm
- http://m.wap.uliejh.cn/bnews/730176.htm
- http://m.wap.uliejh.cn/bnews/3235594.htm
- http://m.wap.uliejh.cn/bnews/7932766.htm
- http://m.wap.uliejh.cn/bnews/7279192.htm
- http://m.wap.uliejh.cn/bnews/5701091.htm
- http://m.wap.uliejh.cn/bnews/0779.htm
- http://m.wap.uliejh.cn/bnews/4586.htm
- http://m.wap.uliejh.cn/bnews/850382.htm
- http://m.wap.uliejh.cn/bnews/062597.htm
- http://m.wap.uliejh.cn/bnews/1882303.htm
- http://m.wap.uliejh.cn/bnews/800669.htm
- http://m.wap.uliejh.cn/bnews/4385.htm
- http://m.wap.uliejh.cn/bnews/7617858.htm
- http://m.wap.uliejh.cn/bnews/770896.htm
- http://m.wap.uliejh.cn/bnews/1590990.htm
- http://m.wap.uliejh.cn/bnews/90398.htm
- http://m.wap.uliejh.cn/bnews/389198.htm
- http://m.wap.uliejh.cn/bnews/15488.htm
- http://m.wap.uliejh.cn/bnews/2142219.htm
- http://m.wap.uliejh.cn/bnews/919025.htm
- http://m.wap.uliejh.cn/bnews/29295.htm
- http://m.wap.uliejh.cn/bnews/9846.htm
- http://m.wap.uliejh.cn/bnews/368570.htm
- http://m.wap.uliejh.cn/bnews/7335.htm
- http://m.wap.uliejh.cn/bnews/9328229.htm
- http://m.wap.uliejh.cn/bnews/85195.htm
- http://m.wap.uliejh.cn/bnews/107165.htm
- http://m.wap.uliejh.cn/bnews/31341.htm
- http://m.wap.uliejh.cn/bnews/06011.htm
- http://m.wap.uliejh.cn/bnews/26051.htm
- http://m.wap.uliejh.cn/bnews/256729.htm
- http://m.wap.uliejh.cn/bnews/69912.htm
- http://m.wap.uliejh.cn/bnews/849695.htm
- http://m.wap.uliejh.cn/bnews/97858.htm
- http://m.wap.uliejh.cn/bnews/0226123.htm
- http://m.wap.uliejh.cn/bnews/67148.htm
- http://m.wap.uliejh.cn/bnews/6202455.htm
- http://m.wap.uliejh.cn/bnews/5178581.htm
- http://m.wap.uliejh.cn/bnews/20993.htm
- http://m.wap.uliejh.cn/bnews/006904.htm
- http://m.wap.uliejh.cn/bnews/220075.htm
- http://m.wap.uliejh.cn/bnews/8268.htm
- http://m.wap.uliejh.cn/bnews/6639380.htm
- http://m.wap.uliejh.cn/bnews/3988.htm
- http://m.wap.uliejh.cn/bnews/22081.htm

## 项目结构

```
linkvault/
├── cmd/                                # 命令行入口与子命令定义
│   ├── server/                         # Web 服务器启动入口 (main.go)
│   └── worker/                         # 后台任务工作进程 (健康检查、元数据更新)
├── pkg/                                # 核心库代码（对外不可导入）
│   ├── crawler/                        # 链接抓取与解析引擎，含重试策略、超时控制
│   ├── storage/                        # 数据库访问层，封装 PostgreSQL 连接池与迁移脚本
│   ├── scheduler/                      # 基于 cron 表达式的任务调度器，调用 Celery 或原生队列
│   ├── exporter/                       # 导出模块，支持 json/csv/markdown/html 等格式生成
│   └── validator/                      # URL 规范校验、域名黑名单、协议白名单过滤逻辑
├── internal/                           # 内部工具包，不暴露给外部依赖
│   ├── config/                         # YAML 配置解析与环境变量覆写
│   ├── metrics/                        # Prometheus 指标采集（请求数、延迟、链接状态分布）
│   └── logger/                         # 结构化日志（JSON 格式，支持输出到 stdout 或文件轮转）
├── web/                                # 前端静态资源与模板
│   ├── templates/                      # Go template 或 Jinja2 渲染的仪表板页面
│   └── static/                         # CSS、JavaScript、图表库（ECharts）资源
├── scripts/                            # 运维辅助脚本
│   ├── backup.sh                       # 数据库备份与快照清理
│   ├── migrate.sh                      # 调用 alembic 执行版本升级
│   └── seed_test_data.py               # 注入测试批次（含当前批次 60/120）数据
├── tests/                              # 单元测试与集成测试
│   ├── unit/                           # 对 pkg 下各模块的模拟测试
│   └── integration/                    # 需要真实数据库/Redis 环境的测试用例
├── docs/                               # 文档源文件（见文档导航章节）
├── config.yaml                         # 主配置文件（含数据库连接、调度周期、日志级别）
├── docker-compose.yml                  # 本地开发环境编排（PostgreSQL + Redis + 应用）
├── Dockerfile                          # 多阶段构建镜像，基于 Alpine 减少体积
├── go.mod / go.sum                     # Go 模块依赖管理（假设使用 Go；若 Python 则为 requirements.txt）
├── Makefile                            # 统一构建目标：build、test、run、lint
└── README.md                           # 当前文件
```

## 贡献指南

我们遵循标准 GitHub Flow，所有贡献均通过 Pull Request 进行。请确保在提交前完成以下步骤：

1. 查阅 issue 列表或创建新 issue 描述您希望修复的问题或新增的功能，避免重复工作。对于较大变更，建议先通过 issue 讨论设计方案。

2. 克隆仓库并创建特性分支，分支命名规范为 `feature/简短描述` 或 `fix/问题编号`。本地运行 `make pre-commit` 以触发代码格式化（gofmt/black）、静态检查（golangci-lint/flake8）及单元测试。

3. 编写或更新对应的单元测试与集成测试，确保新代码的测试覆盖率达到 80% 以上。若涉及 API 变更，需同步更新 `/docs/development/api.md` 中的请求示例与错误码说明。

4. 提交 PR 时填写模板中的检查清单，包括是否通过所有测试、是否添加了变更日志条目、是否更新了相关文档。PR 至少需要一位维护者审阅批准后方可合并。

5. 对于外部链接资源列表的更新（如新增批次数据），请将 CSV 或原始 URL 列表放置于 `data/` 目录，并在 PR 描述中附上去重与校验结果统计。

## 常见问题

**Q: 如何处理链接响应超时或被服务器拒绝连接的情况？**

A: LinkVault 在 `config.yaml` 中提供了 `crawler.timeout`（默认 10 秒）和 `crawler.max_retries`（默认 3 次）参数。对于频繁超时的域名，可将其加入 `crawler.slow_domains` 列表单独延长超时阈值。若服务器返回 429 或 503，系统会自动启用指数退避重试，并在连续失败 5 次后将该链接标记为 `suspended`，暂停后续健康检查直至人工复核。

**Q: 能否在不启动 Web 服务的情况下仅运行命令行导入和导出？**

A: 可以。`manage.py`（或 `cmd/cli`）提供了独立的子命令：`ingest` 用于从文件或标准输入读取 URL 列表并写入数据库；`export` 支持按标签、日期范围或状态筛选后输出为 JSON 或 CSV。这些命令不依赖 Redis 或 Celery，仅需要 PostgreSQL 连接，非常适合在 CI 流水线或定时脚本中调用。

**Q: 数据库迁移失败或 schema 版本不一致应如何处理？**

A: 首先检查 `alembic_version` 表确认当前版本号，然后运行 `make migrate -- --sql` 生成即将执行的 SQL 语句进行人工审核。若生产环境不允许自动变更，可将生成的 SQL 交由 DBA 执行。若迁移中途失败，使用 `alembic downgrade -1` 回滚至上一步，修复迁移脚本后重新尝试。建议在 staging 环境先模拟完整迁移流程再应用于生产。

## 许可证

MIT

> 外链数量: 250 | 生成时间: 2026-08-24 23:40:21
