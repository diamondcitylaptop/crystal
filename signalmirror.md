# Olive Resource Index

Olive Resource Index 是一个面向开发者与技术研究人员的轻量级外链资源汇总工具。项目本身不存储任何实际内容，仅以结构化索引方式托管于 GitHub 仓库，便于团队或个人对分散的技术文档、配置参考、项目笔记等外部资源进行集中归类与版本追踪。目标用户包括运维工程师、架构师、开源贡献者以及需要长期维护外部参考链接的技术写作人员。

本项目采用纯 Markdown 与 Shell 脚本构建，无需数据库或后端服务。通过约定的目录结构与链接清单，用户可快速生成静态资源导航页，或直接通过命令行检索已收录的链接地址。Olive Resource Index 适用于个人知识管理、团队文档站外链备份以及自动化巡检任务中的外部依赖记录。

## 功能概览

- 零依赖静态索引：所有资源链接以 Markdown 列表形式存储，无需额外解析器或运行时环境。
- 链接状态追踪：支持通过外部脚本对已收录 URL 进行可达性检查，便于定期清理失效链接。
- 分类标签系统：每个资源条目可附加自定义标签，支持按主题、来源或用途快速筛选。
- 版本化变更记录：利用 Git 原生能力记录每次增删改操作，回退或比对历史状态无需额外工具。
- 多格式导出：内置脚本支持将链接列表导出为 JSON、CSV 或纯文本格式，便于导入其他系统。
- 离线查阅模式：全仓库克隆后，所有 Markdown 索引文件可在本地直接浏览，不依赖网络。
- 扩展钩子接口：预留 pre-commit 与 post-merge 钩子样本，允许用户集成自定义校验或通知逻辑。

## 应用场景

1. 技术文档外链备份：团队在编写内部 Wiki 时，可将引用的外部官方文档、API 参考或社区教程统一收录至 Olive Resource Index。当外部链接发生迁移或变更时，仅需在索引仓库中更新对应条目，即可同步影响所有引用文档。

2. 自动化巡检任务的依赖清单：运维脚本或定时任务往往依赖多个外部资源（如软件源、状态页、版本发布说明）。使用本索引集中管理这些 URL，配合健康检查脚本，可快速定位异常依赖。

3. 开源项目的外部资源声明：开源项目在 README 中引用第三方工具或数据集时，通常需要清晰标注来源。Olive Resource Index 可作为独立的引用清单仓库，保持主项目文档简洁，同时满足合规与致谢要求。

4. 个人知识库的链接中心：技术写作者或研究员可将日常积累的参考链接按主题归档，配合 Git 分支管理不同研究方向的内容版本，避免浏览器书签的混乱与丢失风险。

5. 离线环境下的资源导航：对于内网隔离环境，预先克隆索引仓库，结合本地镜像服务，可快速生成可访问的内部资源导航页面。

## 快速开始

以下操作适用于 Linux / macOS 及 Windows WSL 环境。请确保系统已安装 Git 与 Bash。

```bash
# 克隆仓库到本地
git clone https://github.com/zerxonhy/olive.git
cd olive

# 安装本地钩子脚本（可选，用于链接格式校验）
cp scripts/pre-commit.sample .git/hooks/pre-commit
chmod +x .git/hooks/pre-commit

# 运行索引构建脚本，生成根目录 README 中的资源列表快照
./scripts/build_index.sh

# 查看当前已收录的全部外链
cat INDEX.md
```

若需自定义索引内容，直接编辑 `./links/` 目录下的分类 Markdown 文件，或修改根目录的 `olive.conf` 配置文件调整构建行为。

## 安装要求

| 依赖项 | 必需版本 | 说明 |
|--------|----------|------|
| Git | 2.20 及以上 | 用于克隆仓库及版本管理，支持子模块操作 |
| Bash | 4.0 及以上 | 运行构建脚本及钩子样例，Windows 用户推荐 Git Bash |
| GNU Sed | 4.0 及以上 | 脚本中用于文本替换与格式清洗，非交互式使用 |
| GNU Grep | 3.0 及以上 | 用于链接格式校验与分类匹配，支持 -P 选项 |
| findutils | 4.6 及以上 | 提供 find 与 xargs 命令，用于递归处理索引文件 |
| coreutils | 8.22 及以上 | 提供 sort、uniq、comm 等基础排序去重工具 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|------|------|------------|
| 用户手册 | docs/user-guide.md | 如何增删链接、如何分类、如何触发自动校验？ |
| 管理员指南 | docs/admin-guide.md | 如何配置钩子、如何设置定期巡检任务、如何处理合并冲突？ |
| 格式规范 | docs/format-spec.md | 链接条目的 Markdown 语法要求、标签命名约束、描述字段长度限制？ |
| 贡献流程 | CONTRIBUTING.md | 外部贡献者如何提交新索引条目、PR 审核标准是什么？ |
| 设计说明 | docs/design.md | 索引结构为什么采用三层分类、脚本设计选型考虑、扩展点在哪里？ |

## 资源列表

- https://github.com/zerxonhy/olive/blob/main/meadowisland.md
- https://github.com/zerxonhy/olive/blob/main/meadowzephyr.md
- https://github.com/zerxonhy/olive/blob/main/midnightocean.md
- https://github.com/zerxonhy/olive/blob/main/midnightquartz.md
- https://github.com/zerxonhy/olive/blob/main/midnighttimber.md
- https://github.com/zerxonhy/olive/blob/main/mirrorprairie.md

## 项目结构

```
olive/
├── .gitignore                     # 忽略构建临时文件与本地配置
├── .gitattributes                 # 统一行尾与 diff 策略
├── README.md                      # 项目主文档（即当前文件）
├── INDEX.md                       # 构建生成的全量链接列表（自动生成）
├── olive.conf                     # 主配置文件：分类映射、超时阈值、输出格式
├── links/                         # 用户自定义索引目录
│   ├── 01-infra/                  # 基础设施类链接（K8s、网络、监控）
│   │   ├── README.md              # 该分类的说明与索引条目
│   │   └── archive/               # 归档历史链接，不再主动更新
│   ├── 02-languages/              # 编程语言与运行时（Go、Rust、Python）
│   │   ├── go.md
│   │   ├── rust.md
│   │   └── python.md
│   ├── 03-databases/              # 数据库与缓存（MySQL、Redis、ClickHouse）
│   │   ├── mysql.md
│   │   └── redis.md
│   ├── 04-observability/          # 可观测性（Prometheus、OpenTelemetry）
│   │   └── prometheus.md
│   └── 99-misc/                   # 未分类或临时资源
│       └── temp.md
├── scripts/                       # 工具脚本目录
│   ├── build_index.sh             # 主构建脚本，合并 links/ 下所有条目
│   ├── check_health.sh            # 并发检查所有 URL 可达性，输出报告
│   ├── export_json.sh             # 将 INDEX.md 转换为 JSON 格式
│   ├── export_csv.sh              # 转换为 CSV，便于 Excel 查看
│   └── pre-commit.sample          # Git 钩子样本：提交前检查链接格式
├── docs/                          # 详细文档
│   ├── user-guide.md
│   ├── admin-guide.md
│   ├── format-spec.md
│   └── design.md
├── tests/                         # 单元测试与集成测试
│   ├── test_parse.bats            # Bats 测试：解析器正确性
│   └── test_health.bats           # 健康检查脚本功能测试
└── examples/                      # 实际使用示例
    ├── personal-knowledge/        # 个人知识库配置样例
    └── team-onboarding/           # 团队新成员外链清单样例
```

## 贡献指南

1. 派生仓库并创建特性分支：从主仓库派生至个人账户，然后基于 `main` 分支创建 `feature/your-change` 分支。所有修改请在分支中进行，禁止直接提交至 main。

2. 遵循链接条目格式规范：每个新增链接必须独占一行，采用 `- [描述](URL)` 或纯 URL 形式。描述文本需简洁明确，长度不超过 80 个字符。若链接归属现有分类，需放入对应 `links/` 子目录下的正确 Markdown 文件；若新增分类，需同步修改 `olive.conf` 中的分类映射表。

3. 运行本地构建与自检：提交前执行 `./scripts/build_index.sh` 确保 INDEX.md 生成无报错。可选执行 `./scripts/check_health.sh` 验证新链接可达性（若网络环境受限可跳过，但需在 PR 说明中标注）。

4. 提交变更并撰写清晰 Commit Message：提交信息格式建议为 `[分类] 操作: 简短说明`，例如 `[infra] add: prometheus official docs` 或 `[databases] update: redis stable version URL`。提交数量不限，但需保证每个提交逻辑独立。

5. 发起 Pull Request 并等待审核：PR 标题需概括变更内容，正文需说明新增或修改链接的用途及来源。审核人员将对链接有效性、分类准确性和格式规范性进行检查。通过后由维护者合并至 main。

## 常见问题

问：索引仓库中的链接发生变更时，我是否需要手动更新所有引用？

答：Olive Resource Index 本身只维护链接列表，并不影响外部文档中的具体引用。若您将此索引作为其他文档的数据源，建议通过脚本定期重新生成引用片段。对于已归档的旧链接，我们鼓励在 INDEX.md 中保留原条目并标记 `[deprecated]`，同时新增新条目，避免历史文档断链。

问：构建脚本报错 "sed: illegal option -- r" 如何处理？

答：该错误通常出现在 macOS 自带的 BSD sed 上。请安装 GNU sed 并将其设为默认（如通过 Homebrew 安装 `gnu-sed`，然后使用 `gsed` 替代），或者在 `olive.conf` 中将 `SED_CMD` 变量指向 GNU 版本。具体操作请参考 `docs/admin-guide.md` 中的环境配置章节。

问：如何将本索引与我的 CI/CD 流水线集成？

答：您可以在流水线中添加一个步骤，定时执行 `./scripts/check_health.sh` 并将失败链接输出为告警信息。若需要生成静态 HTML 导航，可先运行 `./scripts/export_json.sh` 导出结构化数据，再使用任意模板引擎渲染。我们提供的 `examples/` 目录中包含了与 GitHub Actions 和 Jenkins 集成的参考样例。

## 许可证

MIT

> 外链数量: 6 | 生成时间: 2026-07-21 05:13:26
