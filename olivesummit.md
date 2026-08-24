# WebLink Navigator

WebLink Navigator 是一个面向技术内容聚合与外部资源导航的开源工具集，专注于将大量分散的移动端新闻与资讯链接进行结构化梳理与可检索化展示。该项目主要服务于需要批量处理短链资源、建立可维护的外链索引表、以及构建轻量级资讯聚合页面的开发者与内容运营人员。

项目本身不依赖复杂的前端框架，采用纯静态 HTML 与 Shell 脚本实现资源的抓取、清洗与展示，适合部署在低成本的虚拟主机或对象存储环境中。通过约定的 URL 模式与本地缓存机制，WebLink Navigator 能够在不依赖数据库的前提下，实现千级外链资源的高效管理与快速访问。

## 功能概览

**批量链接导入**：支持从纯文本文件、CSV 或标准输入流中一次性导入大量 URL，自动去重并校验格式。

**自定义标签系统**：用户可为每条链接添加多个自定义标签，便于按主题、来源或日期进行多维度筛选。

**全文检索支持**：基于倒排索引的轻量级检索模块，支持对链接标题、描述及标签进行关键词匹配。

**静态页面生成**：内置模板引擎，可将链接数据渲染为适配移动端浏览的静态 HTML 页面，无需服务端动态解析。

**定时更新钩子**：提供 cron 友好的更新脚本，支持定期从远程数据源拉取最新链接并合并至本地索引。

**导出与备份**：支持将当前链接库导出为 JSON、CSV 或纯文本格式，便于迁移或二次加工。

**访问统计看板**：基于访问日志的简单统计模块，展示热门链接与高频标签，辅助内容评估。

## 应用场景

内容聚合站点运维：适用于需要定期更新外链列表的技术博客或资源导航站，通过脚本自动拉取指定来源的新链接，减少人工整理成本。

移动端资讯快照：针对移动端新闻链接（如本仓库所包含的 m.3g.uliejh.cn 系列），建立本地快照索引，避免因源站变动导致的链接失效问题。

开发测试数据集：为爬虫开发、链接可用性监控或 SEO 分析工具提供标准化的测试数据集，包含真实 URL 结构与多样化的路径模式。

个人知识库外链管理：作为个人知识管理系统的补充模块，统一管理散落在笔记或文档中的外部参考链接，提供统一的检索入口。

## 快速开始

以下命令演示了从克隆仓库到启动本地服务的完整流程。

```bash
# 克隆仓库
git clone https://github.com/weblink-navigator/weblink-navigator.git
cd weblink-navigator

# 安装依赖（基于 Debian/Ubuntu 环境）
./scripts/install_deps.sh

# 导入示例链接数据（包含本仓库提供的所有 URL）
./bin/weblink import --source ./data/sample_urls.txt

# 生成静态页面并启动本地预览服务
./bin/weblink build --output ./public
cd public && python3 -m http.server 8080
```

访问 http://localhost:8080 即可查看生成的导航页面。

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|---|---|---|
| Bash | 4.0 及以上 | 用于执行核心管理脚本与任务调度 |
| Python | 3.6 及以上 | 运行链接解析、索引构建与模板渲染模块 |
| grep | 3.0 及以上 | 用于链接格式校验与文本模式匹配 |
| curl | 7.50 及以上 | 用于远程资源拉取与状态检查 |
| sqlite3 | 3.20 及以上 | 可选依赖，用于启用持久化缓存与查询优化 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|---|---|---|
| 用户手册 | docs/user-guide.md | 如何导入链接、如何添加标签、如何生成页面 |
| 开发者指南 | docs/developer-guide.md | 模块划分、自定义解析器、扩展钩子 |
| 运维参考 | docs/operations.md | 定时任务配置、日志轮转、性能调优 |
| 设计说明 | docs/design.md | 数据模型、索引策略、静态生成原理 |

## 资源列表

- http://m.3g.uliejh.cn/nnews/31417.htm
- http://m.3g.uliejh.cn/nnews/7377900.htm
- http://m.3g.uliejh.cn/nnews/4609.htm
- http://m.3g.uliejh.cn/nnews/417243.htm
- http://m.3g.uliejh.cn/nnews/9292.htm
- http://m.3g.uliejh.cn/nnews/4901.htm
- http://m.3g.uliejh.cn/nnews/300697.htm
- http://m.3g.uliejh.cn/nnews/137488.htm
- http://m.3g.uliejh.cn/nnews/463979.htm
- http://m.3g.uliejh.cn/nnews/3333.htm
- http://m.3g.uliejh.cn/nnews/0114.htm
- http://m.3g.uliejh.cn/nnews/53459.htm
- http://m.3g.uliejh.cn/nnews/0300598.htm
- http://m.3g.uliejh.cn/nnews/214416.htm
- http://m.3g.uliejh.cn/nnews/9013997.htm
- http://m.3g.uliejh.cn/nnews/7367.htm
- http://m.3g.uliejh.cn/nnews/8647087.htm
- http://m.3g.uliejh.cn/nnews/8123034.htm
- http://m.3g.uliejh.cn/nnews/8557.htm
- http://m.3g.uliejh.cn/nnews/7320.htm
- http://m.3g.uliejh.cn/nnews/7667.htm
- http://m.3g.uliejh.cn/nnews/8939433.htm
- http://m.3g.uliejh.cn/nnews/9267.htm
- http://m.3g.uliejh.cn/nnews/129470.htm
- http://m.3g.uliejh.cn/nnews/734776.htm
- http://m.3g.uliejh.cn/nnews/768321.htm
- http://m.3g.uliejh.cn/nnews/5566257.htm
- http://m.3g.uliejh.cn/nnews/762919.htm
- http://m.3g.uliejh.cn/nnews/303555.htm
- http://m.3g.uliejh.cn/nnews/741883.htm
- http://m.3g.uliejh.cn/nnews/8031.htm
- http://m.3g.uliejh.cn/nnews/8529.htm
- http://m.3g.uliejh.cn/nnews/475420.htm
- http://m.3g.uliejh.cn/nnews/478755.htm
- http://m.3g.uliejh.cn/nnews/2157602.htm
- http://m.3g.uliejh.cn/nnews/4277.htm
- http://m.3g.uliejh.cn/nnews/88422.htm
- http://m.3g.uliejh.cn/nnews/7427640.htm
- http://m.3g.uliejh.cn/nnews/15878.htm
- http://m.3g.uliejh.cn/nnews/05076.htm
- http://m.3g.uliejh.cn/nnews/2808.htm
- http://m.3g.uliejh.cn/nnews/73473.htm
- http://m.3g.uliejh.cn/nnews/647297.htm
- http://m.3g.uliejh.cn/nnews/8351660.htm
- http://m.3g.uliejh.cn/nnews/1865877.htm
- http://m.3g.uliejh.cn/nnews/2387.htm
- http://m.3g.uliejh.cn/nnews/570111.htm
- http://m.3g.uliejh.cn/nnews/589469.htm
- http://m.3g.uliejh.cn/nnews/261987.htm
- http://m.3g.uliejh.cn/nnews/10983.htm
- http://m.3g.uliejh.cn/nnews/6814.htm
- http://m.3g.uliejh.cn/nnews/0534.htm
- http://m.3g.uliejh.cn/nnews/6091.htm
- http://m.3g.uliejh.cn/nnews/0354.htm
- http://m.3g.uliejh.cn/nnews/31908.htm
- http://m.3g.uliejh.cn/nnews/0053.htm
- http://m.3g.uliejh.cn/nnews/4125.htm
- http://m.3g.uliejh.cn/nnews/617872.htm
- http://m.3g.uliejh.cn/nnews/7523664.htm
- http://m.3g.uliejh.cn/nnews/8961536.htm
- http://m.3g.uliejh.cn/nnews/84430.htm
- http://m.3g.uliejh.cn/nnews/0207.htm
- http://m.3g.uliejh.cn/nnews/533153.htm
- http://m.3g.uliejh.cn/nnews/6407723.htm
- http://m.3g.uliejh.cn/nnews/687268.htm
- http://m.3g.uliejh.cn/nnews/1380.htm
- http://m.3g.uliejh.cn/nnews/9507429.htm
- http://m.3g.uliejh.cn/nnews/016791.htm
- http://m.3g.uliejh.cn/nnews/011681.htm
- http://m.3g.uliejh.cn/nnews/547223.htm
- http://m.3g.uliejh.cn/nnews/907090.htm
- http://m.3g.uliejh.cn/nnews/1451.htm
- http://m.3g.uliejh.cn/nnews/184511.htm
- http://m.3g.uliejh.cn/nnews/124661.htm
- http://m.3g.uliejh.cn/nnews/0501.htm
- http://m.3g.uliejh.cn/nnews/84848.htm
- http://m.3g.uliejh.cn/nnews/59679.htm
- http://m.3g.uliejh.cn/nnews/8251694.htm
- http://m.3g.uliejh.cn/nnews/9065271.htm
- http://m.3g.uliejh.cn/nnews/3026810.htm
- http://m.3g.uliejh.cn/nnews/105368.htm
- http://m.3g.uliejh.cn/nnews/68804.htm
- http://m.3g.uliejh.cn/nnews/7804655.htm
- http://m.3g.uliejh.cn/nnews/3807455.htm
- http://m.3g.uliejh.cn/nnews/86709.htm
- http://m.3g.uliejh.cn/nnews/155442.htm
- http://m.3g.uliejh.cn/nnews/836532.htm
- http://m.3g.uliejh.cn/nnews/8081703.htm
- http://m.3g.uliejh.cn/nnews/8642044.htm
- http://m.3g.uliejh.cn/nnews/6319160.htm
- http://m.3g.uliejh.cn/nnews/7311589.htm
- http://m.3g.uliejh.cn/nnews/4358.htm
- http://m.3g.uliejh.cn/nnews/36407.htm
- http://m.3g.uliejh.cn/nnews/35634.htm
- http://m.3g.uliejh.cn/nnews/365808.htm
- http://m.3g.uliejh.cn/nnews/9449.htm
- http://m.3g.uliejh.cn/nnews/79268.htm
- http://m.3g.uliejh.cn/nnews/827896.htm
- http://m.3g.uliejh.cn/nnews/627771.htm
- http://m.3g.uliejh.cn/nnews/89074.htm
- http://m.3g.uliejh.cn/nnews/5180475.htm
- http://m.3g.uliejh.cn/nnews/8988795.htm
- http://m.3g.uliejh.cn/nnews/8555681.htm
- http://m.3g.uliejh.cn/nnews/2944904.htm
- http://m.3g.uliejh.cn/nnews/2266.htm
- http://m.3g.uliejh.cn/nnews/3392.htm
- http://m.3g.uliejh.cn/nnews/3745499.htm
- http://m.3g.uliejh.cn/nnews/0382098.htm
- http://m.3g.uliejh.cn/nnews/81888.htm
- http://m.3g.uliejh.cn/nnews/4515.htm
- http://m.3g.uliejh.cn/nnews/1502.htm
- http://m.3g.uliejh.cn/nnews/727468.htm
- http://m.3g.uliejh.cn/nnews/9497955.htm
- http://m.3g.uliejh.cn/nnews/7417.htm
- http://m.3g.uliejh.cn/nnews/3147368.htm
- http://m.3g.uliejh.cn/nnews/9666693.htm
- http://m.3g.uliejh.cn/nnews/523619.htm
- http://m.3g.uliejh.cn/nnews/8270.htm
- http://m.3g.uliejh.cn/nnews/7039.htm
- http://m.3g.uliejh.cn/nnews/7271173.htm
- http://m.3g.uliejh.cn/nnews/7111365.htm
- http://m.3g.uliejh.cn/nnews/6191.htm
- http://m.3g.uliejh.cn/nnews/8644.htm
- http://m.3g.uliejh.cn/nnews/332189.htm
- http://m.3g.uliejh.cn/nnews/641874.htm
- http://m.3g.uliejh.cn/nnews/7849.htm
- http://m.3g.uliejh.cn/nnews/6177394.htm
- http://m.3g.uliejh.cn/nnews/80214.htm
- http://m.3g.uliejh.cn/nnews/1082556.htm
- http://m.3g.uliejh.cn/nnews/70730.htm
- http://m.3g.uliejh.cn/nnews/76104.htm
- http://m.3g.uliejh.cn/nnews/13874.htm
- http://m.3g.uliejh.cn/nnews/7611.htm
- http://m.3g.uliejh.cn/nnews/995761.htm
- http://m.3g.uliejh.cn/nnews/587883.htm
- http://m.3g.uliejh.cn/nnews/95734.htm
- http://m.3g.uliejh.cn/nnews/299358.htm
- http://m.3g.uliejh.cn/nnews/78114.htm
- http://m.3g.uliejh.cn/nnews/888882.htm
- http://m.3g.uliejh.cn/nnews/8135.htm
- http://m.3g.uliejh.cn/nnews/83193.htm
- http://m.3g.uliejh.cn/nnews/88749.htm
- http://m.3g.uliejh.cn/nnews/5353.htm
- http://m.3g.uliejh.cn/nnews/60471.htm
- http://m.3g.uliejh.cn/nnews/452857.htm
- http://m.3g.uliejh.cn/nnews/17546.htm
- http://m.3g.uliejh.cn/nnews/4517743.htm
- http://m.3g.uliejh.cn/nnews/258845.htm
- http://m.3g.uliejh.cn/nnews/9973.htm
- http://m.3g.uliejh.cn/nnews/3081792.htm
- http://m.3g.uliejh.cn/nnews/5160.htm
- http://m.3g.uliejh.cn/nnews/8141295.htm
- http://m.3g.uliejh.cn/nnews/845404.htm
- http://m.3g.uliejh.cn/nnews/532334.htm
- http://m.3g.uliejh.cn/nnews/0117.htm
- http://m.3g.uliejh.cn/nnews/688754.htm
- http://m.3g.uliejh.cn/nnews/9459.htm
- http://m.3g.uliejh.cn/nnews/013548.htm
- http://m.3g.uliejh.cn/nnews/5272733.htm
- http://m.3g.uliejh.cn/nnews/0527812.htm
- http://m.3g.uliejh.cn/nnews/6500.htm
- http://m.3g.uliejh.cn/nnews/48451.htm
- http://m.3g.uliejh.cn/nnews/8517.htm
- http://m.3g.uliejh.cn/nnews/555566.htm
- http://m.3g.uliejh.cn/nnews/25829.htm
- http://m.3g.uliejh.cn/nnews/2262.htm
- http://m.3g.uliejh.cn/nnews/5950557.htm
- http://m.3g.uliejh.cn/nnews/31166.htm
- http://m.3g.uliejh.cn/nnews/32694.htm
- http://m.3g.uliejh.cn/nnews/612620.htm
- http://m.3g.uliejh.cn/nnews/921500.htm
- http://m.3g.uliejh.cn/nnews/0694890.htm
- http://m.3g.uliejh.cn/nnews/296061.htm
- http://m.3g.uliejh.cn/nnews/683628.htm
- http://m.3g.uliejh.cn/nnews/4105.htm
- http://m.3g.uliejh.cn/nnews/7222469.htm
- http://m.3g.uliejh.cn/nnews/3053.htm
- http://m.3g.uliejh.cn/nnews/2776245.htm
- http://m.3g.uliejh.cn/nnews/1369655.htm
- http://m.3g.uliejh.cn/nnews/68746.htm
- http://m.3g.uliejh.cn/nnews/1482136.htm
- http://m.3g.uliejh.cn/nnews/16476.htm
- http://m.3g.uliejh.cn/nnews/265764.htm
- http://m.3g.uliejh.cn/nnews/4692375.htm
- http://m.3g.uliejh.cn/nnews/3338137.htm
- http://m.3g.uliejh.cn/nnews/79752.htm
- http://m.3g.uliejh.cn/nnews/2948940.htm
- http://m.3g.uliejh.cn/nnews/9429.htm
- http://m.3g.uliejh.cn/nnews/88107.htm
- http://m.3g.uliejh.cn/nnews/3196.htm
- http://m.3g.uliejh.cn/nnews/0023.htm
- http://m.3g.uliejh.cn/nnews/835994.htm
- http://m.3g.uliejh.cn/nnews/5184037.htm
- http://m.3g.uliejh.cn/nnews/9288428.htm
- http://m.3g.uliejh.cn/nnews/51218.htm
- http://m.3g.uliejh.cn/nnews/3392476.htm
- http://m.3g.uliejh.cn/nnews/8471998.htm
- http://m.3g.uliejh.cn/nnews/17553.htm
- http://m.3g.uliejh.cn/nnews/55821.htm
- http://m.3g.uliejh.cn/nnews/5983.htm
- http://m.3g.uliejh.cn/nnews/849285.htm
- http://m.3g.uliejh.cn/nnews/4367675.htm
- http://m.3g.uliejh.cn/nnews/905880.htm
- http://m.3g.uliejh.cn/nnews/8596.htm
- http://m.3g.uliejh.cn/nnews/7162281.htm
- http://m.3g.uliejh.cn/nnews/023813.htm
- http://m.3g.uliejh.cn/nnews/73293.htm
- http://m.3g.uliejh.cn/nnews/4284075.htm
- http://m.3g.uliejh.cn/nnews/4719.htm
- http://m.3g.uliejh.cn/nnews/43194.htm
- http://m.3g.uliejh.cn/nnews/1629879.htm
- http://m.3g.uliejh.cn/nnews/3390.htm
- http://m.3g.uliejh.cn/nnews/8082971.htm
- http://m.3g.uliejh.cn/nnews/4494.htm
- http://m.3g.uliejh.cn/nnews/183031.htm
- http://m.3g.uliejh.cn/nnews/468251.htm
- http://m.3g.uliejh.cn/nnews/0601857.htm
- http://m.3g.uliejh.cn/nnews/159964.htm
- http://m.3g.uliejh.cn/nnews/50065.htm
- http://m.3g.uliejh.cn/nnews/55971.htm
- http://m.3g.uliejh.cn/nnews/5109.htm
- http://m.3g.uliejh.cn/nnews/404691.htm
- http://m.3g.uliejh.cn/nnews/17851.htm
- http://m.3g.uliejh.cn/nnews/943024.htm
- http://m.3g.uliejh.cn/nnews/9599.htm
- http://m.3g.uliejh.cn/nnews/9223.htm
- http://m.3g.uliejh.cn/nnews/8346.htm
- http://m.3g.uliejh.cn/nnews/9229.htm
- http://m.3g.uliejh.cn/nnews/56466.htm
- http://m.3g.uliejh.cn/nnews/85187.htm
- http://m.3g.uliejh.cn/nnews/039185.htm
- http://m.3g.uliejh.cn/nnews/6453.htm
- http://m.3g.uliejh.cn/nnews/824706.htm
- http://m.3g.uliejh.cn/nnews/45293.htm
- http://m.3g.uliejh.cn/nnews/90130.htm
- http://m.3g.uliejh.cn/nnews/56756.htm
- http://m.3g.uliejh.cn/nnews/443061.htm
- http://m.3g.uliejh.cn/nnews/0158189.htm
- http://m.3g.uliejh.cn/nnews/93062.htm
- http://m.3g.uliejh.cn/nnews/96145.htm
- http://m.3g.uliejh.cn/nnews/2833888.htm
- http://m.3g.uliejh.cn/nnews/7282.htm
- http://m.3g.uliejh.cn/nnews/15674.htm
- http://m.3g.uliejh.cn/nnews/1152.htm
- http://m.3g.uliejh.cn/nnews/1654.htm
- http://m.3g.uliejh.cn/nnews/1488465.htm
- http://m.3g.uliejh.cn/nnews/33709.htm
- http://m.3g.uliejh.cn/nnews/36339.htm
- http://m.3g.uliejh.cn/nnews/265467.htm
- http://m.3g.uliejh.cn/nnews/9208259.htm

## 项目结构

```
weblink-navigator/
├── bin/                            # 可执行脚本入口
│   ├── weblink                     # 主命令行工具（Python 包装器）
│   └── weblink.bat                 # Windows 平台包装脚本
├── lib/                            # 核心库代码
│   ├── core/                       # 链接管理核心模块
│   │   ├── indexer.py              # 倒排索引构建与检索
│   │   ├── parser.py               # URL 解析与格式标准化
│   │   └── storage.py              # SQLite 与 JSON 存储适配器
│   ├── renderer/                   # 静态页面渲染引擎
│   │   ├── template.py             # Jinja2 模板包装
│   │   └── theme_default/          # 默认主题资源（CSS/JS）
│   └── utils/                      # 通用辅助函数
│       ├── fetcher.py              # 远程资源抓取与超时控制
│       └── logger.py               # 分级日志记录器
├── scripts/                        # 运维与辅助脚本
│   ├── install_deps.sh             # 依赖安装脚本（apt/pip）
│   ├── cron_update.sh              # 定时更新任务示例
│   └── migrate_v1_to_v2.py         # 数据迁移工具
├── data/                           # 数据目录
│   ├── sample_urls.txt             # 示例链接数据（本仓库资源）
│   ├── index.db                    # SQLite 索引文件（生成后出现）
│   └── cache/                      # 远程资源缓存目录
├── public/                         # 生成的静态页面输出目录
│   ├── index.html                  # 导航首页
│   ├── tags/                       # 按标签聚合的页面
│   └── assets/                     # 静态资源（CSS/JS/图片）
├── tests/                          # 单元测试与集成测试
│   ├── test_parser.py              # 解析器测试用例
│   ├── test_indexer.py             # 索引器测试用例
│   └── fixtures/                   # 测试固定数据
├── docs/                           # 项目文档
│   ├── user-guide.md               # 用户手册
│   ├── developer-guide.md          # 开发者指南
│   ├── operations.md               # 运维参考
│   └── design.md                   # 设计说明
├── .github/                        # GitHub 工作流配置
│   └── workflows/                  # CI 流水线（测试与构建）
├── README.md                       # 项目介绍（本文件）
├── LICENSE                         # MIT 许可证
├── requirements.txt                # Python 依赖列表
└── setup.py                        # 打包与分发配置
```

## 贡献指南

1. 在 GitHub 仓库页面点击 Fork 按钮，将项目复制到个人账户下，并克隆至本地开发环境。

2. 创建新的功能分支，分支名称遵循 `feature/简短描述` 或 `fix/问题编号` 格式，避免在主干分支直接修改。

3. 编写或修改代码后，运行测试套件确保现有功能未被破坏，测试命令为 `python -m pytest tests/`。

4. 提交代码前执行代码格式化工具（如 `black` 与 `isort`），保持代码风格与项目现有风格一致。

5. 发起 Pull Request 至主干分支，并在描述中清晰说明改动内容、关联问题及测试覆盖情况。

## 常见问题

**问：导入大量链接时内存占用过高怎么办？**

答：对于超过 5000 条的链接导入，建议启用批处理模式。使用 `--batch-size 200` 参数将导入操作分批次提交，每批处理 200 条后提交事务并释放内存。同时可开启 `--no-cache` 选项禁用临时缓存，进一步降低内存开销。

**问：如何自定义生成的静态页面样式？**

答：项目使用 Jinja2 模板引擎渲染页面，所有模板文件位于 `lib/renderer/theme_default/` 目录下。您可以复制该目录并重命名为自定义主题名称，然后修改其中的 HTML 与 CSS 文件。在构建时通过 `--theme 自定义主题名称` 指定即可生效。

**问：链接失效或无法访问时，系统如何处理？**

答：系统在导入阶段不会主动探测链接可用性，以避免网络延迟影响导入速度。但在构建静态页面时，可通过 `--check-links` 选项启用链接状态检查，失效链接会在页面中以特殊样式标记，同时生成一份 `broken_links.txt` 报告文件供后续处理。

## 许可证

MIT

> 外链数量: 250 | 生成时间: 2026-08-24 23:40:21
