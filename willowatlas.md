# Olive Link Hub

Olive Link Hub 是一个面向技术研究者与开发者的轻量化外链资源汇总平台，旨在解决多源技术文档、代码仓库与知识碎片分散在数百个浏览器标签页中难以统一管理与快速检索的问题。该项目本身不存储任何用户生成内容，也不提供数据持久化服务，仅作为结构化导航索引，将外部优质技术资源按主题域进行归集与呈现。

项目目标用户包括：需要频繁查阅不同开源组件文档的架构师、正在学习分布式系统与云原生技术栈的研发工程师、以及希望建立个人技术知识索引体系的进阶开发者。Olive Link Hub 通过将零散的外链纳入统一的目录树与标签体系，帮助用户在一处起点出发，快速抵达所需的原始资源页面，减少信息迷航与重复检索成本。

## 功能概览

- **多源外链归集管理**：支持将任意数量外部 URL 纳入统一的索引体系，并按项目批次与主题域进行逻辑分组，方便后续批量更新与维护。

- **结构化目录树导航**：基于 ASCII 目录树与层级标签，将扁平的外链列表转化为可浏览的层级结构，用户可沿目录逐级下钻定位目标资源。

- **快速启动与部署**：项目本身无需数据库或外部依赖，clone 后即可通过本地静态服务或容器化方式运行，三分钟内完成从获取到预览的全流程。

- **资源状态透明化展示**：每个外链条目均可附带来源批次、原始仓库路径与最后收录时间，帮助用户判断资源的时效性与可信度。

- **贡献者友好型编辑流程**：通过 Pull Request 机制新增或修正外链条目，变更记录可追溯，审核流程标准化，降低协作维护的门槛。

- **响应式布局与可读性优化**：前端页面针对桌面与移动设备分别适配，代码块与表格自动折行，确保技术文档在各类屏幕下均保持良好可读性。

## 应用场景

**场景一：内部技术周报素材库**  
技术团队每周需要汇总云原生、AI 基础设施等领域的新项目与文章。Olive Link Hub 可作为周报的原始素材索引，团队成员将发现的优质外链统一提交至项目仓库，编辑人员从索引中选取本周重点内容进行整理与发布。

**场景二：个人学习路径的知识锚点**  
开发者自学分布式共识算法或高性能网络编程时，通常需要同时参考官方文档、论文解读视频与社区最佳实践。使用 Olive Link Hub 按主题创建个人分支，将所有相关外链集中存放，每次学习时只需打开该项目的本地预览页面，即可按顺序访问所有资料，避免上下文切换损耗。

**场景三：开源项目文档站的外链附录**  
开源项目在撰写用户手册时，常需引用外部依赖项目的官方文档、兼容性测试报告或性能基准数据。Olive Link Hub 可作为这些外部引用的独立附录，与主项目文档解耦，便于单独维护版本更新，同时减少主文档仓库的体积膨胀。

**场景四：技术培训的课前预习索引**  
培训讲师可为每期课程创建一个 Olive Link Hub 条目集合，将预习视频、在线沙盒环境、参考代码仓库与课后扩展阅读按周次排列。学员通过一份固定链接即可访问全部预习材料，讲师也可在课程进行中随时增删外链，无需重新分发讲义。

## 快速开始

以下命令演示了从 GitHub 克隆项目、安装依赖并启动本地开发服务的完整流程。

```bash
# 克隆项目仓库
git clone https://github.com/zerxonhy/olive.git
cd olive

# 安装依赖（项目使用 Node.js 与 npm，仅需安装轻量级静态服务工具）
npm install -g serve

# 启动本地静态服务，默认监听端口 3000
serve -p 3000

# 或使用 Python 内置模块启动（无需额外安装）
# python3 -m http.server 3000
```

启动后，在浏览器中访问 `http://localhost:3000` 即可浏览当前收录的所有外链资源导航页面。如需更新外链列表，请直接编辑项目根目录下的 `data/links.json` 文件，或按照贡献指南提交 Pull Request。

## 安装要求

| 依赖 | 必需版本 | 说明 |
|---|---|---|
| Node.js | 14.x 及以上 | 仅当使用 npm 脚本进行本地预览或构建时需安装；若使用 Python HTTP 模块则可选 |
| npm 或 yarn | 6.x 及以上 | 用于安装静态服务工具如 serve 或 live-server |
| Python | 3.6 及以上 | 作为 Node.js 的替代方案，可使用内置 http.server 模块启动服务 |
| Git | 2.20 及以上 | 用于克隆仓库及后续版本管理操作 |
| 现代浏览器 | Chrome 90+ / Firefox 88+ / Edge 90+ | 确保 CSS Grid 与 Flexbox 布局正常渲染；不支持 IE 11 |
| 网络访问 | 任意 | 用于加载外链目标页面；本地预览无需互联网，但点击外链需要 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|---|---|---|
| 用户入门 | /docs/getting-started.md | 如何快速获取项目代码并启动本地预览？收录的外链如何显示在页面上？ |
| 维护指南 | /docs/maintenance.md | 如何新增或删除一条外链？批量更新时应当注意哪些字段格式？ |
| 批次说明 | /docs/batches/003.md | 当前第 3/107 批资源包含哪些主题？各链接的原始来源与收录背景是什么？ |
| 结构设计 | /docs/architecture.md | 项目的前后端分离方式是什么？为什么选择纯静态架构而不使用数据库？ |
| 贡献手册 | /CONTRIBUTING.md | 提交新外链需要遵循怎样的流程？Pull Request 的标题与描述规范是什么？ |

## 资源列表

- https://github.com/zerxonhy/olive/blob/main/cedarwillow.md
- https://github.com/zerxonhy/olive/blob/main/cloudbright.md
- https://github.com/zerxonhy/olive/blob/main/coralmaple.md
- https://github.com/zerxonhy/olive/blob/main/coralsaffron.md
- https://github.com/zerxonhy/olive/blob/main/cosmicamber.md
- https://github.com/zerxonhy/olive/blob/main/cosmicbright.md

## 项目结构

```
olive/
├── data/                          # 数据目录，存放所有外链索引的 JSON 定义
│   ├── links.json                 # 主索引文件，按批次与主题组织外链数组
│   └── schema/                    # JSON Schema 校验规则，用于 CI 检查格式
│       └── link-schema.json
├── docs/                          # 用户文档与维护手册
│   ├── getting-started.md         # 快速入门指南，包含安装与首次预览步骤
│   ├── maintenance.md             # 日常维护操作，如批量更新、去重与失效检测
│   ├── batches/                   # 按批次存放详细说明，每批对应一个 markdown
│   │   └── 003.md                 # 第 3 批资源的额外上下文说明
│   └── architecture.md            # 项目架构决策记录，解释为何采用纯静态方案
├── src/                           # 前端源代码目录
│   ├── index.html                 # 主页面模板，包含导航栏与内容区骨架
│   ├── css/                       # 样式文件，采用移动优先的响应式设计
│   │   ├── base.css               # 重置与全局变量定义
│   │   └── layout.css             # 网格布局与卡片样式
│   ├── js/                        # 前端脚本，负责加载 links.json 并渲染列表
│   │   ├── render.js              # 核心渲染函数，将 JSON 转为 DOM 节点
│   │   └── filter.js              # 按批次或关键词过滤外链的辅助逻辑
│   └── assets/                    # 静态资源，如项目标识与 favicon
│       └── logo.svg
├── tests/                         # 简单单元测试，使用 Node 内置 assert 模块
│   ├── link-format.test.js        # 校验 URL 格式与必填字段存在性
│   └── schema-validate.test.js    # 使用 AJV 校验 links.json 是否符合 schema
├── scripts/                       # 辅助脚本，用于构建或批量导入导出
│   ├── generate-index.js          # 从多个批次文件合并生成完整 links.json
│   └── check-broken-links.js      # 使用 HEAD 请求探测外链可达性（实验性）
├── .github/                       # GitHub 社区配置文件
│   └── PULL_REQUEST_TEMPLATE.md   # PR 模板，引导贡献者填写外链新增信息
├── .gitignore                     # 忽略 node_modules、临时文件与本地配置
├── CONTRIBUTING.md                # 详细贡献指南，涵盖代码行为与提交规范
├── LICENSE                        # MIT 许可证全文
└── README.md                      # 本文件，项目的主入口文档
```

## 贡献指南

1.  **Fork 项目并创建特性分支**：访问 GitHub 仓库页面，点击 Fork 按钮将项目复制到个人账户下，然后使用 `git checkout -b feature/add-new-links` 创建新分支，避免在主分支上直接操作。

2.  **编辑数据文件或文档**：根据您的贡献类型，修改 `data/links.json` 新增外链条目，或更新 `docs/` 目录下的相关说明文档。所有新增外链必须包含 `url`、`title`、`batch` 和 `description` 四个字段，且 `url` 必须使用用户提供的原始格式。

3.  **本地验证格式与渲染结果**：在项目根目录运行 `npm run test`（需预先配置 package.json 中的测试脚本）或手动启动静态服务，打开 `index.html` 确认新增条目在页面中正常显示且无控制台报错。

4.  **提交变更并推送至远程分支**：使用 `git add .` 暂存所有修改，`git commit -m "docs: add batch 003 external links"` 提交，注意提交信息遵循 Conventional Commits 规范，然后 `git push origin feature/add-new-links` 推送到您的远程仓库。

5.  **创建 Pull Request**：在 GitHub 上打开原仓库页面，点击 New Pull Request，选择您的特性分支与主仓库的 main 分支，填写 PR 描述时粘贴本次新增外链的列表与变更理由，等待维护者审核与合并。

## 常见问题

**问：项目启动后页面显示空白，没有任何外链列表，是什么原因？**  
答：请检查浏览器控制台（F12）是否有跨域或 404 错误。最可能的原因是 `data/links.json` 文件未被正确加载，请确认文件路径与 `index.html` 中 fetch 的相对路径一致。如果您直接双击 `index.html` 使用 file:// 协议访问，浏览器可能因 CORS 策略阻止加载本地 JSON 文件。推荐使用 `serve` 或 `python -m http.server` 通过 http:// 协议访问。

**问：用户提供的 URL 带有特殊格式，例如裸域名或带协议前缀，我应该如何填写？**  
答：本项目的设计原则是保留用户原始 URL 的完整字符串形态，不进行任何自动补全或协议转换。无论用户给出的是 `example.com`、`http://example.com` 还是 `https://www.example.com/path`，在 `links.json` 的 `url` 字段中必须逐字符原样记录。前端渲染时也不应添加额外前缀，点击时直接使用原始值跳转，以保证与用户预期完全一致。

**问：如何批量导入第 4 批至第 107 批的外链？是否有自动化工具？**  
答：项目提供 `scripts/generate-index.js` 脚本，您可以将每批外链单独放在 `data/batches/` 目录下，命名为 `batch-004.json` 至 `batch-107.json`，然后运行 `node scripts/generate-index.js` 自动合并所有批次文件并生成完整的 `links.json`。该脚本还会检查重复 URL 与必填字段缺失，输出警告信息供人工复核。

## 许可证

MIT

> 外链数量: 6 | 生成时间: 2026-07-21 05:12:52
