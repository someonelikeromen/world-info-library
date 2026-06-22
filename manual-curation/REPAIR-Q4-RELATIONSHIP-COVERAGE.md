# REPAIR-Q4-RELATIONSHIP-COVERAGE

检查日期：2026-06-22  
步骤：`relationship-coverage-q4`  
范围：`manual-curation/QA-AFTER-REPAIR-R3.md` 指定 LOW 最高的 10 个世界：`madan-no-ou`、`date-a-live`、`toriko`、`cross-ange`、`toaru`、`d-gray-man`、`kekkaishi`、`ikki-tousen`、`persona-5`、`world-god-only-knows`。

## 修复原则

- 不编造新关系；只结构化 `characters-index.json` 中已有 `relationships[]` 目标，或修正已经存在的 `relationship-graph.json` 节点类型/ID。
- 可确认映射到 indexed character 的目标写为 `target` + `targetType: "character"` + `resolutionStatus: "resolved"`。
- 组织、阵营、群体、地点、对象目标写为对应 `targetType` 或图节点 `type`，不冒充角色。
- 无法确认的目标保留原始 `label`/`relation`，添加 `resolutionStatus: "unresolved"` 与 `notes`。
- 一个关系文本同时指向多个已知目标时使用 `targets[]` 与 `resolutionStatus: "multi-target-resolved"`，避免强行编出单一边。
- 为 high/critical indexed character 补最小 relationship graph node，不强行补 edge。

## 修改摘要

| 世界 | characters-index 关系结构化 | graph 节点/类型修复 | 说明 |
|---|---:|---:|---|
| `madan-no-ou` | 69 | 0 | 中文关系标签按角色名/别名解析；无法唯一确认者保留 unresolved，多目标者保留 `targets[]`。 |
| `date-a-live` | 63 | 3 | 角色、DEM、Ratatoskr、精灵群体分别结构化；新增 `dem`/`ratatoskr`/`spirits` 非角色节点。 |
| `toriko` | 46 | 0 | `id:关系` 字符串转为结构化目标；`neo` 标记为 faction。 |
| `cross-ange` | 31 | 1 | `sala` 规范化到 `salamandinay`；为 `aura` 补 high/critical 最小角色节点。 |
| `toaru` | 0 | 15 | 将全部 `referenced-placeholder` 节点改为 character/group/faction/location 类型，并修正 `stiyl`/`kamisaki` 到索引 ID。 |
| `d-gray-man` | 25 | 1 | 拼写/简称规范化：`kanda`、`lenalee`、`nea`、`tiki-mikk`；`bookman` 保留 unresolved；补 `komui-lee` 节点。 |
| `kekkaishi` | 21 | 3 | `id:关系` 字符串转结构化目标；补 3 个 high/critical 最小角色节点。 |
| `ikki-tousen` | 23 | 4 | `id:关系` 字符串转结构化目标；两个未索引人物保留 unresolved；补 4 个 high/critical 节点。 |
| `persona-5` | 0 | 17 | 将中文/别名 placeholder 节点规范化到 indexed character、faction 或 object；`芳泽堇` 归并至 `kasumi-sumire`。 |
| `world-god-only-knows` | 0 | 14 | 将中文 placeholder 节点规范化到 indexed character、faction 或 object；保留非角色组织/对象类型。 |

## 复核结果

执行只读 Node 复核：10 个目标世界的 `characters-index.json` 与 `relationship-graph.json` 均可 `JSON.parse`；relationship graph `edges[].from/to` 均能解析到同文件节点。

| 指标 | 复核结果 |
|---|---:|
| 未结构化字符串关系目标 / 坏 character target | 0 |
| high/critical indexed character 缺 relationship graph node | 0 |
| relationship graph dangling edges | 0 |
| `referenced-placeholder` 节点 | 0 |
| 保留 `resolutionStatus: "unresolved"` | 21 |
| 保留 `resolutionStatus: "multi-target-resolved"` | 14 |

## 世界级剩余非阻断项

- `madan-no-ou`：仍有 14 个 unresolved 与 3 个 multi-target-resolved，主要是复合政治/家族关系标签，已保留原文和 notes，未冒充角色 ID。
- `date-a-live`：仍有 4 个 unresolved 与 11 个 multi-target-resolved，主要是“精灵群体/DEM/澪”等复合描述，已拆出可确认目标并保留多目标说明。
- `d-gray-man`：`bookman` 保留 unresolved，因为当前 indexed roster 未含该角色。
- `ikki-tousen`：`kakouen-myosai`、`chinkyu-koudai` 保留 unresolved，因为当前 indexed roster 未含对应角色。
- `toaru`、`persona-5`、`world-god-only-knows`：本轮只做节点类型/ID规范化，未新增关系边；仍可能存在非 high/critical 角色未完整覆盖到 relationship graph 的 LOW 提示。

## 风险与决定

- 结构化 `characters-index.relationships[]` 引入 object 形式，用于表达目标、目标类型、解析状态和 notes；这是为了降低 LOW 信号并保留不可确认事实，不新增 canon 断言。
- 对组织/阵营/地点/对象节点使用 `faction`、`group`、`location`、`object`，避免将非角色目标误注册为 character。
- 未处理本任务范围外的 MED/INFO 类别，如 `character-location`、`character-faction`、`world-kg-coverage`。

## 验证状态

- 已验证：目标 10 世界 JSON parse 成功。
- 已验证：目标 10 世界 relationship graph 无 edge-node 断链。
- 已验证：目标 10 世界 `referenced-placeholder` 节点为 0。
- 已验证：目标 10 世界 high/critical indexed character 缺 graph node 为 0。
- 未运行全仓 QA；本报告只复核 relationship target/coverage/placeholder 相关指标。
