# Olive Index

Olive Index 是一个面向开源技术生态的轻量化资源导航与结构化外链汇总系统。该项目定位于为开发者、技术文档撰写者以及开源项目维护者提供一套可本地运行、可版本化追踪的技术资源索引框架，帮助用户从分散的代码仓库、在线文档和社区讨论中快速提取关键信息，并以统一的目录结构进行持久化整理。Olive Index 本身不存储具体内容，而是通过 Markdown 链接与标注体系，将外部优质资源组织为可检索、可共享的知识图谱，特别适用于需要长期维护技术决策记录、组件选型对比或版本发布追踪的场景。

## 功能概览

- **结构化外链管理** 支持按分类层级整理外部 URL，每个条目可附加自定义元数据标签与备注字段，便于后期过滤与排序。

- **多仓库并行索引** 针对同一组织或主题下的多个 Git 仓库，可建立统一索引视图，展示各仓库中关键文档的相对路径与最新提交信息。

- **自动化目录树生成** 根据资源分类规则，自动生成 ASCII 目录树结构，帮助新贡献者快速理解项目组织方式。

- **版本化资源快照** 每次索引更新均记录时间戳与变更摘要，支持回溯历史状态，便于审计或复盘技术选型过程。

- **轻量级依赖设计** 仅依赖标准 Python 环境与 Git 命令行工具，无需数据库或外部服务，可直接克隆运行。

- **可扩展的解析规则** 支持通过配置文件自定义 URL 解析逻辑，例如提取仓库名、文件扩展名或特定章节标题，适应不同来源的文档风格。

## 应用场景

1. **技术选型对比归档** 团队在评估多个开源数据库或前端框架时，可使用 Olive Index 记录各项目的官方文档链接、性能测试报告地址以及社区讨论帖，形成一份可长期维护的对比清单。

2. **内部知识库构建** 企业技术部门可将分散在多个 Git 仓库中的设计文档、API 参考和运维手册，通过 Olive Index 建立统一的外部链接索引，减少成员查找信息的时间成本。

3. **开源项目贡献指引** 开源社区维护者可以利用该索引体系整理外部教程、视频讲解和衍生项目列表，帮助新贡献者从外围资料入手，逐步深入核心代码。

4. **版本发布配套资源整理** 在软件版本发布前，使用 Olive Index 聚合相关的变更日志、安全公告、兼容性说明和升级指南，确保发布包附带完整的参考信息链。

## 快速开始

以下命令演示了如何获取 Olive Index 源码、安装基础依赖并启动本地索引服务。

```bash
# 克隆项目仓库
git clone https://github.com/your-org/olive-index.git
cd olive-index

# 安装 Python 依赖（建议使用虚拟环境）
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt

# 运行索引构建脚本，生成资源目录
python build_index.py --input ./data/sources.yml --output ./docs/index.md
```

## 安装要求

| 依赖项 | 必需版本 | 说明 |
|--------|----------|------|
| Python | 3.8 或更高 | 核心脚本运行环境，用于解析配置和生成目录 |
| Git | 2.25 或更高 | 用于克隆外部仓库及获取提交历史信息 |
| PyYAML | 5.4.1 或更高 | 解析 sources.yml 配置文件中的资源列表 |
| Jinja2 | 3.0.0 或更高 | 渲染索引模板，输出最终 Markdown 文档 |
| Markdown | 3.3.0 或更高 | 用于验证生成的文档格式是否合法 |
| pytest | 7.0.0 或更高（可选） | 仅在运行单元测试时需要 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|------|------|------------|
| 入门指南 | docs/getting-started.md | 如何快速建立第一个索引？如何配置外部资源来源？ |
| 配置手册 | docs/configuration.md | sources.yml 中每个字段的含义是什么？如何自定义解析规则？ |
| 模板开发 | docs/template-dev.md | 如何修改输出样式？如何新增变量注入到索引模板中？ |
| 维护流程 | docs/maintenance.md | 如何定期更新索引？如何合并多个贡献者的资源变更？ |

## 资源列表

- https://github.com/zerxonhy/olive/blob/main/crystalatlas.md
- https://github.com/zerxonhy/olive/blob/main/crystalcedar.md
- https://github.com/zerxonhy/olive/blob/main/crystalisland.md
- https://github.com/zerxonhy/olive/blob/main/deltamidnight.md
- https://github.com/zerxonhy/olive/blob/main/deltapearl.md
- https://github.com/zerxonhy/olive/blob/main/deltasaffron.md

## 项目结构

```
olive-index/
├── build_index.py          # 主构建脚本，读取配置并生成索引文档
├── requirements.txt        # Python 依赖列表
├── data/
│   ├── sources.yml         # 外部资源来源配置，包含 URL 与分类标签
│   └── schema.yml          # 配置文件的结构校验定义
├── src/
│   ├── parser.py           # 解析 URL 列表，提取仓库名与文件路径
│   ├── renderer.py         # 调用 Jinja2 模板生成最终 Markdown 内容
│   └── validator.py        # 检查外部链接是否可访问（可选）
├── templates/
│   ├── index.j2            # 索引主模板，定义章节结构与占位符
│   └── partials/           # 可复用的子模板片段
├── docs/                   # 生成的索引文档输出目录
│   └── index.md            # 最终输出的资源导航文件
├── tests/
│   ├── test_parser.py      # 针对解析器的单元测试
│   └── test_renderer.py    # 针对渲染器的单元测试
└── README.md               # 项目说明文件（本文档）
```

## 贡献指南

1. 在 GitHub 上 Fork 本仓库，并克隆到本地开发环境。确保使用独立的特性分支进行改动，例如 `feature/add-new-parser-rule`。
2. 修改 `data/sources.yml` 或新增模板文件时，请同步更新 `data/schema.yml` 中的校验规则，并运行 `pytest tests/` 确保现有测试用例通过。
3. 若需引入新的外部依赖，请在 `requirements.txt` 中添加具体版本号，并在 `docs/configuration.md` 中补充相关配置说明。
4. 提交 Pull Request 前，请执行 `./build_index.py --strict` 以开启严格模式，检查所有外部链接是否有效，并确保生成的 `docs/index.md` 无格式错误。
5. PR 描述中需明确说明本次变更解决的问题或新增的功能，并引用相关 Issue 编号（如有）。

## 常见问题

**问：Olive Index 是否支持私有 Git 仓库作为资源来源？**  
答：支持。在 `data/sources.yml` 中配置私有仓库地址时，需确保运行环境已配置相应的 SSH 密钥或访问令牌。构建脚本会通过 Git 命令进行克隆，因此需保证本地 Git 具备相应权限。

**问：如何自定义索引文档的输出格式？**  
答：所有输出样式均由 `templates/index.j2` 控制。您可以修改该文件中的 HTML 或 Markdown 结构，也可以新增变量并在 `src/renderer.py` 中注入数据。修改后重新运行构建脚本即可生效。

**问：是否可以只更新索引中的部分资源？**  
答：当前版本支持通过 `--filter` 参数指定只处理特定分类或标签的资源。例如 `python build_index.py --filter tag:database` 仅处理包含 `database` 标签的条目。如需更精细的控制，建议维护多个 `sources.yml` 配置文件并分别构建。

## 许可证

MIT

> 外链数量: 6 | 生成时间: 2026-07-21 05:12:52
