# LinkVault

LinkVault 是一个面向技术内容聚合与外部链接管理的高性能开源链接仓库系统。该项目定位于为开发者、技术博主、研究团队以及内容运营者提供一套结构化、可检索、可审计的外部资源链接管理方案。LinkVault 不仅是一个链接存储库，更是一套包含元数据提取、链接可用性检测、分类标签生成以及访问统计的完整链路管理工具。目标用户包括需要管理大量技术参考链接的文档维护者、需要对外输出资源导航页的社区运营者，以及希望建立个人知识外链体系的独立开发者。

LinkVault 以轻量化部署为核心设计原则，后端基于 Python 与 FastAPI，前端提供极简的管理面板与公共资源展示页面。系统不依赖外部商业 API，所有核心功能均可离线运行，适合部署在低成本的云服务器甚至树莓派等边缘设备上。项目已持续维护超过十八个月，累计管理外链资源超过一万两千条，被超过四十个小型技术社区与个人知识库采用。

## 功能概览

批量导入与结构化存储：支持从 CSV、JSON、Markdown 列表以及浏览器书签导出文件批量导入链接，自动解析标题、描述与标签，并以标准化格式存入 PostgreSQL 数据库。

链接可用性主动探测：内置异步健康检查引擎，可按照可配置周期（默认每二十四小时）对所有存储链接发起 HTTP HEAD 请求，自动标记失效链接并记录响应状态码与响应时间。

智能标签推荐：基于链接 URL 中的域名、路径关键词以及页面标题分词，利用 TF-IDF 算法自动生成候选标签，辅助用户快速完成分类整理。

全文检索与高级筛选：提供基于 PostgreSQL 全文检索引擎的标题与描述搜索能力，同时支持按域名、标签、添加时间范围、可用性状态等多维度组合筛选。

公共资源导航页生成：支持将选定的链接集合渲染为静态 HTML 导航页面，可自定义模板样式，便于对外发布为技术资源导航站或项目文档的外链附录。

访问统计与点击追踪：为每个对外暴露的链接生成唯一跳转短码，记录点击次数、来源 IP 地理区域与 Referer 信息，帮助用户了解资源的实际使用情况。

数据导入导出与备份：提供完整的数据库导入导出命令，支持 YAML 格式的链接集合快照备份，便于版本控制与跨实例迁移。

## 应用场景

技术博客外链管理：技术博主在撰写文章时需引用大量外部文档、论文与工具站。LinkVault 可作为集中式引用仓库，在写作时通过 CLI 工具快速查询并生成标准 Markdown 引用格式，避免重复查找与链接失效问题。

开源项目文档资源页：开源项目维护者可使用 LinkVault 生成项目的「相关资源」导航页，聚合社区教程、插件生态与第三方工具链接，并通过健康检查确保导航页中不包含已失效的外部引用。

技术团队内部知识库外链聚合：研发团队在内部 Wiki 中散落大量参考链接，LinkVault 可定期从 Wiki 标记中抓取链接并统一管理，提供团队共享的检索面板，减少重复性信息查找成本。

技术社区每周资源汇总：技术社区运营人员可每周将社区成员分享的优秀文章、工具与视频链接导入 LinkVault，自动生成带摘要的每周资源汇总页面，并通过点击统计了解社区成员的兴趣偏好。

个人研究文献外链索引：研究人员可将阅读过程中收集的论文预印本、代码仓库与数据集链接统一存入 LinkVault，利用标签与全文检索快速定位特定主题下的历史收藏，提升文献回顾效率。

## 快速开始

以下命令演示了从源码克隆、安装依赖到启动开发服务的完整流程。生产环境部署请参考 `deploy` 目录下的 Docker Compose 配置。

```bash
git clone https://github.com/linkvault/linkvault.git
cd linkvault
python -m venv venv
source venv/bin/activate
pip install -r requirements.txt
cp .env.example .env
python scripts/init_db.py
python scripts/import_demo_data.py
uvicorn main:app --host 0.0.0.0 --port 8000 --reload
```

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|---|---|---|
| Python | 3.10 及以上 | 核心运行环境，类型注解与异步特性依赖 |
| PostgreSQL | 14.0 及以上 | 主数据存储，使用 JSONB 存储扩展元数据 |
| Redis | 6.2 及以上 | 用于缓存链接健康检查结果与短码跳转映射 |
| Node.js | 18.0 及以上 | 仅用于前端管理面板构建，可单独部署 |
| Nginx | 1.20 及以上 | 生产环境推荐反向代理，处理静态资源与负载 |
| Docker | 20.10 及以上 | 可选依赖，用于容器化部署方案 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|---|---|---|
| 用户手册 | docs/user/quick-start.md | 如何快速导入第一批链接并生成导航页 |
| 用户手册 | docs/user/search-syntax.md | 全文检索支持哪些语法与过滤条件 |
| 运维指南 | docs/ops/deployment.md | 如何配置 PostgreSQL 连接池与 Redis 缓存策略 |
| 运维指南 | docs/ops/health-check.md | 链接健康检查引擎的工作机制与调优参数 |
| 开发文档 | docs/dev/api-design.md | 后端 API 路由设计与请求响应模型 |
| 开发文档 | docs/dev/plugin-extension.md | 如何编写自定义标签生成器插件 |

## 资源列表

- http://m.blog.uliejh.cn/snews/04363.htm
- http://m.blog.uliejh.cn/snews/2058542.htm
- http://m.blog.uliejh.cn/snews/0585843.htm
- http://m.blog.uliejh.cn/snews/8737630.htm
- http://m.blog.uliejh.cn/snews/5753.htm
- http://m.blog.uliejh.cn/snews/15966.htm
- http://m.blog.uliejh.cn/snews/513372.htm
- http://m.blog.uliejh.cn/snews/83756.htm
- http://m.blog.uliejh.cn/snews/81372.htm
- http://m.blog.uliejh.cn/snews/0006.htm
- http://m.blog.uliejh.cn/snews/28172.htm
- http://m.blog.uliejh.cn/snews/7804.htm
- http://m.blog.uliejh.cn/snews/7085.htm
- http://m.blog.uliejh.cn/snews/9879.htm
- http://m.blog.uliejh.cn/snews/3020978.htm
- http://m.blog.uliejh.cn/snews/5716.htm
- http://m.blog.uliejh.cn/snews/32996.htm
- http://m.blog.uliejh.cn/snews/6322609.htm
- http://m.blog.uliejh.cn/snews/26090.htm
- http://m.blog.uliejh.cn/snews/81218.htm
- http://m.blog.uliejh.cn/snews/1926077.htm
- http://m.blog.uliejh.cn/snews/7363.htm
- http://m.blog.uliejh.cn/snews/93043.htm
- http://m.blog.uliejh.cn/snews/2054556.htm
- http://m.blog.uliejh.cn/snews/2366965.htm
- http://m.blog.uliejh.cn/snews/9130301.htm
- http://m.blog.uliejh.cn/snews/8461979.htm
- http://m.blog.uliejh.cn/snews/27766.htm
- http://m.blog.uliejh.cn/snews/7266911.htm
- http://m.blog.uliejh.cn/snews/2854.htm
- http://m.blog.uliejh.cn/snews/6105651.htm
- http://m.blog.uliejh.cn/snews/006428.htm
- http://m.blog.uliejh.cn/snews/024628.htm
- http://m.blog.uliejh.cn/snews/74281.htm
- http://m.blog.uliejh.cn/snews/4850.htm
- http://m.blog.uliejh.cn/snews/416507.htm
- http://m.blog.uliejh.cn/snews/44198.htm
- http://m.blog.uliejh.cn/snews/4619.htm
- http://m.blog.uliejh.cn/snews/9349.htm
- http://m.blog.uliejh.cn/snews/68107.htm
- http://m.blog.uliejh.cn/snews/504554.htm
- http://m.blog.uliejh.cn/snews/6707825.htm
- http://m.blog.uliejh.cn/snews/87445.htm
- http://m.blog.uliejh.cn/snews/891076.htm
- http://m.blog.uliejh.cn/snews/2026.htm
- http://m.blog.uliejh.cn/snews/9569.htm
- http://m.blog.uliejh.cn/snews/5166212.htm
- http://m.blog.uliejh.cn/snews/3148.htm
- http://m.blog.uliejh.cn/snews/093017.htm
- http://m.blog.uliejh.cn/snews/1766.htm
- http://m.blog.uliejh.cn/snews/033801.htm
- http://m.blog.uliejh.cn/snews/6986.htm
- http://m.blog.uliejh.cn/snews/0651321.htm
- http://m.blog.uliejh.cn/snews/893814.htm
- http://m.blog.uliejh.cn/snews/71076.htm
- http://m.blog.uliejh.cn/snews/75096.htm
- http://m.blog.uliejh.cn/snews/4254685.htm
- http://m.blog.uliejh.cn/snews/4878429.htm
- http://m.blog.uliejh.cn/snews/59392.htm
- http://m.blog.uliejh.cn/snews/3434.htm
- http://m.blog.uliejh.cn/snews/0091.htm
- http://m.blog.uliejh.cn/snews/54232.htm
- http://m.blog.uliejh.cn/snews/9507.htm
- http://m.blog.uliejh.cn/snews/3309.htm
- http://m.blog.uliejh.cn/snews/80285.htm
- http://m.blog.uliejh.cn/snews/5647153.htm
- http://m.blog.uliejh.cn/snews/2918640.htm
- http://m.blog.uliejh.cn/snews/15099.htm
- http://m.blog.uliejh.cn/snews/49629.htm
- http://m.blog.uliejh.cn/snews/4670634.htm
- http://m.blog.uliejh.cn/snews/1419500.htm
- http://m.blog.uliejh.cn/snews/2415006.htm
- http://m.blog.uliejh.cn/snews/665449.htm
- http://m.blog.uliejh.cn/snews/22480.htm
- http://m.blog.uliejh.cn/snews/0150138.htm
- http://m.blog.uliejh.cn/snews/0440.htm
- http://m.blog.uliejh.cn/snews/92299.htm
- http://m.blog.uliejh.cn/snews/1183090.htm
- http://m.blog.uliejh.cn/snews/950653.htm
- http://m.blog.uliejh.cn/snews/1665.htm
- http://m.blog.uliejh.cn/snews/5429226.htm
- http://m.blog.uliejh.cn/snews/92301.htm
- http://m.blog.uliejh.cn/snews/02384.htm
- http://m.blog.uliejh.cn/snews/0209523.htm
- http://m.blog.uliejh.cn/snews/6191058.htm
- http://m.blog.uliejh.cn/snews/33000.htm
- http://m.blog.uliejh.cn/snews/8693580.htm
- http://m.blog.uliejh.cn/snews/4702.htm
- http://m.blog.uliejh.cn/snews/8375201.htm
- http://m.blog.uliejh.cn/snews/8992.htm
- http://m.blog.uliejh.cn/snews/8321.htm
- http://m.blog.uliejh.cn/snews/7312.htm
- http://m.blog.uliejh.cn/snews/803603.htm
- http://m.blog.uliejh.cn/snews/8882.htm
- http://m.blog.uliejh.cn/snews/2283.htm
- http://m.blog.uliejh.cn/snews/9964740.htm
- http://m.blog.uliejh.cn/snews/3635.htm
- http://m.blog.uliejh.cn/snews/8711263.htm
- http://m.blog.uliejh.cn/snews/7564.htm
- http://m.blog.uliejh.cn/snews/79231.htm
- http://m.blog.uliejh.cn/snews/95579.htm
- http://m.blog.uliejh.cn/snews/82607.htm
- http://m.blog.uliejh.cn/snews/79353.htm
- http://m.blog.uliejh.cn/snews/1875.htm
- http://m.blog.uliejh.cn/snews/26104.htm
- http://m.blog.uliejh.cn/snews/977348.htm
- http://m.blog.uliejh.cn/snews/8985.htm
- http://m.blog.uliejh.cn/snews/7921603.htm
- http://m.blog.uliejh.cn/snews/3502409.htm
- http://m.blog.uliejh.cn/snews/574660.htm
- http://m.blog.uliejh.cn/snews/491626.htm
- http://m.blog.uliejh.cn/snews/02111.htm
- http://m.blog.uliejh.cn/snews/9996.htm
- http://m.blog.uliejh.cn/snews/0341073.htm
- http://m.blog.uliejh.cn/snews/886707.htm
- http://m.blog.uliejh.cn/snews/24923.htm
- http://m.blog.uliejh.cn/snews/2566.htm
- http://m.blog.uliejh.cn/snews/88007.htm
- http://m.blog.uliejh.cn/snews/8183.htm
- http://m.blog.uliejh.cn/snews/812648.htm
- http://m.blog.uliejh.cn/snews/5902835.htm
- http://m.blog.uliejh.cn/snews/01322.htm
- http://m.blog.uliejh.cn/snews/173127.htm
- http://m.blog.uliejh.cn/snews/52544.htm
- http://m.blog.uliejh.cn/snews/2922053.htm
- http://m.blog.uliejh.cn/snews/54226.htm
- http://m.blog.uliejh.cn/snews/30892.htm
- http://m.blog.uliejh.cn/snews/297389.htm
- http://m.blog.uliejh.cn/snews/4406.htm
- http://m.blog.uliejh.cn/snews/237534.htm
- http://m.blog.uliejh.cn/snews/8506474.htm
- http://m.blog.uliejh.cn/snews/931901.htm
- http://m.blog.uliejh.cn/snews/40051.htm
- http://m.blog.uliejh.cn/snews/768727.htm
- http://m.blog.uliejh.cn/snews/2064408.htm
- http://m.blog.uliejh.cn/snews/3570.htm
- http://m.blog.uliejh.cn/snews/930436.htm
- http://m.blog.uliejh.cn/snews/5931409.htm
- http://m.blog.uliejh.cn/snews/55653.htm
- http://m.blog.uliejh.cn/snews/44511.htm
- http://m.blog.uliejh.cn/snews/704470.htm
- http://m.blog.uliejh.cn/snews/020895.htm
- http://m.blog.uliejh.cn/snews/2741.htm
- http://m.blog.uliejh.cn/snews/56953.htm
- http://m.blog.uliejh.cn/snews/8952.htm
- http://m.blog.uliejh.cn/snews/318107.htm
- http://m.blog.uliejh.cn/snews/91928.htm
- http://m.blog.uliejh.cn/snews/7953676.htm
- http://m.blog.uliejh.cn/snews/0678.htm
- http://m.blog.uliejh.cn/snews/69545.htm
- http://m.blog.uliejh.cn/snews/5008.htm
- http://m.blog.uliejh.cn/snews/804725.htm
- http://m.blog.uliejh.cn/snews/5063204.htm
- http://m.blog.uliejh.cn/snews/2258206.htm
- http://m.blog.uliejh.cn/snews/651263.htm
- http://m.blog.uliejh.cn/snews/9894130.htm
- http://m.blog.uliejh.cn/snews/35106.htm
- http://m.blog.uliejh.cn/snews/0239472.htm
- http://m.blog.uliejh.cn/snews/541445.htm
- http://m.blog.uliejh.cn/snews/52998.htm
- http://m.blog.uliejh.cn/snews/49386.htm
- http://m.blog.uliejh.cn/snews/581605.htm
- http://m.blog.uliejh.cn/snews/71089.htm
- http://m.blog.uliejh.cn/snews/6080.htm
- http://m.blog.uliejh.cn/snews/2377.htm
- http://m.blog.uliejh.cn/snews/0103.htm
- http://m.blog.uliejh.cn/snews/85093.htm
- http://m.blog.uliejh.cn/snews/4465.htm
- http://m.blog.uliejh.cn/snews/29772.htm
- http://m.blog.uliejh.cn/snews/973866.htm
- http://m.blog.uliejh.cn/snews/9402687.htm
- http://m.blog.uliejh.cn/snews/8326.htm
- http://m.blog.uliejh.cn/snews/14305.htm
- http://m.blog.uliejh.cn/snews/683283.htm
- http://m.blog.uliejh.cn/snews/6226762.htm
- http://m.blog.uliejh.cn/snews/609564.htm
- http://m.blog.uliejh.cn/snews/24947.htm
- http://m.blog.uliejh.cn/snews/1910722.htm
- http://m.blog.uliejh.cn/snews/48476.htm
- http://m.blog.uliejh.cn/snews/2611.htm
- http://m.blog.uliejh.cn/snews/10810.htm
- http://m.blog.uliejh.cn/snews/544852.htm
- http://m.blog.uliejh.cn/snews/4316.htm
- http://m.blog.uliejh.cn/snews/5941.htm
- http://m.blog.uliejh.cn/snews/522804.htm
- http://m.blog.uliejh.cn/snews/863307.htm
- http://m.blog.uliejh.cn/snews/81393.htm
- http://m.blog.uliejh.cn/snews/95356.htm
- http://m.blog.uliejh.cn/snews/0934604.htm
- http://m.blog.uliejh.cn/snews/4892.htm
- http://m.blog.uliejh.cn/snews/25100.htm
- http://m.blog.uliejh.cn/snews/7476425.htm
- http://m.blog.uliejh.cn/snews/242204.htm
- http://m.blog.uliejh.cn/snews/074895.htm
- http://m.blog.uliejh.cn/snews/247723.htm
- http://m.blog.uliejh.cn/snews/0828204.htm
- http://m.blog.uliejh.cn/snews/6537.htm
- http://m.blog.uliejh.cn/snews/8195.htm
- http://m.blog.uliejh.cn/snews/1634642.htm
- http://m.blog.uliejh.cn/snews/75719.htm
- http://m.blog.uliejh.cn/snews/26301.htm
- http://m.blog.uliejh.cn/snews/87484.htm
- http://m.blog.uliejh.cn/snews/772537.htm
- http://m.blog.uliejh.cn/snews/356272.htm
- http://m.blog.uliejh.cn/snews/2563.htm
- http://m.blog.uliejh.cn/snews/144805.htm
- http://m.blog.uliejh.cn/snews/8011886.htm
- http://m.blog.uliejh.cn/snews/97115.htm
- http://m.blog.uliejh.cn/snews/9069.htm
- http://m.blog.uliejh.cn/snews/3239.htm
- http://m.blog.uliejh.cn/snews/37183.htm
- http://m.blog.uliejh.cn/snews/8527623.htm
- http://m.blog.uliejh.cn/snews/3363.htm
- http://m.blog.uliejh.cn/snews/22177.htm
- http://m.blog.uliejh.cn/snews/8437.htm
- http://m.blog.uliejh.cn/snews/39362.htm
- http://m.blog.uliejh.cn/snews/75674.htm
- http://m.blog.uliejh.cn/snews/2106639.htm
- http://m.blog.uliejh.cn/snews/139138.htm
- http://m.blog.uliejh.cn/snews/5059285.htm
- http://m.blog.uliejh.cn/snews/5714058.htm
- http://m.blog.uliejh.cn/snews/306829.htm
- http://m.blog.uliejh.cn/snews/619089.htm
- http://m.blog.uliejh.cn/snews/5353.htm
- http://m.blog.uliejh.cn/snews/1563.htm
- http://m.blog.uliejh.cn/snews/245446.htm
- http://m.blog.uliejh.cn/snews/712651.htm
- http://m.blog.uliejh.cn/snews/327184.htm
- http://m.blog.uliejh.cn/snews/6549841.htm
- http://m.blog.uliejh.cn/snews/65885.htm
- http://m.blog.uliejh.cn/snews/51606.htm
- http://m.blog.uliejh.cn/snews/0967018.htm
- http://m.blog.uliejh.cn/snews/4836833.htm
- http://m.blog.uliejh.cn/snews/8001324.htm
- http://m.blog.uliejh.cn/snews/6119.htm
- http://m.blog.uliejh.cn/snews/09642.htm
- http://m.blog.uliejh.cn/snews/41364.htm
- http://m.blog.uliejh.cn/snews/10411.htm
- http://m.blog.uliejh.cn/snews/14569.htm
- http://m.blog.uliejh.cn/snews/1342.htm
- http://m.blog.uliejh.cn/snews/005038.htm
- http://m.blog.uliejh.cn/snews/1141.htm
- http://m.blog.uliejh.cn/snews/01958.htm
- http://m.blog.uliejh.cn/snews/6871196.htm
- http://m.blog.uliejh.cn/snews/5821.htm
- http://m.blog.uliejh.cn/snews/83811.htm
- http://m.blog.uliejh.cn/snews/181876.htm
- http://m.blog.uliejh.cn/snews/24215.htm
- http://m.blog.uliejh.cn/snews/236378.htm
- http://m.blog.uliejh.cn/snews/4746.htm

## 项目结构

```
linkvault/
├── main.py                      # FastAPI 应用入口，注册路由与中间件
├── core/
│   ├── config.py                # 环境变量加载与配置对象定义
│   ├── database.py              # PostgreSQL 异步连接池与事务管理
│   └── redis_client.py          # Redis 连接与缓存装饰器实现
├── models/
│   ├── link.py                  # Link 数据模型定义，包含 URL、标题、标签、状态字段
│   ├── tag.py                   # 标签模型与多对多关系映射
│   └── click_log.py             # 点击日志模型，记录访问来源与时间
├── services/
│   ├── health_check.py          # 异步链接探测服务，包含超时与重试策略
│   ├── tag_generator.py         # 基于规则与 TF-IDF 的自动标签生成器
│   ├── search_engine.py         # PostgreSQL 全文检索封装与查询解析器
│   └── static_generator.py      # 从链接集合生成静态 HTML 导航页的模板引擎
├── api/
│   ├── v1/
│   │   ├── links.py             # 链接 CRUD 与批量导入导出接口
│   │   ├── tags.py              # 标签查询与合并接口
│   │   ├── stats.py             # 访问统计与健康检查报告接口
│   │   └── redirect.py          # 短码跳转与点击计数接口
├── scripts/
│   ├── init_db.py               # 初始化数据库表结构与索引
│   ├── import_demo_data.py      # 导入示例链接数据用于快速体验
│   ├── export_snapshot.py       # 导出当前所有链接为 YAML 快照
│   └── health_check_runner.py   # 独立运行的定时健康检查任务脚本
├── web/
│   ├── static/                  # 管理面板的 CSS、JavaScript 与图片资源
│   └── templates/               # Jinja2 模板，包含导航页与仪表盘视图
├── tests/
│   ├── test_health_check.py     # 链接探测服务的单元测试
│   ├── test_search_engine.py    # 全文检索功能的测试用例
│   └── test_tag_generator.py    # 标签生成逻辑的测试覆盖
├── docker-compose.yml           # 包含 PostgreSQL、Redis 与应用的编排配置
├── Dockerfile                   # 基于 Python 3.11 的容器镜像构建文件
├── requirements.txt             # Python 依赖清单，包含 FastAPI、asyncpg、Redis 等
├── .env.example                 # 环境变量配置模板，包含数据库连接串与密钥
└── README.md                    # 项目入口文档
```

## 贡献指南

1. 在 GitHub 上 Fork 本仓库，并克隆到本地开发环境中。请确保本地 Python 版本符合安装要求，并已配置好 PostgreSQL 与 Redis 测试实例。

2. 创建新的功能分支，分支命名遵循 `feature/功能简述` 或 `fix/问题简述` 的格式。所有代码提交前请运行 `make lint` 执行 PEP 8 风格检查与静态类型检测。

3. 编写或更新对应的单元测试，测试文件需放置在 `tests/` 目录下，命名与目标模块保持一致。请确保所有测试用例在本地通过后再发起拉取请求。

4. 若涉及新增配置项或 API 接口变更，请同步更新 `docs/` 目录下的对应文档，并在拉取请求描述中明确标注接口兼容性影响。

5. 提交拉取请求时，请填写完整的变更描述模板，包含改动动机、测试覆盖情况以及是否已通过回归测试。项目维护者将在三个工作日内完成审阅。

## 常见问题

Q: LinkVault 是否支持 SQLite 作为数据库后端以减少部署依赖？

A: 当前版本不提供对 SQLite 的官方支持。LinkVault 重度依赖 PostgreSQL 的全文检索能力（tsvector 与 tsquery）以及 JSONB 字段的高效查询，这些功能在 SQLite 中无法达到同等性能。若需轻量化部署，建议使用项目提供的 Docker Compose 方案，可在单台服务器上快速拉起全部依赖服务。

Q: 链接健康检查是否会对目标网站造成过大请求压力？

A: 健康检查引擎默认使用异步并发控制，最大并发请求数限制为 20，且每个目标域名在五分钟内最多被探测一次。此外，引擎仅发送 HTTP HEAD 请求而非 GET 请求，不会触发目标站点的页面渲染或脚本执行，从而将对目标服务器的负载影响降至最低。用户可在环境变量中调整 `CHECK_CONCURRENCY` 与 `CHECK_INTERVAL_DOMAIN` 参数以进一步适配自身需求。

Q: 如何将现有的浏览器书签或 Pocket 收藏夹批量迁移到 LinkVault？

A: LinkVault 内置的导入脚本支持多种输入格式。对于浏览器书签，请先导出为 HTML 书签文件，然后使用 `scripts/import_bookmarks.py` 进行转换。对于 Pocket 数据，可将 CSV 导出文件直接通过 `/api/v1/links/import` 接口提交。所有导入流程均支持字段映射配置，具体示例可参考 `docs/user/import-guide.md`。

## 许可证

MIT

> 外链数量: 250 | 生成时间: 2026-08-24 23:40:21
