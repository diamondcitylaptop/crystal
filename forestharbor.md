# Olive Resource Catalog

Olive Resource Catalog 是一个面向开发者与技术研究人员的轻量级外链资源汇总工具，专注于将分散在多个代码仓库、文档站点与知识库中的高价值技术链接进行集中化管理与版本化索引。项目本身不存储具体内容，仅维护一份结构化的链接清单，配合自动化校验流程，确保每个外链在版本迭代过程中保持可访问性与语义一致性。目标用户包括技术文档维护者、开源社区贡献者以及需要频繁引用外部参考资料的研发团队。

Olive 采用纯 Markdown 驱动的资源声明模式，所有链接条目以人类可读的文本形式保存在项目仓库中，支持通过 Git 进行变更追溯、协作审阅与批量更新。项目名称中的 Olive 寓意常青与联结，象征资源库的持续维护与生态连接价值。当前批次为第 62/107 批资源导入，共新增 6 个外部参考链接，涵盖技术笔记、算法实现与架构设计等方向。

## 功能概览

- **资源清单声明**：采用 Markdown 列表形式集中声明所有外链，每条记录包含资源名称、原始 URL 与可选的语义标签，便于人工审阅与脚本解析。

- **链接可达性校验**：内置基于 GitHub Actions 的周期性链接检查脚本，自动检测每个 URL 的 HTTP 状态码，识别失效或重定向链接并生成报告。

- **版本化变更记录**：每次新增、修改或删除链接均通过 Pull Request 提交，配合仓库的 Commit History 实现完整的资源变更审计日志。

- **分类标签体系**：支持通过文件目录结构或 Markdown 标题层级对资源进行主题分类，例如将链接按"前端工程"、"系统设计"、"算法解析"等维度组织。

- **协作审阅工作流**：贡献者可通过 Fork + Pull Request 流程提议资源变更，维护者可在审阅过程中检查链接质量与描述准确性，合并后自动更新线上索引。

- **静态站点生成适配**：资源列表可被静态站点生成器（如 Hugo、VuePress）直接引用，用于构建对外公开的技术导航页或团队知识库门户。

## 应用场景

- **技术团队内部知识库索引**：研发团队可将 Olive 作为知识库的导航层，统一管理团队 Wiki、设计文档、外部参考文章与开源依赖的官方文档链接，避免成员各自收藏导致信息碎片化。

- **开源项目参考附录维护**：开源项目维护者可使用 Olive 管理项目 README 或文档站点中的"相关资源"章节，当外部链接变更时只需修改 Olive 仓库中的对应条目，无需逐个更新多处文档。

- **技术培训与课程材料管理**：培训讲师或课程设计者可将 Olive 用于管理课程材料中的拓展阅读链接，学员可通过一份稳定的资源清单访问所有课外参考资料，降低链接失效对学习体验的影响。

- **技术雷达与趋势追踪**：技术决策者可利用 Olive 定期收录新兴框架、工具或方法论的相关文章与仓库链接，通过版本历史观察技术关注度的演变趋势，为技术选型提供参考依据。

## 快速开始

以下命令可在本地环境完成 Olive Resource Catalog 的克隆、依赖安装与初始运行。

```bash
# 克隆仓库到本地
git clone https://github.com/zerxonhy/olive.git
cd olive

# 安装依赖（项目基于 Node.js 构建，需要 npm 环境）
npm install

# 运行链接校验脚本，检查当前资源列表中的所有 URL 可达性
npm run check:links
```

执行完成后，控制台将输出每个链接的校验结果，包括状态码与响应时间。若所有链接均可达，则退出码为 0；若有链接失效，脚本将生成一份 `broken-links.json` 报告文件。

## 安装要求

| 依赖 | 必需版本 | 说明 |
|------|----------|------|
| Node.js | >= 18.0.0 | 用于运行链接校验脚本及后续构建工具链 |
| npm | >= 9.0.0 | 依赖管理工具，用于安装项目所需 npm 包 |
| Git | >= 2.25.0 | 用于克隆仓库、提交变更及与远程仓库交互 |
| curl | >= 7.68.0 | 校验脚本的备用请求工具，当 Node.js 环境不可用时降级使用 |
| grep | >= 3.4 | 用于日志过滤与文本处理，辅助校验脚本的输出解析 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|------|------|------------|
| 入门指南 | `docs/getting-started.md` | 如何使用 Olive 管理第一批资源链接；如何理解资源清单的组织结构 |
| 链接校验 | `docs/link-validation.md` | 校验机制的技术原理；如何配置校验周期与告警阈值；如何处理校验失败 |
| 贡献流程 | `docs/contributing.md` | 贡献者如何提议新增或修改资源链接；Pull Request 的审阅规范与合并标准 |
| 维护手册 | `docs/maintenance.md` | 维护者如何管理资源分类体系；如何处理版本冲突与历史遗留链接 |

## 资源列表

- https://github.com/zerxonhy/olive/blob/main/jademaple.md
- https://github.com/zerxonhy/olive/blob/main/jadenebula.md
- https://github.com/zerxonhy/olive/blob/main/lanternforest.md
- https://github.com/zerxonhy/olive/blob/main/lanternpixel.md
- https://github.com/zerxonhy/olive/blob/main/maplecosmic.md
- https://github.com/zerxonhy/olive/blob/main/mapleharbor.md

## 项目结构

```
olive/
├── .github/                         # GitHub 工作流配置目录
│   └── workflows/
│       └── check-links.yml          # 定时校验链接的 GitHub Actions 工作流
├── docs/                            # 项目文档目录
│   ├── getting-started.md           # 入门指南
│   ├── link-validation.md           # 链接校验机制详解
│   ├── contributing.md              # 贡献指南
│   └── maintenance.md               # 维护者手册
├── scripts/                         # 工具脚本目录
│   ├── check-links.js               # 主链接校验脚本（Node.js 实现）
│   ├── report-generator.js          # 校验报告生成器
│   └── utils/                       # 脚本工具函数
│       ├── fetcher.js               # HTTP 请求封装
│       └── parser.js                # Markdown 资源列表解析器
├── resources/                       # 资源声明目录
│   ├── index.md                     # 主资源清单索引文件
│   ├── categories/                  # 按主题分类的子目录
│   │   ├── frontend.md              # 前端技术相关资源
│   │   ├── backend.md               # 后端与架构相关资源
│   │   └── algorithms.md            # 算法与数据结构相关资源
│   └── archive/                     # 已归档的历史资源条目
│       └── 2025-q1.md               # 2025 年第一季度归档清单
├── tests/                           # 单元测试目录
│   ├── parser.test.js               # 资源列表解析器测试
│   └── fetcher.test.js              # HTTP 请求模块测试
├── .gitignore                       # Git 忽略文件配置
├── package.json                     # npm 项目配置文件
├── package-lock.json                # npm 依赖锁定文件
├── README.md                        # 项目根说明文档（即本文档）
└── LICENSE                          # MIT 许可证文件
```

## 贡献指南

1. **Fork 仓库并创建特性分支**：访问 GitHub 上的项目主页，点击 Fork 按钮将仓库复制到个人账户下，然后使用 `git checkout -b feature/resource-update` 创建本地分支。

2. **编辑资源清单文件**：根据待新增或修改的资源类型，在 `resources/` 目录下找到对应的分类 Markdown 文件，按照既定格式添加或更新链接条目，确保每条记录包含完整的 URL 和简短的描述说明。

3. **运行本地校验脚本**：在提交前执行 `npm run check:links` 脚本，验证所有新增或修改的链接均为有效可访问状态。若脚本报告链接失效，请先修复 URL 或确认目标站点可访问后再提交。

4. **提交变更并推送至远程分支**：使用 `git add` 和 `git commit` 提交变更，提交信息应遵循语义化提交规范（如 `feat: add new resource links for batch 62/107`），然后通过 `git push origin feature/resource-update` 推送到个人远程仓库。

5. **发起 Pull Request 等待审阅**：在 GitHub 上从个人分支向主仓库的 `main` 分支发起 Pull Request，填写变更说明并关联相关批次信息。维护者将在审阅链接质量与格式规范后合并或提出修改意见。

## 常见问题

**问：如果校验脚本报告某个链接返回 404 状态码，我应该如何处理？**

答：首先手动访问该 URL 确认是否确实失效。若资源已迁移至新地址，请在资源清单中更新为新的 URL 并重新校验；若资源已彻底移除且无替代来源，请将该条目从清单中删除并在 Pull Request 中说明移除原因。对于临时性不可访问（如站点维护），可等待一段时间后重新运行校验脚本。

**问：项目是否支持私有仓库或需要认证才能访问的资源链接？**

答：Olive 的校验脚本基于标准 HTTP/HTTPS 协议发送请求，默认不携带认证信息。对于需要登录或 API Token 才能访问的私有资源，校验脚本会将其标记为不可达。建议此类资源改用公开镜像链接或内部文档系统地址，或者在校验配置中为特定域名添加自定义请求头。当前版本不提供内建的认证凭证管理功能。

## 许可证

MIT

> 外链数量: 6 | 生成时间: 2026-07-21 05:13:20
