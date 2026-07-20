# Olive Resource Index

Olive Resource Index 是一个面向开发者与运维工程师的技术资源外链汇总系统，专注于从分散的代码仓库、技术博客、官方文档中提取高质量的参考链接，并以可检索、可分类、可版本化的方式进行统一管理。该项目不直接存储资源内容，而是通过 Markdown 索引文件维护外部 URL 的元数据与分类标签，适用于需要高频查阅外部技术资料、维护私有技术书签库、或构建团队知识导航页面的场景。目标用户包括个人开发者、技术文档撰写者、运维工程师以及技术团队的知识管理者。

## 功能概览

- 外链分类索引：按技术领域、资源类型、适用版本等多个维度对 URL 进行分组与标注，支持快速筛选。

- 元数据扩展机制：每个外链可附带作者、发布日期、归档状态、备用链接等自定义字段，便于长期维护。

- 批量校验与死链检测：内置基础链接可达性检查脚本，可定期输出失效资源报告。

- 标签化检索：支持通过标签组合快速定位特定技术栈或主题的相关资源。

- 版本快照支持：每次索引更新均可提交为 Git 变更，便于回溯历史资源状态。

- 纯静态部署：索引文件完全基于 Markdown，可托管于任意 Git 平台或静态站点服务。

## 应用场景

作为技术文档的外部参考附录：在编写系统设计文档或 API 说明时，可将 Olive Resource Index 中的相关链接作为补充材料引用，避免在文档正文中嵌入大量外链。

作为团队共享的技术书签库：团队成员可统一通过索引文件查阅常用工具、依赖库、规范文档的入口，减少重复查找时间。

作为个人知识管理体系的补充：开发者可将个人收藏的技术文章、教程、视频链接按照本项目的索引规范整理，形成长期可维护的知识导航。

作为 CI/CD 流程中的资源检查环节：在发布流程中自动运行死链检测，确保对外部资源的引用始终有效。

## 快速开始

```bash
# 克隆项目仓库
git clone https://github.com/zerxonhy/olive.git
cd olive

# 安装基础依赖（Python 3.8+ 环境）
python -m venv venv
source venv/bin/activate  # Windows 使用 venv\Scripts\activate
pip install requests pyyaml

# 运行本地索引校验与死链检查
python scripts/check_links.py --index ./README.md --output report.txt
```

## 安装要求

| 依赖项 | 必需版本 | 说明 |
|--------|----------|------|
| Python | 3.8 及以上 | 用于运行校验与检索引擎脚本 |
| pip | 20.0 及以上 | 管理 Python 依赖包 |
| Git | 2.20 及以上 | 克隆仓库与版本管理 |
| requests | 2.25.0 及以上 | 用于 HTTP 链接状态检测 |
| pyyaml | 5.4.0 及以上 | 解析可选的 YAML 元数据配置文件 |
| 终端环境 | Bash / Zsh / PowerShell | 执行快速启动命令 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|------|------|------------|
| 入门 | docs/quickstart.md | 如何在一分钟内完成索引初始化并添加第一条外链？ |
| 使用 | docs/usage.md | 如何添加新资源、更新元数据、执行死链检测？ |
| 维护 | docs/maintenance.md | 如何定期清理失效链接、合并重复条目、生成快照？ |
| 扩展 | docs/extension.md | 如何自定义标签体系、添加额外的元数据字段、集成第三方工具？ |

## 资源列表

- https://github.com/zerxonhy/olive/blob/main/mirrortimber.md
- https://github.com/zerxonhy/olive/blob/main/nebulaviolet.md
- https://github.com/zerxonhy/olive/blob/main/oceanolive.md
- https://github.com/zerxonhy/olive/blob/main/oceanpearl.md
- https://github.com/zerxonhy/olive/blob/main/oceanzephyr.md
- https://github.com/zerxonhy/olive/blob/main/olivemeadow.md

## 项目结构

```
olive/
├── README.md                        # 项目总览与快速入口
├── LICENSE                          # MIT 许可证文件
├── requirements.txt                 # Python 运行时依赖列表
├── config/
│   ├── categories.yaml              # 资源分类体系定义（技术栈/领域/标签）
│   └── aliases.yaml                 # 常用资源简称与缩写映射
├── docs/
│   ├── quickstart.md                # 零基础快速上手指南
│   ├── usage.md                     # 日常使用与索引操作详解
│   ├── maintenance.md               # 定期维护与失效处理策略
│   └── extension.md                 # 自定义扩展与集成开发说明
├── scripts/
│   ├── check_links.py               # 外链可达性批量检查主脚本
│   ├── update_metadata.py           # 批量更新元数据字段的辅助工具
│   └── gen_index.sh                 # 从原始数据生成 Markdown 索引表的 Shell 脚本
├── tests/
│   ├── test_checker.py              # 链接检查模块的单元测试
│   └── fixtures/                    # 测试用模拟资源文件
│       └── sample_links.md
└── .github/
    └── workflows/
        └── link_check.yml           # GitHub Actions 定时死链检测工作流
```

## 贡献指南

1. 复刻本仓库至个人账户，并在本地创建新的功能分支，分支命名建议使用 `feature/描述` 或 `fix/描述` 格式。

2. 在 `config/categories.yaml` 中确认新增资源所属分类是否存在，若不存在请先更新分类定义，再于对应索引文件中添加外链条目，并附带必要的元数据字段（如 `title`、`description`、`tags`）。

3. 运行 `scripts/check_links.py` 对新增或修改的外链进行可达性验证，确保所有链接均返回有效的 HTTP 2xx 或 3xx 状态码。

4. 提交变更并推送到远程仓库，随后通过 GitHub 界面发起 Pull Request，描述中需说明本次新增或修改的资源列表及其用途。

5. 等待维护者审阅，若有反馈请及时在 PR 讨论中回应，合并后即视为贡献生效。

## 常见问题

问：如果某个外链失效了，我应该直接删除该条目吗？

答：不建议直接删除。请在元数据中将 `status` 字段标记为 `broken`，并记录失效日期。若后续找到可用的替代链接，可将 `status` 改为 `redirected` 并更新 `url` 字段。这有助于保留历史引用信息，避免文档中出现断裂的参考记录。

问：如何批量导入我已有的书签文件？

答：项目提供 `scripts/import_bookmarks.py` 辅助脚本（位于 `scripts/` 目录下），支持从 Chrome 导出的 HTML 书签文件或 Firefox 的 JSON 备份中提取 URL 与标题，并按现有分类体系自动匹配写入索引。具体用法请参考 `docs/extension.md` 中的导入章节。

问：我可以在企业内部私有化部署这个索引吗？

答：完全可以。本项目采用 MIT 许可证发布，允许自由使用、修改和再发布。你只需将仓库克隆至内网 Git 服务，并调整 `config/categories.yaml` 中的分类定义以匹配内部技术栈即可。所有脚本均不依赖外部网络（除死链检测自身外），可完全离线运行。

## 许可证

MIT

> 外链数量: 6 | 生成时间: 2026-07-21 05:13:41
