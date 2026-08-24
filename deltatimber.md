# WebIndex 聚合导航系统

WebIndex 是一个面向技术内容聚合与外部资源导航的开源系统，定位于为开发者、技术博主以及信息整理者提供一套轻量级、可自托管的链接聚合与管理平台。该系统以 URL 资源池为核心，支持对大量外部分布式内容进行结构化收录、分类索引以及快速检索，适用于需要长期维护大量参考链接、新闻条目或文档资源的技术团队或个人知识库场景。

WebIndex 并非传统意义上的内容采集器，而是一个以元数据整理和导航为核心的外链汇总站。它不存储原始页面内容，仅对 URL 进行规范化记录、标签化分类以及状态监控，帮助用户从冗杂的浏览器收藏夹中脱离，建立一套可公开或内部分享的导航体系。项目默认兼容移动端访问，开箱即用，适合部署在低成本的虚拟主机或容器环境中。

## 功能概览

批量链接收录：支持通过文本导入、API 单条提交以及批量文件上传三种方式将外部 URL 纳入系统，自动解析域名并提取基础元信息。

分类与标签引擎：允许用户为每条链接自定义多个标签和分类层级，支持模糊匹配与多标签交集筛选，便于快速定位特定主题下的资源集合。

链接状态巡检：内置定时任务，可对已收录的 URL 进行可达性检测和响应时间记录，自动标记失效或响应超时的链接，辅助用户清理或更新资源。

全文检索与过滤：基于标题关键字、URL 片段、标签组合以及收录时间范围进行复合条件检索，检索结果支持按相关性、响应速度或添加时间排序。

数据导入导出：支持 CSV、JSON 以及 Markdown 列表格式的链接批量导入与导出，方便与其他知识管理工具（如 Notion、Obsidian）进行数据交换。

公开导航页生成：提供可配置的静态导航页模板，用户可选择将部分标签下的链接生成独立的公开页面，用于团队分享或个人站点外链模块。

用户分级权限：支持多用户体系，区分管理员、编辑者和只读访客三种角色，管理员可控制每条链接的可见范围和编辑权限。

访问统计看板：基于轻量级日志记录，展示整体链接数量、分类分布、每日新增趋势以及高频访问标签的排行榜。

## 应用场景

技术团队内部文档聚合：开发团队可将日常使用的 API 文档、设计规范、部署手册以及第三方服务控制台等链接统一录入 WebIndex，按项目或技术栈打标，新成员入职时可快速获取所有必要的外部资源入口。

个人知识库外链管理：博客作者或笔记重度用户可将长期积累的参考文章、数据来源、工具站点等链接从浏览器收藏夹迁移至 WebIndex，通过标签和全文检索实现高效回找，避免收藏夹堆积导致的资源沉没。

开源项目外部资源导航站：开源项目维护者可将周边生态工具、社区论坛、视频教程以及相关论文等外链整理为公开导航页，随项目文档一同发布，降低社区用户的学习成本和信息寻找门槛。

内容聚合与新闻监控：运营人员可将每日浏览到的行业新闻、政策文件、竞品动态等链接快速收录，并利用状态巡检功能定期检查链接有效性，为周报或月报整理提供可靠素材池。

## 快速开始

以下步骤适用于 Linux 或 macOS 开发环境，Windows 用户建议通过 WSL 或 Git Bash 执行。

```bash
# 克隆代码仓库
git clone https://github.com/webindex/webindex.git
cd webindex

# 安装项目依赖（使用 pip 虚拟环境）
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt

# 初始化数据库表结构
python manage.py migrate

# 创建管理员账户（交互式输入）
python manage.py createsuperuser

# 启动开发服务器
python manage.py runserver 0.0.0.0:8000
```

启动后访问 http://localhost:8000 即可进入系统首页。管理员后台入口为 /admin，用于执行批量导入、标签管理和用户权限配置等高级操作。

## 安装要求

| 依赖组件 | 最低版本要求 | 说明 |
|---------|------------|------|
| Python | 3.9 | 核心运行环境，建议使用 3.10 以上版本以获得更好的性能 |
| Django | 4.2 | Web 框架，用于处理路由、ORM 以及管理后台 |
| SQLite | 3.31 | 默认嵌入式数据库，适合小规模部署；生产环境可切换至 PostgreSQL |
| Redis | 6.0 | 用于缓存和会话存储，非必需但强烈建议启用以提升检索性能 |
| Celery | 5.3 | 异步任务队列，用于执行链接状态巡检和定时统计任务 |
| Node.js | 18.0 | 仅用于前端资源构建，如不修改静态文件可不安装 |
| Nginx | 1.22 | 生产环境推荐的反向代理服务器，用于托管静态文件和负载均衡 |
| Supervisor | 4.2 | 进程守护工具，用于保持 Celery 和 Django 服务在后台持续运行 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|------|------|----------|
| 用户手册 | /docs/user-guide/ | 如何添加链接、如何创建分类与标签、如何生成公开导航页 |
| 管理员指南 | /docs/admin-guide/ | 如何配置状态巡检频率、如何管理用户权限、如何执行数据备份与恢复 |
| 开发文档 | /docs/developer/ | 如何扩展自定义标签解析器、如何接入外部 OAuth 认证、如何修改前端导航模板 |
| API 参考 | /docs/api/ | 所有 RESTful 接口的请求参数、响应格式以及鉴权方式说明 |
| 部署运维 | /docs/deployment/ | 如何使用 Docker Compose 进行一键部署、如何配置 HTTPS 证书、如何调整数据库连接池 |

## 资源列表

- http://m.wap.uliejh.cn/bnews/23866.htm
- http://m.wap.uliejh.cn/bnews/62719.htm
- http://m.wap.uliejh.cn/bnews/783117.htm
- http://m.wap.uliejh.cn/bnews/81477.htm
- http://m.wap.uliejh.cn/bnews/48757.htm
- http://m.wap.uliejh.cn/bnews/3684.htm
- http://m.wap.uliejh.cn/bnews/4759.htm
- http://m.wap.uliejh.cn/bnews/02985.htm
- http://m.wap.uliejh.cn/bnews/5943.htm
- http://m.wap.uliejh.cn/bnews/014218.htm
- http://m.wap.uliejh.cn/bnews/68533.htm
- http://m.wap.uliejh.cn/bnews/244170.htm
- http://m.wap.uliejh.cn/bnews/5011.htm
- http://m.wap.uliejh.cn/bnews/4221.htm
- http://m.wap.uliejh.cn/bnews/06690.htm
- http://m.wap.uliejh.cn/bnews/6216.htm
- http://m.wap.uliejh.cn/bnews/2339.htm
- http://m.wap.uliejh.cn/bnews/74521.htm
- http://m.wap.uliejh.cn/bnews/12806.htm
- http://m.wap.uliejh.cn/bnews/1774023.htm
- http://m.wap.uliejh.cn/bnews/49019.htm
- http://m.wap.uliejh.cn/bnews/1844190.htm
- http://m.wap.uliejh.cn/bnews/3925.htm
- http://m.wap.uliejh.cn/bnews/820701.htm
- http://m.wap.uliejh.cn/bnews/1015.htm
- http://m.wap.uliejh.cn/bnews/082900.htm
- http://m.wap.uliejh.cn/bnews/4920025.htm
- http://m.wap.uliejh.cn/bnews/06927.htm
- http://m.wap.uliejh.cn/bnews/44008.htm
- http://m.wap.uliejh.cn/bnews/4719541.htm
- http://m.wap.uliejh.cn/bnews/22136.htm
- http://m.wap.uliejh.cn/bnews/62823.htm
- http://m.wap.uliejh.cn/bnews/1575670.htm
- http://m.wap.uliejh.cn/bnews/0501.htm
- http://m.wap.uliejh.cn/bnews/23662.htm
- http://m.wap.uliejh.cn/bnews/665302.htm
- http://m.wap.uliejh.cn/bnews/397325.htm
- http://m.wap.uliejh.cn/bnews/07354.htm
- http://m.wap.uliejh.cn/bnews/35378.htm
- http://m.wap.uliejh.cn/bnews/6705.htm
- http://m.wap.uliejh.cn/bnews/85448.htm
- http://m.wap.uliejh.cn/bnews/34950.htm
- http://m.wap.uliejh.cn/bnews/27120.htm
- http://m.wap.uliejh.cn/bnews/0456887.htm
- http://m.wap.uliejh.cn/bnews/55514.htm
- http://m.wap.uliejh.cn/bnews/71024.htm
- http://m.wap.uliejh.cn/bnews/500871.htm
- http://m.wap.uliejh.cn/bnews/1605.htm
- http://m.wap.uliejh.cn/bnews/7632993.htm
- http://m.wap.uliejh.cn/bnews/58031.htm
- http://m.wap.uliejh.cn/bnews/2714.htm
- http://m.wap.uliejh.cn/bnews/0181485.htm
- http://m.wap.uliejh.cn/bnews/28555.htm
- http://m.wap.uliejh.cn/bnews/4025367.htm
- http://m.wap.uliejh.cn/bnews/5805.htm
- http://m.wap.uliejh.cn/bnews/3409.htm
- http://m.wap.uliejh.cn/bnews/3402.htm
- http://m.wap.uliejh.cn/bnews/9630.htm
- http://m.wap.uliejh.cn/bnews/0949.htm
- http://m.wap.uliejh.cn/bnews/324683.htm
- http://m.wap.uliejh.cn/bnews/2958.htm
- http://m.wap.uliejh.cn/bnews/54393.htm
- http://m.wap.uliejh.cn/bnews/7785437.htm
- http://m.wap.uliejh.cn/bnews/14751.htm
- http://m.wap.uliejh.cn/bnews/8535657.htm
- http://m.wap.uliejh.cn/bnews/1886.htm
- http://m.wap.uliejh.cn/bnews/1633.htm
- http://m.wap.uliejh.cn/bnews/8924.htm
- http://m.wap.uliejh.cn/bnews/215658.htm
- http://m.wap.uliejh.cn/bnews/8026.htm
- http://m.wap.uliejh.cn/bnews/56623.htm
- http://m.wap.uliejh.cn/bnews/03553.htm
- http://m.wap.uliejh.cn/bnews/9000.htm
- http://m.wap.uliejh.cn/bnews/845616.htm
- http://m.wap.uliejh.cn/bnews/12799.htm
- http://m.wap.uliejh.cn/bnews/527423.htm
- http://m.wap.uliejh.cn/bnews/876978.htm
- http://m.wap.uliejh.cn/bnews/42344.htm
- http://m.wap.uliejh.cn/bnews/700543.htm
- http://m.wap.uliejh.cn/bnews/2993.htm
- http://m.wap.uliejh.cn/bnews/1242.htm
- http://m.wap.uliejh.cn/bnews/72139.htm
- http://m.wap.uliejh.cn/bnews/9722.htm
- http://m.wap.uliejh.cn/bnews/4478.htm
- http://m.wap.uliejh.cn/bnews/6747292.htm
- http://m.wap.uliejh.cn/bnews/64978.htm
- http://m.wap.uliejh.cn/bnews/4391.htm
- http://m.wap.uliejh.cn/bnews/13350.htm
- http://m.wap.uliejh.cn/bnews/801410.htm
- http://m.wap.uliejh.cn/bnews/460854.htm
- http://m.wap.uliejh.cn/bnews/3705736.htm
- http://m.wap.uliejh.cn/bnews/736956.htm
- http://m.wap.uliejh.cn/bnews/777645.htm
- http://m.wap.uliejh.cn/bnews/69259.htm
- http://m.wap.uliejh.cn/bnews/1363.htm
- http://m.wap.uliejh.cn/bnews/657073.htm
- http://m.wap.uliejh.cn/bnews/0117134.htm
- http://m.wap.uliejh.cn/bnews/757083.htm
- http://m.wap.uliejh.cn/bnews/06093.htm
- http://m.wap.uliejh.cn/bnews/9868355.htm
- http://m.wap.uliejh.cn/bnews/1492.htm
- http://m.wap.uliejh.cn/bnews/5488.htm
- http://m.wap.uliejh.cn/bnews/51723.htm
- http://m.wap.uliejh.cn/bnews/9753250.htm
- http://m.wap.uliejh.cn/bnews/8844.htm
- http://m.wap.uliejh.cn/bnews/3794081.htm
- http://m.wap.uliejh.cn/bnews/051383.htm
- http://m.wap.uliejh.cn/bnews/79335.htm
- http://m.wap.uliejh.cn/bnews/328890.htm
- http://m.wap.uliejh.cn/bnews/66538.htm
- http://m.wap.uliejh.cn/bnews/8704599.htm
- http://m.wap.uliejh.cn/bnews/78212.htm
- http://m.wap.uliejh.cn/bnews/9553210.htm
- http://m.wap.uliejh.cn/bnews/132569.htm
- http://m.wap.uliejh.cn/bnews/994683.htm
- http://m.wap.uliejh.cn/bnews/10186.htm
- http://m.wap.uliejh.cn/bnews/06818.htm
- http://m.wap.uliejh.cn/bnews/1487729.htm
- http://m.wap.uliejh.cn/bnews/52036.htm
- http://m.wap.uliejh.cn/bnews/2780146.htm
- http://m.wap.uliejh.cn/bnews/6586197.htm
- http://m.wap.uliejh.cn/bnews/4108669.htm
- http://m.wap.uliejh.cn/bnews/5610.htm
- http://m.wap.uliejh.cn/bnews/3964632.htm
- http://m.wap.uliejh.cn/bnews/432095.htm
- http://m.wap.uliejh.cn/bnews/511629.htm
- http://m.wap.uliejh.cn/bnews/39069.htm
- http://m.wap.uliejh.cn/bnews/075403.htm
- http://m.wap.uliejh.cn/bnews/6465899.htm
- http://m.wap.uliejh.cn/bnews/2779390.htm
- http://m.wap.uliejh.cn/bnews/889636.htm
- http://m.wap.uliejh.cn/bnews/7083.htm
- http://m.wap.uliejh.cn/bnews/7814.htm
- http://m.wap.uliejh.cn/bnews/1585101.htm
- http://m.wap.uliejh.cn/bnews/18952.htm
- http://m.wap.uliejh.cn/bnews/6679.htm
- http://m.wap.uliejh.cn/bnews/80369.htm
- http://m.wap.uliejh.cn/bnews/818715.htm
- http://m.wap.uliejh.cn/bnews/218172.htm
- http://m.wap.uliejh.cn/bnews/0481.htm
- http://m.wap.uliejh.cn/bnews/43559.htm
- http://m.wap.uliejh.cn/bnews/168531.htm
- http://m.wap.uliejh.cn/bnews/507490.htm
- http://m.wap.uliejh.cn/bnews/229902.htm
- http://m.wap.uliejh.cn/bnews/5139.htm
- http://m.wap.uliejh.cn/bnews/9615662.htm
- http://m.wap.uliejh.cn/bnews/06500.htm
- http://m.wap.uliejh.cn/bnews/1295.htm
- http://m.wap.uliejh.cn/bnews/832779.htm
- http://m.wap.uliejh.cn/bnews/716533.htm
- http://m.wap.uliejh.cn/bnews/7585868.htm
- http://m.wap.uliejh.cn/bnews/4326.htm
- http://m.wap.uliejh.cn/bnews/03939.htm
- http://m.wap.uliejh.cn/bnews/9951956.htm
- http://m.wap.uliejh.cn/bnews/74264.htm
- http://m.wap.uliejh.cn/bnews/8722.htm
- http://m.wap.uliejh.cn/bnews/18614.htm
- http://m.wap.uliejh.cn/bnews/73899.htm
- http://m.wap.uliejh.cn/bnews/387530.htm
- http://m.wap.uliejh.cn/bnews/5712.htm
- http://m.wap.uliejh.cn/bnews/05979.htm
- http://m.wap.uliejh.cn/bnews/70897.htm
- http://m.wap.uliejh.cn/bnews/38568.htm
- http://m.wap.uliejh.cn/bnews/603133.htm
- http://m.wap.uliejh.cn/bnews/05598.htm
- http://m.wap.uliejh.cn/bnews/305956.htm
- http://m.wap.uliejh.cn/bnews/0997862.htm
- http://m.wap.uliejh.cn/bnews/976238.htm
- http://m.wap.uliejh.cn/bnews/68607.htm
- http://m.wap.uliejh.cn/bnews/5886.htm
- http://m.wap.uliejh.cn/bnews/3675.htm
- http://m.wap.uliejh.cn/bnews/10545.htm
- http://m.wap.uliejh.cn/bnews/7689886.htm
- http://m.wap.uliejh.cn/bnews/221453.htm
- http://m.wap.uliejh.cn/bnews/805780.htm
- http://m.wap.uliejh.cn/bnews/7669.htm
- http://m.wap.uliejh.cn/bnews/156668.htm
- http://m.wap.uliejh.cn/bnews/21637.htm
- http://m.wap.uliejh.cn/bnews/203952.htm
- http://m.wap.uliejh.cn/bnews/915483.htm
- http://m.wap.uliejh.cn/bnews/140640.htm
- http://m.wap.uliejh.cn/bnews/4043.htm
- http://m.wap.uliejh.cn/bnews/1998544.htm
- http://m.wap.uliejh.cn/bnews/6937294.htm
- http://m.wap.uliejh.cn/bnews/9933387.htm
- http://m.wap.uliejh.cn/bnews/96409.htm
- http://m.wap.uliejh.cn/bnews/225829.htm
- http://m.wap.uliejh.cn/bnews/2900.htm
- http://m.wap.uliejh.cn/bnews/6179828.htm
- http://m.wap.uliejh.cn/bnews/6285776.htm
- http://m.wap.uliejh.cn/bnews/3460.htm
- http://m.wap.uliejh.cn/bnews/96173.htm
- http://m.wap.uliejh.cn/bnews/3635137.htm
- http://m.wap.uliejh.cn/bnews/04395.htm
- http://m.wap.uliejh.cn/bnews/7676225.htm
- http://m.wap.uliejh.cn/bnews/7272.htm
- http://m.wap.uliejh.cn/bnews/3574863.htm
- http://m.wap.uliejh.cn/bnews/2507094.htm
- http://m.wap.uliejh.cn/bnews/2754.htm
- http://m.wap.uliejh.cn/bnews/3123.htm
- http://m.wap.uliejh.cn/bnews/23352.htm
- http://m.wap.uliejh.cn/bnews/0911.htm
- http://m.wap.uliejh.cn/bnews/5054940.htm
- http://m.wap.uliejh.cn/bnews/26080.htm
- http://m.wap.uliejh.cn/bnews/954686.htm
- http://m.wap.uliejh.cn/bnews/0457.htm
- http://m.wap.uliejh.cn/bnews/8805642.htm
- http://m.wap.uliejh.cn/bnews/5869366.htm
- http://m.wap.uliejh.cn/bnews/05015.htm
- http://m.wap.uliejh.cn/bnews/18467.htm
- http://m.wap.uliejh.cn/bnews/1137.htm
- http://m.wap.uliejh.cn/bnews/4269972.htm
- http://m.wap.uliejh.cn/bnews/6190084.htm
- http://m.wap.uliejh.cn/bnews/804353.htm
- http://m.wap.uliejh.cn/bnews/171123.htm
- http://m.wap.uliejh.cn/bnews/847767.htm
- http://m.wap.uliejh.cn/bnews/32096.htm
- http://m.wap.uliejh.cn/bnews/7897.htm
- http://m.wap.uliejh.cn/bnews/2422793.htm
- http://m.wap.uliejh.cn/bnews/6169446.htm
- http://m.wap.uliejh.cn/bnews/80420.htm
- http://m.wap.uliejh.cn/bnews/6651.htm
- http://m.wap.uliejh.cn/bnews/8691.htm
- http://m.wap.uliejh.cn/bnews/0100.htm
- http://m.wap.uliejh.cn/bnews/57192.htm
- http://m.wap.uliejh.cn/bnews/68900.htm
- http://m.wap.uliejh.cn/bnews/21110.htm
- http://m.wap.uliejh.cn/bnews/1147.htm
- http://m.wap.uliejh.cn/bnews/5048.htm
- http://m.wap.uliejh.cn/bnews/88755.htm
- http://m.wap.uliejh.cn/bnews/09484.htm
- http://m.wap.uliejh.cn/bnews/27965.htm
- http://m.wap.uliejh.cn/bnews/329123.htm
- http://m.wap.uliejh.cn/bnews/587386.htm
- http://m.wap.uliejh.cn/bnews/50375.htm
- http://m.wap.uliejh.cn/bnews/605082.htm
- http://m.wap.uliejh.cn/bnews/1993.htm
- http://m.wap.uliejh.cn/bnews/7821293.htm
- http://m.wap.uliejh.cn/bnews/5217.htm
- http://m.wap.uliejh.cn/bnews/30114.htm
- http://m.wap.uliejh.cn/bnews/50543.htm
- http://m.wap.uliejh.cn/bnews/15151.htm
- http://m.wap.uliejh.cn/bnews/42704.htm
- http://m.wap.uliejh.cn/bnews/7499550.htm
- http://m.wap.uliejh.cn/bnews/4264516.htm
- http://m.wap.uliejh.cn/bnews/580701.htm
- http://m.wap.uliejh.cn/bnews/456477.htm
- http://m.wap.uliejh.cn/bnews/7141852.htm
- http://m.wap.uliejh.cn/bnews/5220883.htm
- http://m.wap.uliejh.cn/bnews/1076.htm

## 项目结构

```
webindex/
├── manage.py                     # Django 项目入口脚本，用于启动服务、执行迁移和创建用户
├── requirements.txt              # Python 依赖清单，包含 Django、Celery、Redis 等核心库
├── config/                       # 项目全局配置目录
│   ├── settings.py              # 基础配置，含数据库、时区、静态文件、中间件等
│   ├── settings_prod.py         # 生产环境覆盖配置，用于开启缓存、日志和调试开关
│   └── urls.py                  # 根路由映射，包含 admin、api 和前端页面路由
├── apps/                         # 所有自定义应用模块
│   ├── links/                   # 链接管理核心模块，处理收录、标签、检索与状态巡检
│   │   ├── models.py            # Link、Tag、Category 等数据模型定义
│   │   ├── views.py             # 链接列表、详情、导入导出及 API 视图函数
│   │   └── tasks.py             # Celery 异步任务，包括链接可达性检测和统计更新
│   ├── users/                   # 用户与权限管理模块，扩展 Django 默认用户模型
│   │   ├── models.py            # 用户 Profile、操作日志及邀请码模型
│   │   └── backends.py          # 自定义邮箱登录认证后端
│   └── pages/                   # 公开导航页生成模块，负责静态模板渲染和缓存
│       ├── generators.py        # 导航页 HTML 生成器，支持多种布局主题
│       └── filters.py           # 标签过滤与排序逻辑，用于公开页面的动态筛选
├── static/                       # 静态资源目录（CSS、JavaScript、图片）
│   ├── css/
│   │   └── style.css            # 主样式表，基于 Flexbox 和 Grid 实现响应式布局
│   └── js/
│       └── app.js               # 前端交互逻辑，包括标签自动补全和批量选择操作
├── templates/                    # Django 模板文件目录
│   ├── base.html                # 基础模板，定义导航栏、页脚和全局消息块
│   ├── link_list.html           # 链接列表页模板，支持分页和筛选条件展示
│   └── public_nav.html          # 公开导航页模板，独立于后台登录状态
├── scripts/                      # 运维和辅助脚本
│   ├── batch_import.py          # 命令行批量导入工具，支持 CSV 和 JSON 格式
│   └── health_check.sh          # 系统健康检查脚本，用于监控 Celery 和数据库状态
├── logs/                         # 日志文件存储目录（默认按日期轮转）
│   ├── webindex.log             # 应用主日志，记录请求、错误和关键操作
│   └── celery.log               # Celery 任务执行日志，记录巡检结果和异常堆栈
└── docker-compose.yml           # Docker Compose 编排文件，快速启动全套服务栈
```

## 贡献指南

我们欢迎任何形式的贡献，包括但不限于代码提交、文档改进、问题报告和功能建议。请遵循以下步骤参与项目开发：

首先，在 GitHub 上 Fork 本仓库，并将 Fork 后的仓库克隆到本地开发环境。建议在 dev 分支上进行所有修改，避免直接操作 main 分支。

其次，运行项目自带的测试套件以确保现有功能未被破坏。测试用例位于各 apps 目录下的 tests.py 文件中，执行 python manage.py test 即可启动全部单元测试和集成测试。

第三，若您计划新增功能或修复缺陷，请先查阅 issues 列表确认是否已有相关讨论。对于较大规模的功能改动，建议先创建一个 issue 描述您的设计方案，以便核心维护者给出反馈。

第四，提交代码时请遵循 PEP 8 编码规范，并确保所有新增的 API 接口或后台任务包含完整的文档字符串。提交信息请使用简洁的英文祈使句，例如 "Add batch import progress bar" 或 "Fix link status check timeout"。

最后，提交 Pull Request 时请将目标分支设置为 main，并在 PR 描述中清晰说明改动内容、测试覆盖情况以及是否涉及数据库迁移或配置变更。PR 合并前需要至少一位核心维护者进行 Code Review。

## 常见问题

Q: 系统可以处理多少条链接？是否有性能瓶颈？

A: 系统本身对链接数量没有硬性限制，实际承载能力取决于部署环境的数据库和缓存配置。在默认 SQLite 配置下，建议单实例管理不超过 5 万条链接，此时检索和标签过滤响应时间在 200ms 以内。若需要管理更大规模的资源池，推荐切换至 PostgreSQL 并启用 Redis 缓存，实测可支撑 50 万条级别链接的日常使用。状态巡检任务的并发数可通过 Celery 的 concurrency 参数调节，避免对目标站点造成过大压力。

Q: 如何将现有的浏览器书签批量导入系统？

A: 推荐使用浏览器自带的书签导出功能，将书签保存为 HTML 文件或 CSV 格式，然后通过系统后台的「批量导入」功能上传文件。系统会自动解析书签名称、URL 以及文件夹层级，将文件夹名称映射为标签。对于 Chrome 和 Firefox 浏览器，也可以安装官方提供的导入插件，实现一键同步。若书签数量超过 1000 条，建议通过命令行脚本 scripts/batch_import.py 进行异步导入，避免 Web 请求超时。

Q: 公开导航页是否支持自定义样式和域名？

A: 支持。公开导航页基于 Django 模板系统实现，您可以直接修改 templates/public_nav.html 和静态样式文件 static/css/style.css 来定制外观。若希望绑定独立域名（例如 nav.example.com），可在 Nginx 配置中设置反向代理规则，将特定域名的请求转发至 WebIndex 服务的 /public 路径下，并在系统设置中配置公开页面的基础 URL，以确保分页和分享链接正确生成。

## 许可证

MIT

> 外链数量: 250 | 生成时间: 2026-08-24 23:40:21
