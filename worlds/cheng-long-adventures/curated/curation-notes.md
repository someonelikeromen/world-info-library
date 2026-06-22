# 成龙历险记 curation notes

## 阅读来源

- `source-registry.json`
- `raw/imported-worldbooks/成龙历险记世界 (1).worldbook.json`：已人工阅读开篇上古背景、十二符咒、寻觅符咒时代、群魔乱舞时代等条目。
- `world/world.json`、`power-systems/power-systems.json`、`factions/factions.json`、`locations/locations.json`。

## 归纳决策

- 原归档主要以时代剧情和设定说明承载信息，人物分类文件有效条目较少，因此人物清单以已读剧情条目中明确出现的人物、恶魔、组织成员整理。
- 保留原归档对圣主、十二符咒、八大恶魔、盘库宝盒、鬼影兵团和气魔法的重点。
- “圣主之外七大恶魔是否不死”等原条目提示被保留为风险，不在 curated 中强行扩展。

## 风险与验证

- JSON 为人工编写，未运行机器校验。
- 鬼影面具时代与魔气时代细节未逐条展开，后续可按单集条目补充。
- 未修改 raw/imports/既有自动归档文件。