# Olive Link Atlas

Olive Link Atlas 是一个面向技术文档作者、开源项目维护者以及开发者知识管理者的外链资源归集与结构化导航工具。该项目并非传统的爬虫或书签管理器，而是一种基于 Markdown 的、可版本化的外部知识索引范式。它解决的核心问题是：当技术团队或个人在阅读源码、撰写设计文档或进行技术调研时，如何高效地组织、分类和复用散落在 GitHub、技术博客、官方文档中的高价值外链，避免重复检索与信息碎片化。

本项目适用于需要长期维护技术知识图谱的团队，以及希望将外链资源作为项目资产进行规范化管理的开发者。Olive Link Atlas 本身不存储第三方内容，而是通过严格的索引结构，将外链的元数据（如来源仓库、文件路径、内容摘要、标签）以纯文本形式固化在仓库中，从而利用 Git 的版本控制能力实现外链资源的变更追踪与协作审阅。

## 功能概览

**结构化外链索引** 支持按项目、模块、文档层级对外链进行多级分类，每条链接均附带上下文说明与提取时间戳。

**基于 GitHub 文件的深度引用** 能够精确指向 GitHub 仓库内的特定 Markdown 文件或代码行，实现源码级的外链锚定。

**批处理导入能力** 支持一次性导入大批量链接（如本批次 6 条资源），并自动生成对应的索引记录与校验哈希。

**标签化查询系统** 每条外链可附加多个功能标签（如 configuration, troubleshooting, api-reference），支持快速过滤与交集检索。

**变更历史审计** 所有外链的新增、删除、URL 更新操作均通过 Git 提交记录进行审计，便于回溯与回滚。

**纯静态部署友好** 索引文件全部为 Markdown 格式，无需数据库或后端服务，可直接托管在 GitHub Pages 或任何静态服务器上。

**IDE 插件生态支持** 提供 VS Code 扩展，可在编辑 Markdown 文档时自动补全已索引的外链路径。

## 应用场景

技术文档团队批量整理遗留系统的外部依赖文档
当团队接手一个老旧系统时，通常存在大量散落在个人笔记、邮件或聊天记录中的外部链接（如第三方库主页、补丁说明、兼容性列表）。Olive Link Atlas 可在一小时内将这批链接（例如本批次包含的 6 条 marble 系列配置参考）批量导入索引库，并为每条链接补充来源模块、关联 Issue 和最后验证时间，使文档外链从无序状态转变为可维护的项目资产。

开源项目维护者管理贡献者指南中的引用资源
开源项目的 CONTRIBUTING.md 或 README 中常需要引用大量外部资源（如代码规范、提交信息格式、CI 配置示例）。使用 Olive Link Atlas 可以将这些外链单独抽离为索引条目，在主文档中仅保留引用 ID，从而降低主文档的膨胀速度，并允许贡献者通过 PR 独立更新外链列表而不影响主文档结构。

技术调研阶段的多来源信息聚合
开发者在进行技术选型或漏洞分析时，需要同时查阅 GitHub 讨论、官方 JIRA、个人技术博客和 Stack Overflow 问答。Olive Link Atlas 允许为每个调研主题创建独立的索引页面，将来自不同域名的相关链接聚合在一起，并支持添加对比备注（如性能数据、社区活跃度），最终生成一份可交付的调研报告骨架。

离线环境下的文档外链预缓存规划
对于需要部署到内网或离线环境的文档站点，Olive Link Atlas 可以生成所有外链的完整清单，包括协议、域名、路径深度等信息，方便运维人员编写自动化脚本预先抓取静态副本或配置代理白名单。

## 快速开始

以下命令演示了如何从 GitHub 克隆 Olive Link Atlas 项目模板、安装依赖（仅需 Python 3.9+ 和标准库），并运行一次批处理导入来验证索引功能。

```bash
# 克隆项目模板（包含示例索引结构和配置文件）
git clone https://github.com/olive-org/link-atlas-starter.git my-link-atlas
cd my-link-atlas

# 安装轻量级 Python 依赖（用于校验 URL 格式和生成摘要）
pip install -r requirements.txt

# 运行批处理导入命令，将用户提供的原始链接列表归入索引
# 其中 --batch 指向包含 6 条资源的文本文件，--project 指定目标项目代号
python atlas.py import --batch ./samples/batch_63_107.txt --project olive-utils --tag v1.0
```

执行成功后，索引文件将更新于 `index/` 目录下，同时会在 `logs/` 目录生成导入报告。

## 安装要求

| 依赖 | 必需版本 | 说明 |
|------|----------|------|
| Python | 3.9 或更高 | 用于运行核心导入、校验和导出脚本，低于 3.9 将不支持类型注解语法 |
| Git | 2.25 或更高 | 用于版本控制外链索引变更，推荐使用 2.30+ 以获得更好的稀疏检出支持 |
| pip | 20.0 或更高 | 用于安装 requirements.txt 中列出的轻量级库（仅 requests 和 pyyaml） |
| 磁盘空间 | 至少 10 MB | 索引库本身极小，但推荐预留 50 MB 用于存放历史提交对象和缓存摘要 |
| 网络访问 | 任意（推荐外网） | 仅当使用在线校验功能（检查 URL 是否可访问）时需要外网，离线模式可禁用 |
| 终端环境 | Unix/Linux/macOS 或 WSL2 | Windows 原生 cmd 未充分测试，推荐使用 Git Bash 或 WSL2 |
| Markdown 解析器 | 任意 | 索引文件为纯 Markdown，可使用任何主流解析器（如 CommonMark）渲染 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|------|------|------------|
| 用户手册 | docs/user-guide/import-batch.md | 如何批量导入外链、如何自定义元数据模板、如何处理重复 URL |
| 用户手册 | docs/user-guide/query-syntax.md | 支持哪些查询操作符？如何按标签、时间范围或项目名进行复合查询？ |
| 管理员指南 | docs/admin/migration.md | 如何将旧版书签 HTML 或 JSON 格式迁移到 Olive Atlas 索引结构？ |
| 管理员指南 | docs/admin/gc.md | 如何清理长期未验证或指向 404 的失效链接？GC 策略如何配置？ |
| 开发者参考 | docs/dev/api/import-hooks.md | 如何编写自定义钩子函数，在导入前自动补全链接的标题或描述？ |
| 设计文档 | docs/design/versioning.md | 索引文件的版本兼容性策略是什么？如何支持向前兼容旧索引？ |

## 资源列表

- https://github.com/zerxonhy/olive/blob/main/maplejade.md
- https://github.com/zerxonhy/olive/blob/main/marbleamber.md
- https://github.com/zerxonhy/olive/blob/main/marblegolden.md
- https://github.com/zerxonhy/olive/blob/main/marblejade.md
- https://github.com/zerxonhy/olive/blob/main/marblelantern.md
- https://github.com/zerxonhy/olive/blob/main/marblepixel.md

## 项目结构

```
olive-link-atlas/
├── atlas.py                 # CLI 主入口：导入、查询、导出、校验
├── requirements.txt         # 依赖声明（requests==2.28.2, pyyaml==6.0）
├── config/
│   ├── default.yaml         # 默认索引策略：标签别名、校验超时、忽略模式
│   └── schema.json          # 索引记录 JSON Schema，用于 CI 校验
├── index/                   # 核心索引存储区（所有外链条目）
│   ├── projects/            # 按项目名分组的索引文件
│   │   ├── olive-utils.yaml # 当前批次导入的目标项目索引
│   │   └── kernel-tools.yaml # 示例项目索引
│   ├── tags/                # 标签反向索引（自动生成，用于快速标签查询）
│   │   ├── configuration.md
│   │   └── reference.md
│   └── _meta/               # 元数据：导入批次记录、去重表、最后验证时间
│       ├── batch_63_107.sig # 当前批次的 SHA-256 签名文件
│       └── dedup_cache.json # 全局 URL 去重缓存
├── docs/                    # 完整用户文档与开发文档（见文档导航章节）
│   ├── user-guide/
│   ├── admin/
│   └── design/
├── tests/                   # 单元测试与集成测试（覆盖导入、查询、迁移）
│   ├── test_import.py
│   └── fixtures/            # 测试用固定数据（含模拟 URL 列表）
├── scripts/                 # 运维辅助脚本
│   ├── validate-all.sh      # 每日定时校验所有外链可达性
│   └── generate-toc.py      # 自动生成索引目录的 TOC
└── .github/
    └── workflows/           # GitHub Actions 流水线
        ├── ci.yaml          # PR 时运行导入测试与格式检查
        └── nightly-check.yaml # 夜间自动校验所有外链并提交报告
```

## 贡献指南

我们欢迎任何形式的贡献，包括但不限于新增外链接入源、优化导入性能、完善文档以及增加新的查询过滤器。请遵循以下步骤：

1.  **查阅项目看板**：访问 GitHub Projects 页面，查看当前迭代的待办事项列表，避免重复工作。对于新增功能建议，请先创建一个 Issue 并标记为 `proposal`，与维护者达成共识后再进行开发。

2.  **准备开发环境**：Fork 本仓库到个人账户，然后克隆到本地。确保 Python 3.9+ 和 Git 2.30+ 已安装。运行 `pip install -r requirements-dev.txt` 安装开发依赖（包含 pytest、black、mypy）。

3.  **编写或修改代码**：遵循项目根目录下的 `.python-version` 和 `.editorconfig` 设定的编码规范。所有新增的函数必须包含 docstring，且需要为核心逻辑编写至少一个正向测试用例和一个异常测试用例。

4.  **提交变更与自测**：在提交前，请运行 `./scripts/pre-commit.sh` 脚本，该脚本会自动执行 lint 检查、类型检查（mypy）和单元测试。确保所有测试通过且测试覆盖率不低于 85%。

5.  **发起 Pull Request**：推送分支到你的 Fork 仓库，然后向本仓库的 `main` 分支发起 PR。PR 描述中请使用模板，清晰说明变更内容、影响范围以及是否涉及索引格式的兼容性变更。至少需要一位项目维护者 Approve 后方可合并。

## 常见问题

**问：如果外链来源仓库（如 zerkonhy/olive）发生迁移或删除，索引会如何处理？**

答：Olive Link Atlas 不会自动删除或修改已索引的外链。当检测到链接失效时（通过 nightly 校验工作流），系统会在索引条目的 `status` 字段中标记为 `unreachable` 并记录最后失败时间。项目维护者会定期审阅这些失效链接，决定是更新为新 URL 还是将其移入 `archive/` 目录。用户也可以通过手动运行 `atlas.py validate --update-status` 来主动触发校验。

**问：导入大量链接时，如何避免因网络超时导致导入中断？**

答：导入流程默认使用 10 秒超时，且不强制要求在线可达。若您导入的链接数量超过 100 条，建议使用 `--offline` 模式禁用在线校验，仅进行格式和结构检查。此外，导入脚本支持断点续传，使用 `--resume` 参数可从上次中断的批次处继续导入。对于企业内网环境，您还可以通过 `config/default.yaml` 中的 `proxy` 字段配置 HTTP/HTTPS 代理。

**问：索引文件是否支持多分支或多版本？如何回滚到上一批次的索引状态？**

答：因为所有索引数据均以纯文本形式存储在 Git 仓库中，您可以充分利用 Git 的分支和标签功能。例如，在为某个发行版创建稳定文档时，可以打一个标签 `v2.3-stable-index`，此后该版本的索引独立演进。若要回滚，只需执行 `git checkout <target_commit> -- index/` 即可恢复该目录到指定状态。建议在重大变更前手动创建备份分支。

## 许可证

MIT

> 外链数量: 6 | 生成时间: 2026-07-21 05:13:20
