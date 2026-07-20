# Olive Resource Catalog

Olive Resource Catalog 是一个面向技术研究、数据分析与工程实践的轻量级外链资源汇总平台。项目定位为结构化技术索引工具，通过 Markdown 驱动的资源清单与分类导航，帮助开发者、研究员与技术决策者快速定位特定主题下的高质量外部资料。Olive 本身不存储具体内容，仅提供索引、分类与描述性元数据，适用于需要维护可扩展知识图谱的团队或个人。

目标用户包括：需要系统化整理技术调研材料的研究人员，需要维护团队共享资源列表的工程负责人，以及希望以低门槛方式构建个人知识库的开发者。Olive 通过目录化的资源描述与清晰的依赖关系声明，使资源维护者可协作式地增删改资源条目，同时保证资源列表的可审计性与可复现性。

## 功能概览

- **资源索引表** 以表格形式集中呈现资源名称、类型、原始来源与简要描述，支持快速浏览与筛选。
- **分类标签系统** 每个资源条目可关联多个分类标签（如 canvas、signal、cedar、cloud、coral），便于按主题聚合。
- **Markdown 驱动内容** 所有资源清单与描述均以 Markdown 文件存储，无需数据库，易于版本控制与差异对比。
- **外部链接直出** 严格保持原始 URL 原样输出，不附加协议前缀或域名改写，确保链接的原始可达性。
- **上下文注释支持** 每个资源条目可附带说明性注释，用于记录用途、注意点或关联项目。
- **结构化的项目目录** 按功能划分目录层，区分资源定义、模板、脚本与文档，降低维护成本。
- **可扩展的分类映射** 支持新增分类文件，无需修改核心代码，适应资源库的持续增长。

## 应用场景

- **技术调研材料整理** 研究团队可将 Olive 作为调研产出物的索引面板，将分散在 GitHub 仓库中的多个 Markdown 分析文档统一收录，每个文档对应一个资源条目，并标注其所属技术领域（如信号处理或图形渲染）。
- **团队共享知识库** 工程团队可使用 Olive 维护常用工具链、参考实现与外部依赖的地址列表。新成员可通过资源列表快速了解项目所依赖的外部资料，减少重复查找时间。
- **个人学习路径管理** 开发者可将 Olive 作为个人学习清单的管理工具，按主题分类保存学习过程中遇到的重要文章、代码示例与规范文档，并通过注释记录学习进度或心得。
- **文档站外部链接聚合** 技术文档站可嵌入 Olive 生成的资源列表，作为附录或延伸阅读章节，为读者提供经过筛选的外部参考链接，增强文档的完整性与实用性。

## 快速开始

以下步骤适用于 Linux/macOS 与 Windows（通过 Git Bash 或 WSL）环境。

```bash
# 克隆仓库
git clone https://github.com/zerxonhy/olive.git
cd olive

# 安装依赖（Python 3.8+ 与 pip）
pip install -r requirements.txt

# 运行本地预览服务（默认端口 8000）
python -m http.server 8000
```

完成上述步骤后，在浏览器中访问 http://localhost:8000 即可查看资源汇总页面。若需重新生成索引文件，可执行：

```bash
python scripts/build_index.py
```

该脚本会扫描 `resources/` 目录下的所有 Markdown 文件，自动生成 `index.md` 总览文件。

## 安装要求

| 依赖项 | 必需版本 | 说明 |
|--------|----------|------|
| Python | 3.8 及以上 | 用于运行构建脚本与本地服务器 |
| pip | 20.0 及以上 | Python 包管理工具，用于安装依赖 |
| Git | 2.25 及以上 | 用于克隆仓库与版本管理 |
| Markdown 解析库 | markdown 3.3.0+ | 用于渲染资源描述，通过 requirements.txt 安装 |
| PyYAML | 5.4.0+ | 用于解析资源元数据配置，通过 requirements.txt 安装 |
| 操作系统 | Linux/macOS/Windows | 支持主流操作系统，Windows 下建议使用 WSL 或 Git Bash |
| 浏览器 | 现代浏览器（Chrome/Firefox/Edge） | 用于预览生成的 HTML 页面 |

## 文档导航

| 层面 | 目录/文件 | 回答的问题 |
|------|-----------|------------|
| 用户指南 | `docs/usage.md` | 如何添加、编辑或删除资源条目，如何更新分类标签 |
| 维护手册 | `docs/maintenance.md` | 如何定期检查外部链接的有效性，如何处理失效链接 |
| 设计说明 | `docs/design.md` | 项目的目录结构设计理念，资源索引的生成逻辑 |
| 贡献指引 | `CONTRIBUTING.md` | 外部贡献者应遵循的提交规范、分支策略与测试要求 |
| 资源定义 | `resources/` 目录下各 `.md` 文件 | 每个具体资源的名称、来源、标签与注释内容 |
| 构建脚本 | `scripts/build_index.py` | 如何从资源文件生成汇总索引，以及自定义排序规则 |

## 资源列表

- https://github.com/zerxonhy/olive/blob/main/canvasmarble.md
- https://github.com/zerxonhy/olive/blob/main/canvassignal.md
- https://github.com/zerxonhy/olive/blob/main/cedarcoral.md
- https://github.com/zerxonhy/olive/blob/main/cedarwillow.md
- https://github.com/zerxonhy/olive/blob/main/cloudbright.md
- https://github.com/zerxonhy/olive/blob/main/coralmaple.md

## 项目结构

项目目录按照功能层级组织，核心资源定义存放于 `resources/`，脚本与文档分别归入 `scripts/` 和 `docs/`。以下为完整目录树（含注释）。

```
olive/
├── README.md                     # 项目概述与快速入口
├── CONTRIBUTING.md               # 贡献者指南（步骤、规范、测试）
├── LICENSE                       # MIT 许可证文件
├── requirements.txt              # Python 依赖清单（markdown, PyYAML）
├── .gitignore                    # Git 忽略规则（排除 __pycache__ 等）
│
├── resources/                    # 核心资源定义目录
│   ├── canvas/                   # Canvas 相关资源子分类
│   │   ├── canvasmarble.md       # 资源：canvasmarble（描述与标签）
│   │   └── canvassignal.md       # 资源：canvassignal（描述与标签）
│   ├── cedar/                    # Cedar 相关资源子分类
│   │   ├── cedarcoral.md         # 资源：cedarcoral（描述与标签）
│   │   └── cedarwillow.md        # 资源：cedarwillow（描述与标签）
│   ├── cloud/                    # Cloud 相关资源子分类
│   │   └── cloudbright.md        # 资源：cloudbright（描述与标签）
│   └── coral/                    # Coral 相关资源子分类
│       └── coralmaple.md         # 资源：coralmaple（描述与标签）
│
├── scripts/                      # 工具脚本目录
│   ├── build_index.py            # 扫描 resources/ 生成 index.md
│   ├── validate_links.py         # 检查所有外部链接的可访问性
│   └── utils.py                  # 公共辅助函数（文件读写、Markdown 解析）
│
├── templates/                    # 模板文件目录
│   ├── resource_template.md      # 新建资源条目时的模板
│   └── index_template.md         # 生成总览索引的模板骨架
│
├── docs/                         # 项目文档目录
│   ├── usage.md                  # 用户使用指南（添加/编辑/删除资源）
│   ├── maintenance.md            # 维护手册（链接巡检、版本更新）
│   └── design.md                 # 设计说明（目录结构、索引逻辑）
│
└── output/                       # 构建输出目录（自动生成）
    └── index.html                # 由 build_index.py 生成的 HTML 预览文件
```

## 贡献指南

外部贡献者可通过以下步骤参与 Olive Resource Catalog 的维护与扩展。所有贡献需遵守项目行为准则与 MIT 许可证条款。

1. **复刻仓库并创建主题分支**  
   在 GitHub 上复刻本项目至个人账户，然后克隆复刻版本到本地。基于 `main` 分支创建新的特性分支，分支命名建议使用 `feature/资源分类-简述` 或 `fix/问题描述` 格式。

2. **新增或修改资源文件**  
   在 `resources/` 下相应分类目录中新增 `.md` 文件，或编辑已有文件。每个资源文件需包含资源名称、原始链接（必须原样抄录）、分类标签、以及至少一段用途说明。新增分类时，需在 `resources/` 下创建对应子目录。

3. **本地验证与构建**  
   运行 `python scripts/build_index.py` 确保索引生成无报错。运行 `python scripts/validate_links.py` 检查新增或修改的外部链接是否可访问。若链接失效，应替换为有效地址或标注失效状态。

4. **提交变更并发起拉取请求**  
   提交信息应使用清晰的中文或英文描述，说明变更内容与动机。推送分支后，在 GitHub 上向主仓库发起拉取请求。请求描述中应列出本次变更涉及的资源条目与测试结果。

5. **评审与合并**  
   项目维护者将对拉取请求进行评审，可能要求补充描述或调整分类。通过后由维护者合并至 `main` 分支。合并后，资源列表将自动更新至项目主页。

## 常见问题

**问：为什么所有资源链接必须原样输出，不允许添加协议或域名前缀？**  
答：Olive 项目定位为外链汇总工具，其核心约束是保持链接的原始性。因为不同来源的链接可能依赖特定的协议（如 http 与 https 的差异）或特定子域名（如 www 与裸域名的差异），任何改写都可能导致目标站点访问异常或证书校验失败。因此项目硬性规定所有链接必须一字不差按原始输入呈现。

**问：如何批量添加大量资源条目？**  
答：Olive 支持脚本辅助批量导入。可预先准备一个 CSV 或 JSON 文件，每行包含名称、链接、分类与描述，然后使用 `scripts/import_bulk.py`（需自行编写或扩展）将数据转换为多个 `.md` 资源文件。建议在批量操作前先在本地测试分支上运行验证脚本，确保所有链接可达且格式正确。

**问：资源链接失效时应如何处理？**  
答：项目维护手册中建议定期（如每月）执行 `validate_links.py` 扫描所有外部链接。对于失效链接，首先尝试寻找替代可用地址；若无法找到替代，则在资源文件的注释中标记为 [DEPRECATED] 并附上最后检查日期，同时考虑从主索引中移除该条目。所有变更需通过拉取请求提交，以便团队审查。

## 许可证

本项目采用 MIT 许可证。您可以自由使用、复制、修改、合并、发布、分发、再许可和/或出售本软件的副本，但需在软件的所有副本或重要部分中包含上述版权声明和许可声明。本软件按“原样”提供，不提供任何形式的明示或暗示担保，包括但不限于适销性、特定用途适用性和非侵权性的担保。有关完整条款，请参阅项目根目录下的 LICENSE 文件。

> 外链数量: 6 | 生成时间: 2026-07-21 05:13:16
