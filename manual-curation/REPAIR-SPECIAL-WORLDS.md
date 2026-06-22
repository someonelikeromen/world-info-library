# REPAIR-SPECIAL-WORLDS

日期：2026-06-22  
任务：修复特殊/高风险世界的运行时门禁与 QA 明确风险。

## 目标范围

- `worlds/acg-character-database/curated/`
- `worlds/blue-archive/curated/`
- `worlds/monster-hunter/curated/`
- `manual-curation/REPAIR-SPECIAL-WORLDS.md`

仅补元说明、门禁字段、schema/索引骨架与风险提示；未扩写世界设定正文。

## 本轮修复重点

### 1) `acg-character-database`

定位：跨作品角色心理/类脑参考库，不是单一世界。

已补：
- `world.json`
  - `referenceLibraryType: cross-work-character-psychology-reference-library`
  - `runtimeUseGate`
  - 强化 `specialWorldGate`
  - `notes` 追加运行时门禁说明
- `characters-index.json`
  - `indexType` 调整为 reference-library 语义
  - `runtimeUseGate`
  - 保持 `characters: []`，不伪造单一世界 NPC 目录
- `source-registry.json`
  - 补 `sources`
  - `registryUseGate`
  - `registryNotes` 说明仅登记参考库来源，不建立统一连续性

门禁结论：
- 只能当作参考库/人格原型库
- 必须由外部 continuity 选择可用条目
- 禁止自动合并不同作品的地理、阵营、时间线、关系

### 2) `blue-archive`

定位：角色索引偏 RP 角色类型/组织岗位，不是完整 canon 固定人物库。

已补：
- `world.json`
  - `runtimeUseGate`
  - `notes` 明确岗位角色/组织角色不是固定 canon NPC
- `characters-index.json`
  - `runtimeUseGate`
  - `notCompleteCanonRoster: true`
- `source-registry.json`
  - `registryUseGate`
  - `registryNotes` 强调角色覆盖为 role-slot 型

门禁结论：
- “老师/先生”保留为成人调停者定位
- 岗位角色/组织角色只能当可用角色槽位
- 不能从现有条目推断为完整官方学生名录

### 3) `monster-hunter`

定位：系统/生态导向归档，人物表以职业、组织、生态角色为主。

已补：
- `world.json`
  - `runtimeUseGate`
  - `notes` 明确不是完整固定 NPC 库
- `characters-index.json`
  - `runtimeUseGate`
  - `notCompleteCanonRoster: true`
- `source-registry.json`
  - `registryUseGate`
  - `registryNotes` 强调角色覆盖为职业/生态槽位

门禁结论：
- 猎人、公会、村落、研究机构、古龙/禁忌怪物都应视为角色槽位或生态角色
- 不应把生态角色当善恶固定人物
- 不应从岗位条目推断未登记 canon NPC

## QA 复核

已做本地机械复核：

- 315 个 curated JSON 可解析
- 重点世界门禁字段存在
- `acg-character-database` 保持 reference-library 语义
- `blue-archive` / `monster-hunter` 保持“非完整 canon roster”语义
- 图谱与 source registry 未再出现可检测的缺节点/未注册引用

结果：

```text
json_files 315
problems 0
```

## 残留风险

- `acg-character-database` 仍需人工决定未来是否合并/规范化重复来源版本。
- `blue-archive` 与 `monster-hunter` 的若干节点仍是 role-slot 级别，不等于完整 canon 详表。
- `runtimeUseGate` / `specialWorldGate` 是运行时门禁说明，不是正文设定扩写。
