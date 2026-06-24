# 龙珠 curated 手工索引

- 状态：2026-06-24 手工扩展完成；仅整理 `world-info-library/worlds/dragon-ball/curated/`，未改动 campaigns raw/source 文件。
- 主来源：`src-dragon-ball-001`（用户提供世界书/角色卡，B 级；自动归档 215 条）。
- 读取范围：curated README/notes/world/source registry/graphs/characters，campaign `manifest.json`、`source-registry.json`、`reports/*`、`canon-reference/timeline.json`、`canon-reference/arcs.json`、`factions/`、`locations/`、`power-systems/`、`sandbox/`、`technical/`。

## 模块覆盖

- `world.json`：世界摘要、能力体系、阵营、地点、plotArcs、combatRules、timelineNotes、rpNotes、sourceIndex。
- `timeline/story-branches.json`：详细分支时间线；覆盖第一部、Z、GT、超，并标记剧场版/动画原创异闻。
- `timeline/index.json`：时间线入口与源 entryIndex 对照；结论是 story-branches 已足够，index 只做 RP 选线清单。
- `characters-index.json`：核心角色索引；仅保留主干关键角色，强度需按年代冻结。
- `knowledge-graph.json` / `relationship-graph.json`：RP 用高层关系图，不替代完整百科。
- `source-registry.json` / `curation-notes.md`：来源、冲突、低置信与操作风险记录。

## RP 启动规则

- 开局必须选择 `main-db-to-z`、`gt-branch` 或 `super-branch`，并写明 cutoffDate/dateRange。
- GT 与超默认互斥：不要同时默认启用黑星龙珠/超4/邪恶龙与神之气/破坏神/多宇宙。
- 剧场版与动画原创异闻默认是 optional side events；启用时在 session notes 标记。
- 冻结龙珠版本、复活限制、地图耐久、角色强度、可用形态、仙豆/胶囊公司/精神时光屋等战略资源。
- 外部能力体系默认禁用或转写为龙珠内部的气、科技、那美克龙族/魔导师例外。

## 未解决/风险

- 源可靠度 B，且大量时间线条目为 disabled 多选一；curated 仅提供可选分支索引。
- 战斗力/倍率可作 RP 标尺，不建议作为无校准的精确模拟。
- 高阶角色具星球级以上破坏潜力；需在桌面团规则中限定破坏尺度与复活后果。
