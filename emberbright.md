# Olive Resource Atlas

Olive Resource Atlas 是一个面向开发者和技术研究人员的结构化外链与资源汇总工具。本项目不直接托管内容，而是通过严格的 Markdown 索引机制，对分散在 GitHub 仓库中的技术文档、配置模板、实验笔记和架构示意图进行集中编目与分类。项目定位为“技术资源的导航层”，适用于需要快速检索外部参考材料、维护私有知识图谱或搭建个人技术栈索引的用户。通过统一的资源清单文件，用户可避免在多个仓库间反复切换，提升信息获取效率。

## 功能概览

- **外链编目系统** 支持对任意 HTTP/HTTPS 资源进行单行记录，并自动生成资源清单列表，便于批量导入或二次处理。

- **分层标签机制** 每个资源条目可关联多个上下文标签，用于区分文档类型、技术领域或成熟度等级。

- **版本追踪友好** 所有资源引用均以明文 URL 存储，配合 Git 差异对比，可清晰追溯每次增删改的操作记录。

- **静态站点生成适配** 资源列表采用纯 Markdown 格式，可直接被 MkDocs、Hugo、VuePress 等静态站点生成器识别并渲染为导航页面。

- **批量校验接口** 项目提供可选的 Shell 辅助脚本，用于检查列表中各 URL 的可达性状态并生成可用性报告。

- **低依赖设计** 除 Git 和标准 POSIX 环境外，无需额外安装数据库或运行时框架，降低维护门槛。

- **自定义扩展目录** 允许用户在项目根目录下创建 `_ext` 文件夹，存放个人定制的资源分组文件，不与上游冲突。

- **导入导出兼容** 资源列表采用与 GitHub Flavored Markdown 完全兼容的语法，支持通过脚本转换为 JSON、YAML 或 CSV 格式。

## 应用场景

- **技术文档聚合** 当团队拥有多个独立仓库的文档分散在不同分支时，可使用 Olive Resource Atlas 统一记录各文档入口，形成单一索引页面，减少查找时间。

- **实验环境配置备忘** 开发者在进行基础设施搭建或中间件调优时，常参考多个在线配置示例。通过本项目记录关键链接，可快速复现实验环境。

- **项目依赖关系梳理** 在微服务架构或前后端分离项目中，可利用资源列表记录各服务的 API 文档、监控面板和日志查询地址，形成服务拓扑的辅助视图。

- **个人学习路径管理** 学习者可将课程资料、官方手册、社区最佳实践等链接按主题分组保存，构建可迭代的技术知识库。

- **开源项目外部引用声明** 维护者可使用资源列表明确列出项目所引用的第三方资源、数据源或参考实现，满足合规与致谢要求。

## 快速开始

以下步骤帮助您在 5 分钟内完成项目的本地部署与首次资源加载。

```bash
# 克隆项目仓库
git clone https://github.com/zerxonhy/olive.git
cd olive

# 安装基础依赖（仅需 Git 和标准 Shell 环境）
# 若系统未安装 git，请先执行对应包管理器安装命令，此处省略

# 运行初始资源同步脚本（将项目内所有资源链接汇总到单一索引文件）
bash scripts/sync-resources.sh

# 启动内置的简易 HTTP 预览服务（Python 3 环境）
python3 -m http.server 8000

# 浏览器访问 http://localhost:8000 查看生成的资源导航页面
```

## 安装要求

| 依赖项 | 必需版本 | 说明 |
|--------|----------|------|
| Git | 2.20.0 及以上 | 用于克隆仓库、提交变更和查看历史记录 |
| Bash | 4.0 及以上 | 运行项目提供的同步、校验辅助脚本 |
| Python | 3.6 及以上 | 仅当使用内置 HTTP 预览服务时需要 |
| curl | 7.50.0 及以上 | 可选，用于执行资源可达性校验脚本 |
| Markdown 渲染器 | 任意 | 本地预览或静态站点生成时需对应工具 |
| 文件系统权限 | 读/写 | 需要创建索引文件和扩展目录的写入权限 |
| 网络访问 | 外网或内网 | 用于访问列表中记录的外部资源 |
| 文本编辑器 | 任意 | 推荐支持 Markdown 语法高亮，便于编辑资源列表 |
| 操作系统 | Linux / macOS / WSL2 | 项目脚本未在纯 Windows 环境下完整测试 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|------|------|------------|
| 用户手册 | `docs/user-guide.md` | 如何新增、删除、修改资源链接？如何生成导航页？ |
| 脚本参考 | `docs/scripts-reference.md` | 每个辅助脚本的参数、用法和输出格式是什么？ |
| 扩展开发 | `docs/extension-dev.md` | 如何自定义资源分组逻辑？如何添加额外的元数据字段？ |
| 故障排查 | `docs/troubleshooting.md` | 资源校验失败如何处理？索引文件冲突如何解决？ |

## 资源列表

- https://github.com/zerxonhy/olive/blob/main/brightfalcon.md
- https://github.com/zerxonhy/olive/blob/main/brightpixel.md
- https://github.com/zerxonhy/olive/blob/main/brightsilver.md
- https://github.com/zerxonhy/olive/blob/main/canvasmarble.md
- https://github.com/zerxonhy/olive/blob/main/canvassignal.md
- https://github.com/zerxonhy/olive/blob/main/cedarcoral.md

## 项目结构

```
olive/
├── README.md                      # 项目总览与入门指南
├── LICENSE                        # MIT 许可证文件
├── index.md                       # 主资源索引页（自动生成）
├── _ext/                          # 用户自定义扩展目录，不受 Git 追踪
│   └── example-group.md           # 自定义分组示例文件
├── scripts/                       # 辅助脚本集合
│   ├── sync-resources.sh          # 同步所有资源链接到 index.md
│   ├── validate-urls.sh           # 使用 curl 校验列表中每个 URL 的状态
│   └── export-json.sh             # 将资源列表导出为 JSON 格式
├── docs/                          # 完整文档目录
│   ├── user-guide.md              # 用户操作手册
│   ├── scripts-reference.md       # 脚本参数详解
│   ├── extension-dev.md           # 扩展开发指南
│   └── troubleshooting.md         # 常见问题与排错
├── templates/                     # 页面模板目录
│   ├── header.tmpl                # 导航页头部模板
│   └── footer.tmpl                # 导航页尾部模板
└── tests/                         # 单元测试与集成测试
    ├── test_sync.sh               # 测试同步脚本的正确性
    └── test_validate.sh           # 测试校验脚本的返回码逻辑
```

## 贡献指南

1. 复刻本项目仓库至您的个人账户，并克隆到本地开发环境。

2. 在 `_ext` 目录下创建或修改资源分组文件，遵循现有 Markdown 列表语法，确保每个 URL 单独占一行。

3. 运行 `scripts/validate-urls.sh` 校验所有新增或变更的链接有效性，确保无破损引用。

4. 提交变更时使用清晰的消息格式，例如 `docs: add new resource group for logging tools` 或 `fix: remove outdated monitoring link`。

5. 发起 Pull Request 至主仓库的 `main` 分支，并在描述中说明变更目的和测试结果。

## 常见问题

**问：资源列表中的链接发生变更或失效，项目会自动更新吗？**

答：不会自动更新。项目本身不托管外部内容，也不具备自动爬取或监控能力。用户需定期手动运行 `validate-urls.sh` 检查链接状态，并根据实际情况修改或移除失效链接。建议将校验脚本设置为定时任务（如 crontab）以保持列表健康度。

**问：能否在资源列表中添加本地文件路径或内网地址？**

答：可以。项目对 URL 格式不做强制校验，您可以使用 `file:///` 协议或相对路径，但需注意这些链接在静态站点生成或跨设备访问时可能无法正常解析。建议仅在完全受控的内部环境中使用非 HTTP/HTTPS 链接。

**问：如果多个分组文件中出现相同的资源链接，是否会重复索引？**

答：默认情况下，`sync-resources.sh` 会去重并仅保留首次出现的条目。若您需要保留重复条目以用于不同上下文，可修改脚本中的去重逻辑，但不推荐，因为会增加维护复杂度和混淆风险。

## 许可证

MIT

> 外链数量: 6 | 生成时间: 2026-07-21 05:12:52
