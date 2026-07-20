# Olive 技术资源导航站

Olive 是一个面向开发者与运维人员的轻量级技术资源外链汇总与快速导航系统。项目定位于将分散在 GitHub 仓库、技术博客、官方文档中的优质外部链接进行集中化、分类化、可检索化管理，解决开发团队或个人在查阅技术资料时频繁切换上下文、链接散落丢失、版本信息不一致等问题。Olive 本身不存储文档内容，仅提供索引与引用编排能力，适用于作为团队内部技术文档门户的前置导航层，或作为个人开发环境的书签增强替代方案。

## 功能概览

- 外链统一入库与分类标记：支持对任意 HTTPS/HTTP 外部链接添加分类标签、适用版本与简要描述，支持批量导入。

- 可配置的导航目录结构：通过 YAML 配置文件定义多级导航菜单，菜单项可绑定外部链接或本地相对路径，支持按项目、按语言、按阶段筛选。

- 只读静态生成模式：默认构建为纯静态 HTML 页面，无需数据库或后端服务，可直接托管于 GitHub Pages、对象存储或内网 Web 服务器。

- 外部链接健康检查：每日定时检测已收录外链的可达性与响应状态码，对失效链接标记警告并发送通知（支持 Webhook）。

- 全文检索与快速跳转：集成页面内模糊搜索，支持按标题、描述、域名、标签进行实时过滤，并支持键盘快捷键快速定位。

- 访问统计与引用追溯：记录各外链的点击次数与最近访问时间，数据本地化存储，不依赖第三方分析平台。

- 基于 Git 的版本管理：所有配置与链接变更均通过 Git 提交记录追溯，支持回滚、分支开发与 PR 审核流程。

- 开放 API 查询接口：提供只读 JSON API，支持按 ID、分类、关键字查询已收录链接，便于与其他内部工具集成。

## 应用场景

开发团队内部文档聚合：团队在多个代码仓库中分散存放技术设计文档、部署手册、API 规范，Olive 可将这些仓库中的 Markdown 文件链接统一收录，并按业务模块组织成导航页面，减少成员查找时间。

个人技术栈知识库维护：开发者个人维护多个技术栈（如 Kubernetes、React、Rust），通过 Olive 将官方文档、社区教程、最佳实践博客、视频教程等外链统一收藏，并添加个人备注与阅读状态，形成可检索的知识索引。

离线环境下的链接映射管理：在隔离内网或离线开发环境中，外部官方源不可直接访问。Olive 支持将外链映射为内网代理地址或本地镜像路径，并提供清晰的映射表，便于运维人员统一配置反向代理规则。

技术文档版本升级影响分析：当某一依赖框架发布大版本更新时，Olive 可按标签筛选出所有引用旧版本文档的外链，协助团队评估文档更新范围。

## 快速开始

以下命令适用于 Linux / macOS / Windows WSL 环境，要求已安装 Git 与 Node.js 18+。

```bash
# 克隆项目仓库
git clone https://github.com/zerxonhy/olive.git
cd olive

# 安装项目依赖（使用 npm）
npm install

# 执行本地开发构建，生成静态站点至 dist/ 目录
npm run build

# 启动本地预览服务器，监听 http://localhost:8080
npm run serve
```

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|---------|---------|------|
| Node.js | 18.0.0 或更高 | 运行时环境，用于执行构建脚本与 API 服务 |
| npm | 9.0.0 或更高 | 包管理器，用于安装依赖与执行脚本命令 |
| Git | 2.30.0 或更高 | 版本控制，用于克隆仓库及提交配置变更 |
| 操作系统 | Linux / macOS / Windows (WSL2) | 开发与部署环境，生产推荐使用 Linux |
| 网络访问 | 可访问公网或内网镜像源 | 用于构建时检查外链可达性（可配置代理） |
| 磁盘空间 | 至少 200 MB | 包含源码、依赖及构建产物 |
| 内存 | 至少 1 GB | 构建过程中静态页面生成与检索索引构建所需 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|------|------|-----------|
| 入门 | /docs/quick-start.md | 如何快速配置第一个导航分类并添加外链？ |
| 配置 | /docs/configuration.md | 导航菜单、标签体系、健康检查参数如何配置？ |
| 扩展 | /docs/api-reference.md | 如何通过 REST API 查询链接库与统计信息？ |
| 运维 | /docs/deployment-guide.md | 支持哪些部署方式（静态托管、Docker、反向代理）？ |
| 贡献 | /CONTRIBUTING.md | 如何提交新外链推荐、修复失效链接或改进文档？ |
| 版本 | /CHANGELOG.md | 每个版本新增了哪些功能、修复了哪些缺陷？ |

## 资源列表

- https://github.com/zerxonhy/olive/blob/main/silverhorizon.md
- https://github.com/zerxonhy/olive/blob/main/silverisland.md
- https://github.com/zerxonhy/olive/blob/main/summitfield.md
- https://github.com/zerxonhy/olive/blob/main/timberbright.md
- https://github.com/zerxonhy/olive/blob/main/timbercoral.md
- https://github.com/zerxonhy/olive/blob/main/timbersaffron.md

## 项目结构

```
olive/
├── config/                           # 核心配置目录
│   ├── navigation.yaml               # 导航菜单结构定义（层级、标题、外链映射）
│   ├── categories.yaml               # 分类与标签体系定义
│   └── health-check.yaml             # 健康检查频率、超时、通知 Webhook 配置
├── src/
│   ├── core/                         # 核心构建引擎
│   │   ├── collector.js              # 外链收集与去重模块
│   │   ├── generator.js              # 静态 HTML 页面生成器
│   │   └── indexer.js               # 全文检索索引构建器
│   ├── api/                          # 只读 JSON API 实现
│   │   ├── server.js                 # 基于 Express 的 API 服务入口
│   │   └── routes/                   # 按资源类型路由（links, categories, stats）
│   ├── cli/                          # 命令行工具入口
│   │   ├── build.js                  # 构建命令实现
│   │   ├── check.js                  # 手动触发健康检查命令
│   │   └── serve.js                  # 本地预览服务命令
│   └── templates/                    # 页面模板引擎
│       ├── layout.ejs                # 基础 HTML 骨架
│       ├── index.ejs                 # 首页导航视图
│       └── search.ejs                # 搜索结果页视图
├── public/                           # 静态资源目录
│   ├── css/                          # 主题样式（默认暗色/亮色自适应）
│   ├── js/                           # 前端交互（搜索、键盘快捷键、统计展示）
│   └── assets/                       # 图标、Logo 等媒体文件
├── data/                             # 运行时数据存储（不纳入 Git，或仅示例）
│   ├── links.db.json                 # 外链主数据（标题、URL、分类、标签、备注）
│   ├── health-logs.json              # 历史健康检查记录（保留最近 30 天）
│   └── click-stats.json              # 点击计数与时间戳
├── dist/                             # 构建输出目录（生成后部署此目录）
│   ├── index.html                    # 首页生成文件
│   ├── search.html                   # 搜索结果页
│   └── api/                          # API 路由静态 JSON 端点（可选）
├── tests/                            # 单元测试与集成测试
│   ├── collector.test.js
│   ├── generator.test.js
│   └── api.test.js
├── docs/                             # 项目文档（面向用户）
│   ├── quick-start.md
│   ├── configuration.md
│   ├── api-reference.md
│   └── deployment-guide.md
├── .gitignore
├── package.json                      # npm 依赖与脚本定义
├── README.md                         # 项目主页（当前文件）
└── LICENSE                           # MIT 许可证文本
```

## 贡献指南

提交外链推荐或修复失效链接：在 `data/links.db.json` 中按格式添加或修改条目，字段包括 `id`、`title`、`url`、`category`、`tags`、`version`、`status`，然后提交 Pull Request。新增外链需确保 URL 可访问且内容与分类相符。

完善文档或翻译：在 `docs/` 目录下修改对应的 Markdown 文件，遵循英文或中文技术文档写作惯例。文档变更应附带至少一个使用示例或配置片段，便于读者理解。

报告缺陷或提议功能：使用 GitHub Issues 模板提交，需包含复现步骤、预期行为与实际行为、运行环境信息（Node 版本、操作系统、构建命令）。功能提议需说明应用场景与优先级依据。

改进构建性能或 API 响应效率：针对 `src/core/` 或 `src/api/` 中的模块进行优化，需提供基准测试数据对比（如构建时间、内存占用、API 延迟），并确保所有现有测试用例通过。

参与健康检查插件开发：健康检查模块支持自定义协议检测（HTTP、HTTPS、TCP 端口）。如需新增检测方式，请在 `src/core/health-check.js` 中扩展插件接口，并附带单元测试覆盖。

## 常见问题

Q: Olive 是否支持私有仓库或需要登录认证的外链？

A: 不支持。Olive 设计为纯前端静态导航，无法处理需要 Cookie、Token 或 Session 认证的页面。对于私有资源，建议将内网代理地址或镜像地址作为外链收录，并配合 IP 白名单或 VPN 访问控制。

Q: 健康检查显示链接失效，但我确认在浏览器中可以正常打开，是什么原因？

A: 可能原因包括：目标站点启用了反爬机制（如 Cloudflare 五秒盾）、检测服务器 IP 被目标防火墙拦截、目标站点要求特定的 User-Agent 头。您可以在 `config/health-check.yaml` 中自定义请求头（如 `User-Agent: OliveBot`）或增加超时时间。若仍无效，可将该链接加入健康检查白名单，跳过自动检测。

Q: 如何将 Olive 部署到内网且不依赖任何外部 CDN？

A: 构建命令 `npm run build` 默认会生成所有静态文件到 `dist/` 目录，包括 CSS 与 JavaScript。您需要将所有第三方库（如字体、图标库）的引用切换为内网镜像或本地路径。具体操作步骤请参阅 `docs/deployment-guide.md` 中的「完全离线部署」章节，该章节提供了替换 CDN 资源的详细脚本。

## 许可证

MIT

> 外链数量: 6 | 生成时间: 2026-07-21 05:13:43
