# WebLink Navigator

WebLink Navigator 是一个面向技术研究者与内容聚合者的轻量级外链导航与资源归档系统。该项目定位于解决大规模 URL 资源的可维护性、可追溯性与可展示性问题，特别适用于需要定期整理与发布外部链接集合的技术社区、开源文档站点以及个人知识库管理者。用户可通过本项目快速构建一个结构化的外链门户，将散落的网络资源转化为可检索、可分类、可分享的标准化链接库。

本项目第 38/120 批次集成共计 250 个外部资源链接，并提供统一的元数据描述框架与访问状态监测接口，帮助运维人员高效管理海量外链数据。

## 功能概览

**批量链接导入与解析**：支持从纯文本、CSV 及 JSON 格式批量导入 URL 列表，自动解析协议、域名与路径结构，生成标准化的内部记录对象。

**链接状态健康检查**：内置异步 HTTP 探测器，可定期对全部或指定链接发起 HEAD/GET 请求，记录响应码、响应时间与内容哈希，便于及时发现失效或篡改资源。

**分类标签与全文检索**：允许为每条链接附加多级标签（如 technology、tutorial、reference）及自定义备注，并基于 SQLite FTS5 提供轻量级全文检索能力，支持按标签、域名、关键词组合筛选。

**响应式目录展示**：提供基于 ASCII 树形结构的可视化目录生成器，可输出项目内部分类层级关系，同时支持生成静态 HTML 目录页，方便内网或公网部署。

**访问统计与热度排序**：记录每条链接的点击次数、最后访问时间与来源 IP 聚合信息，支持按热度、新增时间、响应速度等多种维度排序输出列表。

**数据导入导出接口**：提供 RESTful API 与命令行工具两种方式，支持将链接库导出为 Markdown 列表、JSON 数组或 CSV 表格，便于与其他系统集成或生成文档。

**多批次增量管理**：支持分批导入（如第 38/120 批），保留批次标签与导入日志，允许按批次回滚、比对与增量更新，解决大规模链接库的版本管理问题。

## 应用场景

技术文档站点的外链附录管理：开源项目文档站通常需要在末尾附带大量参考链接、工具站或社区讨论帖。WebLink Navigator 可帮助文档维护者将这些链接统一录入、分类并自动生成 Markdown 格式的资源列表，直接嵌入 README 或 Wiki 页面，避免手工排版与链接腐坏问题。

个人知识库的网页归档索引：研究者或博主在日常阅读中积累大量临时性网页链接，使用本系统可快速输入链接、添加备注与标签，并定期运行健康检查，及时清理失效条目，维持知识库的整洁与可用性。

社区资源聚合页的持续集成：技术社区或线上课程运营方需要周期性发布“每周好文”、“工具推荐”等聚合内容。通过本系统的批次管理功能，运营者可按周或按主题创建导入批次（如第 38 批），自动生成带时间戳的资源列表，并对外发布为静态页面，极大降低重复性编辑工作。

内部运维团队的链接监控看板：企业运维团队需监控众多内部系统控制台、监控面板及文档入口的可用性。本系统可配置为定时轮询这些内部链接，当检测到连续失败时触发告警，并提供可视化状态看板，帮助团队快速定位故障入口。

## 快速开始

以下指令适用于 Linux / macOS / Windows WSL 环境，要求已安装 Git 与 Node.js 18.x 及以上版本。

```bash
# 克隆项目仓库
git clone https://github.com/weblink-navigator/weblink-navigator.git
cd weblink-navigator

# 安装依赖（使用 npm）
npm install

# 初始化本地数据库与配置文件
npm run init

# 导入当前批次（第 38 批）资源链接
npm run import -- --batch 38 --source ./data/batch_38.txt

# 启动开发服务器，默认监听 3000 端口
npm run dev
```

访问 http://localhost:3000 即可查看链接列表与目录树视图。如需生产部署，请执行 `npm run build` 与 `npm start`。

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|---|---|---|
| Node.js | 18.x 或 20.x LTS | 运行时环境，需支持 ES2022 与原生 fetch |
| npm | 8.x 或 9.x | 包管理工具，用于安装依赖与执行脚本 |
| SQLite3 | 3.35 以上（内嵌） | 内置轻量数据库，无需额外安装，用于存储链接元数据与索引 |
| Git | 2.25 以上 | 用于克隆仓库及版本管理 |
| 网络环境 | 可访问公网（用于健康检查） | 若需对外链进行状态探测，需确保运行环境可访问目标域名 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|---|---|---|
| 用户手册 | /docs/user-guide.md | 如何导入链接、查看列表、执行健康检查与导出报告 |
| 运维手册 | /docs/ops-guide.md | 如何配置定时任务、调整检查并发数、备份数据库与迁移批次 |
| API 参考 | /docs/api-reference.md | 提供哪些 REST 接口、请求参数格式与返回数据结构 |
| 开发指南 | /docs/dev-guide.md | 项目模块划分、如何扩展新的导入格式、如何自定义展示模板 |

## 资源列表

- http://m.3g.uliejh.cn/nnews/5430026.htm
- http://m.3g.uliejh.cn/nnews/7807.htm
- http://m.3g.uliejh.cn/nnews/1661.htm
- http://m.3g.uliejh.cn/nnews/9372.htm
- http://m.3g.uliejh.cn/nnews/423974.htm
- http://m.3g.uliejh.cn/nnews/7714810.htm
- http://m.3g.uliejh.cn/nnews/9930060.htm
- http://m.3g.uliejh.cn/nnews/56674.htm
- http://m.3g.uliejh.cn/nnews/9672469.htm
- http://m.3g.uliejh.cn/nnews/4615447.htm
- http://m.3g.uliejh.cn/nnews/0174.htm
- http://m.3g.uliejh.cn/nnews/571329.htm
- http://m.3g.uliejh.cn/nnews/587305.htm
- http://m.3g.uliejh.cn/nnews/29255.htm
- http://m.3g.uliejh.cn/nnews/3890127.htm
- http://m.3g.uliejh.cn/nnews/6633.htm
- http://m.3g.uliejh.cn/nnews/704164.htm
- http://m.3g.uliejh.cn/nnews/938511.htm
- http://m.3g.uliejh.cn/nnews/543854.htm
- http://m.3g.uliejh.cn/nnews/5927730.htm
- http://m.3g.uliejh.cn/nnews/2283658.htm
- http://m.3g.uliejh.cn/nnews/4787082.htm
- http://m.3g.uliejh.cn/nnews/21353.htm
- http://m.3g.uliejh.cn/nnews/80404.htm
- http://m.3g.uliejh.cn/nnews/6021.htm
- http://m.3g.uliejh.cn/nnews/3625.htm
- http://m.3g.uliejh.cn/nnews/6552.htm
- http://m.3g.uliejh.cn/nnews/1310.htm
- http://m.3g.uliejh.cn/nnews/53040.htm
- http://m.3g.uliejh.cn/nnews/3929476.htm
- http://m.3g.uliejh.cn/nnews/8351.htm
- http://m.3g.uliejh.cn/nnews/6674076.htm
- http://m.3g.uliejh.cn/nnews/7049.htm
- http://m.3g.uliejh.cn/nnews/2539641.htm
- http://m.3g.uliejh.cn/nnews/6739872.htm
- http://m.3g.uliejh.cn/nnews/6204357.htm
- http://m.3g.uliejh.cn/nnews/71119.htm
- http://m.3g.uliejh.cn/nnews/5999238.htm
- http://m.3g.uliejh.cn/nnews/975522.htm
- http://m.3g.uliejh.cn/nnews/344395.htm
- http://m.3g.uliejh.cn/nnews/7716296.htm
- http://m.3g.uliejh.cn/nnews/809961.htm
- http://m.3g.uliejh.cn/nnews/7396.htm
- http://m.3g.uliejh.cn/nnews/23892.htm
- http://m.3g.uliejh.cn/nnews/353103.htm
- http://m.3g.uliejh.cn/nnews/88228.htm
- http://m.3g.uliejh.cn/nnews/27303.htm
- http://m.3g.uliejh.cn/nnews/3702616.htm
- http://m.3g.uliejh.cn/nnews/7617.htm
- http://m.3g.uliejh.cn/nnews/37626.htm
- http://m.3g.uliejh.cn/nnews/0956.htm
- http://m.3g.uliejh.cn/nnews/788314.htm
- http://m.3g.uliejh.cn/nnews/2932.htm
- http://m.3g.uliejh.cn/nnews/1161049.htm
- http://m.3g.uliejh.cn/nnews/9237490.htm
- http://m.3g.uliejh.cn/nnews/6347.htm
- http://m.3g.uliejh.cn/nnews/0426350.htm
- http://m.3g.uliejh.cn/nnews/53002.htm
- http://m.3g.uliejh.cn/nnews/8043.htm
- http://m.3g.uliejh.cn/nnews/5571.htm
- http://m.3g.uliejh.cn/nnews/6369.htm
- http://m.3g.uliejh.cn/nnews/2087.htm
- http://m.3g.uliejh.cn/nnews/555482.htm
- http://m.3g.uliejh.cn/nnews/605671.htm
- http://m.3g.uliejh.cn/nnews/26007.htm
- http://m.3g.uliejh.cn/nnews/9673769.htm
- http://m.3g.uliejh.cn/nnews/290664.htm
- http://m.3g.uliejh.cn/nnews/6950.htm
- http://m.3g.uliejh.cn/nnews/086772.htm
- http://m.3g.uliejh.cn/nnews/45156.htm
- http://m.3g.uliejh.cn/nnews/4829.htm
- http://m.3g.uliejh.cn/nnews/335002.htm
- http://m.3g.uliejh.cn/nnews/4439293.htm
- http://m.3g.uliejh.cn/nnews/179534.htm
- http://m.3g.uliejh.cn/nnews/1347.htm
- http://m.3g.uliejh.cn/nnews/949376.htm
- http://m.3g.uliejh.cn/nnews/706261.htm
- http://m.3g.uliejh.cn/nnews/52711.htm
- http://m.3g.uliejh.cn/nnews/4746175.htm
- http://m.3g.uliejh.cn/nnews/801801.htm
- http://m.3g.uliejh.cn/nnews/1234271.htm
- http://m.3g.uliejh.cn/nnews/7416913.htm
- http://m.3g.uliejh.cn/nnews/1776.htm
- http://m.3g.uliejh.cn/nnews/36466.htm
- http://m.3g.uliejh.cn/nnews/89218.htm
- http://m.3g.uliejh.cn/nnews/314895.htm
- http://m.3g.uliejh.cn/nnews/2168.htm
- http://m.3g.uliejh.cn/nnews/32976.htm
- http://m.3g.uliejh.cn/nnews/00653.htm
- http://m.3g.uliejh.cn/nnews/3876251.htm
- http://m.3g.uliejh.cn/nnews/394960.htm
- http://m.3g.uliejh.cn/nnews/2011772.htm
- http://m.3g.uliejh.cn/nnews/00693.htm
- http://m.3g.uliejh.cn/nnews/148959.htm
- http://m.3g.uliejh.cn/nnews/6429.htm
- http://m.3g.uliejh.cn/nnews/6155.htm
- http://m.3g.uliejh.cn/nnews/648919.htm
- http://m.3g.uliejh.cn/nnews/397884.htm
- http://m.3g.uliejh.cn/nnews/6224.htm
- http://m.3g.uliejh.cn/nnews/39603.htm
- http://m.3g.uliejh.cn/nnews/6781.htm
- http://m.3g.uliejh.cn/nnews/530326.htm
- http://m.3g.uliejh.cn/nnews/3864.htm
- http://m.3g.uliejh.cn/nnews/380734.htm
- http://m.3g.uliejh.cn/nnews/6639849.htm
- http://m.3g.uliejh.cn/nnews/63665.htm
- http://m.3g.uliejh.cn/nnews/9773.htm
- http://m.3g.uliejh.cn/nnews/8352.htm
- http://m.3g.uliejh.cn/nnews/135829.htm
- http://m.3g.uliejh.cn/nnews/17332.htm
- http://m.3g.uliejh.cn/nnews/63818.htm
- http://m.3g.uliejh.cn/nnews/5078440.htm
- http://m.3g.uliejh.cn/nnews/161930.htm
- http://m.3g.uliejh.cn/nnews/03378.htm
- http://m.3g.uliejh.cn/nnews/52999.htm
- http://m.3g.uliejh.cn/nnews/1202.htm
- http://m.3g.uliejh.cn/nnews/7148.htm
- http://m.3g.uliejh.cn/nnews/9664981.htm
- http://m.3g.uliejh.cn/nnews/91127.htm
- http://m.3g.uliejh.cn/nnews/29235.htm
- http://m.3g.uliejh.cn/nnews/2239.htm
- http://m.3g.uliejh.cn/nnews/5023.htm
- http://m.3g.uliejh.cn/nnews/30064.htm
- http://m.3g.uliejh.cn/nnews/8157.htm
- http://m.3g.uliejh.cn/nnews/9306.htm
- http://m.3g.uliejh.cn/nnews/740782.htm
- http://m.3g.uliejh.cn/nnews/45237.htm
- http://m.3g.uliejh.cn/nnews/86397.htm
- http://m.3g.uliejh.cn/nnews/4949669.htm
- http://m.3g.uliejh.cn/nnews/97076.htm
- http://m.3g.uliejh.cn/nnews/5770173.htm
- http://m.3g.uliejh.cn/nnews/5917.htm
- http://m.3g.uliejh.cn/nnews/73808.htm
- http://m.3g.uliejh.cn/nnews/360461.htm
- http://m.3g.uliejh.cn/nnews/33909.htm
- http://m.3g.uliejh.cn/nnews/2017976.htm
- http://m.3g.uliejh.cn/nnews/18354.htm
- http://m.3g.uliejh.cn/nnews/024234.htm
- http://m.3g.uliejh.cn/nnews/8656.htm
- http://m.3g.uliejh.cn/nnews/0032753.htm
- http://m.3g.uliejh.cn/nnews/8504659.htm
- http://m.3g.uliejh.cn/nnews/1620944.htm
- http://m.3g.uliejh.cn/nnews/6231.htm
- http://m.3g.uliejh.cn/nnews/9235965.htm
- http://m.3g.uliejh.cn/nnews/3998774.htm
- http://m.3g.uliejh.cn/nnews/884905.htm
- http://m.3g.uliejh.cn/nnews/3234001.htm
- http://m.3g.uliejh.cn/nnews/4452856.htm
- http://m.3g.uliejh.cn/nnews/97062.htm
- http://m.3g.uliejh.cn/nnews/0616699.htm
- http://m.3g.uliejh.cn/nnews/86463.htm
- http://m.3g.uliejh.cn/nnews/70853.htm
- http://m.3g.uliejh.cn/nnews/4700665.htm
- http://m.3g.uliejh.cn/nnews/02347.htm
- http://m.3g.uliejh.cn/nnews/50718.htm
- http://m.3g.uliejh.cn/nnews/2843688.htm
- http://m.3g.uliejh.cn/nnews/689998.htm
- http://m.3g.uliejh.cn/nnews/4922.htm
- http://m.3g.uliejh.cn/nnews/4187.htm
- http://m.3g.uliejh.cn/nnews/5959.htm
- http://m.3g.uliejh.cn/nnews/57275.htm
- http://m.3g.uliejh.cn/nnews/3672.htm
- http://m.3g.uliejh.cn/nnews/67544.htm
- http://m.3g.uliejh.cn/nnews/127392.htm
- http://m.3g.uliejh.cn/nnews/52595.htm
- http://m.3g.uliejh.cn/nnews/08710.htm
- http://m.3g.uliejh.cn/nnews/847802.htm
- http://m.3g.uliejh.cn/nnews/537067.htm
- http://m.3g.uliejh.cn/nnews/39286.htm
- http://m.3g.uliejh.cn/nnews/3196939.htm
- http://m.3g.uliejh.cn/nnews/1957.htm
- http://m.3g.uliejh.cn/nnews/20557.htm
- http://m.3g.uliejh.cn/nnews/12546.htm
- http://m.3g.uliejh.cn/nnews/9636197.htm
- http://m.3g.uliejh.cn/nnews/90403.htm
- http://m.3g.uliejh.cn/nnews/1142.htm
- http://m.3g.uliejh.cn/nnews/4424.htm
- http://m.3g.uliejh.cn/nnews/94239.htm
- http://m.3g.uliejh.cn/nnews/621340.htm
- http://m.3g.uliejh.cn/nnews/2008.htm
- http://m.3g.uliejh.cn/nnews/1048242.htm
- http://m.3g.uliejh.cn/nnews/0819.htm
- http://m.3g.uliejh.cn/nnews/657558.htm
- http://m.3g.uliejh.cn/nnews/75025.htm
- http://m.3g.uliejh.cn/nnews/01041.htm
- http://m.3g.uliejh.cn/nnews/222958.htm
- http://m.3g.uliejh.cn/nnews/322684.htm
- http://m.3g.uliejh.cn/nnews/4712.htm
- http://m.3g.uliejh.cn/nnews/4578827.htm
- http://m.3g.uliejh.cn/nnews/3523761.htm
- http://m.3g.uliejh.cn/nnews/80149.htm
- http://m.3g.uliejh.cn/nnews/8378.htm
- http://m.3g.uliejh.cn/nnews/1169497.htm
- http://m.3g.uliejh.cn/nnews/9302843.htm
- http://m.3g.uliejh.cn/nnews/04190.htm
- http://m.3g.uliejh.cn/nnews/4114083.htm
- http://m.3g.uliejh.cn/nnews/4911290.htm
- http://m.3g.uliejh.cn/nnews/3198456.htm
- http://m.3g.uliejh.cn/nnews/0166.htm
- http://m.3g.uliejh.cn/nnews/1175.htm
- http://m.3g.uliejh.cn/nnews/4600914.htm
- http://m.3g.uliejh.cn/nnews/5069.htm
- http://m.3g.uliejh.cn/nnews/2796195.htm
- http://m.3g.uliejh.cn/nnews/11478.htm
- http://m.3g.uliejh.cn/nnews/6818.htm
- http://m.3g.uliejh.cn/nnews/85389.htm
- http://m.3g.uliejh.cn/nnews/061418.htm
- http://m.3g.uliejh.cn/nnews/116818.htm
- http://m.3g.uliejh.cn/nnews/4137.htm
- http://m.3g.uliejh.cn/nnews/7998785.htm
- http://m.3g.uliejh.cn/nnews/92653.htm
- http://m.3g.uliejh.cn/nnews/29393.htm
- http://m.3g.uliejh.cn/nnews/2566111.htm
- http://m.3g.uliejh.cn/nnews/2349.htm
- http://m.3g.uliejh.cn/nnews/4048.htm
- http://m.3g.uliejh.cn/nnews/8354301.htm
- http://m.3g.uliejh.cn/nnews/760137.htm
- http://m.3g.uliejh.cn/nnews/478509.htm
- http://m.3g.uliejh.cn/nnews/59067.htm
- http://m.3g.uliejh.cn/nnews/32490.htm
- http://m.3g.uliejh.cn/nnews/0791481.htm
- http://m.3g.uliejh.cn/nnews/21902.htm
- http://m.3g.uliejh.cn/nnews/1682714.htm
- http://m.3g.uliejh.cn/nnews/8546.htm
- http://m.3g.uliejh.cn/nnews/296308.htm
- http://m.3g.uliejh.cn/nnews/03983.htm
- http://m.3g.uliejh.cn/nnews/60819.htm
- http://m.3g.uliejh.cn/nnews/6302741.htm
- http://m.3g.uliejh.cn/nnews/81518.htm
- http://m.3g.uliejh.cn/nnews/9869.htm
- http://m.3g.uliejh.cn/nnews/9331.htm
- http://m.3g.uliejh.cn/nnews/713457.htm
- http://m.3g.uliejh.cn/nnews/418599.htm
- http://m.3g.uliejh.cn/nnews/7126821.htm
- http://m.3g.uliejh.cn/nnews/2769448.htm
- http://m.3g.uliejh.cn/nnews/2538.htm
- http://m.3g.uliejh.cn/nnews/4278.htm
- http://m.3g.uliejh.cn/nnews/8588.htm
- http://m.3g.uliejh.cn/nnews/5550.htm
- http://m.3g.uliejh.cn/nnews/7088563.htm
- http://m.3g.uliejh.cn/nnews/70264.htm
- http://m.3g.uliejh.cn/nnews/309580.htm
- http://m.3g.uliejh.cn/nnews/315132.htm
- http://m.3g.uliejh.cn/nnews/168477.htm
- http://m.3g.uliejh.cn/nnews/46354.htm
- http://m.3g.uliejh.cn/nnews/7196.htm
- http://m.3g.uliejh.cn/nnews/5584404.htm
- http://m.3g.uliejh.cn/nnews/7373.htm
- http://m.3g.uliejh.cn/nnews/64079.htm
- http://m.3g.uliejh.cn/nnews/3092703.htm

## 项目结构

```
weblink-navigator/
├── src/
│   ├── core/                        # 核心数据模型与业务逻辑
│   │   ├── linkRecord.js            # 链接记录对象定义（字段、校验、序列化）
│   │   ├── batchManager.js          # 批次导入、查询、回滚与状态管理
│   │   └── healthChecker.js         # 异步健康检查调度器，支持超时与重试策略
│   ├── api/                         # RESTful API 路由层
│   │   ├── routes.js                # 路由注册与中间件挂载
│   │   └── controllers/             # 资源控制器（列表、详情、导入、导出）
│   ├── cli/                         # 命令行工具入口
│   │   ├── importCmd.js             # 导入命令实现，支持 txt/csv/json
│   │   ├── checkCmd.js              # 手动触发健康检查命令
│   │   └── exportCmd.js             # 导出为 markdown/json/csv 格式
│   ├── db/                          # 数据库层
│   │   ├── schema.sql               # SQLite 表结构定义（链接表、批次表、日志表）
│   │   ├── migration.js             # 版本迁移与增量更新脚本
│   │   └── repository.js            # CRUD 操作封装与查询构建器
│   ├── ui/                          # 前端展示相关
│   │   ├── asciiTreeGenerator.js    # 生成 ASCII 目录树的工具函数
│   │   ├── static/                  # 静态资源（CSS、客户端 JS）
│   │   └── templates/               # 服务端渲染模板（列表页、详情页、管理页）
│   ├── utils/                       # 通用工具函数
│   │   ├── urlParser.js             # URL 解析、域名提取、路径规范化
│   │   ├── logger.js                # 分级日志输出（info/warn/error）与轮转
│   │   └── configLoader.js          # 加载 .env 与 config.json，合并默认配置
│   └── index.js                     # 应用主入口，启动服务器与初始化数据库
├── data/
│   ├── batch_38.txt                 # 第 38 批原始链接列表（纯文本）
│   ├── batch_38_imported.json       # 导入后的元数据缓存（含分类建议）
│   └── weblink.db                   # SQLite 数据库文件（自动生成）
├── docs/                            # 文档目录（用户手册、运维手册等）
├── tests/                           # 单元测试与集成测试脚本
│   ├── unit/                        # 核心模块单元测试（使用 jest）
│   └── integration/                 # API 与数据库集成测试
├── .env.example                     # 环境变量模板（端口、检查间隔、超时阈值）
├── package.json                     # npm 依赖与脚本定义
├── README.md                        # 项目说明文档（即当前文件）
└── LICENSE                          # MIT 许可证文件
```

## 贡献指南

1. 在 GitHub 上 Fork 本仓库，并克隆到本地开发环境。请确保基于 main 分支创建新的特性分支，分支命名建议采用 `feature/功能简述` 或 `fix/问题简述` 格式。

2. 运行 `npm install` 安装所有依赖，并执行 `npm run test` 确认现有测试用例全部通过。新增功能或修复缺陷时，需同步编写对应的单元测试或集成测试，覆盖率不应低于 80%。

3. 提交代码前，请执行 `npm run lint` 与 `npm run format` 统一代码风格（配置基于 ESLint + Prettier）。提交信息应遵循 Conventional Commits 规范，即采用 `type: subject` 格式，其中 type 可为 feat、fix、docs、refactor、test 等。

4. 若涉及数据库 schema 变更，请在 `src/db/migration.js` 中添加对应的迁移版本号与升级/回滚函数，并确保 `schema.sql` 同步更新。建议附带模拟数据脚本以便 reviewers 验证。

5. 发起 Pull Request 至主仓库的 main 分支，并在 PR 描述中清晰说明改动目的、影响范围以及测试结果。至少需获得一名项目维护者的代码评审通过后方可合并。

## 常见问题

**Q：健康检查会对目标服务器造成压力吗？**

A：系统默认采用单并发顺序检查，且每个请求超时时间设定为 5 秒，同时内置指数退避重试机制（最多 2 次）。对于大规模链接库（如超过 1000 条），建议通过 `--concurrency` 参数限制并行数（默认 5），并在非业务高峰期执行。检查结果会缓存在本地数据库，避免短时间内重复探测相同域名。

**Q：如何迁移或备份已有的链接数据？**

A：所有链接元数据存储在 `data/weblink.db` 文件中，直接复制该文件即可完成全量备份。若需迁移至其他服务器，只需携带该数据库文件及 `.env` 配置文件，在新环境执行 `npm run migrate` 自动适配表结构。同时支持通过 `npm run export -- --format json` 导出为纯 JSON 文件，便于跨数据库平台迁移。

**Q：导入链接时能否自动识别重复条目？**

A：系统基于 URL 的标准化形式（去除末尾斜杠及 utm 参数后）计算哈希指纹，在导入过程中自动去重。若发现相同 URL 已存在于数据库，则默认跳过并记录警告日志，同时可通过 `--overwrite` 选项强制更新已有记录的备注或标签字段。去重阈值与匹配规则可在 `config.json` 中调整。

## 许可证

MIT

> 外链数量: 250 | 生成时间: 2026-08-24 23:40:21
