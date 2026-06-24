# Toaru curation notes

## 手工阅读记录

- `source-registry.json`：确认唯一来源 `src-toaru-001`。
- `world/world.json`：阅读“世界观”条目，确认科学侧、魔法侧、学园都市、个人现实、宗教势力。
- `characters/characters.json`：阅读卷号条目 comments 与人物条目 comments；重点阅读上条当麻、茵蒂克丝等人物条目开头，并人工记录后续人物清单。
- `factions/factions.json`：定位魔法/科学侧势力与卷号涉及组织。

## 归纳决策

- 卷号剧情保留为“覆盖弧线”，不在正文使用卷号作为沉浸式指令。
- `[InitVar]`、变量更新、剧情规则、输出格式均排除为技术控制文本。
- “幻想杀手”“个人现实”“妹妹计划”“树状图设计者”作为知识节点，不列为人物。

## 风险

- 源覆盖主要为旧约前中期与部分角色卡，不代表全系列完整设定。
- 个别译名按源文件保留。

## 验证状态

- retry-13 新增 `completion-expansion.json`，覆盖人物、势力、旧约早期时间线、篇章、能力体系、关系和 RP notes。
- 2026-06-24 运行 Python `json.load` 校验本目录全部 JSON：通过。