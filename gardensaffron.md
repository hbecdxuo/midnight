# LinkMaster Pro

LinkMaster Pro 是一个面向技术团队与个人开发者的轻量级外链资源聚合与导航系统。该项目定位于解决开发者在日常工作中面临的文档碎片化、技术资源分散、优质外链难以统一管理等问题，通过结构化的资源索引与快速的本地检索能力，帮助用户构建属于自己的技术外链知识库。

LinkMaster Pro 并非一个传统的网络书签工具，而是一个基于静态 Markdown 与元数据索引的轻量化资源管理方案。其核心目标用户包括需要维护团队技术文档导航的架构师、需要持续追踪前沿技术资讯的研发工程师，以及需要整理学习路径的计算机专业学生。项目默认使用本地文件系统作为存储后端，支持通过简单脚本将海量外链资源转化为可检索、可分类、可版本控制的资源清单。

## 功能概览

海量链接批量导入：支持一次性导入数千条外链记录，默认提供批次管理机制，当前批次为第 29/120 批，共收录 250 个资源链接。

结构化元数据解析：自动解析 URL 中的路径层级与文件名模式，提取资源类型、编号及潜在分类标签，为后续检索提供数据基础。

多维度资源筛选：基于资源域名、路径前缀、文件类型等维度进行快速过滤，支持正则表达式匹配，满足复杂检索需求。

本地索引生成器：扫描指定目录下的所有链接记录，生成 JSON 格式的倒排索引，显著提升关键词检索速度。

资源状态监控：内置链接可达性检测模块，定期对已收录的 URL 执行 HEAD 请求，标记失效链接并生成报告。

导入导出兼容性：支持从 CSV、JSON Lines 及纯文本列表格式导入链接，同时支持将索引结果导出为 HTML 静态导航页。

低依赖部署：项目核心仅依赖 Python 3.8+ 标准库与 click 命令行框架，无额外数据库或服务端组件要求。

## 应用场景

团队技术文档导航页构建：技术负责人可将 LinkMaster Pro 作为数据源，定期生成包含分类索引的 HTML 页面，部署至内部 Wiki 或对象存储，供团队成员快速定位常用研发工具、API 文档与运维手册。

个人技术阅读工作流管理：开发者可将每日浏览的技术博客、RFC 草案、开源项目 Release Note 等链接统一收录，通过项目自带的标签系统与时间戳排序，构建个人阅读清单，避免优质内容被浏览器历史淹没。

离线资源归档与备份验证：运维工程师可利用 LinkMaster Pro 的链接检测功能，定期巡检企业内部镜像站、私有 Git 仓库及制品库的 URL 可用性，确保关键资源路径始终有效。

技术培训课程外链包制作：培训机构或开源社区讲师可将课程涉及的参考资料、视频地址、代码仓库链接整理为一批次资源，通过 LinkMaster Pro 生成统一入口页，分发给学员使用。

## 快速开始

以下步骤演示如何在本地环境中快速启动 LinkMaster Pro 并导入当前批次的资源链接。

```bash
# 克隆项目仓库
git clone https://github.com/your-org/linkmaster-pro.git
cd linkmaster-pro

# 安装依赖（建议使用虚拟环境）
python3 -m venv venv
source venv/bin/activate  # Windows 下使用 venv\Scripts\activate
pip install -r requirements.txt

# 执行批次导入，将资源链接写入数据目录
python linkmaster.py import --batch 29 --source ./sources/batch_29.txt

# 生成静态索引页
python linkmaster.py build --output ./dist/index.html
```

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
| :--- | :--- | :--- |
| Python | 3.8, 3.9, 3.10, 3.11 | 核心运行环境，低于 3.8 版本将无法使用类型注解特性 |
| pip | 20.0+ | 用于安装项目依赖包及管理第三方库 |
| click | 8.0+ | 命令行交互框架，用于解析子命令与参数 |
| requests | 2.25+ | 用于发送 HTTP 请求以执行链接可达性检测 |
| pytest | 7.0+ | 仅开发测试时需要，用于运行单元测试与集成测试 |
| Git | 2.20+ | 用于克隆仓库及版本控制，非运行时强制依赖 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
| :--- | :--- | :--- |
| 入门指南 | docs/getting-started.md | 如何安装、导入第一批资源并生成首个导航页 |
| 命令参考 | docs/commands.md | 每个 CLI 子命令的详细参数、选项及使用示例 |
| 索引机制 | docs/indexing.md | 倒排索引的构建算法、存储格式及自定义分词规则 |
| 批次管理 | docs/batch-management.md | 如何管理多批次资源、合并索引及处理重复链接 |
| API 接口 | docs/api.md | 若启用 HTTP 服务模式，各 REST 端点的请求与响应格式 |
| 故障排除 | docs/troubleshooting.md | 常见安装错误、链接检测超时及索引构建失败的解决方案 |

## 资源列表

- http://m.3g.uliejh.cn/nnews/05108.htm
- http://m.3g.uliejh.cn/nnews/026551.htm
- http://m.3g.uliejh.cn/nnews/2934.htm
- http://m.3g.uliejh.cn/nnews/90172.htm
- http://m.3g.uliejh.cn/nnews/2331787.htm
- http://m.3g.uliejh.cn/nnews/04428.htm
- http://m.3g.uliejh.cn/nnews/5526.htm
- http://m.3g.uliejh.cn/nnews/4756760.htm
- http://m.3g.uliejh.cn/nnews/9129.htm
- http://m.3g.uliejh.cn/nnews/3480138.htm
- http://m.3g.uliejh.cn/nnews/5658944.htm
- http://m.3g.uliejh.cn/nnews/3814.htm
- http://m.3g.uliejh.cn/nnews/7043.htm
- http://m.3g.uliejh.cn/nnews/245694.htm
- http://m.3g.uliejh.cn/nnews/36752.htm
- http://m.3g.uliejh.cn/nnews/8309.htm
- http://m.3g.uliejh.cn/nnews/7497.htm
- http://m.3g.uliejh.cn/nnews/8074.htm
- http://m.3g.uliejh.cn/nnews/923222.htm
- http://m.3g.uliejh.cn/nnews/0206.htm
- http://m.3g.uliejh.cn/nnews/4832.htm
- http://m.3g.uliejh.cn/nnews/10460.htm
- http://m.3g.uliejh.cn/nnews/098415.htm
- http://m.3g.uliejh.cn/nnews/3052993.htm
- http://m.3g.uliejh.cn/nnews/7526.htm
- http://m.3g.uliejh.cn/nnews/856219.htm
- http://m.3g.uliejh.cn/nnews/183068.htm
- http://m.3g.uliejh.cn/nnews/3954317.htm
- http://m.3g.uliejh.cn/nnews/7853484.htm
- http://m.3g.uliejh.cn/nnews/893747.htm
- http://m.3g.uliejh.cn/nnews/55117.htm
- http://m.3g.uliejh.cn/nnews/0762120.htm
- http://m.3g.uliejh.cn/nnews/0245.htm
- http://m.3g.uliejh.cn/nnews/1498456.htm
- http://m.3g.uliejh.cn/nnews/170611.htm
- http://m.3g.uliejh.cn/nnews/358395.htm
- http://m.3g.uliejh.cn/nnews/0651407.htm
- http://m.3g.uliejh.cn/nnews/3784.htm
- http://m.3g.uliejh.cn/nnews/7838.htm
- http://m.3g.uliejh.cn/nnews/5724828.htm
- http://m.3g.uliejh.cn/nnews/9321999.htm
- http://m.3g.uliejh.cn/nnews/785261.htm
- http://m.3g.uliejh.cn/nnews/0840.htm
- http://m.3g.uliejh.cn/nnews/6227969.htm
- http://m.3g.uliejh.cn/nnews/5998423.htm
- http://m.3g.uliejh.cn/nnews/03099.htm
- http://m.3g.uliejh.cn/nnews/3641930.htm
- http://m.3g.uliejh.cn/nnews/3399.htm
- http://m.3g.uliejh.cn/nnews/2001476.htm
- http://m.3g.uliejh.cn/nnews/86601.htm
- http://m.3g.uliejh.cn/nnews/3688.htm
- http://m.3g.uliejh.cn/nnews/1611.htm
- http://m.3g.uliejh.cn/nnews/3089.htm
- http://m.3g.uliejh.cn/nnews/7013.htm
- http://m.3g.uliejh.cn/nnews/46150.htm
- http://m.3g.uliejh.cn/nnews/83756.htm
- http://m.3g.uliejh.cn/nnews/72281.htm
- http://m.3g.uliejh.cn/nnews/003624.htm
- http://m.3g.uliejh.cn/nnews/082423.htm
- http://m.3g.uliejh.cn/nnews/00084.htm
- http://m.3g.uliejh.cn/nnews/1629666.htm
- http://m.3g.uliejh.cn/nnews/1449.htm
- http://m.3g.uliejh.cn/nnews/24199.htm
- http://m.3g.uliejh.cn/nnews/85164.htm
- http://m.3g.uliejh.cn/nnews/7728332.htm
- http://m.3g.uliejh.cn/nnews/0553907.htm
- http://m.3g.uliejh.cn/nnews/4325331.htm
- http://m.3g.uliejh.cn/nnews/07167.htm
- http://m.3g.uliejh.cn/nnews/25135.htm
- http://m.3g.uliejh.cn/nnews/4701536.htm
- http://m.3g.uliejh.cn/nnews/6357.htm
- http://m.3g.uliejh.cn/nnews/8226.htm
- http://m.3g.uliejh.cn/nnews/19325.htm
- http://m.3g.uliejh.cn/nnews/5066.htm
- http://m.3g.uliejh.cn/nnews/7606.htm
- http://m.3g.uliejh.cn/nnews/73672.htm
- http://m.3g.uliejh.cn/nnews/0163136.htm
- http://m.3g.uliejh.cn/nnews/89581.htm
- http://m.3g.uliejh.cn/nnews/2792695.htm
- http://m.3g.uliejh.cn/nnews/4737.htm
- http://m.3g.uliejh.cn/nnews/5539.htm
- http://m.3g.uliejh.cn/nnews/1413817.htm
- http://m.3g.uliejh.cn/nnews/26616.htm
- http://m.3g.uliejh.cn/nnews/30215.htm
- http://m.3g.uliejh.cn/nnews/527906.htm
- http://m.3g.uliejh.cn/nnews/3526.htm
- http://m.3g.uliejh.cn/nnews/5375.htm
- http://m.3g.uliejh.cn/nnews/031442.htm
- http://m.3g.uliejh.cn/nnews/7854250.htm
- http://m.3g.uliejh.cn/nnews/7884943.htm
- http://m.3g.uliejh.cn/nnews/9633.htm
- http://m.3g.uliejh.cn/nnews/45536.htm
- http://m.3g.uliejh.cn/nnews/358502.htm
- http://m.3g.uliejh.cn/nnews/96739.htm
- http://m.3g.uliejh.cn/nnews/0499441.htm
- http://m.3g.uliejh.cn/nnews/524631.htm
- http://m.3g.uliejh.cn/nnews/0290.htm
- http://m.3g.uliejh.cn/nnews/77891.htm
- http://m.3g.uliejh.cn/nnews/103602.htm
- http://m.3g.uliejh.cn/nnews/3293540.htm
- http://m.3g.uliejh.cn/nnews/472360.htm
- http://m.3g.uliejh.cn/nnews/9511705.htm
- http://m.3g.uliejh.cn/nnews/89826.htm
- http://m.3g.uliejh.cn/nnews/5766.htm
- http://m.3g.uliejh.cn/nnews/013292.htm
- http://m.3g.uliejh.cn/nnews/5960.htm
- http://m.3g.uliejh.cn/nnews/22704.htm
- http://m.3g.uliejh.cn/nnews/284161.htm
- http://m.3g.uliejh.cn/nnews/8741037.htm
- http://m.3g.uliejh.cn/nnews/72781.htm
- http://m.3g.uliejh.cn/nnews/13881.htm
- http://m.3g.uliejh.cn/nnews/6511682.htm
- http://m.3g.uliejh.cn/nnews/89265.htm
- http://m.3g.uliejh.cn/nnews/6709.htm
- http://m.3g.uliejh.cn/nnews/879899.htm
- http://m.3g.uliejh.cn/nnews/4266097.htm
- http://m.3g.uliejh.cn/nnews/446124.htm
- http://m.3g.uliejh.cn/nnews/08080.htm
- http://m.3g.uliejh.cn/nnews/291273.htm
- http://m.3g.uliejh.cn/nnews/689150.htm
- http://m.3g.uliejh.cn/nnews/4410068.htm
- http://m.3g.uliejh.cn/nnews/0330643.htm
- http://m.3g.uliejh.cn/nnews/272676.htm
- http://m.3g.uliejh.cn/nnews/76540.htm
- http://m.3g.uliejh.cn/nnews/505112.htm
- http://m.3g.uliejh.cn/nnews/86690.htm
- http://m.3g.uliejh.cn/nnews/8927769.htm
- http://m.3g.uliejh.cn/nnews/95010.htm
- http://m.3g.uliejh.cn/nnews/7250036.htm
- http://m.3g.uliejh.cn/nnews/11365.htm
- http://m.3g.uliejh.cn/nnews/1867.htm
- http://m.3g.uliejh.cn/nnews/9640959.htm
- http://m.3g.uliejh.cn/nnews/7108640.htm
- http://m.3g.uliejh.cn/nnews/8310794.htm
- http://m.3g.uliejh.cn/nnews/47782.htm
- http://m.3g.uliejh.cn/nnews/594362.htm
- http://m.3g.uliejh.cn/nnews/60606.htm
- http://m.3g.uliejh.cn/nnews/7194721.htm
- http://m.3g.uliejh.cn/nnews/12865.htm
- http://m.3g.uliejh.cn/nnews/1487.htm
- http://m.3g.uliejh.cn/nnews/8680055.htm
- http://m.3g.uliejh.cn/nnews/3655858.htm
- http://m.3g.uliejh.cn/nnews/613785.htm
- http://m.3g.uliejh.cn/nnews/4133457.htm
- http://m.3g.uliejh.cn/nnews/541840.htm
- http://m.3g.uliejh.cn/nnews/267707.htm
- http://m.3g.uliejh.cn/nnews/0336.htm
- http://m.3g.uliejh.cn/nnews/771078.htm
- http://m.3g.uliejh.cn/nnews/4026344.htm
- http://m.3g.uliejh.cn/nnews/262013.htm
- http://m.3g.uliejh.cn/nnews/08200.htm
- http://m.3g.uliejh.cn/nnews/4036.htm
- http://m.3g.uliejh.cn/nnews/8180.htm
- http://m.3g.uliejh.cn/nnews/5848.htm
- http://m.3g.uliejh.cn/nnews/3555854.htm
- http://m.3g.uliejh.cn/nnews/86585.htm
- http://m.3g.uliejh.cn/nnews/33032.htm
- http://m.3g.uliejh.cn/nnews/0172.htm
- http://m.3g.uliejh.cn/nnews/1063.htm
- http://m.3g.uliejh.cn/nnews/07565.htm
- http://m.3g.uliejh.cn/nnews/84216.htm
- http://m.3g.uliejh.cn/nnews/3688005.htm
- http://m.3g.uliejh.cn/nnews/3658.htm
- http://m.3g.uliejh.cn/nnews/7895753.htm
- http://m.3g.uliejh.cn/nnews/378629.htm
- http://m.3g.uliejh.cn/nnews/0409566.htm
- http://m.3g.uliejh.cn/nnews/878680.htm
- http://m.3g.uliejh.cn/nnews/5191.htm
- http://m.3g.uliejh.cn/nnews/135905.htm
- http://m.3g.uliejh.cn/nnews/00840.htm
- http://m.3g.uliejh.cn/nnews/4914392.htm
- http://m.3g.uliejh.cn/nnews/2795703.htm
- http://m.3g.uliejh.cn/nnews/9766.htm
- http://m.3g.uliejh.cn/nnews/0720.htm
- http://m.3g.uliejh.cn/nnews/3288.htm
- http://m.3g.uliejh.cn/nnews/637175.htm
- http://m.3g.uliejh.cn/nnews/805514.htm
- http://m.3g.uliejh.cn/nnews/21612.htm
- http://m.3g.uliejh.cn/nnews/8117.htm
- http://m.3g.uliejh.cn/nnews/342710.htm
- http://m.3g.uliejh.cn/nnews/90785.htm
- http://m.3g.uliejh.cn/nnews/9670024.htm
- http://m.3g.uliejh.cn/nnews/0209.htm
- http://m.3g.uliejh.cn/nnews/7709637.htm
- http://m.3g.uliejh.cn/nnews/6780000.htm
- http://m.3g.uliejh.cn/nnews/612931.htm
- http://m.3g.uliejh.cn/nnews/54410.htm
- http://m.3g.uliejh.cn/nnews/7139.htm
- http://m.3g.uliejh.cn/nnews/74535.htm
- http://m.3g.uliejh.cn/nnews/6296227.htm
- http://m.3g.uliejh.cn/nnews/72819.htm
- http://m.3g.uliejh.cn/nnews/32287.htm
- http://m.3g.uliejh.cn/nnews/8624.htm
- http://m.3g.uliejh.cn/nnews/398383.htm
- http://m.3g.uliejh.cn/nnews/4673.htm
- http://m.3g.uliejh.cn/nnews/64417.htm
- http://m.3g.uliejh.cn/nnews/133571.htm
- http://m.3g.uliejh.cn/nnews/2588.htm
- http://m.3g.uliejh.cn/nnews/57229.htm
- http://m.3g.uliejh.cn/nnews/61703.htm
- http://m.3g.uliejh.cn/nnews/086766.htm
- http://m.3g.uliejh.cn/nnews/8355166.htm
- http://m.3g.uliejh.cn/nnews/818109.htm
- http://m.3g.uliejh.cn/nnews/2136.htm
- http://m.3g.uliejh.cn/nnews/6571.htm
- http://m.3g.uliejh.cn/nnews/09763.htm
- http://m.3g.uliejh.cn/nnews/5785.htm
- http://m.3g.uliejh.cn/nnews/34910.htm
- http://m.3g.uliejh.cn/nnews/5424275.htm
- http://m.3g.uliejh.cn/nnews/4798034.htm
- http://m.3g.uliejh.cn/nnews/0418.htm
- http://m.3g.uliejh.cn/nnews/07969.htm
- http://m.3g.uliejh.cn/nnews/3984.htm
- http://m.3g.uliejh.cn/nnews/4053.htm
- http://m.3g.uliejh.cn/nnews/3921.htm
- http://m.3g.uliejh.cn/nnews/934324.htm
- http://m.3g.uliejh.cn/nnews/726408.htm
- http://m.3g.uliejh.cn/nnews/3148.htm
- http://m.3g.uliejh.cn/nnews/8907232.htm
- http://m.3g.uliejh.cn/nnews/1862.htm
- http://m.3g.uliejh.cn/nnews/848990.htm
- http://m.3g.uliejh.cn/nnews/2891.htm
- http://m.3g.uliejh.cn/nnews/86576.htm
- http://m.3g.uliejh.cn/nnews/96103.htm
- http://m.3g.uliejh.cn/nnews/78949.htm
- http://m.3g.uliejh.cn/nnews/91442.htm
- http://m.3g.uliejh.cn/nnews/9357.htm
- http://m.3g.uliejh.cn/nnews/1162.htm
- http://m.3g.uliejh.cn/nnews/143752.htm
- http://m.3g.uliejh.cn/nnews/2026657.htm
- http://m.3g.uliejh.cn/nnews/898669.htm
- http://m.3g.uliejh.cn/nnews/8017897.htm
- http://m.3g.uliejh.cn/nnews/2752.htm
- http://m.3g.uliejh.cn/nnews/2537944.htm
- http://m.3g.uliejh.cn/nnews/20143.htm
- http://m.3g.uliejh.cn/nnews/52663.htm
- http://m.3g.uliejh.cn/nnews/36216.htm
- http://m.3g.uliejh.cn/nnews/291382.htm
- http://m.3g.uliejh.cn/nnews/6348706.htm
- http://m.3g.uliejh.cn/nnews/55643.htm
- http://m.3g.uliejh.cn/nnews/9663431.htm
- http://m.3g.uliejh.cn/nnews/1125361.htm
- http://m.3g.uliejh.cn/nnews/0248.htm
- http://m.3g.uliejh.cn/nnews/0382806.htm
- http://m.3g.uliejh.cn/nnews/6065.htm
- http://m.3g.uliejh.cn/nnews/1703.htm
- http://m.3g.uliejh.cn/nnews/5854083.htm
- http://m.3g.uliejh.cn/nnews/6613906.htm
- http://m.3g.uliejh.cn/nnews/9061.htm
- http://m.3g.uliejh.cn/nnews/38349.htm

## 项目结构

项目采用标准的 Python 包布局，核心模块与辅助脚本分离，便于维护与扩展。

```
linkmaster-pro/
├── linkmaster/                      # 核心 Python 包
│   ├── __init__.py                  # 包初始化，导出主要接口
│   ├── cli.py                       # 命令行入口，注册所有子命令
│   ├── importer.py                  # 导入模块：支持 TXT / CSV / JSONL 格式解析
│   ├── indexer.py                   # 索引构建器：生成倒排索引与元数据缓存
│   ├── checker.py                   # 链接检测器：异步 HTTP 可达性验证
│   ├── exporter.py                  # 导出模块：生成 HTML / JSON / Markdown 格式输出
│   └── models.py                    # 数据模型定义：LinkRecord, BatchMeta, IndexEntry
├── config/                          # 配置目录
│   ├── default.yaml                 # 默认配置：并发数、超时阈值、输出路径
│   └── schema.json                  # 配置字段的 JSON Schema 校验文件
├── data/                            # 数据存储目录（默认）
│   ├── batches/                     # 按批次存储原始链接文件
│   │   └── batch_29.txt             # 当前批次原始数据
│   ├── index/                       # 生成的索引文件
│   │   ├── inverted_index.json      # 倒排索引主文件
│   │   └── metadata.db              # SQLite 元数据库（可选）
│   └── reports/                     # 检测报告输出目录
│       └── availability_20260824.log
├── tests/                           # 单元测试与集成测试
│   ├── test_importer.py             # 导入模块测试用例
│   ├── test_indexer.py              # 索引构建测试用例
│   └── fixtures/                    # 测试用固定样本数据
│       └── sample_links.txt
├── docs/                            # 文档源码
│   ├── getting-started.md
│   ├── commands.md
│   ├── indexing.md
│   └── batch-management.md
├── scripts/                         # 辅助运维脚本
│   ├── cron_check.sh                # 定时链接检测脚本（cron 调度）
│   └── migrate_v1_to_v2.py          # 版本升级数据迁移脚本
├── requirements.txt                 # 生产环境依赖列表
├── requirements-dev.txt             # 开发环境额外依赖（测试、代码检查）
├── setup.py                         # 打包与分发配置
├── README.md                        # 项目说明文档
└── LICENSE                          # MIT 许可证文件
```

## 贡献指南

我们欢迎并鼓励社区贡献，无论是报告问题、改进文档还是提交代码。请遵循以下步骤参与项目开发。

1. 查阅问题追踪器：访问 GitHub Issues 页面，查找未被认领的 bug 或功能请求。对于新需求，请先创建 Issue 进行讨论，避免重复工作。

2. 派生项目仓库：将主仓库 Fork 至个人账户，并克隆至本地开发环境。确保本地 Git 配置了正确的用户信息。

3. 创建功能分支：从 main 分支切出新的分支，分支命名建议采用 `feature/简短描述` 或 `fix/问题编号` 格式。

4. 编写测试与代码：所有新增功能必须包含对应的单元测试，测试覆盖率不低于 80%。代码风格需遵循 PEP 8 规范，并使用 pylint 进行静态检查。

5. 提交拉取请求：推送分支至远程仓库后，向主仓库的 main 分支提交 PR。PR 描述中请清晰说明变更内容、影响范围及测试结果，等待维护者评审。

## 常见问题

Q：导入链接时提示“批次编号冲突”，应如何解决？

A：LinkMaster Pro 默认每个批次编号唯一。若出现冲突，表示 data/batches/ 目录下已存在同名批次文件。解决方案有两种：一是使用 `--batch` 参数指定新的未使用编号；二是使用 `--force` 选项覆盖已有批次文件，但请注意此操作会丢弃原批次数据。

Q：链接检测模块返回大量超时错误，是否代表所有链接均不可用？

A：不一定。超时错误可能受网络环境、目标服务器限流或 DNS 解析延迟影响。建议首先调整配置中的 `check_timeout` 参数（默认 5 秒）和 `concurrency` 并发数（默认 10），以适配不同网络条件。同时检查是否处于代理或 VPN 环境中，可能需要设置 HTTP_PROXY 环境变量。

Q：如何将索引数据迁移至另一台机器？

A：索引数据全部存储在 data/index/ 目录下。你只需将整个 data/ 目录复制到目标机器的相同相对路径，或通过配置修改 `data_dir` 指向新位置。迁移后运行 `linkmaster rebuild` 命令重新校验索引完整性即可。

## 许可证

MIT

> 外链数量: 250 | 生成时间: 2026-08-24 23:40:21
