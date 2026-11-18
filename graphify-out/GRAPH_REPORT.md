# Graph Report - halinote  (2026-11-18)

## Corpus Check
- cluster-only mode — file stats not available

## Summary
- 91 nodes · 95 edges · 17 communities (9 shown, 8 thin omitted)
- Extraction: 92% EXTRACTED · 8% INFERRED · 0% AMBIGUOUS · INFERRED: 8 edges (avg confidence: 0.74)
- Token cost: 0 input · 0 output

## Graph Freshness
- Built from commit: `ce4d538c`
- Run `git rev-parse HEAD` and compare to check if the graph is stale.
- Run `graphify update .` after code changes (no API cost).

## Community Hubs (Navigation)
- 日常日记记录
- AI 工程实践
- Anthropic 学习资源
- 架构与工程思考
- 摘录与思辨
- Agent 循环设计
- 健康与注意力
- Obsidian 知识库搭建
- 博客与财务记录
- 上下文与网络代理
- 教材阅读方法
- 社会经济观察
- 处世态度
- 中庸之道思考
- AI 机制科普
- Simon Willison 博客
- 阮一峰科技周刊

## God Nodes (most connected - your core abstractions)
1. `日记汇总` - 49 edges
2. `Harness 工程（驾驭工程）` - 6 edges
3. `专题学习` - 5 edges
4. `上下文治理：内存与紧凑预算` - 4 edges
5. `2026-04-13 日记` - 4 edges
6. `AI 原生工程师` - 3 edges
7. `《ClaudeCode代码设计指南》` - 3 edges
8. `2026-06-16 日记` - 3 edges
9. `2026-06-23 日记` - 3 edges
10. `AI日常使用记录` - 3 edges

## Surprising Connections (you probably didn't know these)
- `反馈闭环：用结果修正判断` --semantically_similar_to--> `Harness 工程（驾驭工程）`  [INFERRED] [semantically similar]
  50-creative/daily-notes/2026-04-10.md → 20-knowledge/reading-notes/《ClaudeCode代码设计指南》.md
- `AI Friendly 后端架构` --conceptually_related_to--> `Harness 工程（驾驭工程）`  [INFERRED]
  50-creative/daily-notes/2026-06-16.md → 20-knowledge/reading-notes/《ClaudeCode代码设计指南》.md
- `能力沉淀：脚本 → Skill → Agent` --conceptually_related_to--> `AI 原生工程师`  [INFERRED]
  20-knowledge/references/AI日常使用记录.md → 50-creative/daily-notes/2026-06-23.md
- `2026-04-29 日记` --references--> `Harness 工程（驾驭工程）`  [EXTRACTED]
  50-creative/daily-notes/2026-04-29.md → 20-knowledge/reading-notes/《ClaudeCode代码设计指南》.md
- `AI 原生工程师` --conceptually_related_to--> `上下文治理：内存与紧凑预算`  [INFERRED]
  50-creative/daily-notes/2026-06-23.md → 20-knowledge/reading-notes/《ClaudeCode代码设计指南》.md

## Hyperedges (group relationships)
- **阮一峰科技爱好者周刊阅读集群** — 50_creative_dailynotes_20260410_阮一峰的博客, 50_creative_dailynotes_20260410, 50_creative_dailynotes_20260417, 50_creative_dailynotes_20260424, 50_creative_dailynotes_20260518, 50_creative_dailynotes_20260522, 50_creative_dailynotes_20260605, 50_creative_dailynotes_20260618, 50_creative_dailynotes_20260703, 50_creative_dailynotes_20260710, 50_creative_dailynotes_20260810, 50_creative_dailynotes_20260814, 50_creative_dailynotes_20260821, 50_creative_dailynotes_20260828, 50_creative_dailynotes_20260904, 50_creative_dailynotes_20260911, 50_creative_dailynotes_20260920, 50_creative_dailynotes_20261016, 50_creative_dailynotes_20261023, 50_creative_dailynotes_20261030, 50_creative_dailynotes_20261109, 50_creative_dailynotes_20261113 [EXTRACTED 1.00]
- **西蒙·威利森的博客阅读集群** — 50_creative_dailynotes_20260410_西蒙威利森的博客, 50_creative_dailynotes_20260410, 50_creative_dailynotes_20260413, 50_creative_dailynotes_20260416, 50_creative_dailynotes_20260424, 50_creative_dailynotes_20260427, 50_creative_dailynotes_20260428, 50_creative_dailynotes_20260518, 50_creative_dailynotes_20260519, 50_creative_dailynotes_20260525, 50_creative_dailynotes_20260601, 50_creative_dailynotes_20260609, 50_creative_dailynotes_20260611, 50_creative_dailynotes_20260615, 50_creative_dailynotes_20260616, 50_creative_dailynotes_20260622, 50_creative_dailynotes_20260703, 50_creative_dailynotes_20260706, 50_creative_dailynotes_20260707, 50_creative_dailynotes_20260713, 50_creative_dailynotes_20261021 [EXTRACTED 1.00]
- **AI 工程化实践：Harness、上下文、验证与 Loop** — 20_knowledge_readingnotes_claudecode代码设计指南_harness_engineering, 20_knowledge_readingnotes_claudecode代码设计指南_上下文治理, 50_creative_dailynotes_20260616_ai_friendly_backend, 50_creative_dailynotes_20260624_loop_engineering, 50_creative_dailynotes_20260623_ai_native_engineer, 50_creative_dailynotes_20261021_ai_code_review [INFERRED 0.85]

## Communities (17 total, 8 thin omitted)

### Community 0 - "日常日记记录"
Cohesion: 0.06
Nodes (33): 2026-04-14 日记, 2026-04-15 日记, 2026-04-17 日记, 2026-04-24 日记, 2026-04-27 日记, 2026-04-30 日记, 2026-05-09 日记, 2026-05-13 日记 (+25 more)

### Community 1 - "AI 工程实践"
Cohesion: 0.24
Nodes (11): 《ClaudeCode代码设计指南》, Harness 工程（驾驭工程）, read, 上下文治理：内存与紧凑预算, 2026-04-10 日记, 反馈闭环：用结果修正判断, 2026-04-29 日记, 2026-06-16 日记 (+3 more)

### Community 2 - "Anthropic 学习资源"
Cohesion: 0.25
Nodes (8): AI日常使用记录, Agent 模型调用失败的规避方式, 能力沉淀：脚本 → Skill → Agent, Anthropic API文档, Anthropic Courses, Anthropic learn, Anthropic官方文档内容, 专题学习

### Community 3 - "架构与工程思考"
Cohesion: 0.33
Nodes (6): 2026-04-13 日记, 多区域双活架构（Netflix）, NoSQL 适用场景, 品味 + 工程思维, 2026-10-23 日记, 编程的未来：代码审查与单元测试消失

### Community 4 - "摘录与思辨"
Cohesion: 0.40
Nodes (5): 摘录, 持续积累与避免灾难性决策, 2026-04-28 日记, 循环：泡沫、替罪羊与恐慌, 软件大脑的局限

### Community 5 - "Agent 循环设计"
Cohesion: 0.50
Nodes (4): 2026-06-24 日记, Loop 的五个零件与完成条件, 2026-10-21 日记, Review 上浮到规格、下沉到产物

### Community 6 - "健康与注意力"
Cohesion: 0.50
Nodes (4): 2026-07-13 日记, 睡眠与社会关系对健康的影响, 2026-08-10 日记, 注意力经济与专注力衰减

### Community 7 - "Obsidian 知识库搭建"
Cohesion: 0.67
Nodes (3): Lofi'Log 低保真日志, 现金流管理的最终目标, 博客汇总

### Community 8 - "博客与财务记录"
Cohesion: 0.67
Nodes (3): 2026-05-25 日记, Claude Code 长会话上下文管理, 正向代理 / 反向代理 / API 网关

## Knowledge Gaps
- **55 isolated node(s):** `2026-04-14 日记`, `2026-04-15 日记`, `2026-04-17 日记`, `2026-04-24 日记`, `2026-04-27 日记` (+50 more)
  These have ≤1 connection - possible missing edges or undocumented components. (Counts symbols only; 55 node(s) total have ≤1 connection when file, concept and rationale nodes are included.)
- **8 thin communities (<3 nodes) omitted from report** — run `graphify query` to explore isolated nodes.

## Suggested Questions
_Questions this graph is uniquely positioned to answer:_

- **Why does `日记汇总` connect `日常日记记录` to `AI 工程实践`, `架构与工程思考`, `摘录与思辨`, `Agent 循环设计`, `健康与注意力`, `博客与财务记录`, `上下文与网络代理`, `教材阅读方法`, `社会经济观察`, `处世态度`, `中庸之道思考`?**
  _High betweenness centrality (0.803) - this node is a cross-community bridge._
- **Are the 2 inferred relationships involving `Harness 工程（驾驭工程）` (e.g. with `反馈闭环：用结果修正判断` and `AI Friendly 后端架构`) actually correct?**
  _`Harness 工程（驾驭工程）` has 2 INFERRED edges - model-reasoned connections that need verification._
- **What connects `2026-04-14 日记`, `2026-04-15 日记`, `2026-04-17 日记` to the rest of the system?**
  _55 weakly-connected nodes found - possible documentation gaps or missing edges._
- **Should `日常日记记录` be split into smaller, more focused modules?**
  _Cohesion score 0.06060606060606061 - nodes in this community are weakly interconnected._
- **Why does `2026-06-23 日记` connect `AI 工程实践` to `日常日记记录`?**
  _High betweenness centrality (0.178) - this node is a cross-community bridge._
- **Why does `AI 原生工程师` connect `AI 工程实践` to `Anthropic 学习资源`?**
  _High betweenness centrality (0.150) - this node is a cross-community bridge._