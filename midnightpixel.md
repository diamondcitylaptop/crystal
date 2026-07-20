# Olive Index

Olive Index 是一个面向开发者与技术研究者的外链资源归集与结构化导航项目。本项目不对任何外部资源进行内容镜像或代理转发，仅提供基于语义分类与人工校验的链接索引服务。目标用户包括技术选型评估人员、开源贡献者、以及需要快速定位特定领域高质量外链资料的研发团队。Olive Index 通过可维护的 Markdown 索引文件与版本化记录，解决分散收藏、链接失效、分类混乱这三类常见信息管理问题。

## 功能概览

- 语义化分类索引：每个外链条目均附带所属技术领域、关键词标签与收录理由说明，支持按主题快速筛选。
- 多级标签体系：涵盖编程语言、运行时环境、数据存储、网络协议、安全合规、运维监控、人工智能、前端工程、移动开发等 20 个一级标签。
- 人工可用性验证：每条收录链接均经过存活检测与内容相关性评估，失效链接将被标记或迁移至归档区。
- 版本化变更记录：索引文件随项目迭代更新，每次增删改均通过 Git 提交记录保留变更上下文，便于回溯。
- 结构化元数据模板：每个条目包含标题、原始 URL、描述摘要、标签列表、收录日期、最后验证日期共六项元数据。
- 多格式导出支持：除 Markdown 表格视图外，提供 JSON Lines 格式导出，便于与其他工具链集成。
- 权限最小化原则：本项目不要求用户提供任何个人凭证，不嵌入第三方追踪脚本，所有资源链接均以明文形式呈现。

## 应用场景

技术调研期间的资源聚合：当研发团队需要评估多个同类开源项目或技术方案时，可通过 Olive Index 快速获取经过初步筛选的外链集合，减少盲目搜索的时间开销。

个人知识库的外链补充：开发者维护个人技术笔记或博客时，可使用本索引作为外部参考文献的来源池，确保引用链接的可靠性与可追溯性。

离线文档规划的输入源：企业内部文档团队在构建技术手册或培训材料时，可参考 Olive Index 的分类结构与链接清单，规划需要镜像或缓存的关键外部资源。

开源项目的 README 引用库：开源维护者可在自己的项目文档中引用 Olive Index 中的相关条目，作为“进一步阅读”或“相关项目”部分的标准化来源。

## 快速开始

以下命令用于克隆仓库、安装基础依赖并启动本地索引服务。

```bash
git clone https://github.com/zerxonhy/olive.git
cd olive
npm install
npm run build
```

执行完成后，可通过 `npm run serve` 启动本地预览，默认监听端口 8080。索引数据位于 `data/index.json`，可通过编辑该文件进行自定义增删改。

## 安装要求

| 依赖 | 必需版本 | 说明 |
|---|---|---|
| Node.js | 18.x 或 20.x LTS | 运行时环境，用于执行构建脚本与本地服务 |
| npm | 9.x 或 10.x | 包管理器，用于安装项目依赖 |
| Git | 2.30 及以上 | 版本控制工具，用于克隆仓库与提交变更 |
| curl | 7.68 及以上 | 用于外部链接存活检测脚本（可选） |
| jq | 1.6 及以上 | 用于 JSON 数据处理与格式校验（可选） |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|---|---|---|
| 用户手册 | docs/user-guide.md | 如何浏览索引、筛选标签、导出数据 |
| 维护手册 | docs/maintainer-guide.md | 如何新增条目、更新验证状态、处理失效链接 |
| 架构说明 | docs/architecture.md | 索引数据结构、构建流程、插件扩展机制 |
| 变更日志 | CHANGELOG.md | 每个版本的条目增减、字段调整、工具链升级 |

## 资源列表

- https://github.com/zerxonhy/olive/blob/main/lanternforest.md
- https://github.com/zerxonhy/olive/blob/main/lanternpixel.md
- https://github.com/zerxonhy/olive/blob/main/maplecosmic.md
- https://github.com/zerxonhy/olive/blob/main/mapleharbor.md
- https://github.com/zerxonhy/olive/blob/main/maplejade.md
- https://github.com/zerxonhy/olive/blob/main/marbleamber.md

## 项目结构

```
olive/
├── data/                          # 索引数据与元数据存储目录
│   ├── index.json                 # 主索引文件，包含所有条目及标签
│   ├── archive/                   # 已下架或失效链接归档
│   │   └── 2026-q2.json           # 按季度归档的移除记录
│   └── schemas/                   # JSON Schema 校验定义
│       └── entry.schema.json      # 单个条目的字段约束
├── scripts/                       # 工具脚本
│   ├── validate.js               # 校验索引数据完整性
│   ├── check-links.sh            # 批量检测外链可用性
│   └── export-jsonl.js           # 导出 JSON Lines 格式
├── docs/                          # 项目文档
│   ├── user-guide.md             # 用户使用手册
│   ├── maintainer-guide.md       # 维护者操作指南
│   └── architecture.md           # 架构设计与扩展点说明
├── tests/                         # 单元测试与集成测试
│   ├── index.test.js             # 索引数据解析测试
│   └── link-format.test.js       # URL 格式校验测试
├── .github/                       # GitHub 相关配置
│   └── workflows/
│       └── ci.yml                # 持续集成流水线配置
├── package.json                   # Node.js 项目清单
├── README.md                      # 项目入口文档（当前文件）
└── CHANGELOG.md                   # 版本变更历史
```

## 贡献指南

1. 复刻本项目仓库至个人账户，并克隆到本地开发环境。
2. 在 `data/index.json` 中按照现有条目格式新增或修改外链记录，确保所有元数据字段完整。
3. 运行 `npm run test` 执行本地校验，包括 JSON 格式检查与字段类型验证。
4. 提交变更时使用约定式提交规范（如 `feat: add new entry for xyz` 或 `fix: update dead link for abc`）。
5. 发起 Pull Request 并描述变更目的与验证结果，等待维护者审核。

## 常见问题

问：项目是否存储外部资源的副本或快照？
答：否。Olive Index 仅存储链接地址及其元数据描述，不缓存、不代理、不镜像任何外部资源内容。用户访问外部链接时需自行承担网络传输与内容合规责任。

问：如何报告失效链接或建议新增条目？
答：可通过 GitHub Issues 提交反馈，模板中请注明原始 URL、失效日期（如已知）以及建议替换链接。维护者将定期处理并更新索引。

问：索引数据是否支持离线使用？
答：支持。用户可将 `data/index.json` 导出为 JSON Lines 格式并集成至本地文档系统，但外部链接本身仍需网络访问。所有元数据均以纯文本形式存储，无需网络即可检索。

## 许可证

MIT

> 外链数量: 6 | 生成时间: 2026-07-21 05:13:38
