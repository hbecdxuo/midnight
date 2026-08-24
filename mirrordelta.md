# WebLink Navigator

WebLink Navigator 是一个面向技术研究、内容聚合与信息审计场景的开源外链管理工具集。该项目定位于帮助开发者、运维人员与内容策展人高效地收集、验证、分类和监控大量分散的 URL 资源，尤其适用于处理批次量大、来源结构相似的半结构化外链数据。本仓库不提供爬虫或自动化采集功能，而是围绕链接的规范性检查、可用性探测、元数据提取与批量导出等环节提供一系列可组合的 Shell 脚本与配置模板，便于用户快速搭建属于自己的外链健康度监察体系。

## 功能概览

- 批量链接可达性探测：基于 curl 与超时控制，对大批量 URL 执行快速 HEAD 请求，识别死链与重定向链。

- 响应状态码分布统计：自动汇总 2xx、3xx、4xx、5xx 状态码数量，生成简明的终端报表。

- 内容类型与大小抽样：对可访问链接随机抽取样本，记录 Content-Type 与 Content-Length，辅助判断资源类型。

- 域名与路径结构解析：从 URL 中提取域名、路径层级、文件扩展名，支持按来源域名或路径深度分组统计。

- 批次对比与增量检测：支持导入历史快照文件，对比两批链接的状态变化，标记新增失效或恢复的链接。

- 原始数据导出与归档：将处理后的链接状态、状态码、响应时间等字段输出为 TSV 或 CSV 格式，便于导入电子表格或数据库。

- 轻量级配置与日志：所有运行参数通过单个 config.env 文件控制，每次执行自动生成时间戳日志，便于回溯。

## 应用场景

- 网站迁移后的外链审计：当站点域名或路径结构发生变更时，运维人员可利用 WebLink Navigator 批量检测旧链接是否仍能正确重定向至新地址，或返回 404 状态码，从而评估迁移完整性。

- 内容聚合平台的数据源巡检：内容团队定期维护大量外部引用链接（如参考文献、新闻来源、合作伙伴入口），通过本工具每日或每周执行一次可用性扫描，及时发现被删除或封锁的页面，降低用户跳出率。

- 开源项目文档链维护：大型开源项目的 README 或 Wiki 中常包含数十乃至上百个外部参考链接，维护者可在发版前运行检测，避免文档中出现失效的示例站或 API 文档地址，提升文档专业度。

- 安全研究中的批量 IOC 验证：安全分析师收集大量可疑域名或 URL 后，利用本工具快速判断这些资源当前是否仍处于活跃状态，并记录响应头部信息，为后续威胁研判提供基础数据。

## 快速开始

以下命令默认在 Linux 或 macOS 终端环境中执行，需提前安装 git、bash 和 curl。

```bash
# 克隆仓库到本地
git clone https://github.com/weblink-navigator/weblink-navigator.git
cd weblink-navigator

# 安装核心依赖（以 Debian/Ubuntu 为例）
sudo apt-get update
sudo apt-get install -y curl jq moreutils

# 复制示例配置文件并修改
cp config.env.example config.env

# 将待检测的 URL 列表放入 input/urls.txt，每行一个 URL
# 然后执行主检测脚本
./bin/check_links.sh --input input/urls.txt --output reports/result_$(date +%Y%m%d).tsv
```

## 安装要求

| 依赖项 | 必需版本 | 说明 |
|--------|----------|------|
| Bash | 4.0 或更高 | 所有主控脚本均使用 Bash 编写，依赖数组和关联数组特性 |
| curl | 7.68.0 或更高 | 用于执行 HTTP 请求，支持 --max-time、--write-out 等输出控制参数 |
| jq | 1.6 或更高 | 用于解析配置文件中的 JSON 字段，非必需但强烈建议安装以启用高级过滤 |
| moreutils | 0.60 或更高 | 提供 chronic、sponge 等工具，辅助日志和文件写入，提升脚本稳健性 |
| grep | 3.4 或更高 | 用于正则提取 URL 中的域名、路径和查询参数，需支持 -P 或 -E 扩展模式 |
| awk | 5.0.0 或更高 | 用于统计报表生成和字段重排，推荐 GNU awk 以支持数组排序函数 |
| sed | 4.7 或更高 | 用于对 URL 进行字符串替换和清洗，处理换行符和特殊字符转义 |
| coreutils | 8.30 或更高 | 提供 date、sort、uniq、comm 等基础文件处理命令，用于快照对比 |
| git | 2.25.0 或更高 | 仅开发或自定义扩展时需要，用于克隆仓库和版本管理，生产环境可不安装 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|------|------|------------|
| 用户手册 | docs/user-guide.md | 如何安装、配置、运行批量检测？有哪些命令行参数？输出文件如何解读？ |
| 配置参考 | docs/config-reference.md | config.env 中每个变量的含义是什么？如何调整超时、并发数和重试策略？ |
| 输出格式 | docs/output-format.md | 生成的 TSV/CSV 包含哪些字段？状态码映射关系如何定义？如何自定义输出列？ |
| 脚本开发 | docs/developer-guide.md | 脚本的模块划分是怎样的？如何新增一个自定义探测步骤？如何编写单元测试？ |
| 故障排除 | docs/troubleshooting.md | 常见报错信息（如 curl: (28) 超时、jq: parse error）的解决办法有哪些？ |
| 变更日志 | CHANGELOG.md | 每个版本的新增功能、性能改进和修复了哪些缺陷？升级时需要注意哪些破坏性变更？ |

## 资源列表

- http://m.wap.uliejh.cn/bnews/631464.htm
- http://m.wap.uliejh.cn/bnews/9123482.htm
- http://m.wap.uliejh.cn/bnews/2876884.htm
- http://m.wap.uliejh.cn/bnews/06149.htm
- http://m.wap.uliejh.cn/bnews/3406448.htm
- http://m.wap.uliejh.cn/bnews/51205.htm
- http://m.wap.uliejh.cn/bnews/5511733.htm
- http://m.wap.uliejh.cn/bnews/150800.htm
- http://m.wap.uliejh.cn/bnews/23676.htm
- http://m.wap.uliejh.cn/bnews/0987.htm
- http://m.wap.uliejh.cn/bnews/421436.htm
- http://m.wap.uliejh.cn/bnews/8176441.htm
- http://m.wap.uliejh.cn/bnews/156006.htm
- http://m.wap.uliejh.cn/bnews/4738.htm
- http://m.wap.uliejh.cn/bnews/3650.htm
- http://m.wap.uliejh.cn/bnews/431248.htm
- http://m.wap.uliejh.cn/bnews/2436.htm
- http://m.wap.uliejh.cn/bnews/4736248.htm
- http://m.wap.uliejh.cn/bnews/603516.htm
- http://m.wap.uliejh.cn/bnews/7240004.htm
- http://m.wap.uliejh.cn/bnews/2337.htm
- http://m.wap.uliejh.cn/bnews/95087.htm
- http://m.wap.uliejh.cn/bnews/7860.htm
- http://m.wap.uliejh.cn/bnews/7086.htm
- http://m.wap.uliejh.cn/bnews/9239246.htm
- http://m.wap.uliejh.cn/bnews/3461187.htm
- http://m.wap.uliejh.cn/bnews/7952305.htm
- http://m.wap.uliejh.cn/bnews/3741722.htm
- http://m.wap.uliejh.cn/bnews/460874.htm
- http://m.wap.uliejh.cn/bnews/4806169.htm
- http://m.wap.uliejh.cn/bnews/3922.htm
- http://m.wap.uliejh.cn/bnews/27040.htm
- http://m.wap.uliejh.cn/bnews/46388.htm
- http://m.wap.uliejh.cn/bnews/02120.htm
- http://m.wap.uliejh.cn/bnews/980000.htm
- http://m.wap.uliejh.cn/bnews/28477.htm
- http://m.wap.uliejh.cn/bnews/4160.htm
- http://m.wap.uliejh.cn/bnews/360364.htm
- http://m.wap.uliejh.cn/bnews/51766.htm
- http://m.wap.uliejh.cn/bnews/513099.htm
- http://m.wap.uliejh.cn/bnews/297870.htm
- http://m.wap.uliejh.cn/bnews/499988.htm
- http://m.wap.uliejh.cn/bnews/7105.htm
- http://m.wap.uliejh.cn/bnews/8292.htm
- http://m.wap.uliejh.cn/bnews/990432.htm
- http://m.wap.uliejh.cn/bnews/2822.htm
- http://m.wap.uliejh.cn/bnews/3167206.htm
- http://m.wap.uliejh.cn/bnews/2925.htm
- http://m.wap.uliejh.cn/bnews/6177.htm
- http://m.wap.uliejh.cn/bnews/7665645.htm
- http://m.wap.uliejh.cn/bnews/3615910.htm
- http://m.wap.uliejh.cn/bnews/4202.htm
- http://m.wap.uliejh.cn/bnews/1256.htm
- http://m.wap.uliejh.cn/bnews/3292496.htm
- http://m.wap.uliejh.cn/bnews/08273.htm
- http://m.wap.uliejh.cn/bnews/4964998.htm
- http://m.wap.uliejh.cn/bnews/4627.htm
- http://m.wap.uliejh.cn/bnews/07529.htm
- http://m.wap.uliejh.cn/bnews/8434.htm
- http://m.wap.uliejh.cn/bnews/517516.htm
- http://m.wap.uliejh.cn/bnews/5740790.htm
- http://m.wap.uliejh.cn/bnews/939936.htm
- http://m.wap.uliejh.cn/bnews/3772238.htm
- http://m.wap.uliejh.cn/bnews/8993378.htm
- http://m.wap.uliejh.cn/bnews/50688.htm
- http://m.wap.uliejh.cn/bnews/94593.htm
- http://m.wap.uliejh.cn/bnews/9544.htm
- http://m.wap.uliejh.cn/bnews/396165.htm
- http://m.wap.uliejh.cn/bnews/1997.htm
- http://m.wap.uliejh.cn/bnews/51750.htm
- http://m.wap.uliejh.cn/bnews/32975.htm
- http://m.wap.uliejh.cn/bnews/2452.htm
- http://m.wap.uliejh.cn/bnews/747834.htm
- http://m.wap.uliejh.cn/bnews/7804737.htm
- http://m.wap.uliejh.cn/bnews/1496870.htm
- http://m.wap.uliejh.cn/bnews/52367.htm
- http://m.wap.uliejh.cn/bnews/28195.htm
- http://m.wap.uliejh.cn/bnews/9786549.htm
- http://m.wap.uliejh.cn/bnews/0854987.htm
- http://m.wap.uliejh.cn/bnews/163185.htm
- http://m.wap.uliejh.cn/bnews/67594.htm
- http://m.wap.uliejh.cn/bnews/41762.htm
- http://m.wap.uliejh.cn/bnews/015774.htm
- http://m.wap.uliejh.cn/bnews/37480.htm
- http://m.wap.uliejh.cn/bnews/035450.htm
- http://m.wap.uliejh.cn/bnews/745421.htm
- http://m.wap.uliejh.cn/bnews/5642361.htm
- http://m.wap.uliejh.cn/bnews/032105.htm
- http://m.wap.uliejh.cn/bnews/7683903.htm
- http://m.wap.uliejh.cn/bnews/2945.htm
- http://m.wap.uliejh.cn/bnews/01252.htm
- http://m.wap.uliejh.cn/bnews/461730.htm
- http://m.wap.uliejh.cn/bnews/294614.htm
- http://m.wap.uliejh.cn/bnews/63351.htm
- http://m.wap.uliejh.cn/bnews/7590831.htm
- http://m.wap.uliejh.cn/bnews/38698.htm
- http://m.wap.uliejh.cn/bnews/793661.htm
- http://m.wap.uliejh.cn/bnews/996498.htm
- http://m.wap.uliejh.cn/bnews/924342.htm
- http://m.wap.uliejh.cn/bnews/0797.htm
- http://m.wap.uliejh.cn/bnews/0322.htm
- http://m.wap.uliejh.cn/bnews/8004176.htm
- http://m.wap.uliejh.cn/bnews/2030.htm
- http://m.wap.uliejh.cn/bnews/852349.htm
- http://m.wap.uliejh.cn/bnews/197910.htm
- http://m.wap.uliejh.cn/bnews/7370564.htm
- http://m.wap.uliejh.cn/bnews/0766908.htm
- http://m.wap.uliejh.cn/bnews/69339.htm
- http://m.wap.uliejh.cn/bnews/47440.htm
- http://m.wap.uliejh.cn/bnews/98002.htm
- http://m.wap.uliejh.cn/bnews/211793.htm
- http://m.wap.uliejh.cn/bnews/484556.htm
- http://m.wap.uliejh.cn/bnews/26609.htm
- http://m.wap.uliejh.cn/bnews/052456.htm
- http://m.wap.uliejh.cn/bnews/68456.htm
- http://m.wap.uliejh.cn/bnews/9974.htm
- http://m.wap.uliejh.cn/bnews/901438.htm
- http://m.wap.uliejh.cn/bnews/2343.htm
- http://m.wap.uliejh.cn/bnews/1860659.htm
- http://m.wap.uliejh.cn/bnews/13411.htm
- http://m.wap.uliejh.cn/bnews/7268.htm
- http://m.wap.uliejh.cn/bnews/4496.htm
- http://m.wap.uliejh.cn/bnews/541115.htm
- http://m.wap.uliejh.cn/bnews/449307.htm
- http://m.wap.uliejh.cn/bnews/813860.htm
- http://m.wap.uliejh.cn/bnews/26076.htm
- http://m.wap.uliejh.cn/bnews/83397.htm
- http://m.wap.uliejh.cn/bnews/6258370.htm
- http://m.wap.uliejh.cn/bnews/6467.htm
- http://m.wap.uliejh.cn/bnews/427819.htm
- http://m.wap.uliejh.cn/bnews/31410.htm
- http://m.wap.uliejh.cn/bnews/095599.htm
- http://m.wap.uliejh.cn/bnews/4197.htm
- http://m.wap.uliejh.cn/bnews/645309.htm
- http://m.wap.uliejh.cn/bnews/262121.htm
- http://m.wap.uliejh.cn/bnews/93202.htm
- http://m.wap.uliejh.cn/bnews/858778.htm
- http://m.wap.uliejh.cn/bnews/3687.htm
- http://m.wap.uliejh.cn/bnews/797351.htm
- http://m.wap.uliejh.cn/bnews/7068.htm
- http://m.wap.uliejh.cn/bnews/94711.htm
- http://m.wap.uliejh.cn/bnews/7035826.htm
- http://m.wap.uliejh.cn/bnews/638043.htm
- http://m.wap.uliejh.cn/bnews/0834054.htm
- http://m.wap.uliejh.cn/bnews/5829314.htm
- http://m.wap.uliejh.cn/bnews/6835.htm
- http://m.wap.uliejh.cn/bnews/80608.htm
- http://m.wap.uliejh.cn/bnews/2446274.htm
- http://m.wap.uliejh.cn/bnews/8045055.htm
- http://m.wap.uliejh.cn/bnews/0000193.htm
- http://m.wap.uliejh.cn/bnews/0855750.htm
- http://m.wap.uliejh.cn/bnews/2036623.htm
- http://m.wap.uliejh.cn/bnews/71913.htm
- http://m.wap.uliejh.cn/bnews/886518.htm
- http://m.wap.uliejh.cn/bnews/17819.htm
- http://m.wap.uliejh.cn/bnews/9696615.htm
- http://m.wap.uliejh.cn/bnews/705903.htm
- http://m.wap.uliejh.cn/bnews/7996452.htm
- http://m.wap.uliejh.cn/bnews/3960.htm
- http://m.wap.uliejh.cn/bnews/7087.htm
- http://m.wap.uliejh.cn/bnews/2857.htm
- http://m.wap.uliejh.cn/bnews/0801.htm
- http://m.wap.uliejh.cn/bnews/1393805.htm
- http://m.wap.uliejh.cn/bnews/0442.htm
- http://m.wap.uliejh.cn/bnews/4314052.htm
- http://m.wap.uliejh.cn/bnews/0031.htm
- http://m.wap.uliejh.cn/bnews/07165.htm
- http://m.wap.uliejh.cn/bnews/3989319.htm
- http://m.wap.uliejh.cn/bnews/08141.htm
- http://m.wap.uliejh.cn/bnews/207038.htm
- http://m.wap.uliejh.cn/bnews/559733.htm
- http://m.wap.uliejh.cn/bnews/2186.htm
- http://m.wap.uliejh.cn/bnews/43966.htm
- http://m.wap.uliejh.cn/bnews/4898149.htm
- http://m.wap.uliejh.cn/bnews/630800.htm
- http://m.wap.uliejh.cn/bnews/60617.htm
- http://m.wap.uliejh.cn/bnews/9368334.htm
- http://m.wap.uliejh.cn/bnews/72738.htm
- http://m.wap.uliejh.cn/bnews/11998.htm
- http://m.wap.uliejh.cn/bnews/53087.htm
- http://m.wap.uliejh.cn/bnews/92018.htm
- http://m.wap.uliejh.cn/bnews/0123616.htm
- http://m.wap.uliejh.cn/bnews/95045.htm
- http://m.wap.uliejh.cn/bnews/5505572.htm
- http://m.wap.uliejh.cn/bnews/1410949.htm
- http://m.wap.uliejh.cn/bnews/9697724.htm
- http://m.wap.uliejh.cn/bnews/2949.htm
- http://m.wap.uliejh.cn/bnews/7726527.htm
- http://m.wap.uliejh.cn/bnews/5939.htm
- http://m.wap.uliejh.cn/bnews/830068.htm
- http://m.wap.uliejh.cn/bnews/55951.htm
- http://m.wap.uliejh.cn/bnews/7134.htm
- http://m.wap.uliejh.cn/bnews/8004537.htm
- http://m.wap.uliejh.cn/bnews/5275.htm
- http://m.wap.uliejh.cn/bnews/3617.htm
- http://m.wap.uliejh.cn/bnews/24699.htm
- http://m.wap.uliejh.cn/bnews/476503.htm
- http://m.wap.uliejh.cn/bnews/351830.htm
- http://m.wap.uliejh.cn/bnews/00141.htm
- http://m.wap.uliejh.cn/bnews/91493.htm
- http://m.wap.uliejh.cn/bnews/5323.htm
- http://m.wap.uliejh.cn/bnews/0995.htm
- http://m.wap.uliejh.cn/bnews/4906.htm
- http://m.wap.uliejh.cn/bnews/8093062.htm
- http://m.wap.uliejh.cn/bnews/627193.htm
- http://m.wap.uliejh.cn/bnews/0823.htm
- http://m.wap.uliejh.cn/bnews/01197.htm
- http://m.wap.uliejh.cn/bnews/8471.htm
- http://m.wap.uliejh.cn/bnews/3532478.htm
- http://m.wap.uliejh.cn/bnews/3444296.htm
- http://m.wap.uliejh.cn/bnews/4596608.htm
- http://m.wap.uliejh.cn/bnews/264600.htm
- http://m.wap.uliejh.cn/bnews/8423.htm
- http://m.wap.uliejh.cn/bnews/6946.htm
- http://m.wap.uliejh.cn/bnews/237641.htm
- http://m.wap.uliejh.cn/bnews/92043.htm
- http://m.wap.uliejh.cn/bnews/1255230.htm
- http://m.wap.uliejh.cn/bnews/3825024.htm
- http://m.wap.uliejh.cn/bnews/3448623.htm
- http://m.wap.uliejh.cn/bnews/037874.htm
- http://m.wap.uliejh.cn/bnews/4458.htm
- http://m.wap.uliejh.cn/bnews/0717.htm
- http://m.wap.uliejh.cn/bnews/192055.htm
- http://m.wap.uliejh.cn/bnews/46536.htm
- http://m.wap.uliejh.cn/bnews/9061.htm
- http://m.wap.uliejh.cn/bnews/99864.htm
- http://m.wap.uliejh.cn/bnews/453003.htm
- http://m.wap.uliejh.cn/bnews/71636.htm
- http://m.wap.uliejh.cn/bnews/8599978.htm
- http://m.wap.uliejh.cn/bnews/42390.htm
- http://m.wap.uliejh.cn/bnews/55578.htm
- http://m.wap.uliejh.cn/bnews/1182.htm
- http://m.wap.uliejh.cn/bnews/0678.htm
- http://m.wap.uliejh.cn/bnews/47483.htm
- http://m.wap.uliejh.cn/bnews/191607.htm
- http://m.wap.uliejh.cn/bnews/8861869.htm
- http://m.wap.uliejh.cn/bnews/21581.htm
- http://m.wap.uliejh.cn/bnews/2089.htm
- http://m.wap.uliejh.cn/bnews/243333.htm
- http://m.wap.uliejh.cn/bnews/0679376.htm
- http://m.wap.uliejh.cn/bnews/547557.htm
- http://m.wap.uliejh.cn/bnews/4016837.htm
- http://m.wap.uliejh.cn/bnews/0111933.htm
- http://m.wap.uliejh.cn/bnews/7935.htm
- http://m.wap.uliejh.cn/bnews/736215.htm
- http://m.wap.uliejh.cn/bnews/01887.htm
- http://m.wap.uliejh.cn/bnews/09447.htm
- http://m.wap.uliejh.cn/bnews/3600876.htm
- http://m.wap.uliejh.cn/bnews/796567.htm
- http://m.wap.uliejh.cn/bnews/0278860.htm

## 项目结构

```
weblink-navigator/
├── bin/                                 # 可执行脚本主目录
│   ├── check_links.sh                   # 主入口脚本，解析参数并调度各个检测阶段
│   ├── probe.sh                         # 单链接探测函数库，封装 curl 调用与超时重试逻辑
│   ├── stats.sh                         # 统计汇总脚本，生成状态码分布和响应时间分位数
│   └── compare.sh                       # 快照对比脚本，基于 comm 实现两批链接状态差异分析
├── conf/                                # 配置目录
│   ├── config.env.example               # 示例环境变量配置文件，包含所有可调参数及注释
│   └── user_agents.list                 # 自定义 User-Agent 列表，用于轮换请求头
├── input/                               # 用户输入目录
│   └── urls.txt                         # 默认待检测 URL 列表文件，每行一个 URL，支持空行和注释（#开头）
├── output/                              # 默认输出根目录
│   ├── reports/                         # 检测报告存放位置，按日期或批次生成子目录
│   │   └── 2026-08-24/                  # 示例日期子目录，内含 TSV 结果文件
│   └── logs/                            # 运行日志目录，每个脚本独立生成 .log 文件
│       └── check_links_20260824.log     # 主脚本执行日志，含时间戳、错误与警告信息
├── lib/                                 # 公共函数库
│   ├── common.sh                        # 日志记录、参数解析、颜色输出、错误处理等通用函数
│   ├── url_parser.sh                    # URL 解析函数（提取 scheme、host、port、path、query）
│   └── validator.sh                     # 输入校验函数（检查 URL 格式、文件可读性、依赖命令存在性）
├── docs/                                # 完整文档目录
│   ├── user-guide.md                    # 用户手册，详细说明安装步骤、配置项与命令行用法
│   ├── config-reference.md              # 配置参考手册，逐条解释 config.env 中的变量作用域与默认值
│   ├── output-format.md                 # 输出字段定义文档，包括状态码映射表和扩展字段说明
│   ├── developer-guide.md               # 开发者指南，涵盖模块划分、新增功能流程和测试规范
│   └── troubleshooting.md               # 故障排除指南，收集常见错误编号及其解决方案
├── tests/                               # 单元测试与集成测试目录
│   ├── unit/                            # 单元测试脚本，每个函数对应一个 .bats 文件
│   │   ├── url_parser.bats              # 测试 URL 解析函数在各种边界输入下的正确性
│   │   └── validator.bats               # 测试输入校验函数对非法路径、空文件、缺失命令的检测
│   └── integration/                     # 集成测试脚本，模拟完整执行流程，检查最终输出格式与统计值
│       └── full_run.bats                # 使用测试用 URL 列表执行全流程并校验返回码
├── .gitignore                           # Git 忽略规则，排除 output/、*.log、config.env 等敏感或临时文件
├── CHANGELOG.md                         # 变更日志，按语义化版本记录每个版本的特性、修复与破坏性变更
├── LICENSE                              # MIT 许可证全文
└── README.md                            # 项目入口文档（本文件）
```

## 贡献指南

1. 查阅 issues 列表和项目看板，确认当前迭代周期内有待实现的特性或待修复的缺陷，避免重复工作。对于较大的功能提议，建议先创建讨论议题（Discussion）征询维护者意见。

2. 从 main 分支创建新的特性分支，分支命名遵循 `feature/功能简述` 或 `fix/问题简述` 格式。所有开发分支需基于最新的 main 分支，并在提交前执行 `git rebase main` 以保持线性历史。

3. 编写或修改脚本时，请严格遵循项目已有的编码风格：函数使用 `snake_case` 命名，全局变量使用大写加下划线，所有外部依赖命令需在 `validator.sh` 中进行存在性检查。新增的每个函数应附带注释说明输入参数、返回值和副作用。

4. 提交代码前必须运行完整的测试套件（`bats tests/`），确保所有已有单元测试和集成测试通过。对于新增功能，需同步编写对应的单元测试用例，覆盖正常路径与至少两种异常路径。

5. 发起 Pull Request 时，请在描述中清晰说明变更目的、涉及的脚本文件、测试覆盖情况以及是否对配置格式或输出结构产生破坏性变更。维护者会在 48 小时内进行初步评审，并可能要求补充测试或调整实现细节。

## 常见问题

Q: 检测脚本运行时提示 "curl: (35) SSL connect error"，但单独用 curl 访问同一链接正常，如何解决？

A: 该错误通常由服务器端 TLS 配置不兼容或本地证书缓存问题引起。可尝试在 config.env 中设置 `CURL_OPTIONS="--tlsv1.2 --no-keepalive"` 强制指定 TLS 版本并禁用保持连接。若仍无效，建议在脚本中添加 `--insecure` 参数（仅用于测试环境），但生产环境中应优先更新系统的 CA 证书包。

Q: 输出报告中的 "redirect_chain" 字段始终为空，如何启用重定向链跟踪？

A: 重定向链跟踪需要额外解析 curl 的 `--write-out` 输出中的 `%{redirect_url}` 变量，但默认配置下为了性能关闭了该功能。请在 config.env 中设置 `ENABLE_REDIRECT_TRACE=true`，同时建议调低并发数（`MAX_PARALLEL=10`）以避免大量重定向请求导致资源耗尽。开启后，输出文件将新增 `redirect_chain` 列，记录所有中间跳转地址。

Q: 能否将检测结果直接发送到 Elasticsearch 或 Prometheus 等监控系统？

A: 本工具定位为轻量级命令行工具，默认不集成外部监控系统。但您可以通过配置 `POST_PROCESS_CMD` 变量指向自定义处理脚本，在每次检测完成后自动触发数据转换与推送。社区已提供 `contrib/elasticsearch_ingest.sh` 和 `contrib/prometheus_exporter.py` 两个参考实现，请根据实际环境修改其中的索引名称和端点地址后使用。

## 许可证

MIT

> 外链数量: 250 | 生成时间: 2026-08-24 23:40:21
