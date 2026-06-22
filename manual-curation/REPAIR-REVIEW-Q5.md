# REPAIR-REVIEW-Q5

审查日期：2026-06-22  
步骤：`review-q5`  
审查范围：`manual-curation/REPAIR-Q5-*.md` 与 `manual-curation/QA-AFTER-REPAIR-Q5.md`。  
变更范围：仅写入本审查文件；未修改 `worlds/*/curated/`。

## 总体结论

Q5 **未达到完全没问题**。虽然 P0/P1 仍为 0，MED 与 `unresolved-reference` 有实际收敛，但 Q5 后 QA 发现 **HIGH=21**，集中为 4 个世界的 `relationship-graph.json` 边端点断链。因此不能声明“P0/P1/HIGH 持续为 0”。

Q5 的主要成效是：

- MED：`54 → 51`，小幅下降。
- `unresolved-reference`：`8` 个世界 / `178` 次 → `3` 个世界 / `40` 次，明显下降。
- `referenced-placeholder`：继续保持 `0`。
- KG INFO 目标世界补齐了 113 个最小 KG 节点，目标内验证通过。

Q5 的主要残留/回归是：

- HIGH：`0 → 21`，关系图边端点未同步 canonical id。
- LOW：`140 → 295`，按 Q5 QA 更严格口径未下降。
- INFO：`200 → 202`，未下降。
- 泛化 placeholder：宽口径为 20 个世界 / 64 次，但多数不是阻断风险。

## P0 / P1 / HIGH 判定

| 等级 | Q5 后结果 | 审查判定 |
|---|---:|---|
| P0 | 0 | 通过 |
| P1 | 0 | 通过 |
| HIGH | 21 | 不通过 |

### HIGH 残留详情

`QA-AFTER-REPAIR-Q5.md` 报告 21 条 `relationship-graph.json` edge endpoint 与 `nodes[].id` 不匹配：

| 世界 | 断链数 | 代表端点 |
|---|---:|---|
| `blue-archive` | 10 | `茶会`、`万魔殿`、`风纪委员会`、`温泉开发部`、`研讨会`、`C&C`、`玄龙门`、`玄武商会` |
| `monster-hunter` | 5 | `猎人公会`、`禁忌怪物`、`古龙观测局` |
| `overlord` | 5 | `安兹·乌尔·恭` |
| `sora-no-otoshimono` | 1 | `西纳普斯` |

审查判断：这些 HIGH 项属于 **可自动修复**。Q5 unresolved 修复中把若干节点转成 canonical id，但边仍保留旧中文标签端点；应将 `edges[].from/to/source/target` 同步为同文件已存在的 `nodes[].id`，不需要新增 canon 或新增事实。

## MED / LOW / INFO 判定

| Severity | Q4 后 | Q5 后 | 变化 | 审查判定 |
|---|---:|---:|---:|---|
| MED | 54 | 51 | -3 | 有收敛但未清零 |
| LOW | 140 | 295 | +155 | 未收敛，且口径更严格后暴露更多尾项 |
| INFO | 200 | 202 | +2 | 未收敛 |

### 类别分布

- `character-relationship-target`：287。
- `world-kg-coverage`：202。
- `character-faction`：23。
- `character-location`：20。
- `character-powerSystem`：8。
- `relationship-coverage`：8。

审查判断：

- MED 残留涉及 `faction/location/powerSystem` 等结构字段是否能安全对齐 canonical id，不应盲目自动转正。
- LOW 的大头是 `character-relationship-target`，其中一部分可机械结构化，但字符串标签、多目标、组织/地点/概念目标仍需按类型分层。
- INFO `world-kg-coverage` 可继续用最小 KG 节点补齐，但不应与 HIGH 断链修复混在同一批。

## Placeholder 与 unresolved-reference 判定

| 项目 | Q4 后 | Q5 后 | 变化 | 审查判定 |
|---|---:|---:|---:|---|
| `referenced-placeholder` 世界数 | 0 | 0 | 0 | 通过 |
| `referenced-placeholder` 命中数 | 0 | 0 | 0 | 通过 |
| 泛化 placeholder 世界数 | 2 | 20 | +18 | 需分类，不作为阻断 |
| 泛化 placeholder 命中数 | 5 | 64 | +59 | 需分类，不作为阻断 |
| `unresolved-reference` 世界数 | 8 | 3 | -5 | 明显收敛但未清零 |
| `unresolved-reference` 命中数 | 178 | 40 | -138 | 明显收敛但未清零 |

### unresolved-reference 残留

Q5 后仍有 `unresolved-reference` 的世界：

- `acg-character-database`：28 次。
- `blue-archive`：8 次。
- `date-a-live`：4 次。

其中 `date-a-live` 的 4 条在 `REPAIR-Q5-RELATIONSHIP-LOW.md` 中已说明为概念性关系标签，保留是为了避免伪造目标；`REPAIR-Q5-TEXT-TOKEN.md` 也说明其中部分 aggregate placeholder 已转换为 `unresolved-reference` 风险标记。

### 泛化 placeholder 审查

泛化 placeholder 宽口径命中 20 个世界 / 64 次，但 QA 抽样显示包含大量非风险内容，例如：

- `unknown` 字段值。
- source id 中的 `sample`。
- README / curation notes 中的模板说明文字。
- `acg-character-database` 中合法的“人格模板”概念。

审查判断：泛化 placeholder 不应直接等同于 graph placeholder 风险。真正阻断类 `referenced-placeholder` 已保持 0；下一轮应先分类而非盲改。

## Q5 修复日志交叉审查

### `REPAIR-Q5-UNRESOLVED-REFERENCE.md`

- 有效转正多世界可唯一映射节点，尤其是 `overlord`、`sword-art-online`、`monster-hunter`、`rakudai-kishi`、`sora-no-otoshimono`、`cheng-long-adventures`。
- 保留 `blue-archive` 中集合/群体端点，原则正确。
- 但 QA 显示该批或相关批次留下关系图 edge endpoint canonical 同步问题，是 Q5 后 HIGH 回归的核心来源。

### `REPAIR-Q5-RELATIONSHIP-LOW.md`

- 10 个目标世界内字符串关系结构化有效，保留 `date-a-live` 4 条 unresolved 的理由充分。
- 但全库 LOW 仍高，说明目标批之外仍存在大量关系 target 尾项。

### `REPAIR-Q5-MED-TOP.md`

- 对 8 个 MED 高残留世界采用“不伪造 canon、不可证实项移入 notes/metadata”原则，方向正确。
- 全库 MED 仅下降 3，说明后续仍需继续处理非目标世界和更细类别。

### `REPAIR-Q5-KG-INFO.md`

- 11 个目标世界新增 113 个最小 KG 节点，并做目标内验证。
- 全库 INFO 仍为 202，属覆盖启发式尾项，可延后分批收敛。

### `REPAIR-Q5-TEXT-TOKEN.md`

- 将真实风险从 placeholder 状态改为 `unresolved-reference` 标记，避免把占位状态误当 canon。
- 泛化 token 仍需分类复核，不宜作为阻断项。

## 下一轮任务包

### Q6-A：自动修复 HIGH edge endpoint 断链（最高优先级）

目标：把 P0/P1/HIGH 恢复为 0。

范围：

- `worlds/blue-archive/curated/relationship-graph.json`
- `worlds/monster-hunter/curated/relationship-graph.json`
- `worlds/overlord/curated/relationship-graph.json`
- `worlds/sora-no-otoshimono/curated/relationship-graph.json`

要求：

- 只同步 `edges[].from/to/source/target` 到同文件已存在的 `nodes[].id`。
- 优先使用同节点 `metadata.q4SourceRiskReview.mappedId`、`label/name`、已有 canonical id 映射。
- 不新增节点、不新增 canon、不改事实语义。
- 修复后全量 QA，确认 `relationship edge-node 断链=0`、P0/P1/HIGH 全为 0。

### Q6-B：LOW relationship target 分层收敛

目标：降低 `character-relationship-target` 287 与 `relationship-coverage` 8。

建议顺序：

1. 先处理已存在 graph node id/label 可唯一匹配的 target。
2. 再处理组织、地点、概念 target，显式标注 `targetType`。
3. 多目标关系保留 `targets` 数组，避免误压成单目标。
4. 对不可唯一解析的描述性关系继续保留 `resolutionStatus: unresolved` 和说明。

### Q6-C：MED canonical 字段尾项

目标：继续降低 `character-faction`、`character-location`、`character-powerSystem`。

人工确认重点：

- 字段值是 display label、旧 slug、群体词，还是可证实 canonical id。
- 是否已有 world registry / KG / character index 锚点。
- 不可证实时应移入 notes/metadata 留痕，不伪造 canon。

### Q6-D：placeholder 宽口径分类

目标：把 20 个世界 / 64 次泛化 placeholder 命中拆成可执行类别。

分类建议：

- 字段值 `unknown`。
- source id / example / sample。
- README 或 notes 的说明性“模板”。
- 合法世界观概念，如“人格模板”。
- 真正未解析 placeholder / unresolved risk。

仅最后一类需要修 curated 结构；其余应记录为非风险或改 QA 口径。

### Q6-E：INFO KG 覆盖继续批处理

目标：按世界分批降低 `world-kg-coverage` 202。

要求：

- 只为 `world.json` 中已有 factions/locations/powerSystems 添加最小 KG 节点。
- 保持 minimal coverage，不扩展 lore。
- 每批运行目标内 duplicate node、edge endpoint、coverage 校验。

## 人工确认清单

需人工确认或至少半自动复核的项目：

- `acg-character-database` 的 28 次 `unresolved-reference`：需判断哪些是合法“模板/类型”概念，哪些是真未解析实体。
- `blue-archive` 的剩余 unresolved 集合端点：`各学园`、`各校学生`、`阿里乌斯分校`、`三一各派系` 等是否应保留结构性集合节点。
- `date-a-live` 的 4 条概念性 relationship unresolved：是否接受当前“不可唯一目标”的标记，或需要人工指定概念节点。
- MED 中 faction/location/powerSystem 字段：确认 canonical 对齐依据，避免把泛称词硬转为 canon。
- 泛化 placeholder 命中：确认哪些是合法文本/字段值，避免因 token 命中误删有效内容。

## 最终判定

Q5 后状态为：

- `P0=0`：通过。
- `P1=0`：通过。
- `HIGH=21`：不通过，必须先修。
- `MED=51`：未清零。
- `LOW=295`：未收敛。
- `INFO=202`：未收敛。
- `referenced-placeholder=0`：通过。
- 泛化 placeholder：需分类，不作为阻断。
- `unresolved-reference=3` 个世界 / 40 次：明显收敛但未清零。

因此审查结论是：**Q5 有质量收敛成效，但当前不能宣布完全没问题；下一轮必须优先自动修复 21 条 HIGH 关系图端点断链，并重跑全量 QA。**
