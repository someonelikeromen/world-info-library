# REPAIR-Q4-PLACEHOLDERS

检查日期：2026-06-22  
步骤：`placeholder-review-q4`  
范围：`manual-curation/QA-AFTER-REPAIR-R3.md` 点名的 19 个 `referenced-placeholder` 世界。

## 目标

在 P0/P1/HIGH 已为 0 的基础上，复核 19 个世界 `relationship-graph.json` 中由结构修复遗留的 `referenced-placeholder` 节点。能映射到真实 curated 条目的节点改为真实节点类型；不能安全映射的节点改为显式风险状态，避免运行时误认为已核实来源。

## 处理口径

- 精确匹配 `characters-index.characters[].id` 的节点：改为 `type: "character"`。
- 唯一匹配 `characters-index.characters[].name / aliases / codename` 的节点：节点 id 规范化为角色 id，同时同步改写 `relationships[]` / `edges[]` 的 `from/to`。
- 精确或唯一匹配 `knowledge-graph.nodes[].id / label / name` 的节点：改为 KG 节点原类型，并同步必要端点。
- 无法唯一匹配到 characters/KG 的节点：改为 `type: "unresolved-reference"`，并写入 `metadata.q4SourceRiskReview.status = "unresolved-reference-risk"`、`sourceVerification = "not-verified"`、`runtimeUse = "structural-edge-endpoint-only"`。
- 未伪造 sourceId；未把不可证实节点补注册为真实来源。

## 修复统计

| 世界 | 已映射 | 未解析风险 |
|---|---:|---:|
| `acg-character-database` | 1 | 14 |
| `akame-ga-kill` | 14 | 0 |
| `blue-archive` | 5 | 14 |
| `cheng-long-adventures` | 11 | 1 |
| `claymore` | 15 | 0 |
| `infinite-stratos` | 12 | 0 |
| `kill-la-kill` | 12 | 0 |
| `majo-no-tabitabi` | 8 | 0 |
| `monster-hunter` | 3 | 10 |
| `overlord` | 1 | 13 |
| `persona-5` | 0 | 0 |
| `rakudai-kishi` | 0 | 12 |
| `sora-no-otoshimono` | 1 | 12 |
| `sword-art-online` | 0 | 13 |
| `taimanin` | 13 | 0 |
| `testament-sister-new-devil` | 16 | 0 |
| `toaru` | 0 | 0 |
| `world-god-only-knows` | 0 | 0 |
| `xianjian-1` | 16 | 0 |
| **合计** | **128** | **89** |

说明：`persona-5`、`toaru`、`world-god-only-knows` 在本轮复核时已无 `referenced-placeholder` 节点，仅纳入验证统计。

## 主要改动

- 修改 19 个授权世界的 `worlds/*/curated/relationship-graph.json`。
- 将可证实节点写入 `metadata.q4SourceRiskReview.status = "resolved-by-curated-index-match"`，记录 `originalId`、`mappedId`、`mappedKind` 与 `reviewStep`。
- 将不可证实节点改为 `unresolved-reference`，明确 `sourceVerification: "not-verified"`，保留结构端点但阻止运行时误读为已核实事实。
- 未修改 `source-registry.json`：本轮没有发现可安全新增的真实外部 sourceId，也不应伪造来源注册。

## 残余风险

仍有 89 个 `unresolved-reference` 节点，集中在：

- `acg-character-database`：跨作品簇、系列/角色组 id 缺少对应 KG 或角色条目。
- `blue-archive`：部分组织/集合名与 KG/角色索引无法唯一对应。
- `monster-hunter`：职业、生态、区域角色槽多为泛化角色或集合，不适合作为已核实固定角色。
- `overlord`：大量中文显示名未能唯一映射为现有角色 id，或为集合节点。
- `rakudai-kishi`、`sora-no-otoshimono`、`sword-art-online`：当前 relationship 图节点与 characters-index/KG 的 id/名称规范仍需后续人工对齐。

这些是非阻断质量风险；它们已明确标注为未核实结构端点，不再作为已确认来源事实暴露。

## 验证结果

执行只读复核脚本确认：

- 19 个世界的 `source-registry.json`、`characters-index.json`、`knowledge-graph.json`、`relationship-graph.json` 均可 `JSON.parse`。
- 19 个世界关系图中 `relationships[]` / `edges[]` 的 `from/to` 均能解析到同文件 `nodes[].id`；断链数为 0。
- 全库扫描 `referenced-placeholder`：0 命中。
- 全库扫描泛化 `placeholder` 仍有范围外既有命中：`date-a-live` 的 `aggregate-placeholder` 与 `madan-no-ou` notes 中的说明文字；本步骤未获授权修改这些世界。

## 最终判定

- R3 点名的 19 个 `referenced-placeholder` 世界已完成 Q4 复核与清理。
- `referenced-placeholder` 信号已清零。
- 仍存在 89 个非阻断 `unresolved-reference` 风险节点，需要后续人工补齐真实 characters/KG 映射或注册可信 sourceId 后再转正。
