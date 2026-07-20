# Olive Resource Index

Olive 是一个面向开发者的技术资源外链汇总与导航工具，定位于将分散在多个仓库、文档站点和外部平台的高质量技术资料进行集中索引与分类管理。项目目标用户包括技术调研人员、架构师、开源贡献者以及需要系统化查阅特定技术主题的研发团队。Olive 本身不存储具体内容文件，而是通过维护一个结构化 Markdown 索引库，将外部资源链接按主题、粒度、成熟度等维度进行标注和组织，解决开发者在信息检索过程中面临的链接失效、上下文缺失、重复查找等痛点问题。

## 功能概览

- 分层索引体系：基于目录结构和命名规范，将资源链接按主题域（如性能工程、前端构建、数据可视化等）进行一级分类，每个分类目录下维护独立的 README 或索引表。
- 资源元数据标注：每个外链条目支持必填字段包括资源标题、简要描述、文件格式（如 PDF、Markdown、交互式页面）、最后验证时间，便于后续自动化检查链接有效性。
- 多粒度检索入口：提供按技术栈、按应用场景、按作者/组织、按更新时间四种检索维度，每个维度对应独立的索引文件。
- 链接健康检查钩子：项目内置简单的 Shell 脚本，利用 curl 和 grep 对索引中的 HTTP 状态码进行批量检查，输出失效链接报告。
- 版本化快照引用：对于关键外部资源，支持引用 Internet Archive 或 WebCite 快照链接作为备选，降低单点依赖风险。
- 协作式更新流程：通过 Pull Request 模板和 Issue 表单，引导贡献者提交新链接、报告失效链接或更新元数据，所有变更保留 Git 历史记录。
- 本地离线预览：项目提供轻量级 Python HTTP 服务器启动脚本，可在本地以静态站点形式预览索引结构，方便审查变更。
- 与主流文档生成工具集成：索引数据可被 MkDocs、VuePress 或 Docusaurus 通过自定义解析脚本消费，快速生成在线导航站点。

## 应用场景

场景一：技术选型调研。架构师在评估多个消息队列中间件时，可通过 Olive 的“消息系统”分类索引，快速获取官方文档、性能测试报告、社区最佳实践和已知缺陷分析等外部链接，避免重复搜索。

场景二：新人入职学习路径规划。团队技术 Leader 可将 Olive 中标记为“入门级”且按模块组织的资源链接序列，直接作为新员工第一周的自学路线图，配合每周同步检查学习进度。

场景三：开源项目依赖文档聚合。开源项目维护者可将 Olive 作为项目 Wiki 的补充，集中存放所有依赖库的官方文档、迁移指南、安全公告等外链，降低维护多个仓库文档时的同步成本。

场景四：技术会议与演讲资料归档。会后组织者可将讲师允许公开的幻灯片、示例代码仓库、录制视频链接等通过 Olive 统一索引，并附加会议名称、日期、场次等元数据，方便后续查阅。

## 快速开始

以下命令将完成 Olive 索引库的克隆、基础依赖安装，并启动本地预览服务。

```bash
# 克隆项目仓库
git clone https://github.com/zerxonhy/olive.git
cd olive

# 安装链接健康检查工具依赖（基于 Debian/Ubuntu 环境）
# 若使用其他系统，请确保已安装 curl、grep、awk
sudo apt-get update && sudo apt-get install -y curl grep coreutils

# 运行链接状态检查脚本（示例检查 marble 系列资源）
bash scripts/check-links.sh marble*.md

# 启动本地静态预览服务（Python 3）
python3 -m http.server 8000 --directory ./docs
# 浏览器访问 http://localhost:8000 查看索引导航
```

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|---|---|---|
| Git | 2.20 及以上 | 用于克隆仓库、提交变更、查看历史记录 |
| Bash | 4.0 及以上 | 运行链接检查脚本和辅助工具脚本 |
| curl | 7.68 及以上 | 发送 HTTP 请求以验证链接有效性 |
| Python | 3.6 及以上 | 仅用于启动本地静态预览服务器，非运行时必需 |
| grep | 3.4 及以上 | 配合 curl 解析响应状态码与重定向信息 |
| awk | 5.0 及以上 | 用于处理链接列表的文本过滤与格式化 |

## 文档导航

| 层面 | 目录/文件 | 回答的问题 |
|---|---|---|
| 用户入门 | docs/guides/getting-started.md | 如何第一次使用 Olive 索引库查找资源、如何理解目录分类规则 |
| 贡献操作 | CONTRIBUTING.md | 如何提交新链接、如何更新元数据、PR 标题与分支规范是什么 |
| 索引元数据规范 | docs/schemas/resource-schema.yaml | 每个资源条目需要填写哪些字段、字段类型与约束条件 |
| 运维与自动化 | scripts/README.md | 如何运行链接检查、如何生成失效报告、如何集成到 CI 流水线 |
| 设计决策 | docs/design-decisions.md | 为什么选择纯 Markdown + Git 而非数据库、为什么按主题而非时间组织 |

## 资源列表

- https://github.com/zerxonhy/olive/blob/main/marbleamber.md
- https://github.com/zerxonhy/olive/blob/main/marblegolden.md
- https://github.com/zerxonhy/olive/blob/main/marblejade.md
- https://github.com/zerxonhy/olive/blob/main/marblelantern.md
- https://github.com/zerxonhy/olive/blob/main/marblepixel.md
- https://github.com/zerxonhy/olive/blob/main/marblesignal.md

## 项目结构

```
olive/
├── .github/                         # GitHub 社区配置文件
│   ├── ISSUE_TEMPLATE/              # 问题模板：链接失效/新链接申请
│   └── PULL_REQUEST_TEMPLATE.md     # PR 描述模板，引导填写元数据变更
├── categories/                      # 按技术领域划分的一级分类目录
│   ├── frontend/                    # 前端工程化与框架相关索引
│   ├── backend/                     # 后端服务、API 设计、性能优化
│   ├── data/                        # 数据工程、可视化、存储方案
│   ├── ops/                         # 运维监控、可观测性、容器编排
│   └── security/                    # 安全审计、加密、身份认证
├── docs/                            # 项目文档与用户指南
│   ├── guides/                      # 操作教程，含截图示例
│   ├── schemas/                     # 资源条目字段定义的 JSON Schema
│   └── design-decisions.md          # 关键设计权衡记录
├── scripts/                         # 工具脚本目录
│   ├── check-links.sh               # 批量检查索引中的 HTTP 状态
│   ├── generate-report.sh           # 从检查结果生成 Markdown 报告
│   └── validate-schema.py           # 验证资源条目是否符合元数据规范
├── marbleamber.md                   # 第 1 个索引资源（示例主题）
├── marblegolden.md                  # 第 2 个索引资源（示例主题）
├── marblejade.md                    # 第 3 个索引资源（示例主题）
├── marblelantern.md                 # 第 4 个索引资源（示例主题）
├── marblepixel.md                   # 第 5 个索引资源（示例主题）
├── marblesignal.md                  # 第 6 个索引资源（示例主题）
├── LICENSE                          # MIT 许可证全文
├── README.md                        # 项目总体说明（本文件）
└── .gitignore                       # 忽略本地预览缓存与临时文件
```

## 贡献指南

1. 阅读 CONTRIBUTING.md 文件，了解索引条目元数据字段定义、分类目录选择规则以及 Markdown 格式规范。所有新增或修改的资源条目必须严格遵循该规范，否则 PR 将无法通过初审。

2. 在本地仓库中基于 main 分支创建新的功能分支，分支命名采用 `feat/add-resource-<短名称>` 或 `fix/update-link-<短名称>` 格式。确保分支名称简洁描述变更内容。

3. 执行 `scripts/check-links.sh` 脚本验证新增或变更的所有外部链接返回状态码为 200（或 301/302 重定向至有效目标），并将检查结果截图或日志附加到 PR 描述中，以证明链接可达性。

4. 提交 Pull Request 时，使用 .github/PULL_REQUEST_TEMPLATE.md 提供的模板，完整填写变更类型、影响的索引文件列表、是否破坏性变更以及测试步骤。如果 PR 涉及多个资源条目，建议拆分提交以便逐条审查。

5. 等待项目维护者审核。审核期间可能被要求补充资源描述、调整分类或提供更多上下文信息。所有讨论与修改记录保留在 PR 评论区，最终由维护者执行 squash merge。

## 常见问题

问：Olive 索引库中的链接如果失效了怎么办？

答：每个索引条目均包含“最后验证时间”字段。项目维护者每季度通过 GitHub Actions 定时任务运行全量链接检查，自动生成失效链接报告并创建 Issue 标记。用户也可随时通过 Issue 模板报告失效链接，贡献者可按贡献指南提交 PR 更新链接或替换为有效快照。

问：我可以提交非技术类或商业推广性质的链接吗？

答：Olive 严格限定为高质量技术内容索引，包括但不限于开源项目文档、学术预印本、官方技术博客、公认的技术社区深度文章。商业推广、软文、个人无实质内容站点、需要付费订阅且无公开摘要的资源不予收录。提交前请参考 docs/design-decisions.md 中“收录范围边界”一节。

问：我如何在自己的项目中使用 Olive 的索引结构？

答：Olive 采用 MIT 许可证，您可以直接 fork 本仓库并替换 index 文件中的链接内容，保留元数据字段定义。如果您希望以编程方式读取索引数据，可以使用 docs/schemas/resource-schema.yaml 中定义的规范，配合 Python 或 Node.js 解析 Markdown 表格与 YAML Frontmatter。具体示例脚本请参考 scripts/parse-index.py（将于后续版本提供）。

## 许可证

MIT

> 外链数量: 6 | 生成时间: 2026-07-21 05:13:25
