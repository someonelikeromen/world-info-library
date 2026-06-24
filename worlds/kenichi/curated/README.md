# 史上最强弟子兼一 curated 手工索引

状态：retry-07 补完。来源范围：读取 campaigns 与 curated 的 `README.md`、`curation-notes.md`、`source-registry.json`，并抽读 `canon-reference/*`、`power-systems/`、`factions/`、`locations/`、`sandbox/` 分类归档。主来源：`src-kenichi-001` / `shzqdz_card.worldbook.json`。

## 原始素材盘点
- `campaigns/world-library/worlds/kenichi/raw/imported-worldbooks/shzqdz_card.worldbook.json`：导入世界书全文。
- `campaigns/world-library/worlds/kenichi/raw/original-entry-index.json`：原始条目索引。
- 未发现独立小说原文、漫画原文、游戏原文或剧本长文；存在大量世界书条目、角色/能力/势力分类归档和控制/沙盒文本。

## 已整理模块
- `world.json`：扩展武术能力体系、等级、timeline、plotArcs、factions、locations、relationships、combatRules、rpNotes。
- `knowledge-graph.json` / `relationship-graph.json`：保留既有最小图谱，本批未重写。
- `source-registry.json`：保留既有冲突记录，继续标注混入控制/沙盒/NSFW 文本风险。

## 可扩展模块
- 可继续把具体招式、师承、YOMI 成员和一影九拳拆成 `power-systems`/`relationships` 细表。
- 283 条主来源中仍有未分类条目，需区分 canon、原创支线、控制文本和污染内容。
- 提达特王国、一影最终决战等后期节点已保留低置信占位，待细校。
