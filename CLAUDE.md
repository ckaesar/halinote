# CLAUDE.md — halinote 知识库规则手册

## 1. 这是什么

这是运行在 Obsidian Vault `halinote` 中的个人知识库。你（AI）是这里的整理者与写作助手。
所有路径以 Vault 根目录为基准；**目录负责表示"在哪里"，frontmatter 负责表示"怎么样"**。

## 2. 目录说明

顶层按生命周期编号，不按主题划分；层级不超过 3 层。类型、标签、状态、项目归属放进 frontmatter，用搜索或 Dataview 查询。

| 目录 | 放什么 | 不放什么 / 规则 |
|---|---|---|
| `00-inbox/` | 唯一允许混乱的入口：网页剪藏、附件、录音转写、临时草稿 | 停留 ≤ 2 周；超期必须处理 |
| `10-work/` | 进行中的工作：会议纪要、日报周报、项目过程文档 | 完成后升级到 20 或降级到 40 |
| `10-work/daily-logs/` | 工作日常，命名 `YYYY-MM-DD 事项.md` | 个人日记放 50-creative |
| `20-knowledge/` | 处理完成、值得长期保留的知识，检索密度最高 | frontmatter 必须完整，笔记间需 wikilink 互联 |
| `20-knowledge/articles/` | 博客、周刊、外部文章与收藏索引 | 原文剪藏先经 00-inbox 再整理 |
| `20-knowledge/references/` | 参考资料、官方文档、教程、专题索引 | 不放项目过程记录 |
| `20-knowledge/reading-notes/` | 读书/长文阅读笔记与摘录 | 摘录必须注明出处链接 |
| `30-assets/` | 图片、录音、图表、HTML 等资产 | 笔记正文不放资产文件 |
| `30-assets/img/` | 所有图片，引用写 `![[文件名]]` | 文件名保持唯一，不按主题再建子目录 |
| `30-assets/meeting/` | 原始 ASR / 录音转写，文件名加 `_原始ASR` | 成品纪要放 10-work |
| `30-assets/diagrams/` | 图表、Canvas 导出 | — |
| `30-assets/html/` | 单文件 HTML 演示 | — |
| `30-assets/templates/` | 笔记模板（日记模板等） | 模板只用于插入，不直接当笔记编辑；不参与知识图谱 |
| `40-archive/` | 过期但仍有参考价值的内容，按 `YYYY/主题` 组织 | **只进不出**；归档前必须已处理完毕，归档不等于删除 |
| `50-creative/` | 个人创作、学习笔记，与工作内容严格分开 | 便于区分内容性质与将来迁移 |
| `50-creative/daily-notes/` | 个人日记、阅读摘录、随想 | 命名 `YYYY-MM-DD.md`；汇总页 `日记汇总.md` |
| `workspace/` | AI 临时草稿、脚本、缓存、垃圾暂存 | 不纳入同步与知识图谱；可乱，但不污染主库 |

- 新内容默认先落到 `00-inbox/`，由 AI 按类型分发。
- 结构逐步形成：同类内容第三次出现时，才建立新的正式目录。
- 内容与资产分开存放，避免笔记删除后资产变成孤儿文件。

## 3. 禁止事项

1. **不直接删除文件**：清理优先归档、移动或标 `Deprecated`；确需删除时走 Obsidian 回收站，便于恢复。原因：三个月前看似无用的结论，可能正是今天某个决策需要的背景。
2. **不修改 `.obsidian/` 配置文件**：Obsidian 运行时会覆盖外部写入。需要改设置时，通过设置界面或 Obsidian API（`app.vault.setConfig`）完成。原因：外部改动会被静默丢弃，造成状态不一致。
3. **不执行 `git reset --hard`**，也不做任何丢弃历史的重写操作。原因：Vault 是长期积累，历史即资产。
4. **不用原始 ASR 直接生成报告**：先清洗术语、分段、提炼，再写结构化纪要。原因：原文噪声大，直接生成会固化错误。
5. **不用文件系统 `mv` / 重命名**：移动与重命名必须通过 Obsidian（CLI 或 `app.fileManager.renameFile`），否则 wikilink 与附件引用会断裂。
6. **不凭猜测写 frontmatter 取值**：字段名统一 camelCase，状态值统一 PascalCase，避免查询时被当作两个值。

## 4. 写作规范

### frontmatter（YAML）

每篇笔记顶部必须包含：

```yaml
---
title: "标题"
created: 2026-11-18 18:00:00
updated: 2026-11-18 18:00:00
type: daily-note
status: Final
tags: [daily-note]
---
```

- `created` / `updated` 必填，格式 `YYYY-MM-DD HH:MM:SS`，精确到秒；大改时刷新 `updated`。
- `type` 取值：`daily-note`、`meeting-note`、`report`、`reference`、`reading-note`、`article`、`moc`、`pattern`。
- `status` 取值：`Draft → Todo → Doing → Done`；定稿用 `Final`；过时但有参考价值用 `Deprecated`。统一 PascalCase。
- 每日笔记额外写 `date: YYYY-MM-DD`。
- 字段名用 camelCase：`sourceUrl`、`notionUrl`，避免下划线与连字符和工具冲突。
- 只定义 AI 与查询真正需要的字段，正文自由书写。

### 命名

- 每日笔记：`YYYY-MM-DD.md`
- 会议纪要：`YYYY-MM-DD 会议主题.md`
- 原始 ASR：`YYYY-MM-DD 会议主题_原始ASR.md`
- 汇总/索引页：`XXX汇总.md`（如 `日记汇总.md`、`博客汇总.md`）

### 链接与标签

- 笔记之间必须用 `[[wikilink]]` 互联，不把裸 URL 当作唯一关联。
- 标签统一写入 frontmatter `tags`，覆盖类型、业务、状态三类；正文可用 `#标签` 补充。
- 新建或大改知识笔记后，在文末补"参考信息"区块，列出出处链接与相关笔记。

## 5. 流程约定

1. **收件箱清理**：每周检查 `00-inbox/`，超过两周的内容必须处理。
2. **笔记流转**：`00-inbox` → 加工 → `10-work` 或 `20-knowledge` → 定稿后过程文档移入 `40-archive`。
3. **知识笔记维护**：`20-knowledge/` 下新建或大改后，AI 自动补 frontmatter 与"参考信息"关联区块。
4. **资产归位**：新图片/附件统一进 `30-assets/` 对应子目录；粘贴附件路径已设为 `30-assets/img`。
5. **日记创建**：使用核心模板 `30-assets/templates/日记模板.md` 新建到 `50-creative/daily-notes/`，命名 `YYYY-MM-DD.md`；当天结束前把 `status` 从 `Draft` 改为 `Done`。
6. **删除**：一律走 Obsidian 回收站，不永久删除。
7. **移动/重命名**：通过 Obsidian CLI（`obsidian vault="halinote" move ...`）或 `app.fileManager.renameFile`，确保链接同步更新。

## 6. Graphify 知识图谱

图谱文件位于 `graphify-out/graph.json`，用于语义检索与笔记关联；它与目录结构互补，不替代目录。

- **建图 / 增量更新**：`graphify extract . --backend claude-cli`
- **重聚类与刷新报告**：`graphify cluster-only . --backend claude-cli`
- **检索**：`graphify query "问题"`、`graphify path "A" "B" --undirected`、`graphify explain "节点"`
- **导航**：`graphify god-nodes` 查看核心节点；`graphify export obsidian --dir 30-assets/diagrams/graph` 可导出画布

使用规则：

1. 新笔记归位或新建知识笔记前，先查图谱找相关笔记与合适目录。
2. 批量导入或大改后执行一次增量更新；未更新前的新笔记不在图中。
3. 图谱结果只作候选，引用内容必须回原文核对，不能直接当作事实。
4. 建图消耗 token，优先增量更新，避免无意义全量重建。
5. `graphify-out/` 是生成物，不手工编辑；`graphify-out/cache/` 与日期备份不纳入版本控制。

## 参考信息

- 规则来源：[Obsidian 知识库目录结构设计](https://vault.xindoo.xyz/s/14qfgKA6SgodQcVRTFfwu0vBvDXjJljG/02-Obsidian%20%E7%9F%A5%E8%AF%86%E5%BA%93%E7%9B%AE%E5%BD%95%E7%BB%93%E6%9E%84%E8%AE%BE%E8%AE%A1)
- 相关笔记：[[Obsidian教程]]
- 结构变更时同步更新本文件；同一规则只在这里写全，其他笔记只引用。
