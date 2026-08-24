# WebNavi Indexer

WebNavi Indexer 是一个轻量级的技术资源导航与外链汇总工具，专为需要批量管理、分类展示和快速检索大量外部链接的开发团队与内容创作者设计。该项目将分散的 URL 资源以结构化方式组织，提供统一的访问入口与元数据管理能力，适用于文档站、知识库、内部工具链导航等场景。

目标用户包括技术文档维护者、开源项目社区运营人员、技术培训讲师以及需要定期整理外部参考资源的研发团队。WebNavi Indexer 不依赖数据库，基于纯静态 Markdown 与 JSON 数据驱动，可无缝集成至现有的静态站点生成器或 CI/CD 工作流。

## 功能概览

批量链接导入与自动校验：支持从 CSV、JSON 或纯文本列表中批量导入 URL，自动检测协议头、域名格式与状态码，过滤无效或重复链接。

多维度分类与标签系统：每个链接可归属于多个分类（如前端、后端、运维），支持自定义标签，便于按主题或难度层级筛选。

链接元数据增强：内置链接标题提取、描述摘要生成、关键词抽取功能，也可手动补充备注、维护人、更新周期等信息。

状态监控与健康检查：定时对已收录链接发起 HEAD 请求，检测响应状态、重定向链、证书有效期，异常时输出报警日志。

静态站点导出：将链接数据渲染为响应式 HTML 目录页，支持搜索、排序、按标签过滤，导出产物可独立部署至任何 Web 服务器。

RESTful API 查询接口：提供 JSON 格式的链接查询 API，支持按分类、标签、关键词模糊匹配，方便其他系统集成调用。

配置化分类模板：内置技术资源常用分类模板（博客、教程、工具库、视频、官方文档），可一键应用或自定义扩展。

操作审计日志：记录链接的添加、修改、删除及状态变更历史，支持回滚至任意历史版本。

## 应用场景

技术文档站外链管理：大型开源项目文档中包含大量外部参考链接，使用 WebNavi Indexer 统一维护这些链接，可自动检查失效，并在文档构建时嵌入最新有效的链接列表。

内部研发工具链导航：企业内网中部署多个研发平台（代码仓库、CI 系统、监控面板、日志平台），通过 WebNavi Indexer 构建单页导航，并定时检测各平台可用性。

课程资源索引：技术培训讲师在每期课程中提供数百篇延伸阅读资料链接，WebNavi Indexer 可按周次或主题分类导出为静态页面，供学员自行检索。

开源社区外部资源聚合：开源社区 README 或 Wiki 中需引用大量外部项目、文章、视频，WebNavi Indexer 自动生成 Markdown 资源列表，减少手动维护负担。

技术雷达与工具调研：技术选型团队定期收集各类工具、框架、平台的链接，通过标签与分类进行横向对比，监控项目活跃度与文档更新频率。

## 快速开始

以下命令完成项目克隆、依赖安装与本地开发服务器启动。

```bash
git clone https://github.com/webnavi/indexer.git
cd indexer
npm install
npm run dev
```

执行完成后，访问终端输出的本地地址（通常为 http://localhost:5173）即可查看链接管理面板。首次启动会自动加载示例数据。

## 安装要求

| 依赖 | 必需版本 | 说明 |
|------|----------|------|
| Node.js | 18.x 或 20.x LTS | 运行时环境，推荐使用 nvm 管理版本 |
| npm | 9.x 或以上 | 包管理器，用于安装依赖与执行脚本 |
| Git | 2.30 或以上 | 版本控制，用于克隆仓库与提交变更 |
| curl | 7.68 或以上 | 健康检查模块依赖的命令行工具 |
| jq | 1.6 或以上 | 用于处理 JSON 数据的轻量级命令行工具 |

可选依赖：Pandoc（用于导出 PDF 格式链接目录）、Sass（用于自定义主题样式）。生产部署推荐使用 Nginx 或 Caddy 托管静态导出文件。

## 文档导航

| 层面 | 目录 | 回答的问题 |
|------|------|------------|
| 入门 | docs/getting-started.md | 如何快速上手使用 WebNavi Indexer 进行链接管理 |
| 配置 | docs/configuration.md | 分类模板、监控参数、导出选项等如何定制 |
| API | docs/api-reference.md | RESTful 接口的端点、参数与返回数据结构说明 |
| 运维 | docs/operation-guide.md | 健康检查配置、报警通知、数据备份与迁移方法 |

## 资源列表

- http://m.3g.uliejh.cn/nnews/0195.htm
- http://m.3g.uliejh.cn/nnews/953727.htm
- http://m.3g.uliejh.cn/nnews/3753.htm
- http://m.3g.uliejh.cn/nnews/4544.htm
- http://m.3g.uliejh.cn/nnews/6149.htm
- http://m.3g.uliejh.cn/nnews/567187.htm
- http://m.3g.uliejh.cn/nnews/3181.htm
- http://m.3g.uliejh.cn/nnews/4520450.htm
- http://m.3g.uliejh.cn/nnews/6058349.htm
- http://m.3g.uliejh.cn/nnews/140886.htm
- http://m.3g.uliejh.cn/nnews/9101185.htm
- http://m.3g.uliejh.cn/nnews/2064.htm
- http://m.3g.uliejh.cn/nnews/266819.htm
- http://m.3g.uliejh.cn/nnews/38037.htm
- http://m.3g.uliejh.cn/nnews/1697344.htm
- http://m.3g.uliejh.cn/nnews/4816099.htm
- http://m.3g.uliejh.cn/nnews/4498.htm
- http://m.3g.uliejh.cn/nnews/5070.htm
- http://m.3g.uliejh.cn/nnews/44519.htm
- http://m.3g.uliejh.cn/nnews/1500.htm
- http://m.3g.uliejh.cn/nnews/6839.htm
- http://m.3g.uliejh.cn/nnews/87961.htm
- http://m.3g.uliejh.cn/nnews/8215.htm
- http://m.3g.uliejh.cn/nnews/8419925.htm
- http://m.3g.uliejh.cn/nnews/2890.htm
- http://m.3g.uliejh.cn/nnews/7523918.htm
- http://m.3g.uliejh.cn/nnews/1142671.htm
- http://m.3g.uliejh.cn/nnews/16061.htm
- http://m.3g.uliejh.cn/nnews/0962.htm
- http://m.3g.uliejh.cn/nnews/93558.htm
- http://m.3g.uliejh.cn/nnews/55230.htm
- http://m.3g.uliejh.cn/nnews/145759.htm
- http://m.3g.uliejh.cn/nnews/3987290.htm
- http://m.3g.uliejh.cn/nnews/61181.htm
- http://m.3g.uliejh.cn/nnews/890946.htm
- http://m.3g.uliejh.cn/nnews/91815.htm
- http://m.3g.uliejh.cn/nnews/177005.htm
- http://m.3g.uliejh.cn/nnews/8331.htm
- http://m.3g.uliejh.cn/nnews/913810.htm
- http://m.3g.uliejh.cn/nnews/85305.htm
- http://m.3g.uliejh.cn/nnews/8921070.htm
- http://m.3g.uliejh.cn/nnews/047571.htm
- http://m.3g.uliejh.cn/nnews/691860.htm
- http://m.3g.uliejh.cn/nnews/389740.htm
- http://m.3g.uliejh.cn/nnews/99283.htm
- http://m.3g.uliejh.cn/nnews/5061109.htm
- http://m.3g.uliejh.cn/nnews/159373.htm
- http://m.3g.uliejh.cn/nnews/31195.htm
- http://m.3g.uliejh.cn/nnews/3214.htm
- http://m.3g.uliejh.cn/nnews/042190.htm
- http://m.3g.uliejh.cn/nnews/131081.htm
- http://m.3g.uliejh.cn/nnews/8780362.htm
- http://m.3g.uliejh.cn/nnews/4270.htm
- http://m.3g.uliejh.cn/nnews/05549.htm
- http://m.3g.uliejh.cn/nnews/6679.htm
- http://m.3g.uliejh.cn/nnews/6905.htm
- http://m.3g.uliejh.cn/nnews/6209734.htm
- http://m.3g.uliejh.cn/nnews/217367.htm
- http://m.3g.uliejh.cn/nnews/8805.htm
- http://m.3g.uliejh.cn/nnews/69489.htm
- http://m.3g.uliejh.cn/nnews/2038.htm
- http://m.3g.uliejh.cn/nnews/354790.htm
- http://m.3g.uliejh.cn/nnews/3874.htm
- http://m.3g.uliejh.cn/nnews/09639.htm
- http://m.3g.uliejh.cn/nnews/6604.htm
- http://m.3g.uliejh.cn/nnews/0950.htm
- http://m.3g.uliejh.cn/nnews/14938.htm
- http://m.3g.uliejh.cn/nnews/1202258.htm
- http://m.3g.uliejh.cn/nnews/7994773.htm
- http://m.3g.uliejh.cn/nnews/917326.htm
- http://m.3g.uliejh.cn/nnews/73278.htm
- http://m.3g.uliejh.cn/nnews/04011.htm
- http://m.3g.uliejh.cn/nnews/93662.htm
- http://m.3g.uliejh.cn/nnews/508056.htm
- http://m.3g.uliejh.cn/nnews/6481.htm
- http://m.3g.uliejh.cn/nnews/419748.htm
- http://m.3g.uliejh.cn/nnews/735827.htm
- http://m.3g.uliejh.cn/nnews/5644216.htm
- http://m.3g.uliejh.cn/nnews/466832.htm
- http://m.3g.uliejh.cn/nnews/3810.htm
- http://m.3g.uliejh.cn/nnews/1530.htm
- http://m.3g.uliejh.cn/nnews/60589.htm
- http://m.3g.uliejh.cn/nnews/96476.htm
- http://m.3g.uliejh.cn/nnews/27245.htm
- http://m.3g.uliejh.cn/nnews/6725506.htm
- http://m.3g.uliejh.cn/nnews/9211.htm
- http://m.3g.uliejh.cn/nnews/2523.htm
- http://m.3g.uliejh.cn/nnews/199369.htm
- http://m.3g.uliejh.cn/nnews/7273.htm
- http://m.3g.uliejh.cn/nnews/85883.htm
- http://m.3g.uliejh.cn/nnews/110694.htm
- http://m.3g.uliejh.cn/nnews/459074.htm
- http://m.3g.uliejh.cn/nnews/1722672.htm
- http://m.3g.uliejh.cn/nnews/868350.htm
- http://m.3g.uliejh.cn/nnews/5714.htm
- http://m.3g.uliejh.cn/nnews/316645.htm
- http://m.3g.uliejh.cn/nnews/222966.htm
- http://m.3g.uliejh.cn/nnews/3007.htm
- http://m.3g.uliejh.cn/nnews/0444865.htm
- http://m.3g.uliejh.cn/nnews/44496.htm
- http://m.3g.uliejh.cn/nnews/042843.htm
- http://m.3g.uliejh.cn/nnews/65607.htm
- http://m.3g.uliejh.cn/nnews/5461044.htm
- http://m.3g.uliejh.cn/nnews/84363.htm
- http://m.3g.uliejh.cn/nnews/56000.htm
- http://m.3g.uliejh.cn/nnews/3458.htm
- http://m.3g.uliejh.cn/nnews/751670.htm
- http://m.3g.uliejh.cn/nnews/72146.htm
- http://m.3g.uliejh.cn/nnews/4322.htm
- http://m.3g.uliejh.cn/nnews/8050.htm
- http://m.3g.uliejh.cn/nnews/66742.htm
- http://m.3g.uliejh.cn/nnews/9593756.htm
- http://m.3g.uliejh.cn/nnews/534459.htm
- http://m.3g.uliejh.cn/nnews/39054.htm
- http://m.3g.uliejh.cn/nnews/490647.htm
- http://m.3g.uliejh.cn/nnews/664035.htm
- http://m.3g.uliejh.cn/nnews/3657120.htm
- http://m.3g.uliejh.cn/nnews/743645.htm
- http://m.3g.uliejh.cn/nnews/53311.htm
- http://m.3g.uliejh.cn/nnews/78943.htm
- http://m.3g.uliejh.cn/nnews/05844.htm
- http://m.3g.uliejh.cn/nnews/0872.htm
- http://m.3g.uliejh.cn/nnews/1509128.htm
- http://m.3g.uliejh.cn/nnews/4061251.htm
- http://m.3g.uliejh.cn/nnews/09184.htm
- http://m.3g.uliejh.cn/nnews/3786.htm
- http://m.3g.uliejh.cn/nnews/15110.htm
- http://m.3g.uliejh.cn/nnews/24468.htm
- http://m.3g.uliejh.cn/nnews/6108292.htm
- http://m.3g.uliejh.cn/nnews/6946.htm
- http://m.3g.uliejh.cn/nnews/1169898.htm
- http://m.3g.uliejh.cn/nnews/4885947.htm
- http://m.3g.uliejh.cn/nnews/525514.htm
- http://m.3g.uliejh.cn/nnews/16631.htm
- http://m.3g.uliejh.cn/nnews/999835.htm
- http://m.3g.uliejh.cn/nnews/9762.htm
- http://m.3g.uliejh.cn/nnews/565420.htm
- http://m.3g.uliejh.cn/nnews/7159737.htm
- http://m.3g.uliejh.cn/nnews/053312.htm
- http://m.3g.uliejh.cn/nnews/17350.htm
- http://m.3g.uliejh.cn/nnews/204862.htm
- http://m.3g.uliejh.cn/nnews/849467.htm
- http://m.3g.uliejh.cn/nnews/180199.htm
- http://m.3g.uliejh.cn/nnews/535624.htm
- http://m.3g.uliejh.cn/nnews/7290.htm
- http://m.3g.uliejh.cn/nnews/5694757.htm
- http://m.3g.uliejh.cn/nnews/943598.htm
- http://m.3g.uliejh.cn/nnews/414826.htm
- http://m.3g.uliejh.cn/nnews/1951.htm
- http://m.3g.uliejh.cn/nnews/4261.htm
- http://m.3g.uliejh.cn/nnews/9924965.htm
- http://m.3g.uliejh.cn/nnews/937086.htm
- http://m.3g.uliejh.cn/nnews/936326.htm
- http://m.3g.uliejh.cn/nnews/44219.htm
- http://m.3g.uliejh.cn/nnews/81231.htm
- http://m.3g.uliejh.cn/nnews/966398.htm
- http://m.3g.uliejh.cn/nnews/4910.htm
- http://m.3g.uliejh.cn/nnews/14584.htm
- http://m.3g.uliejh.cn/nnews/32161.htm
- http://m.3g.uliejh.cn/nnews/7369226.htm
- http://m.3g.uliejh.cn/nnews/329434.htm
- http://m.3g.uliejh.cn/nnews/5700.htm
- http://m.3g.uliejh.cn/nnews/807162.htm
- http://m.3g.uliejh.cn/nnews/39412.htm
- http://m.3g.uliejh.cn/nnews/5337094.htm
- http://m.3g.uliejh.cn/nnews/3963559.htm
- http://m.3g.uliejh.cn/nnews/0530.htm
- http://m.3g.uliejh.cn/nnews/5293.htm
- http://m.3g.uliejh.cn/nnews/445976.htm
- http://m.3g.uliejh.cn/nnews/62693.htm
- http://m.3g.uliejh.cn/nnews/43694.htm
- http://m.3g.uliejh.cn/nnews/202578.htm
- http://m.3g.uliejh.cn/nnews/50219.htm
- http://m.3g.uliejh.cn/nnews/139814.htm
- http://m.3g.uliejh.cn/nnews/7951.htm
- http://m.3g.uliejh.cn/nnews/4667411.htm
- http://m.3g.uliejh.cn/nnews/71511.htm
- http://m.3g.uliejh.cn/nnews/9751312.htm
- http://m.3g.uliejh.cn/nnews/029135.htm
- http://m.3g.uliejh.cn/nnews/6190765.htm
- http://m.3g.uliejh.cn/nnews/0026.htm
- http://m.3g.uliejh.cn/nnews/8428504.htm
- http://m.3g.uliejh.cn/nnews/287772.htm
- http://m.3g.uliejh.cn/nnews/286530.htm
- http://m.3g.uliejh.cn/nnews/45176.htm
- http://m.3g.uliejh.cn/nnews/65137.htm
- http://m.3g.uliejh.cn/nnews/032432.htm
- http://m.3g.uliejh.cn/nnews/0510566.htm
- http://m.3g.uliejh.cn/nnews/86717.htm
- http://m.3g.uliejh.cn/nnews/3970.htm
- http://m.3g.uliejh.cn/nnews/02987.htm
- http://m.3g.uliejh.cn/nnews/942565.htm
- http://m.3g.uliejh.cn/nnews/6987.htm
- http://m.3g.uliejh.cn/nnews/7673828.htm
- http://m.3g.uliejh.cn/nnews/47586.htm
- http://m.3g.uliejh.cn/nnews/8704.htm
- http://m.3g.uliejh.cn/nnews/7709895.htm
- http://m.3g.uliejh.cn/nnews/2334.htm
- http://m.3g.uliejh.cn/nnews/0794.htm
- http://m.3g.uliejh.cn/nnews/7134226.htm
- http://m.3g.uliejh.cn/nnews/9271814.htm
- http://m.3g.uliejh.cn/nnews/63431.htm
- http://m.3g.uliejh.cn/nnews/776689.htm
- http://m.3g.uliejh.cn/nnews/3193217.htm
- http://m.3g.uliejh.cn/nnews/6122522.htm
- http://m.3g.uliejh.cn/nnews/1201.htm
- http://m.3g.uliejh.cn/nnews/3569219.htm
- http://m.3g.uliejh.cn/nnews/18653.htm
- http://m.3g.uliejh.cn/nnews/7104.htm
- http://m.3g.uliejh.cn/nnews/9073.htm
- http://m.3g.uliejh.cn/nnews/8204669.htm
- http://m.3g.uliejh.cn/nnews/0652439.htm
- http://m.3g.uliejh.cn/nnews/3723046.htm
- http://m.3g.uliejh.cn/nnews/3528298.htm
- http://m.3g.uliejh.cn/nnews/2208.htm
- http://m.3g.uliejh.cn/nnews/9332.htm
- http://m.3g.uliejh.cn/nnews/088163.htm
- http://m.3g.uliejh.cn/nnews/3503.htm
- http://m.3g.uliejh.cn/nnews/00778.htm
- http://m.3g.uliejh.cn/nnews/908767.htm
- http://m.3g.uliejh.cn/nnews/3628.htm
- http://m.3g.uliejh.cn/nnews/85756.htm
- http://m.3g.uliejh.cn/nnews/06639.htm
- http://m.3g.uliejh.cn/nnews/6483.htm
- http://m.3g.uliejh.cn/nnews/7970.htm
- http://m.3g.uliejh.cn/nnews/0815705.htm
- http://m.3g.uliejh.cn/nnews/8904.htm
- http://m.3g.uliejh.cn/nnews/533811.htm
- http://m.3g.uliejh.cn/nnews/5530.htm
- http://m.3g.uliejh.cn/nnews/845460.htm
- http://m.3g.uliejh.cn/nnews/276658.htm
- http://m.3g.uliejh.cn/nnews/677775.htm
- http://m.3g.uliejh.cn/nnews/4515196.htm
- http://m.3g.uliejh.cn/nnews/6424.htm
- http://m.3g.uliejh.cn/nnews/0442449.htm
- http://m.3g.uliejh.cn/nnews/3031.htm
- http://m.3g.uliejh.cn/nnews/5856390.htm
- http://m.3g.uliejh.cn/nnews/454119.htm
- http://m.3g.uliejh.cn/nnews/07487.htm
- http://m.3g.uliejh.cn/nnews/9522492.htm
- http://m.3g.uliejh.cn/nnews/35882.htm
- http://m.3g.uliejh.cn/nnews/746161.htm
- http://m.3g.uliejh.cn/nnews/4169.htm
- http://m.3g.uliejh.cn/nnews/6694507.htm
- http://m.3g.uliejh.cn/nnews/117473.htm
- http://m.3g.uliejh.cn/nnews/0094.htm
- http://m.3g.uliejh.cn/nnews/651666.htm
- http://m.3g.uliejh.cn/nnews/9543.htm
- http://m.3g.uliejh.cn/nnews/47077.htm
- http://m.3g.uliejh.cn/nnews/725816.htm

## 项目结构

```
indexer/
├── src/                           # 核心源代码目录
│   ├── core/                      # 核心引擎模块
│   │   ├── loader.ts              # 链接加载器，支持多种输入格式解析
│   │   ├── validator.ts           # URL 格式与协议校验逻辑
│   │   └── health.ts              # 健康检查调度器，包含超时与重试策略
│   ├── api/                       # RESTful API 服务层
│   │   ├── routes.ts              # 路由定义：查询、分类、标签、状态等端点
│   │   └── middleware.ts          # 请求日志、跨域、限流中间件
│   ├── export/                    # 导出渲染引擎
│   │   ├── markdown.ts            # 生成 Markdown 格式资源列表
│   │   ├── html.ts                # 生成静态 HTML 目录页与内联样式
│   │   └── json.ts                # 导出完整数据集为结构化 JSON
│   └── cli/                       # 命令行交互入口
│       ├── index.ts               # CLI 主程序，整合所有子命令
│       └── commands.ts            # add、check、export、serve 等命令实现
├── config/                        # 配置目录
│   ├── default.yaml               # 默认配置：分类模板、监控间隔、导出路径
│   └── schema.json                # 配置项的 JSON Schema 校验文件
├── data/                          # 数据存储目录（运行时生成）
│   ├── links.json                 # 主链接数据库，包含所有元数据字段
│   ├── history/                   # 审计日志目录，按日期归档变更记录
│   └── cache/                     # 健康检查缓存，减少重复网络请求
├── docs/                          # 项目文档
│   ├── getting-started.md         # 快速入门指南，包含首次运行示例
│   ├── configuration.md           # 完整配置参数说明与调优建议
│   ├── api-reference.md           # API 详细文档，含请求/响应示例
│   └── operation-guide.md         # 生产环境部署与运维手册
├── tests/                         # 单元测试与集成测试
│   ├── unit/                      # 各模块单元测试，覆盖率目标 80% 以上
│   └── fixtures/                  # 测试用的样本数据与模拟响应
├── scripts/                       # 辅助脚本
│   ├── migrate.sh                 # 数据格式升级迁移脚本
│   └── backup.sh                  # 定时备份数据目录到指定位置
├── dist/                          # 构建输出目录（gitignore）
├── package.json                   # npm 项目配置，包含依赖与脚本命令
├── tsconfig.json                  # TypeScript 编译配置
├── .eslintrc.js                   # ESLint 代码风格检查规则
└── README.md                      # 项目说明文档（本文件）
```

## 贡献指南

1. 阅读项目行为准则与贡献者公约，确认遵守社区协作规范。在 GitHub Issues 中查找或新建讨论议题，说明拟解决的问题或新增功能，避免重复劳动。

2. Fork 本仓库至个人账户，在 dev 分支基础上创建功能分支，分支命名遵循 feat/xxx 或 fix/xxx 格式。本地开发时运行 npm install 安装依赖，npm run test 确保现有测试通过。

3. 代码编写需符合 TypeScript 严格模式，所有公开接口必须有 JSDoc 注释。新增功能需附带相应单元测试，并更新 docs 目录下相关文档。提交前运行 npm run lint 与 npm run format 统一代码风格。

4. 提交 commit 时使用约定式提交格式（如 feat: 添加批量导入 CSV 支持），描述需清晰说明变更内容与影响范围。推送分支后在 GitHub 发起 Pull Request，目标分支为 dev。

5. PR 描述中需引用对应 Issue 编号，简述实现方案与测试结果。至少需要一名项目维护者审核通过，且 CI 流水线全部通过后方可合并。合并后会自动触发 dev 分支的预发布构建。

## 常见问题

问：项目支持哪些链接输入格式？是否可以直接导入浏览器书签？

答：WebNavi Indexer 内置了 CSV、JSON 和纯文本（每行一个 URL）三种解析器。浏览器书签可通过导出为 HTML 后，使用社区提供的转换脚本转为 JSON 格式再导入。未来版本计划增加对 Netscape 书签格式的直接支持。

问：健康检查模块如何处理需要登录或带有反爬机制的网站？

答：健康检查默认使用 HEAD 方法，仅验证响应状态码和连接时延，不执行 JavaScript 或加载子资源。对于需要特定 User-Agent 或 Cookie 的站点，可在配置中为单个链接设置自定义请求头。若站点有严格反爬策略，建议将该链接的检查模式调整为手动确认，避免被屏蔽。

问：如何将 WebNavi Indexer 与现有的静态站点生成器（如 VuePress、Docusaurus）集成？

答：推荐使用 export 命令生成 Markdown 格式的资源列表文件，或通过 JSON API 在构建时拉取数据。项目提供了 Docusaurus 插件示例，位于 docs/integration 目录下，可直接引用。对于自定义站点，可调用 API 的 /api/export 端点获取结构化数据并在前端自行渲染。

## 许可证

MIT

> 外链数量: 250 | 生成时间: 2026-08-24 23:40:21
