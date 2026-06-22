# REPAIR-P1-TYPES

日期：2026-06-22  
范围：仅处理 `manual-curation/REPAIR-REVIEW.md` 任务包 A 指定的 17 个 `worlds/*/curated/world.json` 中两类 P1 类型不匹配。  
写入边界：本报告与下列 17 个 `world.json`。

## 修复目标

将 34 项严格类型不匹配清零：

- `sandboxPrinciple`: `string` → `object`
  - 新结构：`{"summary": 原字符串, "notes": []}`
- `foreignPowerSuppressionDefault`: `boolean` → `object`
  - 新结构：`{"enabled": 原布尔值, "summary": "", "notes": []}`

本轮仅做 JSON 类型兼容迁移；未扩写 canon 正文，未新增设定判断。

## 已修改文件

| 世界 | 文件 | 处理结果 |
|---|---|---|
| `absolute-duo` | `worlds/absolute-duo/curated/world.json` | 两字段已迁移为 object |
| `danmachi` | `worlds/danmachi/curated/world.json` | 两字段已迁移为 object |
| `dungeon-fighter-online` | `worlds/dungeon-fighter-online/curated/world.json` | 两字段已迁移为 object |
| `elemental-gelade` | `worlds/elemental-gelade/curated/world.json` | 两字段已迁移为 object |
| `evangelion` | `worlds/evangelion/curated/world.json` | 两字段已迁移为 object |
| `high-school-dxd` | `worlds/high-school-dxd/curated/world.json` | 两字段已迁移为 object |
| `honkai-impact-3rd` | `worlds/honkai-impact-3rd/curated/world.json` | 两字段已迁移为 object |
| `kaguya-sama` | `worlds/kaguya-sama/curated/world.json` | 两字段已迁移为 object |
| `kimetsu-no-yaiba` | `worlds/kimetsu-no-yaiba/curated/world.json` | 两字段已迁移为 object |
| `marvel-cinematic-universe` | `worlds/marvel-cinematic-universe/curated/world.json` | 两字段已迁移为 object |
| `naruto` | `worlds/naruto/curated/world.json` | 两字段已迁移为 object |
| `omamori-himari` | `worlds/omamori-himari/curated/world.json` | 两字段已迁移为 object |
| `rozen-maiden` | `worlds/rozen-maiden/curated/world.json` | 两字段已迁移为 object |
| `sekirei` | `worlds/sekirei/curated/world.json` | 两字段已迁移为 object |
| `spice-and-wolf` | `worlds/spice-and-wolf/curated/world.json` | 两字段已迁移为 object |
| `tokyo-ghoul` | `worlds/tokyo-ghoul/curated/world.json` | 两字段已迁移为 object |
| `type-moon-nasuverse` | `worlds/type-moon-nasuverse/curated/world.json` | 两字段已迁移为 object |

## 复核方法

使用本地 Node.js 脚本扫描 `worlds/*/curated`：

1. 统计世界目录与 5 类 curated JSON。
2. 对全部 curated JSON 执行 `JSON.parse`。
3. 检查 5 类文件是否齐备且无未识别 JSON 文件名。
4. 检查 schema 是否为：
   - `rp-world-v1`
   - `rp-source-registry-v1`
   - `rp-characters-index-v1`
   - `rp-knowledge-graph-v1`
   - `rp-relationship-graph-v1`
5. 检查 `QA-JSON-SCHEMA.md` 列出的顶层必备字段是否存在。
6. 严格检查所有 `world.json` 的：
   - `sandboxPrinciple` 为非数组 object。
   - `foreignPowerSuppressionDefault` 为非数组 object。

## 复核结果

```json
{
  "worldCount": 63,
  "jsonTotal": 315,
  "parseErrors": 0,
  "missingFiles": 0,
  "unknownFiles": 0,
  "schemaMismatch": 0,
  "missingFields": 0,
  "strictWorldTypeMismatches": 0
}
```

## 结论

任务包 A 的 17 个世界、34 项 P1 严格类型不匹配已清零。

- `sandboxPrinciple` 已从 string 迁移为 `{summary, notes}` object，并保留原字符串于 `summary`。
- `foreignPowerSuppressionDefault` 已从 boolean 迁移为 `{enabled, summary, notes}` object，并保留原布尔值于 `enabled`。
- 本轮复核未发现 JSON parse、schema mismatch、顶层必备字段缺失或上述两字段严格类型不匹配。

## 非本轮范围的已知残留

`manual-curation/REPAIR-REVIEW.md` 中提到的 MED 规范化、空 source registry/conflictLog、LOW/INFO 关系和 KG 覆盖属于后续任务包 B/C/D/E；本轮未修改这些内容，也未声称其已清零。
