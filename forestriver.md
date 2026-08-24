# WebResource Central

WebResource Central 是一个面向技术研究与信息检索场景的轻量级外链资源聚合平台。该项目定位于帮助开发者、技术研究员与内容运营人员高效管理和分发分散于各类信息源中的外部链接，提供统一的条目化访问入口与基础元数据描述能力。项目本身不直接存储或托管具体内容，而是作为结构化导航层，将海量 URL 资源以有序、可维护的方式组织起来，适用于需要快速建立专题外链库或进行批量资源整理的使用场景。

项目采用纯静态 HTML 与前端脚本构建，无需后端服务或数据库依赖，所有资源条目通过 JSON 配置文件驱动，支持一键导入、分类标记与全文检索。目标用户包括需要维护技术文档外链索引的团队、进行行业信息采集的分析人员，以及希望建立个人知识导航站点的独立开发者。

## 功能概览

批量资源导入：支持通过 JSON 或 CSV 格式批量导入 URL 列表，自动识别链接标题与来源域名，减少手工录入成本。

分类标签系统：可为每条资源添加多级分类标签与自定义备注字段，便于按主题、来源或用途进行筛选与分组。

全文检索过滤：内置简易倒排索引，支持对链接标题、描述与标签字段进行关键词匹配，返回相关结果排序。

条目状态标记：提供未读、已读、收藏、归档四种状态，辅助用户管理阅读进度与关注优先级。

去重与校验：在导入阶段自动检测重复 URL，并对链接可用性进行基础 HTTP 状态码探测，标记异常条目。

导出与共享：支持将当前资源列表导出为 JSON 或 Markdown 格式，便于备份或与团队成员共享。

界面自适应：响应式布局设计，在桌面端、平板与移动设备上均能获得一致的浏览与操作体验。

## 应用场景

技术文档外链整理：技术团队在撰写项目文档或周报时，需要引用大量外部参考链接。WebResource Central 可作为内部外链中转仓库，按模块分类存储，撰写时直接检索并复制链接，避免重复搜索。

行业信息每日汇总：信息分析人员每日从多个新闻源与技术博客收集素材，通过批量导入功能快速聚合当日链接，并利用状态标记区分已读与待读条目，提升信息处理效率。

个人知识导航站搭建：独立开发者或研究员可将长期积累的技术收藏夹（如教程、工具、论文链接）导入系统，通过分类标签构建清晰的导航层级，并生成可公开访问的静态页面作为个人知识门户。

专题资源包交付：咨询机构或培训讲师在交付专题资料时，可将数百条外部参考链接打包为结构化数据集，配合导出功能生成 Markdown 格式的资源清单，直接嵌入课程讲义或技术方案中。

## 快速开始

以下步骤适用于在本地环境或服务器上快速部署 WebResource Central 实例。

```bash
# 克隆项目仓库
git clone https://github.com/webresource-central/webresource-central.git

# 进入项目目录
cd webresource-central

# 安装依赖（仅需 HTTP 服务器，以 Python 内置模块为例）
# Python 3 版本
python -m http.server 8080

# 若使用 Python 2 版本，请执行：
# python -m SimpleHTTPServer 8080

# 若使用 Node.js，亦可执行：
# npx serve -p 8080

# 打开浏览器访问 http://localhost:8080
```

## 安装要求

| 依赖项 | 必需版本 | 说明 |
|--------|----------|------|
| Web 浏览器 | Chrome 80+ / Firefox 75+ / Edge 80+ | 需支持 ES6 语法与 Fetch API |
| HTTP 服务器 | Python 3.6+ 或 Node.js 12+ | 用于提供静态文件服务，生产环境可换为 Nginx |
| 操作系统 | Linux / macOS / Windows | 无特定限制，可跨平台运行 |
| 内存 | 最低 256 MB | 资源列表大小影响内存占用，建议 512 MB 以上 |
| 磁盘空间 | 最低 50 MB | 主要用于存储 HTML、CSS、JS 及 JSON 数据文件 |
| 网络访问 | 建议外网可达（生产环境） | 用于检测链接可用性，本地运行可忽略 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|------|------|------------|
| 用户手册 | /docs/user-guide.md | 如何导入资源、分类标签操作、检索语法、状态管理 |
| 管理员指南 | /docs/admin-guide.md | 如何自定义分类体系、配置链接校验规则、备份与迁移数据 |
| 数据格式说明 | /docs/data-format.md | JSON 数据结构的字段定义、示例与扩展约定 |
| 开发者参考 | /docs/developer-api.md | 核心函数接口说明、事件钩子、自定义渲染器编写方法 |
| 部署运维 | /docs/deployment.md | 生产环境 Nginx 配置示例、HTTPS 设置、性能调优参数 |

## 资源列表

- http://m.wap.uliejh.cn/bnews/495645.htm
- http://m.wap.uliejh.cn/bnews/129928.htm
- http://m.wap.uliejh.cn/bnews/454540.htm
- http://m.wap.uliejh.cn/bnews/7470955.htm
- http://m.wap.uliejh.cn/bnews/150097.htm
- http://m.wap.uliejh.cn/bnews/5812192.htm
- http://m.wap.uliejh.cn/bnews/2314.htm
- http://m.wap.uliejh.cn/bnews/4793599.htm
- http://m.wap.uliejh.cn/bnews/7804.htm
- http://m.wap.uliejh.cn/bnews/68695.htm
- http://m.wap.uliejh.cn/bnews/70069.htm
- http://m.wap.uliejh.cn/bnews/72159.htm
- http://m.wap.uliejh.cn/bnews/09923.htm
- http://m.wap.uliejh.cn/bnews/3807582.htm
- http://m.wap.uliejh.cn/bnews/30876.htm
- http://m.wap.uliejh.cn/bnews/286461.htm
- http://m.wap.uliejh.cn/bnews/50344.htm
- http://m.wap.uliejh.cn/bnews/9502025.htm
- http://m.wap.uliejh.cn/bnews/444164.htm
- http://m.wap.uliejh.cn/bnews/548102.htm
- http://m.wap.uliejh.cn/bnews/541691.htm
- http://m.wap.uliejh.cn/bnews/05038.htm
- http://m.wap.uliejh.cn/bnews/176673.htm
- http://m.wap.uliejh.cn/bnews/956580.htm
- http://m.wap.uliejh.cn/bnews/8080900.htm
- http://m.wap.uliejh.cn/bnews/4934901.htm
- http://m.wap.uliejh.cn/bnews/450647.htm
- http://m.wap.uliejh.cn/bnews/052557.htm
- http://m.wap.uliejh.cn/bnews/2663614.htm
- http://m.wap.uliejh.cn/bnews/251575.htm
- http://m.wap.uliejh.cn/bnews/5510.htm
- http://m.wap.uliejh.cn/bnews/436062.htm
- http://m.wap.uliejh.cn/bnews/60587.htm
- http://m.wap.uliejh.cn/bnews/74495.htm
- http://m.wap.uliejh.cn/bnews/028270.htm
- http://m.wap.uliejh.cn/bnews/31086.htm
- http://m.wap.uliejh.cn/bnews/2751918.htm
- http://m.wap.uliejh.cn/bnews/2211989.htm
- http://m.wap.uliejh.cn/bnews/7075929.htm
- http://m.wap.uliejh.cn/bnews/214368.htm
- http://m.wap.uliejh.cn/bnews/7334345.htm
- http://m.wap.uliejh.cn/bnews/8914.htm
- http://m.wap.uliejh.cn/bnews/43896.htm
- http://m.wap.uliejh.cn/bnews/302017.htm
- http://m.wap.uliejh.cn/bnews/45149.htm
- http://m.wap.uliejh.cn/bnews/2999.htm
- http://m.wap.uliejh.cn/bnews/1012800.htm
- http://m.wap.uliejh.cn/bnews/997151.htm
- http://m.wap.uliejh.cn/bnews/0876546.htm
- http://m.wap.uliejh.cn/bnews/46319.htm
- http://m.wap.uliejh.cn/bnews/7140.htm
- http://m.wap.uliejh.cn/bnews/852247.htm
- http://m.wap.uliejh.cn/bnews/8312076.htm
- http://m.wap.uliejh.cn/bnews/0226.htm
- http://m.wap.uliejh.cn/bnews/178250.htm
- http://m.wap.uliejh.cn/bnews/130686.htm
- http://m.wap.uliejh.cn/bnews/8282336.htm
- http://m.wap.uliejh.cn/bnews/52379.htm
- http://m.wap.uliejh.cn/bnews/52206.htm
- http://m.wap.uliejh.cn/bnews/7579368.htm
- http://m.wap.uliejh.cn/bnews/3704.htm
- http://m.wap.uliejh.cn/bnews/561116.htm
- http://m.wap.uliejh.cn/bnews/593079.htm
- http://m.wap.uliejh.cn/bnews/098541.htm
- http://m.wap.uliejh.cn/bnews/4693.htm
- http://m.wap.uliejh.cn/bnews/63894.htm
- http://m.wap.uliejh.cn/bnews/499647.htm
- http://m.wap.uliejh.cn/bnews/7388285.htm
- http://m.wap.uliejh.cn/bnews/0588.htm
- http://m.wap.uliejh.cn/bnews/4088.htm
- http://m.wap.uliejh.cn/bnews/91285.htm
- http://m.wap.uliejh.cn/bnews/266927.htm
- http://m.wap.uliejh.cn/bnews/3568.htm
- http://m.wap.uliejh.cn/bnews/5653717.htm
- http://m.wap.uliejh.cn/bnews/334445.htm
- http://m.wap.uliejh.cn/bnews/0485581.htm
- http://m.wap.uliejh.cn/bnews/490734.htm
- http://m.wap.uliejh.cn/bnews/9811.htm
- http://m.wap.uliejh.cn/bnews/29917.htm
- http://m.wap.uliejh.cn/bnews/75433.htm
- http://m.wap.uliejh.cn/bnews/8729292.htm
- http://m.wap.uliejh.cn/bnews/4741522.htm
- http://m.wap.uliejh.cn/bnews/39139.htm
- http://m.wap.uliejh.cn/bnews/75884.htm
- http://m.wap.uliejh.cn/bnews/88250.htm
- http://m.wap.uliejh.cn/bnews/581615.htm
- http://m.wap.uliejh.cn/bnews/8423364.htm
- http://m.wap.uliejh.cn/bnews/7719.htm
- http://m.wap.uliejh.cn/bnews/57958.htm
- http://m.wap.uliejh.cn/bnews/9268.htm
- http://m.wap.uliejh.cn/bnews/535686.htm
- http://m.wap.uliejh.cn/bnews/050205.htm
- http://m.wap.uliejh.cn/bnews/0532990.htm
- http://m.wap.uliejh.cn/bnews/98515.htm
- http://m.wap.uliejh.cn/bnews/824266.htm
- http://m.wap.uliejh.cn/bnews/4416.htm
- http://m.wap.uliejh.cn/bnews/25912.htm
- http://m.wap.uliejh.cn/bnews/541474.htm
- http://m.wap.uliejh.cn/bnews/6922354.htm
- http://m.wap.uliejh.cn/bnews/20467.htm
- http://m.wap.uliejh.cn/bnews/5640431.htm
- http://m.wap.uliejh.cn/bnews/1699.htm
- http://m.wap.uliejh.cn/bnews/7214056.htm
- http://m.wap.uliejh.cn/bnews/68273.htm
- http://m.wap.uliejh.cn/bnews/9536434.htm
- http://m.wap.uliejh.cn/bnews/887229.htm
- http://m.wap.uliejh.cn/bnews/79991.htm
- http://m.wap.uliejh.cn/bnews/279935.htm
- http://m.wap.uliejh.cn/bnews/96139.htm
- http://m.wap.uliejh.cn/bnews/184944.htm
- http://m.wap.uliejh.cn/bnews/96179.htm
- http://m.wap.uliejh.cn/bnews/62122.htm
- http://m.wap.uliejh.cn/bnews/5257.htm
- http://m.wap.uliejh.cn/bnews/1763.htm
- http://m.wap.uliejh.cn/bnews/3313865.htm
- http://m.wap.uliejh.cn/bnews/609328.htm
- http://m.wap.uliejh.cn/bnews/84096.htm
- http://m.wap.uliejh.cn/bnews/80955.htm
- http://m.wap.uliejh.cn/bnews/76054.htm
- http://m.wap.uliejh.cn/bnews/7460.htm
- http://m.wap.uliejh.cn/bnews/2230113.htm
- http://m.wap.uliejh.cn/bnews/354585.htm
- http://m.wap.uliejh.cn/bnews/3503.htm
- http://m.wap.uliejh.cn/bnews/4263.htm
- http://m.wap.uliejh.cn/bnews/970419.htm
- http://m.wap.uliejh.cn/bnews/591220.htm
- http://m.wap.uliejh.cn/bnews/04927.htm
- http://m.wap.uliejh.cn/bnews/7108.htm
- http://m.wap.uliejh.cn/bnews/495796.htm
- http://m.wap.uliejh.cn/bnews/96998.htm
- http://m.wap.uliejh.cn/bnews/266185.htm
- http://m.wap.uliejh.cn/bnews/41606.htm
- http://m.wap.uliejh.cn/bnews/38838.htm
- http://m.wap.uliejh.cn/bnews/6894.htm
- http://m.wap.uliejh.cn/bnews/93002.htm
- http://m.wap.uliejh.cn/bnews/2670.htm
- http://m.wap.uliejh.cn/bnews/729650.htm
- http://m.wap.uliejh.cn/bnews/1320.htm
- http://m.wap.uliejh.cn/bnews/42287.htm
- http://m.wap.uliejh.cn/bnews/3979.htm
- http://m.wap.uliejh.cn/bnews/8908644.htm
- http://m.wap.uliejh.cn/bnews/08405.htm
- http://m.wap.uliejh.cn/bnews/75057.htm
- http://m.wap.uliejh.cn/bnews/486537.htm
- http://m.wap.uliejh.cn/bnews/3592708.htm
- http://m.wap.uliejh.cn/bnews/429263.htm
- http://m.wap.uliejh.cn/bnews/5280.htm
- http://m.wap.uliejh.cn/bnews/6465032.htm
- http://m.wap.uliejh.cn/bnews/3147.htm
- http://m.wap.uliejh.cn/bnews/126105.htm
- http://m.wap.uliejh.cn/bnews/8397.htm
- http://m.wap.uliejh.cn/bnews/0737.htm
- http://m.wap.uliejh.cn/bnews/7651.htm
- http://m.wap.uliejh.cn/bnews/8022961.htm
- http://m.wap.uliejh.cn/bnews/9052.htm
- http://m.wap.uliejh.cn/bnews/836572.htm
- http://m.wap.uliejh.cn/bnews/4556378.htm
- http://m.wap.uliejh.cn/bnews/0652258.htm
- http://m.wap.uliejh.cn/bnews/5419526.htm
- http://m.wap.uliejh.cn/bnews/35107.htm
- http://m.wap.uliejh.cn/bnews/77035.htm
- http://m.wap.uliejh.cn/bnews/506826.htm
- http://m.wap.uliejh.cn/bnews/3598057.htm
- http://m.wap.uliejh.cn/bnews/762247.htm
- http://m.wap.uliejh.cn/bnews/189174.htm
- http://m.wap.uliejh.cn/bnews/1892975.htm
- http://m.wap.uliejh.cn/bnews/7326.htm
- http://m.wap.uliejh.cn/bnews/768540.htm
- http://m.wap.uliejh.cn/bnews/43286.htm
- http://m.wap.uliejh.cn/bnews/3710143.htm
- http://m.wap.uliejh.cn/bnews/0946363.htm
- http://m.wap.uliejh.cn/bnews/3196853.htm
- http://m.wap.uliejh.cn/bnews/5856459.htm
- http://m.wap.uliejh.cn/bnews/8216432.htm
- http://m.wap.uliejh.cn/bnews/4923620.htm
- http://m.wap.uliejh.cn/bnews/9158323.htm
- http://m.wap.uliejh.cn/bnews/37054.htm
- http://m.wap.uliejh.cn/bnews/4664.htm
- http://m.wap.uliejh.cn/bnews/72971.htm
- http://m.wap.uliejh.cn/bnews/9563.htm
- http://m.wap.uliejh.cn/bnews/7856044.htm
- http://m.wap.uliejh.cn/bnews/0997.htm
- http://m.wap.uliejh.cn/bnews/732861.htm
- http://m.wap.uliejh.cn/bnews/68888.htm
- http://m.wap.uliejh.cn/bnews/61397.htm
- http://m.wap.uliejh.cn/bnews/3440.htm
- http://m.wap.uliejh.cn/bnews/26679.htm
- http://m.wap.uliejh.cn/bnews/698468.htm
- http://m.wap.uliejh.cn/bnews/1999230.htm
- http://m.wap.uliejh.cn/bnews/26527.htm
- http://m.wap.uliejh.cn/bnews/169364.htm
- http://m.wap.uliejh.cn/bnews/665353.htm
- http://m.wap.uliejh.cn/bnews/46846.htm
- http://m.wap.uliejh.cn/bnews/51279.htm
- http://m.wap.uliejh.cn/bnews/1863126.htm
- http://m.wap.uliejh.cn/bnews/5687261.htm
- http://m.wap.uliejh.cn/bnews/7932.htm
- http://m.wap.uliejh.cn/bnews/032210.htm
- http://m.wap.uliejh.cn/bnews/4398.htm
- http://m.wap.uliejh.cn/bnews/02489.htm
- http://m.wap.uliejh.cn/bnews/745129.htm
- http://m.wap.uliejh.cn/bnews/89941.htm
- http://m.wap.uliejh.cn/bnews/451514.htm
- http://m.wap.uliejh.cn/bnews/0335.htm
- http://m.wap.uliejh.cn/bnews/72740.htm
- http://m.wap.uliejh.cn/bnews/074541.htm
- http://m.wap.uliejh.cn/bnews/1398.htm
- http://m.wap.uliejh.cn/bnews/896081.htm
- http://m.wap.uliejh.cn/bnews/1543.htm
- http://m.wap.uliejh.cn/bnews/2876915.htm
- http://m.wap.uliejh.cn/bnews/4139103.htm
- http://m.wap.uliejh.cn/bnews/5108101.htm
- http://m.wap.uliejh.cn/bnews/0637.htm
- http://m.wap.uliejh.cn/bnews/2570696.htm
- http://m.wap.uliejh.cn/bnews/159009.htm
- http://m.wap.uliejh.cn/bnews/4299628.htm
- http://m.wap.uliejh.cn/bnews/7376412.htm
- http://m.wap.uliejh.cn/bnews/77151.htm
- http://m.wap.uliejh.cn/bnews/8534.htm
- http://m.wap.uliejh.cn/bnews/965608.htm
- http://m.wap.uliejh.cn/bnews/16771.htm
- http://m.wap.uliejh.cn/bnews/7925.htm
- http://m.wap.uliejh.cn/bnews/09814.htm
- http://m.wap.uliejh.cn/bnews/2420.htm
- http://m.wap.uliejh.cn/bnews/80072.htm
- http://m.wap.uliejh.cn/bnews/1265088.htm
- http://m.wap.uliejh.cn/bnews/4582491.htm
- http://m.wap.uliejh.cn/bnews/958007.htm
- http://m.wap.uliejh.cn/bnews/70441.htm
- http://m.wap.uliejh.cn/bnews/59066.htm
- http://m.wap.uliejh.cn/bnews/01593.htm
- http://m.wap.uliejh.cn/bnews/7220297.htm
- http://m.wap.uliejh.cn/bnews/5953410.htm
- http://m.wap.uliejh.cn/bnews/296434.htm
- http://m.wap.uliejh.cn/bnews/988701.htm
- http://m.wap.uliejh.cn/bnews/54066.htm
- http://m.wap.uliejh.cn/bnews/06924.htm
- http://m.wap.uliejh.cn/bnews/1850.htm
- http://m.wap.uliejh.cn/bnews/5442.htm
- http://m.wap.uliejh.cn/bnews/8626.htm
- http://m.wap.uliejh.cn/bnews/9200923.htm
- http://m.wap.uliejh.cn/bnews/50458.htm
- http://m.wap.uliejh.cn/bnews/533903.htm
- http://m.wap.uliejh.cn/bnews/893257.htm
- http://m.wap.uliejh.cn/bnews/63476.htm
- http://m.wap.uliejh.cn/bnews/5234.htm
- http://m.wap.uliejh.cn/bnews/7863.htm
- http://m.wap.uliejh.cn/bnews/91554.htm
- http://m.wap.uliejh.cn/bnews/39687.htm
- http://m.wap.uliejh.cn/bnews/76735.htm

## 项目结构

```
webresource-central/
├── index.html                # 主页面入口，加载核心样式与脚本
├── favicon.ico               # 站点图标文件
├── assets/
│   ├── css/
│   │   └── main.css          # 全局样式表，包含响应式布局与暗色主题变量
│   ├── js/
│   │   ├── app.js            # 应用主逻辑，包含路由、状态管理与事件绑定
│   │   ├── store.js          # 数据存储层，负责 JSON 加载、增删改查与持久化
│   │   ├── search.js         # 全文检索实现，基于倒排索引与分词器
│   │   └── validator.js      # 链接校验模块，处理去重与 HTTP 状态探测
│   └── data/
│       ├── resources.json    # 主资源数据集，包含所有 URL 条目及元数据字段
│       └── categories.json   # 分类标签定义，包含层级关系与显示颜色
├── docs/
│   ├── user-guide.md         # 用户手册，详细说明界面操作与功能用法
│   ├── admin-guide.md        # 管理员指南，覆盖自定义配置与数据迁移
│   ├── data-format.md        # 数据格式规范，描述 JSON 字段含义与扩展点
│   ├── developer-api.md      # 开发者参考，列出核心接口与回调钩子
│   └── deployment.md         # 部署运维文档，包含 Nginx 配置与性能调优
├── scripts/
│   ├── import-csv.py         # Python 脚本，将 CSV 格式链接转为 JSON 导入
│   └── export-markdown.py    # Python 脚本，将 JSON 数据集导出为 Markdown 列表
├── tests/
│   ├── test-store.js         # 数据存储层的单元测试用例
│   ├── test-search.js        # 检索模块的单元测试用例
│   └── test-validator.js     # 链接校验模块的单元测试用例
├── .gitignore                # Git 忽略规则，排除临时文件与本地配置
├── package.json              # Node.js 项目描述文件，用于测试与构建工具
├── README.md                 # 当前项目说明文档
└── LICENSE                   # MIT 许可证文件
```

## 贡献指南

我们欢迎社区贡献者参与 WebResource Central 的改进与扩展。请按照以下步骤提交您的贡献。

首先，在 GitHub 上 Fork 本仓库，并将您的 Fork 克隆到本地开发环境。建议在 dev 分支上进行修改，保持主分支与上游同步。

其次，若您新增功能或修复缺陷，请编写对应的单元测试用例，确保测试覆盖核心逻辑。测试文件需放置在 tests/ 目录下，命名遵循 test-*.js 格式。

第三，提交代码前请运行项目内置的代码检查工具（通过 npm run lint 调用 ESLint），并确保所有测试用例通过（npm test）。对于用户界面相关的改动，请附上简短的操作描述或截图说明。

第四，提交 Pull Request 时，请清晰描述您的修改目的、实现方案以及影响范围。若与已有 Issue 相关，请在 PR 描述中引用 Issue 编号。维护者会在 5 个工作日内进行评审。

最后，对于非代码类的贡献（如文档改进、翻译、示例补充），请直接在 docs/ 目录下修改对应的 Markdown 文件，并同样通过 Pull Request 方式提交。我们感谢每一份文档优化。

## 常见问题

Q: 导入大量 URL 后页面加载变慢，如何优化？

A: 当资源条目超过 2000 条时，建议开启分页模式。您可以在 assets/js/app.js 中找到 PAGE_SIZE 配置项，将其设置为 50 或 100。同时，可考虑将 resources.json 文件拆分为多个按分类分割的 JSON 文件，并通过 store.js 中的懒加载机制按需加载。

Q: 链接校验功能提示大量超时或拒绝连接，是否会影响正常使用？

A: 链接校验采用浏览器原生 fetch API 进行探测，受跨域策略与目标服务器响应策略影响，部分链接可能返回超时或网络错误。此功能仅作为辅助参考，不影响条目本身的存储与检索。您可以在 validator.js 中调整超时阈值（默认 3000 毫秒），或关闭自动校验开关，改为手动触发。

Q: 能否将资源列表部署为纯静态页面，不依赖任何 HTTP 服务器？

A: 可以。由于项目完全由前端静态资源构成，您只需将整个目录放置在任意支持静态文件服务的环境中即可。若需要在本地直接双击 index.html 打开，请注意浏览器可能因同源策略限制 fetch 本地文件（file:// 协议），此时建议使用 VS Code 的 Live Server 插件或 Python HTTP 模块临时启动服务。

## 许可证

MIT

> 外链数量: 250 | 生成时间: 2026-08-24 23:40:21
