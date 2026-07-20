# Olive Index

Olive Index 是一个面向开发者与技术研究人员的轻量化外链资源聚合系统。本项目不提供具体的软件工具或库实现，而是围绕高质量外部技术文档、稀有代码仓库与特定领域知识图谱进行索引与结构化整理，帮助用户在复杂信息环境中快速定位有效内容。Olive Index 本身不存储或托管任何受版权保护的资料，仅作为公开可用资源的导航入口。

目标用户包括：需要系统化阅读清单的软件工程师、进行技术选型的架构师、从事开源合规审查的法务技术人员，以及希望追踪特定项目演化路径的研究者。通过严格的来源筛选与分类标记，Olive Index 致力于降低技术信息的发现成本与认知负担。

## 功能概览

- 外链规范化收录：所有资源链接强制遵循原始 URL 直出原则，不进行协议补全、域名规范化或路径重写，确保引用可追溯性。

- 多维度标签体系：每个收录条目附带主题域、技术栈、成熟度与活跃度标签，支持快速筛选与关联查阅。

- 结构化元数据提取：自动从目标文档中提取标题、最后更新时间、代码语言分布等基础元信息，形成统一索引卡片。

- 批次化管理模式：按入库批次分组展示资源集合，便于追踪内容引入时间与更新节奏，当前为第 7/107 批。

- 纯静态输出支持：索引数据可渲染为 Markdown 或 JSON 格式，方便嵌入现有文档站点、CI 流程或本地知识库。

- 版本化快照引用：每条外链附带收录时的快照哈希（若源仓库支持 Git 引用），辅助回溯历史状态。

## 应用场景

- 技术选型前的信息收集：架构师可借助 Olive Index 的批次列表快速浏览一批经过初筛的外部仓库或文档，评估其适用性，减少盲目搜索时间。

- 内部培训材料准备：团队负责人可将特定批次的资源链接作为阅读清单分发给新成员，配合元数据中的主题标签组织学习路径。

- 开源合规审计辅助：法务技术人员通过索引中的源仓库路径，快速定位许可证声明文件与版权归属信息，提升合规审查效率。

- 个人知识库构建：开发者可将 Olive Index 作为数据源，通过脚本拉取外链列表并整合到个人笔记系统，形成定制化的技术参考手册。

## 快速开始

以下操作指导您完成 Olive Index 的本地克隆、依赖安装与基础运行，以便生成静态索引页面。

```bash
# 克隆项目仓库
git clone https://github.com/zerxonhy/olive.git
cd olive

# 安装依赖（Python 3.9+ 环境）
pip install -r requirements.txt

# 执行索引构建脚本，输出 docs/index.md
python build_index.py --batch 7 --output docs/index.md
```

执行完毕后，可在 `docs/index.md` 中查看第 7 批资源的格式化索引内容。若需生成 JSON 格式，可添加 `--format json` 参数。

## 安装要求

| 依赖项 | 必需版本 | 说明 |
|--------|----------|------|
| Python | 3.9 及以上 | 运行构建脚本与元数据解析 |
| pip | 21.0 及以上 | 安装 Python 依赖包 |
| Git | 2.30 及以上 | 克隆仓库及获取提交哈希 |
| requests | 2.28.0 | 用于获取外链页面的基础元信息 |
| markdown | 3.4.0 | 用于渲染索引文档为 Markdown 格式 |
| PyYAML | 6.0 | 解析配置文件与标签映射规则 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|------|------|------------|
| 用户手册 | docs/user-guide.md | 如何使用 Olive Index 检索资源、理解标签与批次含义 |
| 维护者指南 | docs/maintainer-guide.md | 如何新增批次、更新元数据、处理失效链接 |
| 数据规范 | docs/data-spec.md | 索引文件的结构定义、字段说明与 JSON Schema |
| 常见流程 | docs/workflows.md | 典型操作步骤，如筛选特定主题资源、导出阅读清单 |

## 资源列表

- https://github.com/zerxonhy/olive/blob/main/goldenatlas.md
- https://github.com/zerxonhy/olive/blob/main/goldencedar.md
- https://github.com/zerxonhy/olive/blob/main/goldenfalcon.md
- https://github.com/zerxonhy/olive/blob/main/harborhorizon.md
- https://github.com/zerxonhy/olive/blob/main/horizonlantern.md
- https://github.com/zerxonhy/olive/blob/main/horizonwillow.md

## 项目结构

```
olive/
├── build_index.py          # 主构建脚本，处理批次与输出
├── config/
│   ├── tags.yaml           # 标签映射配置，定义主题与关键词
│   └── sources.yaml        # 源仓库基础信息配置
├── data/
│   ├── batches/            # 批次原始数据，按编号存放
│   │   └── 007/            # 当前第 7 批数据目录
│   └── cache/              # 外链元数据缓存，减少网络请求
├── docs/                   # 生成的文档输出目录
│   ├── index.md            # 主索引文件
│   └── json/               # JSON 格式输出
├── tests/                  # 单元测试与集成测试
│   ├── test_parser.py
│   └── test_builder.py
├── requirements.txt        # Python 依赖列表
└── README.md               # 本文件
```

## 贡献指南

1. 派生本项目仓库至您的个人账户，并在本地创建功能分支，分支命名建议遵循 `feat/batch-xxx` 或 `fix/xxx` 格式。

2. 在 `data/batches/` 下新增对应批次目录，并按照 `data-spec.md` 中定义的 JSON 格式编写资源列表文件，确保每个 URL 严格使用原始字符串，不添加任何协议前缀或路径改写。

3. 运行本地构建脚本，验证索引输出是否与预期一致，并执行单元测试确保无回归问题。

4. 提交拉取请求至主仓库，描述中需注明新增批次编号、资源数量以及任何特殊处理说明。

5. 维护者审阅后，若符合收录规范与质量要求，将合并并更新主分支索引数据。

## 常见问题

**问：Olive Index 是否存储外部资源的副本或缓存内容？**

答：Olive Index 仅存储资源的 URL 引用与基础元信息（如标题、更新时间），不缓存或镜像任何外部文件内容。部分元信息可通过可选的缓存机制临时存储以减少网络请求，但缓存不会用于分发原始内容。

**问：如果某个外链失效，如何处理？**

答：维护者会定期运行链接检查脚本，标记失效链接。用户可通过 GitHub Issue 报告失效链接。标记后的链接会在索引中保留但附加失效注释，直至源仓库恢复或确认永久移除。

**问：如何批量导出特定标签下的所有资源？**

答：使用构建脚本的 `--filter-tags` 参数，例如 `python build_index.py --filter-tags "rust,network" --format json`，即可输出符合标签条件的资源列表。该筛选逻辑基于 `config/tags.yaml` 中的映射规则。

## 许可证

MIT

> 外链数量: 6 | 生成时间: 2026-07-21 05:12:52
