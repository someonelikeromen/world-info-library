# REPAIR-SOURCE-QUALITY

日期：2026-06-22  
范围：`worlds/*/curated/source-registry.json`；未修改 canon 正文、角色、图谱或世界设定文件。

## 目标

处理 `manual-curation/REPAIR-REVIEW.md` 任务包 D：

1. 治理 10 个 `sources: []` 的 registry。
2. 复核 35 个 `conflictLog: []` 的 registry，并显式区分空值语义。
3. 不伪造来源事实；只从已有 `curatedFrom` / `sourcesUsed` / registry 内已有 trace 补可追踪来源，或标明不可作为已验证来源库。

## 修改原则

- `sources[]` 只由同一 registry 中已经存在的 `curatedFrom` 或 `sourcesUsed` trace 归一化生成。
- 新增来源条目的 `origin` 标为 `local archived worldbook trace`，`capture.method` 标为 `existing-curated-trace`。
- 每个新增来源条目 notes 均声明：这是本地归档 provenance 记录，不是独立 canon verification。
- 未新增任何新的剧情、设定、角色、冲突判断。
- 对空 `conflictLog` 不再默认为“已确认无冲突”，而是增加 `conflictReviewStatus`。

## 10 个空 sources registry 处理结果

本轮 10 个目标世界均能在原 registry 内找到已有 trace，因此均选择“补真实可追踪来源条目”，未保留空 registry。

| 世界 | 处理前 | 处理后 sources 数 | 来源依据 |
|---|---:|---:|---|
| `blue-archive` | 0 | 1 | 既有 `curatedFrom` |
| `cheng-long-adventures` | 0 | 1 | 既有 `curatedFrom` |
| `monster-hunter` | 0 | 4 | 既有 `sourcesUsed` |
| `overlord` | 0 | 4 | 既有 `sourcesUsed` |
| `persona-5` | 0 | 1 | 既有 `curatedFrom` |
| `rakudai-kishi` | 0 | 4 | 既有 `sourcesUsed` |
| `sora-no-otoshimono` | 0 | 5 | 既有 `sourcesUsed` |
| `sword-art-online` | 0 | 4 | 既有 `sourcesUsed` |
| `world-god-only-knows` | 0 | 1 | 既有 `curatedFrom` |
| `xianjian-1` | 0 | 1 | 既有 `curatedFrom` |

各 registry 的 `registryNotes` 已补充统一说明：`sources[]` 仅从既有本地归档 trace 补齐，应作为 provenance 记录使用，不代表独立 canon 校验完成。

## 空 conflictLog 语义治理

复核对象为全部 `worlds/*/curated/source-registry.json` 中 `conflictLog: []` 的 35 个 registry。

新增字段：

```json
"conflictReviewStatus": {
  "status": "not-reviewed | not-applicable",
  "reviewedAt": "2026-06-22",
  "reviewScope": "registry metadata only; no new canon/source facts asserted",
  "rationale": "..."
}
```

分类结果：

| status | 数量 | 语义 |
|---|---:|---|
| `not-reviewed` | 34 | 当前未登记冲突，但尚未独立复核为“确无冲突”。 |
| `not-applicable` | 1 | `acg-character-database` 是跨作品参考库，不是单一 canon 连续性；普通单世界冲突复核不适用。 |
| `confirmed-none` | 0 | 本轮未读取足够外部/原始材料来证明“确无冲突”，因此未使用该状态。 |

## 修改文件

### sources[] 由空补齐的 registry

- `worlds/blue-archive/curated/source-registry.json`
- `worlds/cheng-long-adventures/curated/source-registry.json`
- `worlds/monster-hunter/curated/source-registry.json`
- `worlds/overlord/curated/source-registry.json`
- `worlds/persona-5/curated/source-registry.json`
- `worlds/rakudai-kishi/curated/source-registry.json`
- `worlds/sora-no-otoshimono/curated/source-registry.json`
- `worlds/sword-art-online/curated/source-registry.json`
- `worlds/world-god-only-knows/curated/source-registry.json`
- `worlds/xianjian-1/curated/source-registry.json`

### 添加 conflictReviewStatus 的 35 个 registry

- `worlds/absolute-duo/curated/source-registry.json`
- `worlds/acg-character-database/curated/source-registry.json`
- `worlds/akame-ga-kill/curated/source-registry.json`
- `worlds/blue-archive/curated/source-registry.json`
- `worlds/bocchi-the-rock/curated/source-registry.json`
- `worlds/cheng-long-adventures/curated/source-registry.json`
- `worlds/chunibyo/curated/source-registry.json`
- `worlds/claymore/curated/source-registry.json`
- `worlds/cross-ange/curated/source-registry.json`
- `worlds/d-gray-man/curated/source-registry.json`
- `worlds/gate-jsdf/curated/source-registry.json`
- `worlds/haganai/curated/source-registry.json`
- `worlds/hidan-no-aria/curated/source-registry.json`
- `worlds/ikki-tousen/curated/source-registry.json`
- `worlds/jojo/curated/source-registry.json`
- `worlds/kaguya-sama/curated/source-registry.json`
- `worlds/kekkaishi/curated/source-registry.json`
- `worlds/kill-la-kill/curated/source-registry.json`
- `worlds/majo-no-tabitabi/curated/source-registry.json`
- `worlds/monster-hunter/curated/source-registry.json`
- `worlds/omamori-himari/curated/source-registry.json`
- `worlds/overlord/curated/source-registry.json`
- `worlds/persona-5/curated/source-registry.json`
- `worlds/rakudai-kishi/curated/source-registry.json`
- `worlds/sekirei/curated/source-registry.json`
- `worlds/sora-no-otoshimono/curated/source-registry.json`
- `worlds/spice-and-wolf/curated/source-registry.json`
- `worlds/sword-art-online/curated/source-registry.json`
- `worlds/taimanin/curated/source-registry.json`
- `worlds/testament-sister-new-devil/curated/source-registry.json`
- `worlds/toaru/curated/source-registry.json`
- `worlds/toriko/curated/source-registry.json`
- `worlds/world-god-only-knows/curated/source-registry.json`
- `worlds/xianjian-1/curated/source-registry.json`
- `worlds/zero-no-tsukaima/curated/source-registry.json`

## 验证结果

本地脚本复核：

```json
{
  "sourceRegistryFiles": 63,
  "parseableSourceRegistryFiles": 63,
  "emptySources": 0,
  "emptyConflictLogMissingStatus": 0,
  "conflictReviewStatusCounts": {
    "not-reviewed": 34,
    "not-applicable": 1
  },
  "duplicateSourceIdsWithinRegistry": 0
}
```

补充 JSON/schema/type 快速复核：

```json
{
  "worldCount": 63,
  "jsonTotal": 315,
  "parseErrors": 0,
  "missingFiles": 0,
  "schemaMismatch": 0,
  "strictWorldTypeMismatches": 0
}
```

## 剩余风险与后续建议

- 本轮清零的是“空 sources registry”结构风险；新增来源记录仍主要是本地归档 trace，不等于已完成原作权威来源交叉校验。
- 34 个 `not-reviewed` 空 conflictLog 仍需后续人工阅读后才能升级为 `confirmed-none` 或登记具体 conflict。
- `referenced-placeholder`、`granular-reference-placeholder`、`unregistered-placeholder` 的逐项消化未在本轮完全展开；应在后续来源深挖中继续合并到真实 source 或保留明确风险说明。
- MED/LOW/INFO cross-reference 规范化、关系图与 KG 覆盖不属于本步骤修改范围。

## 当前判定

本任务包 D 范围内：

- 10 个空 `sources[]`：已清零。
- 35 个空 `conflictLog`：已全部显式标注空值语义。
- 未伪造来源事实；所有新增来源均来自 registry 内已有 trace。
- 本轮未发现新的 JSON/schema/P1 类型问题。
