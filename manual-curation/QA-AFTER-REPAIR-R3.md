# QA-AFTER-REPAIR-R3

检查日期：2026-06-22  
步骤：`qa-r3`  
范围：`worlds/*/curated/` 下 63 个世界、315 个 curated JSON。  
执行方式：只读 bash/Node 扫描；未修改 `worlds/*/curated`。唯一写入文件为本报告 `manual-curation/QA-AFTER-REPAIR-R3.md`。

## 结论摘要

- **P0：0**。未发现 JSON parse 失败、5 文件缺失、未识别 JSON、schema mismatch、原始 QA 顶层必备字段缺失、图谱 edge-node 断链、字符串节点或重复 node id。
- **P1：0**。R2 后剩余 6 个 HIGH/P1 未注册 evidence/source 引用已清零；严格类型不匹配也仍为 0。
- **HIGH：0**。未发现图谱断链 HIGH，也未发现未注册 source/evidence HIGH。
- **扩展类型风险：0**。R2 中 6 项 `notCompleteCanonRoster` / `notes` 扩展类型风险已清零。
- **空 sources：0**。所有 `source-registry.sources` 均非空。
- **空 conflictLog：35，但语义状态齐备**。35 个空 `conflictLog` registry 均具备机器可读 `conflictReviewStatus` 与 `registryNotes`，未再计为阻断问题。
- **MED/LOW/INFO：MED 332 / LOW 870 / INFO 349**。这些为规范化与覆盖启发式残留，不是 P0/P1/HIGH 阻断。
- **是否还能判定有问题：是，但不是 P0/P1/HIGH**。结构、注册来源与扩展类型已达本轮目标；仍存在大量 MED/LOW/INFO 质量项与 19 个 placeholder 信号，因此不能判定“完全没问题”。

## 扫描项目与结果

| 检查项 | 结果 |
|---|---:|
| 世界目录数 | 63 |
| JSON 文件总数 | 315 |
| 每世界 5 类 JSON 齐备 | 是 |
| JSON parse 失败 | 0 |
| 未识别 JSON 文件名 | 0 |
| schema mismatch | 0 |
| 原始 QA 顶层必备字段缺失 | 0 |
| 严格类型不匹配 | 0 |
| 扩展运行时字段类型风险 | 0 |
| knowledge/relationship edge-node 断链 | 0 |
| graph string nodes | 0 |
| duplicate graph node ids | 0 |
| source/evidence 未注册 | 0 |
| 空 `source-registry.sources` | 0 |
| 空 `source-registry.conflictLog` | 35 |
| 空 `conflictLog` 缺语义状态 | 0 |
| placeholder 信号 | 19 个世界含 `referenced-placeholder` |

## P0 复核

本轮未发现 P0：

- `worlds/*/curated/*.json` 共 315 个文件均可 `JSON.parse`。
- 63 个世界均具备：`world.json`、`source-registry.json`、`characters-index.json`、`knowledge-graph.json`、`relationship-graph.json`。
- 5 类文件 schema 均匹配：`rp-world-v1`、`rp-source-registry-v1`、`rp-characters-index-v1`、`rp-knowledge-graph-v1`、`rp-relationship-graph-v1`。
- 按 `manual-curation/QA-JSON-SCHEMA.md` 原始字段表复核，顶层必备字段缺失为 0。
- `knowledge-graph.json` / `relationship-graph.json` 中 `edges[].from/to` 均能解析到同文件 `nodes[].id`。
- 未发现图谱字符串节点或重复 node id。

## P1 / HIGH 复核

### 已清零：6 个未注册 evidence/source 引用

R2 报告中的 6 个残留项已清零：

- `worlds/marvel-cinematic-universe/curated/relationship-graph.json`：`edges.3.evidence.0`、`edges.4.evidence.0`
- `worlds/naruto/curated/relationship-graph.json`：`edges.3.evidence.0`、`edges.4.evidence.0`
- `worlds/type-moon-nasuverse/curated/relationship-graph.json`：`edges.3.evidence.0`、`edges.4.evidence.0`

复核口径：字符串 source/evidence 必须匹配同世界 `source-registry.sources[].sourceId`，允许 `sourceId#fragment` 解析到父 `sourceId`；结构化 `{ kind: "internal-curated-field", ref: "characters-index.relationships" }` 按内部 curated 字段依据处理，不计为外部 source id。结果：未注册 source/evidence 为 0。

### 严格类型不匹配

- `world.json:sandboxPrinciple`：0 项不匹配。
- `world.json:foreignPowerSuppressionDefault`：0 项不匹配。
- `source-registry.json:sources/conflictLog`：0 项不匹配。
- `characters-index.json:characters`：0 项不匹配。
- `knowledge-graph.json:nodes/edges` 与 `relationship-graph.json:nodes/edges`：0 项不匹配。

### 扩展类型风险

R2 的 6 项扩展类型风险已清零：

- `blue-archive` / `monster-hunter` 的 `characters-index.json:notCompleteCanonRoster` 与 `runtimeUseGate.notCompleteCanonRoster` 均为 object。
- `date-a-live` / `madan-no-ou` 的 `knowledge-graph.json:notes` 与 `relationship-graph.json:notes` 均为 array。

## 空 sources / conflictLog 语义状态

### `sources` 空状态

- 空 `source-registry.sources`：0。
- 结论：结构上每个世界都有可枚举 sources。

### `conflictLog` 空状态

空 `source-registry.conflictLog` 仍有 35 个世界：

`absolute-duo`、`acg-character-database`、`akame-ga-kill`、`blue-archive`、`bocchi-the-rock`、`cheng-long-adventures`、`chunibyo`、`claymore`、`cross-ange`、`d-gray-man`、`gate-jsdf`、`haganai`、`hidan-no-aria`、`ikki-tousen`、`jojo`、`kaguya-sama`、`kekkaishi`、`kill-la-kill`、`majo-no-tabitabi`、`monster-hunter`、`omamori-himari`、`overlord`、`persona-5`、`rakudai-kishi`、`sekirei`、`sora-no-otoshimono`、`spice-and-wolf`、`sword-art-online`、`taimanin`、`testament-sister-new-devil`、`toaru`、`toriko`、`world-god-only-knows`、`xianjian-1`、`zero-no-tsukaima`。

语义状态复核结果：缺失或不合格为 0。普通世界状态为 `not-reviewed`，`acg-character-database` 为 `not-applicable`；`registryNotes` 均包含空 `conflictLog` 不等于已确认无冲突的说明或等价人工复核说明。

## MED / LOW / INFO 统计

本轮 MED/LOW/INFO 使用只读启发式扫描，类别如下：

| Severity | Count | 主要类别 |
|---|---:|---|
| MED | 332 | `character-location` 168、`character-faction` 121、`world-faction-member` 31、`character-powerSystem` 12 |
| LOW | 870 | `character-relationship-target` 560、`relationship-coverage` 310 |
| INFO | 349 | `world-kg-coverage` 349 |

### 类别说明

- `character-relationship-target`：角色 `relationships[]` 中目标无法直接解析为 indexed character id；大量值是 `id:关系标签` 字符串，可能需要规范化为结构化目标和关系说明。
- `relationship-coverage`：indexed character 未在 `relationship-graph.nodes[]` 中覆盖，属于检索覆盖质量问题。
- `world-kg-coverage`：world 层 faction/location/powerSystem id 未在 KG nodes 中覆盖，属于 INFO 级覆盖提示。
- `character-faction` / `character-location` / `character-powerSystem`：角色字段值与 world 层 id 不完全一致，通常是 slug/display label 规范化问题。
- `world-faction-member`：world faction `knownMembers` 未解析到 indexed character id。

### 残留最多的世界（Top 25）

| 世界 | Total | MED | LOW | INFO |
|---|---:|---:|---:|---:|
| `madan-no-ou` | 109 | 2 | 69 | 38 |
| `date-a-live` | 78 | 0 | 63 | 15 |
| `kekkaishi` | 71 | 41 | 30 | 0 |
| `toriko` | 65 | 0 | 52 | 13 |
| `ikki-tousen` | 63 | 32 | 31 | 0 |
| `cross-ange` | 52 | 0 | 38 | 14 |
| `naruto` | 50 | 3 | 27 | 20 |
| `d-gray-man` | 49 | 0 | 28 | 21 |
| `marvel-cinematic-universe` | 45 | 6 | 17 | 22 |
| `type-moon-nasuverse` | 45 | 22 | 19 | 4 |
| `dragon-ball` | 43 | 0 | 19 | 24 |
| `honkai-impact-3rd` | 42 | 5 | 22 | 15 |
| `toaru` | 42 | 0 | 42 | 0 |
| `danmachi` | 38 | 17 | 17 | 4 |
| `dantalian-no-shoka` | 38 | 0 | 2 | 36 |
| `persona-5` | 35 | 0 | 28 | 7 |
| `gate-jsdf` | 34 | 0 | 10 | 24 |
| `high-school-dxd` | 34 | 11 | 19 | 4 |
| `kimetsu-no-yaiba` | 34 | 11 | 19 | 4 |
| `negima-uq-holder` | 34 | 23 | 10 | 1 |
| `tokyo-ghoul` | 29 | 8 | 17 | 4 |
| `kenichi` | 28 | 17 | 11 | 0 |
| `world-god-only-knows` | 27 | 0 | 25 | 2 |
| `dungeon-fighter-online` | 25 | 7 | 13 | 5 |
| `gundam-seed` | 25 | 0 | 13 | 12 |

## Placeholder / 占位信号

扫描到 19 个世界仍含 `referenced-placeholder`：

`acg-character-database`、`akame-ga-kill`、`blue-archive`、`cheng-long-adventures`、`claymore`、`infinite-stratos`、`kill-la-kill`、`majo-no-tabitabi`、`monster-hunter`、`overlord`、`persona-5`、`rakudai-kishi`、`sora-no-otoshimono`、`sword-art-online`、`taimanin`、`testament-sister-new-devil`、`toaru`、`world-god-only-knows`、`xianjian-1`。

判断：这不是 JSON/schema 阻断，也未计入 P0/P1/HIGH；但属于来源和引用质量风险，运行时不应把 placeholder 当作已核实来源事实。

## 最终判定

- **P0/P1/HIGH 均为 0**：R3 目标中的 6 个未注册 evidence/source、扩展类型风险与空 conflictLog 语义状态均已复核通过。
- **仍不能判定完全没问题**：MED/LOW/INFO 合计 1551 项，另有 19 个 placeholder 信号，说明规范化、覆盖与来源质量仍有后续清理空间。
- **本 QA 步骤未修复任何 curated 文件**：符合 qa-r3 只读要求，唯一写入为本报告。
