# REPAIR-STRUCTURE

检查/修复日期：2026-06-22  
范围：`worlds/*/curated/*.json`  
任务：修复 `manual-curation/QA-JSON-SCHEMA.md` 中 P0/P1 结构问题；不改写世界叙事正文。

## 修改边界

本轮仅做结构性、机械性修复：

- 统一顶层 `schema` 名称。
- 补运行时必需元字段和空骨架。
- 修正明显顶层类型错误。
- 补图谱断链的占位节点。
- 补 source registry 中缺失的引用占位。
- 对空 `conflictLog` 加 registry 说明。
- 未重写 `summary`、人物正文、设定正文、关系正文。

注意：由于需要统一 JSON 结构，相关 JSON 文件被格式化为标准 2 空格缩进；正文字符串内容未按叙事意图改写。

## 统一 schema

所有 `worlds/*/curated/*.json` 已统一为模板期望值：

| 文件 | schema |
|---|---|
| `world.json` | `rp-world-v1` |
| `source-registry.json` | `rp-source-registry-v1` |
| `characters-index.json` | `rp-characters-index-v1` |
| `knowledge-graph.json` | `rp-knowledge-graph-v1` |
| `relationship-graph.json` | `rp-relationship-graph-v1` |

## 补字段规则

### `world.json`

缺失时补入以下骨架：

- `worldId`：优先沿用既有 `worldId`，否则由 `worldSlug` 或目录名派生。
- `worldName`：优先由 `displayName` / `name` / `title` 派生，否则由目录名派生。
- `aliases`: `[]`
- `genre`: 若已有 `tone` 且为数组，则复用该数组；否则 `[]`
- `summary`: 仅缺失时补空字符串 `""`，不从其他正文改写生成。
- `sandboxPrinciple`: `{}`
- `hasFixedFate`: `false`
- `foreignPowerSuppressionDefault`: `{}`
- `notes`: `[]`；若原值为字符串，则保留原字符串并包入数组。
- `powerSystems`: `[]`
- `factions`: `[]`
- `energyEnvironment`: `{}`
- `worldRules`: `{}`；若原值为数组，则保留原数组并移动为 `{ "rules": [...] }`。
- `locations`: `[]`
- `publicEvents`: `[]`
- `hiddenEvents`: `[]`

特别处理：

- `worlds/date-a-live/curated/world.json`
  - `notes` 从字符串改为数组，原文本保留为数组元素。
  - `worldRules` 从数组改为对象，原规则数组保留在 `rules` 字段。
- `worlds/toriko/curated/world.json`
  - `worldRules` 从数组改为对象，原规则数组保留在 `rules` 字段。
- `worlds/acg-character-database/curated/world.json`
  - 保留既有 `isSingleFictionalWorld: false` 等特殊世界信息。
  - 增加 `specialWorldGate` 骨架，标明它是跨作品角色数据库而非单一世界。

### `source-registry.json`

缺失时补入：

- `campaignId`：由世界 ID/目录名派生。
- `sources`: `[]`
- `conflictLog`: 若已有 `conflicts` 数组则复用；否则 `[]`。
- 空 `conflictLog` 的 registry 增加 `registryNotes`：说明当前未登记冲突，仍需后续人工复核是否确无冲突。

同时注册缺失 source 引用：

- 对 `world.json` 中 `sourceRefs` / `sourceBasis` 指向但 registry 未登记的项，增加 `unregistered-placeholder` source。
- 对 curated 文件中递归发现的 `sourceRefs` / `sourceBasis` 粒度引用，若 registry 未登记，增加 `granular-reference-placeholder` source。
- 本轮新增的 source 条目只作为结构占位，不补写来源正文。

### `characters-index.json`

缺失时补入：

- `worldId`
- `characters`: `[]`
- `indices` 骨架：
  - `byId`: `{}`
  - `byName`: `{}`
  - `byAffiliation`: `{}`
  - `byTag`: `{}`

### `knowledge-graph.json`

缺失时补入：

- `campaignId`
- `nodes`: `[]`
- `edges`: `[]`
- `indices` 骨架：
  - `byType`: `{}`
  - `byTag`: `{}`
  - `byVisibility`: `{}`
  - `activeClues`: `[]`
  - `lockedSecrets`: `[]`

并修复现有边引用的缺失节点：

- 若 `edges[].from` / `edges[].to` 指向不存在的 node id，则新增 `type: "referenced-placeholder"` 的占位节点。
- 占位节点只包含 id/label/type/notes，不推断设定内容。

### `relationship-graph.json`

缺失时补入：

- `campaignId`
- `nodes`: `[]`
- `edges`: 若已有 `relationships` 数组则复用为 `edges`；否则 `[]`。
- `views` 骨架：
  - `playerVisibleNodeIds`: `[]`
  - `gmHighlightedNodeIds`: `[]`
  - `activeSceneNodeIds`: `[]`

并修复现有边引用的缺失节点：

- 若 `edges[].from` / `edges[].to` 指向不存在的 node id，则新增 `type: "referenced-placeholder"` 的占位节点。
- 原 `relationships` 字段未删除；如存在，只是补出模板期望的 `edges` 字段以满足运行时读取。

## 修改规模

- `worlds/*/curated/*.json` 总数：315。
- 第一轮结构补齐触及：250 个 JSON 文件。
- 图谱断链占位节点补齐涉及：39 个图谱文件。
  - `knowledge-graph.json`：9 个文件补占位节点。
  - `relationship-graph.json`：30 个文件补占位节点。
- source registry 粒度引用占位补齐涉及：4 个 registry。
  - `claymore`: 3 项。
  - `madan-no-ou`: 36 项。
  - `testament-sister-new-devil`: 28 项。
  - `toaru`: 50 项。

## 复核结果

已执行本地机械 QA，检查项包括：

1. 315 个 curated JSON 均可解析。
2. 5 类文件 schema 均匹配期望值。
3. `QA-JSON-SCHEMA.md` 所列顶层必备字段均存在。
4. `date-a-live` / `toriko` 的 `worldRules` 类型为对象。
5. `date-a-live` 的 `notes` 类型为数组。
6. curated 文件递归发现的 `sourceRefs` / `sourceBasis` 均已在同世界 `source-registry.json` 注册或以占位条目登记。
7. `knowledge-graph.json` 与 `relationship-graph.json` 的现有 `edges` 不再引用缺失节点。

复核命令输出摘要：

```text
json_files 315
problems 0
```

## 残留与风险

本轮目标是 P0/P1 结构修复；仍需后续人工处理的非 P0/P1 项：

- 大量新增字段为空骨架，例如 `sandboxPrinciple`、`energyEnvironment`、`indices`、`views`，仅保证运行时结构存在，不代表内容已完成。
- `referenced-placeholder` 图谱节点需要人工补 label/type/说明，当前只是消除断链。
- `unregistered-placeholder` 与 `granular-reference-placeholder` source 条目需要人工合并、补证据路径或提升可靠性说明。
- 空 `conflictLog` 仅登记“当前未登记冲突”的结构说明，未证明确无冲突。
- 若下游要求更严格字段类型/枚举（例如 `foreignPowerSuppressionDefault` 的具体 schema），还需要按真实模板进一步细化。

## 当前结论

按本轮机械 QA 口径，`manual-curation/QA-JSON-SCHEMA.md` 中列出的 P0/P1 结构问题已修复到未发现剩余问题。后续建议进入人工内容复核与占位字段补全阶段。
