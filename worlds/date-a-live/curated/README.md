# 约会大作战 / DATE A LIVE — curated 档案

## 整理状态

- 状态：已补齐 curated 标准产物。
- 世界 ID：`date-a-live`
- 默认基线：以《约会大作战》主线世界观为基准，兼容来源世界书中的 RP 沙盒入口与《Date A Live Fragment: Date A Bullet / 临界》相关支线人物。
- 整理日期：2026-06-22

## 本目录文件

- `world.json`：世界基础信息、规则、力量体系、势力、地点与事件。
- `source-registry.json`：手工整理使用的来源登记与冲突说明。
- `characters-index.json`：详细人物清单与索引。
- `knowledge-graph.json`：概念、势力、地点、事件、能力的知识图谱。
- `relationship-graph.json`：人物/势力关系图谱。
- `curation-notes.md`：人工判断、冲突、低置信项与后续建议。

## 阅读来源范围

已人工阅读/抽查以下既有归档：

- `campaigns/world-library/manual-curation/PLAN.md`
- `campaigns/world-library/worlds/date-a-live/manifest.json`
- `campaigns/world-library/worlds/date-a-live/source-registry.json`
- `campaigns/world-library/worlds/date-a-live/world/world.json`
- `campaigns/world-library/worlds/date-a-live/characters/characters.json`
- `campaigns/world-library/worlds/date-a-live/factions/factions.json`
- `campaigns/world-library/worlds/date-a-live/power-systems/power-systems.json`
- `campaigns/world-library/worlds/date-a-live/locations/locations.json`
- `campaigns/world-library/worlds/date-a-live/canon-reference/plot-summary.json`

注：`PLAN.md` 中列出的 `skill/`、`rules/`、`templates/` 路径在当前仓库未发现；本次按 `PLAN.md` 明示标准产物和字段手工整理。

## 整理摘要

本世界的 RP 运行核心是：空间震与精灵灾害、精灵封印、以约会/情感稳定替代歼灭、Ratatoskr 与 DEM/AST 的立场冲突、始源精灵崇宫澪引发的长期因果，以及邻界支线的准精灵生存竞争。

主要势力包括：

- 精灵与被封印精灵群体
- Ratatoskr / Fraxinus
- AST 对精灵部队
- DEM Industry
- 普通学校与城市社会
- 邻界准精灵群体

主要机制包括：

- 精灵、灵力、灵结晶、灵装
- 天使与魔王/反转
- 空间震
- 显现装置与 CR-Unit
- 五河士道的封印能力与亲密度/精神稳定机制
- 邻界、准精灵、空无与白之女王相关机制

## 未解决问题

- 来源是单一用户导入世界书，且含大量 RP 扮演指令、状态栏模板和成人向分类；curated 仅保留世界观与人物必要设定，不沿用露骨内容。
- 来源中存在“你是同班同学 / DEM BOSS / 士道 / 真士转生”等玩家身份分支，本次不写入默认正史，仅作为 sandbox/可选入口记录。
- “士织”既是士道女装/变身身份，也被某些条目标为精灵化/分身；curated 中作为五河士道的变体身份处理。
- 临界/Date A Bullet 支线资料在来源中偏摘要级，相关人物证据等级低于主线精灵。

## 下一步建议

1. 如需更高精度，补充轻小说卷别/动画季别/官方设定集来源。
2. 将主线、IF 分支、临界支线分层建立运行配置。
3. 若要刷新全局索引，应由拥有 `manual-curation/` 写权限的步骤修改总索引；本 step mutation scope 仅允许写入本 `curated/` 目录。