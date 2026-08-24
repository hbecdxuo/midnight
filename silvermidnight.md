# LinkVault - 结构化外链资源管理站

LinkVault 是一个面向技术团队与内容运营人员的轻量级外链资源汇总与导航系统，专注于将散落在各处的高价值外部链接进行统一收录、分类标注与快速检索。本项目不提供爬虫或采集功能，而是围绕人工精选的链接清单构建可维护的索引视图，适用于需要长期管理大量引用来源、技术文档索引或行业报告备案的场景。

LinkVault 定位为“链接的 CMS”，而非通用的书签管理器。它解决的核心问题是：当外部链接数量达到数百甚至上千条时，如何通过目录化结构与元数据标签降低查找成本，同时保持原始 URL 的完整可追溯性。项目本身不存储链接内容，仅维护结构化索引，所有外链跳转均直接导向原始资源，符合开源项目中“只做索引、不复制内容”的资源站设计原则。

## 功能概览

**批量链接录入与自动校验**：支持通过文本文件或表单批量提交链接，系统自动检测 URL 可访问性并过滤重复条目，减少人工整理工作量。

**多级目录分类系统**：提供无限层级的自定义分类树，允许按照技术领域、来源站点、时间批次或项目归属对链接进行分组，每个链接可归属多个分类。

**元数据标签与全文检索**：每条链接可附加标题、摘要、关键词标签及备注字段，内置轻量级倒排索引，支持基于标题、标签与备注内容的快速模糊搜索。

**链接状态健康监控**：定时对已收录链接发起 HEAD 请求，标记失效链接（4xx/5xx 状态），并生成变更报告，方便管理员定期清理或更新。

**导入导出与备份机制**：支持 JSON、CSV 及 Markdown 表格格式的链接清单导出，便于与其它系统对接或进行离线备份；导入时自动合并新增与更新。

**访问统计与热度排序**：记录每个链接的点击次数与最近访问时间，提供按热度、收录时间、字母序等多种排序视图，辅助识别高频资源。

**权限分级与操作审计**：区分管理员、编辑者与只读访客三种角色，所有增删改操作记录操作人、时间与变更内容，满足团队协作下的可追溯要求。

**响应式管理面板**：提供适配桌面与移动设备的管理界面，核心操作均通过 RESTful API 完成，方便二次开发或集成至现有后台系统。

## 应用场景

技术文档团队维护外部参考索引。当撰写技术白皮书或项目复盘报告时，需要引用大量外部规范、论文或社区讨论。LinkVault 可以为每篇文档建立独立的链接收藏夹，并按照“已引用”“待审阅”“待弃用”等状态标记，避免在成文过程中遗漏来源或重复核对同一 URL。

开源项目维护者整理社区资源清单。开源项目通常需要在 README 或 Wiki 中列出相关工具、插件或教程链接，但随社区发展这些链接会频繁变动。使用 LinkVault 管理此类资源列表，可以快速生成 Markdown 格式的目录，并定时检查链接有效性，降低维护负担。

行业研究与竞品分析资料库搭建。分析师在调研期间会积累大量行业报告、公司官网及新闻稿链接。LinkVault 的分类树和标签系统能够按主题、时间、地区等多维度组织这些链接，配合备注字段记录核心结论，使调研成果可复用、可交接。

个人知识工作者的阅读清单管理。对于长期跟踪特定技术领域（如数据库内核、前端框架、AI 论文）的开发者，LinkVault 可作为外部阅读列表的后台，按学习阶段或难度等级组织链接，并结合访问统计发现最常查阅的资料，优化个人学习路径。

## 快速开始

以下操作基于 Linux/macOS 环境，要求系统已安装 Git、Node.js 18.x 及以上版本以及 npm 或 yarn。

```bash
# 克隆项目仓库
git clone https://github.com/linkvault/linkvault-core.git
cd linkvault-core

# 安装项目依赖（使用 npm）
npm install

# 复制环境变量模板并填写必要配置
cp .env.example .env
# 编辑 .env 文件，至少设置数据库连接字符串与管理员邮箱

# 初始化数据库结构并创建默认管理员账户
npm run db:init

# 以开发模式启动服务（默认监听 3000 端口）
npm run dev
```

启动后访问 http://localhost:3000 即可进入管理面板。首次登录使用初始化时设置的管理员凭证。生产环境部署请参考 `docs/deployment.md` 使用 PM2 或 Docker 方式运行。

## 安装要求

| 依赖项 | 必需版本 | 说明 |
|--------|----------|------|
| Node.js | 18.x 或 20.x LTS | 运行时环境，推荐使用官方二进制或 nvm 管理 |
| npm | 9.x 及以上 | 依赖管理与脚本执行工具，随 Node.js 一同安装 |
| PostgreSQL | 14.x 及以上 | 主数据库，存储链接元数据、分类树与操作日志 |
| Redis | 7.x 及以上 | 缓存层，用于存放访问统计与临时会话数据（可选，但建议启用） |
| 操作系统 | Linux (Ubuntu 20.04+), macOS 12+, Windows Server 2022 | 支持主流 POSIX 环境，Windows 下需使用 WSL2 |
| 网络环境 | 可访问外网 | 用于链接健康检查与跳转，内网部署需自行配置 DNS 与代理 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|------|------|------------|
| 入门指南 | `docs/getting-started.md` | 如何从零开始安装、配置并启动 LinkVault 服务？第一次登录后应该做什么？ |
| 管理员手册 | `docs/admin-guide.md` | 如何管理分类树、配置健康检查周期、处理失效链接及导入导出数据？ |
| API 参考 | `docs/api-reference.md` | 所有 RESTful 接口的请求参数、响应格式与鉴权方式是什么？如何通过 API 批量操作链接？ |
| 部署运维 | `docs/deployment.md` | 如何配置反向代理、SSL 证书、定时任务及日志轮转？支持哪些容器化部署方案？ |

## 资源列表

- http://m.blog.uliejh.cn/snews/164087.htm
- http://m.blog.uliejh.cn/snews/263688.htm
- http://m.blog.uliejh.cn/snews/929068.htm
- http://m.blog.uliejh.cn/snews/35666.htm
- http://m.blog.uliejh.cn/snews/8406052.htm
- http://m.blog.uliejh.cn/snews/918150.htm
- http://m.blog.uliejh.cn/snews/66869.htm
- http://m.blog.uliejh.cn/snews/7453019.htm
- http://m.blog.uliejh.cn/snews/1239.htm
- http://m.blog.uliejh.cn/snews/5247.htm
- http://m.blog.uliejh.cn/snews/47961.htm
- http://m.blog.uliejh.cn/snews/76269.htm
- http://m.blog.uliejh.cn/snews/34586.htm
- http://m.blog.uliejh.cn/snews/780508.htm
- http://m.blog.uliejh.cn/snews/0772776.htm
- http://m.blog.uliejh.cn/snews/28788.htm
- http://m.blog.uliejh.cn/snews/9885960.htm
- http://m.blog.uliejh.cn/snews/788294.htm
- http://m.blog.uliejh.cn/snews/9192929.htm
- http://m.blog.uliejh.cn/snews/0574.htm
- http://m.blog.uliejh.cn/snews/067689.htm
- http://m.blog.uliejh.cn/snews/9135651.htm
- http://m.blog.uliejh.cn/snews/5441334.htm
- http://m.blog.uliejh.cn/snews/6830.htm
- http://m.blog.uliejh.cn/snews/6544.htm
- http://m.blog.uliejh.cn/snews/326571.htm
- http://m.blog.uliejh.cn/snews/6376.htm
- http://m.blog.uliejh.cn/snews/159653.htm
- http://m.blog.uliejh.cn/snews/2358266.htm
- http://m.blog.uliejh.cn/snews/3590.htm
- http://m.blog.uliejh.cn/snews/320148.htm
- http://m.blog.uliejh.cn/snews/531190.htm
- http://m.blog.uliejh.cn/snews/10954.htm
- http://m.blog.uliejh.cn/snews/759740.htm
- http://m.blog.uliejh.cn/snews/9443697.htm
- http://m.blog.uliejh.cn/snews/6627.htm
- http://m.blog.uliejh.cn/snews/34610.htm
- http://m.blog.uliejh.cn/snews/23209.htm
- http://m.blog.uliejh.cn/snews/376102.htm
- http://m.blog.uliejh.cn/snews/3200.htm
- http://m.blog.uliejh.cn/snews/122216.htm
- http://m.blog.uliejh.cn/snews/0224418.htm
- http://m.blog.uliejh.cn/snews/1318243.htm
- http://m.blog.uliejh.cn/snews/37426.htm
- http://m.blog.uliejh.cn/snews/0838.htm
- http://m.blog.uliejh.cn/snews/3398.htm
- http://m.blog.uliejh.cn/snews/977726.htm
- http://m.blog.uliejh.cn/snews/8113292.htm
- http://m.blog.uliejh.cn/snews/20638.htm
- http://m.blog.uliejh.cn/snews/26176.htm
- http://m.blog.uliejh.cn/snews/8255.htm
- http://m.blog.uliejh.cn/snews/5872.htm
- http://m.blog.uliejh.cn/snews/7368584.htm
- http://m.blog.uliejh.cn/snews/381062.htm
- http://m.blog.uliejh.cn/snews/093259.htm
- http://m.blog.uliejh.cn/snews/2839775.htm
- http://m.blog.uliejh.cn/snews/688828.htm
- http://m.blog.uliejh.cn/snews/21133.htm
- http://m.blog.uliejh.cn/snews/0287.htm
- http://m.blog.uliejh.cn/snews/1668148.htm
- http://m.blog.uliejh.cn/snews/1759.htm
- http://m.blog.uliejh.cn/snews/9707730.htm
- http://m.blog.uliejh.cn/snews/5503085.htm
- http://m.blog.uliejh.cn/snews/81496.htm
- http://m.blog.uliejh.cn/snews/338731.htm
- http://m.blog.uliejh.cn/snews/591093.htm
- http://m.blog.uliejh.cn/snews/83507.htm
- http://m.blog.uliejh.cn/snews/32849.htm
- http://m.blog.uliejh.cn/snews/8858.htm
- http://m.blog.uliejh.cn/snews/4615799.htm
- http://m.blog.uliejh.cn/snews/52354.htm
- http://m.blog.uliejh.cn/snews/833035.htm
- http://m.blog.uliejh.cn/snews/13115.htm
- http://m.blog.uliejh.cn/snews/92822.htm
- http://m.blog.uliejh.cn/snews/721096.htm
- http://m.blog.uliejh.cn/snews/3664624.htm
- http://m.blog.uliejh.cn/snews/4935081.htm
- http://m.blog.uliejh.cn/snews/719426.htm
- http://m.blog.uliejh.cn/snews/6336.htm
- http://m.blog.uliejh.cn/snews/0064.htm
- http://m.blog.uliejh.cn/snews/4193.htm
- http://m.blog.uliejh.cn/snews/34233.htm
- http://m.blog.uliejh.cn/snews/01816.htm
- http://m.blog.uliejh.cn/snews/098523.htm
- http://m.blog.uliejh.cn/snews/8995.htm
- http://m.blog.uliejh.cn/snews/6810.htm
- http://m.blog.uliejh.cn/snews/241447.htm
- http://m.blog.uliejh.cn/snews/38512.htm
- http://m.blog.uliejh.cn/snews/31449.htm
- http://m.blog.uliejh.cn/snews/67874.htm
- http://m.blog.uliejh.cn/snews/04371.htm
- http://m.blog.uliejh.cn/snews/003114.htm
- http://m.blog.uliejh.cn/snews/9269056.htm
- http://m.blog.uliejh.cn/snews/17273.htm
- http://m.blog.uliejh.cn/snews/32673.htm
- http://m.blog.uliejh.cn/snews/246412.htm
- http://m.blog.uliejh.cn/snews/0735117.htm
- http://m.blog.uliejh.cn/snews/8316.htm
- http://m.blog.uliejh.cn/snews/3211702.htm
- http://m.blog.uliejh.cn/snews/767594.htm
- http://m.blog.uliejh.cn/snews/20051.htm
- http://m.blog.uliejh.cn/snews/0627.htm
- http://m.blog.uliejh.cn/snews/555966.htm
- http://m.blog.uliejh.cn/snews/94967.htm
- http://m.blog.uliejh.cn/snews/0789.htm
- http://m.blog.uliejh.cn/snews/8424.htm
- http://m.blog.uliejh.cn/snews/2442.htm
- http://m.blog.uliejh.cn/snews/751249.htm
- http://m.blog.uliejh.cn/snews/690261.htm
- http://m.blog.uliejh.cn/snews/8891.htm
- http://m.blog.uliejh.cn/snews/37966.htm
- http://m.blog.uliejh.cn/snews/33508.htm
- http://m.blog.uliejh.cn/snews/3517780.htm
- http://m.blog.uliejh.cn/snews/38424.htm
- http://m.blog.uliejh.cn/snews/6327.htm
- http://m.blog.uliejh.cn/snews/479642.htm
- http://m.blog.uliejh.cn/snews/630712.htm
- http://m.blog.uliejh.cn/snews/0802.htm
- http://m.blog.uliejh.cn/snews/7708.htm
- http://m.blog.uliejh.cn/snews/74719.htm
- http://m.blog.uliejh.cn/snews/098387.htm
- http://m.blog.uliejh.cn/snews/8778726.htm
- http://m.blog.uliejh.cn/snews/7663408.htm
- http://m.blog.uliejh.cn/snews/5628562.htm
- http://m.blog.uliejh.cn/snews/702883.htm
- http://m.blog.uliejh.cn/snews/897793.htm
- http://m.blog.uliejh.cn/snews/71483.htm
- http://m.blog.uliejh.cn/snews/8744546.htm
- http://m.blog.uliejh.cn/snews/2190034.htm
- http://m.blog.uliejh.cn/snews/6120.htm
- http://m.blog.uliejh.cn/snews/9502745.htm
- http://m.blog.uliejh.cn/snews/34316.htm
- http://m.blog.uliejh.cn/snews/36442.htm
- http://m.blog.uliejh.cn/snews/616939.htm
- http://m.blog.uliejh.cn/snews/871576.htm
- http://m.blog.uliejh.cn/snews/2299260.htm
- http://m.blog.uliejh.cn/snews/06875.htm
- http://m.blog.uliejh.cn/snews/29389.htm
- http://m.blog.uliejh.cn/snews/55010.htm
- http://m.blog.uliejh.cn/snews/5618156.htm
- http://m.blog.uliejh.cn/snews/3145335.htm
- http://m.blog.uliejh.cn/snews/1296.htm
- http://m.blog.uliejh.cn/snews/797606.htm
- http://m.blog.uliejh.cn/snews/8255096.htm
- http://m.blog.uliejh.cn/snews/31737.htm
- http://m.blog.uliejh.cn/snews/73325.htm
- http://m.blog.uliejh.cn/snews/134741.htm
- http://m.blog.uliejh.cn/snews/8721.htm
- http://m.blog.uliejh.cn/snews/877016.htm
- http://m.blog.uliejh.cn/snews/8428473.htm
- http://m.blog.uliejh.cn/snews/28648.htm
- http://m.blog.uliejh.cn/snews/763820.htm
- http://m.blog.uliejh.cn/snews/824715.htm
- http://m.blog.uliejh.cn/snews/9539295.htm
- http://m.blog.uliejh.cn/snews/052481.htm
- http://m.blog.uliejh.cn/snews/3710.htm
- http://m.blog.uliejh.cn/snews/68608.htm
- http://m.blog.uliejh.cn/snews/1487.htm
- http://m.blog.uliejh.cn/snews/980406.htm
- http://m.blog.uliejh.cn/snews/8973932.htm
- http://m.blog.uliejh.cn/snews/5828457.htm
- http://m.blog.uliejh.cn/snews/7988624.htm
- http://m.blog.uliejh.cn/snews/7491267.htm
- http://m.blog.uliejh.cn/snews/681741.htm
- http://m.blog.uliejh.cn/snews/1774580.htm
- http://m.blog.uliejh.cn/snews/3783193.htm
- http://m.blog.uliejh.cn/snews/34381.htm
- http://m.blog.uliejh.cn/snews/2251.htm
- http://m.blog.uliejh.cn/snews/571995.htm
- http://m.blog.uliejh.cn/snews/593638.htm
- http://m.blog.uliejh.cn/snews/75279.htm
- http://m.blog.uliejh.cn/snews/296367.htm
- http://m.blog.uliejh.cn/snews/57158.htm
- http://m.blog.uliejh.cn/snews/3994351.htm
- http://m.blog.uliejh.cn/snews/159518.htm
- http://m.blog.uliejh.cn/snews/0332411.htm
- http://m.blog.uliejh.cn/snews/3111.htm
- http://m.blog.uliejh.cn/snews/922766.htm
- http://m.blog.uliejh.cn/snews/03793.htm
- http://m.blog.uliejh.cn/snews/2531.htm
- http://m.blog.uliejh.cn/snews/5118687.htm
- http://m.blog.uliejh.cn/snews/0728.htm
- http://m.blog.uliejh.cn/snews/71265.htm
- http://m.blog.uliejh.cn/snews/6722114.htm
- http://m.blog.uliejh.cn/snews/7021334.htm
- http://m.blog.uliejh.cn/snews/6725926.htm
- http://m.blog.uliejh.cn/snews/1138.htm
- http://m.blog.uliejh.cn/snews/0624820.htm
- http://m.blog.uliejh.cn/snews/00968.htm
- http://m.blog.uliejh.cn/snews/4739.htm
- http://m.blog.uliejh.cn/snews/36506.htm
- http://m.blog.uliejh.cn/snews/40860.htm
- http://m.blog.uliejh.cn/snews/291371.htm
- http://m.blog.uliejh.cn/snews/2981112.htm
- http://m.blog.uliejh.cn/snews/879319.htm
- http://m.blog.uliejh.cn/snews/5416597.htm
- http://m.blog.uliejh.cn/snews/113782.htm
- http://m.blog.uliejh.cn/snews/0031.htm
- http://m.blog.uliejh.cn/snews/74439.htm
- http://m.blog.uliejh.cn/snews/21841.htm
- http://m.blog.uliejh.cn/snews/402872.htm
- http://m.blog.uliejh.cn/snews/0458366.htm
- http://m.blog.uliejh.cn/snews/14672.htm
- http://m.blog.uliejh.cn/snews/792329.htm
- http://m.blog.uliejh.cn/snews/1058.htm
- http://m.blog.uliejh.cn/snews/965045.htm
- http://m.blog.uliejh.cn/snews/527173.htm
- http://m.blog.uliejh.cn/snews/092739.htm
- http://m.blog.uliejh.cn/snews/939587.htm
- http://m.blog.uliejh.cn/snews/4314.htm
- http://m.blog.uliejh.cn/snews/54113.htm
- http://m.blog.uliejh.cn/snews/599232.htm
- http://m.blog.uliejh.cn/snews/93436.htm
- http://m.blog.uliejh.cn/snews/490035.htm
- http://m.blog.uliejh.cn/snews/6590.htm
- http://m.blog.uliejh.cn/snews/0185843.htm
- http://m.blog.uliejh.cn/snews/458742.htm
- http://m.blog.uliejh.cn/snews/1835.htm
- http://m.blog.uliejh.cn/snews/34927.htm
- http://m.blog.uliejh.cn/snews/43054.htm
- http://m.blog.uliejh.cn/snews/1961226.htm
- http://m.blog.uliejh.cn/snews/721316.htm
- http://m.blog.uliejh.cn/snews/8677.htm
- http://m.blog.uliejh.cn/snews/4814.htm
- http://m.blog.uliejh.cn/snews/466144.htm
- http://m.blog.uliejh.cn/snews/119381.htm
- http://m.blog.uliejh.cn/snews/17459.htm
- http://m.blog.uliejh.cn/snews/5729300.htm
- http://m.blog.uliejh.cn/snews/3674423.htm
- http://m.blog.uliejh.cn/snews/35888.htm
- http://m.blog.uliejh.cn/snews/4638133.htm
- http://m.blog.uliejh.cn/snews/160009.htm
- http://m.blog.uliejh.cn/snews/3825.htm
- http://m.blog.uliejh.cn/snews/52511.htm
- http://m.blog.uliejh.cn/snews/8619.htm
- http://m.blog.uliejh.cn/snews/0268.htm
- http://m.blog.uliejh.cn/snews/5484938.htm
- http://m.blog.uliejh.cn/snews/90333.htm
- http://m.blog.uliejh.cn/snews/5509649.htm
- http://m.blog.uliejh.cn/snews/17809.htm
- http://m.blog.uliejh.cn/snews/7278.htm
- http://m.blog.uliejh.cn/snews/0658.htm
- http://m.blog.uliejh.cn/snews/6342.htm
- http://m.blog.uliejh.cn/snews/6474604.htm
- http://m.blog.uliejh.cn/snews/6099.htm
- http://m.blog.uliejh.cn/snews/5720.htm
- http://m.blog.uliejh.cn/snews/85817.htm
- http://m.blog.uliejh.cn/snews/3636403.htm
- http://m.blog.uliejh.cn/snews/0087431.htm
- http://m.blog.uliejh.cn/snews/6674308.htm

## 项目结构

```
linkvault-core/
├── src/
│   ├── api/                        # RESTful API 路由与控制器
│   │   ├── routes/                 # 按资源划分的路由定义（links, categories, tags, health）
│   │   └── middleware/             # 鉴权、日志、速率限制与错误处理中间件
│   ├── core/                       # 核心业务逻辑
│   │   ├── link-manager/           # 链接增删改查、校验、去重与状态更新
│   │   ├── category-tree/          # 分类树的 CRUD 与层级重算
│   │   ├── health-checker/         # 定时任务调度、HTTP 状态检测与失效通知
│   │   └── stats-collector/        # 点击计数、访问时间戳与热度排序算法
│   ├── db/                         # 数据库相关
│   │   ├── migrations/             # PostgreSQL 结构变更脚本（按时间戳命名）
│   │   ├── models/                 # Sequelize 或 Prisma 实体定义（Link, Category, Log）
│   │   └── seeders/                # 初始分类与默认管理员数据填充
│   ├── cache/                      # Redis 缓存封装（会话、统计聚合、高频查询）
│   └── utils/                      # 通用工具函数（URL 规范化、日志格式化、环境变量校验）
├── config/                         # 环境配置文件（development, staging, production）
├── docs/                           # 完整文档源文件（Markdown + 图表）
├── tests/                          # 单元测试与集成测试（Jest / Mocha）
│   ├── unit/                       # 独立函数与工具测试
│   └── integration/                # API 端到端测试与数据库事务回滚测试
├── scripts/                        # 运维脚本（备份、恢复、数据迁移、健康检查手动触发）
├── public/                         # 静态资源（管理面板前端构建产物、favicon、robots.txt）
├── .env.example                    # 环境变量配置模板
├── .eslintrc.js                    # ESLint 规则（Airbnb 风格定制）
├── .prettierrc                     # 代码格式化配置
├── package.json                    # npm 依赖清单与脚本命令
├── Dockerfile                      # 多阶段构建镜像定义（生产环境）
└── README.md                       # 项目入口文档（本文件）
```

## 贡献指南

1. 阅读项目行为准则（CODE_OF_CONDUCT.md）与贡献者许可协议（CLA），确认同意后 fork 本仓库至个人账户。

2. 在本地开发环境中运行 `npm run dev` 确保现有测试全部通过，然后基于 `main` 分支创建新的功能分支，分支命名遵循 `feature/描述` 或 `fix/描述` 格式。

3. 提交代码前执行 `npm run lint` 与 `npm run test` 保证代码风格统一且未引入回归问题；对于新增功能，需同步编写至少覆盖核心路径的单元测试或集成测试。

4. 发起 Pull Request 至 `main` 分支，在 PR 描述中清晰说明修改动机、实现方案及可能的兼容性影响；PR 需要至少一位项目维护者审阅通过后方可合并。

5. 文档类更新（包括修正拼写错误、补充示例、翻译）可直接提交 PR，无需经过严格的功能测试流程，但需确保文档编译无误且链接有效。

## 常见问题

**Q: 系统能自动抓取链接对应的网页标题和摘要信息吗？**

A: 当前版本不内置任何爬虫或内容抓取功能，主要原因是避免法律风险与目标服务器的负载压力。推荐用户在录入链接时手动填写标题与备注，或通过浏览器扩展配合 API 实现半自动填充。未来版本可能提供基于 Open Graph 或 meta 标签的可选元数据补全，但此功能默认关闭，需要管理员显式启用。

**Q: 健康检查对于需要登录或带有反爬机制的链接如何处理？**

A: 健康检查默认仅发送不带 cookie 的 HEAD 请求，并跟随最多 5 次 3xx 重定向。对于需要登录态或验证码的页面，系统会将其标记为“需人工确认”状态，不会误判为失效。管理员可在分类或标签中单独设置检查策略，例如跳过某些域名或增加超时时间。更复杂的检查逻辑建议通过外部监控系统实现，LinkVault 只作为状态汇总入口。

## 许可证

MIT

> 外链数量: 250 | 生成时间: 2026-08-24 23:40:21
