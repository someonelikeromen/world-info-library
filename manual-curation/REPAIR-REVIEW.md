# REPAIR-REVIEW

日期：2026-06-22  
审查范围：读取 `manual-curation/REPAIR-*.md`、`manual-curation/QA-JSON-SCHEMA-AFTER-REPAIR.md`、`manual-curation/QA-CROSS-REFERENCES-AFTER-REPAIR.md` 后形成修复审查结论。  
写入边界：本步骤仅创建/修改 `manual-curation/REPAIR-REVIEW.md`，未修改 `worlds/*/curated/`。

## 结论摘要

本轮修复已显著降低运行时硬失败风险，但**尚未达到“没问题”的可执行标准**。

原因：修复后 QA 已确认 P0 类问题清零，第一轮重点中的 HIGH 图谱断链、HIGH sourceRefs 未注册、schema/顶层必备字段、特殊世界门禁均已通过；但 `QA-JSON-SCHEMA-AFTER-REPAIR.md` 在严格结构口径下仍报告 **34 项 P1 类型不匹配**，集中在 17 个 `world.json` 的两个字段：

- `sandboxPrinciple`：当前为 `string`，严格预期为 `object`。
- `foreignPowerSuppressionDefault`：当前为 `boolean`，严格预期为 `object`。

因此当前状态应判定为：**P0 未发现；P1 仍存在；不可声明完全没问题**。

## 已修复内容

### 1. JSON/schema/字段骨架

依据 `REPAIR-STRUCTURE.md` 与修复后 QA：

- `worlds/*/curated/*.json` 共 315 个文件全部可解析。
- 63 个世界均具备 5 类 curated JSON：
  - `world.json`
  - `source-registry.json`
  - `characters-index.json`
  - `knowledge-graph.json`
  - `relationship-graph.json`
- 5 类文件的顶层 `schema` 已统一为期望值：
  - `rp-world-v1`
  - `rp-source-registry-v1`
  - `rp-characters-index-v1`
  - `rp-knowledge-graph-v1`
  - `rp-relationship-graph-v1`
- `QA-JSON-SCHEMA.md` 中列出的顶层必备字段缺失项已从修复前 926 项降为 0。
- 原报告明确列出的 3 项顶层类型错误已修复：
  - `worlds/date-a-live/curated/world.json:notes` 已为 array。
  - `worlds/date-a-live/curated/world.json:worldRules` 已为 object。
  - `worlds/toriko/curated/world.json:worldRules` 已为 object。

### 2. HIGH 图谱断链

依据 `REPAIR-GRAPH-HIGH.md` 与 `QA-CROSS-REFERENCES-AFTER-REPAIR.md`：

- 修复目标覆盖 17 个 HIGH 图谱断链世界。
- 对 `knowledge-graph.json` / `relationship-graph.json` 的缺失 endpoint 补入或解析为对象节点。
- 修复后全库重扫：
  - `knowledge-graph.edges[].from/to` 均能解析到同文件 `nodes[].id`。
  - `relationship-graph.edges[].from/to` 均能解析到同文件 `nodes[].id`。
  - HIGH 图谱 endpoint 断链：0。
  - 非对象节点与重复 node id 在修复后 QA 口径下未发现。

### 3. HIGH sourceRefs 未注册

依据 `REPAIR-SOURCE-REFS.md`、`REPAIR-STRUCTURE.md` 与修复后 QA：

- 针对 `madan-no-ou`、`toaru`、`testament-sister-new-devil`、`claymore` 的 HIGH 来源引用未注册问题，已在对应 `source-registry.json` 中登记 parent source 与 fragment/comment/entryIndex alias。
- 额外结构修复也补入了 `unregistered-placeholder` / `granular-reference-placeholder` 类型占位来源，以保证引用可追踪。
- 修复后递归检查 `sourceRefs` / `sourceRef` / `sourceBasis` / `source.ref` / relationship evidence 等来源引用：未发现未注册引用。
- HIGH sourceRefs 未注册：0。

### 4. 特殊世界门禁

依据 `REPAIR-SPECIAL-WORLDS.md` 与修复后 QA：

- `acg-character-database` 已补：
  - `referenceLibraryType`
  - `runtimeUseGate`
  - `specialWorldGate`
  - reference-library 语义说明
- `blue-archive` 已补：
  - `runtimeUseGate`
  - `notCompleteCanonRoster: true`
  - role-slot / 非完整 canon roster 风险说明
- `monster-hunter` 已补：
  - `runtimeUseGate`
  - `notCompleteCanonRoster: true`
  - 职业/生态槽位风险说明
- 修复后 QA 抽查确认这些门禁字段存在。

## 修复后 QA 状态

### JSON/schema QA

来源：`manual-curation/QA-JSON-SCHEMA-AFTER-REPAIR.md`

| 项目 | 修复后状态 |
|---|---:|
| 世界数 | 63 |
| curated JSON 文件数 | 315 |
| JSON 解析失败 | 0 |
| 5 类 curated JSON 缺失 | 0 |
| 未识别 JSON 文件名 | 0 |
| schema mismatch | 0 |
| 顶层必备字段缺失 | 0 |
| 原报告列出的顶层类型错误 | 0 |
| HIGH 图谱 edge-node 断链 | 0 |
| HIGH sourceRefs 未注册 | 0 |
| 特殊世界门禁字段缺失 | 0 |
| 严格类型不匹配 | 34 项 P1 |

### Cross-reference QA

来源：`manual-curation/QA-CROSS-REFERENCES-AFTER-REPAIR.md`

| 项目 | 数量 |
|---|---:|
| 修复后总 findings | 876 |
| HIGH | 0 |
| MED | 438 |
| LOW | 295 |
| INFO | 143 |

残留 category：

| Category | Count | Severity |
|---|---:|---|
| `character-relationship-target` | 231 | LOW |
| `character-location` | 217 | MED |
| `character-faction` | 150 | MED |
| `world-kg-coverage` | 143 | INFO |
| `relationship-coverage` | 64 | LOW |
| `character-powerSystem` | 43 | MED |
| `world-faction-member` | 28 | MED |

## 剩余 P0/P1 判断

- **P0：未发现。** 解析、文件齐备、schema、顶层必备字段、HIGH 图谱断链、HIGH sourceRefs 未注册、特殊世界门禁字段存在性均通过修复后 QA。
- **P1：仍有 34 项。** 严格结构口径下，17 个 `world.json` 的 `sandboxPrinciple` 与 `foreignPowerSuppressionDefault` 类型仍不符合 object 预期。
- **P1 边界/质量风险：** 10 个 `source-registry.json:sources` 为空、35 个 `source-registry.json:conflictLog` 为空，以及大量空骨架/占位来源/占位节点仍有质量风险；它们未被当前 QA 计为硬 schema 失败，但会影响来源可追溯性和检索质量。

## 下一轮精确任务包

### 任务包 A：清零 34 项 P1 严格类型不匹配

目标文件：以下 17 个世界的 `curated/world.json`：

- `worlds/absolute-duo/curated/world.json`
- `worlds/danmachi/curated/world.json`
- `worlds/dungeon-fighter-online/curated/world.json`
- `worlds/elemental-gelade/curated/world.json`
- `worlds/evangelion/curated/world.json`
- `worlds/high-school-dxd/curated/world.json`
- `worlds/honkai-impact-3rd/curated/world.json`
- `worlds/kaguya-sama/curated/world.json`
- `worlds/kimetsu-no-yaiba/curated/world.json`
- `worlds/marvel-cinematic-universe/curated/world.json`
- `worlds/naruto/curated/world.json`
- `worlds/omamori-himari/curated/world.json`
- `worlds/rozen-maiden/curated/world.json`
- `worlds/sekirei/curated/world.json`
- `worlds/spice-and-wolf/curated/world.json`
- `worlds/tokyo-ghoul/curated/world.json`
- `worlds/type-moon-nasuverse/curated/world.json`

精确修改要求：

1. 将 `sandboxPrinciple` 从 string 迁移为 object，不丢失原文本。建议结构：
   - 若原值为非空字符串：`{"summary": "原字符串", "notes": []}`。
   - 若原值为空字符串：`{"summary": "", "notes": []}`。
2. 将 `foreignPowerSuppressionDefault` 从 boolean 迁移为 object，不丢失原布尔语义。建议结构：
   - `{"enabled": 原布尔值, "summary": "", "notes": []}`。
3. 不扩写 canon 正文，不新增未经证实设定；仅做类型兼容迁移。
4. 修改后重跑 JSON/schema QA，验收条件：
   - 315 个 JSON parse error = 0。
   - schema mismatch = 0。
   - 顶层必备字段缺失 = 0。
   - 严格类型不匹配 = 0。

### 任务包 B：第二轮 cross-reference MED 规范化，先处理高残留世界

优先世界：

1. `madan-no-ou`：178 findings，MED 101。
2. `dantalian-no-shoka`：38 findings，MED 24。
3. `gate-jsdf`：33 findings，MED 22。
4. `honkai-impact-3rd`：33 findings，MED 21。
5. `d-gray-man`：31 findings，MED 21。
6. `dragon-ball`：29 findings，MED 21。
7. `naruto`：34 findings，MED 20。
8. `marvel-cinematic-universe`：32 findings，MED 17。
9. `cross-ange`：20 findings，MED 16。
10. `gundam-seed`：15 findings，MED 15。

精确处理类别：

- `character-location`：把角色 location 值规范为 `world.json.locations[].id`；若确为展示名，新增或修正可解析 id/alias 策略，并保持显示名不丢失。
- `character-faction`：把角色 faction 值规范为 `world.json.factions[].id`；若为组织显示名，建立 id 对应关系或迁移为 display label 字段。
- `character-powerSystem`：对齐 `world.json.powerSystems[].id`。
- `world-faction-member`：确保 `world.json.factions[].knownMembers` 指向 `characters-index.characters[].id`，若为别名则补 alias 或改为 canonical id。

验收条件：

- 不新增 HIGH。
- 目标世界 MED 明显下降；优先要求上述 top worlds 的 `character-location` / `character-faction` / `character-powerSystem` / `world-faction-member` 可解析率提升。
- 不用占位 id 掩盖真实未决关系；无法确定时写入 notes 或 registry/curation note，而不是伪造 canon。

### 任务包 C：LOW/INFO 关系图与 KG 覆盖补强

目标：处理非硬断链但影响检索质量的残留。

优先类别：

- `character-relationship-target`：231 项 LOW。
- `relationship-coverage`：64 项 LOW。
- `world-kg-coverage`：143 项 INFO。

精确要求：

1. 对 relationship target 为 group/placeholder/未索引对象的条目分类：
   - 真实角色：补入或对齐 `characters-index.characters[].id`。
   - 组织/阵营/地点：迁移到合适字段，或在 relationship graph 中建明确 object node，不冒充 character。
   - 暂不能确认：保留为 display label，并加 `resolutionStatus`/notes 说明不可解析原因。
2. 为核心角色补 relationship graph 节点时，不强行编造关系；只添加已有资料可支持的节点/边。
3. KG 覆盖仅按启发式处理，优先补已有 world-level 实体的节点索引，不扩写未证实 lore。

### 任务包 D：来源与占位质量治理

目标：降低“结构通过但内容不可追溯”的风险。

精确任务：

1. 检查 `source-registry.json:sources` 为空的 10 个世界：
   - `blue-archive`
   - `cheng-long-adventures`
   - `monster-hunter`
   - `overlord`
   - `persona-5`
   - `rakudai-kishi`
   - `sora-no-otoshimono`
   - `sword-art-online`
   - `world-god-only-knows`
   - `xianjian-1`
2. 对每个空 registry 明确二选一：
   - 补入可追踪的真实/导入来源记录；或
   - 保留为空但写明 `registryUseGate` / `registryNotes`，声明当前不可作为已验证来源库使用。
3. 复核 35 个空 `conflictLog`，至少区分：
   - 确认暂无冲突登记；
   - 未完成冲突复核；
   - 特殊世界/参考库不适用。
4. 清点并逐步消化 `referenced-placeholder`、`granular-reference-placeholder`、`unregistered-placeholder`，能合并到真实来源的合并，不能确认的保留风险说明。

## 最终审查判定

- 本轮第一重点中的大部分硬问题已修复：**schema/字段骨架、原顶层类型错误、HIGH 图谱断链、HIGH sourceRefs 未注册、特殊世界门禁**均通过修复后 QA。
- 但严格结构 QA 仍有 **34 项 P1 类型不匹配**，所以不能给出“已没问题”的放行结论。
- 下一轮应先执行任务包 A 清零 P1；随后按任务包 B/C/D 处理 MED/LOW/INFO 与来源质量问题。
