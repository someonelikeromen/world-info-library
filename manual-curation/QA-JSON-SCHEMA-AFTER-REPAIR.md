# QA-JSON-SCHEMA-AFTER-REPAIR

检查日期：2026-06-22  
范围：`worlds/*/curated/*.json`  
任务：修复后只读复核 JSON/schema；对比 `manual-curation/QA-JSON-SCHEMA.md`；本报告是唯一写入文件，未修改 `worlds/*/curated`。

## 复核方法

使用本地 Python 只读扫描全部 curated JSON，检查：

1. `worlds/*/curated/*.json` 是否可被 `json.loads` 解析。
2. 每个世界是否具备 5 类 JSON：`world.json`、`source-registry.json`、`characters-index.json`、`knowledge-graph.json`、`relationship-graph.json`。
3. 5 类文件顶层 `schema` 是否匹配 `QA-JSON-SCHEMA.md` 中的期望值。
4. `QA-JSON-SCHEMA.md` 列出的顶层必备字段是否存在。
5. 关键顶层集合/对象字段的基础类型是否匹配运行时读取预期。
6. `knowledge-graph.json` / `relationship-graph.json` 的 `edges[].from` / `edges[].to` 是否均能解析到 `nodes[].id`。
7. 图谱 `nodes[]` 是否仍存在字符串节点或重复 node id。
8. 递归检查 `sourceRefs` / `sourceRef` / `sourceBasis` / `source.ref` / relationship `evidence` 中的来源引用是否已在同世界 `source-registry.sources[]` 注册。
9. 特殊世界 `acg-character-database`、`blue-archive`、`monster-hunter` 的运行时门禁字段是否存在。

## 总览对比

| 项目 | 修复前 `QA-JSON-SCHEMA.md` | 修复后复核 |
|---|---:|---:|
| 世界目录数 | 63 | 63 |
| JSON 文件总数 | 315 | 315 |
| 每世界 5 类 JSON 齐备 | 是 | 是 |
| JSON 解析失败 | 0 | 0 |
| 未识别 JSON 文件名 | 0 | 0 |
| schema 值不匹配 | 130 个文件 / 26 个世界 | 0 |
| 缺顶层关键字段 | 200 个文件 / 926 个缺字段项 | 0 |
| 原报告列出的顶层类型不匹配 | 3 项 | 0（已修复） |
| 严格关键字段类型不匹配 | 原报告未完全展开 | 34 项 |
| HIGH 图谱 edge-node 断链 | 原 `QA-CROSS-REFERENCES.md` 有 HIGH | 0 |
| HIGH sourceRefs 未注册 | 原 `QA-CROSS-REFERENCES.md` 有 HIGH | 0 |
| 特殊世界门禁字段缺失 | 修复前有风险 | 0 |

## 解析失败

无。315 个 curated JSON 全部解析成功。

## schema mismatch

无。5 类文件当前均匹配期望 schema：

| 文件 | 当前 schema |
|---|---|
| `world.json` | `rp-world-v1` |
| `source-registry.json` | `rp-source-registry-v1` |
| `characters-index.json` | `rp-characters-index-v1` |
| `knowledge-graph.json` | `rp-knowledge-graph-v1` |
| `relationship-graph.json` | `rp-relationship-graph-v1` |

## 缺顶层关键字段

无。`QA-JSON-SCHEMA.md` 中列出的必备字段均已存在。

## 类型错误

### 已修复的原报告类型错误

`QA-JSON-SCHEMA.md` 原列出的 3 项类型错误已修复：

- `worlds/date-a-live/curated/world.json`：`notes` 当前为 array。
- `worlds/date-a-live/curated/world.json`：`worldRules` 当前为 object。
- `worlds/toriko/curated/world.json`：`worldRules` 当前为 object。

### 严格复核发现的剩余类型不匹配（34 项）

以下字段存在且可解析，但类型仍与结构骨架预期不一致：

- `sandboxPrinciple`：当前为 string，严格预期为 object。
- `foreignPowerSuppressionDefault`：当前为 boolean，严格预期为 object。

受影响世界均为同一模式，每个世界 2 项：

| 世界 | 文件 | 字段 | 当前类型 | 严格预期 |
|---|---|---|---|---|
| `absolute-duo` | `world.json` | `sandboxPrinciple` | string | object |
| `absolute-duo` | `world.json` | `foreignPowerSuppressionDefault` | boolean | object |
| `danmachi` | `world.json` | `sandboxPrinciple` | string | object |
| `danmachi` | `world.json` | `foreignPowerSuppressionDefault` | boolean | object |
| `dungeon-fighter-online` | `world.json` | `sandboxPrinciple` | string | object |
| `dungeon-fighter-online` | `world.json` | `foreignPowerSuppressionDefault` | boolean | object |
| `elemental-gelade` | `world.json` | `sandboxPrinciple` | string | object |
| `elemental-gelade` | `world.json` | `foreignPowerSuppressionDefault` | boolean | object |
| `evangelion` | `world.json` | `sandboxPrinciple` | string | object |
| `evangelion` | `world.json` | `foreignPowerSuppressionDefault` | boolean | object |
| `high-school-dxd` | `world.json` | `sandboxPrinciple` | string | object |
| `high-school-dxd` | `world.json` | `foreignPowerSuppressionDefault` | boolean | object |
| `honkai-impact-3rd` | `world.json` | `sandboxPrinciple` | string | object |
| `honkai-impact-3rd` | `world.json` | `foreignPowerSuppressionDefault` | boolean | object |
| `kaguya-sama` | `world.json` | `sandboxPrinciple` | string | object |
| `kaguya-sama` | `world.json` | `foreignPowerSuppressionDefault` | boolean | object |
| `kimetsu-no-yaiba` | `world.json` | `sandboxPrinciple` | string | object |
| `kimetsu-no-yaiba` | `world.json` | `foreignPowerSuppressionDefault` | boolean | object |
| `marvel-cinematic-universe` | `world.json` | `sandboxPrinciple` | string | object |
| `marvel-cinematic-universe` | `world.json` | `foreignPowerSuppressionDefault` | boolean | object |
| `naruto` | `world.json` | `sandboxPrinciple` | string | object |
| `naruto` | `world.json` | `foreignPowerSuppressionDefault` | boolean | object |
| `omamori-himari` | `world.json` | `sandboxPrinciple` | string | object |
| `omamori-himari` | `world.json` | `foreignPowerSuppressionDefault` | boolean | object |
| `rozen-maiden` | `world.json` | `sandboxPrinciple` | string | object |
| `rozen-maiden` | `world.json` | `foreignPowerSuppressionDefault` | boolean | object |
| `sekirei` | `world.json` | `sandboxPrinciple` | string | object |
| `sekirei` | `world.json` | `foreignPowerSuppressionDefault` | boolean | object |
| `spice-and-wolf` | `world.json` | `sandboxPrinciple` | string | object |
| `spice-and-wolf` | `world.json` | `foreignPowerSuppressionDefault` | boolean | object |
| `tokyo-ghoul` | `world.json` | `sandboxPrinciple` | string | object |
| `tokyo-ghoul` | `world.json` | `foreignPowerSuppressionDefault` | boolean | object |
| `type-moon-nasuverse` | `world.json` | `sandboxPrinciple` | string | object |
| `type-moon-nasuverse` | `world.json` | `foreignPowerSuppressionDefault` | boolean | object |

判断：这些是剩余 P1 风险。若下游按 object 访问 `sandboxPrinciple.*` 或 `foreignPowerSuppressionDefault.*`，会发生类型不兼容；若下游允许 string/boolean 简写，则可降级为兼容性风险。当前按结构骨架严格口径列为残留。

## HIGH 图谱断链复核

未发现剩余图谱端点断链：

- `knowledge-graph.json`：`edges[].from` / `edges[].to` 均存在于同文件 `nodes[].id`。
- `relationship-graph.json`：`edges[].from` / `edges[].to` 均存在于同文件 `nodes[].id`。
- 未发现 `nodes[]` 中残留字符串节点。
- 未发现重复 `nodes[].id`。

结论：`QA-CROSS-REFERENCES.md` 原列出的 HIGH `relationship-edge-node` / `knowledge-edge-node` 类问题在本次机械复核口径下已清零。

## HIGH sourceRefs 未注册复核

未发现剩余未注册来源引用。递归检查范围包括：

- `sourceRefs`
- `sourceRef`
- `sourceBasis`
- `source.ref`
- relationship / graph 中可识别的 `evidence` 来源引用

结论：所有检测到的引用值均能在同世界 `source-registry.sources[]` 中以 `sourceId` 或 `id` 解析。

## 特殊世界门禁复核

| 世界 | 复核结果 |
|---|---|
| `acg-character-database` | `world.json.runtimeUseGate`、`world.json.specialWorldGate`、`characters-index.json.runtimeUseGate`、`source-registry.json.registryUseGate` 均存在。 |
| `blue-archive` | `world.json.runtimeUseGate`、`characters-index.json.runtimeUseGate`、`characters-index.json.notCompleteCanonRoster`、`source-registry.json.registryUseGate` 均存在。 |
| `monster-hunter` | `world.json.runtimeUseGate`、`characters-index.json.runtimeUseGate`、`characters-index.json.notCompleteCanonRoster`、`source-registry.json.registryUseGate` 均存在。 |

结论：特殊世界运行时门禁字段已具备；本轮未验证门禁正文质量，只验证字段存在性。

## 空集合/占位残留风险

这些不是 JSON 解析失败、schema mismatch 或缺字段，但仍影响后续人工质量：

- `source-registry.json:sources` 为空的世界：`blue-archive`、`cheng-long-adventures`、`monster-hunter`、`overlord`、`persona-5`、`rakudai-kishi`、`sora-no-otoshimono`、`sword-art-online`、`world-god-only-knows`、`xianjian-1`。
- `source-registry.json:conflictLog` 为空的世界数：35。空 `conflictLog` 可能表示“未登记冲突”，不等于已证明“无冲突”。
- 大量新增的 `indices`、`views`、运行时骨架字段可能仍为空对象/空数组；这满足结构读取，但不代表检索质量完成。
- 图谱中如仍存在 `referenced-placeholder`、来源中如存在 `granular-reference-placeholder` / `unregistered-placeholder`，属于结构占位质量风险，需要后续人工补证据与类型说明。

## 剩余 P0/P1 结论

- **P0：未发现。** JSON 全部可解析；5 类文件齐备；schema mismatch 为 0；缺顶层必备字段为 0；图谱 HIGH 断链为 0；sourceRefs 未注册为 0。
- **P1：仍有 34 项严格类型不匹配。** 集中在 17 个 `world.json` 的 `sandboxPrinciple`（string 而非 object）与 `foreignPowerSuppressionDefault`（boolean 而非 object）。
- **P1/质量边界风险：** 10 个 registry 的 `sources` 为空、35 个 registry 的 `conflictLog` 为空，以及占位/空骨架字段仍需人工复核；这些未计入 schema 失败，但会影响来源可追溯性和运行时检索质量。

## 校验状态

本次复核已完成并写入：`manual-curation/QA-JSON-SCHEMA-AFTER-REPAIR.md`。  
除本报告外，未修改 curated JSON。
