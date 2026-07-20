# Olive Index

Olive Index 是一个面向开发者与技术研究人员的轻量化外链资源汇总工具，专注于将分散在多个仓库、文档、博客与外部站点中的高价值技术链接进行结构化整理与分类展示。该项目不追求复杂的界面交互，而是以 Markdown 与纯文本数据为基础，提供可快速检索、可版本化追踪、可批量导入导出的链接索引方案。Olive Index 适用于个人知识管理、团队技术文档库构建、开源项目依赖导航、以及自动化巡检脚本的链接源管理。

Olive Index 本身不存储任何外部资源实体，仅存储 URL 元数据、标签体系与状态标记。所有原始数据以文本文件形式存放在仓库的指定目录下，支持通过外部脚本或 CI 流水线进行周期性校验与更新。项目定位为“技术外链的元数据层”，通过统一的条目格式与目录结构，降低维护多源链接的认知负担。

## 功能概览

- **结构化链接目录**：所有链接按主题域、来源项目、文件类型等维度归入多级子目录，每个条目附带采集时间与摘要注释。

- **批量导入与去重**：支持从纯文本列表、CSV 或 JSON 文件批量导入 URL，自动识别重复条目并合并标签。

- **状态标记与过滤**：为每条链接标记有效、失效、待审核、过期等状态，支持按状态过滤输出视图。

- **版本化变更记录**：每次新增、删除或修改链接条目均产生 Git 可追踪的变更日志，便于回溯历史状态。

- **外部校验接口**：提供简单脚本入口，可对当前所有外链发起 HEAD 请求或连通性测试，生成可用性报告。

- **标签体系与全文检索**：每条链接支持多个自定义标签，配合 grep 或 ripgrep 可进行快速关键词定位。

- **导出为多种格式**：可将当前索引导出为纯 Markdown 表格、JSON 数组或 CSV 文件，便于嵌入其他文档系统。

## 应用场景

- **个人技术阅读清单管理**：开发者可将日常阅读的官方文档、博客教程、提案 RFC 等链接集中存放于 Olive Index，按学习主题分类，每周定期校验失效链接并补充新资源。

- **团队共享依赖导航页**：开发团队可使用 Olive Index 维护项目所依赖的中间件官网、镜像站、监控面板、日志系统入口等链接，避免每次临时搜索，减少上下文切换时间。

- **自动化监控脚本的输入源**：运维或 SRE 团队可将 Olive Index 导出的 JSON 列表作为巡检脚本的输入，周期性检查外部服务端点可用性，异常时触发告警。

- **开源项目贡献指引聚合**：开源社区维护者可将贡献指南、编码规范、PR 模板、社区会议链接等整合至 Olive Index，降低新贡献者的上手门槛。

## 快速开始

以下步骤帮助您在本地快速运行 Olive Index 的基础环境，完成仓库克隆、依赖安装与初始索引构建。

```bash
# 1. 克隆仓库
git clone https://github.com/zerxonhy/olive.git
cd olive

# 2. 安装基础依赖（Python 3.9+ 与 pip）
python3 -m venv venv
source venv/bin/activate
pip install --upgrade pip
pip install -r requirements.txt

# 3. 运行初始化构建脚本，生成本地索引缓存
python scripts/build_index.py --input data/raw/ --output dist/index.json

# 4. 查看生成的索引摘要
cat dist/index.json | jq '.summary'
```

## 安装要求

| 依赖 | 必需版本 | 说明 |
|------|----------|------|
| Python | 3.9 及以上 | 核心脚本运行环境，用于索引构建与校验 |
| Git | 2.25 及以上 | 版本控制与变更追踪，用于协作维护 |
| curl | 7.68 及以上 | 外部链接连通性校验的默认后端工具 |
| jq | 1.6 及以上 | 推荐安装，用于命令行下解析 JSON 索引文件 |
| GNU Make | 3.82 及以上 | 用于执行常用任务组合（build / check / clean） |
| rsync | 3.2 及以上 | 可选，用于增量同步远程索引片段 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|------|------|------------|
| 用户手册 | docs/usage.md | 如何新增链接、修改元数据、触发校验任务？ |
| 维护指南 | docs/maintenance.md | 如何清理失效链接、合并重复条目、处理变更冲突？ |
| 格式规范 | docs/schema.md | 每条链接的 JSON 字段定义、标签命名约束、日期格式要求？ |
| 集成示例 | docs/integration.md | 如何将 Olive Index 接入 CI 流水线、Slack 通知或监控看板？ |

## 资源列表

- https://github.com/zerxonhy/olive/blob/main/meadowzephyr.md
- https://github.com/zerxonhy/olive/blob/main/midnightocean.md
- https://github.com/zerxonhy/olive/blob/main/midnightquartz.md
- https://github.com/zerxonhy/olive/blob/main/midnighttimber.md
- https://github.com/zerxonhy/olive/blob/main/mirrorprairie.md
- https://github.com/zerxonhy/olive/blob/main/mirrorshadow.md

## 项目结构

```
olive/
├── data/
│   ├── raw/                        # 原始输入目录，存放待导入的纯文本或 CSV 链接列表
│   │   ├── external_sources.txt
│   │   └── team_bookmarks.csv
│   ├── curated/                    # 经过人工审核与分类后的稳定索引条目
│   │   ├── networking/
│   │   ├── databases/
│   │   └── observability/
│   └── metadata/                   # 每条链接的标签、状态、校验时间等元数据
│       ├── tags.json
│       └── status_history.log
├── scripts/
│   ├── build_index.py              # 主构建脚本，读取 raw 与 curated 生成最终索引
│   ├── validate_urls.py            # 遍历所有链接执行连通性测试并生成报告
│   ├── dedup.py                    # 去重与合并工具，基于标准化 URL 进行比对
│   └── export_formats.py           # 导出为 Markdown / JSON / CSV 的格式转换器
├── dist/                           # 构建输出目录，存放可供外部使用的索引文件
│   ├── index.json
│   ├── index.md
│   └── availability_report.txt
├── docs/                           # 完整文档目录，包含使用、维护与集成指南
│   ├── usage.md
│   ├── maintenance.md
│   ├── schema.md
│   └── integration.md
├── tests/                          # 单元测试与集成测试脚本，覆盖核心解析与校验逻辑
│   ├── test_parser.py
│   ├── test_validator.py
│   └── fixtures/
├── Makefile                        # 任务聚合入口，支持 make build / make check / make clean
└── README.md                       # 本文件
```

## 贡献指南

1. 在 GitHub 上 fork 本仓库至个人空间，并克隆到本地开发环境。确保本地 Python 与 Git 版本满足安装要求。

2. 在 data/raw 或 data/curated 下新增或修改链接条目文件，遵循 docs/schema.md 中定义的 JSON 字段规范与标签命名规则。

3. 运行 scripts/build_index.py 重新生成 dist/index.json，并使用 scripts/validate_urls.py 对新增链接进行连通性预检，确保无格式错误与明显失效条目。

4. 提交变更前执行 make test 运行全部单元测试与集成测试，确认无回归问题。提交信息应使用清晰的行为动词前缀，例如 "add: 新增网络拓扑相关链接" 或 "fix: 修正失效的监控面板地址"。

5. 发起 Pull Request 至主仓库的 main 分支，并在 PR 描述中附上本次变更的摘要说明、新增链接数量以及校验结果摘要。

## 常见问题

**Q: 如何批量标记一批链接为失效状态？**

A: 使用 scripts/validate_urls.py 的 --mark-unreachable 选项可自动对当前索引中所有链接进行探测，并将返回码非 200 或超时的条目自动标记为失效。该操作会更新 metadata/status_history.log 并生成差异摘要，建议在运行前备份当前索引文件。

**Q: 索引文件中的链接顺序如何控制？**

A: Olive Index 默认按链接的采集时间倒序排列，即最新添加的条目出现在索引靠前位置。若需要按字母序或标签分组排序，可在 build_index.py 中通过 --sort-key 参数指定排序字段，支持 url、label、timestamp 三种维度。

**Q: 能否在无网络环境使用 Olive Index？**

A: 索引构建与导出功能完全离线可用，所有数据均存储在本地 data/ 目录中。连通性校验与外部更新脚本则需网络访问。若网络受限，可仅使用 data/curated 下的稳定条目，并跳过 validate_urls 步骤。

## 许可证

MIT

> 外链数量: 6 | 生成时间: 2026-07-21 05:13:40
