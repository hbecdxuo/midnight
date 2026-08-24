# WebLink Navigator

WebLink Navigator 是一个面向技术内容聚合与外部链接管理的开源导航工具。该项目定位于为开发者、技术博主以及内容运营人员提供一套轻量级、可自托管的网络书签与信息链接整理方案。它不同于传统的单页导航站，而是专注于对批量外链进行结构化分类、状态监控与快速检索，适用于需要长期维护大量 URL 资源的个人或团队。

本项目的核心目标用户包括开源社区文档维护者、技术资讯聚合平台运营者、以及需要进行大规模外链审计与归档的研发团队。通过提供标准化的链接录入接口、标签化分类体系以及基础的链接可用性检测机制，WebLink Navigator 帮助用户从杂乱的链接收藏中构建出有序的知识网络。

## 功能概览

- **批量链接导入与解析**：支持通过文本文件、CSV 或直接粘贴的方式批量导入 URL，自动解析协议、域名与路径结构，并提取基础元数据。

- **智能标签与分类管理**：允许用户为每个链接自定义标签（Tag）和分类（Category），支持多级分类体系，便于后续按主题或项目维度进行筛选。

- **链接状态健康检测**：内置定时任务，可周期性对已收录的链接发起 HTTP 请求，检测其可达性、响应时间以及状态码变化，自动标记异常链接。

- **全文检索与快速过滤**：基于标题、描述、标签和 URL 自身内容提供全文检索能力，支持按状态（正常/异常/未检测）、分类、标签组合过滤。

- **数据导入导出标准化**：支持 JSON、YAML 和 Markdown 表格格式的链接数据导入导出，便于与其他工具链（如静态站点生成器、Wiki 系统）集成。

- **外链关系图谱视图**：提供基础的图谱可视化功能，展示不同域名、子路径之间的引用关系，帮助用户理解链接间的拓扑结构。

- **访问统计与点击追踪**：记录每个链接的点击次数和最后访问时间，支持按热度排序，辅助判断内容价值。

- **用户权限与团队协作**：支持多用户账号体系，可配置只读、编辑、管理三级权限，适合团队共同维护链接库。

## 应用场景

**技术文档团队的外链资产维护**  
技术文档中常包含大量引用链接，这些链接随时间推移容易失效。WebLink Navigator 可定期扫描文档中的外链，生成可用性报告，帮助团队及时更新或替换失效引用，保障文档质量。

**开源项目资源导航站建设**  
开源项目通常需要维护生态相关的教程、工具、插件等外部资源列表。使用本项目可以快速构建一个分类清晰、检索方便的资源导航页，并且所有数据以结构化方式存储，便于版本管理和协作更新。

**个人知识库的链接归档与整理**  
研究员或开发者日常会积累大量技术文章、工具站点和视频教程链接。通过本项目的标签和分类体系，可以将这些零散的链接按技术栈、主题或优先级进行系统性整理，构建个人专属的知识检索库。

## 快速开始

以下命令演示了如何从 GitHub 克隆项目、安装依赖并启动开发服务。请确保你的系统中已安装 Git、Node.js（>= 16.0.0）和 npm 或 yarn。

```bash
# 克隆项目仓库
git clone https://github.com/weblink-navigator/weblink-navigator.git

# 进入项目目录
cd weblink-navigator

# 安装依赖包（使用 npm）
npm install

# 或者使用 yarn
yarn install

# 启动开发服务器（默认监听 3000 端口）
npm run dev

# 生产环境构建
npm run build
npm start
```

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|---------|---------|------|
| Node.js | >= 16.0.0 | 运行时环境，推荐使用 LTS 版本 |
| npm | >= 7.0.0 | 包管理器，或使用 yarn 替代 |
| PostgreSQL | >= 13.0 | 主数据库，用于存储链接、标签、用户等数据 |
| Redis | >= 6.0 | 缓存与任务队列，用于提升检测任务性能 |
| Nginx | >= 1.18 | 生产环境反向代理与静态资源服务（可选） |
| Git | >= 2.25 | 版本控制工具，用于克隆与更新代码 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|------|------|-----------|
| 入门指南 | /docs/guide/getting-started.md | 如何从零开始安装、配置并运行第一个实例？ |
| 核心功能 | /docs/features/link-management.md | 如何批量导入链接、设置标签和分类？检测机制如何工作？ |
| API 参考 | /docs/api/endpoints.md | 提供了哪些 RESTful API 接口？请求与响应的格式是什么？ |
| 部署运维 | /docs/operations/deployment.md | 如何在生产环境中使用 Docker 或 PM2 部署？如何进行备份与恢复？ |

## 资源列表

- http://m.wap.uliejh.cn/bnews/4724299.htm
- http://m.wap.uliejh.cn/bnews/7190.htm
- http://m.wap.uliejh.cn/bnews/2527.htm
- http://m.wap.uliejh.cn/bnews/677227.htm
- http://m.wap.uliejh.cn/bnews/7946.htm
- http://m.wap.uliejh.cn/bnews/5616330.htm
- http://m.wap.uliejh.cn/bnews/27769.htm
- http://m.wap.uliejh.cn/bnews/5001.htm
- http://m.wap.uliejh.cn/bnews/2706426.htm
- http://m.wap.uliejh.cn/bnews/132023.htm
- http://m.wap.uliejh.cn/bnews/73013.htm
- http://m.wap.uliejh.cn/bnews/9676001.htm
- http://m.wap.uliejh.cn/bnews/4389127.htm
- http://m.wap.uliejh.cn/bnews/590179.htm
- http://m.wap.uliejh.cn/bnews/391282.htm
- http://m.wap.uliejh.cn/bnews/05212.htm
- http://m.wap.uliejh.cn/bnews/81696.htm
- http://m.wap.uliejh.cn/bnews/195980.htm
- http://m.wap.uliejh.cn/bnews/22431.htm
- http://m.wap.uliejh.cn/bnews/875619.htm
- http://m.wap.uliejh.cn/bnews/0959.htm
- http://m.wap.uliejh.cn/bnews/914783.htm
- http://m.wap.uliejh.cn/bnews/85596.htm
- http://m.wap.uliejh.cn/bnews/406164.htm
- http://m.wap.uliejh.cn/bnews/7099423.htm
- http://m.wap.uliejh.cn/bnews/522589.htm
- http://m.wap.uliejh.cn/bnews/399474.htm
- http://m.wap.uliejh.cn/bnews/393650.htm
- http://m.wap.uliejh.cn/bnews/181567.htm
- http://m.wap.uliejh.cn/bnews/27190.htm
- http://m.wap.uliejh.cn/bnews/8638014.htm
- http://m.wap.uliejh.cn/bnews/84266.htm
- http://m.wap.uliejh.cn/bnews/858205.htm
- http://m.wap.uliejh.cn/bnews/686204.htm
- http://m.wap.uliejh.cn/bnews/175983.htm
- http://m.wap.uliejh.cn/bnews/817085.htm
- http://m.wap.uliejh.cn/bnews/7577212.htm
- http://m.wap.uliejh.cn/bnews/8201973.htm
- http://m.wap.uliejh.cn/bnews/8315.htm
- http://m.wap.uliejh.cn/bnews/503747.htm
- http://m.wap.uliejh.cn/bnews/789439.htm
- http://m.wap.uliejh.cn/bnews/423823.htm
- http://m.wap.uliejh.cn/bnews/4769.htm
- http://m.wap.uliejh.cn/bnews/4529028.htm
- http://m.wap.uliejh.cn/bnews/46974.htm
- http://m.wap.uliejh.cn/bnews/7327.htm
- http://m.wap.uliejh.cn/bnews/204287.htm
- http://m.wap.uliejh.cn/bnews/4427345.htm
- http://m.wap.uliejh.cn/bnews/320534.htm
- http://m.wap.uliejh.cn/bnews/1622.htm
- http://m.wap.uliejh.cn/bnews/13795.htm
- http://m.wap.uliejh.cn/bnews/5958970.htm
- http://m.wap.uliejh.cn/bnews/13460.htm
- http://m.wap.uliejh.cn/bnews/4997877.htm
- http://m.wap.uliejh.cn/bnews/4802403.htm
- http://m.wap.uliejh.cn/bnews/2114042.htm
- http://m.wap.uliejh.cn/bnews/4517141.htm
- http://m.wap.uliejh.cn/bnews/034045.htm
- http://m.wap.uliejh.cn/bnews/1215.htm
- http://m.wap.uliejh.cn/bnews/086848.htm
- http://m.wap.uliejh.cn/bnews/6940.htm
- http://m.wap.uliejh.cn/bnews/90150.htm
- http://m.wap.uliejh.cn/bnews/8548.htm
- http://m.wap.uliejh.cn/bnews/6077.htm
- http://m.wap.uliejh.cn/bnews/1585.htm
- http://m.wap.uliejh.cn/bnews/14211.htm
- http://m.wap.uliejh.cn/bnews/9350.htm
- http://m.wap.uliejh.cn/bnews/467448.htm
- http://m.wap.uliejh.cn/bnews/204421.htm
- http://m.wap.uliejh.cn/bnews/11595.htm
- http://m.wap.uliejh.cn/bnews/13752.htm
- http://m.wap.uliejh.cn/bnews/3061.htm
- http://m.wap.uliejh.cn/bnews/8895.htm
- http://m.wap.uliejh.cn/bnews/9733875.htm
- http://m.wap.uliejh.cn/bnews/0151985.htm
- http://m.wap.uliejh.cn/bnews/14485.htm
- http://m.wap.uliejh.cn/bnews/2271.htm
- http://m.wap.uliejh.cn/bnews/7369446.htm
- http://m.wap.uliejh.cn/bnews/350345.htm
- http://m.wap.uliejh.cn/bnews/6873.htm
- http://m.wap.uliejh.cn/bnews/4887306.htm
- http://m.wap.uliejh.cn/bnews/63902.htm
- http://m.wap.uliejh.cn/bnews/1304960.htm
- http://m.wap.uliejh.cn/bnews/2535.htm
- http://m.wap.uliejh.cn/bnews/701559.htm
- http://m.wap.uliejh.cn/bnews/2086.htm
- http://m.wap.uliejh.cn/bnews/169549.htm
- http://m.wap.uliejh.cn/bnews/99958.htm
- http://m.wap.uliejh.cn/bnews/7006323.htm
- http://m.wap.uliejh.cn/bnews/0298046.htm
- http://m.wap.uliejh.cn/bnews/3723812.htm
- http://m.wap.uliejh.cn/bnews/9656794.htm
- http://m.wap.uliejh.cn/bnews/738829.htm
- http://m.wap.uliejh.cn/bnews/0785852.htm
- http://m.wap.uliejh.cn/bnews/6952963.htm
- http://m.wap.uliejh.cn/bnews/14681.htm
- http://m.wap.uliejh.cn/bnews/94570.htm
- http://m.wap.uliejh.cn/bnews/494399.htm
- http://m.wap.uliejh.cn/bnews/77880.htm
- http://m.wap.uliejh.cn/bnews/673027.htm
- http://m.wap.uliejh.cn/bnews/92157.htm
- http://m.wap.uliejh.cn/bnews/52361.htm
- http://m.wap.uliejh.cn/bnews/8881967.htm
- http://m.wap.uliejh.cn/bnews/9646860.htm
- http://m.wap.uliejh.cn/bnews/0816807.htm
- http://m.wap.uliejh.cn/bnews/843025.htm
- http://m.wap.uliejh.cn/bnews/15449.htm
- http://m.wap.uliejh.cn/bnews/320610.htm
- http://m.wap.uliejh.cn/bnews/995603.htm
- http://m.wap.uliejh.cn/bnews/6227415.htm
- http://m.wap.uliejh.cn/bnews/1653.htm
- http://m.wap.uliejh.cn/bnews/6936.htm
- http://m.wap.uliejh.cn/bnews/352347.htm
- http://m.wap.uliejh.cn/bnews/45931.htm
- http://m.wap.uliejh.cn/bnews/15999.htm
- http://m.wap.uliejh.cn/bnews/000334.htm
- http://m.wap.uliejh.cn/bnews/00579.htm
- http://m.wap.uliejh.cn/bnews/9013466.htm
- http://m.wap.uliejh.cn/bnews/3526313.htm
- http://m.wap.uliejh.cn/bnews/4659.htm
- http://m.wap.uliejh.cn/bnews/9627439.htm
- http://m.wap.uliejh.cn/bnews/1769277.htm
- http://m.wap.uliejh.cn/bnews/9578.htm
- http://m.wap.uliejh.cn/bnews/286965.htm
- http://m.wap.uliejh.cn/bnews/1879326.htm
- http://m.wap.uliejh.cn/bnews/8021190.htm
- http://m.wap.uliejh.cn/bnews/8356.htm
- http://m.wap.uliejh.cn/bnews/370246.htm
- http://m.wap.uliejh.cn/bnews/3885.htm
- http://m.wap.uliejh.cn/bnews/422668.htm
- http://m.wap.uliejh.cn/bnews/368277.htm
- http://m.wap.uliejh.cn/bnews/1714433.htm
- http://m.wap.uliejh.cn/bnews/540268.htm
- http://m.wap.uliejh.cn/bnews/9787.htm
- http://m.wap.uliejh.cn/bnews/18924.htm
- http://m.wap.uliejh.cn/bnews/66274.htm
- http://m.wap.uliejh.cn/bnews/26909.htm
- http://m.wap.uliejh.cn/bnews/2318.htm
- http://m.wap.uliejh.cn/bnews/1570.htm
- http://m.wap.uliejh.cn/bnews/4106820.htm
- http://m.wap.uliejh.cn/bnews/7965.htm
- http://m.wap.uliejh.cn/bnews/69169.htm
- http://m.wap.uliejh.cn/bnews/8725.htm
- http://m.wap.uliejh.cn/bnews/9631.htm
- http://m.wap.uliejh.cn/bnews/64890.htm
- http://m.wap.uliejh.cn/bnews/58629.htm
- http://m.wap.uliejh.cn/bnews/907642.htm
- http://m.wap.uliejh.cn/bnews/2455090.htm
- http://m.wap.uliejh.cn/bnews/511796.htm
- http://m.wap.uliejh.cn/bnews/7988673.htm
- http://m.wap.uliejh.cn/bnews/436292.htm
- http://m.wap.uliejh.cn/bnews/3523640.htm
- http://m.wap.uliejh.cn/bnews/9627296.htm
- http://m.wap.uliejh.cn/bnews/29355.htm
- http://m.wap.uliejh.cn/bnews/3474416.htm
- http://m.wap.uliejh.cn/bnews/690363.htm
- http://m.wap.uliejh.cn/bnews/717094.htm
- http://m.wap.uliejh.cn/bnews/0804.htm
- http://m.wap.uliejh.cn/bnews/64392.htm
- http://m.wap.uliejh.cn/bnews/6187677.htm
- http://m.wap.uliejh.cn/bnews/5700.htm
- http://m.wap.uliejh.cn/bnews/5794137.htm
- http://m.wap.uliejh.cn/bnews/5974.htm
- http://m.wap.uliejh.cn/bnews/5228.htm
- http://m.wap.uliejh.cn/bnews/8391562.htm
- http://m.wap.uliejh.cn/bnews/00021.htm
- http://m.wap.uliejh.cn/bnews/3071684.htm
- http://m.wap.uliejh.cn/bnews/9912808.htm
- http://m.wap.uliejh.cn/bnews/10961.htm
- http://m.wap.uliejh.cn/bnews/0546.htm
- http://m.wap.uliejh.cn/bnews/918632.htm
- http://m.wap.uliejh.cn/bnews/5878.htm
- http://m.wap.uliejh.cn/bnews/4107814.htm
- http://m.wap.uliejh.cn/bnews/82692.htm
- http://m.wap.uliejh.cn/bnews/02553.htm
- http://m.wap.uliejh.cn/bnews/26794.htm
- http://m.wap.uliejh.cn/bnews/0861492.htm
- http://m.wap.uliejh.cn/bnews/0590.htm
- http://m.wap.uliejh.cn/bnews/6824.htm
- http://m.wap.uliejh.cn/bnews/4925.htm
- http://m.wap.uliejh.cn/bnews/0839918.htm
- http://m.wap.uliejh.cn/bnews/38753.htm
- http://m.wap.uliejh.cn/bnews/3854.htm
- http://m.wap.uliejh.cn/bnews/2511.htm
- http://m.wap.uliejh.cn/bnews/2041.htm
- http://m.wap.uliejh.cn/bnews/1018116.htm
- http://m.wap.uliejh.cn/bnews/8055657.htm
- http://m.wap.uliejh.cn/bnews/89468.htm
- http://m.wap.uliejh.cn/bnews/0158.htm
- http://m.wap.uliejh.cn/bnews/161803.htm
- http://m.wap.uliejh.cn/bnews/140781.htm
- http://m.wap.uliejh.cn/bnews/9093.htm
- http://m.wap.uliejh.cn/bnews/35275.htm
- http://m.wap.uliejh.cn/bnews/8372513.htm
- http://m.wap.uliejh.cn/bnews/98584.htm
- http://m.wap.uliejh.cn/bnews/8473.htm
- http://m.wap.uliejh.cn/bnews/7472278.htm
- http://m.wap.uliejh.cn/bnews/189853.htm
- http://m.wap.uliejh.cn/bnews/4399.htm
- http://m.wap.uliejh.cn/bnews/8127816.htm
- http://m.wap.uliejh.cn/bnews/9193.htm
- http://m.wap.uliejh.cn/bnews/9530.htm
- http://m.wap.uliejh.cn/bnews/585095.htm
- http://m.wap.uliejh.cn/bnews/774001.htm
- http://m.wap.uliejh.cn/bnews/325873.htm
- http://m.wap.uliejh.cn/bnews/8774253.htm
- http://m.wap.uliejh.cn/bnews/4301.htm
- http://m.wap.uliejh.cn/bnews/34945.htm
- http://m.wap.uliejh.cn/bnews/976315.htm
- http://m.wap.uliejh.cn/bnews/55386.htm
- http://m.wap.uliejh.cn/bnews/4173.htm
- http://m.wap.uliejh.cn/bnews/47693.htm
- http://m.wap.uliejh.cn/bnews/1703.htm
- http://m.wap.uliejh.cn/bnews/97369.htm
- http://m.wap.uliejh.cn/bnews/09356.htm
- http://m.wap.uliejh.cn/bnews/12282.htm
- http://m.wap.uliejh.cn/bnews/8409.htm
- http://m.wap.uliejh.cn/bnews/870916.htm
- http://m.wap.uliejh.cn/bnews/5470.htm
- http://m.wap.uliejh.cn/bnews/735073.htm
- http://m.wap.uliejh.cn/bnews/371723.htm
- http://m.wap.uliejh.cn/bnews/93208.htm
- http://m.wap.uliejh.cn/bnews/37137.htm
- http://m.wap.uliejh.cn/bnews/8896.htm
- http://m.wap.uliejh.cn/bnews/19769.htm
- http://m.wap.uliejh.cn/bnews/447801.htm
- http://m.wap.uliejh.cn/bnews/2909345.htm
- http://m.wap.uliejh.cn/bnews/843973.htm
- http://m.wap.uliejh.cn/bnews/7426.htm
- http://m.wap.uliejh.cn/bnews/9987.htm
- http://m.wap.uliejh.cn/bnews/019528.htm
- http://m.wap.uliejh.cn/bnews/214000.htm
- http://m.wap.uliejh.cn/bnews/85048.htm
- http://m.wap.uliejh.cn/bnews/185194.htm
- http://m.wap.uliejh.cn/bnews/656898.htm
- http://m.wap.uliejh.cn/bnews/88021.htm
- http://m.wap.uliejh.cn/bnews/5514.htm
- http://m.wap.uliejh.cn/bnews/7895834.htm
- http://m.wap.uliejh.cn/bnews/7877613.htm
- http://m.wap.uliejh.cn/bnews/978717.htm
- http://m.wap.uliejh.cn/bnews/8223.htm
- http://m.wap.uliejh.cn/bnews/08733.htm
- http://m.wap.uliejh.cn/bnews/6354461.htm
- http://m.wap.uliejh.cn/bnews/9346.htm
- http://m.wap.uliejh.cn/bnews/4647433.htm
- http://m.wap.uliejh.cn/bnews/7891.htm
- http://m.wap.uliejh.cn/bnews/2410918.htm
- http://m.wap.uliejh.cn/bnews/723935.htm
- http://m.wap.uliejh.cn/bnews/4938762.htm
- http://m.wap.uliejh.cn/bnews/7997749.htm

## 项目结构

```
weblink-navigator/
├── packages/
│   ├── backend/                # 核心后端服务（Node.js + Express）
│   │   ├── src/
│   │   │   ├── controllers/    # 路由控制器，处理请求与响应
│   │   │   ├── models/         # 数据模型定义（链接、标签、用户等）
│   │   │   ├── services/       # 业务逻辑层（检测、导入、统计等）
│   │   │   ├── queues/         # 任务队列（链接检测定时任务）
│   │   │   └── utils/          # 工具函数（日志、验证、HTTP客户端）
│   │   └── tests/              # 后端单元测试与集成测试
│   ├── frontend/               # 前端应用（React + TypeScript）
│   │   ├── src/
│   │   │   ├── pages/          # 页面组件（列表、详情、仪表盘）
│   │   │   ├── components/     # 可复用UI组件（表格、过滤器、图谱）
│   │   │   ├── hooks/          # 自定义React Hooks
│   │   │   ├── stores/         # 状态管理（Zustand）
│   │   │   └── api/            # 后端接口调用封装
│   │   └── public/             # 静态资源（图标、字体）
│   └── shared/                 # 前后端共享代码（类型定义、常量）
├── config/
│   ├── default.json            # 默认配置（端口、数据库连接）
│   ├── production.json         # 生产环境配置覆盖
│   └── test.json               # 测试环境配置
├── scripts/
│   ├── init-db.sql             # 数据库初始化脚本
│   └── seed-links.js           # 示例链接数据填充脚本
├── docs/                       # 完整文档（详见文档导航）
├── docker-compose.yml          # 本地开发与生产部署的容器编排
├── Dockerfile                  # 后端服务镜像构建文件
├── .github/
│   └── workflows/              # CI/CD 流水线（测试、构建、发布）
├── package.json                # 项目根依赖与脚本命令
├── tsconfig.json               # TypeScript 编译配置
└── README.md                   # 本文档
```

## 贡献指南

1. 阅读项目行为准则与贡献规范  
   在提交任何代码或文档之前，请仔细阅读项目根目录下的 CODE_OF_CONDUCT.md 和 CONTRIBUTING.md 文件，了解社区的基本约定与提交流程。

2. 从 Issue 列表中选择任务或提交新 Issue  
   访问 GitHub Issues 页面，查看当前未被认领的任务（标记为 `help wanted` 或 `good first issue`）。如果发现新的缺陷或有改进建议，请先提交 Issue 并与维护者沟通。

3. 派生项目并创建功能分支  
   将项目派生（Fork）至个人账号下，然后基于 `main` 分支创建一个新的分支，分支命名建议遵循 `feature/xxx` 或 `fix/xxx` 格式。

4. 编写代码并确保通过所有测试  
   在本地开发环境中完成功能开发后，运行 `npm run test` 确保所有已有的单元测试和集成测试通过。新增功能需同步补充对应的测试用例。

5. 提交 Pull Request 并等待审核  
   推送到远程分支后，向原始仓库的 `main` 分支发起 Pull Request。请在 PR 描述中清晰说明改动内容、关联的 Issue 编号以及测试结果。至少需要一位维护者审核通过后方可合并。

## 常见问题

**Q: 链接健康检测的周期是多久？是否支持自定义？**  
A: 默认情况下，系统会每隔 24 小时对所有已收录的链接执行一次状态检测。你可以在配置文件中通过 `scheduler.interval` 字段调整检测间隔（单位：小时）。同时，也支持通过管理界面手动触发对单个链接或特定分类的即时检测。

**Q: 导入大量链接时，是否会导致页面卡顿或超时？**  
A: 项目后端采用队列机制处理批量导入任务。当一次导入超过 100 条链接时，导入操作会进入后台队列异步执行，前端界面立即返回任务 ID。用户可以通过任务中心查看导入进度和结果日志，避免 HTTP 请求超时。

**Q: 如何迁移或备份我的链接数据？**  
A: 你可以在后台管理界面使用「导出数据」功能，系统会将当前所有链接、标签、分类以及元数据导出为一个标准的 JSON 文件。该文件兼容本项目的导入接口，也可使用其他编程语言解析。此外，直接备份 PostgreSQL 数据库也是一种完整备份方式。

## 许可证

MIT

> 外链数量: 250 | 生成时间: 2026-08-24 23:40:21
