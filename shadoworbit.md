# WebLink Nexus

WebLink Nexus 是一个面向开发者、技术研究人员与信息聚合场景的轻量级外链资源汇总与导航系统。该项目定位于将分散在多个来源的资讯链接、技术文档入口与数据页面进行统一收录、分类展示与快速检索，帮助用户从大量原始 URL 中建立结构化的信息访问路径。目标用户包括运维工程师、技术调研人员、内容聚合平台运营者以及需要定期查阅特定信息来源的研发团队。

本项目不提供爬虫或自动化采集功能，而是作为人工筛选与整理后的链接索引层，以清晰的项目结构与文档体系呈现。通过静态化的资源清单与分类目录，用户可以获得稳定、可审查、可扩展的外部信息导航服务。WebLink Nexus 适用于内网部署、个人知识库外链管理以及小团队共享的参考资料库建设场景。

## 功能概览

**多层级分类索引** 系统根据资源主题和文件类型自动生成分类标签，支持按技术领域、内容格式、来源站点等多维度筛选定位。

**纯静态资源清单** 所有外链以明文列表形式维护在项目仓库中，无需数据库依赖，便于版本控制与内容审查。

**快速模糊检索** 内置基于文件名的关键词匹配功能，用户可通过资源编号或标题片段快速定位目标链接。

**原始链接保真展示** 严格保留用户提供的原始 URL 格式，不添加协议前缀、不更改域名大小写、不自动补全路径后缀。

**批量导入与校验** 支持通过标准文本格式批量新增资源链接，并提供重复项检测与格式合法性校验工具。

**响应式目录浏览** 适配桌面与移动端显示，在不同屏幕尺寸下均可获得清晰的资源列表浏览体验。

**标签关联推荐** 基于资源路径特征自动关联同主题或同来源的相关链接，辅助用户扩展信息发现范围。

## 应用场景

技术文档归档与快速查阅：技术团队可将日常参考的官方文档、博客教程、API 手册等外链统一录入 WebLink Nexus，按项目或技术栈分类，新成员入职时可快速获得完整的参考资料入口。

信息监控面板辅助：运维人员将监控系统、日志平台、状态仪表盘等管理后台地址集中管理，配合分类标签实现一键跳转，避免在收藏夹或聊天记录中反复查找。

内容聚合站点的原始素材管理：内容编辑或运营人员将选题相关的新闻源、数据报告页、行业分析文章等链接整理至系统，方便在撰写综述或策划专题时批量调用引用来源。

个人知识库外链中心：知识管理爱好者可将笔记中散落的引用链接剥离出来，统一存放在 WebLink Nexus 中，保持笔记正文的简洁性，同时保留完整的参考资料索引。

## 快速开始

以下命令适用于 Linux / macOS / Windows WSL 环境，若使用 Windows 原生命令行，请将 `cp` 替换为 `copy`，`/` 路径分隔符调整为 `\`。

```bash
# 克隆项目仓库
git clone https://github.com/weblink-nexus/weblink-nexus.git
cd weblink-nexus

# 安装依赖（Python 3.8+ 环境）
pip install -r requirements.txt

# 执行本地预览服务（默认监听 127.0.0.1:8080）
python serve.py --port 8080

# 若需要重新生成静态资源索引，运行
python build_index.py --input ./data/raw_links.txt --output ./data/index.json
```

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|---|---|---|
| Python | 3.8 及以上 | 核心运行环境，用于本地预览与索引构建 |
| pip | 20.0 及以上 | Python 包管理工具，用于安装依赖库 |
| git | 2.20 及以上 | 版本控制工具，用于克隆仓库与提交更新 |
| markdown | 3.3.0 及以上 | 用于将 README 与文档渲染为 HTML 预览 |
| pyyaml | 5.4.0 及以上 | 解析项目配置文件与元数据定义 |
| watchdog | 2.1.0 及以上 | 可选依赖，用于开发时自动重载预览服务 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|---|---|---|
| 用户手册 | docs/user-guide.md | 如何浏览资源列表、使用搜索功能、查看分类标签？ |
| 维护指南 | docs/maintainer-guide.md | 如何新增链接、修改分类、校验格式并提交变更？ |
| 部署参考 | docs/deployment.md | 如何将系统部署到生产服务器或内网静态托管环境？ |
| 设计说明 | docs/design.md | 项目目录结构、索引生成逻辑与前端交互的设计依据是什么？ |

## 资源列表

- http://m.3g.uliejh.cn/nnews/44544.htm
- http://m.3g.uliejh.cn/nnews/55974.htm
- http://m.3g.uliejh.cn/nnews/30385.htm
- http://m.3g.uliejh.cn/nnews/8284893.htm
- http://m.3g.uliejh.cn/nnews/072044.htm
- http://m.3g.uliejh.cn/nnews/8055.htm
- http://m.3g.uliejh.cn/nnews/21929.htm
- http://m.3g.uliejh.cn/nnews/8722.htm
- http://m.3g.uliejh.cn/nnews/2456.htm
- http://m.3g.uliejh.cn/nnews/6085311.htm
- http://m.3g.uliejh.cn/nnews/09060.htm
- http://m.3g.uliejh.cn/nnews/152074.htm
- http://m.3g.uliejh.cn/nnews/3001418.htm
- http://m.3g.uliejh.cn/nnews/29888.htm
- http://m.3g.uliejh.cn/nnews/0538.htm
- http://m.3g.uliejh.cn/nnews/573441.htm
- http://m.3g.uliejh.cn/nnews/97024.htm
- http://m.3g.uliejh.cn/nnews/62856.htm
- http://m.3g.uliejh.cn/nnews/39722.htm
- http://m.3g.uliejh.cn/nnews/6531240.htm
- http://m.3g.uliejh.cn/nnews/122427.htm
- http://m.3g.uliejh.cn/nnews/777797.htm
- http://m.3g.uliejh.cn/nnews/7062.htm
- http://m.3g.uliejh.cn/nnews/1681.htm
- http://m.3g.uliejh.cn/nnews/696194.htm
- http://m.3g.uliejh.cn/nnews/623165.htm
- http://m.3g.uliejh.cn/nnews/76923.htm
- http://m.3g.uliejh.cn/nnews/928917.htm
- http://m.3g.uliejh.cn/nnews/220596.htm
- http://m.3g.uliejh.cn/nnews/1610388.htm
- http://m.3g.uliejh.cn/nnews/8812637.htm
- http://m.3g.uliejh.cn/nnews/67421.htm
- http://m.3g.uliejh.cn/nnews/4278836.htm
- http://m.3g.uliejh.cn/nnews/8472402.htm
- http://m.3g.uliejh.cn/nnews/041293.htm
- http://m.3g.uliejh.cn/nnews/0765964.htm
- http://m.3g.uliejh.cn/nnews/80988.htm
- http://m.3g.uliejh.cn/nnews/268657.htm
- http://m.3g.uliejh.cn/nnews/6557512.htm
- http://m.3g.uliejh.cn/nnews/503698.htm
- http://m.3g.uliejh.cn/nnews/680671.htm
- http://m.3g.uliejh.cn/nnews/731371.htm
- http://m.3g.uliejh.cn/nnews/3457.htm
- http://m.3g.uliejh.cn/nnews/9585720.htm
- http://m.3g.uliejh.cn/nnews/24709.htm
- http://m.3g.uliejh.cn/nnews/60670.htm
- http://m.3g.uliejh.cn/nnews/822177.htm
- http://m.3g.uliejh.cn/nnews/539833.htm
- http://m.3g.uliejh.cn/nnews/136283.htm
- http://m.3g.uliejh.cn/nnews/6332779.htm
- http://m.3g.uliejh.cn/nnews/386710.htm
- http://m.3g.uliejh.cn/nnews/9242476.htm
- http://m.3g.uliejh.cn/nnews/8753.htm
- http://m.3g.uliejh.cn/nnews/06239.htm
- http://m.3g.uliejh.cn/nnews/8367704.htm
- http://m.3g.uliejh.cn/nnews/857091.htm
- http://m.3g.uliejh.cn/nnews/856280.htm
- http://m.3g.uliejh.cn/nnews/185466.htm
- http://m.3g.uliejh.cn/nnews/4682155.htm
- http://m.3g.uliejh.cn/nnews/4366099.htm
- http://m.3g.uliejh.cn/nnews/1933257.htm
- http://m.3g.uliejh.cn/nnews/71643.htm
- http://m.3g.uliejh.cn/nnews/06180.htm
- http://m.3g.uliejh.cn/nnews/8813.htm
- http://m.3g.uliejh.cn/nnews/679759.htm
- http://m.3g.uliejh.cn/nnews/202440.htm
- http://m.3g.uliejh.cn/nnews/9997119.htm
- http://m.3g.uliejh.cn/nnews/44598.htm
- http://m.3g.uliejh.cn/nnews/6051955.htm
- http://m.3g.uliejh.cn/nnews/4891953.htm
- http://m.3g.uliejh.cn/nnews/4985.htm
- http://m.3g.uliejh.cn/nnews/6951874.htm
- http://m.3g.uliejh.cn/nnews/3304181.htm
- http://m.3g.uliejh.cn/nnews/1239.htm
- http://m.3g.uliejh.cn/nnews/3187.htm
- http://m.3g.uliejh.cn/nnews/32225.htm
- http://m.3g.uliejh.cn/nnews/0275.htm
- http://m.3g.uliejh.cn/nnews/555141.htm
- http://m.3g.uliejh.cn/nnews/5160989.htm
- http://m.3g.uliejh.cn/nnews/4262097.htm
- http://m.3g.uliejh.cn/nnews/532142.htm
- http://m.3g.uliejh.cn/nnews/3090044.htm
- http://m.3g.uliejh.cn/nnews/5469.htm
- http://m.3g.uliejh.cn/nnews/648321.htm
- http://m.3g.uliejh.cn/nnews/275301.htm
- http://m.3g.uliejh.cn/nnews/852935.htm
- http://m.3g.uliejh.cn/nnews/26785.htm
- http://m.3g.uliejh.cn/nnews/1240853.htm
- http://m.3g.uliejh.cn/nnews/22287.htm
- http://m.3g.uliejh.cn/nnews/7763034.htm
- http://m.3g.uliejh.cn/nnews/95390.htm
- http://m.3g.uliejh.cn/nnews/7218559.htm
- http://m.3g.uliejh.cn/nnews/26015.htm
- http://m.3g.uliejh.cn/nnews/6671.htm
- http://m.3g.uliejh.cn/nnews/620426.htm
- http://m.3g.uliejh.cn/nnews/1365.htm
- http://m.3g.uliejh.cn/nnews/3893337.htm
- http://m.3g.uliejh.cn/nnews/78289.htm
- http://m.3g.uliejh.cn/nnews/635014.htm
- http://m.3g.uliejh.cn/nnews/19212.htm
- http://m.3g.uliejh.cn/nnews/4324.htm
- http://m.3g.uliejh.cn/nnews/09690.htm
- http://m.3g.uliejh.cn/nnews/81636.htm
- http://m.3g.uliejh.cn/nnews/307347.htm
- http://m.3g.uliejh.cn/nnews/1986.htm
- http://m.3g.uliejh.cn/nnews/980654.htm
- http://m.3g.uliejh.cn/nnews/6591.htm
- http://m.3g.uliejh.cn/nnews/4583912.htm
- http://m.3g.uliejh.cn/nnews/3739.htm
- http://m.3g.uliejh.cn/nnews/545999.htm
- http://m.3g.uliejh.cn/nnews/437621.htm
- http://m.3g.uliejh.cn/nnews/003061.htm
- http://m.3g.uliejh.cn/nnews/91018.htm
- http://m.3g.uliejh.cn/nnews/972004.htm
- http://m.3g.uliejh.cn/nnews/7286400.htm
- http://m.3g.uliejh.cn/nnews/8040192.htm
- http://m.3g.uliejh.cn/nnews/1824.htm
- http://m.3g.uliejh.cn/nnews/81830.htm
- http://m.3g.uliejh.cn/nnews/1062.htm
- http://m.3g.uliejh.cn/nnews/4069147.htm
- http://m.3g.uliejh.cn/nnews/24919.htm
- http://m.3g.uliejh.cn/nnews/6521.htm
- http://m.3g.uliejh.cn/nnews/197923.htm
- http://m.3g.uliejh.cn/nnews/47144.htm
- http://m.3g.uliejh.cn/nnews/8119998.htm
- http://m.3g.uliejh.cn/nnews/190236.htm
- http://m.3g.uliejh.cn/nnews/8212562.htm
- http://m.3g.uliejh.cn/nnews/98371.htm
- http://m.3g.uliejh.cn/nnews/4730.htm
- http://m.3g.uliejh.cn/nnews/9836529.htm
- http://m.3g.uliejh.cn/nnews/26101.htm
- http://m.3g.uliejh.cn/nnews/755667.htm
- http://m.3g.uliejh.cn/nnews/8044912.htm
- http://m.3g.uliejh.cn/nnews/60726.htm
- http://m.3g.uliejh.cn/nnews/8862.htm
- http://m.3g.uliejh.cn/nnews/7799.htm
- http://m.3g.uliejh.cn/nnews/2881130.htm
- http://m.3g.uliejh.cn/nnews/7202757.htm
- http://m.3g.uliejh.cn/nnews/764068.htm
- http://m.3g.uliejh.cn/nnews/3986172.htm
- http://m.3g.uliejh.cn/nnews/575424.htm
- http://m.3g.uliejh.cn/nnews/0104294.htm
- http://m.3g.uliejh.cn/nnews/200178.htm
- http://m.3g.uliejh.cn/nnews/418184.htm
- http://m.3g.uliejh.cn/nnews/3335285.htm
- http://m.3g.uliejh.cn/nnews/8558.htm
- http://m.3g.uliejh.cn/nnews/8378857.htm
- http://m.3g.uliejh.cn/nnews/127176.htm
- http://m.3g.uliejh.cn/nnews/462644.htm
- http://m.3g.uliejh.cn/nnews/35905.htm
- http://m.3g.uliejh.cn/nnews/91883.htm
- http://m.3g.uliejh.cn/nnews/1647036.htm
- http://m.3g.uliejh.cn/nnews/098865.htm
- http://m.3g.uliejh.cn/nnews/4334.htm
- http://m.3g.uliejh.cn/nnews/1712690.htm
- http://m.3g.uliejh.cn/nnews/6630.htm
- http://m.3g.uliejh.cn/nnews/5239.htm
- http://m.3g.uliejh.cn/nnews/5177220.htm
- http://m.3g.uliejh.cn/nnews/0203209.htm
- http://m.3g.uliejh.cn/nnews/334800.htm
- http://m.3g.uliejh.cn/nnews/2343802.htm
- http://m.3g.uliejh.cn/nnews/049169.htm
- http://m.3g.uliejh.cn/nnews/9271102.htm
- http://m.3g.uliejh.cn/nnews/170356.htm
- http://m.3g.uliejh.cn/nnews/4572062.htm
- http://m.3g.uliejh.cn/nnews/429487.htm
- http://m.3g.uliejh.cn/nnews/302551.htm
- http://m.3g.uliejh.cn/nnews/815205.htm
- http://m.3g.uliejh.cn/nnews/7378092.htm
- http://m.3g.uliejh.cn/nnews/2095.htm
- http://m.3g.uliejh.cn/nnews/57276.htm
- http://m.3g.uliejh.cn/nnews/6403.htm
- http://m.3g.uliejh.cn/nnews/903378.htm
- http://m.3g.uliejh.cn/nnews/3318604.htm
- http://m.3g.uliejh.cn/nnews/936988.htm
- http://m.3g.uliejh.cn/nnews/2014.htm
- http://m.3g.uliejh.cn/nnews/2666001.htm
- http://m.3g.uliejh.cn/nnews/87789.htm
- http://m.3g.uliejh.cn/nnews/6912.htm
- http://m.3g.uliejh.cn/nnews/24308.htm
- http://m.3g.uliejh.cn/nnews/75288.htm
- http://m.3g.uliejh.cn/nnews/756044.htm
- http://m.3g.uliejh.cn/nnews/66619.htm
- http://m.3g.uliejh.cn/nnews/6115641.htm
- http://m.3g.uliejh.cn/nnews/7252.htm
- http://m.3g.uliejh.cn/nnews/7340.htm
- http://m.3g.uliejh.cn/nnews/14728.htm
- http://m.3g.uliejh.cn/nnews/1454.htm
- http://m.3g.uliejh.cn/nnews/693026.htm
- http://m.3g.uliejh.cn/nnews/15783.htm
- http://m.3g.uliejh.cn/nnews/7927915.htm
- http://m.3g.uliejh.cn/nnews/602621.htm
- http://m.3g.uliejh.cn/nnews/015075.htm
- http://m.3g.uliejh.cn/nnews/2134.htm
- http://m.3g.uliejh.cn/nnews/4086.htm
- http://m.3g.uliejh.cn/nnews/875225.htm
- http://m.3g.uliejh.cn/nnews/291819.htm
- http://m.3g.uliejh.cn/nnews/41413.htm
- http://m.3g.uliejh.cn/nnews/1850.htm
- http://m.3g.uliejh.cn/nnews/274064.htm
- http://m.3g.uliejh.cn/nnews/025106.htm
- http://m.3g.uliejh.cn/nnews/53808.htm
- http://m.3g.uliejh.cn/nnews/333589.htm
- http://m.3g.uliejh.cn/nnews/8859.htm
- http://m.3g.uliejh.cn/nnews/39156.htm
- http://m.3g.uliejh.cn/nnews/2568.htm
- http://m.3g.uliejh.cn/nnews/0523.htm
- http://m.3g.uliejh.cn/nnews/7998.htm
- http://m.3g.uliejh.cn/nnews/912608.htm
- http://m.3g.uliejh.cn/nnews/6777271.htm
- http://m.3g.uliejh.cn/nnews/4434.htm
- http://m.3g.uliejh.cn/nnews/2954447.htm
- http://m.3g.uliejh.cn/nnews/5410.htm
- http://m.3g.uliejh.cn/nnews/386626.htm
- http://m.3g.uliejh.cn/nnews/688012.htm
- http://m.3g.uliejh.cn/nnews/3703.htm
- http://m.3g.uliejh.cn/nnews/29853.htm
- http://m.3g.uliejh.cn/nnews/2557.htm
- http://m.3g.uliejh.cn/nnews/7009434.htm
- http://m.3g.uliejh.cn/nnews/0455.htm
- http://m.3g.uliejh.cn/nnews/479493.htm
- http://m.3g.uliejh.cn/nnews/3591976.htm
- http://m.3g.uliejh.cn/nnews/461383.htm
- http://m.3g.uliejh.cn/nnews/1610.htm
- http://m.3g.uliejh.cn/nnews/79464.htm
- http://m.3g.uliejh.cn/nnews/279024.htm
- http://m.3g.uliejh.cn/nnews/938421.htm
- http://m.3g.uliejh.cn/nnews/073188.htm
- http://m.3g.uliejh.cn/nnews/6483536.htm
- http://m.3g.uliejh.cn/nnews/689346.htm
- http://m.3g.uliejh.cn/nnews/4820.htm
- http://m.3g.uliejh.cn/nnews/95126.htm
- http://m.3g.uliejh.cn/nnews/7740.htm
- http://m.3g.uliejh.cn/nnews/89870.htm
- http://m.3g.uliejh.cn/nnews/85465.htm
- http://m.3g.uliejh.cn/nnews/6205697.htm
- http://m.3g.uliejh.cn/nnews/3263454.htm
- http://m.3g.uliejh.cn/nnews/0067.htm
- http://m.3g.uliejh.cn/nnews/39791.htm
- http://m.3g.uliejh.cn/nnews/3540993.htm
- http://m.3g.uliejh.cn/nnews/937032.htm
- http://m.3g.uliejh.cn/nnews/18277.htm
- http://m.3g.uliejh.cn/nnews/82044.htm
- http://m.3g.uliejh.cn/nnews/4484.htm
- http://m.3g.uliejh.cn/nnews/0407.htm
- http://m.3g.uliejh.cn/nnews/43219.htm
- http://m.3g.uliejh.cn/nnews/55772.htm
- http://m.3g.uliejh.cn/nnews/08231.htm
- http://m.3g.uliejh.cn/nnews/255341.htm
- http://m.3g.uliejh.cn/nnews/3189215.htm

## 项目结构

```
weblink-nexus/
├── data/                               # 数据存储目录
│   ├── raw_links.txt                   # 原始链接列表（每行一个URL）
│   ├── index.json                      # 构建后生成的索引文件（含分类与标签）
│   └── categories.yaml                 # 用户自定义分类映射配置
├── src/                                # 核心源代码目录
│   ├── builder.py                      # 索引构建器，负责解析链接并生成索引
│   ├── server.py                       # 本地预览服务主程序（基于http.server）
│   └── utils.py                        # 通用工具函数（路径校验、格式清洗）
├── static/                             # 前端静态资源目录
│   ├── css/                            # 样式文件
│   │   ├── main.css                    # 全局布局与排版样式
│   │   └── responsive.css              # 移动端响应式适配样式
│   ├── js/                             # 前端交互脚本
│   │   ├── search.js                   # 关键词模糊检索逻辑
│   │   └── filter.js                   # 分类标签筛选与联动控制
│   └── templates/                      # HTML模板文件
│       ├── index.html                  # 资源列表主页模板
│       └── detail.html                 # 单个资源详情页模板（预留）
├── docs/                               # 项目文档目录
│   ├── user-guide.md                   # 用户操作手册
│   ├── maintainer-guide.md             # 维护者操作指南
│   ├── deployment.md                   # 生产环境部署说明
│   └── design.md                       # 项目架构设计文档
├── tests/                              # 单元测试目录
│   ├── test_builder.py                 # 索引构建模块测试用例
│   └── test_utils.py                   # 工具函数测试用例
├── requirements.txt                    # Python依赖声明文件
├── serve.py                            # 服务启动入口脚本
├── build_index.py                      # 索引构建命令行工具
└── README.md                           # 项目说明文档（本文件）
```

## 贡献指南

1. 复刻项目仓库至个人账号下，并基于 main 分支创建功能特性分支，分支命名建议采用 `feature/功能简述` 或 `fix/问题描述` 格式。

2. 在 `data/raw_links.txt` 中追加或修改链接条目，每行仅包含一个完整 URL，确保不包含多余空白字符。若涉及分类调整，同步更新 `data/categories.yaml` 中的映射规则。

3. 运行 `python build_index.py --input ./data/raw_links.txt --output ./data/index.json` 重新生成索引文件，并执行 `python -m unittest discover tests` 确保所有单元测试通过。

4. 在本地启动预览服务 `python serve.py --port 8080`，通过浏览器访问 `http://127.0.0.1:8080` 验证变更效果，确认列表渲染、搜索筛选功能正常。

5. 提交变更并推送至远程分支，随后在 GitHub 上发起 Pull Request 至主仓库的 main 分支，在 PR 描述中注明变更内容、测试结果及影响范围。

## 常见问题

**问：为什么系统不自动补全 URL 的协议前缀或 www 子域名？**

答：本项目严格遵循原始链接保真原则。用户提供的 URL 可能因来源差异而包含不同协议（http / https）或省略子域名，系统在展示和索引过程中不做任何自动推断或修正，以避免改变原链接的语义或造成访问错误。维护者应确保录入时使用完整且可访问的原始地址。

**问：索引构建时提示链接格式校验失败，如何排查？**

答：请检查 `data/raw_links.txt` 中每一行是否仅包含一个 URL，且未包含行首尾空格、制表符或多余逗号。若链接中包含特殊字符（如中文或空格），需先进行 URL 编码再录入。系统要求每个链接必须包含协议头（http:// 或 https://），且域名部分至少包含一个点号。

**问：本地预览服务启动后页面无数据显示，应如何处理？**

答：首先确认 `data/index.json` 文件是否存在且非空，若不存在则运行 `python build_index.py` 生成索引。若索引存在但页面仍无数据，检查浏览器开发者工具控制台是否有 JavaScript 错误，常见原因包括静态资源路径配置不正确或文件编码为 UTF-8 with BOM 导致解析异常。可尝试将 `static/` 目录下的资源文件重新保存为 UTF-8 without BOM 格式。

## 许可证

MIT

> 外链数量: 250 | 生成时间: 2026-08-24 23:40:21
