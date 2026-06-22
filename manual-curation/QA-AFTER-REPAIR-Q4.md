# QA-AFTER-REPAIR-Q4

检查日期：2026-06-22  
步骤：`qa-q4`  
范围：`worlds/*/curated/` 下 63 个世界、315 个 curated JSON。  
执行方式：只读 bash/Node 全量扫描；未修改 `worlds/*/curated`。唯一写入文件为本报告 `manual-curation/QA-AFTER-REPAIR-Q4.md`。

## 结论摘要

- **P0：0**。JSON parse、5 文件齐备、未识别 JSON、schema mismatch、顶层必备字段缺失、图谱 edge-node 断链、字符串节点、重复 node id 均为 0。
- **P1：0**。严格类型不匹配、扩展类型风险、未注册 source/evidence 均为 0。
- **HIGH：0**。未发现图谱断链 HIGH 或未注册 source/evidence HIGH。
- **MED/LOW/INFO：MED 54 / LOW 140 / INFO 200**。相对 R3 的 MED 332 / LOW 870 / INFO 349，三类均下降。
- **placeholder 信号下降**：`referenced-placeholder` 从 R3 的 19 个世界降为 0；泛化 `placeholder` 仅剩 2 个世界 5 次命中；另有 8 个世界含 `unresolved-reference` 风险标记。
- **仍有非阻断质量问题**：LOW 关系目标规范化、少量 MED 引用规范化、INFO KG 覆盖，以及 `unresolved-reference` 人工复核风险仍存在，但不构成 P0/P1/HIGH 阻断。

## 扫描项目与结果

| 检查项 | 结果 |
|---|---:|
| 世界目录数 | 63 |
| JSON 文件总数 | 315 |
| 每世界 5 类 JSON 齐备 | 是 |
| JSON parse 失败 | 0 |
| 未识别 JSON 文件名 | 0 |
| schema mismatch | 0 |
| 顶层必备字段缺失 | 0 |
| 严格类型不匹配 | 0 |
| 扩展运行时字段类型风险 | 0 |
| knowledge/relationship edge-node 断链 | 0 |
| graph string nodes | 0 |
| duplicate graph node ids | 0 |
| source/evidence 未注册 | 0 |
| 空 `source-registry.sources` | 0 |
| 空 `source-registry.conflictLog` | 35 |
| 空 `conflictLog` 缺语义状态 | 0 |
| `referenced-placeholder` 世界数 | 0 |
| 泛化 `placeholder` 世界数 | 2 |
| `unresolved-reference` 世界数 | 8 |

## MED / LOW / INFO 统计

| Severity | R3 后 | Q4 后 | 变化 |
|---|---:|---:|---:|
| MED | 332 | 54 | -278 |
| LOW | 870 | 140 | -730 |
| INFO | 349 | 200 | -149 |
| 合计 | 1551 | 394 | -1157 |

类别分布：

- `world-kg-coverage`：200
- `character-relationship-target`：101
- `relationship-coverage`：39
- `character-faction`：28
- `character-location`：14
- `character-powerSystem`：8
- `world-faction-member`：4

### 残留最多的世界（Top 25）

| 世界 | Total | MED | LOW | INFO | placeholder |
|---|---:|---:|---:|---:|---:|
| `jojo` | 26 | 23 | 0 | 3 | 0 |
| `type-moon-nasuverse` | 26 | 0 | 6 | 20 | 0 |
| `rozen-maiden` | 22 | 5 | 10 | 7 | 0 |
| `date-a-live` | 21 | 0 | 6 | 15 | 4 |
| `sekirei` | 20 | 2 | 12 | 6 | 0 |
| `danmachi` | 19 | 0 | 7 | 12 | 0 |
| `negima-uq-holder` | 17 | 0 | 5 | 12 | 0 |
| `dungeon-fighter-online` | 16 | 0 | 11 | 5 | 0 |
| `ikki-tousen` | 16 | 0 | 0 | 16 | 0 |
| `kekkaishi` | 16 | 0 | 0 | 16 | 0 |
| `elemental-gelade` | 15 | 7 | 2 | 6 | 0 |
| `kenichi` | 13 | 0 | 2 | 11 | 0 |
| `tokyo-ghoul` | 13 | 0 | 9 | 4 | 0 |
| `gundam-seed` | 12 | 0 | 0 | 12 | 0 |
| `kimetsu-no-yaiba` | 11 | 0 | 7 | 4 | 0 |
| `high-school-dxd` | 10 | 0 | 6 | 4 | 0 |
| `marvel-cinematic-universe` | 10 | 0 | 10 | 0 | 0 |
| `spice-and-wolf` | 10 | 2 | 2 | 6 | 0 |
| `absolute-duo` | 9 | 2 | 3 | 4 | 0 |
| `evangelion` | 9 | 0 | 5 | 4 | 0 |
| `gate-jsdf` | 9 | 0 | 9 | 0 | 0 |
| `honkai-impact-3rd` | 8 | 0 | 8 | 0 | 0 |
| `omamori-himari` | 8 | 3 | 0 | 5 | 0 |
| `kaguya-sama` | 7 | 2 | 1 | 4 | 0 |
| `persona-5` | 7 | 0 | 0 | 7 | 0 |

## Placeholder / 未解析引用

- `referenced-placeholder`：0 个世界，0 次命中；R3 为 19 个世界，已清零。
- 泛化 `placeholder`：2 个世界，5 次命中。该口径包含普通占位词或说明文字，不等同于 graph node 类型 `referenced-placeholder`。
- `unresolved-reference`：8 个世界，178 次命中；这是 Q4 placeholder 清理后保留的非阻断人工复核风险。
- 含泛化 `placeholder` 的世界：`date-a-live`、`madan-no-ou`。
- 含 `unresolved-reference` 的世界：`acg-character-database`、`blue-archive`、`cheng-long-adventures`、`monster-hunter`、`overlord`、`rakudai-kishi`、`sora-no-otoshimono`、`sword-art-online`。

## 空 sources / conflictLog 语义状态

- 空 `source-registry.sources`：0。
- 空 `source-registry.conflictLog`：35；语义状态缺失或不合格：0。
- 复核口径：允许 `conflictReviewStatus` 为对象，读取其 `status` 字段；`registryNotes` 需说明空 `conflictLog` 不等于已确认无冲突。
- 空 conflictLog 世界：`absolute-duo`、`acg-character-database`、`akame-ga-kill`、`blue-archive`、`bocchi-the-rock`、`cheng-long-adventures`、`chunibyo`、`claymore`、`cross-ange`、`d-gray-man`、`gate-jsdf`、`haganai`、`hidan-no-aria`、`ikki-tousen`、`jojo`、`kaguya-sama`、`kekkaishi`、`kill-la-kill`、`majo-no-tabitabi`、`monster-hunter`、`omamori-himari`、`overlord`、`persona-5`、`rakudai-kishi`、`sekirei`、`sora-no-otoshimono`、`spice-and-wolf`、`sword-art-online`、`taimanin`、`testament-sister-new-devil`、`toaru`、`toriko`、`world-god-only-knows`、`xianjian-1`、`zero-no-tsukaima`。

## 执行与校验说明

- 结构扫描：bash/Node 复核 63 个世界、315 个 JSON；结果为 parse/schema/top-field/missing/unknown 全 0。
- 图谱与类型扫描：bash/Node 复核类型、扩展类型、duplicate node、string node、edge endpoint；结果全 0。
- source/evidence 扫描：按 R3 口径只检查 `sourceRef`、`sourceRefs`、`sourceBasis`、`evidence`、`source.ref` 等引用字段；排除普通 `sources[]` registry 内容与内部 curated 字段依据；结果 0。
- MED/LOW/INFO 与 placeholder 扫描：bash/Node 启发式复核；统计结果见上表。

## 最终判定

- **P0/P1/HIGH 仍为 0**：Q4 修复后结构、schema、类型、图谱连通、source/evidence 注册均通过全量复核。
- **MED/LOW/INFO 已下降**：合计从 R3 的 1551 降为 394，净减少 1157。
- **placeholder 信号已下降**：`referenced-placeholder` 清零；泛化 `placeholder` 剩 2 个世界，`unresolved-reference` 剩 8 个世界。
- **仍不能判定完全无质量问题**：剩余主要是 LOW 关系目标规范化、MED world/character 引用规范化、INFO KG 覆盖，以及未解析引用风险；它们属于非阻断质量问题。
