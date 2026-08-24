# ResourceBridge 索引聚合系统

ResourceBridge 是一个面向技术调研、知识管理及内容聚合场景的轻量级外链资源索引系统。项目定位于为开发者、技术作者、运维工程师以及数据分析人员提供结构化的外部文章、新闻资讯与技术笔记的快速查阅入口。系统本身不存储全文内容，仅维护高质量的链接索引与元信息标签，通过简洁的本地 Web 界面或 API 接口实现对海量分散资源的统一检索与分类导航。

本项目的目标用户包括：需要持续跟踪特定技术领域动态的研发团队、撰写技术周报或月刊的编辑人员、开展竞品分析与市场舆情监控的产品经理，以及希望建立个人知识库但缺乏链接管理方案的学习者。ResourceBridge 通过固定的资源批次划分（当前为第 98/120 批，共 250 个资源链接），帮助用户在既定批次范围内快速定位、筛选和回溯外部信息源，避免浏览器书签杂乱无章或依赖第三方网络收藏夹服务带来的隐私泄露风险。

## 功能概览

**多维度标签筛选**：系统为每个资源链接自动生成或手动绑定技术领域、内容类型、来源域名、更新时间等标签维度，支持按标签组合快速过滤目标链接。

**批次化数据管理**：采用 120 批次的滚动更新机制，每批固定收录 250 个外部链接。当前第 98 批次涵盖技术博客、新闻资讯、教程文档等多种内容形态，便于按时间周期进行内容审计与过期链接剔除。

**本地全文检索**：基于内存索引或可选的外部搜索引擎（如 Elasticsearch 或 Meilisearch）提供对链接标题、摘要描述、关键词的快速检索，响应时间控制在 200 毫秒以内。

**链接可用性监控**：内置异步链接探测任务，可定期对已收录的 URL 发起 HEAD 请求，检测状态码变化并标记失效链接，辅助管理员及时更新或移除死链。

**结构化数据导出**：支持将当前批次的资源列表导出为 CSV、JSON 或 Markdown 表格格式，便于下游工具链（如静态站点生成器、数据可视化看板、自动化周报脚本）消费。

**权限与访问控制**：提供基于 IP 白名单或简单 API Token 的只读/读写两级权限管理，适用于内部团队共享部署场景，防止未授权的外部爬虫滥用索引数据。

**自定义元数据扩展**：允许用户为每个链接附加自定义字段，例如阅读优先级（1-5 星）、关联项目代码仓库地址、个人批注笔记等，满足个性化知识管理需求。

## 应用场景

**技术团队周报自动化生成**：研发负责人或技术经理可定期从 ResourceBridge 中拉取第 98 批次内与后端架构、云原生、性能优化相关的链接，结合团队内部项目进度，自动生成附带外部参考阅读材料的技术周报，减少手动搜集链接的时间成本。

**开源项目文档外链管理**：开源项目维护者在编写 README 或官方文档时，需要引用大量外部参考资料、设计决策讨论帖或生态工具列表。通过 ResourceBridge 按批次整理这些外链，可确保文档中的引用链接具有统一的版本记录，便于后续审查与更新。

**技术调研与竞品监控**：产品团队或解决方案架构师在开展技术选型或市场分析时，需要持续跟踪多个竞品公司的官方博客、技术社区热帖和行业评测报告。ResourceBridge 的标签筛选功能可将来自 `m.blog.uliejh.cn` 等特定域名的文章单独聚合，形成垂直监控视图。

**个人知识库外链备份**：独立开发者或技术博主在撰写长文或制作视频教程时，常常需要引用大量网页资料。ResourceBridge 作为外链缓存层，可以提供稳定的链接索引服务，即使原始网页临时不可访问，索引记录仍保留来源信息与采集时间戳，方便后续补链或归档。

## 快速开始

以下步骤指引用户从源码克隆到本地运行 ResourceBridge 基础服务。

```bash
# 克隆项目仓库
git clone https://github.com/resourcebridge/resourcebridge.git

# 进入项目根目录
cd resourcebridge

# 安装 Python 依赖（推荐使用虚拟环境）
python3 -m venv venv
source venv/bin/activate  # Windows 下使用 venv\Scripts\activate
pip install -r requirements.txt

# 初始化本地数据库（SQLite）
python manage.py init_db

# 导入第 98 批次资源链接数据
python manage.py import_batch --batch 98 --source ./data/batch_98.csv

# 启动开发服务器（默认监听 127.0.0.1:8080）
python manage.py runserver --port 8080
```

完成上述步骤后，访问 `http://127.0.0.1:8080` 即可进入 ResourceBridge 的 Web 检索界面。管理员后台默认路径为 `/admin`，初始账号密码请查阅 `docs/default_credentials.md` 文件并在首次登录后立即修改。

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|---|---|---|
| Python | 3.9 及以上 | 核心运行环境，建议使用 3.11 或 3.12 以获取更好性能 |
| SQLite | 3.35 及以上 | 默认嵌入式数据库，用于存储链接索引与元数据，无需额外安装 |
| pip | 21.0 及以上 | Python 包管理工具，用于安装 requirements.txt 中声明的依赖库 |
| 内存 | 最低 512 MB，推荐 2 GB | 当启用全文检索内存缓存时，索引 250 条记录约占用 120 MB 内存 |
| 磁盘空间 | 至少 200 MB | 用于存储数据库文件、日志以及临时导入文件，实际占用随批次数量线性增长 |
| 操作系统 | Linux / macOS / Windows (WSL2 推荐) | 跨平台支持，生产环境推荐 Linux 内核 5.x 以上发行版 |
| 网络 | 可访问公网或内网资源域名 | 用于链接可用性探测任务，若完全离线可关闭该功能模块 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|---|---|---|
| 用户手册 | `docs/user_guide.md` | 如何使用 Web 界面进行资源检索、标签筛选、导出数据以及自定义批注？ |
| 管理员指南 | `docs/admin_guide.md` | 如何创建新的资源批次、批量更新链接元数据、配置链接探测策略和权限管理？ |
| API 参考 | `docs/api_reference.md` | 提供哪些 RESTful 接口用于查询资源列表、按条件过滤、获取单条详情及统计信息？ |
| 开发运维 | `docs/devops.md` | 如何修改前端模板样式、增加新的标签解析规则、以及使用 Docker 镜像进行生产部署？ |

## 资源列表

- http://m.blog.uliejh.cn/snews/20359.htm
- http://m.blog.uliejh.cn/snews/3990338.htm
- http://m.blog.uliejh.cn/snews/5978.htm
- http://m.blog.uliejh.cn/snews/338116.htm
- http://m.blog.uliejh.cn/snews/951483.htm
- http://m.blog.uliejh.cn/snews/3313966.htm
- http://m.blog.uliejh.cn/snews/200903.htm
- http://m.blog.uliejh.cn/snews/4843789.htm
- http://m.blog.uliejh.cn/snews/5304.htm
- http://m.blog.uliejh.cn/snews/4234606.htm
- http://m.blog.uliejh.cn/snews/9581.htm
- http://m.blog.uliejh.cn/snews/6709282.htm
- http://m.blog.uliejh.cn/snews/298320.htm
- http://m.blog.uliejh.cn/snews/3520.htm
- http://m.blog.uliejh.cn/snews/927543.htm
- http://m.blog.uliejh.cn/snews/257994.htm
- http://m.blog.uliejh.cn/snews/32599.htm
- http://m.blog.uliejh.cn/snews/771409.htm
- http://m.blog.uliejh.cn/snews/7745445.htm
- http://m.blog.uliejh.cn/snews/916722.htm
- http://m.blog.uliejh.cn/snews/5589393.htm
- http://m.blog.uliejh.cn/snews/25193.htm
- http://m.blog.uliejh.cn/snews/36324.htm
- http://m.blog.uliejh.cn/snews/09202.htm
- http://m.blog.uliejh.cn/snews/29139.htm
- http://m.blog.uliejh.cn/snews/6484807.htm
- http://m.blog.uliejh.cn/snews/0741.htm
- http://m.blog.uliejh.cn/snews/42862.htm
- http://m.blog.uliejh.cn/snews/6371905.htm
- http://m.blog.uliejh.cn/snews/9872786.htm
- http://m.blog.uliejh.cn/snews/23082.htm
- http://m.blog.uliejh.cn/snews/73093.htm
- http://m.blog.uliejh.cn/snews/9660.htm
- http://m.blog.uliejh.cn/snews/1578.htm
- http://m.blog.uliejh.cn/snews/84242.htm
- http://m.blog.uliejh.cn/snews/0862.htm
- http://m.blog.uliejh.cn/snews/76688.htm
- http://m.blog.uliejh.cn/snews/20960.htm
- http://m.blog.uliejh.cn/snews/6388.htm
- http://m.blog.uliejh.cn/snews/438005.htm
- http://m.blog.uliejh.cn/snews/43524.htm
- http://m.blog.uliejh.cn/snews/282382.htm
- http://m.blog.uliejh.cn/snews/9720.htm
- http://m.blog.uliejh.cn/snews/34246.htm
- http://m.blog.uliejh.cn/snews/2818.htm
- http://m.blog.uliejh.cn/snews/6203.htm
- http://m.blog.uliejh.cn/snews/41340.htm
- http://m.blog.uliejh.cn/snews/011393.htm
- http://m.blog.uliejh.cn/snews/856453.htm
- http://m.blog.uliejh.cn/snews/03030.htm
- http://m.blog.uliejh.cn/snews/1815.htm
- http://m.blog.uliejh.cn/snews/813295.htm
- http://m.blog.uliejh.cn/snews/51256.htm
- http://m.blog.uliejh.cn/snews/28871.htm
- http://m.blog.uliejh.cn/snews/427032.htm
- http://m.blog.uliejh.cn/snews/071814.htm
- http://m.blog.uliejh.cn/snews/676272.htm
- http://m.blog.uliejh.cn/snews/35519.htm
- http://m.blog.uliejh.cn/snews/9050.htm
- http://m.blog.uliejh.cn/snews/815638.htm
- http://m.blog.uliejh.cn/snews/3863.htm
- http://m.blog.uliejh.cn/snews/027459.htm
- http://m.blog.uliejh.cn/snews/4192580.htm
- http://m.blog.uliejh.cn/snews/3045.htm
- http://m.blog.uliejh.cn/snews/81102.htm
- http://m.blog.uliejh.cn/snews/4665.htm
- http://m.blog.uliejh.cn/snews/528650.htm
- http://m.blog.uliejh.cn/snews/0285.htm
- http://m.blog.uliejh.cn/snews/7566.htm
- http://m.blog.uliejh.cn/snews/885104.htm
- http://m.blog.uliejh.cn/snews/933907.htm
- http://m.blog.uliejh.cn/snews/414721.htm
- http://m.blog.uliejh.cn/snews/416893.htm
- http://m.blog.uliejh.cn/snews/0952678.htm
- http://m.blog.uliejh.cn/snews/3667.htm
- http://m.blog.uliejh.cn/snews/8837.htm
- http://m.blog.uliejh.cn/snews/0711.htm
- http://m.blog.uliejh.cn/snews/2090194.htm
- http://m.blog.uliejh.cn/snews/809414.htm
- http://m.blog.uliejh.cn/snews/40096.htm
- http://m.blog.uliejh.cn/snews/30551.htm
- http://m.blog.uliejh.cn/snews/857566.htm
- http://m.blog.uliejh.cn/snews/29974.htm
- http://m.blog.uliejh.cn/snews/802663.htm
- http://m.blog.uliejh.cn/snews/7245478.htm
- http://m.blog.uliejh.cn/snews/96549.htm
- http://m.blog.uliejh.cn/snews/6828814.htm
- http://m.blog.uliejh.cn/snews/54504.htm
- http://m.blog.uliejh.cn/snews/49254.htm
- http://m.blog.uliejh.cn/snews/80029.htm
- http://m.blog.uliejh.cn/snews/69503.htm
- http://m.blog.uliejh.cn/snews/8721796.htm
- http://m.blog.uliejh.cn/snews/83487.htm
- http://m.blog.uliejh.cn/snews/4773.htm
- http://m.blog.uliejh.cn/snews/763927.htm
- http://m.blog.uliejh.cn/snews/3597220.htm
- http://m.blog.uliejh.cn/snews/473595.htm
- http://m.blog.uliejh.cn/snews/66709.htm
- http://m.blog.uliejh.cn/snews/97616.htm
- http://m.blog.uliejh.cn/snews/8175.htm
- http://m.blog.uliejh.cn/snews/4685182.htm
- http://m.blog.uliejh.cn/snews/26911.htm
- http://m.blog.uliejh.cn/snews/8631048.htm
- http://m.blog.uliejh.cn/snews/990381.htm
- http://m.blog.uliejh.cn/snews/754552.htm
- http://m.blog.uliejh.cn/snews/0813348.htm
- http://m.blog.uliejh.cn/snews/46541.htm
- http://m.blog.uliejh.cn/snews/7319526.htm
- http://m.blog.uliejh.cn/snews/6970.htm
- http://m.blog.uliejh.cn/snews/7874205.htm
- http://m.blog.uliejh.cn/snews/506585.htm
- http://m.blog.uliejh.cn/snews/5067.htm
- http://m.blog.uliejh.cn/snews/2260986.htm
- http://m.blog.uliejh.cn/snews/5461.htm
- http://m.blog.uliejh.cn/snews/9063.htm
- http://m.blog.uliejh.cn/snews/287335.htm
- http://m.blog.uliejh.cn/snews/17372.htm
- http://m.blog.uliejh.cn/snews/91642.htm
- http://m.blog.uliejh.cn/snews/98091.htm
- http://m.blog.uliejh.cn/snews/9515.htm
- http://m.blog.uliejh.cn/snews/44804.htm
- http://m.blog.uliejh.cn/snews/236720.htm
- http://m.blog.uliejh.cn/snews/56456.htm
- http://m.blog.uliejh.cn/snews/6664.htm
- http://m.blog.uliejh.cn/snews/9170817.htm
- http://m.blog.uliejh.cn/snews/25296.htm
- http://m.blog.uliejh.cn/snews/2231258.htm
- http://m.blog.uliejh.cn/snews/7395.htm
- http://m.blog.uliejh.cn/snews/898451.htm
- http://m.blog.uliejh.cn/snews/78457.htm
- http://m.blog.uliejh.cn/snews/5838456.htm
- http://m.blog.uliejh.cn/snews/1280.htm
- http://m.blog.uliejh.cn/snews/412462.htm
- http://m.blog.uliejh.cn/snews/5344844.htm
- http://m.blog.uliejh.cn/snews/0244.htm
- http://m.blog.uliejh.cn/snews/2167.htm
- http://m.blog.uliejh.cn/snews/73338.htm
- http://m.blog.uliejh.cn/snews/4123.htm
- http://m.blog.uliejh.cn/snews/9473.htm
- http://m.blog.uliejh.cn/snews/979184.htm
- http://m.blog.uliejh.cn/snews/88671.htm
- http://m.blog.uliejh.cn/snews/2364824.htm
- http://m.blog.uliejh.cn/snews/03653.htm
- http://m.blog.uliejh.cn/snews/579074.htm
- http://m.blog.uliejh.cn/snews/98165.htm
- http://m.blog.uliejh.cn/snews/24288.htm
- http://m.blog.uliejh.cn/snews/128090.htm
- http://m.blog.uliejh.cn/snews/3984.htm
- http://m.blog.uliejh.cn/snews/921961.htm
- http://m.blog.uliejh.cn/snews/9173219.htm
- http://m.blog.uliejh.cn/snews/0204.htm
- http://m.blog.uliejh.cn/snews/5241.htm
- http://m.blog.uliejh.cn/snews/14286.htm
- http://m.blog.uliejh.cn/snews/06992.htm
- http://m.blog.uliejh.cn/snews/55382.htm
- http://m.blog.uliejh.cn/snews/176394.htm
- http://m.blog.uliejh.cn/snews/5818366.htm
- http://m.blog.uliejh.cn/snews/28740.htm
- http://m.blog.uliejh.cn/snews/6956.htm
- http://m.blog.uliejh.cn/snews/88357.htm
- http://m.blog.uliejh.cn/snews/4672.htm
- http://m.blog.uliejh.cn/snews/06071.htm
- http://m.blog.uliejh.cn/snews/677766.htm
- http://m.blog.uliejh.cn/snews/63792.htm
- http://m.blog.uliejh.cn/snews/13555.htm
- http://m.blog.uliejh.cn/snews/8606636.htm
- http://m.blog.uliejh.cn/snews/2574219.htm
- http://m.blog.uliejh.cn/snews/998523.htm
- http://m.blog.uliejh.cn/snews/6591.htm
- http://m.blog.uliejh.cn/snews/6047901.htm
- http://m.blog.uliejh.cn/snews/280293.htm
- http://m.blog.uliejh.cn/snews/4654793.htm
- http://m.blog.uliejh.cn/snews/8463.htm
- http://m.blog.uliejh.cn/snews/7733734.htm
- http://m.blog.uliejh.cn/snews/00570.htm
- http://m.blog.uliejh.cn/snews/4576660.htm
- http://m.blog.uliejh.cn/snews/3993386.htm
- http://m.blog.uliejh.cn/snews/933864.htm
- http://m.blog.uliejh.cn/snews/1508279.htm
- http://m.blog.uliejh.cn/snews/2694.htm
- http://m.blog.uliejh.cn/snews/35714.htm
- http://m.blog.uliejh.cn/snews/73095.htm
- http://m.blog.uliejh.cn/snews/7454983.htm
- http://m.blog.uliejh.cn/snews/748499.htm
- http://m.blog.uliejh.cn/snews/00053.htm
- http://m.blog.uliejh.cn/snews/5979445.htm
- http://m.blog.uliejh.cn/snews/016995.htm
- http://m.blog.uliejh.cn/snews/6971818.htm
- http://m.blog.uliejh.cn/snews/8128.htm
- http://m.blog.uliejh.cn/snews/71612.htm
- http://m.blog.uliejh.cn/snews/759905.htm
- http://m.blog.uliejh.cn/snews/0807.htm
- http://m.blog.uliejh.cn/snews/1923733.htm
- http://m.blog.uliejh.cn/snews/815248.htm
- http://m.blog.uliejh.cn/snews/2797495.htm
- http://m.blog.uliejh.cn/snews/3444.htm
- http://m.blog.uliejh.cn/snews/3049.htm
- http://m.blog.uliejh.cn/snews/043015.htm
- http://m.blog.uliejh.cn/snews/67480.htm
- http://m.blog.uliejh.cn/snews/2682.htm
- http://m.blog.uliejh.cn/snews/1313.htm
- http://m.blog.uliejh.cn/snews/071680.htm
- http://m.blog.uliejh.cn/snews/0121205.htm
- http://m.blog.uliejh.cn/snews/086375.htm
- http://m.blog.uliejh.cn/snews/24012.htm
- http://m.blog.uliejh.cn/snews/0975.htm
- http://m.blog.uliejh.cn/snews/727440.htm
- http://m.blog.uliejh.cn/snews/87983.htm
- http://m.blog.uliejh.cn/snews/84876.htm
- http://m.blog.uliejh.cn/snews/5767831.htm
- http://m.blog.uliejh.cn/snews/886436.htm
- http://m.blog.uliejh.cn/snews/4173399.htm
- http://m.blog.uliejh.cn/snews/982000.htm
- http://m.blog.uliejh.cn/snews/7699062.htm
- http://m.blog.uliejh.cn/snews/3603043.htm
- http://m.blog.uliejh.cn/snews/086143.htm
- http://m.blog.uliejh.cn/snews/964450.htm
- http://m.blog.uliejh.cn/snews/39110.htm
- http://m.blog.uliejh.cn/snews/9671.htm
- http://m.blog.uliejh.cn/snews/20625.htm
- http://m.blog.uliejh.cn/snews/4428.htm
- http://m.blog.uliejh.cn/snews/72070.htm
- http://m.blog.uliejh.cn/snews/307047.htm
- http://m.blog.uliejh.cn/snews/5402.htm
- http://m.blog.uliejh.cn/snews/02434.htm
- http://m.blog.uliejh.cn/snews/13546.htm
- http://m.blog.uliejh.cn/snews/5182.htm
- http://m.blog.uliejh.cn/snews/003227.htm
- http://m.blog.uliejh.cn/snews/3154250.htm
- http://m.blog.uliejh.cn/snews/014163.htm
- http://m.blog.uliejh.cn/snews/5628.htm
- http://m.blog.uliejh.cn/snews/76406.htm
- http://m.blog.uliejh.cn/snews/6207810.htm
- http://m.blog.uliejh.cn/snews/83314.htm
- http://m.blog.uliejh.cn/snews/869525.htm
- http://m.blog.uliejh.cn/snews/38776.htm
- http://m.blog.uliejh.cn/snews/7360.htm
- http://m.blog.uliejh.cn/snews/3902216.htm
- http://m.blog.uliejh.cn/snews/9482421.htm
- http://m.blog.uliejh.cn/snews/81100.htm
- http://m.blog.uliejh.cn/snews/3129411.htm
- http://m.blog.uliejh.cn/snews/1115069.htm
- http://m.blog.uliejh.cn/snews/1035402.htm
- http://m.blog.uliejh.cn/snews/51639.htm
- http://m.blog.uliejh.cn/snews/542488.htm
- http://m.blog.uliejh.cn/snews/54651.htm
- http://m.blog.uliejh.cn/snews/528761.htm
- http://m.blog.uliejh.cn/snews/7670.htm
- http://m.blog.uliejh.cn/snews/83896.htm
- http://m.blog.uliejh.cn/snews/3395976.htm

## 项目结构

```
resourcebridge/
├── cmd/                                 # 命令行入口与启动脚本
│   ├── manage.py                        # 统一管理命令（init_db、import_batch、runserver）
│   └── worker.py                        # 后台异步任务进程（链接探测、数据清理）
├── config/                              # 环境配置目录
│   ├── development.yaml                 # 开发环境配置（开启调试、热重载）
│   ├── production.yaml                  # 生产环境配置（关闭调试、指定日志级别）
│   └── settings.py                      # 配置加载逻辑封装
├── core/                                # 核心业务逻辑层
│   ├── indexer.py                       # 资源索引构建与检索算法
│   ├── batch.py                         # 批次管理（创建、导入、状态切换）
│   ├── tag.py                           # 标签系统（增删改查、合并拆分）
│   └── probe.py                         # 链接可用性探测引擎（异步 HTTP 检查）
├── data/                                # 数据存储与迁移目录
│   ├── migrations/                      # SQLite 数据库表结构变更脚本
│   ├── batch_98.csv                     # 第 98 批次原始导入数据（含标题、描述、标签）
│   └── resource.db                      # 默认 SQLite 数据库文件（首次初始化生成）
├── web/                                 # Web 界面与 API 路由
│   ├── static/                          # 静态资源（CSS、JavaScript、图标）
│   ├── templates/                       # Jinja2 模板文件（首页、检索结果、详情页）
│   └── routes.py                        # Flask 路由注册与请求处理
├── tests/                               # 单元测试与集成测试
│   ├── test_indexer.py                  # 索引模块测试用例
│   ├── test_batch.py                    # 批次管理测试用例
│   └── test_probe.py                    # 链接探测测试用例（模拟 HTTP 响应）
├── docs/                                # 完整文档目录（详见文档导航）
│   ├── user_guide.md
│   ├── admin_guide.md
│   ├── api_reference.md
│   └── devops.md
├── requirements.txt                     # Python 依赖列表（Flask、requests、pyyaml 等）
├── Dockerfile                           # 容器化构建文件（基于 python:3.11-slim）
├── docker-compose.yml                   # 本地开发与测试环境编排（含可选 Elasticsearch 服务）
├── LICENSE                              # MIT 许可证全文
└── README.md                            # 项目总览文档（当前文件）
```

## 贡献指南

1. 查阅 issue 列表或自行提交新 issue，说明计划贡献的内容类型（新增功能、缺陷修复、文档改进或新批次数据整理），等待维护者确认工作范围以避免重复劳动。

2. 从主线分支（main）创建新的功能分支，分支命名遵循 `feature/描述` 或 `fix/描述` 的格式，确保代码变更集中在单一职责范围内。

3. 编写或更新对应的单元测试用例，确保测试覆盖率不低于 85%。对于涉及链接导入或探测的变更，需提供模拟数据或 mock 网络请求的测试代码。

4. 提交前运行完整的测试套件（`pytest tests/`）和代码风格检查（`flake8` 与 `black`），确保无回归错误且符合项目编码规范。

5. 发起 Pull Request 至主仓库，在描述中清晰说明变更目的、测试结果以及影响范围。维护者将在 3 个工作日内进行 Review 并给出合并反馈。

## 常见问题

**Q: 导入批次数据时提示 CSV 格式错误，如何解决？**

A: 请确保导入文件为标准的 UTF-8 编码，且列头顺序为 `url,title,description,tags,source_domain`。若使用 Excel 导出 CSV，需另存为「CSV UTF-8」格式以避免 BOM 头干扰。同时检查每个 URL 是否包含协议前缀（http:// 或 https://），否则解析器会拒绝导入。若仍无法解决，可参考 `data/batch_98.csv` 的示例格式进行调整。

**Q: 链接可用性探测任务占用过多网络带宽，能否调整频率？**

A: 可以。在 `config/production.yaml` 中找到 `probe_interval` 参数，默认值为 86400（即 24 小时探测一次）。可根据实际需求调整为 172800（48 小时）或 43200（12 小时）。若完全不需要该功能，可将 `probe_enabled` 设置为 `false` 以禁用后台探测任务。

**Q: 如何迁移现有数据到新的服务器？**

A: 直接复制 `data/resource.db` 文件至新服务器的相同相对路径即可。SQLite 数据库跨平台兼容，无需额外导出导入操作。若同时使用了自定义标签或元数据扩展字段，请确保 `config/settings.py` 中的数据库连接字符串指向正确的文件路径。迁移后建议运行 `python manage.py check_db` 命令执行完整性校验。

## 许可证

MIT

> 外链数量: 250 | 生成时间: 2026-08-24 23:40:21
