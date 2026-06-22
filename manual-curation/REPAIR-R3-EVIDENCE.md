# REPAIR-R3-EVIDENCE

日期：2026-06-22  
步骤：`fix-evidence-six`  
范围：第三轮定向修复 `manual-curation/QA-AFTER-REPAIR-R2.md` 中 6 个 HIGH/P1 未注册 evidence/source 引用。

## 修复目标

R2 QA 报告列出的 6 个残留 HIGH/P1 均为三组世界 `relationship-graph.json` 中 `edges.3/4.evidence.0 = "characters-index.relationships"`：

- `worlds/marvel-cinematic-universe/curated/relationship-graph.json`
- `worlds/naruto/curated/relationship-graph.json`
- `worlds/type-moon-nasuverse/curated/relationship-graph.json`

## 修复策略

采用策略 1：将字符串 evidence 改为结构化内部依据对象，而不是在 `source-registry.json` 注册伪外部 source id。

选择理由：这些关系边的 `notes` 已说明为 `Minimal relation from curated relationship string.`，语义上是从同世界 `characters-index.relationships` 字段整理出的内部 curated 依据，不是外部 source registry id。结构化对象能保留可追踪来源字段，同时避免严格 source 扫描把它当成未注册 source id。

替换后的 evidence 形式：

```json
{
  "kind": "internal-curated-field",
  "ref": "characters-index.relationships",
  "note": "Derived from curated character relationship field, not external source id."
}
```

## 修改明细

### marvel-cinematic-universe

文件：`worlds/marvel-cinematic-universe/curated/relationship-graph.json`

- `edges.3` / `rel-tony-peter`：`evidence[0]` 从字符串改为 `internal-curated-field` 对象。
- `edges.4` / `rel-thor-avengers`：`evidence[0]` 从字符串改为 `internal-curated-field` 对象。

### naruto

文件：`worlds/naruto/curated/relationship-graph.json`

- `edges.3` / `rel-itachi-sasuke`：`evidence[0]` 从字符串改为 `internal-curated-field` 对象。
- `edges.4` / `rel-pain-naruto`：`evidence[0]` 从字符串改为 `internal-curated-field` 对象。

### type-moon-nasuverse

文件：`worlds/type-moon-nasuverse/curated/relationship-graph.json`

- `edges.3` / `rel-sakura-shirou`：`evidence[0]` 从字符串改为 `internal-curated-field` 对象。
- `edges.4` / `rel-ritsuka-mash`：`evidence[0]` 从字符串改为 `internal-curated-field` 对象。

## 未修改项

- 未修改任何关系边的 `from`、`to`、`type`、`directional`、`visibility`、`strength`、`facets`、`publicDescription`、`gmTruth` 或 `notes`。
- 未修改三个世界的 `source-registry.json`，因为本轮选择将内部字段依据显式标记为非 source id。
- 未处理 R2 QA 中列出的 MED/LOW/INFO 覆盖与规范化问题。
- 未处理 R2 QA 中“非阻断扩展类型风险”涉及的其他世界字段，因为不在本步骤 mutation scope 内。
- 未处理 35 个空 `conflictLog` 世界的全局语义状态，因为其中多数不在本步骤 mutation scope 内；本轮仅记录该风险仍需后续单独修复。

## 验证

执行了聚焦 Node 校验：

```bash
node - <<'NODE'
const fs = require('fs');
const worlds = ['marvel-cinematic-universe','naruto','type-moon-nasuverse'];
for (const world of worlds) {
  const path = `worlds/${world}/curated/relationship-graph.json`;
  const data = JSON.parse(fs.readFileSync(path, 'utf8'));
  const hits = [];
  data.edges.forEach((edge, edgeIndex) => {
    (edge.evidence || []).forEach((item, evidenceIndex) => {
      if (item === 'characters-index.relationships') hits.push(`edges.${edgeIndex}.evidence.${evidenceIndex}`);
    });
  });
  console.log(`${world}: parse ok; remaining string characters-index.relationships = ${hits.length}${hits.length ? ' ' + hits.join(',') : ''}`);
}
NODE
```

结果：

```text
marvel-cinematic-universe: parse ok; remaining string characters-index.relationships = 0
naruto: parse ok; remaining string characters-index.relationships = 0
type-moon-nasuverse: parse ok; remaining string characters-index.relationships = 0
```

## 复核结论

- R2 报告中的 6 个 HIGH/P1 未注册 evidence/source 引用已按内部 curated 字段依据语义修复。
- 三个目标 `relationship-graph.json` 均可 JSON parse。
- 三个目标文件中不再存在字符串形式的 `evidence[] = "characters-index.relationships"`。
- 本轮未运行全库 QA，因此只能确认目标 6 项清零；是否仍有其他 P0/P1/HIGH 需以后续全量 QA 报告为准。
