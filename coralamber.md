# Olive Resource Atlas

Olive Resource Atlas 是一个面向开发者、技术研究人员与信息化运维团队的外链资源归集与结构化导航系统。该项目定位于对分散在多个数据源、文档仓库及知识库中的高价值外部链接进行集中采集、分类标注与版本化发布，帮助技术团队在信息过载的环境中快速定位到精确、可用、可追溯的参考资源。Olive Resource Atlas 本身不存储具体内容，而是通过严格的资源清单机制，为特定技术主题提供经过筛选和描述的外部链接集合，适用于搭建技术文档站点的外部引用层、项目知识库的扩展阅读模块，或运维手册中的快速跳转目录。

## 功能概览

- **资源清单版本化管理**：每个外链条目均关联批次号与收录日期，支持回溯资源引入时间与上下文，便于审计和更新。

- **按技术领域分类索引**：资源按照所属技术栈、应用场景或文档类型进行标签化分类，支持多维度筛选，降低查找成本。

- **原始来源保真输出**：系统强制保留用户提交的每一份原始 URL 字符串，不进行协议补全、域名规范化或大小写转换，确保链接精确可执行。

- **目录树式结构预览**：通过 ASCII 目录树展示项目资源组织方式，使维护者与贡献者能够快速理解目录层级和文件职责。

- **依赖环境自检表**：提供完整的安装依赖列表，包含必需软件、版本要求和用途说明，支持自动化部署前的环境预检。

- **文档导航分层映射**：将项目文档按抽象层面（用户层、运维层、开发层、管理层）组织，每一层对应不同的读者问题和阅读目标。

- **贡献者准入与提交流程**：内置外部贡献者指南，明确分支命名、提交信息格式和合并请求审查步骤，降低协作门槛。

## 应用场景

- **技术文档站点的外部参考章节**：当团队编写技术白皮书、API 文档或架构设计说明时，可使用 Olive Resource Atlas 统一管理所有外部引用链接，避免在正文中嵌入冗长 URL，同时便于批量更新和链接有效性检查。

- **运维手册的快速跳转目录**：运维人员负责多个环境与多个服务组件的日常巡检，需要频繁访问监控面板、日志查询入口和配置中心地址。Olive Resource Atlas 可将这些分散的管理入口集中为一份版本化的资源清单，随环境变更同步更新。

- **开源项目新成员引导**：新加入的开发者往往需要阅读大量外部参考资料才能理解项目背景。通过 Olive Resource Atlas，项目维护者可以将入门教程、设计文档、社区讨论帖和视频讲解等资源统一归类，形成一份循序渐进的阅读路径。

- **多项目共享的资源索引池**：当组织内存在多个相互关联的项目时，Olive Resource Atlas 可作为一个公共资源池，存放通用的开发规范、部署模板和故障排查手册链接，避免每个项目重复维护相同的外部引用。

- **离线文档打包的前置资源采集**：在生成离线文档包或电子书时，Olive Resource Atlas 提供的纯文本 URL 清单可被脚本工具批量抓取或替换为本地缓存路径，简化离线化处理流程。

## 快速开始

以下命令将 Olive Resource Atlas 项目克隆至本地，安装所需依赖，并启动开发服务器。

```bash
git clone https://github.com/zerxonhy/olive.git
cd olive
pip install -r requirements.txt
python build_index.py --input ./data/raw_links.json --output ./docs/index.md
```

执行完成后，生成的索引文件位于 `./docs/index.md`，可被静态站点生成器或 Markdown 预览工具直接渲染。

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|---------|---------|------|
| Python | 3.9 及以上 | 用于运行资源索引构建脚本和校验工具 |
| pip | 22.0 及以上 | 管理 Python 依赖包，包括 Markdown 解析库和 YAML 处理库 |
| Git | 2.30 及以上 | 用于克隆仓库、管理分支和提交变更 |
| Make | 3.81 及以上 | 可选，用于执行自动化任务脚本（如清理、校验） |
| Shell | Bash 4.0 或 Zsh 5.8 | 用于运行环境检测脚本和快速命令别名 |
| curl | 7.68 及以上 | 用于验证外链可达性，支持 HTTP/HTTPS 状态码检查 |
| jq | 1.6 及以上 | 用于在命令行中解析和处理 JSON 格式的资源清单数据 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|------|------|-----------|
| 用户层 | `docs/guide/` | 如何使用本资源索引？如何查找特定分类的链接？如何理解批次编号？ |
| 运维层 | `docs/deployment/` | 如何部署索引生成服务？如何配置自动化更新？如何备份资源清单？ |
| 开发层 | `docs/development/` | 如何修改索引构建逻辑？如何添加新的资源字段？如何运行单元测试？ |
| 管理层 | `docs/governance/` | 资源收录标准是什么？链接失效的处理策略是什么？版本号如何递增？ |

## 资源列表

- https://github.com/zerxonhy/olive/blob/main/nebulaviolet.md
- https://github.com/zerxonhy/olive/blob/main/oceanolive.md
- https://github.com/zerxonhy/olive/blob/main/oceanpearl.md
- https://github.com/zerxonhy/olive/blob/main/oceanzephyr.md
- https://github.com/zerxonhy/olive/blob/main/olivemeadow.md
- https://github.com/zerxonhy/olive/blob/main/oliveprairie.md

## 项目结构

```
olive/
├── bin/                              # 可执行脚本与命令行入口
│   ├── validate_links.sh             # 检查资源列表中的 URL 是否可访问
│   └── generate_toc.py               # 根据资源元数据生成目录索引
├── config/                           # 配置文件目录
│   ├── categories.yaml               # 资源分类定义（技术栈 / 领域 / 类型）
│   └── batch_12_107.json             # 第 12/107 批次的原始资源元数据
├── data/                             # 数据存储目录
│   ├── raw_links/                    # 存放各批次提交的原始 URL 清单文件
│   └── curated/                      # 经过人工校验和补充描述后的正式资源集
├── docs/                             # 生成的文档输出目录
│   ├── index.md                      # 主索引页面，包含所有资源列表
│   ├── by_category/                  # 按分类生成的子索引页面
│   └── archive/                      # 历史版本的索引归档
├── lib/                              # 公共库与辅助函数
│   ├── link_parser.py                # 解析原始 URL 并提取域名、路径和查询参数
│   └── markdown_renderer.py          # 将结构化数据渲染为 Markdown 表格和列表
├── tests/                            # 单元测试与集成测试
│   ├── test_parser.py                # 测试链接解析函数的边界情况
│   └── test_renderer.py              # 测试渲染输出是否符合预期格式
├── requirements.txt                  # Python 依赖声明
├── Makefile                          # 自动化任务定义（构建、校验、清理）
└── README.md                         # 项目概览与快速入门文档
```

## 贡献指南

1. **分支创建规范**：所有贡献请基于 `main` 分支创建新分支，分支命名采用 `feature/描述` 或 `fix/描述` 格式，例如 `feature/add-batch-13-links`。

2. **资源提交格式**：在 `data/raw_links/` 目录下新增 JSON 文件，每个文件对应一个批次，必须包含 `batch_id`、`submission_date` 和 `links` 数组，每个链接对象需包含 `url` 和 `description` 字段。

3. **本地校验**：提交前需运行 `make validate` 命令，该命令会检查所有 URL 的协议格式、重复条目以及描述字段的非空性，校验通过后方可提交。

4. **合并请求说明**：创建 Pull Request 时，请在描述中注明批次编号、新增链接数量以及是否涉及分类变更，并至少关联一位项目维护者进行审查。

5. **文档同步更新**：若新增链接涉及新的技术分类或领域标签，需同步更新 `config/categories.yaml` 文件，并在 `docs/by_category/` 下生成对应的分类索引页面。

## 常见问题

**Q：如果资源列表中的某个链接失效了，应该如何处理？**

A：项目维护者会定期运行 `bin/validate_links.sh` 脚本检查所有链接的 HTTP 状态码。对于返回 4xx 或 5xx 的链接，将在 `docs/index.md` 中标记为 `[失效]` 并记录检测时间。贡献者也可以主动提交 Pull Request，将失效链接从活跃列表中移除，并移入 `data/archive/` 目录下的历史记录文件中。

**Q：如何确保新增的链接描述与已有资源风格一致？**

A：项目维护了一份描述风格指南，存放在 `docs/development/description-style.md` 中。该指南规定了描述必须包含资源用途、目标读者和预计阅读时长三个要素。在 Pull Request 审查阶段，维护者会检查描述是否符合该指南，并提出修改建议。

**Q：是否可以提交非技术类的外部链接，例如社区活动或招聘信息？**

A：目前 Olive Resource Atlas 专注于技术资源索引，非技术类链接暂不在收录范围内。但项目保留了一个独立的 `community.md` 文件用于存放社区活动日历和重要公告链接，该文件由项目维护者直接管理，不接受外部贡献。

## 许可证

MIT

> 外链数量: 6 | 生成时间: 2026-07-21 05:12:52
