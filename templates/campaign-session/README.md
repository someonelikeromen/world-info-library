# Campaign / Session 状态模板

本目录提供世界无关的 RP campaign/session 层状态模板，用于把 `worlds/<world-slug>/curated/` 的静态世界资料接入实际跑团或角色扮演运行时。

> 约束：这些模板不修改任何 `worlds/*/curated` 正文；所有实际游玩中的变化都记录为 campaign/session 状态与 delta。

## 文件

- `campaign-template.json`：长期 campaign 档案；绑定当前世界、角色卡、规则偏好、可见性策略与来源。
- `session-template.json`：单次 session 记录；记录场景、时间、参与者、回合/事件、检索上下文与产出 delta。
- `state-template.json`：运行中状态快照；记录玩家/主角状态、地点、时间、关系/知识/地图覆盖层、低置信与待核查事项。
- `session-graph-delta-template.json`：本 session 对关系图与知识图的增量变更。
- `map-delta-template.json`：地点、区域、路径、地图可见性与占用状态的增量变更。
- `progress-template.md`：人工/自动 QA 与游玩进度汇总模板。

## 推荐运行时流程

1. **选择当前世界**：从 `manual-curation/INDEX.md` 定位 `worldId/worldSlug`，再读取对应 `worlds/<world-slug>/curated/README.md` 与核心 JSON。
2. **初始化 campaign**：复制 `campaign-template.json`，填入 `campaignId`、当前世界、角色卡与安全/叙事偏好。
3. **初始化状态**：复制 `state-template.json`，建立初始时间、地点、玩家/主角状态、可见性边界。
4. **开 session**：复制 `session-template.json`，记录本次目标、已检索来源、场景与事件。
5. **写 delta，不改 curated**：关系变化、知识揭露和地图变化分别写入 `session-graph-delta-template.json` 与 `map-delta-template.json` 的实例。
6. **合并快照**：session 结束后把已确认 delta 折叠进 campaign state；保留来源引用、置信度与可见性。
7. **复核**：使用 `progress-template.md` 记录 JSON/schema 校验、交叉引用校验、高风险抽样复核、运行时检索文档状态。

## 可见性约定

- `public`：玩家与 GM 均可见，可直接在叙事中使用。
- `player_known`：当前 campaign 中玩家已知；可能来自 session 揭露，不一定是世界初始公开资料。
- `gm_only`：仅 GM/系统可见；不得直接泄露给玩家。
- `secret`：强隐藏秘密；只有满足 `revealConditions` 或明确 GM 决定时才揭露。
- `unknown`：未确认或资料不足。

## 置信度约定

- `A`：高置信；有明确 curated 来源或 session 内强证据。
- `B`：中高置信；资料一致但细节可补。
- `C`：中低置信；推断、概括或上下文依赖。
- `D`：低置信；需标注 `lowConfidenceNotes` 并列入待核查。
- `E`：冲突/不可信；只能作为争议线索或待裁定事项。

## 来源引用约定

所有重要状态与 delta 应保留来源：

```json
{
  "sourceRefs": [
    {
      "kind": "curated|session-log|gm-ruling|player-input|derived",
      "path": "worlds/<world-slug>/curated/world.json",
      "refId": "src-or-node-id-or-event-id",
      "quote": "可选短摘录或摘要",
      "confidence": "A"
    }
  ]
}
```

## ID 建议

- campaign：`camp-<world-slug>-<short-name>`
- session：`sess-YYYYMMDD-NN`
- state：`state-<campaign-id>-latest` 或 `state-YYYYMMDD-NN`
- graph delta：`gdelta-<session-id>`
- map delta：`mdelta-<session-id>`
