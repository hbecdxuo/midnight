# WebLink Archive Navigator

WebLink Archive Navigator 是一个面向技术研究人员、数据归档工程师和内容策展人的轻量级外链资源汇总与导航系统。该项目旨在解决分散在网络各处的技术文章、新闻动态与参考链接难以统一收集、分类检索和长期保存的问题，通过结构化的索引机制将大量原始 URL 转换为可浏览、可查询、可版本化的知识库入口。

本项目定位于中大型外链集合的快速接入层，不提供全文抓取或内容渲染功能，而是以高效的路由映射和标签化分类为核心，为上层应用（如知识库、监控系统、自动化报告生成器）提供稳定的链接索引服务。当前批次为第 88/120 批，共计收录 250 个资源链接，覆盖技术博客、行业新闻、项目文档等多种类型。

## 功能概览

批量链接导入：支持以文本列表、CSV 或 JSON 格式一次导入数百个外部 URL，自动进行去重和格式校验。

分类标签系统：每个链接可绑定多个自定义标签（如 "backend"、"security"、"release-notes"），支持按标签快速筛选。

状态监控面板：定时检测每个链接的可达性，返回 HTTP 状态码与响应时间，标记失效或重定向链接。

元数据提取：自动从目标页面提取标题、描述、关键词和发布日期，作为检索与排序的依据。

只读视图模式：提供适合大屏展示和打印的只读列表视图，隐藏编辑入口，适用于监控大屏或会议室展示。

全文检索：基于标题和标签构建倒排索引，支持布尔查询和模糊匹配，响应时间控制在 200 毫秒以内。

导出与报告：支持将当前链接列表导出为 Markdown、HTML 或 JSON 格式，便于嵌入其他文档系统。

访问控制：基于 IP 白名单或简单令牌的只读访问限制，适用于内网部署或私有化场景。

## 应用场景

技术团队内部知识库构建：开发团队可将日常阅读的技术博客、问题排查帖、官方更新公告统一录入系统，按微服务、数据库、前端框架等维度打标，形成团队共享的知识入口，减少重复搜索成本。

自动化日报生成：运维人员可配置定时任务，每日凌晨拉取所有链接并检测状态，将失效链接和新出现的 404 错误汇总成日报邮件发送给相关负责人，辅助站点健康度管理。

学术文献与参考资料归档：研究人员在撰写论文或技术报告时，可将引用的网络资源全部导入系统，利用元数据提取功能自动生成参考文献初稿，并持续跟踪链接可用性，避免引用失效。

产品需求与竞品动态跟踪：产品经理可将竞品官网、更新日志、行业分析报告等链接集中管理，通过状态监控第一时间发现竞品页面更新，为决策提供情报支持。

大型开源项目外部依赖索引：开源项目维护者可将依赖库的文档、issue 列表、CI 状态页面等外链统一收录，方便新贡献者快速找到所有相关外部资源。

## 快速开始

以下命令演示了从克隆代码到启动服务的完整流程。

```bash
git clone https://github.com/example/weblink-archive-navigator.git
cd weblink-archive-navigator
pip install -r requirements.txt
python manage.py migrate
python manage.py load_links --batch 88 --file ./data/batch_88.txt
python manage.py runserver --host 0.0.0.0 --port 8080
```

执行上述命令后，服务将在本地 8080 端口启动。访问 http://localhost:8080 即可进入导航面板首页。如需导入本批次提供的 URL 列表，请将原始链接逐行保存为 batch_88.txt 文件，然后执行 load_links 命令。

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|---|---|---|
| Python | 3.10 及以上 | 核心运行环境，建议使用 3.11 LTS |
| Django | 4.2 LTS | Web 框架，用于路由、ORM 和管理界面 |
| PostgreSQL | 14.0 及以上 | 主要数据库，存储链接元数据和标签关系 |
| Redis | 7.0 及以上 | 缓存层，用于检索结果缓存和会话存储 |
| Celery | 5.3 及以上 | 异步任务队列，用于链接状态检测和元数据抓取 |
| Node.js | 18.0 及以上 | 前端构建工具依赖，仅开发模式需要 |
| Nginx | 1.24 及以上 | 生产环境反向代理和静态文件服务（推荐） |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|---|---|---|
| 用户手册 | /docs/user-guide/ | 如何导入链接、如何打标签、如何导出报告、如何配置监控频率 |
| 运维手册 | /docs/ops-guide/ | 如何部署到生产环境、如何备份数据库、如何扩展 worker 节点 |
| API 参考 | /docs/api-reference/ | 如何通过 REST API 进行链接增删改查、如何调用状态检测接口 |
| 架构设计 | /docs/architecture/ | 系统模块如何划分、数据流如何流转、缓存策略与失效机制 |
| 贡献者指南 | /docs/contributing/ | 代码风格规范、测试用例编写要求、PR 提交流程 |

## 资源列表

- http://m.blog.uliejh.cn/snews/888740.htm
- http://m.blog.uliejh.cn/snews/5991138.htm
- http://m.blog.uliejh.cn/snews/2237.htm
- http://m.blog.uliejh.cn/snews/8501.htm
- http://m.blog.uliejh.cn/snews/3578384.htm
- http://m.blog.uliejh.cn/snews/80345.htm
- http://m.blog.uliejh.cn/snews/288495.htm
- http://m.blog.uliejh.cn/snews/3075572.htm
- http://m.blog.uliejh.cn/snews/5651826.htm
- http://m.blog.uliejh.cn/snews/0182.htm
- http://m.blog.uliejh.cn/snews/82128.htm
- http://m.blog.uliejh.cn/snews/980843.htm
- http://m.blog.uliejh.cn/snews/29380.htm
- http://m.blog.uliejh.cn/snews/9004077.htm
- http://m.blog.uliejh.cn/snews/299892.htm
- http://m.blog.uliejh.cn/snews/4930.htm
- http://m.blog.uliejh.cn/snews/25828.htm
- http://m.blog.uliejh.cn/snews/1038838.htm
- http://m.blog.uliejh.cn/snews/896216.htm
- http://m.blog.uliejh.cn/snews/7601.htm
- http://m.blog.uliejh.cn/snews/7550.htm
- http://m.blog.uliejh.cn/snews/912189.htm
- http://m.blog.uliejh.cn/snews/6438252.htm
- http://m.blog.uliejh.cn/snews/5743.htm
- http://m.blog.uliejh.cn/snews/3447657.htm
- http://m.blog.uliejh.cn/snews/644463.htm
- http://m.blog.uliejh.cn/snews/2021314.htm
- http://m.blog.uliejh.cn/snews/69632.htm
- http://m.blog.uliejh.cn/snews/274806.htm
- http://m.blog.uliejh.cn/snews/3524777.htm
- http://m.blog.uliejh.cn/snews/1731.htm
- http://m.blog.uliejh.cn/snews/66700.htm
- http://m.blog.uliejh.cn/snews/4191035.htm
- http://m.blog.uliejh.cn/snews/1119.htm
- http://m.blog.uliejh.cn/snews/775577.htm
- http://m.blog.uliejh.cn/snews/866553.htm
- http://m.blog.uliejh.cn/snews/8675.htm
- http://m.blog.uliejh.cn/snews/2997677.htm
- http://m.blog.uliejh.cn/snews/00310.htm
- http://m.blog.uliejh.cn/snews/807836.htm
- http://m.blog.uliejh.cn/snews/61156.htm
- http://m.blog.uliejh.cn/snews/3411191.htm
- http://m.blog.uliejh.cn/snews/2455.htm
- http://m.blog.uliejh.cn/snews/5375572.htm
- http://m.blog.uliejh.cn/snews/99152.htm
- http://m.blog.uliejh.cn/snews/9831913.htm
- http://m.blog.uliejh.cn/snews/679820.htm
- http://m.blog.uliejh.cn/snews/974966.htm
- http://m.blog.uliejh.cn/snews/38557.htm
- http://m.blog.uliejh.cn/snews/76453.htm
- http://m.blog.uliejh.cn/snews/2781.htm
- http://m.blog.uliejh.cn/snews/1045776.htm
- http://m.blog.uliejh.cn/snews/717266.htm
- http://m.blog.uliejh.cn/snews/31111.htm
- http://m.blog.uliejh.cn/snews/06055.htm
- http://m.blog.uliejh.cn/snews/7557.htm
- http://m.blog.uliejh.cn/snews/778007.htm
- http://m.blog.uliejh.cn/snews/5773.htm
- http://m.blog.uliejh.cn/snews/008642.htm
- http://m.blog.uliejh.cn/snews/1570786.htm
- http://m.blog.uliejh.cn/snews/139876.htm
- http://m.blog.uliejh.cn/snews/6351.htm
- http://m.blog.uliejh.cn/snews/1900489.htm
- http://m.blog.uliejh.cn/snews/311339.htm
- http://m.blog.uliejh.cn/snews/53094.htm
- http://m.blog.uliejh.cn/snews/466512.htm
- http://m.blog.uliejh.cn/snews/0988939.htm
- http://m.blog.uliejh.cn/snews/3368.htm
- http://m.blog.uliejh.cn/snews/8332250.htm
- http://m.blog.uliejh.cn/snews/8367911.htm
- http://m.blog.uliejh.cn/snews/487768.htm
- http://m.blog.uliejh.cn/snews/2784.htm
- http://m.blog.uliejh.cn/snews/3176468.htm
- http://m.blog.uliejh.cn/snews/2541.htm
- http://m.blog.uliejh.cn/snews/46997.htm
- http://m.blog.uliejh.cn/snews/703407.htm
- http://m.blog.uliejh.cn/snews/0609.htm
- http://m.blog.uliejh.cn/snews/1267902.htm
- http://m.blog.uliejh.cn/snews/991512.htm
- http://m.blog.uliejh.cn/snews/7425.htm
- http://m.blog.uliejh.cn/snews/9841779.htm
- http://m.blog.uliejh.cn/snews/94072.htm
- http://m.blog.uliejh.cn/snews/70490.htm
- http://m.blog.uliejh.cn/snews/8507945.htm
- http://m.blog.uliejh.cn/snews/149713.htm
- http://m.blog.uliejh.cn/snews/48680.htm
- http://m.blog.uliejh.cn/snews/35367.htm
- http://m.blog.uliejh.cn/snews/931908.htm
- http://m.blog.uliejh.cn/snews/3725583.htm
- http://m.blog.uliejh.cn/snews/724691.htm
- http://m.blog.uliejh.cn/snews/0979.htm
- http://m.blog.uliejh.cn/snews/516162.htm
- http://m.blog.uliejh.cn/snews/0618.htm
- http://m.blog.uliejh.cn/snews/47386.htm
- http://m.blog.uliejh.cn/snews/083000.htm
- http://m.blog.uliejh.cn/snews/1254432.htm
- http://m.blog.uliejh.cn/snews/091959.htm
- http://m.blog.uliejh.cn/snews/7991.htm
- http://m.blog.uliejh.cn/snews/3553738.htm
- http://m.blog.uliejh.cn/snews/62031.htm
- http://m.blog.uliejh.cn/snews/3575745.htm
- http://m.blog.uliejh.cn/snews/4591268.htm
- http://m.blog.uliejh.cn/snews/4135284.htm
- http://m.blog.uliejh.cn/snews/9612810.htm
- http://m.blog.uliejh.cn/snews/0918.htm
- http://m.blog.uliejh.cn/snews/0305531.htm
- http://m.blog.uliejh.cn/snews/29192.htm
- http://m.blog.uliejh.cn/snews/43040.htm
- http://m.blog.uliejh.cn/snews/037866.htm
- http://m.blog.uliejh.cn/snews/3254.htm
- http://m.blog.uliejh.cn/snews/47986.htm
- http://m.blog.uliejh.cn/snews/515247.htm
- http://m.blog.uliejh.cn/snews/48325.htm
- http://m.blog.uliejh.cn/snews/978842.htm
- http://m.blog.uliejh.cn/snews/1517.htm
- http://m.blog.uliejh.cn/snews/84646.htm
- http://m.blog.uliejh.cn/snews/89324.htm
- http://m.blog.uliejh.cn/snews/10379.htm
- http://m.blog.uliejh.cn/snews/73649.htm
- http://m.blog.uliejh.cn/snews/117387.htm
- http://m.blog.uliejh.cn/snews/1745.htm
- http://m.blog.uliejh.cn/snews/698139.htm
- http://m.blog.uliejh.cn/snews/41534.htm
- http://m.blog.uliejh.cn/snews/8225.htm
- http://m.blog.uliejh.cn/snews/5496792.htm
- http://m.blog.uliejh.cn/snews/2415534.htm
- http://m.blog.uliejh.cn/snews/7795984.htm
- http://m.blog.uliejh.cn/snews/7659621.htm
- http://m.blog.uliejh.cn/snews/413990.htm
- http://m.blog.uliejh.cn/snews/9059079.htm
- http://m.blog.uliejh.cn/snews/3760.htm
- http://m.blog.uliejh.cn/snews/0153894.htm
- http://m.blog.uliejh.cn/snews/3271902.htm
- http://m.blog.uliejh.cn/snews/704003.htm
- http://m.blog.uliejh.cn/snews/01397.htm
- http://m.blog.uliejh.cn/snews/917515.htm
- http://m.blog.uliejh.cn/snews/086555.htm
- http://m.blog.uliejh.cn/snews/5424.htm
- http://m.blog.uliejh.cn/snews/6452.htm
- http://m.blog.uliejh.cn/snews/7838.htm
- http://m.blog.uliejh.cn/snews/6978.htm
- http://m.blog.uliejh.cn/snews/940861.htm
- http://m.blog.uliejh.cn/snews/1585870.htm
- http://m.blog.uliejh.cn/snews/0014445.htm
- http://m.blog.uliejh.cn/snews/5012422.htm
- http://m.blog.uliejh.cn/snews/10140.htm
- http://m.blog.uliejh.cn/snews/31896.htm
- http://m.blog.uliejh.cn/snews/6616124.htm
- http://m.blog.uliejh.cn/snews/27916.htm
- http://m.blog.uliejh.cn/snews/4142.htm
- http://m.blog.uliejh.cn/snews/8131.htm
- http://m.blog.uliejh.cn/snews/255912.htm
- http://m.blog.uliejh.cn/snews/48039.htm
- http://m.blog.uliejh.cn/snews/5892318.htm
- http://m.blog.uliejh.cn/snews/8640.htm
- http://m.blog.uliejh.cn/snews/5542738.htm
- http://m.blog.uliejh.cn/snews/45468.htm
- http://m.blog.uliejh.cn/snews/24112.htm
- http://m.blog.uliejh.cn/snews/54546.htm
- http://m.blog.uliejh.cn/snews/80734.htm
- http://m.blog.uliejh.cn/snews/02467.htm
- http://m.blog.uliejh.cn/snews/1228002.htm
- http://m.blog.uliejh.cn/snews/9785138.htm
- http://m.blog.uliejh.cn/snews/061563.htm
- http://m.blog.uliejh.cn/snews/78901.htm
- http://m.blog.uliejh.cn/snews/16849.htm
- http://m.blog.uliejh.cn/snews/41157.htm
- http://m.blog.uliejh.cn/snews/075358.htm
- http://m.blog.uliejh.cn/snews/772074.htm
- http://m.blog.uliejh.cn/snews/8209553.htm
- http://m.blog.uliejh.cn/snews/794105.htm
- http://m.blog.uliejh.cn/snews/48817.htm
- http://m.blog.uliejh.cn/snews/668866.htm
- http://m.blog.uliejh.cn/snews/953244.htm
- http://m.blog.uliejh.cn/snews/2245850.htm
- http://m.blog.uliejh.cn/snews/569692.htm
- http://m.blog.uliejh.cn/snews/220457.htm
- http://m.blog.uliejh.cn/snews/8520042.htm
- http://m.blog.uliejh.cn/snews/9238.htm
- http://m.blog.uliejh.cn/snews/7508411.htm
- http://m.blog.uliejh.cn/snews/71839.htm
- http://m.blog.uliejh.cn/snews/07234.htm
- http://m.blog.uliejh.cn/snews/8442.htm
- http://m.blog.uliejh.cn/snews/6437710.htm
- http://m.blog.uliejh.cn/snews/227447.htm
- http://m.blog.uliejh.cn/snews/62102.htm
- http://m.blog.uliejh.cn/snews/653783.htm
- http://m.blog.uliejh.cn/snews/7771.htm
- http://m.blog.uliejh.cn/snews/83550.htm
- http://m.blog.uliejh.cn/snews/1759964.htm
- http://m.blog.uliejh.cn/snews/88407.htm
- http://m.blog.uliejh.cn/snews/3714242.htm
- http://m.blog.uliejh.cn/snews/9458.htm
- http://m.blog.uliejh.cn/snews/063610.htm
- http://m.blog.uliejh.cn/snews/5371471.htm
- http://m.blog.uliejh.cn/snews/108758.htm
- http://m.blog.uliejh.cn/snews/0643782.htm
- http://m.blog.uliejh.cn/snews/38728.htm
- http://m.blog.uliejh.cn/snews/88156.htm
- http://m.blog.uliejh.cn/snews/5813.htm
- http://m.blog.uliejh.cn/snews/6313.htm
- http://m.blog.uliejh.cn/snews/05215.htm
- http://m.blog.uliejh.cn/snews/6170.htm
- http://m.blog.uliejh.cn/snews/3874.htm
- http://m.blog.uliejh.cn/snews/91716.htm
- http://m.blog.uliejh.cn/snews/5422942.htm
- http://m.blog.uliejh.cn/snews/6612.htm
- http://m.blog.uliejh.cn/snews/8410.htm
- http://m.blog.uliejh.cn/snews/64802.htm
- http://m.blog.uliejh.cn/snews/1568275.htm
- http://m.blog.uliejh.cn/snews/21864.htm
- http://m.blog.uliejh.cn/snews/318437.htm
- http://m.blog.uliejh.cn/snews/7473.htm
- http://m.blog.uliejh.cn/snews/76061.htm
- http://m.blog.uliejh.cn/snews/25470.htm
- http://m.blog.uliejh.cn/snews/0172602.htm
- http://m.blog.uliejh.cn/snews/7468.htm
- http://m.blog.uliejh.cn/snews/71872.htm
- http://m.blog.uliejh.cn/snews/0519.htm
- http://m.blog.uliejh.cn/snews/6396.htm
- http://m.blog.uliejh.cn/snews/33797.htm
- http://m.blog.uliejh.cn/snews/5814685.htm
- http://m.blog.uliejh.cn/snews/1354263.htm
- http://m.blog.uliejh.cn/snews/1526120.htm
- http://m.blog.uliejh.cn/snews/29888.htm
- http://m.blog.uliejh.cn/snews/6613195.htm
- http://m.blog.uliejh.cn/snews/18647.htm
- http://m.blog.uliejh.cn/snews/71331.htm
- http://m.blog.uliejh.cn/snews/757339.htm
- http://m.blog.uliejh.cn/snews/274178.htm
- http://m.blog.uliejh.cn/snews/96725.htm
- http://m.blog.uliejh.cn/snews/3342406.htm
- http://m.blog.uliejh.cn/snews/00473.htm
- http://m.blog.uliejh.cn/snews/4394.htm
- http://m.blog.uliejh.cn/snews/9819879.htm
- http://m.blog.uliejh.cn/snews/8176.htm
- http://m.blog.uliejh.cn/snews/714361.htm
- http://m.blog.uliejh.cn/snews/6682088.htm
- http://m.blog.uliejh.cn/snews/235539.htm
- http://m.blog.uliejh.cn/snews/6207.htm
- http://m.blog.uliejh.cn/snews/20007.htm
- http://m.blog.uliejh.cn/snews/45079.htm
- http://m.blog.uliejh.cn/snews/577562.htm
- http://m.blog.uliejh.cn/snews/5383079.htm
- http://m.blog.uliejh.cn/snews/0015926.htm
- http://m.blog.uliejh.cn/snews/89940.htm
- http://m.blog.uliejh.cn/snews/243633.htm
- http://m.blog.uliejh.cn/snews/7629472.htm
- http://m.blog.uliejh.cn/snews/0972.htm
- http://m.blog.uliejh.cn/snews/91962.htm

## 项目结构

```
weblink-archive-navigator/
├── manage.py                         # Django 项目入口脚本，用于开发和运维命令
├── requirements.txt                  # Python 依赖清单，包含 Django、Celery、psycopg2 等
├── docker-compose.yml                # 容器编排文件，用于一键启动 PostgreSQL、Redis、Nginx 等服务
├── .env.example                      # 环境变量模板，包含数据库连接串、Redis URL、密钥配置
├── src/                              # 核心源代码目录
│   ├── core/                         # 项目全局配置与基础抽象层
│   │   ├── settings/                 # 分环境配置文件夹（base, dev, prod, test）
│   │   ├── celery.py                 # Celery 应用实例与任务调度配置
│   │   └── urls.py                   # 主路由分发，挂载 api 和 admin 路由
│   ├── links/                        # 链接管理核心应用
│   │   ├── models/                   # 数据模型定义，包含 Link, Tag, LinkStatus, LinkMetadata
│   │   ├── services/                 # 业务逻辑层，包含导入器、状态检测器、元数据提取器
│   │   ├── tasks/                    # Celery 异步任务，包含 check_links, fetch_metadata, export_report
│   │   ├── api/                      # REST API 视图，基于 Django REST Framework 实现
│   │   └── management/               # 自定义管理命令，包含 load_links, check_all, export_json
│   ├── users/                        # 用户与权限管理应用
│   │   ├── models/                   # 用户扩展模型，包含 API 令牌和 IP 白名单
│   │   └── middleware/               # 只读模式中间件与令牌认证中间件
│   ├── frontend/                     # 前端静态资源与模板（基于 Bootstrap 5 和 Vanilla JS）
│   │   ├── templates/                # Django 模板文件，包含列表页、详情页、仪表盘
│   │   └── static/                   # 编译后的 CSS、JS、字体文件
│   └── utils/                        # 通用工具函数库
│       ├── validators.py             # URL 格式校验、去重逻辑
│       ├── cache.py                  # Redis 缓存封装，支持键值过期和批量失效
│       └── logger.py                 # 结构化日志配置，按天滚动
├── tests/                            # 单元测试与集成测试
│   ├── test_models.py                # 模型层测试覆盖
│   ├── test_services.py              # 服务层测试用例，含 mock 外部请求
│   └── test_api.py                   # API 端点测试，覆盖增删改查与筛选
├── scripts/                          # 运维脚本与定时任务
│   ├── backup_db.sh                  # PostgreSQL 备份脚本
│   └── rotate_logs.sh                # 日志轮转脚本
└── docs/                             # 文档源文件（Markdown 格式）
    ├── user-guide/                   # 用户手册分章节
    ├── ops-guide/                    # 运维手册分章节
    └── api-reference/                # API 端点详细说明
```

## 贡献指南

提交 Issue 报告缺陷或功能请求：请在 GitHub Issues 页面新建 Issue，使用提供的模板填写系统版本、运行环境、复现步骤和期望行为。缺陷报告需附带最小复现代码或配置示例。

创建 Pull Request 修改代码或文档：Fork 本仓库到个人账户，在本地新建功能分支（命名格式为 feature/简述或 fix/简述），完成修改后推送并提交 PR。PR 描述需说明修改动机、实现方案和测试情况。

运行测试套件确保质量：在提交 PR 前，请在本地执行 `pytest tests/` 确保全部用例通过，同时使用 `flake8` 和 `black` 检查代码风格。新增功能需同步补充对应的测试用例。

更新文档记录变更：如果修改涉及用户可见的功能变化（如新 API 参数、配置项变更），请在 docs/ 目录下同步更新对应的手册章节，并在 PR 中说明文档变更位置。

遵守行为准则：所有交流与贡献须遵循项目行为准则，保持专业、友善、建设性的沟通氛围，禁止任何形式的歧视或人身攻击。

## 常见问题

问：导入大量 URL 时页面响应很慢或超时怎么办？

答：导入操作默认同步执行，适合少量链接（50 条以内）。对于超过 100 条的批量导入，请使用管理命令 `python manage.py load_links --file` 异步执行，该命令会将任务分发给 Celery worker，不阻塞 Web 请求。如果必须通过 API 导入，请将 `async=true` 参数加入请求体，系统会返回任务 ID 供后续查询进度。

问：状态监控检测到链接失效，但浏览器中可以正常访问，是什么原因？

答：状态监控默认使用 HEAD 请求检测，部分服务器对 HEAD 请求返回 405 或 403，但支持 GET 请求。请在监控配置中将检测方法改为 GET，或增加自定义请求头（如 User-Agent）模拟真实浏览器访问。此外，某些站点有反爬机制，需在配置中设置合理的请求间隔（建议不低于 5 秒）并启用 cookie 持久化。

问：如何将当前系统迁移到另一台服务器？

答：迁移分为数据迁移和环境迁移两部分。数据迁移需使用 `pg_dump` 导出 PostgreSQL 数据库，并备份 Redis 持久化文件（dump.rdb）。环境迁移建议使用 Docker 镜像锁定所有依赖版本，在目标服务器上导入镜像并挂载数据卷。具体步骤请参考运维手册中的「备份与恢复」章节，其中包含完整的命令示例和校验清单。

## 许可证

MIT

> 外链数量: 250 | 生成时间: 2026-08-24 23:40:21
