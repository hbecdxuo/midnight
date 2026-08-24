# NewsLink Aggregate Service

NewsLink Aggregate Service 是一个面向移动端资讯聚合与分发场景的轻量级技术资源导航工具。该项目专注于将分散的、按批次组织的 URL 资源进行结构化收录，为开发者、内容运营人员以及资讯聚合平台提供可复用的外链数据管理与检索基础框架。项目本身不生产内容，也不抓取页面，仅作为已审核 URL 资源的索引容器，适用于内部知识库建设、外部链接归档以及批量数据交接等场景。

目标用户包括：需要管理大量外链资源的后端开发人员、负责内容聚合平台运营的数据专员、以及希望基于现成 URL 批次快速搭建内部导航页面的全栈工程师。项目通过提供固定的目录结构、清晰的安装运行流程以及标准化的数据录入格式，显著降低批量 URL 处理与展示的工程门槛。

## 功能概览

批量 URL 导入与去重校验：支持按批次导入包含大量 URL 的文本数据，自动识别格式异常、协议缺失或重复条目，并提供冲突检测报告。

结构化目录树生成：根据 URL 的域名、路径层级、文件类型等特征，自动生成多级分类目录，便于按业务模块组织资源。

快速启动开发服务器：内置基于 Node.js 的轻量级开发服务，支持热重载，可在本地环境中即时预览资源列表的渲染效果。

资源状态标记与备注：为每条 URL 提供状态字段（有效、失效、待审核）和自定义备注能力，支持运营人员对链接进行人工标注。

多格式数据导出：支持将收录的 URL 列表导出为 JSON、CSV 或纯文本格式，便于与其他系统进行数据交换。

访问统计埋点接口：预留标准的访问计数与日志记录接口，可对接第三方分析服务，追踪每条链接的被访问频率。

权限分级管理：内置基于角色的访问控制模型，区分管理员、编辑者和只读访客三种权限层级。

## 应用场景

内部知识库外链归档：企业技术团队可将项目部署为内部文档系统的外链附件库，统一存放参考文档、API 手册、技术博客等外部资源链接，便于团队成员检索与复用。

资讯聚合平台数据交接：资讯类应用的后台运营人员可借助该项目整理每批次待上线的新闻链接，在内容审核与发布流程之间形成标准化的数据交换中间层。

个人开发者的资源导航站点搭建：独立开发者可利用项目提供的目录树生成能力，快速建立个人风格的网址导航页面，将日常收集的技术工具、学习资料、开源仓库等链接分门别类展示。

数据清洗前的链接预检：数据工程师在处理大型爬虫数据集时，可先将待处理的 URL 列表导入本项目，利用去重校验和状态标记功能完成初步清洗，再将干净数据交付下游流程。

## 快速开始

以下指令适用于 Linux 与 macOS 环境，Windows 用户建议使用 Git Bash 或 WSL2 执行。

```bash
# 克隆项目仓库
git clone https://github.com/example/newslink-aggregate.git

# 进入项目目录
cd newslink-aggregate

# 安装项目依赖（需要 Node.js 16.x 及以上版本）
npm install

# 启动开发服务器，默认监听端口 3000
npm run dev
```

启动后，在浏览器中访问 http://localhost:3000 即可查看当前批次（第 7/120 批）的 URL 资源列表页面。如需导入新批次数据，可将 URL 列表放入 `data/batch-7/` 目录下的 `urls.txt` 文件中，并执行 `npm run build-index` 命令刷新索引。

## 安装要求

| 依赖项 | 必需版本 | 说明 |
|--------|----------|------|
| Node.js | 16.x 或更高 | 运行时环境，用于执行构建脚本与开发服务器 |
| npm | 8.x 或更高 | 包管理器，用于安装项目依赖 |
| Git | 2.25 或更高 | 版本控制工具，用于克隆仓库与提交变更 |
| 操作系统 | Linux / macOS / Windows (WSL2) | 项目在主流操作系统上均可运行，Windows 原生环境需配置环境变量 |
| 磁盘空间 | 至少 200 MB | 用于存放项目源码、依赖包及生成的索引文件 |
| 内存 | 至少 512 MB | 开发服务器运行时的最低内存要求 |
| 网络 | 外网访问 | 安装依赖时需访问 npm 公共仓库，运行时不强制联网 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|------|------|------------|
| 入门指南 | docs/getting-started.md | 如何快速部署项目、理解目录结构并进行首次数据导入？ |
| 数据格式规范 | docs/data-format.md | URL 列表文件应遵循何种格式？如何编写备注与状态标记？ |
| 目录树配置 | docs/directory-config.md | 如何自定义分类规则，使 URL 按业务模块自动归类？ |
| API 参考 | docs/api-reference.md | 项目提供了哪些内部接口供二次开发调用？参数与返回值各是什么？ |
| 部署指南 | docs/deployment.md | 如何将项目部署到生产环境（如 Nginx + PM2 或 Docker）？ |
| 常见问题 | docs/faq.md | 遇到端口冲突、数据不更新或权限报错时应如何处理？ |

## 资源列表

- http://m.3g.uliejh.cn/nnews/73480.htm
- http://m.3g.uliejh.cn/nnews/34966.htm
- http://m.3g.uliejh.cn/nnews/078011.htm
- http://m.3g.uliejh.cn/nnews/42600.htm
- http://m.3g.uliejh.cn/nnews/0683985.htm
- http://m.3g.uliejh.cn/nnews/351330.htm
- http://m.3g.uliejh.cn/nnews/6232747.htm
- http://m.3g.uliejh.cn/nnews/4725907.htm
- http://m.3g.uliejh.cn/nnews/599235.htm
- http://m.3g.uliejh.cn/nnews/62954.htm
- http://m.3g.uliejh.cn/nnews/28420.htm
- http://m.3g.uliejh.cn/nnews/623096.htm
- http://m.3g.uliejh.cn/nnews/057443.htm
- http://m.3g.uliejh.cn/nnews/8830.htm
- http://m.3g.uliejh.cn/nnews/666025.htm
- http://m.3g.uliejh.cn/nnews/8488301.htm
- http://m.3g.uliejh.cn/nnews/667039.htm
- http://m.3g.uliejh.cn/nnews/493617.htm
- http://m.3g.uliejh.cn/nnews/70843.htm
- http://m.3g.uliejh.cn/nnews/208558.htm
- http://m.3g.uliejh.cn/nnews/6044.htm
- http://m.3g.uliejh.cn/nnews/02063.htm
- http://m.3g.uliejh.cn/nnews/766863.htm
- http://m.3g.uliejh.cn/nnews/5640.htm
- http://m.3g.uliejh.cn/nnews/79068.htm
- http://m.3g.uliejh.cn/nnews/1420701.htm
- http://m.3g.uliejh.cn/nnews/4434363.htm
- http://m.3g.uliejh.cn/nnews/9877.htm
- http://m.3g.uliejh.cn/nnews/2566245.htm
- http://m.3g.uliejh.cn/nnews/282877.htm
- http://m.3g.uliejh.cn/nnews/2375.htm
- http://m.3g.uliejh.cn/nnews/69332.htm
- http://m.3g.uliejh.cn/nnews/8509.htm
- http://m.3g.uliejh.cn/nnews/2199.htm
- http://m.3g.uliejh.cn/nnews/56793.htm
- http://m.3g.uliejh.cn/nnews/9272.htm
- http://m.3g.uliejh.cn/nnews/2461214.htm
- http://m.3g.uliejh.cn/nnews/30093.htm
- http://m.3g.uliejh.cn/nnews/3013.htm
- http://m.3g.uliejh.cn/nnews/909886.htm
- http://m.3g.uliejh.cn/nnews/1634055.htm
- http://m.3g.uliejh.cn/nnews/3327.htm
- http://m.3g.uliejh.cn/nnews/9116299.htm
- http://m.3g.uliejh.cn/nnews/118425.htm
- http://m.3g.uliejh.cn/nnews/36181.htm
- http://m.3g.uliejh.cn/nnews/0396.htm
- http://m.3g.uliejh.cn/nnews/446336.htm
- http://m.3g.uliejh.cn/nnews/1222.htm
- http://m.3g.uliejh.cn/nnews/7936.htm
- http://m.3g.uliejh.cn/nnews/5248.htm
- http://m.3g.uliejh.cn/nnews/4187642.htm
- http://m.3g.uliejh.cn/nnews/42398.htm
- http://m.3g.uliejh.cn/nnews/7040.htm
- http://m.3g.uliejh.cn/nnews/9564.htm
- http://m.3g.uliejh.cn/nnews/764635.htm
- http://m.3g.uliejh.cn/nnews/7443214.htm
- http://m.3g.uliejh.cn/nnews/01511.htm
- http://m.3g.uliejh.cn/nnews/9618596.htm
- http://m.3g.uliejh.cn/nnews/9481.htm
- http://m.3g.uliejh.cn/nnews/2140.htm
- http://m.3g.uliejh.cn/nnews/94299.htm
- http://m.3g.uliejh.cn/nnews/5106293.htm
- http://m.3g.uliejh.cn/nnews/83127.htm
- http://m.3g.uliejh.cn/nnews/8729.htm
- http://m.3g.uliejh.cn/nnews/936825.htm
- http://m.3g.uliejh.cn/nnews/28064.htm
- http://m.3g.uliejh.cn/nnews/170267.htm
- http://m.3g.uliejh.cn/nnews/5271111.htm
- http://m.3g.uliejh.cn/nnews/365069.htm
- http://m.3g.uliejh.cn/nnews/326134.htm
- http://m.3g.uliejh.cn/nnews/79698.htm
- http://m.3g.uliejh.cn/nnews/199741.htm
- http://m.3g.uliejh.cn/nnews/8281869.htm
- http://m.3g.uliejh.cn/nnews/131807.htm
- http://m.3g.uliejh.cn/nnews/751402.htm
- http://m.3g.uliejh.cn/nnews/49978.htm
- http://m.3g.uliejh.cn/nnews/8696.htm
- http://m.3g.uliejh.cn/nnews/324543.htm
- http://m.3g.uliejh.cn/nnews/785612.htm
- http://m.3g.uliejh.cn/nnews/066668.htm
- http://m.3g.uliejh.cn/nnews/9130073.htm
- http://m.3g.uliejh.cn/nnews/201839.htm
- http://m.3g.uliejh.cn/nnews/5014.htm
- http://m.3g.uliejh.cn/nnews/3778678.htm
- http://m.3g.uliejh.cn/nnews/6002.htm
- http://m.3g.uliejh.cn/nnews/1234.htm
- http://m.3g.uliejh.cn/nnews/4944517.htm
- http://m.3g.uliejh.cn/nnews/836585.htm
- http://m.3g.uliejh.cn/nnews/8190704.htm
- http://m.3g.uliejh.cn/nnews/1049.htm
- http://m.3g.uliejh.cn/nnews/4602958.htm
- http://m.3g.uliejh.cn/nnews/53534.htm
- http://m.3g.uliejh.cn/nnews/3840973.htm
- http://m.3g.uliejh.cn/nnews/6077622.htm
- http://m.3g.uliejh.cn/nnews/14114.htm
- http://m.3g.uliejh.cn/nnews/7669.htm
- http://m.3g.uliejh.cn/nnews/062806.htm
- http://m.3g.uliejh.cn/nnews/60430.htm
- http://m.3g.uliejh.cn/nnews/93010.htm
- http://m.3g.uliejh.cn/nnews/97232.htm
- http://m.3g.uliejh.cn/nnews/1227.htm
- http://m.3g.uliejh.cn/nnews/12779.htm
- http://m.3g.uliejh.cn/nnews/229242.htm
- http://m.3g.uliejh.cn/nnews/4146.htm
- http://m.3g.uliejh.cn/nnews/36753.htm
- http://m.3g.uliejh.cn/nnews/18640.htm
- http://m.3g.uliejh.cn/nnews/3641.htm
- http://m.3g.uliejh.cn/nnews/7308499.htm
- http://m.3g.uliejh.cn/nnews/8003568.htm
- http://m.3g.uliejh.cn/nnews/3476.htm
- http://m.3g.uliejh.cn/nnews/26508.htm
- http://m.3g.uliejh.cn/nnews/7651234.htm
- http://m.3g.uliejh.cn/nnews/922545.htm
- http://m.3g.uliejh.cn/nnews/91712.htm
- http://m.3g.uliejh.cn/nnews/844877.htm
- http://m.3g.uliejh.cn/nnews/78591.htm
- http://m.3g.uliejh.cn/nnews/6764144.htm
- http://m.3g.uliejh.cn/nnews/1361.htm
- http://m.3g.uliejh.cn/nnews/7970054.htm
- http://m.3g.uliejh.cn/nnews/45806.htm
- http://m.3g.uliejh.cn/nnews/3885090.htm
- http://m.3g.uliejh.cn/nnews/754078.htm
- http://m.3g.uliejh.cn/nnews/92395.htm
- http://m.3g.uliejh.cn/nnews/4183.htm
- http://m.3g.uliejh.cn/nnews/7955.htm
- http://m.3g.uliejh.cn/nnews/35528.htm
- http://m.3g.uliejh.cn/nnews/9673.htm
- http://m.3g.uliejh.cn/nnews/00695.htm
- http://m.3g.uliejh.cn/nnews/723644.htm
- http://m.3g.uliejh.cn/nnews/98363.htm
- http://m.3g.uliejh.cn/nnews/965383.htm
- http://m.3g.uliejh.cn/nnews/95842.htm
- http://m.3g.uliejh.cn/nnews/068641.htm
- http://m.3g.uliejh.cn/nnews/3161345.htm
- http://m.3g.uliejh.cn/nnews/03136.htm
- http://m.3g.uliejh.cn/nnews/9193070.htm
- http://m.3g.uliejh.cn/nnews/806706.htm
- http://m.3g.uliejh.cn/nnews/571554.htm
- http://m.3g.uliejh.cn/nnews/3855303.htm
- http://m.3g.uliejh.cn/nnews/33867.htm
- http://m.3g.uliejh.cn/nnews/7577.htm
- http://m.3g.uliejh.cn/nnews/6093.htm
- http://m.3g.uliejh.cn/nnews/3937.htm
- http://m.3g.uliejh.cn/nnews/079816.htm
- http://m.3g.uliejh.cn/nnews/8342.htm
- http://m.3g.uliejh.cn/nnews/3806.htm
- http://m.3g.uliejh.cn/nnews/0942035.htm
- http://m.3g.uliejh.cn/nnews/213919.htm
- http://m.3g.uliejh.cn/nnews/5845113.htm
- http://m.3g.uliejh.cn/nnews/420017.htm
- http://m.3g.uliejh.cn/nnews/31418.htm
- http://m.3g.uliejh.cn/nnews/14159.htm
- http://m.3g.uliejh.cn/nnews/4031449.htm
- http://m.3g.uliejh.cn/nnews/342928.htm
- http://m.3g.uliejh.cn/nnews/303603.htm
- http://m.3g.uliejh.cn/nnews/0863564.htm
- http://m.3g.uliejh.cn/nnews/8300.htm
- http://m.3g.uliejh.cn/nnews/8652393.htm
- http://m.3g.uliejh.cn/nnews/611274.htm
- http://m.3g.uliejh.cn/nnews/4174.htm
- http://m.3g.uliejh.cn/nnews/028790.htm
- http://m.3g.uliejh.cn/nnews/5412748.htm
- http://m.3g.uliejh.cn/nnews/75427.htm
- http://m.3g.uliejh.cn/nnews/135430.htm
- http://m.3g.uliejh.cn/nnews/084037.htm
- http://m.3g.uliejh.cn/nnews/69883.htm
- http://m.3g.uliejh.cn/nnews/230035.htm
- http://m.3g.uliejh.cn/nnews/5671534.htm
- http://m.3g.uliejh.cn/nnews/5192843.htm
- http://m.3g.uliejh.cn/nnews/1714.htm
- http://m.3g.uliejh.cn/nnews/57152.htm
- http://m.3g.uliejh.cn/nnews/87428.htm
- http://m.3g.uliejh.cn/nnews/3631903.htm
- http://m.3g.uliejh.cn/nnews/0798638.htm
- http://m.3g.uliejh.cn/nnews/18996.htm
- http://m.3g.uliejh.cn/nnews/5489.htm
- http://m.3g.uliejh.cn/nnews/747661.htm
- http://m.3g.uliejh.cn/nnews/6601.htm
- http://m.3g.uliejh.cn/nnews/5814.htm
- http://m.3g.uliejh.cn/nnews/0425131.htm
- http://m.3g.uliejh.cn/nnews/771928.htm
- http://m.3g.uliejh.cn/nnews/8021771.htm
- http://m.3g.uliejh.cn/nnews/6279948.htm
- http://m.3g.uliejh.cn/nnews/83888.htm
- http://m.3g.uliejh.cn/nnews/26066.htm
- http://m.3g.uliejh.cn/nnews/4044566.htm
- http://m.3g.uliejh.cn/nnews/853997.htm
- http://m.3g.uliejh.cn/nnews/1739.htm
- http://m.3g.uliejh.cn/nnews/1335956.htm
- http://m.3g.uliejh.cn/nnews/3943.htm
- http://m.3g.uliejh.cn/nnews/9922766.htm
- http://m.3g.uliejh.cn/nnews/1992706.htm
- http://m.3g.uliejh.cn/nnews/369725.htm
- http://m.3g.uliejh.cn/nnews/35613.htm
- http://m.3g.uliejh.cn/nnews/954897.htm
- http://m.3g.uliejh.cn/nnews/44365.htm
- http://m.3g.uliejh.cn/nnews/139775.htm
- http://m.3g.uliejh.cn/nnews/294708.htm
- http://m.3g.uliejh.cn/nnews/6411605.htm
- http://m.3g.uliejh.cn/nnews/70084.htm
- http://m.3g.uliejh.cn/nnews/2025492.htm
- http://m.3g.uliejh.cn/nnews/978058.htm
- http://m.3g.uliejh.cn/nnews/01058.htm
- http://m.3g.uliejh.cn/nnews/99570.htm
- http://m.3g.uliejh.cn/nnews/78814.htm
- http://m.3g.uliejh.cn/nnews/921833.htm
- http://m.3g.uliejh.cn/nnews/351731.htm
- http://m.3g.uliejh.cn/nnews/89570.htm
- http://m.3g.uliejh.cn/nnews/563944.htm
- http://m.3g.uliejh.cn/nnews/24949.htm
- http://m.3g.uliejh.cn/nnews/811409.htm
- http://m.3g.uliejh.cn/nnews/0175646.htm
- http://m.3g.uliejh.cn/nnews/075444.htm
- http://m.3g.uliejh.cn/nnews/4636139.htm
- http://m.3g.uliejh.cn/nnews/9712.htm
- http://m.3g.uliejh.cn/nnews/3678105.htm
- http://m.3g.uliejh.cn/nnews/08451.htm
- http://m.3g.uliejh.cn/nnews/9473462.htm
- http://m.3g.uliejh.cn/nnews/52460.htm
- http://m.3g.uliejh.cn/nnews/31700.htm
- http://m.3g.uliejh.cn/nnews/428605.htm
- http://m.3g.uliejh.cn/nnews/273797.htm
- http://m.3g.uliejh.cn/nnews/2256.htm
- http://m.3g.uliejh.cn/nnews/288339.htm
- http://m.3g.uliejh.cn/nnews/6662914.htm
- http://m.3g.uliejh.cn/nnews/6754790.htm
- http://m.3g.uliejh.cn/nnews/8057.htm
- http://m.3g.uliejh.cn/nnews/7228.htm
- http://m.3g.uliejh.cn/nnews/56653.htm
- http://m.3g.uliejh.cn/nnews/13363.htm
- http://m.3g.uliejh.cn/nnews/7437051.htm
- http://m.3g.uliejh.cn/nnews/190691.htm
- http://m.3g.uliejh.cn/nnews/2383682.htm
- http://m.3g.uliejh.cn/nnews/2146693.htm
- http://m.3g.uliejh.cn/nnews/076557.htm
- http://m.3g.uliejh.cn/nnews/795335.htm
- http://m.3g.uliejh.cn/nnews/74101.htm
- http://m.3g.uliejh.cn/nnews/5446.htm
- http://m.3g.uliejh.cn/nnews/26432.htm
- http://m.3g.uliejh.cn/nnews/7461.htm
- http://m.3g.uliejh.cn/nnews/47677.htm
- http://m.3g.uliejh.cn/nnews/7727.htm
- http://m.3g.uliejh.cn/nnews/10571.htm
- http://m.3g.uliejh.cn/nnews/65336.htm
- http://m.3g.uliejh.cn/nnews/301641.htm
- http://m.3g.uliejh.cn/nnews/9138095.htm
- http://m.3g.uliejh.cn/nnews/06237.htm
- http://m.3g.uliejh.cn/nnews/97712.htm
- http://m.3g.uliejh.cn/nnews/1670.htm
- http://m.3g.uliejh.cn/nnews/990745.htm

## 项目结构

```
newslink-aggregate/
├── data/                                 # 数据存储目录
│   ├── batch-7/                          # 第 7 批次原始数据
│   │   ├── urls.txt                      # 原始 URL 列表（每行一个）
│   │   └── metadata.json                 # 批次元信息（来源、日期、审核状态）
│   ├── index/                            # 构建后的索引文件
│   │   ├── tree.json                     # 目录树结构数据
│   │   └── mapping.json                  # URL 与分类节点的映射表
│   └── archive/                          # 历史批次归档（只读）
│       ├── batch-1/                      # 第 1 批次数据
│       ├── batch-2/                      # 第 2 批次数据
│       └── ...
├── src/                                  # 源代码目录
│   ├── core/                             # 核心逻辑模块
│   │   ├── importer.js                   # URL 导入与去重校验器
│   │   ├── tree-builder.js               # 目录树生成器
│   │   └── validator.js                  # 链接格式与协议校验器
│   ├── server/                           # 开发服务器模块
│   │   ├── index.js                      # 服务入口（Express 应用）
│   │   └── routes/                       # 路由定义
│   │       ├── api.js                    # RESTful API 路由
│   │       └── view.js                   # 页面渲染路由
│   ├── templates/                        # 前端模板文件
│   │   ├── layout.ejs                    # 基础布局模板
│   │   ├── list.ejs                      # 资源列表页模板
│   │   └── detail.ejs                    # 单条资源详情页模板
│   └── utils/                            # 通用工具函数
│       ├── logger.js                     # 日志记录器
│       ├── config.js                     # 配置加载器
│       └── file-helper.js                # 文件读写辅助函数
├── tests/                                # 单元测试与集成测试
│   ├── importer.test.js                  # 导入器测试用例
│   ├── validator.test.js                 # 校验器测试用例
│   └── tree-builder.test.js              # 树生成器测试用例
├── docs/                                 # 项目文档目录
│   ├── getting-started.md                # 入门指南
│   ├── data-format.md                    # 数据格式规范
│   ├── directory-config.md               # 目录树配置说明
│   ├── api-reference.md                  # API 接口文档
│   ├── deployment.md                     # 生产环境部署指南
│   └── faq.md                            # 常见问题集合
├── scripts/                              # 构建与运维脚本
│   ├── build-index.js                    # 索引构建脚本
│   ├── export-csv.js                     # CSV 导出脚本
│   └── health-check.js                   # 链接可用性检查脚本
├── .env.example                          # 环境变量配置示例
├── .gitignore                            # Git 忽略文件列表
├── package.json                          # npm 项目配置文件
├── package-lock.json                     # 依赖锁定文件
├── README.md                             # 项目说明文档（本文件）
└── LICENSE                               # MIT 许可证文件
```

## 贡献指南

欢迎各类形式的贡献，包括但不限于新增功能、修复缺陷、完善文档以及提交新的 URL 批次数据。请遵循以下流程：

1. 复刻项目仓库：在 GitHub 上点击 Fork 按钮，将项目复刻至个人账户下，然后克隆本地副本。所有修改均应在个人分支中完成。

2. 创建功能分支：基于 main 分支创建新的特性分支，分支命名应遵循格式 `feature/简短描述` 或 `fix/问题编号`，例如 `feature/batch-8-import`。

3. 编写或修改代码：遵循项目现有的代码风格（使用 ESLint 配置），为新增逻辑编写对应的单元测试，并确保所有现有测试用例通过。若涉及数据格式变更，需同步更新 docs/ 目录下的相关文档。

4. 提交变更并推送：编写清晰的提交信息，格式为 `<类型>: <简短描述>`，类型可选 feat、fix、docs、test、refactor 等。推送分支至个人远程仓库。

5. 发起拉取请求：在 GitHub 上向原仓库的 main 分支发起 Pull Request，在描述中详细说明本次变更的目的、实现方式以及影响范围。项目维护者将在 3 个工作日内进行审核。

## 常见问题

Q: 启动开发服务器时提示端口 3000 已被占用，应如何解决？

A: 可通过修改 `.env` 文件中的 `PORT` 变量来指定其他可用端口，例如 `PORT=3001`。修改后重新执行 `npm run dev` 即可。若未创建 `.env` 文件，可复制 `.env.example` 并重命名后再进行编辑。

Q: 导入新的 URL 列表后，页面上的资源列表没有更新，是什么原因？

A: 导入操作仅将原始数据写入 `data/` 目录，并不会自动触发索引重建。您需要在导入后手动执行 `npm run build-index` 命令，该脚本会重新扫描所有批次数据并生成最新的目录树索引文件。索引生成后刷新页面即可看到更新。

Q: 如何批量标记某条 URL 为失效状态，而不将其从列表中删除？

A: 您可以在对应批次的 `metadata.json` 文件中，为特定 URL 添加 `"status": "invalid"` 字段，并可选填写 `"note"` 字段记录失效原因。项目前端渲染时会根据状态字段显示不同的视觉标识，但不会主动过滤掉该条目，确保数据完整性。

## 许可证

MIT

> 外链数量: 250 | 生成时间: 2026-08-24 23:40:21
