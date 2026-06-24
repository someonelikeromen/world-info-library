# 史上最强弟子兼一 curation notes

## retry-07 补完记录
- 已读取说明/登记：`campaigns/world-library/worlds/kenichi/source-registry.json`、`campaigns/world-library/worlds/kenichi/curated/README.md`、`campaigns/world-library/worlds/kenichi/curated/curation-notes.md`、`world-info-library/worlds/kenichi/curated/README.md`、`world-info-library/worlds/kenichi/curated/source-registry.json`。
- 已抽读素材：`canon-reference/arcs.json`、`canon-reference/timeline.json`、`power-systems/power-systems.json`、`factions/factions.json`、`locations/locations.json`、`sandbox/scenario-seeds.json`。
- 原始素材盘点：仅发现导入世界书 `raw/imported-worldbooks/shzqdz_card.worldbook.json` 与 `raw/original-entry-index.json`；未发现独立小说/漫画/游戏/剧本文本。
- 本批扩展：`world.json` 新增/扩展武术等级、活人拳/杀人拳、情报策略、timeline、plotArcs、factions、locations、relationships、combatRules、rpNotes。

## 人工判断
- 初版将“力量体系”定义为可跑团的武术阶层和理念冲突。
- 分开弟子级、妙手级、达人级，不允许达人随意代打。
- 新白联合适合承担情报、撤退、支援和街头秩序，而非纯战力组织。

## 低置信/待补
- 未分类 30 条未人工展开；可能含控制文本或沙盒支线。
- 绪方等暗侧成员、一影九拳细节、YOMI 具体师承需对照原条目继续校验。
- 提达特王国与一影最终决战在源中是预留/后期节点，本批仅低置信占位。

## 验证状态
- retry-07 已运行 JSON 解析验证，详见最终汇报。

## 2026-06-22 MED 规范化补记
- 已将可明确对应的 world registry 条目规范化为 canonical id，并同步更新角色字段。
- 原始显示名保存在角色 `metadata.originalReferenceLabels` 与 `normalizationNotes` 中；无法确定的条目未硬改。
- 已补入 `strategy` 以承接新岛春男的情报/策略标签。
