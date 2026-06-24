# EVA curation notes

- 人工阅读/索引来源：campaign manifest、source-registry、分类报告、低置信/冲突报告，以及 `world/`、`characters/`、`factions/`、`locations/`、`power-systems/`、`canon-reference/` 下的归档文件。
- 来源结构：`src-evangelion-001` 为 EVA 沙盒世界书，`src-evangelion-002` 为“旧约”世界书；两者均保留在 campaign raw/imported-worldbooks，不直接搬入 curated。
- 连续性风险：TV、旧剧场、新剧场、旧约/沙盒扩写混用会造成角色状态、补完计划、NERV/SEELE 与结局冲突；curated 使用 route-lock 原则。
- 子代理状态：`r2`/`r3` Evangelion 步骤因 `Service temporarily unavailable` 中断；已改由本地工具收尾。
- 本地收尾：新增 `completion-index.json`，用于记录 read/notes/source 覆盖、raw 分离、连续性分支和 RP 启动建议。
- 验证状态：2026-06-24 本地运行 JSON parse 验证，`curated/` 下所有 JSON 均有效；未修改 campaign 原始归档。
