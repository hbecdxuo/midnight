# WebIndex 聚合导航系统

WebIndex 是一个面向技术研究人员与信息分析人员的轻量级外链聚合与导航系统。该项目定位于将分散于各类信息源的动态页面、公告文档与参考材料统一归档，并通过可维护的索引结构提供快速访问入口。WebIndex 不依赖外部数据库，所有资源以静态超链接形式组织，适用于个人知识库构建、团队共享书签库或自动化信息采集链路的前置导航层。

目标用户包括运维工程师、渗透测试人员、威胁情报分析师、数据采集工程师以及需要频繁查阅分散参考资料的技术决策者。WebIndex 通过提供稳定的超链接索引表，有效降低信息遗失风险，并提升多源资料的并行查阅效率。

## 功能概览

- 静态超链接索引管理：所有外链以纯文本形式维护于版本控制系统中，支持增删改查的完整变更追踪。

- 多层级目录分类：资源按项目批次与主题领域划分至独立子目录，便于按场景筛选。

- 原始来源标记：每条链接保留原始发布域与路径结构，便于追溯信息源头。

- 自动化链接存活检测：集成周期性 HEAD 请求检查，对失效链接输出告警日志。

- 快速全文检索：基于文件名与注释字段的轻量级 grep 检索，支持正则表达式过滤。

- 批量导入导出：支持按行分隔的 URL 列表批量追加，与主流书签管理工具格式兼容。

- 访问统计看板：基于访问日志聚合热点链接点击频次，辅助判断高价值资源。

## 应用场景

1. 安全研究人员的漏洞公告聚合
   安全团队可将多个漏洞披露平台、厂商安全公告页面的历史链接统一收录至 WebIndex，按月分批次归档。当需要回溯某漏洞的原始通告时，通过索引条目快速定位，无需重复搜索。

2. 数据采集任务的入口管理
   数据采集工程师在面对数十个不同数据源的接口文档、样例页面和变更日志时，使用 WebIndex 维护一份稳定的入口清单。当数据源域名或路径发生迁移时，只需更新索引中的单条记录，下游采集脚本统一引用索引变量。

3. 技术文档撰写的外部参考整理
   开源项目文档撰写者可将所有引用的外部规范、RFC 文档、参考实现的源码仓库地址汇总至 WebIndex。在文档更新周期内，索引文件可作为独立的参考附录发布，保证引用链路的可验证性。

4. 团队共享知识库的书签中心
   技术团队可将内部常用的运维控制台、监控面板、日志查询入口、代码仓库、CI/CD 流水线地址统一收录。新成员入职时通过 WebIndex 即可获取全部必要外部入口，减少交接遗漏。

5. 历史归档资料的导航恢复
   对于长期运行的业务系统，历史版本的依赖库镜像、旧版 API 文档、下线服务的快照地址可通过 WebIndex 保留索引。即使原始服务已不可达，索引记录仍可作为迁移计划的参考依据。

## 快速开始

以下操作步骤适用于 Linux / macOS / Windows WSL 环境。请确保系统已安装 Git 与 Python 3.8 以上版本。

```bash
# 克隆仓库
git clone https://github.com/webindex/webindex.git
cd webindex

# 安装依赖（使用 pip 安装虚拟环境及必要工具包）
python3 -m venv venv
source venv/bin/activate
pip install --upgrade pip
pip install -r requirements.txt

# 运行本地预览服务（默认监听 127.0.0.1:8080）
python3 server.py --port 8080
```

执行完成后，使用浏览器访问 http://127.0.0.1:8080 即可查看当前索引主页。如需导入用户提供的 URL 批次数据，将原始列表保存为 data/batch_14.txt 后执行：

```bash
python3 import.py --batch 14 --source data/batch_14.txt
```

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|---|---|---|
| Python | 3.8 及以上 | 运行核心服务与工具脚本的解释器 |
| Git | 2.20 及以上 | 克隆仓库及版本管理 |
| pip | 20.0 及以上 | Python 包依赖管理工具 |
| Flask | 2.0.x | 可选，用于提供 Web 界面预览服务 |
| requests | 2.25.x | 用于链接存活检测与 HTTP 状态检查 |
| pytest | 6.0 及以上 | 仅开发测试环境需要，用于单元测试 |
| gunicorn | 20.0.x | 生产环境推荐部署的 WSGI 服务器 |
| virtualenv | 16.0 及以上 | 创建独立 Python 运行环境 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|---|---|---|
| 用户手册 | docs/user_guide.md | 如何导入新批次链接、如何进行检索、如何自定义分类标签 |
| 运维指南 | docs/ops_guide.md | 如何部署至生产服务器、如何配置日志轮转、如何设置存活检测周期 |
| 开发参考 | docs/dev_reference.md | 索引文件格式规范、插件接口定义、新增解析器的开发流程 |
| 常见问题 | docs/faq.md | 链接失效如何处理、索引文件编码问题、批量去重策略 |
| 版本记录 | CHANGELOG.md | 每个版本的更新内容、已修复缺陷、不兼容变更说明 |

## 资源列表

- http://m.3g.uliejh.cn/nnews/817407.htm
- http://m.3g.uliejh.cn/nnews/534020.htm
- http://m.3g.uliejh.cn/nnews/9193855.htm
- http://m.3g.uliejh.cn/nnews/572508.htm
- http://m.3g.uliejh.cn/nnews/937030.htm
- http://m.3g.uliejh.cn/nnews/30740.htm
- http://m.3g.uliejh.cn/nnews/0227400.htm
- http://m.3g.uliejh.cn/nnews/6983946.htm
- http://m.3g.uliejh.cn/nnews/932757.htm
- http://m.3g.uliejh.cn/nnews/4367020.htm
- http://m.3g.uliejh.cn/nnews/42625.htm
- http://m.3g.uliejh.cn/nnews/7567079.htm
- http://m.3g.uliejh.cn/nnews/4944661.htm
- http://m.3g.uliejh.cn/nnews/0151579.htm
- http://m.3g.uliejh.cn/nnews/6988172.htm
- http://m.3g.uliejh.cn/nnews/6181466.htm
- http://m.3g.uliejh.cn/nnews/23499.htm
- http://m.3g.uliejh.cn/nnews/7504.htm
- http://m.3g.uliejh.cn/nnews/58799.htm
- http://m.3g.uliejh.cn/nnews/64667.htm
- http://m.3g.uliejh.cn/nnews/52463.htm
- http://m.3g.uliejh.cn/nnews/745702.htm
- http://m.3g.uliejh.cn/nnews/6447.htm
- http://m.3g.uliejh.cn/nnews/592503.htm
- http://m.3g.uliejh.cn/nnews/4126013.htm
- http://m.3g.uliejh.cn/nnews/561536.htm
- http://m.3g.uliejh.cn/nnews/9488252.htm
- http://m.3g.uliejh.cn/nnews/6107840.htm
- http://m.3g.uliejh.cn/nnews/9594.htm
- http://m.3g.uliejh.cn/nnews/163144.htm
- http://m.3g.uliejh.cn/nnews/3637.htm
- http://m.3g.uliejh.cn/nnews/49196.htm
- http://m.3g.uliejh.cn/nnews/41065.htm
- http://m.3g.uliejh.cn/nnews/893162.htm
- http://m.3g.uliejh.cn/nnews/70100.htm
- http://m.3g.uliejh.cn/nnews/4476714.htm
- http://m.3g.uliejh.cn/nnews/090008.htm
- http://m.3g.uliejh.cn/nnews/34698.htm
- http://m.3g.uliejh.cn/nnews/902400.htm
- http://m.3g.uliejh.cn/nnews/50262.htm
- http://m.3g.uliejh.cn/nnews/5677864.htm
- http://m.3g.uliejh.cn/nnews/913166.htm
- http://m.3g.uliejh.cn/nnews/2265611.htm
- http://m.3g.uliejh.cn/nnews/363140.htm
- http://m.3g.uliejh.cn/nnews/370403.htm
- http://m.3g.uliejh.cn/nnews/2394655.htm
- http://m.3g.uliejh.cn/nnews/083865.htm
- http://m.3g.uliejh.cn/nnews/58099.htm
- http://m.3g.uliejh.cn/nnews/8222267.htm
- http://m.3g.uliejh.cn/nnews/37496.htm
- http://m.3g.uliejh.cn/nnews/76263.htm
- http://m.3g.uliejh.cn/nnews/112196.htm
- http://m.3g.uliejh.cn/nnews/558910.htm
- http://m.3g.uliejh.cn/nnews/18812.htm
- http://m.3g.uliejh.cn/nnews/280904.htm
- http://m.3g.uliejh.cn/nnews/93310.htm
- http://m.3g.uliejh.cn/nnews/2518.htm
- http://m.3g.uliejh.cn/nnews/776172.htm
- http://m.3g.uliejh.cn/nnews/8830959.htm
- http://m.3g.uliejh.cn/nnews/126771.htm
- http://m.3g.uliejh.cn/nnews/8294.htm
- http://m.3g.uliejh.cn/nnews/96835.htm
- http://m.3g.uliejh.cn/nnews/667728.htm
- http://m.3g.uliejh.cn/nnews/2828.htm
- http://m.3g.uliejh.cn/nnews/48994.htm
- http://m.3g.uliejh.cn/nnews/3352589.htm
- http://m.3g.uliejh.cn/nnews/6249977.htm
- http://m.3g.uliejh.cn/nnews/449623.htm
- http://m.3g.uliejh.cn/nnews/4876553.htm
- http://m.3g.uliejh.cn/nnews/93402.htm
- http://m.3g.uliejh.cn/nnews/4787.htm
- http://m.3g.uliejh.cn/nnews/08325.htm
- http://m.3g.uliejh.cn/nnews/7325.htm
- http://m.3g.uliejh.cn/nnews/70340.htm
- http://m.3g.uliejh.cn/nnews/548126.htm
- http://m.3g.uliejh.cn/nnews/06593.htm
- http://m.3g.uliejh.cn/nnews/6566.htm
- http://m.3g.uliejh.cn/nnews/1127199.htm
- http://m.3g.uliejh.cn/nnews/4113.htm
- http://m.3g.uliejh.cn/nnews/621279.htm
- http://m.3g.uliejh.cn/nnews/0267.htm
- http://m.3g.uliejh.cn/nnews/88327.htm
- http://m.3g.uliejh.cn/nnews/93044.htm
- http://m.3g.uliejh.cn/nnews/003574.htm
- http://m.3g.uliejh.cn/nnews/5238561.htm
- http://m.3g.uliejh.cn/nnews/7388672.htm
- http://m.3g.uliejh.cn/nnews/438105.htm
- http://m.3g.uliejh.cn/nnews/6555.htm
- http://m.3g.uliejh.cn/nnews/00630.htm
- http://m.3g.uliejh.cn/nnews/774157.htm
- http://m.3g.uliejh.cn/nnews/0093492.htm
- http://m.3g.uliejh.cn/nnews/1232.htm
- http://m.3g.uliejh.cn/nnews/6170124.htm
- http://m.3g.uliejh.cn/nnews/7995.htm
- http://m.3g.uliejh.cn/nnews/4247.htm
- http://m.3g.uliejh.cn/nnews/75957.htm
- http://m.3g.uliejh.cn/nnews/501414.htm
- http://m.3g.uliejh.cn/nnews/422388.htm
- http://m.3g.uliejh.cn/nnews/5961508.htm
- http://m.3g.uliejh.cn/nnews/204381.htm
- http://m.3g.uliejh.cn/nnews/2464468.htm
- http://m.3g.uliejh.cn/nnews/843458.htm
- http://m.3g.uliejh.cn/nnews/2817.htm
- http://m.3g.uliejh.cn/nnews/4282271.htm
- http://m.3g.uliejh.cn/nnews/825363.htm
- http://m.3g.uliejh.cn/nnews/389627.htm
- http://m.3g.uliejh.cn/nnews/5057765.htm
- http://m.3g.uliejh.cn/nnews/04197.htm
- http://m.3g.uliejh.cn/nnews/8713.htm
- http://m.3g.uliejh.cn/nnews/230457.htm
- http://m.3g.uliejh.cn/nnews/686393.htm
- http://m.3g.uliejh.cn/nnews/272553.htm
- http://m.3g.uliejh.cn/nnews/4093.htm
- http://m.3g.uliejh.cn/nnews/8047.htm
- http://m.3g.uliejh.cn/nnews/714733.htm
- http://m.3g.uliejh.cn/nnews/36254.htm
- http://m.3g.uliejh.cn/nnews/0467247.htm
- http://m.3g.uliejh.cn/nnews/3626.htm
- http://m.3g.uliejh.cn/nnews/6001.htm
- http://m.3g.uliejh.cn/nnews/414780.htm
- http://m.3g.uliejh.cn/nnews/3256.htm
- http://m.3g.uliejh.cn/nnews/4828062.htm
- http://m.3g.uliejh.cn/nnews/1300.htm
- http://m.3g.uliejh.cn/nnews/7188.htm
- http://m.3g.uliejh.cn/nnews/78522.htm
- http://m.3g.uliejh.cn/nnews/6569274.htm
- http://m.3g.uliejh.cn/nnews/938005.htm
- http://m.3g.uliejh.cn/nnews/3873103.htm
- http://m.3g.uliejh.cn/nnews/7230770.htm
- http://m.3g.uliejh.cn/nnews/1785.htm
- http://m.3g.uliejh.cn/nnews/2018.htm
- http://m.3g.uliejh.cn/nnews/7154.htm
- http://m.3g.uliejh.cn/nnews/383290.htm
- http://m.3g.uliejh.cn/nnews/2386.htm
- http://m.3g.uliejh.cn/nnews/55266.htm
- http://m.3g.uliejh.cn/nnews/2359092.htm
- http://m.3g.uliejh.cn/nnews/696307.htm
- http://m.3g.uliejh.cn/nnews/431112.htm
- http://m.3g.uliejh.cn/nnews/187402.htm
- http://m.3g.uliejh.cn/nnews/6429919.htm
- http://m.3g.uliejh.cn/nnews/304436.htm
- http://m.3g.uliejh.cn/nnews/0673.htm
- http://m.3g.uliejh.cn/nnews/1086956.htm
- http://m.3g.uliejh.cn/nnews/662190.htm
- http://m.3g.uliejh.cn/nnews/33663.htm
- http://m.3g.uliejh.cn/nnews/4009419.htm
- http://m.3g.uliejh.cn/nnews/64313.htm
- http://m.3g.uliejh.cn/nnews/283100.htm
- http://m.3g.uliejh.cn/nnews/859207.htm
- http://m.3g.uliejh.cn/nnews/162925.htm
- http://m.3g.uliejh.cn/nnews/72328.htm
- http://m.3g.uliejh.cn/nnews/65487.htm
- http://m.3g.uliejh.cn/nnews/94297.htm
- http://m.3g.uliejh.cn/nnews/40902.htm
- http://m.3g.uliejh.cn/nnews/853912.htm
- http://m.3g.uliejh.cn/nnews/6540.htm
- http://m.3g.uliejh.cn/nnews/87569.htm
- http://m.3g.uliejh.cn/nnews/40134.htm
- http://m.3g.uliejh.cn/nnews/891147.htm
- http://m.3g.uliejh.cn/nnews/5314110.htm
- http://m.3g.uliejh.cn/nnews/5732.htm
- http://m.3g.uliejh.cn/nnews/11016.htm
- http://m.3g.uliejh.cn/nnews/8928164.htm
- http://m.3g.uliejh.cn/nnews/71438.htm
- http://m.3g.uliejh.cn/nnews/9889.htm
- http://m.3g.uliejh.cn/nnews/2634.htm
- http://m.3g.uliejh.cn/nnews/2800979.htm
- http://m.3g.uliejh.cn/nnews/789649.htm
- http://m.3g.uliejh.cn/nnews/204324.htm
- http://m.3g.uliejh.cn/nnews/434967.htm
- http://m.3g.uliejh.cn/nnews/630029.htm
- http://m.3g.uliejh.cn/nnews/91427.htm
- http://m.3g.uliejh.cn/nnews/599861.htm
- http://m.3g.uliejh.cn/nnews/84393.htm
- http://m.3g.uliejh.cn/nnews/1439374.htm
- http://m.3g.uliejh.cn/nnews/4982525.htm
- http://m.3g.uliejh.cn/nnews/98248.htm
- http://m.3g.uliejh.cn/nnews/455076.htm
- http://m.3g.uliejh.cn/nnews/9703915.htm
- http://m.3g.uliejh.cn/nnews/2660.htm
- http://m.3g.uliejh.cn/nnews/0611.htm
- http://m.3g.uliejh.cn/nnews/341452.htm
- http://m.3g.uliejh.cn/nnews/6767.htm
- http://m.3g.uliejh.cn/nnews/7250214.htm
- http://m.3g.uliejh.cn/nnews/753203.htm
- http://m.3g.uliejh.cn/nnews/00723.htm
- http://m.3g.uliejh.cn/nnews/6539000.htm
- http://m.3g.uliejh.cn/nnews/0027235.htm
- http://m.3g.uliejh.cn/nnews/59891.htm
- http://m.3g.uliejh.cn/nnews/9738201.htm
- http://m.3g.uliejh.cn/nnews/5503.htm
- http://m.3g.uliejh.cn/nnews/992997.htm
- http://m.3g.uliejh.cn/nnews/032119.htm
- http://m.3g.uliejh.cn/nnews/71359.htm
- http://m.3g.uliejh.cn/nnews/65425.htm
- http://m.3g.uliejh.cn/nnews/59533.htm
- http://m.3g.uliejh.cn/nnews/6459.htm
- http://m.3g.uliejh.cn/nnews/5275188.htm
- http://m.3g.uliejh.cn/nnews/015680.htm
- http://m.3g.uliejh.cn/nnews/430893.htm
- http://m.3g.uliejh.cn/nnews/6604561.htm
- http://m.3g.uliejh.cn/nnews/063378.htm
- http://m.3g.uliejh.cn/nnews/68714.htm
- http://m.3g.uliejh.cn/nnews/859709.htm
- http://m.3g.uliejh.cn/nnews/30940.htm
- http://m.3g.uliejh.cn/nnews/799997.htm
- http://m.3g.uliejh.cn/nnews/7573.htm
- http://m.3g.uliejh.cn/nnews/8156792.htm
- http://m.3g.uliejh.cn/nnews/795659.htm
- http://m.3g.uliejh.cn/nnews/5590.htm
- http://m.3g.uliejh.cn/nnews/3537.htm
- http://m.3g.uliejh.cn/nnews/3299942.htm
- http://m.3g.uliejh.cn/nnews/4767.htm
- http://m.3g.uliejh.cn/nnews/35221.htm
- http://m.3g.uliejh.cn/nnews/331837.htm
- http://m.3g.uliejh.cn/nnews/9060077.htm
- http://m.3g.uliejh.cn/nnews/1087018.htm
- http://m.3g.uliejh.cn/nnews/3124824.htm
- http://m.3g.uliejh.cn/nnews/6933.htm
- http://m.3g.uliejh.cn/nnews/706329.htm
- http://m.3g.uliejh.cn/nnews/508823.htm
- http://m.3g.uliejh.cn/nnews/3865.htm
- http://m.3g.uliejh.cn/nnews/31811.htm
- http://m.3g.uliejh.cn/nnews/4160764.htm
- http://m.3g.uliejh.cn/nnews/4207.htm
- http://m.3g.uliejh.cn/nnews/4011310.htm
- http://m.3g.uliejh.cn/nnews/37818.htm
- http://m.3g.uliejh.cn/nnews/22421.htm
- http://m.3g.uliejh.cn/nnews/230128.htm
- http://m.3g.uliejh.cn/nnews/562895.htm
- http://m.3g.uliejh.cn/nnews/91280.htm
- http://m.3g.uliejh.cn/nnews/058832.htm
- http://m.3g.uliejh.cn/nnews/717470.htm
- http://m.3g.uliejh.cn/nnews/7232.htm
- http://m.3g.uliejh.cn/nnews/085833.htm
- http://m.3g.uliejh.cn/nnews/73512.htm
- http://m.3g.uliejh.cn/nnews/87133.htm
- http://m.3g.uliejh.cn/nnews/096854.htm
- http://m.3g.uliejh.cn/nnews/2034787.htm
- http://m.3g.uliejh.cn/nnews/0832707.htm
- http://m.3g.uliejh.cn/nnews/506997.htm
- http://m.3g.uliejh.cn/nnews/3015.htm
- http://m.3g.uliejh.cn/nnews/838596.htm
- http://m.3g.uliejh.cn/nnews/53671.htm
- http://m.3g.uliejh.cn/nnews/1836163.htm
- http://m.3g.uliejh.cn/nnews/04978.htm
- http://m.3g.uliejh.cn/nnews/1093300.htm
- http://m.3g.uliejh.cn/nnews/486592.htm
- http://m.3g.uliejh.cn/nnews/38644.htm
- http://m.3g.uliejh.cn/nnews/6853.htm

## 项目结构

```
webindex/
├── data/                               # 数据目录，存放所有批次索引文件
│   ├── batches/                        # 按批次拆分的原始 URL 列表
│   │   ├── batch_001.txt               # 第1批资源，已归档
│   │   ├── batch_002.txt               # 第2批资源，已归档
│   │   └── batch_014.txt               # 第14批资源，当前导入批次
│   ├── categories/                     # 分类映射表，将 URL 映射至主题领域
│   │   ├── security.txt                # 安全相关资源分类
│   │   ├── development.txt             # 开发工具与框架分类
│   │   └── operations.txt              # 运维与监控分类
│   └── metadata/                       # 元数据记录，含导入时间与来源备注
│       ├── import_log.json             # 导入操作审计日志
│       └── source_mapping.csv          # URL 与原始来源的对照表
├── src/                                # 源代码目录
│   ├── core/                           # 核心模块
│   │   ├── indexer.py                  # 索引构建与更新引擎
│   │   ├── checker.py                  # 链接存活检测线程池实现
│   │   └── parser.py                   # 多种格式 URL 列表解析器
│   ├── web/                            # Web 服务模块
│   │   ├── app.py                      # Flask 应用入口与路由定义
│   │   ├── templates/                  # Jinja2 模板文件
│   │   │   ├── index.html              # 首页导航模板
│   │   │   └── batch.html              # 单批次详情页模板
│   │   └── static/                     # 静态资源（CSS / JS）
│   │       ├── style.css               # 基础样式表
│   │       └── filter.js               # 前端检索过滤脚本
│   └── cli/                            # 命令行工具集
│       ├── import.py                   # 批量导入命令行入口
│       ├── export.py                   # 导出为 JSON / CSV 格式
│       └── health.py                   # 健康检查与失效链接报告生成
├── tests/                              # 单元测试与集成测试
│   ├── test_indexer.py                 # 索引引擎单元测试
│   ├── test_checker.py                 # 存活检测模块测试
│   └── fixtures/                       # 测试用固定数据集
│       └── sample_batch.txt            # 样例批次文件
├── docs/                               # 完整文档目录（参见文档导航章节）
│   ├── user_guide.md
│   ├── ops_guide.md
│   ├── dev_reference.md
│   └── faq.md
├── requirements.txt                    # Python 运行时依赖列表
├── server.py                           # 生产级 WSGI 启动脚本
├── CHANGELOG.md                        # 版本变更日志
└── README.md                           # 项目说明文件（本文件）
```

## 贡献指南

1. 复刻主仓库并创建功能分支
   访问 GitHub 仓库页面，点击 Fork 按钮将项目复制至个人账户。随后在本地克隆复刻版本，并基于 main 分支创建新的功能分支，分支命名采用 feature/xxx 或 fix/xxx 格式。

2. 新增批次数据或改进现有模块
   若新增资源批次，将 URL 列表放置于 data/batches/ 目录下，按 batch_xxx.txt 格式命名。若修改核心解析逻辑，需同步更新对应的单元测试用例至 tests/ 目录，确保测试覆盖率达到 80% 以上。

3. 提交变更并编写规范的提交信息
   提交信息需遵循 Conventional Commits 规范，格式为 type(scope): description。例如 feat(parser): add support for tab-separated batch files。提交前运行本地测试套件确保无回归缺陷。

4. 发起拉取请求并参与代码评审
   将功能分支推送至远程复刻仓库，随后向主仓库的 main 分支发起拉取请求。请求描述中需明确说明变更目的、影响范围及测试结果。评审通过后由项目维护者合并。

5. 文档同步更新
   凡涉及用户可见功能变更或配置项调整，需同步更新 docs/ 目录下对应的手册文件。新增配置项需在 ops_guide.md 中补充说明，新增命令行参数需在 user_guide.md 中体现。

## 常见问题

问：导入批次时出现编码错误，提示 UnicodeDecodeError，如何解决？

答：请确保批次文件使用 UTF-8 编码保存。若文件来源于 Windows 系统，可能带有 BOM 头或使用 GBK 编码。可使用以下命令进行转换：iconv -f GBK -t UTF-8 batch_014.txt > batch_014_utf8.txt，随后重新执行导入命令。

问：链接存活检测报告显示大量超时，是否表示所有链接均失效？

答：超时并不等同于链接失效。部分目标服务器可能对 HEAD 请求限制或存在防火墙规则。建议在 checker.py 配置中调整超时阈值（默认 5 秒）至 15 秒，并启用 TCP 重试机制。同时可配置代理参数以绕过网络限制。

问：如何对已导入的批次进行去重，避免同一 URL 多次收录？

答：系统提供了内置的去重工具，可通过 cli/dedup.py 执行。该工具会读取所有批次文件，构建 URL 哈希集合，输出重复项报告。对于重复记录，建议保留最早批次的条目，从新批次中手动移除重复行。

问：Web 界面无法加载任何链接，显示空白页面，可能是什么原因？

答：首先检查 data/ 目录下是否存在至少一个批次文件（如 batch_001.txt）。其次确认 server.py 运行用户对 data/ 目录具有读取权限。若使用反向代理部署，需检查代理配置是否正确传递了 X-Real-IP 头。最后查看 logs/ 目录下的错误日志获取详细堆栈信息。

## 许可证

MIT

> 外链数量: 250 | 生成时间: 2026-08-24 23:40:21
