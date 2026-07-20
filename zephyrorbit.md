# Olive Resource Atlas

Olive Resource Atlas 是一个面向开发者与技术研究人员的结构化外链资源汇总工具。项目以纯 Markdown 文件为载体，将散落在 GitHub 仓库、技术文档与社区讨论中的高质量参考链接按主题域进行归集与标注，形成可追溯、可扩展的知识索引体系。本项目不提供新的技术框架或库实现，而是致力于解决技术信息过载环境下的资源发现与路径导航问题，适用于需要快速建立某一技术领域知识图谱的个体或团队。

本项目定位为静态资源索引层，所有条目均以文本文件形式存储在 `olive` 仓库的 `main` 分支下，用户可通过文件路径直接访问原始内容。项目遵循“最小化维护”原则，不依赖数据库或后端服务，仅依靠 Git 版本控制进行内容更新与历史回溯。目标用户包括技术文档撰写者、开源项目维护者、技术调研人员以及需要系统化学习某一技术栈的开发者。

## 功能概览

- **主题化文件聚合**：每个 Markdown 文件对应一个独立主题域，如 `islandcrystal.md` 聚焦于分布式系统一致性模型相关内容，`lanternforest.md` 关注网络协议与边缘计算资源。文件内部按子主题段落组织链接，并附有简要说明。

- **链接状态标注**：每个资源条目包含链接标题、原始 URL、归档日期及访问状态（有效/失效/需代理）。状态信息通过文件头部的 YAML Front Matter 或表格列进行记录，便于定期巡检。

- **跨文件交叉引用**：主题文件之间通过相对路径链接实现相互引用，例如 `jadeatlas.md` 中会引用 `jademaple.md` 中的某些通用资源，形成网状知识结构。引用关系在文件末尾的“参见”段落中明确列出。

- **版本变更日志**：每个文件底部维护独立的变更记录表格，记录每次新增、删除或修改资源链接的日期与简要说明。变更日志与 Git 提交历史互补，提供面向内容的审计线索。

- **模板化新建流程**：项目根目录提供 `TEMPLATE.md` 模板文件，新主题文件可复制模板并填写相应段落，确保所有文件保持一致的段落结构与标注格式，降低维护成本。

- **批量检查脚本**：`scripts/check_links.sh` 提供基于 `curl` 的批量链接可用性检查，支持输出 JSON 格式报告，便于集成到 CI 流程中定时触发。

- **静态站点生成支持**：文件结构设计兼容 MkDocs 与 VuePress 等静态站点生成器，用户可通过配置 `mkdocs.yml` 将整个资源集转化为可浏览的 HTML 站点，支持全文搜索与标签筛选。

## 应用场景

- **技术调研阶段资源归档**：当研发团队需要对某一新兴技术领域（如 WebAssembly 或 eBPF）进行系统调研时，可使用 Olive Resource Atlas 创建主题文件，将发现的论文、演讲视频、开源项目与最佳实践文档统一归档，并共享给团队成员。每个资源条目附带简短的摘要与适用场景说明，帮助他人快速判断阅读优先级。

- **开源项目文档的外部参考附录**：开源项目维护者可将 Olive Resource Atlas 中的相关主题文件链接加入项目 README 的“参考文献”或“延伸阅读”章节，为使用者提供经过筛选的外部学习材料，降低项目上手门槛。例如，一个消息队列项目可引用 `islandcrystal.md` 中关于一致性哈希的资源。

- **个人知识管理体系的骨架**：技术博主或终身学习者可使用本项目作为个人知识管理（PKM）系统的外部资源层，将日常阅读中发现的优质链接按主题分类存入对应文件，并通过交叉引用构建主题之间的语义关联。相比纯标签系统，文件路径本身即蕴含分类层次，便于后期回顾与整理。

- **团队内部周报素材库**：技术团队可将 Olive Resource Atlas 作为周报“行业动态”栏目的素材来源。每周由一位成员负责更新 `jadenebula.md` 或 `lanternforest.md` 中与团队业务相关的链接，其他成员可直接从文件中提取信息撰写周报，减少重复搜索时间。

## 快速开始

以下命令可完成项目克隆、依赖安装与本地预览环境的启动。

```bash
# 克隆仓库
git clone https://github.com/zerxonhy/olive.git
cd olive

# 安装链接检查工具依赖（基于 Debian/Ubuntu）
sudo apt-get update
sudo apt-get install -y curl jq moreutils

# 运行链接状态检查（示例：检查 islandcrystal.md 中的所有外链）
./scripts/check_links.sh -f islandcrystal.md -o report.json

# 若需生成静态站点（需 Python 3.8+ 及 mkdocs）
pip install mkdocs mkdocs-material
mkdocs build --clean
mkdocs serve --dev-addr=127.0.0.1:8000
```

## 安装要求

| 依赖项 | 必需版本 | 说明 |
|--------|----------|------|
| Git | 2.25.0 或更高 | 用于克隆仓库及提交内容变更 |
| Bash | 4.0 或更高 | 运行 `scripts/` 目录下的 Shell 检查脚本 |
| curl | 7.68.0 或更高 | 用于发送 HTTP 请求以验证链接可用性 |
| jq | 1.5 或更高 | 解析 `check_links.sh` 输出的 JSON 报告 |
| Python | 3.8 至 3.11 | 仅当使用 MkDocs 生成静态站点时需要 |
| mkdocs-material | 9.0.0 或更高 | 可选依赖，用于站点主题渲染 |
| GNU sed | 4.7 或更高 | 用于脚本中的文本替换操作 |
| findutils | 4.7.0 或更高 | 提供 `find` 命令用于文件遍历 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|------|------|------------|
| 主题资源文件 | `./*.md`（根目录） | 每个主题文件包含哪些外部链接？链接的摘要与状态如何？ |
| 模板与规范 | `./TEMPLATE.md`、`./CONTRIBUTING.md` | 新建主题文件时应遵循什么段落结构与元数据格式？ |
| 自动化脚本 | `./scripts/` | 如何批量检查链接有效性？如何生成统计报表？ |
| 站点配置 | `./mkdocs.yml`、`./docs/` | 如何将 Markdown 资源集转为可搜索的 HTML 站点？ |
| 变更历史 | 每个文件底部的“变更记录”表格 | 某条链接是什么时候加入的？之前是否被删除或替换过？ |
| 全局索引 | `./INDEX.md` | 所有主题文件的完整列表及其简要描述，便于全局检索 |

## 资源列表

- https://github.com/zerxonhy/olive/blob/main/islandcrystal.md
- https://github.com/zerxonhy/olive/blob/main/islandfield.md
- https://github.com/zerxonhy/olive/blob/main/jadeatlas.md
- https://github.com/zerxonhy/olive/blob/main/jademaple.md
- https://github.com/zerxonhy/olive/blob/main/jadenebula.md
- https://github.com/zerxonhy/olive/blob/main/lanternforest.md

## 项目结构

```
olive/
├── .github/                         # GitHub 社区模板与 CI 配置
│   └── workflows/
│       └── link-check.yml           # 每周一 03:00 触发批量链接检查
├── scripts/                         # 维护工具脚本
│   ├── check_links.sh               # 单文件链接检查，支持 -f 指定文件
│   ├── generate_index.sh            # 自动生成 INDEX.md 全局索引表
│   └── stats.py                     # 统计各文件链接数量与状态分布
├── docs/                            # MkDocs 静态站点源文件目录
│   ├── index.md                     # 站点首页，重定向至根目录 README
│   └── overrides/                   # 主题自定义样式覆盖
├── islandcrystal.md                 # 主题：分布式一致性（含 Raft/Paxos/ZAB）
├── islandfield.md                   # 主题：容器编排与调度（K8s/Nomad）
├── jadeatlas.md                     # 主题：服务网格与流量管理（Envoy/Linkerd）
├── jademaple.md                     # 主题：可观测性与监控（Prometheus/OTel）
├── jadenebula.md                    # 主题：云原生存储（Ceph/Longhorn）
├── lanternforest.md                 # 主题：边缘计算与 IoT 协议（MQTT/CoAP）
├── TEMPLATE.md                      # 新主题文件复制起点，含完整段落骨架
├── CONTRIBUTING.md                  # 贡献指南详细版（含提交消息规范）
├── INDEX.md                         # 自动生成的全局索引（不手动编辑）
├── mkdocs.yml                       # MkDocs 站点配置文件，定义导航结构
├── README.md                        # 本文件，项目总览与快速入门
└── LICENSE                          # MIT 许可证全文
```

## 贡献指南

1.  **新建主题文件**：复制 `TEMPLATE.md` 至根目录，命名为 `<主题名>.md`。主题名使用小写字母与连字符，需简要概括资源方向。填写文件头部的 YAML Front Matter，包含 `title`、`description`、`created` 与 `tags` 字段。

2.  **添加资源条目**：在“资源列表”章节下按 `- [标题](URL) - 摘要` 格式新增条目。摘要部分控制在 15 个汉字以内，注明资源类型（论文/博客/仓库/视频）。新增条目后，需在文件底部的“变更记录”表格中增加一行，记录日期与操作说明。

3.  **运行本地检查**：在提交 Pull Request 前，执行 `./scripts/check_links.sh -f <你的文件名>.md` 确保所有外链可访问。若链接返回 4xx 或 5xx 状态码，需确认是否为临时故障，若为永久失效则替换为可用链接或删除该条目。

4.  **同步全局索引**：若新增或删除主题文件，需执行 `./scripts/generate_index.sh` 更新 `INDEX.md`。该脚本会扫描根目录下所有 `*.md` 文件（除 `README.md`、`TEMPLATE.md`、`INDEX.md` 及 `docs/` 下文件），提取 YAML Front Matter 中的标题与描述，生成按创建时间排序的索引表格。

5.  **提交 Pull Request**：提交信息需遵循 `[主题名] 操作类型: 简要描述` 格式，例如 `[islandcrystal] add: 新增 etcd Raft 实现解析博客链接`。PR 描述中需附带 `check_links.sh` 的输出摘要，证明新增链接均有效。

## 常见问题

**Q: 如果某个外链临时无法访问，但资源本身仍有价值，应该如何处理？**

A: 在资源条目后添加 `[失效]` 标注，并在“备注”列中记录最后一次成功访问的日期。同时，尝试寻找替代 URL（如 Wayback Machine 存档或官方镜像站），将替代链接以“备选”形式附在原链接下方。若链接持续不可用超过 60 天，将在月度维护时移除该条目，并记录于变更日志中。

**Q: 主题文件之间的交叉引用应该如何维护，以避免循环依赖？**

A: 交叉引用应保持单向性，即从更具体的主题指向更通用的主题。例如，`jadenebula.md`（云原生存储）可以引用 `islandcrystal.md`（分布式一致性），但反向引用应避免，因为存储主题并不为一致性主题提供必要的上下文。所有交叉引用均使用相对路径，并在引用段落后附上简短说明为何需要参见该文件。项目维护者会在定期复审时检查引用图的层级深度，确保不超过三层。

**Q: 如何将我自己的博客或开源项目添加到合适的主题文件中？**

A: 请先评估您的资源是否与目标主题高度相关，且能为其他读者带来独立的参考价值。我们不收录仅用于个人宣传且缺乏实质技术内容的链接。若符合标准，请按照贡献指南第 2 条格式提交 Pull Request。对于新出现的细分领域，如果现有主题文件均无法覆盖，您也可以按照贡献指南第 1 条新建主题文件，但需在 PR 中说明该领域目前的资源丰富程度与合并必要性。

## 许可证

MIT

> 外链数量: 6 | 生成时间: 2026-07-21 05:12:52
