# REPAIR-Q4-KG-COVERAGE

修复日期：2026-06-22  
步骤：`kg-coverage-q4`  
目标：降低 `manual-curation/QA-AFTER-REPAIR-R3.md` 中 INFO 高优先世界的 `world-kg-coverage` 信号。  
范围：仅修改目标世界的 `knowledge-graph.json`，读取对应 `world.json`，并创建本报告。

## 处理原则

- 只为 `world.json` 已有的 `factions[]`、`locations[]`、`powerSystems[]` 补最小 KG node。
- 不新增未证实设定，不新增关系 edge。
- 新节点字段仅使用 `world.json` 中已有 `id`、`name`/`label`、必要时 `summary`。
- 已有同 id KG node 视为已覆盖，不重复创建。

## 修改统计

| 世界 | 新增 KG nodes | 修复后 world 层缺口 |
|---|---:|---:|
| `madan-no-ou` | 38 | 0 |
| `dantalian-no-shoka` | 36 | 0 |
| `dragon-ball` | 24 | 0 |
| `gate-jsdf` | 24 | 0 |
| `marvel-cinematic-universe` | 21 | 0 |
| `d-gray-man` | 21 | 0 |
| `naruto` | 17 | 0 |
| `honkai-impact-3rd` | 15 | 0 |
| `cross-ange` | 13 | 0 |
| `toriko` | 13 | 0 |
| **合计** | **222** | **0** |

说明：`marvel-cinematic-universe` R3 报告中 INFO 缺口为 22；其中 `asgard` 已作为 KG node 存在，且同 id 覆盖 world 层 faction/location 之一，因此本轮实际新增 21 个 node 即清零目标缺口。

## 文件变更

- `worlds/madan-no-ou/curated/knowledge-graph.json`：补齐 world 层 38 个 faction/location/powerSystem 节点。
- `worlds/dantalian-no-shoka/curated/knowledge-graph.json`：补齐 world 层 36 个 faction/location/powerSystem 节点。
- `worlds/dragon-ball/curated/knowledge-graph.json`：补齐 world 层 24 个 faction/location/powerSystem 节点。
- `worlds/gate-jsdf/curated/knowledge-graph.json`：补齐 world 层 24 个 faction/location/powerSystem 节点。
- `worlds/marvel-cinematic-universe/curated/knowledge-graph.json`：补齐 world 层 21 个 faction/location/powerSystem 节点。
- `worlds/d-gray-man/curated/knowledge-graph.json`：补齐 world 层 21 个 faction/location/powerSystem 节点。
- `worlds/naruto/curated/knowledge-graph.json`：补齐 world 层 17 个 faction/location/powerSystem 节点。
- `worlds/honkai-impact-3rd/curated/knowledge-graph.json`：补齐 world 层 15 个 faction/location/powerSystem 节点。
- `worlds/cross-ange/curated/knowledge-graph.json`：补齐 world 层 13 个 faction/location/powerSystem 节点。
- `worlds/toriko/curated/knowledge-graph.json`：补齐 world 层 13 个 faction/location/powerSystem 节点。

## 复核结果

对 10 个目标世界执行复核：

- `world.json` 中 `factions[]`、`locations[]`、`powerSystems[]` 的 id 均能在同世界 `knowledge-graph.json:nodes[].id` 中找到。
- 目标世界 `knowledge-graph.json` 无重复 node id。
- 目标世界 `knowledge-graph.json` 无 edge-node 断链。

全库 KG 结构复核：

- 世界数：63。
- `knowledge-graph.json` parse 失败：0。
- 重复 KG node id：0。
- KG edge-node 断链：0。

## 残留非阻断问题

- 本轮只处理 R3 指定的 10 个 INFO 高优先世界；其他世界的 `world-kg-coverage`、MED/LOW 规范化问题未纳入修改范围。
- 本轮未处理 R3 报告中的 placeholder 信号；指定 10 个世界不在 R3 placeholder 世界列表中。
- 新增 KG node 为最小覆盖节点，未补写复杂关系；后续可在有来源依据时继续补强关系与摘要。

## 验证命令

使用只读 Node.js 脚本完成两类验证：

1. 目标世界覆盖验证：检查 world 层 faction/location/powerSystem id 是否全部存在于 KG nodes，同时检查目标 KG 重复 id 与 edge-node 断链。
2. 全库 KG 结构验证：检查 63 个世界的 KG JSON parse、重复 node id、edge-node 断链。

验证状态：通过。
