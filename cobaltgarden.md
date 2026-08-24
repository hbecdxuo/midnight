# NewsLink Navigator

NewsLink Navigator 是一个面向新闻聚合、内容追溯与移动端信息抓取场景的轻量化外链导航系统。该项目旨在为开发者、数据分析师与内容运营人员提供一套可复用的新闻外链组织方案，能够将分散于移动端页面中的深层链接（深层链接）进行结构化整理，并生成可供二次处理的索引清单。项目本身不存储任何新闻内容，仅作为 URL 路由与元信息映射的中间层，适用于需要快速构建新闻外链看板、舆情监控数据源或内容归档索引的场景。

项目采用静态化配置与动态路由解析相结合的方式，所有资源链接均以纯文本形式维护于配置目录中，支持通过脚本批量校验链接可用性、提取域名分布与状态码。目标用户包括需要定期追踪特定新闻源的技术人员、搭建内部知识库的团队以及从事信息流分析的研究者。

## 功能概览

批量外链导入与自动去重：支持一次性导入大量以 .htm 结尾的移动端新闻链接，系统自动识别重复条目并生成唯一资源 ID。

链接状态批量检测：内置 HTTP 状态码检测模块，可并行发送 HEAD 请求，快速筛选出失效或重定向的链接。

域名聚合统计：自动解析链接中的域名与路径层级，输出按顶级域名、二级目录分组的数量分布报表。

自定义标签标注：允许用户为每个链接添加多组自定义标签（如“科技”、“社会”、“国际”），便于后续分类检索。

全文元信息抓取（可选）：集成了轻量级爬虫模块，可提取链接对应页面的标题、发布时间与摘要文本，存储为 JSON 格式的元数据文件。

配置热加载：所有链接配置文件支持修改后自动重载，无需重启服务即可更新导航列表。

导出为 CSV 与 Markdown 表格：支持将当前链接清单及元信息导出为标准 CSV 或 Markdown 格式，用于外部工具导入。

定时任务框架集成：提供基于 cron 表达式的定时校验与报告生成接口，可与现有调度系统无缝对接。

## 应用场景

舆情监控系统的数据源初始化：用户在搭建舆情看板时，需批量导入多个新闻站点的深层链接作为监控目标。NewsLink Navigator 可一次性接收数百个链接，完成去重与基础校验后，输出结构化的链接清单供上游爬虫使用。

内容归档项目的链接备份：针对移动端新闻链接易失效的特点，内容归档团队可定期将一批链接导入系统，通过状态检测功能标记异常链接，并批量导出可用链接列表，提高归档效率。

技术文档中的示例链接集维护：开发者撰写爬虫教程或 API 示例文档时，需要一组真实且稳定的测试链接。本项目可作为示例数据源，提供大量真实移动端新闻链接供学习使用，同时提供校验工具保证示例的可用性。

内部知识库的参考链接索引：企业内部的法务或合规部门需跟踪特定领域的新闻动态，可使用本项目将分散的新闻链接统一收录，并通过标签分类快速筛选出相关条目，形成内部参考索引。

## 快速开始

以下命令演示了从克隆仓库到启动本地服务的完整流程。

```bash
# 克隆项目仓库
git clone https://github.com/example/newslink-navigator.git

# 进入项目目录
cd newslink-navigator

# 安装 Python 依赖（推荐使用虚拟环境）
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt

# 导入示例链接数据（包含本批次 250 个链接）
python scripts/import_links.py --source data/links_batch_16.txt

# 启动本地开发服务器
python app.py --port 8080
```

访问 http://localhost:8080 即可查看链接导航面板，默认展示全部已导入链接。

## 安装要求

| 依赖项 | 必需版本 | 说明 |
|--------|----------|------|
| Python | 3.8 及以上 | 核心运行环境，用于后端服务与脚本执行 |
| Flask | 2.0.0 及以上 | Web 框架，提供导航面板界面与 REST API |
| requests | 2.25.0 及以上 | 用于发送 HTTP 请求，执行链接状态检测 |
| beautifulsoup4 | 4.9.0 及以上 | 可选依赖，用于元信息抓取模块的 HTML 解析 |
| croniter | 1.0.0 及以上 | 定时任务表达式解析，用于调度模块 |
| pytest | 6.0.0 及以上 | 开发依赖，用于运行单元测试与集成测试 |
| tox | 3.20.0 及以上 | 开发依赖，用于多版本 Python 环境验证 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|------|------|------------|
| 入门指南 | docs/getting-started.md | 如何快速导入第一批链接并启动面板？ |
| 配置手册 | docs/configuration.md | 链接配置文件格式、标签规则、环境变量有哪些？ |
| API 参考 | docs/api-reference.md | 如何通过 REST API 增删改查链接以及触发校验任务？ |
| 运维指南 | docs/operations.md | 如何部署到生产环境、配置定时任务与监控链接健康度？ |

## 资源列表

- http://m.3g.uliejh.cn/nnews/637163.htm
- http://m.3g.uliejh.cn/nnews/1468.htm
- http://m.3g.uliejh.cn/nnews/3156000.htm
- http://m.3g.uliejh.cn/nnews/8186530.htm
- http://m.3g.uliejh.cn/nnews/6184948.htm
- http://m.3g.uliejh.cn/nnews/397816.htm
- http://m.3g.uliejh.cn/nnews/7050419.htm
- http://m.3g.uliejh.cn/nnews/0831399.htm
- http://m.3g.uliejh.cn/nnews/4971966.htm
- http://m.3g.uliejh.cn/nnews/0976010.htm
- http://m.3g.uliejh.cn/nnews/833361.htm
- http://m.3g.uliejh.cn/nnews/961036.htm
- http://m.3g.uliejh.cn/nnews/40286.htm
- http://m.3g.uliejh.cn/nnews/6834077.htm
- http://m.3g.uliejh.cn/nnews/4311.htm
- http://m.3g.uliejh.cn/nnews/70093.htm
- http://m.3g.uliejh.cn/nnews/066333.htm
- http://m.3g.uliejh.cn/nnews/174376.htm
- http://m.3g.uliejh.cn/nnews/835085.htm
- http://m.3g.uliejh.cn/nnews/1191.htm
- http://m.3g.uliejh.cn/nnews/8374.htm
- http://m.3g.uliejh.cn/nnews/671433.htm
- http://m.3g.uliejh.cn/nnews/41045.htm
- http://m.3g.uliejh.cn/nnews/7811295.htm
- http://m.3g.uliejh.cn/nnews/7047583.htm
- http://m.3g.uliejh.cn/nnews/65149.htm
- http://m.3g.uliejh.cn/nnews/7081.htm
- http://m.3g.uliejh.cn/nnews/587668.htm
- http://m.3g.uliejh.cn/nnews/622852.htm
- http://m.3g.uliejh.cn/nnews/3256105.htm
- http://m.3g.uliejh.cn/nnews/494254.htm
- http://m.3g.uliejh.cn/nnews/007671.htm
- http://m.3g.uliejh.cn/nnews/5335.htm
- http://m.3g.uliejh.cn/nnews/2394729.htm
- http://m.3g.uliejh.cn/nnews/6208171.htm
- http://m.3g.uliejh.cn/nnews/1966800.htm
- http://m.3g.uliejh.cn/nnews/11973.htm
- http://m.3g.uliejh.cn/nnews/7218829.htm
- http://m.3g.uliejh.cn/nnews/4476.htm
- http://m.3g.uliejh.cn/nnews/879987.htm
- http://m.3g.uliejh.cn/nnews/20182.htm
- http://m.3g.uliejh.cn/nnews/5990755.htm
- http://m.3g.uliejh.cn/nnews/5307.htm
- http://m.3g.uliejh.cn/nnews/10326.htm
- http://m.3g.uliejh.cn/nnews/242026.htm
- http://m.3g.uliejh.cn/nnews/903414.htm
- http://m.3g.uliejh.cn/nnews/8111118.htm
- http://m.3g.uliejh.cn/nnews/5788265.htm
- http://m.3g.uliejh.cn/nnews/48780.htm
- http://m.3g.uliejh.cn/nnews/973246.htm
- http://m.3g.uliejh.cn/nnews/397836.htm
- http://m.3g.uliejh.cn/nnews/2466.htm
- http://m.3g.uliejh.cn/nnews/1194.htm
- http://m.3g.uliejh.cn/nnews/3433.htm
- http://m.3g.uliejh.cn/nnews/23909.htm
- http://m.3g.uliejh.cn/nnews/168020.htm
- http://m.3g.uliejh.cn/nnews/5351767.htm
- http://m.3g.uliejh.cn/nnews/19402.htm
- http://m.3g.uliejh.cn/nnews/8534990.htm
- http://m.3g.uliejh.cn/nnews/262229.htm
- http://m.3g.uliejh.cn/nnews/6330.htm
- http://m.3g.uliejh.cn/nnews/541562.htm
- http://m.3g.uliejh.cn/nnews/0727324.htm
- http://m.3g.uliejh.cn/nnews/3880.htm
- http://m.3g.uliejh.cn/nnews/6103222.htm
- http://m.3g.uliejh.cn/nnews/61238.htm
- http://m.3g.uliejh.cn/nnews/5271.htm
- http://m.3g.uliejh.cn/nnews/0100648.htm
- http://m.3g.uliejh.cn/nnews/5892.htm
- http://m.3g.uliejh.cn/nnews/54339.htm
- http://m.3g.uliejh.cn/nnews/9066.htm
- http://m.3g.uliejh.cn/nnews/9016992.htm
- http://m.3g.uliejh.cn/nnews/28267.htm
- http://m.3g.uliejh.cn/nnews/969566.htm
- http://m.3g.uliejh.cn/nnews/8054.htm
- http://m.3g.uliejh.cn/nnews/9104871.htm
- http://m.3g.uliejh.cn/nnews/2767477.htm
- http://m.3g.uliejh.cn/nnews/836316.htm
- http://m.3g.uliejh.cn/nnews/4611.htm
- http://m.3g.uliejh.cn/nnews/3389436.htm
- http://m.3g.uliejh.cn/nnews/0202565.htm
- http://m.3g.uliejh.cn/nnews/0405498.htm
- http://m.3g.uliejh.cn/nnews/4361431.htm
- http://m.3g.uliejh.cn/nnews/3404099.htm
- http://m.3g.uliejh.cn/nnews/5771.htm
- http://m.3g.uliejh.cn/nnews/488442.htm
- http://m.3g.uliejh.cn/nnews/37435.htm
- http://m.3g.uliejh.cn/nnews/703862.htm
- http://m.3g.uliejh.cn/nnews/1221.htm
- http://m.3g.uliejh.cn/nnews/0159.htm
- http://m.3g.uliejh.cn/nnews/6722562.htm
- http://m.3g.uliejh.cn/nnews/41476.htm
- http://m.3g.uliejh.cn/nnews/88167.htm
- http://m.3g.uliejh.cn/nnews/541690.htm
- http://m.3g.uliejh.cn/nnews/42201.htm
- http://m.3g.uliejh.cn/nnews/9986.htm
- http://m.3g.uliejh.cn/nnews/380417.htm
- http://m.3g.uliejh.cn/nnews/7215747.htm
- http://m.3g.uliejh.cn/nnews/9079213.htm
- http://m.3g.uliejh.cn/nnews/7047051.htm
- http://m.3g.uliejh.cn/nnews/553793.htm
- http://m.3g.uliejh.cn/nnews/06991.htm
- http://m.3g.uliejh.cn/nnews/5200.htm
- http://m.3g.uliejh.cn/nnews/52571.htm
- http://m.3g.uliejh.cn/nnews/70052.htm
- http://m.3g.uliejh.cn/nnews/84218.htm
- http://m.3g.uliejh.cn/nnews/2295678.htm
- http://m.3g.uliejh.cn/nnews/454018.htm
- http://m.3g.uliejh.cn/nnews/9265870.htm
- http://m.3g.uliejh.cn/nnews/05443.htm
- http://m.3g.uliejh.cn/nnews/3484793.htm
- http://m.3g.uliejh.cn/nnews/7158675.htm
- http://m.3g.uliejh.cn/nnews/7222.htm
- http://m.3g.uliejh.cn/nnews/80693.htm
- http://m.3g.uliejh.cn/nnews/1119234.htm
- http://m.3g.uliejh.cn/nnews/1297122.htm
- http://m.3g.uliejh.cn/nnews/986265.htm
- http://m.3g.uliejh.cn/nnews/8825171.htm
- http://m.3g.uliejh.cn/nnews/43558.htm
- http://m.3g.uliejh.cn/nnews/8402944.htm
- http://m.3g.uliejh.cn/nnews/88101.htm
- http://m.3g.uliejh.cn/nnews/1372002.htm
- http://m.3g.uliejh.cn/nnews/2570603.htm
- http://m.3g.uliejh.cn/nnews/310031.htm
- http://m.3g.uliejh.cn/nnews/7780.htm
- http://m.3g.uliejh.cn/nnews/50041.htm
- http://m.3g.uliejh.cn/nnews/7063.htm
- http://m.3g.uliejh.cn/nnews/936744.htm
- http://m.3g.uliejh.cn/nnews/393443.htm
- http://m.3g.uliejh.cn/nnews/24168.htm
- http://m.3g.uliejh.cn/nnews/1351.htm
- http://m.3g.uliejh.cn/nnews/13217.htm
- http://m.3g.uliejh.cn/nnews/7288095.htm
- http://m.3g.uliejh.cn/nnews/074603.htm
- http://m.3g.uliejh.cn/nnews/918177.htm
- http://m.3g.uliejh.cn/nnews/0602.htm
- http://m.3g.uliejh.cn/nnews/77266.htm
- http://m.3g.uliejh.cn/nnews/5151707.htm
- http://m.3g.uliejh.cn/nnews/463056.htm
- http://m.3g.uliejh.cn/nnews/08007.htm
- http://m.3g.uliejh.cn/nnews/76057.htm
- http://m.3g.uliejh.cn/nnews/411108.htm
- http://m.3g.uliejh.cn/nnews/34419.htm
- http://m.3g.uliejh.cn/nnews/0545311.htm
- http://m.3g.uliejh.cn/nnews/1015216.htm
- http://m.3g.uliejh.cn/nnews/89843.htm
- http://m.3g.uliejh.cn/nnews/55846.htm
- http://m.3g.uliejh.cn/nnews/104928.htm
- http://m.3g.uliejh.cn/nnews/7857804.htm
- http://m.3g.uliejh.cn/nnews/1460685.htm
- http://m.3g.uliejh.cn/nnews/61530.htm
- http://m.3g.uliejh.cn/nnews/47613.htm
- http://m.3g.uliejh.cn/nnews/125324.htm
- http://m.3g.uliejh.cn/nnews/953812.htm
- http://m.3g.uliejh.cn/nnews/96088.htm
- http://m.3g.uliejh.cn/nnews/35050.htm
- http://m.3g.uliejh.cn/nnews/7161682.htm
- http://m.3g.uliejh.cn/nnews/938051.htm
- http://m.3g.uliejh.cn/nnews/0885.htm
- http://m.3g.uliejh.cn/nnews/1463.htm
- http://m.3g.uliejh.cn/nnews/46406.htm
- http://m.3g.uliejh.cn/nnews/0592572.htm
- http://m.3g.uliejh.cn/nnews/6629.htm
- http://m.3g.uliejh.cn/nnews/33600.htm
- http://m.3g.uliejh.cn/nnews/7471682.htm
- http://m.3g.uliejh.cn/nnews/12304.htm
- http://m.3g.uliejh.cn/nnews/9589.htm
- http://m.3g.uliejh.cn/nnews/9561.htm
- http://m.3g.uliejh.cn/nnews/8319944.htm
- http://m.3g.uliejh.cn/nnews/6834832.htm
- http://m.3g.uliejh.cn/nnews/4382.htm
- http://m.3g.uliejh.cn/nnews/25378.htm
- http://m.3g.uliejh.cn/nnews/4520.htm
- http://m.3g.uliejh.cn/nnews/23334.htm
- http://m.3g.uliejh.cn/nnews/0371.htm
- http://m.3g.uliejh.cn/nnews/2337.htm
- http://m.3g.uliejh.cn/nnews/1852.htm
- http://m.3g.uliejh.cn/nnews/72860.htm
- http://m.3g.uliejh.cn/nnews/0254.htm
- http://m.3g.uliejh.cn/nnews/5790.htm
- http://m.3g.uliejh.cn/nnews/32003.htm
- http://m.3g.uliejh.cn/nnews/5903051.htm
- http://m.3g.uliejh.cn/nnews/23700.htm
- http://m.3g.uliejh.cn/nnews/07052.htm
- http://m.3g.uliejh.cn/nnews/600916.htm
- http://m.3g.uliejh.cn/nnews/466765.htm
- http://m.3g.uliejh.cn/nnews/4475.htm
- http://m.3g.uliejh.cn/nnews/62573.htm
- http://m.3g.uliejh.cn/nnews/06322.htm
- http://m.3g.uliejh.cn/nnews/596919.htm
- http://m.3g.uliejh.cn/nnews/8668290.htm
- http://m.3g.uliejh.cn/nnews/45510.htm
- http://m.3g.uliejh.cn/nnews/905098.htm
- http://m.3g.uliejh.cn/nnews/5770916.htm
- http://m.3g.uliejh.cn/nnews/5879.htm
- http://m.3g.uliejh.cn/nnews/4877432.htm
- http://m.3g.uliejh.cn/nnews/340554.htm
- http://m.3g.uliejh.cn/nnews/5894837.htm
- http://m.3g.uliejh.cn/nnews/918592.htm
- http://m.3g.uliejh.cn/nnews/1326.htm
- http://m.3g.uliejh.cn/nnews/5710173.htm
- http://m.3g.uliejh.cn/nnews/6430.htm
- http://m.3g.uliejh.cn/nnews/40586.htm
- http://m.3g.uliejh.cn/nnews/232370.htm
- http://m.3g.uliejh.cn/nnews/1398313.htm
- http://m.3g.uliejh.cn/nnews/070603.htm
- http://m.3g.uliejh.cn/nnews/58254.htm
- http://m.3g.uliejh.cn/nnews/9923272.htm
- http://m.3g.uliejh.cn/nnews/6094623.htm
- http://m.3g.uliejh.cn/nnews/69608.htm
- http://m.3g.uliejh.cn/nnews/7163.htm
- http://m.3g.uliejh.cn/nnews/7460005.htm
- http://m.3g.uliejh.cn/nnews/08259.htm
- http://m.3g.uliejh.cn/nnews/33546.htm
- http://m.3g.uliejh.cn/nnews/0763095.htm
- http://m.3g.uliejh.cn/nnews/03141.htm
- http://m.3g.uliejh.cn/nnews/4262.htm
- http://m.3g.uliejh.cn/nnews/07509.htm
- http://m.3g.uliejh.cn/nnews/10668.htm
- http://m.3g.uliejh.cn/nnews/815727.htm
- http://m.3g.uliejh.cn/nnews/60294.htm
- http://m.3g.uliejh.cn/nnews/1527077.htm
- http://m.3g.uliejh.cn/nnews/908258.htm
- http://m.3g.uliejh.cn/nnews/912474.htm
- http://m.3g.uliejh.cn/nnews/7343.htm
- http://m.3g.uliejh.cn/nnews/9732.htm
- http://m.3g.uliejh.cn/nnews/232853.htm
- http://m.3g.uliejh.cn/nnews/057783.htm
- http://m.3g.uliejh.cn/nnews/93595.htm
- http://m.3g.uliejh.cn/nnews/7564.htm
- http://m.3g.uliejh.cn/nnews/923936.htm
- http://m.3g.uliejh.cn/nnews/3843462.htm
- http://m.3g.uliejh.cn/nnews/488112.htm
- http://m.3g.uliejh.cn/nnews/7502887.htm
- http://m.3g.uliejh.cn/nnews/10797.htm
- http://m.3g.uliejh.cn/nnews/3621.htm
- http://m.3g.uliejh.cn/nnews/9609.htm
- http://m.3g.uliejh.cn/nnews/4314.htm
- http://m.3g.uliejh.cn/nnews/5505244.htm
- http://m.3g.uliejh.cn/nnews/266597.htm
- http://m.3g.uliejh.cn/nnews/81290.htm
- http://m.3g.uliejh.cn/nnews/6944.htm
- http://m.3g.uliejh.cn/nnews/0244841.htm
- http://m.3g.uliejh.cn/nnews/2170.htm
- http://m.3g.uliejh.cn/nnews/74208.htm
- http://m.3g.uliejh.cn/nnews/984687.htm
- http://m.3g.uliejh.cn/nnews/67585.htm
- http://m.3g.uliejh.cn/nnews/817295.htm
- http://m.3g.uliejh.cn/nnews/234649.htm
- http://m.3g.uliejh.cn/nnews/4905.htm

## 项目结构

项目采用分层架构，将配置、核心逻辑、接口与工具脚本分离，便于维护与扩展。

```
newslink-navigator/
├── app.py                      # Flask 应用入口，注册路由与启动服务
├── config/
│   ├── settings.py             # 全局配置（端口、超时、缓存策略等）
│   └── link_sources.yaml       # 定义链接批次与数据源映射关系
├── core/
│   ├── __init__.py
│   ├── importer.py             # 链接导入与去重核心逻辑
│   ├── checker.py              # 批量状态检测模块（并发请求）
│   ├── parser.py               # 元信息抓取与 HTML 解析封装
│   └── aggregator.py           # 域名聚合与统计报表生成
├── api/
│   ├── __init__.py
│   ├── routes.py               # REST API 路由定义（增删改查、校验触发）
│   └── schemas.py              # 请求与响应的 Pydantic 模型
├── scripts/
│   ├── import_links.py         # 命令行导入脚本，支持指定批次文件
│   ├── check_all.py            # 批量校验所有已导入链接的可用性
│   └── export_csv.py           # 导出当前链接清单为 CSV 格式
├── data/
│   ├── links_batch_16.txt      # 本批次原始链接列表（250 条）
│   └── metadata/               # 存储抓取到的页面元信息（JSON 格式）
├── tests/
│   ├── test_importer.py        # 导入模块的单元测试
│   ├── test_checker.py         # 状态检测模块的单元测试
│   └── test_api.py             # API 接口的集成测试
├── docs/
│   ├── getting-started.md      # 入门指南
│   ├── configuration.md        # 完整配置说明
│   ├── api-reference.md        # API 端点详细文档
│   └── operations.md           # 生产环境部署与运维手册
├── requirements.txt            # 生产环境依赖列表
├── requirements-dev.txt        # 开发与测试环境额外依赖
├── Dockerfile                  # 容器化构建文件
├── docker-compose.yml          # 本地开发与测试的编排配置
└── README.md                   # 项目总体说明文档（本文件）
```

## 贡献指南

我们欢迎并鼓励社区贡献，无论是报告问题、提交代码还是完善文档。请遵循以下步骤参与项目。

第一步：查阅现有的 Issue 列表与项目看板，确认您想要解决的问题或希望新增的功能尚未被他人认领。如无相关 Issue，请先新建一个 Issue 描述您的需求或问题。

第二步：Fork 本仓库到您的个人账户，然后 clone 到本地开发环境。请确保您的开发分支基于最新的 main 分支，并使用规范的命名方式，例如 feature/link-tagging 或 fix/checker-timeout。

第三步：编写代码或文档变更时，请遵循项目现有的代码风格（PEP 8 用于 Python，使用 black 进行自动格式化）。所有新增功能必须包含对应的单元测试，测试覆盖率不应低于 80%。

第四步：提交代码前，请在本机运行完整的测试套件（使用 tox 或 pytest）以确保没有引入回归问题。同时更新相关文档（如 API 参考或配置手册）以反映您的变更。

第五步：发起 Pull Request 到主仓库的 main 分支，并在 PR 描述中清晰引用相关的 Issue 编号，简述您的实现方案与测试结果。PR 将会由维护者进行 Code Review，通过后即可合并。

## 常见问题

问：批量导入链接时，系统提示部分链接格式无效，该如何处理？

答：导入模块默认要求链接以 http:// 或 https:// 开头，且文件扩展名为 .htm 或 .html。如果您的链接不符合此格式，请先使用脚本 scripts/preprocess_links.py 进行格式化预处理。此外，链接中若包含空格或特殊字符，需要先进行 URL 编码。您可以查看 logs/import_errors.log 获取详细的失败原因列表。

问：状态检测模块返回大量超时或连接错误，是什么原因？

答：这通常是因为目标新闻站点的响应速度较慢，或者网络环境存在限制。您可以调整 config/settings.py 中的 REQUEST_TIMEOUT 参数（默认值为 10 秒）和 MAX_CONCURRENT_REQUESTS 参数（默认值为 20）来优化检测策略。同时，建议在非高峰时段执行批量检测，并考虑使用代理或 VPN 以改善连接稳定性。

问：如何定期自动更新链接状态并发送报告？

答：项目内置了调度模块，您可以在 config/settings.py 中配置 CHECK_CRON 表达式（例如 '0 2 * * *' 表示每天凌晨 2 点执行）。启动服务时添加 --scheduler 参数即可启用内置调度器。对于生产环境，我们推荐使用系统级 cron 任务或 Kubernetes CronJob 来定期执行 scripts/check_all.py，并将输出报告通过邮件或 Webhook 发送给相关责任人。

## 许可证

MIT

> 外链数量: 250 | 生成时间: 2026-08-24 23:40:21
