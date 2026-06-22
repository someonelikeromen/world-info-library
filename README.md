# World Info Library

本目录是从项目 `campaigns/world-library/` 单独拆出的世界信息库，当前只包含手工框架化整理后的 `curated/` 产物与总索引，不包含原始 raw/worldbook 大文件。

## 内容

- `manual-curation/PLAN.md`：整理计划与规则
- `manual-curation/STATUS.md`：完成度与风险状态
- `manual-curation/INDEX.md`：世界总索引
- `worlds/<world-slug>/curated/`：每个世界的标准产物

每个世界的 `curated/` 目录应包含：

- `README.md`
- `world.json`
- `source-registry.json`
- `characters-index.json`
- `knowledge-graph.json`
- `relationship-graph.json`
- `curation-notes.md`

## 当前状态

- 世界数：63
- 标准产物：63 × 7 = 441
- 原始素材：未包含

## 使用建议

运行时查询世界信息时，先读 `manual-curation/INDEX.md`，再进入对应 `worlds/<world-slug>/curated/` 按需读取。
