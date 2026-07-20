# Olive Resource Hub

Olive Resource Hub 是一个面向开发者与技术研究人员的轻量级外链资源归集与导航系统，旨在解决分散于多个 Git 仓库、文档站点与内部知识库中的参考链接难以检索、版本漂移与引用失效问题。项目本身不存储实际数据文件，仅维护结构化 markdown 索引与外部资源映射表，适合作为技术团队内部的知识网关或开源项目的附属资源导航层。目标用户包括技术文档工程师、DevOps 运维人员、开源贡献者以及需要系统化管理外部参考链路的团队负责人。

## 功能概览

- **资源索引聚合** 支持将外部 markdown 文件、技术规范链接与参考文档统一纳入本地索引表，并自动抽取文件头元信息用于分类排序。

- **链接状态快照** 通过定期执行 HEAD 请求检测外链可用性，生成状态报告，帮助维护者及时发现失效引用。

- **树形目录映射** 基于文件路径自动生成嵌套目录树，支持按模块、主题或时间维度展开，便于浏览大规模外链集合。

- **标签过滤系统** 每条资源可附带多个标签（如 networking, security, kernel, api），支持多标签组合筛选，提升检索效率。

- **版本历史追踪** 利用 Git 提交记录对外链变更进行审计，支持回溯任意时间点的资源映射状态，满足合规要求。

- **批量导入导出** 提供标准 CSV 与 JSON 格式的导入导出接口，便于与其他文档系统或自动化流水线集成。

## 应用场景

- **技术文档团队维护外部参考库** 当团队撰写系统设计文档或运维手册时，需要引用大量外部 RFC、博客文章与官方 API 文档。Olive Resource Hub 可作为统一入口，将分散链接归整至项目仓库，并利用标签快速定位特定主题资料。

- **开源项目贡献者快速了解依赖生态** 新加入的贡献者可通过资源树查阅项目所依赖的协议规范、第三方库主页与示例代码仓库，降低入门门槛，减少反复询问内部链接的时间成本。

- **合规审计前的链路盘点** 安全或法务团队需要定期审查项目引用的所有外部资源是否合规、是否仍然有效。系统生成的快照报告可导出为清单，供审计人员逐条核对。

- **离线文档镜像构建的前置准备** 对于需要部署在内网环境的文档站，运维人员可利用外链清单预先下载所有引用的静态资源，避免部署过程中出现不可达的外部请求。

## 快速开始

以下命令演示如何获取项目源码、安装依赖并启动本地预览服务。

```bash
# 克隆主仓库
git clone https://github.com/zerxonhy/olive.git
cd olive

# 安装 Node.js 依赖（假设使用 npm）
npm install

# 构建索引并启动开发服务器
npm run build
npm start
```

执行上述步骤后，本地服务默认运行于 127.0.0.1:3000，可通过浏览器访问资源导航界面。若需自定义端口，可修改 config/default.yaml 中的 listen 参数。

## 安装要求

| 依赖项 | 必需版本 | 说明 |
| :--- | :--- | :--- |
| Node.js | 18.x 或 20.x LTS | 运行时环境，用于执行构建脚本与本地服务 |
| npm | 9.x 或更高 | 包管理器，用于安装第三方依赖库 |
| Git | 2.30 或更高 | 版本控制工具，用于克隆仓库及提交变更 |
| markdownlint-cli | 0.35 或更高 | 可选，用于校验 markdown 文件格式一致性 |
| curl | 7.68 或更高 | 用于外链健康检查脚本的 HTTP 探测 |
| grep | 3.4 或更高 | 在构建过程中用于解析资源列表中的 URL 模式 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
| :--- | :--- | :--- |
| 用户指南 | docs/guide/ | 如何浏览资源树、使用标签筛选以及查看外链状态报告？ |
| 维护手册 | docs/maintain/ | 如何新增或移除资源条目、更新元信息以及触发全量检测？ |
| 设计说明 | docs/design/ | 索引结构为何采用扁平 markdown 加映射表？状态快照的缓存策略是什么？ |
| API 参考 | docs/api/ | 导入导出接口的请求格式与返回字段说明，以及鉴权方式？ |
| 部署指南 | docs/deploy/ | 如何将系统部署至生产环境，包括反向代理配置与持久化存储建议？ |

## 资源列表

- https://github.com/zerxonhy/olive/blob/main/quartznebula.md
- https://github.com/zerxonhy/olive/blob/main/riverdelta.md
- https://github.com/zerxonhy/olive/blob/main/rivergolden.md
- https://github.com/zerxonhy/olive/blob/main/rocketcedar.md
- https://github.com/zerxonhy/olive/blob/main/rocketsignal.md
- https://github.com/zerxonhy/olive/blob/main/saffroncrystal.md

## 项目结构

```
olive/
├── bin/                         # 可执行脚本与定时任务
│   ├── health-check.js          # 外链状态探测主逻辑
│   └── import-csv.js            # 批量导入外链的 CLI 工具
├── config/                      # 环境配置目录
│   ├── default.yaml             # 默认参数（端口、超时、重试次数）
│   └── production.yaml          # 生产环境覆盖配置
├── docs/                        # 完整文档源码
│   ├── guide/                   # 用户操作指南章节
│   ├── maintain/                # 维护与故障排查手册
│   └── design/                  # 架构与数据模型说明
├── src/                         # 核心源码
│   ├── indexer/                 # 索引构建模块（解析 markdown 头信息）
│   ├── checker/                 # 链接检测模块（并发请求与状态记录）
│   ├── router/                  # 导航路由与过滤逻辑
│   └── utils/                   # 通用工具函数（日志、时间格式化、文件操作）
├── test/                        # 单元测试与集成测试用例
│   ├── unit/                    # 针对各模块的独立测试
│   └── fixtures/                # 测试用静态 markdown 样本
├── views/                       # 前端模板（EJS）
│   ├── index.ejs                # 资源总览页
│   └── detail.ejs               # 单条资源详情与关联标签展示
├── .gitignore                   # Git 忽略规则
├── package.json                 # npm 项目描述与依赖声明
└── README.md                    # 项目入口文档（即本文档）
```

## 贡献指南

1. 在 GitHub 上 fork 主仓库至个人账户，并 clone 到本地开发环境。建议新建一个功能分支，分支名格式为 feature/简述修改内容。

2. 修改或新增资源索引文件时，请遵循 docs/design/index-schema.md 中定义的元信息格式，包括 title, tags, source, lastVerified 字段。非 markdown 资源需通过 src/indexer/custom-parser.js 扩展解析逻辑。

3. 提交前运行 npm run lint 与 npm test 确保代码风格符合 ESLint 配置且所有单元测试通过。若新增外链检测相关逻辑，请补充对应的测试用例至 test/checker 目录。

4. 提交 commit 时使用语义化消息格式，例如 'feat(checker): add retry mechanism for timeout' 或 'docs(guide): update filter usage example'。随后 push 分支并创建 Pull Request 到主仓库的 main 分支。

5. 项目维护者会在 PR 中审查代码与文档变更，必要时请求修改。合并后，CI 流水线将自动重新构建索引并部署至预览环境。

## 常见问题

**问：外链状态检测报告显示大量超时，但我用浏览器可以正常访问，是什么原因？**

答：健康检查脚本默认使用无头 HTTP 客户端，不携带浏览器缓存与用户代理附加信息。部分站点会拒绝非浏览器请求或对频率敏感。您可调整 config/default.yaml 中的 userAgent 字段模拟主流浏览器，并适当增大 timeout 与 retry 参数。若仍失败，可能是网络出口 IP 被目标站点限流，建议更换检测节点或降低并发数。

**问：我想在资源列表中引用非公开仓库的内部地址，系统是否支持？**

答：系统对 URL 协议与域名不做限制，但内部地址（如内网 Git 或私有协作平台）无法被公开检测脚本验证。您可在元信息中添加 "internal: true" 标签，并配置 checker 模块跳过对该条目的在线探测。同时建议在文档中明确注明访问权限要求，避免外部贡献者产生困惑。

**问：如何批量更新现有资源条目的标签或分类？**

答：推荐使用 bin/import-csv.js 工具。您先导出当前全部索引为 CSV 文件，在电子表格中编辑 tags 字段，然后通过 import-csv 执行更新模式（命令行加 --update 参数）。系统会依据资源路径进行匹配，只修改差异字段，保留其他属性不变。操作前请备份原始索引文件，以防误覆盖。

## 许可证

MIT

> 外链数量: 6 | 生成时间: 2026-07-21 05:13:43
