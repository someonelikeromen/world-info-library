# 龙珠 curation notes

- 人工判断：按 RP 使用优先整理“可操作规则”而非完整百科。
- 来源登记：主来源 `src-dragon-ball-001`，自动归档入口数 215；分类报告显示人物/能力/物种重复交叉严重。
- 冲突：剧场版异闻（布罗利、生化布罗利、邪念波、龙拳等）与主线可并存但不可默认同线。
- 低置信：自动 low-confidence 指向 unclassified 与 technical；未在初版吸收控制变量文本。
- 风险：高阶角色破坏尺度过大；RP 应明确地图耐久、复活规则与是否允许星球级攻击。
## 2026-06-22 MED 规范化补记
- `world.json` 中原字符串型 `factions`/`locations` 已规范化为 `{id,name}` 节点，并补入 `capsule-corporation`, `satan-friendly-buu-branch`, `west-city`, `king-kai-planet`, `kaioshin-realm` 等角色索引需要的安全归一节点。
- 角色 `locations`/`factions`/`powerSystems` 已改为 canonical id；原显示名保存在 `metadata.originalReferenceLabels`。
- `namekian`, `technology`, `alien-biology`, `magic` 原非 registry 标记已分别归一为明确 powerSystem id。
