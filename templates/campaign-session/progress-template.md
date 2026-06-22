# Campaign / Session QA 与进度汇总模板

- Campaign ID: `<camp-...>`
- World: `<worldName>` (`<worldId>` / `worlds/<world-slug>/curated/`)
- Current Session: `<sess-YYYYMMDD-01>`
- State Snapshot: `<state-id>`
- Last Updated: `<ISO-8601>`

## 1. JSON / Schema 校验

| 文件 | Schema 字段 | JSON 有效 | 必填块完整 | 状态 | 备注 |
|---|---|---:|---:|---|---|
| `campaign-template.json` / campaign 实例 | `rp-campaign-v1` | ☐ | ☐ | pending | 当前世界、角色卡、可见性、来源引用需填写 |
| `session-template.json` / session 实例 | `rp-session-v1` | ☐ | ☐ | pending | 事件、检索记录、知识/关系 delta 摘要需填写 |
| `state-template.json` / state 实例 | `rp-campaign-state-v1` | ☐ | ☐ | pending | 玩家/主角状态、地点、时间、地图状态需填写 |
| `session-graph-delta-template.json` / delta 实例 | `rp-session-graph-delta-v1` | ☐ | ☐ | pending | 关系 delta 与知识揭露 delta 需可追溯 |
| `map-delta-template.json` / delta 实例 | `rp-map-delta-v1` | ☐ | ☐ | pending | 地点/路径/占用/地图可见性需可追溯 |

### Schema 检查说明

- 所有 JSON 文件必须为标准 JSON，不使用注释或尾逗号。
- `schema` 字段必须与文件用途一致。
- 重要变更必须包含 `sourceRefs`、`confidence`、`visibility`。
- 低置信内容必须写入 `lowConfidenceNotes` 或等价字段。

## 2. 交叉引用校验

| 引用类型 | 应解析到 | 状态 | 未解析 ID | 处理动作 |
|---|---|---|---|---|
| `worldId/worldSlug` | `manual-curation/INDEX.md` 与 `worlds/<slug>/curated/world.json` | pending |  |  |
| `characterId` | `characters-index.json` 或 campaign `characterCards` | pending |  |  |
| `cardId` | campaign `characterCards` / state `characterStates` | pending |  |  |
| `locationId` | curated `world.json.locations` 或 campaign/map delta 新建地点 | pending |  |  |
| `knowledgeNodeId` | `knowledge-graph.json.nodes` 或 campaign knowledge overlay | pending |  |  |
| `relationshipId` | `relationship-graph.json.edges` 或 campaign relationship overlay | pending |  |  |
| `eventId` | session `eventLog` | pending |  |  |
| `mapId/routeId` | campaign `mapState` 或 `map-delta` | pending |  |  |
| `sourceRefs.refId` | `source-registry.json`、curated node id、session event id 或 GM ruling id | pending |  |  |

## 3. 高风险质量抽样复核

高风险项包括：秘密揭露、角色关系大幅变化、主角状态重大损伤/死亡、地图关键通路变化、与 curated 正文可能冲突的设定、低置信度 C/D/E 的事实。

| 抽样 ID | 类型 | 关联文件/字段 | 风险等级 | 复核结论 | 修正动作 |
|---|---|---|---|---|---|
| `sample-001` | knowledge reveal | `<file>#<id>` | high | pending |  |
| `sample-002` | relationship delta | `<file>#<id>` | medium | pending |  |
| `sample-003` | map/location delta | `<file>#<id>` | medium | pending |  |

复核清单：

- ☐ 未把 `gm_only` / `secret` 直接写入玩家可见摘要。
- ☐ 未修改 `worlds/*/curated` 正文。
- ☐ 与 curated 事实冲突的分支已标记为 branch/retcon/low confidence。
- ☐ 所有重大 delta 有 session event 或 GM ruling 来源。
- ☐ 玩家/主角状态变化有事件支撑。
- ☐ 地图可见性与实际占用状态分离记录。

## 4. 运行时检索文档

| 检索目的 | 已读路径 | 关键 ID | 结论摘要 | 可见性 | 置信度 | 后续 |
|---|---|---|---|---|---|---|
| 世界定位 | `manual-curation/INDEX.md` | `<worldId>` |  | gm_only | B |  |
| 世界规则 | `worlds/<slug>/curated/world.json` | `<ids>` |  | gm_only | B |  |
| 角色卡 | `worlds/<slug>/curated/characters-index.json` | `<ids>` |  | gm_only | B |  |
| 知识图 | `worlds/<slug>/curated/knowledge-graph.json` | `<ids>` |  | gm_only | B |  |
| 关系图 | `worlds/<slug>/curated/relationship-graph.json` | `<ids>` |  | gm_only | B |  |
| 来源注册 | `worlds/<slug>/curated/source-registry.json` | `<src ids>` |  | gm_only | B |  |

检索缺口：

- `<gap-001>`：`<缺失资料>`；临时处理：`<如何低置信处理>`；复核动作：`<下一步>`。

## 5. Campaign / Session 进度

### 当前世界

- World ID: `<worldId>`
- World Name: `<worldName>`
- Curated Root: `worlds/<world-slug>/curated/`
- 当前可用来源：`<world.json / characters-index.json / ...>`

### 当前角色卡

| Card ID | 名称 | 类型 | Linked Character ID | 当前地点 | 可见性 | 状态摘要 |
|---|---|---|---|---|---|---|
| `pc-001` | `<name>` | player-character |  | `<location>` | player_known |  |
| `npc-001` | `<name>` | npc | `<characterId>` | `<location>` | gm_only |  |

### 当前 Session

- Session ID: `<sess-...>`
- Session Title: `<title>`
- In-world Time: `<start>` → `<current/end>`
- Current Location: `<locationId>`
- Focus: `<goal / scene focus>`

### 玩家/主角状态

- Health / Conditions: `<summary>`
- Resources: `<summary>`
- Inventory: `<summary>`
- Goals: `<short-term / long-term>`
- Low-confidence state assumptions: `<none or list>`

### 地点与地图状态

- Active Map ID: `<map-id>`
- Visible Regions: `<ids>`
- Hidden/GM-only Regions: `<ids>`
- Blocked/Conditional Routes: `<ids>`
- Active Hazards/Assets: `<ids>`

### 关系 Delta 摘要

| Delta ID | From | To | 变化 | 可见性 | 置信度 | 来源事件 |
|---|---|---|---|---|---|---|
| `rel-delta-001` | `<id>` | `<id>` | `<summary>` | player_known | B | `evt-001` |

### 知识揭露 Delta 摘要

| Delta ID | Knowledge ID | 揭露内容 | From → To | 已知者 | 置信度 | 来源事件 |
|---|---|---|---|---|---|---|
| `kg-delta-001` | `<id>` | `<summary>` | secret → player_known | `pc-001` | B | `evt-001` |

### 来源引用与低置信说明

- 关键来源：
  - `<sourceRef>`：`<why used>`
- 低置信说明：
  - `<lc-id>`：`<topic>`；原因：`<why>`；影响：`<impact>`；复核：`<action>`

## 6. 决策与风险

- 已确认决策：
  - `<decision>`
- 待 GM/玩家确认：
  - `<pending>`
- 风险：
  - `<risk>` → 缓解：`<mitigation>`

## 7. 下一步

- ☐ 完成本 session 事件记录。
- ☐ 应用已批准的 graph/map delta 到 state 快照。
- ☐ 更新玩家可见 recap，隐藏 GM-only 内容。
- ☐ 复核 unresolved refs 与 low confidence notes。
- ☐ 准备下一 session hooks。
