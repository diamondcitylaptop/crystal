# Olive Index

Olive Index 是一个面向开发者与研究人员的轻量化技术资源导航与元数据归档项目。该项目不提供代码托管或在线服务，而是以结构化 Markdown 文档的形式，对分散在网络各处的技术文章、工具文档、社区讨论与实验性项目进行索引、摘要与分类整理。Olive Index 的目标用户包括：需要快速检索特定技术主题上下文的新手开发者、希望追踪特定仓库周边生态的研究者，以及习惯于通过命令行或静态文档浏览技术资料的高级工程师。项目本身不依赖动态后台或数据库，所有索引记录均以纯文本文件形式维护于仓库中，支持离线查阅、版本追踪与分支管理。

## 功能概览

- **主题化资源聚合**：每个索引条目按技术领域、工具名称或问题域进行标签化归类，支持多级目录组织。
- **原始内容锚点直链**：每条记录直接关联至目标文档的原始 URL，确保访问路径最短、信息失真最小。
- **元数据字段标准化**：每条索引包含标题、作者（或来源）、摘要、关键字、归档时间与原始链接字段。
- **全文检索友好**：Markdown 源文件结构清晰，可配合 grep、ripgrep 等命令行工具实现毫秒级关键词检索。
- **版本化更新日志**：通过 Git 提交记录追踪每次索引的新增、修订与删除，方便回溯历史状态。
- **外部引用完整性校验**：定期通过自动化脚本检查索引中 URL 的可达性，标记失效链接。
- **多级目录挂载**：支持按 `/topic`、`/type`、`/source` 等多维度建立虚拟视图，便于按需浏览。

## 应用场景

- **技术栈快速调研**：当团队计划引入新的开源工具时，可通过 Olive Index 查阅预先整理的相关文档、案例与讨论链接，快速形成初步认知。
- **离线文档库构建**：开发者可将 Olive Index 克隆至本地，结合静态站点生成器（如 Hugo、MkDocs）构建私有技术文档门户。
- **社区知识沉淀**：技术社区维护者可利用 Olive Index 的结构化模板，定期将社区内的高质量问答、博客与演示文稿归档，形成长期可用的知识库。

## 快速开始

```bash
# 克隆仓库
git clone https://github.com/zerxonhy/olive.git

# 进入项目根目录
cd olive

# 安装依赖（仅需 Python 3.8+ 与标准库）
# 若需运行 URL 可达性检查脚本，可安装 requests 与 aiohttp
pip install requests aiohttp

# 运行索引健康检查（可选）
python scripts/check_links.py --root ./ --output report.md

# 浏览索引内容
cat index/topics/network.md
```

## 安装要求

| 依赖项 | 必需版本 | 说明 |
|--------|----------|------|
| Git | 2.25 及以上 | 用于克隆仓库及版本管理 |
| Python | 3.8 及以上 | 运行辅助脚本（链接检查、元数据统计） |
| requests | 2.25 及以上 | 可选，用于 HTTP/HTTPS 可达性探测 |
| aiohttp | 3.8 及以上 | 可选，用于并发链接检查 |
| Markdown 解析器 | 任意 | 仅当需要生成 HTML 视图时使用，非核心必需 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|------|------|------------|
| 顶层索引 | `index/topics/` | 按技术主题划分，如 networking、security、database |
| 资源类型 | `index/types/` | 按文档形式划分，如 tutorial、paper、slides、discussion |
| 来源组织 | `index/sources/` | 按发布来源划分，如 GitHub、Medium、arXiv、Stack Overflow |
| 归档日志 | `logs/changelog.md` | 每次索引变更的时间、操作者与变更摘要 |

## 资源列表

- https://github.com/zerxonhy/olive/blob/main/rocketsignal.md
- https://github.com/zerxonhy/olive/blob/main/saffroncrystal.md
- https://github.com/zerxonhy/olive/blob/main/saffronisland.md
- https://github.com/zerxonhy/olive/blob/main/saffronwillow.md
- https://github.com/zerxonhy/olive/blob/main/shadowbridge.md
- https://github.com/zerxonhy/olive/blob/main/shadowcobalt.md

## 项目结构

```
olive/
├── index/
│   ├── topics/                # 按主题分类的主索引文件
│   │   ├── network.md         # 网络协议、代理、隧道相关内容
│   │   ├── crypto.md          # 加密算法、证书、PKI 相关内容
│   │   └── devops.md          # CI/CD、容器化、监控相关内容
│   ├── types/                 # 按资源类型分类的映射视图
│   │   ├── tutorial.md        # 教程类文档清单
│   │   ├── specification.md   # 规范、RFC 类文档清单
│   │   └── discussion.md      # 论坛、Issue 讨论类链接清单
│   └── sources/               # 按原始站点分类的索引
│       ├── github.md          # GitHub 仓库与 Gist 链接集合
│       └── external.md        # 非 GitHub 站点的链接集合
├── scripts/
│   ├── check_links.py         # 批量检查所有记录 URL 的有效性
│   └── generate_toc.py        # 自动生成各目录的汇总表格
├── assets/
│   └── templates/             # 新索引条目的 Markdown 模板
│       └── entry_template.md
├── logs/
│   └── changelog.md           # 按月记录的索引变更日志
├── config/
│   └── ignored_patterns.txt   # 链接检查时忽略的 URL 正则列表
├── README.md                  # 项目总览与使用说明
└── LICENSE                    # MIT 许可证
```

## 贡献指南

1. **创建索引条目**：从 `assets/templates/entry_template.md` 复制模板，在对应主题目录下新建 `.md` 文件，填写完整元数据。
2. **验证链接有效性**：运行 `scripts/check_links.py` 确保新增或修改的 URL 可正常访问，若返回 4xx/5xx 状态码需修正或备注。
3. **更新变更日志**：在 `logs/changelog.md` 顶部追加本次变更记录，格式为 `[YYYY-MM-DD] 操作者 变更摘要`。
4. **提交代码审查**：创建分支并提交 Pull Request，描述中需注明本次索引新增、修订或删除的具体条目及理由。
5. **合并后同步视图**：合并后执行 `scripts/generate_toc.py` 更新所有目录汇总文件，确保各维度视图一致。

## 常见问题

**Q: 索引中的链接失效了怎么办？**
A: 项目每月自动运行一次链接检查，并将失效链接输出至 `logs/broken_links.md`。维护人员或贡献者可参考该报告，通过搜索 Wayback Machine 或原作者的新地址更新对应条目。若无法找到替代链接，则将该条目移动至 `logs/archived.md` 并注明失效日期。

**Q: 如何请求新增某个特定主题的索引？**
A: 请在此仓库的 Issues 中提交新增主题请求，标题格式为 `[主题请求] 主题名称`，内容中附上至少 3 个代表性参考链接。项目维护者会在 5 个工作日内评估主题范围，并回复是否接纳该主题分类。

**Q: Olive Index 与常规书签管理器有何区别？**
A: Olive Index 并非实时同步或云存储工具，而是一个基于文本文件的静态知识整理方案。它的核心价值在于：(1) 每条记录强制包含摘要和关键字，避免仅保存 URL 导致遗忘上下文；(2) 所有数据可通过 Git 进行协作与版本控制；(3) 不依赖特定浏览器或在线服务，完全可移植。

## 许可证

MIT

> 外链数量: 6 | 生成时间: 2026-07-21 05:13:23
