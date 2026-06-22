# QA-AFTER-REPAIR-Q6A

检查日期：2026-06-22  
步骤：`qa-q6a`  
范围：`worlds/*/curated/` 下 63 个世界、315 个 curated JSON。  
执行方式：只读 Node/batch 全量扫描；未修改 `worlds/*/curated`。唯一写入文件为本报告 `manual-curation/QA-AFTER-REPAIR-Q6A.md`。

## 结论摘要

- **P0：0**。JSON parse、5 文件齐备、未知 JSON、schema mismatch、顶层必备字段缺失、类型风险、字符串 node、重复 node id 均未发现阻断项。
- **P1：0**。空 `source-registry.sources`、未注册 source/evidence、空 `conflictLog` 缺语义状态均未发现阻断项；source registry 的 `sourceId` 口径与 Q5 修正口径保持一致。
- **HIGH：0**。Q5 报告的 21 条 relationship edge endpoint 断链已清零；knowledge edge-node 断链也为 0。
- **Q5 21 HIGH 回归确认：已清零**。`blue-archive`、`monster-hunter`、`overlord`、`sora-no-otoshimono` 的 `relationship-graph.json` 中 `relationships[]` 与 `edges[]` 端点均可解析到同文件 `nodes[].id`。
- **P0/P1/HIGH 总门禁：通过**。Q6A 后阻断级别回到 `P0=0 / P1=0 / HIGH=0`。

## 扫描项目与结果

| 检查项 | Q6A 结果 |
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
| relationship edge-node 断链 | 0 |
| knowledge edge-node 断链 | 0 |
| source/evidence 未注册 | 0 |
| 空 `source-registry.sources` | 0 |
| 空 `source-registry.conflictLog` | 35 |
| 空 `conflictLog` 缺语义状态 | 0 |
| `referenced-placeholder` 世界数 | 0 |
| 泛化 `placeholder` 世界数 | 15 |
| `unresolved-reference` 世界数 | 3 |

## Q5 HIGH 断链复核

Q5 的 21 条 HIGH 集中在 4 个 relationship graph。Q6A 复核结果如下：

| 世界 | Q5 HIGH | Q6A dangling endpoints | 判定 |
|---|---:|---:|---|
| `blue-archive` | 10 | 0 | 已清零 |
| `monster-hunter` | 5 | 0 | 已清零 |
| `overlord` | 5 | 0 | 已清零 |
| `sora-no-otoshimono` | 1 | 0 | 已清零 |
| **合计** | **21** | **0** | **通过** |

复核口径：对 `relationship-graph.json` 的 `relationships[]` 与 `edges[]` 同时检查 `from`、`to`、`source`、`target`，要求端点字符串必须存在于同文件 `nodes[].id`。

## MED / LOW / INFO

本次 Q6A 的核心目标是阻断级 P0/P1/HIGH 回归确认；MED/LOW/INFO 为非阻断启发式残留统计。由于本轮仅允许写 QA 报告，未修复 MED/LOW/INFO。

| Severity | Q6A 启发式结果 |
|---|---:|
| MED | 0 |
| LOW | 687 |
| INFO | 445 |
| 合计 | 1132 |

类别分布：

- `character-relationship-target`：687。
- `world-kg-coverage`：445。

残留最多的世界（Top 30）：

| 世界 | Total | MED | LOW | INFO |
|---|---:|---:|---:|---:|
| `dantalian-no-shoka` | 64 | 0 | 64 | 0 |
| `toriko` | 58 | 0 | 46 | 12 |
| `madan-no-ou` | 52 | 0 | 52 | 0 |
| `date-a-live` | 48 | 0 | 48 | 0 |
| `cross-ange` | 41 | 0 | 31 | 10 |
| `rozen-maiden` | 37 | 0 | 26 | 11 |
| `d-gray-man` | 34 | 0 | 24 | 10 |
| `kekkaishi` | 33 | 0 | 21 | 12 |
| `gate-jsdf` | 30 | 0 | 22 | 8 |
| `ikki-tousen` | 30 | 0 | 21 | 9 |
| `sekirei` | 30 | 0 | 20 | 10 |
| `naruto` | 27 | 0 | 27 | 0 |
| `dragon-ball` | 26 | 0 | 19 | 7 |
| `honkai-impact-3rd` | 25 | 0 | 17 | 8 |
| `high-school-dxd` | 22 | 0 | 15 | 7 |
| `kimetsu-no-yaiba` | 22 | 0 | 15 | 7 |
| `danmachi` | 21 | 0 | 14 | 7 |
| `type-moon-nasuverse` | 21 | 0 | 19 | 2 |
| `kaguya-sama` | 20 | 0 | 14 | 6 |
| `omamori-himari` | 20 | 0 | 14 | 6 |
| `elemental-gelade` | 19 | 0 | 12 | 7 |
| `gundam-seed` | 19 | 0 | 13 | 6 |
| `tokyo-ghoul` | 19 | 0 | 13 | 6 |
| `absolute-duo` | 18 | 0 | 11 | 7 |
| `hidan-no-aria` | 18 | 0 | 12 | 6 |
| `evangelion` | 17 | 0 | 12 | 5 |
| `marvel-cinematic-universe` | 17 | 0 | 17 | 0 |
| `kenichi` | 16 | 0 | 10 | 6 |
| `negima-uq-holder` | 16 | 0 | 10 | 6 |
| `dungeon-fighter-online` | 15 | 0 | 9 | 6 |

说明：Q6A 的 MED/LOW/INFO 统计用于确认非阻断残留存在，不作为 Q5/Q6A 质量变化的强对比指标；Q6A 修复目标仅为 21 条 HIGH endpoint 断链。

## Placeholder / 未解析引用

| 项目 | Q6A 结果 |
|---|---:|
| `referenced-placeholder` 世界数 | 0 |
| `referenced-placeholder` 命中数 | 0 |
| 泛化 `placeholder` 世界数 | 15 |
| 泛化 `placeholder` 命中数 | 50 |
| `unresolved-reference` 世界数 | 3 |
| `unresolved-reference` 命中数 | 40 |

`unresolved-reference` 剩余世界：

- `acg-character-database`
- `blue-archive`
- `date-a-live`

泛化 placeholder 宽口径剩余世界：`acg-character-database`、`akame-ga-kill`、`cross-ange`、`gundam-seed`、`haganai`、`high-school-dxd`、`honkai-impact-3rd`、`infinite-stratos`、`marvel-cinematic-universe`、`naruto`、`rozen-maiden`、`toriko`、`type-moon-nasuverse`、`world-god-only-knows`、`zero-no-tsukaima`。

## 空 sources / conflictLog 语义状态

- 空 `source-registry.sources`：0。
- 空 `source-registry.conflictLog`：35。
- 空 `conflictLog` 缺语义状态：0。
- 空 conflictLog 世界：`absolute-duo`、`acg-character-database`、`akame-ga-kill`、`blue-archive`、`bocchi-the-rock`、`cheng-long-adventures`、`chunibyo`、`claymore`、`cross-ange`、`d-gray-man`、`gate-jsdf`、`haganai`、`hidan-no-aria`、`ikki-tousen`、`jojo`、`kaguya-sama`、`kekkaishi`、`kill-la-kill`、`majo-no-tabitabi`、`monster-hunter`、`omamori-himari`、`overlord`、`persona-5`、`rakudai-kishi`、`sekirei`、`sora-no-otoshimono`、`spice-and-wolf`、`sword-art-online`、`taimanin`、`testament-sister-new-devil`、`toaru`、`toriko`、`world-god-only-knows`、`xianjian-1`、`zero-no-tsukaima`。

## 执行与校验说明

实际运行的只读检查包括：

- JSON/schema 扫描：统计 63 个世界、315 个 JSON；检查 parse、5 文件齐备、未知 JSON、顶层对象、各标准文件关键数组字段。
- 阻断项扫描：检查 source registry、空 sources、空 conflictLog 语义状态、graph string node、duplicate node id、relationship/knowledge edge endpoint 断链。
- source/evidence 扫描：按 Q5 修正口径读取 `sourceId`/`source_id`、`sourceRefs`、`sourceReferences`、`evidence`、`evidenceSource(s)`；registry 支持 `sourceId` 与 `id`。
- 残留扫描：统计 MED/LOW/INFO 启发式类别、`referenced-placeholder`、泛化 placeholder、`unresolved-reference`。

## 最终判定

- **Q5 的 21 条 HIGH relationship edge endpoint 断链已回到 0**。
- **P0/P1/HIGH 全部为 0**：`P0=0 / P1=0 / HIGH=0`。
- **Q6A 阻断回归修复验证通过**；后续若继续处理，应转入非阻断 MED/LOW/INFO、泛化 placeholder 与 unresolved-reference 的独立批次。
