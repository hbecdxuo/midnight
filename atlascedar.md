# WebLink Archive Aggregator

WebLink Archive Aggregator 是一个面向技术文档研究者、前端开发者和数据挖掘工程师的轻量级外链资源汇总工具。该项目通过结构化方式收集并索引分布于互联网各节点的技术资讯页面，提供统一的访问入口与元数据提取能力，帮助用户在海量分散的链接中快速定位目标内容。项目本身不生产内容，仅做链接的整理与分类展示，适用于需要定期追踪特定域名下文档更新的自动化工作流。

## 功能概览

批量链接导入与去重：支持从纯文本列表、CSV 或直接粘贴的 URL 清单中批量导入链接，自动识别重复条目并生成唯一索引标识。

链接健康状态检测：内置 HTTP 状态码检查模块，可定时探测每个链接的可达性，标记异常链接并生成可用性报告。

元数据自动提取：对每个链接自动发起 HEAD 请求，提取 Content-Type、Last-Modified、Content-Length 等响应头信息，辅助判断资源类型。

分类标签管理：允许用户为每个链接添加自定义标签（如 "技术文档"、"API 参考"、"新闻公告"），支持按标签过滤和检索。

全文检索与过滤：基于链接 URL、页面标题、标签和提取的元数据构建简单的倒排索引，支持关键词模糊匹配与多条件组合筛选。

导出与订阅机制：支持将当前链接列表导出为 JSON、CSV 或纯文本格式，并提供基于时间戳的增量订阅文件生成功能。

定时更新触发器：集成 cron 表达式调度器，可设定每日、每周或每月自动重新检测所有链接状态，并推送变更通知。

## 应用场景

技术文档版本追踪：团队内部需要持续监控某外部文档站点的更新情况时，可将该站点的系列链接导入系统，定期检查 Last-Modified 变化，及时获取新版本发布信息。

历史页面归档检索：研究人员收集某域名下大量历史新闻页面后，利用本项目的标签与检索功能快速按时间、主题或关键词回溯特定事件报道，避免人工逐条翻阅。

数据源可用性监控：数据采集管道依赖多个外部资讯源，运维人员将全部依赖链接纳入本项目，通过健康检测模块在数据拉取前置检查源可用性，减少采集失败率。

资源聚合展示：个人开发者或内容策展人将不同分类的技术资源链接汇总后，通过导出功能生成静态列表，用于搭建个人导航站或技术周刊素材库。

自动化告警链路：将项目与邮件或即时通讯工具集成，当检测到核心链接连续不可达或返回异常状态码时自动触发告警，降低业务被动中断风险。

## 快速开始

以下指令适用于 Linux 与 macOS 环境，Windows 用户建议使用 WSL 或 Git Bash 执行。

```bash
# 克隆项目仓库
git clone https://github.com/weblink-archive/aggregator.git
cd aggregator

# 安装 Python 依赖（要求 Python 3.9+）
pip install -r requirements.txt

# 初始化本地数据库与配置文件
python scripts/init_db.py --config config/default.yaml

# 运行链接导入示例（导入 resources/example_links.txt 中的链接）
python cli.py import --file resources/example_links.txt

# 启动健康检测服务（后台运行）
python cli.py health-check --interval 3600 --daemon

# 启动 Web 管理界面（默认端口 8080）
python app.py --host 0.0.0.0 --port 8080
```

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|---|---|---|
| Python | 3.9.0 及以上 | 核心运行环境，低于此版本将无法解析类型注解与异步语法 |
| SQLite | 3.35.0 及以上 | 嵌入式数据库，用于存储链接元数据与检测历史记录 |
| aiohttp | 3.8.0 及以上 | 异步 HTTP 客户端，用于高并发健康检测与元数据抓取 |
| PyYAML | 6.0 及以上 | 配置文件解析器，用于加载用户自定义调度规则与过滤条件 |
| uvicorn | 0.20.0 及以上 | ASGI 服务器，用于启动 Web 管理界面的服务进程 |
| python-crontab | 3.0.0 及以上 | 定时任务管理库，用于解析和执行 cron 表达式调度 |
| click | 8.1.0 及以上 | 命令行交互框架，提供子命令解析与参数校验能力 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|---|---|---|
| 用户指南 | docs/user_guide/import_export.md | 如何批量导入链接、如何导出筛选结果、支持哪些数据格式 |
| 运维手册 | docs/ops/health_check.md | 健康检测的工作原理、阈值配置方法、告警通道如何设置 |
| 开发者文档 | docs/developer/api_reference.md | 核心模块的类结构、方法签名、扩展自定义检测器的接口规范 |
| 配置参考 | docs/config/scheduling.md | cron 表达式的写法、调度器优先级、日志轮转策略 |

## 资源列表

- http://m.wap.uliejh.cn/bnews/8863.htm
- http://m.wap.uliejh.cn/bnews/5459.htm
- http://m.wap.uliejh.cn/bnews/9648.htm
- http://m.wap.uliejh.cn/bnews/073118.htm
- http://m.wap.uliejh.cn/bnews/448493.htm
- http://m.wap.uliejh.cn/bnews/5342980.htm
- http://m.wap.uliejh.cn/bnews/34208.htm
- http://m.wap.uliejh.cn/bnews/07851.htm
- http://m.wap.uliejh.cn/bnews/81724.htm
- http://m.wap.uliejh.cn/bnews/25856.htm
- http://m.wap.uliejh.cn/bnews/5875.htm
- http://m.wap.uliejh.cn/bnews/39754.htm
- http://m.wap.uliejh.cn/bnews/0857.htm
- http://m.wap.uliejh.cn/bnews/14706.htm
- http://m.wap.uliejh.cn/bnews/686883.htm
- http://m.wap.uliejh.cn/bnews/8051.htm
- http://m.wap.uliejh.cn/bnews/61130.htm
- http://m.wap.uliejh.cn/bnews/1302.htm
- http://m.wap.uliejh.cn/bnews/72574.htm
- http://m.wap.uliejh.cn/bnews/77437.htm
- http://m.wap.uliejh.cn/bnews/80812.htm
- http://m.wap.uliejh.cn/bnews/5552869.htm
- http://m.wap.uliejh.cn/bnews/40879.htm
- http://m.wap.uliejh.cn/bnews/60690.htm
- http://m.wap.uliejh.cn/bnews/4266279.htm
- http://m.wap.uliejh.cn/bnews/3254041.htm
- http://m.wap.uliejh.cn/bnews/7905736.htm
- http://m.wap.uliejh.cn/bnews/92387.htm
- http://m.wap.uliejh.cn/bnews/944303.htm
- http://m.wap.uliejh.cn/bnews/047439.htm
- http://m.wap.uliejh.cn/bnews/1801808.htm
- http://m.wap.uliejh.cn/bnews/92087.htm
- http://m.wap.uliejh.cn/bnews/6306317.htm
- http://m.wap.uliejh.cn/bnews/2657.htm
- http://m.wap.uliejh.cn/bnews/059541.htm
- http://m.wap.uliejh.cn/bnews/10469.htm
- http://m.wap.uliejh.cn/bnews/6460.htm
- http://m.wap.uliejh.cn/bnews/31839.htm
- http://m.wap.uliejh.cn/bnews/62710.htm
- http://m.wap.uliejh.cn/bnews/3303.htm
- http://m.wap.uliejh.cn/bnews/308583.htm
- http://m.wap.uliejh.cn/bnews/13500.htm
- http://m.wap.uliejh.cn/bnews/55781.htm
- http://m.wap.uliejh.cn/bnews/5049004.htm
- http://m.wap.uliejh.cn/bnews/06740.htm
- http://m.wap.uliejh.cn/bnews/8374.htm
- http://m.wap.uliejh.cn/bnews/1011766.htm
- http://m.wap.uliejh.cn/bnews/381490.htm
- http://m.wap.uliejh.cn/bnews/93978.htm
- http://m.wap.uliejh.cn/bnews/57036.htm
- http://m.wap.uliejh.cn/bnews/78978.htm
- http://m.wap.uliejh.cn/bnews/106641.htm
- http://m.wap.uliejh.cn/bnews/9767.htm
- http://m.wap.uliejh.cn/bnews/3922968.htm
- http://m.wap.uliejh.cn/bnews/002966.htm
- http://m.wap.uliejh.cn/bnews/8889.htm
- http://m.wap.uliejh.cn/bnews/1792299.htm
- http://m.wap.uliejh.cn/bnews/5589910.htm
- http://m.wap.uliejh.cn/bnews/2967683.htm
- http://m.wap.uliejh.cn/bnews/0639.htm
- http://m.wap.uliejh.cn/bnews/9001900.htm
- http://m.wap.uliejh.cn/bnews/3188433.htm
- http://m.wap.uliejh.cn/bnews/211826.htm
- http://m.wap.uliejh.cn/bnews/425972.htm
- http://m.wap.uliejh.cn/bnews/722615.htm
- http://m.wap.uliejh.cn/bnews/0092132.htm
- http://m.wap.uliejh.cn/bnews/9051920.htm
- http://m.wap.uliejh.cn/bnews/8008.htm
- http://m.wap.uliejh.cn/bnews/8003.htm
- http://m.wap.uliejh.cn/bnews/369305.htm
- http://m.wap.uliejh.cn/bnews/1773.htm
- http://m.wap.uliejh.cn/bnews/969055.htm
- http://m.wap.uliejh.cn/bnews/743333.htm
- http://m.wap.uliejh.cn/bnews/17894.htm
- http://m.wap.uliejh.cn/bnews/571472.htm
- http://m.wap.uliejh.cn/bnews/236234.htm
- http://m.wap.uliejh.cn/bnews/08253.htm
- http://m.wap.uliejh.cn/bnews/5888.htm
- http://m.wap.uliejh.cn/bnews/6839620.htm
- http://m.wap.uliejh.cn/bnews/3497481.htm
- http://m.wap.uliejh.cn/bnews/088621.htm
- http://m.wap.uliejh.cn/bnews/9586.htm
- http://m.wap.uliejh.cn/bnews/8562.htm
- http://m.wap.uliejh.cn/bnews/0184564.htm
- http://m.wap.uliejh.cn/bnews/6814716.htm
- http://m.wap.uliejh.cn/bnews/1931.htm
- http://m.wap.uliejh.cn/bnews/80957.htm
- http://m.wap.uliejh.cn/bnews/1446974.htm
- http://m.wap.uliejh.cn/bnews/156267.htm
- http://m.wap.uliejh.cn/bnews/9522125.htm
- http://m.wap.uliejh.cn/bnews/905740.htm
- http://m.wap.uliejh.cn/bnews/53224.htm
- http://m.wap.uliejh.cn/bnews/594028.htm
- http://m.wap.uliejh.cn/bnews/404380.htm
- http://m.wap.uliejh.cn/bnews/988533.htm
- http://m.wap.uliejh.cn/bnews/7040278.htm
- http://m.wap.uliejh.cn/bnews/22635.htm
- http://m.wap.uliejh.cn/bnews/3763848.htm
- http://m.wap.uliejh.cn/bnews/7901.htm
- http://m.wap.uliejh.cn/bnews/2189.htm
- http://m.wap.uliejh.cn/bnews/4485.htm
- http://m.wap.uliejh.cn/bnews/47579.htm
- http://m.wap.uliejh.cn/bnews/46014.htm
- http://m.wap.uliejh.cn/bnews/819552.htm
- http://m.wap.uliejh.cn/bnews/297758.htm
- http://m.wap.uliejh.cn/bnews/73146.htm
- http://m.wap.uliejh.cn/bnews/04793.htm
- http://m.wap.uliejh.cn/bnews/760337.htm
- http://m.wap.uliejh.cn/bnews/6742.htm
- http://m.wap.uliejh.cn/bnews/3585187.htm
- http://m.wap.uliejh.cn/bnews/39086.htm
- http://m.wap.uliejh.cn/bnews/49385.htm
- http://m.wap.uliejh.cn/bnews/5671232.htm
- http://m.wap.uliejh.cn/bnews/89629.htm
- http://m.wap.uliejh.cn/bnews/1612.htm
- http://m.wap.uliejh.cn/bnews/0430.htm
- http://m.wap.uliejh.cn/bnews/3616288.htm
- http://m.wap.uliejh.cn/bnews/30755.htm
- http://m.wap.uliejh.cn/bnews/547680.htm
- http://m.wap.uliejh.cn/bnews/93485.htm
- http://m.wap.uliejh.cn/bnews/806335.htm
- http://m.wap.uliejh.cn/bnews/7306.htm
- http://m.wap.uliejh.cn/bnews/3125.htm
- http://m.wap.uliejh.cn/bnews/87707.htm
- http://m.wap.uliejh.cn/bnews/14632.htm
- http://m.wap.uliejh.cn/bnews/7762573.htm
- http://m.wap.uliejh.cn/bnews/001159.htm
- http://m.wap.uliejh.cn/bnews/875946.htm
- http://m.wap.uliejh.cn/bnews/4049408.htm
- http://m.wap.uliejh.cn/bnews/0453.htm
- http://m.wap.uliejh.cn/bnews/140282.htm
- http://m.wap.uliejh.cn/bnews/00138.htm
- http://m.wap.uliejh.cn/bnews/5511358.htm
- http://m.wap.uliejh.cn/bnews/9361754.htm
- http://m.wap.uliejh.cn/bnews/89583.htm
- http://m.wap.uliejh.cn/bnews/3361316.htm
- http://m.wap.uliejh.cn/bnews/1834130.htm
- http://m.wap.uliejh.cn/bnews/2752049.htm
- http://m.wap.uliejh.cn/bnews/3735721.htm
- http://m.wap.uliejh.cn/bnews/358193.htm
- http://m.wap.uliejh.cn/bnews/8782296.htm
- http://m.wap.uliejh.cn/bnews/643785.htm
- http://m.wap.uliejh.cn/bnews/3975268.htm
- http://m.wap.uliejh.cn/bnews/777014.htm
- http://m.wap.uliejh.cn/bnews/37428.htm
- http://m.wap.uliejh.cn/bnews/3881550.htm
- http://m.wap.uliejh.cn/bnews/0681.htm
- http://m.wap.uliejh.cn/bnews/80349.htm
- http://m.wap.uliejh.cn/bnews/745543.htm
- http://m.wap.uliejh.cn/bnews/313365.htm
- http://m.wap.uliejh.cn/bnews/27620.htm
- http://m.wap.uliejh.cn/bnews/3432908.htm
- http://m.wap.uliejh.cn/bnews/7258.htm
- http://m.wap.uliejh.cn/bnews/25377.htm
- http://m.wap.uliejh.cn/bnews/4497024.htm
- http://m.wap.uliejh.cn/bnews/984905.htm
- http://m.wap.uliejh.cn/bnews/5267819.htm
- http://m.wap.uliejh.cn/bnews/435097.htm
- http://m.wap.uliejh.cn/bnews/39987.htm
- http://m.wap.uliejh.cn/bnews/0776631.htm
- http://m.wap.uliejh.cn/bnews/71964.htm
- http://m.wap.uliejh.cn/bnews/9874.htm
- http://m.wap.uliejh.cn/bnews/778674.htm
- http://m.wap.uliejh.cn/bnews/7786718.htm
- http://m.wap.uliejh.cn/bnews/698539.htm
- http://m.wap.uliejh.cn/bnews/9718066.htm
- http://m.wap.uliejh.cn/bnews/777332.htm
- http://m.wap.uliejh.cn/bnews/1801028.htm
- http://m.wap.uliejh.cn/bnews/445181.htm
- http://m.wap.uliejh.cn/bnews/7082803.htm
- http://m.wap.uliejh.cn/bnews/12831.htm
- http://m.wap.uliejh.cn/bnews/9376.htm
- http://m.wap.uliejh.cn/bnews/226952.htm
- http://m.wap.uliejh.cn/bnews/69403.htm
- http://m.wap.uliejh.cn/bnews/437042.htm
- http://m.wap.uliejh.cn/bnews/094015.htm
- http://m.wap.uliejh.cn/bnews/20498.htm
- http://m.wap.uliejh.cn/bnews/77901.htm
- http://m.wap.uliejh.cn/bnews/841513.htm
- http://m.wap.uliejh.cn/bnews/783443.htm
- http://m.wap.uliejh.cn/bnews/772853.htm
- http://m.wap.uliejh.cn/bnews/6687875.htm
- http://m.wap.uliejh.cn/bnews/3806.htm
- http://m.wap.uliejh.cn/bnews/1516.htm
- http://m.wap.uliejh.cn/bnews/6162216.htm
- http://m.wap.uliejh.cn/bnews/3967271.htm
- http://m.wap.uliejh.cn/bnews/777159.htm
- http://m.wap.uliejh.cn/bnews/960399.htm
- http://m.wap.uliejh.cn/bnews/564727.htm
- http://m.wap.uliejh.cn/bnews/940393.htm
- http://m.wap.uliejh.cn/bnews/9361.htm
- http://m.wap.uliejh.cn/bnews/3708.htm
- http://m.wap.uliejh.cn/bnews/7500.htm
- http://m.wap.uliejh.cn/bnews/482084.htm
- http://m.wap.uliejh.cn/bnews/8612008.htm
- http://m.wap.uliejh.cn/bnews/458484.htm
- http://m.wap.uliejh.cn/bnews/3986650.htm
- http://m.wap.uliejh.cn/bnews/1396.htm
- http://m.wap.uliejh.cn/bnews/5706762.htm
- http://m.wap.uliejh.cn/bnews/835783.htm
- http://m.wap.uliejh.cn/bnews/2473.htm
- http://m.wap.uliejh.cn/bnews/6133.htm
- http://m.wap.uliejh.cn/bnews/5698.htm
- http://m.wap.uliejh.cn/bnews/9675.htm
- http://m.wap.uliejh.cn/bnews/326852.htm
- http://m.wap.uliejh.cn/bnews/554750.htm
- http://m.wap.uliejh.cn/bnews/3952.htm
- http://m.wap.uliejh.cn/bnews/4267.htm
- http://m.wap.uliejh.cn/bnews/49972.htm
- http://m.wap.uliejh.cn/bnews/687977.htm
- http://m.wap.uliejh.cn/bnews/307940.htm
- http://m.wap.uliejh.cn/bnews/8288.htm
- http://m.wap.uliejh.cn/bnews/39829.htm
- http://m.wap.uliejh.cn/bnews/72037.htm
- http://m.wap.uliejh.cn/bnews/3997528.htm
- http://m.wap.uliejh.cn/bnews/1812356.htm
- http://m.wap.uliejh.cn/bnews/0126055.htm
- http://m.wap.uliejh.cn/bnews/54254.htm
- http://m.wap.uliejh.cn/bnews/00554.htm
- http://m.wap.uliejh.cn/bnews/2446948.htm
- http://m.wap.uliejh.cn/bnews/5347264.htm
- http://m.wap.uliejh.cn/bnews/2916390.htm
- http://m.wap.uliejh.cn/bnews/70754.htm
- http://m.wap.uliejh.cn/bnews/921375.htm
- http://m.wap.uliejh.cn/bnews/9577.htm
- http://m.wap.uliejh.cn/bnews/5882239.htm
- http://m.wap.uliejh.cn/bnews/9970986.htm
- http://m.wap.uliejh.cn/bnews/5588.htm
- http://m.wap.uliejh.cn/bnews/319486.htm
- http://m.wap.uliejh.cn/bnews/8009872.htm
- http://m.wap.uliejh.cn/bnews/15510.htm
- http://m.wap.uliejh.cn/bnews/50653.htm
- http://m.wap.uliejh.cn/bnews/2720.htm
- http://m.wap.uliejh.cn/bnews/10031.htm
- http://m.wap.uliejh.cn/bnews/4191546.htm
- http://m.wap.uliejh.cn/bnews/525986.htm
- http://m.wap.uliejh.cn/bnews/598142.htm
- http://m.wap.uliejh.cn/bnews/859561.htm
- http://m.wap.uliejh.cn/bnews/85096.htm
- http://m.wap.uliejh.cn/bnews/21559.htm
- http://m.wap.uliejh.cn/bnews/39009.htm
- http://m.wap.uliejh.cn/bnews/0714736.htm
- http://m.wap.uliejh.cn/bnews/1095.htm
- http://m.wap.uliejh.cn/bnews/3062968.htm
- http://m.wap.uliejh.cn/bnews/0543.htm
- http://m.wap.uliejh.cn/bnews/5794353.htm
- http://m.wap.uliejh.cn/bnews/9692336.htm
- http://m.wap.uliejh.cn/bnews/457071.htm
- http://m.wap.uliejh.cn/bnews/357570.htm
- http://m.wap.uliejh.cn/bnews/74071.htm

## 项目结构

```
aggregator/
├── app.py                      # Web 管理界面入口，基于 FastAPI 提供 REST API 与静态页面
├── cli.py                      # 命令行接口主入口，注册 import、health-check、export 等子命令
├── config/
│   ├── default.yaml            # 默认全局配置，含数据库路径、检测并发数、日志级别
│   ├── scheduling.yaml         # 调度任务配置，定义 cron 表达式与对应的检测策略
│   └── custom/                 # 用户自定义配置目录，支持多环境隔离
├── core/
│   ├── __init__.py
│   ├── db.py                   # SQLite 数据库连接池与 ORM 映射，定义 Link、CheckHistory 模型
│   ├── fetcher.py              # 异步 HTTP 请求封装，含重试、超时、代理支持逻辑
│   ├── parser.py               # 响应头解析与元数据提取，包括 Content-Type 判定与编码识别
│   ├── scheduler.py            # 基于 python-crontab 的定时任务引擎，触发健康检测与报告生成
│   └── indexer.py              # 轻量级倒排索引构建器，支持 URL 与标签的模糊匹配
├── resources/
│   ├── example_links.txt       # 示例链接列表，供快速导入测试使用
│   └── user_agents.txt         # 轮换使用的 User-Agent 池，降低被检测站点屏蔽的概率
├── scripts/
│   ├── init_db.py              # 初始化数据库表结构与创建默认管理员账户
│   └── migrate_v2.py           # 数据库版本升级脚本，从 v1 结构迁移至 v2
├── tests/
│   ├── test_fetcher.py         # 异步 HTTP 请求模块的单元测试，覆盖超时与异常重试场景
│   ├── test_parser.py          # 元数据解析模块的边界值测试，含非标准响应头处理
│   └── test_scheduler.py       # 调度器任务触发的集成测试，验证 cron 表达式生效情况
├── docs/                       # 完整文档目录，包含用户指南、运维手册与 API 文档
├── requirements.txt            # Python 依赖列表，固定版本号以保证环境一致性
└── LICENSE                     # MIT 许可证文件
```

## 贡献指南

提交 Issue 报告缺陷或功能请求：在 GitHub Issues 页面创建新问题，使用提供的模板填写复现步骤、运行环境及日志片段，维护者将在 48 小时内响应。

代码贡献流程：Fork 本仓库至个人账户，在 dev 分支上创建功能特性分支（命名格式为 feature/功能简述），完成开发后提交 Pull Request 到主仓库的 dev 分支，需确保通过所有单元测试且代码覆盖率不低于 85%。

文档完善与翻译：欢迎修正文档中的拼写错误、补充缺失的配置说明或增加新的使用案例。文档采用 Markdown 格式编写，存放于 docs 目录下，提交时请遵循中文技术文档写作规范。

本地测试环境搭建：运行 make test 命令可自动启动虚拟环境并执行全部测试用例。新增功能需同步编写对应的测试用例，测试文件放置在 tests 目录下，命名与源模块对应。

行为准则：所有参与者需遵守贡献者公约，保持友善与专业的沟通氛围。涉及安全漏洞的报告请直接发送至维护者邮箱，勿公开披露。

## 常见问题

问：导入大量链接时出现超时或内存占用过高，应如何处理？

答：项目默认单次导入最大条目数为 10000 条，若超过此数量建议将文件拆分为多个批次。同时可以在 config/default.yaml 中调整 batch_size 参数控制单次事务提交的记录数，降低内存峰值。对于超大文件，推荐使用 --stream 模式逐行读取而非一次性加载。

问：健康检测结果显示为异常，但手动访问该链接在浏览器中正常，可能是什么原因？

答：检测模块默认使用无头 HTTP 客户端，不执行 JavaScript 和加载外部资源。若目标页面依赖客户端渲染或需要特定 Cookie 才能返回 200 状态码，则检测结果可能误判。解决方案是在配置中为特定域名设置静态 User-Agent 或自定义请求头，或使用 --follow-redirects 参数开启重定向跟踪。

问：Web 管理界面无法启动，提示端口被占用，如何解决？

答：该错误通常由其他进程占用 8080 端口引起。可通过 --port 参数指定其他空闲端口，例如 python app.py --port 9090。若在 Linux 系统中，也可使用 netstat -tulpn | grep 8080 查找占用进程并终止。

## 许可证

MIT

> 外链数量: 250 | 生成时间: 2026-08-24 23:40:21
