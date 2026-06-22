# 仙剑奇侠传Ⅰ curation notes

## 阅读来源

人工阅读/抽查了以下既有归档：

- `source-registry.json`
- `characters/characters.json`：人物条目、战力规则、部分地点与物品条目。
- `world/world.json`：世界规则与战力体系。
- `factions/factions.json`、`locations/locations.json`、`power-systems/power-systems.json`、`canon-reference/plot-summary.json`。

## 归纳决策

- 原归档中 UI 状态栏、交互规则、成人内容规则等被识别为世界书技术/叙事辅助文本，未纳入核心世界观。
- 人物清单优先收录归档 comment 中明确出现的核心人物、重要配角、单元人物与灾厄实体。
- 战力层级按原归档文本保留，但在 curated 中压缩为 RP 判定框架。
- 仙剑原著悲剧节点在本整理中均标注为“可被 RP 改写”的变量，而非强制剧情。

## 风险与待校验

- JSON 为人工编写，未运行机器校验。
- 部分人物能力与关系为对既有条目及通行设定的人工合并，需在严格 canon 场合回查原条目。
- 原归档条目存在大量跨分类重复，curated 已去重。未修改 raw/imports/自动归档文件。
