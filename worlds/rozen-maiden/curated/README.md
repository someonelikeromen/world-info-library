# 蔷薇少女 curated 手工整理

状态：Batch D 手工整理完成（初版）。

来源范围：人工阅读 `world/world.json`、`characters/characters.json`、`factions/factions.json`、`power-systems/power-systems.json`、`locations/locations.json`、`reports/*` 中的归档条目；主要可追踪来源为 `src-rozen-maiden-001` / `qwsn_card.worldbook.json`，尤其“世界蓝图”“世界知识”“主要角色-画像”和各人物条目。

整理范围：箱庭式现代现实、N之领域、契约系统、爱丽丝游戏、七位蔷薇少女与媒介/制作者/敌对相关人物。

未解决问题：原归档混合正作、动画原创与 RP 扩写；蔷薇水晶、槐等动画原创条目标为 adapted/低置信；部分人物最终卷状态与沙盒初始状态冲突，初始图谱按“爱丽丝游戏进行中”处理。

2026-06-24 本地收尾：新增 `timeline-branch-index.json` 作为漫画/动画原创/沙盒初始分支入口；新增 `completion-index.json` 记录 source 覆盖、raw 分离、低置信和验证状态。

入口建议：
- `world.json`：箱庭、契约、N之领域、爱丽丝游戏与力量规则。
- `timeline-branch-index.json`：分支选择、爱丽丝游戏/N之领域/动画原创线索入口。
- `characters-index.json` / `relationship-graph.json`：蔷薇少女、媒介、人工精灵与敌对关系。
- `completion-index.json`：收尾复核和残余风险。

下一步：若需要深挖，可补全各人工精灵单独节点、按具体漫画/动画章节拆分完整时间线、为战斗评级补充逐项面板。

验证：2026-06-24 本地验证 `curated/` 下所有 JSON 均可解析；未修改 `campaigns/world-library/worlds/rozen-maiden/` 原始归档。
