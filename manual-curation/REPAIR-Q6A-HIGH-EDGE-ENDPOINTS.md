# REPAIR-Q6A-HIGH-EDGE-ENDPOINTS

检查日期：2026-06-22  
步骤：`q6a-fix-edge-endpoints`  
目标：修复 `manual-curation/QA-AFTER-REPAIR-Q5.md` 报告的 21 条 relationship-graph HIGH edge endpoint 断链。

## 修复范围

仅修改以下允许文件：

- `worlds/blue-archive/curated/relationship-graph.json`
- `worlds/monster-hunter/curated/relationship-graph.json`
- `worlds/overlord/curated/relationship-graph.json`
- `worlds/sora-no-otoshimono/curated/relationship-graph.json`
- `manual-curation/REPAIR-Q6A-HIGH-EDGE-ENDPOINTS.md`

未新增节点，未新增 canon，未修改关系语义；仅把 `relationships[]` 与 `edges[]` 中旧中文端点同步为同文件已存在的 `nodes[].id`。

## 端点同步映射

### blue-archive

| 旧端点 | 已存在 node id |
|---|---|
| `茶会` | `tea-party-host` |
| `万魔殿` | `pandemonium-member` |
| `风纪委员会` | `prefect-team-student` |
| `温泉开发部` | `hot-spring-dev` |
| `研讨会` | `millennium-seminar` |
| `C&C` | `c-and-c-agent` |
| `玄龙门` | `genryumon-member` |
| `玄武商会` | `genbu-merchant` |

### monster-hunter

| 旧端点 | 已存在 node id |
|---|---|
| `猎人公会` | `guild` |
| `禁忌怪物` | `forbidden` |
| `古龙观测局` | `observatory` |

### overlord

| 旧端点 | 已存在 node id |
|---|---|
| `安兹·乌尔·恭` | `ainz` |

### sora-no-otoshimono

| 旧端点 | 已存在 node id |
|---|---|
| `西纳普斯` | `synapse` |

## 修改说明

- 同步字段：`from`、`to`、`source`、`target`。
- 同步区域：`relationships[]` 与 `edges[]`，保持同文件两段关系端点一致。
- 映射依据：同文件 `nodes[].id`、`label` 以及 `metadata.q4SourceRiskReview.originalId/mappedId` 中已经存在的 Q4/Q5 映射信息。
- 数据约束：所有目标 id 在写入前均已确认存在于同文件 `nodes[]`。

## 验证结果

### 目标文件 dangling endpoint 校验

只读 Node 扫描 4 个目标 relationship graph，检查 `relationships[]` 与 `edges[]` 的 `from/to/source/target` 是否均存在于同文件 `nodes[].id`：

| 文件 | dangling endpoints |
|---|---:|
| `worlds/blue-archive/curated/relationship-graph.json` | 0 |
| `worlds/monster-hunter/curated/relationship-graph.json` | 0 |
| `worlds/overlord/curated/relationship-graph.json` | 0 |
| `worlds/sora-no-otoshimono/curated/relationship-graph.json` | 0 |

### Q6A 全量阻断项复核

仓库未发现现成 QA 脚本或 `package.json`，因此执行等价只读 Node 全量扫描，覆盖 `worlds/*/curated` 下 63 个世界、315 个 JSON：

| 指标 | 结果 |
|---|---:|
| 世界目录数 | 63 |
| JSON 文件数 | 315 |
| P0 | 0 |
| P1 | 0 |
| HIGH | 0 |

复核项目包括 JSON parse、每世界 5 类 curated JSON 齐备、未知 JSON 文件、graph string nodes、duplicate node id、relationship/knowledge edge endpoint 断链、空 `source-registry.sources` 与空 `conflictLog` 语义状态。Q6A 后 P0/P1/HIGH 已回到 0。

## 风险与边界

- 本次未处理 `QA-AFTER-REPAIR-Q5.md` 中列出的 MED/LOW/INFO 残留；它们不在 Q6A mutation scope 内。
- 本次未新增、删除或重命名任何 node；若后续要收敛 LOW relationship target，需要单独任务处理。
