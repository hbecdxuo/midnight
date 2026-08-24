# Weblink Indexer

Weblink Indexer 是一个面向技术文档与外部资源链接的轻量级索引与导航系统。项目定位为技术团队或个人知识库中的外链统一管理入口，用于解决多源链接分散、访问状态不可追踪、分类混乱等问题。目标用户包括技术文档维护者、开源项目运营者、内部知识库管理员以及需要长期维护大量外链资源的开发者。

本系统不提供爬虫或自动采集功能，而是基于人工整理与静态数据驱动，输出结构化的链接清单、分类视图与基础状态标记。通过可扩展的数据格式和简单生成流程，Weblink Indexer 能够适配大多数静态站点生成器或内部文档平台。

## 功能概览

批量链接导入与结构化存储：支持将大量原始 URL 以列表形式导入系统，自动生成唯一标识并归入统一数据目录，每条链接保留原始地址、批次号、添加时间与自定义标签。

分类标签与多维度筛选：允许为每条链接赋予一个或多个分类标签，系统内置“技术博客”“官方文档”“社区论坛”“视频教程”“工具资源”五个基础分类，并支持自定义扩展。

链接状态检测：提供基于 HTTP 请求的状态码检测脚本，可定期检查链接可用性，标记失效或重定向链接，输出检测报告。

静态导航页面生成：内置基础模板引擎，可将链接数据渲染为 HTML 导航页面，支持按标签、按批次、按首字母排序展示，方便内网部署或静态托管。

数据导入导出：支持 JSON 与 CSV 格式的数据导入导出，便于与现有文档工具或电子表格软件对接。

搜索与过滤：提供命令行交互式搜索功能，支持按关键词、分类、状态码过滤链接列表，快速定位目标资源。

批次管理：每批次导入的链接自动记录批次编号与导入时间，支持批次整体删除、导出与统计，便于长期维护多期资源。

## 应用场景

技术文档站点维护：技术团队在维护产品文档时，需要引用大量外部参考链接。使用 Weblink Indexer 可统一管理这些引用源，定期检测有效性，避免文档中出现死链。

开源项目资源汇总：开源项目维护者可将社区贡献的教程、视频、衍生项目链接集中收录，按版本或主题分类，方便社区成员查阅。

内部知识库导航：企业内部的 Wiki 或知识库常包含数百个外部工具链接，通过本系统可构建一个轻量导航页，减少重复录入与散落问题。

个人学习资源整理：个人开发者可将每日阅读的技术文章、在线工具、官方手册等链接统一归档，配合状态检测及时发现失效资源。

批量链接迁移辅助：在更换文档平台或重构站点时，通过本系统的导入导出功能可快速迁移外链数据，保持链接结构一致。

## 快速开始

以下步骤适用于 Linux 与 macOS 环境，Windows 用户建议使用 WSL 或 Git Bash。

```bash
git clone https://github.com/weblink-indexer/weblink-indexer.git
cd weblink-indexer

pip install -r requirements.txt

python scripts/import_links.py --batch 84 --input ./data/batch_84.txt
python scripts/generate_index.py --batch 84 --output ./dist/index.html
python scripts/check_status.py --batch 84 --timeout 5
```

其中 `batch_84.txt` 为本次批次的原始链接列表文件，每行一个 URL。`import_links.py` 会将链接写入数据目录，`generate_index.py` 生成导航页面，`check_status.py` 执行状态检测。

## 安装要求

| 依赖 | 必需版本 | 说明 |
|------|----------|------|
| Python | 3.8 及以上 | 核心运行环境，用于执行导入、检测、生成脚本 |
| pip | 20.0 及以上 | Python 包管理工具，用于安装依赖库 |
| requests | 2.25.0 及以上 | 用于链接状态检测的 HTTP 请求库 |
| markdown | 3.3.0 及以上 | 用于将 README 中的 Markdown 列表解析为内部数据结构 |
| PyYAML | 5.4.0 及以上 | 用于解析可选的自定义配置文件（如标签映射） |
| jinja2 | 3.0.0 及以上 | 模板引擎，用于生成静态导航 HTML 页面 |
| pytest | 7.0.0 及以上 | 仅开发测试需要，生产环境可不安装 |
| flake8 | 5.0.0 及以上 | 仅代码风格检查需要，非运行时依赖 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|------|------|------------|
| 用户手册 | docs/user-guide.md | 如何导入链接、生成页面、检查状态、导出数据 |
| 配置说明 | docs/configuration.md | 如何自定义标签分类、模板路径、检测超时参数 |
| 开发者指南 | docs/developer-guide.md | 如何扩展数据模型、增加新的输出格式、编写测试 |
| 维护与排障 | docs/maintenance.md | 如何处理检测失败、如何清理失效链接、如何升级批次结构 |

## 资源列表

- http://m.blog.uliejh.cn/snews/09775.htm
- http://m.blog.uliejh.cn/snews/312133.htm
- http://m.blog.uliejh.cn/snews/9747779.htm
- http://m.blog.uliejh.cn/snews/09817.htm
- http://m.blog.uliejh.cn/snews/8065.htm
- http://m.blog.uliejh.cn/snews/4622652.htm
- http://m.blog.uliejh.cn/snews/9610.htm
- http://m.blog.uliejh.cn/snews/1123957.htm
- http://m.blog.uliejh.cn/snews/01042.htm
- http://m.blog.uliejh.cn/snews/4414193.htm
- http://m.blog.uliejh.cn/snews/35620.htm
- http://m.blog.uliejh.cn/snews/2144.htm
- http://m.blog.uliejh.cn/snews/5033.htm
- http://m.blog.uliejh.cn/snews/8473775.htm
- http://m.blog.uliejh.cn/snews/092262.htm
- http://m.blog.uliejh.cn/snews/30939.htm
- http://m.blog.uliejh.cn/snews/17718.htm
- http://m.blog.uliejh.cn/snews/5561586.htm
- http://m.blog.uliejh.cn/snews/33879.htm
- http://m.blog.uliejh.cn/snews/5812.htm
- http://m.blog.uliejh.cn/snews/4670121.htm
- http://m.blog.uliejh.cn/snews/0610510.htm
- http://m.blog.uliejh.cn/snews/4663683.htm
- http://m.blog.uliejh.cn/snews/79309.htm
- http://m.blog.uliejh.cn/snews/2982.htm
- http://m.blog.uliejh.cn/snews/1643.htm
- http://m.blog.uliejh.cn/snews/90592.htm
- http://m.blog.uliejh.cn/snews/8532.htm
- http://m.blog.uliejh.cn/snews/883875.htm
- http://m.blog.uliejh.cn/snews/59970.htm
- http://m.blog.uliejh.cn/snews/8376095.htm
- http://m.blog.uliejh.cn/snews/2789185.htm
- http://m.blog.uliejh.cn/snews/28508.htm
- http://m.blog.uliejh.cn/snews/00794.htm
- http://m.blog.uliejh.cn/snews/4354221.htm
- http://m.blog.uliejh.cn/snews/533305.htm
- http://m.blog.uliejh.cn/snews/209566.htm
- http://m.blog.uliejh.cn/snews/7188435.htm
- http://m.blog.uliejh.cn/snews/5347.htm
- http://m.blog.uliejh.cn/snews/7867.htm
- http://m.blog.uliejh.cn/snews/31635.htm
- http://m.blog.uliejh.cn/snews/1777.htm
- http://m.blog.uliejh.cn/snews/001322.htm
- http://m.blog.uliejh.cn/snews/182703.htm
- http://m.blog.uliejh.cn/snews/4309384.htm
- http://m.blog.uliejh.cn/snews/20466.htm
- http://m.blog.uliejh.cn/snews/5475.htm
- http://m.blog.uliejh.cn/snews/307555.htm
- http://m.blog.uliejh.cn/snews/7307908.htm
- http://m.blog.uliejh.cn/snews/132210.htm
- http://m.blog.uliejh.cn/snews/740174.htm
- http://m.blog.uliejh.cn/snews/69783.htm
- http://m.blog.uliejh.cn/snews/8132417.htm
- http://m.blog.uliejh.cn/snews/5609.htm
- http://m.blog.uliejh.cn/snews/201471.htm
- http://m.blog.uliejh.cn/snews/8322959.htm
- http://m.blog.uliejh.cn/snews/1179.htm
- http://m.blog.uliejh.cn/snews/663195.htm
- http://m.blog.uliejh.cn/snews/0459693.htm
- http://m.blog.uliejh.cn/snews/33688.htm
- http://m.blog.uliejh.cn/snews/37229.htm
- http://m.blog.uliejh.cn/snews/7975650.htm
- http://m.blog.uliejh.cn/snews/8745.htm
- http://m.blog.uliejh.cn/snews/1779.htm
- http://m.blog.uliejh.cn/snews/65434.htm
- http://m.blog.uliejh.cn/snews/5417572.htm
- http://m.blog.uliejh.cn/snews/8786530.htm
- http://m.blog.uliejh.cn/snews/33591.htm
- http://m.blog.uliejh.cn/snews/601820.htm
- http://m.blog.uliejh.cn/snews/4113118.htm
- http://m.blog.uliejh.cn/snews/84409.htm
- http://m.blog.uliejh.cn/snews/98748.htm
- http://m.blog.uliejh.cn/snews/43255.htm
- http://m.blog.uliejh.cn/snews/962666.htm
- http://m.blog.uliejh.cn/snews/81228.htm
- http://m.blog.uliejh.cn/snews/1644.htm
- http://m.blog.uliejh.cn/snews/8549419.htm
- http://m.blog.uliejh.cn/snews/16934.htm
- http://m.blog.uliejh.cn/snews/69148.htm
- http://m.blog.uliejh.cn/snews/3532392.htm
- http://m.blog.uliejh.cn/snews/687723.htm
- http://m.blog.uliejh.cn/snews/47433.htm
- http://m.blog.uliejh.cn/snews/11359.htm
- http://m.blog.uliejh.cn/snews/7271731.htm
- http://m.blog.uliejh.cn/snews/41025.htm
- http://m.blog.uliejh.cn/snews/9445838.htm
- http://m.blog.uliejh.cn/snews/6945.htm
- http://m.blog.uliejh.cn/snews/614315.htm
- http://m.blog.uliejh.cn/snews/137742.htm
- http://m.blog.uliejh.cn/snews/366548.htm
- http://m.blog.uliejh.cn/snews/1925881.htm
- http://m.blog.uliejh.cn/snews/446210.htm
- http://m.blog.uliejh.cn/snews/76282.htm
- http://m.blog.uliejh.cn/snews/1016.htm
- http://m.blog.uliejh.cn/snews/47787.htm
- http://m.blog.uliejh.cn/snews/3406770.htm
- http://m.blog.uliejh.cn/snews/305686.htm
- http://m.blog.uliejh.cn/snews/8000194.htm
- http://m.blog.uliejh.cn/snews/511793.htm
- http://m.blog.uliejh.cn/snews/3524969.htm
- http://m.blog.uliejh.cn/snews/314144.htm
- http://m.blog.uliejh.cn/snews/0959073.htm
- http://m.blog.uliejh.cn/snews/562916.htm
- http://m.blog.uliejh.cn/snews/74901.htm
- http://m.blog.uliejh.cn/snews/038659.htm
- http://m.blog.uliejh.cn/snews/086309.htm
- http://m.blog.uliejh.cn/snews/064262.htm
- http://m.blog.uliejh.cn/snews/7190963.htm
- http://m.blog.uliejh.cn/snews/981206.htm
- http://m.blog.uliejh.cn/snews/77354.htm
- http://m.blog.uliejh.cn/snews/44159.htm
- http://m.blog.uliejh.cn/snews/73670.htm
- http://m.blog.uliejh.cn/snews/12456.htm
- http://m.blog.uliejh.cn/snews/22316.htm
- http://m.blog.uliejh.cn/snews/849485.htm
- http://m.blog.uliejh.cn/snews/00545.htm
- http://m.blog.uliejh.cn/snews/9265.htm
- http://m.blog.uliejh.cn/snews/9506941.htm
- http://m.blog.uliejh.cn/snews/36142.htm
- http://m.blog.uliejh.cn/snews/597904.htm
- http://m.blog.uliejh.cn/snews/972524.htm
- http://m.blog.uliejh.cn/snews/6098.htm
- http://m.blog.uliejh.cn/snews/1676.htm
- http://m.blog.uliejh.cn/snews/3473472.htm
- http://m.blog.uliejh.cn/snews/9779.htm
- http://m.blog.uliejh.cn/snews/77177.htm
- http://m.blog.uliejh.cn/snews/03945.htm
- http://m.blog.uliejh.cn/snews/2282852.htm
- http://m.blog.uliejh.cn/snews/68338.htm
- http://m.blog.uliejh.cn/snews/816732.htm
- http://m.blog.uliejh.cn/snews/55821.htm
- http://m.blog.uliejh.cn/snews/26584.htm
- http://m.blog.uliejh.cn/snews/5498366.htm
- http://m.blog.uliejh.cn/snews/762591.htm
- http://m.blog.uliejh.cn/snews/7528.htm
- http://m.blog.uliejh.cn/snews/4167310.htm
- http://m.blog.uliejh.cn/snews/5927.htm
- http://m.blog.uliejh.cn/snews/25868.htm
- http://m.blog.uliejh.cn/snews/8910876.htm
- http://m.blog.uliejh.cn/snews/690478.htm
- http://m.blog.uliejh.cn/snews/7779394.htm
- http://m.blog.uliejh.cn/snews/9474.htm
- http://m.blog.uliejh.cn/snews/6366612.htm
- http://m.blog.uliejh.cn/snews/739228.htm
- http://m.blog.uliejh.cn/snews/9050881.htm
- http://m.blog.uliejh.cn/snews/6820282.htm
- http://m.blog.uliejh.cn/snews/17579.htm
- http://m.blog.uliejh.cn/snews/1104374.htm
- http://m.blog.uliejh.cn/snews/1193.htm
- http://m.blog.uliejh.cn/snews/94258.htm
- http://m.blog.uliejh.cn/snews/5248023.htm
- http://m.blog.uliejh.cn/snews/92217.htm
- http://m.blog.uliejh.cn/snews/695591.htm
- http://m.blog.uliejh.cn/snews/880610.htm
- http://m.blog.uliejh.cn/snews/60658.htm
- http://m.blog.uliejh.cn/snews/64599.htm
- http://m.blog.uliejh.cn/snews/132394.htm
- http://m.blog.uliejh.cn/snews/9402.htm
- http://m.blog.uliejh.cn/snews/1107700.htm
- http://m.blog.uliejh.cn/snews/1523.htm
- http://m.blog.uliejh.cn/snews/49707.htm
- http://m.blog.uliejh.cn/snews/2686.htm
- http://m.blog.uliejh.cn/snews/0640977.htm
- http://m.blog.uliejh.cn/snews/4094194.htm
- http://m.blog.uliejh.cn/snews/3074886.htm
- http://m.blog.uliejh.cn/snews/241804.htm
- http://m.blog.uliejh.cn/snews/2895.htm
- http://m.blog.uliejh.cn/snews/9577.htm
- http://m.blog.uliejh.cn/snews/9442.htm
- http://m.blog.uliejh.cn/snews/49178.htm
- http://m.blog.uliejh.cn/snews/3649.htm
- http://m.blog.uliejh.cn/snews/3338998.htm
- http://m.blog.uliejh.cn/snews/1816.htm
- http://m.blog.uliejh.cn/snews/1267.htm
- http://m.blog.uliejh.cn/snews/074418.htm
- http://m.blog.uliejh.cn/snews/9110995.htm
- http://m.blog.uliejh.cn/snews/613069.htm
- http://m.blog.uliejh.cn/snews/91124.htm
- http://m.blog.uliejh.cn/snews/97063.htm
- http://m.blog.uliejh.cn/snews/91513.htm
- http://m.blog.uliejh.cn/snews/357665.htm
- http://m.blog.uliejh.cn/snews/02241.htm
- http://m.blog.uliejh.cn/snews/877690.htm
- http://m.blog.uliejh.cn/snews/1622.htm
- http://m.blog.uliejh.cn/snews/2742085.htm
- http://m.blog.uliejh.cn/snews/8315535.htm
- http://m.blog.uliejh.cn/snews/92608.htm
- http://m.blog.uliejh.cn/snews/334718.htm
- http://m.blog.uliejh.cn/snews/540355.htm
- http://m.blog.uliejh.cn/snews/5554.htm
- http://m.blog.uliejh.cn/snews/9284175.htm
- http://m.blog.uliejh.cn/snews/3094.htm
- http://m.blog.uliejh.cn/snews/26646.htm
- http://m.blog.uliejh.cn/snews/941336.htm
- http://m.blog.uliejh.cn/snews/888980.htm
- http://m.blog.uliejh.cn/snews/8016.htm
- http://m.blog.uliejh.cn/snews/0276295.htm
- http://m.blog.uliejh.cn/snews/6283.htm
- http://m.blog.uliejh.cn/snews/83933.htm
- http://m.blog.uliejh.cn/snews/410953.htm
- http://m.blog.uliejh.cn/snews/8205.htm
- http://m.blog.uliejh.cn/snews/15992.htm
- http://m.blog.uliejh.cn/snews/3337.htm
- http://m.blog.uliejh.cn/snews/68952.htm
- http://m.blog.uliejh.cn/snews/94773.htm
- http://m.blog.uliejh.cn/snews/9586564.htm
- http://m.blog.uliejh.cn/snews/80030.htm
- http://m.blog.uliejh.cn/snews/4181.htm
- http://m.blog.uliejh.cn/snews/38717.htm
- http://m.blog.uliejh.cn/snews/1078215.htm
- http://m.blog.uliejh.cn/snews/650235.htm
- http://m.blog.uliejh.cn/snews/9214267.htm
- http://m.blog.uliejh.cn/snews/30499.htm
- http://m.blog.uliejh.cn/snews/6872.htm
- http://m.blog.uliejh.cn/snews/412678.htm
- http://m.blog.uliejh.cn/snews/1945.htm
- http://m.blog.uliejh.cn/snews/9762.htm
- http://m.blog.uliejh.cn/snews/78155.htm
- http://m.blog.uliejh.cn/snews/4673731.htm
- http://m.blog.uliejh.cn/snews/8735.htm
- http://m.blog.uliejh.cn/snews/22715.htm
- http://m.blog.uliejh.cn/snews/1011.htm
- http://m.blog.uliejh.cn/snews/79933.htm
- http://m.blog.uliejh.cn/snews/176898.htm
- http://m.blog.uliejh.cn/snews/172331.htm
- http://m.blog.uliejh.cn/snews/5191.htm
- http://m.blog.uliejh.cn/snews/4289025.htm
- http://m.blog.uliejh.cn/snews/3035.htm
- http://m.blog.uliejh.cn/snews/1876822.htm
- http://m.blog.uliejh.cn/snews/09201.htm
- http://m.blog.uliejh.cn/snews/490601.htm
- http://m.blog.uliejh.cn/snews/647260.htm
- http://m.blog.uliejh.cn/snews/11472.htm
- http://m.blog.uliejh.cn/snews/93960.htm
- http://m.blog.uliejh.cn/snews/91681.htm
- http://m.blog.uliejh.cn/snews/673687.htm
- http://m.blog.uliejh.cn/snews/384369.htm
- http://m.blog.uliejh.cn/snews/7945.htm
- http://m.blog.uliejh.cn/snews/52837.htm
- http://m.blog.uliejh.cn/snews/171948.htm
- http://m.blog.uliejh.cn/snews/8580501.htm
- http://m.blog.uliejh.cn/snews/20511.htm
- http://m.blog.uliejh.cn/snews/170266.htm
- http://m.blog.uliejh.cn/snews/523483.htm
- http://m.blog.uliejh.cn/snews/5125465.htm
- http://m.blog.uliejh.cn/snews/74279.htm
- http://m.blog.uliejh.cn/snews/398000.htm
- http://m.blog.uliejh.cn/snews/24661.htm
- http://m.blog.uliejh.cn/snews/6291084.htm
- http://m.blog.uliejh.cn/snews/5403.htm

## 项目结构

```
weblink-indexer/
├── data/                          # 数据存储目录，存放所有批次链接与元数据
│   ├── batches/                   # 各批次数据子目录，按批次编号命名
│   │   ├── batch_84.json          # 第84批次的链接对象列表，含原始URL与元信息
│   │   └── batch_84_status.json   # 第84批次的状态检测结果缓存
│   ├── tags/                      # 标签映射数据，存储自定义标签与链接ID的关联
│   │   └── custom_tags.yaml       # 用户自定义标签配置文件
│   └── schema/                    # 数据格式定义，JSON Schema用于校验
│       └── link_schema_v2.json    # 链接对象的结构定义
├── scripts/                       # 可执行脚本目录，包含核心功能入口
│   ├── import_links.py            # 从文本文件导入链接，生成batch JSON
│   ├── generate_index.py          # 读取数据并渲染HTML导航页面
│   ├── check_status.py            # 遍历链接执行HTTP状态检测并更新缓存
│   └── export_csv.py              # 导出指定批次为CSV格式
├── templates/                     # Jinja2模板目录，用于生成HTML页面
│   ├── index_template.html        # 导航页主模板
│   └── status_report_template.html # 状态报告页模板
├── tests/                         # 单元测试与集成测试目录
│   ├── test_import.py             # 导入模块的测试用例
│   ├── test_status.py             # 状态检测模块的测试用例
│   └── fixtures/                  # 测试用的固定数据样本
│       └── sample_batch.txt       # 示例链接列表文件
├── docs/                          # 用户与开发者文档，Markdown格式
│   ├── user-guide.md              # 用户操作手册
│   ├── configuration.md           # 配置项说明
│   ├── developer-guide.md         # 扩展开发指南
│   └── maintenance.md             # 日常维护与排障流程
├── requirements.txt               # Python依赖列表，含版本约束
├── setup.py                       # 包安装脚本，支持pip install -e .
├── LICENSE                        # MIT许可证文件
└── README.md                      # 本文件
```

## 贡献指南

提交链接资源：若您希望为某批次补充链接，请按现有数据格式提交Pull Request，在 `data/batches/` 目录下修改对应的JSON文件，并附带简短的添加说明。

改进检测逻辑：状态检测模块位于 `scripts/check_status.py`，欢迎提交优化超时重试、支持重定向追踪、增加自定义User-Agent等功能的补丁。

完善文档：文档位于 `docs/` 目录，若发现内容错误或缺失章节，请提交修改请求，建议同时说明适用场景或提供示例。

报告问题：请在Issues中详细描述问题现象，附上复现步骤、环境信息（Python版本、操作系统）以及相关日志输出。

代码风格：提交前请使用 `flake8` 检查代码风格，并确保 `pytest` 测试套件全部通过。

## 常见问题

Q: 导入链接时提示文件格式错误，如何处理？

A: 请确保输入文件为纯文本格式，每行一个URL，不含多余空格或空行。若使用Windows系统，请将换行符转换为LF格式。可使用 `dos2unix` 工具转换，或在VS Code中切换行尾序列。

Q: 状态检测脚本返回大量超时，可能是什么原因？

A: 可能原因包括：目标服务器限流、网络代理配置缺失、DNS解析延迟。建议调整 `--timeout` 参数至10秒以上，或使用 `--delay` 参数增加请求间隔。如果检测环境位于企业内网，请检查 `HTTP_PROXY` 环境变量。

Q: 生成的HTML导航页面样式能否自定义？

A: 可以。模板文件位于 `templates/` 目录，使用Jinja2语法。您可以修改 `index_template.html` 中的HTML结构与CSS样式，或替换为完全自定义的模板文件，并通过 `--template` 参数指定。

## 许可证

MIT

> 外链数量: 250 | 生成时间: 2026-08-24 23:40:21
