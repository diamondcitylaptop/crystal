# Olive Link Collection

Olive Link Collection 是一个面向开发者与技术研究人员的结构化外链资源汇总工具。该项目通过 Markdown 文件形式对互联网上的优质技术文章、教程、工具文档及社区讨论进行索引与分类，帮助用户在特定技术领域内快速定位高价值外部资源。

项目本身不存储资源内容，而是以精心维护的链接清单与标签体系，解决技术学习中信息过载与检索效率低下的问题。目标用户包括自学者、技术团队知识管理者以及需要频繁查阅外部参考资料的开发人员。Olive Link Collection 采用纯文本格式，兼容 Git 版本控制，支持协作维护与私有化部署。

## 功能概览

- **按技术主题分类索引**：每个 Markdown 文件对应一个细粒度主题，内部链接按子主题或难度层级排列。
- **多维度标签系统**：链接附带语言、框架、适用场景等标签，便于过滤与检索。
- **定期健康检查**：通过自动化流程检测失效链接并标记，保证资源可用性。
- **版本化更新记录**：每次链接增删改均通过 Git 提交记录，可追溯变更历史。
- **社区贡献友好**：支持通过 Pull Request 提交新链接或更新已有条目，配有贡献指南与模板。
- **轻量级无依赖**：仅需标准 Markdown 解析器即可阅读，无需数据库或运行时环境。
- **可扩展元数据**：每个链接可附加摘要、推荐指数、阅读时长等自定义字段。

## 应用场景

**技术团队内部知识库补充**：技术团队可将 Olive Link Collection 作为内部 Wiki 的补充模块，用于统一存放分散在个人书签或即时通讯软件中的外部参考链接，新成员入职时可快速了解团队常用资源。

**开源项目文档的外部参考附录**：开源项目维护者可将本项目的链接清单作为项目文档的“延伸阅读”部分，减轻主文档篇幅压力，同时为用户提供更丰富的上下文信息。

**技术博客与教程的引用来源管理**：技术博主或在线课程作者可使用本项目维护写作中引用的所有外部链接，避免文章内嵌链接过多导致维护困难，也便于读者一站式获取所有引用资料。

**个人学习路径的组织与分享**：自学者可基于本项目创建个人学习分支，按学习阶段整理链接，并将成果公开分享，形成可复用的学习资源集合。

## 快速开始

以下命令可在本地完整克隆并运行 Olive Link Collection 的辅助工具（链接格式校验与状态检查）。

```bash
# 克隆仓库
git clone https://github.com/zerxonhy/olive.git
cd olive

# 安装依赖（Python 3.8+ 环境，用于运行校验脚本）
pip install -r requirements.txt

# 运行链接格式校验与基础可达性检测
python scripts/check_links.py --path ./ --recursive
```

## 安装要求

| 依赖 | 必需 | 说明 |
|------|------|------|
| Git | 是 | 用于克隆仓库及提交变更 |
| Python 3.8 或更高版本 | 否 | 仅在运行辅助校验脚本时需要 |
| pip 与 setuptools | 否 | 安装校验脚本依赖包时需要 |
| 标准 Markdown 解析器 | 否 | 任何支持 CommonMark 的解析器均可阅读 |
| 网络连接 | 否 | 本地阅读无需网络，执行链接检查时需要 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|------|------|------------|
| 顶层索引 | README.md | 项目整体定位、安装与基本使用方式 |
| 主题分类 | categories/ | 按技术领域（如前端、后端、运维）划分的链接入口 |
| 具体资源清单 | categories/*/*.md | 特定子主题下的完整外链列表与摘要信息 |
| 贡献操作 | CONTRIBUTING.md | 如何新增链接、更新链接或报告失效链接 |
| 自动化流程 | .github/workflows/ | 链接健康检查的执行频率与触发条件 |
| 变更历史 | CHANGELOG.md | 每次版本迭代涉及的链接数量变化与重要调整 |

## 资源列表

- https://github.com/zerxonhy/olive/blob/main/brightpixel.md
- https://github.com/zerxonhy/olive/blob/main/brightsilver.md
- https://github.com/zerxonhy/olive/blob/main/canvasmarble.md
- https://github.com/zerxonhy/olive/blob/main/canvassignal.md
- https://github.com/zerxonhy/olive/blob/main/cedarcoral.md
- https://github.com/zerxonhy/olive/blob/main/cedarwillow.md

## 项目结构

```
olive/
├── .github/                         # GitHub 自动化工作流配置
│   └── workflows/
│       └── link_health_check.yml    # 每周定时检测所有外链状态
├── categories/                      # 按一级技术领域分类
│   ├── frontend/                    # 前端技术相关链接
│   │   ├── react.md                 # React 生态资源清单
│   │   └── css.md                   # CSS 布局与动画资源
│   ├── backend/                     # 后端技术相关链接
│   │   ├── python.md                # Python Web 框架与工具
│   │   └── database.md              # 数据库设计与调优参考
│   ├── devops/                      # 运维与部署相关链接
│   │   ├── docker.md                # 容器化与编排资源
│   │   └── monitoring.md            # 监控与日志系统文档
│   └── general/                     # 通用开发技能
│       ├── git.md                   # Git 高级用法与工作流
│       └── regex.md                 # 正则表达式在线工具与教程
├── scripts/                         # 辅助工具脚本
│   ├── check_links.py               # 链接状态批量检测主脚本
│   └── utils.py                     # 通用工具函数（请求、解析等）
├── templates/                       # 新增资源清单的模板文件
│   └── link_template.md             # 统一条目格式（标题、标签、摘要、链接）
├── requirements.txt                 # Python 脚本依赖列表
├── CONTRIBUTING.md                  # 贡献者操作指南（步骤与规范）
├── CHANGELOG.md                     # 版本更新日志
└── README.md                        # 项目主文档（本文件）
```

## 贡献指南

1. **选择或创建主题文件**：在 `categories/` 下找到合适的分类目录，若不存在可新建 Markdown 文件，文件命名使用小写字母与连字符。
2. **遵循条目模板格式**：每个链接条目需包含标题、原始 URL、摘要说明（1-2 句）、适用标签。新增条目时请复制 `templates/link_template.md` 中的结构，确保格式统一。
3. **本地校验**：在提交前运行 `python scripts/check_links.py --path ./`，确保所有新增或修改的链接 URL 格式正确且基础域名可达。
4. **提交 Pull Request**：将变更推送到个人分支，向主仓库发起 Pull Request，并在描述中说明新增或更新的链接数量与所属主题。
5. **处理反馈**：项目维护者可能会就链接相关性、摘要准确性或格式问题提出修改意见，请在约定时间内响应并更新。

## 常见问题

**问：本项目中的链接由谁维护，如何保证链接质量？**

答：所有链接由项目维护者与社区贡献者共同维护。每次 Pull Request 合并前会经过人工审核，重点评估链接内容的技术相关性、来源可靠性以及摘要描述的准确性。同时，自动化工作流每周运行一次链接状态检查，发现失效链接后会在仓库 Issues 中记录，便于后续跟进。

**问：我想批量添加大量链接，是否有更高效的方式？**

答：对于批量提交，建议先将链接整理为 CSV 或 TSV 格式（包含标题、URL、摘要、标签四列），然后在 Issue 中附上文件内容并说明批量添加的用途。维护者评估后可协助通过脚本批量转换并生成符合模板的 Markdown 条目，减少手动编辑工作量。

## 许可证

MIT

> 外链数量: 6 | 生成时间: 2026-07-21 05:12:52
