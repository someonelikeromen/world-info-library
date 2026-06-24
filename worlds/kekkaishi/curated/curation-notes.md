# 结界师 curation notes

## retry-07 补完记录
- 已读取说明/登记：`campaigns/world-library/worlds/kekkaishi/source-registry.json`、`campaigns/world-library/worlds/kekkaishi/curated/README.md`、`campaigns/world-library/worlds/kekkaishi/curated/curation-notes.md`、`world-info-library/worlds/kekkaishi/curated/README.md`、`world-info-library/worlds/kekkaishi/curated/source-registry.json`。
- 已抽读素材：`canon-reference/arcs.json`、`canon-reference/timeline.json`、`power-systems/power-systems.json`、`factions/factions.json`、`locations/locations.json`、`sandbox/scenario-seeds.json`。
- 原始素材盘点：仅发现导入世界书 `raw/imported-worldbooks/jjs_card.worldbook.json` 与 `raw/original-entry-index.json`；未发现独立小说/漫画/游戏/剧本文本。
- 本批扩展：`world.json` 新增/扩展结界术细则、乌森规则、妖犬搭档、timeline、plotArcs、factions、locations、relationships、combatRules、rpNotes。

## 人工判断
- 把乌森之地作为地点兼力量节点，而非单纯地点。
- 结界术记录为可操作规则：定位、成形、封锁、消灭。
- 间时守、守美子、宙心丸相关线保持 GM-only/待补，避免过早公开。
- 日常→巡逻→遭遇→结界战→清理→日常后果是推荐 RP 节奏。

## 低置信/待补
- 夜行大量成员只列核心，细部能力需再读条目。
- 黑芒楼人物译名按源条目合并，后续可对照官方译名。
- 宙心丸未单列成角色，留待后期剧情校对。
- 扇家线、里会干部和后期政治结构尚未完全拆索引。

## 来源追踪
- 主要依据：`src-kekkaishi-001`；分类报告显示 100 条已完整归档。

## 验证状态
- retry-07 已运行 JSON 解析验证，详见最终汇报。

## 2026-06-22 MED 规范化补记
- 已将可明确对应的 world registry 条目规范化为 canonical id，并同步更新角色字段。
- 原始显示名保存在角色 `metadata.originalReferenceLabels` 与 `normalizationNotes` 中；无法确定的条目未硬改。
