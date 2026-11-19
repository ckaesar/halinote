---
title: "Home Page"
created: 2026-11-19 11:58:24
updated: 2026-11-19 11:58:24
type: dashboard
status: Final
tags: [dashboard, moc]
---

# 🏠 Home Page

> 知识库总览：结构、活跃度与待办一屏掌握。以下数据由 Dataview 实时计算，随笔记变化自动刷新。

## 核心数据

```dataviewjs
const isExcluded = (path) =>
  path === "homePage.md" ||
  path === "CLAUDE.md" ||
  path.startsWith("workspace/") ||
  path.startsWith("graphify-out/") ||
  path.startsWith("30-assets/templates/");

const files = app.vault.getMarkdownFiles().filter((f) => !isExcluded(f.path));
const paths = new Set(files.map((f) => f.path));
const pages = dv.pages().where((p) => paths.has(p.file.path));

const daily = files.filter((f) => /^50-creative\/daily-notes\/\d{4}-\d{2}-\d{2}\.md$/.test(f.path)).length;
const knowledge = files.filter((f) => f.path.startsWith("20-knowledge/")).length;
const work = files.filter((f) => f.path.startsWith("10-work/")).length;
const assets = app.vault.getFiles().filter((f) => ["png", "jpg", "jpeg", "gif", "webp", "svg"].includes(f.extension)).length;

let openTasks = 0;
let doneTasks = 0;
for (const p of pages) {
  for (const t of p.file.tasks ?? []) {
    if (t.completed) doneTasks++;
    else openTasks++;
  }
}

const tagCount = new Map();
for (const p of pages) {
  for (const t of p.file.tags ?? []) {
    tagCount.set(t, (tagCount.get(t) ?? 0) + 1);
  }
}
const topTags = [...tagCount.entries()].sort((a, b) => b[1] - a[1]).slice(0, 8);

let graph = null;
try {
  graph = JSON.parse(await app.vault.adapter.read("graphify-out/graph.json"));
} catch (e) {
  graph = null;
}
const nodes = graph?.nodes?.length ?? 0;
const edges = graph?.links?.length ?? 0;
const communities = graph
  ? new Set(graph.nodes.map((n) => n.community).filter((c) => c !== undefined && c !== null)).size
  : 0;

const card = (label, value, sub) => `
  <div style="border:1px solid var(--background-modifier-border);border-radius:10px;padding:12px 14px;background:var(--background-secondary)">
    <div style="font-size:12px;color:var(--text-muted);margin-bottom:6px">${label}</div>
    <div style="font-size:26px;font-weight:700;line-height:1.1;color:var(--text-normal)">${value}</div>
    <div style="font-size:11px;color:var(--text-faint);margin-top:6px">${sub}</div>
  </div>`;

dv.container.innerHTML = `
  <div style="display:grid;grid-template-columns:repeat(auto-fit,minmax(140px,1fr));gap:10px;margin:8px 0 4px">
    ${card("笔记总数", files.length, "Markdown 笔记")}
    ${card("日记", daily, "daily-notes")}
    ${card("知识笔记", knowledge, "20-knowledge")}
    ${card("工作文档", work, "10-work")}
    ${card("图片资产", assets, "30-assets")}
    ${card("未完成任务", openTasks, `已完成 ${doneTasks}`)}
    ${card("图谱节点", nodes, `${edges} 条边`)}
    ${card("图谱社区", communities, "graphify")}
  </div>
  <div style="margin-top:10px;font-size:12px;color:var(--text-muted)">
    高频标签：${topTags.map(([t, c]) => `<code>${t}</code> ×${c}`).join("　") || "暂无"}
  </div>`;
```

## 快捷入口

- [[10-work/任务看板|📋 任务看板]]
- [[50-creative/daily-notes/日记汇总|📔 日记汇总]]
- [[CLAUDE|📐 知识库规则]]
- [[Obsidian教程|📖 Obsidian 教程]]
- [[graphify-out/GRAPH_REPORT|🕸 图谱报告]]

## 分区概览

```dataview
TABLE length(rows) AS "数量", dateformat(max(rows.file.mtime), "yyyy-MM-dd") AS "最近更新"
FROM ""
WHERE file.name != "homePage" AND file.name != "CLAUDE"
  AND !contains(file.path, "workspace/")
  AND !contains(file.path, "graphify-out/")
  AND !contains(file.path, "30-assets/")
GROUP BY file.folder
SORT length(rows) DESC
```

## 类型分布

```dataview
TABLE length(rows) AS "数量"
FROM ""
WHERE file.name != "homePage" AND file.name != "CLAUDE"
  AND !contains(file.path, "workspace/")
  AND !contains(file.path, "graphify-out/")
  AND !contains(file.path, "30-assets/")
GROUP BY type
SORT length(rows) DESC
```

## 最近更新

```dataview
TABLE type AS "类型", status AS "状态", dateformat(file.mtime, "MM-dd HH:mm") AS "更新"
FROM ""
WHERE file.name != "homePage" AND file.name != "CLAUDE"
  AND !contains(file.path, "workspace/")
  AND !contains(file.path, "graphify-out/")
  AND !contains(file.path, "30-assets/")
SORT file.mtime DESC
LIMIT 10
```

## 未完成任务

```dataview
TASK
FROM ""
WHERE !completed AND file.name != "homePage" AND file.name != "CLAUDE"
```

## 最近日记

```dataview
LIST
FROM "50-creative/daily-notes"
WHERE type = "daily-note"
SORT file.name DESC
LIMIT 7
```

## 标签分布

```dataview
TABLE length(rows) AS "笔记数"
FROM ""
WHERE file.name != "homePage" AND file.name != "CLAUDE"
  AND !contains(file.path, "workspace/")
  AND !contains(file.path, "graphify-out/")
  AND !contains(file.path, "30-assets/")
FLATTEN file.tags AS tag
GROUP BY tag
SORT length(rows) DESC
LIMIT 12
```

## 知识图谱

```dataviewjs
const graph = JSON.parse(await app.vault.adapter.read("graphify-out/graph.json"));
const labels = new Map(graph.nodes.map((n) => [n.id, n.label]));
const degree = new Map();
for (const e of graph.links ?? []) {
  degree.set(e.source, (degree.get(e.source) ?? 0) + 1);
  degree.set(e.target, (degree.get(e.target) ?? 0) + 1);
}
const top = [...degree.entries()]
  .sort((a, b) => b[1] - a[1])
  .slice(0, 8)
  .map(([id, d]) => `<li style="margin:4px 0"><span style="color:var(--text-normal)">${labels.get(id) ?? id}</span> <span style="color:var(--text-faint)">· ${d} 条关联</span></li>`)
  .join("");

dv.container.innerHTML = `
  <div style="border:1px solid var(--background-modifier-border);border-radius:10px;padding:12px 16px;background:var(--background-secondary)">
    <div style="font-size:13px;color:var(--text-muted);margin-bottom:8px">关联最多的核心节点</div>
    <ul style="margin:0 0 0 18px;padding:0">${top || "<li style=\"color:var(--text-faint)\">图谱尚未生成</li>"}</ul>
    <div style="margin-top:10px;font-size:12px;color:var(--text-faint)">共 ${graph.nodes.length} 个节点 / ${graph.links.length} 条边</div>
  </div>`;
```

## 参考信息

- 查询依赖：[Dataview](https://blacksmithgu.github.io/obsidian-dataview/) 与 [Tasks](https://publish.obsidian.md/tasks/)
- 图谱来源：`graphify-out/graph.json`，更新方式见 [[CLAUDE#6. Graphify 知识图谱|CLAUDE]]
- 相关页面：[[10-work/任务看板|任务看板]]、[[50-creative/daily-notes/日记汇总|日记汇总]]
