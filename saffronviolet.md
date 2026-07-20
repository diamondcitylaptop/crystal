# Olive Index

Olive Index 是一个面向开发者、研究员与技术文档撰写者的技术资源外链汇总与结构化导航系统。本项目的核心定位并非构建一个新的内容仓库，而是对分散在多个代码仓库、技术博客、官方文档与社区讨论中的高质量外部链接进行集中收录、分类索引与语义化标注。目标用户包括需要快速查阅特定技术栈原始资料的后端工程师、需要追踪多个开源项目更新动态的维护者，以及需要为团队搭建内部技术导航页面的基础设施负责人。Olive Index 通过严格的链接校验、版本化元数据记录与扁平化的目录结构，解决技术书签易丢失、外链失效难追溯、上下文碎片化等长期痛点，使外部资源真正成为可复用、可审计、可继承的项目资产。

## 功能概览

- 外链单向收录引擎 支持批量导入外部 Markdown 文件中的超链接，自动去重并提取标题与上下文摘要，保留原始仓库的目录层级作为分类线索。

- 链接健康状态巡检 周期性对已收录的 URL 发起 HEAD 请求，标记返回码非 200 的链接为异常状态，并生成失效报告供维护者批量更新或移除。

- 多级标签与全文检索 每条外链可绑定多个技术领域标签，配合基于文件名的模糊搜索与基于内容摘要的关键词过滤，快速定位特定主题的参考资料。

- 元数据版本快照 记录每次收录操作的时间戳、操作者与来源文件哈希值，支持回滚至任意历史版本的链接集合，便于审计变更轨迹。

- 静态站点生成适配 项目结构天然兼容静态站点生成器，可将外链列表与注释说明直接渲染为 HTML 导航页面，无需额外数据库即可部署至任意 Web 服务器。

- 外链关联图谱 自动分析不同外链指向的同一域名或同一仓库路径，生成关联度热力图，帮助发现高频引用的核心基础设施项目。

- 自定义元字段扩展 允许为每条外链添加自定义键值对，例如优先级、阅读状态、关联内部项目编号，满足团队级协作需求。

## 应用场景

- 技术选型调研阶段 架构师需要横向对比多个中间件项目的官方文档、性能测试报告与社区案例。Olive Index 可将这些分散在不同 GitHub 仓库、技术博客与 PDF 链接中的资料统一收录，并通过标签快速筛选出关于高可用、吞吐量或运维复杂度的关键文章，大幅缩短信息收集周期。

- 开源项目维护者追踪依赖更新 当项目依赖多个上游仓库时，维护者使用 Olive Index 收录每个上游仓库的 Release Notes 链接与 CHANGELOG 文件地址。每日巡检机制会自动检测链接可达性，一旦某上游仓库的文档路径发生变动，维护者能第一时间收到通知，避免依赖版本升级时遗漏重要变更说明。

- 团队内部知识库外链治理 技术团队长期积累的 Confluence 页面、飞书文档或 Notion 笔记中散落大量外部参考链接，但缺乏统一管理。Olive Index 作为独立的外链治理工具，允许团队成员将各自收藏的链接提交至统一索引，由自动化流程检查重复与失效情况，最终生成一份经过清洗的、带注释的团队共享外链白名单，直接嵌入内部文档门户。

## 快速开始

以下命令演示了从克隆项目到启动本地索引服务的完整流程。请确保在执行前已安装 Git 与 Node.js 环境。

```bash
git clone https://github.com/zerxonhy/olive.git
cd olive
npm install
npm run build
npm start
```

执行完毕后，Olive Index 将监听本地 3000 端口，通过浏览器访问 http://localhost:3000 即可查看默认收录的外链列表。若需要导入自定义链接集，请将 Markdown 文件放置于 `./data/imports/` 目录下，随后运行 `npm run ingest` 执行批量收录。

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|---|---|---|
| Node.js | 18.x 或 20.x LTS | 运行时环境，用于执行索引引擎与巡检脚本 |
| npm | 9.x 或以上 | 依赖管理工具，用于安装项目所需第三方包 |
| Git | 2.30 或以上 | 版本控制工具，用于克隆仓库与提交链接变更记录 |
| curl | 7.68 或以上 | 用于健康巡检脚本中的备用 HTTP 探测，当 Node.js 原生请求超时时降级使用 |
| sqlite3 | 3.x (系统级) | 可选依赖，用于持久化链接元数据；若缺失则自动回退至内存存储模式，但重启后数据丢失 |
| awk | GNU 或 POSIX 兼容 | 用于日志分析辅助脚本，非核心功能但建议安装以获取完整统计报告 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|---|---|---|
| 入门指南 | docs/getting-started.md | 如何首次运行、如何导入第一批外链、如何理解控制台输出日志 |
| 链接管理 | docs/link-management.md | 如何添加单条外链、如何批量更新标签、如何处理失效链接的批量替换 |
| 巡检配置 | docs/health-check.md | 如何调整巡检频率、如何自定义超时阈值、如何配置通知接收渠道 |
| 静态导出 | docs/static-export.md | 如何将当前索引导出为 HTML 静态页面、如何自定义输出模板样式 |

## 资源列表

- https://github.com/zerxonhy/olive/blob/main/cloudbright.md
- https://github.com/zerxonhy/olive/blob/main/coralmaple.md
- https://github.com/zerxonhy/olive/blob/main/coralsaffron.md
- https://github.com/zerxonhy/olive/blob/main/cosmicamber.md
- https://github.com/zerxonhy/olive/blob/main/cosmicbright.md
- https://github.com/zerxonhy/olive/blob/main/cosmicquartz.md

## 项目结构

```
olive/
├── bin/                                 # 可执行脚本入口
│   ├── index.js                         # 主服务启动脚本
│   └── health-check.js                  # 独立巡检命令行工具
├── config/                              # 运行时配置文件目录
│   ├── default.json                     # 默认端口、超时、分页大小等参数
│   └── custom-schema.json               # 用户自定义元字段的 JSON Schema 定义
├── data/                                # 数据存储与导入导出目录
│   ├── imports/                         # 存放待收录的外部 Markdown 文件
│   ├── exports/                         # 导出为 JSON 或 HTML 的输出目录
│   └── index.db                         # sqlite3 数据库文件（若启用持久化）
├── docs/                                # 项目文档与用户指南
│   ├── getting-started.md               # 快速入门完整教程
│   ├── link-management.md               # 链接生命周期管理详解
│   ├── health-check.md                  # 巡检机制原理与调优参数
│   └── static-export.md                 # 静态站点生成步骤与示例
├── src/                                 # 核心源码目录
│   ├── core/                            # 索引引擎核心模块
│   │   ├── collector.js                 # 链接提取与去重逻辑
│   │   └── validator.js                 # URL 规范化与可达性预检
│   ├── scheduler/                       # 巡检任务调度模块
│   │   ├── timer.js                     # 基于 node-cron 的周期调度器
│   │   └── notifier.js                  # 失效链接通知聚合器
│   └── web/                             # 轻量级 Web 展示层
│       ├── routes.js                    # 路由定义与请求参数解析
│       └── templates/                   # 服务端渲染视图模板
├── test/                                # 单元测试与集成测试用例
│   ├── collector.test.js                # 链接提取方法测试
│   └── validator.test.js                # URL 校验边界情况测试
├── .gitignore                           # Git 忽略文件清单
├── LICENSE                              # MIT 许可证全文
├── package.json                         # npm 项目描述文件
└── README.md                            # 项目根目录说明文档（本文件）
```

## 贡献指南

1. 查阅 issues 列表，选择未被认领且标记为 `help-wanted` 或 `good-first-issue` 的任务，在 issue 下回复说明意图以避免重复工作。

2. 克隆项目并创建新分支，分支命名遵循 `feature/功能简述` 或 `fix/问题简述` 的格式，例如 `feature/add-export-format` 或 `fix/health-check-timeout`。

3. 提交代码前运行 `npm run lint` 与 `npm run test` 确保代码风格一致且所有已有测试用例通过。新增功能需同步编写对应的测试文件并置于 `test/` 目录下。

4. 编写详细的 PR 描述，说明改动点、影响范围以及测试方式，并在 PR 中关联对应的 issue 编号。若改动涉及外链数据结构的变更，必须同步更新 `config/custom-schema.json` 和对应文档。

5. PR 合并前至少需要一位项目维护者进行 Code Review。非核心维护者提交的 PR 默认由当前活跃的维护者轮值审阅，审阅周期不超过 48 小时。

## 常见问题

Q: 导入包含大量外链的 Markdown 文件时，进程内存占用过高导致卡顿如何处理？

A: 建议将大文件拆分为多个小于 2MB 的片段，分批放入 `data/imports/` 目录并逐个运行 `npm run ingest -- --file 文件名`。亦可调整 `config/default.json` 中的 `batchSize` 参数，减小单次批量处理的链接数量，以降低内存峰值。

Q: 健康巡检脚本报告某链接为失效，但我手动访问浏览器可以正常打开，原因是什么？

A: 巡检脚本默认使用 HEAD 请求且超时时间为 5 秒，某些站点可能屏蔽 HEAD 方法或响应较慢。此时可修改 `config/default.json` 中的 `healthCheck.method` 为 `GET`，并适当增加 `timeout` 值。若仍存在问题，请检查该站点是否有防自动化访问机制，例如 Cloudflare 人机验证页面。

Q: 静态导出生成的 HTML 页面包含所有链接，但我想按标签过滤后仅导出部分链接，如何实现？

A: 使用 `npm run export -- --tags "标签1,标签2"` 命令，并在 `--tags` 参数后指定需要的标签名称（多个标签用逗号分隔）。导出器会仅匹配至少包含其中一个标签的链接进行渲染。若未指定 `--tags` 参数，则默认导出全部链接。

## 许可证

MIT

> 外链数量: 6 | 生成时间: 2026-07-21 05:12:52
