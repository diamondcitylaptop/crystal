# Olive Link Atlas

Olive Link Atlas 是一个面向技术文档聚合与外部资源结构化管理的轻量级索引系统。项目本身不存储任何实际内容，仅通过对既定仓库内 Markdown 描述文件进行统一引用与分类，构建出一张可扩展的外部资源地图。目标用户包括技术调研人员、文档维护者以及需要频繁查阅分散式技术笔记的开发者。Olive Link Atlas 通过提供固定的目录结构、可追溯的引用链和标准化的资源列表，解决了分散链接难以归类、版本同步困难以及团队协作中资源丢失的问题。

## 功能概览

- **资源索引固化**：将分散在多个外部文档中的关键链接纳入统一索引体系，每次更新均保留历史记录。
- **路径映射表**：提供从资源编号到仓库内相对路径的双向映射，支持快速定位原始描述文件。
- **状态标识系统**：每个资源条目可标记为稳定、过期、待审或弃用，便于生命周期管理。
- **批量校验接口**：内置链接可达性检查脚本，可定时输出失效资源报告。
- **标签分组机制**：允许对资源进行多维度打标，例如按技术栈、按所属团队、按文档类型进行二次筛选。
- **变更日志集成**：每次提交自动生成资源变动摘要，便于 Code Review 时快速评估影响面。
- **外部镜像声明**：支持为每个资源声明至少一个镜像地址或备用访问通道，降低单点故障风险。

## 应用场景

- **技术选型调研**：团队在引入新中间件时，通过 Olive Link Atlas 快速汇总官方文档、社区评测、性能对比与安全通告，所有链接均从指定描述文件内读取，确保引用出处明确。
- **文档站外链治理**：项目文档中存在大量外部引用，使用本索引系统可集中管理这些链接，当外部站点变更时只需更新描述文件中的对应条目，无需修改主文档正文。
- **离线阅读准备**：在无网络环境中，运维人员可依据资源列表预先批量下载关键内容，本索引中每个条目均附带内容摘要与文件大小预估，辅助规划存储空间。
- **合规审计追溯**：合规团队需要定期检查外部引用是否违反数据安全政策，通过 Olive Link Atlas 提供的变更日志和状态标识，可快速定位新增或变更的外部资源，并追溯到引入时间和提交人。
- **多仓库协同引用**：当多个微服务仓库均需引用同一份外部技术规范时，Olive Link Atlas 可作为唯一事实来源，各仓库通过子模块或脚本同步该索引，避免各自维护导致的引用不一致。

## 快速开始

以下命令可在任意 Linux 或 macOS 环境下完成 Olive Link Atlas 的初始部署与运行。

```bash
# 克隆项目仓库
git clone https://github.com/zerxonhy/olive.git
cd olive

# 安装依赖（仅需标准 Python 环境与 requests 库）
python3 -m venv venv
source venv/bin/activate
pip install requests

# 运行索引校验脚本，检查所有资源链接可达性
python scripts/check_links.py --source ./link_index.json
```

## 安装要求

| 依赖 | 必需版本 | 说明 |
|---|---|---|
| Python | 3.8 及以上 | 用于运行校验脚本与索引生成工具 |
| Git | 2.25 及以上 | 克隆仓库及管理版本变更 |
| requests | 2.25.0 及以上 | 发送 HTTP 请求进行链接状态检查 |
| pytest | 7.0.0 及以上 | 可选，用于执行单元测试和集成测试 |
| curl | 7.68.0 及以上 | 作为备选校验工具，用于脚本中非 Python 环境下的快速检查 |
| shellcheck | 0.7.0 及以上 | 可选，用于静态检查脚本中的 shell 代码规范 |
| GNU Make | 3.81 及以上 | 用于运行预定义的构建任务，例如生成摘要报告 |
| jq | 1.6 及以上 | 可选，用于命令行下解析 JSON 索引文件 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|---|---|---|
| 用户手册 | docs/user-guide/index.md | 如何添加、删除或修改资源条目，以及如何理解状态标识 |
| 运维指南 | docs/ops/health-check.md | 如何部署链接监控定时任务，以及如何处理失效链接告警 |
| 开发规范 | docs/development/coding-standards.md | 索引 JSON Schema 定义，以及提交信息格式要求 |
| 设计说明 | docs/design/architecture-overview.md | 整体数据流、缓存策略以及扩展性设计，适合二次开发 |
| 常见任务 | docs/tasks/batch-import.md | 如何从 CSV 或现有数据库批量导入资源列表 |
| 版本记录 | CHANGELOG.md | 每个版本新增、弃用或修复了哪些资源条目 |

## 资源列表

- https://github.com/zerxonhy/olive/blob/main/willowvelvet.md
- https://github.com/zerxonhy/olive/blob/main/amberocean.md
- https://github.com/zerxonhy/olive/blob/main/amberwillow.md
- https://github.com/zerxonhy/olive/blob/main/anchorbloom.md
- https://github.com/zerxonhy/olive/blob/main/anchormaple.md
- https://github.com/zerxonhy/olive/blob/main/atlascanvas.md

## 项目结构

```
olive/
├── link_index.json                # 主索引文件，包含所有资源条目及其元数据
├── CHANGELOG.md                   # 版本变更日志，按时间倒序排列
├── CONTRIBUTING.md                # 贡献者指南，包含流程和代码规范
├── LICENSE                        # MIT 许可证全文
├── Makefile                       # 构建任务定义，如 make test 与 make report
├── README.md                      # 项目概览与快速入门（即本文档）
├── docs/                          # 文档目录
│   ├── user-guide/                # 面向最终用户的详细操作手册
│   │   └── index.md
│   ├── ops/                       # 运维与监控相关文档
│   │   ├── health-check.md
│   │   └── alert-config.md
│   ├── development/               # 面向开发者的技术说明
│   │   ├── coding-standards.md
│   │   └── schema-definition.md
│   ├── design/                    # 架构设计文档
│   │   └── architecture-overview.md
│   └── tasks/                     # 常见操作任务指南
│       └── batch-import.md
├── scripts/                       # 可执行脚本目录
│   ├── check_links.py             # 主校验脚本，生成可达性报告
│   ├── generate_summary.sh        # 生成资源摘要统计信息
│   └── validate_schema.py         # 校验索引文件是否符合 JSON Schema
├── tests/                         # 单元测试与集成测试
│   ├── test_check_links.py
│   ├── test_schema_validation.py
│   └── fixtures/                  # 测试用固定数据
│       └── sample_index.json
└── .github/                       # GitHub 自动化配置
    └── workflows/
        └── nightly-check.yml      # 定时执行链接检查的 GitHub Actions 配置
```

## 贡献指南

1. 查阅 issue 列表或创建新 issue 说明拟修改的资源条目及原因，等待维护者确认。若为新增资源，需提供原始描述文件的完整路径以及推荐的状态和标签。
2. Fork 本项目并创建新的特性分支，分支命名遵循 `feature/resource-{序号}` 或 `fix/resource-{序号}` 格式。
3. 修改 `link_index.json` 或相关描述文件后，运行本地校验脚本 `python scripts/check_links.py --source ./link_index.json --strict` 确保所有链接可达且 JSON 格式合法。
4. 提交变更时，Commit Message 必须包含对应 issue 编号以及变更摘要，例如 `feat: add resource #42 (willowvelvet) — update status to stable`。
5. 发起 Pull Request 至主分支，至少需要一位维护者 Approve 且所有 CI 检查通过后方可合并。合并后资源列表将自动更新至 `docs/user-guide/index.md` 中的示例部分。

## 常见问题

**Q：索引中的资源链接失效了怎么办？**

A：首先确认失效是临时性（例如站点维护）还是永久性（资源被移除）。若为临时失效，可在该资源条目中添加 `retry_after` 字段记录预计恢复时间；若为永久失效，则需将该资源状态标记为 `deprecated`，并在 `replacement` 字段中提供替代链接（如果有），随后提交 PR 更新索引。定时检查脚本会在每日报告中高亮标记所有失效条目。

**Q：如何保证多个贡献者同时修改索引时不产生冲突？**

A：本项目要求所有对 `link_index.json` 的修改必须基于最新主分支进行。若出现冲突，优先保留时间戳较新的条目，并人工复核该资源的状态和标签。CI 流程中加入了冲突检测步骤，若检测到无法自动合并的变更，会阻止 PR 合并并提示贡献者手动解决。

**Q：是否支持为同一个资源添加多个备用链接？**

A：支持。在索引条目的 `mirrors` 数组中可以声明任意数量的备用 URL。校验脚本会依次检查主链接和所有备用链接，只要至少有一条可达，该资源即视为可用。备用链接的检查结果会单独记录在报告中，便于后续维护。

## 许可证

MIT

> 外链数量: 6 | 生成时间: 2026-07-21 05:13:28
