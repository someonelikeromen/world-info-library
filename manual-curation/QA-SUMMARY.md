# QA-SUMMARY：world-info-library 后续 QA 与模板汇总

更新日期：2026-06-22  
范围：汇总本轮 checklist、JSON/schema、交叉引用、高风险质量抽样、运行时检索文档、campaign/session 模板产物。  
约束：本汇总未修改任何 `worlds/*/curated/` 正文；仅写入本文件。

## 产物完成状态

| 项 | 状态 | 产物路径 | 说明 |
|---:|---|---|---|
| 0 | 已完成 | `manual-curation/QA-CHECKLIST.md` | 建立 1-5 项 QA/建设清单与第 6 项汇总标准。 |
| 1 | 已完成，有阻断/高风险发现 | `manual-curation/QA-JSON-SCHEMA.md` | 全量检查 63 个世界 × 5 个 JSON，共 315 文件。JSON 均可解析，但 schema/字段/类型问题较多。 |
| 2 | 已完成，有大量高风险发现 | `manual-curation/QA-CROSS-REFERENCES.md` | 全量扫描 63 个世界的跨文件引用一致性，发现 1406 条疑点，其中 HIGH 379 条。 |
| 3 | 已完成 | `manual-curation/QA-QUALITY-SAMPLE.md` | 人工复核 12 个重点世界。未发现明显可执行控制文本残留；记录 IF、成人源、单源、岗位型人物索引等风险。 |
| 4 | 已完成 | `manual-curation/RETRIEVAL.md` | 建立运行时 curated-only 最小检索规则、常见查询场景、低置信/冲突/剧透处理规则。 |
| 5 | 已完成 | `templates/campaign-session/` | 创建 campaign/session 层 7 个模板文件，用 overlay/delta 记录运行态，不污染 curated 正文。 |

> 路径差异说明：`QA-CHECKLIST.md` 中早期规划名包括 `QA-HIGH-RISK-SAMPLING.md`、`RUNTIME-RETRIEVAL.md`、`CAMPAIGN-SESSION-TEMPLATES.md`；实际完成产物分别为 `QA-QUALITY-SAMPLE.md`、`RETRIEVAL.md`、`templates/campaign-session/`。

## 1. JSON / schema 校验结论

来源：`manual-curation/QA-JSON-SCHEMA.md`

### 已完成

- 检查范围：`worlds/*/curated/*.json`。
- 世界数：63。
- JSON 文件数：315（63 × 5）。
- 五类 JSON 文件齐备：是。
- JSON 解析失败：0。
- 未识别文件名：0。

### 主要发现

- `schema` 值不匹配：130 个文件，集中在 26 个世界；常见为 `curated-*-v1` 或 `rp-curated-*-v1`，未统一到模板期望的 `rp-*-v1`。
- 缺顶层关键字段：200 个文件，共 926 个缺字段项。
- 顶层类型不匹配：3 项：
  - `worlds/date-a-live/curated/world.json`：`notes` 应为 array，实际 string。
  - `worlds/date-a-live/curated/world.json`：`worldRules` 应为 object，实际 array。
  - `worlds/toriko/curated/world.json`：`worldRules` 应为 object，实际 array。
- 空数组/空对象风险：12 项，均为 `source-registry.json` 的 `conflictLog` 为空，需要确认是“确无冲突”还是“尚未整理”。

### 影响判断

- JSON 语法层面可消费，但 schema 与顶层结构未达统一模板要求。
- campaign/session 初始化、运行时检索、自动图谱消费若严格依赖模板字段，会遇到缺字段或类型错误。
- 建议把此项视为下一轮修复的 P0/P1 输入，而不是生产通过证明。

## 2. 交叉引用校验结论

来源：`manual-curation/QA-CROSS-REFERENCES.md`

### 已完成

- 扫描范围：63 个 `worlds/*/curated/` 世界。
- 有疑点世界：51 个。
- 总发现：1406 条。
- 严重度统计：HIGH 379，MED 707，LOW 238，INFO 82。

### 高频问题类别

| 类别 | 数量 | 风险 |
|---|---:|---|
| `character-location` | 377 | 角色 location 与 `world.locations[].id` 不匹配；多为显示名/slug 混用。 |
| `character-faction` | 287 | 角色 faction 与 `world.factions[].id` 不匹配；多为中文名/概念名未映射到 id。 |
| `relationship-edge-node` | 187 | 关系边端点缺少关系图节点，可能阻断关系遍历。 |
| `source-ref` | 178 | 来源引用未在 source registry 注册，影响可追溯性。 |
| `world-kg-coverage` | 127 | 世界核心设定在 KG 中无明显节点，影响检索覆盖。 |
| `character-relationship-target` | 100 | 人物关系目标未解析；部分可能是群体占位符。 |

### HIGH 重点世界/模式

- `madan-no-ou`：70 HIGH，包含关系/KG 端点缺失和大量 source fragment id 与 registry 不一致。
- `toaru`：50 HIGH，主要是 `characters-index.characters[].sourceRefs` 使用 `characters.json comment ...`，未注册为 `sourceId`。
- `jojo`：36 HIGH，关系边引用大量未在 `relationship-graph.nodes` 中登记的人物。
- `claymore`：32 HIGH，sourceRefs 使用 `characters.json entryIndex ...`，未注册。
- `zero-no-tsukaima`：31 HIGH，关系边/KG 端点缺失。
- `saijaku-muhai-bahamut`：30 HIGH，关系边端点缺失。
- `testament-sister-new-devil`：28 HIGH，sourceRefs 使用人类可读 comment 而非 sourceId。
- `to-love-ru`：28 HIGH，关系边端点缺失。
- `haganai`、`chunibyo`、`bocchi-the-rock`：关系图端点缺失呈系统性。

### 影响判断

- 不建议将 HIGH broken graph/source reference 世界直接作为默认关系遍历或来源追溯示例。
- MED 中大量显示名 vs slug id 混用需要先确定字段规范：运行时字段是否必须使用 id，还是允许 alias/mapping。
- LOW/INFO 中的 group placeholder 与稀疏图谱不一定是错误，但需要文档化，避免被运行时当作断链。

## 3. 高风险质量抽样复核结论

来源：`manual-curation/QA-QUALITY-SAMPLE.md`

### 已完成

人工阅读 12 个指定世界的：

- `curated/README.md`
- `curated/characters-index.json`
- `curated/world.json`
- `curated/curation-notes.md`

覆盖世界：

- 补齐组：`dantalian-no-shoka`、`date-a-live`、`toriko`、`madan-no-ou`
- 高风险/特殊组：`acg-character-database`、`blue-archive`、`monster-hunter`、`infinite-stratos`、`taimanin`、`testament-sister-new-devil`、`toaru`、`jojo`

### 主要结论

- 未发现 curated 正文中存在会被运行时直接执行的明显系统级控制文本。
- 多数高风险世界在 README/notes 中明确排除了状态栏、变量、输出格式、成人向规则、`{{user}}` 玩家设定等源内控制/成人化内容。
- 成人向源材料已做 SFW 化，但运行时仍必须避免从 raw/imports 回流相关内容。
- 主要质量风险集中在：
  - 单源世界书可靠度。
  - 原作、IF、玩家替代线、支线连续性混杂。
  - 跨作品数据库被误当作单一世界。
  - 岗位/角色类型与 canon 固定人物混在人物索引中。
  - 部分终局、隐藏真相、高危能力需要 GM-only/剧透分层。

### 需特别标注的世界

- `acg-character-database`：不是单一世界，而是跨作品角色心理/人格参考库；不得构造统一 continuity。
- `blue-archive`、`monster-hunter`：人物索引大量为岗位/角色类型，不是完整 canon 角色姓名库。
- `madan-no-ou`、`date-a-live`、`toriko`、`infinite-stratos`：调用前需明确正史/IF/替代/共存模式。
- `taimanin`、`testament-sister-new-devil`、`date-a-live`、`infinite-stratos`、`dantalian-no-shoka`、`acg-character-database`：成人或高敏源背景较重，运行时只可使用 SFW curated 信息。

## 4. 运行时检索文档结论

来源：`manual-curation/RETRIEVAL.md`

### 已完成内容

- 明确 curated-only 运行时策略：普通问答/RP 默认不读取 raw/worldbook。
- 推荐定位顺序：
  1. `manual-curation/INDEX.md`
  2. `worlds/<world-slug>/curated/README.md`
  3. 按问题读取 `world.json`、`characters-index.json`、`knowledge-graph.json`、`relationship-graph.json`、`source-registry.json`、`curation-notes.md`
- 覆盖查询场景：世界基本设定、角色查询、角色关系/RP 互动、术语/组织/地点/事件关联、RP/session 背景、跨世界比较/混合 RP、来源/可信度查询。
- 建立最小上下文原则：不要一次性加载全部 7 个 curated 产物；按问题读取必要文件。
- 建立低置信、冲突和剧透处理规则：标注不确定、冲突不强行合并、重大剧透放入 GM-only。
- 给 agent_team 子代理提供简短规则，并要求最终回答列出实际读取文件。

### 影响判断

- 该文档可作为后续 RP/查询代理的默认检索规程。
- 但由于 JSON/schema 与 crossref 仍有大量问题，运行时应结合 QA 报告降级使用：遇到断链、缺字段、低置信时报告 curated 缺口，而不是自动补完为 canon。

## 5. Campaign / session 模板结论

来源目录：`templates/campaign-session/`

### 已创建文件

- `templates/campaign-session/README.md`
- `templates/campaign-session/campaign-template.json`
- `templates/campaign-session/session-template.json`
- `templates/campaign-session/state-template.json`
- `templates/campaign-session/session-graph-delta-template.json`
- `templates/campaign-session/map-delta-template.json`
- `templates/campaign-session/progress-template.md`

### 覆盖能力

模板覆盖：

- 当前世界：`worldId`、`worldSlug`、`worldName`、`curatedRoot`、curated 文件引用路径。
- 角色卡：PC/NPC/canon-or-original NPC、`linkedCharacterId`、`cardId`、可见性、GM notes。
- Session：场景、事件日志、参与者、运行时检索记录。
- 玩家/主角状态：生命/伤势/疲劳/压力、资源、条件、物品、能力、目标、声望。
- 地点与时间：campaign clock、session in-world time、active/known locations。
- 关系与知识 delta：关系强度、facets、visibility before/after、source events、knowledge reveal conditions。
- 地图 delta：地点、路径、占用、hazard/asset、可见性变化。
- 来源引用：curated path、session-log、GM ruling、player input、derived。
- 可见性：`public`、`player_known`、`gm_only`、`secret`、`unknown`。
- 低置信说明：`confidence`、`lowConfidenceNotes`、review action、impact if wrong。
- QA/进度：`progress-template.md` 包含 JSON/schema、交叉引用、高风险抽样、运行时检索、campaign/session 进度表。

### 设计判断

- 模板是世界无关的，不绑定具体作品世界。
- 实际运行时要求“写 delta，不改 curated”。
- 通过 overlay/delta 管理 campaign/session 状态，避免污染 `worlds/<world-slug>/curated/`。
- 玩家可见、GM-only、secret 分层，有助于降低秘密泄露风险。
- 所有重大变化要求保留来源引用、置信度和可见性。

## 当前阻断项与残余风险

### P0 / 阻断级建议优先处理

1. **修正 JSON 顶层类型不匹配**：
   - `date-a-live` 的 `notes`、`worldRules`。
   - `toriko` 的 `worldRules`。
2. **修复 HIGH broken graph references**：优先处理 `relationship-edge-node`、`knowledge-edge-node`，为关系/KG 边补节点或修正端点 id。
3. **修复 HIGH source-ref 系统性问题**：
   - `madan-no-ou` fragment id。
   - `toaru` / `testament-sister-new-devil` human-readable comment refs。
   - `claymore` entryIndex refs。
   - 统一替换为 registry 中存在的 `sourceId`，或补注册来源。
4. **为 `acg-character-database` 补足/重构 schema 基础字段**：该世界在 JSON/schema 报告中缺 `characters`、`sources` 等核心块，且语义上不是单一世界，应有明确运行时门禁。

### P1 / 高优先级

1. 统一 26 个世界的 `schema` 字段命名，消除 130 个 schema mismatch。
2. 批量补齐图谱运行时元字段：`knowledge-graph.json:campaignId/indices`、`relationship-graph.json:campaignId/views`。
3. 为 26 个世界补 `characters-index.json:worldId/indices`。
4. 补 `world.json` 中 campaign/session 依赖较强的字段：`worldName`、`sandboxPrinciple`、`hasFixedFate`、`foreignPowerSuppressionDefault`、`energyEnvironment`、`worldRules`。
5. 决定 `characters-index` 中 `factions`、`locations`、`powerSystems` 是否必须使用 id；若必须，建立显示名到 id 的映射或修正字段。

### P2 / 中低优先级

1. 对空 `conflictLog` 增加语义说明：确无冲突 vs 尚未整理。
2. 对 group placeholder、岗位角色、生态角色、组织占位符进行文档化，避免交叉引用 QA 将其误判为断链。
3. 补充关系图中 high/critical 角色覆盖，以提升 RP 关系检索质量。
4. 对单源/低置信世界补 source registry、curation notes 或后续人工复核记录。

## 对运行时使用的建议

- 当前库可用于 curated-only 问答与 RP 准备，但不应宣称全库 schema/crossref 已通过。
- 对默认生产级 RP，建议先选择 JSON/schema 和 crossref 问题较少的世界。
- 对命中 HIGH 断链或 source-ref 问题的世界：
  - 不自动进行关系图遍历结论。
  - 不把缺失 source id 当作已验证出处。
  - 输出中标注“curated 引用待修复/低置信”。
- 对抽样报告列出的高风险世界，运行时应优先读取 `curation-notes.md`，并执行剧透/IF/成人源/SFW 边界控制。
- 使用 campaign/session 模板时，只写实例状态和 delta；不得把 session 变化写回 `worlds/*/curated/`。

## 下一步建议

1. 另开 curated 修复任务，mutation scope 明确限定到目标世界，按 P0 → P1 → P2 批次处理。
2. 先修机器消费问题：schema 名称、缺字段骨架、顶层类型不匹配。
3. 再修引用图：关系/KG missing node 与 source registry 未注册引用。
4. 建立 id/alias 规范：特别是中文显示名、slug id、组织/地点/能力体系字段。
5. 对 `acg-character-database`、`blue-archive`、`monster-hunter` 建立特殊世界/参考库门禁，避免当作普通 canon 世界。
6. 修复后重新运行 JSON/schema 与交叉引用 QA，并更新本汇总或新建修复后 QA 报告。

## 验证状态

- 本汇总读取并汇总了以下产物：
  - `manual-curation/QA-CHECKLIST.md`
  - `manual-curation/QA-JSON-SCHEMA.md`
  - `manual-curation/QA-CROSS-REFERENCES.md`
  - `manual-curation/QA-QUALITY-SAMPLE.md`
  - `manual-curation/RETRIEVAL.md`
  - `templates/campaign-session/README.md`
  - `templates/campaign-session/progress-template.md`
  - `templates/campaign-session/` 文件列表
- 本 step 仅写入：`manual-curation/QA-SUMMARY.md`。
- 未执行额外 JSON parser、schema validator、测试命令或修复命令。
- 未修改任何 `worlds/*/curated/` 正文。
