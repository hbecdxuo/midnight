# LinkVault 外链资源聚合系统

LinkVault 是一个面向技术内容创作者、SEO 分析师和站点运营人员的外链资源聚合与管理平台。该项目专注于对分散的移动端新闻及资讯类链接进行结构化采集、分类存储与快速检索，帮助用户从大量原始 URL 中提取有价值的引用来源、内容线索与站点拓扑关系。LinkVault 并非一个通用爬虫或浏览器工具，而是一个针对特定数据源格式（如 uliejh.cn 下的 bnews 路径模式）设计的轻量化外链治理方案，适用于需要定期跟踪、导出和审计外部链接的技术团队。

## 功能概览

- 批量链接导入与自动规范化：支持从文本文件、CSV 或直接粘贴的原始 URL 列表中批量导入链接，自动识别协议、主机与路径结构，对不符合规范的条目进行告警提示。

- 多维度标签与分类引擎：允许用户为每条链接添加自定义标签（如“科技”、“财经”、“移动端”），并基于 URL 路径中的数字 ID 段、来源域名和文件扩展名自动生成推荐分类。

- 链接状态健康检查：内置异步 HTTP 头检测模块，定期探测链接的可访问性、响应时间与状态码变化，标记失效或重定向链接。

- 全文元数据提取：对可访问的目标页面提取标题、描述、关键词和正文首段文本，生成内容摘要索引，支持后续关键词检索。

- 外链关系图谱可视化：基于链接来源与目标域名的共现关系，生成简单的有向图数据输出，便于分析站群结构或内容引用网络。

- 定时任务与报告生成：支持每日、每周或自定义周期的链接状态报告，以 Markdown 或 JSON 格式输出新增、失效和变更链接清单。

- 只读 API 接口：提供基于 REST 风格的查询接口，允许外部系统按标签、状态、时间范围等条件获取链接列表，方便集成到更庞大的数据流水线中。

## 应用场景

技术博客与内容站点运营：技术博客作者在撰写聚合类或“每周资讯”文章时，可通过 LinkVault 集中管理备选外链，快速筛选出响应正常、内容相关的来源，避免手动整理大量散乱 URL。

SEO 外链质量审计：SEO 顾问或站点管理员定期导入网站外部链接数据，利用 LinkVault 的状态检查功能识别失效外链、降权站点或不稳定的引用源，从而调整外链策略。

移动端资讯数据采集前置处理：数据采集工程师在启动大规模抓取任务前，使用 LinkVault 清洗和验证目标 URL 列表，剔除明显不可达或格式错误的条目，减少采集任务的无效请求开销。

历史链接归档与检索：研究机构或内容档案馆人员可将历史新闻链接导入系统，利用元数据提取功能建立可检索的摘要库，即使原始页面后续发生变更，仍保留采集时的内容快照信息。

## 快速开始

以下步骤帮助您在本地环境中快速启动 LinkVault 服务。

```bash
# 克隆项目仓库
git clone https://github.com/your-org/linkvault.git

# 进入项目目录
cd linkvault

# 安装 Python 依赖（推荐使用虚拟环境）
python3 -m venv venv
source venv/bin/activate  # Windows 下使用 venv\Scripts\activate
pip install -r requirements.txt

# 初始化 SQLite 数据库
python scripts/init_db.py

# 启动开发服务器
python app.py --host 127.0.0.1 --port 8080
```

启动成功后，可通过浏览器访问 `http://127.0.0.1:8080` 进入 Web 管理界面，或通过 API 端点 `http://127.0.0.1:8080/api/v1/links` 进行程序化调用。

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|---------|---------|------|
| Python | 3.8 及以上 | 核心运行环境，推荐 3.10 或 3.11 |
| SQLite | 3.28 及以上 | 默认内置数据库，用于存储链接元数据和状态 |
| requests | 2.28.0 及以上 | HTTP 请求库，用于链接健康检查和元数据提取 |
| beautifulsoup4 | 4.11.0 及以上 | HTML 解析库，用于提取目标页面的标题与描述 |
| flask | 2.2.0 及以上 | Web 框架，提供管理界面和 REST API |
| flask-cors | 3.0.10 及以上 | 跨域资源共享支持，便于 API 被前端或第三方调用 |
| apscheduler | 3.9.0 及以上 | 定时任务调度器，用于周期性链接状态检查 |
| pandas | 1.5.0 及以上 | 数据分析工具，用于导出报告和数据汇总（可选） |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|------|------|----------|
| 用户手册 | docs/user-guide.md | 如何批量导入链接、如何设置标签、如何查看健康状态报告 |
| API 参考 | docs/api-reference.md | 各接口的请求参数、返回格式、鉴权方式与错误码说明 |
| 部署指南 | docs/deployment.md | 如何将 LinkVault 部署到生产服务器，包括 Nginx 代理与 systemd 配置 |
| 内部设计 | docs/architecture.md | 数据库表结构设计、定时任务调度机制、元数据提取流程 |

## 资源列表

- http://m.wap.uliejh.cn/bnews/7021203.htm
- http://m.wap.uliejh.cn/bnews/5177292.htm
- http://m.wap.uliejh.cn/bnews/1449665.htm
- http://m.wap.uliejh.cn/bnews/139606.htm
- http://m.wap.uliejh.cn/bnews/2524000.htm
- http://m.wap.uliejh.cn/bnews/997770.htm
- http://m.wap.uliejh.cn/bnews/3585.htm
- http://m.wap.uliejh.cn/bnews/257649.htm
- http://m.wap.uliejh.cn/bnews/3568757.htm
- http://m.wap.uliejh.cn/bnews/303576.htm
- http://m.wap.uliejh.cn/bnews/7137.htm
- http://m.wap.uliejh.cn/bnews/8916.htm
- http://m.wap.uliejh.cn/bnews/9264.htm
- http://m.wap.uliejh.cn/bnews/8092312.htm
- http://m.wap.uliejh.cn/bnews/7561716.htm
- http://m.wap.uliejh.cn/bnews/15991.htm
- http://m.wap.uliejh.cn/bnews/1438742.htm
- http://m.wap.uliejh.cn/bnews/0070.htm
- http://m.wap.uliejh.cn/bnews/20569.htm
- http://m.wap.uliejh.cn/bnews/343532.htm
- http://m.wap.uliejh.cn/bnews/7954.htm
- http://m.wap.uliejh.cn/bnews/3603508.htm
- http://m.wap.uliejh.cn/bnews/2099973.htm
- http://m.wap.uliejh.cn/bnews/2479141.htm
- http://m.wap.uliejh.cn/bnews/59319.htm
- http://m.wap.uliejh.cn/bnews/298579.htm
- http://m.wap.uliejh.cn/bnews/25652.htm
- http://m.wap.uliejh.cn/bnews/4492681.htm
- http://m.wap.uliejh.cn/bnews/8447889.htm
- http://m.wap.uliejh.cn/bnews/927644.htm
- http://m.wap.uliejh.cn/bnews/7507.htm
- http://m.wap.uliejh.cn/bnews/56536.htm
- http://m.wap.uliejh.cn/bnews/65496.htm
- http://m.wap.uliejh.cn/bnews/5541751.htm
- http://m.wap.uliejh.cn/bnews/02600.htm
- http://m.wap.uliejh.cn/bnews/02460.htm
- http://m.wap.uliejh.cn/bnews/624193.htm
- http://m.wap.uliejh.cn/bnews/9091.htm
- http://m.wap.uliejh.cn/bnews/96435.htm
- http://m.wap.uliejh.cn/bnews/489798.htm
- http://m.wap.uliejh.cn/bnews/78564.htm
- http://m.wap.uliejh.cn/bnews/89439.htm
- http://m.wap.uliejh.cn/bnews/3272.htm
- http://m.wap.uliejh.cn/bnews/569291.htm
- http://m.wap.uliejh.cn/bnews/5231295.htm
- http://m.wap.uliejh.cn/bnews/670595.htm
- http://m.wap.uliejh.cn/bnews/0299115.htm
- http://m.wap.uliejh.cn/bnews/3386.htm
- http://m.wap.uliejh.cn/bnews/411632.htm
- http://m.wap.uliejh.cn/bnews/308608.htm
- http://m.wap.uliejh.cn/bnews/4257418.htm
- http://m.wap.uliejh.cn/bnews/18814.htm
- http://m.wap.uliejh.cn/bnews/5312629.htm
- http://m.wap.uliejh.cn/bnews/2541.htm
- http://m.wap.uliejh.cn/bnews/09630.htm
- http://m.wap.uliejh.cn/bnews/313591.htm
- http://m.wap.uliejh.cn/bnews/3192.htm
- http://m.wap.uliejh.cn/bnews/896746.htm
- http://m.wap.uliejh.cn/bnews/9388.htm
- http://m.wap.uliejh.cn/bnews/996837.htm
- http://m.wap.uliejh.cn/bnews/2814.htm
- http://m.wap.uliejh.cn/bnews/9380.htm
- http://m.wap.uliejh.cn/bnews/8897.htm
- http://m.wap.uliejh.cn/bnews/9114957.htm
- http://m.wap.uliejh.cn/bnews/73844.htm
- http://m.wap.uliejh.cn/bnews/217137.htm
- http://m.wap.uliejh.cn/bnews/6890851.htm
- http://m.wap.uliejh.cn/bnews/6963.htm
- http://m.wap.uliejh.cn/bnews/793621.htm
- http://m.wap.uliejh.cn/bnews/0690872.htm
- http://m.wap.uliejh.cn/bnews/4076.htm
- http://m.wap.uliejh.cn/bnews/1913672.htm
- http://m.wap.uliejh.cn/bnews/354249.htm
- http://m.wap.uliejh.cn/bnews/194005.htm
- http://m.wap.uliejh.cn/bnews/2181.htm
- http://m.wap.uliejh.cn/bnews/40921.htm
- http://m.wap.uliejh.cn/bnews/71708.htm
- http://m.wap.uliejh.cn/bnews/4545844.htm
- http://m.wap.uliejh.cn/bnews/07038.htm
- http://m.wap.uliejh.cn/bnews/2429534.htm
- http://m.wap.uliejh.cn/bnews/5069.htm
- http://m.wap.uliejh.cn/bnews/09512.htm
- http://m.wap.uliejh.cn/bnews/32083.htm
- http://m.wap.uliejh.cn/bnews/759594.htm
- http://m.wap.uliejh.cn/bnews/243706.htm
- http://m.wap.uliejh.cn/bnews/26278.htm
- http://m.wap.uliejh.cn/bnews/84549.htm
- http://m.wap.uliejh.cn/bnews/352133.htm
- http://m.wap.uliejh.cn/bnews/891689.htm
- http://m.wap.uliejh.cn/bnews/0630148.htm
- http://m.wap.uliejh.cn/bnews/484830.htm
- http://m.wap.uliejh.cn/bnews/9552.htm
- http://m.wap.uliejh.cn/bnews/88628.htm
- http://m.wap.uliejh.cn/bnews/76704.htm
- http://m.wap.uliejh.cn/bnews/966550.htm
- http://m.wap.uliejh.cn/bnews/0809498.htm
- http://m.wap.uliejh.cn/bnews/91485.htm
- http://m.wap.uliejh.cn/bnews/79881.htm
- http://m.wap.uliejh.cn/bnews/23110.htm
- http://m.wap.uliejh.cn/bnews/47499.htm
- http://m.wap.uliejh.cn/bnews/98520.htm
- http://m.wap.uliejh.cn/bnews/8290599.htm
- http://m.wap.uliejh.cn/bnews/2270.htm
- http://m.wap.uliejh.cn/bnews/90162.htm
- http://m.wap.uliejh.cn/bnews/90717.htm
- http://m.wap.uliejh.cn/bnews/3949.htm
- http://m.wap.uliejh.cn/bnews/2840317.htm
- http://m.wap.uliejh.cn/bnews/7556.htm
- http://m.wap.uliejh.cn/bnews/492814.htm
- http://m.wap.uliejh.cn/bnews/4221654.htm
- http://m.wap.uliejh.cn/bnews/0581795.htm
- http://m.wap.uliejh.cn/bnews/1713.htm
- http://m.wap.uliejh.cn/bnews/0431284.htm
- http://m.wap.uliejh.cn/bnews/0685.htm
- http://m.wap.uliejh.cn/bnews/1929.htm
- http://m.wap.uliejh.cn/bnews/8457063.htm
- http://m.wap.uliejh.cn/bnews/29819.htm
- http://m.wap.uliejh.cn/bnews/6055.htm
- http://m.wap.uliejh.cn/bnews/22609.htm
- http://m.wap.uliejh.cn/bnews/509691.htm
- http://m.wap.uliejh.cn/bnews/31462.htm
- http://m.wap.uliejh.cn/bnews/11812.htm
- http://m.wap.uliejh.cn/bnews/3172.htm
- http://m.wap.uliejh.cn/bnews/151953.htm
- http://m.wap.uliejh.cn/bnews/5949606.htm
- http://m.wap.uliejh.cn/bnews/424621.htm
- http://m.wap.uliejh.cn/bnews/5198.htm
- http://m.wap.uliejh.cn/bnews/29809.htm
- http://m.wap.uliejh.cn/bnews/0593.htm
- http://m.wap.uliejh.cn/bnews/25371.htm
- http://m.wap.uliejh.cn/bnews/8713.htm
- http://m.wap.uliejh.cn/bnews/63860.htm
- http://m.wap.uliejh.cn/bnews/67248.htm
- http://m.wap.uliejh.cn/bnews/25632.htm
- http://m.wap.uliejh.cn/bnews/49055.htm
- http://m.wap.uliejh.cn/bnews/1462.htm
- http://m.wap.uliejh.cn/bnews/0792452.htm
- http://m.wap.uliejh.cn/bnews/2039.htm
- http://m.wap.uliejh.cn/bnews/15425.htm
- http://m.wap.uliejh.cn/bnews/20702.htm
- http://m.wap.uliejh.cn/bnews/01813.htm
- http://m.wap.uliejh.cn/bnews/9291252.htm
- http://m.wap.uliejh.cn/bnews/18185.htm
- http://m.wap.uliejh.cn/bnews/04867.htm
- http://m.wap.uliejh.cn/bnews/2299.htm
- http://m.wap.uliejh.cn/bnews/0582.htm
- http://m.wap.uliejh.cn/bnews/70470.htm
- http://m.wap.uliejh.cn/bnews/563025.htm
- http://m.wap.uliejh.cn/bnews/3546548.htm
- http://m.wap.uliejh.cn/bnews/489115.htm
- http://m.wap.uliejh.cn/bnews/3664.htm
- http://m.wap.uliejh.cn/bnews/74757.htm
- http://m.wap.uliejh.cn/bnews/76319.htm
- http://m.wap.uliejh.cn/bnews/81413.htm
- http://m.wap.uliejh.cn/bnews/847728.htm
- http://m.wap.uliejh.cn/bnews/8458554.htm
- http://m.wap.uliejh.cn/bnews/42252.htm
- http://m.wap.uliejh.cn/bnews/351649.htm
- http://m.wap.uliejh.cn/bnews/87761.htm
- http://m.wap.uliejh.cn/bnews/19955.htm
- http://m.wap.uliejh.cn/bnews/9383441.htm
- http://m.wap.uliejh.cn/bnews/5034.htm
- http://m.wap.uliejh.cn/bnews/44227.htm
- http://m.wap.uliejh.cn/bnews/5746280.htm
- http://m.wap.uliejh.cn/bnews/01630.htm
- http://m.wap.uliejh.cn/bnews/1108079.htm
- http://m.wap.uliejh.cn/bnews/50300.htm
- http://m.wap.uliejh.cn/bnews/2158.htm
- http://m.wap.uliejh.cn/bnews/063290.htm
- http://m.wap.uliejh.cn/bnews/4562.htm
- http://m.wap.uliejh.cn/bnews/78935.htm
- http://m.wap.uliejh.cn/bnews/17546.htm
- http://m.wap.uliejh.cn/bnews/99430.htm
- http://m.wap.uliejh.cn/bnews/54676.htm
- http://m.wap.uliejh.cn/bnews/3842.htm
- http://m.wap.uliejh.cn/bnews/4148.htm
- http://m.wap.uliejh.cn/bnews/7336537.htm
- http://m.wap.uliejh.cn/bnews/0816.htm
- http://m.wap.uliejh.cn/bnews/130796.htm
- http://m.wap.uliejh.cn/bnews/81623.htm
- http://m.wap.uliejh.cn/bnews/51381.htm
- http://m.wap.uliejh.cn/bnews/1247.htm
- http://m.wap.uliejh.cn/bnews/07466.htm
- http://m.wap.uliejh.cn/bnews/7782677.htm
- http://m.wap.uliejh.cn/bnews/39570.htm
- http://m.wap.uliejh.cn/bnews/866669.htm
- http://m.wap.uliejh.cn/bnews/4224747.htm
- http://m.wap.uliejh.cn/bnews/2709.htm
- http://m.wap.uliejh.cn/bnews/58132.htm
- http://m.wap.uliejh.cn/bnews/42452.htm
- http://m.wap.uliejh.cn/bnews/1041838.htm
- http://m.wap.uliejh.cn/bnews/4526.htm
- http://m.wap.uliejh.cn/bnews/072355.htm
- http://m.wap.uliejh.cn/bnews/17380.htm
- http://m.wap.uliejh.cn/bnews/233025.htm
- http://m.wap.uliejh.cn/bnews/0742566.htm
- http://m.wap.uliejh.cn/bnews/04346.htm
- http://m.wap.uliejh.cn/bnews/40550.htm
- http://m.wap.uliejh.cn/bnews/673424.htm
- http://m.wap.uliejh.cn/bnews/30238.htm
- http://m.wap.uliejh.cn/bnews/751242.htm
- http://m.wap.uliejh.cn/bnews/3400.htm
- http://m.wap.uliejh.cn/bnews/24000.htm
- http://m.wap.uliejh.cn/bnews/64709.htm
- http://m.wap.uliejh.cn/bnews/1098.htm
- http://m.wap.uliejh.cn/bnews/3636.htm
- http://m.wap.uliejh.cn/bnews/53845.htm
- http://m.wap.uliejh.cn/bnews/44150.htm
- http://m.wap.uliejh.cn/bnews/1660497.htm
- http://m.wap.uliejh.cn/bnews/424913.htm
- http://m.wap.uliejh.cn/bnews/15714.htm
- http://m.wap.uliejh.cn/bnews/1040.htm
- http://m.wap.uliejh.cn/bnews/1851092.htm
- http://m.wap.uliejh.cn/bnews/9859.htm
- http://m.wap.uliejh.cn/bnews/10530.htm
- http://m.wap.uliejh.cn/bnews/1412.htm
- http://m.wap.uliejh.cn/bnews/7165438.htm
- http://m.wap.uliejh.cn/bnews/695122.htm
- http://m.wap.uliejh.cn/bnews/09938.htm
- http://m.wap.uliejh.cn/bnews/7517496.htm
- http://m.wap.uliejh.cn/bnews/8064.htm
- http://m.wap.uliejh.cn/bnews/63054.htm
- http://m.wap.uliejh.cn/bnews/091700.htm
- http://m.wap.uliejh.cn/bnews/6404249.htm
- http://m.wap.uliejh.cn/bnews/8696.htm
- http://m.wap.uliejh.cn/bnews/686636.htm
- http://m.wap.uliejh.cn/bnews/7133196.htm
- http://m.wap.uliejh.cn/bnews/346478.htm
- http://m.wap.uliejh.cn/bnews/4778.htm
- http://m.wap.uliejh.cn/bnews/4705009.htm
- http://m.wap.uliejh.cn/bnews/306200.htm
- http://m.wap.uliejh.cn/bnews/7329.htm
- http://m.wap.uliejh.cn/bnews/29762.htm
- http://m.wap.uliejh.cn/bnews/558492.htm
- http://m.wap.uliejh.cn/bnews/50966.htm
- http://m.wap.uliejh.cn/bnews/9876.htm
- http://m.wap.uliejh.cn/bnews/7478.htm
- http://m.wap.uliejh.cn/bnews/49362.htm
- http://m.wap.uliejh.cn/bnews/5798769.htm
- http://m.wap.uliejh.cn/bnews/23856.htm
- http://m.wap.uliejh.cn/bnews/426882.htm
- http://m.wap.uliejh.cn/bnews/3189.htm
- http://m.wap.uliejh.cn/bnews/63972.htm
- http://m.wap.uliejh.cn/bnews/4559945.htm
- http://m.wap.uliejh.cn/bnews/439294.htm
- http://m.wap.uliejh.cn/bnews/4175268.htm
- http://m.wap.uliejh.cn/bnews/3351.htm
- http://m.wap.uliejh.cn/bnews/118312.htm
- http://m.wap.uliejh.cn/bnews/6246.htm
- http://m.wap.uliejh.cn/bnews/314735.htm

## 项目结构

```
linkvault/
├── app.py                         # Flask 应用主入口，注册路由与初始化扩展
├── config.py                      # 配置管理模块，包含数据库路径、调度间隔、日志级别
├── requirements.txt               # Python 依赖清单，锁定所有第三方库版本
├── scripts/
│   ├── init_db.py                 # 初始化 SQLite 数据库表结构（links, tags, tasks）
│   ├── import_links.py            # 从 CSV 或纯文本批量导入链接的独立脚本
│   └── export_report.py           # 生成 Markdown 或 JSON 格式报告的导出工具
├── core/
│   ├── __init__.py
│   ├── checker.py                 # 链接健康检查核心逻辑，包含超时重试与状态码判断
│   ├── extractor.py               # 元数据提取模块，使用 BeautifulSoup 解析标题与描述
│   ├── scheduler.py               # APScheduler 封装，管理定时任务周期与执行上下文
│   └── graph.py                   # 链接关系图生成模块，输出邻接表或 DOT 格式数据
├── web/
│   ├── __init__.py
│   ├── routes.py                  # Web 路由定义，包含页面渲染与 API 端点
│   ├── forms.py                   # WTForms 表单类，用于链接编辑与搜索过滤
│   └── templates/
│       ├── base.html              # Jinja2 基础模板，包含公共导航与样式引用
│       ├── index.html             # 首页面板，显示链接总数、状态分布与近期任务
│       └── detail.html            # 单条链接详情页，展示元数据与历史检查记录
├── static/
│   ├── css/
│   │   └── style.css              # 自定义样式表，采用简洁的栅格布局与配色
│   └── js/
│       └── dashboard.js           # 前端交互脚本，处理表格排序、筛选与图表渲染
├── data/
│   └── linkvault.db               # SQLite 数据库文件（首次运行自动生成）
├── logs/
│   └── app.log                    # 运行日志输出，按日期轮转存储
└── tests/
    ├── test_checker.py            # 健康检查模块的单元测试
    ├── test_extractor.py          # 元数据提取模块的单元测试
    └── test_api.py                # API 端点的集成测试
```

## 贡献指南

1. 提交 Issue 讨论：在开始任何实质性开发前，请先在本项目的 Issue 列表中搜索是否已有相关讨论。若无，请新建 Issue 描述您希望修复的问题或新增的功能，并说明预期实现方案，以避免重复劳动或方向偏离。

2. 派生项目并创建特性分支：从主仓库派生代码到您的个人账户下，然后在本地基于 `main` 分支创建新的特性分支，分支名称建议采用 `feature/功能简述` 或 `fix/问题简述` 的格式。

3. 编写测试用例与代码：针对新增功能或修复内容，在 `tests/` 目录下补充对应的单元测试或集成测试用例，确保测试覆盖率达到 80% 以上。代码风格应遵循 PEP 8 规范，并保持与现有代码一致的命名习惯。

4. 提交 Pull Request：完成本地开发和测试后，将分支推送至您的派生仓库，然后向主仓库的 `main` 分支发起 Pull Request。请在 PR 描述中关联相关的 Issue 编号，并简要列出主要改动点与测试结果。

5. 代码评审与合并：维护者将对 PR 进行评审，可能提出修改意见。请及时响应反馈并更新代码。通过评审后，PR 将被合并到主分支，并自动关闭关联的 Issue。

## 常见问题

Q: LinkVault 是否支持 HTTPS 协议的链接检测？

A: 支持。底层使用的 requests 库会自动跟随 HTTP 到 HTTPS 的重定向，但系统不会强制将用户输入的 HTTP 链接改为 HTTPS，这符合本项目的设计原则——保留用户原始输入的 URL 不变。如果用户希望统一使用 HTTPS，可在导入前自行批量替换。

Q: 导入大量链接后，系统性能是否会下降？

A: LinkVault 对超过一万条链接的批量操作进行了优化：数据库查询使用索引（基于 url 字段和 status 字段），定时健康检查采用异步队列方式避免阻塞主线程。如果链接数量超过十万条，建议部署时使用 PostgreSQL 替代 SQLite，并在配置文件中调整检查任务的并发数。

Q: 如何导出特定标签或特定状态下的链接列表？

A: 您可以通过 Web 界面的过滤面板选择标签和状态条件，然后点击“导出”按钮下载 CSV 文件。也可以通过 API 接口 `/api/v1/links?tag=tech&status=active` 获取 JSON 格式的筛选结果，方便与外部数据分析工具集成。

## 许可证

MIT

> 外链数量: 250 | 生成时间: 2026-08-24 23:40:21
