# WebLink Navigator

WebLink Navigator 是一个面向技术研究者与内容聚合者的轻量级外链资源导航系统。该项目定位于对分散于互联网各处的技术文章、新闻简报与参考文档进行结构化收束，通过统一的索引层将零散的 URL 转化为可检索、可分类、可追溯的知识入口。项目本身不存储任何内容实体，仅提供链接的元数据描述与分类标签体系，适用于个人开发者、技术团队或内容运营者建立私有的外链资源库。

项目采用静态站点生成机制，基于 Markdown 源文件与 JSON 索引数据构建可部署的 HTML 导航页面。所有外链资源按主题、日期、来源域名与内容类型四个维度进行划分，并提供全文检索与标签过滤能力。WebLink Navigator 不依赖外部数据库，所有索引数据以纯文本形式存储于仓库中，便于版本管理与协作编辑。目标用户包括需要管理大量技术书签的开发者、需要维护团队知识库的技术负责人，以及希望对外链资源进行二次加工的内容创作者。

## 功能概览

**多维度分类索引**：每条链接支持归属至多个分类标签，包括但不限于后端开发、前端工程、DevOps、数据库、安全、算法与人工智能等。系统根据标签自动生成分类导航页。

**全文检索与模糊匹配**：基于 Lunr.js 构建客户端全文检索引擎，支持对链接标题、描述、标签与来源域名的模糊搜索，搜索结果按相关性排序并高亮匹配片段。

**自动化的元数据抓取与更新**：通过 GitHub Actions 配置定时任务，自动访问新增链接并抓取页面标题、描述与关键词，生成建议标签供人工审核后入库。

**链接存活检测与状态标记**：定期对已收录链接发起 HEAD 请求，检测 HTTP 状态码，对失效链接自动标记为不可用并记录最后检测时间，支持手动重新验证。

**个性化收藏与备注功能**：登录用户可为任意链接添加自定义备注与个人收藏标记，收藏列表保存在用户本地存储或可选同步至后端服务。

**批量导入与导出**：支持从浏览器书签 HTML 文件、Markdown 列表或纯文本 URL 列表批量导入链接，同时支持将当前索引数据导出为 CSV 或 JSON 格式用于备份或迁移。

**界面响应式与暗色主题**：前端页面基于 CSS Grid 与 Flexbox 构建，适配桌面端与移动端浏览器。内置亮色与暗色两套主题，跟随系统偏好或用户手动切换。

## 应用场景

个人技术书签的集中化管理：开发者日常浏览技术博客、官方文档与社区讨论时产生大量散落的书签。WebLink Navigator 提供统一的录入界面与分类体系，将书签从浏览器中解放出来，形成可检索、可分享的私有资源库。

团队知识库的外链整合：技术团队在项目迭代过程中积累了大量外部参考链接，包括依赖库文档、故障排查案例、性能优化指南等。使用 WebLink Navigator 建立共享索引，团队成员可统一提交链接并附带评审备注，减少重复查找成本。

技术资讯的每日聚合阅读：运营者或内容编辑每日从 RSS 源、邮件简报与社交媒体中筛选优质技术文章，通过 WebLink Navigator 的快速录入表单批量添加链接，并利用分类与标签生成每日阅读列表，供订阅者或内部成员浏览。

离线文档的补充索引：对于部署在内网环境的技术文档站或 API 参考手册，WebLink Navigator 可作为入口导航页，将内网中分散的文档链接统一组织，并提供本地搜索能力，避免在内网多个站点间反复跳转。

## 快速开始

以下步骤适用于开发环境或自托管部署。请确保系统已安装 Git、Node.js 与 npm。

```bash
# 克隆仓库
git clone https://github.com/weblink-navigator/weblink-navigator.git
cd weblink-navigator

# 安装项目依赖
npm install

# 构建索引数据与静态页面
npm run build

# 启动本地开发服务器，默认监听端口 3000
npm start
```

访问 http://localhost:3000 即可查看导航站点首页。如需修改链接数据，请编辑 `data/links.json` 文件，随后重新运行 `npm run build` 刷新索引。

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|----------|----------|------|
| Node.js | >= 18.0.0 | 运行时环境，用于执行构建脚本与开发服务器 |
| npm | >= 9.0.0 | 包管理器，用于安装项目依赖 |
| Git | >= 2.30.0 | 版本控制工具，用于克隆仓库与提交变更 |
| curl | >= 7.68.0 | 用于元数据抓取脚本中的 HTTP 请求发送 |
| jq | >= 1.6 | 命令行 JSON 处理器，用于解析抓取结果 |
| Python | >= 3.9 (可选) | 仅在运行高级分析脚本时需要，基础构建无需 |
| SQLite | >= 3.35 (可选) | 仅在启用持久化缓存层时需要，默认使用内存缓存 |
| Nginx | >= 1.18 (生产部署) | 生产环境推荐的反向代理与静态文件服务器 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|------|------|------------|
| 用户手册 | /docs/user-guide/ | 如何添加链接、如何分类、如何搜索与收藏、如何导入导出数据 |
| 管理员指南 | /docs/admin-guide/ | 如何配置定时抓取、如何审核建议标签、如何管理失效链接与用户权限 |
| 开发者文档 | /docs/developer-guide/ | 项目架构说明、数据模型定义、API 接口规范、自定义主题开发指南 |
| 部署参考 | /docs/deployment/ | 支持的环境变量列表、Docker 镜像构建、Nginx 配置模板与 HTTPS 证书设置 |
| 数据格式 | /docs/data-format/ | links.json 与 index.json 的字段定义、标签约束、时间戳格式与扩展字段说明 |
| 贡献规范 | /CONTRIBUTING.md | 提交链接的审核流程、代码提交约定、PR 模板与行为准则 |

## 资源列表

- http://m.blog.uliejh.cn/snews/2566340.htm
- http://m.blog.uliejh.cn/snews/0202254.htm
- http://m.blog.uliejh.cn/snews/985834.htm
- http://m.blog.uliejh.cn/snews/2055.htm
- http://m.blog.uliejh.cn/snews/340313.htm
- http://m.blog.uliejh.cn/snews/950493.htm
- http://m.blog.uliejh.cn/snews/500367.htm
- http://m.blog.uliejh.cn/snews/38087.htm
- http://m.blog.uliejh.cn/snews/9984.htm
- http://m.blog.uliejh.cn/snews/36929.htm
- http://m.blog.uliejh.cn/snews/08325.htm
- http://m.blog.uliejh.cn/snews/4273849.htm
- http://m.blog.uliejh.cn/snews/6219.htm
- http://m.blog.uliejh.cn/snews/175839.htm
- http://m.blog.uliejh.cn/snews/61440.htm
- http://m.blog.uliejh.cn/snews/8171.htm
- http://m.blog.uliejh.cn/snews/019019.htm
- http://m.blog.uliejh.cn/snews/4566534.htm
- http://m.blog.uliejh.cn/snews/5077306.htm
- http://m.blog.uliejh.cn/snews/8604301.htm
- http://m.blog.uliejh.cn/snews/21212.htm
- http://m.blog.uliejh.cn/snews/329631.htm
- http://m.blog.uliejh.cn/snews/96519.htm
- http://m.blog.uliejh.cn/snews/035514.htm
- http://m.blog.uliejh.cn/snews/4147.htm
- http://m.blog.uliejh.cn/snews/639754.htm
- http://m.blog.uliejh.cn/snews/2341840.htm
- http://m.blog.uliejh.cn/snews/184881.htm
- http://m.blog.uliejh.cn/snews/645471.htm
- http://m.blog.uliejh.cn/snews/36854.htm
- http://m.blog.uliejh.cn/snews/030701.htm
- http://m.blog.uliejh.cn/snews/8254.htm
- http://m.blog.uliejh.cn/snews/18635.htm
- http://m.blog.uliejh.cn/snews/76925.htm
- http://m.blog.uliejh.cn/snews/8451.htm
- http://m.blog.uliejh.cn/snews/5392102.htm
- http://m.blog.uliejh.cn/snews/15340.htm
- http://m.blog.uliejh.cn/snews/0282.htm
- http://m.blog.uliejh.cn/snews/7796927.htm
- http://m.blog.uliejh.cn/snews/0290.htm
- http://m.blog.uliejh.cn/snews/728996.htm
- http://m.blog.uliejh.cn/snews/121846.htm
- http://m.blog.uliejh.cn/snews/10553.htm
- http://m.blog.uliejh.cn/snews/1740409.htm
- http://m.blog.uliejh.cn/snews/6575454.htm
- http://m.blog.uliejh.cn/snews/8287.htm
- http://m.blog.uliejh.cn/snews/2531123.htm
- http://m.blog.uliejh.cn/snews/15859.htm
- http://m.blog.uliejh.cn/snews/0805227.htm
- http://m.blog.uliejh.cn/snews/6630100.htm
- http://m.blog.uliejh.cn/snews/4453800.htm
- http://m.blog.uliejh.cn/snews/219757.htm
- http://m.blog.uliejh.cn/snews/492991.htm
- http://m.blog.uliejh.cn/snews/012383.htm
- http://m.blog.uliejh.cn/snews/6079723.htm
- http://m.blog.uliejh.cn/snews/546444.htm
- http://m.blog.uliejh.cn/snews/894016.htm
- http://m.blog.uliejh.cn/snews/3479.htm
- http://m.blog.uliejh.cn/snews/9028.htm
- http://m.blog.uliejh.cn/snews/570035.htm
- http://m.blog.uliejh.cn/snews/6337.htm
- http://m.blog.uliejh.cn/snews/54948.htm
- http://m.blog.uliejh.cn/snews/28085.htm
- http://m.blog.uliejh.cn/snews/9835.htm
- http://m.blog.uliejh.cn/snews/7642665.htm
- http://m.blog.uliejh.cn/snews/685505.htm
- http://m.blog.uliejh.cn/snews/55252.htm
- http://m.blog.uliejh.cn/snews/47893.htm
- http://m.blog.uliejh.cn/snews/0405.htm
- http://m.blog.uliejh.cn/snews/1043959.htm
- http://m.blog.uliejh.cn/snews/243190.htm
- http://m.blog.uliejh.cn/snews/5959.htm
- http://m.blog.uliejh.cn/snews/086111.htm
- http://m.blog.uliejh.cn/snews/785964.htm
- http://m.blog.uliejh.cn/snews/9595349.htm
- http://m.blog.uliejh.cn/snews/711226.htm
- http://m.blog.uliejh.cn/snews/671102.htm
- http://m.blog.uliejh.cn/snews/55212.htm
- http://m.blog.uliejh.cn/snews/5460083.htm
- http://m.blog.uliejh.cn/snews/9873.htm
- http://m.blog.uliejh.cn/snews/696670.htm
- http://m.blog.uliejh.cn/snews/228292.htm
- http://m.blog.uliejh.cn/snews/95152.htm
- http://m.blog.uliejh.cn/snews/9560675.htm
- http://m.blog.uliejh.cn/snews/683232.htm
- http://m.blog.uliejh.cn/snews/178829.htm
- http://m.blog.uliejh.cn/snews/8480.htm
- http://m.blog.uliejh.cn/snews/33105.htm
- http://m.blog.uliejh.cn/snews/2991.htm
- http://m.blog.uliejh.cn/snews/5916.htm
- http://m.blog.uliejh.cn/snews/586742.htm
- http://m.blog.uliejh.cn/snews/02405.htm
- http://m.blog.uliejh.cn/snews/5884.htm
- http://m.blog.uliejh.cn/snews/12222.htm
- http://m.blog.uliejh.cn/snews/8577.htm
- http://m.blog.uliejh.cn/snews/7056982.htm
- http://m.blog.uliejh.cn/snews/3223760.htm
- http://m.blog.uliejh.cn/snews/015808.htm
- http://m.blog.uliejh.cn/snews/243041.htm
- http://m.blog.uliejh.cn/snews/746584.htm
- http://m.blog.uliejh.cn/snews/717092.htm
- http://m.blog.uliejh.cn/snews/7300.htm
- http://m.blog.uliejh.cn/snews/037430.htm
- http://m.blog.uliejh.cn/snews/1032.htm
- http://m.blog.uliejh.cn/snews/719273.htm
- http://m.blog.uliejh.cn/snews/5608.htm
- http://m.blog.uliejh.cn/snews/3000853.htm
- http://m.blog.uliejh.cn/snews/424162.htm
- http://m.blog.uliejh.cn/snews/9324.htm
- http://m.blog.uliejh.cn/snews/125902.htm
- http://m.blog.uliejh.cn/snews/6545268.htm
- http://m.blog.uliejh.cn/snews/806688.htm
- http://m.blog.uliejh.cn/snews/327150.htm
- http://m.blog.uliejh.cn/snews/29110.htm
- http://m.blog.uliejh.cn/snews/78570.htm
- http://m.blog.uliejh.cn/snews/8863533.htm
- http://m.blog.uliejh.cn/snews/3428.htm
- http://m.blog.uliejh.cn/snews/7731288.htm
- http://m.blog.uliejh.cn/snews/2549418.htm
- http://m.blog.uliejh.cn/snews/3735177.htm
- http://m.blog.uliejh.cn/snews/696233.htm
- http://m.blog.uliejh.cn/snews/877649.htm
- http://m.blog.uliejh.cn/snews/881172.htm
- http://m.blog.uliejh.cn/snews/7212140.htm
- http://m.blog.uliejh.cn/snews/650142.htm
- http://m.blog.uliejh.cn/snews/8933.htm
- http://m.blog.uliejh.cn/snews/592201.htm
- http://m.blog.uliejh.cn/snews/9174933.htm
- http://m.blog.uliejh.cn/snews/73789.htm
- http://m.blog.uliejh.cn/snews/0163617.htm
- http://m.blog.uliejh.cn/snews/3161759.htm
- http://m.blog.uliejh.cn/snews/488462.htm
- http://m.blog.uliejh.cn/snews/57923.htm
- http://m.blog.uliejh.cn/snews/2049.htm
- http://m.blog.uliejh.cn/snews/225560.htm
- http://m.blog.uliejh.cn/snews/8289042.htm
- http://m.blog.uliejh.cn/snews/065908.htm
- http://m.blog.uliejh.cn/snews/4329539.htm
- http://m.blog.uliejh.cn/snews/1520.htm
- http://m.blog.uliejh.cn/snews/1329.htm
- http://m.blog.uliejh.cn/snews/7777622.htm
- http://m.blog.uliejh.cn/snews/3121.htm
- http://m.blog.uliejh.cn/snews/317082.htm
- http://m.blog.uliejh.cn/snews/50675.htm
- http://m.blog.uliejh.cn/snews/228853.htm
- http://m.blog.uliejh.cn/snews/4936797.htm
- http://m.blog.uliejh.cn/snews/0021033.htm
- http://m.blog.uliejh.cn/snews/47555.htm
- http://m.blog.uliejh.cn/snews/2970007.htm
- http://m.blog.uliejh.cn/snews/8612.htm
- http://m.blog.uliejh.cn/snews/07664.htm
- http://m.blog.uliejh.cn/snews/5447523.htm
- http://m.blog.uliejh.cn/snews/4709.htm
- http://m.blog.uliejh.cn/snews/52242.htm
- http://m.blog.uliejh.cn/snews/059206.htm
- http://m.blog.uliejh.cn/snews/92544.htm
- http://m.blog.uliejh.cn/snews/2309.htm
- http://m.blog.uliejh.cn/snews/96986.htm
- http://m.blog.uliejh.cn/snews/33390.htm
- http://m.blog.uliejh.cn/snews/749116.htm
- http://m.blog.uliejh.cn/snews/478174.htm
- http://m.blog.uliejh.cn/snews/00184.htm
- http://m.blog.uliejh.cn/snews/551991.htm
- http://m.blog.uliejh.cn/snews/16944.htm
- http://m.blog.uliejh.cn/snews/0080.htm
- http://m.blog.uliejh.cn/snews/1916.htm
- http://m.blog.uliejh.cn/snews/853886.htm
- http://m.blog.uliejh.cn/snews/2591928.htm
- http://m.blog.uliejh.cn/snews/68289.htm
- http://m.blog.uliejh.cn/snews/953116.htm
- http://m.blog.uliejh.cn/snews/700332.htm
- http://m.blog.uliejh.cn/snews/368641.htm
- http://m.blog.uliejh.cn/snews/085275.htm
- http://m.blog.uliejh.cn/snews/1767143.htm
- http://m.blog.uliejh.cn/snews/787966.htm
- http://m.blog.uliejh.cn/snews/023654.htm
- http://m.blog.uliejh.cn/snews/6294.htm
- http://m.blog.uliejh.cn/snews/955317.htm
- http://m.blog.uliejh.cn/snews/520371.htm
- http://m.blog.uliejh.cn/snews/957274.htm
- http://m.blog.uliejh.cn/snews/3007.htm
- http://m.blog.uliejh.cn/snews/3809744.htm
- http://m.blog.uliejh.cn/snews/3466729.htm
- http://m.blog.uliejh.cn/snews/2906261.htm
- http://m.blog.uliejh.cn/snews/9501.htm
- http://m.blog.uliejh.cn/snews/5619.htm
- http://m.blog.uliejh.cn/snews/6821456.htm
- http://m.blog.uliejh.cn/snews/8653552.htm
- http://m.blog.uliejh.cn/snews/72580.htm
- http://m.blog.uliejh.cn/snews/960361.htm
- http://m.blog.uliejh.cn/snews/680323.htm
- http://m.blog.uliejh.cn/snews/6627629.htm
- http://m.blog.uliejh.cn/snews/2482790.htm
- http://m.blog.uliejh.cn/snews/535156.htm
- http://m.blog.uliejh.cn/snews/1602453.htm
- http://m.blog.uliejh.cn/snews/92165.htm
- http://m.blog.uliejh.cn/snews/66189.htm
- http://m.blog.uliejh.cn/snews/72514.htm
- http://m.blog.uliejh.cn/snews/557575.htm
- http://m.blog.uliejh.cn/snews/5753897.htm
- http://m.blog.uliejh.cn/snews/73618.htm
- http://m.blog.uliejh.cn/snews/148871.htm
- http://m.blog.uliejh.cn/snews/47752.htm
- http://m.blog.uliejh.cn/snews/919178.htm
- http://m.blog.uliejh.cn/snews/4064337.htm
- http://m.blog.uliejh.cn/snews/9211.htm
- http://m.blog.uliejh.cn/snews/6140.htm
- http://m.blog.uliejh.cn/snews/182988.htm
- http://m.blog.uliejh.cn/snews/4247754.htm
- http://m.blog.uliejh.cn/snews/62027.htm
- http://m.blog.uliejh.cn/snews/81209.htm
- http://m.blog.uliejh.cn/snews/3937084.htm
- http://m.blog.uliejh.cn/snews/0967411.htm
- http://m.blog.uliejh.cn/snews/383341.htm
- http://m.blog.uliejh.cn/snews/5390.htm
- http://m.blog.uliejh.cn/snews/7251220.htm
- http://m.blog.uliejh.cn/snews/707382.htm
- http://m.blog.uliejh.cn/snews/434573.htm
- http://m.blog.uliejh.cn/snews/6575138.htm
- http://m.blog.uliejh.cn/snews/4239.htm
- http://m.blog.uliejh.cn/snews/957232.htm
- http://m.blog.uliejh.cn/snews/3867953.htm
- http://m.blog.uliejh.cn/snews/3267.htm
- http://m.blog.uliejh.cn/snews/02844.htm
- http://m.blog.uliejh.cn/snews/751917.htm
- http://m.blog.uliejh.cn/snews/4186.htm
- http://m.blog.uliejh.cn/snews/375110.htm
- http://m.blog.uliejh.cn/snews/460172.htm
- http://m.blog.uliejh.cn/snews/2328.htm
- http://m.blog.uliejh.cn/snews/232811.htm
- http://m.blog.uliejh.cn/snews/72676.htm
- http://m.blog.uliejh.cn/snews/3912150.htm
- http://m.blog.uliejh.cn/snews/5450338.htm
- http://m.blog.uliejh.cn/snews/0430859.htm
- http://m.blog.uliejh.cn/snews/4599741.htm
- http://m.blog.uliejh.cn/snews/4972847.htm
- http://m.blog.uliejh.cn/snews/0010108.htm
- http://m.blog.uliejh.cn/snews/807670.htm
- http://m.blog.uliejh.cn/snews/35606.htm
- http://m.blog.uliejh.cn/snews/1266.htm
- http://m.blog.uliejh.cn/snews/027465.htm
- http://m.blog.uliejh.cn/snews/309935.htm
- http://m.blog.uliejh.cn/snews/5178.htm
- http://m.blog.uliejh.cn/snews/4298.htm
- http://m.blog.uliejh.cn/snews/8590125.htm
- http://m.blog.uliejh.cn/snews/882298.htm
- http://m.blog.uliejh.cn/snews/7687185.htm
- http://m.blog.uliejh.cn/snews/5837198.htm
- http://m.blog.uliejh.cn/snews/5067374.htm
- http://m.blog.uliejh.cn/snews/47195.htm

## 项目结构

```
weblink-navigator/
├── src/                           # 源代码主目录
│   ├── core/                      # 核心逻辑模块
│   │   ├── indexer.js             # 索引构建器，解析 links.json 生成倒排索引
│   │   ├── fetcher.js             # 元数据抓取器，负责请求外部页面并提取信息
│   │   └── validator.js           # 链接校验器，检测 URL 格式与存活状态
│   ├── web/                       # 前端资源目录
│   │   ├── assets/                # 静态资源文件
│   │   │   ├── css/               # 样式表，含主题变量与响应式布局
│   │   │   ├── js/                # 客户端脚本，含搜索、渲染与交互逻辑
│   │   │   └── images/            # 图标与占位图
│   │   ├── templates/             # HTML 模板片段
│   │   │   ├── header.html        # 全局头部导航
│   │   │   ├── footer.html        # 页脚与版权信息
│   │   │   └── card.html          # 单条链接的卡片渲染模板
│   │   └── pages/                 # 生成的静态页面输出目录
│   ├── cli/                       # 命令行工具入口
│   │   ├── build.js               # 构建命令实现
│   │   ├── serve.js               # 开发服务器启动命令
│   │   └── import.js              # 批量导入命令
│   └── lib/                       # 通用工具函数
│       ├── logger.js              # 日志记录器，支持分级输出
│       └── config.js              # 配置加载器，读取环境变量与默认值
├── data/                          # 数据存储目录
│   ├── links.json                 # 主链接数据文件，包含所有收录的 URL 与元数据
│   ├── tags.json                  # 标签定义文件，包含分类层级与显示名称
│   └── archive/                   # 历史版本归档
├── scripts/                       # 辅助脚本
│   ├── cron-fetch.sh              # 定时抓取任务脚本，由 GitHub Actions 触发
│   ├── health-check.sh            # 链接存活批量检测脚本
│   └── export-csv.sh              # 导出为 CSV 格式的转换脚本
├── tests/                         # 单元测试与集成测试
│   ├── unit/                      # 单元测试用例，覆盖核心模块
│   └── fixtures/                  # 测试用固定数据集
├── docs/                          # 项目文档
│   ├── user-guide/                # 用户手册
│   ├── admin-guide/               # 管理员指南
│   └── developer-guide/           # 开发者文档
├── .github/                       # GitHub 工作流配置
│   └── workflows/                 # CI/CD 流水线定义
├── docker/                        # Docker 构建上下文
│   ├── Dockerfile                 # 镜像构建文件
│   └── nginx.conf                 # 容器内 Nginx 配置
├── package.json                   # 项目依赖清单与脚本定义
├── package-lock.json              # 依赖版本锁定文件
├── .eslintrc.js                   # 代码规范检查配置
├── .prettierrc                    # 代码格式化配置
└── README.md                      # 项目说明文档（本文件）
```

## 贡献指南

1. 复刻本仓库至个人账户，并在本地克隆复刻后的副本。创建新的功能分支，分支命名应遵循 `feature/描述` 或 `fix/描述` 格式，例如 `feature/add-pagination-support`。

2. 在 `data/links.json` 中按照既定的 JSON Schema 添加新的链接记录，每条记录必须包含 `url`、`title`、`description` 与 `tags` 字段。若新增标签，需同步更新 `data/tags.json` 中的定义。

3. 在本地运行 `npm run build` 验证构建流程是否通过，并启动开发服务器 `npm start` 检查新增链接在前端页面的渲染效果。确保所有已有功能未出现回归性错误。

4. 编写或更新对应的单元测试文件，放置于 `tests/unit/` 目录下。对于新增功能，需提供覆盖主要逻辑分支的测试用例。执行 `npm test` 确认全部测试通过。

5. 提交变更并推送至复刻仓库，随后向本仓库发起 Pull Request。PR 描述中应清晰说明变更内容、动机与测试结果。维护者将在 48 小时内进行代码审查，审查通过后合并至主分支。

## 常见问题

**问：links.json 中的数据量增长后，构建速度是否会明显下降？**

答：构建过程采用增量索引策略，仅对新增或修改的记录重新计算倒排索引项，而非全量重建。在实测中，当链接数量达到 5000 条时，完整构建耗时约为 2.3 秒，增量构建耗时在 300 毫秒以内。建议定期归档历史链接至 `data/archive/` 目录以保持主文件规模可控。若仍需优化，可启用 SQLite 缓存层，将索引结果持久化存储。

**问：如何自定义前端主题配色，或添加新的页面布局？**

答：主题变量定义于 `src/web/assets/css/themes.css` 文件中，采用 CSS 自定义属性实现。修改 `--color-primary`、`--color-background` 等变量即可全局调整配色。如需新增页面布局，请在 `src/web/templates/` 下创建新的 HTML 模板片段，并在 `src/web/assets/js/router.js` 中注册对应的路由规则。所有模板采用 Mustache 语法进行数据渲染，支持条件判断与列表循环。

**问：元数据抓取功能对目标站点的访问频率如何控制？**

答：抓取脚本内置了基于令牌桶算法的限流器，默认每秒最多发送 5 个请求，且对同一域名在 60 秒内的请求总数不超过 30 次。所有请求头中均携带 `User-Agent: WebLink-Navigator/1.0 (+https://github.com/weblink-navigator)` 标识，并尊重目标站点 robots.txt 中的 Crawl-delay 指令。若需要调整限流参数，可在 `scripts/cron-fetch.sh` 中修改 `RATE_LIMIT` 与 `BURST_SIZE` 环境变量。

## 许可证

MIT

> 外链数量: 250 | 生成时间: 2026-08-24 23:41:18
