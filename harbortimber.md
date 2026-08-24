# WebLink Navigator

WebLink Navigator 是一个面向技术调研、内容聚合与信息归档场景的轻量级外链资源管理与导航系统。该项目定位于帮助开发者、技术写作者、舆情分析人员以及数据归档工程师，以结构化方式组织和访问大量分散的 URL 资源，并提供本地化的快速查阅与分类能力。

该项目不依赖外部数据库或云服务，所有资源索引基于静态文件与约定式目录结构，适合部署在各类 Web 容器或本地开发环境中。WebLink Navigator 尤其适用于需要定期导入、清洗、标注和浏览大批量外链链接的工作流，其设计目标是在不引入复杂前端框架的前提下，提供清晰的信息层级与可扩展的元数据管理接口。

## 功能概览

- 批量链接导入与去重：支持从纯文本列表或 CSV 中导入大量 URL，自动识别重复条目并生成唯一资源标识。

- 分层标签与分类系统：允许用户为每个链接分配多个标签，并按主题、来源、批次或日期进行多维度分类。

- 全文检索与字段过滤：基于标题、描述、标签、导入批次等字段提供快速过滤与关键字搜索功能。

- 资源快照与状态标记：支持记录每个链接的访问状态、可用性检查时间、备注信息以及自定义优先级。

- 数据导出与备份机制：可将全部资源列表及元数据导出为 JSON、Markdown 或结构化文本格式，便于版本控制与迁移。

- 静态站点生成模式：内置模板引擎可将资源列表渲染为静态 HTML 页面，方便内网分享或离线浏览。

- 扩展字段自定义：用户可根据业务需要添加自定义属性字段，如所属项目编号、审核状态、关联报告编号等。

## 应用场景

- 技术文献与参考资料归档：研究人员或工程师在阅读技术博客、论文、官方文档时，将分散的参考链接统一收录，并通过标签区分主题，后续撰写技术报告时可快速检索引用来源。

- 舆情信息收集与简报制作：内容运营人员或公关团队定期从多个新闻源收集报道链接，导入系统后按日期、地域或情感倾向分类，生成每日舆情简报。

- 项目外部依赖与参考资源管理：开发团队在技术选型或竞品分析阶段，将候选框架、工具、服务商的官网及评测文章链接集中管理，方便团队内部共享和评估。

- 数据质量审计与死链检测：质量保障人员定期导入待检测的链接清单，系统通过状态标记功能记录每个链接的响应情况，形成可用性报告供后续处理。

## 快速开始

以下步骤帮助您在本地环境中快速启动 WebLink Navigator 服务。

```bash
# 克隆项目仓库至本地
git clone https://github.com/weblink-navigator/weblink-navigator.git

# 进入项目根目录
cd weblink-navigator

# 安装 Python 依赖（建议使用虚拟环境）
python -m venv venv
source venv/bin/activate  # Linux/macOS 下使用
# venv\Scripts\activate   # Windows 下使用
pip install -r requirements.txt

# 执行初始化数据迁移与资源目录创建
python manage.py init --resources ./data/resources.json

# 启动本地开发服务器
python manage.py serve --host 127.0.0.1 --port 8080
```

启动后，在浏览器中访问 `http://127.0.0.1:8080` 即可看到资源列表主界面。首次启动将自动生成示例数据与目录结构。

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
| :--- | :--- | :--- |
| Python | 3.9 至 3.12 | 核心运行环境，用于后端服务与数据处理脚本 |
| pip | 22.0 及以上 | Python 包管理工具，用于安装项目依赖 |
| Git | 2.25 及以上 | 用于克隆仓库及后续版本管理 |
| 磁盘空间 | 至少 200 MB | 用于存放资源索引文件、日志及静态缓存 |
| 内存 | 最低 512 MB，推荐 1 GB | 保证批量导入和搜索功能的流畅运行 |
| 操作系统 | Linux / macOS / Windows | 跨平台支持，生产环境建议使用 Linux |
| 浏览器 | 现代浏览器（Chrome 90+ / Firefox 88+ / Edge 90+） | 用于访问 Web 管理界面 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
| :--- | :--- | :--- |
| 入门指南 | `docs/quick-start/` | 如何安装、配置首次运行、导入第一批链接 |
| 用户手册 | `docs/user-guide/` | 如何执行搜索、分类、导出与快照管理 |
| 开发文档 | `docs/developer/` | 如何扩展自定义字段、增加导入格式或修改前端模板 |
| 运维参考 | `docs/operations/` | 如何备份数据、迁移环境、调整性能参数 |

## 资源列表

- http://m.wap.uliejh.cn/bnews/08263.htm
- http://m.wap.uliejh.cn/bnews/91193.htm
- http://m.wap.uliejh.cn/bnews/0427.htm
- http://m.wap.uliejh.cn/bnews/1888.htm
- http://m.wap.uliejh.cn/bnews/9597484.htm
- http://m.wap.uliejh.cn/bnews/805581.htm
- http://m.wap.uliejh.cn/bnews/040664.htm
- http://m.wap.uliejh.cn/bnews/594635.htm
- http://m.wap.uliejh.cn/bnews/5417901.htm
- http://m.wap.uliejh.cn/bnews/0601762.htm
- http://m.wap.uliejh.cn/bnews/8203.htm
- http://m.wap.uliejh.cn/bnews/0367.htm
- http://m.wap.uliejh.cn/bnews/571383.htm
- http://m.wap.uliejh.cn/bnews/9394878.htm
- http://m.wap.uliejh.cn/bnews/211493.htm
- http://m.wap.uliejh.cn/bnews/286453.htm
- http://m.wap.uliejh.cn/bnews/498777.htm
- http://m.wap.uliejh.cn/bnews/3161.htm
- http://m.wap.uliejh.cn/bnews/479742.htm
- http://m.wap.uliejh.cn/bnews/1087.htm
- http://m.wap.uliejh.cn/bnews/846883.htm
- http://m.wap.uliejh.cn/bnews/1817099.htm
- http://m.wap.uliejh.cn/bnews/64451.htm
- http://m.wap.uliejh.cn/bnews/9058804.htm
- http://m.wap.uliejh.cn/bnews/6258.htm
- http://m.wap.uliejh.cn/bnews/1625986.htm
- http://m.wap.uliejh.cn/bnews/5044.htm
- http://m.wap.uliejh.cn/bnews/185038.htm
- http://m.wap.uliejh.cn/bnews/310258.htm
- http://m.wap.uliejh.cn/bnews/839326.htm
- http://m.wap.uliejh.cn/bnews/7099.htm
- http://m.wap.uliejh.cn/bnews/9161.htm
- http://m.wap.uliejh.cn/bnews/06016.htm
- http://m.wap.uliejh.cn/bnews/7820.htm
- http://m.wap.uliejh.cn/bnews/7425734.htm
- http://m.wap.uliejh.cn/bnews/2013553.htm
- http://m.wap.uliejh.cn/bnews/0582521.htm
- http://m.wap.uliejh.cn/bnews/6976.htm
- http://m.wap.uliejh.cn/bnews/1960894.htm
- http://m.wap.uliejh.cn/bnews/8757310.htm
- http://m.wap.uliejh.cn/bnews/021126.htm
- http://m.wap.uliejh.cn/bnews/2569801.htm
- http://m.wap.uliejh.cn/bnews/40634.htm
- http://m.wap.uliejh.cn/bnews/72878.htm
- http://m.wap.uliejh.cn/bnews/694934.htm
- http://m.wap.uliejh.cn/bnews/9136.htm
- http://m.wap.uliejh.cn/bnews/22818.htm
- http://m.wap.uliejh.cn/bnews/3850444.htm
- http://m.wap.uliejh.cn/bnews/4540.htm
- http://m.wap.uliejh.cn/bnews/785471.htm
- http://m.wap.uliejh.cn/bnews/9642087.htm
- http://m.wap.uliejh.cn/bnews/23773.htm
- http://m.wap.uliejh.cn/bnews/4866888.htm
- http://m.wap.uliejh.cn/bnews/8704286.htm
- http://m.wap.uliejh.cn/bnews/6466.htm
- http://m.wap.uliejh.cn/bnews/35041.htm
- http://m.wap.uliejh.cn/bnews/6958944.htm
- http://m.wap.uliejh.cn/bnews/6696.htm
- http://m.wap.uliejh.cn/bnews/58486.htm
- http://m.wap.uliejh.cn/bnews/791737.htm
- http://m.wap.uliejh.cn/bnews/512759.htm
- http://m.wap.uliejh.cn/bnews/8248910.htm
- http://m.wap.uliejh.cn/bnews/08589.htm
- http://m.wap.uliejh.cn/bnews/804460.htm
- http://m.wap.uliejh.cn/bnews/8601.htm
- http://m.wap.uliejh.cn/bnews/75039.htm
- http://m.wap.uliejh.cn/bnews/232055.htm
- http://m.wap.uliejh.cn/bnews/94170.htm
- http://m.wap.uliejh.cn/bnews/8455.htm
- http://m.wap.uliejh.cn/bnews/7704353.htm
- http://m.wap.uliejh.cn/bnews/9692.htm
- http://m.wap.uliejh.cn/bnews/858173.htm
- http://m.wap.uliejh.cn/bnews/1461148.htm
- http://m.wap.uliejh.cn/bnews/2093.htm
- http://m.wap.uliejh.cn/bnews/0365.htm
- http://m.wap.uliejh.cn/bnews/467939.htm
- http://m.wap.uliejh.cn/bnews/256497.htm
- http://m.wap.uliejh.cn/bnews/5294.htm
- http://m.wap.uliejh.cn/bnews/5452921.htm
- http://m.wap.uliejh.cn/bnews/8446.htm
- http://m.wap.uliejh.cn/bnews/946848.htm
- http://m.wap.uliejh.cn/bnews/14251.htm
- http://m.wap.uliejh.cn/bnews/55119.htm
- http://m.wap.uliejh.cn/bnews/2120.htm
- http://m.wap.uliejh.cn/bnews/47644.htm
- http://m.wap.uliejh.cn/bnews/1843530.htm
- http://m.wap.uliejh.cn/bnews/329648.htm
- http://m.wap.uliejh.cn/bnews/3356422.htm
- http://m.wap.uliejh.cn/bnews/99680.htm
- http://m.wap.uliejh.cn/bnews/6011801.htm
- http://m.wap.uliejh.cn/bnews/8504.htm
- http://m.wap.uliejh.cn/bnews/948147.htm
- http://m.wap.uliejh.cn/bnews/1775524.htm
- http://m.wap.uliejh.cn/bnews/5086.htm
- http://m.wap.uliejh.cn/bnews/3583605.htm
- http://m.wap.uliejh.cn/bnews/9644.htm
- http://m.wap.uliejh.cn/bnews/4765.htm
- http://m.wap.uliejh.cn/bnews/51053.htm
- http://m.wap.uliejh.cn/bnews/5748.htm
- http://m.wap.uliejh.cn/bnews/11097.htm
- http://m.wap.uliejh.cn/bnews/53765.htm
- http://m.wap.uliejh.cn/bnews/3153.htm
- http://m.wap.uliejh.cn/bnews/3339887.htm
- http://m.wap.uliejh.cn/bnews/0102.htm
- http://m.wap.uliejh.cn/bnews/1509415.htm
- http://m.wap.uliejh.cn/bnews/569817.htm
- http://m.wap.uliejh.cn/bnews/254892.htm
- http://m.wap.uliejh.cn/bnews/651897.htm
- http://m.wap.uliejh.cn/bnews/1974.htm
- http://m.wap.uliejh.cn/bnews/2287714.htm
- http://m.wap.uliejh.cn/bnews/8678026.htm
- http://m.wap.uliejh.cn/bnews/8859055.htm
- http://m.wap.uliejh.cn/bnews/338766.htm
- http://m.wap.uliejh.cn/bnews/3169.htm
- http://m.wap.uliejh.cn/bnews/28057.htm
- http://m.wap.uliejh.cn/bnews/8517.htm
- http://m.wap.uliejh.cn/bnews/36531.htm
- http://m.wap.uliejh.cn/bnews/209122.htm
- http://m.wap.uliejh.cn/bnews/66180.htm
- http://m.wap.uliejh.cn/bnews/16996.htm
- http://m.wap.uliejh.cn/bnews/1143.htm
- http://m.wap.uliejh.cn/bnews/90075.htm
- http://m.wap.uliejh.cn/bnews/53647.htm
- http://m.wap.uliejh.cn/bnews/882916.htm
- http://m.wap.uliejh.cn/bnews/786121.htm
- http://m.wap.uliejh.cn/bnews/2885.htm
- http://m.wap.uliejh.cn/bnews/68057.htm
- http://m.wap.uliejh.cn/bnews/39712.htm
- http://m.wap.uliejh.cn/bnews/398593.htm
- http://m.wap.uliejh.cn/bnews/2406506.htm
- http://m.wap.uliejh.cn/bnews/35790.htm
- http://m.wap.uliejh.cn/bnews/2373979.htm
- http://m.wap.uliejh.cn/bnews/4160488.htm
- http://m.wap.uliejh.cn/bnews/8278.htm
- http://m.wap.uliejh.cn/bnews/2215.htm
- http://m.wap.uliejh.cn/bnews/53361.htm
- http://m.wap.uliejh.cn/bnews/7130.htm
- http://m.wap.uliejh.cn/bnews/2711947.htm
- http://m.wap.uliejh.cn/bnews/9664063.htm
- http://m.wap.uliejh.cn/bnews/9393.htm
- http://m.wap.uliejh.cn/bnews/57553.htm
- http://m.wap.uliejh.cn/bnews/80553.htm
- http://m.wap.uliejh.cn/bnews/711313.htm
- http://m.wap.uliejh.cn/bnews/15958.htm
- http://m.wap.uliejh.cn/bnews/9742365.htm
- http://m.wap.uliejh.cn/bnews/85896.htm
- http://m.wap.uliejh.cn/bnews/2277955.htm
- http://m.wap.uliejh.cn/bnews/6484310.htm
- http://m.wap.uliejh.cn/bnews/9190257.htm
- http://m.wap.uliejh.cn/bnews/16365.htm
- http://m.wap.uliejh.cn/bnews/11632.htm
- http://m.wap.uliejh.cn/bnews/86056.htm
- http://m.wap.uliejh.cn/bnews/6951041.htm
- http://m.wap.uliejh.cn/bnews/61069.htm
- http://m.wap.uliejh.cn/bnews/96830.htm
- http://m.wap.uliejh.cn/bnews/06884.htm
- http://m.wap.uliejh.cn/bnews/928073.htm
- http://m.wap.uliejh.cn/bnews/8329.htm
- http://m.wap.uliejh.cn/bnews/1689.htm
- http://m.wap.uliejh.cn/bnews/9450501.htm
- http://m.wap.uliejh.cn/bnews/0604.htm
- http://m.wap.uliejh.cn/bnews/32079.htm
- http://m.wap.uliejh.cn/bnews/932171.htm
- http://m.wap.uliejh.cn/bnews/7148352.htm
- http://m.wap.uliejh.cn/bnews/1368.htm
- http://m.wap.uliejh.cn/bnews/12363.htm
- http://m.wap.uliejh.cn/bnews/872702.htm
- http://m.wap.uliejh.cn/bnews/5127720.htm
- http://m.wap.uliejh.cn/bnews/3023939.htm
- http://m.wap.uliejh.cn/bnews/31650.htm
- http://m.wap.uliejh.cn/bnews/5406.htm
- http://m.wap.uliejh.cn/bnews/54702.htm
- http://m.wap.uliejh.cn/bnews/6453471.htm
- http://m.wap.uliejh.cn/bnews/37323.htm
- http://m.wap.uliejh.cn/bnews/934227.htm
- http://m.wap.uliejh.cn/bnews/1902.htm
- http://m.wap.uliejh.cn/bnews/33814.htm
- http://m.wap.uliejh.cn/bnews/93790.htm
- http://m.wap.uliejh.cn/bnews/79492.htm
- http://m.wap.uliejh.cn/bnews/53841.htm
- http://m.wap.uliejh.cn/bnews/6492.htm
- http://m.wap.uliejh.cn/bnews/191085.htm
- http://m.wap.uliejh.cn/bnews/0447.htm
- http://m.wap.uliejh.cn/bnews/999043.htm
- http://m.wap.uliejh.cn/bnews/09437.htm
- http://m.wap.uliejh.cn/bnews/876877.htm
- http://m.wap.uliejh.cn/bnews/9598.htm
- http://m.wap.uliejh.cn/bnews/293268.htm
- http://m.wap.uliejh.cn/bnews/9674.htm
- http://m.wap.uliejh.cn/bnews/575117.htm
- http://m.wap.uliejh.cn/bnews/33277.htm
- http://m.wap.uliejh.cn/bnews/325140.htm
- http://m.wap.uliejh.cn/bnews/90455.htm
- http://m.wap.uliejh.cn/bnews/3531336.htm
- http://m.wap.uliejh.cn/bnews/5447.htm
- http://m.wap.uliejh.cn/bnews/382590.htm
- http://m.wap.uliejh.cn/bnews/8795.htm
- http://m.wap.uliejh.cn/bnews/6613.htm
- http://m.wap.uliejh.cn/bnews/3131471.htm
- http://m.wap.uliejh.cn/bnews/4797.htm
- http://m.wap.uliejh.cn/bnews/28914.htm
- http://m.wap.uliejh.cn/bnews/33904.htm
- http://m.wap.uliejh.cn/bnews/97697.htm
- http://m.wap.uliejh.cn/bnews/8044.htm
- http://m.wap.uliejh.cn/bnews/357440.htm
- http://m.wap.uliejh.cn/bnews/85091.htm
- http://m.wap.uliejh.cn/bnews/057706.htm
- http://m.wap.uliejh.cn/bnews/5208408.htm
- http://m.wap.uliejh.cn/bnews/0187626.htm
- http://m.wap.uliejh.cn/bnews/3747.htm
- http://m.wap.uliejh.cn/bnews/48457.htm
- http://m.wap.uliejh.cn/bnews/1794.htm
- http://m.wap.uliejh.cn/bnews/49742.htm
- http://m.wap.uliejh.cn/bnews/04897.htm
- http://m.wap.uliejh.cn/bnews/35862.htm
- http://m.wap.uliejh.cn/bnews/7651040.htm
- http://m.wap.uliejh.cn/bnews/49136.htm
- http://m.wap.uliejh.cn/bnews/5118.htm
- http://m.wap.uliejh.cn/bnews/073602.htm
- http://m.wap.uliejh.cn/bnews/3513.htm
- http://m.wap.uliejh.cn/bnews/771867.htm
- http://m.wap.uliejh.cn/bnews/4415106.htm
- http://m.wap.uliejh.cn/bnews/62380.htm
- http://m.wap.uliejh.cn/bnews/00145.htm
- http://m.wap.uliejh.cn/bnews/847838.htm
- http://m.wap.uliejh.cn/bnews/157586.htm
- http://m.wap.uliejh.cn/bnews/0448.htm
- http://m.wap.uliejh.cn/bnews/8664158.htm
- http://m.wap.uliejh.cn/bnews/947576.htm
- http://m.wap.uliejh.cn/bnews/64053.htm
- http://m.wap.uliejh.cn/bnews/97175.htm
- http://m.wap.uliejh.cn/bnews/0863922.htm
- http://m.wap.uliejh.cn/bnews/26599.htm
- http://m.wap.uliejh.cn/bnews/283085.htm
- http://m.wap.uliejh.cn/bnews/8662836.htm
- http://m.wap.uliejh.cn/bnews/449285.htm
- http://m.wap.uliejh.cn/bnews/55372.htm
- http://m.wap.uliejh.cn/bnews/5438684.htm
- http://m.wap.uliejh.cn/bnews/01205.htm
- http://m.wap.uliejh.cn/bnews/333937.htm
- http://m.wap.uliejh.cn/bnews/4906355.htm
- http://m.wap.uliejh.cn/bnews/945685.htm
- http://m.wap.uliejh.cn/bnews/47707.htm
- http://m.wap.uliejh.cn/bnews/90939.htm
- http://m.wap.uliejh.cn/bnews/3368.htm
- http://m.wap.uliejh.cn/bnews/6197171.htm
- http://m.wap.uliejh.cn/bnews/2291843.htm
- http://m.wap.uliejh.cn/bnews/7077638.htm
- http://m.wap.uliejh.cn/bnews/13495.htm
- http://m.wap.uliejh.cn/bnews/44544.htm

## 项目结构

```
weblink-navigator/
├── data/                                 # 数据存储目录
│   ├── resources/                        # 资源索引与元数据
│   │   ├── index.json                    # 主索引文件，记录所有链接及标签
│   │   └── snapshots/                    # 历史快照版本目录
│   └── imports/                          # 外部导入数据暂存区
│       └── pending/                      # 待处理导入任务队列
├── src/                                  # 核心源代码目录
│   ├── core/                             # 核心逻辑模块
│   │   ├── loader.py                     # 资源加载与解析器
│   │   ├── deduplicator.py               # 去重与冲突处理
│   │   └── exporter.py                   # 导出与序列化工具
│   ├── cli/                              # 命令行接口子模块
│   │   ├── main.py                       # CLI 入口与路由
│   │   └── commands/                     # 各子命令实现（init/serve/import/export）
│   └── web/                              # Web 界面与模板
│       ├── templates/                    # Jinja2 模板文件
│       ├── static/                       # CSS 与前端资源
│       └── routes.py                     # 路由与视图函数
├── tests/                                # 单元测试与集成测试
│   ├── test_core/                        # 核心功能测试
│   └── test_cli/                         # CLI 命令测试
├── docs/                                 # 完整文档目录
│   ├── quick-start/                      # 快速入门指南
│   ├── user-guide/                       # 用户手册
│   ├── developer/                        # 开发人员文档
│   └── operations/                       # 运维与部署指南
├── scripts/                              # 辅助运维脚本
│   ├── backup.sh                         # 数据备份脚本
│   └── migrate.sh                        # 迁移与升级脚本
├── requirements.txt                      # Python 生产依赖列表
├── requirements-dev.txt                  # 开发环境额外依赖
├── setup.py                              # 打包与分发配置
├── README.md                             # 项目说明文件（当前文档）
└── LICENSE                               # MIT 许可证文件
```

## 贡献指南

1. 在 GitHub 上 fork 本仓库，并 clone 到本地开发环境中。请确保使用最新的 main 分支作为基线。

2. 创建以 feature/ 或 fix/ 为前缀的分支，例如 `feature/add-csv-import`。所有开发工作请在独立分支中完成，避免直接修改 main 分支。

3. 编写或修改代码后，请补充对应的单元测试，确保测试覆盖率达到 80% 以上。运行 `pytest tests/` 验证全部测试通过。

4. 更新相关文档，包括用户手册中受影响的部分、API 说明以及示例配置。文档更新应与代码变更保持同步。

5. 提交 pull request 至主仓库的 develop 分支，在描述中清晰说明变更目的、实现方案及测试结果。核心维护者将在 3 个工作日内进行 Review。

## 常见问题

Q: 导入大量链接时出现内存不足错误，如何解决？

A: 建议将导入文件拆分为多个较小的批次（每批 500 至 1000 条），使用 `--batch-size` 参数控制单次处理数量。同时可以调整 Python 解释器的内存限制，或在配置文件中启用流式处理模式。如果数据量超过十万级别，推荐使用 PostgreSQL 作为后端存储引擎。

Q: 如何自定义资源的元数据字段，比如增加“审核人”或“关联工单号”？

A: 项目支持通过配置文件 `config/custom_fields.yaml` 扩展自定义属性。您可以在该文件中声明字段名称、类型（字符串、数字、日期、枚举）和默认值。重启服务后，Web 界面和导入接口将自动识别并显示新增字段。具体语法请参考 `docs/developer/custom-fields.md`。

Q: 生成的静态站点是否可以部署到 Nginx 或 Apache 等 Web 服务器？

A: 可以。执行 `python manage.py build --output ./dist` 命令后，所有静态 HTML、CSS 和资源索引文件会输出到 `./dist` 目录。您只需将该目录的内容复制到 Web 服务器的根目录下即可。该模式生成的页面完全不依赖后端服务，适用于内网文档站点或离线分发场景。

## 许可证

MIT

> 外链数量: 250 | 生成时间: 2026-08-24 23:40:21
