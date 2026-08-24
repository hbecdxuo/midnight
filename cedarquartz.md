# WebLink Navigator

WebLink Navigator 是一个面向技术研究者和信息分析人员的结构化外链资源聚合与导航系统。项目定位于对分散于互联网各处的技术文章、学术资料、行业报告及深度评论进行系统性收录、分类与检索，帮助用户从海量信息中快速定位高价值内容。本项目不提供内容存储或二次分发，仅作为 URL 元数据的组织与展示层，所有资源版权归原始出处所有。

目标用户包括：技术研究员、开源社区贡献者、产品经理、数据分析师、以及需要持续追踪特定领域资讯的从业人员。通过统一的索引视图和标签体系，用户可以在数秒内完成从宏观浏览到微观定位的信息筛选流程。

## 功能概览

**多维度分类导航**：按技术领域、内容类型、发布时间、来源站点等维度提供交叉筛选入口，支持用户自定义标签组合。

**全文元数据检索**：基于标题、描述、关键词及自定义注释字段进行快速检索，检索结果高亮显示匹配位置。

**收藏夹与阅读列表**：允许用户创建私有收藏夹，将待读或重点关注资源暂存，支持导入导出为 JSON 格式。

**定期快照校验**：对已收录的 URL 进行定期的可访问性检查，自动标记失效链接并生成报告，便于维护者清理或更新。

**批次管理视图**：以项目批次（如第 95/120 批）为单位展示资源收录进度，每个批次包含独立的提交记录与审核状态。

**原始数据导出**：支持将当前视图下的所有 URL 列表导出为纯文本、CSV 或 Markdown 表格格式，便于外部工具处理。

**权限分级控制**：管理员、编辑者、访客三级权限体系，控制资源的增删改查及敏感信息查看范围。

## 应用场景

**技术团队内部知识库构建**：团队可将本系统作为内部技术文档的外链索引中心，将日常阅读的优质博客、官方文档、API 参考统一收录，新成员入职时可快速了解团队关注的资源图谱。

**开源项目参考文档聚合**：开源项目维护者可以利用本系统收集与项目相关的依赖库、同类竞品分析、社区讨论帖及性能测试报告，方便在项目 README 或 Wiki 中引用外部证据。

**学术文献辅助整理**：研究人员在撰写文献综述时，可将散落在不同数据库和预印本平台上的相关论文、数据集页面及工具仓库地址集中管理，并添加个人批注与重要性评分。

**信息监控与趋势跟踪**：产品经理或行业分析师可订阅特定标签下的新增资源，定期查看本批次收录中是否出现新的竞争对手动态、技术标准更新或用户需求讨论。

## 快速开始

以下命令演示如何在本地环境中部署 WebLink Navigator 开发实例。

```bash
# 克隆代码仓库
git clone https://github.com/weblink-navigator/weblink-navigator.git
cd weblink-navigator

# 安装项目依赖（使用 pip 与虚拟环境）
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt

# 初始化数据库并导入示例批次数据（第 95/120 批）
python manage.py migrate
python manage.py loaddata batch_095_fixture.json

# 启动开发服务器
python manage.py runserver 0.0.0.0:8000
```

访问 `http://localhost:8000` 即可进入导航主页。默认管理员账号为 `admin`，密码为 `admin123`，首次登录后请务必修改。

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|---------|---------|------|
| Python | 3.9 至 3.11 | 核心运行环境，3.12 暂未完成兼容性测试 |
| Django | 4.2.x LTS | Web 框架，用于处理路由、ORM 及管理后台 |
| PostgreSQL | 14 及以上 | 生产环境推荐数据库，支持全文搜索及 JSON 字段 |
| Redis | 7.0 及以上 | 用于缓存会话、页面碎片及任务队列代理 |
| Celery | 5.3.x | 异步任务处理器，执行链接快照校验与邮件通知 |
| uWSGI | 2.0.x | 生产环境 WSGI 服务器，处理高并发请求 |
| Node.js | 18.x 或 20.x | 用于前端静态资源构建（Sass 编译与 JS 打包） |
| Nginx | 1.24 及以上 | 反向代理与静态文件服务，生产环境必备 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|------|------|-----------|
| 用户手册 | `/docs/user-guide/` | 如何注册账号、创建收藏夹、使用检索与筛选功能？ |
| 管理员指南 | `/docs/admin-guide/` | 如何管理批次、审核资源、查看校验报告与用户权限？ |
| 开发参考 | `/docs/developer-api/` | API 端点定义、数据模型字段说明及自定义插件开发规范？ |
| 部署运维 | `/docs/deployment/` | 如何配置 Nginx + uWSGI + PostgreSQL 的生产集群环境？ |
| 贡献规范 | `/docs/contributing/` | 提交资源、修复 Bug 或增加功能时应遵循的流程与代码风格？ |
| 常见问题 | `/docs/faq/` | 链接失效如何处理？导入导出格式支持哪些？如何迁移数据库？ |

## 资源列表

- http://m.blog.uliejh.cn/snews/9612.htm
- http://m.blog.uliejh.cn/snews/79085.htm
- http://m.blog.uliejh.cn/snews/9582392.htm
- http://m.blog.uliejh.cn/snews/985409.htm
- http://m.blog.uliejh.cn/snews/5826130.htm
- http://m.blog.uliejh.cn/snews/1770.htm
- http://m.blog.uliejh.cn/snews/116219.htm
- http://m.blog.uliejh.cn/snews/49669.htm
- http://m.blog.uliejh.cn/snews/36314.htm
- http://m.blog.uliejh.cn/snews/8209.htm
- http://m.blog.uliejh.cn/snews/614977.htm
- http://m.blog.uliejh.cn/snews/7383596.htm
- http://m.blog.uliejh.cn/snews/14547.htm
- http://m.blog.uliejh.cn/snews/533404.htm
- http://m.blog.uliejh.cn/snews/611134.htm
- http://m.blog.uliejh.cn/snews/700229.htm
- http://m.blog.uliejh.cn/snews/7794.htm
- http://m.blog.uliejh.cn/snews/562892.htm
- http://m.blog.uliejh.cn/snews/604599.htm
- http://m.blog.uliejh.cn/snews/0857.htm
- http://m.blog.uliejh.cn/snews/06154.htm
- http://m.blog.uliejh.cn/snews/701158.htm
- http://m.blog.uliejh.cn/snews/37006.htm
- http://m.blog.uliejh.cn/snews/16682.htm
- http://m.blog.uliejh.cn/snews/0019089.htm
- http://m.blog.uliejh.cn/snews/56851.htm
- http://m.blog.uliejh.cn/snews/0724.htm
- http://m.blog.uliejh.cn/snews/8202.htm
- http://m.blog.uliejh.cn/snews/13678.htm
- http://m.blog.uliejh.cn/snews/968912.htm
- http://m.blog.uliejh.cn/snews/0831.htm
- http://m.blog.uliejh.cn/snews/2166.htm
- http://m.blog.uliejh.cn/snews/6766.htm
- http://m.blog.uliejh.cn/snews/090571.htm
- http://m.blog.uliejh.cn/snews/30455.htm
- http://m.blog.uliejh.cn/snews/5618.htm
- http://m.blog.uliejh.cn/snews/8069683.htm
- http://m.blog.uliejh.cn/snews/5611.htm
- http://m.blog.uliejh.cn/snews/1301.htm
- http://m.blog.uliejh.cn/snews/84796.htm
- http://m.blog.uliejh.cn/snews/0342.htm
- http://m.blog.uliejh.cn/snews/913279.htm
- http://m.blog.uliejh.cn/snews/551118.htm
- http://m.blog.uliejh.cn/snews/2837644.htm
- http://m.blog.uliejh.cn/snews/1345.htm
- http://m.blog.uliejh.cn/snews/613391.htm
- http://m.blog.uliejh.cn/snews/5695.htm
- http://m.blog.uliejh.cn/snews/19428.htm
- http://m.blog.uliejh.cn/snews/17909.htm
- http://m.blog.uliejh.cn/snews/443655.htm
- http://m.blog.uliejh.cn/snews/9125322.htm
- http://m.blog.uliejh.cn/snews/478471.htm
- http://m.blog.uliejh.cn/snews/3369153.htm
- http://m.blog.uliejh.cn/snews/6797283.htm
- http://m.blog.uliejh.cn/snews/3740.htm
- http://m.blog.uliejh.cn/snews/2564949.htm
- http://m.blog.uliejh.cn/snews/2559511.htm
- http://m.blog.uliejh.cn/snews/94609.htm
- http://m.blog.uliejh.cn/snews/02713.htm
- http://m.blog.uliejh.cn/snews/9564.htm
- http://m.blog.uliejh.cn/snews/262522.htm
- http://m.blog.uliejh.cn/snews/6197253.htm
- http://m.blog.uliejh.cn/snews/8751770.htm
- http://m.blog.uliejh.cn/snews/005841.htm
- http://m.blog.uliejh.cn/snews/502308.htm
- http://m.blog.uliejh.cn/snews/4025611.htm
- http://m.blog.uliejh.cn/snews/5465978.htm
- http://m.blog.uliejh.cn/snews/231616.htm
- http://m.blog.uliejh.cn/snews/6470770.htm
- http://m.blog.uliejh.cn/snews/1707.htm
- http://m.blog.uliejh.cn/snews/6984830.htm
- http://m.blog.uliejh.cn/snews/8636.htm
- http://m.blog.uliejh.cn/snews/25398.htm
- http://m.blog.uliejh.cn/snews/846082.htm
- http://m.blog.uliejh.cn/snews/7088.htm
- http://m.blog.uliejh.cn/snews/7161.htm
- http://m.blog.uliejh.cn/snews/532223.htm
- http://m.blog.uliejh.cn/snews/9439.htm
- http://m.blog.uliejh.cn/snews/23295.htm
- http://m.blog.uliejh.cn/snews/49843.htm
- http://m.blog.uliejh.cn/snews/018376.htm
- http://m.blog.uliejh.cn/snews/787304.htm
- http://m.blog.uliejh.cn/snews/264071.htm
- http://m.blog.uliejh.cn/snews/82093.htm
- http://m.blog.uliejh.cn/snews/196080.htm
- http://m.blog.uliejh.cn/snews/8037486.htm
- http://m.blog.uliejh.cn/snews/010737.htm
- http://m.blog.uliejh.cn/snews/7234.htm
- http://m.blog.uliejh.cn/snews/275245.htm
- http://m.blog.uliejh.cn/snews/5707.htm
- http://m.blog.uliejh.cn/snews/54152.htm
- http://m.blog.uliejh.cn/snews/98987.htm
- http://m.blog.uliejh.cn/snews/85340.htm
- http://m.blog.uliejh.cn/snews/1100.htm
- http://m.blog.uliejh.cn/snews/012568.htm
- http://m.blog.uliejh.cn/snews/1464.htm
- http://m.blog.uliejh.cn/snews/1713692.htm
- http://m.blog.uliejh.cn/snews/75047.htm
- http://m.blog.uliejh.cn/snews/768016.htm
- http://m.blog.uliejh.cn/snews/4663.htm
- http://m.blog.uliejh.cn/snews/35112.htm
- http://m.blog.uliejh.cn/snews/1632.htm
- http://m.blog.uliejh.cn/snews/8899.htm
- http://m.blog.uliejh.cn/snews/288121.htm
- http://m.blog.uliejh.cn/snews/425438.htm
- http://m.blog.uliejh.cn/snews/745750.htm
- http://m.blog.uliejh.cn/snews/38642.htm
- http://m.blog.uliejh.cn/snews/134644.htm
- http://m.blog.uliejh.cn/snews/44087.htm
- http://m.blog.uliejh.cn/snews/8787494.htm
- http://m.blog.uliejh.cn/snews/2315909.htm
- http://m.blog.uliejh.cn/snews/26720.htm
- http://m.blog.uliejh.cn/snews/119824.htm
- http://m.blog.uliejh.cn/snews/5276538.htm
- http://m.blog.uliejh.cn/snews/3516.htm
- http://m.blog.uliejh.cn/snews/9952.htm
- http://m.blog.uliejh.cn/snews/02084.htm
- http://m.blog.uliejh.cn/snews/92524.htm
- http://m.blog.uliejh.cn/snews/821716.htm
- http://m.blog.uliejh.cn/snews/8229.htm
- http://m.blog.uliejh.cn/snews/71309.htm
- http://m.blog.uliejh.cn/snews/29460.htm
- http://m.blog.uliejh.cn/snews/826832.htm
- http://m.blog.uliejh.cn/snews/3541.htm
- http://m.blog.uliejh.cn/snews/1343209.htm
- http://m.blog.uliejh.cn/snews/04257.htm
- http://m.blog.uliejh.cn/snews/933151.htm
- http://m.blog.uliejh.cn/snews/3732789.htm
- http://m.blog.uliejh.cn/snews/35009.htm
- http://m.blog.uliejh.cn/snews/6219293.htm
- http://m.blog.uliejh.cn/snews/963579.htm
- http://m.blog.uliejh.cn/snews/5838710.htm
- http://m.blog.uliejh.cn/snews/2318.htm
- http://m.blog.uliejh.cn/snews/1922973.htm
- http://m.blog.uliejh.cn/snews/3545.htm
- http://m.blog.uliejh.cn/snews/0822.htm
- http://m.blog.uliejh.cn/snews/76333.htm
- http://m.blog.uliejh.cn/snews/540004.htm
- http://m.blog.uliejh.cn/snews/0657.htm
- http://m.blog.uliejh.cn/snews/6454.htm
- http://m.blog.uliejh.cn/snews/449374.htm
- http://m.blog.uliejh.cn/snews/0270.htm
- http://m.blog.uliejh.cn/snews/956382.htm
- http://m.blog.uliejh.cn/snews/4535.htm
- http://m.blog.uliejh.cn/snews/37830.htm
- http://m.blog.uliejh.cn/snews/1060.htm
- http://m.blog.uliejh.cn/snews/174310.htm
- http://m.blog.uliejh.cn/snews/728215.htm
- http://m.blog.uliejh.cn/snews/0841.htm
- http://m.blog.uliejh.cn/snews/28218.htm
- http://m.blog.uliejh.cn/snews/5939.htm
- http://m.blog.uliejh.cn/snews/68420.htm
- http://m.blog.uliejh.cn/snews/533795.htm
- http://m.blog.uliejh.cn/snews/8119.htm
- http://m.blog.uliejh.cn/snews/137767.htm
- http://m.blog.uliejh.cn/snews/1512419.htm
- http://m.blog.uliejh.cn/snews/5616645.htm
- http://m.blog.uliejh.cn/snews/244602.htm
- http://m.blog.uliejh.cn/snews/234020.htm
- http://m.blog.uliejh.cn/snews/9817.htm
- http://m.blog.uliejh.cn/snews/784385.htm
- http://m.blog.uliejh.cn/snews/1880.htm
- http://m.blog.uliejh.cn/snews/8177950.htm
- http://m.blog.uliejh.cn/snews/5532.htm
- http://m.blog.uliejh.cn/snews/1284560.htm
- http://m.blog.uliejh.cn/snews/4337465.htm
- http://m.blog.uliejh.cn/snews/17719.htm
- http://m.blog.uliejh.cn/snews/9695.htm
- http://m.blog.uliejh.cn/snews/14379.htm
- http://m.blog.uliejh.cn/snews/1329151.htm
- http://m.blog.uliejh.cn/snews/8158.htm
- http://m.blog.uliejh.cn/snews/6844.htm
- http://m.blog.uliejh.cn/snews/2545489.htm
- http://m.blog.uliejh.cn/snews/8375.htm
- http://m.blog.uliejh.cn/snews/2150269.htm
- http://m.blog.uliejh.cn/snews/56757.htm
- http://m.blog.uliejh.cn/snews/5270.htm
- http://m.blog.uliejh.cn/snews/638545.htm
- http://m.blog.uliejh.cn/snews/2393910.htm
- http://m.blog.uliejh.cn/snews/2562.htm
- http://m.blog.uliejh.cn/snews/9964133.htm
- http://m.blog.uliejh.cn/snews/087485.htm
- http://m.blog.uliejh.cn/snews/4169.htm
- http://m.blog.uliejh.cn/snews/7023536.htm
- http://m.blog.uliejh.cn/snews/150778.htm
- http://m.blog.uliejh.cn/snews/7904.htm
- http://m.blog.uliejh.cn/snews/0057.htm
- http://m.blog.uliejh.cn/snews/7454178.htm
- http://m.blog.uliejh.cn/snews/58243.htm
- http://m.blog.uliejh.cn/snews/8545.htm
- http://m.blog.uliejh.cn/snews/873299.htm
- http://m.blog.uliejh.cn/snews/8941.htm
- http://m.blog.uliejh.cn/snews/62845.htm
- http://m.blog.uliejh.cn/snews/90553.htm
- http://m.blog.uliejh.cn/snews/994402.htm
- http://m.blog.uliejh.cn/snews/77176.htm
- http://m.blog.uliejh.cn/snews/0570.htm
- http://m.blog.uliejh.cn/snews/0391570.htm
- http://m.blog.uliejh.cn/snews/67670.htm
- http://m.blog.uliejh.cn/snews/39421.htm
- http://m.blog.uliejh.cn/snews/404465.htm
- http://m.blog.uliejh.cn/snews/339445.htm
- http://m.blog.uliejh.cn/snews/85993.htm
- http://m.blog.uliejh.cn/snews/29780.htm
- http://m.blog.uliejh.cn/snews/46442.htm
- http://m.blog.uliejh.cn/snews/247501.htm
- http://m.blog.uliejh.cn/snews/9648.htm
- http://m.blog.uliejh.cn/snews/7779909.htm
- http://m.blog.uliejh.cn/snews/650986.htm
- http://m.blog.uliejh.cn/snews/5404631.htm
- http://m.blog.uliejh.cn/snews/5419674.htm
- http://m.blog.uliejh.cn/snews/959637.htm
- http://m.blog.uliejh.cn/snews/1789.htm
- http://m.blog.uliejh.cn/snews/99335.htm
- http://m.blog.uliejh.cn/snews/4260553.htm
- http://m.blog.uliejh.cn/snews/4991583.htm
- http://m.blog.uliejh.cn/snews/98010.htm
- http://m.blog.uliejh.cn/snews/2290.htm
- http://m.blog.uliejh.cn/snews/5555.htm
- http://m.blog.uliejh.cn/snews/246537.htm
- http://m.blog.uliejh.cn/snews/02901.htm
- http://m.blog.uliejh.cn/snews/5078400.htm
- http://m.blog.uliejh.cn/snews/2553691.htm
- http://m.blog.uliejh.cn/snews/27189.htm
- http://m.blog.uliejh.cn/snews/42285.htm
- http://m.blog.uliejh.cn/snews/15188.htm
- http://m.blog.uliejh.cn/snews/98853.htm
- http://m.blog.uliejh.cn/snews/878325.htm
- http://m.blog.uliejh.cn/snews/85294.htm
- http://m.blog.uliejh.cn/snews/040106.htm
- http://m.blog.uliejh.cn/snews/3122577.htm
- http://m.blog.uliejh.cn/snews/0726721.htm
- http://m.blog.uliejh.cn/snews/39154.htm
- http://m.blog.uliejh.cn/snews/0390.htm
- http://m.blog.uliejh.cn/snews/4874.htm
- http://m.blog.uliejh.cn/snews/12453.htm
- http://m.blog.uliejh.cn/snews/95720.htm
- http://m.blog.uliejh.cn/snews/71271.htm
- http://m.blog.uliejh.cn/snews/0330.htm
- http://m.blog.uliejh.cn/snews/928492.htm
- http://m.blog.uliejh.cn/snews/1630590.htm
- http://m.blog.uliejh.cn/snews/9473567.htm
- http://m.blog.uliejh.cn/snews/4235.htm
- http://m.blog.uliejh.cn/snews/4904.htm
- http://m.blog.uliejh.cn/snews/7850818.htm
- http://m.blog.uliejh.cn/snews/590229.htm
- http://m.blog.uliejh.cn/snews/7393702.htm
- http://m.blog.uliejh.cn/snews/430909.htm
- http://m.blog.uliejh.cn/snews/9683413.htm
- http://m.blog.uliejh.cn/snews/95559.htm

## 项目结构

```
weblink-navigator/
├── manage.py                    # Django 项目管理入口
├── requirements.txt             # Python 依赖清单（生产与开发分离）
├── config/                      # 项目全局配置目录
│   ├── settings/                # 多环境配置（base, dev, prod, test）
│   │   ├── base.py              # 基础配置，适用于所有环境
│   │   ├── dev.py               # 开发环境：DEBUG=True, 本地数据库
│   │   └── prod.py              # 生产环境：DEBUG=False, 外部数据库
│   ├── urls.py                  # 根路由配置
│   └── celery.py                # Celery 应用实例与调度配置
├── apps/                        # 所有自定义 Django 应用
│   ├── resources/               # 资源核心模块：URL 收录、分类、标签
│   │   ├── models.py            # Resource, Batch, Tag, CheckRecord 模型
│   │   ├── views.py             # 资源列表、详情、检索、导出视图
│   │   └── tasks.py             # 异步校验、快照生成任务
│   ├── accounts/                # 用户认证与权限管理
│   │   ├── models.py            # 扩展 User 模型，添加角色与收藏关系
│   │   └── backends.py          # 自定义邮箱/用户名双字段认证后端
│   ├── collections/             # 收藏夹与阅读列表模块
│   │   ├── models.py            # Collection, CollectionItem 模型
│   │   └── services.py          # 导入/导出 JSON 格式的业务逻辑
│   └── dashboard/               # 管理仪表盘与统计视图
│       ├── views.py             # 批次进度、校验报告、热门资源图表
│       └── templatetags/        # 自定义模板过滤器，用于格式化日期与状态
├── static/                      # 静态资源（CSS, JS, 图片）
│   ├── css/                     # 基于 Sass 编译的主样式与主题变量
│   ├── js/                      # 原生 JavaScript 及 Vue 组件（搜索框、筛选面板）
│   └── images/                  # Logo、默认占位图及图表背景
├── templates/                   # Django 模板文件
│   ├── base.html                # 基础骨架模板，包含导航栏与页脚
│   ├── resources/               # 资源相关页面模板
│   │   ├── list.html            # 资源列表（支持分页、筛选、排序）
│   │   └── detail.html          # 资源详情（显示完整元数据与校验状态）
│   └── dashboard/               # 仪表盘页面模板
├── fixtures/                    # 初始数据与示例批次
│   ├── batch_095_fixture.json   # 第 95/120 批次的预置数据（含 250 条 URL）
│   └── default_tags.json        # 预设标签体系（技术、学术、新闻等）
├── scripts/                     # 运维及辅助脚本
│   ├── check_links.py           # 手动触发全量链接校验的命令行工具
│   └── export_batch.py          # 将指定批次导出为 CSV/JSON 格式
├── logs/                        # 应用日志存储目录（按日切割）
│   ├── access.log               # 访问日志
│   └── error.log                # 错误与异常追踪日志
├── docker-compose.yml           # Docker Compose 编排文件（含 Postgres + Redis）
├── Dockerfile                   # 生产环境镜像构建定义
├── .env.example                 # 环境变量示例文件（数据库连接、密钥等）
└── README.md                    # 本项目文档（即当前文件）
```

## 贡献指南

1. 复刻本项目仓库至个人账户，并在本地创建功能分支（命名格式为 `feature/描述` 或 `fix/描述`）。所有的开发工作应在分支上进行，避免直接修改主分支。

2. 新增资源收录时，请确保每个 URL 附带标题、来源简述及至少一个分类标签。若提交批量数据，需按照 `fixtures/batch_template.json` 的格式准备 JSON 文件，并在 Pull Request 中说明批次来源及审核依据。

3. 代码变更须通过现有的单元测试与静态检查（Flake8 和 Black）。在提交前运行 `python manage.py test` 确保所有测试通过，同时使用 `black .` 格式化代码。新功能需附带对应的测试用例。

4. 提交 Pull Request 时，请清晰描述变更动机、实现方式及影响范围。若涉及数据库模型变更，必须包含迁移文件（`python manage.py makemigrations`）并在 PR 中说明迁移的向前兼容性。

5. 文档更新与代码变更同等重要。任何新增功能或修改的 API 行为，须同步更新 `/docs/` 下的对应手册。翻译或校对工作也欢迎通过 Issue 认领。

## 常见问题

**Q：收录的链接失效了怎么办？**

系统每天凌晨通过 Celery 定时任务对所有已收录 URL 发起 HEAD 请求检查状态码。若连续三次校验均返回 4xx 或 5xx，该资源会被标记为“失效”并移至待复核列表。管理员可在后台查看失效详情，手动决定是否移除或更新链接。普通用户若发现失效链接，也可通过资源详情页的“报告问题”按钮提交反馈。

**Q：如何将本系统的数据迁移到另一个环境？**

推荐使用 Django 的 dumpdata 和 loaddata 命令进行数据迁移。首先在源环境执行 `python manage.py dumpdata --exclude auth.permission --exclude contenttypes > data.json`，然后在新环境执行 `python manage.py loaddata data.json`。注意排除权限和内容类型表以避免冲突。对于 PostgreSQL，也可使用 pg_dump 进行完整数据库迁移，但需确保两台服务器的 PostgreSQL 大版本一致。

**Q：检索时为什么某些刚添加的资源搜不到？**

检索功能基于数据库的全文搜索索引，索引更新存在约 5 分钟的异步延迟（由 Celery 任务触发）。如果急需搜索刚添加的资源，可以手动在管理后台执行“重建索引”操作，或等待下一次索引周期。该设计是为了降低频繁写入操作对检索性能的影响。

## 许可证

MIT

> 外链数量: 250 | 生成时间: 2026-08-24 23:40:21
