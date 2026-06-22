# Runtime Retrieval Guide

更新日期：2026-06-22

用途：为世界查询、RP 运行时、以及 `agent_team` 子代理提供轻量按需检索规则。目标是在不读取原始 raw/worldbook 大文件的前提下，用最小上下文回答问题或支撑会话。

> 当前独立库路径以 `worlds/<world-slug>/curated/` 为准；`manual-curation/INDEX.md` 中若出现历史路径前缀 `campaigns/world-library/`，在本仓库内应映射为当前根目录下的同名 `worlds/` 路径。

## 总原则

1. **先总索引，后单世界**：先读 `manual-curation/INDEX.md` 确认世界 slug 与产物完整性，再进入对应 `worlds/<world-slug>/curated/`。
2. **先 README，后数据文件**：进入目标世界后先读 `README.md`，理解整理状态、主要来源、未解决项和风险。
3. **按问题最小加载**：只读取回答当前问题所需文件；不要一次性加载全部 JSON。
4. **优先 curated，避免 raw**：运行时只使用 curated 产物。当前库不包含 raw；即使在上游仓库存在 raw，也默认不要读取，除非任务明确要求 QA/溯源并授权。
5. **不确定即标注**：遇到低置信、冲突、未解决项、剧透风险时，明确标注，而不是把推测当事实。

## 标准加载顺序

### 0. 定位世界

读取：

- `manual-curation/INDEX.md`

目的：

- 找到目标 `world-slug`。
- 确认该世界是否有完整 curated 产物。
- 对多世界问题，先列出涉及的 slug，再逐个按需进入。

### 1. 读取世界 README

读取：

- `worlds/<world-slug>/curated/README.md`

目的：

- 获取中文/常用标题、整理批次、来源概况。
- 识别未解决项、风险、低置信或后续需补读内容。
- 判断是否适合直接回答，或是否需要引用 `curation-notes.md` 说明限制。

### 2. 按问题选择数据文件

在读完 README 后，根据问题类型选择下列文件：

| 文件 | 何时读取 | 典型用途 |
|---|---|---|
| `world.json` | 世界设定、时代背景、地理、组织、规则、力量体系、术语总览 | 回答“这个世界是什么”“世界规则/能力体系/阵营背景” |
| `characters-index.json` | 人物、身份、能力、出场关系、角色列表 | 查询某角色是谁、所属阵营、能力、人设摘要 |
| `knowledge-graph.json` | 概念、地点、组织、事件、物品、术语之间的语义关系 | 找设定关联、概念依赖、事件脉络、世界观知识网络 |
| `relationship-graph.json` | 角色间关系、阵营关系、敌友/师徒/家族/恋爱等边 | RP 互动、人物关系、冲突与亲密度判断 |
| `source-registry.json` | 来源条目、来源 ID、整理依据 | 需要溯源、核对来源、解释可信度时 |
| `curation-notes.md` | 整理备注、风险、缺口、人工判断 | 低置信、冲突、敏感/剧透、QA 或审稿场景 |

建议顺序：

1. `world.json`
2. `characters-index.json`
3. `knowledge-graph.json`
4. `relationship-graph.json`
5. `source-registry.json`
6. `curation-notes.md`

但这不是强制全读顺序；应按问题跳读。

## 常见查询场景

### A. “某世界的基本设定是什么？”

最小加载：

1. `manual-curation/INDEX.md`
2. `worlds/<world-slug>/curated/README.md`
3. `worlds/<world-slug>/curated/world.json`

可选：

- 若问题要求“哪些设定仍不完整/不确定”，再读 `curation-notes.md`。
- 若需要来源说明，再读 `source-registry.json`。

### B. “某角色是谁？能力/身份/所属阵营是什么？”

最小加载：

1. `INDEX.md`
2. 目标世界 `README.md`
3. `characters-index.json`

可选：

- 能力体系或组织背景不清楚时读 `world.json`。
- 角色与他人关系时读 `relationship-graph.json`。
- 需要概念/地点/事件关联时读 `knowledge-graph.json`。

### C. “两个角色是什么关系？RP 中该如何互动？”

最小加载：

1. `INDEX.md`
2. 目标世界 `README.md`
3. `characters-index.json`
4. `relationship-graph.json`

可选：

- 关系涉及事件、组织、契约、能力规则时读 `knowledge-graph.json` 或 `world.json`。
- 对会话安全、剧透边界、低置信关系读 `curation-notes.md`。

### D. “某设定/术语/组织/地点和哪些东西有关？”

最小加载：

1. `INDEX.md`
2. 目标世界 `README.md`
3. `world.json`
4. `knowledge-graph.json`

可选：

- 涉及人物，读 `characters-index.json`。
- 涉及阵营/人物关系，读 `relationship-graph.json`。

### E. “请基于某世界开 RP / 写 session 背景”

最小加载：

1. `INDEX.md`
2. 目标世界 `README.md`
3. `world.json`
4. `characters-index.json`

按需追加：

- 角色互动：`relationship-graph.json`
- 设定网络/事件脉络：`knowledge-graph.json`
- 剧透/不确定边界：`curation-notes.md`

运行时建议：

- 先建立“世界规则 + 当前场景 + 参与角色”的小上下文。
- 只加载本 session 会出现的角色和设定，不要把整个世界所有人物塞入提示。
- 对玩家尚未接触的关键真相，以“可隐藏信息/GM-only”处理。

### F. “跨世界比较或混合世界 RP”

最小加载：

1. `INDEX.md`
2. 每个目标世界的 `README.md`
3. 每个世界按问题读取 `world.json` 或 `characters-index.json`

建议：

- 先分别回答各世界事实，再给出比较/融合建议。
- 不要把一个世界的规则自动套用到另一个世界。
- 混合 RP 时明确哪些是 canon/curated 信息，哪些是为了 campaign 临时设定。

### G. “请给出来源/可信度/为什么这样整理？”

最小加载：

1. `INDEX.md`
2. 目标世界 `README.md`
3. `source-registry.json`
4. `curation-notes.md`

可选：

- 若要核对具体事实，再读包含该事实的 `world.json`、`characters-index.json` 或图谱文件。

## 最小上下文加载策略

- **一次只服务一个问题**：不要因为同一世界存在 7 个文件就全部读取。
- **先读小文件**：`README.md` 通常足以判断风险与下一步。
- **JSON 可局部理解**：对于大型 JSON，先找顶层结构或关键词，再读取相关片段；避免无关字段进入上下文。
- **回答中区分事实层级**：
  - `curated 明确记录`：可直接陈述。
  - `由图谱关系推断`：说明是基于关系推断。
  - `curation-notes 标为未解决/低置信`：必须标注不确定。
  - `RP 临时补全`：必须标注为 campaign/session 设定，不是原始 canon。

## 避免读取 raw 的规则

- 本库设计为 curated-only：运行时查询默认不需要 raw/worldbook 原文。
- 不要为了普通问答、RP、角色介绍读取 raw。
- 不要向用户承诺“已核对原始素材”，除非任务明确授权且实际完成。
- 当 curated 信息不足时，应：
  1. 说明当前 curated 资料不足；
  2. 指出可检查的 curated 文件或备注；
  3. 如需 raw 复核，作为后续 QA 建议提出，而不是擅自读取。

## 低置信、冲突与剧透处理

### 低置信/冲突

- 优先检查 `README.md` 与 `curation-notes.md` 是否记录未解决项。
- 若不同文件表述冲突：
  1. 不要强行合并为单一事实；
  2. 列出冲突来源；
  3. 给出“运行时可采用的保守版本”；
  4. 标注需要后续 QA 或原始来源复核。
- RP 中可把低置信内容降级为传闻、未公开情报或 GM 可选设定。

### 剧透

- 用户未明确要求完整剧情/真相时，默认避免揭示核心反转、最终敌人、死亡、身份真相等。
- 回答前可采用分层格式：
  - “无剧透摘要”
  - “轻度剧透”
  - “重大剧透（仅在用户明确要求时展开）”
- RP/session 中将重大剧透放入 GM-only notes，不放入玩家可见开场白。

## 给 `agent_team` 子代理的简短规则

可直接放入子代理任务说明：

1. 只读取 `manual-curation/INDEX.md` 和目标 `worlds/<slug>/curated/` 下的必要文件。
2. 进入世界后先读 `README.md`；除非问题需要，不要全量读取 7 个产物。
3. 问世界规则读 `world.json`；问角色读 `characters-index.json`；问概念/事件/地点关联读 `knowledge-graph.json`；问人物关系读 `relationship-graph.json`；问来源/可信度读 `source-registry.json` 和 `curation-notes.md`。
4. 不读取 raw/worldbook 原文；若资料不足，报告 curated 缺口和建议复核项。
5. 对低置信、冲突、未解决项、RP 临时补全、重大剧透必须显式标注。
6. 最终回答要列出实际读取的文件路径，不要声称读取了未读取文件。

## 输出建议

普通查询建议输出：

- **结论/摘要**
- **相关角色/设定**（如适用）
- **不确定或剧透提示**（如适用）
- **已读取文件**

RP/session 建议输出：

- **玩家可见背景**
- **当前场景与目标**
- **可出场 NPC/阵营**
- **世界规则注意事项**
- **GM-only：隐藏真相、剧透、低置信或可选设定**
- **已读取文件**
