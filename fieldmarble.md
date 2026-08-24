# WebLink Catalog System

WebLink Catalog System 是一个面向技术文档聚合与外部资源链接管理的开源项目，旨在为开发者、技术博主及内容运营团队提供一套轻量级、可扩展的外链汇总与导航方案。该项目定位于中大型技术文档站点的辅助工具，特别适用于需要批量维护外部参考链接、按批次组织资源条目、并对外提供统一访问入口的场景。

项目核心解决的是技术文档中外部链接分散、维护成本高、缺乏结构化元数据管理的问题。通过将原始链接列表转换为带分类标识、批次属性和基础校验能力的可维护数据集，WebLink Catalog System 帮助用户建立清晰的外链资源地图，同时保留原始 URL 的完整可溯源性。目标用户包括开源文档维护者、技术博客聚合平台运营方、以及企业内部知识库管理员。

## 功能概览

批量外链导入与规范化校验：支持从原始列表批量导入 URL，自动识别协议头、域名及路径结构，并对非标准格式条目输出警告日志。

批次管理与进度追踪：内置批次计数器与进度标记功能，当前版本支持第 47/120 批次的资源处理，并提供批次完成度百分比计算。

资源元数据自动补全：对每个链接条目自动生成资源编号、导入时间戳及基础状态标记（有效/待验证/已失效），便于后续筛查。

多维度筛选与检索：支持按资源编号段、域名前缀、文件扩展名（如 .htm）进行快速筛选，并提供正则表达式匹配接口。

结构化文档生成器：将资源列表按固定章节模板导出为 Markdown 文档，支持自定义批次说明和头部注释内容，方便直接用于 README 或 Wiki 页面。

依赖校验与环境检查：启动时自动检测运行环境是否满足最低依赖要求，并生成详细的缺失组件报告。

日志记录与故障隔离：每次批量操作均生成独立日志文件，单个链接解析失败不影响整体导入流程，错误信息记录至 logs/errors 目录。

## 应用场景

技术文档站点外链资源整编：技术团队在撰写产品文档或 API 参考时，需要引用大量外部标准或社区讨论链接。WebLink Catalog System 可用于统一收录这些引用来源，并为每个版本发布生成对应的外链清单，确保文档可追溯性。

开源项目 README 资源汇总：开源维护者需要定期更新项目首页中的相关资源列表（如社区教程、视频讲解、第三方工具）。本项目可直接将整理好的链接批次转换为符合 README 规范的资源列表章节，减少手动排版错误。

企业内部知识库外部参考管理：企业内部 Wiki 中常包含指向外部供应商、技术论坛或标准组织的链接。使用本项目可以对这类链接进行集中登记、定期有效性抽查，并在链接失效时快速定位相关文档页面。

批量链接迁移与域名替换辅助：当上游资源站更换域名或路径结构时，本项目支持基于前缀匹配的批量替换预览功能，帮助运维人员评估影响范围并生成迁移报告。

## 快速开始

```bash
# 克隆项目仓库
git clone https://github.com/weblink-catalog/weblink-catalog-system.git

# 进入项目目录
cd weblink-catalog-system

# 安装依赖（使用 pip 或 Poetry）
pip install -r requirements.txt

# 或使用 Poetry
poetry install

# 运行初始化命令，创建数据目录和配置文件
python cli.py init

# 导入当前批次资源（示例为第47批次）
python cli.py import --batch 47 --source list_47.txt

# 生成 Markdown 文档输出
python cli.py generate --batch 47 --output README_batch47.md
```

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|---|---|---|
| Python | 3.9 及以上 | 核心运行环境，低于此版本将导致类型注解解析失败 |
| requests | 2.28.0 及以上 | 用于链接可达性校验与元数据抓取 |
| pyyaml | 6.0 及以上 | 解析配置文件及批次元数据 YAML 格式 |
| click | 8.1.0 及以上 | 命令行交互框架，提供子命令解析能力 |
| loguru | 0.7.0 及以上 | 结构化日志输出，支持日志轮转与错误分级 |
| pytest | 7.4.0 及以上 | 单元测试框架（仅开发依赖，生产环境可不安装） |
| black | 23.0.0 及以上 | 代码格式化工具（仅开发依赖） |
| mypy | 1.5.0 及以上 | 静态类型检查（仅开发依赖） |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|---|---|---|
| 用户指南 | docs/user_guide.md | 如何安装、配置、导入第一批资源并生成文档输出 |
| 批次管理 | docs/batch_management.md | 批次编号规则、进度标记方法、多批次数据合并策略 |
| 故障排查 | docs/troubleshooting.md | 链接解析失败、依赖缺失、编码异常等常见问题的处理步骤 |
| 贡献者手册 | docs/contributor_guide.md | 代码风格、测试流程、Pull Request 提交规范及审核标准 |

## 资源列表

- http://m.wap.uliejh.cn/bnews/0886.htm
- http://m.wap.uliejh.cn/bnews/3761.htm
- http://m.wap.uliejh.cn/bnews/025192.htm
- http://m.wap.uliejh.cn/bnews/105430.htm
- http://m.wap.uliejh.cn/bnews/5670.htm
- http://m.wap.uliejh.cn/bnews/6119.htm
- http://m.wap.uliejh.cn/bnews/276199.htm
- http://m.wap.uliejh.cn/bnews/73860.htm
- http://m.wap.uliejh.cn/bnews/6999686.htm
- http://m.wap.uliejh.cn/bnews/0739.htm
- http://m.wap.uliejh.cn/bnews/07511.htm
- http://m.wap.uliejh.cn/bnews/11043.htm
- http://m.wap.uliejh.cn/bnews/690290.htm
- http://m.wap.uliejh.cn/bnews/0009184.htm
- http://m.wap.uliejh.cn/bnews/654522.htm
- http://m.wap.uliejh.cn/bnews/0978.htm
- http://m.wap.uliejh.cn/bnews/5817.htm
- http://m.wap.uliejh.cn/bnews/286923.htm
- http://m.wap.uliejh.cn/bnews/480980.htm
- http://m.wap.uliejh.cn/bnews/066202.htm
- http://m.wap.uliejh.cn/bnews/124266.htm
- http://m.wap.uliejh.cn/bnews/44036.htm
- http://m.wap.uliejh.cn/bnews/0127676.htm
- http://m.wap.uliejh.cn/bnews/15903.htm
- http://m.wap.uliejh.cn/bnews/77291.htm
- http://m.wap.uliejh.cn/bnews/47171.htm
- http://m.wap.uliejh.cn/bnews/5732.htm
- http://m.wap.uliejh.cn/bnews/56261.htm
- http://m.wap.uliejh.cn/bnews/0838.htm
- http://m.wap.uliejh.cn/bnews/45415.htm
- http://m.wap.uliejh.cn/bnews/7685797.htm
- http://m.wap.uliejh.cn/bnews/10346.htm
- http://m.wap.uliejh.cn/bnews/95336.htm
- http://m.wap.uliejh.cn/bnews/3044.htm
- http://m.wap.uliejh.cn/bnews/3592032.htm
- http://m.wap.uliejh.cn/bnews/250421.htm
- http://m.wap.uliejh.cn/bnews/0405.htm
- http://m.wap.uliejh.cn/bnews/5694.htm
- http://m.wap.uliejh.cn/bnews/7969191.htm
- http://m.wap.uliejh.cn/bnews/55487.htm
- http://m.wap.uliejh.cn/bnews/58018.htm
- http://m.wap.uliejh.cn/bnews/06578.htm
- http://m.wap.uliejh.cn/bnews/56299.htm
- http://m.wap.uliejh.cn/bnews/6214438.htm
- http://m.wap.uliejh.cn/bnews/22234.htm
- http://m.wap.uliejh.cn/bnews/744299.htm
- http://m.wap.uliejh.cn/bnews/977639.htm
- http://m.wap.uliejh.cn/bnews/406825.htm
- http://m.wap.uliejh.cn/bnews/94909.htm
- http://m.wap.uliejh.cn/bnews/87606.htm
- http://m.wap.uliejh.cn/bnews/8947.htm
- http://m.wap.uliejh.cn/bnews/0892950.htm
- http://m.wap.uliejh.cn/bnews/4765619.htm
- http://m.wap.uliejh.cn/bnews/099067.htm
- http://m.wap.uliejh.cn/bnews/2839735.htm
- http://m.wap.uliejh.cn/bnews/8137.htm
- http://m.wap.uliejh.cn/bnews/8050714.htm
- http://m.wap.uliejh.cn/bnews/5578497.htm
- http://m.wap.uliejh.cn/bnews/72981.htm
- http://m.wap.uliejh.cn/bnews/1456809.htm
- http://m.wap.uliejh.cn/bnews/4132386.htm
- http://m.wap.uliejh.cn/bnews/6186.htm
- http://m.wap.uliejh.cn/bnews/138904.htm
- http://m.wap.uliejh.cn/bnews/1868969.htm
- http://m.wap.uliejh.cn/bnews/7322.htm
- http://m.wap.uliejh.cn/bnews/15458.htm
- http://m.wap.uliejh.cn/bnews/4226509.htm
- http://m.wap.uliejh.cn/bnews/84347.htm
- http://m.wap.uliejh.cn/bnews/1490821.htm
- http://m.wap.uliejh.cn/bnews/47993.htm
- http://m.wap.uliejh.cn/bnews/99229.htm
- http://m.wap.uliejh.cn/bnews/219638.htm
- http://m.wap.uliejh.cn/bnews/4511100.htm
- http://m.wap.uliejh.cn/bnews/60059.htm
- http://m.wap.uliejh.cn/bnews/153480.htm
- http://m.wap.uliejh.cn/bnews/2946.htm
- http://m.wap.uliejh.cn/bnews/2461258.htm
- http://m.wap.uliejh.cn/bnews/8876908.htm
- http://m.wap.uliejh.cn/bnews/9245879.htm
- http://m.wap.uliejh.cn/bnews/579944.htm
- http://m.wap.uliejh.cn/bnews/8289.htm
- http://m.wap.uliejh.cn/bnews/3821.htm
- http://m.wap.uliejh.cn/bnews/131986.htm
- http://m.wap.uliejh.cn/bnews/77920.htm
- http://m.wap.uliejh.cn/bnews/1684.htm
- http://m.wap.uliejh.cn/bnews/81824.htm
- http://m.wap.uliejh.cn/bnews/634755.htm
- http://m.wap.uliejh.cn/bnews/0873.htm
- http://m.wap.uliejh.cn/bnews/00242.htm
- http://m.wap.uliejh.cn/bnews/009527.htm
- http://m.wap.uliejh.cn/bnews/9407.htm
- http://m.wap.uliejh.cn/bnews/71827.htm
- http://m.wap.uliejh.cn/bnews/73892.htm
- http://m.wap.uliejh.cn/bnews/46300.htm
- http://m.wap.uliejh.cn/bnews/16765.htm
- http://m.wap.uliejh.cn/bnews/59272.htm
- http://m.wap.uliejh.cn/bnews/608041.htm
- http://m.wap.uliejh.cn/bnews/1967.htm
- http://m.wap.uliejh.cn/bnews/626468.htm
- http://m.wap.uliejh.cn/bnews/930746.htm
- http://m.wap.uliejh.cn/bnews/6959.htm
- http://m.wap.uliejh.cn/bnews/287327.htm
- http://m.wap.uliejh.cn/bnews/988594.htm
- http://m.wap.uliejh.cn/bnews/2583.htm
- http://m.wap.uliejh.cn/bnews/2946448.htm
- http://m.wap.uliejh.cn/bnews/48899.htm
- http://m.wap.uliejh.cn/bnews/42135.htm
- http://m.wap.uliejh.cn/bnews/205413.htm
- http://m.wap.uliejh.cn/bnews/04794.htm
- http://m.wap.uliejh.cn/bnews/66076.htm
- http://m.wap.uliejh.cn/bnews/6212902.htm
- http://m.wap.uliejh.cn/bnews/677161.htm
- http://m.wap.uliejh.cn/bnews/8067511.htm
- http://m.wap.uliejh.cn/bnews/7696.htm
- http://m.wap.uliejh.cn/bnews/02436.htm
- http://m.wap.uliejh.cn/bnews/1160.htm
- http://m.wap.uliejh.cn/bnews/122345.htm
- http://m.wap.uliejh.cn/bnews/1128243.htm
- http://m.wap.uliejh.cn/bnews/83508.htm
- http://m.wap.uliejh.cn/bnews/455531.htm
- http://m.wap.uliejh.cn/bnews/1091453.htm
- http://m.wap.uliejh.cn/bnews/4462277.htm
- http://m.wap.uliejh.cn/bnews/6490.htm
- http://m.wap.uliejh.cn/bnews/96928.htm
- http://m.wap.uliejh.cn/bnews/28688.htm
- http://m.wap.uliejh.cn/bnews/9090.htm
- http://m.wap.uliejh.cn/bnews/534082.htm
- http://m.wap.uliejh.cn/bnews/39407.htm
- http://m.wap.uliejh.cn/bnews/5232.htm
- http://m.wap.uliejh.cn/bnews/7962335.htm
- http://m.wap.uliejh.cn/bnews/401856.htm
- http://m.wap.uliejh.cn/bnews/9155.htm
- http://m.wap.uliejh.cn/bnews/1746010.htm
- http://m.wap.uliejh.cn/bnews/29804.htm
- http://m.wap.uliejh.cn/bnews/903498.htm
- http://m.wap.uliejh.cn/bnews/2407582.htm
- http://m.wap.uliejh.cn/bnews/76550.htm
- http://m.wap.uliejh.cn/bnews/8401.htm
- http://m.wap.uliejh.cn/bnews/480636.htm
- http://m.wap.uliejh.cn/bnews/8965703.htm
- http://m.wap.uliejh.cn/bnews/8526905.htm
- http://m.wap.uliejh.cn/bnews/4558632.htm
- http://m.wap.uliejh.cn/bnews/7542898.htm
- http://m.wap.uliejh.cn/bnews/69569.htm
- http://m.wap.uliejh.cn/bnews/0376390.htm
- http://m.wap.uliejh.cn/bnews/264952.htm
- http://m.wap.uliejh.cn/bnews/5094.htm
- http://m.wap.uliejh.cn/bnews/0814.htm
- http://m.wap.uliejh.cn/bnews/478504.htm
- http://m.wap.uliejh.cn/bnews/88819.htm
- http://m.wap.uliejh.cn/bnews/5678089.htm
- http://m.wap.uliejh.cn/bnews/6322913.htm
- http://m.wap.uliejh.cn/bnews/86818.htm
- http://m.wap.uliejh.cn/bnews/1779995.htm
- http://m.wap.uliejh.cn/bnews/18955.htm
- http://m.wap.uliejh.cn/bnews/8895850.htm
- http://m.wap.uliejh.cn/bnews/2563913.htm
- http://m.wap.uliejh.cn/bnews/3307.htm
- http://m.wap.uliejh.cn/bnews/20658.htm
- http://m.wap.uliejh.cn/bnews/4123134.htm
- http://m.wap.uliejh.cn/bnews/0078384.htm
- http://m.wap.uliejh.cn/bnews/528747.htm
- http://m.wap.uliejh.cn/bnews/0585061.htm
- http://m.wap.uliejh.cn/bnews/2719908.htm
- http://m.wap.uliejh.cn/bnews/7588.htm
- http://m.wap.uliejh.cn/bnews/7759.htm
- http://m.wap.uliejh.cn/bnews/9680.htm
- http://m.wap.uliejh.cn/bnews/6520.htm
- http://m.wap.uliejh.cn/bnews/1457.htm
- http://m.wap.uliejh.cn/bnews/51789.htm
- http://m.wap.uliejh.cn/bnews/091345.htm
- http://m.wap.uliejh.cn/bnews/7974800.htm
- http://m.wap.uliejh.cn/bnews/6794.htm
- http://m.wap.uliejh.cn/bnews/840255.htm
- http://m.wap.uliejh.cn/bnews/6752.htm
- http://m.wap.uliejh.cn/bnews/4480185.htm
- http://m.wap.uliejh.cn/bnews/5367.htm
- http://m.wap.uliejh.cn/bnews/72636.htm
- http://m.wap.uliejh.cn/bnews/29692.htm
- http://m.wap.uliejh.cn/bnews/797302.htm
- http://m.wap.uliejh.cn/bnews/546870.htm
- http://m.wap.uliejh.cn/bnews/444492.htm
- http://m.wap.uliejh.cn/bnews/721679.htm
- http://m.wap.uliejh.cn/bnews/2488194.htm
- http://m.wap.uliejh.cn/bnews/6358.htm
- http://m.wap.uliejh.cn/bnews/1382.htm
- http://m.wap.uliejh.cn/bnews/94502.htm
- http://m.wap.uliejh.cn/bnews/2371420.htm
- http://m.wap.uliejh.cn/bnews/23040.htm
- http://m.wap.uliejh.cn/bnews/110345.htm
- http://m.wap.uliejh.cn/bnews/744761.htm
- http://m.wap.uliejh.cn/bnews/163202.htm
- http://m.wap.uliejh.cn/bnews/98001.htm
- http://m.wap.uliejh.cn/bnews/573969.htm
- http://m.wap.uliejh.cn/bnews/29634.htm
- http://m.wap.uliejh.cn/bnews/81112.htm
- http://m.wap.uliejh.cn/bnews/510984.htm
- http://m.wap.uliejh.cn/bnews/95525.htm
- http://m.wap.uliejh.cn/bnews/830025.htm
- http://m.wap.uliejh.cn/bnews/508493.htm
- http://m.wap.uliejh.cn/bnews/6326.htm
- http://m.wap.uliejh.cn/bnews/362657.htm
- http://m.wap.uliejh.cn/bnews/406157.htm
- http://m.wap.uliejh.cn/bnews/900135.htm
- http://m.wap.uliejh.cn/bnews/0009.htm
- http://m.wap.uliejh.cn/bnews/2297.htm
- http://m.wap.uliejh.cn/bnews/10281.htm
- http://m.wap.uliejh.cn/bnews/69074.htm
- http://m.wap.uliejh.cn/bnews/7532309.htm
- http://m.wap.uliejh.cn/bnews/26846.htm
- http://m.wap.uliejh.cn/bnews/5239883.htm
- http://m.wap.uliejh.cn/bnews/386503.htm
- http://m.wap.uliejh.cn/bnews/69525.htm
- http://m.wap.uliejh.cn/bnews/8992812.htm
- http://m.wap.uliejh.cn/bnews/7872.htm
- http://m.wap.uliejh.cn/bnews/12145.htm
- http://m.wap.uliejh.cn/bnews/0662.htm
- http://m.wap.uliejh.cn/bnews/8692.htm
- http://m.wap.uliejh.cn/bnews/0390.htm
- http://m.wap.uliejh.cn/bnews/030374.htm
- http://m.wap.uliejh.cn/bnews/63135.htm
- http://m.wap.uliejh.cn/bnews/811996.htm
- http://m.wap.uliejh.cn/bnews/87356.htm
- http://m.wap.uliejh.cn/bnews/7111072.htm
- http://m.wap.uliejh.cn/bnews/2369902.htm
- http://m.wap.uliejh.cn/bnews/72959.htm
- http://m.wap.uliejh.cn/bnews/2943.htm
- http://m.wap.uliejh.cn/bnews/47720.htm
- http://m.wap.uliejh.cn/bnews/17860.htm
- http://m.wap.uliejh.cn/bnews/15306.htm
- http://m.wap.uliejh.cn/bnews/5852446.htm
- http://m.wap.uliejh.cn/bnews/2824522.htm
- http://m.wap.uliejh.cn/bnews/959076.htm
- http://m.wap.uliejh.cn/bnews/23061.htm
- http://m.wap.uliejh.cn/bnews/96463.htm
- http://m.wap.uliejh.cn/bnews/82316.htm
- http://m.wap.uliejh.cn/bnews/60750.htm
- http://m.wap.uliejh.cn/bnews/97328.htm
- http://m.wap.uliejh.cn/bnews/5250898.htm
- http://m.wap.uliejh.cn/bnews/5685.htm
- http://m.wap.uliejh.cn/bnews/16594.htm
- http://m.wap.uliejh.cn/bnews/1705899.htm
- http://m.wap.uliejh.cn/bnews/54375.htm
- http://m.wap.uliejh.cn/bnews/29907.htm
- http://m.wap.uliejh.cn/bnews/59076.htm
- http://m.wap.uliejh.cn/bnews/70171.htm
- http://m.wap.uliejh.cn/bnews/7463944.htm
- http://m.wap.uliejh.cn/bnews/1524124.htm
- http://m.wap.uliejh.cn/bnews/6244.htm
- http://m.wap.uliejh.cn/bnews/1856.htm

## 项目结构

```
weblink-catalog-system/
├── cli.py                      # 命令行入口，注册 init/import/generate 子命令
├── config/
│   ├── default.yaml            # 默认配置，含日志级别、批次大小、超时阈值
│   └── schema.json             # 配置文件 JSON Schema 校验定义
├── core/
│   ├── __init__.py
│   ├── importer.py             # 批量导入核心逻辑，含 URL 解析与校验
│   ├── batch.py                # 批次管理，含进度计算与状态持久化
│   └── validator.py            # 链接协议、路径格式及可达性检查
├── models/
│   ├── __init__.py
│   ├── resource.py             # Resource 数据类定义，含编号、URL、时间戳
│   └── batch_meta.py           # BatchMeta 数据类，含批次号、总数、完成标记
├── generators/
│   ├── __init__.py
│   ├── markdown.py             # Markdown 文档生成器，按模板输出章节
│   └── html.py                 # HTML 预览生成器（可选扩展）
├── utils/
│   ├── __init__.py
│   ├── logger.py               # loguru 日志封装，含文件轮转与错误分级
│   └── file_utils.py           # 文件读写、目录创建、编码检测工具
├── logs/
│   ├── access.log              # 常规操作日志
│   └── errors/                 # 错误日志按日期分文件存储
├── data/
│   ├── batches/                # 按批次存储资源清单 JSON 文件
│   └── meta/                   # 全局元数据及批次索引
├── tests/
│   ├── unit/                   # 单元测试用例，覆盖 importer/validator 模块
│   └── fixtures/               # 测试用固定数据集
├── docs/                       # 文档目录，包含用户指南与贡献手册
├── requirements.txt            # 生产环境依赖列表
├── pyproject.toml              # Poetry 项目定义，含依赖与构建配置
└── README.md                   # 项目首页文档（本文件）
```

## 贡献指南

提交 Issue 报告缺陷或功能建议：请在 GitHub Issues 页面选择对应模板，清晰描述复现步骤、预期行为与实际结果，并附上相关日志片段或配置文件示例。

创建功能分支并遵循代码规范：从 main 分支签出新的 feature/xxx 分支，提交前运行 black 与 mypy 进行格式检查和类型校验，确保无警告或错误。

编写或更新单元测试：新增功能或修复缺陷时，需在 tests/unit 目录下补充对应的测试用例，确保代码覆盖率不低于 85%。

提交 Pull Request 并关联 Issue：在 PR 描述中关联相关 Issue 编号，详细说明变更内容、测试结果及文档更新情况，等待至少一位维护者审核。

更新文档与示例：若变更影响用户操作流程，需同步更新 docs 目录下的对应手册，并在 PR 中标注文档已同步修改。

## 常见问题

Q: 导入链接时提示 "URL scheme 不支持"，该如何处理？

A: 本项目当前仅支持 http 与 https 协议。请检查原始链接是否包含其他协议头（如 ftp、file），若确需支持，可修改 core/validator.py 中的 SCHEME_WHITELIST 列表并重新运行。对于裸域名或缺少协议头的条目，系统会自动尝试补充 http://，但建议在导入前统一处理源数据格式。

Q: 批量生成 Markdown 文档时，资源列表顺序与导入时不一致？

A: 生成器默认按照资源编号升序输出，编号由导入顺序自动分配。若需保持原始列表顺序，可在生成命令中添加 --preserve-order 参数。同时注意，若批次数据中包含重复 URL，系统会保留首次出现的条目并记录警告日志，重复项不会再次写入输出文档。

Q: 如何迁移已有批次数据到新版本？

A: 从 v1.x 升级至 v2.x 时，运行 python cli.py migrate --batch 47 --target-version 2.0 命令，系统会自动读取旧格式 JSON 文件，补全新版本所需的元数据字段，并备份原始文件至 data/backup 目录。迁移完成后建议使用 validate 子命令校验数据完整性。

## 许可证

MIT

> 外链数量: 250 | 生成时间: 2026-08-24 23:40:21
