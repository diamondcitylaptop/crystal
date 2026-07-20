# Olive Resource Navigator

Olive Resource Navigator 是一个专注于技术文档、开发笔记与项目参考材料的轻量化外链汇总与导航系统。项目本身不托管实际内容文件，而是通过结构化的 Markdown 索引与外部引用机制，帮助开发者快速定位分散在多个仓库、文档站点与代码片段中的高价值信息。项目目标用户包括技术调研人员、项目维护者、文档编写者以及需要频繁跨仓库查阅参考实现的开发工程师。

Olive 的核心定位是“技术参考的元索引层”。它不替代搜索引擎或代码托管平台，而是通过人工筛选与分类，将特定领域内最相关的资源链接组织成可读性强、便于版本控制的目录结构。项目本身使用纯 Markdown 与 Shell 脚本维护，可无缝集成到 CI/CD 流程中，支持自动化链接有效性检查与更新提示。

## 功能概览

- **结构化外链索引**：基于分类标签与功能领域对参考链接进行多级分组，每个条目包含标题、简短摘要与原始出处，便于快速筛选。

- **批量资源导入**：支持从指定文件或目录批量读取链接列表，自动去重并生成索引条目，减少人工录入错误。

- **链接状态检测**：内置基于 curl 的轻量级检测脚本，可定时检查各外链的可达性，并在变更时输出差异报告。

- **版本化变更记录**：每次更新索引或修改分类结构时，强制要求编写变更摘要，并将记录保存在专用的 changelog 文件中，便于回溯。

- **多格式输出支持**：除 Markdown 外，提供 JSON 与 YAML 格式的索引导出接口，方便其他工具或脚本进行二次处理。

- **标签过滤与搜索**：在生成的静态站点中支持按标签、关键词或文件路径进行实时过滤，降低信息过载。

- **协作审核机制**：每个新增或修改的链接条目需经过至少一位维护者的审核确认，审核状态通过特定标记字段记录。

## 应用场景

- **技术选型调研**：团队在评估多个数据库中间件或前端框架时，可使用 Olive 汇总各项目的官方文档、性能测试报告与社区评测文章，形成统一参考入口，避免重复搜索。

- **微服务治理参考索引**：对于采用 Spring Cloud 或 Dubbo 的微服务架构，运维人员可将内部故障排查手册、外部官方指南与已知问题列表通过 Olive 集中管理，缩短故障定位时间。

- **开源项目贡献指引**：项目维护者可将外部贡献者常见问题、编码规范参考、依赖库说明与示例代码链接统一整理到 Olive 中，降低新成员参与门槛。

- **离线文档镜像准备**：在受限网络环境下，团队可先使用 Olive 汇总所有必需的外部链接，再通过批量下载工具将相关内容保存为离线副本，确保开发环境一致性。

- **月度技术简报生成**：技术负责人可每周或每月将新发现的高质量技术博文、会议录像与仓库更新记录整理到 Olive 中，自动生成简报供团队阅读。

## 快速开始

以下步骤演示如何获取 Olive 项目并启动本地索引服务。

```bash
# 克隆项目仓库
git clone https://github.com/zerxonhy/olive.git
cd olive

# 安装基础依赖（详见安装要求章节）
bash scripts/install_deps.sh

# 构建本地索引并启动预览服务
make build
make serve
```

执行完成后，可通过浏览器访问 http://localhost:8080 查看生成的索引页面。若需自定义数据源，请参考 `docs/configuration.md` 中的配置说明。

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|---|---|---|
| Git | 2.20 或更高 | 用于克隆仓库及提交变更记录 |
| Bash | 4.0 或更高 | 运行维护脚本与链接检测工具 |
| curl | 7.68 或更高 | 用于外链可达性检测与状态码获取 |
| Python | 3.8 或更高 | 运行索引生成器与静态站点构建工具 |
| make | 3.81 或更高 | 调度构建任务与常用命令封装 |
| jq | 1.6 或更高 | 处理 JSON 格式的索引导出文件 |
| yq | 4.0 或更高 | 处理 YAML 格式的索引导出文件（可选） |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|---|---|---|
| 入门指南 | docs/getting_started.md | 如何安装、配置并首次运行 Olive？ |
| 索引维护 | docs/maintenance.md | 如何添加、更新或删除外链条目？如何运行链接检测？ |
| 高级配置 | docs/advanced.md | 如何自定义分类模板？如何集成 CI/CD 自动更新？ |
| 常见工作流 | docs/workflows.md | 如何批量导入链接？如何生成不同格式的索引文件？ |

## 资源列表

- https://github.com/zerxonhy/olive/blob/main/deltasaffron.md
- https://github.com/zerxonhy/olive/blob/main/deltasignal.md
- https://github.com/zerxonhy/olive/blob/main/emberamber.md
- https://github.com/zerxonhy/olive/blob/main/emberbridge.md
- https://github.com/zerxonhy/olive/blob/main/falconanchor.md
- https://github.com/zerxonhy/olive/blob/main/falconisland.md

## 项目结构

```
olive/
├── config/                         # 全局配置文件目录
│   ├── categories.yaml             # 分类与标签映射定义
│   └── sources.list                # 外部数据源白名单
├── docs/                           # 用户文档与操作指南
│   ├── getting_started.md          # 快速入门教程
│   ├── maintenance.md              # 日常维护与更新流程
│   ├── advanced.md                 # 高级配置与扩展接口
│   └── workflows.md                # 典型工作流案例
├── scripts/                        # 维护与工具脚本
│   ├── install_deps.sh             # 自动安装所需依赖
│   ├── link_checker.sh             # 外链可达性批量检测
│   ├── import_batch.sh             # 批量导入链接条目
│   └── export_formats.py           # 导出 JSON/YAML 格式索引
├── src/                            # 核心源码目录
│   ├── indexer.py                  # 索引生成主逻辑
│   ├── validator.py                # 链接格式与去重校验
│   └── staticgen.py                # 静态 HTML 站点生成
├── tests/                          # 单元测试与集成测试
│   ├── test_indexer.py             # 索引生成模块测试
│   ├── test_validator.py           # 校验模块测试
│   └── fixtures/                   # 测试用固定样本数据
├── var/                            # 运行时数据目录
│   ├── cache/                      # 检测结果缓存文件
│   └── logs/                       # 操作日志与错误记录
├── Makefile                        # 构建任务入口
├── README.md                       # 项目概述文档
└── LICENSE                         # MIT 许可证文件
```

## 贡献指南

1. 阅读 `docs/getting_started.md` 完成本地环境搭建，并确保所有依赖已正确安装。

2. 从 `main` 分支签出新的功能分支，分支命名建议采用 `feature/描述` 或 `fix/描述` 格式。

3. 在 `config/categories.yaml` 中定义新的分类或标签，然后在 `var/sources/` 目录下添加对应的链接列表文件（Markdown 格式）。

4. 运行 `make test` 执行所有单元测试与链接格式校验，确保无报错。若新增或修改了核心逻辑，请同步更新 `tests/` 下的对应测试用例。

5. 提交变更并推送至远程仓库，然后通过 Pull Request 提交审核。PR 描述中需包含变更摘要、测试结果以及是否影响现有索引结构的说明。

## 常见问题

**Q: 为什么我运行 link_checker.sh 时部分链接被标记为不可达，但浏览器可以正常访问？**

A: 该脚本默认使用 curl 的 `--head` 参数仅获取响应头，某些站点可能屏蔽 HEAD 请求或返回 403/405。可尝试修改脚本中的 curl 参数为 `-I` 或 `-X GET` 并增加超时时间。另外，请确保网络环境能够正常访问外部站点，部分企业网络可能需要配置代理。

**Q: 我能否将 Olive 部署为公共 Web 服务供团队外的人访问？**

A: 可以。Olive 生成的静态站点完全由 HTML、CSS 与 JavaScript 构成，可托管到任何静态 Web 服务器（如 Nginx、Apache 或云对象存储）。但请注意，外链指向的内容版权与可用性由原始站点负责，Olive 仅提供引用，不承担内容审核责任。建议在部署页面底部声明内容来源与免责信息。

**Q: 如何批量更新索引中的链接描述或分类？**

A: 推荐使用 `scripts/import_batch.sh` 脚本配合 CSV 或 TSV 文件进行批量更新。文件格式为 `链接,标题,分类,标签`，每行一个条目。运行脚本时会自动与现有索引合并，并根据链接去重规则保留最新修改。批量操作前建议备份 `var/index.json` 文件。

## 许可证

MIT

> 外链数量: 6 | 生成时间: 2026-07-21 05:12:52
