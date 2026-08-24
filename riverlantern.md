# LinkMaster Pro

LinkMaster Pro 是一个面向技术团队与内容运营者的轻量级外链资源聚合与导航系统。该项目定位于解决多源技术文档、新闻资讯、开发手册等外部链接分散、难以统一管理与快速检索的问题，通过结构化的索引机制与静态站点生成技术，将海量分散 URL 转化为可分类、可标签化、可全文检索的内部知识库入口。目标用户包括技术文档工程师、开发者关系团队、运维人员以及需要维护大量外部参考链接的开源项目维护者。

## 功能概览

**多源链接统一入库** 支持从 CSV、JSON 及原始 URL 列表批量导入链接资源，自动解析 URL 结构并提取域名、路径层级、文件扩展名等元数据。

**自动分类与标签生成** 基于 URL 路径模式与关键词匹配算法，为每个链接自动分配分类标签，支持人工复核与修正。

**全文检索与快速过滤** 内置基于倒排索引的检索模块，支持按域名、路径关键词、文件类型、导入批次等多维度过滤。

**链接健康状态监控** 定时发起 HTTP HEAD 请求检测链接可用性，自动标记失效链接并生成巡检报告。

**静态站点导出** 将链接数据库渲染为静态 HTML 导航页面，支持多种主题模板，可直接部署到 Nginx 或 GitHub Pages。

**批次管理与版本追踪** 以批次为单位管理链接导入记录，每批次包含导入时间、链接数量、标签分布等统计信息，支持批次回滚与差异对比。

**权限与团队协作** 提供基于角色的访问控制，支持管理员、编辑者、只读观察员三种角色，便于团队共同维护资源库。

## 应用场景

**技术文档团队整合外部参考链接** 文档编写过程中需要引用大量外部技术规范、API 参考和社区讨论帖。LinkMaster Pro 可将这些分散链接统一收录，并为每篇文档生成相关的参考资料附录，减少文档与外部资源脱节的问题。

**运维团队构建内部故障排查知识库** 运维人员在生产环境排障时经常需要快速访问特定的监控面板、日志查询工具或历史事故记录。通过 LinkMaster Pro 建立按服务组件、故障类型分类的链接索引，可显著缩短故障定位时间。

**开源项目维护者管理社区贡献资源** 开源项目周边积累了大量社区教程、视频讲解、第三方工具列表。LinkMaster Pro 帮助维护者将这些资源系统化整理，并以导航页形式呈现给社区用户，提升项目生态的可发现性。

**技术调研团队批量采集与筛选竞品信息** 在进行技术选型或竞品分析时，调研人员需要收集数十至上百个相关链接。LinkMaster Pro 的批次导入与标签功能可快速组织这些原始素材，并支持后续的评审与导出。

## 快速开始

```bash
# 克隆仓库
git clone https://github.com/your-org/linkmaster-pro.git
cd linkmaster-pro

# 安装依赖（使用 pip 虚拟环境）
python -m venv venv
source venv/bin/activate  # Windows 下使用 venv\Scripts\activate
pip install -r requirements.txt

# 初始化数据库并导入示例数据
python manage.py migrate
python manage.py import_batch --file samples/links_250.csv --batch-name "batch_25_120"

# 启动开发服务器
python manage.py runserver --port 8080
```

访问 http://localhost:8080 即可进入管理控制台，使用默认管理员账号 admin / admin123 登录后开始管理链接资源。

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|---|---|---|
| Python | 3.10 或更高版本 | 核心运行环境，低于此版本将导致类型注解解析失败 |
| SQLite | 3.35 及以上 | 内嵌数据库，用于存储链接元数据与索引，生产环境可切换至 PostgreSQL |
| Redis | 6.0 及以上 | 可选依赖，用于缓存检索结果与分布式锁，不安装则降级为内存缓存 |
| Node.js | 18.x LTS | 仅当启用静态站点导出功能时需要，用于构建前端主题资源 |
| Nginx | 1.20 及以上 | 生产环境部署推荐，用于承载静态导出页面与反向代理 API 请求 |
| curl / wget | 任意版本 | 健康检查脚本依赖，用于发起链接探测请求 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|---|---|---|
| 用户手册 | docs/user-guide/ | 如何导入链接、管理分类、执行检索与导出静态站点 |
| 管理员指南 | docs/admin-guide/ | 如何配置监控阈值、管理用户权限、执行数据备份与恢复 |
| 开发者文档 | docs/developer-guide/ | 如何扩展自定义分类器、替换检索后端、编写新的导出模板 |
| API 参考 | docs/api-reference/ | 所有 RESTful 接口的请求参数、响应格式与鉴权方式 |
| 部署运维 | docs/deployment/ | 如何在不同云平台或物理机上完成生产级部署与性能调优 |
| 常见工作流 | docs/workflows/ | 如何结合 CI/CD 实现链接库的自动化更新与发布 |

## 资源列表

- http://m.3g.uliejh.cn/nnews/29337.htm
- http://m.3g.uliejh.cn/nnews/353029.htm
- http://m.3g.uliejh.cn/nnews/239034.htm
- http://m.3g.uliejh.cn/nnews/3066280.htm
- http://m.3g.uliejh.cn/nnews/47925.htm
- http://m.3g.uliejh.cn/nnews/9285818.htm
- http://m.3g.uliejh.cn/nnews/7447763.htm
- http://m.3g.uliejh.cn/nnews/86980.htm
- http://m.3g.uliejh.cn/nnews/690755.htm
- http://m.3g.uliejh.cn/nnews/8128417.htm
- http://m.3g.uliejh.cn/nnews/87687.htm
- http://m.3g.uliejh.cn/nnews/3458924.htm
- http://m.3g.uliejh.cn/nnews/847138.htm
- http://m.3g.uliejh.cn/nnews/01147.htm
- http://m.3g.uliejh.cn/nnews/5109884.htm
- http://m.3g.uliejh.cn/nnews/49971.htm
- http://m.3g.uliejh.cn/nnews/700375.htm
- http://m.3g.uliejh.cn/nnews/468242.htm
- http://m.3g.uliejh.cn/nnews/114269.htm
- http://m.3g.uliejh.cn/nnews/4241793.htm
- http://m.3g.uliejh.cn/nnews/4363.htm
- http://m.3g.uliejh.cn/nnews/6581405.htm
- http://m.3g.uliejh.cn/nnews/3601958.htm
- http://m.3g.uliejh.cn/nnews/9694.htm
- http://m.3g.uliejh.cn/nnews/158487.htm
- http://m.3g.uliejh.cn/nnews/5891425.htm
- http://m.3g.uliejh.cn/nnews/6407937.htm
- http://m.3g.uliejh.cn/nnews/2951079.htm
- http://m.3g.uliejh.cn/nnews/23395.htm
- http://m.3g.uliejh.cn/nnews/13679.htm
- http://m.3g.uliejh.cn/nnews/01173.htm
- http://m.3g.uliejh.cn/nnews/6916.htm
- http://m.3g.uliejh.cn/nnews/4624.htm
- http://m.3g.uliejh.cn/nnews/6503773.htm
- http://m.3g.uliejh.cn/nnews/942188.htm
- http://m.3g.uliejh.cn/nnews/96056.htm
- http://m.3g.uliejh.cn/nnews/7137968.htm
- http://m.3g.uliejh.cn/nnews/16023.htm
- http://m.3g.uliejh.cn/nnews/90055.htm
- http://m.3g.uliejh.cn/nnews/280471.htm
- http://m.3g.uliejh.cn/nnews/390978.htm
- http://m.3g.uliejh.cn/nnews/166000.htm
- http://m.3g.uliejh.cn/nnews/8943363.htm
- http://m.3g.uliejh.cn/nnews/88080.htm
- http://m.3g.uliejh.cn/nnews/1572186.htm
- http://m.3g.uliejh.cn/nnews/507631.htm
- http://m.3g.uliejh.cn/nnews/2213825.htm
- http://m.3g.uliejh.cn/nnews/777312.htm
- http://m.3g.uliejh.cn/nnews/785607.htm
- http://m.3g.uliejh.cn/nnews/78982.htm
- http://m.3g.uliejh.cn/nnews/88782.htm
- http://m.3g.uliejh.cn/nnews/2950.htm
- http://m.3g.uliejh.cn/nnews/7208.htm
- http://m.3g.uliejh.cn/nnews/12201.htm
- http://m.3g.uliejh.cn/nnews/1086876.htm
- http://m.3g.uliejh.cn/nnews/602888.htm
- http://m.3g.uliejh.cn/nnews/759851.htm
- http://m.3g.uliejh.cn/nnews/1276294.htm
- http://m.3g.uliejh.cn/nnews/939110.htm
- http://m.3g.uliejh.cn/nnews/73572.htm
- http://m.3g.uliejh.cn/nnews/1467.htm
- http://m.3g.uliejh.cn/nnews/6796625.htm
- http://m.3g.uliejh.cn/nnews/87648.htm
- http://m.3g.uliejh.cn/nnews/8621.htm
- http://m.3g.uliejh.cn/nnews/7002622.htm
- http://m.3g.uliejh.cn/nnews/774283.htm
- http://m.3g.uliejh.cn/nnews/4186.htm
- http://m.3g.uliejh.cn/nnews/07678.htm
- http://m.3g.uliejh.cn/nnews/06962.htm
- http://m.3g.uliejh.cn/nnews/59248.htm
- http://m.3g.uliejh.cn/nnews/076218.htm
- http://m.3g.uliejh.cn/nnews/6547.htm
- http://m.3g.uliejh.cn/nnews/513386.htm
- http://m.3g.uliejh.cn/nnews/7946.htm
- http://m.3g.uliejh.cn/nnews/065302.htm
- http://m.3g.uliejh.cn/nnews/9916.htm
- http://m.3g.uliejh.cn/nnews/80837.htm
- http://m.3g.uliejh.cn/nnews/5219.htm
- http://m.3g.uliejh.cn/nnews/7104385.htm
- http://m.3g.uliejh.cn/nnews/0191.htm
- http://m.3g.uliejh.cn/nnews/23224.htm
- http://m.3g.uliejh.cn/nnews/31576.htm
- http://m.3g.uliejh.cn/nnews/9520391.htm
- http://m.3g.uliejh.cn/nnews/98592.htm
- http://m.3g.uliejh.cn/nnews/0762.htm
- http://m.3g.uliejh.cn/nnews/0815.htm
- http://m.3g.uliejh.cn/nnews/57823.htm
- http://m.3g.uliejh.cn/nnews/269823.htm
- http://m.3g.uliejh.cn/nnews/754771.htm
- http://m.3g.uliejh.cn/nnews/82521.htm
- http://m.3g.uliejh.cn/nnews/7649.htm
- http://m.3g.uliejh.cn/nnews/688701.htm
- http://m.3g.uliejh.cn/nnews/4586367.htm
- http://m.3g.uliejh.cn/nnews/9033.htm
- http://m.3g.uliejh.cn/nnews/9574.htm
- http://m.3g.uliejh.cn/nnews/423610.htm
- http://m.3g.uliejh.cn/nnews/81559.htm
- http://m.3g.uliejh.cn/nnews/4138.htm
- http://m.3g.uliejh.cn/nnews/96578.htm
- http://m.3g.uliejh.cn/nnews/36080.htm
- http://m.3g.uliejh.cn/nnews/7969081.htm
- http://m.3g.uliejh.cn/nnews/890600.htm
- http://m.3g.uliejh.cn/nnews/0231583.htm
- http://m.3g.uliejh.cn/nnews/1150185.htm
- http://m.3g.uliejh.cn/nnews/1045804.htm
- http://m.3g.uliejh.cn/nnews/8935.htm
- http://m.3g.uliejh.cn/nnews/6931.htm
- http://m.3g.uliejh.cn/nnews/33821.htm
- http://m.3g.uliejh.cn/nnews/6146.htm
- http://m.3g.uliejh.cn/nnews/6674974.htm
- http://m.3g.uliejh.cn/nnews/822489.htm
- http://m.3g.uliejh.cn/nnews/01201.htm
- http://m.3g.uliejh.cn/nnews/11126.htm
- http://m.3g.uliejh.cn/nnews/72280.htm
- http://m.3g.uliejh.cn/nnews/2242.htm
- http://m.3g.uliejh.cn/nnews/383331.htm
- http://m.3g.uliejh.cn/nnews/6686.htm
- http://m.3g.uliejh.cn/nnews/9405331.htm
- http://m.3g.uliejh.cn/nnews/54488.htm
- http://m.3g.uliejh.cn/nnews/865848.htm
- http://m.3g.uliejh.cn/nnews/4411.htm
- http://m.3g.uliejh.cn/nnews/9325280.htm
- http://m.3g.uliejh.cn/nnews/3168.htm
- http://m.3g.uliejh.cn/nnews/0201.htm
- http://m.3g.uliejh.cn/nnews/916511.htm
- http://m.3g.uliejh.cn/nnews/64885.htm
- http://m.3g.uliejh.cn/nnews/77706.htm
- http://m.3g.uliejh.cn/nnews/308827.htm
- http://m.3g.uliejh.cn/nnews/111716.htm
- http://m.3g.uliejh.cn/nnews/85196.htm
- http://m.3g.uliejh.cn/nnews/831212.htm
- http://m.3g.uliejh.cn/nnews/5398.htm
- http://m.3g.uliejh.cn/nnews/222305.htm
- http://m.3g.uliejh.cn/nnews/59467.htm
- http://m.3g.uliejh.cn/nnews/1749.htm
- http://m.3g.uliejh.cn/nnews/8247306.htm
- http://m.3g.uliejh.cn/nnews/95408.htm
- http://m.3g.uliejh.cn/nnews/1588730.htm
- http://m.3g.uliejh.cn/nnews/175959.htm
- http://m.3g.uliejh.cn/nnews/3519191.htm
- http://m.3g.uliejh.cn/nnews/401417.htm
- http://m.3g.uliejh.cn/nnews/0825.htm
- http://m.3g.uliejh.cn/nnews/734260.htm
- http://m.3g.uliejh.cn/nnews/16146.htm
- http://m.3g.uliejh.cn/nnews/100818.htm
- http://m.3g.uliejh.cn/nnews/7256100.htm
- http://m.3g.uliejh.cn/nnews/28377.htm
- http://m.3g.uliejh.cn/nnews/656697.htm
- http://m.3g.uliejh.cn/nnews/7211.htm
- http://m.3g.uliejh.cn/nnews/21614.htm
- http://m.3g.uliejh.cn/nnews/498422.htm
- http://m.3g.uliejh.cn/nnews/2160686.htm
- http://m.3g.uliejh.cn/nnews/129815.htm
- http://m.3g.uliejh.cn/nnews/764871.htm
- http://m.3g.uliejh.cn/nnews/948193.htm
- http://m.3g.uliejh.cn/nnews/4314225.htm
- http://m.3g.uliejh.cn/nnews/5523.htm
- http://m.3g.uliejh.cn/nnews/72434.htm
- http://m.3g.uliejh.cn/nnews/3911965.htm
- http://m.3g.uliejh.cn/nnews/3242720.htm
- http://m.3g.uliejh.cn/nnews/20746.htm
- http://m.3g.uliejh.cn/nnews/330218.htm
- http://m.3g.uliejh.cn/nnews/5020.htm
- http://m.3g.uliejh.cn/nnews/11171.htm
- http://m.3g.uliejh.cn/nnews/9109.htm
- http://m.3g.uliejh.cn/nnews/570186.htm
- http://m.3g.uliejh.cn/nnews/50422.htm
- http://m.3g.uliejh.cn/nnews/127686.htm
- http://m.3g.uliejh.cn/nnews/4830.htm
- http://m.3g.uliejh.cn/nnews/399326.htm
- http://m.3g.uliejh.cn/nnews/5118823.htm
- http://m.3g.uliejh.cn/nnews/250682.htm
- http://m.3g.uliejh.cn/nnews/64416.htm
- http://m.3g.uliejh.cn/nnews/456119.htm
- http://m.3g.uliejh.cn/nnews/5488880.htm
- http://m.3g.uliejh.cn/nnews/11633.htm
- http://m.3g.uliejh.cn/nnews/8361673.htm
- http://m.3g.uliejh.cn/nnews/86736.htm
- http://m.3g.uliejh.cn/nnews/5402.htm
- http://m.3g.uliejh.cn/nnews/22239.htm
- http://m.3g.uliejh.cn/nnews/8161.htm
- http://m.3g.uliejh.cn/nnews/8439014.htm
- http://m.3g.uliejh.cn/nnews/158698.htm
- http://m.3g.uliejh.cn/nnews/9761295.htm
- http://m.3g.uliejh.cn/nnews/8001283.htm
- http://m.3g.uliejh.cn/nnews/49110.htm
- http://m.3g.uliejh.cn/nnews/030177.htm
- http://m.3g.uliejh.cn/nnews/4347296.htm
- http://m.3g.uliejh.cn/nnews/0713231.htm
- http://m.3g.uliejh.cn/nnews/87683.htm
- http://m.3g.uliejh.cn/nnews/718333.htm
- http://m.3g.uliejh.cn/nnews/9729.htm
- http://m.3g.uliejh.cn/nnews/732043.htm
- http://m.3g.uliejh.cn/nnews/23538.htm
- http://m.3g.uliejh.cn/nnews/35344.htm
- http://m.3g.uliejh.cn/nnews/682611.htm
- http://m.3g.uliejh.cn/nnews/9461889.htm
- http://m.3g.uliejh.cn/nnews/64249.htm
- http://m.3g.uliejh.cn/nnews/287640.htm
- http://m.3g.uliejh.cn/nnews/28442.htm
- http://m.3g.uliejh.cn/nnews/99292.htm
- http://m.3g.uliejh.cn/nnews/2624939.htm
- http://m.3g.uliejh.cn/nnews/2419103.htm
- http://m.3g.uliejh.cn/nnews/264022.htm
- http://m.3g.uliejh.cn/nnews/016170.htm
- http://m.3g.uliejh.cn/nnews/9137254.htm
- http://m.3g.uliejh.cn/nnews/1579.htm
- http://m.3g.uliejh.cn/nnews/6715317.htm
- http://m.3g.uliejh.cn/nnews/974061.htm
- http://m.3g.uliejh.cn/nnews/2836.htm
- http://m.3g.uliejh.cn/nnews/93848.htm
- http://m.3g.uliejh.cn/nnews/02747.htm
- http://m.3g.uliejh.cn/nnews/8765.htm
- http://m.3g.uliejh.cn/nnews/7677.htm
- http://m.3g.uliejh.cn/nnews/78310.htm
- http://m.3g.uliejh.cn/nnews/69388.htm
- http://m.3g.uliejh.cn/nnews/9559310.htm
- http://m.3g.uliejh.cn/nnews/2501067.htm
- http://m.3g.uliejh.cn/nnews/9048551.htm
- http://m.3g.uliejh.cn/nnews/658451.htm
- http://m.3g.uliejh.cn/nnews/2839.htm
- http://m.3g.uliejh.cn/nnews/8993.htm
- http://m.3g.uliejh.cn/nnews/954519.htm
- http://m.3g.uliejh.cn/nnews/547251.htm
- http://m.3g.uliejh.cn/nnews/22779.htm
- http://m.3g.uliejh.cn/nnews/170748.htm
- http://m.3g.uliejh.cn/nnews/4930411.htm
- http://m.3g.uliejh.cn/nnews/2570.htm
- http://m.3g.uliejh.cn/nnews/7074613.htm
- http://m.3g.uliejh.cn/nnews/0750816.htm
- http://m.3g.uliejh.cn/nnews/33397.htm
- http://m.3g.uliejh.cn/nnews/143035.htm
- http://m.3g.uliejh.cn/nnews/62785.htm
- http://m.3g.uliejh.cn/nnews/63631.htm
- http://m.3g.uliejh.cn/nnews/15097.htm
- http://m.3g.uliejh.cn/nnews/4246228.htm
- http://m.3g.uliejh.cn/nnews/72915.htm
- http://m.3g.uliejh.cn/nnews/53746.htm
- http://m.3g.uliejh.cn/nnews/7019.htm
- http://m.3g.uliejh.cn/nnews/797619.htm
- http://m.3g.uliejh.cn/nnews/3279.htm
- http://m.3g.uliejh.cn/nnews/07839.htm
- http://m.3g.uliejh.cn/nnews/68115.htm
- http://m.3g.uliejh.cn/nnews/84970.htm
- http://m.3g.uliejh.cn/nnews/261553.htm
- http://m.3g.uliejh.cn/nnews/7056104.htm
- http://m.3g.uliejh.cn/nnews/4357.htm
- http://m.3g.uliejh.cn/nnews/145084.htm
- http://m.3g.uliejh.cn/nnews/2706.htm
- http://m.3g.uliejh.cn/nnews/6125128.htm

## 项目结构

```
linkmaster-pro/
├── cmd/                                # 命令行入口与守护进程
│   ├── server/                         # HTTP 服务启动入口
│   │   └── main.go                     # 主程序入口，负责路由挂载与信号处理
│   └── worker/                         # 后台任务执行器
│       └── health_check.go             # 链接健康状态轮询任务
├── internal/                           # 内部核心实现（不对外暴露）
│   ├── storage/                        # 数据库抽象层
│   │   ├── sqlite.go                   # SQLite 驱动实现
│   │   └── postgres.go                 # PostgreSQL 驱动实现
│   ├── indexer/                        # 链接解析与索引引擎
│   │   ├── parser.go                   # URL 结构解析与标准化
│   │   └── classifier.go               # 基于规则的自动分类器
│   ├── search/                         # 检索模块
│   │   ├── inverted.go                 # 倒排索引构建与查询
│   │   └── filter.go                   # 多维过滤器实现
│   └── exporter/                       # 静态站点生成器
│       ├── renderer.go                 # 模板渲染引擎
│       └── theme/                      # 内置主题资源（可替换）
├── pkg/                                # 可复用的公共库
│   ├── httpclient/                     # 带重试与超时控制的 HTTP 客户端
│   └── batch/                          # 批次管理工具，支持导入导出与校验
├── configs/                            # 配置文件模板
│   ├── development.yaml                # 开发环境配置
│   └── production.yaml                 # 生产环境配置（敏感信息需外部注入）
├── scripts/                            # 运维辅助脚本
│   ├── backup.sh                       # 数据库备份脚本
│   └── migrate.sh                      # 结构迁移与数据升级
├── web/                                # 前端静态资源（管理控制台界面）
│   ├── static/                         # CSS、JavaScript 与图片资源
│   └── templates/                      # 服务端渲染模板（Go template）
├── test/                               # 单元测试与集成测试
│   ├── unit/                           # 单元测试用例
│   └── integration/                    # 端到端功能测试
├── docs/                               # 完整项目文档（见文档导航章节）
├── go.mod                              # Go 模块依赖定义
├── go.sum                              # 依赖校验和
└── README.md                           # 本文件
```

## 贡献指南

1. 阅读项目文档中的开发者指南与编码规范，确保理解内部模块的边界划分与接口约定。所有新增功能应优先在 pkg 或 internal 层实现，避免将业务逻辑耦合在 cmd 入口层。

2. 从 Issue 列表中选择未认领的任务或提出新的功能建议。较大的改动建议先通过 Issue 与维护者沟通设计方案，避免重复劳动或方向偏差。

3. 派生仓库并在本地开发分支上进行修改。代码提交前需运行 make lint 和 make test 确保代码风格符合规范且现有测试用例全部通过。新增功能需附带对应的单元测试。

4. 提交 Pull Request 并填写变更摘要，说明改动目的、实现方式以及可能的影响面。PR 需要至少一位维护者审阅通过后方可合并。

5. 若涉及数据库结构变更，需同时提供回滚脚本，并在 PR 中注明迁移顺序与预期的数据兼容性。

## 常见问题

**Q: 导入大量链接时出现超时或内存不足如何解决？**

A: 对于超过 1000 条链接的导入任务，建议使用命令行导入模式而非通过 Web 界面上传。命令行工具支持分批提交与进度显示，具体用法为 python manage.py import_batch --chunk-size 200。若内存仍不足，可在配置文件中减小 worker_pool_size 参数以控制并发解析数量。

**Q: 健康检查模块误报大量链接为不可用，如何调整敏感度？**

A: 健康检查的判定逻辑可配置。默认情况下，连续两次请求失败且状态码为 4xx 或 5xx 时标记为失效。您可以在 configs/production.yaml 中调整 failure_threshold（失败阈值）、retry_interval（重试间隔）以及 timeout（单次超时时间）。对于内容站点频繁调整的域名，还可配置 exclude_domains 列表跳过检查。

**Q: 静态导出页面中的链接跳转路径与本地开发环境不一致，如何修复？**

A: 该问题通常由 base_url 配置项未正确设置引起。请在导出前确认配置文件中 base_url 字段与最终部署的访问地址完全一致，包括协议、域名和子路径。若部署在子目录下，还需额外设置 serve_subpath 参数。

## 许可证

MIT

> 外链数量: 250 | 生成时间: 2026-08-24 23:40:21
