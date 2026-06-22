# QA-AFTER-REPAIR-Q5

检查日期：2026-06-22  
步骤：`qa-q5`  
范围：`worlds/*/curated/` 下 63 个世界、315 个 curated JSON。  
执行方式：只读 bash/Node 全量扫描；未修改 `worlds/*/curated`。唯一写入文件为本报告 `manual-curation/QA-AFTER-REPAIR-Q5.md`。

## 结论摘要

- **P0：0**。JSON parse、5 文件齐备、未识别 JSON、schema mismatch、顶层必备字段缺失、字符串节点、重复 node id 均未发现。
- **P1：0（按 Q4 修正口径）**。空 `source-registry.sources` 为 0；空 `conflictLog` 的语义状态缺失为 0；抽样确认 `characters-index.relationships` 属于 `internal-curated-field`，不按未注册 source 计入。
- **HIGH：21**。Q5 后不再是 0：`blue-archive`、`monster-hunter`、`overlord`、`sora-no-otoshimono` 的 `relationship-graph.json` 出现 edge endpoint 与 `nodes[].id` 不匹配，主要是节点已转成 canonical id，但边仍保留中文标签端点。
- **MED/LOW/INFO：MED 51 / LOW 295 / INFO 202**。与 Q4 的 MED 54 / LOW 140 / INFO 200 相比，MED 小幅下降 3；LOW 上升 155；INFO 上升 2。LOW 上升主要来自更严格识别字符串/结构化 relationship target 残留，INFO 上升为 KG 覆盖启发式尾项。
- **placeholder / unresolved**：`referenced-placeholder` 仍为 0；泛化 placeholder 宽口径为 20 个世界 64 次命中；`unresolved-reference` 为 3 个世界 40 次命中。`unresolved-reference` 世界数较 Q4 的 8 下降到 3，命中次数从 178 下降到 40。
- **最终判定**：Q5 质量收敛有效降低了 MED 与 unresolved，但引入或暴露了关系图 HIGH 断链；在修复这 21 条端点前，不能声明 P0/P1/HIGH 持续为 0。

## 扫描项目与结果

| 检查项 | Q5 结果 |
|---|---:|
| 世界目录数 | 63 |
| JSON 文件总数 | 315 |
| 每世界 5 类 JSON 齐备 | 是 |
| JSON parse 失败 | 0 |
| 未识别 JSON 文件名 | 0 |
| schema mismatch | 0 |
| 顶层必备字段缺失 | 0 |
| 严格类型/运行时类型阻断风险 | 0 |
| graph string nodes | 0 |
| duplicate graph node ids | 0 |
| relationship edge-node 断链 | 21 |
| knowledge edge-node 断链 | 0 |
| source/evidence 未注册 | 0（修正口径后） |
| 空 `source-registry.sources` | 0 |
| 空 `source-registry.conflictLog` | 35 |
| 空 `conflictLog` 缺语义状态 | 0 |
| `referenced-placeholder` 世界数 | 0 |
| 泛化 `placeholder` 世界数 | 20 |
| `unresolved-reference` 世界数 | 3 |

## HIGH 断链详情

`relationship-graph.json` 中 21 条边端点未能解析到同文件 `nodes[].id`：

| 世界 | 断链数 | 代表端点 |
|---|---:|---|
| `blue-archive` | 10 | `茶会`、`万魔殿`、`风纪委员会`、`温泉开发部`、`研讨会`、`C&C`、`玄龙门`、`玄武商会` |
| `monster-hunter` | 5 | `猎人公会`、`禁忌怪物`、`古龙观测局` |
| `overlord` | 5 | `安兹·乌尔·恭` |
| `sora-no-otoshimono` | 1 | `西纳普斯` |

抽样确认：这些图中存在已解析节点，例如 `blue-archive` 有 `tea-party-host`、`monster-hunter` 有 `guild`、`overlord` 有 `ainz`，但边仍使用旧中文端点。因此这是可机械修复的 canonical endpoint 同步问题，而不是缺少事实来源。

## MED / LOW / INFO 统计

| Severity | Q4 后 | Q5 后 | 变化 |
|---|---:|---:|---:|
| MED | 54 | 51 | -3 |
| LOW | 140 | 295 | +155 |
| INFO | 200 | 202 | +2 |
| 合计 | 394 | 548 | +154 |

类别分布：

- `character-relationship-target`：287
- `world-kg-coverage`：202
- `character-faction`：23
- `character-location`：20
- `character-powerSystem`：8
- `relationship-coverage`：8

### 残留最多的世界（Top 30）

| 世界 | Total | MED | LOW | INFO |
|---|---:|---:|---:|---:|
| `dantalian-no-shoka` | 64 | 0 | 64 | 0 |
| `hidan-no-aria` | 36 | 7 | 12 | 17 |
| `black-bullet` | 28 | 11 | 7 | 10 |
| `naruto` | 27 | 0 | 27 | 0 |
| `record-of-ragnarok` | 27 | 11 | 7 | 9 |
| `campione` | 25 | 9 | 6 | 10 |
| `high-school-dxd` | 25 | 0 | 15 | 10 |
| `kimetsu-no-yaiba` | 25 | 0 | 15 | 10 |
| `strike-the-blood` | 22 | 5 | 6 | 11 |
| `evangelion` | 21 | 1 | 12 | 8 |
| `dragon-ball` | 19 | 0 | 19 | 0 |
| `omamori-himari` | 19 | 0 | 14 | 5 |
| `seikoku-no-dragonar` | 19 | 6 | 5 | 8 |
| `elemental-gelade` | 18 | 0 | 12 | 6 |
| `kaguya-sama` | 18 | 0 | 14 | 4 |
| `senran-kagura` | 17 | 1 | 6 | 10 |
| `absolute-duo` | 15 | 0 | 11 | 4 |
| `gundam-seed` | 14 | 0 | 13 | 1 |
| `dungeon-fighter-online` | 11 | 0 | 0 | 11 |
| `kenichi` | 11 | 0 | 10 | 1 |
| `negima-uq-holder` | 11 | 0 | 10 | 1 |
| `ikki-tousen` | 10 | 0 | 1 | 9 |
| `kekkaishi` | 9 | 0 | 1 | 8 |
| `tokyo-ghoul` | 9 | 0 | 0 | 9 |
| `spice-and-wolf` | 8 | 0 | 2 | 6 |
| `world-god-only-knows` | 7 | 0 | 0 | 7 |
| `cheng-long-adventures` | 6 | 0 | 0 | 6 |
| `cross-ange` | 6 | 0 | 6 | 0 |
| `persona-5` | 6 | 0 | 0 | 6 |
| `claymore` | 3 | 0 | 0 | 3 |

## Placeholder / 未解析引用

| 项目 | Q4 后 | Q5 后 | 变化 |
|---|---:|---:|---:|
| `referenced-placeholder` 世界数 | 0 | 0 | 0 |
| `referenced-placeholder` 命中数 | 0 | 0 | 0 |
| 泛化 `placeholder` 世界数 | 2 | 20 | +18 |
| 泛化 `placeholder` 命中数 | 5 | 64 | +59 |
| `unresolved-reference` 世界数 | 8 | 3 | -5 |
| `unresolved-reference` 命中数 | 178 | 40 | -138 |

`unresolved-reference` 剩余世界：

- `acg-character-database`：28 次。
- `blue-archive`：8 次。
- `date-a-live`：4 次。

泛化 placeholder 宽口径剩余世界：`acg-character-database`、`akame-ga-kill`、`cross-ange`、`dantalian-no-shoka`、`date-a-live`、`gundam-seed`、`haganai`、`high-school-dxd`、`honkai-impact-3rd`、`infinite-stratos`、`madan-no-ou`、`marvel-cinematic-universe`、`naruto`、`overlord`、`rozen-maiden`、`sword-art-online`、`toriko`、`type-moon-nasuverse`、`world-god-only-knows`、`zero-no-tsukaima`。

抽样说明：泛化 placeholder 命中包含大量非风险文本或字段值，例如 `attitudeToOutsiders: "unknown"`、`source id` 中的 `sample`、README/curation-notes 中说明“模板/状态栏模板”的文字，以及 `acg-character-database` 的合法“人格模板”概念。因此该宽口径不能直接等同于 graph placeholder 风险；真正的 `referenced-placeholder` 仍为 0。

## 空 sources / conflictLog 语义状态

- 空 `source-registry.sources`：0。
- 空 `source-registry.conflictLog`：35；语义状态缺失或不合格：0。
- 空 conflictLog 世界与 Q4 一致：`absolute-duo`、`acg-character-database`、`akame-ga-kill`、`blue-archive`、`bocchi-the-rock`、`cheng-long-adventures`、`chunibyo`、`claymore`、`cross-ange`、`d-gray-man`、`gate-jsdf`、`haganai`、`hidan-no-aria`、`ikki-tousen`、`jojo`、`kaguya-sama`、`kekkaishi`、`kill-la-kill`、`majo-no-tabitabi`、`monster-hunter`、`omamori-himari`、`overlord`、`persona-5`、`rakudai-kishi`、`sekirei`、`sora-no-otoshimono`、`spice-and-wolf`、`sword-art-online`、`taimanin`、`testament-sister-new-devil`、`toaru`、`toriko`、`world-god-only-knows`、`xianjian-1`、`zero-no-tsukaima`。

## Q5 修复效果对照

- `q5-med-top`：MED 从 54 降至 51，目标世界中 `jojo` 等结构字段误引用大幅下降；但本次启发式仍在其他世界发现 51 条 MED 尾项。
- `q5-relationship-low`：目标世界的部分关系对象结构化有效，但全库 LOW 口径下仍有 287 条 `character-relationship-target` 与 8 条 `relationship-coverage`；需要继续区分“字符串标签”“群体/地点/概念 target”和真实缺 graph node。
- `q5-kg-info`：报告称 11 个目标世界补了 113 个 KG 节点；全库启发式仍有 202 条 `world-kg-coverage`。这类仍属 INFO，不阻断运行。
- `q5-unresolved-reference`：有效将 unresolved 世界从 8 降至 3、命中从 178 降至 40；但该步骤疑似在 4 个世界留下了边端点 canonical 同步回归，形成 HIGH 断链。
- `q5-text-token`：真实 `referenced-placeholder` 仍清零；泛化 placeholder 宽口径主要是说明性/字段名/合法概念命中，不建议作为阻断项。

## 是否可安全自动修复

- **可安全自动修复**：21 条 HIGH 断链可按同文件节点的 `metadata.q4SourceRiskReview.mappedId`、`label/name` 或已知 canonical id 映射，把 `edges[].from/to/source/target` 从旧中文标签同步到 `nodes[].id`。该修复不需要新增 canon，仅同步结构端点。
- **可半自动修复**：LOW `character-relationship-target` 中明显为已存在 node id、组织/地点/概念节点的，可批量结构化；但字符串关系描述和多目标语义仍需人工复核。
- **不建议盲目自动修复**：MED 的 `character-faction/location/powerSystem` 以及 `world-faction-member` 涉及是否为 display label、旧 slug、群体词或未证实 canon，应继续按 Q5 原则“不伪造 canon”。
- **INFO 可延后**：`world-kg-coverage` 是检索覆盖提示，可用最小 KG 节点补齐，但不应与断链修复混在同一批。
- **placeholder 宽口径需人工分类**：`unknown`、`sample`、`模板` 多数不是占位节点；建议拆分为“字段值 unknown”“sourceId sample”“说明性模板文本”“真实 unresolved placeholder”四类后再处理。

## 执行与校验说明

实际运行的只读命令包括：

- Node 结构扫描：统计 63 个世界、315 个 JSON；检查 parse、5 文件齐备、未知 JSON、schema、顶层字段、类型、source/evidence、edge-node、string node、duplicate node、空 sources、conflictLog 语义状态。
- Node 残留扫描：统计 MED/LOW/INFO 类别与 Top 世界；额外输出 relationship/knowledge edge-node 断链样本。
- Node token 扫描：统计 `referenced-placeholder`、泛化 placeholder、`unresolved-reference`。
- `grep -RInE` 抽样：复核泛化 placeholder 的具体语义，确认大量命中为说明性文本、字段值或 source id，而非 graph placeholder。

## 最终判定

- **P0/P1/HIGH 不再全部为 0**：P0=0、P1=0，但 HIGH=21，集中在 4 个关系图的边端点断链。
- **MED 下降**：54 → 51，小幅改善。
- **LOW/INFO 未下降**：LOW 140 → 295，INFO 200 → 202；按本次全量启发式口径，Q5 后仍需继续关系规范化与 KG 覆盖收敛。
- **unresolved 明显下降**：8 世界/178 次 → 3 世界/40 次，Q5 在该目标上有效。
- **referenced-placeholder 保持清零**；泛化 placeholder 宽口径上升但多数不是阻断风险。
- **下一轮优先级**：先自动同步 21 条 HIGH edge endpoint；再重跑 QA，确认 P0/P1/HIGH 回到 0；随后再分批处理 LOW 关系规范化和 INFO KG 覆盖。
