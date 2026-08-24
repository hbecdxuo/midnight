# NewsLink Archive

NewsLink Archive 是一个面向技术内容聚合与长期外链资源管理的轻量化归档系统。本项目定位于为开发者、内容研究者与信息分析人员提供一套可自部署的 URL 资源汇总与导航框架，解决分散链接难以集中管理、检索与状态监控的痛点。系统以静态站点或轻量后端服务的形式运行，对原始链接进行结构化存储、标签化分类与可用性探测，适用于需要维护大量外部参考链接的技术文档库、研究笔记或开源项目资源站。

本项目不依赖商业云服务，所有数据存储于本地或对象存储，支持导出为标准 Markdown 或 JSON 格式，便于集成至现有文档工作流。

## 功能概览

- 批量链接导入与去重：支持从文本文件或 CSV 批量导入 URL，自动识别重复条目并合并标签。
- 自定义分类与标签体系：允许用户创建多级分类目录，为每条链接附加多个标签，支持按分类或标签筛选视图。
- 链接可用性定时检测：内置调度任务，可配置检测周期（如每日、每周），对每条链接发起 HEAD 请求并记录状态码与响应时间。
- 全文检索与过滤：基于标题、描述、标签、分类进行关键词检索，支持正则表达式与通配符模式匹配。
- 数据导出为多种格式：支持将整个归档或筛选结果导出为标准 Markdown 列表、JSON 数组或 CSV 表格，便于迁移或发布。
- 静态站点生成模式：内置模板引擎，可将归档数据生成为静态 HTML 站点，直接托管于 GitHub Pages 或任何 Web 服务器。
- 访问统计与点击跟踪：可选记录每个链接的点击次数与最后访问时间，生成简单热度排行。

## 应用场景

1. 技术团队内部知识库维护：团队可将日常调研中发现的优秀技术文章、工具仓库、官方文档链接统一收录，按项目或技术领域分类，并定期检测链接有效性，避免知识库中出现大量死链。

2. 开源项目外链资源页托管：开源项目维护者可使用本项目生成项目官网的“相关资源”或“生态链接”页面，自动从归档数据渲染为静态 HTML，无需手动编写 HTML 列表。

3. 个人研究者文献与资料管理：研究人员可将数百篇论文链接、数据源地址、官方 API 文档集中管理，利用标签体系按主题、年份或重要程度组织，并导出为 Markdown 笔记。

4. 信息监控与变化追踪：结合可用性检测与历史状态记录，可监控某些关键接口文档或服务状态页的在线情况，当链接返回非 200 状态时触发告警通知。

5. 构建导航站点的数据中台：作为导航类网站的后台数据管理模块，提供链接增删改查与分类管理 API，前端可独立调用渲染。

## 快速开始

以下步骤适用于 Linux / macOS / Windows WSL 环境。

```bash
# 克隆仓库
git clone https://github.com/your-org/newslink-archive.git
cd newslink-archive

# 安装依赖（使用 Python 虚拟环境）
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt

# 初始化数据库与配置文件
cp .env.example .env
python scripts/init_db.py

# 启动开发服务器（默认监听 127.0.0.1:5000）
python app.py
```

访问 http://127.0.0.1:5000 即可进入管理界面。首次启动将自动创建管理员账户，默认用户名 `admin`，密码请查看启动日志中的临时生成密码。

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|---------|---------|------|
| Python | 3.8 或更高 | 核心运行环境，推荐使用 3.10 以上 |
| SQLite | 3.28 或更高 | 默认数据库引擎，无需额外安装 |
| Redis | 6.0 或更高 | 可选，用于缓存与任务队列（不启用则使用内存队列） |
| Node.js | 16.x 或更高 | 仅静态站点生成模式需要，用于前端打包 |
| Git | 2.20 或更高 | 用于版本管理与更新拉取 |
| 系统内存 | 512 MB 以上 | 建议 1 GB 以上以支持较大归档 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|------|------|-----------|
| 用户手册 | /docs/user-guide/ | 如何导入链接、如何创建分类、如何配置检测计划 |
| 部署指南 | /docs/deployment/ | 如何将其部署到生产服务器、使用 Nginx 反向代理、配置 SSL |
| API 参考 | /docs/api/ | 提供了哪些 RESTful 接口、请求参数与返回格式、鉴权方式 |
| 开发者指南 | /docs/developer/ | 插件扩展机制、自定义检测器编写、数据模型与迁移说明 |

## 资源列表

- http://m.3g.uliejh.cn/nnews/9603.htm
- http://m.3g.uliejh.cn/nnews/2175286.htm
- http://m.3g.uliejh.cn/nnews/801191.htm
- http://m.3g.uliejh.cn/nnews/816959.htm
- http://m.3g.uliejh.cn/nnews/96084.htm
- http://m.3g.uliejh.cn/nnews/6676927.htm
- http://m.3g.uliejh.cn/nnews/093187.htm
- http://m.3g.uliejh.cn/nnews/65707.htm
- http://m.3g.uliejh.cn/nnews/93760.htm
- http://m.3g.uliejh.cn/nnews/7161.htm
- http://m.3g.uliejh.cn/nnews/6089.htm
- http://m.3g.uliejh.cn/nnews/0938.htm
- http://m.3g.uliejh.cn/nnews/6804583.htm
- http://m.3g.uliejh.cn/nnews/091489.htm
- http://m.3g.uliejh.cn/nnews/858640.htm
- http://m.3g.uliejh.cn/nnews/5515632.htm
- http://m.3g.uliejh.cn/nnews/980332.htm
- http://m.3g.uliejh.cn/nnews/675050.htm
- http://m.3g.uliejh.cn/nnews/8105.htm
- http://m.3g.uliejh.cn/nnews/558080.htm
- http://m.3g.uliejh.cn/nnews/424641.htm
- http://m.3g.uliejh.cn/nnews/7120.htm
- http://m.3g.uliejh.cn/nnews/426580.htm
- http://m.3g.uliejh.cn/nnews/1645.htm
- http://m.3g.uliejh.cn/nnews/6112897.htm
- http://m.3g.uliejh.cn/nnews/41502.htm
- http://m.3g.uliejh.cn/nnews/3436342.htm
- http://m.3g.uliejh.cn/nnews/149339.htm
- http://m.3g.uliejh.cn/nnews/09649.htm
- http://m.3g.uliejh.cn/nnews/723041.htm
- http://m.3g.uliejh.cn/nnews/55252.htm
- http://m.3g.uliejh.cn/nnews/0350.htm
- http://m.3g.uliejh.cn/nnews/2376.htm
- http://m.3g.uliejh.cn/nnews/08152.htm
- http://m.3g.uliejh.cn/nnews/9495098.htm
- http://m.3g.uliejh.cn/nnews/436916.htm
- http://m.3g.uliejh.cn/nnews/9156523.htm
- http://m.3g.uliejh.cn/nnews/1412186.htm
- http://m.3g.uliejh.cn/nnews/165785.htm
- http://m.3g.uliejh.cn/nnews/00872.htm
- http://m.3g.uliejh.cn/nnews/6872306.htm
- http://m.3g.uliejh.cn/nnews/96742.htm
- http://m.3g.uliejh.cn/nnews/5406390.htm
- http://m.3g.uliejh.cn/nnews/8265.htm
- http://m.3g.uliejh.cn/nnews/354327.htm
- http://m.3g.uliejh.cn/nnews/80790.htm
- http://m.3g.uliejh.cn/nnews/62212.htm
- http://m.3g.uliejh.cn/nnews/872196.htm
- http://m.3g.uliejh.cn/nnews/5099245.htm
- http://m.3g.uliejh.cn/nnews/62413.htm
- http://m.3g.uliejh.cn/nnews/69689.htm
- http://m.3g.uliejh.cn/nnews/52616.htm
- http://m.3g.uliejh.cn/nnews/3872.htm
- http://m.3g.uliejh.cn/nnews/56165.htm
- http://m.3g.uliejh.cn/nnews/9780.htm
- http://m.3g.uliejh.cn/nnews/4860.htm
- http://m.3g.uliejh.cn/nnews/8699873.htm
- http://m.3g.uliejh.cn/nnews/2254611.htm
- http://m.3g.uliejh.cn/nnews/92707.htm
- http://m.3g.uliejh.cn/nnews/9382862.htm
- http://m.3g.uliejh.cn/nnews/02374.htm
- http://m.3g.uliejh.cn/nnews/27579.htm
- http://m.3g.uliejh.cn/nnews/966645.htm
- http://m.3g.uliejh.cn/nnews/3517.htm
- http://m.3g.uliejh.cn/nnews/86871.htm
- http://m.3g.uliejh.cn/nnews/5488.htm
- http://m.3g.uliejh.cn/nnews/8458.htm
- http://m.3g.uliejh.cn/nnews/5958.htm
- http://m.3g.uliejh.cn/nnews/60013.htm
- http://m.3g.uliejh.cn/nnews/18719.htm
- http://m.3g.uliejh.cn/nnews/20610.htm
- http://m.3g.uliejh.cn/nnews/4925.htm
- http://m.3g.uliejh.cn/nnews/77032.htm
- http://m.3g.uliejh.cn/nnews/58487.htm
- http://m.3g.uliejh.cn/nnews/96593.htm
- http://m.3g.uliejh.cn/nnews/238903.htm
- http://m.3g.uliejh.cn/nnews/8956.htm
- http://m.3g.uliejh.cn/nnews/2790.htm
- http://m.3g.uliejh.cn/nnews/94545.htm
- http://m.3g.uliejh.cn/nnews/4923.htm
- http://m.3g.uliejh.cn/nnews/256417.htm
- http://m.3g.uliejh.cn/nnews/29593.htm
- http://m.3g.uliejh.cn/nnews/2697.htm
- http://m.3g.uliejh.cn/nnews/321625.htm
- http://m.3g.uliejh.cn/nnews/70129.htm
- http://m.3g.uliejh.cn/nnews/0424346.htm
- http://m.3g.uliejh.cn/nnews/1870839.htm
- http://m.3g.uliejh.cn/nnews/259640.htm
- http://m.3g.uliejh.cn/nnews/662843.htm
- http://m.3g.uliejh.cn/nnews/1014767.htm
- http://m.3g.uliejh.cn/nnews/7935.htm
- http://m.3g.uliejh.cn/nnews/78297.htm
- http://m.3g.uliejh.cn/nnews/681623.htm
- http://m.3g.uliejh.cn/nnews/873031.htm
- http://m.3g.uliejh.cn/nnews/36332.htm
- http://m.3g.uliejh.cn/nnews/542131.htm
- http://m.3g.uliejh.cn/nnews/4240.htm
- http://m.3g.uliejh.cn/nnews/774088.htm
- http://m.3g.uliejh.cn/nnews/792157.htm
- http://m.3g.uliejh.cn/nnews/48921.htm
- http://m.3g.uliejh.cn/nnews/8690833.htm
- http://m.3g.uliejh.cn/nnews/7589762.htm
- http://m.3g.uliejh.cn/nnews/3397.htm
- http://m.3g.uliejh.cn/nnews/4552966.htm
- http://m.3g.uliejh.cn/nnews/1583703.htm
- http://m.3g.uliejh.cn/nnews/9680562.htm
- http://m.3g.uliejh.cn/nnews/5561.htm
- http://m.3g.uliejh.cn/nnews/9819582.htm
- http://m.3g.uliejh.cn/nnews/6249361.htm
- http://m.3g.uliejh.cn/nnews/490680.htm
- http://m.3g.uliejh.cn/nnews/861777.htm
- http://m.3g.uliejh.cn/nnews/5816.htm
- http://m.3g.uliejh.cn/nnews/139103.htm
- http://m.3g.uliejh.cn/nnews/0016.htm
- http://m.3g.uliejh.cn/nnews/59223.htm
- http://m.3g.uliejh.cn/nnews/8992481.htm
- http://m.3g.uliejh.cn/nnews/29714.htm
- http://m.3g.uliejh.cn/nnews/5767048.htm
- http://m.3g.uliejh.cn/nnews/5448097.htm
- http://m.3g.uliejh.cn/nnews/40346.htm
- http://m.3g.uliejh.cn/nnews/7876.htm
- http://m.3g.uliejh.cn/nnews/790451.htm
- http://m.3g.uliejh.cn/nnews/409718.htm
- http://m.3g.uliejh.cn/nnews/88776.htm
- http://m.3g.uliejh.cn/nnews/08412.htm
- http://m.3g.uliejh.cn/nnews/8680.htm
- http://m.3g.uliejh.cn/nnews/13767.htm
- http://m.3g.uliejh.cn/nnews/72737.htm
- http://m.3g.uliejh.cn/nnews/511691.htm
- http://m.3g.uliejh.cn/nnews/4232760.htm
- http://m.3g.uliejh.cn/nnews/73039.htm
- http://m.3g.uliejh.cn/nnews/76968.htm
- http://m.3g.uliejh.cn/nnews/0031171.htm
- http://m.3g.uliejh.cn/nnews/07182.htm
- http://m.3g.uliejh.cn/nnews/23773.htm
- http://m.3g.uliejh.cn/nnews/899144.htm
- http://m.3g.uliejh.cn/nnews/119279.htm
- http://m.3g.uliejh.cn/nnews/93566.htm
- http://m.3g.uliejh.cn/nnews/744882.htm
- http://m.3g.uliejh.cn/nnews/6343269.htm
- http://m.3g.uliejh.cn/nnews/3727059.htm
- http://m.3g.uliejh.cn/nnews/3153.htm
- http://m.3g.uliejh.cn/nnews/87452.htm
- http://m.3g.uliejh.cn/nnews/2472.htm
- http://m.3g.uliejh.cn/nnews/8926.htm
- http://m.3g.uliejh.cn/nnews/54592.htm
- http://m.3g.uliejh.cn/nnews/5531.htm
- http://m.3g.uliejh.cn/nnews/0911.htm
- http://m.3g.uliejh.cn/nnews/749284.htm
- http://m.3g.uliejh.cn/nnews/9570804.htm
- http://m.3g.uliejh.cn/nnews/436374.htm
- http://m.3g.uliejh.cn/nnews/7248113.htm
- http://m.3g.uliejh.cn/nnews/086957.htm
- http://m.3g.uliejh.cn/nnews/713532.htm
- http://m.3g.uliejh.cn/nnews/1170.htm
- http://m.3g.uliejh.cn/nnews/278835.htm
- http://m.3g.uliejh.cn/nnews/4361.htm
- http://m.3g.uliejh.cn/nnews/715698.htm
- http://m.3g.uliejh.cn/nnews/118221.htm
- http://m.3g.uliejh.cn/nnews/0337145.htm
- http://m.3g.uliejh.cn/nnews/0379.htm
- http://m.3g.uliejh.cn/nnews/612707.htm
- http://m.3g.uliejh.cn/nnews/94112.htm
- http://m.3g.uliejh.cn/nnews/59608.htm
- http://m.3g.uliejh.cn/nnews/719670.htm
- http://m.3g.uliejh.cn/nnews/01468.htm
- http://m.3g.uliejh.cn/nnews/69965.htm
- http://m.3g.uliejh.cn/nnews/449025.htm
- http://m.3g.uliejh.cn/nnews/5902.htm
- http://m.3g.uliejh.cn/nnews/814220.htm
- http://m.3g.uliejh.cn/nnews/8617682.htm
- http://m.3g.uliejh.cn/nnews/000867.htm
- http://m.3g.uliejh.cn/nnews/8506.htm
- http://m.3g.uliejh.cn/nnews/951721.htm
- http://m.3g.uliejh.cn/nnews/1132570.htm
- http://m.3g.uliejh.cn/nnews/507814.htm
- http://m.3g.uliejh.cn/nnews/9843.htm
- http://m.3g.uliejh.cn/nnews/7283.htm
- http://m.3g.uliejh.cn/nnews/4874.htm
- http://m.3g.uliejh.cn/nnews/277435.htm
- http://m.3g.uliejh.cn/nnews/7305421.htm
- http://m.3g.uliejh.cn/nnews/1916441.htm
- http://m.3g.uliejh.cn/nnews/71617.htm
- http://m.3g.uliejh.cn/nnews/74320.htm
- http://m.3g.uliejh.cn/nnews/253897.htm
- http://m.3g.uliejh.cn/nnews/494067.htm
- http://m.3g.uliejh.cn/nnews/9107612.htm
- http://m.3g.uliejh.cn/nnews/998953.htm
- http://m.3g.uliejh.cn/nnews/2044450.htm
- http://m.3g.uliejh.cn/nnews/492025.htm
- http://m.3g.uliejh.cn/nnews/7275129.htm
- http://m.3g.uliejh.cn/nnews/12762.htm
- http://m.3g.uliejh.cn/nnews/6361.htm
- http://m.3g.uliejh.cn/nnews/7687.htm
- http://m.3g.uliejh.cn/nnews/0182591.htm
- http://m.3g.uliejh.cn/nnews/65737.htm
- http://m.3g.uliejh.cn/nnews/0914.htm
- http://m.3g.uliejh.cn/nnews/7216624.htm
- http://m.3g.uliejh.cn/nnews/3358.htm
- http://m.3g.uliejh.cn/nnews/493293.htm
- http://m.3g.uliejh.cn/nnews/1340.htm
- http://m.3g.uliejh.cn/nnews/12375.htm
- http://m.3g.uliejh.cn/nnews/1325852.htm
- http://m.3g.uliejh.cn/nnews/1880867.htm
- http://m.3g.uliejh.cn/nnews/5216.htm
- http://m.3g.uliejh.cn/nnews/01888.htm
- http://m.3g.uliejh.cn/nnews/27643.htm
- http://m.3g.uliejh.cn/nnews/9805.htm
- http://m.3g.uliejh.cn/nnews/66847.htm
- http://m.3g.uliejh.cn/nnews/8022.htm
- http://m.3g.uliejh.cn/nnews/6154183.htm
- http://m.3g.uliejh.cn/nnews/133795.htm
- http://m.3g.uliejh.cn/nnews/3071.htm
- http://m.3g.uliejh.cn/nnews/4706.htm
- http://m.3g.uliejh.cn/nnews/477607.htm
- http://m.3g.uliejh.cn/nnews/5245.htm
- http://m.3g.uliejh.cn/nnews/6186.htm
- http://m.3g.uliejh.cn/nnews/430978.htm
- http://m.3g.uliejh.cn/nnews/764590.htm
- http://m.3g.uliejh.cn/nnews/2085.htm
- http://m.3g.uliejh.cn/nnews/9737191.htm
- http://m.3g.uliejh.cn/nnews/459220.htm
- http://m.3g.uliejh.cn/nnews/9291.htm
- http://m.3g.uliejh.cn/nnews/391016.htm
- http://m.3g.uliejh.cn/nnews/356057.htm
- http://m.3g.uliejh.cn/nnews/8499.htm
- http://m.3g.uliejh.cn/nnews/56877.htm
- http://m.3g.uliejh.cn/nnews/03076.htm
- http://m.3g.uliejh.cn/nnews/9316322.htm
- http://m.3g.uliejh.cn/nnews/84501.htm
- http://m.3g.uliejh.cn/nnews/6745226.htm
- http://m.3g.uliejh.cn/nnews/602500.htm
- http://m.3g.uliejh.cn/nnews/881835.htm
- http://m.3g.uliejh.cn/nnews/5389798.htm
- http://m.3g.uliejh.cn/nnews/5207659.htm
- http://m.3g.uliejh.cn/nnews/792083.htm
- http://m.3g.uliejh.cn/nnews/649207.htm
- http://m.3g.uliejh.cn/nnews/409201.htm
- http://m.3g.uliejh.cn/nnews/878149.htm
- http://m.3g.uliejh.cn/nnews/0073380.htm
- http://m.3g.uliejh.cn/nnews/1396.htm
- http://m.3g.uliejh.cn/nnews/917548.htm
- http://m.3g.uliejh.cn/nnews/89169.htm
- http://m.3g.uliejh.cn/nnews/97036.htm
- http://m.3g.uliejh.cn/nnews/1228.htm
- http://m.3g.uliejh.cn/nnews/620417.htm
- http://m.3g.uliejh.cn/nnews/919075.htm
- http://m.3g.uliejh.cn/nnews/6038591.htm
- http://m.3g.uliejh.cn/nnews/4756877.htm
- http://m.3g.uliejh.cn/nnews/126998.htm

## 项目结构

```
newslink-archive/
├── app/                              # 主应用目录
│   ├── __init__.py                   # 应用工厂与配置加载
│   ├── routes/                       # 路由蓝图
│   │   ├── api.py                    # RESTful API 端点（链接增删改查）
│   │   ├── admin.py                  # 管理后台界面路由
│   │   └── public.py                 # 公开导航页与静态生成入口
│   ├── models/                       # 数据模型与 ORM 映射
│   │   ├── link.py                   # 链接实体模型（URL、标题、状态、标签）
│   │   ├── category.py               # 分类树模型
│   │   └── check_log.py              # 检测历史日志模型
│   ├── services/                     # 业务服务层
│   │   ├── importer.py               # 批量导入服务（支持 CSV/文本）
│   │   ├── checker.py                # 链接可用性检测服务（异步任务）
│   │   ├── exporter.py               # 导出服务（Markdown/JSON/CSV）
│   │   └── static_generator.py       # 静态站点生成器（Jinja2 + 前端打包）
│   ├── templates/                    # Jinja2 模板文件
│   │   ├── admin/                    # 管理后台页面模板
│   │   └── static/                   # 静态站主题模板（默认主题）
│   └── static/                       # 静态资源（CSS / JS / 图片）
│       ├── css/                      # 基于 Bulma 的自定义样式
│       └── js/                       # 前端交互逻辑（Vue 3 或原生 JS）
├── scripts/                          # 运维与工具脚本
│   ├── init_db.py                    # 初始化数据库与默认分类数据
│   ├── migrate_db.py                 # 数据库迁移脚本（升级版本）
│   └── batch_import.py               # 命令行批量导入工具
├── tests/                            # 单元测试与集成测试
│   ├── test_models.py                # 数据模型测试
│   ├── test_api.py                   # API 端点测试（pytest + Flask test client）
│   └── test_checker.py               # 检测服务模拟测试
├── docs/                             # 文档源码（Markdown）
│   ├── user-guide/                   # 用户手册章节
│   ├── deployment/                   # 部署文档
│   ├── api/                          # API 参考文档（OpenAPI 生成）
│   └── developer/                    # 开发者指南与扩展说明
├── config/                           # 配置文件目录
│   ├── default.py                    # 默认配置（开发环境）
│   ├── production.py                 # 生产环境配置模板
│   └── logging.yaml                  # 日志格式与级别配置
├── data/                             # 数据存储目录（不纳入版本控制）
│   ├── newslink.db                   # SQLite 数据库文件
│   └── exports/                      # 导出文件临时存放目录
├── .env.example                      # 环境变量示例文件
├── requirements.txt                  # Python 依赖列表
├── package.json                      # 前端构建依赖（Node.js）
├── webpack.config.js                 # 静态资源打包配置
├── app.py                            # 应用启动入口（开发服务器）
├── wsgi.py                           # 生产环境 WSGI 入口（gunicorn）
└── README.md                         # 本文件
```

## 贡献指南

1. 阅读项目行为准则与贡献规范：在提交任何代码或文档前，请先阅读项目根目录下的 CODE_OF_CONDUCT.md 与 CONTRIBUTING.md 文件，了解预期行为与提交流程。

2. 选择或创建 Issue：前往 GitHub Issues 查看待办任务，或新建 Issue 描述你希望修复的缺陷或新增的功能。建议先与维护者沟通设计思路，避免重复劳动。

3. 派生仓库并创建功能分支：将本项目 Fork 至个人账号，然后基于 main 分支创建新的功能分支，分支命名采用 `feature/描述` 或 `fix/描述` 格式。

4. 编写代码并添加测试：确保新增代码有对应的单元测试覆盖，所有测试通过（运行 `pytest tests/`）。代码风格遵循 PEP 8，并保持注释清晰。

5. 提交 Pull Request：提交前请确保分支与上游 main 保持同步，PR 标题简明扼要，正文中描述改动内容、影响范围及测试情况。等待至少一位维护者审阅。

## 常见问题

Q: 项目是否必须使用 Redis？如果没有 Redis 可以运行吗？

A: Redis 并非强制依赖。系统默认使用基于内存的简单队列进行任务调度，适合单机部署或链接总数低于 5000 的场景。若需要持久化任务状态、分布式执行或大量并发检测，则建议启用 Redis。你可以在配置文件中将 `QUEUE_BACKEND` 设置为 `memory` 或 `redis` 来切换。

Q: 静态站点生成模式是否支持自定义主题？

A: 支持。项目使用 Jinja2 模板引擎，所有模板文件位于 `app/templates/static/` 目录下。你可以复制默认主题目录并修改其中的 HTML 结构和 CSS 样式，然后在配置中指定 `STATIC_THEME` 变量指向新目录。静态资源打包使用 Webpack，支持 SCSS 与 ES6 编译。

Q: 导入大量链接时是否会卡顿？

A: 导入过程采用批量插入与事务控制，每 500 条提交一次。对于 1 万条以内的链接，SQLite 可在数秒内完成导入。若超过 5 万条，建议使用 PostgreSQL 作为后端数据库（需在配置中切换 `SQLALCHEMY_DATABASE_URI`），并启用索引优化。同时在管理界面中，分页加载每页默认 50 条，避免前端渲染压力。

## 许可证

MIT

> 外链数量: 250 | 生成时间: 2026-08-24 23:40:21
