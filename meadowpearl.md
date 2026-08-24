# LinkVault Indexer

LinkVault Indexer 是一个面向技术文档聚合与外部资源索引的开源工具链，专为需要批量管理、分类展示和快速检索大量外部 URL 的开发团队与内容运营者设计。该项目不依赖特定 CMS 或商业平台，通过纯静态化的索引机制，将零散的链接资源转化为结构清晰、可维护的导航数据。

项目目标用户包括开源文档维护者、技术社区运营人员、科研信息整理人员以及需要定期同步外部参考链接的 DevOps 团队。LinkVault Indexer 解决的核心问题是：当外部参考链接数量超过人工管理阈值时，如何通过自动化索引脚本保证链接的可访问性、分类一致性和更新可追溯性。

## 功能概览

**批量链接标准化入库**：支持从纯文本、CSV 或简单列表批量导入 URL，自动识别协议与域名格式，并在入库时执行协议一致性校验。

**多级标签分类系统**：允许用户为每个链接定义层级标签（如 /tech/backend/rust /news/security），并基于标签树生成多维度分类视图。

**可配置的可用性检查**：内置轻量级 HTTP 探活模块，可定期检测链接状态，输出失效报告，并标记异常链接。

**静态文档生成引擎**：基于模板系统将索引数据渲染为完整的 HTML 或 Markdown 文档，适合直接部署为静态站点或集成至 MkDocs、VuePress 等工具。

**外部元数据缓存**：支持通过配置抓取目标页面的标题、描述或关键词，减少重复请求，提升索引页面的信息密度。

**链接关系图谱输出**：提供简单的引用关系分析功能，可识别域内链接与域外链接的分布比例，辅助内容审计。

**增量更新与变更日志**：每次运行索引脚本时自动生成变更记录（新增、删除、URL 变动），方便团队协作审查。

## 应用场景

技术博客的参考链接库维护：技术作者在撰写多篇相关文章时，可将所有外部引用链接统一提交至 LinkVault Indexer，由系统自动生成带分类的引用附录，避免手动整理时的遗漏或重复。

开源项目文档的外部依赖索引：大型开源项目通常需要引用多种协议、服务或工具官网。维护者可将这些链接录入系统，并在每次发版前运行可用性检查，确保文档中的所有外部链接依然有效。

企业内部知识库的链接导航构建：企业技术部门可将日常使用的内部工具地址、云服务控制台入口、日志系统链接等集中管理，通过 LinkVault Indexer 生成部门共享的导航页面，减少员工查找时间。

批量历史数据迁移中的链接转储：当旧版网站或 Wiki 系统需要迁移时，可将所有内嵌外链导出为列表，利用 LinkVault Indexer 进行分类和去重，为迁移后的链接重定向策略提供数据基础。

## 快速开始

以下步骤适用于 Linux 及 macOS 环境，Windows 用户可借助 WSL 或 Git Bash 执行。

```bash
git clone https://github.com/your-org/linkvault-indexer.git
cd linkvault-indexer

# 创建 Python 虚拟环境并安装依赖
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt

# 准备链接数据文件（默认读取 ./data/raw_links.txt，每行一个 URL）
# 示例：将下方「资源列表」中的链接保存到 raw_links.txt

# 运行索引构建命令
python indexer.py build --input ./data/raw_links.txt --output ./dist

# 启动本地预览服务器
python -m http.server 8000 --directory ./dist
```

访问 `http://localhost:8000` 即可查看生成的索引页面。

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|---------|---------|------|
| Python | 3.9 及以上 | 核心运行环境，需支持 asyncio 和 pathlib |
| pip | 22.0 及以上 | 包管理工具，用于安装 requirements.txt 中的依赖 |
| requests | 2.28.0 | 用于 HTTP 可用性检查与元数据抓取 |
| jinja2 | 3.1.0 | 模板引擎，负责渲染静态文档 |
| pyyaml | 6.0 | 解析配置文件（config.yaml），支持标签映射和规则定义 |
| rich | 13.0 | 终端日志美化，用于显示构建进度和检查结果 |
| pytest | 7.0 | 仅开发测试时需要，生产环境可不安装 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|------|------|-----------|
| 用户手册 | /docs/user-guide/ | 如何安装、配置输入源、调整标签规则、执行构建命令？ |
| 模板开发指南 | /docs/template-guide/ | 如何自定义索引页面的布局、样式和元数据显示方式？ |
| 配置文件参考 | /docs/config-reference/ | config.yaml 中每个字段的含义、默认值及可选项是什么？ |
| 插件扩展文档 | /docs/plugin-dev/ | 如何编写自定义校验器、元数据抓取器和输出格式插件？ |
| API 接口说明 | /docs/api/ | 内部模块函数与类的调用约定，适用于二次开发或集成调用 |

## 资源列表

- http://m.3g.uliejh.cn/nnews/7227737.htm
- http://m.3g.uliejh.cn/nnews/45473.htm
- http://m.3g.uliejh.cn/nnews/06506.htm
- http://m.3g.uliejh.cn/nnews/35067.htm
- http://m.3g.uliejh.cn/nnews/523385.htm
- http://m.3g.uliejh.cn/nnews/8034401.htm
- http://m.3g.uliejh.cn/nnews/2689.htm
- http://m.3g.uliejh.cn/nnews/929423.htm
- http://m.3g.uliejh.cn/nnews/55001.htm
- http://m.3g.uliejh.cn/nnews/642749.htm
- http://m.3g.uliejh.cn/nnews/8909467.htm
- http://m.3g.uliejh.cn/nnews/5680.htm
- http://m.3g.uliejh.cn/nnews/8614861.htm
- http://m.3g.uliejh.cn/nnews/815399.htm
- http://m.3g.uliejh.cn/nnews/2673849.htm
- http://m.3g.uliejh.cn/nnews/5751164.htm
- http://m.3g.uliejh.cn/nnews/9160.htm
- http://m.3g.uliejh.cn/nnews/2310.htm
- http://m.3g.uliejh.cn/nnews/9921.htm
- http://m.3g.uliejh.cn/nnews/4404.htm
- http://m.3g.uliejh.cn/nnews/08739.htm
- http://m.3g.uliejh.cn/nnews/1058827.htm
- http://m.3g.uliejh.cn/nnews/36671.htm
- http://m.3g.uliejh.cn/nnews/192429.htm
- http://m.3g.uliejh.cn/nnews/5508631.htm
- http://m.3g.uliejh.cn/nnews/84587.htm
- http://m.3g.uliejh.cn/nnews/8049372.htm
- http://m.3g.uliejh.cn/nnews/34870.htm
- http://m.3g.uliejh.cn/nnews/373349.htm
- http://m.3g.uliejh.cn/nnews/8945.htm
- http://m.3g.uliejh.cn/nnews/6059.htm
- http://m.3g.uliejh.cn/nnews/0037.htm
- http://m.3g.uliejh.cn/nnews/087047.htm
- http://m.3g.uliejh.cn/nnews/662285.htm
- http://m.3g.uliejh.cn/nnews/5270.htm
- http://m.3g.uliejh.cn/nnews/44035.htm
- http://m.3g.uliejh.cn/nnews/8996693.htm
- http://m.3g.uliejh.cn/nnews/385757.htm
- http://m.3g.uliejh.cn/nnews/922476.htm
- http://m.3g.uliejh.cn/nnews/9818.htm
- http://m.3g.uliejh.cn/nnews/54037.htm
- http://m.3g.uliejh.cn/nnews/091823.htm
- http://m.3g.uliejh.cn/nnews/045069.htm
- http://m.3g.uliejh.cn/nnews/756697.htm
- http://m.3g.uliejh.cn/nnews/6761128.htm
- http://m.3g.uliejh.cn/nnews/5990500.htm
- http://m.3g.uliejh.cn/nnews/5595.htm
- http://m.3g.uliejh.cn/nnews/942709.htm
- http://m.3g.uliejh.cn/nnews/8452654.htm
- http://m.3g.uliejh.cn/nnews/5012.htm
- http://m.3g.uliejh.cn/nnews/8733.htm
- http://m.3g.uliejh.cn/nnews/084724.htm
- http://m.3g.uliejh.cn/nnews/5885.htm
- http://m.3g.uliejh.cn/nnews/7119.htm
- http://m.3g.uliejh.cn/nnews/5000.htm
- http://m.3g.uliejh.cn/nnews/48897.htm
- http://m.3g.uliejh.cn/nnews/7278.htm
- http://m.3g.uliejh.cn/nnews/94653.htm
- http://m.3g.uliejh.cn/nnews/50273.htm
- http://m.3g.uliejh.cn/nnews/8655.htm
- http://m.3g.uliejh.cn/nnews/7304.htm
- http://m.3g.uliejh.cn/nnews/96839.htm
- http://m.3g.uliejh.cn/nnews/638521.htm
- http://m.3g.uliejh.cn/nnews/2729.htm
- http://m.3g.uliejh.cn/nnews/22445.htm
- http://m.3g.uliejh.cn/nnews/35268.htm
- http://m.3g.uliejh.cn/nnews/582055.htm
- http://m.3g.uliejh.cn/nnews/9132554.htm
- http://m.3g.uliejh.cn/nnews/5181078.htm
- http://m.3g.uliejh.cn/nnews/1529.htm
- http://m.3g.uliejh.cn/nnews/119522.htm
- http://m.3g.uliejh.cn/nnews/2597.htm
- http://m.3g.uliejh.cn/nnews/2043.htm
- http://m.3g.uliejh.cn/nnews/987177.htm
- http://m.3g.uliejh.cn/nnews/1735099.htm
- http://m.3g.uliejh.cn/nnews/5430889.htm
- http://m.3g.uliejh.cn/nnews/2254.htm
- http://m.3g.uliejh.cn/nnews/664732.htm
- http://m.3g.uliejh.cn/nnews/7473489.htm
- http://m.3g.uliejh.cn/nnews/6935883.htm
- http://m.3g.uliejh.cn/nnews/2883.htm
- http://m.3g.uliejh.cn/nnews/3685.htm
- http://m.3g.uliejh.cn/nnews/313265.htm
- http://m.3g.uliejh.cn/nnews/422734.htm
- http://m.3g.uliejh.cn/nnews/232990.htm
- http://m.3g.uliejh.cn/nnews/7458185.htm
- http://m.3g.uliejh.cn/nnews/247220.htm
- http://m.3g.uliejh.cn/nnews/4328713.htm
- http://m.3g.uliejh.cn/nnews/15269.htm
- http://m.3g.uliejh.cn/nnews/4607803.htm
- http://m.3g.uliejh.cn/nnews/26123.htm
- http://m.3g.uliejh.cn/nnews/9227.htm
- http://m.3g.uliejh.cn/nnews/166759.htm
- http://m.3g.uliejh.cn/nnews/0161.htm
- http://m.3g.uliejh.cn/nnews/9216004.htm
- http://m.3g.uliejh.cn/nnews/57203.htm
- http://m.3g.uliejh.cn/nnews/528289.htm
- http://m.3g.uliejh.cn/nnews/39224.htm
- http://m.3g.uliejh.cn/nnews/3451646.htm
- http://m.3g.uliejh.cn/nnews/1510.htm
- http://m.3g.uliejh.cn/nnews/6968426.htm
- http://m.3g.uliejh.cn/nnews/3507.htm
- http://m.3g.uliejh.cn/nnews/569320.htm
- http://m.3g.uliejh.cn/nnews/3179888.htm
- http://m.3g.uliejh.cn/nnews/600475.htm
- http://m.3g.uliejh.cn/nnews/66134.htm
- http://m.3g.uliejh.cn/nnews/6745.htm
- http://m.3g.uliejh.cn/nnews/234033.htm
- http://m.3g.uliejh.cn/nnews/15671.htm
- http://m.3g.uliejh.cn/nnews/07879.htm
- http://m.3g.uliejh.cn/nnews/6942.htm
- http://m.3g.uliejh.cn/nnews/85867.htm
- http://m.3g.uliejh.cn/nnews/46797.htm
- http://m.3g.uliejh.cn/nnews/0282.htm
- http://m.3g.uliejh.cn/nnews/740794.htm
- http://m.3g.uliejh.cn/nnews/2191.htm
- http://m.3g.uliejh.cn/nnews/493031.htm
- http://m.3g.uliejh.cn/nnews/935884.htm
- http://m.3g.uliejh.cn/nnews/7203.htm
- http://m.3g.uliejh.cn/nnews/6252.htm
- http://m.3g.uliejh.cn/nnews/483356.htm
- http://m.3g.uliejh.cn/nnews/4500.htm
- http://m.3g.uliejh.cn/nnews/52212.htm
- http://m.3g.uliejh.cn/nnews/0143323.htm
- http://m.3g.uliejh.cn/nnews/558770.htm
- http://m.3g.uliejh.cn/nnews/9557.htm
- http://m.3g.uliejh.cn/nnews/42850.htm
- http://m.3g.uliejh.cn/nnews/06721.htm
- http://m.3g.uliejh.cn/nnews/6882.htm
- http://m.3g.uliejh.cn/nnews/3796704.htm
- http://m.3g.uliejh.cn/nnews/1673778.htm
- http://m.3g.uliejh.cn/nnews/81523.htm
- http://m.3g.uliejh.cn/nnews/7100.htm
- http://m.3g.uliejh.cn/nnews/33201.htm
- http://m.3g.uliejh.cn/nnews/2936.htm
- http://m.3g.uliejh.cn/nnews/676467.htm
- http://m.3g.uliejh.cn/nnews/4799280.htm
- http://m.3g.uliejh.cn/nnews/458713.htm
- http://m.3g.uliejh.cn/nnews/3004686.htm
- http://m.3g.uliejh.cn/nnews/613905.htm
- http://m.3g.uliejh.cn/nnews/0023882.htm
- http://m.3g.uliejh.cn/nnews/400132.htm
- http://m.3g.uliejh.cn/nnews/982367.htm
- http://m.3g.uliejh.cn/nnews/81452.htm
- http://m.3g.uliejh.cn/nnews/7372.htm
- http://m.3g.uliejh.cn/nnews/7663.htm
- http://m.3g.uliejh.cn/nnews/352241.htm
- http://m.3g.uliejh.cn/nnews/0236809.htm
- http://m.3g.uliejh.cn/nnews/1410.htm
- http://m.3g.uliejh.cn/nnews/657448.htm
- http://m.3g.uliejh.cn/nnews/1690.htm
- http://m.3g.uliejh.cn/nnews/9557884.htm
- http://m.3g.uliejh.cn/nnews/27987.htm
- http://m.3g.uliejh.cn/nnews/93938.htm
- http://m.3g.uliejh.cn/nnews/119718.htm
- http://m.3g.uliejh.cn/nnews/9521.htm
- http://m.3g.uliejh.cn/nnews/25659.htm
- http://m.3g.uliejh.cn/nnews/51879.htm
- http://m.3g.uliejh.cn/nnews/13654.htm
- http://m.3g.uliejh.cn/nnews/9205151.htm
- http://m.3g.uliejh.cn/nnews/580815.htm
- http://m.3g.uliejh.cn/nnews/20878.htm
- http://m.3g.uliejh.cn/nnews/1608929.htm
- http://m.3g.uliejh.cn/nnews/59386.htm
- http://m.3g.uliejh.cn/nnews/763448.htm
- http://m.3g.uliejh.cn/nnews/06689.htm
- http://m.3g.uliejh.cn/nnews/3668.htm
- http://m.3g.uliejh.cn/nnews/4902796.htm
- http://m.3g.uliejh.cn/nnews/992577.htm
- http://m.3g.uliejh.cn/nnews/27236.htm
- http://m.3g.uliejh.cn/nnews/058318.htm
- http://m.3g.uliejh.cn/nnews/6455535.htm
- http://m.3g.uliejh.cn/nnews/8130783.htm
- http://m.3g.uliejh.cn/nnews/1895.htm
- http://m.3g.uliejh.cn/nnews/3867.htm
- http://m.3g.uliejh.cn/nnews/16925.htm
- http://m.3g.uliejh.cn/nnews/974923.htm
- http://m.3g.uliejh.cn/nnews/23644.htm
- http://m.3g.uliejh.cn/nnews/4134685.htm
- http://m.3g.uliejh.cn/nnews/677586.htm
- http://m.3g.uliejh.cn/nnews/1519.htm
- http://m.3g.uliejh.cn/nnews/046348.htm
- http://m.3g.uliejh.cn/nnews/664793.htm
- http://m.3g.uliejh.cn/nnews/61514.htm
- http://m.3g.uliejh.cn/nnews/4371.htm
- http://m.3g.uliejh.cn/nnews/6779.htm
- http://m.3g.uliejh.cn/nnews/4520964.htm
- http://m.3g.uliejh.cn/nnews/6252708.htm
- http://m.3g.uliejh.cn/nnews/579688.htm
- http://m.3g.uliejh.cn/nnews/60339.htm
- http://m.3g.uliejh.cn/nnews/3700071.htm
- http://m.3g.uliejh.cn/nnews/6379.htm
- http://m.3g.uliejh.cn/nnews/3005.htm
- http://m.3g.uliejh.cn/nnews/4441.htm
- http://m.3g.uliejh.cn/nnews/797922.htm
- http://m.3g.uliejh.cn/nnews/218934.htm
- http://m.3g.uliejh.cn/nnews/99976.htm
- http://m.3g.uliejh.cn/nnews/6164923.htm
- http://m.3g.uliejh.cn/nnews/9921426.htm
- http://m.3g.uliejh.cn/nnews/1260790.htm
- http://m.3g.uliejh.cn/nnews/73121.htm
- http://m.3g.uliejh.cn/nnews/740742.htm
- http://m.3g.uliejh.cn/nnews/8789.htm
- http://m.3g.uliejh.cn/nnews/3802.htm
- http://m.3g.uliejh.cn/nnews/9860013.htm
- http://m.3g.uliejh.cn/nnews/760387.htm
- http://m.3g.uliejh.cn/nnews/570420.htm
- http://m.3g.uliejh.cn/nnews/06042.htm
- http://m.3g.uliejh.cn/nnews/63744.htm
- http://m.3g.uliejh.cn/nnews/9246694.htm
- http://m.3g.uliejh.cn/nnews/2440784.htm
- http://m.3g.uliejh.cn/nnews/7432757.htm
- http://m.3g.uliejh.cn/nnews/161599.htm
- http://m.3g.uliejh.cn/nnews/4302.htm
- http://m.3g.uliejh.cn/nnews/008494.htm
- http://m.3g.uliejh.cn/nnews/50356.htm
- http://m.3g.uliejh.cn/nnews/19958.htm
- http://m.3g.uliejh.cn/nnews/1497.htm
- http://m.3g.uliejh.cn/nnews/0747656.htm
- http://m.3g.uliejh.cn/nnews/4984986.htm
- http://m.3g.uliejh.cn/nnews/0126821.htm
- http://m.3g.uliejh.cn/nnews/8742.htm
- http://m.3g.uliejh.cn/nnews/9010.htm
- http://m.3g.uliejh.cn/nnews/389546.htm
- http://m.3g.uliejh.cn/nnews/56341.htm
- http://m.3g.uliejh.cn/nnews/8923259.htm
- http://m.3g.uliejh.cn/nnews/31569.htm
- http://m.3g.uliejh.cn/nnews/58909.htm
- http://m.3g.uliejh.cn/nnews/1407.htm
- http://m.3g.uliejh.cn/nnews/9976691.htm
- http://m.3g.uliejh.cn/nnews/4724044.htm
- http://m.3g.uliejh.cn/nnews/46582.htm
- http://m.3g.uliejh.cn/nnews/9967321.htm
- http://m.3g.uliejh.cn/nnews/1887.htm
- http://m.3g.uliejh.cn/nnews/666132.htm
- http://m.3g.uliejh.cn/nnews/07074.htm
- http://m.3g.uliejh.cn/nnews/872381.htm
- http://m.3g.uliejh.cn/nnews/448953.htm
- http://m.3g.uliejh.cn/nnews/26577.htm
- http://m.3g.uliejh.cn/nnews/6689629.htm
- http://m.3g.uliejh.cn/nnews/04412.htm
- http://m.3g.uliejh.cn/nnews/92599.htm
- http://m.3g.uliejh.cn/nnews/7679780.htm
- http://m.3g.uliejh.cn/nnews/6821261.htm
- http://m.3g.uliejh.cn/nnews/5584.htm
- http://m.3g.uliejh.cn/nnews/5691.htm
- http://m.3g.uliejh.cn/nnews/39184.htm
- http://m.3g.uliejh.cn/nnews/3345865.htm
- http://m.3g.uliejh.cn/nnews/267836.htm
- http://m.3g.uliejh.cn/nnews/596548.htm

## 项目结构

```
linkvault-indexer/
├── indexer.py                 # 主入口脚本，整合构建、检查与输出流程
├── config.yaml                # 全局配置文件，定义标签映射、超时阈值、输出目录
├── requirements.txt           # Python 依赖清单，锁定主要库版本
├── .gitignore                 # 忽略 .venv、__pycache__、dist 等临时目录
│
├── core/                      # 核心逻辑模块包
│   ├── __init__.py
│   ├── loader.py              # 原始链接加载器，支持 txt / csv / json 格式
│   ├── validator.py           # 协议校验、去重、域名白名单过滤
│   ├── checker.py             # HTTP 可用性探活，异步并发检查
│   └── cache.py               # 元数据与状态缓存管理，减少重复网络请求
│
├── parser/                    # 解析与分类模块
│   ├── __init__.py
│   ├── tagger.py              # 基于路径关键字与正则表达式的自动标签生成
│   └── extractor.py           # 从目标页面提取 title / description (可配置)
│
├── renderer/                  # 文档渲染模块
│   ├── __init__.py
│   ├── context.py             # 构建模板上下文（标签树、统计信息、变更日志）
│   ├── markdown.py            # 输出 Markdown 格式的索引文件
│   └── html.py                # 输出 HTML 格式（使用 Jinja2 模板）
│
├── templates/                 # Jinja2 模板文件目录
│   ├── base.html              # 基础布局模板
│   ├── index.html             # 索引主页模板
│   └── detail.html            # 单条链接详情页模板（可选）
│
├── data/                      # 数据与样例目录
│   ├── raw_links.sample.txt   # 样例链接列表文件，用户可替换为自己的数据
│   └── tags.mapping.yaml      # 预定义标签映射规则（正则 -> 标签路径）
│
├── dist/                      # 默认输出目录（构建生成，不纳入版本控制）
│   ├── index.html
│   ├── links.md
│   └── reports/               # 可用性检查报告存放位置
│
└── tests/                     # 单元测试与集成测试目录
    ├── test_loader.py
    ├── test_validator.py
    ├── test_checker.py
    └── test_renderer.py
```

## 贡献指南

1. 查阅 issue 列表或项目看板，选取未被指派的特性或缺陷任务，在对应 issue 下回复确认认领，避免重复工作。

2. 派生项目仓库至个人账户，基于 main 分支创建功能分支，分支命名遵循 `feature/简述` 或 `fix/简述` 格式，例如 `feature/tag-optimize`。

3. 编写或修改代码时，需同步更新受影响模块的 docstring 及对应的单元测试用例，确保测试覆盖新增逻辑，并运行 `pytest tests/` 验证全部用例通过。

4. 提交前执行 `python indexer.py build --test` 以完整构建一次示例数据，确认输出页面无异常渲染或路径错误，同时检查 `dist/` 目录下的报告文件是否正常生成。

5. 发起合并请求至 main 分支，在描述中关联对应 issue 编号，并附上本地构建日志或截图（如有页面样式改动）。项目维护者将在 2 个工作日内进行审查。

## 常见问题

问：输入文件中的链接包含多种协议（http、https、ftp 等），系统如何处理？

答：当前版本仅支持 http 与 https 协议的链接校验与探活。其他协议（如 ftp、mailto）会被记录为 "跳过" 状态，并在报告中单独标注。用户可在 config.yaml 中调整 `allowed_protocols` 列表以扩展支持范围，但需自行承担相应协议的可用性检查逻辑实现。

问：链接可用性检查的并发数和超时时间如何调整？

答：在 config.yaml 的 `checker` 段落下，通过 `max_concurrent` 控制最大并发数（默认 20），`timeout_seconds` 控制单次请求超时（默认 5 秒）。对于网络条件较差的运行环境，建议降低并发数并适当增加超时时间，以减少误报。调整后无需重启服务，下次构建时自动生效。

问：生成的索引页面能否直接部署到 GitHub Pages 或 Nginx？

答：可以。`dist/` 目录中输出的是纯静态 HTML 和 Markdown 文件，不依赖后端服务。将 `dist/` 下的所有文件上传至 GitHub Pages 仓库的根目录或 docs 文件夹，或复制到 Nginx 的 html 目录下，即可直接访问。注意需要保留相对路径结构，避免资源引用 404 错误。

## 许可证

MIT

> 外链数量: 250 | 生成时间: 2026-08-24 23:40:21
