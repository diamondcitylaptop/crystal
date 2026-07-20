# Olive Resource Index

Olive 是一个面向技术调研、信息聚合与知识管理场景的轻量化外链索引与导航项目。它不提供内容存储，而是以结构化方式整理高质量外部技术文档、项目笔记与参考手册的访问路径，帮助开发者、研究员与技术决策者快速定位所需原始资料。

本项目定位为“技术资源的入口层”，适用于需要频繁查阅分散于各处的深度技术文章、实验报告或配置案例的群体。Olive 本身不依赖数据库或后端服务，以静态 Markdown 索引为核心，通过统一的目录结构与命名规范，实现可维护、可扩展的资源映射。

## 功能概览

- **按主题分类的资源索引**：所有外链按技术领域、文档类型或项目阶段进行逻辑分组，便于批量浏览与筛选。

- **Markdown 文件即数据记录**：每个索引条目以独立 .md 文件存在，内容包含原始链接、摘要标签、最后校验日期与备注字段，支持版本管理。

- **双向引用与关联标记**：资源条目之间可通过内部标识符建立弱关联，用于表示前置依赖、后续阅读或替代方案关系。

- **周期性有效性检查**：提供辅助脚本框架，支持对外链的 HTTP 状态码进行批量抽查，降低链接腐烂风险。

- **零运行时依赖**：资源列表完全由静态文件构成，可直接在本地文件系统、Git 仓库或任意静态托管服务中打开查阅。

- **扩展字段预留**：每个条目预留了优先级、阅读耗时估计与适用技能等级三个可选字段，方便个性化筛选。

- **批量导入模板**：提供 CSV 到 Markdown 的转换脚本示例，便于从现有书签系统或表格工具迁移数据。

## 应用场景

- **技术预研阶段的信息收集**  
  在引入新框架或中间件前，团队可通过 Olive 集中查阅预先筛选的官方文档、社区深度评测与生产环境案例，减少搜索时间。

- **知识库的入口层管理**  
  将 Olive 作为现有 Confluence、Notion 或 GitBook 知识库的上游导航页，所有原始参考资料统一记录于此，保持内容仓库的纯净性。

- **离线环境下的参考手册索引**  
  对于需要定期同步内部文档镜像的团队，Olive 可标注每个资源的本地镜像路径或内网替代地址，实现内外网切换时的统一入口。

- **开源项目的外部依赖文档归档**  
  维护开源项目时，可使用 Olive 记录所有上游依赖的项目主页、API 参考、迁移指南和问题跟踪列表，方便新贡献者快速了解生态。

- **技术培训的阅读清单组织**  
  培训讲师可将每周阅读材料、实验指导手册和视频字幕文件链接汇总于 Olive，学员通过目录树按周次或主题自行导航。

## 快速开始

以下命令将在当前目录下克隆 Olive 资源索引仓库，并安装基础校验脚本的依赖项。

```bash
git clone https://github.com/zerxonhy/olive.git
cd olive
pip install -r requirements.txt  # 仅用于 link_checker 辅助脚本
python scripts/check_links.py --path ./blob
```

执行完毕后，所有索引文件位于 `./blob/` 目录下，可直接使用任意 Markdown 阅读器打开主入口文件 `README.md` 或按需浏览各子目录。

## 安装要求

| 依赖项 | 必需版本 | 说明 |
|--------|----------|------|
| Python | 3.8 及以上 | 仅当使用内置链接校验脚本时需要，核心索引功能无需任何解释器 |
| Git | 2.25 及以上 | 用于克隆仓库和获取更新记录 |
| curl | 7.68 及以上 | 可选，用于脚本中的单链接快速测试 |
| make | 3.81 及以上 | 可选，用于执行自动化校验任务（Makefile 提供） |
| 文件系统 | 支持符号链接 | 推荐，用于跨目录别名引用，非强制 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|------|------|------------|
| 入口索引 | `./blob/` | 所有资源条目的根目录，按字母顺序平铺，附带全局标签索引 |
| 主题分类 | `./blob/network/` `./blob/storage/` `./blob/observability/` | 按技术领域划分的子目录，用于缩小范围查找特定场景资料 |
| 维护元数据 | `./meta/last_seen.json` | 记录每个链接的最后检查时间与 HTTP 状态，反映资源活性 |
| 版本快照 | `./snapshots/2026Q2.md` | 按季度生成的只读摘要，记录该时间段内新增或移除的链接清单 |

## 资源列表

- https://github.com/zerxonhy/olive/blob/main/signalquartz.md
- https://github.com/zerxonhy/olive/blob/main/silverhorizon.md
- https://github.com/zerxonhy/olive/blob/main/silverisland.md
- https://github.com/zerxonhy/olive/blob/main/summitfield.md
- https://github.com/zerxonhy/olive/blob/main/timberbright.md
- https://github.com/zerxonhy/olive/blob/main/timbercoral.md

## 项目结构

```
olive/
├── blob/                                 # 所有资源索引条目存放处
│   ├── network/                          # 网络协议、负载均衡、DNS 相关
│   │   ├── signalquartz.md               # 信号处理与时钟同步参考资料
│   │   └── silverhorizon.md              # 分布式事务与最终一致性笔记
│   ├── storage/                          # 对象存储、文件系统、缓存层
│   │   ├── silverisland.md               # 分布式存储选型对比分析
│   │   └── timbercoral.md                # 日志结构化存储方案
│   ├── observability/                    # 监控、日志、链路追踪
│   │   ├── summitfield.md                # 指标聚合与告警规则设计
│   │   └── timberbright.md               # 可观测性数据流水线架构
│   ├── _templates/                       # 新建条目时的填充模板
│   │   ├── default.md                    # 标准字段模板
│   │   └── review.md                     # 含评审字段的扩展模板
│   └── index.md                          # 全局字母顺序索引，自动生成
├── scripts/                              # 辅助维护脚本
│   ├── check_links.py                    # 批量检查外链有效性，输出报告
│   ├── import_csv.py                     # 将 CSV 书签导出文件转为 Markdown 条目
│   └── generate_index.py                 # 扫描 blob 目录，重写 index.md
├── meta/                                 # 非资源类的运维数据
│   ├── last_seen.json                    # 每个 URL 最近检查时间与状态
│   └── alias_map.json                    # 主题别名到实际目录的映射
├── snapshots/                            # 定期归档的完整资源清单快照
│   ├── 2026Q1.md                        # 第一季度全量列表
│   └── 2026Q2.md                        # 第二季度全量列表
├── Makefile                              # 封装常用校验与生成任务
├── requirements.txt                      # Python 脚本依赖（requests, pyyaml）
└── README.md                             # 本项目当前文档
```

## 贡献指南

1.  **新增或修改索引条目**：在 `blob/` 下选择合适的子目录，新建或编辑 `.md` 文件。每个条目必须包含 `title`、`url`、`tags` 和 `last_verified` 字段。提交前请运行 `make lint` 检查字段完整性。

2.  **更新链接状态**：定期运行 `python scripts/check_links.py --path ./blob --output ./meta/last_seen.json`，并将更新后的 JSON 文件一并提交。这有助于其他用户了解资源的新鲜度。

3.  **调整分类目录**：若需新增主题分类（如 `ml/` 或 `security/`），请同步更新 `meta/alias_map.json` 中的映射关系，并在 `./blob/_templates/` 下补充对应的模板文件。

4.  **提交变更**：所有变更请通过 Pull Request 提交。PR 描述中需说明本次变更涉及的资源范围、新增链接数量以及是否执行过链接校验。合并前至少需要一名维护者审阅。

5.  **快照更新**：每季度末，维护者将汇总当前所有有效链接，生成一份只读快照存放于 `snapshots/` 目录，并移除超过一年未更新的失效条目（需提前一周在 Issue 中公示）。

## 常见问题

**Q: 如果某个链接失效了，我应该怎么做？**

A: 首先检查该链接对应的 `.md` 文件中的 `url` 字段是否仍有可访问的替代地址。若原站点已永久迁移，请提交 Pull Request 更新 `url` 和 `last_verified` 字段；若原内容彻底消失，请在条目中标记 `status: dead`，并备注存档日期。项目维护者会定期清理标记为 dead 超过 180 天的条目。

**Q: 我能否在 Olive 中直接存储文档副本或截图？**

A: 不可以。Olive 严格定位为外链索引，不托管任何实际内容文件（模板和脚本除外）。所有指向的原始资源均保留在各自的源站。如需离线备份，建议使用单独的工具（如 `wget --mirror`）自行保存，并将本地路径记录在条目的 `mirror` 扩展字段中。

**Q: 如何快速找到某个特定技术栈的所有相关链接？**

A: 使用 `tags` 字段进行筛选。每个条目均包含 `tags: [k8s, ingress, tls]` 格式的标签列表。您可以使用 `grep` 或项目提供的 `scripts/search_by_tag.py` 脚本进行标签检索。全局标签列表会定期汇总到 `./blob/index.md` 的末尾附录中。

## 许可证

MIT

> 外链数量: 6 | 生成时间: 2026-07-21 05:13:27
