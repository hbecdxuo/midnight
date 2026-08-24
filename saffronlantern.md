# WebLink Navigator

WebLink Navigator 是一个面向技术调研、内容聚合与批量外链管理的开源工具集，专注于对以 m.wap.uliejh.cn 为代表的内容源进行结构化采集、分类存储与快速检索。本项目并非简单的链接收藏夹，而是一套包含抓取调度、内容解析、去重索引和前端展示的轻量级外链中台系统，适合需要定期跟进大量动态资讯的研发团队、数据分析师与独立站长。

本项目定位为技术资源外链汇总站，核心目标用户包括：需要进行竞品内容监控的产品经理、维护行业资讯聚合页的运营人员、以及希望批量获取 URL 数据集用于 NLP 或 SEO 实验的开发者。通过将分散的链接纳入统一的元数据管理体系，WebLink Navigator 帮助用户从“被动保存链接”升级为“主动管理知识资产”。

## 功能概览

批量链接导入与自动去重：支持通过文本文件、CSV 或直接粘贴的方式一次性导入数百个 URL，系统自动基于链接特征与来源域名计算唯一指纹，避免重复入库。

多维度标签分类：每个链接可关联多个自定义标签，内置“技术文档”“行业报告”“视频教程”“官方公告”“博客观点”五类基础标签，并支持用户新增层级标签。

定时健康检查：后台守护进程每 24 小时对所有链接进行可达性探测，自动标记失效链接（HTTP 状态码 4xx/5xx），并生成可用率趋势报表。

全文元数据提取：对每个 URL 自动抓取页面标题、meta description、发布时间、正文前 200 字符摘要，存入结构化字段，支持后续高级筛选。

高级筛选与全文检索：基于 SQLite FTS5 或 Elasticsearch 可选后端，支持对标题、摘要、标签、来源域名的复合条件查询，搜索结果可按时间、相关性或点击热度排序。

自定义列表导出：支持将筛选后的链接列表导出为 Markdown 表格、JSON API 格式或纯文本清单，便于嵌入其他文档或系统。

单页快照存档：对重要链接可手动触发 HTML 快照保存，保留页面原始布局与样式，防止内容下架或改版导致信息丢失。

## 应用场景

技术团队内部知识库维护：团队可将日常阅读的技术博客、开源项目发布页、架构设计文档通过 WebLink Navigator 统一入库，并分配“后端”“前端”“DevOps”等标签，新成员入职时可快速获取按主题整理的学习路径。

行业动态日报自动生成：运营人员配置基于标签的定时任务，系统每日早晨 8 点自动筛选前 24 小时内新增的“行业报告”与“官方公告”类链接，生成摘要日报并发送至企业微信群或邮件列表。

SEO 外链效果监控：站长将自有站点在不同平台发布的外部引用链接导入系统，通过健康检查模块每周监控外链存活率，及时发现被删除或 nofollow 变化的链接，便于调整推广策略。

数据采集管道测试集构建：数据工程师将 m.wap.uliejh.cn 等来源的数百个 URL 作为种子，结合本项目的元数据导出功能，快速生成用于爬虫解析模板测试的样本集，显著提升测试覆盖率。

## 快速开始

以下步骤适用于 Linux / macOS 系统，Windows 用户建议通过 WSL2 或 Git Bash 执行。

```bash
# 1. 克隆项目仓库
git clone https://github.com/your-org/weblink-navigator.git
cd weblink-navigator

# 2. 安装 Python 依赖（推荐使用虚拟环境）
python3 -m venv venv
source venv/bin/activate
pip install --upgrade pip
pip install -r requirements.txt

# 3. 初始化数据库与配置
cp config/env.example .env
python manage.py init_db
python manage.py load_tags --builtin

# 4. 导入示例链接列表（包含本项目批次链接）
python manage.py import --file sample_links.csv --tag "batch43"

# 5. 启动开发服务器
python manage.py runserver --host 0.0.0.0 --port 8080
```

访问 http://localhost:8080 即可进入 Web 管理界面。生产环境部署请参考 `docs/deployment.md`。

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|---|---|---|
| Python | 3.9 ~ 3.11 | 核心运行环境，3.12 暂未完全兼容 |
| SQLite | 3.35+ | 内置数据库，支持 FTS5 全文检索扩展 |
| Redis | 6.0+ | 可选，用于缓存与任务队列（生产环境推荐） |
| Node.js | 16.0+ | 仅用于前端资产构建，后端运行可不安装 |
| Nginx | 1.18+ | 生产环境反向代理与静态资源服务 |
| Supervisor | 4.2+ | 用于守护 Celery 工作进程与健康检查调度器 |
| git | 2.25+ | 版本管理与自动更新脚本依赖 |
| curl / wget | 任意现代版本 | 健康检查模块底层探测工具 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|---|---|---|
| 入门指南 | docs/quickstart.md | 如何 5 分钟内跑起服务并导入第一批链接？ |
| 运维手册 | docs/operations.md | 如何配置定时健康检查、备份数据库、迁移服务器？ |
| API 参考 | docs/api_reference.md | 如何通过 RESTful API 批量增删改查链接及标签？ |
| 自定义开发 | docs/development.md | 如何新增一个内容解析器或替换全文检索引擎？ |

## 资源列表

- http://m.wap.uliejh.cn/bnews/71625.htm
- http://m.wap.uliejh.cn/bnews/1197484.htm
- http://m.wap.uliejh.cn/bnews/9187205.htm
- http://m.wap.uliejh.cn/bnews/084410.htm
- http://m.wap.uliejh.cn/bnews/2268651.htm
- http://m.wap.uliejh.cn/bnews/829636.htm
- http://m.wap.uliejh.cn/bnews/8666860.htm
- http://m.wap.uliejh.cn/bnews/909905.htm
- http://m.wap.uliejh.cn/bnews/81770.htm
- http://m.wap.uliejh.cn/bnews/91714.htm
- http://m.wap.uliejh.cn/bnews/5479.htm
- http://m.wap.uliejh.cn/bnews/7050.htm
- http://m.wap.uliejh.cn/bnews/1493388.htm
- http://m.wap.uliejh.cn/bnews/186836.htm
- http://m.wap.uliejh.cn/bnews/07284.htm
- http://m.wap.uliejh.cn/bnews/5357.htm
- http://m.wap.uliejh.cn/bnews/9079.htm
- http://m.wap.uliejh.cn/bnews/4036653.htm
- http://m.wap.uliejh.cn/bnews/767453.htm
- http://m.wap.uliejh.cn/bnews/537875.htm
- http://m.wap.uliejh.cn/bnews/314597.htm
- http://m.wap.uliejh.cn/bnews/09656.htm
- http://m.wap.uliejh.cn/bnews/375425.htm
- http://m.wap.uliejh.cn/bnews/611447.htm
- http://m.wap.uliejh.cn/bnews/38858.htm
- http://m.wap.uliejh.cn/bnews/2232.htm
- http://m.wap.uliejh.cn/bnews/2853430.htm
- http://m.wap.uliejh.cn/bnews/2293140.htm
- http://m.wap.uliejh.cn/bnews/4945.htm
- http://m.wap.uliejh.cn/bnews/114796.htm
- http://m.wap.uliejh.cn/bnews/9525.htm
- http://m.wap.uliejh.cn/bnews/805314.htm
- http://m.wap.uliejh.cn/bnews/49702.htm
- http://m.wap.uliejh.cn/bnews/35607.htm
- http://m.wap.uliejh.cn/bnews/4770209.htm
- http://m.wap.uliejh.cn/bnews/1788326.htm
- http://m.wap.uliejh.cn/bnews/0888.htm
- http://m.wap.uliejh.cn/bnews/5812.htm
- http://m.wap.uliejh.cn/bnews/8935386.htm
- http://m.wap.uliejh.cn/bnews/916206.htm
- http://m.wap.uliejh.cn/bnews/8396.htm
- http://m.wap.uliejh.cn/bnews/1541270.htm
- http://m.wap.uliejh.cn/bnews/292236.htm
- http://m.wap.uliejh.cn/bnews/854873.htm
- http://m.wap.uliejh.cn/bnews/0052.htm
- http://m.wap.uliejh.cn/bnews/768050.htm
- http://m.wap.uliejh.cn/bnews/8066.htm
- http://m.wap.uliejh.cn/bnews/0122301.htm
- http://m.wap.uliejh.cn/bnews/3299.htm
- http://m.wap.uliejh.cn/bnews/0381.htm
- http://m.wap.uliejh.cn/bnews/75415.htm
- http://m.wap.uliejh.cn/bnews/0123.htm
- http://m.wap.uliejh.cn/bnews/8094.htm
- http://m.wap.uliejh.cn/bnews/02191.htm
- http://m.wap.uliejh.cn/bnews/96514.htm
- http://m.wap.uliejh.cn/bnews/823452.htm
- http://m.wap.uliejh.cn/bnews/2222.htm
- http://m.wap.uliejh.cn/bnews/8933664.htm
- http://m.wap.uliejh.cn/bnews/209814.htm
- http://m.wap.uliejh.cn/bnews/737862.htm
- http://m.wap.uliejh.cn/bnews/1816496.htm
- http://m.wap.uliejh.cn/bnews/632625.htm
- http://m.wap.uliejh.cn/bnews/188310.htm
- http://m.wap.uliejh.cn/bnews/05841.htm
- http://m.wap.uliejh.cn/bnews/4548933.htm
- http://m.wap.uliejh.cn/bnews/9025394.htm
- http://m.wap.uliejh.cn/bnews/85582.htm
- http://m.wap.uliejh.cn/bnews/8317485.htm
- http://m.wap.uliejh.cn/bnews/5864.htm
- http://m.wap.uliejh.cn/bnews/612345.htm
- http://m.wap.uliejh.cn/bnews/552821.htm
- http://m.wap.uliejh.cn/bnews/01597.htm
- http://m.wap.uliejh.cn/bnews/238113.htm
- http://m.wap.uliejh.cn/bnews/0631.htm
- http://m.wap.uliejh.cn/bnews/5741244.htm
- http://m.wap.uliejh.cn/bnews/18385.htm
- http://m.wap.uliejh.cn/bnews/2546660.htm
- http://m.wap.uliejh.cn/bnews/35154.htm
- http://m.wap.uliejh.cn/bnews/25198.htm
- http://m.wap.uliejh.cn/bnews/5580.htm
- http://m.wap.uliejh.cn/bnews/8196723.htm
- http://m.wap.uliejh.cn/bnews/6771.htm
- http://m.wap.uliejh.cn/bnews/7923.htm
- http://m.wap.uliejh.cn/bnews/5074.htm
- http://m.wap.uliejh.cn/bnews/5635.htm
- http://m.wap.uliejh.cn/bnews/046416.htm
- http://m.wap.uliejh.cn/bnews/569113.htm
- http://m.wap.uliejh.cn/bnews/553479.htm
- http://m.wap.uliejh.cn/bnews/68623.htm
- http://m.wap.uliejh.cn/bnews/05423.htm
- http://m.wap.uliejh.cn/bnews/077169.htm
- http://m.wap.uliejh.cn/bnews/51702.htm
- http://m.wap.uliejh.cn/bnews/016519.htm
- http://m.wap.uliejh.cn/bnews/042317.htm
- http://m.wap.uliejh.cn/bnews/8013.htm
- http://m.wap.uliejh.cn/bnews/250591.htm
- http://m.wap.uliejh.cn/bnews/59153.htm
- http://m.wap.uliejh.cn/bnews/8677.htm
- http://m.wap.uliejh.cn/bnews/687142.htm
- http://m.wap.uliejh.cn/bnews/4371211.htm
- http://m.wap.uliejh.cn/bnews/6054343.htm
- http://m.wap.uliejh.cn/bnews/791861.htm
- http://m.wap.uliejh.cn/bnews/643853.htm
- http://m.wap.uliejh.cn/bnews/882398.htm
- http://m.wap.uliejh.cn/bnews/14770.htm
- http://m.wap.uliejh.cn/bnews/913973.htm
- http://m.wap.uliejh.cn/bnews/9090008.htm
- http://m.wap.uliejh.cn/bnews/1278711.htm
- http://m.wap.uliejh.cn/bnews/9674818.htm
- http://m.wap.uliejh.cn/bnews/86455.htm
- http://m.wap.uliejh.cn/bnews/269238.htm
- http://m.wap.uliejh.cn/bnews/1018.htm
- http://m.wap.uliejh.cn/bnews/14142.htm
- http://m.wap.uliejh.cn/bnews/4562687.htm
- http://m.wap.uliejh.cn/bnews/39693.htm
- http://m.wap.uliejh.cn/bnews/327773.htm
- http://m.wap.uliejh.cn/bnews/3029.htm
- http://m.wap.uliejh.cn/bnews/82391.htm
- http://m.wap.uliejh.cn/bnews/717010.htm
- http://m.wap.uliejh.cn/bnews/5509.htm
- http://m.wap.uliejh.cn/bnews/1036.htm
- http://m.wap.uliejh.cn/bnews/55686.htm
- http://m.wap.uliejh.cn/bnews/3498377.htm
- http://m.wap.uliejh.cn/bnews/3289269.htm
- http://m.wap.uliejh.cn/bnews/9887829.htm
- http://m.wap.uliejh.cn/bnews/66625.htm
- http://m.wap.uliejh.cn/bnews/795232.htm
- http://m.wap.uliejh.cn/bnews/99266.htm
- http://m.wap.uliejh.cn/bnews/468518.htm
- http://m.wap.uliejh.cn/bnews/1163164.htm
- http://m.wap.uliejh.cn/bnews/8469184.htm
- http://m.wap.uliejh.cn/bnews/9401943.htm
- http://m.wap.uliejh.cn/bnews/90356.htm
- http://m.wap.uliejh.cn/bnews/88099.htm
- http://m.wap.uliejh.cn/bnews/6958.htm
- http://m.wap.uliejh.cn/bnews/25645.htm
- http://m.wap.uliejh.cn/bnews/8060.htm
- http://m.wap.uliejh.cn/bnews/17874.htm
- http://m.wap.uliejh.cn/bnews/36978.htm
- http://m.wap.uliejh.cn/bnews/74510.htm
- http://m.wap.uliejh.cn/bnews/833329.htm
- http://m.wap.uliejh.cn/bnews/8991432.htm
- http://m.wap.uliejh.cn/bnews/3971.htm
- http://m.wap.uliejh.cn/bnews/2780.htm
- http://m.wap.uliejh.cn/bnews/67751.htm
- http://m.wap.uliejh.cn/bnews/448911.htm
- http://m.wap.uliejh.cn/bnews/4252.htm
- http://m.wap.uliejh.cn/bnews/6429.htm
- http://m.wap.uliejh.cn/bnews/5310.htm
- http://m.wap.uliejh.cn/bnews/5597.htm
- http://m.wap.uliejh.cn/bnews/2799988.htm
- http://m.wap.uliejh.cn/bnews/8855717.htm
- http://m.wap.uliejh.cn/bnews/666552.htm
- http://m.wap.uliejh.cn/bnews/06723.htm
- http://m.wap.uliejh.cn/bnews/056242.htm
- http://m.wap.uliejh.cn/bnews/758019.htm
- http://m.wap.uliejh.cn/bnews/39157.htm
- http://m.wap.uliejh.cn/bnews/1995.htm
- http://m.wap.uliejh.cn/bnews/1368884.htm
- http://m.wap.uliejh.cn/bnews/686530.htm
- http://m.wap.uliejh.cn/bnews/143771.htm
- http://m.wap.uliejh.cn/bnews/573444.htm
- http://m.wap.uliejh.cn/bnews/80544.htm
- http://m.wap.uliejh.cn/bnews/005305.htm
- http://m.wap.uliejh.cn/bnews/7428.htm
- http://m.wap.uliejh.cn/bnews/165599.htm
- http://m.wap.uliejh.cn/bnews/1714.htm
- http://m.wap.uliejh.cn/bnews/586744.htm
- http://m.wap.uliejh.cn/bnews/28559.htm
- http://m.wap.uliejh.cn/bnews/1911565.htm
- http://m.wap.uliejh.cn/bnews/966938.htm
- http://m.wap.uliejh.cn/bnews/336989.htm
- http://m.wap.uliejh.cn/bnews/4901801.htm
- http://m.wap.uliejh.cn/bnews/0166.htm
- http://m.wap.uliejh.cn/bnews/2864566.htm
- http://m.wap.uliejh.cn/bnews/54049.htm
- http://m.wap.uliejh.cn/bnews/719620.htm
- http://m.wap.uliejh.cn/bnews/24274.htm
- http://m.wap.uliejh.cn/bnews/370605.htm
- http://m.wap.uliejh.cn/bnews/3386151.htm
- http://m.wap.uliejh.cn/bnews/38447.htm
- http://m.wap.uliejh.cn/bnews/623666.htm
- http://m.wap.uliejh.cn/bnews/6344937.htm
- http://m.wap.uliejh.cn/bnews/63912.htm
- http://m.wap.uliejh.cn/bnews/3612.htm
- http://m.wap.uliejh.cn/bnews/856803.htm
- http://m.wap.uliejh.cn/bnews/346317.htm
- http://m.wap.uliejh.cn/bnews/57564.htm
- http://m.wap.uliejh.cn/bnews/36120.htm
- http://m.wap.uliejh.cn/bnews/91649.htm
- http://m.wap.uliejh.cn/bnews/5194.htm
- http://m.wap.uliejh.cn/bnews/50775.htm
- http://m.wap.uliejh.cn/bnews/313864.htm
- http://m.wap.uliejh.cn/bnews/086228.htm
- http://m.wap.uliejh.cn/bnews/76685.htm
- http://m.wap.uliejh.cn/bnews/6435.htm
- http://m.wap.uliejh.cn/bnews/12462.htm
- http://m.wap.uliejh.cn/bnews/0694.htm
- http://m.wap.uliejh.cn/bnews/7056948.htm
- http://m.wap.uliejh.cn/bnews/7134188.htm
- http://m.wap.uliejh.cn/bnews/09034.htm
- http://m.wap.uliejh.cn/bnews/3637.htm
- http://m.wap.uliejh.cn/bnews/8450.htm
- http://m.wap.uliejh.cn/bnews/2355.htm
- http://m.wap.uliejh.cn/bnews/230444.htm
- http://m.wap.uliejh.cn/bnews/6255.htm
- http://m.wap.uliejh.cn/bnews/2986.htm
- http://m.wap.uliejh.cn/bnews/7529199.htm
- http://m.wap.uliejh.cn/bnews/707225.htm
- http://m.wap.uliejh.cn/bnews/4672.htm
- http://m.wap.uliejh.cn/bnews/94476.htm
- http://m.wap.uliejh.cn/bnews/9801.htm
- http://m.wap.uliejh.cn/bnews/7604474.htm
- http://m.wap.uliejh.cn/bnews/17614.htm
- http://m.wap.uliejh.cn/bnews/4376354.htm
- http://m.wap.uliejh.cn/bnews/91954.htm
- http://m.wap.uliejh.cn/bnews/50494.htm
- http://m.wap.uliejh.cn/bnews/716742.htm
- http://m.wap.uliejh.cn/bnews/448447.htm
- http://m.wap.uliejh.cn/bnews/6596.htm
- http://m.wap.uliejh.cn/bnews/568394.htm
- http://m.wap.uliejh.cn/bnews/5747.htm
- http://m.wap.uliejh.cn/bnews/9658.htm
- http://m.wap.uliejh.cn/bnews/2190857.htm
- http://m.wap.uliejh.cn/bnews/595736.htm
- http://m.wap.uliejh.cn/bnews/38601.htm
- http://m.wap.uliejh.cn/bnews/1825.htm
- http://m.wap.uliejh.cn/bnews/6206.htm
- http://m.wap.uliejh.cn/bnews/03762.htm
- http://m.wap.uliejh.cn/bnews/403171.htm
- http://m.wap.uliejh.cn/bnews/929673.htm
- http://m.wap.uliejh.cn/bnews/4367870.htm
- http://m.wap.uliejh.cn/bnews/32516.htm
- http://m.wap.uliejh.cn/bnews/8347631.htm
- http://m.wap.uliejh.cn/bnews/20720.htm
- http://m.wap.uliejh.cn/bnews/95240.htm
- http://m.wap.uliejh.cn/bnews/171025.htm
- http://m.wap.uliejh.cn/bnews/9028.htm
- http://m.wap.uliejh.cn/bnews/7892.htm
- http://m.wap.uliejh.cn/bnews/761442.htm
- http://m.wap.uliejh.cn/bnews/833030.htm
- http://m.wap.uliejh.cn/bnews/331523.htm
- http://m.wap.uliejh.cn/bnews/39025.htm
- http://m.wap.uliejh.cn/bnews/3601418.htm
- http://m.wap.uliejh.cn/bnews/340054.htm
- http://m.wap.uliejh.cn/bnews/7192.htm
- http://m.wap.uliejh.cn/bnews/4337072.htm
- http://m.wap.uliejh.cn/bnews/1404.htm
- http://m.wap.uliejh.cn/bnews/4920.htm
- http://m.wap.uliejh.cn/bnews/6406.htm

## 项目结构

```
weblink-navigator/
├── .github/                         # GitHub 社区配置文件
│   ├── ISSUE_TEMPLATE/              # 问题报告与功能请求模板
│   └── workflows/                   # CI 流水线（测试、代码检查）
├── config/                          # 环境配置目录
│   ├── env.example                  # 环境变量模板（数据库、Redis、日志级别）
│   ├── gunicorn.conf.py             # 生产级 Gunicorn 工作进程配置
│   └── supervisor/                  # Supervisor 进程管理配置片段
├── docs/                            # 完整项目文档
│   ├── quickstart.md               # 5 分钟快速上手教程
│   ├── operations.md               # 日常运维与故障排查手册
│   ├── api_reference.md            # RESTful API 端点详细说明
│   └── development.md              # 二次开发环境搭建与代码规范
├── src/                             # 核心源代码
│   ├── core/                       # 核心业务模块
│   │   ├── importer.py             # 批量导入、去重与标签分配引擎
│   │   ├── checker.py              # 健康检查调度器与探测结果持久化
│   │   └── extractor.py            # 元数据抓取、解析与摘要生成器
│   ├── web/                        # Web 界面与 API 路由
│   │   ├── app.py                  # Flask 应用工厂与蓝图注册
│   │   ├── routes/                 # 按功能拆分路由模块（链接、标签、导出）
│   │   └── static/                 # 前端静态资源（CSS / JS / 图标）
│   ├── models/                     # 数据模型与 ORM 映射
│   │   ├── link.py                 # Link 实体与指纹计算逻辑
│   │   ├── tag.py                  # 标签树与多对多关联表
│   │   └── snapshot.py             # 快照存档记录模型
│   ├── services/                   # 外部服务集成层
│   │   ├── search.py               # FTS5 与 Elasticsearch 适配器
│   │   ├── cache.py                # Redis 缓存装饰器与失效策略
│   │   └── queue.py                # Celery 任务定义与路由配置
│   └── utils/                      # 通用工具函数
│       ├── http.py                 # 带超时重试的 HTTP 请求封装
│       ├── logger.py               # 结构化日志配置（JSON 格式）
│       └── validator.py            # URL 归一化与安全校验
├── tests/                           # 单元测试与集成测试
│   ├── unit/                       # 针对核心函数的细粒度测试
│   └── integration/                # 数据库与外部依赖的端到端测试
├── scripts/                         # 运维与辅助脚本
│   ├── backup_db.sh                # 数据库自动备份脚本（cron 调用）
│   └── migrate_tags.py             # 标签体系版本迁移工具
├── data/                            # 运行时数据目录（默认 SQLite 与日志存放处）
│   ├── weblink.db                  # 主数据库文件（自动生成）
│   └── snapshots/                  # 按域名分组的 HTML 快照存储
├── requirements.txt                 # Python 生产依赖列表
├── requirements-dev.txt             # 开发与测试额外依赖
├── setup.py                         # 项目打包与安装入口
└── README.md                        # 本文档
```

## 贡献指南

1. 阅读项目文档与代码规范：在提交任何代码或文档变更前，请先通读 `docs/development.md` 了解项目架构、编码风格（PEP 8 + Black 格式化）以及 Git 提交信息格式要求（Conventional Commits）。

2. 查找或创建 Issue 并认领任务：访问 GitHub Issues 页面，查找带有 `good-first-issue` 或 `help-wanted` 标签的任务。若无相关 Issue，请先新建一个描述清楚你所发现的问题或希望新增的功能，等待维护者回复确认后再开始编码。

3. 派生仓库并创建功能分支：Fork 本项目至个人账户，基于 `main` 分支创建以 `feature/` 或 `fix/` 为前缀的分支，例如 `feature/add-rss-export`。严禁在 main 分支上直接修改。

4. 编写测试用例并确保 CI 通过：新增功能需在 `tests/` 对应目录下添加单元测试或集成测试，确保测试覆盖率达到 80% 以上。提交后触发 GitHub Actions 流水线，需等待所有检查（测试、Lint、构建）通过。

5. 发起 Pull Request 并参与评审：推送到个人分支后，向主仓库的 `main` 分支发起 PR。PR 描述需引用关联 Issue 编号，并列出主要变更点与测试结果。至少需要一名维护者 Approve 后方可合并。

## 常见问题

Q: 导入几百个链接时页面卡顿或超时，如何处理？
A: 建议使用命令行导入模式而非 Web 界面上传，执行 `python manage.py import --file your_list.csv --batch-size 50` 可分段提交，每批 50 条。同时请确保 Redis 和 Celery 工作进程已启动，系统会自动将导入任务转为异步执行，前端不再阻塞。

Q: 健康检查模块报告大量链接超时，但浏览器手动访问正常？
A: 检查服务器网络出口是否受限或 DNS 解析异常。健康检查使用系统默认网络栈，可能受防火墙或代理配置影响。请修改 `.env` 中的 `CHECKER_TIMEOUT` 和 `CHECKER_USER_AGENT` 参数，部分站点对非浏览器 User-Agent 返回 403 或 429。另可开启 `CHECKER_VERIFY_SSL=false` 绕过证书验证。

Q: 如何将本系统与现有的 Wiki 或笔记软件（如 Notion、Obsidian）联动？
A: 使用导出功能生成 Markdown 表格或 JSON 文件，再通过各软件提供的导入接口或 API 同步。本项目的 `export` 命令支持 `--format json` 与 `--format markdown`，并可通过 `--tag` 筛选特定分类。推荐编写简单的 cron 定时任务每日导出最新列表并推送到 WebDAV 或 Git 仓库。

## 许可证

MIT

> 外链数量: 250 | 生成时间: 2026-08-24 23:40:21
