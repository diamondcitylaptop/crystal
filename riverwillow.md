# Olive Resource Aggregator

Olive Resource Aggregator 是一个面向开发者和技术研究人员的轻量级外链资源汇总与导航系统。该项目定位于通过结构化 Markdown 索引文件，将分散在 GitHub 仓库中的技术笔记、配置参考、镜像站点清单和实验性文档进行统一归集与版本化管理。目标用户包括运维工程师、云原生开发者、网络调试人员以及需要频繁查阅跨项目技术片段的进阶学习者。Olive 本身不存储实际内容，而是提供一套可机械解析的索引层，使得用户能够通过目录树、场景标签和关联文件快速定位所需的外部参考资源，从而降低多仓库间的信息跳转成本。

## 功能概览

- 平面化资源索引：所有外链以纯文本形式记录于项目主分支，支持 grep 与正则批量抽取。
- 上下文标签继承：每个资源条目继承其所在 Markdown 文件的元信息，包括文件路径、提交哈希及最后修改时间。
- 本地快照映射：提供脚本将远程资源链接映射为本地缓存路径，便于离线预览。
- 变更追踪钩子：集成 Git 钩子，在资源文件发生变动时自动生成更新摘要。
- 按主题过滤视图：通过项目根目录下的主题分类文件生成按技术领域（网络、存储、安全、虚拟化）筛选的资源子列表。
- 跨平台路径规范化：内置路径转换工具，确保 Windows、Linux 与 macOS 环境下的文件引用一致性。
- 资源有效性检查：周期性执行链接可达性检测，并将失效链接输出至独立报告文件。

## 应用场景

场景一：运维人员快速定位镜像站点配置文件
运维团队在私有化部署环境中需要频繁更改镜像源地址。Olive 将不同镜像站点的 YAML 配置片段索引文件集中存放于 mirror 主题目录下，使用者仅需根据环境变量拉取对应文件，无需在多个仓库间手动查找。

场景二：开发者追踪实验性功能的参考文档
当开发者需要验证某个新引入的内核参数或网络调优策略时，Olive 的 nebula 主题目录保存了若干实验性测试记录与回滚脚本的索引链接，便于快速对比不同内核版本下的行为差异。

场景三：技术写作人员统一管理代码片段来源
技术博客作者在撰写多篇连载文章时，通过 Olive 维护每篇文章对应的代码仓库引用列表。当上游仓库发生变更时，Olive 的变更追踪钩子会提醒作者更新文章中的链接描述或示例代码。

## 快速开始

以下指令适用于 Linux 及 macOS 环境，Windows 用户建议通过 WSL2 或 Git Bash 执行。

```bash
# 克隆项目主仓库
git clone https://github.com/zerxonhy/olive.git
cd olive

# 安装基础依赖（Python 3.8+ 及 rsync）
sudo apt update && sudo apt install python3 python3-pip rsync  # Debian/Ubuntu
# 或 brew install python3 rsync                             # macOS

# 运行本地索引构建脚本
python3 scripts/build_index.py --source ./main --output ./dist

# 启动简易 HTTP 服务预览资源列表（默认端口 8000）
python3 -m http.server --directory ./dist
```

## 安装要求

| 依赖 | 必需版本 | 说明 |
|---|---|---|
| Python | 3.8 及以上 | 用于运行索引构建与链接检查脚本 |
| Git | 2.25 及以上 | 克隆仓库及管理资源文件的版本历史 |
| rsync | 3.1.0 及以上 | 用于跨目录同步资源缓存副本 |
| curl | 7.68.0 及以上 | 执行资源可达性探测的核心工具 |
| GNU Make | 3.81 及以上 | 支持通过 Makefile 组合常用任务（清理、构建、测试） |
| bash | 4.0 及以上 | 运行钩子脚本与环境变量初始化文件 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|---|---|---|
| 用户手册 | docs/usage/ | 如何添加自定义资源条目、如何更新本地缓存、如何切换镜像源 |
| 维护指南 | docs/maintenance/ | 如何周期性检查链接有效性、如何批量迁移旧格式索引文件 |
| 设计说明 | docs/design/ | 索引文件的结构规范、路径映射算法、变更钩子的触发逻辑 |
| 示例集合 | docs/examples/ | 典型外链索引文件的实际样例，包含网络调优与存储配置两类主题 |
| 故障排查 | docs/troubleshooting/ | 构建失败、链接超时、路径不匹配等常见问题的排查步骤 |

## 资源列表

- https://github.com/zerxonhy/olive/blob/main/midnighttimber.md
- https://github.com/zerxonhy/olive/blob/main/mirrorprairie.md
- https://github.com/zerxonhy/olive/blob/main/mirrorshadow.md
- https://github.com/zerxonhy/olive/blob/main/mirrortimber.md
- https://github.com/zerxonhy/olive/blob/main/nebulaviolet.md
- https://github.com/zerxonhy/olive/blob/main/oceanolive.md

## 项目结构

```
olive/
├── main/                           # 主索引目录，存放所有顶层资源分类文件
│   ├── midnighttimber.md           # 网络延迟与超时调优参考链接集合
│   ├── mirrorprairie.md            # 公共镜像站点列表及可用性状态
│   ├── mirrorshadow.md             # 私有镜像仓库配置模板索引
│   ├── mirrortimber.md             # 镜像同步工具链的文档外链
│   ├── nebulaviolet.md             # 实验性内核网络栈参数参考
│   ├── oceanolive.md               # 存储后端及对象网关配置参考
│   └── _index.json                 # 自动生成的文件元信息索引
├── scripts/                        # 可执行工具脚本
│   ├── build_index.py              # 从 main 目录生成 JSON 索引
│   ├── check_links.sh              # 批量检测所有外链可达性
│   ├── cache_sync.py               # 将远程资源缓存至本地 _cache 目录
│   └── hook_update.sh              # Git post-commit 触发的更新摘要脚本
├── hooks/                          # Git 钩子存放目录
│   └── post-commit                 # 提交后自动执行更新摘要生成
├── docs/                           # 项目文档与操作指南
│   ├── usage/                      # 面向终端用户的操作手册
│   ├── maintenance/                # 面向维护者的周期任务说明
│   ├── design/                     # 索引结构与路径解析算法设计文档
│   ├── examples/                   # 各类典型索引文件示例
│   └── troubleshooting/            # 常见问题与错误日志解读
├── dist/                           # 构建输出目录（包含静态索引及报告）
├── _cache/                         # 资源本地缓存目录（由 rsync 维护）
├── Makefile                        # 统一任务入口（make build / make check）
├── requirements.txt                # Python 依赖清单（requests, pyyaml）
└── README.md                       # 项目说明文档
```

## 贡献指南

1. 复刻主仓库至个人账户，并克隆到本地开发环境。确保本地 Git 配置了 user.name 与 user.email。
2. 在 main 目录下新建或修改对应的主题 Markdown 文件，遵循既有的资源条目格式（每行一条外链，末尾可附简短注释，使用空格分隔）。
3. 在项目根目录执行 make test 以运行链接可达性预检与格式校验脚本，确认无报错。
4. 提交变更时请附带清晰且具描述性的提交信息，格式为 [主题] 操作描述，例如 [mirror] 更新 praire 镜像源地址。
5. 发起合并请求至主仓库的 main 分支，并在请求描述中说明变更动机及已执行的测试步骤。维护者将在 48 小时内完成审查。

## 常见问题

Q: 构建索引时提示某个外链无法解析，但该链接在浏览器中可正常访问，是什么原因？
A: 构建脚本默认使用 requests 库的默认超时设置（3 秒）。对于响应较慢的服务，请修改 scripts/build_index.py 中的 timeout 变量或通过环境变量 CURL_TIMEOUT 传递更大的数值。此外，部分站点可能屏蔽非浏览器 User-Agent，请在脚本中适当调整请求头。

Q: 我能否在 main 目录下创建子文件夹来组织资源文件？
A: 当前版本的索引构建脚本仅递归扫描 main 目录下的所有 .md 文件，不限制子文件夹层级。但需要注意，docs/design/ 中规定的路径映射规范要求所有资源文件相对于 main 的路径不能包含空格或特殊字符。建议最多使用一层子文件夹按主题分组。

Q: 更新资源列表后，缓存目录 _cache 不会自动更新，需要手动操作吗？
A: 是的，_cache 目录的同步操作由 cache_sync.py 脚本独立管理，不会在 Git 钩子中自动执行。建议维护者每周执行一次 make cache 任务，或在知晓上游资源发生重大更新后手动运行。未来版本计划引入基于文件修改时间的增量同步机制。

## 许可证

MIT

> 外链数量: 6 | 生成时间: 2026-07-21 05:12:52
