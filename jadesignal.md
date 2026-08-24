# LinkVault Resource Aggregator

LinkVault Resource Aggregator 是一个面向技术调研、舆情监测和内容聚合场景的轻量级外链资源归集系统。该项目定位于帮助数据分析师、内容运营人员以及独立开发者，将大量分散的 URL 资源进行集中化存储、分类标注与快速检索，降低人工整理成本，提升信息流转效率。

本项目不提供爬虫或采集功能，而是作为已有链接数据的结构化存储与管理前端。通过标准化的目录树组织与元数据配置，用户可将任意数量的外部链接按批次导入系统，并生成具备可读性的文档化输出。LinkVault 适用于中大型内容迁移、历史归档整理以及定期外链巡检等任务，支持批次管理（当前为第 27/120 批），并允许用户通过简单的标记系统对链接进行状态追踪。

## 功能概览

**批次化资源管理**：采用批次编号机制（批次号/总批次），支持多批次并行导入，每个批次独立记录导入时间与资源数量，便于审计与回溯。

**原样链接存储**：所有 URL 严格保留用户输入的原始格式，不自动补全协议头或域名前缀，不进行大小写转换或结尾斜杠修正，确保链接指纹一致性。

**多维度资源分类**：内置分类标签系统，用户可为每个链接分配主分类、子分类及自定义标签，支持按分类筛选和统计。

**结构化目录输出**：自动根据资源来源域名或路径特征生成 ASCII 目录树，以可视化方式展示链接仓库的层级关系，方便快速定位。

**快速检索与过滤**：基于链接 ID、来源域名、批次号、导入时间等字段提供命令行过滤接口，支持正则表达式匹配，便于从 250 个链接中快速筛选目标资源。

**状态跟踪与备注**：每个链接可附加状态标记（如待审、已读、无效、归档）和文本备注字段，支持后续人工审核与处理记录。

**跨平台终端兼容**：使用 Python 3 开发，依赖极少，可在 Linux、macOS、Windows WSL 环境下无缝运行，输出为纯 Markdown 格式，兼容主流文档平台。

## 应用场景

内容聚合网站的日常运维。编辑人员每日从多个信源收集数百条外部链接，在发布前需要统一整理、去重与归类。LinkVault 提供了批量导入与快速标注流程，可将原始链接列表快速转化为结构化的内部资源索引，减少人工排版与录入错误。

历史数据迁移与合规审计。企业进行旧站内容迁移或合规复查时，需对大量外链进行逐一验证。管理员可将待检链接一次性导入 LinkVault 的某个批次，利用状态标记功能记录每条链接的检测结果，并生成包含完整资源列表的审计报告供存档。

个人知识库的外链管理。独立研究者或技术博主在撰写文章或维护笔记时，常需要引用大量外部参考资料。使用 LinkVault 可以按项目或主题建立独立的链接仓库，每个仓库以批次为单位组织，方便后续回溯与引文校验。

离线环境下的资源清单维护。在无法连接外网的内网环境中，运维人员可借助 LinkVault 维护一份完整的资源地址清单，并定期导出为 Markdown 或 HTML 页面，作为离线文档的一部分交付给项目组使用。

## 快速开始

以下命令演示了如何从代码仓库克隆项目、安装依赖并运行一次完整的链接导入流程。

```bash
git clone https://github.com/your-org/linkvault.git
cd linkvault
pip install -r requirements.txt
python linkvault.py --batch 27 --total 120 --input urls_27.txt --output README.md
```

执行上述命令后，系统将读取 `urls_27.txt` 中的原始链接，生成符合本项目文档规范的 Markdown 资源列表，并输出至指定文件。用户可按需调整输出路径与批次编号。

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|----------|----------|------|
| Python  | 3.8 及以上 | 核心运行环境，提供标准库与语法支持 |
| pip     | 21.0 及以上 | 依赖包管理工具，用于安装第三方库 |
| Git     | 2.25 及以上 | 用于克隆项目仓库及版本控制 |
| Markdown 解析库 | markdown-it-py 2.0+ | 用于生成和验证输出的 Markdown 格式 |
| 文件系统权限 | 读写权限 | 需对输出目录有写入权限，对输入文件有读取权限 |
| 终端环境 | Bash/Zsh/ PowerShell | 支持命令行交互，用于执行脚本与参数传递 |
| 内存 | 512 MB 及以上 | 处理 250 条以内链接无需高内存占用 |
| 磁盘空间 | 50 MB 空闲 | 存放项目文件、日志及输出文档 |
| 操作系统 | Linux/macOS/Windows WSL2 | 保证路径解析与换行符兼容性 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|------|------|------------|
| 入门 | docs/quickstart.md | 如何三分钟完成首批资源导入并生成文档？ |
| 功能 | docs/batch-management.md | 批次如何创建、切换、合并和删除？ |
| 功能 | docs/link-annotation.md | 如何为链接添加分类、状态和备注信息？ |
| 运维 | docs/export-formats.md | 支持导出为哪些格式？如何自定义输出模板？ |
| 运维 | docs/validation-rules.md | 系统如何验证 URL 格式？哪些错误会被自动修正？ |
| 参考 | docs/cli-reference.md | 所有命令行参数的完整列表与使用示例。 |
| 参考 | docs/config-example.yml | 如何通过配置文件预设默认参数？ |

## 资源列表

- http://m.3g.uliejh.cn/nnews/40393.htm
- http://m.3g.uliejh.cn/nnews/112995.htm
- http://m.3g.uliejh.cn/nnews/726578.htm
- http://m.3g.uliejh.cn/nnews/578147.htm
- http://m.3g.uliejh.cn/nnews/590142.htm
- http://m.3g.uliejh.cn/nnews/6666946.htm
- http://m.3g.uliejh.cn/nnews/118626.htm
- http://m.3g.uliejh.cn/nnews/48998.htm
- http://m.3g.uliejh.cn/nnews/4395003.htm
- http://m.3g.uliejh.cn/nnews/8971434.htm
- http://m.3g.uliejh.cn/nnews/5757611.htm
- http://m.3g.uliejh.cn/nnews/2476.htm
- http://m.3g.uliejh.cn/nnews/9049859.htm
- http://m.3g.uliejh.cn/nnews/397361.htm
- http://m.3g.uliejh.cn/nnews/85604.htm
- http://m.3g.uliejh.cn/nnews/2695225.htm
- http://m.3g.uliejh.cn/nnews/0855689.htm
- http://m.3g.uliejh.cn/nnews/2277.htm
- http://m.3g.uliejh.cn/nnews/414783.htm
- http://m.3g.uliejh.cn/nnews/7766.htm
- http://m.3g.uliejh.cn/nnews/2309.htm
- http://m.3g.uliejh.cn/nnews/936860.htm
- http://m.3g.uliejh.cn/nnews/613134.htm
- http://m.3g.uliejh.cn/nnews/55072.htm
- http://m.3g.uliejh.cn/nnews/677383.htm
- http://m.3g.uliejh.cn/nnews/1597.htm
- http://m.3g.uliejh.cn/nnews/3369104.htm
- http://m.3g.uliejh.cn/nnews/27604.htm
- http://m.3g.uliejh.cn/nnews/25526.htm
- http://m.3g.uliejh.cn/nnews/90017.htm
- http://m.3g.uliejh.cn/nnews/920635.htm
- http://m.3g.uliejh.cn/nnews/26981.htm
- http://m.3g.uliejh.cn/nnews/1831699.htm
- http://m.3g.uliejh.cn/nnews/7866.htm
- http://m.3g.uliejh.cn/nnews/6990009.htm
- http://m.3g.uliejh.cn/nnews/5580.htm
- http://m.3g.uliejh.cn/nnews/1136288.htm
- http://m.3g.uliejh.cn/nnews/8390950.htm
- http://m.3g.uliejh.cn/nnews/85435.htm
- http://m.3g.uliejh.cn/nnews/901860.htm
- http://m.3g.uliejh.cn/nnews/41002.htm
- http://m.3g.uliejh.cn/nnews/1692955.htm
- http://m.3g.uliejh.cn/nnews/9626.htm
- http://m.3g.uliejh.cn/nnews/996758.htm
- http://m.3g.uliejh.cn/nnews/55766.htm
- http://m.3g.uliejh.cn/nnews/5730661.htm
- http://m.3g.uliejh.cn/nnews/1067.htm
- http://m.3g.uliejh.cn/nnews/168293.htm
- http://m.3g.uliejh.cn/nnews/9829.htm
- http://m.3g.uliejh.cn/nnews/19147.htm
- http://m.3g.uliejh.cn/nnews/1635055.htm
- http://m.3g.uliejh.cn/nnews/674804.htm
- http://m.3g.uliejh.cn/nnews/3553252.htm
- http://m.3g.uliejh.cn/nnews/1224.htm
- http://m.3g.uliejh.cn/nnews/0169103.htm
- http://m.3g.uliejh.cn/nnews/28020.htm
- http://m.3g.uliejh.cn/nnews/63668.htm
- http://m.3g.uliejh.cn/nnews/49709.htm
- http://m.3g.uliejh.cn/nnews/698654.htm
- http://m.3g.uliejh.cn/nnews/48881.htm
- http://m.3g.uliejh.cn/nnews/2896148.htm
- http://m.3g.uliejh.cn/nnews/766362.htm
- http://m.3g.uliejh.cn/nnews/454219.htm
- http://m.3g.uliejh.cn/nnews/1650.htm
- http://m.3g.uliejh.cn/nnews/76973.htm
- http://m.3g.uliejh.cn/nnews/1777687.htm
- http://m.3g.uliejh.cn/nnews/1989851.htm
- http://m.3g.uliejh.cn/nnews/6774618.htm
- http://m.3g.uliejh.cn/nnews/354158.htm
- http://m.3g.uliejh.cn/nnews/697812.htm
- http://m.3g.uliejh.cn/nnews/885812.htm
- http://m.3g.uliejh.cn/nnews/63495.htm
- http://m.3g.uliejh.cn/nnews/7516878.htm
- http://m.3g.uliejh.cn/nnews/485937.htm
- http://m.3g.uliejh.cn/nnews/8255692.htm
- http://m.3g.uliejh.cn/nnews/63015.htm
- http://m.3g.uliejh.cn/nnews/00803.htm
- http://m.3g.uliejh.cn/nnews/45253.htm
- http://m.3g.uliejh.cn/nnews/0015.htm
- http://m.3g.uliejh.cn/nnews/8188992.htm
- http://m.3g.uliejh.cn/nnews/2576925.htm
- http://m.3g.uliejh.cn/nnews/4211290.htm
- http://m.3g.uliejh.cn/nnews/7794077.htm
- http://m.3g.uliejh.cn/nnews/86927.htm
- http://m.3g.uliejh.cn/nnews/5491276.htm
- http://m.3g.uliejh.cn/nnews/5546139.htm
- http://m.3g.uliejh.cn/nnews/6255.htm
- http://m.3g.uliejh.cn/nnews/247832.htm
- http://m.3g.uliejh.cn/nnews/53678.htm
- http://m.3g.uliejh.cn/nnews/114204.htm
- http://m.3g.uliejh.cn/nnews/88349.htm
- http://m.3g.uliejh.cn/nnews/700376.htm
- http://m.3g.uliejh.cn/nnews/633069.htm
- http://m.3g.uliejh.cn/nnews/6966.htm
- http://m.3g.uliejh.cn/nnews/234712.htm
- http://m.3g.uliejh.cn/nnews/059371.htm
- http://m.3g.uliejh.cn/nnews/7070.htm
- http://m.3g.uliejh.cn/nnews/7675748.htm
- http://m.3g.uliejh.cn/nnews/1895680.htm
- http://m.3g.uliejh.cn/nnews/75398.htm
- http://m.3g.uliejh.cn/nnews/8114.htm
- http://m.3g.uliejh.cn/nnews/5192.htm
- http://m.3g.uliejh.cn/nnews/66188.htm
- http://m.3g.uliejh.cn/nnews/4653461.htm
- http://m.3g.uliejh.cn/nnews/9133.htm
- http://m.3g.uliejh.cn/nnews/87699.htm
- http://m.3g.uliejh.cn/nnews/7980.htm
- http://m.3g.uliejh.cn/nnews/8561.htm
- http://m.3g.uliejh.cn/nnews/6478485.htm
- http://m.3g.uliejh.cn/nnews/3462245.htm
- http://m.3g.uliejh.cn/nnews/7570.htm
- http://m.3g.uliejh.cn/nnews/6653.htm
- http://m.3g.uliejh.cn/nnews/3445470.htm
- http://m.3g.uliejh.cn/nnews/1421312.htm
- http://m.3g.uliejh.cn/nnews/128690.htm
- http://m.3g.uliejh.cn/nnews/127213.htm
- http://m.3g.uliejh.cn/nnews/46683.htm
- http://m.3g.uliejh.cn/nnews/1510573.htm
- http://m.3g.uliejh.cn/nnews/1601800.htm
- http://m.3g.uliejh.cn/nnews/240904.htm
- http://m.3g.uliejh.cn/nnews/4035.htm
- http://m.3g.uliejh.cn/nnews/7695.htm
- http://m.3g.uliejh.cn/nnews/765799.htm
- http://m.3g.uliejh.cn/nnews/9340133.htm
- http://m.3g.uliejh.cn/nnews/210023.htm
- http://m.3g.uliejh.cn/nnews/7187882.htm
- http://m.3g.uliejh.cn/nnews/9454329.htm
- http://m.3g.uliejh.cn/nnews/8966491.htm
- http://m.3g.uliejh.cn/nnews/4941211.htm
- http://m.3g.uliejh.cn/nnews/8032681.htm
- http://m.3g.uliejh.cn/nnews/1736576.htm
- http://m.3g.uliejh.cn/nnews/1980428.htm
- http://m.3g.uliejh.cn/nnews/9260.htm
- http://m.3g.uliejh.cn/nnews/7466267.htm
- http://m.3g.uliejh.cn/nnews/9027750.htm
- http://m.3g.uliejh.cn/nnews/3409622.htm
- http://m.3g.uliejh.cn/nnews/52000.htm
- http://m.3g.uliejh.cn/nnews/9616245.htm
- http://m.3g.uliejh.cn/nnews/273271.htm
- http://m.3g.uliejh.cn/nnews/496379.htm
- http://m.3g.uliejh.cn/nnews/6993636.htm
- http://m.3g.uliejh.cn/nnews/36605.htm
- http://m.3g.uliejh.cn/nnews/6826.htm
- http://m.3g.uliejh.cn/nnews/47543.htm
- http://m.3g.uliejh.cn/nnews/3482.htm
- http://m.3g.uliejh.cn/nnews/88795.htm
- http://m.3g.uliejh.cn/nnews/6450707.htm
- http://m.3g.uliejh.cn/nnews/2588480.htm
- http://m.3g.uliejh.cn/nnews/2753.htm
- http://m.3g.uliejh.cn/nnews/5395222.htm
- http://m.3g.uliejh.cn/nnews/1865277.htm
- http://m.3g.uliejh.cn/nnews/1059.htm
- http://m.3g.uliejh.cn/nnews/1762037.htm
- http://m.3g.uliejh.cn/nnews/5301953.htm
- http://m.3g.uliejh.cn/nnews/937343.htm
- http://m.3g.uliejh.cn/nnews/498905.htm
- http://m.3g.uliejh.cn/nnews/16922.htm
- http://m.3g.uliejh.cn/nnews/04650.htm
- http://m.3g.uliejh.cn/nnews/633075.htm
- http://m.3g.uliejh.cn/nnews/76003.htm
- http://m.3g.uliejh.cn/nnews/8625478.htm
- http://m.3g.uliejh.cn/nnews/9876.htm
- http://m.3g.uliejh.cn/nnews/316183.htm
- http://m.3g.uliejh.cn/nnews/4981.htm
- http://m.3g.uliejh.cn/nnews/3628326.htm
- http://m.3g.uliejh.cn/nnews/0970.htm
- http://m.3g.uliejh.cn/nnews/41099.htm
- http://m.3g.uliejh.cn/nnews/686239.htm
- http://m.3g.uliejh.cn/nnews/78406.htm
- http://m.3g.uliejh.cn/nnews/7059122.htm
- http://m.3g.uliejh.cn/nnews/893739.htm
- http://m.3g.uliejh.cn/nnews/407781.htm
- http://m.3g.uliejh.cn/nnews/63947.htm
- http://m.3g.uliejh.cn/nnews/093529.htm
- http://m.3g.uliejh.cn/nnews/631090.htm
- http://m.3g.uliejh.cn/nnews/0968280.htm
- http://m.3g.uliejh.cn/nnews/40245.htm
- http://m.3g.uliejh.cn/nnews/9142283.htm
- http://m.3g.uliejh.cn/nnews/0585.htm
- http://m.3g.uliejh.cn/nnews/297753.htm
- http://m.3g.uliejh.cn/nnews/990852.htm
- http://m.3g.uliejh.cn/nnews/96389.htm
- http://m.3g.uliejh.cn/nnews/157509.htm
- http://m.3g.uliejh.cn/nnews/6308.htm
- http://m.3g.uliejh.cn/nnews/4019310.htm
- http://m.3g.uliejh.cn/nnews/4543.htm
- http://m.3g.uliejh.cn/nnews/030564.htm
- http://m.3g.uliejh.cn/nnews/3594378.htm
- http://m.3g.uliejh.cn/nnews/8989337.htm
- http://m.3g.uliejh.cn/nnews/02011.htm
- http://m.3g.uliejh.cn/nnews/3468738.htm
- http://m.3g.uliejh.cn/nnews/427014.htm
- http://m.3g.uliejh.cn/nnews/2275.htm
- http://m.3g.uliejh.cn/nnews/026920.htm
- http://m.3g.uliejh.cn/nnews/757914.htm
- http://m.3g.uliejh.cn/nnews/2147879.htm
- http://m.3g.uliejh.cn/nnews/8597287.htm
- http://m.3g.uliejh.cn/nnews/1911758.htm
- http://m.3g.uliejh.cn/nnews/344351.htm
- http://m.3g.uliejh.cn/nnews/996611.htm
- http://m.3g.uliejh.cn/nnews/245743.htm
- http://m.3g.uliejh.cn/nnews/817426.htm
- http://m.3g.uliejh.cn/nnews/1637365.htm
- http://m.3g.uliejh.cn/nnews/0931774.htm
- http://m.3g.uliejh.cn/nnews/3658637.htm
- http://m.3g.uliejh.cn/nnews/4279359.htm
- http://m.3g.uliejh.cn/nnews/9364067.htm
- http://m.3g.uliejh.cn/nnews/9232.htm
- http://m.3g.uliejh.cn/nnews/738840.htm
- http://m.3g.uliejh.cn/nnews/822656.htm
- http://m.3g.uliejh.cn/nnews/5767198.htm
- http://m.3g.uliejh.cn/nnews/1206.htm
- http://m.3g.uliejh.cn/nnews/153534.htm
- http://m.3g.uliejh.cn/nnews/72485.htm
- http://m.3g.uliejh.cn/nnews/02713.htm
- http://m.3g.uliejh.cn/nnews/0359227.htm
- http://m.3g.uliejh.cn/nnews/055992.htm
- http://m.3g.uliejh.cn/nnews/164074.htm
- http://m.3g.uliejh.cn/nnews/3227360.htm
- http://m.3g.uliejh.cn/nnews/4513415.htm
- http://m.3g.uliejh.cn/nnews/7967295.htm
- http://m.3g.uliejh.cn/nnews/070950.htm
- http://m.3g.uliejh.cn/nnews/322953.htm
- http://m.3g.uliejh.cn/nnews/08387.htm
- http://m.3g.uliejh.cn/nnews/1627765.htm
- http://m.3g.uliejh.cn/nnews/79968.htm
- http://m.3g.uliejh.cn/nnews/661832.htm
- http://m.3g.uliejh.cn/nnews/3876289.htm
- http://m.3g.uliejh.cn/nnews/8995639.htm
- http://m.3g.uliejh.cn/nnews/84192.htm
- http://m.3g.uliejh.cn/nnews/22994.htm
- http://m.3g.uliejh.cn/nnews/18962.htm
- http://m.3g.uliejh.cn/nnews/0193133.htm
- http://m.3g.uliejh.cn/nnews/9853481.htm
- http://m.3g.uliejh.cn/nnews/285471.htm
- http://m.3g.uliejh.cn/nnews/6995139.htm
- http://m.3g.uliejh.cn/nnews/568481.htm
- http://m.3g.uliejh.cn/nnews/2316.htm
- http://m.3g.uliejh.cn/nnews/808635.htm
- http://m.3g.uliejh.cn/nnews/8973277.htm
- http://m.3g.uliejh.cn/nnews/5942.htm
- http://m.3g.uliejh.cn/nnews/7069.htm
- http://m.3g.uliejh.cn/nnews/4032.htm
- http://m.3g.uliejh.cn/nnews/2636.htm
- http://m.3g.uliejh.cn/nnews/6350284.htm
- http://m.3g.uliejh.cn/nnews/862474.htm
- http://m.3g.uliejh.cn/nnews/32344.htm
- http://m.3g.uliejh.cn/nnews/69923.htm
- http://m.3g.uliejh.cn/nnews/76576.htm
- http://m.3g.uliejh.cn/nnews/40895.htm

## 项目结构

```
linkvault/
├── README.md                     # 项目主文档，含简介、安装、资源列表
├── linkvault.py                  # 核心入口脚本，处理参数解析与流程调度
├── requirements.txt              # Python 依赖声明（markdown-it-py, pytest 等）
├── config/
│   ├── default.yml               # 默认系统配置（输出路径、批次编号格式）
│   └── schema.json               # 资源列表 JSON Schema 校验规则
├── core/
│   ├── importer.py               # 链接导入模块，读取原始文件并解析
│   ├── exporter.py               # 输出生成模块，渲染 Markdown 与 ASCII 树
│   ├── validator.py              # URL 格式校验器，检测协议头与非法字符
│   └── batch_manager.py          # 批次管理模块，维护批次元数据与状态
├── models/
│   ├── link.py                   # 链接数据模型定义（字段：id, url, status, tags）
│   └── batch.py                  # 批次数据模型（字段：batch_id, total, created_at）
├── utils/
│   ├── file_utils.py             # 文件读写工具（确保目录存在、编码检测）
│   └── logger.py                 # 日志记录模块，分级输出到控制台与文件
├── tests/
│   ├── test_importer.py          # 导入流程单元测试
│   ├── test_validator.py         # URL 校验规则测试用例
│   └── fixtures/                 # 测试用固定数据集（含样例 URL 列表）
├── docs/
│   ├── quickstart.md             # 快速上手指南
│   ├── cli-reference.md          # 命令行参数完整参考
│   └── api-design.md             # 内部模块接口设计说明
├── scripts/
│   ├── batch_import.sh           # 批量导入辅助 shell 脚本
│   └── generate_toc.py           # 自动生成目录树索引的工具脚本
└── .github/
    └── workflows/
        └── ci.yml                # GitHub Actions 持续集成配置（Python 3.8/3.9/3.10）
```

## 贡献指南

贡献者请遵循以下流程以确保代码质量和文档一致性。

1. 从 GitHub 仓库派生（Fork）项目至个人账号，并在本地克隆派生后的代码库。创建新分支时请使用功能前缀，例如 `feat/batch-merge` 或 `fix/url-encoding`。

2. 在本地环境运行完整的测试套件（`pytest tests/`）以确认现有功能未受影响。所有新增功能必须包含对应的单元测试用例，覆盖率不低于 85%。

3. 对核心模块或工具函数进行修改后，请同步更新 `docs/api-design.md` 中的接口说明。如涉及命令行参数变更，务必同步修改 `docs/cli-reference.md` 并更新 `config/default.yml` 中的默认值。

4. 提交前执行代码格式化工具 `black` 和静态检查 `flake8`，确保代码风格符合 PEP 8 规范。提交信息（commit message）应使用简洁的英文描述，格式为 `<type>: <subject>`，例如 `feat: add batch status filter`。

5. 发起 Pull Request 时，请在描述中说明修改动机、实现方式以及测试结果。项目维护者将在 3 个工作日内进行审查。如需讨论较大变更，建议先创建 Issue 进行技术方案沟通。

## 常见问题

**Q: 系统能否自动补全缺失的协议头（例如将 example.com 转为 https://example.com）？**

A: 不能。根据设计原则，LinkVault 严格保留用户输入的原始格式。这是为了避免自动补全导致的链接指纹变化，以及防止将原本指向本地文件或特定协议的路径误转为 HTTP 请求。用户应在导入前自行确认链接格式的正确性。如需批量添加协议头，可使用 `scripts/batch_import.sh` 中的预处理选项。

**Q: 如果单批次链接数量超过 500 条，系统性能是否受到影响？**

A: LinkVault 的核心操作均为内存级读写，单批次 500 条以内的链接处理时间通常在 2 秒以内。超过 1000 条时，建议按子主题拆分为多个批次，或使用 `--chunk-size` 参数分批写入输出文件。系统本身不限制批次上限，但生成单一 Markdown 文件过大时可能影响编辑器渲染性能。

**Q: 如何在不同批次间复制或移动链接？**

A: 当前版本不提供直接的跨批次移动命令。推荐做法是导出源批次为文本列表（使用 `--export` 参数），手动编辑后作为新批次的输入文件重新导入。系统会在导入时自动检测重复 URL（基于完整字符串匹配），并在日志中给出警告，但不强制去重，保留用户决策权。

## 许可证

MIT

> 外链数量: 250 | 生成时间: 2026-08-24 23:40:21
