# WebIndex 技术资源导航

WebIndex 是一个面向开发者与技术研究人员的轻量级外链资源汇总与导航系统。该项目定位于对分散于互联网各处的技术文档、工具站点、数据页面及行业资讯进行结构化整理，通过统一的索引视图提供快速访问入口。WebIndex 本身不存储任何资源内容，仅作为URL路由与分类展示层，适用于个人开发者作为浏览器起始页、团队内部知识库入口，或作为微服务架构中的外部依赖管理面板。

项目采用静态站点生成方案，所有链接数据通过配置文件注入，支持自动构建与持续集成。目标用户包括需要频繁查阅技术手册的后端工程师、关注数据动态的分析人员，以及希望建立统一访问入口的运维管理者。WebIndex 通过目录分层与标签体系，将原始散列链接转化为可维护、可扩展的语义化导航结构，有效降低日常信息检索的认知负担。

## 功能概览

- **分级目录导航**：支持无限层级的分类目录，用户可根据业务域或技术栈自定义顶层入口，每级目录可绑定独立URL集合。

- **链接元数据注入**：每条资源可附加标题、描述、标签与权重字段，便于构建搜索索引与卡片式展示。

- **自动健康检查**：内置HTTP状态探测模块，定时对收录链接进行可达性验证，并标记异常条目，避免用户访问失效资源。

- **全文模糊检索**：基于标题与描述字段的轻量级倒排索引，支持中英文混排快速定位，响应时间控制在200毫秒以内。

- **响应式布局适配**：前端界面基于CSS Grid与Flexbox构建，兼容桌面端与移动端浏览器，保证在主流视口尺寸下的可用性。

- **批量导入导出**：支持JSON与CSV格式的链接批量操作，便于从既有书签系统迁移或同步至团队仓库。

- **访问热度统计**：记录每个外链的点击次数与最后访问时间，辅助识别高频资源，为目录权重调整提供数据依据。

- **暗色主题切换**：内置浅色与暗色两套视觉方案，跟随系统偏好或用户手动切换，降低长时间阅读的视觉疲劳。

## 应用场景

- **个人技术起始页**：开发者可将日常高频访问的API文档、监控面板、日志系统与代码仓库入口统一收录，替换浏览器原生新标签页，每次开屏即可直达工作上下文。

- **团队知识库入口聚合**：技术团队可在内部服务器部署WebIndex，将散落在Wiki、Jira、Confluence、GitLab及各类监控工具中的链接分类整理，新成员入职时仅需记住一个地址即可获取全部必要资源。

- **微服务依赖关系梳理**：架构师可利用目录层级表达服务间依赖顺序，将注册中心、配置中心、网关及每个业务服务的控制台地址按环境（开发/测试/生产）分组，作为运维手册的补充视图。

- **数据看板与报表导航**：数据分析师可将每日需查看的经营数据报表、实时大盘、异常告警页面集中管理，配合健康检查功能提前发现数据源页面异常。

## 快速开始

以下命令序列适用于Linux/macOS环境，若使用Windows，请将`./webindex`替换为`webindex.exe`或使用WSL执行。

```bash
# 克隆代码仓库至本地
git clone https://github.com/webindex/webindex.git

# 进入项目工作目录
cd webindex

# 安装项目依赖（基于Node.js 18+）
npm install

# 执行构建流程，生成静态站点至dist目录
npm run build

# 启动本地开发服务器，默认监听端口3000
npm start
```

构建完成后，可通过浏览器访问 `http://localhost:3000` 查看站点。若需自定义收录链接，请编辑 `data/sources.json` 文件，按文档说明的Schema结构添加或修改条目后重新执行构建。

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|----------|----------|------|
| Node.js | 18.x 或 20.x LTS | 运行时环境，用于执行构建脚本与开发服务器 |
| npm | 9.x 或 10.x | 包管理器，用于安装项目依赖 |
| Git | 2.30 及以上 | 版本控制工具，用于克隆仓库及提交贡献 |
| 现代浏览器 | Chrome 110+ / Firefox 109+ / Edge 110+ | 前端界面运行环境，需支持ES2022语法 |
| 操作系统 | Linux (glibc 2.28+) / macOS 11+ / Windows 10+ | 构建工具链依赖系统底层库，Windows需启用WSL2或使用PowerShell |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|------|------|------------|
| 用户手册 | docs/usage/ | 如何添加、删除或分类管理链接？如何切换主题与设置偏好？ |
| 配置参考 | docs/configuration/ | sources.json的完整字段定义是什么？健康检查的阈值如何调整？ |
| 开发指南 | docs/development/ | 如何扩展前端组件？怎样自定义卡片渲染逻辑？单元测试如何运行？ |
| 部署运维 | docs/deployment/ | 支持哪些静态托管平台？如何配置Nginx反向代理？环境变量有哪些？ |

## 资源列表

- http://m.wap.uliejh.cn/bnews/0126.htm
- http://m.wap.uliejh.cn/bnews/817468.htm
- http://m.wap.uliejh.cn/bnews/6476.htm
- http://m.wap.uliejh.cn/bnews/5274634.htm
- http://m.wap.uliejh.cn/bnews/0666953.htm
- http://m.wap.uliejh.cn/bnews/3793.htm
- http://m.wap.uliejh.cn/bnews/2637835.htm
- http://m.wap.uliejh.cn/bnews/95516.htm
- http://m.wap.uliejh.cn/bnews/11618.htm
- http://m.wap.uliejh.cn/bnews/365176.htm
- http://m.wap.uliejh.cn/bnews/1646192.htm
- http://m.wap.uliejh.cn/bnews/43840.htm
- http://m.wap.uliejh.cn/bnews/08460.htm
- http://m.wap.uliejh.cn/bnews/6139.htm
- http://m.wap.uliejh.cn/bnews/097998.htm
- http://m.wap.uliejh.cn/bnews/26426.htm
- http://m.wap.uliejh.cn/bnews/299200.htm
- http://m.wap.uliejh.cn/bnews/866163.htm
- http://m.wap.uliejh.cn/bnews/4520.htm
- http://m.wap.uliejh.cn/bnews/1821643.htm
- http://m.wap.uliejh.cn/bnews/0176.htm
- http://m.wap.uliejh.cn/bnews/86902.htm
- http://m.wap.uliejh.cn/bnews/8683871.htm
- http://m.wap.uliejh.cn/bnews/9238925.htm
- http://m.wap.uliejh.cn/bnews/8574.htm
- http://m.wap.uliejh.cn/bnews/03430.htm
- http://m.wap.uliejh.cn/bnews/55293.htm
- http://m.wap.uliejh.cn/bnews/2167783.htm
- http://m.wap.uliejh.cn/bnews/5070605.htm
- http://m.wap.uliejh.cn/bnews/8753.htm
- http://m.wap.uliejh.cn/bnews/6932606.htm
- http://m.wap.uliejh.cn/bnews/9274.htm
- http://m.wap.uliejh.cn/bnews/06590.htm
- http://m.wap.uliejh.cn/bnews/0652.htm
- http://m.wap.uliejh.cn/bnews/1929891.htm
- http://m.wap.uliejh.cn/bnews/219588.htm
- http://m.wap.uliejh.cn/bnews/935327.htm
- http://m.wap.uliejh.cn/bnews/67081.htm
- http://m.wap.uliejh.cn/bnews/8293.htm
- http://m.wap.uliejh.cn/bnews/883195.htm
- http://m.wap.uliejh.cn/bnews/43978.htm
- http://m.wap.uliejh.cn/bnews/0053506.htm
- http://m.wap.uliejh.cn/bnews/220178.htm
- http://m.wap.uliejh.cn/bnews/55432.htm
- http://m.wap.uliejh.cn/bnews/48067.htm
- http://m.wap.uliejh.cn/bnews/945443.htm
- http://m.wap.uliejh.cn/bnews/862138.htm
- http://m.wap.uliejh.cn/bnews/9988.htm
- http://m.wap.uliejh.cn/bnews/633642.htm
- http://m.wap.uliejh.cn/bnews/7308.htm
- http://m.wap.uliejh.cn/bnews/9556.htm
- http://m.wap.uliejh.cn/bnews/652499.htm
- http://m.wap.uliejh.cn/bnews/82397.htm
- http://m.wap.uliejh.cn/bnews/05021.htm
- http://m.wap.uliejh.cn/bnews/5891935.htm
- http://m.wap.uliejh.cn/bnews/6691.htm
- http://m.wap.uliejh.cn/bnews/632454.htm
- http://m.wap.uliejh.cn/bnews/119382.htm
- http://m.wap.uliejh.cn/bnews/3712589.htm
- http://m.wap.uliejh.cn/bnews/51075.htm
- http://m.wap.uliejh.cn/bnews/3920.htm
- http://m.wap.uliejh.cn/bnews/6872348.htm
- http://m.wap.uliejh.cn/bnews/91162.htm
- http://m.wap.uliejh.cn/bnews/705953.htm
- http://m.wap.uliejh.cn/bnews/7122285.htm
- http://m.wap.uliejh.cn/bnews/129705.htm
- http://m.wap.uliejh.cn/bnews/2674458.htm
- http://m.wap.uliejh.cn/bnews/41251.htm
- http://m.wap.uliejh.cn/bnews/29264.htm
- http://m.wap.uliejh.cn/bnews/0229.htm
- http://m.wap.uliejh.cn/bnews/002812.htm
- http://m.wap.uliejh.cn/bnews/9817604.htm
- http://m.wap.uliejh.cn/bnews/315229.htm
- http://m.wap.uliejh.cn/bnews/2385094.htm
- http://m.wap.uliejh.cn/bnews/0263973.htm
- http://m.wap.uliejh.cn/bnews/666338.htm
- http://m.wap.uliejh.cn/bnews/2749035.htm
- http://m.wap.uliejh.cn/bnews/35524.htm
- http://m.wap.uliejh.cn/bnews/9572.htm
- http://m.wap.uliejh.cn/bnews/58928.htm
- http://m.wap.uliejh.cn/bnews/4884409.htm
- http://m.wap.uliejh.cn/bnews/13796.htm
- http://m.wap.uliejh.cn/bnews/466374.htm
- http://m.wap.uliejh.cn/bnews/744744.htm
- http://m.wap.uliejh.cn/bnews/26347.htm
- http://m.wap.uliejh.cn/bnews/81591.htm
- http://m.wap.uliejh.cn/bnews/57757.htm
- http://m.wap.uliejh.cn/bnews/7095.htm
- http://m.wap.uliejh.cn/bnews/24013.htm
- http://m.wap.uliejh.cn/bnews/81842.htm
- http://m.wap.uliejh.cn/bnews/7440.htm
- http://m.wap.uliejh.cn/bnews/0555.htm
- http://m.wap.uliejh.cn/bnews/5289.htm
- http://m.wap.uliejh.cn/bnews/3618604.htm
- http://m.wap.uliejh.cn/bnews/8347991.htm
- http://m.wap.uliejh.cn/bnews/06129.htm
- http://m.wap.uliejh.cn/bnews/1763791.htm
- http://m.wap.uliejh.cn/bnews/099263.htm
- http://m.wap.uliejh.cn/bnews/73692.htm
- http://m.wap.uliejh.cn/bnews/5573103.htm
- http://m.wap.uliejh.cn/bnews/016132.htm
- http://m.wap.uliejh.cn/bnews/3119867.htm
- http://m.wap.uliejh.cn/bnews/3962.htm
- http://m.wap.uliejh.cn/bnews/4086320.htm
- http://m.wap.uliejh.cn/bnews/9749963.htm
- http://m.wap.uliejh.cn/bnews/12632.htm
- http://m.wap.uliejh.cn/bnews/6611205.htm
- http://m.wap.uliejh.cn/bnews/6927098.htm
- http://m.wap.uliejh.cn/bnews/388666.htm
- http://m.wap.uliejh.cn/bnews/905056.htm
- http://m.wap.uliejh.cn/bnews/16587.htm
- http://m.wap.uliejh.cn/bnews/01439.htm
- http://m.wap.uliejh.cn/bnews/6146414.htm
- http://m.wap.uliejh.cn/bnews/85278.htm
- http://m.wap.uliejh.cn/bnews/2710.htm
- http://m.wap.uliejh.cn/bnews/78337.htm
- http://m.wap.uliejh.cn/bnews/150284.htm
- http://m.wap.uliejh.cn/bnews/86758.htm
- http://m.wap.uliejh.cn/bnews/8703.htm
- http://m.wap.uliejh.cn/bnews/837524.htm
- http://m.wap.uliejh.cn/bnews/172928.htm
- http://m.wap.uliejh.cn/bnews/5111416.htm
- http://m.wap.uliejh.cn/bnews/0882587.htm
- http://m.wap.uliejh.cn/bnews/6830439.htm
- http://m.wap.uliejh.cn/bnews/50452.htm
- http://m.wap.uliejh.cn/bnews/602194.htm
- http://m.wap.uliejh.cn/bnews/508296.htm
- http://m.wap.uliejh.cn/bnews/235814.htm
- http://m.wap.uliejh.cn/bnews/3631.htm
- http://m.wap.uliejh.cn/bnews/4676.htm
- http://m.wap.uliejh.cn/bnews/22915.htm
- http://m.wap.uliejh.cn/bnews/54776.htm
- http://m.wap.uliejh.cn/bnews/1586823.htm
- http://m.wap.uliejh.cn/bnews/989287.htm
- http://m.wap.uliejh.cn/bnews/5856170.htm
- http://m.wap.uliejh.cn/bnews/3600.htm
- http://m.wap.uliejh.cn/bnews/7363251.htm
- http://m.wap.uliejh.cn/bnews/389691.htm
- http://m.wap.uliejh.cn/bnews/4316.htm
- http://m.wap.uliejh.cn/bnews/95415.htm
- http://m.wap.uliejh.cn/bnews/261903.htm
- http://m.wap.uliejh.cn/bnews/1852766.htm
- http://m.wap.uliejh.cn/bnews/78114.htm
- http://m.wap.uliejh.cn/bnews/15305.htm
- http://m.wap.uliejh.cn/bnews/596287.htm
- http://m.wap.uliejh.cn/bnews/4004121.htm
- http://m.wap.uliejh.cn/bnews/6975.htm
- http://m.wap.uliejh.cn/bnews/3352579.htm
- http://m.wap.uliejh.cn/bnews/1490365.htm
- http://m.wap.uliejh.cn/bnews/486912.htm
- http://m.wap.uliejh.cn/bnews/121878.htm
- http://m.wap.uliejh.cn/bnews/0599324.htm
- http://m.wap.uliejh.cn/bnews/9402.htm
- http://m.wap.uliejh.cn/bnews/4012.htm
- http://m.wap.uliejh.cn/bnews/1077.htm
- http://m.wap.uliejh.cn/bnews/5006.htm
- http://m.wap.uliejh.cn/bnews/8262.htm
- http://m.wap.uliejh.cn/bnews/88580.htm
- http://m.wap.uliejh.cn/bnews/668419.htm
- http://m.wap.uliejh.cn/bnews/51858.htm
- http://m.wap.uliejh.cn/bnews/2405.htm
- http://m.wap.uliejh.cn/bnews/4400402.htm
- http://m.wap.uliejh.cn/bnews/479793.htm
- http://m.wap.uliejh.cn/bnews/73032.htm
- http://m.wap.uliejh.cn/bnews/7133.htm
- http://m.wap.uliejh.cn/bnews/79123.htm
- http://m.wap.uliejh.cn/bnews/8481.htm
- http://m.wap.uliejh.cn/bnews/629350.htm
- http://m.wap.uliejh.cn/bnews/46662.htm
- http://m.wap.uliejh.cn/bnews/7196.htm
- http://m.wap.uliejh.cn/bnews/5680264.htm
- http://m.wap.uliejh.cn/bnews/4421599.htm
- http://m.wap.uliejh.cn/bnews/1472101.htm
- http://m.wap.uliejh.cn/bnews/3211662.htm
- http://m.wap.uliejh.cn/bnews/3197040.htm
- http://m.wap.uliejh.cn/bnews/576429.htm
- http://m.wap.uliejh.cn/bnews/9571443.htm
- http://m.wap.uliejh.cn/bnews/313381.htm
- http://m.wap.uliejh.cn/bnews/4309.htm
- http://m.wap.uliejh.cn/bnews/64923.htm
- http://m.wap.uliejh.cn/bnews/8461528.htm
- http://m.wap.uliejh.cn/bnews/3539.htm
- http://m.wap.uliejh.cn/bnews/6639801.htm
- http://m.wap.uliejh.cn/bnews/26174.htm
- http://m.wap.uliejh.cn/bnews/502205.htm
- http://m.wap.uliejh.cn/bnews/10499.htm
- http://m.wap.uliejh.cn/bnews/1442.htm
- http://m.wap.uliejh.cn/bnews/96633.htm
- http://m.wap.uliejh.cn/bnews/563503.htm
- http://m.wap.uliejh.cn/bnews/8286197.htm
- http://m.wap.uliejh.cn/bnews/2173.htm
- http://m.wap.uliejh.cn/bnews/318915.htm
- http://m.wap.uliejh.cn/bnews/59706.htm
- http://m.wap.uliejh.cn/bnews/6943953.htm
- http://m.wap.uliejh.cn/bnews/5735.htm
- http://m.wap.uliejh.cn/bnews/48156.htm
- http://m.wap.uliejh.cn/bnews/46125.htm
- http://m.wap.uliejh.cn/bnews/0184.htm
- http://m.wap.uliejh.cn/bnews/9501534.htm
- http://m.wap.uliejh.cn/bnews/652568.htm
- http://m.wap.uliejh.cn/bnews/9234319.htm
- http://m.wap.uliejh.cn/bnews/16401.htm
- http://m.wap.uliejh.cn/bnews/0757.htm
- http://m.wap.uliejh.cn/bnews/11760.htm
- http://m.wap.uliejh.cn/bnews/8236.htm
- http://m.wap.uliejh.cn/bnews/1755.htm
- http://m.wap.uliejh.cn/bnews/80313.htm
- http://m.wap.uliejh.cn/bnews/999038.htm
- http://m.wap.uliejh.cn/bnews/9998430.htm
- http://m.wap.uliejh.cn/bnews/6499921.htm
- http://m.wap.uliejh.cn/bnews/6810418.htm
- http://m.wap.uliejh.cn/bnews/9317190.htm
- http://m.wap.uliejh.cn/bnews/360745.htm
- http://m.wap.uliejh.cn/bnews/9379918.htm
- http://m.wap.uliejh.cn/bnews/5622605.htm
- http://m.wap.uliejh.cn/bnews/3544961.htm
- http://m.wap.uliejh.cn/bnews/1347705.htm
- http://m.wap.uliejh.cn/bnews/25656.htm
- http://m.wap.uliejh.cn/bnews/9219770.htm
- http://m.wap.uliejh.cn/bnews/87945.htm
- http://m.wap.uliejh.cn/bnews/951591.htm
- http://m.wap.uliejh.cn/bnews/0334.htm
- http://m.wap.uliejh.cn/bnews/6004776.htm
- http://m.wap.uliejh.cn/bnews/85308.htm
- http://m.wap.uliejh.cn/bnews/67344.htm
- http://m.wap.uliejh.cn/bnews/2921874.htm
- http://m.wap.uliejh.cn/bnews/054090.htm
- http://m.wap.uliejh.cn/bnews/432744.htm
- http://m.wap.uliejh.cn/bnews/4030.htm
- http://m.wap.uliejh.cn/bnews/39480.htm
- http://m.wap.uliejh.cn/bnews/68209.htm
- http://m.wap.uliejh.cn/bnews/5762166.htm
- http://m.wap.uliejh.cn/bnews/287476.htm
- http://m.wap.uliejh.cn/bnews/0580381.htm
- http://m.wap.uliejh.cn/bnews/83804.htm
- http://m.wap.uliejh.cn/bnews/8514.htm
- http://m.wap.uliejh.cn/bnews/4423.htm
- http://m.wap.uliejh.cn/bnews/7010.htm
- http://m.wap.uliejh.cn/bnews/102640.htm
- http://m.wap.uliejh.cn/bnews/7153120.htm
- http://m.wap.uliejh.cn/bnews/14549.htm
- http://m.wap.uliejh.cn/bnews/3744.htm
- http://m.wap.uliejh.cn/bnews/99842.htm
- http://m.wap.uliejh.cn/bnews/4804.htm
- http://m.wap.uliejh.cn/bnews/591449.htm
- http://m.wap.uliejh.cn/bnews/3994.htm
- http://m.wap.uliejh.cn/bnews/98894.htm
- http://m.wap.uliejh.cn/bnews/91690.htm
- http://m.wap.uliejh.cn/bnews/222793.htm
- http://m.wap.uliejh.cn/bnews/7728720.htm

## 项目结构

```
webindex/
├── data/                                 # 数据配置目录
│   ├── sources.json                      # 核心链接数据源，包含所有收录URL及元数据
│   ├── categories.json                   # 目录层级定义，描述分类树及显示顺序
│   └── health/                           # 健康检查结果缓存目录，由探测任务自动生成
│       └── status.db                     # SQLite数据库，存储最近一次探测状态
├── src/                                  # 源代码根目录
│   ├── core/                             # 核心逻辑模块
│   │   ├── loader.js                     # 加载并验证sources.json与categories.json
│   │   ├── indexer.js                    # 构建内存倒排索引，提供检索接口
│   │   └── health.js                     # 并发HTTP探测调度器，超时与重试策略
│   ├── server/                           # 服务端相关模块
│   │   ├── app.js                        # Express应用主入口，路由挂载与中间件配置
│   │   ├── routes/                       # 路由定义目录
│   │   │   ├── api.js                    # RESTful接口，提供前端数据拉取
│   │   │   └── page.js                   # 页面渲染路由，处理SPA回退
│   │   └── middleware/                   # 自定义中间件
│   │       ├── cors.js                   # 跨域资源共享策略
│   │       └── logger.js                 # 访问日志记录
│   ├── client/                           # 前端资源目录
│   │   ├── styles/                       # 样式源码（SCSS）
│   │   │   ├── base/                     # 全局重置与变量定义
│   │   │   ├── components/               # 卡片、导航栏、搜索框组件样式
│   │   │   └── themes/                   # 浅色与暗色主题变量覆盖
│   │   ├── scripts/                      # 客户端JavaScript（ES模块）
│   │   │   ├── app.js                    # 页面初始化，注册事件监听
│   │   │   ├── search.js                 # 搜索交互与结果渲染
│   │   │   └── health.js                 # 健康状态徽章更新逻辑
│   │   └── assets/                       # 静态图片与字体资源
│   └── templates/                        # 服务端模板（EJS）
│       ├── index.ejs                     # 主页面结构
│       └── partials/                     # 可复用的头部、底部与卡片片段
├── tests/                                 # 单元测试与集成测试
│   ├── unit/                              # 针对loader、indexer的独立测试
│   └── integration/                       # API端点与健康检查流程测试
├── scripts/                               # 辅助工具脚本
│   ├── build.js                           # 生产环境构建脚本，调用esbuild
│   └── health-cron.js                     # 定时健康检查任务，可配置cron表达式
├── config/                                # 环境配置文件
│   ├── default.json                       # 基础配置，端口、超时阈值
│   └── production.json                    # 生产环境覆盖配置
├── dist/                                  # 构建输出目录（生成后出现）
│   ├── client/                            # 打包后的CSS与JS文件
│   └── server/                            # 编译后的服务端代码
├── .github/                               # GitHub Actions工作流定义
│   └── workflows/
│       ├── ci.yml                         # 持续集成流程，执行测试与构建
│       └── health-check.yml               # 定时运行健康检查并提交状态
├── package.json                           # npm依赖清单与脚本定义
├── README.md                              # 项目说明文档（当前文件）
└── LICENSE                                # MIT许可证文本
```

## 贡献指南

1. 复刻仓库并创建功能分支：从主仓库复刻至个人账户，随后在本地新建分支，分支名称需体现修改意图，例如 `feat/add-dark-theme` 或 `fix/health-check-timeout`。

2. 完成代码修改并确保通过所有测试：在提交前运行 `npm test` 验证单元测试与集成测试全部通过。若新增功能，需同步补充对应测试用例，测试覆盖率不得低于80%。

3. 遵循编码规范并格式化代码：项目使用ESLint与Prettier统一代码风格，提交前执行 `npm run lint` 与 `npm run format` 自动修复格式问题。

4. 提交变更并推送到远程复刻仓库：提交信息采用语义化格式，首行简短描述（不超过50字符），后续可补充详细说明。推送后通过GitHub界面发起Pull Request至主仓库的main分支。

5. 参与代码评审并协同修改：维护者将在Pull Request中给出评审意见，贡献者需根据反馈进行调整。合并前需确保所有对话已解决且CI流水线状态为绿色。

## 常见问题

**问：健康检查功能是否会对外部站点造成压力？**

答：健康检查模块采用单线程并发控制，默认并发数为5，超时设置为3秒，且每个URL在24小时内仅探测一次。探测请求使用标准的HEAD方法（若服务器不支持则降级为GET并取消响应体接收），不会造成显著的流量消耗。用户可在配置文件中调整并发数或完全禁用该功能。

**问：如何迁移现有浏览器书签至WebIndex？**

答：主流浏览器支持导出书签为HTML文件，WebIndex提供了转换工具脚本 `scripts/import-bookmark.js`，可将该HTML文件解析并生成符合 `sources.json` 结构的输出。执行命令为 `node scripts/import-bookmark.js --input bookmarks.html --output data/sources.json`。迁移后需手动按分类整理，因为浏览器标签与WebIndex的层级语义存在差异。

**问：WebIndex是否支持多用户或权限控制？**

答：当前版本定位为个人或小团队内部使用的静态导航工具，不内置用户认证与细粒度权限系统。若需要多用户隔离，建议采用多实例部署，每个实例使用独立的 `data/sources.json` 文件，或通过反向代理基于路径路由至不同进程。未来的路线图考虑增加基于API Key的简单鉴权，但不支持OAuth或LDAP等企业级方案。

## 许可证

MIT

> 外链数量: 250 | 生成时间: 2026-08-24 23:40:21
