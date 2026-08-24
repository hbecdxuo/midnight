# WebLink Navigator

WebLink Navigator 是一个面向技术研究者和信息分析人员的轻量级外链资源聚合与导航工具。该项目旨在解决分散于各处的新闻、公告、技术文档入口难以统一检索和长期追踪的问题，通过将大量外部链接以结构化方式收录并辅以元信息标签，提供高效的访问入口管理方案。

项目核心定位为技术资源导航枢纽，适用于需要频繁查阅特定领域信息源、构建个人知识采集工作流的用户。WebLink Navigator 不存储或缓存任何外部资源内容，仅提供链接索引与分类展示功能，所有访问行为直接跳转至原始来源。

## 功能概览

批量链接导入与自动规范化：支持从纯文本、CSV 及 JSON 格式批量导入链接数据，自动识别 URL 结构并校验可用性。

自定义分类标签系统：允许用户为每条链接添加多级标签，支持基于标签的快速筛选与聚合视图。

链接状态健康检查：内置异步 HTTP 状态检测器，可定时检查链接可达性，并以图标形式标注异常状态。

全文检索与高级过滤：基于链接标题、描述、标签及来源域名的全文搜索，支持多条件组合过滤。

收藏夹与阅读列表：用户可将高频访问链接加入个人收藏夹，或创建临时阅读列表用于阶段性研究任务。

数据导入导出接口：提供 RESTful API 与命令行工具，支持链接库的完整导入导出，便于迁移与备份。

访问统计与热度排序：记录链接被点击的次数与最近访问时间，支持按热度、更新时间或创建时间排序。

## 应用场景

技术文档聚合查阅：开发者在学习新技术栈时，可将官方文档、社区教程、API 参考及问题讨论帖的链接统一收录，通过标签分类快速定位所需资料，避免在多个浏览器标签页间反复切换。

舆情信息追踪：分析师或媒体从业者可将多个新闻站点、公告栏、行业报告的入口链接集中管理，每日定时刷新查看更新，配合状态检测功能及时发现失效或变更的链接。

开源项目依赖链管理：开源维护者可将项目所依赖的第三方库、工具链、部署平台及监控面板的链接汇总，作为项目外部资源清单随版本发布，方便贡献者快速上手。

学术文献参考索引：研究人员在撰写论文或综述时，可将参考文献的在线版本、数据来源网站、预印本服务器及合作者主页等链接统一整理，生成可共享的资源列表。

个人知识库入口整合：知识管理爱好者可将各类订阅源、笔记软件共享链接、云存储目录及协作白板的入口集中存放，形成统一的外部资源访问起点。

## 快速开始

以下步骤指导您在本地环境快速启动 WebLink Navigator 服务。

```bash
# 克隆代码仓库
git clone https://github.com/weblink-navigator/weblink-navigator.git
cd weblink-navigator

# 安装项目依赖（使用 pip 和 npm）
pip install -r requirements.txt
cd frontend && npm install && cd ..

# 初始化数据库并运行开发服务器
python manage.py migrate
python manage.py runserver 0.0.0.0:8000
```

启动成功后，访问 http://localhost:8000 即可进入导航主页。默认管理员账号为 admin，密码为 admin123，首次登录后请及时修改。

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
| :--- | :--- | :--- |
| Python | 3.9 至 3.11 | 后端运行环境，3.12 暂未完全兼容 |
| Node.js | 18.x 或 20.x LTS | 前端构建与开发依赖管理 |
| PostgreSQL | 13.0 及以上 | 主数据库，用于存储链接元数据与用户信息 |
| Redis | 6.0 及以上 | 缓存与异步任务队列后端 |
| Nginx | 1.20 及以上 | 生产环境反向代理与静态资源服务（可选） |
| Elasticsearch | 7.17 至 8.5 | 全文检索增强引擎（可选，未安装时回退至 SQL 模糊匹配） |

## 文档导航

| 层面 | 目录 | 回答的问题 |
| :--- | :--- | :--- |
| 用户手册 | /docs/user-guide/ | 如何注册账号、导入链接、使用分类标签、查看健康状态？ |
| 管理员指南 | /docs/admin-guide/ | 如何配置邮件服务、调整检测频率、管理用户权限？ |
| 开发文档 | /docs/developer-guide/ | 如何扩展数据源、编写自定义标签规则、调试 API？ |
| 部署运维 | /docs/deployment/ | 如何使用 Docker Compose 一键部署、配置 HTTPS、做数据备份？ |

## 资源列表

- http://m.wap.uliejh.cn/bnews/6868152.htm
- http://m.wap.uliejh.cn/bnews/2663.htm
- http://m.wap.uliejh.cn/bnews/0930121.htm
- http://m.wap.uliejh.cn/bnews/75326.htm
- http://m.wap.uliejh.cn/bnews/1361.htm
- http://m.wap.uliejh.cn/bnews/9702558.htm
- http://m.wap.uliejh.cn/bnews/2830.htm
- http://m.wap.uliejh.cn/bnews/5834920.htm
- http://m.wap.uliejh.cn/bnews/3008165.htm
- http://m.wap.uliejh.cn/bnews/7615.htm
- http://m.wap.uliejh.cn/bnews/45202.htm
- http://m.wap.uliejh.cn/bnews/0749135.htm
- http://m.wap.uliejh.cn/bnews/533363.htm
- http://m.wap.uliejh.cn/bnews/835875.htm
- http://m.wap.uliejh.cn/bnews/7058038.htm
- http://m.wap.uliejh.cn/bnews/52943.htm
- http://m.wap.uliejh.cn/bnews/901998.htm
- http://m.wap.uliejh.cn/bnews/6685.htm
- http://m.wap.uliejh.cn/bnews/0903620.htm
- http://m.wap.uliejh.cn/bnews/652672.htm
- http://m.wap.uliejh.cn/bnews/6748.htm
- http://m.wap.uliejh.cn/bnews/0133.htm
- http://m.wap.uliejh.cn/bnews/01946.htm
- http://m.wap.uliejh.cn/bnews/110807.htm
- http://m.wap.uliejh.cn/bnews/95827.htm
- http://m.wap.uliejh.cn/bnews/95228.htm
- http://m.wap.uliejh.cn/bnews/4833.htm
- http://m.wap.uliejh.cn/bnews/3308.htm
- http://m.wap.uliejh.cn/bnews/535116.htm
- http://m.wap.uliejh.cn/bnews/3152.htm
- http://m.wap.uliejh.cn/bnews/323409.htm
- http://m.wap.uliejh.cn/bnews/0217980.htm
- http://m.wap.uliejh.cn/bnews/3849.htm
- http://m.wap.uliejh.cn/bnews/3479901.htm
- http://m.wap.uliejh.cn/bnews/10167.htm
- http://m.wap.uliejh.cn/bnews/168577.htm
- http://m.wap.uliejh.cn/bnews/71122.htm
- http://m.wap.uliejh.cn/bnews/12319.htm
- http://m.wap.uliejh.cn/bnews/9236337.htm
- http://m.wap.uliejh.cn/bnews/3220642.htm
- http://m.wap.uliejh.cn/bnews/5689908.htm
- http://m.wap.uliejh.cn/bnews/0393.htm
- http://m.wap.uliejh.cn/bnews/1278248.htm
- http://m.wap.uliejh.cn/bnews/635786.htm
- http://m.wap.uliejh.cn/bnews/8881.htm
- http://m.wap.uliejh.cn/bnews/256066.htm
- http://m.wap.uliejh.cn/bnews/42547.htm
- http://m.wap.uliejh.cn/bnews/40823.htm
- http://m.wap.uliejh.cn/bnews/285181.htm
- http://m.wap.uliejh.cn/bnews/1494.htm
- http://m.wap.uliejh.cn/bnews/5308406.htm
- http://m.wap.uliejh.cn/bnews/30967.htm
- http://m.wap.uliejh.cn/bnews/4017.htm
- http://m.wap.uliejh.cn/bnews/031236.htm
- http://m.wap.uliejh.cn/bnews/89861.htm
- http://m.wap.uliejh.cn/bnews/1884.htm
- http://m.wap.uliejh.cn/bnews/1033931.htm
- http://m.wap.uliejh.cn/bnews/754927.htm
- http://m.wap.uliejh.cn/bnews/0296.htm
- http://m.wap.uliejh.cn/bnews/45981.htm
- http://m.wap.uliejh.cn/bnews/4340.htm
- http://m.wap.uliejh.cn/bnews/976958.htm
- http://m.wap.uliejh.cn/bnews/78650.htm
- http://m.wap.uliejh.cn/bnews/9257.htm
- http://m.wap.uliejh.cn/bnews/4107.htm
- http://m.wap.uliejh.cn/bnews/7298.htm
- http://m.wap.uliejh.cn/bnews/06686.htm
- http://m.wap.uliejh.cn/bnews/711072.htm
- http://m.wap.uliejh.cn/bnews/353737.htm
- http://m.wap.uliejh.cn/bnews/57087.htm
- http://m.wap.uliejh.cn/bnews/53614.htm
- http://m.wap.uliejh.cn/bnews/196056.htm
- http://m.wap.uliejh.cn/bnews/263749.htm
- http://m.wap.uliejh.cn/bnews/83455.htm
- http://m.wap.uliejh.cn/bnews/69129.htm
- http://m.wap.uliejh.cn/bnews/2479.htm
- http://m.wap.uliejh.cn/bnews/976834.htm
- http://m.wap.uliejh.cn/bnews/4014406.htm
- http://m.wap.uliejh.cn/bnews/5578.htm
- http://m.wap.uliejh.cn/bnews/39111.htm
- http://m.wap.uliejh.cn/bnews/0548569.htm
- http://m.wap.uliejh.cn/bnews/0389.htm
- http://m.wap.uliejh.cn/bnews/15379.htm
- http://m.wap.uliejh.cn/bnews/934827.htm
- http://m.wap.uliejh.cn/bnews/37387.htm
- http://m.wap.uliejh.cn/bnews/1834.htm
- http://m.wap.uliejh.cn/bnews/1663.htm
- http://m.wap.uliejh.cn/bnews/05574.htm
- http://m.wap.uliejh.cn/bnews/85207.htm
- http://m.wap.uliejh.cn/bnews/0843850.htm
- http://m.wap.uliejh.cn/bnews/6070.htm
- http://m.wap.uliejh.cn/bnews/6236.htm
- http://m.wap.uliejh.cn/bnews/8026556.htm
- http://m.wap.uliejh.cn/bnews/77785.htm
- http://m.wap.uliejh.cn/bnews/812979.htm
- http://m.wap.uliejh.cn/bnews/06159.htm
- http://m.wap.uliejh.cn/bnews/406396.htm
- http://m.wap.uliejh.cn/bnews/756002.htm
- http://m.wap.uliejh.cn/bnews/3586.htm
- http://m.wap.uliejh.cn/bnews/23191.htm
- http://m.wap.uliejh.cn/bnews/170087.htm
- http://m.wap.uliejh.cn/bnews/697233.htm
- http://m.wap.uliejh.cn/bnews/8778.htm
- http://m.wap.uliejh.cn/bnews/461334.htm
- http://m.wap.uliejh.cn/bnews/4974.htm
- http://m.wap.uliejh.cn/bnews/65675.htm
- http://m.wap.uliejh.cn/bnews/056025.htm
- http://m.wap.uliejh.cn/bnews/5301213.htm
- http://m.wap.uliejh.cn/bnews/7088126.htm
- http://m.wap.uliejh.cn/bnews/53533.htm
- http://m.wap.uliejh.cn/bnews/8096000.htm
- http://m.wap.uliejh.cn/bnews/014732.htm
- http://m.wap.uliejh.cn/bnews/6474701.htm
- http://m.wap.uliejh.cn/bnews/669848.htm
- http://m.wap.uliejh.cn/bnews/43069.htm
- http://m.wap.uliejh.cn/bnews/2054.htm
- http://m.wap.uliejh.cn/bnews/023286.htm
- http://m.wap.uliejh.cn/bnews/06583.htm
- http://m.wap.uliejh.cn/bnews/4652.htm
- http://m.wap.uliejh.cn/bnews/2704.htm
- http://m.wap.uliejh.cn/bnews/7793036.htm
- http://m.wap.uliejh.cn/bnews/7584.htm
- http://m.wap.uliejh.cn/bnews/086553.htm
- http://m.wap.uliejh.cn/bnews/7735269.htm
- http://m.wap.uliejh.cn/bnews/8382087.htm
- http://m.wap.uliejh.cn/bnews/030111.htm
- http://m.wap.uliejh.cn/bnews/3068.htm
- http://m.wap.uliejh.cn/bnews/602126.htm
- http://m.wap.uliejh.cn/bnews/4561223.htm
- http://m.wap.uliejh.cn/bnews/0052156.htm
- http://m.wap.uliejh.cn/bnews/60487.htm
- http://m.wap.uliejh.cn/bnews/41356.htm
- http://m.wap.uliejh.cn/bnews/5813.htm
- http://m.wap.uliejh.cn/bnews/474609.htm
- http://m.wap.uliejh.cn/bnews/89005.htm
- http://m.wap.uliejh.cn/bnews/8070.htm
- http://m.wap.uliejh.cn/bnews/514200.htm
- http://m.wap.uliejh.cn/bnews/730121.htm
- http://m.wap.uliejh.cn/bnews/94531.htm
- http://m.wap.uliejh.cn/bnews/5210775.htm
- http://m.wap.uliejh.cn/bnews/155113.htm
- http://m.wap.uliejh.cn/bnews/8993.htm
- http://m.wap.uliejh.cn/bnews/7867.htm
- http://m.wap.uliejh.cn/bnews/7579713.htm
- http://m.wap.uliejh.cn/bnews/85276.htm
- http://m.wap.uliejh.cn/bnews/806435.htm
- http://m.wap.uliejh.cn/bnews/384808.htm
- http://m.wap.uliejh.cn/bnews/322850.htm
- http://m.wap.uliejh.cn/bnews/207294.htm
- http://m.wap.uliejh.cn/bnews/9934.htm
- http://m.wap.uliejh.cn/bnews/1981977.htm
- http://m.wap.uliejh.cn/bnews/663729.htm
- http://m.wap.uliejh.cn/bnews/641326.htm
- http://m.wap.uliejh.cn/bnews/105937.htm
- http://m.wap.uliejh.cn/bnews/70006.htm
- http://m.wap.uliejh.cn/bnews/86012.htm
- http://m.wap.uliejh.cn/bnews/9037986.htm
- http://m.wap.uliejh.cn/bnews/45236.htm
- http://m.wap.uliejh.cn/bnews/158758.htm
- http://m.wap.uliejh.cn/bnews/6106632.htm
- http://m.wap.uliejh.cn/bnews/3629.htm
- http://m.wap.uliejh.cn/bnews/5911.htm
- http://m.wap.uliejh.cn/bnews/9316536.htm
- http://m.wap.uliejh.cn/bnews/72088.htm
- http://m.wap.uliejh.cn/bnews/6252198.htm
- http://m.wap.uliejh.cn/bnews/2286262.htm
- http://m.wap.uliejh.cn/bnews/9082237.htm
- http://m.wap.uliejh.cn/bnews/899399.htm
- http://m.wap.uliejh.cn/bnews/256814.htm
- http://m.wap.uliejh.cn/bnews/279538.htm
- http://m.wap.uliejh.cn/bnews/6614565.htm
- http://m.wap.uliejh.cn/bnews/76145.htm
- http://m.wap.uliejh.cn/bnews/4583704.htm
- http://m.wap.uliejh.cn/bnews/802218.htm
- http://m.wap.uliejh.cn/bnews/2543.htm
- http://m.wap.uliejh.cn/bnews/51818.htm
- http://m.wap.uliejh.cn/bnews/4986445.htm
- http://m.wap.uliejh.cn/bnews/61275.htm
- http://m.wap.uliejh.cn/bnews/423012.htm
- http://m.wap.uliejh.cn/bnews/2540.htm
- http://m.wap.uliejh.cn/bnews/84814.htm
- http://m.wap.uliejh.cn/bnews/1854.htm
- http://m.wap.uliejh.cn/bnews/47464.htm
- http://m.wap.uliejh.cn/bnews/23400.htm
- http://m.wap.uliejh.cn/bnews/22170.htm
- http://m.wap.uliejh.cn/bnews/39978.htm
- http://m.wap.uliejh.cn/bnews/2810.htm
- http://m.wap.uliejh.cn/bnews/9986362.htm
- http://m.wap.uliejh.cn/bnews/2617324.htm
- http://m.wap.uliejh.cn/bnews/29839.htm
- http://m.wap.uliejh.cn/bnews/1497.htm
- http://m.wap.uliejh.cn/bnews/80698.htm
- http://m.wap.uliejh.cn/bnews/692992.htm
- http://m.wap.uliejh.cn/bnews/9928.htm
- http://m.wap.uliejh.cn/bnews/5925228.htm
- http://m.wap.uliejh.cn/bnews/6397.htm
- http://m.wap.uliejh.cn/bnews/7723.htm
- http://m.wap.uliejh.cn/bnews/3255.htm
- http://m.wap.uliejh.cn/bnews/8810.htm
- http://m.wap.uliejh.cn/bnews/999172.htm
- http://m.wap.uliejh.cn/bnews/9398470.htm
- http://m.wap.uliejh.cn/bnews/9756427.htm
- http://m.wap.uliejh.cn/bnews/4426.htm
- http://m.wap.uliejh.cn/bnews/37572.htm
- http://m.wap.uliejh.cn/bnews/067482.htm
- http://m.wap.uliejh.cn/bnews/9847.htm
- http://m.wap.uliejh.cn/bnews/3496355.htm
- http://m.wap.uliejh.cn/bnews/599954.htm
- http://m.wap.uliejh.cn/bnews/14125.htm
- http://m.wap.uliejh.cn/bnews/283944.htm
- http://m.wap.uliejh.cn/bnews/4228.htm
- http://m.wap.uliejh.cn/bnews/7007.htm
- http://m.wap.uliejh.cn/bnews/65888.htm
- http://m.wap.uliejh.cn/bnews/5144322.htm
- http://m.wap.uliejh.cn/bnews/1057429.htm
- http://m.wap.uliejh.cn/bnews/43639.htm
- http://m.wap.uliejh.cn/bnews/41881.htm
- http://m.wap.uliejh.cn/bnews/33037.htm
- http://m.wap.uliejh.cn/bnews/144302.htm
- http://m.wap.uliejh.cn/bnews/5760.htm
- http://m.wap.uliejh.cn/bnews/51553.htm
- http://m.wap.uliejh.cn/bnews/519952.htm
- http://m.wap.uliejh.cn/bnews/6791961.htm
- http://m.wap.uliejh.cn/bnews/8359349.htm
- http://m.wap.uliejh.cn/bnews/5803737.htm
- http://m.wap.uliejh.cn/bnews/87727.htm
- http://m.wap.uliejh.cn/bnews/869217.htm
- http://m.wap.uliejh.cn/bnews/511751.htm
- http://m.wap.uliejh.cn/bnews/37490.htm
- http://m.wap.uliejh.cn/bnews/347612.htm
- http://m.wap.uliejh.cn/bnews/57011.htm
- http://m.wap.uliejh.cn/bnews/532779.htm
- http://m.wap.uliejh.cn/bnews/8435131.htm
- http://m.wap.uliejh.cn/bnews/01474.htm
- http://m.wap.uliejh.cn/bnews/950375.htm
- http://m.wap.uliejh.cn/bnews/7666507.htm
- http://m.wap.uliejh.cn/bnews/322915.htm
- http://m.wap.uliejh.cn/bnews/8595134.htm
- http://m.wap.uliejh.cn/bnews/186461.htm
- http://m.wap.uliejh.cn/bnews/57274.htm
- http://m.wap.uliejh.cn/bnews/9045207.htm
- http://m.wap.uliejh.cn/bnews/31214.htm
- http://m.wap.uliejh.cn/bnews/7224.htm
- http://m.wap.uliejh.cn/bnews/882505.htm
- http://m.wap.uliejh.cn/bnews/65531.htm
- http://m.wap.uliejh.cn/bnews/47936.htm
- http://m.wap.uliejh.cn/bnews/487768.htm
- http://m.wap.uliejh.cn/bnews/6678.htm
- http://m.wap.uliejh.cn/bnews/44023.htm
- http://m.wap.uliejh.cn/bnews/4208624.htm

## 项目结构

```
weblink-navigator/
├── backend/                                  # 后端服务主目录
│   ├── api/                                  # RESTful API 路由与视图
│   │   ├── endpoints/                        # 按资源划分的端点模块
│   │   │   ├── links.py                      # 链接增删改查接口
│   │   │   ├── tags.py                       # 标签管理接口
│   │   │   └── health.py                     # 健康检查与状态上报接口
│   │   └── serializers/                      # 数据序列化与校验逻辑
│   ├── core/                                 # 核心业务逻辑层
│   │   ├── checker.py                       # 异步链接状态检测引擎
│   │   ├── importer.py                      # 批量导入与格式转换器
│   │   └── stats.py                         # 访问统计与热度计算
│   ├── models/                               # 数据库模型定义
│   │   ├── link.py                          # 链接主表模型
│   │   ├── tag.py                           # 标签表模型
│   │   └── user.py                          # 用户与权限模型
│   ├── tasks/                                # 分布式任务队列（Celery）
│   │   ├── periodic.py                      # 定时任务定义（如每日检测）
│   │   └── workers.py                       # 任务执行器注册
│   └── utils/                                # 通用工具函数集
│       ├── http.py                          # 增强型 HTTP 请求客户端
│       └── validators.py                    # URL 校验与清洗工具
├── frontend/                                 # 前端单页应用（React）
│   ├── src/
│   │   ├── components/                      # 可复用 UI 组件
│   │   │   ├── LinkTable.jsx               # 链接列表与排序表格
│   │   │   ├── TagFilter.jsx               # 标签筛选器面板
│   │   │   └── StatusBadge.jsx             # 链接状态图标组件
│   │   ├── pages/                           # 路由页面级组件
│   │   │   ├── Dashboard.jsx               # 总览面板
│   │   │   ├── ImportPage.jsx              # 批量导入页面
│   │   │   └── SettingsPage.jsx            # 用户设置页面
│   │   ├── hooks/                           # 自定义 React Hooks
│   │   │   ├── useLinks.js                 # 链接数据获取与缓存
│   │   │   └── useFilter.js                # 筛选状态管理
│   │   └── store/                           # 全局状态管理（Redux Toolkit）
│   └── public/                               # 静态资源入口
├── docker-compose.yml                        # 生产环境容器编排文件
├── Dockerfile.backend                        # 后端服务镜像构建脚本
├── Dockerfile.frontend                       # 前端构建镜像脚本
├── requirements.txt                          # Python 依赖清单
├── package.json                              # Node.js 依赖清单
├── nginx.conf                                # Nginx 反向代理配置模板
└── README.md                                 # 本文档
```

## 贡献指南

我们欢迎并鼓励社区贡献者参与 WebLink Navigator 的开发与改进。请遵循以下流程提交贡献。

1. 阅读项目行为准则与贡献者许可协议，确认您的提交将采用 MIT 许可证发布。所有贡献需附带清晰的提交说明，并确保代码通过现有测试用例。

2. 在 GitHub Issues 中查找标记为 "help wanted" 或 "good first issue" 的任务，或自行提交新功能提案并等待维护者确认。重大变更建议先创建讨论议题，避免无效开发。

3. 派生项目仓库至个人账号，在本地新建功能分支，分支命名遵循 `feature/功能简述` 或 `fix/问题简述` 格式。开发过程中请保持与主分支的同步。

4. 完成代码编写后，确保执行 `black` 与 `eslint` 进行代码格式化，并编写或更新对应的单元测试。提交前运行完整的测试套件，保证所有测试通过。

5. 发起合并请求至主仓库的 `develop` 分支，请求描述需清晰说明变更内容、影响范围及测试情况。至少两位维护者审阅通过后，合并至主分支并随下一版本发布。

## 常见问题

问：WebLink Navigator 是否提供在线演示环境？

答：项目未部署公开的持续演示实例，因外部链接状态动态变化且涉及用户数据隔离。您可依据快速开始章节在本地部署完整环境，所有功能均可正常体验。如需云环境测试，建议使用 Docker Compose 一键部署至个人服务器。

问：链接健康检查的频率和超时时间可否调整？

答：可以。健康检查的周期、并发数以及单次超时阈值均可在 `backend/core/checker.py` 的配置类中修改，或通过环境变量 `CHECK_INTERVAL`、`CHECK_TIMEOUT` 和 `CHECK_CONCURRENCY` 在启动时覆盖。默认周期为 6 小时，超时 10 秒，并发 20 条。

问：如何从旧版链接收藏工具迁移数据？

答：项目提供 `importer.py` 命令行工具，支持从 CSV（列顺序可配置）、JSON（键值映射）及部分流行书签管理工具的 HTML 导出格式进行转换。具体用法请参阅 `python manage.py import --help`。若您的数据格式未在支持列表中，可提交格式样本至 Issues，我们会评估添加支持的可能性。

## 许可证

MIT

> 外链数量: 250 | 生成时间: 2026-08-24 23:40:21
