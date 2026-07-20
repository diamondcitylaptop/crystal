# Olive Resource Navigator

Olive Resource Navigator 是一个面向开发者与技术研究人员的轻量级外链资源聚合与导航工具。项目定位于将分散在多个仓库、文档和社区中的高质量技术链接进行集中归类、版本追踪和快速检索，解决技术资料收藏后难以查找、链接失效后无法感知、跨项目资源散落不易共享等痛点。它不提供内容的永久存储，而是作为一层透明的索引与校验层，帮助团队或个人维护一套可复用的外链资产清单，并支持与现有工作流（如 CI/CD、文档站点、知识库）进行集成。

## 功能概览

- 外链索引化存储：以纯文本标记格式记录资源元数据，支持自定义标签、状态标记和备注字段。
- 批量链接状态检查：基于 HTTP 状态码与响应时间对已收录链接进行可用性探测，支持定期巡检。
- 多维筛选与检索：按协议类型、域名、文件后缀、关键词或自定义标签快速定位目标资源。
- 变更历史追踪：通过 Git 版本控制记录每一次外链增删改操作，支持回溯与审计。
- 资源分类模板：提供技术文档、开源项目、学习视频、工具站点、社区论坛等内置分类模板。
- 外部数据导入：支持从 CSV、Markdown 列表、JSON 和浏览器书签 HTML 中批量导入链接。
- 只读只写分离：支持将资源列表以只读方式嵌入 MkDocs、VuePress 或 Hugo 站点，同时支持 CLI 写入操作。

## 应用场景

- 个人技术知识库构建：开发者可将日常阅读的博客、论文、API 参考和教程链接统一收录，并利用标签和备注记录阅读状态与心得，逐步形成个人外链知识体系。
- 团队文档资源库维护：技术团队可将项目依赖的第三方库、部署文档、监控面板和内部工具链接集中管理，通过版本控制同步更新，避免成员之间重复询问或查找过时链接。
- 开源项目外部依赖说明：开源项目维护者可将项目依赖的基准文档、数据源、参考实现和姊妹项目链接整理为资源列表，随仓库发布，便于贡献者快速理解上下文。
- 自动化链接监控报警：运维或质量保障人员可配置定时任务，对外链资源列表进行周期性可达性检查，当关键链接（如 SDK 下载地址、许可证原文、镜像源）返回异常时触发通知。

## 快速开始

以下步骤帮助您在本地快速启动 Olive Resource Navigator 的核心功能。

```bash
# 克隆项目仓库
git clone https://github.com/zerxonhy/olive.git
cd olive

# 安装基础依赖（Python 3.9+）
pip install -r requirements.txt

# 构建本地索引并启动简易 Web 预览
python scripts/build_index.py --source ./resources --output ./dist
python -m http.server 8000 --directory ./dist
```

启动后，访问 `http://127.0.0.1:8000` 即可查看资源列表的只读展示页面。

## 安装要求

| 依赖项 | 必需版本 | 说明 |
|--------|----------|------|
| Python | 3.9 至 3.12 | 核心脚本与工具链运行环境 |
| Git | 2.25 及以上 | 用于版本追踪与仓库克隆 |
| pip | 21.0 及以上 | Python 包管理工具 |
| requests | 2.28.0 | 用于外链状态检查与网络请求 |
| pyyaml | 6.0 | 解析资源元数据配置文件 |
| markdown | 3.4 | 生成资源列表的 HTML 预览 |
| pytest | 7.2 | 单元测试与集成测试框架（仅开发环境） |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|------|------|------------|
| 用户手册 | docs/user-guide.md | 如何添加、编辑、删除外链资源？如何导入导出数据？ |
| 管理员指南 | docs/admin-guide.md | 如何配置定时检查任务？如何自定义标签体系？ |
| 开发者文档 | docs/developer-guide.md | 核心模块设计、API 接口、扩展插件开发方法 |
| 部署参考 | docs/deployment.md | 如何将资源站部署到 Nginx、CDN 或 Pages 服务？ |
| 变更日志 | CHANGELOG.md | 每个版本新增功能、修复问题和破坏性变更 |

## 资源列表

- https://github.com/zerxonhy/olive/blob/main/oceanzephyr.md
- https://github.com/zerxonhy/olive/blob/main/olivemeadow.md
- https://github.com/zerxonhy/olive/blob/main/oliveprairie.md
- https://github.com/zerxonhy/olive/blob/main/orbitmidnight.md
- https://github.com/zerxonhy/olive/blob/main/orbitolive.md
- https://github.com/zerxonhy/olive/blob/main/orbitpearl.md

## 项目结构

```
olive/
├── resources/                         # 资源元数据存储目录
│   ├── categories/                    # 分类定义文件（yaml）
│   │   ├── devtools.yaml              # 开发工具分类
│   │   ├── docs.yaml                  # 技术文档分类
│   │   ├── community.yaml             # 社区论坛分类
│   │   └── multimedia.yaml            # 音视频/课程分类
│   ├── indexes/                       # 外链索引主文件
│   │   ├── main.index                 # 主资源列表（行式记录）
│   │   └── archive.index              # 已归档链接备份
│   └── tags/                          # 标签别名映射
│       └── alias.yaml                 # 标签同义词与分组
├── scripts/                           # 核心脚本集
│   ├── build_index.py                 # 构建索引并生成静态输出
│   ├── check_links.py                 # 批量链接状态检查
│   ├── import_bookmarks.py            # 从浏览器书签导入
│   └── export_csv.py                  # 导出资源列表为 CSV
├── tests/                             # 测试套件
│   ├── unit/                          # 单元测试
│   └── integration/                   # 集成测试（含网络请求模拟）
├── docs/                              # 完整文档源码
│   ├── user-guide.md
│   ├── admin-guide.md
│   ├── developer-guide.md
│   └── deployment.md
├── dist/                              # 构建输出目录（默认忽略）
├── config.yaml                        # 全局配置（调度间隔、请求超时等）
├── requirements.txt                   # 生产环境依赖列表
├── requirements-dev.txt               # 开发环境额外依赖
├── LICENSE                            # MIT 许可证文本
└── README.md                          # 本项目文件
```

## 贡献指南

1. 在 GitHub 上 fork 本仓库，并克隆到本地开发环境。建议使用独立的 feature 分支进行修改，分支命名格式为 `feature/简述改动内容`。
2. 对于新增资源链接，请遵循 `resources/indexes/main.index` 中已有的记录格式，包括字段顺序、分隔符和可选备注。若引入新分类，需同步更新 `categories/` 下的对应 yaml 文件。
3. 提交代码前，请在本地执行 `pytest tests/` 确保所有测试用例通过，并运行 `scripts/check_links.py --full` 对新增或修改的链接进行完整检查，避免收录不可用地址。
4. 提交 Pull Request 时，请在描述中明确说明本次变更的动机、涉及的文件范围以及是否影响现有功能。若为新增分类或标签，请提供使用示例。
5. 核心贡献者会定期审查 PR，并在合并前进行二次链接复核与文档一致性检查。合并后，CI 流水线将自动重新构建并部署预览站点。

## 常见问题

**Q: 如果某个外链资源已失效，系统如何处理？**

A: 当执行链接状态检查脚本时，所有返回非 2xx/3xx 状态码或超时的链接会被标记为 `unreachable` 状态，并记录响应时间与错误码。用户可通过命令行过滤查看失效链接列表，手动决定是否更新 URL 或从索引中移除。系统不会自动删除任何条目，以确保变更经过人工确认。

**Q: 是否可以同时维护多套资源列表（例如：公开列表与内部列表）？**

A: 可以。您可以通过 `config.yaml` 中的 `source_paths` 字段指定多个索引文件路径，构建脚本会按顺序合并它们。建议将公开资源与内部敏感链接分开存储，并通过 `.gitignore` 忽略内部文件，或使用 Git 子模块进行权限隔离。合并后的最终列表会统一出现在生成的预览页面中，但内部文件本身不会提交至公开仓库。

**Q: 导入浏览器书签时，如何保留原有的文件夹层级结构？**

A: 导入脚本 `import_bookmarks.py` 支持将书签文件夹名称自动转换为标签。例如，文件夹 `Dev/Backend` 会生成 `dev` 和 `backend` 两个标签。您也可以通过 `--tag-prefix` 参数为所有导入链接添加统一前缀，便于区分来源。若需要保留完整层级路径作为备注，可启用 `--keep-hierarchy` 选项，该选项会将路径信息写入记录的备注字段。

## 许可证

MIT

> 外链数量: 6 | 生成时间: 2026-07-21 05:13:20
