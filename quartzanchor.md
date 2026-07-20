# Olive Index

Olive Index 是一个面向开发人员、技术研究人员与开源生态参与者的结构化外链与资源导航系统。该项目不提供代码托管或内容聚合服务，而是通过人工筛选与语义化分类，将分散于网络各处的高质量技术文档、项目公告、深度分析文章与社区讨论入口整合为统一的索引视图。Olive Index 的目标用户包括需要快速追踪特定技术栈演进状态的中高级工程师、需要为团队建立内部知识库入口的架构师，以及希望降低信息噪音、提升阅读信噪比的技术决策者。该项目通过维护一批稳定更新的 Markdown 入口文件，解决了技术阅读中信息源碎片化、关键内容被低质量转载淹没、以及跨仓库资源难以追溯原始出处等问题。

## 功能概览

- 结构化入口索引：每个资源条目以独立 Markdown 文件形式存储，包含资源标题、原始链接、内容摘要、关键词标签与最后验证时间，便于脚本化处理与静态站点生成。

- 语义化分类层级：基于资源所涉技术领域、文档类型（如白皮书、API 参考、变更日志）与成熟度阶段（孵化、稳定、废弃）建立三级分类体系，支持快速过滤。

- 自动化链接健康检查：内置基于 GitHub Actions 的周期性链接检查工作流，自动标记返回码非 200 或响应超时的条目，并生成待处理报告。

- 版本锚点追踪：对于指向代码仓库特定提交或标签的链接，自动提取当前 HEAD 的短哈希与提交时间，辅助判断文档时效性。

- 外部元数据增强：通过调用第三方 API（如 GitHub 仓库元数据接口）补充各资源的 Star 数、Fork 数与最近更新日期，并在索引列表中予以展示。

- 自定义标签与全文检索：支持用户通过修改本地标签文件或使用 grep 命令进行多关键词组合检索，满足离线环境下的快速查找需求。

- 静态导出与嵌入兼容：提供将索引导出为单一 JSON 文件或 HTML 片段的功能，便于嵌入团队内部 Wiki、Confluence 页面或企业级门户。

## 应用场景

- 团队新人入职技术摸底：新成员可通过 Olive Index 快速浏览团队关注的技术资源清单，了解当前推荐的消息队列中间件、服务网格方案或数据库驱动版本，缩短环境搭建与文档查阅的路径长度。

- 技术选型前的调研信息汇总：在评估多个开源项目时，工程师可将候选项目的官方网站、性能测试报告、社区案例与安全审计记录统一收录至 Olive Index 的临时分类下，形成可横向对比的素材集合。

- 离线环境下的知识库镜像：对于网络访问受限的开发环境，运维人员可利用 Olive Index 的链接聚合列表，结合 wget 或 curl 批量下载对应资源，构建内部只读镜像站点。

- 开源社区贡献者入门引导：项目维护者可创建一份针对贡献者的 Olive Index 子集，包含贡献指南、代码规范、测试套件说明与近期 Good First Issue 列表，降低外部贡献者的认知负担。

## 快速开始

以下命令适用于 Linux / macOS / Windows WSL 环境，需要提前安装 Git 与 Node.js 18.x 及以上版本。

```bash
# 克隆项目仓库
git clone https://github.com/zerxonhy/olive.git
cd olive

# 安装依赖（用于链接检查与元数据更新脚本）
npm install

# 运行本地索引生成服务（默认监听 127.0.0.1:4000）
npm run build
npm start
```

执行完毕后，可通过浏览器访问 `http://127.0.0.1:4000` 查看生成的索引首页。若仅需在终端输出当前所有资源的扁平列表，可运行 `npm run list`。

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
| :--- | :--- | :--- |
| Node.js | 18.x 或 20.x LTS | 运行时环境，用于执行构建脚本与链接检查任务 |
| npm | 9.x 或 10.x | 包管理器，用于安装项目依赖 |
| Git | 2.30 及以上 | 版本控制工具，用于克隆仓库与提交本地修改 |
| curl | 7.68 及以上 | 用于链接健康检查中的备选请求方式 |
| grep | 3.4 及以上 | 用于全文检索与过滤功能（Unix 工具链） |
| 磁盘可用空间 | 至少 200 MB | 用于存放索引文件、日志与缓存元数据 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
| :--- | :--- | :--- |
| 用户入门 | `docs/getting-started.md` | 如何首次运行索引构建？如何添加第一个资源条目？ |
| 维护操作 | `docs/maintenance.md` | 如何触发链接检查？如何处理失效链接报告？ |
| 分类体系 | `docs/taxonomy.md` | 当前定义了哪些技术域分类？如何为新资源选择合适分类？ |
| 高级定制 | `docs/customization.md` | 如何修改首页布局？如何增加自定义元数据字段？ |

## 资源列表

- https://github.com/zerxonhy/olive/blob/main/goldencedar.md
- https://github.com/zerxonhy/olive/blob/main/goldenfalcon.md
- https://github.com/zerxonhy/olive/blob/main/harborhorizon.md
- https://github.com/zerxonhy/olive/blob/main/horizonlantern.md
- https://github.com/zerxonhy/olive/blob/main/horizonwillow.md
- https://github.com/zerxonhy/olive/blob/main/islandcrystal.md

## 项目结构

```
olive/
├── bin/                                 # 可执行脚本目录
│   ├── check-links.js                   # 链接健康检查主脚本
│   ├── fetch-metadata.js                # 从第三方 API 获取资源元数据
│   └── generate-index.js                # 根据分类生成静态索引页
├── config/                              # 配置文件目录
│   ├── categories.json                  # 分类定义（名称、描述、父级关系）
│   └── sources.json                     # 外部 API 端点配置
├── docs/                                # 文档目录
│   ├── getting-started.md               # 快速入门指南
│   ├── maintenance.md                   # 日常维护流程说明
│   ├── taxonomy.md                      # 分类体系详细说明
│   └── customization.md                 # 界面与脚本定制参考
├── entries/                             # 资源条目存储目录（每个资源一个 .md 文件）
│   ├── goldencedar.md                   # 第 25/107 批资源条目
│   ├── goldenfalcon.md                  # 第 25/107 批资源条目
│   ├── harborhorizon.md                 # 第 25/107 批资源条目
│   ├── horizonlantern.md                # 第 25/107 批资源条目
│   ├── horizonwillow.md                 # 第 25/107 批资源条目
│   └── islandcrystal.md                 # 第 25/107 批资源条目
├── output/                              # 构建输出目录（静态站点生成）
│   ├── index.html                       # 入口页面
│   └── feed.json                        # JSON 格式的完整索引
├── scripts/                             # 辅助脚本目录
│   ├── validate-entries.sh              # 校验条目文件格式
│   └── export-html.sh                   # 将索引导出为独立 HTML 文件
├── tests/                               # 单元测试与集成测试目录
│   ├── link-checker.test.js             # 链接检查功能测试
│   └── metadata-fetch.test.js           # 元数据获取功能测试
├── .github/workflows/                   # GitHub Actions 工作流
│   └── nightly-check.yml                # 每日凌晨执行链接检查并生成报告
├── package.json                         # npm 项目配置文件
└── README.md                            # 项目说明文档（本文件）
```

## 贡献指南

1. 复刻主仓库至个人账号下，并克隆至本地开发环境。请确保本地 Git 配置了正确的用户信息，以便提交记录可追溯。

2. 在 `entries/` 目录下新建或修改资源条目文件。每个文件须遵循规定的 Markdown 模板，包含 `Title`、`Link`、`Category`、`Description` 与 `LastVerified` 字段。新增条目需同步更新 `config/categories.json` 中对应的分类计数。

3. 运行本地测试套件 `npm test` 以验证新增或修改的条目格式正确、链接可访问且分类标签有效。所有测试用例通过后方可进行下一步。

4. 提交变更并推送到个人复刻仓库，随后通过 GitHub Web 界面创建 Pull Request 至主仓库的 `main` 分支。PR 描述中应明确列出本次变更涉及的资源条目编号与修改原因。

5. 等待项目维护者审核。审核通过后，CI 流水线将自动合并变更并触发线上索引重新构建，更新内容通常在 10 分钟内生效。

## 常见问题

问：如何批量添加多个资源条目，而不是逐个创建文件？

答：项目提供了 `scripts/batch-import.sh` 脚本，接受一个 CSV 文件作为输入，每行包含标题、链接、分类和描述。执行后会自动生成对应的条目文件并更新分类配置。该脚本位于 `scripts/` 目录下，使用前请查阅脚本头部的参数说明。

问：链接检查报告显示某个链接失效，但我在浏览器中访问正常，应如何处理？

答：这种情况通常是因为资源服务器对 `User-Agent` 或 `Accept` 请求头有特殊要求。您可以修改 `bin/check-links.js` 中的请求头配置，增加 `User-Agent: Olive-Index/1.0` 或调整超时时间。若问题依然存在，请在资源条目文件中将 `LastVerified` 字段置为 `pending`，并在项目 Issue 中提交相关 URL 以供团队统一排查。

## 许可证

MIT

> 外链数量: 6 | 生成时间: 2026-07-21 05:12:52
