# WebIndex 聚合导航系统

WebIndex 是一个面向技术调研与信息采集场景的轻量级外链资源聚合导航系统。该项目定位于为开发者、数据分析师、运维人员以及内容研究员提供一套结构清晰、可快速部署的 URL 资源索引框架。通过将分散的原始链接纳入统一的目录树与分类逻辑，WebIndex 能够帮助团队高效管理大批量外链资源，降低信息遗失与重复检索的成本，并支持自定义标签扩展与访问状态监控。

WebIndex 本身不依赖数据库，基于纯静态文件与轻量级脚本实现资源清单的解析与渲染，既可作为独立导航站运行，也可嵌入现有文档体系或内部知识库。项目遵循最小可用原则，所有资源条目均以 Markdown 或 YAML 格式维护，便于版本控制与协作编辑，适用于中小型技术团队、开源项目文档站以及个人知识管理工具链。

## 功能概览

- **批量链接导入与规范化校验**：支持从纯文本列表、CSV 或 Markdown 清单中批量导入 URL，自动执行协议补全、去重与格式清洗，并输出标准化条目。

- **多维度标签分类与全文检索**：每个资源条目可绑定多个自定义标签（如 "前端工具"、"运维监控"、"数据源"），同时提供基于标题、描述与标签的模糊搜索功能，快速定位目标链接。

- **访问状态健康检查**：内置定时或手动触发的 HTTP 头探测机制，检测每个外链的可达性、响应时间与状态码，并以可视化标记（正常/异常/超时）直观呈现。

- **目录树与面包屑导航**：将资源按主题、来源或业务场景组织为多级目录结构，页面顶部生成动态面包屑，用户可随时了解当前位置并快速回退。

- **个性化收藏与备注**：允许用户在本地存储中标记常用链接或添加私人备注，不影响公共资源库，适合个人研究工作流。

- **批量导出与报告生成**：支持将当前筛选或搜索后的资源列表导出为 CSV、JSON 或 Markdown 表格，便于离线分析或嵌入文档。

- **暗色主题与响应式布局**：内置亮色/暗色两套主题，适配桌面与移动设备，在移动端自动折叠侧边栏并优化触摸交互。

## 应用场景

**技术团队内部文档导航**  
研发团队可将 WebIndex 部署为内部知识库的入口，集中存放常用开发文档、API 参考、运维面板、日志系统等链接，避免每位成员各自收藏导致信息碎片化。

**开源项目外部资源附录**  
开源项目维护者可以使用 WebIndex 整理相关生态工具、社区论坛、视频教程或扩展阅读列表，作为项目 README 或 Wiki 的补充附件，帮助新贡献者快速了解周边生态。

**数据采集与调研工作台**  
从事行业分析或市场调研的人员，可将大量待访问的数据源、新闻站点、统计报告链接统一纳入 WebIndex，通过健康检查功能定期确认资源有效性，减少调研过程中的链接失效干扰。

**个人知识库的入口聚合**  
知识管理爱好者可将 WebIndex 作为个人书签管理器的替代方案，按学习领域、项目阶段或兴趣主题组织链接，配合备注与收藏功能，构建长期积累的研究入口。

## 快速开始

以下步骤适用于 Linux / macOS / Windows WSL 环境，需提前安装 Git 与 Node.js 16+。

```bash
# 克隆项目仓库
git clone https://github.com/webindex/webindex-starter.git
cd webindex-starter

# 安装依赖（使用 npm）
npm install

# 启动开发服务器，默认监听 3000 端口
npm run dev

# 生产环境构建静态文件
npm run build

# 预览构建结果
npm run preview
```

首次启动后，访问 http://localhost:3000 即可看到默认示例资源列表。如需使用自定义数据，请将链接清单放入 `data/sources` 目录下的 `.txt` 或 `.yml` 文件中，系统会自动扫描并合并。

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|---------|---------|------|
| Node.js | 16.x 或更高 | 运行时环境，用于执行构建脚本与开发服务器 |
| npm | 8.x 或更高 | 包管理器，用于安装项目依赖 |
| Git | 2.30 或更高 | 版本控制工具，用于克隆仓库与提交变更 |
| 现代浏览器 | Chrome 90+ / Firefox 88+ / Edge 90+ | 前端界面运行环境，需支持 ES2020 与 CSS Grid |
| 磁盘空间 | 至少 200 MB | 用于存放源码、依赖包及构建产物 |
| 网络连接 | 外网访问 | 用于首次安装依赖包以及检测外部链接状态 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|-----|------|-----------|
| 入门指南 | `/docs/getting-started.md` | 如何快速部署、配置数据源并生成第一个导航页面？ |
| 数据规范 | `/docs/data-format.md` | 资源清单支持哪些格式？YAML 字段如何定义？标签体系如何设计？ |
| 运维手册 | `/docs/operations.md` | 如何执行健康检查、更新缓存、备份数据以及迁移服务器？ |
| 开发参考 | `/docs/development.md` | 项目目录结构、核心脚本说明、API 接口及如何扩展自定义功能？ |
| 常见流程 | `/docs/workflows.md` | 如何批量导入新链接、如何导出报告、如何重置本地收藏数据？ |

## 资源列表

- http://m.wap.uliejh.cn/bnews/0323.htm
- http://m.wap.uliejh.cn/bnews/341467.htm
- http://m.wap.uliejh.cn/bnews/86696.htm
- http://m.wap.uliejh.cn/bnews/1257.htm
- http://m.wap.uliejh.cn/bnews/86729.htm
- http://m.wap.uliejh.cn/bnews/3508057.htm
- http://m.wap.uliejh.cn/bnews/134492.htm
- http://m.wap.uliejh.cn/bnews/1893646.htm
- http://m.wap.uliejh.cn/bnews/246882.htm
- http://m.wap.uliejh.cn/bnews/0197771.htm
- http://m.wap.uliejh.cn/bnews/815966.htm
- http://m.wap.uliejh.cn/bnews/6163718.htm
- http://m.wap.uliejh.cn/bnews/5514395.htm
- http://m.wap.uliejh.cn/bnews/85504.htm
- http://m.wap.uliejh.cn/bnews/27725.htm
- http://m.wap.uliejh.cn/bnews/932103.htm
- http://m.wap.uliejh.cn/bnews/17288.htm
- http://m.wap.uliejh.cn/bnews/586047.htm
- http://m.wap.uliejh.cn/bnews/1035666.htm
- http://m.wap.uliejh.cn/bnews/6368908.htm
- http://m.wap.uliejh.cn/bnews/4504.htm
- http://m.wap.uliejh.cn/bnews/4673305.htm
- http://m.wap.uliejh.cn/bnews/400601.htm
- http://m.wap.uliejh.cn/bnews/0081506.htm
- http://m.wap.uliejh.cn/bnews/1837855.htm
- http://m.wap.uliejh.cn/bnews/8700.htm
- http://m.wap.uliejh.cn/bnews/599564.htm
- http://m.wap.uliejh.cn/bnews/6314369.htm
- http://m.wap.uliejh.cn/bnews/059039.htm
- http://m.wap.uliejh.cn/bnews/903651.htm
- http://m.wap.uliejh.cn/bnews/0348232.htm
- http://m.wap.uliejh.cn/bnews/6811.htm
- http://m.wap.uliejh.cn/bnews/4597.htm
- http://m.wap.uliejh.cn/bnews/736421.htm
- http://m.wap.uliejh.cn/bnews/3692.htm
- http://m.wap.uliejh.cn/bnews/07731.htm
- http://m.wap.uliejh.cn/bnews/190472.htm
- http://m.wap.uliejh.cn/bnews/1632747.htm
- http://m.wap.uliejh.cn/bnews/1126309.htm
- http://m.wap.uliejh.cn/bnews/4176125.htm
- http://m.wap.uliejh.cn/bnews/0363.htm
- http://m.wap.uliejh.cn/bnews/8993433.htm
- http://m.wap.uliejh.cn/bnews/887418.htm
- http://m.wap.uliejh.cn/bnews/1490.htm
- http://m.wap.uliejh.cn/bnews/96065.htm
- http://m.wap.uliejh.cn/bnews/6343.htm
- http://m.wap.uliejh.cn/bnews/74788.htm
- http://m.wap.uliejh.cn/bnews/678302.htm
- http://m.wap.uliejh.cn/bnews/3763.htm
- http://m.wap.uliejh.cn/bnews/865185.htm
- http://m.wap.uliejh.cn/bnews/604870.htm
- http://m.wap.uliejh.cn/bnews/5833352.htm
- http://m.wap.uliejh.cn/bnews/77410.htm
- http://m.wap.uliejh.cn/bnews/6905.htm
- http://m.wap.uliejh.cn/bnews/0326.htm
- http://m.wap.uliejh.cn/bnews/69208.htm
- http://m.wap.uliejh.cn/bnews/25606.htm
- http://m.wap.uliejh.cn/bnews/2915695.htm
- http://m.wap.uliejh.cn/bnews/8939.htm
- http://m.wap.uliejh.cn/bnews/52465.htm
- http://m.wap.uliejh.cn/bnews/518092.htm
- http://m.wap.uliejh.cn/bnews/64224.htm
- http://m.wap.uliejh.cn/bnews/993993.htm
- http://m.wap.uliejh.cn/bnews/81915.htm
- http://m.wap.uliejh.cn/bnews/52074.htm
- http://m.wap.uliejh.cn/bnews/796443.htm
- http://m.wap.uliejh.cn/bnews/309361.htm
- http://m.wap.uliejh.cn/bnews/00718.htm
- http://m.wap.uliejh.cn/bnews/456452.htm
- http://m.wap.uliejh.cn/bnews/8093193.htm
- http://m.wap.uliejh.cn/bnews/38424.htm
- http://m.wap.uliejh.cn/bnews/6813554.htm
- http://m.wap.uliejh.cn/bnews/617256.htm
- http://m.wap.uliejh.cn/bnews/8452.htm
- http://m.wap.uliejh.cn/bnews/5915514.htm
- http://m.wap.uliejh.cn/bnews/2326.htm
- http://m.wap.uliejh.cn/bnews/11540.htm
- http://m.wap.uliejh.cn/bnews/8742.htm
- http://m.wap.uliejh.cn/bnews/22179.htm
- http://m.wap.uliejh.cn/bnews/774758.htm
- http://m.wap.uliejh.cn/bnews/5687848.htm
- http://m.wap.uliejh.cn/bnews/483036.htm
- http://m.wap.uliejh.cn/bnews/59858.htm
- http://m.wap.uliejh.cn/bnews/54276.htm
- http://m.wap.uliejh.cn/bnews/32433.htm
- http://m.wap.uliejh.cn/bnews/50349.htm
- http://m.wap.uliejh.cn/bnews/62422.htm
- http://m.wap.uliejh.cn/bnews/196088.htm
- http://m.wap.uliejh.cn/bnews/613073.htm
- http://m.wap.uliejh.cn/bnews/264877.htm
- http://m.wap.uliejh.cn/bnews/2764019.htm
- http://m.wap.uliejh.cn/bnews/2152.htm
- http://m.wap.uliejh.cn/bnews/7040834.htm
- http://m.wap.uliejh.cn/bnews/94204.htm
- http://m.wap.uliejh.cn/bnews/4094.htm
- http://m.wap.uliejh.cn/bnews/42789.htm
- http://m.wap.uliejh.cn/bnews/3366682.htm
- http://m.wap.uliejh.cn/bnews/340947.htm
- http://m.wap.uliejh.cn/bnews/9522.htm
- http://m.wap.uliejh.cn/bnews/26344.htm
- http://m.wap.uliejh.cn/bnews/1531120.htm
- http://m.wap.uliejh.cn/bnews/801041.htm
- http://m.wap.uliejh.cn/bnews/142579.htm
- http://m.wap.uliejh.cn/bnews/2280261.htm
- http://m.wap.uliejh.cn/bnews/3479673.htm
- http://m.wap.uliejh.cn/bnews/346798.htm
- http://m.wap.uliejh.cn/bnews/085421.htm
- http://m.wap.uliejh.cn/bnews/10946.htm
- http://m.wap.uliejh.cn/bnews/6128576.htm
- http://m.wap.uliejh.cn/bnews/8143915.htm
- http://m.wap.uliejh.cn/bnews/29770.htm
- http://m.wap.uliejh.cn/bnews/42325.htm
- http://m.wap.uliejh.cn/bnews/61260.htm
- http://m.wap.uliejh.cn/bnews/6743800.htm
- http://m.wap.uliejh.cn/bnews/70052.htm
- http://m.wap.uliejh.cn/bnews/14602.htm
- http://m.wap.uliejh.cn/bnews/5023575.htm
- http://m.wap.uliejh.cn/bnews/9533010.htm
- http://m.wap.uliejh.cn/bnews/1809.htm
- http://m.wap.uliejh.cn/bnews/08890.htm
- http://m.wap.uliejh.cn/bnews/0179963.htm
- http://m.wap.uliejh.cn/bnews/094084.htm
- http://m.wap.uliejh.cn/bnews/7698.htm
- http://m.wap.uliejh.cn/bnews/92647.htm
- http://m.wap.uliejh.cn/bnews/9655001.htm
- http://m.wap.uliejh.cn/bnews/7627088.htm
- http://m.wap.uliejh.cn/bnews/4254.htm
- http://m.wap.uliejh.cn/bnews/5011279.htm
- http://m.wap.uliejh.cn/bnews/776550.htm
- http://m.wap.uliejh.cn/bnews/3019817.htm
- http://m.wap.uliejh.cn/bnews/699620.htm
- http://m.wap.uliejh.cn/bnews/766175.htm
- http://m.wap.uliejh.cn/bnews/0005231.htm
- http://m.wap.uliejh.cn/bnews/60094.htm
- http://m.wap.uliejh.cn/bnews/6123.htm
- http://m.wap.uliejh.cn/bnews/1146097.htm
- http://m.wap.uliejh.cn/bnews/8912.htm
- http://m.wap.uliejh.cn/bnews/31842.htm
- http://m.wap.uliejh.cn/bnews/703712.htm
- http://m.wap.uliejh.cn/bnews/269856.htm
- http://m.wap.uliejh.cn/bnews/31937.htm
- http://m.wap.uliejh.cn/bnews/6455605.htm
- http://m.wap.uliejh.cn/bnews/580931.htm
- http://m.wap.uliejh.cn/bnews/622976.htm
- http://m.wap.uliejh.cn/bnews/2836444.htm
- http://m.wap.uliejh.cn/bnews/1169987.htm
- http://m.wap.uliejh.cn/bnews/4572583.htm
- http://m.wap.uliejh.cn/bnews/4278928.htm
- http://m.wap.uliejh.cn/bnews/0287436.htm
- http://m.wap.uliejh.cn/bnews/26011.htm
- http://m.wap.uliejh.cn/bnews/342703.htm
- http://m.wap.uliejh.cn/bnews/3264224.htm
- http://m.wap.uliejh.cn/bnews/8746.htm
- http://m.wap.uliejh.cn/bnews/817001.htm
- http://m.wap.uliejh.cn/bnews/6374.htm
- http://m.wap.uliejh.cn/bnews/76736.htm
- http://m.wap.uliejh.cn/bnews/6539.htm
- http://m.wap.uliejh.cn/bnews/9339036.htm
- http://m.wap.uliejh.cn/bnews/0434268.htm
- http://m.wap.uliejh.cn/bnews/4028880.htm
- http://m.wap.uliejh.cn/bnews/34514.htm
- http://m.wap.uliejh.cn/bnews/36006.htm
- http://m.wap.uliejh.cn/bnews/7635310.htm
- http://m.wap.uliejh.cn/bnews/6834.htm
- http://m.wap.uliejh.cn/bnews/5099.htm
- http://m.wap.uliejh.cn/bnews/135813.htm
- http://m.wap.uliejh.cn/bnews/7924651.htm
- http://m.wap.uliejh.cn/bnews/1930.htm
- http://m.wap.uliejh.cn/bnews/6321.htm
- http://m.wap.uliejh.cn/bnews/201739.htm
- http://m.wap.uliejh.cn/bnews/5660468.htm
- http://m.wap.uliejh.cn/bnews/4573448.htm
- http://m.wap.uliejh.cn/bnews/709456.htm
- http://m.wap.uliejh.cn/bnews/1215333.htm
- http://m.wap.uliejh.cn/bnews/58393.htm
- http://m.wap.uliejh.cn/bnews/42812.htm
- http://m.wap.uliejh.cn/bnews/94647.htm
- http://m.wap.uliejh.cn/bnews/223071.htm
- http://m.wap.uliejh.cn/bnews/8407007.htm
- http://m.wap.uliejh.cn/bnews/5225.htm
- http://m.wap.uliejh.cn/bnews/0137447.htm
- http://m.wap.uliejh.cn/bnews/00913.htm
- http://m.wap.uliejh.cn/bnews/2201424.htm
- http://m.wap.uliejh.cn/bnews/84728.htm
- http://m.wap.uliejh.cn/bnews/4865786.htm
- http://m.wap.uliejh.cn/bnews/03866.htm
- http://m.wap.uliejh.cn/bnews/042568.htm
- http://m.wap.uliejh.cn/bnews/1122282.htm
- http://m.wap.uliejh.cn/bnews/9417178.htm
- http://m.wap.uliejh.cn/bnews/9994.htm
- http://m.wap.uliejh.cn/bnews/394404.htm
- http://m.wap.uliejh.cn/bnews/3102.htm
- http://m.wap.uliejh.cn/bnews/881472.htm
- http://m.wap.uliejh.cn/bnews/1962.htm
- http://m.wap.uliejh.cn/bnews/51920.htm
- http://m.wap.uliejh.cn/bnews/4598.htm
- http://m.wap.uliejh.cn/bnews/989184.htm
- http://m.wap.uliejh.cn/bnews/1410.htm
- http://m.wap.uliejh.cn/bnews/343890.htm
- http://m.wap.uliejh.cn/bnews/196089.htm
- http://m.wap.uliejh.cn/bnews/036823.htm
- http://m.wap.uliejh.cn/bnews/1549118.htm
- http://m.wap.uliejh.cn/bnews/13735.htm
- http://m.wap.uliejh.cn/bnews/07157.htm
- http://m.wap.uliejh.cn/bnews/5102.htm
- http://m.wap.uliejh.cn/bnews/0008988.htm
- http://m.wap.uliejh.cn/bnews/5613227.htm
- http://m.wap.uliejh.cn/bnews/0633670.htm
- http://m.wap.uliejh.cn/bnews/13320.htm
- http://m.wap.uliejh.cn/bnews/5250.htm
- http://m.wap.uliejh.cn/bnews/5387413.htm
- http://m.wap.uliejh.cn/bnews/647820.htm
- http://m.wap.uliejh.cn/bnews/566218.htm
- http://m.wap.uliejh.cn/bnews/95068.htm
- http://m.wap.uliejh.cn/bnews/977989.htm
- http://m.wap.uliejh.cn/bnews/332392.htm
- http://m.wap.uliejh.cn/bnews/49764.htm
- http://m.wap.uliejh.cn/bnews/969628.htm
- http://m.wap.uliejh.cn/bnews/05738.htm
- http://m.wap.uliejh.cn/bnews/86479.htm
- http://m.wap.uliejh.cn/bnews/8013094.htm
- http://m.wap.uliejh.cn/bnews/2470597.htm
- http://m.wap.uliejh.cn/bnews/278627.htm
- http://m.wap.uliejh.cn/bnews/6705743.htm
- http://m.wap.uliejh.cn/bnews/9050252.htm
- http://m.wap.uliejh.cn/bnews/916969.htm
- http://m.wap.uliejh.cn/bnews/917287.htm
- http://m.wap.uliejh.cn/bnews/44570.htm
- http://m.wap.uliejh.cn/bnews/7595189.htm
- http://m.wap.uliejh.cn/bnews/718264.htm
- http://m.wap.uliejh.cn/bnews/8348.htm
- http://m.wap.uliejh.cn/bnews/41253.htm
- http://m.wap.uliejh.cn/bnews/085603.htm
- http://m.wap.uliejh.cn/bnews/40443.htm
- http://m.wap.uliejh.cn/bnews/08456.htm
- http://m.wap.uliejh.cn/bnews/4295.htm
- http://m.wap.uliejh.cn/bnews/939646.htm
- http://m.wap.uliejh.cn/bnews/8591393.htm
- http://m.wap.uliejh.cn/bnews/9564085.htm
- http://m.wap.uliejh.cn/bnews/42952.htm
- http://m.wap.uliejh.cn/bnews/759347.htm
- http://m.wap.uliejh.cn/bnews/595577.htm
- http://m.wap.uliejh.cn/bnews/8694649.htm
- http://m.wap.uliejh.cn/bnews/662703.htm
- http://m.wap.uliejh.cn/bnews/3647.htm
- http://m.wap.uliejh.cn/bnews/9033685.htm
- http://m.wap.uliejh.cn/bnews/2748461.htm
- http://m.wap.uliejh.cn/bnews/589053.htm
- http://m.wap.uliejh.cn/bnews/2294287.htm
- http://m.wap.uliejh.cn/bnews/4051.htm

## 项目结构

```
webindex/
├── data/                                 # 数据层，存放所有资源清单与配置
│   ├── sources/                          # 原始外链数据目录（按主题分文件）
│   │   ├── batch_42.txt                  # 第42批次导入的原始链接清单
│   │   ├── tech_news.yml                 # 技术新闻类资源（YAML 格式）
│   │   └── ops_tools.yml                 # 运维工具类资源（含标签与备注）
│   ├── categories.yml                    # 全局分类定义与层级映射
│   └── tags.yml                          # 标签别名与颜色配置
├── scripts/                              # 脚本工具集
│   ├── import.js                         # 批量导入脚本，支持 txt/csv/yaml 解析
│   ├── health-check.js                   # 外链健康状态探测脚本（基于 node-fetch）
│   ├── export.js                         # 导出为 CSV / JSON / Markdown 的工具
│   └── build-index.js                    # 生成静态索引页面的核心构建脚本
├── src/                                  # 前端源代码目录
│   ├── components/                       # Vue / React 组件（依框架而定）
│   │   ├── NavTree.vue                   # 左侧分类目录树组件
│   │   ├── LinkTable.vue                 # 资源列表表格组件（含状态标记）
│   │   └── SearchBar.vue                 # 全文检索与过滤组件
│   ├── assets/                           # 静态资源（样式、字体、图标）
│   │   ├── theme-dark.css                # 暗色主题样式表
│   │   └── theme-light.css               # 亮色主题样式表
│   └── main.js                           # 前端应用入口文件
├── public/                                # 构建输出目录（静态站点根目录）
│   ├── index.html                        # 首页入口
│   └── favicon.ico                       # 站点图标
├── docs/                                  # 项目文档（面向开发者与用户）
│   ├── getting-started.md                # 快速入门指南
│   ├── data-format.md                    # 数据格式规范与字段说明
│   ├── operations.md                     # 日常运维与故障排查
│   └── development.md                    # 二次开发与扩展指南
├── config/                                # 运行时配置文件
│   ├── app.yml                           # 站点名称、默认主题、分页大小等
│   └── health-check.yml                  # 健康检查超时、重试、并发数配置
├── tests/                                 # 单元测试与集成测试
│   ├── import.test.js                    # 导入功能测试用例
│   └── health.test.js                    # 健康检查逻辑测试
├── .gitignore                             # Git 忽略文件列表
├── package.json                           # npm 项目配置与依赖声明
└── README.md                              # 项目说明文档（本文件）
```

## 贡献指南

1.  Fork 本仓库至个人账号，并克隆到本地开发环境。请确保本地 Node.js 版本不低于 16.x，并执行 `npm install` 完成依赖安装。

2.  在 `data/sources` 目录下新增或编辑 YAML 文件以添加资源条目，每个条目需包含 `url`、`title`、`tags` 字段，可选 `description` 与 `category`。提交前请运行 `npm run lint` 校验数据格式。

3.  若需调整前端界面或交互逻辑，请修改 `src/components` 下的对应组件，并遵循项目已有的代码风格（ESLint + Prettier 配置已在根目录提供）。修改后执行 `npm run build` 确认构建无报错。

4.  新增功能或修复缺陷时，请编写对应的单元测试文件，存放于 `tests` 目录下，并确保所有现有测试通过（`npm test`）。

5.  提交 Pull Request 前，请更新 `docs` 目录下相关文档，并在 PR 描述中清晰说明变更内容、影响范围及测试情况。PR 合并前需至少一位项目维护者审阅。

## 常见问题

**Q：导入大量链接后，页面加载变慢或搜索卡顿，如何优化？**  
A：建议对数据源进行分文件拆分，每个 YAML 文件不超过 500 条记录。同时可在 `config/app.yml` 中调整前端分页大小（默认 50 条/页），减少单次渲染的 DOM 数量。若条目超过 2000 条，推荐开启服务端搜索模式（需额外配置 Elasticsearch 或 Lunr 索引）。

**Q：健康检查功能显示大量超时或失败，是什么原因？**  
A：首先确认运行环境能够正常访问外网，且目标站点未屏蔽 HEAD 请求。部分站点对 HEAD 请求响应较慢或返回 405，可在 `config/health-check.yml` 中将 `method` 改为 `GET` 并设置合理的 `timeout`（建议 5000ms）。若仍大量失败，可能是目标站点临时不可用，请间隔一段时间后重试。

**Q：如何将现有浏览器书签批量导入 WebIndex？**  
A：大多数浏览器支持将书签导出为 HTML 文件。您可以使用社区提供的转换脚本（位于 `scripts/convert-bookmarks.js`）将 HTML 书签解析为 YAML 条目，然后放入 `data/sources` 目录。具体步骤请参考 `docs/workflows.md` 中的“书签迁移”章节。

## 许可证

MIT

> 外链数量: 250 | 生成时间: 2026-08-24 23:40:21
