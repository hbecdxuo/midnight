# WAPLink Archive

WAPLink Archive 是一个面向移动端网页资源的高效外链管理与归档系统。该项目旨在为开发者、内容聚合者以及历史网页研究者提供一套标准化的 URL 采集、分类、存储与检索方案。通过规范化的数据入口和轻量级的架构设计，WAPLink Archive 能够处理大规模分散链接，特别适用于处理来自内容分发网络（CDN）或旧版移动门户（WAP Portal）的海量数据流。

本项目专注于解决移动互联网时代下短生命周期 URL 的长期保存问题，提供从数据导入、元数据提取到全文索引的完整工具链。目标用户包括数据挖掘工程师、SEO 优化师、数字档案管理员以及需要批量处理动态路由页面的全栈开发者。

## 功能概览

批量 URL 导入解析：支持基于列表的纯文本链接批量注入，自动识别不同层级的动态参数与路由结构，提供基础的去重与格式校验机制。

元数据智能提取：针对特定路径模式（如 /bnews/ 目录）自动匹配内容类型，提取页面标题、发布时间、内容摘要等关键字段，降低人工标注成本。

全文本检索支持：内置轻量级倒排索引引擎，支持对已归档内容进行关键字与短语搜索，并可根据相关性或时间顺序排序。

状态监控与健康检查：定时探测已归档链接的 HTTP 响应状态码（200, 404, 301, 302 等），自动标记失效链接并生成可用性报告。

数据导出与迁移：支持将归档数据导出为 JSON, CSV 以及标准 HTML 目录索引，便于与其他系统（如 CMS 或静态站点生成器）对接。

访问统计与分析：记录每个链接的调用次数与来源 IP 区域分布，提供基于时间粒度的访问趋势折线图数据接口。

权限分级管理：内置管理员、编辑者、访客三级角色控制，支持对敏感链接进行访问白名单配置，适用于多人协作环境。

## 应用场景

移动端历史页面回溯：在移动互联网技术快速迭代的背景下，大量早期 WAP 页面面临访问失效风险。通过 WAPLink Archive，数字档案管理员可批量收录指定域名下的历史路由，构建可供学术研究或法律审计使用的时间快照。

SEO 外链质量审计：SEO 优化师可利用本系统的状态监控模块，定期扫描网站反链池中的存活情况。针对返回 4xx 或 5xx 状态码的链接，系统自动生成清理建议报告，协助维护网站域名权重。

内容聚合源数据清洗：内容聚合平台在采集第三方来源时，常遇到链接格式不统一或参数冗余的问题。项目提供的导入解析器可自定义正则过滤规则，将杂乱的原始 URL 清洗为结构化的标准入口，提升下游数据处理效率。

内部知识库快速部署：企业或技术团队在搭建内部知识导航时，可使用本项目的批量导入功能将分散在邮件、文档或即时通讯记录中的参考链接统一收录，并通过内置检索功能实现团队级信息共享。

## 快速开始

以下命令演示了如何在 Linux 或 macOS 环境下从源码部署 WAPLink Archive 的最小化实例。

```bash
# 克隆项目仓库至本地
git clone https://github.com/waplink/waplink-archive.git

# 进入项目根目录
cd waplink-archive

# 安装 Python 依赖包（建议使用虚拟环境）
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt

# 初始化 SQLite 数据库与索引目录
python manage.py initdb
python manage.py build-index

# 启动内置开发服务器（默认监听 127.0.0.1:5000）
python manage.py runserver
```

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
| :--- | :--- | :--- |
| Python | 3.8 及以上 | 核心运行环境，用于解释执行后端逻辑与 CLI 命令。 |
| SQLite3 | 3.31.0 及以上 | 默认嵌入式关系型数据库，用于存储链接元数据与索引映射。 |
| Redis | 6.0 及以上 | 可选缓存中间件，用于提升高频查询场景下的响应速度。 |
| Node.js | 14.0 及以上 | 仅用于前端资源构建（如静态文件压缩与打包），非运行时必需。 |
| Nginx | 1.18 及以上 | 生产环境推荐的反向代理服务器，用于处理静态资源与负载均衡。 |
| Git | 2.25 及以上 | 版本控制工具，用于克隆源码与后续更新同步。 |
| make | 3.81 及以上 | 构建工具，用于自动化执行安装脚本与测试套件。 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
| :--- | :--- | :--- |
| 入门指南 | docs/getting-started.md | 如何快速配置环境并导入第一批链接数据？ |
| 操作手册 | docs/operation/cli-reference.md | 管理端命令行工具（manage.py）包含哪些子命令及其参数？ |
| 开发指南 | docs/development/api-design.md | 后端 API 的路由规范、请求格式与鉴权方式是什么？ |
| 运维部署 | docs/deployment/production-setup.md | 如何配置 Nginx + Gunicorn 实现高并发生产环境部署？ |

## 资源列表

- http://m.wap.uliejh.cn/bnews/3074327.htm
- http://m.wap.uliejh.cn/bnews/7626990.htm
- http://m.wap.uliejh.cn/bnews/568258.htm
- http://m.wap.uliejh.cn/bnews/8668989.htm
- http://m.wap.uliejh.cn/bnews/10849.htm
- http://m.wap.uliejh.cn/bnews/7736984.htm
- http://m.wap.uliejh.cn/bnews/1159116.htm
- http://m.wap.uliejh.cn/bnews/5650.htm
- http://m.wap.uliejh.cn/bnews/18212.htm
- http://m.wap.uliejh.cn/bnews/5045.htm
- http://m.wap.uliejh.cn/bnews/281725.htm
- http://m.wap.uliejh.cn/bnews/8247347.htm
- http://m.wap.uliejh.cn/bnews/6730225.htm
- http://m.wap.uliejh.cn/bnews/775319.htm
- http://m.wap.uliejh.cn/bnews/6111.htm
- http://m.wap.uliejh.cn/bnews/154400.htm
- http://m.wap.uliejh.cn/bnews/80006.htm
- http://m.wap.uliejh.cn/bnews/4828.htm
- http://m.wap.uliejh.cn/bnews/9146.htm
- http://m.wap.uliejh.cn/bnews/33492.htm
- http://m.wap.uliejh.cn/bnews/5630.htm
- http://m.wap.uliejh.cn/bnews/014584.htm
- http://m.wap.uliejh.cn/bnews/60455.htm
- http://m.wap.uliejh.cn/bnews/9943354.htm
- http://m.wap.uliejh.cn/bnews/3131696.htm
- http://m.wap.uliejh.cn/bnews/6077093.htm
- http://m.wap.uliejh.cn/bnews/039826.htm
- http://m.wap.uliejh.cn/bnews/6194.htm
- http://m.wap.uliejh.cn/bnews/74894.htm
- http://m.wap.uliejh.cn/bnews/7648245.htm
- http://m.wap.uliejh.cn/bnews/7288701.htm
- http://m.wap.uliejh.cn/bnews/9991963.htm
- http://m.wap.uliejh.cn/bnews/481621.htm
- http://m.wap.uliejh.cn/bnews/9512.htm
- http://m.wap.uliejh.cn/bnews/655741.htm
- http://m.wap.uliejh.cn/bnews/8097469.htm
- http://m.wap.uliejh.cn/bnews/9263.htm
- http://m.wap.uliejh.cn/bnews/3638.htm
- http://m.wap.uliejh.cn/bnews/1680.htm
- http://m.wap.uliejh.cn/bnews/643316.htm
- http://m.wap.uliejh.cn/bnews/42582.htm
- http://m.wap.uliejh.cn/bnews/9650.htm
- http://m.wap.uliejh.cn/bnews/5830939.htm
- http://m.wap.uliejh.cn/bnews/4269427.htm
- http://m.wap.uliejh.cn/bnews/58510.htm
- http://m.wap.uliejh.cn/bnews/451237.htm
- http://m.wap.uliejh.cn/bnews/62333.htm
- http://m.wap.uliejh.cn/bnews/0244043.htm
- http://m.wap.uliejh.cn/bnews/5249130.htm
- http://m.wap.uliejh.cn/bnews/700009.htm
- http://m.wap.uliejh.cn/bnews/779792.htm
- http://m.wap.uliejh.cn/bnews/7540849.htm
- http://m.wap.uliejh.cn/bnews/62772.htm
- http://m.wap.uliejh.cn/bnews/716466.htm
- http://m.wap.uliejh.cn/bnews/480952.htm
- http://m.wap.uliejh.cn/bnews/3128092.htm
- http://m.wap.uliejh.cn/bnews/6360.htm
- http://m.wap.uliejh.cn/bnews/8838516.htm
- http://m.wap.uliejh.cn/bnews/2981241.htm
- http://m.wap.uliejh.cn/bnews/702891.htm
- http://m.wap.uliejh.cn/bnews/310979.htm
- http://m.wap.uliejh.cn/bnews/553018.htm
- http://m.wap.uliejh.cn/bnews/895431.htm
- http://m.wap.uliejh.cn/bnews/13323.htm
- http://m.wap.uliejh.cn/bnews/7043708.htm
- http://m.wap.uliejh.cn/bnews/1094.htm
- http://m.wap.uliejh.cn/bnews/5353647.htm
- http://m.wap.uliejh.cn/bnews/635479.htm
- http://m.wap.uliejh.cn/bnews/215489.htm
- http://m.wap.uliejh.cn/bnews/4548.htm
- http://m.wap.uliejh.cn/bnews/36070.htm
- http://m.wap.uliejh.cn/bnews/88641.htm
- http://m.wap.uliejh.cn/bnews/220905.htm
- http://m.wap.uliejh.cn/bnews/956593.htm
- http://m.wap.uliejh.cn/bnews/54149.htm
- http://m.wap.uliejh.cn/bnews/5920.htm
- http://m.wap.uliejh.cn/bnews/085735.htm
- http://m.wap.uliejh.cn/bnews/95290.htm
- http://m.wap.uliejh.cn/bnews/099509.htm
- http://m.wap.uliejh.cn/bnews/1414825.htm
- http://m.wap.uliejh.cn/bnews/31234.htm
- http://m.wap.uliejh.cn/bnews/0211.htm
- http://m.wap.uliejh.cn/bnews/6934.htm
- http://m.wap.uliejh.cn/bnews/6136.htm
- http://m.wap.uliejh.cn/bnews/974992.htm
- http://m.wap.uliejh.cn/bnews/63804.htm
- http://m.wap.uliejh.cn/bnews/5495.htm
- http://m.wap.uliejh.cn/bnews/9713.htm
- http://m.wap.uliejh.cn/bnews/51345.htm
- http://m.wap.uliejh.cn/bnews/7303519.htm
- http://m.wap.uliejh.cn/bnews/2875.htm
- http://m.wap.uliejh.cn/bnews/42988.htm
- http://m.wap.uliejh.cn/bnews/747839.htm
- http://m.wap.uliejh.cn/bnews/1626.htm
- http://m.wap.uliejh.cn/bnews/35071.htm
- http://m.wap.uliejh.cn/bnews/9663.htm
- http://m.wap.uliejh.cn/bnews/5821345.htm
- http://m.wap.uliejh.cn/bnews/0676633.htm
- http://m.wap.uliejh.cn/bnews/3310.htm
- http://m.wap.uliejh.cn/bnews/535849.htm
- http://m.wap.uliejh.cn/bnews/39062.htm
- http://m.wap.uliejh.cn/bnews/4506.htm
- http://m.wap.uliejh.cn/bnews/9509.htm
- http://m.wap.uliejh.cn/bnews/86336.htm
- http://m.wap.uliejh.cn/bnews/53517.htm
- http://m.wap.uliejh.cn/bnews/041422.htm
- http://m.wap.uliejh.cn/bnews/6839767.htm
- http://m.wap.uliejh.cn/bnews/6358457.htm
- http://m.wap.uliejh.cn/bnews/7905243.htm
- http://m.wap.uliejh.cn/bnews/73028.htm
- http://m.wap.uliejh.cn/bnews/4403.htm
- http://m.wap.uliejh.cn/bnews/6992287.htm
- http://m.wap.uliejh.cn/bnews/6108614.htm
- http://m.wap.uliejh.cn/bnews/931321.htm
- http://m.wap.uliejh.cn/bnews/49318.htm
- http://m.wap.uliejh.cn/bnews/149345.htm
- http://m.wap.uliejh.cn/bnews/3782.htm
- http://m.wap.uliejh.cn/bnews/05667.htm
- http://m.wap.uliejh.cn/bnews/843378.htm
- http://m.wap.uliejh.cn/bnews/1643474.htm
- http://m.wap.uliejh.cn/bnews/0698.htm
- http://m.wap.uliejh.cn/bnews/4064610.htm
- http://m.wap.uliejh.cn/bnews/6066.htm
- http://m.wap.uliejh.cn/bnews/2290.htm
- http://m.wap.uliejh.cn/bnews/5892.htm
- http://m.wap.uliejh.cn/bnews/2463.htm
- http://m.wap.uliejh.cn/bnews/2778.htm
- http://m.wap.uliejh.cn/bnews/1476210.htm
- http://m.wap.uliejh.cn/bnews/5989176.htm
- http://m.wap.uliejh.cn/bnews/0517.htm
- http://m.wap.uliejh.cn/bnews/620923.htm
- http://m.wap.uliejh.cn/bnews/42666.htm
- http://m.wap.uliejh.cn/bnews/0996310.htm
- http://m.wap.uliejh.cn/bnews/326108.htm
- http://m.wap.uliejh.cn/bnews/28378.htm
- http://m.wap.uliejh.cn/bnews/4090.htm
- http://m.wap.uliejh.cn/bnews/2252062.htm
- http://m.wap.uliejh.cn/bnews/6204.htm
- http://m.wap.uliejh.cn/bnews/16865.htm
- http://m.wap.uliejh.cn/bnews/041922.htm
- http://m.wap.uliejh.cn/bnews/243844.htm
- http://m.wap.uliejh.cn/bnews/939853.htm
- http://m.wap.uliejh.cn/bnews/5640.htm
- http://m.wap.uliejh.cn/bnews/1136463.htm
- http://m.wap.uliejh.cn/bnews/3452.htm
- http://m.wap.uliejh.cn/bnews/297716.htm
- http://m.wap.uliejh.cn/bnews/259080.htm
- http://m.wap.uliejh.cn/bnews/96071.htm
- http://m.wap.uliejh.cn/bnews/3472820.htm
- http://m.wap.uliejh.cn/bnews/43231.htm
- http://m.wap.uliejh.cn/bnews/50949.htm
- http://m.wap.uliejh.cn/bnews/69751.htm
- http://m.wap.uliejh.cn/bnews/3337205.htm
- http://m.wap.uliejh.cn/bnews/69945.htm
- http://m.wap.uliejh.cn/bnews/5908.htm
- http://m.wap.uliejh.cn/bnews/8608892.htm
- http://m.wap.uliejh.cn/bnews/376521.htm
- http://m.wap.uliejh.cn/bnews/8177.htm
- http://m.wap.uliejh.cn/bnews/47153.htm
- http://m.wap.uliejh.cn/bnews/3492.htm
- http://m.wap.uliejh.cn/bnews/9726112.htm
- http://m.wap.uliejh.cn/bnews/900257.htm
- http://m.wap.uliejh.cn/bnews/69838.htm
- http://m.wap.uliejh.cn/bnews/3540.htm
- http://m.wap.uliejh.cn/bnews/614111.htm
- http://m.wap.uliejh.cn/bnews/7130462.htm
- http://m.wap.uliejh.cn/bnews/7177311.htm
- http://m.wap.uliejh.cn/bnews/0323596.htm
- http://m.wap.uliejh.cn/bnews/6577.htm
- http://m.wap.uliejh.cn/bnews/3324188.htm
- http://m.wap.uliejh.cn/bnews/10175.htm
- http://m.wap.uliejh.cn/bnews/71666.htm
- http://m.wap.uliejh.cn/bnews/80945.htm
- http://m.wap.uliejh.cn/bnews/4093.htm
- http://m.wap.uliejh.cn/bnews/3869.htm
- http://m.wap.uliejh.cn/bnews/9908027.htm
- http://m.wap.uliejh.cn/bnews/617613.htm
- http://m.wap.uliejh.cn/bnews/94386.htm
- http://m.wap.uliejh.cn/bnews/173342.htm
- http://m.wap.uliejh.cn/bnews/99874.htm
- http://m.wap.uliejh.cn/bnews/0916.htm
- http://m.wap.uliejh.cn/bnews/30035.htm
- http://m.wap.uliejh.cn/bnews/7645.htm
- http://m.wap.uliejh.cn/bnews/2369782.htm
- http://m.wap.uliejh.cn/bnews/620828.htm
- http://m.wap.uliejh.cn/bnews/142187.htm
- http://m.wap.uliejh.cn/bnews/0498169.htm
- http://m.wap.uliejh.cn/bnews/7611.htm
- http://m.wap.uliejh.cn/bnews/7057184.htm
- http://m.wap.uliejh.cn/bnews/40926.htm
- http://m.wap.uliejh.cn/bnews/242316.htm
- http://m.wap.uliejh.cn/bnews/204512.htm
- http://m.wap.uliejh.cn/bnews/39753.htm
- http://m.wap.uliejh.cn/bnews/8878842.htm
- http://m.wap.uliejh.cn/bnews/2312.htm
- http://m.wap.uliejh.cn/bnews/087044.htm
- http://m.wap.uliejh.cn/bnews/8981.htm
- http://m.wap.uliejh.cn/bnews/17639.htm
- http://m.wap.uliejh.cn/bnews/968645.htm
- http://m.wap.uliejh.cn/bnews/80588.htm
- http://m.wap.uliejh.cn/bnews/3469510.htm
- http://m.wap.uliejh.cn/bnews/3314878.htm
- http://m.wap.uliejh.cn/bnews/8830422.htm
- http://m.wap.uliejh.cn/bnews/4553.htm
- http://m.wap.uliejh.cn/bnews/50263.htm
- http://m.wap.uliejh.cn/bnews/6717308.htm
- http://m.wap.uliejh.cn/bnews/6790035.htm
- http://m.wap.uliejh.cn/bnews/8089879.htm
- http://m.wap.uliejh.cn/bnews/00564.htm
- http://m.wap.uliejh.cn/bnews/572741.htm
- http://m.wap.uliejh.cn/bnews/376690.htm
- http://m.wap.uliejh.cn/bnews/7756377.htm
- http://m.wap.uliejh.cn/bnews/440094.htm
- http://m.wap.uliejh.cn/bnews/08537.htm
- http://m.wap.uliejh.cn/bnews/47039.htm
- http://m.wap.uliejh.cn/bnews/013291.htm
- http://m.wap.uliejh.cn/bnews/025073.htm
- http://m.wap.uliejh.cn/bnews/9113.htm
- http://m.wap.uliejh.cn/bnews/2664.htm
- http://m.wap.uliejh.cn/bnews/6170.htm
- http://m.wap.uliejh.cn/bnews/2029180.htm
- http://m.wap.uliejh.cn/bnews/6623326.htm
- http://m.wap.uliejh.cn/bnews/7890310.htm
- http://m.wap.uliejh.cn/bnews/99566.htm
- http://m.wap.uliejh.cn/bnews/2351864.htm
- http://m.wap.uliejh.cn/bnews/2057.htm
- http://m.wap.uliejh.cn/bnews/68753.htm
- http://m.wap.uliejh.cn/bnews/198435.htm
- http://m.wap.uliejh.cn/bnews/106785.htm
- http://m.wap.uliejh.cn/bnews/0500738.htm
- http://m.wap.uliejh.cn/bnews/81801.htm
- http://m.wap.uliejh.cn/bnews/23615.htm
- http://m.wap.uliejh.cn/bnews/77827.htm
- http://m.wap.uliejh.cn/bnews/68332.htm
- http://m.wap.uliejh.cn/bnews/9562484.htm
- http://m.wap.uliejh.cn/bnews/650360.htm
- http://m.wap.uliejh.cn/bnews/90041.htm
- http://m.wap.uliejh.cn/bnews/20948.htm
- http://m.wap.uliejh.cn/bnews/0110771.htm
- http://m.wap.uliejh.cn/bnews/73674.htm
- http://m.wap.uliejh.cn/bnews/90045.htm
- http://m.wap.uliejh.cn/bnews/81780.htm
- http://m.wap.uliejh.cn/bnews/7890488.htm
- http://m.wap.uliejh.cn/bnews/84679.htm
- http://m.wap.uliejh.cn/bnews/18519.htm
- http://m.wap.uliejh.cn/bnews/2102230.htm
- http://m.wap.uliejh.cn/bnews/1685922.htm
- http://m.wap.uliejh.cn/bnews/02978.htm
- http://m.wap.uliejh.cn/bnews/55369.htm
- http://m.wap.uliejh.cn/bnews/0341914.htm

## 项目结构

```text
waplink-archive/
├── manage.py                 # 项目入口控制脚本，集成数据库迁移、索引构建与服务启动命令
├── requirements.txt          # Python 依赖清单，包含 Flask, requests, lxml 等核心库
├── config/
│   ├── settings.py           # 应用配置（调试模式、密钥、数据库连接字符串）
│   └── logging.conf          # 日志分级输出配置（文件轮转与控制台打印格式）
├── core/                     # 核心业务逻辑层
│   ├── importer.py           # 批量 URL 解析与入库模块，支持 CSV 与纯文本列表格式
│   ├── indexer.py            # 基于 whoosh 的全文索引构建与更新实现
│   ├── monitor.py            # 异步 HTTP 状态探测与告警触发器
│   └── exporter.py           # 数据导出为 JSON/HTML 目录结构的序列化器
├── web/                      # Web 交互层
│   ├── routes/               # Flask 路由蓝图（首页、检索、详情、管理后台）
│   ├── static/               # 编译后的 CSS/JavaScript 静态资源
│   └── templates/            # Jinja2 渲染模板（列表页、详情页、错误页）
├── tests/                    # 单元测试与集成测试用例
│   ├── test_importer.py
│   ├── test_monitor.py
│   └── fixtures/             # 测试用的模拟数据样本
├── scripts/                  # 运维辅助脚本
│   ├── clean_cache.sh        # 清理过期 Redis 缓存键的定时任务脚本
│   └── backup_db.sh          # SQLite 数据库热备脚本（配合 crontab 使用）
└── docs/                     # 项目文档源码
    ├── getting-started.md
    ├── operation/
    └── development/
```

## 贡献指南

我们欢迎任何形式的贡献，包括但不限于功能建议、代码修复、文档完善与测试用例补充。请遵循以下流程以保证协作效率：

1. 问题跟踪与讨论：在提交拉取请求之前，请先在 Issues 列表中搜索是否已有相关讨论。若无，请新建一个 Issue 详细描述您发现的问题或希望新增的功能，并等待核心维护者的反馈。

2. 分叉仓库与开发分支：将主仓库分叉至您的个人账户下，并基于 main 分支创建一个具有描述性的新分支（例如 feature/add-json-export 或 fix/monitor-timeout）。

3. 代码规范与测试：确保您的代码符合 PEP 8 编码规范。新增功能必须包含对应的单元测试，且所有现有测试套件需在本地通过（执行 python -m pytest）。

4. 提交拉取请求：推送您的本地分支至远程分叉仓库，然后向主仓库的 main 分支发起拉取请求。请求描述中需清晰关联对应的 Issue 编号，并列出主要变更点。

5. 代码审查与合并：核心维护者将在 48 小时内审查您的提交。若审查通过，您的代码将被合并；若需要修改，您将收到具体的调整建议。合并后的代码将随下一个版本号一同发布。

## 常见问题

问：项目启动时报错 "No module named 'whoosh'" 如何解决？

答：该错误表示全文索引依赖库未正确安装。请确认您已激活虚拟环境，并执行 pip install -r requirements.txt 重新安装所有依赖。若网络环境较差，可尝试使用国内镜像源（如 pip install -i https://pypi.tuna.tsinghua.edu.cn/simple whoosh）。

问：导入大量链接时页面响应变慢甚至超时，应如何优化？

答：导入操作属于 CPU 与 I/O 密集型任务，默认使用同步阻塞模式不适合处理大批量数据。建议在命令行下使用 manage.py import --batch-size 1000 --file links.txt 进行后台导入。同时，可调整 config/settings.py 中的 POOL_SIZE 参数增加数据库连接池容量。

问：如何升级到最新版本并保留现有数据？

答：首先使用 git pull 拉取最新源码。随后执行 python manage.py db-upgrade 自动执行数据库迁移脚本。请务必在执行升级前备份 data/ 目录下的 waplink.db 文件。若迁移过程中遇到冲突，请参照 docs/operation/upgrade-guide.md 中的手动处理步骤。

## 许可证

MIT

> 外链数量: 250 | 生成时间: 2026-08-24 23:40:21
