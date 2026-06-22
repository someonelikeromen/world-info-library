# QA-AFTER-REPAIR-R2

检查日期：2026-06-22  
范围：`worlds/*/curated/` 下 63 个世界、315 个 curated JSON。  
执行方式：只读 bash/Node 扫描；本步骤未修改 curated，唯一写入文件为本报告 `manual-curation/QA-AFTER-REPAIR-R2.md`。

## 结论摘要

- **P0：0**。未发现 JSON parse 失败、5 文件缺失、未识别 JSON、schema mismatch、原始 QA 顶层必备字段缺失、图谱 edge-node 断链、字符串节点或重复 node id。
- **P1：6**。34 项 r7 后遗留严格类型不匹配已清零；但本轮严格来源引用扫描发现 6 条 `relationship-graph.json` 的 `evidence` 值未注册到同世界 `source-registry.sources[]`。
- **HIGH：6**。全部为未注册 evidence/source 引用；图谱断链 HIGH 为 0。
- **MED/LOW/INFO：MED 75 / LOW 1039 / INFO 353**。这些为规范化、关系覆盖、KG 覆盖启发式问题，不是 JSON/schema 阻断。
- **是否可判定没问题：否**。结构性 P0 已清零，但仍有 6 个 HIGH/P1 来源注册问题，以及大量 MED/LOW/INFO 质量残留。

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
| 原始 QA/修复目标严格类型不匹配 | 0 |
| 扩展运行时字段类型风险 | 6（见“非阻断扩展类型风险”） |
| knowledge/relationship edge-node 断链 | 0 |
| graph string nodes | 0 |
| duplicate graph node ids | 0 |
| source/evidence 未注册 | 6 |
| 空 `source-registry.sources` | 0 |
| 空 `source-registry.conflictLog` | 35 |
| placeholder 信号 | 19 个世界含 `referenced-placeholder` |

## P0 复核

本轮未发现 P0：

- `worlds/*/curated/*.json` 共 315 个文件均可 `JSON.parse`。
- 63 个世界均具备：`world.json`、`source-registry.json`、`characters-index.json`、`knowledge-graph.json`、`relationship-graph.json`。
- 5 类文件 schema 均匹配：`rp-world-v1`、`rp-source-registry-v1`、`rp-characters-index-v1`、`rp-knowledge-graph-v1`、`rp-relationship-graph-v1`。
- 按 `manual-curation/QA-JSON-SCHEMA.md` 原始字段表复核，顶层必备字段缺失为 0。
- `knowledge-graph.json` / `relationship-graph.json` 中 `edges[].from/to` 均能解析到同文件 `nodes[].id`。
- 未发现图谱字符串节点或重复 node id。

## P1 / HIGH 残留清单

### 已清零

`manual-curation/REPAIR-P1-TYPES.md` 指定的 34 项严格类型不匹配已清零：

- `world.json:sandboxPrinciple` 已为 object。
- `world.json:foreignPowerSuppressionDefault` 已为 object。
- 原始 QA 中 `date-a-live` / `toriko` 的 `notes`、`worldRules` 类型问题也为 0。

### 仍残留：6 个未注册 evidence/source 引用

严格 source registry 扫描把 `sourceRefs`、`sourceRef`、`sourceBasis`、`source.ref` 与 relationship `evidence` 中可识别的字符串来源都要求注册到同世界 `source-registry.sources[]`。本轮发现以下 6 条未注册，按 HIGH/P1 计：

| 世界 | 文件 | 字段路径 | 未注册值 |
|---|---|---|---|
| `marvel-cinematic-universe` | `relationship-graph.json` | `edges.3.evidence.0` | `characters-index.relationships` |
| `marvel-cinematic-universe` | `relationship-graph.json` | `edges.4.evidence.0` | `characters-index.relationships` |
| `naruto` | `relationship-graph.json` | `edges.3.evidence.0` | `characters-index.relationships` |
| `naruto` | `relationship-graph.json` | `edges.4.evidence.0` | `characters-index.relationships` |
| `type-moon-nasuverse` | `relationship-graph.json` | `edges.3.evidence.0` | `characters-index.relationships` |
| `type-moon-nasuverse` | `relationship-graph.json` | `edges.4.evidence.0` | `characters-index.relationships` |

判断：这些值看起来像“来自 characters-index.relationships 字段”的内部依据说明，而不是 registry source id；但在严格来源引用口径下仍是未注册引用，需要改为已注册 source id，或明确把字段语义改成非 source 引用。

## MED / LOW / INFO 统计

本轮 MED/LOW/INFO 使用只读启发式扫描，类别如下：

| Severity | Count | 主要类别 |
|---|---:|---|
| MED | 75 | `world-faction-member` 31、`character-powerSystem` 12、`character-faction` 18、`character-location` 14 |
| LOW | 1039 | `character-relationship-target` 729、`relationship-coverage` 310 |
| INFO | 353 | `world-kg-coverage` 353 |

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
| `dantalian-no-shoka` | 100 | 0 | 64 | 36 |
| `date-a-live` | 78 | 0 | 63 | 15 |
| `toriko` | 65 | 0 | 52 | 13 |
| `cross-ange` | 52 | 0 | 38 | 14 |
| `naruto` | 50 | 3 | 27 | 20 |
| `d-gray-man` | 49 | 0 | 28 | 21 |
| `gate-jsdf` | 48 | 0 | 24 | 24 |
| `marvel-cinematic-universe` | 45 | 6 | 17 | 22 |
| `dragon-ball` | 43 | 0 | 19 | 24 |
| `rozen-maiden` | 43 | 5 | 31 | 7 |
| `honkai-impact-3rd` | 42 | 5 | 22 | 15 |
| `toaru` | 42 | 0 | 42 | 0 |
| `persona-5` | 35 | 0 | 28 | 7 |
| `sekirei` | 35 | 2 | 27 | 6 |
| `type-moon-nasuverse` | 33 | 10 | 19 | 4 |
| `ikki-tousen` | 31 | 0 | 31 | 0 |
| `kekkaishi` | 30 | 0 | 30 | 0 |
| `danmachi` | 29 | 8 | 17 | 4 |
| `elemental-gelade` | 29 | 7 | 16 | 6 |
| `world-god-only-knows` | 27 | 0 | 25 | 2 |
| `kimetsu-no-yaiba` | 26 | 3 | 19 | 4 |
| `gundam-seed` | 25 | 0 | 13 | 12 |
| `high-school-dxd` | 25 | 2 | 19 | 4 |
| `omamori-himari` | 23 | 3 | 15 | 5 |

## 空 sources / conflictLog 语义状态

### `sources` 空状态

- 空 `source-registry.sources`：0。
- 结论：第二轮后空 source registry 已清零，至少结构上每个世界都有可枚举 sources。

### `conflictLog` 空状态

空 `source-registry.conflictLog` 仍有 35 个世界：

`absolute-duo`、`acg-character-database`、`akame-ga-kill`、`blue-archive`、`bocchi-the-rock`、`cheng-long-adventures`、`chunibyo`、`claymore`、`cross-ange`、`d-gray-man`、`gate-jsdf`、`haganai`、`hidan-no-aria`、`ikki-tousen`、`jojo`、`kaguya-sama`、`kekkaishi`、`kill-la-kill`、`majo-no-tabitabi`、`monster-hunter`、`omamori-himari`、`overlord`、`persona-5`、`rakudai-kishi`、`sekirei`、`sora-no-otoshimono`、`spice-and-wolf`、`sword-art-online`、`taimanin`、`testament-sister-new-devil`、`toaru`、`toriko`、`world-god-only-knows`、`xianjian-1`、`zero-no-tsukaima`。

判断：空 `conflictLog` 不再是结构错误，但语义仍不充分；无法区分“已确认无冲突”与“尚未整理冲突”。建议后续加入显式 notes/status 字段或 registry 注记。

## 非阻断扩展类型风险

按原始 QA 字段表，严格类型错误为 0；但若运行时使用第二轮新增/扩展字段骨架，下列 6 项仍可能触发兼容性风险：

| 世界 | 文件 | 字段 | 当前类型 | 扩展期望 |
|---|---|---|---|---|
| `blue-archive` | `characters-index.json` | `notCompleteCanonRoster` | boolean | object |
| `monster-hunter` | `characters-index.json` | `notCompleteCanonRoster` | boolean | object |
| `date-a-live` | `knowledge-graph.json` | `notes` | string | array |
| `date-a-live` | `relationship-graph.json` | `notes` | string | array |
| `madan-no-ou` | `knowledge-graph.json` | `notes` | string | array |
| `madan-no-ou` | `relationship-graph.json` | `notes` | string | array |

判断：这些未计入本报告 P1，因为它们不属于 `manual-curation/QA-JSON-SCHEMA.md` 原始类型表，也不属于 r7 后 34 项 P1；但若消费者按扩展 object/array 读取，应在后续修复。

## Placeholder / 占位信号

扫描到 19 个世界仍含 `referenced-placeholder`：

`acg-character-database`、`akame-ga-kill`、`blue-archive`、`cheng-long-adventures`、`claymore`、`infinite-stratos`、`kill-la-kill`、`majo-no-tabitabi`、`monster-hunter`、`overlord`、`persona-5`、`rakudai-kishi`、`sora-no-otoshimono`、`sword-art-online`、`taimanin`、`testament-sister-new-devil`、`toaru`、`world-god-only-knows`、`xianjian-1`。

判断：这不是 JSON/schema 阻断，但属于来源和引用质量风险；运行时不应把 placeholder 当作已核实来源事实。

## 最终判定

- **不可判定“没问题”**：P0 已清零，34 项原 P1 类型不匹配已清零，但仍存在 6 个 HIGH/P1 未注册 evidence/source 引用。
- **可进入下一轮定向修复**：优先修复 6 个 `characters-index.relationships` evidence 注册/语义问题；随后处理 35 个空 `conflictLog` 的语义标记，以及 MED/LOW/INFO 的关系字符串规范化和 KG/relationship 覆盖。
- **curated 修改状态**：本 QA 步骤未修改 `worlds/*/curated`。