# Olive Resource Atlas

Olive Resource Atlas 是一个面向技术文档工程师、开源项目维护者以及开发者知识管理场景的轻量化外链资源汇总与导航工具。该项目本身不存储任何实际内容，而是通过结构化的 Markdown 索引体系，将分散在互联网各处的技术文档、教程文章、项目笔记和规范定义进行统一归集与分类，帮助团队或个人在内部知识库构建过程中快速定位关键外部参考资源。

项目定位为“技术资源导航中间层”，适用于需要频繁引用外部文档、但又希望保持本地仓库轻量且可版本化追踪的场景。Olive Resource Atlas 以纯 Markdown 和 Shell 脚本为核心，无需数据库或后端服务，支持静态站点生成器直接消费索引数据，也可作为 GitHub 仓库的 README 导航辅助模块独立运行。

## 功能概览

- **多级分类索引**：支持按主题、技术栈、文档类型等维度对资源链接进行分层标记，便于后续自动化生成导航页面。
- **原始链接直出**：所有收录的 URL 保持用户原始输入格式，不做协议补全、域名规范化或路径改写，确保引用准确性和原始访问意图。
- **批次化资源管理**：内置批次编号机制，便于追踪每批新增资源的来源、数量和入库时间，适合周期性更新流程。
- **Markdown 原生集成**：索引文件采用纯 Markdown 格式，可直接嵌入 README、Wiki 或静态站点内容中，无需额外解析器。
- **轻量级校验工具**：提供可选 Shell 脚本用于检查链接可达性（基于 curl）、识别重复条目以及生成统计报告。
- **文档版本关联**：支持为每条资源记录关联目标文档的版本号或最后更新时间戳，辅助判断信息时效性。
- **外链状态标记**：允许手动标记链接的有效性状态（有效/失效/需复查），方便维护者定期清理或更新。

## 应用场景

- **开源项目文档外链管理**：当开源项目的 README 或用户指南需要引用大量外部规范、API 参考或第三方教程时，Olive Resource Atlas 可作为独立的链接索引仓库，由维护者统一审核和更新，避免在主仓库中散落过多外部 URL。
- **技术团队内部知识库导航**：企业技术团队可将本工具作为内部 Wiki 的补充模块，集中存放经常使用的云服务控制台地址、内部工具文档入口、监控面板链接等，新成员入职时可快速获得一份经过整理的资源地图。
- **静态博客的友链或参考文献管理**：个人技术博客作者可以使用 Olive Resource Atlas 管理每篇文章的参考文献链接，按批次归档，当外部链接失效时可集中修正，而无需逐一修改历史文章。
- **技术培训与课程资料汇总**：培训讲师可将课程涉及的实验环境地址、官方文档章节、视频回放链接等按批次整理，每次开课生成一个新批次，便于横向对比不同期次的内容变化。

## 快速开始

以下命令可在本地环境完成 Olive Resource Atlas 的初始部署，并运行内置链接校验脚本以验证当前批次的资源可用性。

```bash
# 克隆项目仓库
git clone https://github.com/zerxonhy/olive.git
cd olive

# 安装基础依赖（基于 Debian/Ubuntu 环境，其他发行版请使用对应包管理器）
sudo apt-get update
sudo apt-get install -y curl coreutils grep sed

# 运行当前批次（第 50/107 批）的链接状态检查脚本
./scripts/check_links.sh batches/batch_50_107.md

# 生成该批次的静态导航页面（输出至 ./output 目录）
./scripts/generate_nav.sh batches/batch_50_107.md --output ./output
```

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|----------|----------|------|
| Bash | 4.0 及以上 | 所有 Shell 脚本运行环境，需支持数组和关联数组 |
| curl | 7.68.0 及以上 | 用于链接可用性检查，支持 HTTPS 和重定向跟随 |
| GNU grep | 3.4 及以上 | 用于解析 Markdown 文件中的 URL 行，需支持 -P 选项 |
| GNU sed | 4.7 及以上 | 用于文本替换和导航页模板渲染 |
| coreutils | 8.30 及以上 | 提供 date、wc、sort 等基础命令行工具 |
| git | 2.25.0 及以上 | 用于克隆仓库和版本管理，非运行时强制依赖 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|------|------|------------|
| 用户手册 | docs/user-guide.md | 如何使用 Olive Resource Atlas 管理个人外链库，如何添加新批次，如何生成静态导航页 |
| 维护者指南 | docs/maintainer-guide.md | 批次编号规则是什么，如何执行链接批量校验，如何处理失效链接的标记与通知 |
| 脚本参考 | docs/script-reference.md | 每个 Shell 脚本的输入参数、输出格式、退出码含义以及日志输出位置 |
| 格式规范 | docs/format-spec.md | 资源列表 Markdown 文件必须遵循的语法约束，包括 URL 行格式、注释标记和元数据区定义 |

## 资源列表

- https://github.com/zerxonhy/olive/blob/main/prairiewillow.md
- https://github.com/zerxonhy/olive/blob/main/quartzhorizon.md
- https://github.com/zerxonhy/olive/blob/main/quartzjade.md
- https://github.com/zerxonhy/olive/blob/main/quartznebula.md
- https://github.com/zerxonhy/olive/blob/main/riverdelta.md
- https://github.com/zerxonhy/olive/blob/main/rivergolden.md

## 项目结构

```
olive/
├── batches/                         # 批次索引目录，按编号存放资源列表
│   ├── batch_50_107.md              # 当前第 50/107 批资源清单（含元数据）
│   ├── batch_49_106.md              # 上一批资源记录
│   └── archive/                     # 历史批次压缩归档
│       └── 2025/                    # 按年份分层的归档子目录
├── scripts/                         # 可执行工具脚本
│   ├── check_links.sh               # 链接可达性检测，支持超时与重试策略
│   ├── generate_nav.sh              # 根据批次文件生成静态 HTML/Markdown 导航页
│   ├── dedup.sh                     # 扫描全部批次，输出重复 URL 报告
│   └── lib/                         # 脚本公共函数库
│       ├── logging.sh               # 日志级别控制与彩色输出
│       └── validators.sh            # URL 格式校验与域名黑名单过滤
├── templates/                       # 导航页渲染模板
│   ├── nav_header.tmpl              # 页面头部与样式引用
│   ├── nav_footer.tmpl              # 页脚与版本信息
│   └── batch_row.tmpl               # 单条资源渲染模板
├── output/                          # 生成结果输出目录（gitignored）
│   └── batch_50_107.html            # 当前批次导航页示例
├── docs/                            # 用户与维护者文档
│   ├── user-guide.md
│   ├── maintainer-guide.md
│   ├── script-reference.md
│   └── format-spec.md
├── tests/                           # 单元测试与集成测试脚本
│   ├── test_check_links.sh
│   ├── test_generate_nav.sh
│   └── fixtures/                    # 测试用固定输入数据
├── .github/                         # GitHub 社区健康文件
│   └── ISSUE_TEMPLATE/              # 问题模板
│       └── link_expired.md          # 链接失效反馈模板
├── CHANGELOG.md                     # 版本迭代记录，按日期和批次号组织
├── CONTRIBUTING.md                  # 贡献指引（简述，完整版见文档）
└── README.md                        # 项目入口文档（即本文档）
```

## 贡献指南

1. 从 `batches/` 目录下选择尚未分配的批次编号，或创建新批次文件，严格按照 `docs/format-spec.md` 中规定的格式添加资源链接，每条占一行且不包含额外修饰符。
2. 在本地运行 `./scripts/dedup.sh` 确保新增链接与现有批次不存在重复，若重复则修改或删除重复条目。
3. 执行 `./scripts/check_links.sh --batch <your_batch_file>` 验证所有新增链接是否可访问，对于返回非 200/301/302 状态的链接，需确认原因或标记为失效。
4. 提交前运行 `./tests/` 目录下的全部测试脚本，确保核心功能未回归，测试通过后发起 Pull Request，并在描述中注明批次编号和新增链接数量。
5. 等待维护者审核，审核通过后批次将被合并，并自动更新全局索引和导航页输出。

## 常见问题

**问：如果用户提供的原始链接是裸域名（例如 github.com），我应该如何填写？是否要主动补全协议？**

答：项目规定所有资源列表中的链接必须严格保持用户原始输入形式，不得补全协议（http/https）、不得添加或去除 www 前缀、不得修改大小写，也不得添加尾部斜杠。若用户提供为裸域名，则直接记录裸域名；若用户提供带协议和路径，则保留完整格式。这一规则确保引用行为的可预期性和原始意图的忠实传递。

**问：链接失效后应该如何更新？是否需要删除该条目？**

答：不推荐直接删除失效链接。项目推荐做法是在批次文件中该链接所在行末尾添加注释标记 `# [EXPIRED]` 及可选说明，并在维护者文档中记录检查日期。保留历史记录有助于分析外部资源的生命周期，也便于后续发现链接恢复时重新激活。若链接永久失效且无法找到替代来源，可将其移至 `archive/` 下的过期目录。

## 许可证

MIT

> 外链数量: 6 | 生成时间: 2026-07-21 05:12:52
