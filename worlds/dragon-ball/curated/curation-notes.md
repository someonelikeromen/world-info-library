# 龙珠 curation notes

- 人工判断：按 RP 使用优先整理“可操作规则”而非完整百科；不导入 campaigns raw/source 文本，也不吸收 NSFW 分类内容。
- 来源登记：主来源 `src-dragon-ball-001`，自动归档入口数 215；分类报告显示人物/能力/物种重复交叉严重。
- 本轮读取：curated README/notes/world/source-registry/graphs/characters，campaign `manifest.json`、`source-registry.json`、`reports/*`、`canon-reference/timeline.json`、`canon-reference/arcs.json`、`factions/`、`locations/`、`power-systems/`、`sandbox/`、`technical/`。
- 冲突：剧场版异闻（布罗利、生化布罗利、邪念波、龙拳等）、动画原创、GT、超与 Z 主干可并存于来源，但 curated 默认不合并为同一主线。
- 低置信：自动 low-confidence 指向 unclassified、technical 与分类 `confidence` 字段；本轮只把技术文本中可作为 RP 边界的状态栏、战斗裁决、世界观过滤和金钱/资源规则转写为摘要。
- 风险：高阶角色破坏尺度过大；RP 应明确地图耐久、复活规则、仙豆/龙珠/精神时光屋获取窗口与是否允许星球级攻击。

## 2026-06-22 MED 规范化补记

- `world.json` 中原字符串型 `factions`/`locations` 已规范化为 `{id,name}` 节点，并补入 `capsule-corporation`, `satan-friendly-buu-branch`, `west-city`, `king-kai-planet`, `kaioshin-realm` 等角色索引需要的安全归一节点。
- 角色 `locations`/`factions`/`powerSystems` 已改为 canonical id；原显示名保存在 `metadata.originalReferenceLabels`。
- `namekian`, `technology`, `alien-biology`, `magic` 原非 registry 标记已分别归一为明确 powerSystem id。

## 2026-06-24 dragon-ball-finish 补记

- `timeline/story-branches.json` 已足够作为详细分支时间线；新增 `timeline/index.json` 只做入口、source entryIndex 映射和 branch selection checklist，避免复制完整事件线。
- `world.json` 扩展了 `plotArcs`、`rpNotes`、`sourceIndex`、分支限定阵营/地点/神之气系统和更明确的 combat/world rules。
- `source-registry.json` 扩展 consulted archive paths、GT/超/剧场版/disabled 条目冲突与 B 级低置信说明。
- README 更新为实际模块覆盖与 RP 启动规则：必须选 `main-db-to-z`、`gt-branch` 或 `super-branch`，并冻结 cutoffDate、角色强度、龙珠/复活/地图耐久。
- 未触碰 campaigns raw/source 文件；curated 层仍只保留摘要和索引。
