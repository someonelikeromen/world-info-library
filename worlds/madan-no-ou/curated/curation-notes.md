# 魔弹之王与战姬 curated notes

## 处理范围
- 仅人工阅读并归纳 `manifest.json`、`world/world.json`、`characters/characters.json`、`factions/factions.json`、`locations/locations.json`、`power-systems/power-systems.json`、`assets/items.json`、`graphs/*`、`reports/*` 与既有 `curated/README.md`。
- 未修改 `raw/`、`imports/raw/`、既有自动归档文件。
- 本次 curated 目标是补齐标准产物，而不是重新抽取原始正文。

## 主要判断
1. **本篇主线为默认 canonical main**
   - 以《魔弹之王与战姬》本篇为默认事实线。
   - 艾莲俘虏堤格尔、布琉努内乱、亚斯瓦尔王位内战、第二次布琉努内乱、吉斯塔特内乱、圣窟宫终局可串成默认时间线。

2. **冻涟 IF 需单独标注**
   - 世界书明确写出《魔弹之王与冻涟的雪姬》模式说明。
   - 米拉、拉娜、堤格尔父亲是否存活等内容与本篇存在分支差异，不能无标注混写。
   - 因此 `world.json` 中使用 `alternateContinuities` 记录，不在主线中强行融合。

3. **七战姬为政治军事领袖，不是纯感情附庸**
   - 归档中反复强调：不能把战姬简化为后宫花瓶。
   - curated 的人物索引与关系图均按独立领袖处理。

4. **黑弓与蒂尔·纳·法应默认高保密**
   - 黑弓真实来历、降临容器机制、魔物对黑弓持有者的特殊看待均属于隐藏真相。
   - 在人物索引与图谱里相关节点使用 `gm-only`，避免把剧透当公开常识。

5. **凡伦蒂娜与后期圣窟宫事件属 GM-only**
   - 她的王位野心、吉斯塔特内乱、与卢斯兰/米莉兹/魔物的关联，属于后期剧情核弹。
   - 在 curated 中保留，但标记为 GM-only，便于 RP 侧控制揭露节奏。

## 低置信/待补
- `巴多兰`、`葛雷亚斯特`、`撒迦利亚国王`、`尤金王子`、`琉蒂`、`桂妮薇亚` 等条目：已确认存在，但目前仅能从标题或分散信息判断身份，后续应逐条回看卷别相关条目补足。
- `米莉兹/米莉札`：归档里存在译名浮动，待后续统一。
- `乌鲁斯·冯伦`：本篇与冻涟 IF 线的父亲存活状态不同，需在后续使用时依模式选用。
- `拉娜·露利叶`：本篇与 IF 线状态冲突明显，已在人物表中 private 处理。

## 风险提示
- 由于源世界书同时覆盖本篇与 IF 线，后续若扩展到剧情生成，应先确定使用哪条 continuity。
- 若要进一步充实知识图谱，可从 `canon-reference/*.json` 中逐卷补事件节点，但仍需人工阅读，不可脚本抽正文。

## 当前完成度
- 已补齐标准产物：`world.json`、`source-registry.json`、`characters-index.json`、`knowledge-graph.json`、`relationship-graph.json`、`curation-notes.md`。
- `README.md` 仍需保持并说明来源与整理状态，作为 curator 入口。

## 2026-06-22 MED 规范化补记
- 已将角色索引中的地点/势力/能力显示名尽量改为 `world.json` 内 canonical id，并在角色 `metadata.originalReferenceLabels` 保留原显示名。
- 为可安全确认但原世界注册表缺少 id 的公国驻地、家族/王室、银色流星军、魔物相关能力等补入 `normalization-stub` 节点，标明需后续补强。
- `亚尔萨斯` 作为 character-faction 时按“亚尔萨斯领/冯伦领民共同体”补入 `alsace-domain`；未强行伪造的残留仅包括：`杜兰达尔` 是 artifact 而非 powerSystem；`王室` 未能安全判定所属王室。以上保留在角色 `normalizationNotes`。
