# WebLink Catalog System

WebLink Catalog System 是一个面向技术文档聚合与外部资源导航的开源静态站点生成工具。该项目定位于帮助开发者、技术团队及内容创作者快速建立结构化的外部链接资源库，将分散的优质技术文章、官方文档、社区讨论与内部知识库进行统一编目与检索。项目本身不提供具体内容，而是通过可配置的元数据驱动方式，将大量原始 URL 转化为可浏览、可搜索、可按标签与时间排序的静态 HTML 页面，适用于搭建个人技术书架、团队知识周报、项目外部依赖文档镜像站等场景。

## 功能概览

批量 URL 导入与结构化存储：系统支持从纯文本列表、CSV 或 JSON 批量导入 URL，自动解析来源域名、路径特征与文件扩展名，生成唯一标识符并存入本地 SQLite 数据库或 Markdown 元数据文件，为后续分类与展示提供基础。

多维度分类与标签系统：每个资源条目可绑定多个自定义标签（如 "backend"、"microservices"、"security"）以及所属类别（如 "blog"、"official-doc"、"tutorial"），支持基于标签云的快速筛选与关联推荐。

全文元数据检索：基于 SQLite FTS5 或 MiniSearch 引擎，对资源标题、描述、标签、来源域名建立全文索引，支持布尔查询、短语匹配与模糊搜索，检索结果按相关度与时间排序。

静态站点生成引擎：内置基于 EJS 或 Handlebars 模板的渲染管线，可将资源数据渲染为响应式 HTML 页面，支持暗色主题、分页导航与 RSS/Atom 订阅输出，生成产物可部署到任意静态托管服务。

增量更新与过期检测：通过记录每个 URL 的首次收录时间与最后访问状态，系统可定期执行健康检查，标记失效链接（HTTP 状态码非 200）并生成过期报告，辅助维护者清理或更新资源。

导入导出与备份机制：支持将全部资源数据导出为 JSON、YAML 或 CSV 格式，便于迁移至其他系统或进行离线分析；同时提供定时自动备份数据库与配置文件的命令行选项。

访问统计与热度排序：可选集成轻量级点击计数（基于文件系统或 Redis），统计每个资源的被访问次数，并按热度（日/周/月）生成热门榜单，帮助用户发现高价值内容。

权限分级与私有资源标记：支持基于用户角色的访问控制（需搭配简单认证中间件），可将部分 URL 标记为内部/私有，仅登录用户可见，适用于企业内部分享场景。

## 应用场景

个人技术书签库的集中化管理：开发者可将长期积累的分散在浏览器书签、笔记软件中的技术文章链接统一导入 WebLink Catalog System，通过标签和搜索快速找回特定主题的资料，避免重复收藏和遗忘。

团队知识周报与月刊编排：技术团队每周会产生大量有价值的外部链接（如最佳实践、故障复盘、新工具发布），利用本系统可将这些链接按周/月分类，自动生成美观的周报页面并发送给团队成员，替代传统邮件群发。

项目外部依赖文档镜像导航：在微服务或前后端分离项目中，团队依赖多个第三方库和框架的官方文档，通过本系统建立统一的文档导航页，列出所有依赖项的官方地址、社区教程和已知问题讨论链接，降低新成员上手成本。

技术社区资源聚合站：开源社区或技术媒体可将投稿、推荐的外部文章按领域（AI、云原生、数据库等）组织为分类目录页，同时提供热门榜单和搜索功能，为读者提供一站式的优质内容发现入口。

离线开发环境辅助文档库：在无法访问外网的内网开发环境中，可将常用外部文档的缓存地址或内部镜像地址录入系统，配合静态生成功能构建内网可用的文档门户，减少对外网依赖。

## 快速开始

以下步骤适用于 Linux / macOS / Windows WSL 环境，要求已安装 Node.js 18 或 Python 3.10（视发行版选择）。

```bash
# 克隆项目仓库
git clone https://github.com/weblink-catalog/weblink-system.git
cd weblink-system

# 安装依赖（以 Node.js 版本为例）
npm install

# 复制环境变量模板并编辑数据库路径与站点标题
cp .env.example .env
nano .env

# 执行初始数据迁移与静态站点生成
npm run migrate
npm run build

# 启动开发服务器，默认监听 http://localhost:3000
npm run serve
```

访问本地服务后，即可通过管理后台（/admin）进行 URL 导入与分类操作，或直接浏览生成的静态页面（/public）。

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|---------|---------|------|
| Node.js | 18.x 或 20.x LTS | 运行时环境，用于执行构建脚本与开发服务器 |
| SQLite3 | 3.35.0 以上 | 内置元数据存储引擎，无需额外安装，但需确保系统支持 |
| npm 或 yarn | 8.x 或 1.22.x | 包管理器，用于安装项目依赖与运行脚本 |
| Git | 2.25.0 以上 | 版本控制工具，用于克隆仓库与获取更新 |
| 操作系统 | Linux (glibc 2.28+), macOS 11+, Windows 10+ (WSL2) | 支持主流操作系统，Windows 原生环境需使用 PowerShell 7 |
| Python 3 | 3.10+（可选） | 若使用 Python 发行版，需安装 pip 与 virtualenv |
| Redis | 6.2+（可选） | 若启用热度统计功能，需要 Redis 作为计数缓存 |
| Nginx 或 Caddy | 最新稳定版（可选） | 用于生产环境反向代理与静态文件托管 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|------|------|-----------|
| 用户手册 | /docs/user-guide/installation | 如何在不同操作系统上安装与配置 WebLink Catalog System |
| 用户手册 | /docs/user-guide/importing | 支持哪些导入格式，如何处理批量 URL 与重复检测 |
| 用户手册 | /docs/user-guide/tagging | 如何创建、合并与删除标签，以及标签的层级关系 |
| 用户手册 | /docs/user-guide/search | 搜索语法说明，包括模糊匹配、字段限定与排序方式 |
| 运维指南 | /docs/ops/deployment | 生产环境部署建议（静态托管、Docker、systemd 服务） |
| 运维指南 | /docs/ops/backup | 数据库备份策略与恢复步骤，以及迁移到新服务器的方法 |
| 开发者文档 | /docs/dev/architecture | 整体架构图、数据流、核心模块职责与扩展点设计 |
| 开发者文档 | /docs/dev/api | RESTful API 端点说明，用于外部系统集成与二次开发 |
| 贡献者指南 | /CONTRIBUTING.md | 提交代码、报告问题、完善文档的流程与代码规范 |

## 资源列表

- http://m.blog.uliejh.cn/snews/096682.htm
- http://m.blog.uliejh.cn/snews/9662663.htm
- http://m.blog.uliejh.cn/snews/91939.htm
- http://m.blog.uliejh.cn/snews/0853951.htm
- http://m.blog.uliejh.cn/snews/601333.htm
- http://m.blog.uliejh.cn/snews/0698.htm
- http://m.blog.uliejh.cn/snews/89728.htm
- http://m.blog.uliejh.cn/snews/995631.htm
- http://m.blog.uliejh.cn/snews/903976.htm
- http://m.blog.uliejh.cn/snews/6168573.htm
- http://m.blog.uliejh.cn/snews/5751287.htm
- http://m.blog.uliejh.cn/snews/5723647.htm
- http://m.blog.uliejh.cn/snews/75055.htm
- http://m.blog.uliejh.cn/snews/446966.htm
- http://m.blog.uliejh.cn/snews/85135.htm
- http://m.blog.uliejh.cn/snews/2570706.htm
- http://m.blog.uliejh.cn/snews/495137.htm
- http://m.blog.uliejh.cn/snews/62230.htm
- http://m.blog.uliejh.cn/snews/4289605.htm
- http://m.blog.uliejh.cn/snews/6469.htm
- http://m.blog.uliejh.cn/snews/418052.htm
- http://m.blog.uliejh.cn/snews/842983.htm
- http://m.blog.uliejh.cn/snews/7854.htm
- http://m.blog.uliejh.cn/snews/176466.htm
- http://m.blog.uliejh.cn/snews/631665.htm
- http://m.blog.uliejh.cn/snews/5970981.htm
- http://m.blog.uliejh.cn/snews/79746.htm
- http://m.blog.uliejh.cn/snews/3365.htm
- http://m.blog.uliejh.cn/snews/54938.htm
- http://m.blog.uliejh.cn/snews/1600904.htm
- http://m.blog.uliejh.cn/snews/9437.htm
- http://m.blog.uliejh.cn/snews/1689.htm
- http://m.blog.uliejh.cn/snews/7578.htm
- http://m.blog.uliejh.cn/snews/2800049.htm
- http://m.blog.uliejh.cn/snews/2084614.htm
- http://m.blog.uliejh.cn/snews/6987570.htm
- http://m.blog.uliejh.cn/snews/262800.htm
- http://m.blog.uliejh.cn/snews/1628.htm
- http://m.blog.uliejh.cn/snews/1692196.htm
- http://m.blog.uliejh.cn/snews/70892.htm
- http://m.blog.uliejh.cn/snews/912350.htm
- http://m.blog.uliejh.cn/snews/952435.htm
- http://m.blog.uliejh.cn/snews/645569.htm
- http://m.blog.uliejh.cn/snews/964806.htm
- http://m.blog.uliejh.cn/snews/40759.htm
- http://m.blog.uliejh.cn/snews/7402011.htm
- http://m.blog.uliejh.cn/snews/24907.htm
- http://m.blog.uliejh.cn/snews/0533.htm
- http://m.blog.uliejh.cn/snews/0247.htm
- http://m.blog.uliejh.cn/snews/46622.htm
- http://m.blog.uliejh.cn/snews/87142.htm
- http://m.blog.uliejh.cn/snews/8358232.htm
- http://m.blog.uliejh.cn/snews/844749.htm
- http://m.blog.uliejh.cn/snews/6608764.htm
- http://m.blog.uliejh.cn/snews/22993.htm
- http://m.blog.uliejh.cn/snews/45607.htm
- http://m.blog.uliejh.cn/snews/886502.htm
- http://m.blog.uliejh.cn/snews/3889.htm
- http://m.blog.uliejh.cn/snews/69670.htm
- http://m.blog.uliejh.cn/snews/89868.htm
- http://m.blog.uliejh.cn/snews/753440.htm
- http://m.blog.uliejh.cn/snews/33987.htm
- http://m.blog.uliejh.cn/snews/8280.htm
- http://m.blog.uliejh.cn/snews/2498.htm
- http://m.blog.uliejh.cn/snews/29365.htm
- http://m.blog.uliejh.cn/snews/993661.htm
- http://m.blog.uliejh.cn/snews/226595.htm
- http://m.blog.uliejh.cn/snews/381939.htm
- http://m.blog.uliejh.cn/snews/82450.htm
- http://m.blog.uliejh.cn/snews/6159.htm
- http://m.blog.uliejh.cn/snews/0572.htm
- http://m.blog.uliejh.cn/snews/8044734.htm
- http://m.blog.uliejh.cn/snews/969285.htm
- http://m.blog.uliejh.cn/snews/6845.htm
- http://m.blog.uliejh.cn/snews/0909.htm
- http://m.blog.uliejh.cn/snews/24051.htm
- http://m.blog.uliejh.cn/snews/5386.htm
- http://m.blog.uliejh.cn/snews/9172.htm
- http://m.blog.uliejh.cn/snews/7774.htm
- http://m.blog.uliejh.cn/snews/942641.htm
- http://m.blog.uliejh.cn/snews/52809.htm
- http://m.blog.uliejh.cn/snews/258953.htm
- http://m.blog.uliejh.cn/snews/4450658.htm
- http://m.blog.uliejh.cn/snews/644927.htm
- http://m.blog.uliejh.cn/snews/419235.htm
- http://m.blog.uliejh.cn/snews/9037.htm
- http://m.blog.uliejh.cn/snews/794031.htm
- http://m.blog.uliejh.cn/snews/73360.htm
- http://m.blog.uliejh.cn/snews/153984.htm
- http://m.blog.uliejh.cn/snews/0752973.htm
- http://m.blog.uliejh.cn/snews/4443864.htm
- http://m.blog.uliejh.cn/snews/838935.htm
- http://m.blog.uliejh.cn/snews/015981.htm
- http://m.blog.uliejh.cn/snews/7387.htm
- http://m.blog.uliejh.cn/snews/7490.htm
- http://m.blog.uliejh.cn/snews/4807447.htm
- http://m.blog.uliejh.cn/snews/10313.htm
- http://m.blog.uliejh.cn/snews/6295.htm
- http://m.blog.uliejh.cn/snews/2996.htm
- http://m.blog.uliejh.cn/snews/680536.htm
- http://m.blog.uliejh.cn/snews/01325.htm
- http://m.blog.uliejh.cn/snews/238229.htm
- http://m.blog.uliejh.cn/snews/3676678.htm
- http://m.blog.uliejh.cn/snews/544248.htm
- http://m.blog.uliejh.cn/snews/2361687.htm
- http://m.blog.uliejh.cn/snews/98156.htm
- http://m.blog.uliejh.cn/snews/433649.htm
- http://m.blog.uliejh.cn/snews/6745910.htm
- http://m.blog.uliejh.cn/snews/06641.htm
- http://m.blog.uliejh.cn/snews/0933.htm
- http://m.blog.uliejh.cn/snews/600254.htm
- http://m.blog.uliejh.cn/snews/7001.htm
- http://m.blog.uliejh.cn/snews/9342455.htm
- http://m.blog.uliejh.cn/snews/3785214.htm
- http://m.blog.uliejh.cn/snews/65549.htm
- http://m.blog.uliejh.cn/snews/205568.htm
- http://m.blog.uliejh.cn/snews/6513118.htm
- http://m.blog.uliejh.cn/snews/2441703.htm
- http://m.blog.uliejh.cn/snews/2870915.htm
- http://m.blog.uliejh.cn/snews/7908832.htm
- http://m.blog.uliejh.cn/snews/48492.htm
- http://m.blog.uliejh.cn/snews/60661.htm
- http://m.blog.uliejh.cn/snews/51702.htm
- http://m.blog.uliejh.cn/snews/822537.htm
- http://m.blog.uliejh.cn/snews/17075.htm
- http://m.blog.uliejh.cn/snews/319165.htm
- http://m.blog.uliejh.cn/snews/94450.htm
- http://m.blog.uliejh.cn/snews/9415965.htm
- http://m.blog.uliejh.cn/snews/4272.htm
- http://m.blog.uliejh.cn/snews/8426644.htm
- http://m.blog.uliejh.cn/snews/8012.htm
- http://m.blog.uliejh.cn/snews/2570649.htm
- http://m.blog.uliejh.cn/snews/869798.htm
- http://m.blog.uliejh.cn/snews/2181651.htm
- http://m.blog.uliejh.cn/snews/281551.htm
- http://m.blog.uliejh.cn/snews/85806.htm
- http://m.blog.uliejh.cn/snews/706880.htm
- http://m.blog.uliejh.cn/snews/4797.htm
- http://m.blog.uliejh.cn/snews/416851.htm
- http://m.blog.uliejh.cn/snews/6795350.htm
- http://m.blog.uliejh.cn/snews/0336608.htm
- http://m.blog.uliejh.cn/snews/9220.htm
- http://m.blog.uliejh.cn/snews/21153.htm
- http://m.blog.uliejh.cn/snews/163163.htm
- http://m.blog.uliejh.cn/snews/84150.htm
- http://m.blog.uliejh.cn/snews/644018.htm
- http://m.blog.uliejh.cn/snews/3742312.htm
- http://m.blog.uliejh.cn/snews/4024.htm
- http://m.blog.uliejh.cn/snews/960657.htm
- http://m.blog.uliejh.cn/snews/3150.htm
- http://m.blog.uliejh.cn/snews/570297.htm
- http://m.blog.uliejh.cn/snews/786127.htm
- http://m.blog.uliejh.cn/snews/1439132.htm
- http://m.blog.uliejh.cn/snews/56801.htm
- http://m.blog.uliejh.cn/snews/0290867.htm
- http://m.blog.uliejh.cn/snews/2442489.htm
- http://m.blog.uliejh.cn/snews/154436.htm
- http://m.blog.uliejh.cn/snews/24498.htm
- http://m.blog.uliejh.cn/snews/65706.htm
- http://m.blog.uliejh.cn/snews/662016.htm
- http://m.blog.uliejh.cn/snews/760471.htm
- http://m.blog.uliejh.cn/snews/7350993.htm
- http://m.blog.uliejh.cn/snews/798734.htm
- http://m.blog.uliejh.cn/snews/4505.htm
- http://m.blog.uliejh.cn/snews/441893.htm
- http://m.blog.uliejh.cn/snews/0589872.htm
- http://m.blog.uliejh.cn/snews/3451.htm
- http://m.blog.uliejh.cn/snews/217587.htm
- http://m.blog.uliejh.cn/snews/8452.htm
- http://m.blog.uliejh.cn/snews/6840038.htm
- http://m.blog.uliejh.cn/snews/91557.htm
- http://m.blog.uliejh.cn/snews/9262881.htm
- http://m.blog.uliejh.cn/snews/86318.htm
- http://m.blog.uliejh.cn/snews/2922.htm
- http://m.blog.uliejh.cn/snews/78058.htm
- http://m.blog.uliejh.cn/snews/8119792.htm
- http://m.blog.uliejh.cn/snews/78631.htm
- http://m.blog.uliejh.cn/snews/5080.htm
- http://m.blog.uliejh.cn/snews/42905.htm
- http://m.blog.uliejh.cn/snews/19991.htm
- http://m.blog.uliejh.cn/snews/59660.htm
- http://m.blog.uliejh.cn/snews/346800.htm
- http://m.blog.uliejh.cn/snews/718036.htm
- http://m.blog.uliejh.cn/snews/28834.htm
- http://m.blog.uliejh.cn/snews/74095.htm
- http://m.blog.uliejh.cn/snews/409105.htm
- http://m.blog.uliejh.cn/snews/153569.htm
- http://m.blog.uliejh.cn/snews/698001.htm
- http://m.blog.uliejh.cn/snews/254719.htm
- http://m.blog.uliejh.cn/snews/458640.htm
- http://m.blog.uliejh.cn/snews/5524633.htm
- http://m.blog.uliejh.cn/snews/0052881.htm
- http://m.blog.uliejh.cn/snews/5567890.htm
- http://m.blog.uliejh.cn/snews/803820.htm
- http://m.blog.uliejh.cn/snews/74096.htm
- http://m.blog.uliejh.cn/snews/51806.htm
- http://m.blog.uliejh.cn/snews/0782430.htm
- http://m.blog.uliejh.cn/snews/8035.htm
- http://m.blog.uliejh.cn/snews/1518.htm
- http://m.blog.uliejh.cn/snews/9967.htm
- http://m.blog.uliejh.cn/snews/20138.htm
- http://m.blog.uliejh.cn/snews/5504977.htm
- http://m.blog.uliejh.cn/snews/5220600.htm
- http://m.blog.uliejh.cn/snews/0046577.htm
- http://m.blog.uliejh.cn/snews/0629062.htm
- http://m.blog.uliejh.cn/snews/67805.htm
- http://m.blog.uliejh.cn/snews/5894.htm
- http://m.blog.uliejh.cn/snews/5546428.htm
- http://m.blog.uliejh.cn/snews/5985.htm
- http://m.blog.uliejh.cn/snews/8092147.htm
- http://m.blog.uliejh.cn/snews/068138.htm
- http://m.blog.uliejh.cn/snews/775900.htm
- http://m.blog.uliejh.cn/snews/0219.htm
- http://m.blog.uliejh.cn/snews/370088.htm
- http://m.blog.uliejh.cn/snews/375759.htm
- http://m.blog.uliejh.cn/snews/4056538.htm
- http://m.blog.uliejh.cn/snews/272890.htm
- http://m.blog.uliejh.cn/snews/2480748.htm
- http://m.blog.uliejh.cn/snews/3316294.htm
- http://m.blog.uliejh.cn/snews/7455.htm
- http://m.blog.uliejh.cn/snews/7698174.htm
- http://m.blog.uliejh.cn/snews/7554943.htm
- http://m.blog.uliejh.cn/snews/1775949.htm
- http://m.blog.uliejh.cn/snews/43497.htm
- http://m.blog.uliejh.cn/snews/3226073.htm
- http://m.blog.uliejh.cn/snews/4315181.htm
- http://m.blog.uliejh.cn/snews/568468.htm
- http://m.blog.uliejh.cn/snews/358342.htm
- http://m.blog.uliejh.cn/snews/08543.htm
- http://m.blog.uliejh.cn/snews/379640.htm
- http://m.blog.uliejh.cn/snews/0357488.htm
- http://m.blog.uliejh.cn/snews/0081374.htm
- http://m.blog.uliejh.cn/snews/7805.htm
- http://m.blog.uliejh.cn/snews/02991.htm
- http://m.blog.uliejh.cn/snews/912232.htm
- http://m.blog.uliejh.cn/snews/0255.htm
- http://m.blog.uliejh.cn/snews/186481.htm
- http://m.blog.uliejh.cn/snews/1818597.htm
- http://m.blog.uliejh.cn/snews/348483.htm
- http://m.blog.uliejh.cn/snews/8690238.htm
- http://m.blog.uliejh.cn/snews/6521737.htm
- http://m.blog.uliejh.cn/snews/705649.htm
- http://m.blog.uliejh.cn/snews/64231.htm
- http://m.blog.uliejh.cn/snews/9644638.htm
- http://m.blog.uliejh.cn/snews/1600.htm
- http://m.blog.uliejh.cn/snews/3647296.htm
- http://m.blog.uliejh.cn/snews/50141.htm
- http://m.blog.uliejh.cn/snews/2078.htm
- http://m.blog.uliejh.cn/snews/85499.htm
- http://m.blog.uliejh.cn/snews/715773.htm

## 项目结构

```
weblink-system/
├── .github/                         # GitHub 相关配置
│   ├── workflows/                   # CI/CD 流水线（测试、构建、发布）
│   └── ISSUE_TEMPLATE/              # 问题报告与功能请求模板
├── src/                             # 核心源代码目录
│   ├── core/                        # 核心模块：数据库访问、配置管理、日志
│   │   ├── database.js              # SQLite 连接池与迁移管理
│   │   ├── config.js                # 环境变量解析与默认值合并
│   │   └── logger.js                # 结构化日志（JSON 格式，支持多级别）
│   ├── importers/                   # 导入器模块：处理不同格式的 URL 列表
│   │   ├── csv-importer.js          # CSV 格式导入，支持自定义列映射
│   │   ├── json-importer.js         # JSON 数组或对象导入
│   │   └── plaintext-importer.js    # 纯文本每行一个 URL 的导入
│   ├── models/                      # 数据模型与 ORM 映射
│   │   ├── resource.js              # 资源条目模型（URL、标题、描述、标签）
│   │   ├── tag.js                   # 标签模型（名称、别名、父标签）
│   │   └── visit.js                 # 访问记录模型（IP、时间、引用来源）
│   ├── services/                    # 业务服务层
│   │   ├── search-service.js        # 全文搜索服务（FTS5 索引与查询解析）
│   │   ├── health-check.js          # 批量 URL 健康检查（并发控制与超时）
│   │   ├── stats-service.js         # 热度统计与排行榜计算
│   │   └── export-service.js        # 数据导出为 JSON/YAML/CSV
│   ├── generators/                  # 静态站点生成器
│   │   ├── renderer.js              # 模板引擎封装（EJS 与 Markdown 混合）
│   │   ├── paginator.js             # 分页逻辑与页码计算
│   │   └── rss-feed.js              # RSS/Atom 订阅源生成
│   ├── admin/                       # 管理后台（Express + 简单鉴权）
│   │   ├── routes.js                # 后台路由定义（导入、编辑、删除）
│   │   └── middleware.js            # 身份验证与日志中间件
│   └── cli/                         # 命令行工具入口
│       ├── index.js                 # CLI 主命令分发器
│       └── commands/                # 子命令实现（migrate, build, serve, check）
├── public/                          # 生成的静态站点输出目录（可部署）
│   ├── index.html                   # 首页（热门资源、最新添加、分类导航）
│   ├── tags/                        # 标签页目录（每个标签一个 HTML）
│   ├── resources/                   # 资源详情页（按 ID 或 slug 命名）
│   └── static/                      # 静态资源（CSS、JS、图片）
│       ├── css/                     # 主题样式（暗色/亮色）
│       └── js/                      # 前端交互（搜索、分页、暗色切换）
├── templates/                       # 模板文件（EJS 布局与组件）
│   ├── layouts/                     # 页面布局（头部、底部、导航）
│   └── partials/                    # 可复用组件（卡片、标签云、分页条）
├── data/                            # 数据存储目录
│   ├── weblink.db                   # SQLite 数据库文件（默认位置）
│   └── backups/                     # 自动备份的数据库归档
├── tests/                           # 单元测试与集成测试
│   ├── unit/                        # 模型与工具函数测试（Jest）
│   └── integration/                 # 导入、搜索、生成流程的端到端测试
├── docs/                            # 文档源码（Markdown）
│   ├── user-guide/                  # 用户手册章节
│   ├── ops/                         # 运维与部署指南
│   └── dev/                         # 开发者文档与 API 参考
├── scripts/                         # 辅助脚本（数据迁移、性能测试）
├── .env.example                     # 环境变量示例（含数据库路径、站点标题）
├── .eslintrc.js                     # ESLint 代码风格配置
├── .prettierrc                      # Prettier 格式化规则
├── package.json                     # Node.js 项目清单与依赖声明
├── README.md                        # 项目主页说明（当前文件）
├── LICENSE                          # MIT 许可证全文
└── CHANGELOG.md                     # 版本更新日志
```

## 贡献指南

提交问题报告与功能请求：请先查阅 GitHub Issues 中是否已存在类似条目，若无则新建 Issue，使用提供的模板清晰描述复现步骤、预期行为与实际结果，并附上系统版本与相关日志。

完善文档与翻译：文档位于 /docs 目录，采用 Markdown 编写，欢迎修正错别字、补充示例或增加其他语言翻译。提交前请确保本地构建通过（npm run docs:build）且格式符合 Prettier 规范。

代码贡献流程：Fork 本仓库，在 feat/ 或 fix/ 分支上开发，遵循项目 ESLint 与 Prettier 配置，添加或修改单元测试以覆盖变更，确保所有测试通过（npm test），最后发起 Pull Request 到 main 分支，描述变更动机与影响范围。

新增导入器或生成器插件：若希望支持新的数据源格式（如 RSS Feed、Notion 导出）或新的输出格式（如 PDF、JSON API），请在 src/importers 或 src/generators 下新增模块，并在对应服务的注册表中添加条目，同时提供至少一个示例文件与测试用例。

参与社区讨论与评审：欢迎加入项目的 GitHub Discussions 板块，分享使用心得、提出改进建议或帮助评审他人的 Pull Request，活跃贡献者将被邀请为 Collaborator。

## 常见问题

问：导入大量 URL 时出现内存不足或超时错误，应如何处理？

答：对于超过 1000 条 URL 的批量导入，建议使用命令行方式（npm run import -- --batch-size=200 --delay=100）而非通过管理后台，以控制并发请求数量并避免浏览器超时。同时可调整环境变量 NODE_OPTIONS=--max-old-space-size=4096 增加 Node.js 内存限制。若网络状况不佳，建议先关闭健康检查功能（--skip-health-check），导入完成后再单独执行检查。

问：如何将现有浏览器书签（如 Chrome 或 Firefox 导出的 HTML）迁移到本系统？

答：本系统未直接支持浏览器书签 HTML 格式，但可借助转换工具先行处理。推荐使用 bookmark-parser 命令行工具将书签 HTML 转换为 JSON 数组，再通过本系统的 JSON 导入器完成迁移。具体转换命令可参考 /docs/user-guide/migration-from-bookmarks 章节，其中提供了示例脚本与字段映射说明。

问：静态站点生成后，部分资源链接无法打开或显示 404，如何排查？

答：首先检查资源条目中的 URL 是否完整无误（包括协议头），若确认无误，请运行健康检查命令（npm run check -- --timeout=5000）获取每个 URL 的 HTTP 状态码与响应时间。若大量链接超时，可能是目标站点存在反爬机制，可调整 user-agent 或增加延迟参数。若个别链接失效，建议在管理后台将其标记为“已失效”并查找替代链接更新，或保留历史记录供参考。

## 许可证

MIT License

Copyright (c) 2026 WebLink Catalog System Contributors

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

> 外链数量: 250 | 生成时间: 2026-08-24 23:40:21
