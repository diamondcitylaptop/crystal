# Olive Index

Olive Index 是一个面向开发者与研究人员的技术资源外链汇总与导航系统，定位于从分散的代码仓库、技术笔记、讨论帖与实验文档中提取高价值参考资料，并以可检索、可分类、可版本化的目录结构进行统一管理。该项目主要服务于需要持续跟踪多个上游仓库变更、维护私有技术知识库或构建内部开发者门户的团队与个人。Olive Index 不存储资源实体内容，而是通过稳定的 Markdown 索引文件记录外部链接、摘要标签与快照元数据，从而实现轻量级、低维护成本的技术资源聚合。

## 功能概览

- 多源链接聚合：支持从 GitHub 仓库、技术博客、官方文档等渠道批量导入链接，并按自定义标签体系自动归类。
- 索引版本控制：所有索引文件以 Markdown 形式存储在 Git 仓库中，支持提交历史追溯、差异对比与回滚。
- 标签与全文检索：内置基于 grep 与 ripgrep 的轻量级检索方案，可按标签、文件名、内容片段快速定位资源。
- 快照元数据记录：为每个外链记录添加时间戳、抓取状态码、内容摘要哈希值，便于检测目标页面变更。
- 每日自动更新：通过 GitHub Actions 或 cron 任务定时拉取上游仓库的索引分支，合并新增或变更的链接条目。
- 结构化输出格式：支持生成 JSON、CSV 与 HTML 三种导出格式，便于接入其他监控系统或静态站点生成器。
- 链接可用性检查：周期性对已收录链接发起 HEAD 请求，标记失效或重定向条目，生成健康报告。

## 应用场景

1. 技术团队内部知识库维护：团队可将常用的 API 文档、设计提案、故障复盘笔记等外部链接统一收录到 Olive Index，通过标签区分项目或模块，新成员入职时可快速了解项目依赖的技术资源全景。

2. 开源项目依赖追踪：开源维护者可以使用 Olive Index 记录上游依赖库的变更日志、迁移指南或安全公告链接，当上游发布新版本时，通过索引变更提醒快速评估影响范围。

3. 技术调研与竞品分析：研究人员在调研多个竞品或技术方案时，可将各方的官网、技术白皮书、性能测试报告等链接集中索引，并通过摘要字段记录每个方案的核心特点，方便横向对比。

4. 个人开发者笔记整理：个人开发者可将日常浏览中发现的有价值文章、代码片段仓库、在线工具等链接存入 Olive Index，配合标签和全文检索，构建属于自己的技术外链数据库。

## 快速开始

```bash
# 克隆项目仓库
git clone https://github.com/zerxonhy/olive.git
cd olive

# 安装基础依赖（仅需 Git 与 Python 3.8+）
python -m venv venv
source venv/bin/activate
pip install -r requirements.txt

# 运行索引初始化，生成目录结构与示例索引文件
python scripts/init_index.py --config config/default.yaml

# 执行首次链接抓取与状态检查
python scripts/fetch_metadata.py --target index/ --output reports/
```

## 安装要求

| 依赖项 | 必需版本 | 说明 |
|--------|----------|------|
| Git | 2.20 及以上 | 用于克隆仓库、提交索引变更以及拉取上游更新 |
| Python | 3.8 至 3.11 | 运行索引管理脚本、元数据抓取与格式转换工具 |
| ripgrep | 13.0 及以上 | 可选，用于提高全文检索速度，未安装时自动降级为 grep |
| curl | 7.68 及以上 | 用于执行链接可用性检查中的 HTTP 请求 |
| yq | 4.25 及以上 | 可选，用于在 shell 脚本中解析 YAML 格式的配置文件 |
| GNU Make | 3.81 及以上 | 用于执行预定义的任务组合，如更新、检查、导出 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|------|------|------------|
| 用户手册 | docs/user-guide/ | 如何添加链接、使用标签、检索索引以及导出不同格式 |
| 维护指南 | docs/maintainer-guide/ | 如何配置自动更新、处理链接失效、合并上游索引变更 |
| 设计文档 | docs/design/ | Olive Index 的元数据模型、目录结构规范及扩展点设计 |
| 示例索引 | examples/ | 提供完整的示例索引目录，包含各类标签与典型链接案例 |

## 资源列表

- https://github.com/zerxonhy/olive/blob/main/velvetrocket.md
- https://github.com/zerxonhy/olive/blob/main/violettimber.md
- https://github.com/zerxonhy/olive/blob/main/willowsilver.md
- https://github.com/zerxonhy/olive/blob/main/willowvelvet.md
- https://github.com/zerxonhy/olive/blob/main/amberocean.md
- https://github.com/zerxonhy/olive/blob/main/amberwillow.md

## 项目结构

```
olive/
├── config/                         # 配置文件目录
│   ├── default.yaml                # 主配置：索引路径、抓取间隔、标签别名
│   └── sources.yaml                # 上游仓库与分支映射，定义外部资源来源
├── index/                          # 索引根目录，所有外链以 Markdown 形式存放
│   ├── network/                    # 网络层相关资源，如协议、负载均衡、DNS
│   │   ├── README.md               # 该分类的说明与维护规则
│   │   └── tcp.md                  # TCP 相关链接条目列表
│   ├── storage/                    # 存储与数据库相关资源
│   │   ├── redis.md                # Redis 链接索引
│   │   └── postgresql.md           # PostgreSQL 链接索引
│   ├── security/                   # 安全与加密相关资源
│   │   ├── authentication.md       # 认证授权方案链接
│   │   └── audit.md                # 审计与日志安全链接
│   ├── observability/              # 可观测性相关资源
│   │   ├── metrics.md              # Prometheus、StatsD 等指标系统链接
│   │   └── logging.md              # 结构化日志与采集系统链接
│   └── meta/                       # 索引自身的元数据，如标签字典、快照记录
│       ├── tags.yaml               # 标签体系定义与同义词映射
│       └── snapshots/              # 每次抓取生成的链接状态快照
├── scripts/                        # 维护与操作脚本
│   ├── init_index.py               # 初始化索引目录结构
│   ├── fetch_metadata.py           # 抓取链接元数据并更新快照
│   ├── check_availability.py       # 检查所有链接可用性并生成报告
│   └── export_format.py            # 导出为 JSON / CSV / HTML
├── reports/                        # 生成的报告存放目录
│   ├── availability/               # 可用性检查报告，按日期归档
│   └── changes/                    # 索引变更差异报告
├── tests/                          # 单元测试与集成测试脚本
│   ├── test_index_parser.py        # 索引文件解析测试
│   └── test_fetch.py               # 元数据抓取功能测试
├── .github/workflows/              # CI/CD 自动化配置
│   ├── daily_update.yaml           # 每日定时更新索引
│   └── check_links.yaml            # 每次推送后执行链接检查
├── requirements.txt                # Python 依赖列表
├── Makefile                        # 常用任务快捷命令
└── README.md                       # 项目概述与快速入门（当前文档）
```

## 贡献指南

1. 在 GitHub 上 fork 本仓库，并克隆到本地开发环境。建议在 dev 分支上进行修改，保持 main 分支与上游同步。
2. 在 index/ 目录下按主题分类添加或修改链接条目。每个 Markdown 文件应遵循标准模板：顶部为分类说明，下方为无序列表，每项包含链接标题、URL 以及可选的标签和摘要。
3. 运行本地测试脚本确保索引格式正确且所有新增链接可访问：`make test` 或 `python tests/run_all.py`。
4. 提交变更时使用语义化提交信息，例如 `feat(index): add new links for storage category` 或 `fix(meta): correct tag alias mapping`。
5. 发起 pull request 至主仓库的 main 分支，等待维护者审阅。维护者将检查链接有效性、格式规范及标签一致性，通过后合并。

## 常见问题

**Q：Olive Index 是否存储资源内容的副本或缓存？**
A：不存储。Olive Index 仅保存链接地址、标题、标签和元数据（如最后检查时间、状态码）。所有资源内容仍由原始来源提供，用户点击链接后将直接跳转至外部站点。建议用户自行评估外部资源的安全性与可用性。

**Q：如何处理上游索引文件中的链接失效问题？**
A：项目内置了链接可用性检查脚本，可定期运行并生成失效链接报告。维护者或贡献者可根据报告中的状态码与时间戳判断是否需要更新链接地址或移除条目。对于频繁变动的资源，建议在索引文件的摘要字段中注明来源版本或具体章节，以提高定位准确性。

**Q：能否将 Olive Index 部署为只读的静态网站？**
A：可以。项目提供了 HTML 导出功能，用户可通过 `export_format.py --format html` 将索引目录生成静态 HTML 文件，随后使用任意 Web 服务器（如 Nginx、Caddy 或 GitHub Pages）托管。导出的 HTML 页面保留标签筛选和全文检索功能，适合作为团队内部的技术导航站点。

## 许可证

MIT

> 外链数量: 6 | 生成时间: 2026-07-21 05:12:52
