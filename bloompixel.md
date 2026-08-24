# WebLink Collective

WebLink Collective 是一个面向技术研究人员、信息聚合者和内容管理者的外链资源归集与导航系统。该项目定位于将分散在各类信息源中的高价值外链进行结构化整理、分类标注和版本化追踪，解决技术团队在文档沉淀、知识库构建和外部参考溯源过程中面临的链接失效、上下文缺失和检索效率低下等问题。WebLink Collective 本身不生产内容，而是通过严格的链接元数据提取和状态监控机制，为上层应用提供稳定、可查询、可审计的外链数据层。

## 功能概览

- **批量链接导入与归一化**：支持从纯文本、CSV 和 Markdown 列表中批量导入原始 URL，自动完成协议补全检测、末尾斜杠归一化和重复项去重，生成统一的内部资源编号。

- **元数据自动提取与补全**：对每条导入的链接执行可配置的元数据抓取流程，包括页面标题提取、摘要生成、内容类型识别（文章、文档、视频、工具等）和发布时间推断。

- **链接状态健康检查**：内置定时巡检任务，对资源库中的每条外链执行 HTTP 状态码检测、响应时间测量和 TLS 证书有效性验证，标记失效、重定向或内容变更的链接。

- **多级标签与分类体系**：提供扁平标签和树状分类两种组织模式，支持为每条链接赋予多个业务标签，并基于标签组合生成动态分类视图。

- **版本化变更追踪**：记录每条链接从导入到每次元数据更新、状态变更的完整操作日志，支持按时间轴回溯任意资源的修改历史。

- **可编程查询接口**：提供 RESTful API 和命令行工具两种访问方式，支持按域名、标签、状态、导入时间范围等维度进行复杂条件筛选和批量导出。

- **自定义视图与面板**：允许用户基于标签组合和筛选条件保存自定义视图，每个视图可独立配置列表排序、显示字段和刷新策略。

- **变更通知与订阅**：支持为特定标签或分类配置变更订阅，当关联链接出现状态异常、元数据更新或新增资源时，通过 Webhook 或邮件发送通知。

## 应用场景

**技术团队知识库外链管理**：技术团队在编写内部文档、设计文档或技术方案时，经常需要引用外部参考资料。WebLink Collective 可作为团队知识库的外链中台，所有外部引用统一经由平台登记和监控，避免文档中出现失效链接，同时提供统一的引用格式和回溯入口。

**行业信息监控与简报生成**：市场分析人员或行业研究员可将日常关注的媒体专栏、政策发布页和行业报告源批量导入平台，利用定时健康检查感知内容更新，结合标签分类快速生成特定主题的简报素材。

**开源项目依赖资源归档**：开源项目维护者可将项目依赖的文档站点、API 参考、社区论坛和镜像源地址纳入 WebLink Collective 管理，在版本发布时导出稳定的外链清单，确保 Release 资产中的外部引用长期可访问。

**个人知识库外链去重与整理**：知识管理重度用户可将散落在笔记、书签和阅读列表中的大量链接统一导入平台，利用自动去重、标签归类和元数据提取能力，将零散的书签转化为结构化的资源地图。

## 快速开始

以下步骤指导您在本地环境中完成 WebLink Collective 的克隆、安装和首次启动。

```bash
# 克隆项目仓库
git clone https://github.com/weblink-collective/weblink-collective.git
cd weblink-collective

# 安装项目依赖（使用 pip 和虚拟环境）
python -m venv venv
source venv/bin/activate  # Windows 下使用 venv\Scripts\activate
pip install -r requirements.txt

# 初始化配置文件和环境变量
cp .env.example .env
cp config.example.yaml config.yaml

# 执行数据库迁移和初始数据导入
python manage.py migrate
python manage.py loaddata initial_tags

# 启动开发服务器
python manage.py runserver --host 0.0.0.0 --port 8080
```

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|---|---|---|
| Python | 3.9 至 3.11 | 核心运行环境，3.12 及以上版本暂未进行完整兼容性测试 |
| PostgreSQL | 13.0 及以上 | 主数据库，用于存储链接元数据、标签体系和操作日志，支持 JSONB 字段类型 |
| Redis | 6.0 及以上 | 缓存和任务队列后端，用于链接状态检查任务的异步调度和结果缓存 |
| Node.js | 18.0 及以上 | 仅用于前端资源构建，后端运行无需此依赖 |
| Nginx | 1.20 及以上 | 生产环境推荐反向代理服务器，用于静态资源服务和请求负载均衡 |
| Celery Worker | 5.2 及以上 | 作为 Python 包安装，负责执行定时巡检和元数据抓取等异步任务 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|---|---|---|
| 入门指南 | docs/getting-started.md | 如何快速完成首次部署；如何导入第一批链接；如何理解核心数据模型 |
| 运维手册 | docs/operations.md | 如何配置巡检策略；如何监控任务队列；如何备份和恢复数据库 |
| API 参考 | docs/api-reference.md | 如何通过 REST API 查询链接；如何创建批量导入任务；如何订阅变更通知 |
| 架构设计 | docs/architecture.md | 系统由哪些模块组成；各模块间如何通信；数据流向和扩展点在哪里 |

## 资源列表

- http://m.blog.uliejh.cn/snews/700436.htm
- http://m.blog.uliejh.cn/snews/42420.htm
- http://m.blog.uliejh.cn/snews/17598.htm
- http://m.blog.uliejh.cn/snews/97040.htm
- http://m.blog.uliejh.cn/snews/462218.htm
- http://m.blog.uliejh.cn/snews/64636.htm
- http://m.blog.uliejh.cn/snews/4438.htm
- http://m.blog.uliejh.cn/snews/674037.htm
- http://m.blog.uliejh.cn/snews/23839.htm
- http://m.blog.uliejh.cn/snews/8308.htm
- http://m.blog.uliejh.cn/snews/3859.htm
- http://m.blog.uliejh.cn/snews/36573.htm
- http://m.blog.uliejh.cn/snews/884731.htm
- http://m.blog.uliejh.cn/snews/209305.htm
- http://m.blog.uliejh.cn/snews/21290.htm
- http://m.blog.uliejh.cn/snews/7752.htm
- http://m.blog.uliejh.cn/snews/73091.htm
- http://m.blog.uliejh.cn/snews/82230.htm
- http://m.blog.uliejh.cn/snews/52083.htm
- http://m.blog.uliejh.cn/snews/9806.htm
- http://m.blog.uliejh.cn/snews/5385.htm
- http://m.blog.uliejh.cn/snews/86075.htm
- http://m.blog.uliejh.cn/snews/838854.htm
- http://m.blog.uliejh.cn/snews/79234.htm
- http://m.blog.uliejh.cn/snews/5119397.htm
- http://m.blog.uliejh.cn/snews/937611.htm
- http://m.blog.uliejh.cn/snews/6694106.htm
- http://m.blog.uliejh.cn/snews/83592.htm
- http://m.blog.uliejh.cn/snews/28721.htm
- http://m.blog.uliejh.cn/snews/661585.htm
- http://m.blog.uliejh.cn/snews/9849313.htm
- http://m.blog.uliejh.cn/snews/63242.htm
- http://m.blog.uliejh.cn/snews/18719.htm
- http://m.blog.uliejh.cn/snews/8728.htm
- http://m.blog.uliejh.cn/snews/0391.htm
- http://m.blog.uliejh.cn/snews/869796.htm
- http://m.blog.uliejh.cn/snews/1350.htm
- http://m.blog.uliejh.cn/snews/55983.htm
- http://m.blog.uliejh.cn/snews/5181.htm
- http://m.blog.uliejh.cn/snews/01130.htm
- http://m.blog.uliejh.cn/snews/64276.htm
- http://m.blog.uliejh.cn/snews/4079.htm
- http://m.blog.uliejh.cn/snews/789567.htm
- http://m.blog.uliejh.cn/snews/4300360.htm
- http://m.blog.uliejh.cn/snews/2653.htm
- http://m.blog.uliejh.cn/snews/2301.htm
- http://m.blog.uliejh.cn/snews/56611.htm
- http://m.blog.uliejh.cn/snews/3005478.htm
- http://m.blog.uliejh.cn/snews/94639.htm
- http://m.blog.uliejh.cn/snews/196939.htm
- http://m.blog.uliejh.cn/snews/90597.htm
- http://m.blog.uliejh.cn/snews/78152.htm
- http://m.blog.uliejh.cn/snews/642207.htm
- http://m.blog.uliejh.cn/snews/314333.htm
- http://m.blog.uliejh.cn/snews/649286.htm
- http://m.blog.uliejh.cn/snews/5027399.htm
- http://m.blog.uliejh.cn/snews/6773553.htm
- http://m.blog.uliejh.cn/snews/581751.htm
- http://m.blog.uliejh.cn/snews/944379.htm
- http://m.blog.uliejh.cn/snews/62505.htm
- http://m.blog.uliejh.cn/snews/2382.htm
- http://m.blog.uliejh.cn/snews/8054066.htm
- http://m.blog.uliejh.cn/snews/35042.htm
- http://m.blog.uliejh.cn/snews/35764.htm
- http://m.blog.uliejh.cn/snews/54984.htm
- http://m.blog.uliejh.cn/snews/85552.htm
- http://m.blog.uliejh.cn/snews/641345.htm
- http://m.blog.uliejh.cn/snews/34802.htm
- http://m.blog.uliejh.cn/snews/6506669.htm
- http://m.blog.uliejh.cn/snews/962753.htm
- http://m.blog.uliejh.cn/snews/3951758.htm
- http://m.blog.uliejh.cn/snews/487059.htm
- http://m.blog.uliejh.cn/snews/6338295.htm
- http://m.blog.uliejh.cn/snews/55421.htm
- http://m.blog.uliejh.cn/snews/71561.htm
- http://m.blog.uliejh.cn/snews/4833384.htm
- http://m.blog.uliejh.cn/snews/34828.htm
- http://m.blog.uliejh.cn/snews/0146715.htm
- http://m.blog.uliejh.cn/snews/591401.htm
- http://m.blog.uliejh.cn/snews/8544473.htm
- http://m.blog.uliejh.cn/snews/2335.htm
- http://m.blog.uliejh.cn/snews/7313.htm
- http://m.blog.uliejh.cn/snews/147994.htm
- http://m.blog.uliejh.cn/snews/546724.htm
- http://m.blog.uliejh.cn/snews/3481702.htm
- http://m.blog.uliejh.cn/snews/36479.htm
- http://m.blog.uliejh.cn/snews/56464.htm
- http://m.blog.uliejh.cn/snews/720074.htm
- http://m.blog.uliejh.cn/snews/8388114.htm
- http://m.blog.uliejh.cn/snews/0268273.htm
- http://m.blog.uliejh.cn/snews/8058778.htm
- http://m.blog.uliejh.cn/snews/0375.htm
- http://m.blog.uliejh.cn/snews/921310.htm
- http://m.blog.uliejh.cn/snews/32848.htm
- http://m.blog.uliejh.cn/snews/693819.htm
- http://m.blog.uliejh.cn/snews/9431483.htm
- http://m.blog.uliejh.cn/snews/8851.htm
- http://m.blog.uliejh.cn/snews/5095273.htm
- http://m.blog.uliejh.cn/snews/2222.htm
- http://m.blog.uliejh.cn/snews/5774.htm
- http://m.blog.uliejh.cn/snews/2153.htm
- http://m.blog.uliejh.cn/snews/70187.htm
- http://m.blog.uliejh.cn/snews/1975112.htm
- http://m.blog.uliejh.cn/snews/347308.htm
- http://m.blog.uliejh.cn/snews/55269.htm
- http://m.blog.uliejh.cn/snews/67387.htm
- http://m.blog.uliejh.cn/snews/196726.htm
- http://m.blog.uliejh.cn/snews/112008.htm
- http://m.blog.uliejh.cn/snews/1941.htm
- http://m.blog.uliejh.cn/snews/37744.htm
- http://m.blog.uliejh.cn/snews/67647.htm
- http://m.blog.uliejh.cn/snews/43644.htm
- http://m.blog.uliejh.cn/snews/7676533.htm
- http://m.blog.uliejh.cn/snews/2963.htm
- http://m.blog.uliejh.cn/snews/978902.htm
- http://m.blog.uliejh.cn/snews/2851.htm
- http://m.blog.uliejh.cn/snews/073002.htm
- http://m.blog.uliejh.cn/snews/8455470.htm
- http://m.blog.uliejh.cn/snews/2772367.htm
- http://m.blog.uliejh.cn/snews/353103.htm
- http://m.blog.uliejh.cn/snews/9282.htm
- http://m.blog.uliejh.cn/snews/4205.htm
- http://m.blog.uliejh.cn/snews/0531.htm
- http://m.blog.uliejh.cn/snews/778763.htm
- http://m.blog.uliejh.cn/snews/7843.htm
- http://m.blog.uliejh.cn/snews/4809465.htm
- http://m.blog.uliejh.cn/snews/8988358.htm
- http://m.blog.uliejh.cn/snews/193962.htm
- http://m.blog.uliejh.cn/snews/5826.htm
- http://m.blog.uliejh.cn/snews/727475.htm
- http://m.blog.uliejh.cn/snews/2383468.htm
- http://m.blog.uliejh.cn/snews/59004.htm
- http://m.blog.uliejh.cn/snews/2918580.htm
- http://m.blog.uliejh.cn/snews/95565.htm
- http://m.blog.uliejh.cn/snews/1083774.htm
- http://m.blog.uliejh.cn/snews/58678.htm
- http://m.blog.uliejh.cn/snews/36608.htm
- http://m.blog.uliejh.cn/snews/7334.htm
- http://m.blog.uliejh.cn/snews/56589.htm
- http://m.blog.uliejh.cn/snews/8708094.htm
- http://m.blog.uliejh.cn/snews/7479.htm
- http://m.blog.uliejh.cn/snews/834951.htm
- http://m.blog.uliejh.cn/snews/251537.htm
- http://m.blog.uliejh.cn/snews/1739429.htm
- http://m.blog.uliejh.cn/snews/8428.htm
- http://m.blog.uliejh.cn/snews/71423.htm
- http://m.blog.uliejh.cn/snews/93722.htm
- http://m.blog.uliejh.cn/snews/16679.htm
- http://m.blog.uliejh.cn/snews/491774.htm
- http://m.blog.uliejh.cn/snews/11842.htm
- http://m.blog.uliejh.cn/snews/4952.htm
- http://m.blog.uliejh.cn/snews/97790.htm
- http://m.blog.uliejh.cn/snews/7395814.htm
- http://m.blog.uliejh.cn/snews/4854.htm
- http://m.blog.uliejh.cn/snews/2623.htm
- http://m.blog.uliejh.cn/snews/8449665.htm
- http://m.blog.uliejh.cn/snews/95291.htm
- http://m.blog.uliejh.cn/snews/850868.htm
- http://m.blog.uliejh.cn/snews/709001.htm
- http://m.blog.uliejh.cn/snews/9341.htm
- http://m.blog.uliejh.cn/snews/9683869.htm
- http://m.blog.uliejh.cn/snews/43186.htm
- http://m.blog.uliejh.cn/snews/4325463.htm
- http://m.blog.uliejh.cn/snews/4657602.htm
- http://m.blog.uliejh.cn/snews/539299.htm
- http://m.blog.uliejh.cn/snews/7159368.htm
- http://m.blog.uliejh.cn/snews/3350752.htm
- http://m.blog.uliejh.cn/snews/3514145.htm
- http://m.blog.uliejh.cn/snews/912456.htm
- http://m.blog.uliejh.cn/snews/69251.htm
- http://m.blog.uliejh.cn/snews/1858.htm
- http://m.blog.uliejh.cn/snews/1093703.htm
- http://m.blog.uliejh.cn/snews/96348.htm
- http://m.blog.uliejh.cn/snews/8345.htm
- http://m.blog.uliejh.cn/snews/23872.htm
- http://m.blog.uliejh.cn/snews/3332559.htm
- http://m.blog.uliejh.cn/snews/960753.htm
- http://m.blog.uliejh.cn/snews/230875.htm
- http://m.blog.uliejh.cn/snews/86164.htm
- http://m.blog.uliejh.cn/snews/4354964.htm
- http://m.blog.uliejh.cn/snews/602633.htm
- http://m.blog.uliejh.cn/snews/632651.htm
- http://m.blog.uliejh.cn/snews/0912.htm
- http://m.blog.uliejh.cn/snews/662885.htm
- http://m.blog.uliejh.cn/snews/933534.htm
- http://m.blog.uliejh.cn/snews/4332.htm
- http://m.blog.uliejh.cn/snews/661114.htm
- http://m.blog.uliejh.cn/snews/84996.htm
- http://m.blog.uliejh.cn/snews/009488.htm
- http://m.blog.uliejh.cn/snews/13177.htm
- http://m.blog.uliejh.cn/snews/868006.htm
- http://m.blog.uliejh.cn/snews/71888.htm
- http://m.blog.uliejh.cn/snews/798212.htm
- http://m.blog.uliejh.cn/snews/652909.htm
- http://m.blog.uliejh.cn/snews/6611594.htm
- http://m.blog.uliejh.cn/snews/147702.htm
- http://m.blog.uliejh.cn/snews/7368.htm
- http://m.blog.uliejh.cn/snews/1690.htm
- http://m.blog.uliejh.cn/snews/284047.htm
- http://m.blog.uliejh.cn/snews/4996.htm
- http://m.blog.uliejh.cn/snews/1832152.htm
- http://m.blog.uliejh.cn/snews/80894.htm
- http://m.blog.uliejh.cn/snews/910835.htm
- http://m.blog.uliejh.cn/snews/8396.htm
- http://m.blog.uliejh.cn/snews/5540.htm
- http://m.blog.uliejh.cn/snews/4773456.htm
- http://m.blog.uliejh.cn/snews/6110810.htm
- http://m.blog.uliejh.cn/snews/0771571.htm
- http://m.blog.uliejh.cn/snews/4784194.htm
- http://m.blog.uliejh.cn/snews/427149.htm
- http://m.blog.uliejh.cn/snews/47243.htm
- http://m.blog.uliejh.cn/snews/6505059.htm
- http://m.blog.uliejh.cn/snews/12218.htm
- http://m.blog.uliejh.cn/snews/883748.htm
- http://m.blog.uliejh.cn/snews/8859216.htm
- http://m.blog.uliejh.cn/snews/681782.htm
- http://m.blog.uliejh.cn/snews/5117545.htm
- http://m.blog.uliejh.cn/snews/0448.htm
- http://m.blog.uliejh.cn/snews/02021.htm
- http://m.blog.uliejh.cn/snews/03272.htm
- http://m.blog.uliejh.cn/snews/2217019.htm
- http://m.blog.uliejh.cn/snews/47103.htm
- http://m.blog.uliejh.cn/snews/881674.htm
- http://m.blog.uliejh.cn/snews/81836.htm
- http://m.blog.uliejh.cn/snews/3823.htm
- http://m.blog.uliejh.cn/snews/8947260.htm
- http://m.blog.uliejh.cn/snews/1994658.htm
- http://m.blog.uliejh.cn/snews/53809.htm
- http://m.blog.uliejh.cn/snews/4993.htm
- http://m.blog.uliejh.cn/snews/4383.htm
- http://m.blog.uliejh.cn/snews/9345891.htm
- http://m.blog.uliejh.cn/snews/183659.htm
- http://m.blog.uliejh.cn/snews/0625.htm
- http://m.blog.uliejh.cn/snews/24016.htm
- http://m.blog.uliejh.cn/snews/1155.htm
- http://m.blog.uliejh.cn/snews/454242.htm
- http://m.blog.uliejh.cn/snews/1861406.htm
- http://m.blog.uliejh.cn/snews/7692.htm
- http://m.blog.uliejh.cn/snews/3959868.htm
- http://m.blog.uliejh.cn/snews/64304.htm
- http://m.blog.uliejh.cn/snews/968670.htm
- http://m.blog.uliejh.cn/snews/11108.htm
- http://m.blog.uliejh.cn/snews/952990.htm
- http://m.blog.uliejh.cn/snews/7282650.htm
- http://m.blog.uliejh.cn/snews/9088776.htm
- http://m.blog.uliejh.cn/snews/291876.htm
- http://m.blog.uliejh.cn/snews/7279516.htm
- http://m.blog.uliejh.cn/snews/08175.htm
- http://m.blog.uliejh.cn/snews/8213.htm
- http://m.blog.uliejh.cn/snews/297318.htm

## 项目结构

```
weblink-collective/
├── cmd/                                 # 命令行入口程序
│   ├── server/                          # Web 服务启动入口
│   │   └── main.go                      # 主服务进程启动逻辑，含信号处理和优雅停机
│   └── worker/                          # 异步任务工作进程
│       └── main.go                      # Celery 风格任务消费者的启动入口
├── internal/                            # 内部私有包，不对外暴露
│   ├── core/                            # 核心业务逻辑
│   │   ├── link.go                      # 链接实体定义、状态机与归一化算法
│   │   ├── tag.go                       # 标签与分类树的核心数据结构和操作
│   │   └── pipeline.go                  # 链接导入流水线，包含去重、校验和元数据提取编排
│   ├── storage/                         # 存储层实现
│   │   ├── postgres.go                  # PostgreSQL 数据库连接池与 CRUD 操作
│   │   ├── redis.go                     # Redis 缓存与分布式锁封装
│   │   └── migrations/                  # 数据库版本迁移脚本
│   ├── checker/                         # 链接健康检查模块
│   │   ├── http.go                      # HTTP 状态码与响应时间检测
│   │   ├── tls.go                       # TLS 证书有效期与协议版本检测
│   │   └── scheduler.go                 # 巡检任务的定时调度与并发控制
│   └── collector/                       # 元数据采集模块
│       ├── fetcher.go                   # 页面内容获取与编码处理
│       ├── parser.go                    # 基于 goquery 的 HTML 元数据解析
│       └── extractor.go                 # 结构化数据抽取（JSON-LD、Open Graph）
├── pkg/                                 # 可被外部引用的公共库
│   ├── api/                             # RESTful API 的路由定义与中间件
│   │   ├── handler.go                   # 链接、标签、视图等资源的 HTTP 处理器
│   │   └── response.go                  # 统一响应格式与错误码定义
│   ├── config/                          # 配置加载与解析
│   │   └── config.go                    # 支持 YAML 和 ENV 两种配置源，含默认值
│   └── queue/                           # 任务队列客户端封装
│       └── client.go                    # 基于 Redis 的延迟任务和优先级队列
├── web/                                 # 前端静态资源与构建产物
│   ├── static/                          # CSS、JavaScript 和图片资源
│   └── templates/                       # 服务端渲染的 HTML 模板（管理后台）
├── scripts/                             # 运维与开发辅助脚本
│   ├── setup_dev.sh                     # 开发环境一键初始化
│   └── health_check.sh                  # 生产环境健康状态探测脚本
├── config.example.yaml                  # 配置示例文件，含所有可配置项注释
├── .env.example                         # 环境变量示例，含数据库连接和密钥占位
├── go.mod                               # Go 模块依赖定义
├── go.sum                               # 依赖版本锁定文件
├── Makefile                             # 常用构建任务封装（build、test、lint）
└── README.md                            # 项目说明文档（本文件）
```

## 贡献指南

1. **选择或创建 Issue**：在提交代码变更之前，请先在 Issues 列表中查找是否存在相关讨论。对于新功能或较大规模的改动，建议先创建一个 Issue 描述您的设计思路和实现计划，以便维护者和其他贡献者提前提供反馈。

2. **派生仓库并创建功能分支**：将主仓库派生至个人账户下，基于主分支创建一个描述性的功能分支。分支命名建议采用 `feature/功能简述` 或 `fix/问题简述` 的格式，例如 `feature/support-import-csv`。

3. **编写测试用例与代码**：所有新增功能或缺陷修复均需包含对应的单元测试或集成测试。测试覆盖率不应低于现有基准。代码风格需遵循项目配置的 golint 和 gofmt 规则，提交前请执行 `make lint` 和 `make test` 确保全部通过。

4. **编写或更新文档**：对于影响用户可见行为或配置方式的变更，需同步更新 README 或对应 docs 目录下的文档。文档更新应与代码变更放在同一个提交中，以保持原子性。

5. **提交 Pull Request**：向主仓库的 main 分支提交 Pull Request。PR 描述中请引用相关的 Issue 编号，并清晰列出本次变更的内容摘要、测试结果和任何破坏性变更说明。PR 合并前至少需要一名维护者进行 Code Review。

## 常见问题

**Q：导入的链接出现重复，系统如何处理？**

系统在导入流水线中会基于 URL 的归一化形式（协议统一为小写、移除末尾斜杠、解码百分号编码）进行精确去重。如果检测到重复，系统会跳过新导入的链接并记录一条警告日志，同时保留原始链接的所有历史元数据。您可以在导入任务的结果报告中查看被跳过的重复记录。

**Q：链接健康检查的频率和超时时间如何配置？**

健康检查的全局调度策略在 `config.yaml` 中的 `checker.schedule` 字段配置，支持 cron 表达式或固定间隔两种方式。单次检查的 HTTP 超时时间由 `checker.http_timeout_seconds` 控制，默认值为 10 秒。对于响应较慢的目标站点，建议通过环境变量 `CHECKER_HTTP_TIMEOUT` 调整为更大的值。

**Q：如何批量更新已有链接的标签分类？**

您可以使用命令行工具执行批量更新操作，命令格式为 `weblink-cli tag batch --id-file ids.txt --add tech --remove archive`，其中 `ids.txt` 为每行一个内部资源 ID 的文本文件。也可通过 API 接口 `POST /api/v1/links/batch/tags` 提交 JSON 格式的批量更新请求，请求体需包含 `ids` 数组和 `add_tags`、`remove_tags` 字段。

## 许可证

MIT

> 外链数量: 250 | 生成时间: 2026-08-24 23:40:21
