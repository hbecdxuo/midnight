# NewsLink Aggregator

NewsLink Aggregator 是一个面向技术资讯聚合与轻量级新闻分发场景的 URL 索引与转发系统。该项目定位为技术内容外链汇总中间件，主要服务于个人开发者、小型内容团队以及自建资讯门户的运维人员，帮助其将分散的新闻条目通过统一索引层进行归集、分类与分发。系统不存储原始文章内容，仅维护新闻条目的元信息与原始地址映射，从而降低内容管理成本，同时保留对第三方新闻源的最大兼容性。

## 功能概览

- 统一外链索引管理：支持批量导入新闻条目原始 URL，自动生成内部唯一标识，建立稳定的索引映射表。

- 元信息自动补全：通过可插拔的元数据抓取插件，自动获取新闻标题、发布时间、来源域名等基础信息，减少人工录入。

- 分类标签系统：允许用户为每个新闻链接添加多个自定义标签，支持按标签筛选和聚合展示。

- 批量导入导出：提供 CSV 与 JSON 格式的批量链接导入导出接口，方便与其他系统进行数据迁移或同步。

- 访问统计与热榜排序：记录每个外链的点击次数与最后访问时间，支持按热度、时间等维度生成排行榜。

- 只读缓存层：内置 Redis 缓存，对高频访问的链接列表进行缓存加速，降低数据库查询压力。

- RESTful API 接口：提供完整的 JSON API，支持第三方客户端或前端页面进行远程调用与集成。

## 应用场景

个人技术博客的每日新闻聚合
个人博主或独立开发者可以使用 NewsLink Aggregator 每日导入关注领域内的新闻链接，通过分类标签整理后嵌入博客侧边栏或独立新闻页面，为站点访客提供增值内容。

小型内容团队的内部资讯共享
内容编辑团队可将各部门关注的行业动态链接统一录入系统，通过标签过滤快速定位相关新闻，减少重复检索与信息遗漏，提升协作效率。

自建新闻门户的底层索引支撑
面向特定领域的新闻门户站点可使用该系统作为底层外链索引服务，前端通过 API 调用获取链接列表，实现新闻栏目的动态更新与排序。

运维监控通知聚合
运维团队可将各类监控告警消息的链接地址导入系统，按服务器或应用名称打标，形成统一的通知看板，便于故障回溯与复盘。

## 快速开始

以下步骤帮助你在本地环境快速启动 NewsLink Aggregator 服务。

```bash
# 克隆代码仓库
git clone https://github.com/example/newslink-aggregator.git

# 进入项目目录
cd newslink-aggregator

# 安装依赖（使用 pip 与虚拟环境）
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt

# 初始化数据库表结构
python manage.py migrate

# 启动开发服务器
python manage.py runserver --host 0.0.0.0 --port 8080
```

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|---------|---------|------|
| Python | 3.9 及以上 | 核心运行环境，推荐使用 3.11 长期支持版本 |
| PostgreSQL | 14.0 及以上 | 主数据库，用于存储链接元信息与索引数据 |
| Redis | 6.2 及以上 | 缓存与临时会话存储，用于提升高频查询性能 |
| Celery Broker | RabbitMQ 3.10 或 Redis 7.0 | 任务队列后端，用于异步元数据抓取 |
| Node.js | 18.0 及以上 | 仅在前端构建或开发调试时需要，生产环境非必需 |
| Nginx | 1.22 及以上 | 生产环境推荐反向代理服务器，非直接依赖 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|------|------|-----------|
| 用户手册 | /docs/user-guide/ | 如何导入链接、管理标签、查看排行榜，以及日常运维操作 |
| 开发者指南 | /docs/developer-guide/ | 如何扩展元数据插件、自定义 API 端点、修改缓存策略 |
| 部署指南 | /docs/deployment/ | 如何在生产环境配置 Nginx、PostgreSQL 高可用、Redis 集群 |
| API 参考 | /docs/api-reference/ | 完整的 RESTful API 端点列表、请求参数、响应格式与错误码说明 |
| 架构设计 | /docs/architecture/ | 系统整体架构图、数据流走向、各模块职责边界与扩展点设计 |
| 常见问题 | /docs/faq/ | 汇总社区反馈的高频疑问，涵盖安装、配置、性能调优等方面 |

## 资源列表

- http://m.3g.uliejh.cn/nnews/6864478.htm
- http://m.3g.uliejh.cn/nnews/63682.htm
- http://m.3g.uliejh.cn/nnews/0250112.htm
- http://m.3g.uliejh.cn/nnews/587110.htm
- http://m.3g.uliejh.cn/nnews/24927.htm
- http://m.3g.uliejh.cn/nnews/9167.htm
- http://m.3g.uliejh.cn/nnews/35240.htm
- http://m.3g.uliejh.cn/nnews/4935314.htm
- http://m.3g.uliejh.cn/nnews/60594.htm
- http://m.3g.uliejh.cn/nnews/2392.htm
- http://m.3g.uliejh.cn/nnews/7017610.htm
- http://m.3g.uliejh.cn/nnews/65601.htm
- http://m.3g.uliejh.cn/nnews/8530.htm
- http://m.3g.uliejh.cn/nnews/836249.htm
- http://m.3g.uliejh.cn/nnews/3799.htm
- http://m.3g.uliejh.cn/nnews/438934.htm
- http://m.3g.uliejh.cn/nnews/12673.htm
- http://m.3g.uliejh.cn/nnews/33041.htm
- http://m.3g.uliejh.cn/nnews/044318.htm
- http://m.3g.uliejh.cn/nnews/7632.htm
- http://m.3g.uliejh.cn/nnews/5097585.htm
- http://m.3g.uliejh.cn/nnews/05842.htm
- http://m.3g.uliejh.cn/nnews/6214710.htm
- http://m.3g.uliejh.cn/nnews/08158.htm
- http://m.3g.uliejh.cn/nnews/760075.htm
- http://m.3g.uliejh.cn/nnews/325477.htm
- http://m.3g.uliejh.cn/nnews/8188363.htm
- http://m.3g.uliejh.cn/nnews/3906857.htm
- http://m.3g.uliejh.cn/nnews/7707.htm
- http://m.3g.uliejh.cn/nnews/739219.htm
- http://m.3g.uliejh.cn/nnews/9916111.htm
- http://m.3g.uliejh.cn/nnews/725408.htm
- http://m.3g.uliejh.cn/nnews/186934.htm
- http://m.3g.uliejh.cn/nnews/60289.htm
- http://m.3g.uliejh.cn/nnews/908091.htm
- http://m.3g.uliejh.cn/nnews/18926.htm
- http://m.3g.uliejh.cn/nnews/3460913.htm
- http://m.3g.uliejh.cn/nnews/5310.htm
- http://m.3g.uliejh.cn/nnews/35176.htm
- http://m.3g.uliejh.cn/nnews/26103.htm
- http://m.3g.uliejh.cn/nnews/86476.htm
- http://m.3g.uliejh.cn/nnews/71676.htm
- http://m.3g.uliejh.cn/nnews/1903875.htm
- http://m.3g.uliejh.cn/nnews/86120.htm
- http://m.3g.uliejh.cn/nnews/041191.htm
- http://m.3g.uliejh.cn/nnews/04165.htm
- http://m.3g.uliejh.cn/nnews/17838.htm
- http://m.3g.uliejh.cn/nnews/94607.htm
- http://m.3g.uliejh.cn/nnews/52563.htm
- http://m.3g.uliejh.cn/nnews/5596620.htm
- http://m.3g.uliejh.cn/nnews/36256.htm
- http://m.3g.uliejh.cn/nnews/0658034.htm
- http://m.3g.uliejh.cn/nnews/3592.htm
- http://m.3g.uliejh.cn/nnews/65235.htm
- http://m.3g.uliejh.cn/nnews/5437.htm
- http://m.3g.uliejh.cn/nnews/625518.htm
- http://m.3g.uliejh.cn/nnews/2225844.htm
- http://m.3g.uliejh.cn/nnews/9865.htm
- http://m.3g.uliejh.cn/nnews/881850.htm
- http://m.3g.uliejh.cn/nnews/9007317.htm
- http://m.3g.uliejh.cn/nnews/3658432.htm
- http://m.3g.uliejh.cn/nnews/49309.htm
- http://m.3g.uliejh.cn/nnews/03404.htm
- http://m.3g.uliejh.cn/nnews/5184.htm
- http://m.3g.uliejh.cn/nnews/8133.htm
- http://m.3g.uliejh.cn/nnews/7133.htm
- http://m.3g.uliejh.cn/nnews/94866.htm
- http://m.3g.uliejh.cn/nnews/0056.htm
- http://m.3g.uliejh.cn/nnews/1274067.htm
- http://m.3g.uliejh.cn/nnews/397461.htm
- http://m.3g.uliejh.cn/nnews/2878704.htm
- http://m.3g.uliejh.cn/nnews/5729668.htm
- http://m.3g.uliejh.cn/nnews/7558.htm
- http://m.3g.uliejh.cn/nnews/3825.htm
- http://m.3g.uliejh.cn/nnews/47208.htm
- http://m.3g.uliejh.cn/nnews/43422.htm
- http://m.3g.uliejh.cn/nnews/344860.htm
- http://m.3g.uliejh.cn/nnews/34090.htm
- http://m.3g.uliejh.cn/nnews/01671.htm
- http://m.3g.uliejh.cn/nnews/2830743.htm
- http://m.3g.uliejh.cn/nnews/7269.htm
- http://m.3g.uliejh.cn/nnews/77174.htm
- http://m.3g.uliejh.cn/nnews/7127564.htm
- http://m.3g.uliejh.cn/nnews/517363.htm
- http://m.3g.uliejh.cn/nnews/863440.htm
- http://m.3g.uliejh.cn/nnews/487477.htm
- http://m.3g.uliejh.cn/nnews/0555.htm
- http://m.3g.uliejh.cn/nnews/478519.htm
- http://m.3g.uliejh.cn/nnews/7160514.htm
- http://m.3g.uliejh.cn/nnews/7008.htm
- http://m.3g.uliejh.cn/nnews/5129.htm
- http://m.3g.uliejh.cn/nnews/48115.htm
- http://m.3g.uliejh.cn/nnews/7800.htm
- http://m.3g.uliejh.cn/nnews/386517.htm
- http://m.3g.uliejh.cn/nnews/6580.htm
- http://m.3g.uliejh.cn/nnews/8321585.htm
- http://m.3g.uliejh.cn/nnews/5299.htm
- http://m.3g.uliejh.cn/nnews/186474.htm
- http://m.3g.uliejh.cn/nnews/0722976.htm
- http://m.3g.uliejh.cn/nnews/6812151.htm
- http://m.3g.uliejh.cn/nnews/82414.htm
- http://m.3g.uliejh.cn/nnews/43356.htm
- http://m.3g.uliejh.cn/nnews/999591.htm
- http://m.3g.uliejh.cn/nnews/61970.htm
- http://m.3g.uliejh.cn/nnews/505221.htm
- http://m.3g.uliejh.cn/nnews/76457.htm
- http://m.3g.uliejh.cn/nnews/23952.htm
- http://m.3g.uliejh.cn/nnews/272144.htm
- http://m.3g.uliejh.cn/nnews/2953.htm
- http://m.3g.uliejh.cn/nnews/5209.htm
- http://m.3g.uliejh.cn/nnews/1236.htm
- http://m.3g.uliejh.cn/nnews/435239.htm
- http://m.3g.uliejh.cn/nnews/9529.htm
- http://m.3g.uliejh.cn/nnews/8417780.htm
- http://m.3g.uliejh.cn/nnews/776490.htm
- http://m.3g.uliejh.cn/nnews/741106.htm
- http://m.3g.uliejh.cn/nnews/691841.htm
- http://m.3g.uliejh.cn/nnews/8364408.htm
- http://m.3g.uliejh.cn/nnews/417826.htm
- http://m.3g.uliejh.cn/nnews/2505197.htm
- http://m.3g.uliejh.cn/nnews/3505.htm
- http://m.3g.uliejh.cn/nnews/6266.htm
- http://m.3g.uliejh.cn/nnews/5265.htm
- http://m.3g.uliejh.cn/nnews/7696047.htm
- http://m.3g.uliejh.cn/nnews/82848.htm
- http://m.3g.uliejh.cn/nnews/17466.htm
- http://m.3g.uliejh.cn/nnews/5411.htm
- http://m.3g.uliejh.cn/nnews/887634.htm
- http://m.3g.uliejh.cn/nnews/7942799.htm
- http://m.3g.uliejh.cn/nnews/12213.htm
- http://m.3g.uliejh.cn/nnews/02080.htm
- http://m.3g.uliejh.cn/nnews/3207299.htm
- http://m.3g.uliejh.cn/nnews/74095.htm
- http://m.3g.uliejh.cn/nnews/9576.htm
- http://m.3g.uliejh.cn/nnews/480822.htm
- http://m.3g.uliejh.cn/nnews/70405.htm
- http://m.3g.uliejh.cn/nnews/993593.htm
- http://m.3g.uliejh.cn/nnews/550377.htm
- http://m.3g.uliejh.cn/nnews/6598374.htm
- http://m.3g.uliejh.cn/nnews/66545.htm
- http://m.3g.uliejh.cn/nnews/86973.htm
- http://m.3g.uliejh.cn/nnews/0967.htm
- http://m.3g.uliejh.cn/nnews/25577.htm
- http://m.3g.uliejh.cn/nnews/55063.htm
- http://m.3g.uliejh.cn/nnews/7329.htm
- http://m.3g.uliejh.cn/nnews/87163.htm
- http://m.3g.uliejh.cn/nnews/7910.htm
- http://m.3g.uliejh.cn/nnews/41259.htm
- http://m.3g.uliejh.cn/nnews/1248.htm
- http://m.3g.uliejh.cn/nnews/59721.htm
- http://m.3g.uliejh.cn/nnews/70987.htm
- http://m.3g.uliejh.cn/nnews/1214258.htm
- http://m.3g.uliejh.cn/nnews/59937.htm
- http://m.3g.uliejh.cn/nnews/8198.htm
- http://m.3g.uliejh.cn/nnews/098880.htm
- http://m.3g.uliejh.cn/nnews/94531.htm
- http://m.3g.uliejh.cn/nnews/5140829.htm
- http://m.3g.uliejh.cn/nnews/666523.htm
- http://m.3g.uliejh.cn/nnews/6029364.htm
- http://m.3g.uliejh.cn/nnews/8932011.htm
- http://m.3g.uliejh.cn/nnews/71941.htm
- http://m.3g.uliejh.cn/nnews/8960.htm
- http://m.3g.uliejh.cn/nnews/306068.htm
- http://m.3g.uliejh.cn/nnews/29852.htm
- http://m.3g.uliejh.cn/nnews/4153003.htm
- http://m.3g.uliejh.cn/nnews/2914.htm
- http://m.3g.uliejh.cn/nnews/28066.htm
- http://m.3g.uliejh.cn/nnews/59000.htm
- http://m.3g.uliejh.cn/nnews/4011.htm
- http://m.3g.uliejh.cn/nnews/0697.htm
- http://m.3g.uliejh.cn/nnews/3607.htm
- http://m.3g.uliejh.cn/nnews/2791873.htm
- http://m.3g.uliejh.cn/nnews/7835203.htm
- http://m.3g.uliejh.cn/nnews/008812.htm
- http://m.3g.uliejh.cn/nnews/3367.htm
- http://m.3g.uliejh.cn/nnews/66396.htm
- http://m.3g.uliejh.cn/nnews/796186.htm
- http://m.3g.uliejh.cn/nnews/97855.htm
- http://m.3g.uliejh.cn/nnews/12463.htm
- http://m.3g.uliejh.cn/nnews/6514.htm
- http://m.3g.uliejh.cn/nnews/5486658.htm
- http://m.3g.uliejh.cn/nnews/9688441.htm
- http://m.3g.uliejh.cn/nnews/8034.htm
- http://m.3g.uliejh.cn/nnews/974537.htm
- http://m.3g.uliejh.cn/nnews/48082.htm
- http://m.3g.uliejh.cn/nnews/1660.htm
- http://m.3g.uliejh.cn/nnews/0540.htm
- http://m.3g.uliejh.cn/nnews/9382.htm
- http://m.3g.uliejh.cn/nnews/60842.htm
- http://m.3g.uliejh.cn/nnews/184432.htm
- http://m.3g.uliejh.cn/nnews/7376.htm
- http://m.3g.uliejh.cn/nnews/1117.htm
- http://m.3g.uliejh.cn/nnews/083863.htm
- http://m.3g.uliejh.cn/nnews/2552133.htm
- http://m.3g.uliejh.cn/nnews/773623.htm
- http://m.3g.uliejh.cn/nnews/5641418.htm
- http://m.3g.uliejh.cn/nnews/3290068.htm
- http://m.3g.uliejh.cn/nnews/6063219.htm
- http://m.3g.uliejh.cn/nnews/7018089.htm
- http://m.3g.uliejh.cn/nnews/16719.htm
- http://m.3g.uliejh.cn/nnews/97850.htm
- http://m.3g.uliejh.cn/nnews/472833.htm
- http://m.3g.uliejh.cn/nnews/87509.htm
- http://m.3g.uliejh.cn/nnews/5052.htm
- http://m.3g.uliejh.cn/nnews/3873688.htm
- http://m.3g.uliejh.cn/nnews/92624.htm
- http://m.3g.uliejh.cn/nnews/5284561.htm
- http://m.3g.uliejh.cn/nnews/0124199.htm
- http://m.3g.uliejh.cn/nnews/1221390.htm
- http://m.3g.uliejh.cn/nnews/1862779.htm
- http://m.3g.uliejh.cn/nnews/73563.htm
- http://m.3g.uliejh.cn/nnews/0544693.htm
- http://m.3g.uliejh.cn/nnews/8909176.htm
- http://m.3g.uliejh.cn/nnews/97162.htm
- http://m.3g.uliejh.cn/nnews/09533.htm
- http://m.3g.uliejh.cn/nnews/3326601.htm
- http://m.3g.uliejh.cn/nnews/2251932.htm
- http://m.3g.uliejh.cn/nnews/1809.htm
- http://m.3g.uliejh.cn/nnews/715566.htm
- http://m.3g.uliejh.cn/nnews/31352.htm
- http://m.3g.uliejh.cn/nnews/2152.htm
- http://m.3g.uliejh.cn/nnews/4070953.htm
- http://m.3g.uliejh.cn/nnews/739643.htm
- http://m.3g.uliejh.cn/nnews/18866.htm
- http://m.3g.uliejh.cn/nnews/329648.htm
- http://m.3g.uliejh.cn/nnews/6310928.htm
- http://m.3g.uliejh.cn/nnews/3442.htm
- http://m.3g.uliejh.cn/nnews/548593.htm
- http://m.3g.uliejh.cn/nnews/0471665.htm
- http://m.3g.uliejh.cn/nnews/97634.htm
- http://m.3g.uliejh.cn/nnews/8915.htm
- http://m.3g.uliejh.cn/nnews/527615.htm
- http://m.3g.uliejh.cn/nnews/5320195.htm
- http://m.3g.uliejh.cn/nnews/918244.htm
- http://m.3g.uliejh.cn/nnews/7208353.htm
- http://m.3g.uliejh.cn/nnews/495118.htm
- http://m.3g.uliejh.cn/nnews/4794990.htm
- http://m.3g.uliejh.cn/nnews/5263.htm
- http://m.3g.uliejh.cn/nnews/08227.htm
- http://m.3g.uliejh.cn/nnews/50441.htm
- http://m.3g.uliejh.cn/nnews/2255133.htm
- http://m.3g.uliejh.cn/nnews/7904.htm
- http://m.3g.uliejh.cn/nnews/490127.htm
- http://m.3g.uliejh.cn/nnews/6404993.htm
- http://m.3g.uliejh.cn/nnews/561380.htm
- http://m.3g.uliejh.cn/nnews/68716.htm
- http://m.3g.uliejh.cn/nnews/4807380.htm
- http://m.3g.uliejh.cn/nnews/7602703.htm
- http://m.3g.uliejh.cn/nnews/526746.htm
- http://m.3g.uliejh.cn/nnews/957030.htm

## 项目结构

项目采用分层架构，将核心索引、元数据抓取、API 展示和后台任务分离为独立模块。

```
news-aggregator/
├── src/                                 # 核心源代码目录
│   ├── aggregator/                      # 聚合引擎主模块
│   │   ├── indexer.py                   # 链接索引生成器，负责生成唯一标识
│   │   ├── fetcher.py                   # 元数据抓取调度器，调用插件抓取信息
│   │   ├── cache.py                     # 缓存管理，封装 Redis 读写逻辑
│   │   └── tags.py                      # 标签系统，处理标签增删改查
│   ├── api/                             # RESTful API 模块
│   │   ├── routes.py                    # 路由注册，绑定 URL 与视图函数
│   │   ├── serializers.py               # 请求参数与响应数据序列化
│   │   └── middlewares.py               # 鉴权与日志中间件
│   ├── models/                          # 数据模型层（ORM 映射）
│   │   ├── link.py                      # 链接实体模型，含字段与索引定义
│   │   ├── click_log.py                 # 点击日志模型，用于统计热度
│   │   └── tag.py                       # 标签实体模型，多对多关联链接
│   └── plugins/                         # 元数据抓取插件目录
│       ├── base.py                      # 插件基类，定义抓取接口规范
│       ├── opengraph.py                 # Open Graph 协议解析插件
│       └── html_parser.py               # 通用 HTML 标题与描述解析插件
├── config/                              # 配置文件目录
│   ├── development.py                   # 开发环境配置（本地数据库、缓存）
│   ├── production.py                    # 生产环境配置（外部服务、连接池）
│   └── settings.py                      # 全局配置加载器
├── scripts/                             # 运维与工具脚本
│   ├── import_links.py                  # 批量导入链接命令行工具
│   ├── export_stats.py                  # 导出统计数据脚本
│   └── clean_cache.py                   # 清理过期缓存任务脚本
├── tests/                               # 单元测试与集成测试目录
│   ├── test_indexer.py                  # 索引生成器单元测试
│   ├── test_api.py                      # API 端点集成测试
│   └── fixtures/                        # 测试用固定数据集
├── docs/                                # 项目文档源码（Markdown 与 Sphinx）
├── requirements.txt                     # Python 依赖清单（生产环境）
├── requirements-dev.txt                 # 开发额外依赖（测试、代码检查工具）
├── manage.py                            # 应用管理入口（启动、迁移、shell）
├── Dockerfile                           # 容器化构建文件
├── docker-compose.yml                   # 本地开发编排服务（PostgreSQL + Redis）
└── README.md                            # 项目入口文档（本文件）
```

## 贡献指南

欢迎各类形式的贡献，包括但不限于功能建议、代码提交、文档修正和插件开发。请遵循以下流程：

1. 查阅问题列表与项目看板
访问 GitHub Issues 与 Project Board，了解当前待处理的任务与规划中的功能。如发现未被记录的问题或改进点，请先新建 Issue 进行讨论，避免重复劳动。

2. 派生仓库并创建功能分支
将主仓库派生至个人账户，然后克隆派生仓库到本地。基于 main 分支创建新的功能分支，分支命名采用 feat/xxx 或 fix/xxx 格式，例如 feat/weibo-fetcher。

3. 编写代码与单元测试
在功能分支上完成代码修改，并同步编写对应的单元测试，确保测试覆盖新增或修改的逻辑。运行现有测试套件，保证无回归问题。

4. 提交变更并推送至派生仓库
编写符合规范的提交信息，采用 type(scope): description 格式，例如 feat(plugin): add weibo metadata extractor。提交后推送至派生仓库的对应分支。

5. 发起拉取请求
在 GitHub 上向主仓库的 main 分支发起拉取请求。在 PR 描述中清晰说明变更目的、实现方案、测试结果以及是否涉及破坏性改动。等待维护者审阅与反馈。

## 常见问题

Q: 元数据抓取失败或超时的处理方式是什么？

A: 系统内置了指数退避重试机制，默认对失败任务重试三次。若依旧失败，该链接会被标记为“抓取异常”状态，并记录错误日志。管理员可通过管理后台手动重新触发抓取，或检查目标站点是否可访问、是否存在反爬限制。

Q: 如何扩展新的元数据抓取插件？

A: 在 plugins 目录下新建 Python 文件，继承 base.py 中的 BaseFetcher 类，实现 fetch_metadata(url) 方法，返回包含 title、published_at、source_domain 等字段的字典。然后在配置文件的 PLUGIN_LIST 中注册该类即可。

Q: 生产环境下如何提升系统的并发处理能力？

A: 建议采用分离部署策略：API 服务部署多个实例，前端使用 Nginx 负载均衡；Celery Worker 独立部署，并根据队列深度动态调整 Worker 数量；PostgreSQL 开启连接池，Redis 使用集群模式。具体调优参数可参考部署文档中的性能调优章节。

## 许可证

MIT

> 外链数量: 250 | 生成时间: 2026-08-24 23:40:21
