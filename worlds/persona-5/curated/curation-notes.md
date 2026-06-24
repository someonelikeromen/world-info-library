# Persona 5 curation notes

## 阅读来源

- `source-registry.json`
- `characters/characters.json`：人工检视了世界观、地点、认知世界、人格面具、阴影、天鹅绒房间、时间线，以及 Joker、坂本龙司、高卷杏、摩尔加纳、喜多川祐介、新岛真、佐仓双叶、奥村春、明智吾郎、芳泽霞/堇、丸喜拓人、协助者等 comment 条目。
- `world/world.json`、`locations/locations.json`、`power-systems/power-systems.json`、`factions/factions.json`。
- `canon-reference/timeline.json`、`canon-reference/arcs.json`、`canon-reference/plot-summary.json`：用于补充 `timeline-index.json` 的 P5R 月份流程、殿堂目标、Royal 条件、异世界导航 App、Coop/时间管理与组织势力索引。

## 归纳决策

- 以 P5R 为主，保留第三学期、丸喜拓人、芳泽霞/堇、吉祥寺等 Royal 内容。
- 人物清单分为怪盗团、P5R 关键人物、天鹅绒房间、协助者、殿堂目标/反派。
- 新增 `timeline-index.json` 作为 compact RP module：不复制完整剧情文本，只索引章节、殿堂/预告信/期限、Royal 第三学期门槛、Confidant 功能、Metaverse 规则和场景钩子。
- 原归档中的格式、音乐、SD 提示词、游戏面板等非世界观条目未纳入核心 curated。

## 风险与验证

- 归档分类报告显示 preserved entries 59、unclassified 0；但多个源条目 confidence 为 C，且时间线条目自称“只参考”，因此 `timeline-index.json` 标注为 RP 索引而非独立正史校验。
- `source-registry.json` 的 `conflictLog` 仍为空且 `conflictReviewStatus.status` 为 `not-reviewed`；当前只确认没有登记具体冲突，不声明无冲突。
- 部分殿堂目标只列主线关键代表，未穷尽所有支线委托目标。
- 未修改 raw/imports/既有自动归档文件或 campaigns 源文件。