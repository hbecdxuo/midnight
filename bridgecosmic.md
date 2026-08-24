# LinkVault Core

LinkVault Core 是一个面向技术内容聚合与外部资源归档的开源工具集，定位于为开发者、技术博主、研究机构以及企业知识管理部门提供轻量级、可扩展的外链管理与批量导入能力。该项目主要解决大规模 URL 数据集的导入、去重、状态监控、标签分类与快速检索问题，适用于需要将大量分散外部链接纳入统一本地知识库或内容索引体系的场景。LinkVault Core 不依赖外部数据库或云服务，以纯文件系统与内存索引为核心，可运行于 Linux、macOS 及 Windows 环境下的标准命令行终端。

## 功能概览

批量 URL 导入解析：支持从纯文本文件、CSV 以及标准输入流中读取大量 URL 记录，自动识别协议头、查询参数及片段标识，并生成唯一内部标识符用于后续跟踪。

链接状态实时探测：内置异步 HTTP 客户端，可并发检查 URL 可达性、响应状态码、内容类型及响应时间，支持自定义超时与重试策略，便于识别失效或重定向链接。

多级标签分类系统：允许用户为每条链接附加一个或多个文本标签，支持层级命名空间（如 "backend/database/mysql"），并基于标签进行快速筛选与统计。

增量数据存储引擎：基于 LMDB 嵌入式键值存储，提供毫秒级读写性能，支持增量导入与更新，避免全量重写，适合百万级链接规模。

结构化目录导出：可将导入的链接数据按标签、域名或导入批次导出为 JSON、YAML 或 Markdown 表格格式，便于生成静态站点资源列表或外部报告。

命令行交互与脚本集成：提供完整的 CLI 子命令体系，包括 import、check、tag、search、export 和 clean，支持通过管道组合与 shell 脚本自动化调用。

内存与磁盘占用监控：内置资源使用计量模块，可在长时间运行任务中输出处理速率、内存占用峰值及磁盘 I/O 统计，方便运维调优。

## 应用场景

技术博客外链归档：技术作者可将多年积累的参考链接批量导入 LinkVault Core，定期运行状态检查，自动标记已失效链接，并在博客迁移时统一导出为兼容格式。

企业合规性链接审计：法务或信息安全团队可利用该工具导入外部政策页面、第三方服务条款链接，通过标签标注审核状态，并生成周期性可达性报告。

科研文献数据溯源：研究人员在整理论文引用或数据集来源时，可将数百个外部数据源 URL 集中管理，按项目、机构、时间范围分类，便于长期维护与协作共享。

DevOps 监控链接聚合：运维团队可将内部监控面板、日志查询入口、报警管理页面的 URL 汇总导入，结合状态探测快速发现内部服务入口异常。

开源项目文档外链维护：开源项目维护者可将 README、Wiki、官网中引用的所有外部链接统一纳入 LinkVault Core，在版本发布前校验链接有效性，避免文档中出现死链。

## 快速开始

以下命令演示了从克隆仓库到运行基础导入检查的完整流程。

```bash
git clone https://github.com/linkvault/core.git linkvault-core
cd linkvault-core
make build
./bin/linkvault import --input ./samples/urls.txt --batch 117
./bin/linkvault check --batch 117 --concurrency 50
./bin/linkvault export --batch 117 --format markdown --output ./exports/batch_117.md
```

若使用 Docker 环境，可执行以下命令快速启动：

```bash
docker build -t linkvault/core:latest .
docker run -v $(pwd)/data:/data linkvault/core:latest import --input /data/urls.txt
```

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|---------|---------|------|
| C 编译器 (gcc / clang) | 4.8 或更高 | 用于编译 LMDB 及内部 C 扩展模块 |
| Rust 工具链 | 1.70.0 或更高 | 核心异步运行时与 HTTP 客户端基于 Rust 实现 |
| Make | 3.81 或更高 | 构建脚本与任务编排依赖 |
| OpenSSL 开发库 | 1.1.1 或更高 | 提供 HTTPS 连接所需的 TLS 实现 |
| 磁盘可用空间 | 至少 200 MB | 存放二进制文件、LMDB 数据文件及临时缓存 |
| 内存 | 建议 512 MB 以上 | 并发检查时内存占用随并发数线性增长 |
| 操作系统 | Linux 内核 4.0+ / macOS 10.15+ / Windows 10+ | 需支持异步 I/O 及线程局部存储 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|------|------|-----------|
| 用户手册 | docs/user-guide/quick-start.md | 如何安装、导入第一批链接、执行状态检查？ |
| 配置参考 | docs/reference/config.md | 所有环境变量、配置文件参数及默认值是什么？ |
| 开发指南 | docs/development/architecture.md | 项目模块划分、数据流方向及关键数据结构如何设计？ |
| 运维调优 | docs/operations/tuning.md | 在大规模链接集下如何调整并发、缓存与日志级别？ |

完整文档目录位于 docs/ 根目录，包含 API 设计说明、错误码对照表及性能测试报告。

## 资源列表

- http://m.blog.uliejh.cn/snews/4489.htm
- http://m.blog.uliejh.cn/snews/83828.htm
- http://m.blog.uliejh.cn/snews/1034.htm
- http://m.blog.uliejh.cn/snews/6253978.htm
- http://m.blog.uliejh.cn/snews/4877993.htm
- http://m.blog.uliejh.cn/snews/827296.htm
- http://m.blog.uliejh.cn/snews/80109.htm
- http://m.blog.uliejh.cn/snews/0752186.htm
- http://m.blog.uliejh.cn/snews/60922.htm
- http://m.blog.uliejh.cn/snews/2694346.htm
- http://m.blog.uliejh.cn/snews/0988.htm
- http://m.blog.uliejh.cn/snews/5463.htm
- http://m.blog.uliejh.cn/snews/9934.htm
- http://m.blog.uliejh.cn/snews/0236.htm
- http://m.blog.uliejh.cn/snews/0547254.htm
- http://m.blog.uliejh.cn/snews/5090.htm
- http://m.blog.uliejh.cn/snews/2142606.htm
- http://m.blog.uliejh.cn/snews/74673.htm
- http://m.blog.uliejh.cn/snews/0263.htm
- http://m.blog.uliejh.cn/snews/812942.htm
- http://m.blog.uliejh.cn/snews/27153.htm
- http://m.blog.uliejh.cn/snews/3240.htm
- http://m.blog.uliejh.cn/snews/386139.htm
- http://m.blog.uliejh.cn/snews/80134.htm
- http://m.blog.uliejh.cn/snews/97606.htm
- http://m.blog.uliejh.cn/snews/5037.htm
- http://m.blog.uliejh.cn/snews/79407.htm
- http://m.blog.uliejh.cn/snews/2697.htm
- http://m.blog.uliejh.cn/snews/3664.htm
- http://m.blog.uliejh.cn/snews/8350654.htm
- http://m.blog.uliejh.cn/snews/264233.htm
- http://m.blog.uliejh.cn/snews/367804.htm
- http://m.blog.uliejh.cn/snews/5757.htm
- http://m.blog.uliejh.cn/snews/387471.htm
- http://m.blog.uliejh.cn/snews/9989.htm
- http://m.blog.uliejh.cn/snews/1136488.htm
- http://m.blog.uliejh.cn/snews/0099.htm
- http://m.blog.uliejh.cn/snews/0592.htm
- http://m.blog.uliejh.cn/snews/43242.htm
- http://m.blog.uliejh.cn/snews/6562792.htm
- http://m.blog.uliejh.cn/snews/8812.htm
- http://m.blog.uliejh.cn/snews/4134.htm
- http://m.blog.uliejh.cn/snews/610808.htm
- http://m.blog.uliejh.cn/snews/637439.htm
- http://m.blog.uliejh.cn/snews/0820783.htm
- http://m.blog.uliejh.cn/snews/0546646.htm
- http://m.blog.uliejh.cn/snews/6504.htm
- http://m.blog.uliejh.cn/snews/780392.htm
- http://m.blog.uliejh.cn/snews/7635676.htm
- http://m.blog.uliejh.cn/snews/58778.htm
- http://m.blog.uliejh.cn/snews/4115.htm
- http://m.blog.uliejh.cn/snews/2954384.htm
- http://m.blog.uliejh.cn/snews/6844590.htm
- http://m.blog.uliejh.cn/snews/9336312.htm
- http://m.blog.uliejh.cn/snews/72968.htm
- http://m.blog.uliejh.cn/snews/3967888.htm
- http://m.blog.uliejh.cn/snews/35373.htm
- http://m.blog.uliejh.cn/snews/8224.htm
- http://m.blog.uliejh.cn/snews/398502.htm
- http://m.blog.uliejh.cn/snews/2679.htm
- http://m.blog.uliejh.cn/snews/0385.htm
- http://m.blog.uliejh.cn/snews/324246.htm
- http://m.blog.uliejh.cn/snews/6044.htm
- http://m.blog.uliejh.cn/snews/4337116.htm
- http://m.blog.uliejh.cn/snews/55344.htm
- http://m.blog.uliejh.cn/snews/817637.htm
- http://m.blog.uliejh.cn/snews/3827114.htm
- http://m.blog.uliejh.cn/snews/18638.htm
- http://m.blog.uliejh.cn/snews/9197.htm
- http://m.blog.uliejh.cn/snews/05860.htm
- http://m.blog.uliejh.cn/snews/922793.htm
- http://m.blog.uliejh.cn/snews/0166.htm
- http://m.blog.uliejh.cn/snews/4585560.htm
- http://m.blog.uliejh.cn/snews/5874.htm
- http://m.blog.uliejh.cn/snews/15807.htm
- http://m.blog.uliejh.cn/snews/17219.htm
- http://m.blog.uliejh.cn/snews/2722.htm
- http://m.blog.uliejh.cn/snews/544776.htm
- http://m.blog.uliejh.cn/snews/4322738.htm
- http://m.blog.uliejh.cn/snews/75134.htm
- http://m.blog.uliejh.cn/snews/541163.htm
- http://m.blog.uliejh.cn/snews/34194.htm
- http://m.blog.uliejh.cn/snews/91976.htm
- http://m.blog.uliejh.cn/snews/0358773.htm
- http://m.blog.uliejh.cn/snews/5257.htm
- http://m.blog.uliejh.cn/snews/4396.htm
- http://m.blog.uliejh.cn/snews/0698879.htm
- http://m.blog.uliejh.cn/snews/42391.htm
- http://m.blog.uliejh.cn/snews/3783817.htm
- http://m.blog.uliejh.cn/snews/4616.htm
- http://m.blog.uliejh.cn/snews/4407.htm
- http://m.blog.uliejh.cn/snews/8028.htm
- http://m.blog.uliejh.cn/snews/2746.htm
- http://m.blog.uliejh.cn/snews/70029.htm
- http://m.blog.uliejh.cn/snews/9608716.htm
- http://m.blog.uliejh.cn/snews/4492.htm
- http://m.blog.uliejh.cn/snews/883450.htm
- http://m.blog.uliejh.cn/snews/59247.htm
- http://m.blog.uliejh.cn/snews/2378456.htm
- http://m.blog.uliejh.cn/snews/1408396.htm
- http://m.blog.uliejh.cn/snews/743070.htm
- http://m.blog.uliejh.cn/snews/51725.htm
- http://m.blog.uliejh.cn/snews/4842.htm
- http://m.blog.uliejh.cn/snews/39346.htm
- http://m.blog.uliejh.cn/snews/998248.htm
- http://m.blog.uliejh.cn/snews/343950.htm
- http://m.blog.uliejh.cn/snews/2486.htm
- http://m.blog.uliejh.cn/snews/829192.htm
- http://m.blog.uliejh.cn/snews/860221.htm
- http://m.blog.uliejh.cn/snews/14339.htm
- http://m.blog.uliejh.cn/snews/8124.htm
- http://m.blog.uliejh.cn/snews/10926.htm
- http://m.blog.uliejh.cn/snews/828406.htm
- http://m.blog.uliejh.cn/snews/1859.htm
- http://m.blog.uliejh.cn/snews/398054.htm
- http://m.blog.uliejh.cn/snews/70138.htm
- http://m.blog.uliejh.cn/snews/2851438.htm
- http://m.blog.uliejh.cn/snews/81808.htm
- http://m.blog.uliejh.cn/snews/825853.htm
- http://m.blog.uliejh.cn/snews/7207.htm
- http://m.blog.uliejh.cn/snews/676433.htm
- http://m.blog.uliejh.cn/snews/9480.htm
- http://m.blog.uliejh.cn/snews/47568.htm
- http://m.blog.uliejh.cn/snews/2461.htm
- http://m.blog.uliejh.cn/snews/635943.htm
- http://m.blog.uliejh.cn/snews/9320647.htm
- http://m.blog.uliejh.cn/snews/292504.htm
- http://m.blog.uliejh.cn/snews/8259.htm
- http://m.blog.uliejh.cn/snews/05979.htm
- http://m.blog.uliejh.cn/snews/9182.htm
- http://m.blog.uliejh.cn/snews/9670.htm
- http://m.blog.uliejh.cn/snews/966475.htm
- http://m.blog.uliejh.cn/snews/922059.htm
- http://m.blog.uliejh.cn/snews/86914.htm
- http://m.blog.uliejh.cn/snews/383618.htm
- http://m.blog.uliejh.cn/snews/0402.htm
- http://m.blog.uliejh.cn/snews/45023.htm
- http://m.blog.uliejh.cn/snews/5349.htm
- http://m.blog.uliejh.cn/snews/1098.htm
- http://m.blog.uliejh.cn/snews/654839.htm
- http://m.blog.uliejh.cn/snews/800923.htm
- http://m.blog.uliejh.cn/snews/1652.htm
- http://m.blog.uliejh.cn/snews/046375.htm
- http://m.blog.uliejh.cn/snews/1626379.htm
- http://m.blog.uliejh.cn/snews/411344.htm
- http://m.blog.uliejh.cn/snews/9821588.htm
- http://m.blog.uliejh.cn/snews/81432.htm
- http://m.blog.uliejh.cn/snews/58532.htm
- http://m.blog.uliejh.cn/snews/9449.htm
- http://m.blog.uliejh.cn/snews/91507.htm
- http://m.blog.uliejh.cn/snews/2474.htm
- http://m.blog.uliejh.cn/snews/7913338.htm
- http://m.blog.uliejh.cn/snews/42681.htm
- http://m.blog.uliejh.cn/snews/055046.htm
- http://m.blog.uliejh.cn/snews/45485.htm
- http://m.blog.uliejh.cn/snews/0824626.htm
- http://m.blog.uliejh.cn/snews/800445.htm
- http://m.blog.uliejh.cn/snews/4826.htm
- http://m.blog.uliejh.cn/snews/0784.htm
- http://m.blog.uliejh.cn/snews/630943.htm
- http://m.blog.uliejh.cn/snews/3819156.htm
- http://m.blog.uliejh.cn/snews/8106952.htm
- http://m.blog.uliejh.cn/snews/9105.htm
- http://m.blog.uliejh.cn/snews/94218.htm
- http://m.blog.uliejh.cn/snews/9248.htm
- http://m.blog.uliejh.cn/snews/8356183.htm
- http://m.blog.uliejh.cn/snews/8379311.htm
- http://m.blog.uliejh.cn/snews/2423.htm
- http://m.blog.uliejh.cn/snews/8808.htm
- http://m.blog.uliejh.cn/snews/238429.htm
- http://m.blog.uliejh.cn/snews/896912.htm
- http://m.blog.uliejh.cn/snews/5491076.htm
- http://m.blog.uliejh.cn/snews/536677.htm
- http://m.blog.uliejh.cn/snews/1014934.htm
- http://m.blog.uliejh.cn/snews/148046.htm
- http://m.blog.uliejh.cn/snews/155037.htm
- http://m.blog.uliejh.cn/snews/640868.htm
- http://m.blog.uliejh.cn/snews/265331.htm
- http://m.blog.uliejh.cn/snews/112387.htm
- http://m.blog.uliejh.cn/snews/54392.htm
- http://m.blog.uliejh.cn/snews/1156649.htm
- http://m.blog.uliejh.cn/snews/7892051.htm
- http://m.blog.uliejh.cn/snews/192330.htm
- http://m.blog.uliejh.cn/snews/244373.htm
- http://m.blog.uliejh.cn/snews/4189257.htm
- http://m.blog.uliejh.cn/snews/000154.htm
- http://m.blog.uliejh.cn/snews/524949.htm
- http://m.blog.uliejh.cn/snews/10919.htm
- http://m.blog.uliejh.cn/snews/6975835.htm
- http://m.blog.uliejh.cn/snews/58448.htm
- http://m.blog.uliejh.cn/snews/2985717.htm
- http://m.blog.uliejh.cn/snews/5469967.htm
- http://m.blog.uliejh.cn/snews/259560.htm
- http://m.blog.uliejh.cn/snews/0053.htm
- http://m.blog.uliejh.cn/snews/8931571.htm
- http://m.blog.uliejh.cn/snews/27775.htm
- http://m.blog.uliejh.cn/snews/243336.htm
- http://m.blog.uliejh.cn/snews/65806.htm
- http://m.blog.uliejh.cn/snews/3044124.htm
- http://m.blog.uliejh.cn/snews/0099656.htm
- http://m.blog.uliejh.cn/snews/8138342.htm
- http://m.blog.uliejh.cn/snews/1485168.htm
- http://m.blog.uliejh.cn/snews/508686.htm
- http://m.blog.uliejh.cn/snews/999344.htm
- http://m.blog.uliejh.cn/snews/710595.htm
- http://m.blog.uliejh.cn/snews/86777.htm
- http://m.blog.uliejh.cn/snews/36043.htm
- http://m.blog.uliejh.cn/snews/53839.htm
- http://m.blog.uliejh.cn/snews/2261881.htm
- http://m.blog.uliejh.cn/snews/0933117.htm
- http://m.blog.uliejh.cn/snews/1918.htm
- http://m.blog.uliejh.cn/snews/6927.htm
- http://m.blog.uliejh.cn/snews/34358.htm
- http://m.blog.uliejh.cn/snews/8066.htm
- http://m.blog.uliejh.cn/snews/8816.htm
- http://m.blog.uliejh.cn/snews/15069.htm
- http://m.blog.uliejh.cn/snews/5392957.htm
- http://m.blog.uliejh.cn/snews/07889.htm
- http://m.blog.uliejh.cn/snews/6959213.htm
- http://m.blog.uliejh.cn/snews/04871.htm
- http://m.blog.uliejh.cn/snews/0261.htm
- http://m.blog.uliejh.cn/snews/22680.htm
- http://m.blog.uliejh.cn/snews/81239.htm
- http://m.blog.uliejh.cn/snews/918430.htm
- http://m.blog.uliejh.cn/snews/5649388.htm
- http://m.blog.uliejh.cn/snews/53579.htm
- http://m.blog.uliejh.cn/snews/795166.htm
- http://m.blog.uliejh.cn/snews/3535474.htm
- http://m.blog.uliejh.cn/snews/050746.htm
- http://m.blog.uliejh.cn/snews/9695531.htm
- http://m.blog.uliejh.cn/snews/34006.htm
- http://m.blog.uliejh.cn/snews/5343.htm
- http://m.blog.uliejh.cn/snews/25036.htm
- http://m.blog.uliejh.cn/snews/15113.htm
- http://m.blog.uliejh.cn/snews/06826.htm
- http://m.blog.uliejh.cn/snews/709456.htm
- http://m.blog.uliejh.cn/snews/8538.htm
- http://m.blog.uliejh.cn/snews/348969.htm
- http://m.blog.uliejh.cn/snews/7527.htm
- http://m.blog.uliejh.cn/snews/703605.htm
- http://m.blog.uliejh.cn/snews/9173.htm
- http://m.blog.uliejh.cn/snews/57432.htm
- http://m.blog.uliejh.cn/snews/8658261.htm
- http://m.blog.uliejh.cn/snews/1644448.htm
- http://m.blog.uliejh.cn/snews/2013.htm
- http://m.blog.uliejh.cn/snews/0331.htm
- http://m.blog.uliejh.cn/snews/24415.htm
- http://m.blog.uliejh.cn/snews/44998.htm
- http://m.blog.uliejh.cn/snews/55873.htm
- http://m.blog.uliejh.cn/snews/76122.htm

## 项目结构

```
linkvault-core/
├── Cargo.toml                    # Rust 项目清单，定义依赖与工作空间
├── Makefile                      # 构建入口，包含 build、test、clean 等目标
├── README.md                     # 项目主文档
├── LICENSE                       # MIT 许可证全文
├── .env.example                  # 环境变量配置模板
├── .gitignore                    # 版本控制忽略文件列表
├── src/                          # 核心源代码目录
│   ├── main.rs                   # CLI 入口，解析子命令与参数
│   ├── lib.rs                    # 库模块导出，定义公共接口
│   ├── importer/                 # 导入子模块：解析不同输入格式
│   │   ├── mod.rs                # 导入器工厂与调度
│   │   ├── text_parser.rs        # 纯文本与 CSV 行解析器
│   │   └── url_normalizer.rs     # URL 规范化与去重逻辑
│   ├── checker/                  # 状态检查子模块：异步 HTTP 探测
│   │   ├── mod.rs                # 检查器主循环与并发控制
│   │   ├── client.rs             # 自定义 HTTP 客户端封装
│   │   └── metrics.rs            # 检查结果统计与汇总
│   ├── storage/                  # 存储子模块：LMDB 键值封装
│   │   ├── mod.rs                # 存储引擎 trait 定义
│   │   ├── lmdb_adapter.rs       # LMDB 具体实现
│   │   └── schema.rs             # 数据序列化与反序列化
│   ├── tagger/                   # 标签子模块：层级标签管理
│   │   ├── mod.rs                # 标签树与匹配逻辑
│   │   └── matcher.rs            # 通配符与前缀匹配规则
│   └── export/                   # 导出子模块：多格式输出
│       ├── mod.rs                # 导出格式路由
│       ├── json_formatter.rs     # JSON 阵列输出
│       └── markdown_formatter.rs # Markdown 表格与列表生成
├── tests/                        # 集成测试目录
│   ├── import_tests.rs           # 导入流程端到端测试
│   └── checker_tests.rs          # 状态检查模拟测试
├── benches/                      # 性能基准测试
│   └── storage_bench.rs          # 存储读写吞吐压测
├── docs/                         # 详细文档目录
│   ├── user-guide/               # 用户手册分章节
│   ├── reference/                # 配置与 API 参考
│   └── development/              # 设计决策与贡献者指南
├── samples/                      # 示例数据文件
│   ├── urls.txt                  # 普通 URL 列表示例
│   └── urls_with_tags.csv        # 含标签列的 CSV 示例
├── scripts/                      # 运维辅助脚本
│   ├── batch_import.sh           # 批量导入封装脚本
│   └── health_check.sh           # 系统依赖检查脚本
└── target/                       # 编译输出目录（git 忽略）
    ├── debug/                    # 调试构建产物
    └── release/                  # 发布构建产物
```

## 贡献指南

贡献者需遵循以下流程以确保代码质量和项目一致性。

第一步：查阅 issue 列表与项目看板，确认当前待处理的特性或缺陷，避免重复工作。对于新特性提议，应先创建讨论 issue 并等待维护者反馈。

第二步：派生项目仓库至个人账号，在本地新建特性分支（命名格式为 feature/描述或 fix/描述），确保分支名称简洁且反映变更内容。

第三步：编写或修改代码时，须遵守项目根目录下的 rustfmt.toml 与 clippy.toml 配置，所有公共接口需附有文档注释，且必须通过现有的单元测试与集成测试。

第四步：提交代码前执行 make precommit，该命令会自动运行格式化、静态检查、测试套件以及覆盖率报告，确保无回归问题。

第五步：发起合并请求至主仓库的 develop 分支，在请求描述中清晰列出变更点、测试结果以及影响范围，维护者将在两个工作日内进行审查。

## 常见问题

问：LinkVault Core 是否支持导入 HTTPS 与 HTTP 混合列表？对非标准端口如何处理？

答：支持混合协议导入。URL 规范化模块会自动保留协议头与端口号，状态检查器会根据协议选择相应 TLS 配置。对于非标准端口（如 :8080），检查器会正确构造请求目标，无需特殊配置。

问：批量检查过程中出现大量超时或连接拒绝，如何调整参数？

答：可通过命令行参数 --timeout 设置单次请求超时（默认 30 秒），--concurrency 控制并发连接数（默认 20）。若目标服务器存在频率限制，建议降低并发数并增加 --retry 重试次数（默认 3 次）。也可在环境变量中设置 HTTP_PROXY 以通过代理服务器路由流量。

问：数据存储目录是否可以迁移或备份？如何导出全部数据？

答：存储目录默认为 ./data，可通过 --storage-path 指定其他位置。迁移时只需整体复制该目录至新机器相同路径，或通过 --storage-path 指向新位置。导出全部数据可使用 export --batch all --format json，输出文件为全量 JSON 格式，包含每条链接的原始 URL、状态、标签及时间戳。

## 许可证

MIT

> 外链数量: 250 | 生成时间: 2026-08-24 23:41:17
