# SNews Link Aggregator

SNews Link Aggregator 是一个面向技术内容聚合与结构化外链管理的开源工具集。该项目定位于为开发者、技术博主以及信息整理人员提供一套轻量级、可扩展的链接收录与展示方案，能够将分散的、非结构化的 URL 资源转化为具有清晰分类、可检索、可追溯的静态站点或文档库。

本项目并非一个通用的爬虫框架或社交平台，而是专注于解决“海量无序外链的规范化存储与友好呈现”这一具体问题。其核心目标用户包括需要维护技术周刊的编辑、搭建个人知识库的工程师、以及需要批量管理项目参考链接的团队。通过本项目提供的模板与脚本，用户可以快速启动一个包含完整 README 导航、资源清单、项目结构说明和贡献流程的外链中心。

## 功能概览

批量链接导入与校验 支持从纯文本文件、CSV 或直接粘贴的原始数据中批量导入 URL，并在导入时自动执行协议一致性检查、域名合法性校验以及重复项过滤。

结构化目录树生成 根据链接的来源域名、文件类型或用户自定义标签，自动生成符合项目规范的 ASCII 目录树，用于快速定位资源所属的模块或批次。

多维度资源列表渲染 将原始链接列表按照指定格式（每行一个 URL，不带额外标签或超链接语法）输出为可读性高的 Markdown 表格或列表，便于嵌入文档或站点页面。

依赖环境检测与配置向导 启动时自动检测运行环境所需的 Python 版本、依赖库及文件权限，并提供交互式配置向导，引导用户完成初始设置。

增量更新与版本追踪 支持对已收录的链接进行增量追加或移除操作，每次变更均会生成变更日志（CHANGELOG），便于回溯资源列表的演变历史。

静态站点导出 内置简单的模板引擎，可将所有资源列表与项目文档导出为静态 HTML 文件，适合部署到任意 Web 服务器或托管平台。

## 应用场景

技术周刊内容编排 编辑人员每周收集数十个技术文章、工具库或视频教程的链接，通过 SNews Link Aggregator 快速生成带编号、分类和简短注释的资源列表，并直接嵌入周刊发布流程。

个人知识库外链归档 开发者在阅读技术文档或参与开源项目时，积累了大量参考链接。使用本项目可按主题（如微服务、前端框架、数据库调优）将链接归档，并配合目录树快速检索。

团队项目文档外联管理 大型项目的 README 或 Wiki 中常需引用大量外部资源（规范文档、API 参考、依赖仓库）。本项目提供标准化的链接收录格式和更新流程，确保团队成员添加或更新外链时遵循统一规范。

开源项目资源导航站 开源社区维护者利用本项目构建项目周边的生态资源导航页，收录相关工具、插件、示例代码和教程，提升社区贡献者的入门效率。

## 快速开始

以下步骤适用于 Linux/macOS 及 Windows WSL 环境，需预先安装 Git 与 Python 3.8 及以上版本。

```bash
# 克隆项目仓库
git clone https://github.com/snews-io/link-aggregator.git
cd link-aggregator

# 创建并激活 Python 虚拟环境
python3 -m venv venv
source venv/bin/activate  # Windows 下使用 venv\Scripts\activate

# 安装核心依赖
pip install -r requirements.txt

# 执行初始化配置，生成默认的配置文件和目录结构
python scripts/init_project.py --batch 90/120

# 运行链接导入示例（将原始 URL 列表保存为 raw_links.txt 后执行）
python scripts/import_links.py --input raw_links.txt --output resources.md

# 启动本地预览服务（默认监听 8000 端口）
python -m http.server 8000
```

访问 http://localhost:8000 即可查看生成的资源导航页面。如需自定义样式或模板，请参考 `docs/customization.md`。

## 安装要求

| 依赖项 | 必需版本 | 说明 |
|--------|----------|------|
| Python | 3.8 至 3.11 | 核心运行环境，3.12 暂未全面测试 |
| Git | 2.25 及以上 | 用于克隆仓库及版本管理 |
| pip | 20.0 及以上 | Python 包管理器，用于安装依赖 |
| virtualenv | 可选 | 推荐使用 venv 模块（Python 内置） |
| Markdown | 3.3 及以上 | 用于解析和渲染 Markdown 文档结构 |
| PyYAML | 5.4 及以上 | 用于读取配置文件中的分类规则与元数据 |
| requests | 2.26 及以上 | 用于链接可达性校验（可选，默认启用） |
| beautifulsoup4 | 4.10 及以上 | 用于解析 HTML 页面标题以生成链接注释（可选） |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|------|------|------------|
| 入门指南 | `docs/getting-started.md` | 如何安装、初始化并运行第一个链接导入任务？ |
| 配置参考 | `docs/configuration.md` | 配置文件中的各字段含义是什么？如何自定义分类规则和输出格式？ |
| 命令行工具 | `docs/cli.md` | 有哪些可用的 CLI 命令？每个命令的参数和选项如何使用？ |
| 模板开发 | `docs/template-dev.md` | 如何修改默认的 HTML 模板或创建新的输出样式？ |
| 常见工作流 | `docs/workflows.md` | 如何批量更新链接、处理失效 URL 或合并多个资源列表？ |
| API 接口 | `docs/api.md` | 是否提供程序化调用的接口？如何在自己的脚本中引用核心功能？ |
| 贡献规范 | `CONTRIBUTING.md` | 提交代码或文档时需遵循哪些流程和代码风格？ |

## 资源列表

- http://m.blog.uliejh.cn/snews/7245798.htm
- http://m.blog.uliejh.cn/snews/67202.htm
- http://m.blog.uliejh.cn/snews/491612.htm
- http://m.blog.uliejh.cn/snews/1284.htm
- http://m.blog.uliejh.cn/snews/447767.htm
- http://m.blog.uliejh.cn/snews/7878.htm
- http://m.blog.uliejh.cn/snews/690068.htm
- http://m.blog.uliejh.cn/snews/0927.htm
- http://m.blog.uliejh.cn/snews/8557451.htm
- http://m.blog.uliejh.cn/snews/6793051.htm
- http://m.blog.uliejh.cn/snews/252498.htm
- http://m.blog.uliejh.cn/snews/209096.htm
- http://m.blog.uliejh.cn/snews/356920.htm
- http://m.blog.uliejh.cn/snews/2912.htm
- http://m.blog.uliejh.cn/snews/0438.htm
- http://m.blog.uliejh.cn/snews/371310.htm
- http://m.blog.uliejh.cn/snews/756013.htm
- http://m.blog.uliejh.cn/snews/171832.htm
- http://m.blog.uliejh.cn/snews/7689206.htm
- http://m.blog.uliejh.cn/snews/7818.htm
- http://m.blog.uliejh.cn/snews/5646.htm
- http://m.blog.uliejh.cn/snews/0118013.htm
- http://m.blog.uliejh.cn/snews/92726.htm
- http://m.blog.uliejh.cn/snews/6122.htm
- http://m.blog.uliejh.cn/snews/2732.htm
- http://m.blog.uliejh.cn/snews/095396.htm
- http://m.blog.uliejh.cn/snews/6924016.htm
- http://m.blog.uliejh.cn/snews/3060956.htm
- http://m.blog.uliejh.cn/snews/6595794.htm
- http://m.blog.uliejh.cn/snews/5617.htm
- http://m.blog.uliejh.cn/snews/1926539.htm
- http://m.blog.uliejh.cn/snews/7045.htm
- http://m.blog.uliejh.cn/snews/1027591.htm
- http://m.blog.uliejh.cn/snews/3244.htm
- http://m.blog.uliejh.cn/snews/697501.htm
- http://m.blog.uliejh.cn/snews/638447.htm
- http://m.blog.uliejh.cn/snews/8833480.htm
- http://m.blog.uliejh.cn/snews/769726.htm
- http://m.blog.uliejh.cn/snews/345460.htm
- http://m.blog.uliejh.cn/snews/1956.htm
- http://m.blog.uliejh.cn/snews/0414972.htm
- http://m.blog.uliejh.cn/snews/9412398.htm
- http://m.blog.uliejh.cn/snews/3744063.htm
- http://m.blog.uliejh.cn/snews/5527.htm
- http://m.blog.uliejh.cn/snews/2261.htm
- http://m.blog.uliejh.cn/snews/8207929.htm
- http://m.blog.uliejh.cn/snews/2492.htm
- http://m.blog.uliejh.cn/snews/3021.htm
- http://m.blog.uliejh.cn/snews/80526.htm
- http://m.blog.uliejh.cn/snews/8755988.htm
- http://m.blog.uliejh.cn/snews/57083.htm
- http://m.blog.uliejh.cn/snews/347773.htm
- http://m.blog.uliejh.cn/snews/081759.htm
- http://m.blog.uliejh.cn/snews/241352.htm
- http://m.blog.uliejh.cn/snews/842341.htm
- http://m.blog.uliejh.cn/snews/4247251.htm
- http://m.blog.uliejh.cn/snews/452492.htm
- http://m.blog.uliejh.cn/snews/07079.htm
- http://m.blog.uliejh.cn/snews/439904.htm
- http://m.blog.uliejh.cn/snews/61324.htm
- http://m.blog.uliejh.cn/snews/471160.htm
- http://m.blog.uliejh.cn/snews/0702217.htm
- http://m.blog.uliejh.cn/snews/0232494.htm
- http://m.blog.uliejh.cn/snews/8519489.htm
- http://m.blog.uliejh.cn/snews/545118.htm
- http://m.blog.uliejh.cn/snews/33430.htm
- http://m.blog.uliejh.cn/snews/91547.htm
- http://m.blog.uliejh.cn/snews/8727115.htm
- http://m.blog.uliejh.cn/snews/4749461.htm
- http://m.blog.uliejh.cn/snews/281580.htm
- http://m.blog.uliejh.cn/snews/82795.htm
- http://m.blog.uliejh.cn/snews/655093.htm
- http://m.blog.uliejh.cn/snews/9752208.htm
- http://m.blog.uliejh.cn/snews/10856.htm
- http://m.blog.uliejh.cn/snews/7252.htm
- http://m.blog.uliejh.cn/snews/9094904.htm
- http://m.blog.uliejh.cn/snews/056989.htm
- http://m.blog.uliejh.cn/snews/2549.htm
- http://m.blog.uliejh.cn/snews/98169.htm
- http://m.blog.uliejh.cn/snews/1688.htm
- http://m.blog.uliejh.cn/snews/2084.htm
- http://m.blog.uliejh.cn/snews/3670.htm
- http://m.blog.uliejh.cn/snews/0791.htm
- http://m.blog.uliejh.cn/snews/33342.htm
- http://m.blog.uliejh.cn/snews/5217.htm
- http://m.blog.uliejh.cn/snews/5264895.htm
- http://m.blog.uliejh.cn/snews/6281.htm
- http://m.blog.uliejh.cn/snews/725138.htm
- http://m.blog.uliejh.cn/snews/865879.htm
- http://m.blog.uliejh.cn/snews/4650988.htm
- http://m.blog.uliejh.cn/snews/5490480.htm
- http://m.blog.uliejh.cn/snews/4143.htm
- http://m.blog.uliejh.cn/snews/8250.htm
- http://m.blog.uliejh.cn/snews/59126.htm
- http://m.blog.uliejh.cn/snews/2680.htm
- http://m.blog.uliejh.cn/snews/53951.htm
- http://m.blog.uliejh.cn/snews/030740.htm
- http://m.blog.uliejh.cn/snews/6332281.htm
- http://m.blog.uliejh.cn/snews/2121988.htm
- http://m.blog.uliejh.cn/snews/80290.htm
- http://m.blog.uliejh.cn/snews/9682.htm
- http://m.blog.uliejh.cn/snews/7739.htm
- http://m.blog.uliejh.cn/snews/9295.htm
- http://m.blog.uliejh.cn/snews/504367.htm
- http://m.blog.uliejh.cn/snews/8235556.htm
- http://m.blog.uliejh.cn/snews/8357.htm
- http://m.blog.uliejh.cn/snews/82664.htm
- http://m.blog.uliejh.cn/snews/973313.htm
- http://m.blog.uliejh.cn/snews/4112.htm
- http://m.blog.uliejh.cn/snews/868134.htm
- http://m.blog.uliejh.cn/snews/6645389.htm
- http://m.blog.uliejh.cn/snews/419521.htm
- http://m.blog.uliejh.cn/snews/91655.htm
- http://m.blog.uliejh.cn/snews/49192.htm
- http://m.blog.uliejh.cn/snews/028696.htm
- http://m.blog.uliejh.cn/snews/85327.htm
- http://m.blog.uliejh.cn/snews/8485754.htm
- http://m.blog.uliejh.cn/snews/3287295.htm
- http://m.blog.uliejh.cn/snews/0022962.htm
- http://m.blog.uliejh.cn/snews/3945019.htm
- http://m.blog.uliejh.cn/snews/5733302.htm
- http://m.blog.uliejh.cn/snews/7364.htm
- http://m.blog.uliejh.cn/snews/681501.htm
- http://m.blog.uliejh.cn/snews/5577.htm
- http://m.blog.uliejh.cn/snews/20109.htm
- http://m.blog.uliejh.cn/snews/5848184.htm
- http://m.blog.uliejh.cn/snews/1273462.htm
- http://m.blog.uliejh.cn/snews/2308579.htm
- http://m.blog.uliejh.cn/snews/2660.htm
- http://m.blog.uliejh.cn/snews/2596716.htm
- http://m.blog.uliejh.cn/snews/857864.htm
- http://m.blog.uliejh.cn/snews/2462.htm
- http://m.blog.uliejh.cn/snews/217098.htm
- http://m.blog.uliejh.cn/snews/09124.htm
- http://m.blog.uliejh.cn/snews/90346.htm
- http://m.blog.uliejh.cn/snews/045374.htm
- http://m.blog.uliejh.cn/snews/6949388.htm
- http://m.blog.uliejh.cn/snews/134227.htm
- http://m.blog.uliejh.cn/snews/9459.htm
- http://m.blog.uliejh.cn/snews/93491.htm
- http://m.blog.uliejh.cn/snews/528329.htm
- http://m.blog.uliejh.cn/snews/82197.htm
- http://m.blog.uliejh.cn/snews/305341.htm
- http://m.blog.uliejh.cn/snews/8228257.htm
- http://m.blog.uliejh.cn/snews/4601942.htm
- http://m.blog.uliejh.cn/snews/5563681.htm
- http://m.blog.uliejh.cn/snews/016462.htm
- http://m.blog.uliejh.cn/snews/6782075.htm
- http://m.blog.uliejh.cn/snews/674669.htm
- http://m.blog.uliejh.cn/snews/9820352.htm
- http://m.blog.uliejh.cn/snews/47133.htm
- http://m.blog.uliejh.cn/snews/1938.htm
- http://m.blog.uliejh.cn/snews/28023.htm
- http://m.blog.uliejh.cn/snews/707275.htm
- http://m.blog.uliejh.cn/snews/73353.htm
- http://m.blog.uliejh.cn/snews/4084.htm
- http://m.blog.uliejh.cn/snews/19942.htm
- http://m.blog.uliejh.cn/snews/852803.htm
- http://m.blog.uliejh.cn/snews/3427.htm
- http://m.blog.uliejh.cn/snews/0037347.htm
- http://m.blog.uliejh.cn/snews/866397.htm
- http://m.blog.uliejh.cn/snews/29031.htm
- http://m.blog.uliejh.cn/snews/8291.htm
- http://m.blog.uliejh.cn/snews/1936.htm
- http://m.blog.uliejh.cn/snews/39549.htm
- http://m.blog.uliejh.cn/snews/4900650.htm
- http://m.blog.uliejh.cn/snews/155901.htm
- http://m.blog.uliejh.cn/snews/717774.htm
- http://m.blog.uliejh.cn/snews/759017.htm
- http://m.blog.uliejh.cn/snews/0384399.htm
- http://m.blog.uliejh.cn/snews/714831.htm
- http://m.blog.uliejh.cn/snews/1390.htm
- http://m.blog.uliejh.cn/snews/8229990.htm
- http://m.blog.uliejh.cn/snews/3736.htm
- http://m.blog.uliejh.cn/snews/1004572.htm
- http://m.blog.uliejh.cn/snews/0524.htm
- http://m.blog.uliejh.cn/snews/50744.htm
- http://m.blog.uliejh.cn/snews/4399.htm
- http://m.blog.uliejh.cn/snews/815097.htm
- http://m.blog.uliejh.cn/snews/3379.htm
- http://m.blog.uliejh.cn/snews/478188.htm
- http://m.blog.uliejh.cn/snews/1839.htm
- http://m.blog.uliejh.cn/snews/9113.htm
- http://m.blog.uliejh.cn/snews/29876.htm
- http://m.blog.uliejh.cn/snews/43831.htm
- http://m.blog.uliejh.cn/snews/14117.htm
- http://m.blog.uliejh.cn/snews/2288.htm
- http://m.blog.uliejh.cn/snews/654130.htm
- http://m.blog.uliejh.cn/snews/63998.htm
- http://m.blog.uliejh.cn/snews/63668.htm
- http://m.blog.uliejh.cn/snews/8398.htm
- http://m.blog.uliejh.cn/snews/8178.htm
- http://m.blog.uliejh.cn/snews/436359.htm
- http://m.blog.uliejh.cn/snews/247871.htm
- http://m.blog.uliejh.cn/snews/867349.htm
- http://m.blog.uliejh.cn/snews/731705.htm
- http://m.blog.uliejh.cn/snews/1184.htm
- http://m.blog.uliejh.cn/snews/7233.htm
- http://m.blog.uliejh.cn/snews/62420.htm
- http://m.blog.uliejh.cn/snews/27457.htm
- http://m.blog.uliejh.cn/snews/7755.htm
- http://m.blog.uliejh.cn/snews/43339.htm
- http://m.blog.uliejh.cn/snews/46648.htm
- http://m.blog.uliejh.cn/snews/69094.htm
- http://m.blog.uliejh.cn/snews/6039.htm
- http://m.blog.uliejh.cn/snews/53605.htm
- http://m.blog.uliejh.cn/snews/7505.htm
- http://m.blog.uliejh.cn/snews/428230.htm
- http://m.blog.uliejh.cn/snews/2586172.htm
- http://m.blog.uliejh.cn/snews/1061617.htm
- http://m.blog.uliejh.cn/snews/612775.htm
- http://m.blog.uliejh.cn/snews/2829.htm
- http://m.blog.uliejh.cn/snews/833027.htm
- http://m.blog.uliejh.cn/snews/6806644.htm
- http://m.blog.uliejh.cn/snews/971167.htm
- http://m.blog.uliejh.cn/snews/1748.htm
- http://m.blog.uliejh.cn/snews/526933.htm
- http://m.blog.uliejh.cn/snews/3308.htm
- http://m.blog.uliejh.cn/snews/5458560.htm
- http://m.blog.uliejh.cn/snews/1113.htm
- http://m.blog.uliejh.cn/snews/379338.htm
- http://m.blog.uliejh.cn/snews/1073.htm
- http://m.blog.uliejh.cn/snews/8711896.htm
- http://m.blog.uliejh.cn/snews/864121.htm
- http://m.blog.uliejh.cn/snews/3456747.htm
- http://m.blog.uliejh.cn/snews/4989091.htm
- http://m.blog.uliejh.cn/snews/520308.htm
- http://m.blog.uliejh.cn/snews/853497.htm
- http://m.blog.uliejh.cn/snews/593627.htm
- http://m.blog.uliejh.cn/snews/31245.htm
- http://m.blog.uliejh.cn/snews/777944.htm
- http://m.blog.uliejh.cn/snews/6438047.htm
- http://m.blog.uliejh.cn/snews/7817.htm
- http://m.blog.uliejh.cn/snews/725623.htm
- http://m.blog.uliejh.cn/snews/0302798.htm
- http://m.blog.uliejh.cn/snews/425483.htm
- http://m.blog.uliejh.cn/snews/06990.htm
- http://m.blog.uliejh.cn/snews/59683.htm
- http://m.blog.uliejh.cn/snews/3090.htm
- http://m.blog.uliejh.cn/snews/116129.htm
- http://m.blog.uliejh.cn/snews/027129.htm
- http://m.blog.uliejh.cn/snews/4924344.htm
- http://m.blog.uliejh.cn/snews/52388.htm
- http://m.blog.uliejh.cn/snews/7625111.htm
- http://m.blog.uliejh.cn/snews/6617.htm
- http://m.blog.uliejh.cn/snews/692931.htm
- http://m.blog.uliejh.cn/snews/3424.htm
- http://m.blog.uliejh.cn/snews/57363.htm
- http://m.blog.uliejh.cn/snews/23517.htm
- http://m.blog.uliejh.cn/snews/8359.htm

## 项目结构

```
link-aggregator/
├── README.md                     # 项目总览与入口文档
├── CONTRIBUTING.md               # 贡献者指南与行为准则
├── LICENSE                       # MIT 许可证文件
├── requirements.txt              # Python 依赖列表（生产环境）
├── requirements-dev.txt          # 开发与测试额外依赖
├── config/
│   ├── default.yaml              # 默认配置（分类规则、输出路径）
│   └── custom.yaml.example       # 用户自定义配置示例
├── data/
│   ├── raw/                      # 存放原始输入文件（如 raw_links.txt）
│   ├── parsed/                   # 解析后的结构化链接数据（JSON）
│   └── cache/                    # 请求缓存与校验记录
├── docs/                         # 完整文档目录
│   ├── getting-started.md
│   ├── configuration.md
│   ├── cli.md
│   ├── template-dev.md
│   ├── workflows.md
│   ├── api.md
│   └── customization.md
├── scripts/                      # 核心可执行脚本
│   ├── init_project.py           # 项目初始化与批处理设置
│   ├── import_links.py           # 链接导入与解析主程序
│   ├── validate_links.py         # 链接可达性与格式校验
│   ├── export_static.py          # 导出为静态 HTML 站点
│   └── utils.py                  # 通用工具函数集合
├── templates/                    # Jinja2/HTML 模板
│   ├── base.html
│   ├── index.html
│   └── resource_list.html
├── tests/                        # 单元测试与集成测试
│   ├── test_import.py
│   ├── test_validate.py
│   └── fixtures/                 # 测试用样本数据
└── output/                       # 生成的文档与站点输出目录（自动创建）
    ├── resources.md
    └── static/
```

## 贡献指南

我们欢迎各类贡献，包括但不限于代码优化、文档改进、新增功能提案和问题反馈。请遵循以下流程以确保协作顺畅：

1. 查阅问题追踪器 访问 GitHub Issues 页面，查看现有待办事项或报告新问题。提交新 Issue 时请使用提供的模板，并清晰描述复现步骤、预期行为与实际行为。

2. 派生仓库并创建特性分支 从主仓库派生副本到个人账户，然后基于 main 分支创建新的特性分支，分支命名建议使用 `feature/描述` 或 `fix/描述` 格式。

3. 编写或修改代码并添加测试 确保所有新增功能均包含对应的单元测试，测试覆盖率不低于 80%。运行 `pytest tests/` 确认所有测试通过，并执行 `flake8 scripts/` 检查代码风格。

4. 更新相关文档 若变更涉及命令行参数、配置文件字段或工作流程，必须同步更新 `docs/` 目录下对应的文档文件，并在 `CHANGELOG.md` 中记录主要变更点。

5. 提交拉取请求 推送分支到派生仓库，然后向主仓库提交 Pull Request。PR 描述中需引用关联的 Issue 编号，并简要说明变更内容、测试结果和文档更新情况。等待维护者审核与合并。

## 常见问题

Q: 导入链接时提示“协议不受支持”或“URL 格式无效”，应如何解决？

A: 本项目严格遵循用户提供的 URL 原样输出，因此所有链接均保持原始协议（http 或 https）。若校验器报告格式错误，请检查链接是否包含多余空格、换行符或中文标点。建议使用纯文本编辑器保存原始数据，并确保每行仅包含一个 URL。对于非标准协议（如 ftp、file），校验器会跳过并记录警告，不影响其他链接导入。

Q: 如何更新已导入的链接列表？是否支持删除或修改特定条目？

A: 支持增量更新。您可以在 `data/raw/` 目录下创建一个新的输入文件（如 `update_20260824.txt`），仅包含新增或变更的链接。运行 `import_links.py --input update_20260824.txt --update` 即可追加新链接并覆盖现有链接的注释信息。若需删除链接，请在配置文件中指定 `exclude_list` 字段，列出需要移除的 URL 或 ID，重新运行导入脚本后系统会自动过滤。

Q: 静态站点导出后，部分链接显示为裸域名或路径不完整，如何确保所有超链接可点击？

A: 本项目的设计原则是“资源列表”部分严格按原始字符串输出，不进行任何自动超链接化或协议补全，以确保用户数据的绝对忠实呈现。在静态站点模板中，我们提供了两种渲染模式：列表模式（纯文本）和卡片模式（自动添加 `a` 标签）。您可以通过修改 `config/default.yaml` 中的 `render.mode` 字段切换为 `card`，此时系统会为每个链接生成可点击的锚点，但链接地址仍然使用原始 URL 字符串，不添加额外前缀或尾部斜杠。若使用列表模式，建议用户自行复制链接到浏览器地址栏访问。

## 许可证

MIT License

Copyright (c) 2026 SNews Link Aggregator Contributors

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

> 外链数量: 250 | 生成时间: 2026-08-24 23:40:21
