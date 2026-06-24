# Taimanin curation notes

## 阅读来源
- `source-registry.json`：确认唯一源 `src-taimanin-001`，标题“0010对魔忍”。
- `world/world.json`：阅读水城不知火、世界设定、五车学园条目。
- `characters/characters.json`：阅读/定位秋山凛子、高坂静流、井河阿莎姬、水城雪风、水城不知火、五车学园，以及源内状态栏/玩家怪物设定。

## 处理决策
- 对魔忍原素材和源世界书存在大量成人向内容；curated 层只做 SFW 世界观整理。
- `{{user}}` 寄生魔、`{{user}}状态栏`、`NPC状态栏` 明确列入 excludedEntries，不作为世界观或人物索引。
- 五车学园虽非人物，但源中在 characters 分类出现且是重要机构，因此在 characters-index 末尾标注为“非人物但核心机构”。

## 风险
- 源文件角色数量较少，且部分设定是世界书改写版本；后续如有官方向归档可再拆分版本。
- 不知火“现状”涉及堕落/魔化等成人向语境，curated 仅保留任务失败后魔化这一剧情事实。

## 验证状态
- 已创建 7 个 curated 标准文件。
- retry-13 新增 `completion-expansion.json`，覆盖人物、势力、时间线、篇章、能力体系、关系和 RP notes。
- 2026-06-24 运行 Python `json.load` 校验本目录全部 JSON：通过。