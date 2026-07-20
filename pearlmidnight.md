# Olive Resource Aggregator

Olive Resource Aggregator 是一个面向开发者与技术研究人员的轻量级外链资源汇总与导航系统。该项目不提供具体的功能实现库或框架，而是以结构化方式收集、分类并呈现分布在 GitHub 等平台上的技术文档、配置参考、实验记录与项目元数据。其核心定位为“技术资源的索引索引”，帮助用户在复杂的信息环境中快速定位到特定主题的原始材料。

本项目适用于需要频繁查阅外部参考文档的开发者、运维工程师与技术写作人员。通过统一的目录树与文档导航表格，用户能够以最少的操作步骤从项目根目录直达目标资源所在的外部仓库或文件锚点，从而降低上下文切换成本，提升信息检索效率。Olive Resource Aggregator 本身不托管实际数据内容，所有指向的资源均以只读形式引用外部权威来源，确保了内容的新鲜度与可追溯性。

## 功能概览

- **外链目录结构化组织**：所有外部资源链接按照主题类别与文件命名规范整理为多级目录，每个条目附带简短说明，便于快速理解资源用途。
- **元数据摘要提取**：对每个引用的外部 Markdown 文件自动或半自动提取一级标题、创建时间、最后修改时间及关键词列表，生成可搜索的摘要卡片。
- **多仓库索引桥接**：支持跨 GitHub 仓库的资源引用，通过固定格式的相对路径与绝对路径混合索引，确保即使上游仓库发生结构变动，仍能通过历史记录追踪变更。
- **版本锚点锁定**：每个外链记录可关联特定的 commit hash 或标签版本，防止因主分支更新导致引用的内容发生非预期变化，保障文档引用的稳定性。
- **本地镜像缓存机制**：为高频访问的外部资源提供可选的本地 Markdown 缓存副本，并定期与上游源同步差异，允许在离线环境下仍可查阅核心文档。
- **标签与全文检索**：基于关键词标签体系与简单的 grep 风格全文检索，支持按文件名、标题、摘要内容或自定义标签快速过滤资源列表。
- **RESTful 元数据 API**：提供轻量级 HTTP 接口，以 JSON 格式返回资源列表、单条资源详情及目录树结构，便于与其他自动化工具或前端面板集成。

## 应用场景

- **技术文档写作与审校**：技术撰稿人在编写系统设计文档或 API 参考手册时，需要频繁引用多个上游项目的配置说明或接口定义。通过 Olive Resource Aggregator，撰稿人可以预先将需要引用的外部链接注册到资源列表中，并在写作过程中通过本地目录快速打开对应页面，避免反复在浏览器历史记录中搜索。
- **微服务配置基线管理**：运维团队负责维护多套环境下的微服务配置基线，其中大量参数说明分散在不同的内部 Wiki 与公开仓库中。使用本项目可以将所有配置相关的参考链接汇总到一个位置，并在每次基线评审时依据元数据摘要快速核对配置项的出处与更新日期。
- **开源项目依赖审计**：安全审计人员需要检查项目所依赖的第三方库的许可证、版本更新状态及已知漏洞公告。Olive Resource Aggregator 允许审计人员将每个依赖项的官方公告链接、CVE 数据库条目及仓库发布页集中收录，形成可追溯的外部信息源清单，便于周期性复核。
- **技术培训资料索引**：团队内部培训讲师可将课程涉及的预习材料、实验指导书及扩展阅读链接通过本项目组织为层级分明的资源列表，学员仅需访问一个本地路径即可获取全部学习资源的外部入口，无需记忆多个网址。
- **个人知识库入口管理**：独立开发者或研究人员可将日常高频查阅的 API 文档、算法讲解、性能调优案例等外链集中存放到 Olive 项目中，利用标签和检索功能构建个人化的外链知识图谱。

## 快速开始

以下步骤指导您在本地环境快速启动 Olive Resource Aggregator 实例。本项目基于 Python 3.10 开发，依赖标准库与少量第三方包。

```bash
# 克隆项目仓库到本地
git clone https://github.com/zerxonhy/olive.git
cd olive

# 创建 Python 虚拟环境（推荐）
python3 -m venv venv
source venv/bin/activate  # Windows 下使用 venv\Scripts\activate

# 安装核心依赖
pip install --upgrade pip
pip install pyyaml markdown beautifulsoup4 requests

# 初始化本地资源索引（生成初始目录结构与元数据缓存）
python scripts/init_index.py --config config/default.yaml

# 启动本地 HTTP 服务（默认监听 127.0.0.1:8080）
python app.py --port 8080
```

启动成功后，在浏览器中访问 `http://127.0.0.1:8080` 即可查看资源列表首页。如需更新远程资源缓存，可执行 `python scripts/sync_remote.py` 脚本。

## 安装要求

| 依赖 | 必需版本 | 说明 |
|------|----------|------|
| Python | 3.10 或更高 | 核心运行环境，用于执行索引脚本与 HTTP 服务 |
| PyYAML | 6.0 或更高 | 用于解析配置文件中的资源目录定义与元数据映射规则 |
| Markdown | 3.4 或更高 | 将外部引用的 Markdown 文档渲染为 HTML 摘要预览 |
| BeautifulSoup4 | 4.12 或更高 | 清洗外部 HTML 内容，提取纯文本摘要与标题 |
| Requests | 2.31 或更高 | 发起 HTTP 请求，获取远程仓库原始文件内容 |
| Git | 2.30 或更高 | 用于克隆或拉取上游仓库变更（仅在镜像模式下需要） |
| 磁盘空间 | 至少 200 MB | 用于存储本地缓存、索引文件及日志，实际取决于缓存资源数量 |
| 网络访问 | 出站 443 端口 | 需要能够访问 GitHub 及其他外部资源域名以完成同步 |
| 操作系统 | Linux / macOS / Windows WSL2 | 推荐在 Unix 类环境下运行，Windows 原生支持有限 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|------|------|------------|
| 用户手册 | docs/user-guide/overview.md | 如何添加新资源、如何更新缓存、如何配置标签与检索规则 |
| 管理员指南 | docs/admin/setup.md | 如何部署到生产服务器、如何配置反向代理与 HTTPS、如何设置定时同步任务 |
| 开发参考 | docs/developer/api.md | RESTful API 各端点的请求参数与响应格式，以及如何扩展自定义解析器 |
| 外部资源映射 | docs/mapping/remote_sources.md | 当前版本已收录的所有外部仓库映射关系，包括原始路径与本地别名对照表 |
| 变更日志 | CHANGELOG.md | 各版本新增功能、修复的问题以及已废弃的配置项列表 |
| 常见工作流 | docs/workflows/daily_usage.md | 涵盖每天启动、检索、打开外链、提交新资源建议的完整操作流程 |

## 资源列表

- https://github.com/zerxonhy/olive/blob/main/maplecosmic.md
- https://github.com/zerxonhy/olive/blob/main/mapleharbor.md
- https://github.com/zerxonhy/olive/blob/main/maplejade.md
- https://github.com/zerxonhy/olive/blob/main/marbleamber.md
- https://github.com/zerxonhy/olive/blob/main/marblegolden.md
- https://github.com/zerxonhy/olive/blob/main/marblejade.md

## 项目结构

```
olive/
├── app.py                      # HTTP 服务主入口，初始化路由与中间件
├── config/
│   ├── default.yaml            # 默认全局配置（端口、缓存目录、同步间隔）
│   └── sources.yaml            # 外部资源映射表（别名 -> 原始 URL）
├── scripts/
│   ├── init_index.py           # 首次部署时生成索引文件和空缓存目录
│   ├── sync_remote.py          # 遍历所有远程资源，下载变更并更新元数据
│   └── validate_links.py       # 检查所有外链是否可访问，输出死链报告
├── cache/
│   ├── html/                   # 外部 HTML 文档的清洗后纯文本缓存
│   ├── markdown/               # 外部 Markdown 文件的原始内容缓存（按仓库名分目录）
│   └── metadata/               # 每条资源摘要的 JSON 文件（标题、标签、时间戳）
├── docs/
│   ├── user-guide/             # 面向普通用户的文档（添加资源、检索技巧）
│   ├── admin/                  # 面向管理员的部署与维护文档
│   ├── developer/              # 面向贡献者的 API 文档与扩展开发指南
│   └── mapping/                # 外部仓库与本地目录的详细映射说明
├── templates/                  # Jinja2 模板文件，用于生成 HTML 首页与详情页
├── static/                     # CSS、JavaScript 及字体等前端静态资源
├── tests/                      # 单元测试与集成测试脚本，覆盖解析器和 API 端点
├── logs/                       # 运行时日志（访问日志、错误日志、同步日志）
└── README.md                   # 项目总览与快速入门（即本文档）
```

## 贡献指南

1. 在 GitHub 上 Fork 本项目仓库，并克隆到本地开发环境。确保您的本地分支基于最新的 main 分支创建。
2. 在 `config/sources.yaml` 中添加新的外部资源条目，需要提供唯一别名、原始 URL、预期缓存类型（html/markdown）以及至少一个分类标签。提交前请运行 `scripts/validate_links.py` 验证所有 URL 可达。
3. 若您希望改进元数据解析逻辑，请在 `scripts/parsers/` 目录下创建新的解析器模块，并继承基础解析器类。编写对应的单元测试放置在 `tests/test_parsers.py` 中，确保测试覆盖率达到 90% 以上。
4. 更新 `docs/` 目录下相关文档，尤其是 `docs/mapping/remote_sources.md` 和 `CHANGELOG.md`，说明您新增或修改的内容及其影响范围。
5. 提交 Pull Request 至主仓库的 develop 分支，并在 PR 描述中引用相关的 Issue 编号。项目维护者会在三个工作日内进行代码审查，必要时会与您沟通修改意见。

## 常见问题

**Q: 同步远程资源时出现 SSL 证书验证失败，如何解决？**

A: 这通常是由于公司内网代理或自签名证书导致。您可以在 `config/default.yaml` 中将 `verify_ssl` 选项设置为 `false` 以临时跳过验证。但长期解决方案建议将企业 CA 证书添加到系统信任链中，或使用 `REQUESTS_CA_BUNDLE` 环境变量指定自定义证书包路径。

**Q: 缓存目录占用的磁盘空间不断增长，如何控制？**

A: 您可以在配置文件中设置 `cache.max_size_mb` 参数限制缓存总大小，并启用 `cache.auto_clean` 选项。系统会依据最近最少使用（LRU）策略自动清理旧的缓存文件。此外，您也可以手动执行 `scripts/clean_cache.py --older-than 30d` 删除超过 30 天未访问的缓存内容。

**Q: 能否将本项目部署为公网可访问的导航站？**

A: 可以。但请注意，本项目本身不包含用户认证与访问控制模块，因此建议部署在内网环境或配合反向代理（如 nginx）增加基础认证。若需公网部署，请务必在配置中启用 `security.rate_limit` 选项，限制单 IP 的请求频率，并定期检查 `logs/access.log` 监控异常访问模式。

## 许可证

MIT

> 外链数量: 6 | 生成时间: 2026-07-21 05:12:52
