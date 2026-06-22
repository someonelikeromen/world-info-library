# QA-JSON-SCHEMA

检查日期：2026-06-22  
范围：`worlds/*/curated/*.json`  
只读校验：未修改任何 `worlds/*/curated` 正文。

## 校验依据

参考结构：

- `../templates/rp-framework/world-template.json`
- `../templates/rp-framework/source-registry-template.json`
- `../templates/rp-framework/knowledge-graph-template.json`
- `../templates/rp-framework/relationship-graph-template.json`
- `manual-curation/PLAN.md` 中 `characters-index.json` 结构

基础检查项：

| 文件 | 期望 schema | 顶层必备字段 |
|---|---|---|
| `world.json` | `rp-world-v1` | `schema`, `worldId`, `worldName`, `aliases`, `genre`, `summary`, `sandboxPrinciple`, `hasFixedFate`, `foreignPowerSuppressionDefault`, `notes`, `powerSystems`, `factions`, `energyEnvironment`, `worldRules`, `locations`, `publicEvents`, `hiddenEvents` |
| `source-registry.json` | `rp-source-registry-v1` | `schema`, `campaignId`, `sources`, `conflictLog` |
| `characters-index.json` | `rp-characters-index-v1` | `schema`, `worldId`, `characters`, `indices` |
| `knowledge-graph.json` | `rp-knowledge-graph-v1` | `schema`, `campaignId`, `nodes`, `edges`, `indices` |
| `relationship-graph.json` | `rp-relationship-graph-v1` | `schema`, `campaignId`, `nodes`, `edges`, `views` |

## 总览

- 世界目录数：63
- JSON 文件总数：315
- 每个世界 5 类 JSON 文件齐备：是（63 × 5）
- JSON 解析失败：0
- 未识别文件名：0
- schema 值不匹配：130 个文件，集中在 26 个世界（通常为 `curated-*` 或 `rp-curated-*` 前缀）
- 缺顶层关键字段：200 个文件存在问题，共 926 个缺字段项
- 顶层类型不匹配：3 项
- 空数组/空对象风险：12 项（仅统计已存在且为空的关键集合/对象；未把正常可空的业务字段作错误处理）

## 解析失败

无。所有 315 个 JSON 文件均可被 Python `json.loads` 成功解析。

## schema 值不匹配

以下 26 个世界的 5 类 JSON 均存在 schema 命名与模板不一致的问题。建议统一为模板/PLAN 中的 `rp-*-v1`：

- `acg-character-database`：使用 `curated-*-v1`
- `akame-ga-kill`：使用 `rp-curated-*-v1`
- `blue-archive`：使用 `rp-curated-*-v1`
- `bocchi-the-rock`：使用 `rp-curated-*-v1`
- `cheng-long-adventures`：使用 `rp-curated-*-v1`
- `chunibyo`：使用 `rp-curated-*-v1`
- `claymore`：使用 `curated-*-v1`
- `haganai`：使用 `rp-curated-*-v1`
- `infinite-stratos`：使用 `rp-curated-*-v1`
- `jojo`：使用 `rp-curated-*-v1`
- `kill-la-kill`：使用 `rp-curated-*-v1`
- `majo-no-tabitabi`：使用 `rp-curated-*-v1`
- `monster-hunter`：使用 `curated-*-v1`
- `overlord`：使用 `curated-*-v1`
- `persona-5`：使用 `rp-curated-*-v1`
- `rakudai-kishi`：使用 `curated-*-v1`
- `saijaku-muhai-bahamut`：使用 `rp-curated-*-v1`
- `sora-no-otoshimono`：使用 `curated-*-v1`
- `sword-art-online`：使用 `curated-*-v1`
- `taimanin`：使用 `rp-curated-*-v1`
- `testament-sister-new-devil`：使用 `curated-*-v1`
- `to-love-ru`：使用 `rp-curated-*-v1`
- `toaru`：使用 `curated-*-v1`
- `world-god-only-knows`：使用 `rp-curated-*-v1`
- `xianjian-1`：使用 `rp-curated-*-v1`
- `zero-no-tsukaima`：使用 `rp-curated-*-v1`

## 缺关键字段统计

按字段聚合：

| 缺失次数 | 文件:字段 |
|---:|---|
| 46 | `knowledge-graph.json:campaignId` |
| 46 | `knowledge-graph.json:indices` |
| 46 | `relationship-graph.json:campaignId` |
| 46 | `relationship-graph.json:views` |
| 46 | `world.json:worldName` |
| 46 | `world.json:sandboxPrinciple` |
| 46 | `world.json:hasFixedFate` |
| 46 | `world.json:foreignPowerSuppressionDefault` |
| 46 | `world.json:energyEnvironment` |
| 44 | `world.json:aliases` |
| 44 | `world.json:notes` |
| 44 | `world.json:worldRules` |
| 43 | `world.json:publicEvents` |
| 43 | `world.json:hiddenEvents` |
| 36 | `source-registry.json:campaignId` |
| 33 | `world.json:genre` |
| 26 | `characters-index.json:worldId` |
| 26 | `characters-index.json:indices` |
| 26 | `source-registry.json:conflictLog` |
| 26 | `world.json:worldId` |
| 19 | `relationship-graph.json:nodes` |
| 19 | `relationship-graph.json:edges` |
| 19 | `world.json:locations` |
| 17 | `world.json:powerSystems` |
| 17 | `world.json:summary` |
| 15 | `world.json:factions` |
| 14 | `source-registry.json:sources` |
| 1 | `characters-index.json:characters` |

高频模式：

1. 46 个世界的 `knowledge-graph.json` 缺 `campaignId` 与 `indices`，`relationship-graph.json` 缺 `campaignId` 与 `views`。
2. 46 个世界的 `world.json` 更像简化结构，缺模板要求的 `worldName`、沙盒/命运/外来力量默认字段，以及 `energyEnvironment` 等运行时字段。
3. 26 个世界的 `characters-index.json` 缺 `worldId` 与 `indices`，与 PLAN 中人物索引结构不一致。
4. 26 个世界的 `source-registry.json` 缺 `conflictLog`；36 个缺 `campaignId`。

## 缺关键字段详情（按世界）

> 仅列出存在缺字段的文件；未列出的同世界文件通过顶层字段存在性检查。

- `acg-character-database`
  - `characters-index.json`: `worldId`, `characters`, `indices`
  - `knowledge-graph.json`: `campaignId`, `indices`
  - `relationship-graph.json`: `campaignId`, `nodes`, `edges`, `views`
  - `source-registry.json`: `campaignId`, `sources`, `conflictLog`
  - `world.json`: `worldId`, `worldName`, `aliases`, `genre`, `sandboxPrinciple`, `hasFixedFate`, `foreignPowerSuppressionDefault`, `notes`, `powerSystems`, `factions`, `energyEnvironment`, `worldRules`, `locations`, `publicEvents`, `hiddenEvents`
- `akame-ga-kill`
  - `characters-index.json`: `worldId`, `indices`
  - `knowledge-graph.json`: `campaignId`, `indices`
  - `relationship-graph.json`: `campaignId`, `nodes`, `edges`, `views`
  - `source-registry.json`: `campaignId`, `conflictLog`
  - `world.json`: `worldId`, `worldName`, `aliases`, `genre`, `summary`, `sandboxPrinciple`, `hasFixedFate`, `foreignPowerSuppressionDefault`, `notes`, `energyEnvironment`, `worldRules`, `publicEvents`, `hiddenEvents`
- `black-bullet`
  - `knowledge-graph.json`: `campaignId`, `indices`
  - `relationship-graph.json`: `campaignId`, `views`
  - `source-registry.json`: `campaignId`
  - `world.json`: `worldName`, `aliases`, `genre`, `sandboxPrinciple`, `hasFixedFate`, `foreignPowerSuppressionDefault`, `notes`, `energyEnvironment`, `worldRules`, `publicEvents`, `hiddenEvents`
- `blue-archive`
  - `characters-index.json`: `worldId`, `indices`
  - `knowledge-graph.json`: `campaignId`, `indices`
  - `relationship-graph.json`: `campaignId`, `nodes`, `edges`, `views`
  - `source-registry.json`: `campaignId`, `sources`, `conflictLog`
  - `world.json`: `worldId`, `worldName`, `aliases`, `summary`, `sandboxPrinciple`, `hasFixedFate`, `foreignPowerSuppressionDefault`, `notes`, `powerSystems`, `factions`, `energyEnvironment`, `worldRules`, `locations`, `publicEvents`, `hiddenEvents`
- `bocchi-the-rock`, `chunibyo`, `haganai`：同类问题集中于 `characters-index.json` 缺 `worldId/indices`、图谱缺 `campaignId/indices/views`、`source-registry.json` 缺 `campaignId/conflictLog`、`world.json` 缺模板运行时字段。
- `campione`, `cross-ange`, `d-gray-man`, `dragon-ball`, `gate-jsdf`, `gundam-seed`, `hidan-no-aria`, `ikki-tousen`, `kekkaishi`, `kenichi`, `madan-no-ou`, `negima-uq-holder`, `record-of-ragnarok`, `seikoku-no-dragonar`, `senran-kagura`, `strike-the-blood`, `toriko`：主要是 46-world 模式，即 `knowledge-graph.json` 缺 `campaignId/indices`、`relationship-graph.json` 缺 `campaignId/views`、`world.json` 缺 `worldName` 及运行时字段；部分 `source-registry.json` 还缺 `campaignId`。
- `cheng-long-adventures`, `claymore`, `infinite-stratos`, `kill-la-kill`, `majo-no-tabitabi`, `monster-hunter`, `overlord`, `persona-5`, `rakudai-kishi`, `sora-no-otoshimono`, `sword-art-online`, `taimanin`, `testament-sister-new-devil`, `toaru`, `world-god-only-knows`, `xianjian-1`：除 schema 不匹配外，多数还缺 `characters-index.json:worldId/indices`、图谱 `campaignId/indices/views`、`source-registry.json:campaignId/sources/conflictLog` 中若干项，以及 `world.json` 大量模板字段。
- `date-a-live`, `dantalian-no-shoka`：主要缺图谱 `campaignId/indices/views` 与 `world.json` 中若干模板字段。
- `jojo`, `saijaku-muhai-bahamut`, `to-love-ru`, `zero-no-tsukaima`：主要缺 `characters-index.json:worldId/indices`、图谱运行时字段、`source-registry.json` 部分字段与 `world.json` 模板字段。

完整机器统计已在本报告“缺关键字段统计”中聚合；若修复，建议用同一规则批量补齐结构骨架，但不要用脚本重写正文内容。

## 顶层类型不匹配

发现 3 项会影响按模板读取：

| 文件 | 字段 | 实际类型 | 期望类型 |
|---|---|---:|---:|
| `worlds/date-a-live/curated/world.json` | `notes` | string | array |
| `worlds/date-a-live/curated/world.json` | `worldRules` | array | object |
| `worlds/toriko/curated/world.json` | `worldRules` | array | object |

## 空数组/空对象风险

这些不是 JSON 解析错误；但运行时检索或冲突追踪会因空集合缺信息，需要人工确认是否“确无冲突/来源”还是“尚未整理”。

| 文件 | 空字段 |
|---|---|
| `worlds/absolute-duo/curated/source-registry.json` | `conflictLog` |
| `worlds/cross-ange/curated/source-registry.json` | `conflictLog` |
| `worlds/d-gray-man/curated/source-registry.json` | `conflictLog` |
| `worlds/gate-jsdf/curated/source-registry.json` | `conflictLog` |
| `worlds/hidan-no-aria/curated/source-registry.json` | `conflictLog` |
| `worlds/ikki-tousen/curated/source-registry.json` | `conflictLog` |
| `worlds/kaguya-sama/curated/source-registry.json` | `conflictLog` |
| `worlds/kekkaishi/curated/source-registry.json` | `conflictLog` |
| `worlds/omamori-himari/curated/source-registry.json` | `conflictLog` |
| `worlds/sekirei/curated/source-registry.json` | `conflictLog` |
| `worlds/spice-and-wolf/curated/source-registry.json` | `conflictLog` |
| `worlds/toriko/curated/source-registry.json` | `conflictLog` |

## 建议修复项

1. **先统一 schema 名称**：把 `curated-*-v1` 与 `rp-curated-*-v1` 统一为模板中的 `rp-world-v1`、`rp-source-registry-v1`、`rp-characters-index-v1`、`rp-knowledge-graph-v1`、`rp-relationship-graph-v1`。这能消除 130 个 schema mismatch。
2. **为图谱补运行时元字段**：所有缺项优先补 `knowledge-graph.json:campaignId/indices` 与 `relationship-graph.json:campaignId/views`。空索引可先按模板给出对象骨架，例如 `byVisibility/byType/byTag/activeClues/lockedSecrets` 与 `playerVisibleNodeIds/gmHighlightedNodeIds/activeSceneNodeIds`，但内容需人工或后续 QA 确认。
3. **补 `characters-index.json` 的 `worldId` 与 `indices`**：26 个世界缺人物索引运行字段，另 `acg-character-database` 连 `characters` 也缺，需优先人工处理。
4. **补 `world.json` 模板字段**：尤其 `worldName`、`sandboxPrinciple`、`hasFixedFate`、`foreignPowerSuppressionDefault`、`energyEnvironment`、`worldRules`。这些字段会被 campaign/session 初始化和跨世界规则处理依赖。
5. **修正顶层类型不匹配**：`date-a-live` 的 `notes` 与 `worldRules`、`toriko` 的 `worldRules` 应改成模板期望类型，否则消费者按字段访问时容易报错。
6. **确认空 `conflictLog` 语义**：若确无冲突，建议保留空数组但在 `curation-notes.md` 或 registry notes 中注明；若未整理，应新增待办/低置信标记。
7. **避免脚本生成/改写正文**：可以用脚本发现缺字段并生成修复清单；字段内容、summary、来源和关系正文仍应人工归纳，遵循 PLAN 的“禁止用脚本自动抽取/改写正文”。

## 校验状态

- 结构 QA 报告已生成：`manual-curation/QA-JSON-SCHEMA.md`
- 本次仅写入本报告文件；未写入 `worlds/*/curated`。
