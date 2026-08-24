# WebLink Hub

WebLink Hub 是一个面向技术文档聚合与外部资源导航的开源项目，旨在为开发者、研究员及技术写作人员提供高效、可维护的外链收录与管理方案。本项目不直接托管内容，而是通过结构化 Markdown 对散布于各处的技术文章、教程、工具站点进行编目与索引，解决个人书签混乱、团队共享困难、资源失效难追踪等痛点。

项目定位为“技术外链的轻量级中台”，适用于个人知识库构建、团队技术周报自动化、静态站点资源整合等场景。通过约定式目录结构与元数据标记，WebLink Hub 可被静态站点生成器（如 Hugo、VuePress）直接消费，也可作为 CI/CD 流水线中的数据源，实现链接可用性检测与变更通知。

## 功能概览

- **结构化资源索引**：支持按技术领域、来源站点、更新日期等多维度对链接进行标记与分类，内置标签系统与失效链接检测接口。
- **自动化元数据提取**：集成可选的 Python 辅助脚本，可从目标 URL 的 HTML 中提取标题、描述、关键词，生成标准化 YAML Frontmatter。
- **批量链接校验**：提供 `check_links.py` 工具，支持并发 HEAD 请求，输出失效链接报告与状态码分布统计。
- **灵活的渲染模板**：提供适用于 VuePress 和 MkDocs 的主题适配层，可将资源列表渲染为响应式卡片或表格视图。
- **周期性更新机制**：通过 GitHub Actions 配置每周自动运行链接校验，并生成更新日志，保持资源时效性。
- **多格式导出**：支持将资源列表导出为 JSON、CSV 或 OPML 格式，便于导入其他知识管理工具或 RSS 阅读器。

## 应用场景

**个人技术知识库构建**：开发者可将日常浏览到的优质技术博客、官方文档、视频教程通过本项目统一收录，利用标签与分类功能快速检索，避免遗忘或重复查找。

**团队技术周报自动化**：团队技术负责人可将每周推荐的阅读材料、工具更新、社区讨论帖以本项目格式录入，配合 CI 生成周报页面或邮件摘要，减少人工排版成本。

**文档站资源导航页**：开源项目或企业文档站可利用本项目维护“生态伙伴”“相关工具”“参考文献”等外链区块，保持与上游资源的同步更新，提升文档的完整性与实用性。

**链接健康度监控**：运维或技术运营人员可定期运行校验工具，及时发现团队文档或产品官网中的失效外链，生成待修复清单，降低用户访问挫败感。

## 快速开始

以下命令适用于 Linux/macOS 及 Windows WSL 环境。

```bash
# 克隆仓库
git clone https://github.com/your-org/weblink-hub.git
cd weblink-hub

# 安装 Python 依赖（用于辅助校验与元数据提取）
pip install -r requirements.txt

# 运行示例校验任务（默认扫描 resources/ 目录）
python scripts/check_links.py --source resources/ --output reports/broken_links.json

# 生成静态资源索引页（需安装 VuePress）
npm install -g vuepress
vuepress build docs/
```

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|---|---|---|
| Python | 3.8 及以上 | 运行链接校验与元数据提取脚本 |
| requests | 2.28.0 及以上 | 用于 HTTP 请求与响应处理 |
| pyyaml | 6.0 及以上 | 解析和生成 YAML Frontmatter |
| Node.js | 16.0 及以上 | 仅当使用 VuePress 渲染时需要 |
| git | 2.30 及以上 | 版本控制与协作 |
| make | 3.81 及以上 | 可选，用于简化常用命令组合 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|---|---|---|
| 用户手册 | `docs/guide/` | 如何添加新链接、如何运行校验、如何自定义分类标签 |
| 配置参考 | `docs/config/` | 校验超时时间、并发数、忽略模式等参数如何调整 |
| 开发指南 | `docs/development/` | 如何扩展校验器、如何增加新的导出格式、PR 提交流程 |
| 运维说明 | `docs/operations/` | 如何配置 GitHub Actions 定时任务、如何部署到静态托管服务 |

## 资源列表

- http://m.blog.uliejh.cn/snews/00855.htm
- http://m.blog.uliejh.cn/snews/6671.htm
- http://m.blog.uliejh.cn/snews/48108.htm
- http://m.blog.uliejh.cn/snews/530222.htm
- http://m.blog.uliejh.cn/snews/2078422.htm
- http://m.blog.uliejh.cn/snews/787151.htm
- http://m.blog.uliejh.cn/snews/1306223.htm
- http://m.blog.uliejh.cn/snews/101752.htm
- http://m.blog.uliejh.cn/snews/268556.htm
- http://m.blog.uliejh.cn/snews/038317.htm
- http://m.blog.uliejh.cn/snews/6784.htm
- http://m.blog.uliejh.cn/snews/4562118.htm
- http://m.blog.uliejh.cn/snews/64539.htm
- http://m.blog.uliejh.cn/snews/59547.htm
- http://m.blog.uliejh.cn/snews/63372.htm
- http://m.blog.uliejh.cn/snews/3627.htm
- http://m.blog.uliejh.cn/snews/428533.htm
- http://m.blog.uliejh.cn/snews/44400.htm
- http://m.blog.uliejh.cn/snews/873620.htm
- http://m.blog.uliejh.cn/snews/4682.htm
- http://m.blog.uliejh.cn/snews/8982223.htm
- http://m.blog.uliejh.cn/snews/7327.htm
- http://m.blog.uliejh.cn/snews/3989493.htm
- http://m.blog.uliejh.cn/snews/4970.htm
- http://m.blog.uliejh.cn/snews/126460.htm
- http://m.blog.uliejh.cn/snews/341369.htm
- http://m.blog.uliejh.cn/snews/9660288.htm
- http://m.blog.uliejh.cn/snews/46977.htm
- http://m.blog.uliejh.cn/snews/4011429.htm
- http://m.blog.uliejh.cn/snews/2292855.htm
- http://m.blog.uliejh.cn/snews/73947.htm
- http://m.blog.uliejh.cn/snews/4488.htm
- http://m.blog.uliejh.cn/snews/7316.htm
- http://m.blog.uliejh.cn/snews/17249.htm
- http://m.blog.uliejh.cn/snews/0883.htm
- http://m.blog.uliejh.cn/snews/2433659.htm
- http://m.blog.uliejh.cn/snews/00435.htm
- http://m.blog.uliejh.cn/snews/826380.htm
- http://m.blog.uliejh.cn/snews/727409.htm
- http://m.blog.uliejh.cn/snews/0006971.htm
- http://m.blog.uliejh.cn/snews/59822.htm
- http://m.blog.uliejh.cn/snews/93914.htm
- http://m.blog.uliejh.cn/snews/3849.htm
- http://m.blog.uliejh.cn/snews/744923.htm
- http://m.blog.uliejh.cn/snews/8719721.htm
- http://m.blog.uliejh.cn/snews/8993934.htm
- http://m.blog.uliejh.cn/snews/5545964.htm
- http://m.blog.uliejh.cn/snews/7529.htm
- http://m.blog.uliejh.cn/snews/635998.htm
- http://m.blog.uliejh.cn/snews/047559.htm
- http://m.blog.uliejh.cn/snews/68019.htm
- http://m.blog.uliejh.cn/snews/4135138.htm
- http://m.blog.uliejh.cn/snews/45787.htm
- http://m.blog.uliejh.cn/snews/108722.htm
- http://m.blog.uliejh.cn/snews/4189944.htm
- http://m.blog.uliejh.cn/snews/760600.htm
- http://m.blog.uliejh.cn/snews/413093.htm
- http://m.blog.uliejh.cn/snews/6502.htm
- http://m.blog.uliejh.cn/snews/258966.htm
- http://m.blog.uliejh.cn/snews/6272563.htm
- http://m.blog.uliejh.cn/snews/0102813.htm
- http://m.blog.uliejh.cn/snews/2993.htm
- http://m.blog.uliejh.cn/snews/3686.htm
- http://m.blog.uliejh.cn/snews/153960.htm
- http://m.blog.uliejh.cn/snews/5460947.htm
- http://m.blog.uliejh.cn/snews/3724.htm
- http://m.blog.uliejh.cn/snews/431547.htm
- http://m.blog.uliejh.cn/snews/12900.htm
- http://m.blog.uliejh.cn/snews/1728.htm
- http://m.blog.uliejh.cn/snews/233882.htm
- http://m.blog.uliejh.cn/snews/656513.htm
- http://m.blog.uliejh.cn/snews/48629.htm
- http://m.blog.uliejh.cn/snews/1862392.htm
- http://m.blog.uliejh.cn/snews/1149.htm
- http://m.blog.uliejh.cn/snews/8778655.htm
- http://m.blog.uliejh.cn/snews/4845.htm
- http://m.blog.uliejh.cn/snews/0387.htm
- http://m.blog.uliejh.cn/snews/6096.htm
- http://m.blog.uliejh.cn/snews/84163.htm
- http://m.blog.uliejh.cn/snews/08174.htm
- http://m.blog.uliejh.cn/snews/57527.htm
- http://m.blog.uliejh.cn/snews/569124.htm
- http://m.blog.uliejh.cn/snews/4076099.htm
- http://m.blog.uliejh.cn/snews/3111432.htm
- http://m.blog.uliejh.cn/snews/5059.htm
- http://m.blog.uliejh.cn/snews/3498.htm
- http://m.blog.uliejh.cn/snews/86472.htm
- http://m.blog.uliejh.cn/snews/3788.htm
- http://m.blog.uliejh.cn/snews/93252.htm
- http://m.blog.uliejh.cn/snews/8870642.htm
- http://m.blog.uliejh.cn/snews/7168.htm
- http://m.blog.uliejh.cn/snews/94737.htm
- http://m.blog.uliejh.cn/snews/999427.htm
- http://m.blog.uliejh.cn/snews/08330.htm
- http://m.blog.uliejh.cn/snews/23161.htm
- http://m.blog.uliejh.cn/snews/2499.htm
- http://m.blog.uliejh.cn/snews/367952.htm
- http://m.blog.uliejh.cn/snews/618996.htm
- http://m.blog.uliejh.cn/snews/035003.htm
- http://m.blog.uliejh.cn/snews/1673.htm
- http://m.blog.uliejh.cn/snews/9196844.htm
- http://m.blog.uliejh.cn/snews/0793.htm
- http://m.blog.uliejh.cn/snews/0276433.htm
- http://m.blog.uliejh.cn/snews/9855050.htm
- http://m.blog.uliejh.cn/snews/8633.htm
- http://m.blog.uliejh.cn/snews/4921769.htm
- http://m.blog.uliejh.cn/snews/7726741.htm
- http://m.blog.uliejh.cn/snews/4741971.htm
- http://m.blog.uliejh.cn/snews/01000.htm
- http://m.blog.uliejh.cn/snews/56224.htm
- http://m.blog.uliejh.cn/snews/12112.htm
- http://m.blog.uliejh.cn/snews/407894.htm
- http://m.blog.uliejh.cn/snews/61994.htm
- http://m.blog.uliejh.cn/snews/781985.htm
- http://m.blog.uliejh.cn/snews/790918.htm
- http://m.blog.uliejh.cn/snews/0430.htm
- http://m.blog.uliejh.cn/snews/3442456.htm
- http://m.blog.uliejh.cn/snews/812758.htm
- http://m.blog.uliejh.cn/snews/45838.htm
- http://m.blog.uliejh.cn/snews/079729.htm
- http://m.blog.uliejh.cn/snews/6330753.htm
- http://m.blog.uliejh.cn/snews/12584.htm
- http://m.blog.uliejh.cn/snews/92711.htm
- http://m.blog.uliejh.cn/snews/655883.htm
- http://m.blog.uliejh.cn/snews/6916993.htm
- http://m.blog.uliejh.cn/snews/2137720.htm
- http://m.blog.uliejh.cn/snews/2637725.htm
- http://m.blog.uliejh.cn/snews/89526.htm
- http://m.blog.uliejh.cn/snews/765634.htm
- http://m.blog.uliejh.cn/snews/599507.htm
- http://m.blog.uliejh.cn/snews/913456.htm
- http://m.blog.uliejh.cn/snews/81145.htm
- http://m.blog.uliejh.cn/snews/271892.htm
- http://m.blog.uliejh.cn/snews/0467.htm
- http://m.blog.uliejh.cn/snews/82988.htm
- http://m.blog.uliejh.cn/snews/1309.htm
- http://m.blog.uliejh.cn/snews/82643.htm
- http://m.blog.uliejh.cn/snews/56520.htm
- http://m.blog.uliejh.cn/snews/8889210.htm
- http://m.blog.uliejh.cn/snews/0943.htm
- http://m.blog.uliejh.cn/snews/6266.htm
- http://m.blog.uliejh.cn/snews/049901.htm
- http://m.blog.uliejh.cn/snews/93698.htm
- http://m.blog.uliejh.cn/snews/9524.htm
- http://m.blog.uliejh.cn/snews/30702.htm
- http://m.blog.uliejh.cn/snews/2452416.htm
- http://m.blog.uliejh.cn/snews/78325.htm
- http://m.blog.uliejh.cn/snews/308332.htm
- http://m.blog.uliejh.cn/snews/33023.htm
- http://m.blog.uliejh.cn/snews/40897.htm
- http://m.blog.uliejh.cn/snews/72844.htm
- http://m.blog.uliejh.cn/snews/103713.htm
- http://m.blog.uliejh.cn/snews/365632.htm
- http://m.blog.uliejh.cn/snews/67053.htm
- http://m.blog.uliejh.cn/snews/7175752.htm
- http://m.blog.uliejh.cn/snews/3508771.htm
- http://m.blog.uliejh.cn/snews/2727148.htm
- http://m.blog.uliejh.cn/snews/60002.htm
- http://m.blog.uliejh.cn/snews/7999.htm
- http://m.blog.uliejh.cn/snews/0360983.htm
- http://m.blog.uliejh.cn/snews/0005.htm
- http://m.blog.uliejh.cn/snews/389195.htm
- http://m.blog.uliejh.cn/snews/025384.htm
- http://m.blog.uliejh.cn/snews/7368411.htm
- http://m.blog.uliejh.cn/snews/8820.htm
- http://m.blog.uliejh.cn/snews/948648.htm
- http://m.blog.uliejh.cn/snews/0022.htm
- http://m.blog.uliejh.cn/snews/08052.htm
- http://m.blog.uliejh.cn/snews/3502930.htm
- http://m.blog.uliejh.cn/snews/125295.htm
- http://m.blog.uliejh.cn/snews/08316.htm
- http://m.blog.uliejh.cn/snews/0505844.htm
- http://m.blog.uliejh.cn/snews/4219823.htm
- http://m.blog.uliejh.cn/snews/6002084.htm
- http://m.blog.uliejh.cn/snews/4295.htm
- http://m.blog.uliejh.cn/snews/8218.htm
- http://m.blog.uliejh.cn/snews/5196.htm
- http://m.blog.uliejh.cn/snews/8131134.htm
- http://m.blog.uliejh.cn/snews/784845.htm
- http://m.blog.uliejh.cn/snews/42514.htm
- http://m.blog.uliejh.cn/snews/1741325.htm
- http://m.blog.uliejh.cn/snews/648836.htm
- http://m.blog.uliejh.cn/snews/39826.htm
- http://m.blog.uliejh.cn/snews/4893.htm
- http://m.blog.uliejh.cn/snews/7872.htm
- http://m.blog.uliejh.cn/snews/2606.htm
- http://m.blog.uliejh.cn/snews/729541.htm
- http://m.blog.uliejh.cn/snews/4270260.htm
- http://m.blog.uliejh.cn/snews/711412.htm
- http://m.blog.uliejh.cn/snews/9730390.htm
- http://m.blog.uliejh.cn/snews/45526.htm
- http://m.blog.uliejh.cn/snews/31256.htm
- http://m.blog.uliejh.cn/snews/805436.htm
- http://m.blog.uliejh.cn/snews/786533.htm
- http://m.blog.uliejh.cn/snews/676182.htm
- http://m.blog.uliejh.cn/snews/60270.htm
- http://m.blog.uliejh.cn/snews/737732.htm
- http://m.blog.uliejh.cn/snews/41514.htm
- http://m.blog.uliejh.cn/snews/700674.htm
- http://m.blog.uliejh.cn/snews/739237.htm
- http://m.blog.uliejh.cn/snews/767666.htm
- http://m.blog.uliejh.cn/snews/37231.htm
- http://m.blog.uliejh.cn/snews/012218.htm
- http://m.blog.uliejh.cn/snews/605992.htm
- http://m.blog.uliejh.cn/snews/0077428.htm
- http://m.blog.uliejh.cn/snews/129909.htm
- http://m.blog.uliejh.cn/snews/66275.htm
- http://m.blog.uliejh.cn/snews/007488.htm
- http://m.blog.uliejh.cn/snews/16407.htm
- http://m.blog.uliejh.cn/snews/0999624.htm
- http://m.blog.uliejh.cn/snews/1463129.htm
- http://m.blog.uliejh.cn/snews/4565.htm
- http://m.blog.uliejh.cn/snews/97480.htm
- http://m.blog.uliejh.cn/snews/5076.htm
- http://m.blog.uliejh.cn/snews/745231.htm
- http://m.blog.uliejh.cn/snews/9537.htm
- http://m.blog.uliejh.cn/snews/74311.htm
- http://m.blog.uliejh.cn/snews/3666321.htm
- http://m.blog.uliejh.cn/snews/098082.htm
- http://m.blog.uliejh.cn/snews/19292.htm
- http://m.blog.uliejh.cn/snews/68684.htm
- http://m.blog.uliejh.cn/snews/0760056.htm
- http://m.blog.uliejh.cn/snews/8648.htm
- http://m.blog.uliejh.cn/snews/494666.htm
- http://m.blog.uliejh.cn/snews/0357.htm
- http://m.blog.uliejh.cn/snews/0947376.htm
- http://m.blog.uliejh.cn/snews/4531800.htm
- http://m.blog.uliejh.cn/snews/5089.htm
- http://m.blog.uliejh.cn/snews/34449.htm
- http://m.blog.uliejh.cn/snews/8775795.htm
- http://m.blog.uliejh.cn/snews/333099.htm
- http://m.blog.uliejh.cn/snews/3503138.htm
- http://m.blog.uliejh.cn/snews/3996478.htm
- http://m.blog.uliejh.cn/snews/7370.htm
- http://m.blog.uliejh.cn/snews/9090956.htm
- http://m.blog.uliejh.cn/snews/6917420.htm
- http://m.blog.uliejh.cn/snews/9772653.htm
- http://m.blog.uliejh.cn/snews/6450536.htm
- http://m.blog.uliejh.cn/snews/399018.htm
- http://m.blog.uliejh.cn/snews/335785.htm
- http://m.blog.uliejh.cn/snews/0843347.htm
- http://m.blog.uliejh.cn/snews/421930.htm
- http://m.blog.uliejh.cn/snews/97876.htm
- http://m.blog.uliejh.cn/snews/715071.htm
- http://m.blog.uliejh.cn/snews/9510711.htm
- http://m.blog.uliejh.cn/snews/5481.htm
- http://m.blog.uliejh.cn/snews/564570.htm
- http://m.blog.uliejh.cn/snews/3803784.htm
- http://m.blog.uliejh.cn/snews/2441287.htm
- http://m.blog.uliejh.cn/snews/7718.htm

## 项目结构

```
weblink-hub/
├── resources/                         # 主资源目录，按领域分类
│   ├── backend/                       # 后端技术相关链接
│   │   ├── golang/                    # Go 语言生态资源
│   │   └── python/                    # Python 框架与库
│   ├── frontend/                      # 前端框架与工具
│   ├── devops/                        # CI/CD、容器化、监控
│   ├── academic/                      # 论文、预印本、学术博客
│   └── meta/                          # 项目自身元数据与标签定义
├── scripts/                           # 辅助工具集
│   ├── check_links.py                 # 并发链接校验主程序
│   ├── extract_meta.py                # 从 URL 提取标题/描述
│   └── export_formats/                # 导出 JSON/CSV/OPML 的子模块
├── docs/                              # 项目文档与站点源码
│   ├── .vuepress/                     # VuePress 配置与主题覆盖
│   ├── guide/                         # 用户使用手册
│   └── development/                   # 贡献者开发指南
├── reports/                           # 校验报告输出目录（gitignored）
├── .github/                           # GitHub Actions 工作流
│   └── workflows/
│       └── weekly_check.yml           # 每周自动校验任务
├── requirements.txt                   # Python 依赖声明
├── Makefile                           # 常用任务快捷命令
└── README.md                          # 项目入口文档
```

## 贡献指南

1. 在 `resources/` 下选择合适的分类目录，若不存在可新建，并更新 `meta/tags.yaml` 中的分类定义。
2. 新增资源条目时，请在同目录的 `index.md` 或独立 `.md` 文件中以无序列表格式添加 URL，并尽量包含 `<!-- title: ... -->` 等元数据注释。
3. 提交前请本地运行 `python scripts/check_links.py --source resources/` 确保新增链接可访问，若有失效需先修复或注释说明。
4. 提交 Pull Request 时请参照 `docs/development/PR_TEMPLATE.md` 填写变更摘要，包括新增链接数量、校验结果摘要及分类调整说明。
5. 若需批量导入或清理过期链接，请使用 `scripts/batch_import.py` 辅助脚本，并在 PR 中附上导入日志。

## 常见问题

**Q：链接校验工具报 SSL 证书错误如何处理？**
A：部分内网或自签名站点会出现此问题。可在 `scripts/config.yaml` 中将 `verify_ssl` 设为 `false`，但仅建议在受信网络环境中使用。亦可通过 `--timeout` 参数增大超时阈值。

**Q：资源列表中的链接数量很大，如何避免校验耗时过长？**
A：校验脚本默认并发数为 50，可通过 `--concurrency` 参数调整。建议在 CI 环境中设置为 20 以避免被目标站点限流。同时可利用 `--only-new` 参数仅校验上次运行后新增的链接。

**Q：本项目是否可以直接用于生产环境文档站？**
A：可以。项目本身不包含服务端逻辑，仅维护 Markdown 数据与校验工具。您可将 `resources/` 目录作为数据源，通过任意静态站点生成器构建导航页面。生产部署时建议配合 CDN 缓存与定期校验任务。

## 许可证

MIT

> 外链数量: 250 | 生成时间: 2026-08-24 23:40:21
