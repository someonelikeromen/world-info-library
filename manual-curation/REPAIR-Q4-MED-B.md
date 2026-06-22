# REPAIR-Q4-MED-B

日期：2026-06-22  
步骤：`med-normalization-q4b`  
范围：`high-school-dxd`、`kimetsu-no-yaiba`、`tokyo-ghoul`、`dungeon-fighter-online`、`honkai-impact-3rd`、`marvel-cinematic-universe`、`naruto`、`madan-no-ou`。

## 目标

根据 `manual-curation/QA-AFTER-REPAIR-R3.md` 的 MED 次优先世界 B，清理以下启发式质量项：

- `character-location`
- `character-faction`
- `world-faction-member`
- `character-powerSystem`

原则：只做可证实的 world 层 `id` / display name 对齐；不新增或伪造 canon；不能确定的原标签移入 `metadata.originalReferenceLabels` 并写入 `normalizationNotes`。

## 处理策略

- 对 `characters-index.json` 中角色的 `factions` / `locations` / `powerSystems`：
  - 若值不能解析到同世界 `world.json` 的对应 world 层 id，则从角色字段移除。
  - 原标签保留在 `metadata.originalReferenceLabels.<field>`。
  - 添加 `normalizationNotes`，说明 `unresolved (no safe canonical id)`。
- 对 `world.json` 中 faction 的 `knownMembers`：
  - 若成员值不能解析到 `characters-index.json.characters[].id`，则从 `knownMembers` 移除。
  - 原标签保留在 faction 的 `metadata.originalReferenceLabels.knownMembers`。
  - 添加 `normalizationNotes`，说明该标签不在角色索引 id 中。
- 同步 `characters-index.json.indices.byFaction`、`byPowerSystem`、`byVisibility`、`majorCharacters`，避免规范化字段与索引不一致。

## 逐世界结果

| World | 处理结果 |
|---|---|
| `high-school-dxd` | `azazel` 的未解析 faction/location 原标签保留到 notes；`three-factions.knownMembers` 中未建档 `michael` 移入 notes。 |
| `kimetsu-no-yaiba` | 角色未解析 location 标签（如 `大正日本`、`炭治郎身边`、`鬼杀队`、`潜伏处`）移入 notes；未建档成员 `shinobu-kocho`、`kokushibo`、`rui` 移入 notes。 |
| `tokyo-ghoul` | 角色未解析 location/faction 标签（如 `东京`、`CCG`、`v-organization`）移入 notes；未建档 `juuzou-suzuya` 移入 notes。 |
| `dungeon-fighter-online` | 角色未解析 location 标签（如 `阿拉德`、`旅店/城镇`、`黑色大地` 等）移入 notes；`emperor-faction` 移入 faction notes。 |
| `honkai-impact-3rd` | 未解析角色字段与未建档 faction members（如 `welt-yang`、`tesla`、`einstein`、`jackal`、`raven`）保留为 notes。 |
| `marvel-cinematic-universe` | 未解析/未建档 faction members（如 `clint-barton`、`nick-fury`、`phil-coulson`、`winter-soldier`、`loki`、`stephen-strange`）保留为 notes；角色字段索引同步。 |
| `naruto` | 未解析角色字段保留为 notes；未建档 faction members `konan`、`kisame-hoshigaki` 保留为 notes。 |
| `madan-no-ou` | 保留既有已规范化条目；`roland.powerSystems: 杜兰达尔` 与 `eugene.factions: 王室` 等无法安全映射项保持 unresolved notes；索引同步。 |

## 复核

执行目标类别复核脚本，检查 8 个世界中：

- 角色 `factions` 是否全部解析到 `world.factions[].id`。
- 角色 `locations` 是否全部解析到 `world.locations` id/字符串。
- 角色 `powerSystems` 是否全部解析到 `world.powerSystems[].id`。
- world faction `knownMembers` 是否全部解析到 `characters-index.characters[].id`。

结果：`target direct MED category mismatches: 0`。

JSON 解析复核：8 个世界的 `world.json` 与 `characters-index.json` 共 16 个文件均可 `JSON.parse`，结果 `JSON parse OK: 16 files`。

Placeholder 复核：目标 8 世界未检出 `referenced-placeholder`。

## 剩余非阻断问题

- 本轮只处理目标 4 类 MED 规范化信号；未处理 `LOW` 的 relationship target/coverage 与 `INFO` 的 KG coverage。
- 多个原标签是可信世界事实但当前缺少 world 层 canonical id 或角色索引 id；已按约束记录在 `normalizationNotes`，未新增 canon。
- 由于目标 JSON 原本多为单行，程序化保存后转为多行格式；内容变更集中于规范化字段、notes 与索引同步。
