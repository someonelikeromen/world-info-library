# Manual Curation QA Checklist

更新日期：2026-06-22  
参考文件：`manual-curation/STATUS.md`、`manual-curation/INDEX.md`  
适用范围：`campaigns/world-library/worlds/*/curated/` 下 63 个已完整产出的世界。  
约束：本清单仅规划后续 QA 与模板产物；执行时不得直接修改 `worlds/*/curated/` 正文，修复建议与汇总应写入 `manual-curation/` 下的 QA 记录文件。

## 当前基线

- 世界总数：63。
- 每世界标准产物均已存在，共 7 项：
  - `README.md`
  - `world.json`
  - `source-registry.json`
  - `characters-index.json`
  - `knowledge-graph.json`
  - `relationship-graph.json`
  - `curation-notes.md`
- 已完成检查类型：存在性检查。
- 未完成检查类型：JSON 解析、schema/字段完整性、跨文件交叉引用、正文质量复核、运行时检索规则、campaign/session 层模板。

## 执行顺序总览

| 顺序 | QA/建设项 | 风险等级 | 主要产物路径 | 阻塞关系 |
|---:|---|---|---|---|
| 1 | JSON/schema 校验 | 高 | `manual-curation/QA-JSON-SCHEMA.md` | 后续交叉引用检查依赖 JSON 可解析与基础字段稳定。 |
| 2 | 交叉引用校验 | 高 | `manual-curation/QA-CROSS-REFERENCES.md` | 依赖第 1 项；为运行时检索与模板引用提供一致 ID。 |
| 3 | 高风险/最后补齐世界质量抽样复核 | 高 | `manual-curation/QA-HIGH-RISK-SAMPLING.md` | 可与第 2 项部分并行，但最终结论应吸收第 1、2 项异常。 |
| 4 | 运行时检索规则文档 | 中 | `manual-curation/RUNTIME-RETRIEVAL.md` | 依赖第 1、2 项确认可检索字段与引用一致性。 |
| 5 | campaign/session 层模板 | 中 | `manual-curation/CAMPAIGN-SESSION-TEMPLATES.md` | 依赖第 4 项检索规则，避免模板固化错误字段或越权剧透。 |
| 6 | QA 汇总 | 中 | `manual-curation/QA-SUMMARY.md` | 汇总第 1-5 项结果、残余风险与下一轮修复建议。 |

## 1. JSON/schema 校验

**目标**：确认 63 个世界的 5 个 JSON 标准产物均可解析，并满足统一字段约束与最低结构完整性要求。

**检查范围**：

- `campaigns/world-library/worlds/*/curated/world.json`
- `campaigns/world-library/worlds/*/curated/source-registry.json`
- `campaigns/world-library/worlds/*/curated/characters-index.json`
- `campaigns/world-library/worlds/*/curated/knowledge-graph.json`
- `campaigns/world-library/worlds/*/curated/relationship-graph.json`

**执行清单**：

- [ ] 收集 63 个 `curated/` 路径，数量与 `manual-curation/INDEX.md` 一致。
- [ ] 对全部 `.json` 文件执行 JSON 解析，记录语法错误、重复 key 风险、编码异常。
- [ ] 为每类 JSON 建立最低字段检查表：世界标识、名称/标题、条目 ID、来源引用、节点/边类型、描述字段、可选 metadata。
- [ ] 检查数组/对象顶层形态是否一致，避免同类文件结构漂移。
- [ ] 检查关键字段类型：字符串、数组、对象、布尔值、数字不得混用。
- [ ] 检查空字符串、空数组、占位符、明显模板残留。
- [ ] 记录每世界通过/失败状态与错误定位。

**验收标准**：

- 63 个世界的所有 JSON 文件均被纳入清单，无遗漏。
- 每个 JSON 文件至少有“解析通过/失败”和“schema 通过/失败”结论。
- 所有失败项记录到文件路径、字段路径、错误类型、建议处理方式。
- 不因 schema 校验直接修改 `curated/` 正文；仅输出 QA 记录。

**计划产物路径**：`manual-curation/QA-JSON-SCHEMA.md`

**风险等级**：高。JSON 或 schema 错误会阻断自动检索、交叉引用校验和 campaign/session 模板消费。

## 2. 交叉引用校验

**目标**：验证同一世界内人物、知识节点、关系边、来源编号之间的引用一致性，减少孤儿节点、悬空关系和来源不可追溯问题。

**检查范围**：

- `characters-index.json` 中人物 ID/别名/阵营/标签。
- `knowledge-graph.json` 中节点 ID、节点类型、来源引用、关联人物/组织/地点。
- `relationship-graph.json` 中边的 source/target、关系类型、证据来源。
- `source-registry.json` 中 source ID、文件/来源描述、可信度或备注字段。
- `world.json` 中世界 slug、名称、主要设定与图谱入口字段。

**执行清单**：

- [ ] 检查 `world.json` slug 与目录 slug 是否一致。
- [ ] 检查所有 source 引用均存在于 `source-registry.json`。
- [ ] 检查所有 relationship source/target 均可在人物索引或知识图谱节点中解析。
- [ ] 检查 knowledge-graph 节点引用的人物、组织、地点、事件是否存在或有合理文本说明。
- [ ] 检查人物别名、组织名、阵营名在同世界内是否存在明显冲突或重复 ID。
- [ ] 检查跨文件引用大小写、连字符、下划线、中文/英文译名混用导致的潜在错链。
- [ ] 对孤儿节点、悬空边、未使用来源、重复来源编号生成问题表。

**验收标准**：

- 每个世界均有交叉引用状态：通过、警告、失败。
- 每个失败项包含：世界 slug、文件路径、引用字段、缺失/冲突对象、影响等级。
- 对可接受的“文本说明型引用”单独标记为警告而非失败。
- 高风险悬空关系不得进入后续运行时检索规则的默认示例。

**计划产物路径**：`manual-curation/QA-CROSS-REFERENCES.md`

**风险等级**：高。交叉引用错误会导致检索上下文错配、角色关系误导和 session 模板引用失败。

## 3. 高风险/最后补齐世界质量抽样复核

**目标**：对 `STATUS.md` 标注的特殊、高风险和最后补齐世界进行人工抽样，确认正文质量、边界处理、成人化/控制文本剥离、剧透可见性和来源覆盖范围。

**优先复核世界**：

最后补齐世界（优先级 P0）：

- `dantalian-no-shoka`
- `date-a-live`
- `toriko`
- `madan-no-ou`

特殊/高风险世界（优先级 P1）：

- `acg-character-database`
- `blue-archive`
- `monster-hunter`
- `infinite-stratos`
- `taimanin`
- `testament-sister-new-devil`
- `toaru`
- `jojo`

其他 `STATUS.md` 点名风险（优先级 P2）：

- `haganai`
- `kill-la-kill`
- `zero-no-tsukaima`
- `chunibyo`
- `claymore`

**抽样建议**：

- 每个 P0/P1 世界至少抽查：`README.md`、`world.json`、`characters-index.json`、两类图谱、`curation-notes.md`。
- 每个世界至少抽取 5 个角色条目、5 个知识节点、5 条关系边；角色不足的世界改抽岗位/生态/组织条目。
- 对含 IF/支线/多部作品的世界，额外检查边界标记与覆盖范围说明。
- 对源内存在成人化、状态栏、玩家寄生、控制变量、模板残留的世界，额外检查是否已剥离或非露骨化。

**执行清单**：

- [ ] 建立 P0/P1/P2 抽样表。
- [ ] 逐世界记录抽样条目 ID、所在文件、抽样理由。
- [ ] 检查是否存在未剥离的控制文本，如 `{{user}}` 被误固化、状态栏、系统提示、变量占位符。
- [ ] 检查敏感或成人化内容是否被改写为安全、非露骨、世界观必要信息。
- [ ] 检查译名、阵营、时间线、支线/IF 线边界是否一致。
- [ ] 检查特殊库 `acg-character-database` 的跨作品边界，不应误作单一世界连续设定。
- [ ] 检查 `blue-archive`、`monster-hunter` 中岗位/生态角色是否清楚标为非固定姓名角色或需补证。

**验收标准**：

- P0 与 P1 世界均完成抽样记录；P2 至少完成风险点核对。
- 每条问题均标注风险等级：阻断、高、中、低。
- 对“可接受但需说明”的内容给出保留理由。
- 对需修复内容只提出建议，不直接修改 `curated/` 正文。

**计划产物路径**：`manual-curation/QA-HIGH-RISK-SAMPLING.md`

**风险等级**：高。此项直接关系到内容安全、设定准确性、边界清晰度和归档可信度。

## 4. 运行时检索规则

**目标**：形成供运行时使用的检索与上下文拼装规则，明确何时读取世界摘要、人物索引、知识图谱、关系图谱和来源说明，避免过量注入、错链和剧透越权。

**规则设计清单**：

- [ ] 定义默认检索顺序：`world.json` → `README.md` → `characters-index.json` → `knowledge-graph.json` → `relationship-graph.json` → `source-registry.json`/`curation-notes.md`。
- [ ] 定义按任务类型的检索策略：世界观问答、角色扮演、关系查询、地点/组织查询、剧情时间线查询、来源追溯。
- [ ] 定义最小上下文原则：仅注入与当前 session 目标相关的世界、角色、关系和知识节点。
- [ ] 定义剧透控制策略：区分公开基础设定、角色已知信息、后期/终局/隐藏设定。
- [ ] 定义冲突处理：优先采用 curated 明确字段；不确定项引用 `curation-notes.md` 风险说明。
- [ ] 定义失败回退：JSON 不可用、引用悬空、角色缺失、来源缺失时如何降级。
- [ ] 定义禁止项：不得把 QA 问题、schema 错误、控制变量、成人化模板残留作为运行时事实注入。

**验收标准**：

- 规则覆盖 7 个标准产物在运行时的用途与读取优先级。
- 至少包含 5 类典型查询场景及推荐读取文件组合。
- 包含剧透/隐藏设定控制规则，特别适配 `toriko`、`date-a-live`、`madan-no-ou` 等有终局或支线风险的世界。
- 包含对高风险世界的降级与人工确认建议。

**计划产物路径**：`manual-curation/RUNTIME-RETRIEVAL.md`

**风险等级**：中。检索规则错误会影响使用质量，但通常不破坏底层归档文件。

## 5. Campaign/session 层模板

**目标**：设计不修改世界正文的 campaign/session 层模板，用于把 curated 世界资料安全拼装为具体会话上下文、角色设定、任务目标和检索配置。

**模板范围**：

- Campaign 模板：选择世界、设定时间点、允许剧透等级、核心冲突、参与角色、检索策略。
- Session 模板：当前场景、玩家/用户角色槽位、NPC 列表、已知信息、禁止注入项、引用文件清单。
- QA 兼容字段：记录是否通过 JSON/schema、交叉引用、高风险抽样。

**执行清单**：

- [ ] 定义 campaign 元数据字段：campaign_id、world_slug、canon_scope、timeline_scope、spoiler_level、safety_notes。
- [ ] 定义 session 元数据字段：session_id、campaign_id、scene_summary、active_characters、retrieval_targets、known_facts、blocked_facts。
- [ ] 定义用户角色槽位规则：保留 `{{user}}` 或等价占位，不把用户槽位固化为原作人物。
- [ ] 定义跨文件引用格式：世界 slug、角色 ID、知识节点 ID、关系边 ID、source ID。
- [ ] 定义质量门禁字段：qa_json_schema_status、qa_crossref_status、qa_sampling_status。
- [ ] 提供至少 1 个 campaign 模板和 1 个 session 模板示例。
- [ ] 模板示例不得引入未校验事实，不直接复制高风险露骨或控制文本。

**验收标准**：

- 模板可独立说明如何引用 `curated/` 产物，但不要求修改 `curated/`。
- campaign 与 session 模板字段边界清晰，session 不覆盖 campaign 的长期设定。
- 模板包含 QA 状态门禁，能阻止未通过校验的世界进入默认生产使用。
- 模板包含剧透等级和用户槽位保护规则。

**计划产物路径**：`manual-curation/CAMPAIGN-SESSION-TEMPLATES.md`

**风险等级**：中。模板若字段不清晰，会造成运行时上下文膨胀、剧透泄漏或用户槽位误固化。

## 6. QA 汇总与关闭标准

**目标**：在第 1-5 项完成后生成总览，明确通过项、失败项、残余风险、建议修复批次。

**执行清单**：

- [ ] 汇总每个世界在 JSON/schema、交叉引用、抽样复核中的状态。
- [ ] 汇总运行时检索规则与 campaign/session 模板是否完成。
- [ ] 标出阻断项：JSON 不可解析、schema 缺关键字段、悬空关系、严重安全/控制文本残留。
- [ ] 标出非阻断项：命名不统一、来源说明不足、覆盖范围需补证。
- [ ] 形成下一轮修复优先级：P0 阻断、P1 高风险、P2 中低风险。

**验收标准**：

- 63 个世界均有最终 QA 状态。
- 所有计划产物路径均有完成/未完成状态。
- 汇总明确说明是否仍禁止修改 `curated/` 正文，或是否需要另开修复任务。
- 汇总不虚构已执行命令或未完成验证结果。

**计划产物路径**：`manual-curation/QA-SUMMARY.md`

**风险等级**：中。汇总不准确会误导后续修复优先级。

## 风险等级定义

- **高**：可能导致 JSON 无法消费、引用错配、内容安全问题、世界边界严重错误。
- **中**：可能导致运行时质量下降、上下文过载、剧透控制不稳、模板复用困难。
- **低**：主要为命名、格式、备注完善，不阻断基本检索与归档使用。

## 产物路径清单

本轮已创建/维护：

- `manual-curation/QA-CHECKLIST.md`

后续建议创建：

- `manual-curation/QA-JSON-SCHEMA.md`
- `manual-curation/QA-CROSS-REFERENCES.md`
- `manual-curation/QA-HIGH-RISK-SAMPLING.md`
- `manual-curation/RUNTIME-RETRIEVAL.md`
- `manual-curation/CAMPAIGN-SESSION-TEMPLATES.md`
- `manual-curation/QA-SUMMARY.md`

## 最小执行策略

1. 先完成 JSON/schema，确保所有机器可读文件能被稳定消费。
2. 再完成交叉引用，确保 ID、来源、节点、关系不悬空。
3. 同步启动 P0/P1 人工抽样，但最终记录需吸收前两项发现。
4. 在结构与引用稳定后编写运行时检索规则。
5. 最后编写 campaign/session 模板，并以 QA 状态作为模板启用门禁。
6. 生成汇总，决定是否另开 curated 修复任务。