# Curation notes - GATE

## 人工判断
- `src-gate-jsdf-001` 角色名录非常完整，可信度按源注册表为 B；本次以人物名录、派系、地点、力量体系交叉阅读后提炼。
- 现代军事 vs 奇幻生态是核心冲突；战力评估不采用单一等级，而按战略投送/局部遭遇分别处理。
- 源内 NSFW/交互/玩家身份控制项不纳入 curated 主体。

## 冲突与低置信
- 日文/中文译名存在多写法：萝莉/罗莉、杜嘉/杜卡、索沙尔/佐尔札尔等；本档采用源文件中文写法为主。
- 外传使徒与海自后续未完全展开，标为 medium 或 notes。

## 可追踪来源
- `campaigns/world-library/worlds/gate-jsdf/manifest.json`
- `campaigns/world-library/worlds/gate-jsdf/source-registry.json`
- `campaigns/world-library/worlds/gate-jsdf/characters/characters.json`
- `campaigns/world-library/worlds/gate-jsdf/world/world.json`

## 2026-06-22 MED 规范化补记
- `world.json` 中原字符串型 `factions`/`locations` 已规范化为 `{id,name}` 节点，并补入 `special-region`, `apostles`, `kato-students` 等角色索引需要的安全归一节点。
- 角色 `locations`/`factions`/`powerSystems` 已改为 canonical id；原显示名保存在 `metadata.originalReferenceLabels`。
- `political`、`martial` 这类原非 registry 标记被归入非超自然能力节点 `political-authority`、`martial-training`，避免误作魔法体系。

## 2026-06-24 retry-05 补完
- 补第三侦查队、蔷薇骑士、暗黑精灵、帝都黑街人物；扩展阿尔努斯共同体、地球列强干涉、黑街复仇和封门后重建模块。
- 低置信：雪莉/菅原线、海自外传、贝尔纳戈与诸神使徒谱系。
