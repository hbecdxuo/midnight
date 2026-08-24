# WebFront Resource Aggregator

WebFront Resource Aggregator 是一个面向前端开发者和技术内容研究人员的结构化外链资源汇总系统。该项目旨在解决分散于各类移动端资讯站点的技术文章、行业动态和工程实践内容难以系统化检索与长期追踪的问题。通过将散落的深度技术报道、案例分析、工具评测和架构演进记录按统一索引框架进行归集，本项目为技术决策者、一线开发者和技术运营人员提供可快速定位、可交叉参考的高质量外链集合。WebFront Resource Aggregator 定位于中大型研发团队的技术知识中台辅助组件，也可作为个人开发者构建系统化阅读清单的基础数据源。

## 功能概览

- 分层索引体系：资源按移动端技术、前端工程化、性能优化、安全实践、架构设计、运维监控、语言特性、工具生态等维度组织，每个外链均附带自动提取的元信息标签。
- 批量导入与解析：支持从标准输入、文件批量导入原始链接列表，系统自动完成可访问性检测、标题提取和内容摘要生成。
- 多级筛选与检索：提供基于关键词、发布时间区间、来源域名、内容类型（教程/案例/规范/工具）的多条件组合过滤，检索结果支持按相关度或时间排序。
- 资源状态监控：定期对已收录外链进行存活检测和内容变更比对，当目标页面返回 4xx/5xx 状态码或关键内容结构发生变化时生成告警通知。
- 自定义分类与标签管理：允许用户创建私有分类树和标签体系，支持批量打标、标签合并与冲突检测，分类数据可导出为 JSON 或 YAML 格式。
- 阅读列表与收藏夹：每个用户可维护独立的待读列表和收藏夹，支持添加个人笔记、标注重点段落和设置阅读优先级。
- API 接口与 Webhook：提供 RESTful API 用于第三方工具集成，支持通过 Webhook 将新增资源自动推送到企业微信、钉钉或 Slack 频道。
- 数据统计看板：内置可视化仪表盘，展示资源总量、增长趋势、来源分布、状态健康度、最热标签排行等关键指标。

## 应用场景

- 技术团队周报与月刊素材采集：团队技术负责人或运营人员可通过本系统定期检索近期收录的移动端技术文章和行业案例，快速筛选出适合内部分享或对外输出的高质量内容，大幅降低人工翻阅数十个资讯源的时间成本。
- 架构选型与方案评审参考库：在进行技术选型或架构评审前，架构师可以按标签和分类快速定位同类场景下的实际落地案例、性能对比数据和踩坑记录，为评审决策提供客观的第三方依据。
- 开发者个人知识体系构建：前端或全栈开发者可将本系统作为日常阅读入口，通过收藏、标注和自定义分类逐步积累属于自己的技术知识库，并结合 API 将收藏内容同步至个人笔记工具。
- 技术内容合规与安全审计：安全团队可利用资源状态监控功能，持续追踪依赖库和第三方服务相关的外链变更情况，及时发现被篡改或失效的引用链接，保障内部文档和产品中的外链合规性。

## 快速开始

以下步骤帮助您在本地环境快速启动 WebFront Resource Aggregator 服务。

```bash
# 克隆代码仓库
git clone https://github.com/webfront-resource/aggregator.git
cd aggregator

# 安装依赖（使用 npm）
npm install

# 配置环境变量（复制示例配置并编辑）
cp .env.example .env
# 使用文本编辑器修改 .env 中的数据库连接、端口等参数

# 初始化数据库结构
npm run db:migrate

# 导入示例资源链接（用户提供的首批数据）
npm run import:links -- --source ./data/initial_links.txt

# 启动开发服务器
npm run dev
```

访问 http://localhost:3000 即可进入资源检索界面。生产环境部署请参考 `docs/deployment.md`。

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|---------|---------|------|
| Node.js | >= 18.0.0 | 运行时环境，推荐使用 LTS 版本 |
| PostgreSQL | >= 14.0 | 主数据库，用于存储资源元信息、用户数据和分类体系 |
| Redis | >= 6.2 | 缓存与任务队列后端，用于资源状态监控的定时任务调度 |
| npm 或 yarn | >= 8.0 / >= 1.22 | 包管理器，用于安装项目依赖 |
| Git | >= 2.30 | 版本控制工具，用于克隆仓库和管理补丁 |
| PM2（生产环境） | >= 5.0 | 进程守护工具，用于生产环境服务持久化运行 |
| Nginx（可选） | >= 1.20 | 反向代理服务器，用于负载均衡和静态资源缓存 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|------|------|-----------|
| 入门指南 | `docs/getting-started.md` | 如何快速完成首次启动？如何导入第一批资源链接？如何理解系统界面布局？ |
| 数据模型 | `docs/data-model.md` | 资源、标签、分类、用户、收藏、阅读记录之间的关联关系是怎样的？数据库 ER 图如何解读？ |
| API 参考 | `docs/api-reference.md` | 提供哪些 RESTful 端点？如何认证？请求与响应格式分别是什么？分页和过滤参数如何使用？ |
| 运维手册 | `docs/operations.md` | 如何配置资源状态监控的轮询间隔？如何备份和恢复数据库？日志文件存放在哪里？如何升级版本？ |

## 资源列表

- http://m.wap.uliejh.cn/bnews/0361.htm
- http://m.wap.uliejh.cn/bnews/261681.htm
- http://m.wap.uliejh.cn/bnews/37920.htm
- http://m.wap.uliejh.cn/bnews/393074.htm
- http://m.wap.uliejh.cn/bnews/9154991.htm
- http://m.wap.uliejh.cn/bnews/3315282.htm
- http://m.wap.uliejh.cn/bnews/915006.htm
- http://m.wap.uliejh.cn/bnews/54867.htm
- http://m.wap.uliejh.cn/bnews/274476.htm
- http://m.wap.uliejh.cn/bnews/8833.htm
- http://m.wap.uliejh.cn/bnews/92805.htm
- http://m.wap.uliejh.cn/bnews/0533.htm
- http://m.wap.uliejh.cn/bnews/850508.htm
- http://m.wap.uliejh.cn/bnews/485518.htm
- http://m.wap.uliejh.cn/bnews/8201.htm
- http://m.wap.uliejh.cn/bnews/8671.htm
- http://m.wap.uliejh.cn/bnews/0783174.htm
- http://m.wap.uliejh.cn/bnews/1299.htm
- http://m.wap.uliejh.cn/bnews/53407.htm
- http://m.wap.uliejh.cn/bnews/1151620.htm
- http://m.wap.uliejh.cn/bnews/6094584.htm
- http://m.wap.uliejh.cn/bnews/662750.htm
- http://m.wap.uliejh.cn/bnews/804372.htm
- http://m.wap.uliejh.cn/bnews/004587.htm
- http://m.wap.uliejh.cn/bnews/39506.htm
- http://m.wap.uliejh.cn/bnews/52895.htm
- http://m.wap.uliejh.cn/bnews/5915811.htm
- http://m.wap.uliejh.cn/bnews/5758.htm
- http://m.wap.uliejh.cn/bnews/2383.htm
- http://m.wap.uliejh.cn/bnews/8809388.htm
- http://m.wap.uliejh.cn/bnews/47118.htm
- http://m.wap.uliejh.cn/bnews/85099.htm
- http://m.wap.uliejh.cn/bnews/7427.htm
- http://m.wap.uliejh.cn/bnews/4889.htm
- http://m.wap.uliejh.cn/bnews/667472.htm
- http://m.wap.uliejh.cn/bnews/989990.htm
- http://m.wap.uliejh.cn/bnews/1215988.htm
- http://m.wap.uliejh.cn/bnews/492166.htm
- http://m.wap.uliejh.cn/bnews/7436184.htm
- http://m.wap.uliejh.cn/bnews/3990898.htm
- http://m.wap.uliejh.cn/bnews/0641735.htm
- http://m.wap.uliejh.cn/bnews/43799.htm
- http://m.wap.uliejh.cn/bnews/5606.htm
- http://m.wap.uliejh.cn/bnews/22037.htm
- http://m.wap.uliejh.cn/bnews/5114.htm
- http://m.wap.uliejh.cn/bnews/1576.htm
- http://m.wap.uliejh.cn/bnews/32022.htm
- http://m.wap.uliejh.cn/bnews/1778.htm
- http://m.wap.uliejh.cn/bnews/88878.htm
- http://m.wap.uliejh.cn/bnews/15152.htm
- http://m.wap.uliejh.cn/bnews/2594.htm
- http://m.wap.uliejh.cn/bnews/1520907.htm
- http://m.wap.uliejh.cn/bnews/198938.htm
- http://m.wap.uliejh.cn/bnews/7679.htm
- http://m.wap.uliejh.cn/bnews/9839.htm
- http://m.wap.uliejh.cn/bnews/9088866.htm
- http://m.wap.uliejh.cn/bnews/104023.htm
- http://m.wap.uliejh.cn/bnews/4535798.htm
- http://m.wap.uliejh.cn/bnews/3325.htm
- http://m.wap.uliejh.cn/bnews/105694.htm
- http://m.wap.uliejh.cn/bnews/213508.htm
- http://m.wap.uliejh.cn/bnews/910738.htm
- http://m.wap.uliejh.cn/bnews/6253.htm
- http://m.wap.uliejh.cn/bnews/1175400.htm
- http://m.wap.uliejh.cn/bnews/6551.htm
- http://m.wap.uliejh.cn/bnews/950497.htm
- http://m.wap.uliejh.cn/bnews/79232.htm
- http://m.wap.uliejh.cn/bnews/5852.htm
- http://m.wap.uliejh.cn/bnews/8549.htm
- http://m.wap.uliejh.cn/bnews/4677.htm
- http://m.wap.uliejh.cn/bnews/08561.htm
- http://m.wap.uliejh.cn/bnews/5702.htm
- http://m.wap.uliejh.cn/bnews/75637.htm
- http://m.wap.uliejh.cn/bnews/0930.htm
- http://m.wap.uliejh.cn/bnews/5235.htm
- http://m.wap.uliejh.cn/bnews/982596.htm
- http://m.wap.uliejh.cn/bnews/1366118.htm
- http://m.wap.uliejh.cn/bnews/22440.htm
- http://m.wap.uliejh.cn/bnews/655059.htm
- http://m.wap.uliejh.cn/bnews/03134.htm
- http://m.wap.uliejh.cn/bnews/0535203.htm
- http://m.wap.uliejh.cn/bnews/6420.htm
- http://m.wap.uliejh.cn/bnews/3813.htm
- http://m.wap.uliejh.cn/bnews/548694.htm
- http://m.wap.uliejh.cn/bnews/453721.htm
- http://m.wap.uliejh.cn/bnews/42778.htm
- http://m.wap.uliejh.cn/bnews/256394.htm
- http://m.wap.uliejh.cn/bnews/92814.htm
- http://m.wap.uliejh.cn/bnews/2603850.htm
- http://m.wap.uliejh.cn/bnews/6978238.htm
- http://m.wap.uliejh.cn/bnews/5826.htm
- http://m.wap.uliejh.cn/bnews/3492428.htm
- http://m.wap.uliejh.cn/bnews/5033813.htm
- http://m.wap.uliejh.cn/bnews/481022.htm
- http://m.wap.uliejh.cn/bnews/878252.htm
- http://m.wap.uliejh.cn/bnews/84429.htm
- http://m.wap.uliejh.cn/bnews/720727.htm
- http://m.wap.uliejh.cn/bnews/756949.htm
- http://m.wap.uliejh.cn/bnews/4519.htm
- http://m.wap.uliejh.cn/bnews/992659.htm
- http://m.wap.uliejh.cn/bnews/8233.htm
- http://m.wap.uliejh.cn/bnews/1078353.htm
- http://m.wap.uliejh.cn/bnews/89213.htm
- http://m.wap.uliejh.cn/bnews/03295.htm
- http://m.wap.uliejh.cn/bnews/5794.htm
- http://m.wap.uliejh.cn/bnews/5876.htm
- http://m.wap.uliejh.cn/bnews/88221.htm
- http://m.wap.uliejh.cn/bnews/15394.htm
- http://m.wap.uliejh.cn/bnews/2553.htm
- http://m.wap.uliejh.cn/bnews/287735.htm
- http://m.wap.uliejh.cn/bnews/12107.htm
- http://m.wap.uliejh.cn/bnews/9397.htm
- http://m.wap.uliejh.cn/bnews/471002.htm
- http://m.wap.uliejh.cn/bnews/3181517.htm
- http://m.wap.uliejh.cn/bnews/6026.htm
- http://m.wap.uliejh.cn/bnews/4723207.htm
- http://m.wap.uliejh.cn/bnews/8252996.htm
- http://m.wap.uliejh.cn/bnews/31581.htm
- http://m.wap.uliejh.cn/bnews/6084463.htm
- http://m.wap.uliejh.cn/bnews/664025.htm
- http://m.wap.uliejh.cn/bnews/5804876.htm
- http://m.wap.uliejh.cn/bnews/8848.htm
- http://m.wap.uliejh.cn/bnews/815688.htm
- http://m.wap.uliejh.cn/bnews/59405.htm
- http://m.wap.uliejh.cn/bnews/384709.htm
- http://m.wap.uliejh.cn/bnews/23495.htm
- http://m.wap.uliejh.cn/bnews/501392.htm
- http://m.wap.uliejh.cn/bnews/730237.htm
- http://m.wap.uliejh.cn/bnews/9047.htm
- http://m.wap.uliejh.cn/bnews/20102.htm
- http://m.wap.uliejh.cn/bnews/1552677.htm
- http://m.wap.uliejh.cn/bnews/76757.htm
- http://m.wap.uliejh.cn/bnews/64028.htm
- http://m.wap.uliejh.cn/bnews/3482.htm
- http://m.wap.uliejh.cn/bnews/2222365.htm
- http://m.wap.uliejh.cn/bnews/436775.htm
- http://m.wap.uliejh.cn/bnews/379336.htm
- http://m.wap.uliejh.cn/bnews/937856.htm
- http://m.wap.uliejh.cn/bnews/4748.htm
- http://m.wap.uliejh.cn/bnews/8773988.htm
- http://m.wap.uliejh.cn/bnews/1793.htm
- http://m.wap.uliejh.cn/bnews/2159648.htm
- http://m.wap.uliejh.cn/bnews/94538.htm
- http://m.wap.uliejh.cn/bnews/8878910.htm
- http://m.wap.uliejh.cn/bnews/7685.htm
- http://m.wap.uliejh.cn/bnews/1811.htm
- http://m.wap.uliejh.cn/bnews/8914028.htm
- http://m.wap.uliejh.cn/bnews/0349624.htm
- http://m.wap.uliejh.cn/bnews/3715940.htm
- http://m.wap.uliejh.cn/bnews/038182.htm
- http://m.wap.uliejh.cn/bnews/804051.htm
- http://m.wap.uliejh.cn/bnews/5308.htm
- http://m.wap.uliejh.cn/bnews/732956.htm
- http://m.wap.uliejh.cn/bnews/502144.htm
- http://m.wap.uliejh.cn/bnews/981705.htm
- http://m.wap.uliejh.cn/bnews/4864705.htm
- http://m.wap.uliejh.cn/bnews/92411.htm
- http://m.wap.uliejh.cn/bnews/63196.htm
- http://m.wap.uliejh.cn/bnews/9823.htm
- http://m.wap.uliejh.cn/bnews/015249.htm
- http://m.wap.uliejh.cn/bnews/1106.htm
- http://m.wap.uliejh.cn/bnews/36376.htm
- http://m.wap.uliejh.cn/bnews/9727.htm
- http://m.wap.uliejh.cn/bnews/796160.htm
- http://m.wap.uliejh.cn/bnews/3394.htm
- http://m.wap.uliejh.cn/bnews/284477.htm
- http://m.wap.uliejh.cn/bnews/281292.htm
- http://m.wap.uliejh.cn/bnews/0777896.htm
- http://m.wap.uliejh.cn/bnews/3528187.htm
- http://m.wap.uliejh.cn/bnews/0718.htm
- http://m.wap.uliejh.cn/bnews/49988.htm
- http://m.wap.uliejh.cn/bnews/90830.htm
- http://m.wap.uliejh.cn/bnews/9805194.htm
- http://m.wap.uliejh.cn/bnews/36740.htm
- http://m.wap.uliejh.cn/bnews/2948116.htm
- http://m.wap.uliejh.cn/bnews/30841.htm
- http://m.wap.uliejh.cn/bnews/231360.htm
- http://m.wap.uliejh.cn/bnews/938748.htm
- http://m.wap.uliejh.cn/bnews/56643.htm
- http://m.wap.uliejh.cn/bnews/1843718.htm
- http://m.wap.uliejh.cn/bnews/2430716.htm
- http://m.wap.uliejh.cn/bnews/0889205.htm
- http://m.wap.uliejh.cn/bnews/781077.htm
- http://m.wap.uliejh.cn/bnews/64531.htm
- http://m.wap.uliejh.cn/bnews/55546.htm
- http://m.wap.uliejh.cn/bnews/7254.htm
- http://m.wap.uliejh.cn/bnews/45621.htm
- http://m.wap.uliejh.cn/bnews/3462.htm
- http://m.wap.uliejh.cn/bnews/0491238.htm
- http://m.wap.uliejh.cn/bnews/9209787.htm
- http://m.wap.uliejh.cn/bnews/60037.htm
- http://m.wap.uliejh.cn/bnews/8147.htm
- http://m.wap.uliejh.cn/bnews/1917945.htm
- http://m.wap.uliejh.cn/bnews/9308.htm
- http://m.wap.uliejh.cn/bnews/62781.htm
- http://m.wap.uliejh.cn/bnews/29367.htm
- http://m.wap.uliejh.cn/bnews/1523321.htm
- http://m.wap.uliejh.cn/bnews/2227.htm
- http://m.wap.uliejh.cn/bnews/9639283.htm
- http://m.wap.uliejh.cn/bnews/1339356.htm
- http://m.wap.uliejh.cn/bnews/332002.htm
- http://m.wap.uliejh.cn/bnews/3766193.htm
- http://m.wap.uliejh.cn/bnews/8830435.htm
- http://m.wap.uliejh.cn/bnews/03248.htm
- http://m.wap.uliejh.cn/bnews/8054.htm
- http://m.wap.uliejh.cn/bnews/33853.htm
- http://m.wap.uliejh.cn/bnews/18379.htm
- http://m.wap.uliejh.cn/bnews/0150085.htm
- http://m.wap.uliejh.cn/bnews/75629.htm
- http://m.wap.uliejh.cn/bnews/3395.htm
- http://m.wap.uliejh.cn/bnews/772983.htm
- http://m.wap.uliejh.cn/bnews/9791.htm
- http://m.wap.uliejh.cn/bnews/9830.htm
- http://m.wap.uliejh.cn/bnews/6922.htm
- http://m.wap.uliejh.cn/bnews/5738913.htm
- http://m.wap.uliejh.cn/bnews/765379.htm
- http://m.wap.uliejh.cn/bnews/7135.htm
- http://m.wap.uliejh.cn/bnews/23365.htm
- http://m.wap.uliejh.cn/bnews/7022750.htm
- http://m.wap.uliejh.cn/bnews/2280875.htm
- http://m.wap.uliejh.cn/bnews/0591007.htm
- http://m.wap.uliejh.cn/bnews/40796.htm
- http://m.wap.uliejh.cn/bnews/5000.htm
- http://m.wap.uliejh.cn/bnews/95819.htm
- http://m.wap.uliejh.cn/bnews/81339.htm
- http://m.wap.uliejh.cn/bnews/2293484.htm
- http://m.wap.uliejh.cn/bnews/0552045.htm
- http://m.wap.uliejh.cn/bnews/549316.htm
- http://m.wap.uliejh.cn/bnews/12515.htm
- http://m.wap.uliejh.cn/bnews/38430.htm
- http://m.wap.uliejh.cn/bnews/8693102.htm
- http://m.wap.uliejh.cn/bnews/264560.htm
- http://m.wap.uliejh.cn/bnews/594192.htm
- http://m.wap.uliejh.cn/bnews/3326589.htm
- http://m.wap.uliejh.cn/bnews/1155.htm
- http://m.wap.uliejh.cn/bnews/1341.htm
- http://m.wap.uliejh.cn/bnews/2728.htm
- http://m.wap.uliejh.cn/bnews/54719.htm
- http://m.wap.uliejh.cn/bnews/86618.htm
- http://m.wap.uliejh.cn/bnews/0592.htm
- http://m.wap.uliejh.cn/bnews/782312.htm
- http://m.wap.uliejh.cn/bnews/04537.htm
- http://m.wap.uliejh.cn/bnews/133702.htm
- http://m.wap.uliejh.cn/bnews/520357.htm
- http://m.wap.uliejh.cn/bnews/388439.htm
- http://m.wap.uliejh.cn/bnews/0485130.htm
- http://m.wap.uliejh.cn/bnews/7400846.htm
- http://m.wap.uliejh.cn/bnews/7860145.htm
- http://m.wap.uliejh.cn/bnews/0683.htm
- http://m.wap.uliejh.cn/bnews/1511.htm

## 项目结构

```
aggregator/
├── apps/                                # 应用入口与路由层
│   ├── api/                             # RESTful API 端点实现
│   │   ├── v1/                          # API 版本 v1 路由
│   │   │   ├── resources.js             # 资源 CRUD 端点
│   │   │   ├── tags.js                  # 标签管理端点
│   │   │   └── stats.js                 # 统计看板数据端点
│   │   └── webhooks/                    # Webhook 接收与分发处理
│   └── web/                             # Web 界面路由（SSR 渲染）
│       ├── dashboard/                   # 仪表盘页面
│       ├── search/                      # 检索与筛选页面
│       └── collection/                  # 收藏与阅读列表页面
├── core/                                # 核心业务逻辑层
│   ├── crawler/                         # 资源抓取与解析引擎
│   │   ├── fetcher.js                   # HTTP 请求与重试策略
│   │   ├── parser.js                    # HTML 元信息提取
│   │   └── scheduler.js                 # 定时任务调度
│   ├── indexer/                         # 索引构建与查询引擎
│   │   ├── tokenizer.js                 # 中文分词与关键词提取
│   │   └── ranker.js                    # 相关度排序算法
│   └── monitor/                         # 资源状态监控模块
│       ├── checker.js                   # 存活检测与状态码判定
│       └── notifier.js                  # 告警通知渠道适配
├── data/                                # 数据存储与迁移层
│   ├── migrations/                      # 数据库迁移脚本（按时间戳命名）
│   ├── seeders/                         # 初始数据填充脚本
│   └── repositories/                    # 数据访问对象（DAO）
├── services/                            # 外部服务集成层
│   ├── cache/                           # Redis 缓存服务封装
│   ├── queue/                           # 任务队列（Bull）配置
│   └── webhook/                         # 企业微信/钉钉/Slack 适配器
├── shared/                              # 跨层共享工具与常量
│   ├── constants/                       # 状态码、分类枚举、配置常量
│   ├── utils/                           # 通用工具函数（日志、验证、加密）
│   └── validators/                      # 输入校验规则（Joi 模式）
├── tests/                               # 单元测试与集成测试
│   ├── unit/                            # 各模块单元测试
│   └── integration/                     # API 端到端测试
├── docs/                                # 完整项目文档（见文档导航）
├── scripts/                             # 运维与工具脚本
│   ├── import-links.js                  # 批量导入链接脚本
│   └── health-check.js                  # 系统健康检查脚本
├── .env.example                         # 环境变量配置模板
├── package.json                         # 项目依赖与脚本定义
├── docker-compose.yml                   # 本地开发容器编排
└── README.md                            # 本项目说明文件
```

## 贡献指南

1. 复刻主仓库并创建功能分支：从 GitHub 复刻 WebFront Resource Aggregator 主仓库到个人账号，然后基于 `main` 分支创建一个描述性的功能分支（例如 `feat/add-rss-import` 或 `fix/memory-leak-crawler`）。
2. 遵循代码规范与测试要求：所有 JavaScript/TypeScript 代码须通过 ESLint 和 Prettier 格式化，新增功能需附带对应的单元测试或集成测试，确保测试覆盖率达到 80% 以上。
3. 提交拉取请求并填写模板：向主仓库的 `main` 分支发起拉取请求，完整填写 PR 模板中的变更描述、测试结果和影响范围，关联相关 Issue 编号。
4. 参与代码评审并完成修改：项目维护者将在 48 小时内进行评审，如有修改意见请及时响应并推送修正提交，待所有检查通过后由维护者合入。
5. 文档同步更新：任何对外接口、数据模型或配置项的变更，须同步更新 `docs/` 目录下的对应文档，并在 PR 中注明文档变更情况。

## 常见问题

**Q：导入大量链接后，系统响应变慢甚至超时，应如何优化？**

A：建议优先检查 Redis 缓存是否正常运行，并确认任务队列（Bull）的工作进程数量是否与 CPU 核数匹配。对于首次导入，可分批处理（例如每批 500 条），使用 `scripts/import-links.js --batch-size 500` 参数执行。另外，检查 PostgreSQL 的 `work_mem` 和 `shared_buffers` 配置是否满足数据量需求，通常建议 `shared_buffers` 设置为物理内存的 25%。

**Q：资源状态监控显示大量链接超时或返回 403，是否意味着这些资源已失效？**

A：不一定。部分目标站点可能启用了反爬机制或请求频率限制。建议检查 `core/monitor/checker.js` 中的请求头配置，可尝试增加 `User-Agent` 轮换和请求间隔（默认间隔为 5 秒，可调至 10-15 秒）。若持续返回 403，请在系统配置中开启代理模式（设置 `HTTP_PROXY` 环境变量）。对于返回 429 的站点，系统会自动加入冷却列表，冷却时间默认 30 分钟。

**Q：能否将本系统部署为无数据库的纯静态站点？**

A：当前版本依赖 PostgreSQL 和 Redis 实现动态检索、分类和监控功能，不支持纯静态模式。若仅需展示固定链接列表，可考虑使用 `npm run export:static` 命令导出当前数据为 HTML 文件，该命令会生成一份静态快照页面，但该页面不包含实时检索和更新能力，适合临时分享或归档用途。

## 许可证

MIT

> 外链数量: 250 | 生成时间: 2026-08-24 23:40:21
