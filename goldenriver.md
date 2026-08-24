# WebIndex 技术资源导航站

WebIndex 是一个面向技术研究者与开发者的轻量级外链资源汇总系统，专注于对分散在互联网各处的深度技术文章、行业报告与工程实践案例进行结构化收录与索引。项目本身不存储任何原始内容，仅提供 URL 元数据管理与分类导航能力，适用于搭建个人或团队内部的技术知识库入口。

目标用户包括技术团队的知识管理者、开源项目维护者、技术内容创作者以及希望系统化跟进特定领域动态的研发人员。WebIndex 帮助用户将零散的书签与收藏转化为可检索、可分类、可分享的导航体系，降低信息遗忘与重复查找的成本。

## 功能概览

批量链接导入与去重 支持从文本文件或剪贴板批量导入 URL 列表，系统自动识别重复条目并标记已有记录，避免资源冗余堆积。

自定义分类标签体系 允许为每个链接添加多级标签（如 "backend/performance"、"frontend/build-tool"），并支持基于标签树的快速筛选与浏览。

全文元数据抓取 后台异步抓取目标页面的标题、描述与关键词信息，填充资源卡片的基础字段，减少手动录入工作量。

多维度检索与过滤 提供按标题关键词、域名、标签、导入时间等多条件组合检索，支持结果排序与分页浏览。

收藏与阅读列表 用户可将重要资源加入个人收藏夹或待读列表，支持标记阅读状态与添加个人笔记。

定期可用性检查 内置链接有效性巡检任务，定期检测已收录 URL 的 HTTP 状态码，自动标记失效链接并生成报告。

数据导出与分享 支持将选定分类或全部链接导出为 JSON、CSV 或纯文本列表，便于备份或与团队成员共享。

访问统计与热度排序 记录每个资源的点击次数与最近访问时间，提供按热度排序的"热门资源"视图。

## 应用场景

技术团队内部知识库建设 团队管理者可将长期积累的工程博客、故障复盘报告、性能调优案例集中录入 WebIndex，按服务模块或技术栈打标，新成员入职时可通过标签快速了解团队所关注的技术脉络。

个人技术阅读流管理 开发者每天浏览大量 Hacker News、技术周刊、GitHub 趋势等来源的文章，可将有价值的单篇链接即时存入 WebIndex，后续按主题整理成自己的"最佳实践手册"。

开源项目文档导航 开源项目维护者将项目中涉及的依赖库文档、设计决策说明、社区讨论 thread、性能测试报告等外链统一收录，避免重要参考链接散落在 issue 或聊天记录中难以追溯。

技术培训与课程资料包 培训机构或技术导师可将课程涉及的延伸阅读材料、官方规范文档、视频教程地址等资源汇总为专题列表，学员通过统一入口即可获取全部参考资料。

## 快速开始

以下命令演示了如何在本地环境克隆代码仓库、安装依赖并启动开发服务器。

```bash
# 克隆代码仓库
git clone https://github.com/webindex/webindex.git
cd webindex

# 安装项目依赖
npm install

# 初始化本地配置文件
cp .env.example .env

# 启动开发服务器（默认监听 3000 端口）
npm run dev
```

生产环境部署请参考 `deploy` 目录下的 Dockerfile 与 compose 配置，或使用 `npm run build` 生成静态产物后配合 Nginx 托管。

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|---|---|---|
| Node.js | >= 18.0.0 | 运行时环境，需支持 ES2022 特性 |
| npm | >= 9.0.0 或 yarn >= 1.22 | 包管理器，用于安装依赖与执行脚本 |
| PostgreSQL | >= 14.0 | 主数据库，存储资源元数据与用户数据 |
| Redis | >= 6.2 | 缓存会话与异步任务队列（可选，生产环境推荐） |
| nginx | >= 1.20 | 生产环境反向代理与静态资源服务（推荐） |
| git | >= 2.30 | 版本控制，用于克隆与更新代码 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|---|---|---|
| 使用手册 | /docs/usage/ | 如何添加链接、打标签、导入导出数据以及使用检索功能 |
| 部署指南 | /docs/deployment/ | 如何配置生产环境、数据库迁移、SSL 证书与定时任务 |
| API 参考 | /docs/api/ | 后端 RESTful 接口的请求/响应格式、鉴权方式与错误码说明 |
| 架构设计 | /docs/architecture/ | 系统模块划分、数据流、异步任务队列设计与扩展方案 |

## 资源列表

- http://m.wap.uliejh.cn/bnews/3610.htm
- http://m.wap.uliejh.cn/bnews/8294.htm
- http://m.wap.uliejh.cn/bnews/24790.htm
- http://m.wap.uliejh.cn/bnews/4234098.htm
- http://m.wap.uliejh.cn/bnews/798013.htm
- http://m.wap.uliejh.cn/bnews/0563093.htm
- http://m.wap.uliejh.cn/bnews/44697.htm
- http://m.wap.uliejh.cn/bnews/915518.htm
- http://m.wap.uliejh.cn/bnews/53261.htm
- http://m.wap.uliejh.cn/bnews/7979148.htm
- http://m.wap.uliejh.cn/bnews/2376998.htm
- http://m.wap.uliejh.cn/bnews/902062.htm
- http://m.wap.uliejh.cn/bnews/750785.htm
- http://m.wap.uliejh.cn/bnews/1737567.htm
- http://m.wap.uliejh.cn/bnews/6063.htm
- http://m.wap.uliejh.cn/bnews/4909.htm
- http://m.wap.uliejh.cn/bnews/447622.htm
- http://m.wap.uliejh.cn/bnews/45326.htm
- http://m.wap.uliejh.cn/bnews/0537174.htm
- http://m.wap.uliejh.cn/bnews/8975.htm
- http://m.wap.uliejh.cn/bnews/671765.htm
- http://m.wap.uliejh.cn/bnews/144112.htm
- http://m.wap.uliejh.cn/bnews/9817658.htm
- http://m.wap.uliejh.cn/bnews/707711.htm
- http://m.wap.uliejh.cn/bnews/2430434.htm
- http://m.wap.uliejh.cn/bnews/10299.htm
- http://m.wap.uliejh.cn/bnews/4207154.htm
- http://m.wap.uliejh.cn/bnews/59313.htm
- http://m.wap.uliejh.cn/bnews/30198.htm
- http://m.wap.uliejh.cn/bnews/9954.htm
- http://m.wap.uliejh.cn/bnews/2367092.htm
- http://m.wap.uliejh.cn/bnews/6045.htm
- http://m.wap.uliejh.cn/bnews/937774.htm
- http://m.wap.uliejh.cn/bnews/7447.htm
- http://m.wap.uliejh.cn/bnews/15535.htm
- http://m.wap.uliejh.cn/bnews/2014.htm
- http://m.wap.uliejh.cn/bnews/2582948.htm
- http://m.wap.uliejh.cn/bnews/4666.htm
- http://m.wap.uliejh.cn/bnews/77441.htm
- http://m.wap.uliejh.cn/bnews/8938.htm
- http://m.wap.uliejh.cn/bnews/35366.htm
- http://m.wap.uliejh.cn/bnews/09848.htm
- http://m.wap.uliejh.cn/bnews/662102.htm
- http://m.wap.uliejh.cn/bnews/3367890.htm
- http://m.wap.uliejh.cn/bnews/456459.htm
- http://m.wap.uliejh.cn/bnews/377316.htm
- http://m.wap.uliejh.cn/bnews/956282.htm
- http://m.wap.uliejh.cn/bnews/43285.htm
- http://m.wap.uliejh.cn/bnews/8763303.htm
- http://m.wap.uliejh.cn/bnews/3928019.htm
- http://m.wap.uliejh.cn/bnews/181502.htm
- http://m.wap.uliejh.cn/bnews/8501.htm
- http://m.wap.uliejh.cn/bnews/5600.htm
- http://m.wap.uliejh.cn/bnews/9245994.htm
- http://m.wap.uliejh.cn/bnews/3137438.htm
- http://m.wap.uliejh.cn/bnews/26882.htm
- http://m.wap.uliejh.cn/bnews/418074.htm
- http://m.wap.uliejh.cn/bnews/5772338.htm
- http://m.wap.uliejh.cn/bnews/00689.htm
- http://m.wap.uliejh.cn/bnews/718005.htm
- http://m.wap.uliejh.cn/bnews/5169397.htm
- http://m.wap.uliejh.cn/bnews/4358.htm
- http://m.wap.uliejh.cn/bnews/4747.htm
- http://m.wap.uliejh.cn/bnews/83827.htm
- http://m.wap.uliejh.cn/bnews/9989325.htm
- http://m.wap.uliejh.cn/bnews/8536525.htm
- http://m.wap.uliejh.cn/bnews/0507.htm
- http://m.wap.uliejh.cn/bnews/90997.htm
- http://m.wap.uliejh.cn/bnews/3937.htm
- http://m.wap.uliejh.cn/bnews/6334387.htm
- http://m.wap.uliejh.cn/bnews/085087.htm
- http://m.wap.uliejh.cn/bnews/62874.htm
- http://m.wap.uliejh.cn/bnews/98640.htm
- http://m.wap.uliejh.cn/bnews/6466903.htm
- http://m.wap.uliejh.cn/bnews/6540.htm
- http://m.wap.uliejh.cn/bnews/797896.htm
- http://m.wap.uliejh.cn/bnews/8188045.htm
- http://m.wap.uliejh.cn/bnews/4589106.htm
- http://m.wap.uliejh.cn/bnews/884766.htm
- http://m.wap.uliejh.cn/bnews/932147.htm
- http://m.wap.uliejh.cn/bnews/95055.htm
- http://m.wap.uliejh.cn/bnews/8136.htm
- http://m.wap.uliejh.cn/bnews/4574.htm
- http://m.wap.uliejh.cn/bnews/81890.htm
- http://m.wap.uliejh.cn/bnews/2868272.htm
- http://m.wap.uliejh.cn/bnews/4819396.htm
- http://m.wap.uliejh.cn/bnews/7142355.htm
- http://m.wap.uliejh.cn/bnews/6953845.htm
- http://m.wap.uliejh.cn/bnews/3873.htm
- http://m.wap.uliejh.cn/bnews/4151976.htm
- http://m.wap.uliejh.cn/bnews/6270392.htm
- http://m.wap.uliejh.cn/bnews/0261.htm
- http://m.wap.uliejh.cn/bnews/851128.htm
- http://m.wap.uliejh.cn/bnews/980465.htm
- http://m.wap.uliejh.cn/bnews/7464989.htm
- http://m.wap.uliejh.cn/bnews/6269.htm
- http://m.wap.uliejh.cn/bnews/603986.htm
- http://m.wap.uliejh.cn/bnews/3171.htm
- http://m.wap.uliejh.cn/bnews/252425.htm
- http://m.wap.uliejh.cn/bnews/44014.htm
- http://m.wap.uliejh.cn/bnews/2470.htm
- http://m.wap.uliejh.cn/bnews/647881.htm
- http://m.wap.uliejh.cn/bnews/197475.htm
- http://m.wap.uliejh.cn/bnews/0526.htm
- http://m.wap.uliejh.cn/bnews/36732.htm
- http://m.wap.uliejh.cn/bnews/83928.htm
- http://m.wap.uliejh.cn/bnews/87278.htm
- http://m.wap.uliejh.cn/bnews/9157.htm
- http://m.wap.uliejh.cn/bnews/96213.htm
- http://m.wap.uliejh.cn/bnews/4137375.htm
- http://m.wap.uliejh.cn/bnews/40117.htm
- http://m.wap.uliejh.cn/bnews/8003334.htm
- http://m.wap.uliejh.cn/bnews/85661.htm
- http://m.wap.uliejh.cn/bnews/5946.htm
- http://m.wap.uliejh.cn/bnews/52138.htm
- http://m.wap.uliejh.cn/bnews/9484279.htm
- http://m.wap.uliejh.cn/bnews/2531203.htm
- http://m.wap.uliejh.cn/bnews/98047.htm
- http://m.wap.uliejh.cn/bnews/9170.htm
- http://m.wap.uliejh.cn/bnews/5981.htm
- http://m.wap.uliejh.cn/bnews/35035.htm
- http://m.wap.uliejh.cn/bnews/9002.htm
- http://m.wap.uliejh.cn/bnews/2836416.htm
- http://m.wap.uliejh.cn/bnews/4713549.htm
- http://m.wap.uliejh.cn/bnews/8277433.htm
- http://m.wap.uliejh.cn/bnews/568443.htm
- http://m.wap.uliejh.cn/bnews/566890.htm
- http://m.wap.uliejh.cn/bnews/0736.htm
- http://m.wap.uliejh.cn/bnews/1017.htm
- http://m.wap.uliejh.cn/bnews/6872992.htm
- http://m.wap.uliejh.cn/bnews/2753164.htm
- http://m.wap.uliejh.cn/bnews/86002.htm
- http://m.wap.uliejh.cn/bnews/20010.htm
- http://m.wap.uliejh.cn/bnews/9274077.htm
- http://m.wap.uliejh.cn/bnews/365443.htm
- http://m.wap.uliejh.cn/bnews/47058.htm
- http://m.wap.uliejh.cn/bnews/47232.htm
- http://m.wap.uliejh.cn/bnews/568952.htm
- http://m.wap.uliejh.cn/bnews/4554790.htm
- http://m.wap.uliejh.cn/bnews/1764574.htm
- http://m.wap.uliejh.cn/bnews/5541741.htm
- http://m.wap.uliejh.cn/bnews/522855.htm
- http://m.wap.uliejh.cn/bnews/759674.htm
- http://m.wap.uliejh.cn/bnews/769933.htm
- http://m.wap.uliejh.cn/bnews/178352.htm
- http://m.wap.uliejh.cn/bnews/00198.htm
- http://m.wap.uliejh.cn/bnews/2788338.htm
- http://m.wap.uliejh.cn/bnews/1025474.htm
- http://m.wap.uliejh.cn/bnews/0360744.htm
- http://m.wap.uliejh.cn/bnews/8565406.htm
- http://m.wap.uliejh.cn/bnews/9870860.htm
- http://m.wap.uliejh.cn/bnews/2037.htm
- http://m.wap.uliejh.cn/bnews/18915.htm
- http://m.wap.uliejh.cn/bnews/65082.htm
- http://m.wap.uliejh.cn/bnews/5775.htm
- http://m.wap.uliejh.cn/bnews/4764382.htm
- http://m.wap.uliejh.cn/bnews/408929.htm
- http://m.wap.uliejh.cn/bnews/7516111.htm
- http://m.wap.uliejh.cn/bnews/87231.htm
- http://m.wap.uliejh.cn/bnews/4629854.htm
- http://m.wap.uliejh.cn/bnews/8816305.htm
- http://m.wap.uliejh.cn/bnews/22604.htm
- http://m.wap.uliejh.cn/bnews/265964.htm
- http://m.wap.uliejh.cn/bnews/614225.htm
- http://m.wap.uliejh.cn/bnews/26306.htm
- http://m.wap.uliejh.cn/bnews/203424.htm
- http://m.wap.uliejh.cn/bnews/8817413.htm
- http://m.wap.uliejh.cn/bnews/3996.htm
- http://m.wap.uliejh.cn/bnews/67862.htm
- http://m.wap.uliejh.cn/bnews/3265.htm
- http://m.wap.uliejh.cn/bnews/525422.htm
- http://m.wap.uliejh.cn/bnews/13598.htm
- http://m.wap.uliejh.cn/bnews/5377218.htm
- http://m.wap.uliejh.cn/bnews/15773.htm
- http://m.wap.uliejh.cn/bnews/748512.htm
- http://m.wap.uliejh.cn/bnews/73767.htm
- http://m.wap.uliejh.cn/bnews/2693368.htm
- http://m.wap.uliejh.cn/bnews/1080.htm
- http://m.wap.uliejh.cn/bnews/2277.htm
- http://m.wap.uliejh.cn/bnews/4832691.htm
- http://m.wap.uliejh.cn/bnews/50281.htm
- http://m.wap.uliejh.cn/bnews/935774.htm
- http://m.wap.uliejh.cn/bnews/0610.htm
- http://m.wap.uliejh.cn/bnews/82903.htm
- http://m.wap.uliejh.cn/bnews/95650.htm
- http://m.wap.uliejh.cn/bnews/21202.htm
- http://m.wap.uliejh.cn/bnews/3898164.htm
- http://m.wap.uliejh.cn/bnews/712939.htm
- http://m.wap.uliejh.cn/bnews/90010.htm
- http://m.wap.uliejh.cn/bnews/411757.htm
- http://m.wap.uliejh.cn/bnews/044916.htm
- http://m.wap.uliejh.cn/bnews/8327619.htm
- http://m.wap.uliejh.cn/bnews/6673338.htm
- http://m.wap.uliejh.cn/bnews/47267.htm
- http://m.wap.uliejh.cn/bnews/41322.htm
- http://m.wap.uliejh.cn/bnews/01489.htm
- http://m.wap.uliejh.cn/bnews/2265405.htm
- http://m.wap.uliejh.cn/bnews/253434.htm
- http://m.wap.uliejh.cn/bnews/5356030.htm
- http://m.wap.uliejh.cn/bnews/93940.htm
- http://m.wap.uliejh.cn/bnews/472497.htm
- http://m.wap.uliejh.cn/bnews/8081.htm
- http://m.wap.uliejh.cn/bnews/6535650.htm
- http://m.wap.uliejh.cn/bnews/957397.htm
- http://m.wap.uliejh.cn/bnews/2565.htm
- http://m.wap.uliejh.cn/bnews/8993575.htm
- http://m.wap.uliejh.cn/bnews/31231.htm
- http://m.wap.uliejh.cn/bnews/943795.htm
- http://m.wap.uliejh.cn/bnews/6725.htm
- http://m.wap.uliejh.cn/bnews/614441.htm
- http://m.wap.uliejh.cn/bnews/2549502.htm
- http://m.wap.uliejh.cn/bnews/3186246.htm
- http://m.wap.uliejh.cn/bnews/342874.htm
- http://m.wap.uliejh.cn/bnews/4707.htm
- http://m.wap.uliejh.cn/bnews/142391.htm
- http://m.wap.uliejh.cn/bnews/0862397.htm
- http://m.wap.uliejh.cn/bnews/9184820.htm
- http://m.wap.uliejh.cn/bnews/3507967.htm
- http://m.wap.uliejh.cn/bnews/344881.htm
- http://m.wap.uliejh.cn/bnews/38137.htm
- http://m.wap.uliejh.cn/bnews/0890228.htm
- http://m.wap.uliejh.cn/bnews/2097.htm
- http://m.wap.uliejh.cn/bnews/1454.htm
- http://m.wap.uliejh.cn/bnews/8436.htm
- http://m.wap.uliejh.cn/bnews/9062.htm
- http://m.wap.uliejh.cn/bnews/412519.htm
- http://m.wap.uliejh.cn/bnews/1111.htm
- http://m.wap.uliejh.cn/bnews/80971.htm
- http://m.wap.uliejh.cn/bnews/506502.htm
- http://m.wap.uliejh.cn/bnews/0514.htm
- http://m.wap.uliejh.cn/bnews/5140268.htm
- http://m.wap.uliejh.cn/bnews/66449.htm
- http://m.wap.uliejh.cn/bnews/17363.htm
- http://m.wap.uliejh.cn/bnews/35194.htm
- http://m.wap.uliejh.cn/bnews/67453.htm
- http://m.wap.uliejh.cn/bnews/426262.htm
- http://m.wap.uliejh.cn/bnews/510605.htm
- http://m.wap.uliejh.cn/bnews/17831.htm
- http://m.wap.uliejh.cn/bnews/62715.htm
- http://m.wap.uliejh.cn/bnews/45872.htm
- http://m.wap.uliejh.cn/bnews/3380.htm
- http://m.wap.uliejh.cn/bnews/291116.htm
- http://m.wap.uliejh.cn/bnews/7487.htm
- http://m.wap.uliejh.cn/bnews/5303.htm
- http://m.wap.uliejh.cn/bnews/664436.htm
- http://m.wap.uliejh.cn/bnews/1371.htm
- http://m.wap.uliejh.cn/bnews/9148312.htm
- http://m.wap.uliejh.cn/bnews/417844.htm
- http://m.wap.uliejh.cn/bnews/9172986.htm
- http://m.wap.uliejh.cn/bnews/1084.htm

## 项目结构

```
webindex/
├── src/                           # 核心源代码目录
│   ├── api/                       # RESTful API 路由与控制器
│   │   ├── v1/                    # API 版本 v1 实现
│   │   │   ├── links/             # 链接资源的 CRUD 与检索接口
│   │   │   ├── tags/              # 标签管理接口
│   │   │   └── stats/             # 访问统计与热度计算接口
│   │   └── middleware/            # 鉴权、日志、限流中间件
│   ├── services/                  # 业务逻辑层
│   │   ├── crawler/               # 元数据抓取服务（基于 puppeteer 与 cheerio）
│   │   ├── checker/               # 链接可用性巡检服务（定时任务）
│   │   └── exporter/              # 数据导出服务（JSON/CSV 生成）
│   ├── models/                    # 数据库模型定义（Prisma ORM）
│   │   ├── link.prisma            # 链接表结构定义
│   │   ├── tag.prisma             # 标签表与关联表定义
│   │   └── user.prisma            # 用户与收藏表定义
│   ├── web/                       # 前端 Web 界面（React + Next.js）
│   │   ├── pages/                 # 页面路由组件
│   │   ├── components/            # 可复用 UI 组件（表格、筛选器、卡片）
│   │   └── hooks/                 # 自定义 React Hooks（数据请求与状态管理）
│   └── utils/                     # 通用工具函数（日志、加密、验证、日期处理）
├── config/                        # 环境配置与运行参数
│   ├── default.json               # 默认配置（端口、数据库连接池、超时阈值）
│   ├── production.json            # 生产环境覆盖配置
│   └── development.json           # 开发环境覆盖配置
├── tests/                         # 单元测试与集成测试
│   ├── unit/                      # 服务层与工具函数单元测试（Jest）
│   └── integration/               # API 端到端测试（Supertest）
├── scripts/                       # 运维与开发辅助脚本
│   ├── migrate-db.sh              # 数据库迁移脚本
│   ├── seed-data.js               # 初始测试数据填充
│   └── health-check.js            # 系统健康状态检查脚本
├── docs/                          # 项目文档（使用手册、API 参考、部署指南）
├── deploy/                        # 生产部署配置
│   ├── Dockerfile                 # 容器镜像构建定义
│   ├── docker-compose.yml         # 多容器编排（app + postgres + redis）
│   └── nginx.conf                 # 反向代理与静态资源缓存配置
├── .env.example                   # 环境变量模板文件
├── .gitignore                     # Git 版本忽略规则
├── package.json                   # npm 依赖清单与脚本定义
└── README.md                      # 项目入口说明文档（本文件）
```

## 贡献指南

提交问题报告与功能请求 请先查阅已有 issue 列表避免重复，新建 issue 时使用提供的模板清晰描述复现步骤、预期行为与实际表现，并附上环境信息与相关日志。

代码贡献流程 从 `main` 分支拉取最新代码，创建以 `feature/` 或 `fix/` 为前缀的专题分支，完成开发后确保所有测试通过（`npm run test`），并提交包含清晰 commit 信息的 pull request。

文档完善与翻译 欢迎补充使用示例、API 使用场景说明以及将文档翻译为其他语言。文档变更需同步更新 `docs/` 目录下对应的 markdown 文件，并保持与代码实际行为一致。

链接资源推荐 如果您发现高质量的技术文章、工具或报告，可通过项目内置的"推荐链接"功能提交，经审核后纳入公共资源库。推荐时请提供简要的推荐理由与建议标签。

测试用例补充 新功能或修复应附带对应的测试用例，单元测试覆盖核心逻辑，集成测试覆盖 API 边界场景。测试代码需与功能代码在同一 pull request 中提交。

## 常见问题

Q: 系统支持导入的最大链接数量是多少？性能是否有瓶颈？

A: 当前版本在 PostgreSQL 数据库下，单表可稳定支持百万级链接记录。检索性能依赖数据库索引（已对标题、标签、创建时间等字段建立联合索引）。如果链接数量超过 50 万条，建议启用 Redis 缓存热点查询结果，并在配置中调整巡检任务的并发数与超时阈值。

Q: 元数据抓取服务是否会频繁被目标网站封禁 IP？

A: 系统默认启用请求间隔控制（最小间隔 500ms），并支持配置代理池轮转。抓取时使用标准 User-Agent 头，并遵循 robots.txt 的允许规则。如果目标网站明确禁止自动化访问，可在配置中将该域名加入黑名单，系统将跳过抓取仅保留手动录入。

Q: 如何将现有的浏览器书签或 Pocket 收藏迁移到 WebIndex？

A: 浏览器书签可导出为 HTML 文件，系统管理后台提供"导入书签"功能，自动解析 `<a>` 标签的 href 与标题。Pocket 用户可先导出 CSV 文件，通过批量导入接口或管理界面的 CSV 上传入口完成迁移。具体操作步骤请参阅 `docs/usage/import-export.md`。

## 许可证

MIT

> 外链数量: 250 | 生成时间: 2026-08-24 23:40:21
