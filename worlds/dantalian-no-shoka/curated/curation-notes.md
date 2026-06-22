# dantalian-no-shoka curation notes

## 人工整理依据

本次仅在 `campaigns/world-library/worlds/dantalian-no-shoka/curated/` 下创建文件。已人工阅读并归纳以下现有归档：

- `campaigns/world-library/manual-curation/PLAN.md`
- `campaigns/world-library/worlds/dantalian-no-shoka/manifest.json`
- `campaigns/world-library/worlds/dantalian-no-shoka/source-registry.json`
- `campaigns/world-library/worlds/dantalian-no-shoka/world/world.json`
- `campaigns/world-library/worlds/dantalian-no-shoka/characters/characters.json`
- `campaigns/world-library/worlds/dantalian-no-shoka/factions/factions.json`
- `campaigns/world-library/worlds/dantalian-no-shoka/power-systems/power-systems.json`

规则/模板路径在当前仓库未找到（`skill/`, `rules/`, `templates/` 不存在于 `campaigns/world-library/`），因此按 `PLAN.md` 明示的标准产物与字段要求手工整理。

## 命名统一

- 主名采用：修伊·安索尼·迪斯瓦特、妲丽安、哈尔·卡姆赫德、芙兰蓓尔、拉结尔。
- aliases 保留：修·安东尼·迪斯瓦德、达利安、但他林、芙兰卑尔奇、拉洁爱尔等。
- “教授”与“哈尔”在来源中存在称谓/身份混用；curated 将焚书官哈尔和研究幻稿的教授分列，以减少 RP 运行歧义。

## 人工判断

- 默认正史采用各章节“正常剧情路线”；来源中坏结局、回溯提示与 IF 结局归为 RP sandbox，不写成既定事实。
- `characters-index.json` 已列主要人物和关键支线人物 40+ 名；第 6-8 卷部分角色仅在摘要中出现，证据等级标为 B/C。
- 幻书是核心机制，但每本幻书单独建卡会显著扩大工作量；本次仅在世界主档与人物道具字段记录关键幻书。
- 读姬、钥匙守护者、焚书官、幻书窃贼与教授/赤之读姬构成主要 RP 势力轴。

## 低置信与待补项

- 第六卷“不死杀手卫斯理/雏形”、欧立克宅邸、雷萨姆群岛海魔事件的人物细节在本轮只读到摘要，已低置信保留。
- 第七卷奥利佛、坎普森、卡德菲尔女子学校的详细 NPC 可后续逐条补齐。
- 第八卷怪盗秘银、莉菲雅、阿斯奎斯侯爵夫人的关系仍需细读完整条目。
- 幻书名称中存在中文、繁体、音译与意译混用，例如《罗惇都灵宝会元》《山河社稷图》《香神经疏》等，后续可建立 `phantom-books-index.json` 统一。

## RP 风险

- 来源中有部分血腥、精神操控、人体改造、复活腐败、家暴、血亲禁忌等黑暗内容；默认应作为哥特恐怖/悬疑元素处理，不自动露骨化。
- 自动分类中存在 NSFW 相关条目；本 curated 没有沿用露骨互动规则，只保留世界观必要的危险、恐怖与身份设定。
- 幻书能力可达城市/全球灾害级，但必须受到读者资格、媒介、仪式、代价、信息量和剧情逻辑限制，避免无成本万能化。

## 验收状态

- 已创建标准产物 7 个：README.md, world.json, source-registry.json, characters-index.json, knowledge-graph.json, relationship-graph.json, curation-notes.md。
- 未修改 raw/imports/既有自动归档文件。
- 未刷新总索引：本 step mutation scope 只允许写入 `worlds/dantalian-no-shoka/curated/`。
