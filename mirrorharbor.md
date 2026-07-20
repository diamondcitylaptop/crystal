# Olive Link Atlas

Olive Link Atlas 是一个面向开发者和技术研究人员的结构化外链资源聚合与导航系统。该项目并非传统的 Web 应用或库框架，而是一个基于 Markdown 与 Git 版本管理的资源索引仓库，旨在解决技术文档、代码示例、社区讨论及配置模板等分散于互联网各处、难以统一检索与追溯的问题。项目目标用户包括架构师、运维工程师、开源贡献者以及需要频繁查阅底层实现细节的资深开发者。

本项目通过将原始素材链接封装为带有上下文标签和摘要描述的结构化条目，并提供本地检索与分类浏览能力，使得用户无需依赖特定在线服务即可在本地维护一套高可用的技术外链知识库。Olive Link Atlas 强调数据主权与长期可维护性，所有资源索引均以纯文本形式存储，支持标准 Git 工作流，便于团队共享和版本回溯。

## 功能概览

- **原始链接无损收录** 支持将任意 HTTP/HTTPS 协议链接按原始格式导入索引库，保留协议头、域名及路径大小写，确保跳转准确率百分之百。
- **多级标签分类系统** 每个资源条目可绑定多个技术领域标签，如 `network`、`storage`、`security`、`rust`、`kernel`，支持按标签组合进行快速过滤。
- **摘要与上下文批注** 允许为每条链接添加自定义摘要说明、阅读优先级及关联 Issue 编号，方便团队内部知识传递。
- **本地 CLI 检索工具** 内置 Python 脚本，支持基于关键词、标签、文件名模式的正则搜索，输出结果包含链接、摘要及最后更新时间。
- **变更历史审计** 利用 Git 提交日志记录所有增删改操作，可追溯任意资源条目的引入原因和修改责任人。
- **结构化 Markdown 渲染** 索引数据以特定 Front Matter 格式存储于 `.md` 文件中，可直接在 GitHub/GitLab 上预览，也支持通过 CI 流水线生成静态 HTML 站点。

## 应用场景

- **微服务架构依赖梳理** 团队在拆分单体应用时，需要查阅大量服务注册、配置中心、熔断降级相关的官方文档和最佳实践。Olive Link Atlas 可将这些分散的链接统一归档，并按 `service-mesh`、`config` 等标签归类，减少重复搜索时间。
- **开源项目贡献参考** 当开发者准备向知名开源项目提交 PR 时，通常需要参考其贡献指南、编码风格规范以及相似功能的实现代码。本项目的索引库可收录这些参考链接，并附带社区讨论帖的摘要，帮助贡献者快速理解项目维护者的偏好。
- **安全漏洞响应跟踪** 安全工程师需要监控多个 CVE 数据库、厂商安全公告及第三方漏洞分析博客。Olive Link Atlas 允许按 `CVE`、`patch`、`advisory` 等标签组织链接，并记录每个漏洞的处置状态，形成内部安全知识时间线。
- **新成员入职培训路径** 将内部架构文档、核心业务流程图、CI/CD 流水线配置模板、代码规范等链接整理为一条培训路径，新人可通过索引库顺序阅读，并随时在本地添加个人笔记链接而不影响主库。

## 快速开始

以下命令演示如何在本地克隆 Olive Link Atlas 仓库、安装基础依赖并运行内置检索脚本。

```bash
# 克隆项目仓库
git clone https://github.com/zerxonhy/olive.git olive-link-atlas
cd olive-link-atlas

# 安装 Python 依赖（建议使用虚拟环境）
python3 -m venv .venv
source .venv/bin/activate
pip install --upgrade pip
pip install pyyaml termcolor

# 运行索引构建脚本，生成本地检索数据库
python scripts/build_index.py --input ./entries --output ./index.db

# 执行关键词检索示例
python scripts/search.py --keyword "timber" --format table
```

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|---|---|---|
| Git | 2.25 及以上 | 用于克隆仓库及提交变更记录 |
| Python | 3.8 及以上 | 运行检索脚本及索引构建工具 |
| pip | 21.0 及以上 | 安装 Python 依赖包 |
| pyyaml | 6.0 | 解析条目元数据中的 YAML 头部信息 |
| termcolor | 2.0 | 为 CLI 检索结果提供彩色高亮输出 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|---|---|---|
| 入门指南 | `docs/getting-started.md` | 如何首次初始化索引库、配置个人标签别名 |
| 条目编辑规范 | `docs/entry-format.md` | 新增或修改资源条目的 Markdown 格式要求与 Front Matter 字段说明 |
| CLI 命令参考 | `docs/cli-commands.md` | `build_index`、`search`、`export` 等子命令的参数详解与示例 |
| 高级工作流 | `docs/advanced-workflow.md` | 如何通过 Git Hook 自动校验条目 URL 有效性、如何合并上游更新 |

## 资源列表

- https://github.com/zerxonhy/olive/blob/main/timberbright.md
- https://github.com/zerxonhy/olive/blob/main/timbercoral.md
- https://github.com/zerxonhy/olive/blob/main/timbersaffron.md
- https://github.com/zerxonhy/olive/blob/main/velvetcedar.md
- https://github.com/zerxonhy/olive/blob/main/velvetisland.md
- https://github.com/zerxonhy/olive/blob/main/velvetrocket.md

## 项目结构

```
olive-link-atlas/
├── entries/                         # 核心资源条目目录，按领域划分
│   ├── networking/                  # 网络协议、负载均衡、DNS 相关链接
│   │   ├── timberbright.md          # 条目示例：包含 YAML 头部与摘要
│   │   └── velvetcedar.md           # 条目示例：侧重 TCP 调优参数
│   ├── storage/                     # 数据库、对象存储、缓存系统链接
│   │   ├── timbercoral.md           # 条目示例：分布式事务讨论
│   │   └── velvetisland.md          # 条目示例：LSM 树实现分析
│   ├── security/                    # 认证授权、加密、漏洞公告链接
│   │   ├── timbersaffron.md         # 条目示例：JWT 安全实践
│   │   └── velvetrocket.md          # 条目示例：TLS 1.3 特性解读
│   ├── observability/               # 监控、日志、链路追踪链接
│   │   └── (待扩展)
│   └── ci-cd/                       # 流水线配置、容器编排链接
│       └── (待扩展)
├── scripts/                         # 可执行工具脚本
│   ├── build_index.py               # 解析 entries 下所有 md 文件生成索引
│   ├── search.py                    # 交互式检索入口
│   └── utils/                       # 公共辅助函数
│       ├── parsers.py
│       └── validators.py
├── docs/                            # 用户文档
│   ├── getting-started.md
│   ├── entry-format.md
│   ├── cli-commands.md
│   └── advanced-workflow.md
├── tests/                           # 单元测试与集成测试
│   ├── test_parsers.py
│   └── fixtures/                    # 测试用示例条目
├── .gitignore                       # 忽略 .venv、*.db、__pycache__
├── README.md                        # 本文件
└── LICENSE                          # MIT 许可证
```

## 贡献指南

1.  **Fork 仓库并创建功能分支**：从主仓库 Fork 到个人账户，然后基于 `main` 分支创建 `feature/your-feature-name` 分支，避免直接在主分支上操作。
2.  **遵循条目格式规范**：新增或修改 `entries/` 目录下的 `.md` 文件时，必须包含 YAML Front Matter，字段包括 `title`、`tags`、`source`、`priority`，正文部分需撰写至少两行中文摘要说明链接内容与价值。
3.  **本地自检**：在提交前，运行 `python scripts/build_index.py --strict` 确保所有新增条目通过格式校验，且无重复 URL 或无效标签。
4.  **编写变更日志**：在 `docs/CHANGELOG.md` 中简要记录本次变更的目的和影响范围，便于其他贡献者审阅。
5.  **发起 Pull Request**：将分支推送至 GitHub，并创建 PR，描述中需关联相关 Issue 编号（若有），并勾选自检清单。等待维护者审核，根据反馈进行修改直至合并。

## 常见问题

**Q：导入的原始链接如果失效怎么办？**

项目内置了 `validate_urls.py` 脚本，可定期对索引库中的所有链接进行 HEAD 请求检查。建议用户每周运行一次该脚本，并将失效链接的条目移入 `entries/deprecated/` 目录，同时保留历史记录以便追溯。CI 流水线也可配置为每日自动执行检测并生成报告。

**Q：如何与团队共享我的本地标签分类方案？**

标签分类规则统一记录在根目录的 `taxonomy.yaml` 文件中。您可以将该文件提交至仓库，团队其他成员拉取后即获得一致的标签体系。若需扩展新标签，请先在团队内沟通，并同步更新 `taxonomy.yaml` 的 `allowed_tags` 列表，避免检索时标签名歧义。

**Q：是否支持从在线书签服务（如 Pocket、Raindrop）批量导入？**

当前版本未内置直接导入功能，但项目提供了 `scripts/import_csv.py` 脚本，可将符合格式（列顺序：`url,title,tags,note`）的 CSV 文件转换为标准条目文件。用户可从大多数书签服务导出 CSV，再执行该脚本完成批量迁移。后续版本将考虑增加对 HTML 书签导出文件的解析支持。

## 许可证

MIT

> 外链数量: 6 | 生成时间: 2026-07-21 05:13:15
