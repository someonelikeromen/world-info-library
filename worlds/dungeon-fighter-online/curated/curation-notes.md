# DFO curation notes

- 人工阅读导入 README、分类报告、manifest、canon timeline/arcs、factions、locations、power-systems、abilities、现有 curated 图谱。
- r1 补跑采用拆分模块方式完成：`timeline.json`、`plot-arcs.json`、`factions.json`、`locations.json`、`power-systems.json`、`relationships.json`、`lore.json`、`rp-notes.md`，并重建 `knowledge-graph.json` / `relationship-graph.json`。
- 人物索引从“冒险家/赛丽亚/三使徒/卡赞”扩展到赫尔德、罗特斯、狄瑞吉、安徒恩、卢克、卡恩、普雷、卡西利亚斯、米歇尔、艾泽拉·洛伊等关键节点。
- 源归档大量条目为 `confidence=C`，本轮只做结构化摘要，不把低置信素材提升为绝对正史；对应来源和冲突已写入 `source-registry.json`。
- `canon-reference/plot-summary.json` 当前是状态栏/界面规则模板，不作为剧情摘要或世界 lore 使用。
- 职业与版本跨度极大，战斗评级必须按职业、转职、觉醒、装备、剧情阶段单独建模；本轮未逐条清洗 197 个 powerSystems 和 318 个 abilities。
- 仍未完整展开所有职业导师、地区领主、NPC语音、NSFW条目、装备/物品、种族与神界细分社会结构；使用时需回查 campaign 源档。
