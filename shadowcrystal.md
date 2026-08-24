# LinkSphere 技术外链聚合引擎

LinkSphere 是一个面向技术研究者与内容创作者的轻量级外链汇总与导航系统。该项目定位于将分散于互联网各处的优质技术博文、教程、工具文档与行业动态进行集中式收录与分类展示，解决技术从业者在信息检索过程中面临的多源跳转、重复筛选与内容发现效率低下等问题。LinkSphere 不生产内容，而是通过结构化的外链管理机制，帮助用户快速定位特定主题下的高质量阅读材料，适用于个人知识库构建、团队技术沉淀以及公开内容策展等场景。

## 功能概览

**批量外链导入与去重**：支持从文本文件、表格或直接粘贴的 URL 列表中批量导入外链数据，系统自动检测并剔除重复条目，确保资源池的唯一性。

**智能分类与标签体系**：每一篇外链可赋予多个层级标签（如后端架构、前端工程化、运维监控、AI 模型等），支持基于标签组合的快速筛选与聚合视图。

**全文检索与元数据过滤**：基于外链标题、摘要、来源域名及标签进行关键词检索，同时支持按发布日期、热度评分、阅读时长等元数据维度进行排序与过滤。

**资源状态监控与死链检测**：内置定期健康检查模块，自动探测已收录 URL 的可访问性，对返回 4xx 或 5xx 状态码的链接进行标记并生成告警报告。

**自定义收藏夹与阅读清单**：用户可注册账号并创建多个收藏夹，将感兴趣的外链分组保存，支持生成公开或私有的阅读清单，便于团队内部共享。

**RSS 订阅源生成**：为每个分类或标签自动生成 RSS 订阅地址，用户可通过标准 RSS 阅读器接收该分类下的新增外链推送。

**数据统计与趋势看板**：提供管理员仪表盘，展示外链总量、每日新增趋势、热门分类排行榜以及用户点击热度分布，辅助运营决策。

**开放 API 接口**：提供 RESTful API，允许第三方开发者批量获取外链数据，支持 JSON 与 RSS 两种输出格式，便于集成至其他知识管理工具。

## 应用场景

技术团队内部知识库构建：团队技术负责人可将日常阅读的优秀博文、官方文档、故障排查案例通过 LinkSphere 统一收录，并按照微服务、数据库、前端框架等维度分类，新成员入职时可快速浏览团队推荐的必读材料，缩短上手周期。

个人开发者每日阅读聚合：独立开发者或工程师可将关注的数十个技术博客、个人站点、资讯周刊的外链集中导入 LinkSphere，每日通过检索标签或查看未读清单的方式高效筛选当日值得阅读的文章，避免在社交时间线上碎片化消耗注意力。

公开技术资源导航站运营：社区组织或技术媒体可基于 LinkSphere 搭建公开的技术资源导航门户，按主题（如 Python 生态、云原生、机器学习）陈列精选外链，并为每一条链接附上简注与推荐指数，为更广泛的开发者群体提供经过人工筛选的优质内容入口。

## 快速开始

以下命令演示了如何在本地环境中克隆项目仓库、安装依赖并启动开发服务器。

```bash
# 克隆仓库至本地
git clone https://github.com/your-org/linksphere.git

# 进入项目根目录
cd linksphere

# 安装后端与前端依赖
npm run setup:all

# 配置环境变量（数据库连接、JWT 密钥等）
cp .env.example .env

# 执行数据库迁移与初始数据填充
npm run migrate
npm run seed

# 启动开发模式（同时运行后端 API 与前端开发服务器）
npm run dev
```

访问本地 `http://localhost:3000` 即可开始使用 LinkSphere 基础功能。生产环境部署请参考 `docs/deployment.md` 文档。

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|---|---|---|
| Node.js | 18.x 或 20.x LTS | 运行时环境，用于执行后端服务与前端构建工具 |
| PostgreSQL | 14.x 或 15.x | 主数据库，存储用户、外链条目、标签及关联关系 |
| Redis | 7.x | 缓存与会话存储，用于提升高频查询性能与分布式锁 |
| Elasticsearch | 8.x | 可选依赖，用于全文检索增强，如不安装则回退至 SQL 模糊查询 |
| Nginx | 1.24+ | 生产环境反向代理与静态资源服务，非开发环境必需 |
| PM2 | 5.x | 进程守护工具，用于生产环境管理 Node.js 服务实例 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|---|---|---|
| 用户手册 | `/docs/user-guide/` | 如何注册账号、导入外链、创建分类、使用检索与收藏功能 |
| 管理员指南 | `/docs/admin-guide/` | 如何执行健康检查、管理用户权限、调整系统配置与查看统计看板 |
| 开发者文档 | `/docs/developer/` | API 接口规范、数据库 ER 图、插件扩展机制与本地调试流程 |
| 部署运维 | `/docs/operations/` | 生产环境架构选型、容器化部署模板、监控告警与备份恢复策略 |

## 资源列表

- http://m.blog.uliejh.cn/snews/6410458.htm
- http://m.blog.uliejh.cn/snews/9011497.htm
- http://m.blog.uliejh.cn/snews/6877.htm
- http://m.blog.uliejh.cn/snews/3928585.htm
- http://m.blog.uliejh.cn/snews/4210.htm
- http://m.blog.uliejh.cn/snews/48524.htm
- http://m.blog.uliejh.cn/snews/51933.htm
- http://m.blog.uliejh.cn/snews/4337637.htm
- http://m.blog.uliejh.cn/snews/1917155.htm
- http://m.blog.uliejh.cn/snews/30722.htm
- http://m.blog.uliejh.cn/snews/1678370.htm
- http://m.blog.uliejh.cn/snews/19521.htm
- http://m.blog.uliejh.cn/snews/343396.htm
- http://m.blog.uliejh.cn/snews/100096.htm
- http://m.blog.uliejh.cn/snews/4020092.htm
- http://m.blog.uliejh.cn/snews/5106337.htm
- http://m.blog.uliejh.cn/snews/5356395.htm
- http://m.blog.uliejh.cn/snews/593801.htm
- http://m.blog.uliejh.cn/snews/8718.htm
- http://m.blog.uliejh.cn/snews/439445.htm
- http://m.blog.uliejh.cn/snews/0943557.htm
- http://m.blog.uliejh.cn/snews/0292.htm
- http://m.blog.uliejh.cn/snews/213149.htm
- http://m.blog.uliejh.cn/snews/039825.htm
- http://m.blog.uliejh.cn/snews/3556.htm
- http://m.blog.uliejh.cn/snews/72938.htm
- http://m.blog.uliejh.cn/snews/672391.htm
- http://m.blog.uliejh.cn/snews/799154.htm
- http://m.blog.uliejh.cn/snews/3916614.htm
- http://m.blog.uliejh.cn/snews/710782.htm
- http://m.blog.uliejh.cn/snews/9494690.htm
- http://m.blog.uliejh.cn/snews/7993748.htm
- http://m.blog.uliejh.cn/snews/08169.htm
- http://m.blog.uliejh.cn/snews/3592.htm
- http://m.blog.uliejh.cn/snews/5496.htm
- http://m.blog.uliejh.cn/snews/314382.htm
- http://m.blog.uliejh.cn/snews/2747.htm
- http://m.blog.uliejh.cn/snews/87209.htm
- http://m.blog.uliejh.cn/snews/7068158.htm
- http://m.blog.uliejh.cn/snews/386906.htm
- http://m.blog.uliejh.cn/snews/67185.htm
- http://m.blog.uliejh.cn/snews/8606.htm
- http://m.blog.uliejh.cn/snews/1498234.htm
- http://m.blog.uliejh.cn/snews/76046.htm
- http://m.blog.uliejh.cn/snews/64824.htm
- http://m.blog.uliejh.cn/snews/819888.htm
- http://m.blog.uliejh.cn/snews/6015.htm
- http://m.blog.uliejh.cn/snews/3367740.htm
- http://m.blog.uliejh.cn/snews/29775.htm
- http://m.blog.uliejh.cn/snews/1497.htm
- http://m.blog.uliejh.cn/snews/0866227.htm
- http://m.blog.uliejh.cn/snews/4222.htm
- http://m.blog.uliejh.cn/snews/4531.htm
- http://m.blog.uliejh.cn/snews/3413285.htm
- http://m.blog.uliejh.cn/snews/892829.htm
- http://m.blog.uliejh.cn/snews/849609.htm
- http://m.blog.uliejh.cn/snews/13445.htm
- http://m.blog.uliejh.cn/snews/73258.htm
- http://m.blog.uliejh.cn/snews/1169048.htm
- http://m.blog.uliejh.cn/snews/6397835.htm
- http://m.blog.uliejh.cn/snews/339442.htm
- http://m.blog.uliejh.cn/snews/6269.htm
- http://m.blog.uliejh.cn/snews/7814383.htm
- http://m.blog.uliejh.cn/snews/8085635.htm
- http://m.blog.uliejh.cn/snews/7108108.htm
- http://m.blog.uliejh.cn/snews/4818.htm
- http://m.blog.uliejh.cn/snews/18744.htm
- http://m.blog.uliejh.cn/snews/58487.htm
- http://m.blog.uliejh.cn/snews/478713.htm
- http://m.blog.uliejh.cn/snews/159710.htm
- http://m.blog.uliejh.cn/snews/871938.htm
- http://m.blog.uliejh.cn/snews/1271810.htm
- http://m.blog.uliejh.cn/snews/18138.htm
- http://m.blog.uliejh.cn/snews/3181.htm
- http://m.blog.uliejh.cn/snews/5006.htm
- http://m.blog.uliejh.cn/snews/2987.htm
- http://m.blog.uliejh.cn/snews/48500.htm
- http://m.blog.uliejh.cn/snews/7538.htm
- http://m.blog.uliejh.cn/snews/2544.htm
- http://m.blog.uliejh.cn/snews/7808822.htm
- http://m.blog.uliejh.cn/snews/87315.htm
- http://m.blog.uliejh.cn/snews/64531.htm
- http://m.blog.uliejh.cn/snews/8525423.htm
- http://m.blog.uliejh.cn/snews/8993.htm
- http://m.blog.uliejh.cn/snews/108183.htm
- http://m.blog.uliejh.cn/snews/5491218.htm
- http://m.blog.uliejh.cn/snews/20489.htm
- http://m.blog.uliejh.cn/snews/082022.htm
- http://m.blog.uliejh.cn/snews/7233918.htm
- http://m.blog.uliejh.cn/snews/8201188.htm
- http://m.blog.uliejh.cn/snews/92444.htm
- http://m.blog.uliejh.cn/snews/7280018.htm
- http://m.blog.uliejh.cn/snews/5833.htm
- http://m.blog.uliejh.cn/snews/0860.htm
- http://m.blog.uliejh.cn/snews/1159.htm
- http://m.blog.uliejh.cn/snews/430654.htm
- http://m.blog.uliejh.cn/snews/54900.htm
- http://m.blog.uliejh.cn/snews/0975138.htm
- http://m.blog.uliejh.cn/snews/2914454.htm
- http://m.blog.uliejh.cn/snews/7946.htm
- http://m.blog.uliejh.cn/snews/08326.htm
- http://m.blog.uliejh.cn/snews/591218.htm
- http://m.blog.uliejh.cn/snews/81046.htm
- http://m.blog.uliejh.cn/snews/094401.htm
- http://m.blog.uliejh.cn/snews/3139990.htm
- http://m.blog.uliejh.cn/snews/153914.htm
- http://m.blog.uliejh.cn/snews/9747009.htm
- http://m.blog.uliejh.cn/snews/8740.htm
- http://m.blog.uliejh.cn/snews/6164466.htm
- http://m.blog.uliejh.cn/snews/55011.htm
- http://m.blog.uliejh.cn/snews/966585.htm
- http://m.blog.uliejh.cn/snews/002988.htm
- http://m.blog.uliejh.cn/snews/8997.htm
- http://m.blog.uliejh.cn/snews/163203.htm
- http://m.blog.uliejh.cn/snews/5538.htm
- http://m.blog.uliejh.cn/snews/954523.htm
- http://m.blog.uliejh.cn/snews/7380392.htm
- http://m.blog.uliejh.cn/snews/4305.htm
- http://m.blog.uliejh.cn/snews/7489015.htm
- http://m.blog.uliejh.cn/snews/227854.htm
- http://m.blog.uliejh.cn/snews/3615.htm
- http://m.blog.uliejh.cn/snews/45684.htm
- http://m.blog.uliejh.cn/snews/5436.htm
- http://m.blog.uliejh.cn/snews/2730418.htm
- http://m.blog.uliejh.cn/snews/72852.htm
- http://m.blog.uliejh.cn/snews/5789.htm
- http://m.blog.uliejh.cn/snews/5537.htm
- http://m.blog.uliejh.cn/snews/21879.htm
- http://m.blog.uliejh.cn/snews/35629.htm
- http://m.blog.uliejh.cn/snews/7355370.htm
- http://m.blog.uliejh.cn/snews/10816.htm
- http://m.blog.uliejh.cn/snews/0647781.htm
- http://m.blog.uliejh.cn/snews/934340.htm
- http://m.blog.uliejh.cn/snews/96773.htm
- http://m.blog.uliejh.cn/snews/503953.htm
- http://m.blog.uliejh.cn/snews/4508.htm
- http://m.blog.uliejh.cn/snews/32184.htm
- http://m.blog.uliejh.cn/snews/5552317.htm
- http://m.blog.uliejh.cn/snews/32058.htm
- http://m.blog.uliejh.cn/snews/8280430.htm
- http://m.blog.uliejh.cn/snews/413071.htm
- http://m.blog.uliejh.cn/snews/9406282.htm
- http://m.blog.uliejh.cn/snews/9272.htm
- http://m.blog.uliejh.cn/snews/11304.htm
- http://m.blog.uliejh.cn/snews/002262.htm
- http://m.blog.uliejh.cn/snews/49075.htm
- http://m.blog.uliejh.cn/snews/1357.htm
- http://m.blog.uliejh.cn/snews/51742.htm
- http://m.blog.uliejh.cn/snews/772369.htm
- http://m.blog.uliejh.cn/snews/3795.htm
- http://m.blog.uliejh.cn/snews/780461.htm
- http://m.blog.uliejh.cn/snews/748614.htm
- http://m.blog.uliejh.cn/snews/4464.htm
- http://m.blog.uliejh.cn/snews/1010.htm
- http://m.blog.uliejh.cn/snews/1134031.htm
- http://m.blog.uliejh.cn/snews/6953.htm
- http://m.blog.uliejh.cn/snews/3687.htm
- http://m.blog.uliejh.cn/snews/8762.htm
- http://m.blog.uliejh.cn/snews/151161.htm
- http://m.blog.uliejh.cn/snews/1772.htm
- http://m.blog.uliejh.cn/snews/7883372.htm
- http://m.blog.uliejh.cn/snews/9885116.htm
- http://m.blog.uliejh.cn/snews/77596.htm
- http://m.blog.uliejh.cn/snews/962031.htm
- http://m.blog.uliejh.cn/snews/4542.htm
- http://m.blog.uliejh.cn/snews/255235.htm
- http://m.blog.uliejh.cn/snews/4522080.htm
- http://m.blog.uliejh.cn/snews/82656.htm
- http://m.blog.uliejh.cn/snews/3968.htm
- http://m.blog.uliejh.cn/snews/199734.htm
- http://m.blog.uliejh.cn/snews/12797.htm
- http://m.blog.uliejh.cn/snews/2267.htm
- http://m.blog.uliejh.cn/snews/474774.htm
- http://m.blog.uliejh.cn/snews/96983.htm
- http://m.blog.uliejh.cn/snews/3242488.htm
- http://m.blog.uliejh.cn/snews/1271.htm
- http://m.blog.uliejh.cn/snews/61207.htm
- http://m.blog.uliejh.cn/snews/597999.htm
- http://m.blog.uliejh.cn/snews/12031.htm
- http://m.blog.uliejh.cn/snews/6898.htm
- http://m.blog.uliejh.cn/snews/5550140.htm
- http://m.blog.uliejh.cn/snews/87765.htm
- http://m.blog.uliejh.cn/snews/4101.htm
- http://m.blog.uliejh.cn/snews/571248.htm
- http://m.blog.uliejh.cn/snews/3082.htm
- http://m.blog.uliejh.cn/snews/076984.htm
- http://m.blog.uliejh.cn/snews/7442.htm
- http://m.blog.uliejh.cn/snews/87962.htm
- http://m.blog.uliejh.cn/snews/08818.htm
- http://m.blog.uliejh.cn/snews/3143.htm
- http://m.blog.uliejh.cn/snews/8252019.htm
- http://m.blog.uliejh.cn/snews/52276.htm
- http://m.blog.uliejh.cn/snews/5458720.htm
- http://m.blog.uliejh.cn/snews/14497.htm
- http://m.blog.uliejh.cn/snews/551994.htm
- http://m.blog.uliejh.cn/snews/0875308.htm
- http://m.blog.uliejh.cn/snews/412321.htm
- http://m.blog.uliejh.cn/snews/63865.htm
- http://m.blog.uliejh.cn/snews/0354853.htm
- http://m.blog.uliejh.cn/snews/140565.htm
- http://m.blog.uliejh.cn/snews/6917.htm
- http://m.blog.uliejh.cn/snews/5906.htm
- http://m.blog.uliejh.cn/snews/988908.htm
- http://m.blog.uliejh.cn/snews/992597.htm
- http://m.blog.uliejh.cn/snews/55888.htm
- http://m.blog.uliejh.cn/snews/42181.htm
- http://m.blog.uliejh.cn/snews/8726376.htm
- http://m.blog.uliejh.cn/snews/1571.htm
- http://m.blog.uliejh.cn/snews/685988.htm
- http://m.blog.uliejh.cn/snews/718164.htm
- http://m.blog.uliejh.cn/snews/971104.htm
- http://m.blog.uliejh.cn/snews/354295.htm
- http://m.blog.uliejh.cn/snews/0168.htm
- http://m.blog.uliejh.cn/snews/51282.htm
- http://m.blog.uliejh.cn/snews/6652253.htm
- http://m.blog.uliejh.cn/snews/947698.htm
- http://m.blog.uliejh.cn/snews/8510203.htm
- http://m.blog.uliejh.cn/snews/92951.htm
- http://m.blog.uliejh.cn/snews/66859.htm
- http://m.blog.uliejh.cn/snews/7435088.htm
- http://m.blog.uliejh.cn/snews/031269.htm
- http://m.blog.uliejh.cn/snews/7282422.htm
- http://m.blog.uliejh.cn/snews/729685.htm
- http://m.blog.uliejh.cn/snews/71069.htm
- http://m.blog.uliejh.cn/snews/9102179.htm
- http://m.blog.uliejh.cn/snews/43851.htm
- http://m.blog.uliejh.cn/snews/427661.htm
- http://m.blog.uliejh.cn/snews/9741.htm
- http://m.blog.uliejh.cn/snews/867404.htm
- http://m.blog.uliejh.cn/snews/968770.htm
- http://m.blog.uliejh.cn/snews/64140.htm
- http://m.blog.uliejh.cn/snews/14719.htm
- http://m.blog.uliejh.cn/snews/12131.htm
- http://m.blog.uliejh.cn/snews/58410.htm
- http://m.blog.uliejh.cn/snews/2380.htm
- http://m.blog.uliejh.cn/snews/00627.htm
- http://m.blog.uliejh.cn/snews/7766.htm
- http://m.blog.uliejh.cn/snews/2493.htm
- http://m.blog.uliejh.cn/snews/2781505.htm
- http://m.blog.uliejh.cn/snews/71873.htm
- http://m.blog.uliejh.cn/snews/51651.htm
- http://m.blog.uliejh.cn/snews/773341.htm
- http://m.blog.uliejh.cn/snews/10282.htm
- http://m.blog.uliejh.cn/snews/660444.htm
- http://m.blog.uliejh.cn/snews/220154.htm
- http://m.blog.uliejh.cn/snews/6595.htm
- http://m.blog.uliejh.cn/snews/9512211.htm
- http://m.blog.uliejh.cn/snews/0778.htm
- http://m.blog.uliejh.cn/snews/5355.htm
- http://m.blog.uliejh.cn/snews/033339.htm

## 项目结构

```
linksphere/
├── backend/                          # 后端服务源代码
│   ├── src/
│   │   ├── api/                      # RESTful API 路由与控制器
│   │   │   ├── v1/                   # API 版本 v1 端点
│   │   │   │   ├── links.js          # 外链增删改查接口
│   │   │   │   ├── tags.js           # 标签管理接口
│   │   │   │   ├── users.js          # 用户认证与资料接口
│   │   │   │   └── stats.js          # 统计看板数据接口
│   │   │   └── middleware/           # 鉴权、日志、限流中间件
│   │   ├── services/                 # 业务逻辑层
│   │   │   ├── linkService.js        # 外链接入、去重、健康检查逻辑
│   │   │   ├── searchService.js      # 全文检索与过滤排序逻辑
│   │   │   └── rssService.js         # RSS 订阅源生成逻辑
│   │   ├── models/                   # 数据库对象关系映射模型
│   │   │   ├── Link.js               # 外链条目模型
│   │   │   ├── Tag.js                # 标签模型
│   │   │   └── User.js               # 用户模型
│   │   ├── workers/                  # 后台任务队列
│   │   │   ├── healthCheck.js        # 定时死链检测任务
│   │   │   └── indexWorker.js        # 外链索引更新任务
│   │   └── config/                   # 环境配置与数据库连接
│   ├── tests/                        # 单元测试与集成测试
│   └── package.json
├── frontend/                         # 前端单页应用源代码
│   ├── src/
│   │   ├── pages/                    # 路由页面组件
│   │   │   ├── Home.jsx              # 首页外链列表与检索
│   │   │   ├── Detail.jsx            # 单条外链详情页
│   │   │   ├── Dashboard.jsx         # 管理员仪表盘
│   │   │   └── Favorites.jsx         # 用户收藏夹管理
│   │   ├── components/               # 可复用 UI 组件
│   │   │   ├── LinkCard.jsx          # 外链卡片展示组件
│   │   │   ├── TagFilter.jsx         # 标签筛选组件
│   │   │   └── Pagination.jsx        # 分页组件
│   │   ├── hooks/                    # 自定义 React Hooks
│   │   ├── utils/                    # 工具函数与 API 客户端
│   │   └── styles/                   # 全局样式与主题变量
│   ├── public/                       # 静态资源
│   └── package.json
├── docs/                             # 项目文档
│   ├── user-guide/                   # 用户手册
│   ├── developer/                    # 开发者文档
│   └── operations/                   # 部署运维手册
├── scripts/                          # 运维与部署脚本
│   ├── seed.js                       # 测试数据填充脚本
│   └── migrate.js                    # 数据库迁移脚本
├── docker-compose.yml                # 容器编排配置
├── Dockerfile                        # 应用容器镜像构建文件
├── .env.example                      # 环境变量模板
├── nginx.conf                        # 生产环境 Nginx 配置示例
├── LICENSE                           # MIT 许可证
└── README.md                         # 本文件
```

## 贡献指南

我们欢迎所有形式的贡献，包括但不限于功能提议、缺陷报告、代码提交与文档完善。请遵循以下流程参与项目开发。

首先，在 GitHub 仓库中提交 Issue 描述您希望解决的问题或新增的功能，等待维护者确认可行性并分配标签。对于简单的拼写错误或文档修正，可直接发起 Pull Request。

其次，Fork 本仓库至您的个人账号，并基于 `develop` 分支创建您的特性分支（如 `feature/rss-export` 或 `fix/search-empty`）。请确保分支命名简洁且语义清晰。

第三，在本地完成开发后，运行完整的测试套件与代码风格检查（`npm run test` 与 `npm run lint`），确保所有现有功能未发生回归，同时为新增代码补充相应的单元测试与文档注释。

第四，提交 Pull Request 至本仓库的 `develop` 分支，并在 PR 描述中关联对应的 Issue 编号，详细说明变更内容、测试覆盖情况以及可能的破坏性影响。PR 须经过至少两名维护者 Code Review 后方可合并。

最后，对于长期贡献者，可申请加入核心开发团队，获得直接推送权限并参与版本发布规划。所有贡献者均需遵守项目行为准则，维护友善、专业的协作氛围。

## 常见问题

**Q：LinkSphere 是否支持私有化部署，以及数据库是否必须使用 PostgreSQL？**

A：LinkSphere 完全支持私有化部署，所有源代码均可本地编译运行。目前主数据库仅适配 PostgreSQL，因其 JSONB 类型与复杂索引能力对标签体系与检索性能至关重要。如需使用 MySQL 或其他关系型数据库，需自行修改模型层适配，官方暂不提供原生支持。

**Q：外链健康检查的检测频率与异常处理机制是怎样的？**

A：系统默认每 24 小时对所有已收录外链执行一次 HEAD 请求检测，超时阈值设为 10 秒。针对返回 4xx/5xx 状态码或超时的链接，系统会将其标记为「异常」并记录错误详情。异常链接不会自动删除，而是保留在数据库中供管理员人工审核，同时提供重检按钮支持按需重新检测。连续 7 次检测失败的链接会触发邮件告警通知。

**Q：如何将已有的外链收藏数据（如浏览器书签、Pocket、Instapaper）迁移至 LinkSphere？**

A：LinkSphere 提供数据导入工具，支持 HTML 书签文件（Netscape 格式）、CSV 表格以及 Pocket 导出的 JSON 格式。用户可在「设置 - 数据导入」页面上传文件，系统自动解析并映射标题、URL 与标签。对于自定义格式，开发者可参考 `docs/developer/import-adapter.md` 编写适配器扩展。

## 许可证

MIT

> 外链数量: 250 | 生成时间: 2026-08-24 23:41:17
