# Cosmic Index

Cosmic Index 是一个面向开发者、研究人员与技术文档撰写者的结构化外链与资源导航系统。本项目不对托管内容进行二次存储或镜像，而是通过严格的分类索引机制，将分散于各处的优质技术文档、项目笔记与参考手册以可追溯、可维护的方式进行聚合管理。项目定位为技术资源的外链汇总站，适用于需要频繁查阅多源资料、维护项目依赖文档链、或构建个人知识图谱的工程场景。目标用户包括但不限于开源贡献者、技术作者、架构师以及 DevOps 工程师。

## 功能概览

- 分级资源索引：支持按项目、模块、主题对资源链接进行多级标签与目录归类，便于快速定位。
- 原始链接透传：所有资源条目均保留原始 URL 不做改写，确保来源可溯性与版权完整性。
- 批量导入与校验：支持从外部清单批量导入链接，并自动执行可用性及协议一致性检查。
- 文档状态标记：每条资源可标注维护状态、更新日期及关联议题编号，便于团队协作。
- 静态站点生成：内置模板引擎可将索引数据渲染为静态 HTML 或 Markdown 文档，适配 GitHub Pages 或独立站点部署。
- 变更历史记录：基于 Git 日志自动生成资源增删改的时间线，支持回滚与审计。
- 外部元数据缓存：可选缓存目标页面的标题与描述信息，减少重复网络请求，提升索引展示效率。

## 应用场景

- 技术文档聚合与版本追踪：团队在维护多个组件库时，可将各库的设计文档、API 参考与变更日志链接统一收录，并通过状态标记快速识别过期内容。
- 个人知识库外链管理：研究员或开发者可将日常阅读的论文、博客、规范草案等资源按主题分类，配合注释功能构建可检索的个人参考手册。
- 开源项目 README 资源附录：开源维护者可将项目依赖的外部工具、教程或相关项目链接通过 Cosmic Index 进行集中管理，减少主 README 的冗长列表，同时保持更新便利性。
- 离线文档预处理管道：在受控网络环境中，可借助索引列表预先获取所有外链页面的关键元数据，为后续离线存档或合规审查提供基础数据。

## 快速开始

以下命令将克隆项目仓库、安装必要依赖并启动本地开发服务器。

```bash
git clone https://github.com/yourorg/cosmic-index.git
cd cosmic-index
npm install
npm run dev
```

执行完毕后，访问控制台输出的本地地址（通常为 http://localhost:3000 ）即可查看索引面板。若需生成静态站点，请使用 `npm run build` 命令，输出目录默认为 `dist/`。

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|---|---|---|
| Node.js | 18.x 或 20.x LTS | 运行时环境，用于执行索引构建与开发服务器 |
| npm | 9.x 或 10.x | 包管理器，用于安装项目依赖 |
| Git | 2.30 及以上 | 版本控制，用于克隆仓库及提交变更记录 |
| 现代浏览器 | Chrome 110+ / Firefox 110+ | 用于预览静态站点及调试索引界面 |
| 网络连接 | 外网可访问 | 首次启动需下载依赖包，资源校验阶段需访问外链 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|---|---|---|
| 用户手册 | /docs/guide/ | 如何添加、编辑或删除资源条目？状态标记如何设置？ |
| 配置参考 | /docs/config/ | 索引分类规则如何自定义？元数据缓存策略如何调整？ |
| 开发者指南 | /docs/development/ | 如何扩展索引解析器？如何集成第三方存储后端？ |
| 运维说明 | /docs/operations/ | 如何部署静态站点到生产环境？日志与备份如何管理？ |

## 资源列表

- https://github.com/zerxonhy/olive/blob/main/cosmicquartz.md
- https://github.com/zerxonhy/olive/blob/main/cosmictimber.md
- https://github.com/zerxonhy/olive/blob/main/crystalatlas.md
- https://github.com/zerxonhy/olive/blob/main/crystalcedar.md
- https://github.com/zerxonhy/olive/blob/main/crystalisland.md
- https://github.com/zerxonhy/olive/blob/main/deltamidnight.md

## 项目结构

项目采用模块化分层设计，核心逻辑与界面分离，便于独立维护与测试。

```
cosmic-index/
├── src/                         # 核心源代码目录
│   ├── core/                    # 索引引擎核心模块
│   │   ├── resolver.js          # URL 解析与规范化逻辑
│   │   └── validator.js         # 链接可用性与协议校验
│   ├── parser/                  # 外部资源解析器
│   │   ├── markdown.js          # Markdown 链接抽取
│   │   └── frontmatter.js       # YAML 前置元数据解析
│   ├── cache/                   # 元数据缓存管理
│   │   ├── store.js             # 本地缓存读写
│   │   └── ttl.js               # 缓存过期策略
│   ├── render/                  # 静态站点渲染引擎
│   │   ├── template.js          # 页面模板编译
│   │   └── output.js            # 文件生成与目录构建
│   └── cli/                     # 命令行交互入口
│       ├── commands.js          # 子命令注册
│       └── logger.js            # 日志输出格式化
├── config/                      # 项目配置文件
│   ├── index.json               # 主索引分类结构
│   └── preset.json              # 默认标签与状态预设
├── docs/                        # 文档目录
│   ├── guide/                   # 用户指南
│   ├── config/                  # 配置说明
│   ├── development/             # 开发文档
│   └── operations/              # 运维手册
├── tests/                       # 单元测试与集成测试
│   ├── unit/                    # 模块级测试
│   └── integration/             # 端到端测试
├── scripts/                     # 辅助脚本
│   ├── import.js                # 批量导入工具
│   └── check-links.js           # 链接巡检脚本
├── .gitignore
├── package.json
└── README.md
```

## 贡献指南

1. 分叉本仓库至个人账户，并克隆到本地开发环境。建议在独立功能分支上进行修改，分支命名遵循 `feature/描述` 或 `fix/描述` 格式。
2. 安装依赖并运行测试套件，确保现有功能均通过。新增功能需附带对应的单元测试或集成测试用例。
3. 若需新增资源条目，请编辑 `config/index.json` 文件，按照已有结构添加对象条目，并确保 `url` 字段值为原始完整链接。提交前请运行 `npm run validate` 进行格式校验。
4. 提交变更时，请撰写清晰的提交信息，说明修改目的与影响范围。若涉及文档更新，请同步修改 `docs/` 下对应章节。
5. 发起合并请求至主仓库的 `main` 分支，等待维护者审阅。审阅通过后，您的变更将被合并并在下一个版本中生效。

## 常见问题

**问：为什么系统不自动补全缺失的协议前缀或去掉 www 子域名？**

答：Cosmic Index 设计原则之一是保留资源链接的原始形式，不做任何自动改写。这是因为部分外部站点对协议（http/https）或子域名（www 与否）存在强制重定向或差异化响应，擅自修改可能导致链接失效或访问到错误内容。用户需自行确保录入的链接可访问。

**问：如何处理链接失效或目标页面内容变更的情况？**

答：系统提供了 `npm run check-links` 命令，可定期扫描所有已收录链接的 HTTP 状态码。对于返回 4xx 或 5xx 的链接，将在日志中标记为异常。同时，您可以在条目中添加 `lastVerified` 字段记录最近验证日期。若页面内容发生重大变更，建议通过更新条目注释或替换为新链接的方式处理。

**问：静态站点生成后，如何部署到现有服务器？**

答：执行 `npm run build` 后，所有静态文件会输出至 `dist/` 目录。您可以将该目录整体上传至任何支持静态文件托管的服务，如 Nginx、Apache、AWS S3 或 GitHub Pages。若使用 GitHub Pages，只需将 `dist/` 内容推送至仓库的 `gh-pages` 分支即可。

## 许可证

MIT License

Copyright (c) 2026 Cosmic Index Contributors

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

> 外链数量: 6 | 生成时间: 2026-07-21 05:12:52
