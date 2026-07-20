# Olive Link Aggregator

Olive Link Aggregator 是一个面向开发者与技术研究人员的轻量级外链资源归集与导航系统。该项目不对托管内容本身进行修改或二次分发，仅提供结构化索引与访问入口，用于帮助用户快速定位分布在多个仓库或文档站点中的技术笔记、配置参考、实验记录与版本说明。

Olive Link Aggregator 的目标用户包括：需要维护多源技术链接的团队、个人知识库管理者、以及希望以最低成本建立可读链接索引的文档维护者。项目本身不依赖数据库或后端服务，完全基于静态 Markdown 与 GitHub 仓库元数据构建，适合部署在 GitHub Pages、Vercel 或其他静态托管环境中。

## 功能概览

- 多源链接归集：支持将分散在不同仓库或分支中的 Markdown 文件统一抽象为外链条目，按文件名称自动生成语义化分类标签。

- 链接状态可观测性：通过 GitHub 仓库的提交历史与文件变更记录，间接追踪目标链接的新增、修改与删除时间点。

- 纯静态零依赖：项目运行时无需任何外部服务或持久化存储，仅依赖 Git 与标准 Unix 工具链，可在任何 POSIX 兼容环境中执行。

- 可扩展元数据模板：每个外链条目允许附加可选说明字段，用于记录目标资源的用途、维护责任人、预期更新频率或关联项目编号。

- 批量导入与校验：提供基础 Shell 脚本，支持从 CSV 或纯文本列表中批量导入新链接，并在导入前对 URL 格式进行正则校验。

- 仓库级快照引用：通过固定提交哈希（commit hash）引用目标文件，降低目标分支变动导致的链接失效风险，同时保留可人工核验的审计路径。

- 标签过滤与检索：在生成的静态页面中内置纯前端标签过滤能力，允许用户按文件前缀（如 velvet、willow、amber 等）快速缩小范围。

## 应用场景

场景一：技术笔记索引维护
技术团队在内部 GitHub 仓库中维护大量实验性文档，文档名称采用随机前缀或代号（如 velvetisland、amberocean 等）。Olive Link Aggregator 可帮助团队快速生成一份按文件名排序的链接清单，避免频繁切换仓库页面查看。

场景二：多仓库文档入口聚合
当技术文档分散在多个 GitHub 仓库且每个仓库的文档路径不统一时，Olive Link Aggregator 可作为轻量级入口层，将所有相关文档的原始链接集中在一个项目内管理，减少团队成员的记忆成本。

场景三：开源项目外部参考列表
开源项目维护者可以使用 Olive Link Aggregator 维护一份“相关资源”或“致谢引用”列表，将依赖的上游文档、衍生项目或参考实现以纯链接形式归档，便于后续审计与合规检查。

场景四：个人知识库外链备份索引
个人知识库工具（如 Obsidian、Foam 等）通常只处理内部 Wiki 链接。Olive Link Aggregator 可作为外部链接的补充层，专门存放那些不适合直接嵌入笔记正文的长尾 URL 引用。

## 快速开始

以下命令适用于 Linux 与 macOS 环境，Windows 用户建议通过 WSL 或 Git Bash 执行。

```bash
# 克隆项目仓库
git clone https://github.com/zerxonhy/olive.git
cd olive

# 安装基础依赖（仅需 Git 与 coreutils）
# Ubuntu/Debian
sudo apt update && sudo apt install git coreutils

# macOS (Homebrew)
brew install git coreutils

# 运行本地索引生成脚本
./scripts/generate-index.sh

# 启动简易 HTTP 服务查看结果（Python 3）
python3 -m http.server 8000
```

执行完成后，访问 http://localhost:8000 即可浏览生成的链接索引页面。

## 安装要求

| 依赖 | 必需版本 | 说明 |
|---|---|---|
| Git | 2.25 或更高 | 用于克隆仓库及读取提交元数据 |
| Bash | 4.0 或更高 | 运行所有 Shell 脚本 |
| coreutils | 8.30 或更高 | 提供 realpath、md5sum 等基础工具 |
| grep | 3.1 或更高 | 用于正则匹配与过滤 |
| Python 3 | 3.6 或更高 | 仅用于本地预览服务，非运行时必需 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|---|---|---|
| 入门指南 | docs/quickstart.md | 如何在三分钟内完成项目搭建并生成第一个索引页面 |
| 链接管理 | docs/link-management.md | 如何新增、删除或修改外链条目，以及如何批量更新 |
| 标签体系 | docs/tagging.md | 标签命名规范、自动分类逻辑与自定义标签方法 |
| 部署参考 | docs/deployment.md | 支持哪些静态托管平台，以及各自的配置示例 |

## 资源列表

- https://github.com/zerxonhy/olive/blob/main/velvetisland.md
- https://github.com/zerxonhy/olive/blob/main/velvetrocket.md
- https://github.com/zerxonhy/olive/blob/main/violettimber.md
- https://github.com/zerxonhy/olive/blob/main/willowsilver.md
- https://github.com/zerxonhy/olive/blob/main/willowvelvet.md
- https://github.com/zerxonhy/olive/blob/main/amberocean.md

## 项目结构

```
olive/
├── .github/                         # GitHub 相关配置（Issue 模板、CI 等）
│   └── workflows/
│       └── index-update.yml         # 每日自动更新索引的 GitHub Actions 工作流
├── scripts/                         # 可执行脚本目录
│   ├── generate-index.sh            # 主索引生成脚本，扫描 main 分支下的所有目标文件
│   ├── validate-urls.sh             # 校验资源列表中的 URL 是否可访问（HEAD 请求）
│   └── batch-import.sh              # 从外部文本文件批量导入链接的辅助脚本
├── docs/                            # 项目自身文档
│   ├── quickstart.md                # 快速入门指南
│   ├── link-management.md           # 链接增删改操作说明
│   ├── tagging.md                   # 标签与分类策略
│   └── deployment.md                # 部署到不同托管平台的配置参考
├── templates/                       # 静态页面模板
│   ├── index.template.html          # 索引页面的 HTML 骨架（含纯前端过滤逻辑）
│   └── entry.template.html          # 单个链接详情页的备用模板
├── .gitignore                       # Git 忽略规则（不纳入版本控制的临时文件）
├── README.md                        # 项目概述与使用说明（当前文件）
└── LICENSE                          # MIT 许可证全文
```

## 贡献指南

1. 复刻项目仓库至个人账号，并在本地切换到新功能分支，分支命名建议采用 `feature/描述性名称` 或 `fix/问题编号` 格式。

2. 在 `scripts/` 或 `docs/` 目录下进行修改时，请确保所有 Shell 脚本均通过 `shellcheck` 检查（建议使用默认规则集），并保持 Markdown 文档的行宽不超过 120 字符。

3. 若需新增资源链接，请将链接追加至 `资源列表` 章节，并同步更新 `docs/link-management.md` 中的变更记录示例，确保文档与实际列表保持一致。

4. 提交变更前，在本地执行 `./scripts/validate-urls.sh` 验证所有已收录链接的 HTTP 状态，确保不存在 4xx 或 5xx 响应。

5. 发起 Pull Request 时，请在描述中明确说明本次变更的目的、影响范围以及是否涉及破坏性改动（如重命名现有字段或更改输出格式）。

## 常见问题

Q: 项目是否会对目标链接的内容进行缓存或备份？
A: 不会。Olive Link Aggregator 仅存储目标文件的原始 URL 地址，不下载、不缓存、不代理任何外部内容。所有访问均直接重定向至原始 GitHub 仓库地址。

Q: 如果目标文件被移动或删除，项目如何处理？
A: 项目本身不会自动删除失效链接。维护者应定期执行 `./scripts/validate-urls.sh` 检查链接状态，并根据检查结果手动更新或移除失效条目。建议在 CI 流程中集成该校验脚本。

Q: 是否支持添加非 GitHub 域名的外部链接？
A: 支持。项目对 URL 来源没有限制，任何合法的 HTTP/HTTPS 链接均可收录。但需要注意，非 GitHub 链接无法利用提交哈希进行版本锁定，失效风险由维护者自行承担。

## 许可证

MIT

> 外链数量: 6 | 生成时间: 2026-07-21 05:12:52
