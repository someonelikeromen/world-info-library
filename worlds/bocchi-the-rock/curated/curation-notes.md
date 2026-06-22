# Curation notes - bocchi-the-rock

## 人工阅读来源

- `campaigns/world-library/worlds/bocchi-the-rock/source-registry.json`
- `campaigns/world-library/worlds/bocchi-the-rock/characters/characters.json`
- `campaigns/world-library/worlds/bocchi-the-rock/world/world.json`
- `campaigns/world-library/worlds/bocchi-the-rock/factions/factions.json`
- `campaigns/world-library/worlds/bocchi-the-rock/locations/locations.json`
- `campaigns/world-library/worlds/bocchi-the-rock/reports/unclassified-entries.json`
- `campaigns/world-library/worlds/bocchi-the-rock/characters/character-voice.json`

## 归纳决策

- 自动分类把山田凉、喜多郁代等人物分散到 factions/locations/species/voice 与 unclassified；curated 层按人工阅读内容统一归入人物索引。
- “纽带乐队（結束バンド）由吉他手后藤独、鼓手兼队长伊地知虹夏、贝斯手山田凉、主唱兼吉他手喜多郁代组成”作为乐队构成核心依据。
- 伊地知星歌虽非乐队成员，但源中为虹夏姐姐与 STARRY 店长，是场景结构关键人物，列入索引。

## 排除内容

- 未纳入与乐队/校园无关的自动分类误判。
- 未把喜剧化心理夸张当作超自然能力。

## 风险

- 源中后藤独独立条目较短，主要通过“小波奇”昵称与乐队构成条目追踪。
- JSON 未运行机器解析校验。
