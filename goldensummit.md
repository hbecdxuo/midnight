# WebLink Navigator

WebLink Navigator 是一个面向技术研究者和信息分析人员的结构化外链资源聚合与导航系统。该项目定位于解决海量分散链接的归类、检索与状态监控问题，通过统一的索引框架将零散的 URL 资源转化为可维护、可追溯的知识资产。目标用户包括开源项目维护者、技术文档编写者、安全分析人员以及需要定期跟踪大量外部信息源的研究团队。

本项目不提供内容抓取或存储服务，而是作为资源定位与管理的中枢，帮助用户建立规范的外链引用清单，并配合自动化脚本检测链接可用性、变更频率及页面摘要信息，从而降低人工维护成本。

## 功能概览

- 批量链接导入与去重：支持从文本文件、CSV 或直接粘贴的方式导入大量 URL，自动识别并移除重复条目，保留原始顺序。

- 自定义标签与分类体系：用户可为每个链接添加多级标签（如“技术博客”“官方文档”“数据接口”），并基于标签组合进行快速筛选。

- 链接状态健康检查：内置异步 HTTP 探测器，定期检测每个资源的响应状态码、加载时间及重定向链，生成可用性报告。

- 全文元数据提取：自动抓取目标页面的标题、描述、关键词及最后修改时间，为链接生成摘要索引，便于离线检索。

- 批量导出与共享：支持将当前链接清单导出为 Markdown 表格、JSON 或 CSV 格式，方便嵌入文档、wiki 或与其他工具集成。

- 变更日志追踪：记录每条链接的添加时间、状态变化历史及备注更新，提供完整的审计轨迹，满足团队协作场景下的追溯需求。

## 应用场景

- 技术文档维护：开源项目文档中常包含大量外部参考链接，使用 WebLink Navigator 统一管理这些引用，可在版本发布前批量检查链接有效性，避免文档中出现死链。

- 威胁情报聚合：安全研究人员每日需要跟踪数十个情报源，通过本系统将分散的 URL 集中管理，并利用状态检测功能快速发现被屏蔽或内容变更的页面，及时调整监控策略。

- 学术文献补充材料管理：论文或技术报告中常附带大量数据来源链接，使用本导航工具可以为每个链接添加阅读笔记、重要程度标记和访问日期，生成规范的参考文献附录。

- 内部知识库构建：企业技术团队可将常用开发文档、API 参考、内部工具入口等链接统一收纳，通过标签和分类快速定位，新成员入职时可直接获得完整资源地图。

## 快速开始

以下步骤帮助您在本地环境中快速启动 WebLink Navigator 服务。

```bash
# 克隆项目仓库
git clone https://github.com/weblink-navigator/weblink-navigator.git

# 进入项目目录
cd weblink-navigator

# 安装依赖（使用 pip 与虚拟环境）
python3 -m venv venv
source venv/bin/activate  # Windows 下使用 venv\Scripts\activate
pip install -r requirements.txt

# 初始化本地数据库
python scripts/init_db.py

# 启动开发服务器
python app.py runserver --host=0.0.0.0 --port=8080
```

访问 http://localhost:8080 即可进入 Web 管理界面。首次启动将自动创建示例数据并生成默认管理员账户，登录信息见控制台输出。

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|---|---|---|
| Python | 3.9 及以上 | 核心运行环境，建议使用 3.10 或 3.11 长期支持版本 |
| SQLite | 3.35 及以上 | 内置轻量级数据库，用于存储链接元数据和状态记录，无需额外安装 |
| requests | 2.28.0 及以上 | HTTP 请求库，用于链接健康检查与元数据抓取 |
| beautifulsoup4 | 4.11.0 及以上 | HTML 解析库，用于提取页面标题、描述等信息 |
| apscheduler | 3.10.0 及以上 | 定时任务调度器，用于周期执行链接状态检测 |
| flask | 2.2.0 及以上 | Web 管理界面框架，提供 RESTful API 和前端页面渲染 |
| gunicorn | 20.1.0 及以上 | 生产环境 WSGI 服务器（仅部署时需要） |
| pytest | 7.2.0 及以上 | 单元测试框架（开发环境可选） |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|---|---|---|
| 用户手册 | /docs/user-guide/ | 如何添加链接、配置标签、查看检测报告及导出数据？ |
| 运维指南 | /docs/operations/ | 如何部署生产环境、配置定时任务、备份数据库及迁移版本？ |
| API 参考 | /docs/api/ | 如何通过 REST API 批量导入链接、获取状态结果及集成到外部脚本？ |
| 开发者文档 | /docs/developer/ | 项目代码结构、插件扩展机制、单元测试编写规范及 PR 提交要求？ |

## 资源列表

- http://m.wap.uliejh.cn/bnews/393664.htm
- http://m.wap.uliejh.cn/bnews/38266.htm
- http://m.wap.uliejh.cn/bnews/886884.htm
- http://m.wap.uliejh.cn/bnews/4900088.htm
- http://m.wap.uliejh.cn/bnews/01920.htm
- http://m.wap.uliejh.cn/bnews/59908.htm
- http://m.wap.uliejh.cn/bnews/8533.htm
- http://m.wap.uliejh.cn/bnews/660522.htm
- http://m.wap.uliejh.cn/bnews/250886.htm
- http://m.wap.uliejh.cn/bnews/8100640.htm
- http://m.wap.uliejh.cn/bnews/8998.htm
- http://m.wap.uliejh.cn/bnews/0237406.htm
- http://m.wap.uliejh.cn/bnews/9584.htm
- http://m.wap.uliejh.cn/bnews/487833.htm
- http://m.wap.uliejh.cn/bnews/2190780.htm
- http://m.wap.uliejh.cn/bnews/977354.htm
- http://m.wap.uliejh.cn/bnews/959823.htm
- http://m.wap.uliejh.cn/bnews/5033509.htm
- http://m.wap.uliejh.cn/bnews/1439.htm
- http://m.wap.uliejh.cn/bnews/0026579.htm
- http://m.wap.uliejh.cn/bnews/243789.htm
- http://m.wap.uliejh.cn/bnews/730222.htm
- http://m.wap.uliejh.cn/bnews/43508.htm
- http://m.wap.uliejh.cn/bnews/151825.htm
- http://m.wap.uliejh.cn/bnews/7094249.htm
- http://m.wap.uliejh.cn/bnews/7445507.htm
- http://m.wap.uliejh.cn/bnews/4858411.htm
- http://m.wap.uliejh.cn/bnews/9100633.htm
- http://m.wap.uliejh.cn/bnews/936538.htm
- http://m.wap.uliejh.cn/bnews/6011.htm
- http://m.wap.uliejh.cn/bnews/2685115.htm
- http://m.wap.uliejh.cn/bnews/043045.htm
- http://m.wap.uliejh.cn/bnews/2138123.htm
- http://m.wap.uliejh.cn/bnews/43558.htm
- http://m.wap.uliejh.cn/bnews/22722.htm
- http://m.wap.uliejh.cn/bnews/83954.htm
- http://m.wap.uliejh.cn/bnews/5284.htm
- http://m.wap.uliejh.cn/bnews/02072.htm
- http://m.wap.uliejh.cn/bnews/99924.htm
- http://m.wap.uliejh.cn/bnews/1914319.htm
- http://m.wap.uliejh.cn/bnews/6237.htm
- http://m.wap.uliejh.cn/bnews/0888432.htm
- http://m.wap.uliejh.cn/bnews/4349.htm
- http://m.wap.uliejh.cn/bnews/45097.htm
- http://m.wap.uliejh.cn/bnews/7251069.htm
- http://m.wap.uliejh.cn/bnews/796177.htm
- http://m.wap.uliejh.cn/bnews/34646.htm
- http://m.wap.uliejh.cn/bnews/5412.htm
- http://m.wap.uliejh.cn/bnews/922390.htm
- http://m.wap.uliejh.cn/bnews/9849791.htm
- http://m.wap.uliejh.cn/bnews/3904094.htm
- http://m.wap.uliejh.cn/bnews/2042.htm
- http://m.wap.uliejh.cn/bnews/6907875.htm
- http://m.wap.uliejh.cn/bnews/82772.htm
- http://m.wap.uliejh.cn/bnews/9389543.htm
- http://m.wap.uliejh.cn/bnews/86108.htm
- http://m.wap.uliejh.cn/bnews/6816574.htm
- http://m.wap.uliejh.cn/bnews/778219.htm
- http://m.wap.uliejh.cn/bnews/2506084.htm
- http://m.wap.uliejh.cn/bnews/4545.htm
- http://m.wap.uliejh.cn/bnews/877237.htm
- http://m.wap.uliejh.cn/bnews/0445427.htm
- http://m.wap.uliejh.cn/bnews/8640829.htm
- http://m.wap.uliejh.cn/bnews/2404.htm
- http://m.wap.uliejh.cn/bnews/79660.htm
- http://m.wap.uliejh.cn/bnews/6165.htm
- http://m.wap.uliejh.cn/bnews/8385128.htm
- http://m.wap.uliejh.cn/bnews/19502.htm
- http://m.wap.uliejh.cn/bnews/4705.htm
- http://m.wap.uliejh.cn/bnews/573291.htm
- http://m.wap.uliejh.cn/bnews/592898.htm
- http://m.wap.uliejh.cn/bnews/1834591.htm
- http://m.wap.uliejh.cn/bnews/12124.htm
- http://m.wap.uliejh.cn/bnews/34548.htm
- http://m.wap.uliejh.cn/bnews/563007.htm
- http://m.wap.uliejh.cn/bnews/5834.htm
- http://m.wap.uliejh.cn/bnews/0948700.htm
- http://m.wap.uliejh.cn/bnews/205561.htm
- http://m.wap.uliejh.cn/bnews/3048.htm
- http://m.wap.uliejh.cn/bnews/4468.htm
- http://m.wap.uliejh.cn/bnews/249418.htm
- http://m.wap.uliejh.cn/bnews/6885.htm
- http://m.wap.uliejh.cn/bnews/1894.htm
- http://m.wap.uliejh.cn/bnews/20653.htm
- http://m.wap.uliejh.cn/bnews/3511020.htm
- http://m.wap.uliejh.cn/bnews/1759.htm
- http://m.wap.uliejh.cn/bnews/4304369.htm
- http://m.wap.uliejh.cn/bnews/03444.htm
- http://m.wap.uliejh.cn/bnews/8171743.htm
- http://m.wap.uliejh.cn/bnews/0594.htm
- http://m.wap.uliejh.cn/bnews/6743309.htm
- http://m.wap.uliejh.cn/bnews/4225220.htm
- http://m.wap.uliejh.cn/bnews/822386.htm
- http://m.wap.uliejh.cn/bnews/3203722.htm
- http://m.wap.uliejh.cn/bnews/89193.htm
- http://m.wap.uliejh.cn/bnews/5732302.htm
- http://m.wap.uliejh.cn/bnews/97431.htm
- http://m.wap.uliejh.cn/bnews/98841.htm
- http://m.wap.uliejh.cn/bnews/82657.htm
- http://m.wap.uliejh.cn/bnews/410619.htm
- http://m.wap.uliejh.cn/bnews/329599.htm
- http://m.wap.uliejh.cn/bnews/331107.htm
- http://m.wap.uliejh.cn/bnews/1027526.htm
- http://m.wap.uliejh.cn/bnews/071961.htm
- http://m.wap.uliejh.cn/bnews/46258.htm
- http://m.wap.uliejh.cn/bnews/0291840.htm
- http://m.wap.uliejh.cn/bnews/34530.htm
- http://m.wap.uliejh.cn/bnews/58534.htm
- http://m.wap.uliejh.cn/bnews/90031.htm
- http://m.wap.uliejh.cn/bnews/6013714.htm
- http://m.wap.uliejh.cn/bnews/0992136.htm
- http://m.wap.uliejh.cn/bnews/722225.htm
- http://m.wap.uliejh.cn/bnews/995634.htm
- http://m.wap.uliejh.cn/bnews/6359149.htm
- http://m.wap.uliejh.cn/bnews/6463.htm
- http://m.wap.uliejh.cn/bnews/38690.htm
- http://m.wap.uliejh.cn/bnews/5105089.htm
- http://m.wap.uliejh.cn/bnews/9396727.htm
- http://m.wap.uliejh.cn/bnews/5315243.htm
- http://m.wap.uliejh.cn/bnews/497928.htm
- http://m.wap.uliejh.cn/bnews/95549.htm
- http://m.wap.uliejh.cn/bnews/5759035.htm
- http://m.wap.uliejh.cn/bnews/610730.htm
- http://m.wap.uliejh.cn/bnews/5704868.htm
- http://m.wap.uliejh.cn/bnews/120163.htm
- http://m.wap.uliejh.cn/bnews/578939.htm
- http://m.wap.uliejh.cn/bnews/550552.htm
- http://m.wap.uliejh.cn/bnews/951646.htm
- http://m.wap.uliejh.cn/bnews/3169518.htm
- http://m.wap.uliejh.cn/bnews/339433.htm
- http://m.wap.uliejh.cn/bnews/1736918.htm
- http://m.wap.uliejh.cn/bnews/494216.htm
- http://m.wap.uliejh.cn/bnews/68988.htm
- http://m.wap.uliejh.cn/bnews/662578.htm
- http://m.wap.uliejh.cn/bnews/050165.htm
- http://m.wap.uliejh.cn/bnews/98826.htm
- http://m.wap.uliejh.cn/bnews/601393.htm
- http://m.wap.uliejh.cn/bnews/1526941.htm
- http://m.wap.uliejh.cn/bnews/44444.htm
- http://m.wap.uliejh.cn/bnews/85269.htm
- http://m.wap.uliejh.cn/bnews/9060.htm
- http://m.wap.uliejh.cn/bnews/8944110.htm
- http://m.wap.uliejh.cn/bnews/6272737.htm
- http://m.wap.uliejh.cn/bnews/3679367.htm
- http://m.wap.uliejh.cn/bnews/15823.htm
- http://m.wap.uliejh.cn/bnews/7206.htm
- http://m.wap.uliejh.cn/bnews/93176.htm
- http://m.wap.uliejh.cn/bnews/2562.htm
- http://m.wap.uliejh.cn/bnews/1247401.htm
- http://m.wap.uliejh.cn/bnews/72867.htm
- http://m.wap.uliejh.cn/bnews/9283.htm
- http://m.wap.uliejh.cn/bnews/0232711.htm
- http://m.wap.uliejh.cn/bnews/7975.htm
- http://m.wap.uliejh.cn/bnews/0756.htm
- http://m.wap.uliejh.cn/bnews/154799.htm
- http://m.wap.uliejh.cn/bnews/266616.htm
- http://m.wap.uliejh.cn/bnews/2879.htm
- http://m.wap.uliejh.cn/bnews/6792.htm
- http://m.wap.uliejh.cn/bnews/8531.htm
- http://m.wap.uliejh.cn/bnews/90013.htm
- http://m.wap.uliejh.cn/bnews/1652.htm
- http://m.wap.uliejh.cn/bnews/8262978.htm
- http://m.wap.uliejh.cn/bnews/13472.htm
- http://m.wap.uliejh.cn/bnews/0076.htm
- http://m.wap.uliejh.cn/bnews/907826.htm
- http://m.wap.uliejh.cn/bnews/7370641.htm
- http://m.wap.uliejh.cn/bnews/37196.htm
- http://m.wap.uliejh.cn/bnews/8146544.htm
- http://m.wap.uliejh.cn/bnews/9806.htm
- http://m.wap.uliejh.cn/bnews/574195.htm
- http://m.wap.uliejh.cn/bnews/5187.htm
- http://m.wap.uliejh.cn/bnews/6112.htm
- http://m.wap.uliejh.cn/bnews/6223319.htm
- http://m.wap.uliejh.cn/bnews/223671.htm
- http://m.wap.uliejh.cn/bnews/457146.htm
- http://m.wap.uliejh.cn/bnews/5453.htm
- http://m.wap.uliejh.cn/bnews/20142.htm
- http://m.wap.uliejh.cn/bnews/75712.htm
- http://m.wap.uliejh.cn/bnews/744864.htm
- http://m.wap.uliejh.cn/bnews/77527.htm
- http://m.wap.uliejh.cn/bnews/10026.htm
- http://m.wap.uliejh.cn/bnews/2169450.htm
- http://m.wap.uliejh.cn/bnews/126538.htm
- http://m.wap.uliejh.cn/bnews/15028.htm
- http://m.wap.uliejh.cn/bnews/82447.htm
- http://m.wap.uliejh.cn/bnews/7950.htm
- http://m.wap.uliejh.cn/bnews/9573858.htm
- http://m.wap.uliejh.cn/bnews/3149305.htm
- http://m.wap.uliejh.cn/bnews/6497.htm
- http://m.wap.uliejh.cn/bnews/05215.htm
- http://m.wap.uliejh.cn/bnews/45896.htm
- http://m.wap.uliejh.cn/bnews/97258.htm
- http://m.wap.uliejh.cn/bnews/7367620.htm
- http://m.wap.uliejh.cn/bnews/2779.htm
- http://m.wap.uliejh.cn/bnews/4094870.htm
- http://m.wap.uliejh.cn/bnews/84430.htm
- http://m.wap.uliejh.cn/bnews/6753597.htm
- http://m.wap.uliejh.cn/bnews/8163566.htm
- http://m.wap.uliejh.cn/bnews/027694.htm
- http://m.wap.uliejh.cn/bnews/5364172.htm
- http://m.wap.uliejh.cn/bnews/8615.htm
- http://m.wap.uliejh.cn/bnews/2756924.htm
- http://m.wap.uliejh.cn/bnews/8139919.htm
- http://m.wap.uliejh.cn/bnews/2850224.htm
- http://m.wap.uliejh.cn/bnews/49895.htm
- http://m.wap.uliejh.cn/bnews/2482717.htm
- http://m.wap.uliejh.cn/bnews/26635.htm
- http://m.wap.uliejh.cn/bnews/69950.htm
- http://m.wap.uliejh.cn/bnews/6612394.htm
- http://m.wap.uliejh.cn/bnews/3703.htm
- http://m.wap.uliejh.cn/bnews/808604.htm
- http://m.wap.uliejh.cn/bnews/736909.htm
- http://m.wap.uliejh.cn/bnews/6613224.htm
- http://m.wap.uliejh.cn/bnews/2228307.htm
- http://m.wap.uliejh.cn/bnews/8574449.htm
- http://m.wap.uliejh.cn/bnews/2304.htm
- http://m.wap.uliejh.cn/bnews/7337204.htm
- http://m.wap.uliejh.cn/bnews/42684.htm
- http://m.wap.uliejh.cn/bnews/254521.htm
- http://m.wap.uliejh.cn/bnews/4547669.htm
- http://m.wap.uliejh.cn/bnews/30583.htm
- http://m.wap.uliejh.cn/bnews/9229.htm
- http://m.wap.uliejh.cn/bnews/215334.htm
- http://m.wap.uliejh.cn/bnews/6442.htm
- http://m.wap.uliejh.cn/bnews/041210.htm
- http://m.wap.uliejh.cn/bnews/8984005.htm
- http://m.wap.uliejh.cn/bnews/576315.htm
- http://m.wap.uliejh.cn/bnews/5903532.htm
- http://m.wap.uliejh.cn/bnews/54638.htm
- http://m.wap.uliejh.cn/bnews/146918.htm
- http://m.wap.uliejh.cn/bnews/838201.htm
- http://m.wap.uliejh.cn/bnews/233918.htm
- http://m.wap.uliejh.cn/bnews/09510.htm
- http://m.wap.uliejh.cn/bnews/053790.htm
- http://m.wap.uliejh.cn/bnews/65380.htm
- http://m.wap.uliejh.cn/bnews/2990.htm
- http://m.wap.uliejh.cn/bnews/556531.htm
- http://m.wap.uliejh.cn/bnews/31736.htm
- http://m.wap.uliejh.cn/bnews/15240.htm
- http://m.wap.uliejh.cn/bnews/3771443.htm
- http://m.wap.uliejh.cn/bnews/125398.htm
- http://m.wap.uliejh.cn/bnews/9776.htm
- http://m.wap.uliejh.cn/bnews/477435.htm
- http://m.wap.uliejh.cn/bnews/02759.htm
- http://m.wap.uliejh.cn/bnews/12181.htm
- http://m.wap.uliejh.cn/bnews/6554691.htm
- http://m.wap.uliejh.cn/bnews/264207.htm
- http://m.wap.uliejh.cn/bnews/1702.htm
- http://m.wap.uliejh.cn/bnews/854476.htm
- http://m.wap.uliejh.cn/bnews/067689.htm

## 项目结构

```
weblink-navigator/
├── app/                                # 主应用模块
│   ├── __init__.py                     # 应用工厂与配置加载
│   ├── routes/                         # 路由视图层
│   │   ├── index.py                    # 首页仪表盘与统计概览
│   │   ├── links.py                    # 链接管理 CRUD 接口
│   │   ├── tags.py                     # 标签体系管理接口
│   │   └── api.py                      # RESTful API 端点
│   ├── models/                         # 数据模型与 ORM 定义
│   │   ├── link.py                     # Link 实体模型（含状态、标签、备注）
│   │   ├── check.py                    # 健康检查记录模型
│   │   └── user.py                     # 用户与权限模型
│   ├── services/                       # 业务逻辑服务层
│   │   ├── fetcher.py                  # HTTP 请求与元数据抓取服务
│   │   ├── scheduler.py                # 定时检测任务调度服务
│   │   └── exporter.py                 # 批量导出（JSON/CSV/Markdown）服务
│   └── templates/                      # Jinja2 前端模板
│       ├── base.html                   # 基础布局模板
│       ├── dashboard.html              # 仪表盘视图
│       └── link_list.html              # 链接列表与筛选视图
├── scripts/                            # 运维与开发辅助脚本
│   ├── init_db.py                      # 初始化数据库表结构与默认数据
│   ├── import_links.py                 # 从外部文件批量导入链接
│   └── run_check.py                    # 手动触发全量链接健康检查
├── tests/                              # 单元测试与集成测试
│   ├── test_models.py                  # 数据模型层测试用例
│   ├── test_services.py                # 服务层功能测试
│   └── test_api.py                     # API 端点接口测试
├── docs/                               # 项目文档源码
│   ├── user-guide/                     # 用户手册章节
│   ├── operations/                     # 运维部署指南
│   └── developer/                      # 开发者贡献文档
├── requirements.txt                    # Python 依赖清单（生产环境）
├── requirements-dev.txt                # 开发环境额外依赖
├── setup.py                            # 项目打包与分发配置
├── config.py                           # 全局配置（含数据库路径、检测间隔等）
└── README.md                           # 项目说明文档（本文件）
```

## 贡献指南

1. 阅读开发者文档中关于代码风格（遵循 PEP 8）和提交规范（使用语义化提交信息）的说明，确保本地开发环境已安装所有开发依赖（requirements-dev.txt）。

2. 在 GitHub Issues 中查找标记为“help wanted”或“good first issue”的任务，或提交新 Issue 描述您发现的问题或希望增加的功能，等待维护者确认后再开始编码。

3. Fork 本仓库到您的个人账号，创建新的功能分支（命名格式为 feature/简短描述或 fix/问题编号），并在本地完成代码实现与单元测试，确保所有现有测试用例通过。

4. 提交代码时请附上清晰的 commit message，说明变更原因和具体改动。推送分支后，在原始仓库中发起 Pull Request，并在描述中关联对应的 Issue 编号。

5. PR 合并前需要至少一位维护者进行 Code Review，并根据反馈进行修订。合并后您的贡献将出现在下一版本的更新日志中，同时您将被列入贡献者列表。

## 常见问题

Q: 链接健康检查的频率和超时时间是否可以调整？
A: 可以。在 config.py 文件中，CHECK_INTERVAL_HOURS 变量控制检测间隔（默认 24 小时），REQUEST_TIMEOUT 变量控制单次请求超时（默认 10 秒）。修改后重启服务即可生效。对于频繁变更的链接，建议将间隔调整为 6 小时；对于稳定的长期资源，可延长至 72 小时以减少网络开销。

Q: 项目是否支持 PostgreSQL 替代 SQLite 作为生产数据库？
A: 支持。WebLink Navigator 使用 SQLAlchemy ORM，您只需在 config.py 中修改 DATABASE_URL 为 PostgreSQL 的连接字符串（格式为 postgresql://user:password@host/dbname），并安装 psycopg2-binary 依赖即可。迁移现有 SQLite 数据可使用 scripts/migrate_db.py 工具完成。

Q: 如何批量删除或归档不再使用的链接？
A: 在 Web 界面的链接列表页面，勾选目标条目后点击“批量操作”下拉菜单，可选择“删除”或“归档”。归档的链接将移入归档区，不再参与健康检查，但仍可搜索和恢复。若需按标签或状态条件批量处理，可使用 API 接口的批量更新端点，传递 filtered_ids 参数进行精确控制。

## 许可证

MIT

> 外链数量: 250 | 生成时间: 2026-08-24 23:40:21
