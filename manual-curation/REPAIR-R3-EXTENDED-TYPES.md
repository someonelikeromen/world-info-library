# REPAIR-R3-EXTENDED-TYPES

修复日期：2026-06-22  
范围：第三轮定向修复 `manual-curation/QA-AFTER-REPAIR-R2.md` 中“非阻断扩展类型风险”的 6 项。  
约束：只做类型兼容迁移，保留原值，不扩写正文。

## 修复内容

### `characters-index.json:notCompleteCanonRoster`

以下布尔值字段已迁移为对象形态，并在 `enabled` 中保留原布尔值：

- `worlds/blue-archive/curated/characters-index.json`
  - 顶层 `notCompleteCanonRoster: true` → `{ "enabled": true, "summary": "", "notes": [] }`
  - `runtimeUseGate.notCompleteCanonRoster: true` → `{ "enabled": true, "summary": "", "notes": [] }`
- `worlds/monster-hunter/curated/characters-index.json`
  - 顶层 `notCompleteCanonRoster: true` → `{ "enabled": true, "summary": "", "notes": [] }`
  - `runtimeUseGate.notCompleteCanonRoster: true` → `{ "enabled": true, "summary": "", "notes": [] }`

### `knowledge-graph.json` / `relationship-graph.json:notes`

以下顶层 `notes` 字符串已迁移为数组，并保留原字符串作为唯一数组元素：

- `worlds/date-a-live/curated/knowledge-graph.json`
- `worlds/date-a-live/curated/relationship-graph.json`
- `worlds/madan-no-ou/curated/knowledge-graph.json`
- `worlds/madan-no-ou/curated/relationship-graph.json`

## 验证

已执行窄范围 Node 校验：

- 6 个目标 JSON 文件均可 `JSON.parse`。
- `blue-archive` / `monster-hunter` 的顶层与 `runtimeUseGate.notCompleteCanonRoster` 均为对象，且 `enabled` 保留原 `true`。
- `date-a-live` / `madan-no-ou` 的目标图谱文件顶层 `notes` 均为数组，且数组首项保留原字符串。

命令结果：`R3 extended type check passed`。

## 复核结论

- 本轮指定的 6 项“非阻断扩展类型风险”已处理完成。
- 本轮 mutation scope 不包含 `marvel-cinematic-universe`、`naruto`、`type-moon-nasuverse` 的 `relationship-graph.json` 或 `source-registry.json`，因此 `QA-AFTER-REPAIR-R2.md` 中记录的 6 个未注册 `evidence/source` HIGH/P1 未在本步骤修改。
- 按本轮实际复核范围，未发现新增 JSON 解析或目标扩展类型问题。
- 全库 P0/P1/HIGH 是否清零仍需后续在允许修改来源引用相关文件后复扫确认；基于 R2 报告，未注册 evidence/source 的 6 个 HIGH/P1 预计仍残留。
