# WebLink Navigator

WebLink Navigator 是一个面向技术研究、数据挖掘与内容聚合场景的高密度外链资源汇总平台。该项目定位于将分散于网络各处的深度技术文章、行业报告、案例分析及工程实践文档，按照统一的入口规范进行集中收录与索引，为开发者、技术决策者及信息分析人员提供可复用、可追溯、可批量访问的链接资产库。

本项目不生产原始内容，也不对第三方页面进行缓存或代理，而是以结构化目录的形式，对高质量外链资源进行编目与归档。当前批次为第 57/120 批，共计收录 250 个独立资源链接，覆盖技术资讯、工程日志、行业动态等多个维度。通过 WebLink Navigator，用户可以快速获取经过筛选的垂直领域链接集合，用于技术调研、竞品分析、知识图谱构建或自动化采集任务的种子数据源。

## 功能概览

批量链接导入：支持一次性导入大批量 URL 列表，自动进行去重、格式校验与存活探测，并生成标准化的资源索引表。

分类标签系统：每个链接可关联多个自定义标签，支持按技术栈、行业领域、内容类型或时间维度进行快速筛选与分组。

链接状态监控：内置周期性访问状态检查机制，对返回码、响应时间、页面标题变化进行跟踪，及时标记失效或内容变动的资源。

自定义元数据扩展：允许为每个链接附加备注、优先级、阅读状态、关联项目等自定义字段，满足个性化知识管理需求。

全文检索与过滤：基于链接标题、来源域名、标签组合及备注内容提供多条件全文检索，支持正则表达式与模糊匹配。

数据导入导出：支持 JSON、CSV、Markdown 表格三种格式的批量导入与导出，便于与其他知识管理工具或自动化脚本集成。

只读 API 接口：提供 RESTful 风格的只读查询接口，支持按标签、域名、状态码等参数获取链接列表，方便嵌入其他系统或定时任务。

## 应用场景

技术团队内部知识库建设：技术负责人或文档维护者可以使用 WebLink Navigator 汇总团队长期积累的参考文档、最佳实践链接和内部工具站点，形成统一的知识入口，减少重复查找时间。

自动化数据采集任务种子管理：数据工程师或爬虫开发者可将本项目的链接列表作为采集任务的起始 URL 池，结合状态监控功能定期更新种子库，确保采集链路稳定。

行业动态追踪与竞品分析：分析师可按照细分领域标签筛选相关资源，定期导出最新链接列表，配合第三方阅读工具进行信息聚合，快速把握行业趋势。

开源项目文档外链整理：开源项目维护者可将项目依赖的参考材料、生态工具、社区讨论帖等外链集中托管于此，降低 README 或 Wiki 中的链接维护成本。

学术研究文献索引辅助：研究人员可将论文中引用的在线资源、数据集主页、工具代码仓库等链接统一归档，便于论文撰写过程中快速回溯与验证引用来源。

## 快速开始

以下步骤帮助您在本地环境中快速启动 WebLink Navigator 服务。

```bash
# 克隆代码仓库
git clone https://github.com/weblink-navigator/weblink-navigator.git
cd weblink-navigator

# 安装 Python 依赖（推荐使用虚拟环境）
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt

# 初始化 SQLite 数据库并加载种子链接
python manage.py initdb
python manage.py load --batch 57 --input ./data/batch_57_links.json

# 启动开发服务器
python manage.py runserver --host 0.0.0.0 --port 8080
```

访问 http://localhost:8080 即可进入 Web 管理界面。首次启动将自动创建管理员账户，默认用户名 `admin`，密码打印在控制台日志中，请及时修改。

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|---|---|---|
| Python | 3.9 - 3.12 | 核心运行环境，建议使用 3.11 以获得最佳性能 |
| SQLite | 3.35.0 以上 | 内置数据库，用于存储链接元数据与状态历史 |
| Redis | 7.0 以上 | 可选，用于提升链接状态监控的队列处理性能 |
| Node.js | 18.0 以上 | 仅当需要构建前端静态资源时必需，生产环境可使用预构建包 |
| Nginx | 1.24 以上 | 生产环境反向代理推荐，非强制 |
| 系统内存 | 至少 512 MB | 单机部署最低要求，建议 2 GB 以上用于大规模批量操作 |
| 磁盘空间 | 至少 1 GB | 用于存储数据库文件及日志，链接数量每增加 1 万条约占用 50 MB |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|---|---|---|
| 用户手册 | /docs/user-guide/ | 如何添加链接、设置标签、导出列表、配置监控频率 |
| 管理员指南 | /docs/admin-guide/ | 如何管理用户权限、调整系统参数、执行数据备份与恢复 |
| API 参考 | /docs/api-reference/ | 查询接口的认证方式、请求参数、返回字段与错误码说明 |
| 部署运维 | /docs/deployment/ | 生产环境部署方案、容器化配置、性能调优与日志轮转策略 |
| 贡献者规范 | /docs/contributing/ | 代码提交规范、测试要求、文档编写标准与评审流程 |

完整文档托管于项目 Wiki 页面，离线版本可随每次发布打包下载。

## 资源列表

- http://m.wap.uliejh.cn/bnews/08387.htm
- http://m.wap.uliejh.cn/bnews/7845636.htm
- http://m.wap.uliejh.cn/bnews/5776.htm
- http://m.wap.uliejh.cn/bnews/27242.htm
- http://m.wap.uliejh.cn/bnews/4275793.htm
- http://m.wap.uliejh.cn/bnews/67566.htm
- http://m.wap.uliejh.cn/bnews/7821428.htm
- http://m.wap.uliejh.cn/bnews/6627923.htm
- http://m.wap.uliejh.cn/bnews/24229.htm
- http://m.wap.uliejh.cn/bnews/849672.htm
- http://m.wap.uliejh.cn/bnews/7914927.htm
- http://m.wap.uliejh.cn/bnews/8375275.htm
- http://m.wap.uliejh.cn/bnews/038883.htm
- http://m.wap.uliejh.cn/bnews/20008.htm
- http://m.wap.uliejh.cn/bnews/16542.htm
- http://m.wap.uliejh.cn/bnews/2051349.htm
- http://m.wap.uliejh.cn/bnews/1012904.htm
- http://m.wap.uliejh.cn/bnews/298645.htm
- http://m.wap.uliejh.cn/bnews/04940.htm
- http://m.wap.uliejh.cn/bnews/1918.htm
- http://m.wap.uliejh.cn/bnews/3382.htm
- http://m.wap.uliejh.cn/bnews/755695.htm
- http://m.wap.uliejh.cn/bnews/6118.htm
- http://m.wap.uliejh.cn/bnews/2230704.htm
- http://m.wap.uliejh.cn/bnews/166106.htm
- http://m.wap.uliejh.cn/bnews/6205.htm
- http://m.wap.uliejh.cn/bnews/7557152.htm
- http://m.wap.uliejh.cn/bnews/780096.htm
- http://m.wap.uliejh.cn/bnews/9356692.htm
- http://m.wap.uliejh.cn/bnews/1402.htm
- http://m.wap.uliejh.cn/bnews/4802.htm
- http://m.wap.uliejh.cn/bnews/30145.htm
- http://m.wap.uliejh.cn/bnews/96098.htm
- http://m.wap.uliejh.cn/bnews/101638.htm
- http://m.wap.uliejh.cn/bnews/03702.htm
- http://m.wap.uliejh.cn/bnews/8986.htm
- http://m.wap.uliejh.cn/bnews/3700238.htm
- http://m.wap.uliejh.cn/bnews/44745.htm
- http://m.wap.uliejh.cn/bnews/50970.htm
- http://m.wap.uliejh.cn/bnews/650625.htm
- http://m.wap.uliejh.cn/bnews/9032.htm
- http://m.wap.uliejh.cn/bnews/338215.htm
- http://m.wap.uliejh.cn/bnews/166717.htm
- http://m.wap.uliejh.cn/bnews/8162215.htm
- http://m.wap.uliejh.cn/bnews/97563.htm
- http://m.wap.uliejh.cn/bnews/274413.htm
- http://m.wap.uliejh.cn/bnews/4426268.htm
- http://m.wap.uliejh.cn/bnews/01352.htm
- http://m.wap.uliejh.cn/bnews/1754076.htm
- http://m.wap.uliejh.cn/bnews/1545408.htm
- http://m.wap.uliejh.cn/bnews/4187.htm
- http://m.wap.uliejh.cn/bnews/6039.htm
- http://m.wap.uliejh.cn/bnews/16818.htm
- http://m.wap.uliejh.cn/bnews/65014.htm
- http://m.wap.uliejh.cn/bnews/488460.htm
- http://m.wap.uliejh.cn/bnews/961030.htm
- http://m.wap.uliejh.cn/bnews/8672.htm
- http://m.wap.uliejh.cn/bnews/3798.htm
- http://m.wap.uliejh.cn/bnews/6396.htm
- http://m.wap.uliejh.cn/bnews/3183138.htm
- http://m.wap.uliejh.cn/bnews/74550.htm
- http://m.wap.uliejh.cn/bnews/0278.htm
- http://m.wap.uliejh.cn/bnews/1818.htm
- http://m.wap.uliejh.cn/bnews/962291.htm
- http://m.wap.uliejh.cn/bnews/3932240.htm
- http://m.wap.uliejh.cn/bnews/9403185.htm
- http://m.wap.uliejh.cn/bnews/1559973.htm
- http://m.wap.uliejh.cn/bnews/661396.htm
- http://m.wap.uliejh.cn/bnews/900778.htm
- http://m.wap.uliejh.cn/bnews/0482151.htm
- http://m.wap.uliejh.cn/bnews/47233.htm
- http://m.wap.uliejh.cn/bnews/5707.htm
- http://m.wap.uliejh.cn/bnews/4380554.htm
- http://m.wap.uliejh.cn/bnews/0714.htm
- http://m.wap.uliejh.cn/bnews/647260.htm
- http://m.wap.uliejh.cn/bnews/509493.htm
- http://m.wap.uliejh.cn/bnews/0867125.htm
- http://m.wap.uliejh.cn/bnews/7514.htm
- http://m.wap.uliejh.cn/bnews/048437.htm
- http://m.wap.uliejh.cn/bnews/283665.htm
- http://m.wap.uliejh.cn/bnews/1388.htm
- http://m.wap.uliejh.cn/bnews/27598.htm
- http://m.wap.uliejh.cn/bnews/5471.htm
- http://m.wap.uliejh.cn/bnews/4662367.htm
- http://m.wap.uliejh.cn/bnews/1356.htm
- http://m.wap.uliejh.cn/bnews/5234069.htm
- http://m.wap.uliejh.cn/bnews/1205.htm
- http://m.wap.uliejh.cn/bnews/7202353.htm
- http://m.wap.uliejh.cn/bnews/8660.htm
- http://m.wap.uliejh.cn/bnews/1887.htm
- http://m.wap.uliejh.cn/bnews/317142.htm
- http://m.wap.uliejh.cn/bnews/0683259.htm
- http://m.wap.uliejh.cn/bnews/4832.htm
- http://m.wap.uliejh.cn/bnews/33402.htm
- http://m.wap.uliejh.cn/bnews/22035.htm
- http://m.wap.uliejh.cn/bnews/0813331.htm
- http://m.wap.uliejh.cn/bnews/16321.htm
- http://m.wap.uliejh.cn/bnews/584439.htm
- http://m.wap.uliejh.cn/bnews/70951.htm
- http://m.wap.uliejh.cn/bnews/681062.htm
- http://m.wap.uliejh.cn/bnews/686253.htm
- http://m.wap.uliejh.cn/bnews/2442927.htm
- http://m.wap.uliejh.cn/bnews/8595.htm
- http://m.wap.uliejh.cn/bnews/0819.htm
- http://m.wap.uliejh.cn/bnews/3195819.htm
- http://m.wap.uliejh.cn/bnews/887288.htm
- http://m.wap.uliejh.cn/bnews/0838058.htm
- http://m.wap.uliejh.cn/bnews/1723391.htm
- http://m.wap.uliejh.cn/bnews/39344.htm
- http://m.wap.uliejh.cn/bnews/9418984.htm
- http://m.wap.uliejh.cn/bnews/4385882.htm
- http://m.wap.uliejh.cn/bnews/725720.htm
- http://m.wap.uliejh.cn/bnews/53929.htm
- http://m.wap.uliejh.cn/bnews/4041.htm
- http://m.wap.uliejh.cn/bnews/8340.htm
- http://m.wap.uliejh.cn/bnews/0990057.htm
- http://m.wap.uliejh.cn/bnews/28175.htm
- http://m.wap.uliejh.cn/bnews/5715564.htm
- http://m.wap.uliejh.cn/bnews/6431409.htm
- http://m.wap.uliejh.cn/bnews/443599.htm
- http://m.wap.uliejh.cn/bnews/358214.htm
- http://m.wap.uliejh.cn/bnews/171917.htm
- http://m.wap.uliejh.cn/bnews/2805433.htm
- http://m.wap.uliejh.cn/bnews/1769.htm
- http://m.wap.uliejh.cn/bnews/4717.htm
- http://m.wap.uliejh.cn/bnews/1500.htm
- http://m.wap.uliejh.cn/bnews/6434629.htm
- http://m.wap.uliejh.cn/bnews/644665.htm
- http://m.wap.uliejh.cn/bnews/5054970.htm
- http://m.wap.uliejh.cn/bnews/50564.htm
- http://m.wap.uliejh.cn/bnews/5728.htm
- http://m.wap.uliejh.cn/bnews/321433.htm
- http://m.wap.uliejh.cn/bnews/9347713.htm
- http://m.wap.uliejh.cn/bnews/55894.htm
- http://m.wap.uliejh.cn/bnews/28822.htm
- http://m.wap.uliejh.cn/bnews/495055.htm
- http://m.wap.uliejh.cn/bnews/0419693.htm
- http://m.wap.uliejh.cn/bnews/66834.htm
- http://m.wap.uliejh.cn/bnews/2894.htm
- http://m.wap.uliejh.cn/bnews/834906.htm
- http://m.wap.uliejh.cn/bnews/4086444.htm
- http://m.wap.uliejh.cn/bnews/9469.htm
- http://m.wap.uliejh.cn/bnews/60452.htm
- http://m.wap.uliejh.cn/bnews/461885.htm
- http://m.wap.uliejh.cn/bnews/4669365.htm
- http://m.wap.uliejh.cn/bnews/684163.htm
- http://m.wap.uliejh.cn/bnews/7896398.htm
- http://m.wap.uliejh.cn/bnews/19214.htm
- http://m.wap.uliejh.cn/bnews/99381.htm
- http://m.wap.uliejh.cn/bnews/1233.htm
- http://m.wap.uliejh.cn/bnews/7052680.htm
- http://m.wap.uliejh.cn/bnews/528757.htm
- http://m.wap.uliejh.cn/bnews/0209.htm
- http://m.wap.uliejh.cn/bnews/1222256.htm
- http://m.wap.uliejh.cn/bnews/698915.htm
- http://m.wap.uliejh.cn/bnews/9185805.htm
- http://m.wap.uliejh.cn/bnews/047349.htm
- http://m.wap.uliejh.cn/bnews/4235657.htm
- http://m.wap.uliejh.cn/bnews/1994664.htm
- http://m.wap.uliejh.cn/bnews/4354.htm
- http://m.wap.uliejh.cn/bnews/0968931.htm
- http://m.wap.uliejh.cn/bnews/3253.htm
- http://m.wap.uliejh.cn/bnews/05706.htm
- http://m.wap.uliejh.cn/bnews/734213.htm
- http://m.wap.uliejh.cn/bnews/970978.htm
- http://m.wap.uliejh.cn/bnews/00919.htm
- http://m.wap.uliejh.cn/bnews/194226.htm
- http://m.wap.uliejh.cn/bnews/2919006.htm
- http://m.wap.uliejh.cn/bnews/84065.htm
- http://m.wap.uliejh.cn/bnews/367165.htm
- http://m.wap.uliejh.cn/bnews/625261.htm
- http://m.wap.uliejh.cn/bnews/904414.htm
- http://m.wap.uliejh.cn/bnews/3071919.htm
- http://m.wap.uliejh.cn/bnews/76895.htm
- http://m.wap.uliejh.cn/bnews/0569.htm
- http://m.wap.uliejh.cn/bnews/82774.htm
- http://m.wap.uliejh.cn/bnews/253188.htm
- http://m.wap.uliejh.cn/bnews/1568.htm
- http://m.wap.uliejh.cn/bnews/4826.htm
- http://m.wap.uliejh.cn/bnews/72913.htm
- http://m.wap.uliejh.cn/bnews/8419.htm
- http://m.wap.uliejh.cn/bnews/0824.htm
- http://m.wap.uliejh.cn/bnews/159049.htm
- http://m.wap.uliejh.cn/bnews/1988003.htm
- http://m.wap.uliejh.cn/bnews/4419.htm
- http://m.wap.uliejh.cn/bnews/32991.htm
- http://m.wap.uliejh.cn/bnews/3719.htm
- http://m.wap.uliejh.cn/bnews/8000480.htm
- http://m.wap.uliejh.cn/bnews/3750.htm
- http://m.wap.uliejh.cn/bnews/6238580.htm
- http://m.wap.uliejh.cn/bnews/6916052.htm
- http://m.wap.uliejh.cn/bnews/74996.htm
- http://m.wap.uliejh.cn/bnews/1450405.htm
- http://m.wap.uliejh.cn/bnews/279345.htm
- http://m.wap.uliejh.cn/bnews/22256.htm
- http://m.wap.uliejh.cn/bnews/2602.htm
- http://m.wap.uliejh.cn/bnews/6287674.htm
- http://m.wap.uliejh.cn/bnews/524432.htm
- http://m.wap.uliejh.cn/bnews/5430138.htm
- http://m.wap.uliejh.cn/bnews/37265.htm
- http://m.wap.uliejh.cn/bnews/0400436.htm
- http://m.wap.uliejh.cn/bnews/935927.htm
- http://m.wap.uliejh.cn/bnews/2271297.htm
- http://m.wap.uliejh.cn/bnews/3484556.htm
- http://m.wap.uliejh.cn/bnews/988375.htm
- http://m.wap.uliejh.cn/bnews/80477.htm
- http://m.wap.uliejh.cn/bnews/7751.htm
- http://m.wap.uliejh.cn/bnews/7558064.htm
- http://m.wap.uliejh.cn/bnews/6971684.htm
- http://m.wap.uliejh.cn/bnews/3174808.htm
- http://m.wap.uliejh.cn/bnews/56260.htm
- http://m.wap.uliejh.cn/bnews/76161.htm
- http://m.wap.uliejh.cn/bnews/1235145.htm
- http://m.wap.uliejh.cn/bnews/98623.htm
- http://m.wap.uliejh.cn/bnews/5094931.htm
- http://m.wap.uliejh.cn/bnews/365614.htm
- http://m.wap.uliejh.cn/bnews/104611.htm
- http://m.wap.uliejh.cn/bnews/52754.htm
- http://m.wap.uliejh.cn/bnews/5605351.htm
- http://m.wap.uliejh.cn/bnews/96107.htm
- http://m.wap.uliejh.cn/bnews/48644.htm
- http://m.wap.uliejh.cn/bnews/82309.htm
- http://m.wap.uliejh.cn/bnews/5711536.htm
- http://m.wap.uliejh.cn/bnews/636728.htm
- http://m.wap.uliejh.cn/bnews/4251671.htm
- http://m.wap.uliejh.cn/bnews/527520.htm
- http://m.wap.uliejh.cn/bnews/8598130.htm
- http://m.wap.uliejh.cn/bnews/6633850.htm
- http://m.wap.uliejh.cn/bnews/4983610.htm
- http://m.wap.uliejh.cn/bnews/859473.htm
- http://m.wap.uliejh.cn/bnews/13149.htm
- http://m.wap.uliejh.cn/bnews/0190814.htm
- http://m.wap.uliejh.cn/bnews/415533.htm
- http://m.wap.uliejh.cn/bnews/9976.htm
- http://m.wap.uliejh.cn/bnews/3043607.htm
- http://m.wap.uliejh.cn/bnews/3150805.htm
- http://m.wap.uliejh.cn/bnews/6790.htm
- http://m.wap.uliejh.cn/bnews/84626.htm
- http://m.wap.uliejh.cn/bnews/839839.htm
- http://m.wap.uliejh.cn/bnews/15585.htm
- http://m.wap.uliejh.cn/bnews/625207.htm
- http://m.wap.uliejh.cn/bnews/420301.htm
- http://m.wap.uliejh.cn/bnews/816383.htm
- http://m.wap.uliejh.cn/bnews/6053690.htm
- http://m.wap.uliejh.cn/bnews/30659.htm
- http://m.wap.uliejh.cn/bnews/35286.htm
- http://m.wap.uliejh.cn/bnews/780874.htm
- http://m.wap.uliejh.cn/bnews/0752.htm
- http://m.wap.uliejh.cn/bnews/900530.htm
- http://m.wap.uliejh.cn/bnews/640451.htm

## 项目结构

```
weblink-navigator/
├── cmd/                                 # 命令行入口与启动脚本
│   ├── server/                          # HTTP 服务启动入口
│   │   └── main.go                      # 主服务进程，含路由注册与中间件
│   └── cli/                             # 命令行工具入口
│       ├── import.go                    # 批量导入子命令实现
│       ├── export.go                    # 批量导出子命令实现
│       └── monitor.go                   # 链接状态扫描触发子命令
├── internal/                            # 内部核心包，不对外暴露
│   ├── storage/                         # 数据存储抽象层
│   │   ├── sqlite.go                    # SQLite 驱动实现，含表结构迁移
│   │   └── redis.go                     # Redis 缓存与队列实现
│   ├── model/                           # 数据模型定义
│   │   ├── link.go                      # Link 结构体，含标签与状态字段
│   │   └── batch.go                     # 批次元数据模型
│   ├── service/                         # 业务逻辑层
│   │   ├── link_service.go              # 链接增删改查、标签管理核心逻辑
│   │   └── health_service.go            # 链接存活探测与状态更新逻辑
│   ├── api/                             # HTTP 处理函数
│   │   ├── handler_v1.go                # v1 版本 API 路由处理器
│   │   └── middleware.go                # 鉴权、日志、限流中间件
│   └── config/                          # 配置加载与解析
│       └── config.go                    # 支持环境变量与 YAML 配置文件
├── pkg/                                 # 可复用的公共库
│   ├── checker/                         # HTTP 状态检查工具包
│   │   └── http_checker.go              # 支持超时、重定向跟踪与 TLS 校验
│   └── utils/                           # 通用工具函数集合
│       ├── slug.go                      # URL 规范化与标签清洗
│       └── validator.go                 # 链接格式校验与域名黑名单过滤
├── web/                                 # 前端静态资源与模板
│   ├── static/                          # CSS、JavaScript 及图标文件
│   ├── templates/                       # Go 模板引擎渲染的 HTML 页面
│   └── dist/                            # 前端构建产物（生产环境使用）
├── scripts/                             # 辅助脚本与运维工具
│   ├── backup.sh                        # 数据库定期备份脚本
│   ├── migrate.sh                       # 数据库版本升级迁移脚本
│   └── seed_batch_57.sh                 # 当前批次链接加载示例脚本
├── configs/                             # 配置文件模板与示例
│   ├── app.yaml.example                 # 主配置文件示例，含端口、日志级别
│   └── monitor.yaml.example             # 链接监控周期与告警阈值配置
├── tests/                               # 单元测试与集成测试
│   ├── unit/                            # 各模块单元测试文件
│   └── integration/                     # 数据库与 API 集成测试
├── docs/                                # 文档源文件（Markdown 格式）
│   ├── user-guide/                      # 用户手册分章节
│   ├── api-reference/                   # API 接口文档
│   └── deployment/                      # 部署相关文档
├── go.mod                               # Go 模块依赖定义
├── go.sum                               # 依赖版本锁定文件
├── Makefile                             # 编译、测试、打包任务自动化
└── README.md                            # 项目总体介绍与快速入门（本文件）
```

## 贡献指南

提交 Issue 报告缺陷或功能请求：请使用 GitHub Issue 模板，清晰描述复现步骤、预期行为与实际行为，并附上相关日志或截图。功能请求请说明使用场景与期望收益。

分支开发与提交规范：从 `main` 分支切出 `feature/xxx` 或 `fix/xxx` 分支进行开发。提交信息遵循 Conventional Commits 格式，即 `type(scope): subject`，例如 `fix(storage): 修复链接去重时的大小写敏感问题`。

编写或更新测试用例：所有新功能或缺陷修复必须附带对应的单元测试或集成测试，确保测试覆盖率达到 80% 以上。运行 `make test` 验证本地所有测试通过。

更新文档：涉及用户可见功能变更时，需同步更新 `docs/` 目录下对应的用户手册或 API 文档，并在 Pull Request 描述中标注文档变更位置。

提交 Pull Request：推送到远程仓库后，创建 Pull Request 至 `main` 分支，填写 PR 模板中的检查清单。至少一名项目维护者进行 Code Review 后方可合并。

## 常见问题

Q: 导入大量链接时页面响应变慢或超时，如何解决？

A: 导入操作建议通过命令行工具 `manage.py import --batch 57 --input links.csv` 异步执行，避免通过 Web 界面上传超过 500 条记录。若仍需使用 Web 导入，可调整 Nginx 与 Go 服务的超时参数，并在配置文件中将 `import.batch_size` 设置为 200 以减少单次事务压力。

Q: 链接状态监控显示大量超时，但浏览器可以正常访问，是什么原因？

A: 监控服务默认使用 5 秒超时且不携带 Cookie 或浏览器特征头。部分站点对无头请求或非移动端 User-Agent 返回 403 或 503。您可以在 `configs/monitor.yaml` 中调整 `user_agent` 为移动端字符串，并适当增加 `timeout_seconds` 至 15 秒。若仍异常，可排除该域名或使用 `checker.skip_tls_verify` 忽略证书校验。

Q: 如何将本项目的链接列表同步到其他知识库工具，例如 Notion 或 Obsidian？

A: 推荐使用导出功能生成 CSV 或 JSON 文件，再通过目标工具的原生导入或社区插件进行转换。对于 Notion，可使用 `export --format csv --output links.csv` 导出，然后通过 Notion 的 CSV 导入功能创建数据库。对于 Obsidian，可使用 `export --format markdown --output links.md` 生成带链接列表的 Markdown 文件，直接放入 Obsidian 库中。

## 许可证

MIT

> 外链数量: 250 | 生成时间: 2026-08-24 23:40:21
