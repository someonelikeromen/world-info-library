# Curation notes - zero-no-tsukaima

## 人工阅读来源

- `campaigns/world-library/worlds/zero-no-tsukaima/source-registry.json`
- `campaigns/world-library/worlds/zero-no-tsukaima/world/world.json`
- `campaigns/world-library/worlds/zero-no-tsukaima/characters/characters.json`
- `campaigns/world-library/worlds/zero-no-tsukaima/factions/factions.json`
- `campaigns/world-library/worlds/zero-no-tsukaima/locations/locations.json`
- `campaigns/world-library/worlds/zero-no-tsukaima/power-systems/power-systems.json`

## 归纳决策

- 将哈尔凯尼亚、双月、贵族/平民阶级、四元素魔法、虚无魔法、使魔系统作为世界骨架。
- `{{user}}` 在源中作为召唤出的异界使魔/RP 玩家对象反复出现；curated 不把它固化为原作人物，而在关系图中保留 `user-familiar` 槽位。
- 人物索引列入：露易丝、塔巴莎、蒂法妮娅、丘鲁克、基修、蒙莫朗西、朱力欧、谢斯塔、安丽埃塔、约瑟夫、谢菲尔德、约赛特、威尔士、欧斯曼、阿尼埃斯、艾蕾欧诺尔、卡特莉亚。
- “日耳曼尼亚王国”“托里斯汀魔法学院”等被自动分入 characters 的非人物条目，curated 放入 world/knowledge graph 而非人物索引。

## 排除内容

- `格式`、`chat状态栏`、提示模板、技术控制文本不作为世界观。
- 成人化/NSFW 描写被剔除，仅保留 SFW 身份、能力、关系与剧情功能。

## 风险

- 源内部分 XML 标签不闭合或命名异常，curated 按可读文本人工归纳。
- JSON 未运行机器解析校验。
