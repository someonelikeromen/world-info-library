# DFO RP notes

## 使用边界

- 默认时间锚点可放在阿拉德历990年前后：冒险家救出赛丽亚、格兰之森异变、早期地下城调查，便于低等级开局。
- 若从后期篇章开始，先声明主线阶段：天界/安徒恩、寂静城/魔界、希洛克复活、第二次暗黑圣战、机械崛起/神界。
- 使徒不是统一阵营小队；每个使徒的动机、灾害方式、可沟通性和讨伐条件都要单独处理。
- 职业强度不要只按职业名判断；需同时看等级、转职、觉醒、装备、剧情时期、队伍支援和副本机制。
- 本轮没有逐条清洗 197 个 powerSystems 与 318 个 abilities；具体职业技能若未在 curated 中出现，应回查源档再使用。

## 推荐开局切片

1. **艾尔文防线开局**：玩家作为新晋冒险家救援赛丽亚，调查格兰之森异变和大魔法阵异常。
2. **西海岸远征**：从天空之城、天空之海、天帷巨兽与GBL幸存者切入罗特斯篇。
3. **诺伊佩拉瘟疫调查**：在人类与暗精灵误会升级前查明狄瑞吉幻影，兼顾外交和治疗剂。
4. **天界战争线**：从登上天界、皇女艾丽婕救援、卡勒特战争或能源中心安徒恩切入。
5. **魔界盟会线**：以魔法组织竞争、佧修派袭击和黑暗之眼为主，适合中高阶角色。
6. **黑色大地线**：围绕卡赞遗体、伪装者、黑暗教团、奥兹玛与雷米迪亚内部冲突推进。
7. **神界远征线**：作为高阶后期篇章，重点是白海、晴烟、迷雾高原和索利达里斯冲突。

## 冲突与低置信处理

- 源归档多项 `confidence=C`，curated 文件只做结构化摘要，不提升为绝对正史。
- 发现版本差异、职业技能不确定、NPC定位差异时，记录到 `curation-notes.md` 或 `source-registry.json` 的 conflictLog。
- 不把 `canon-reference/plot-summary.json` 中的状态栏/界面模板当作世界设定；已仅作为 technical/UI 源，不纳入 lore。
- 玩家若改变重大节点，记录为沙盒分歧，不覆盖 canonical timeline。

## 需要回查的源文件

- 时间线：`campaigns/world-library/worlds/dungeon-fighter-online/canon-reference/timeline.json`
- 篇章/使徒条目：`campaigns/world-library/worlds/dungeon-fighter-online/canon-reference/arcs.json`
- 人物：`campaigns/world-library/worlds/dungeon-fighter-online/characters/characters.json`
- 阵营：`campaigns/world-library/worlds/dungeon-fighter-online/factions/factions.json`
- 地点：`campaigns/world-library/worlds/dungeon-fighter-online/locations/locations.json`
- 能力：`campaigns/world-library/worlds/dungeon-fighter-online/power-systems/abilities.json`
