# World Info Library

本目录是从项目 `campaigns/world-library/` 单独拆出的世界信息库，当前只包含手工框架化整理后的 `curated/` 产物与总索引，不包含原始 raw/worldbook 大文件。

## 内容

- `manual-curation/PLAN.md`：整理计划与规则
- `manual-curation/STATUS.md`：完成度与风险状态
- `manual-curation/INDEX.md`：世界总索引
- `worlds/<world-slug>/curated/`：每个世界的标准产物

每个世界的 `curated/` 目录应至少包含：

- `README.md`
- `world.json`
- `source-registry.json`
- `characters-index.json`
- `knowledge-graph.json`
- `relationship-graph.json`
- `curation-notes.md`

## 架构原则：最小框架 + 按源扩展

上述 7 个文件只是世界/角色数据的**最小可运行框架**，不是最终固定上限。整理时应根据本地源信息的完整、详细程度，在当前结构上按需增加扩展信息，避免为了统一格式而压缩或丢弃高密度设定。

允许并鼓励的扩展包括但不限于：

- `timeline.*` / `timeline/`：正史时间线、前传、篇章顺序、角色状态变化、关键历史节点。
- `arcs.*` / `plot-arcs/`：剧情篇章、冲突阶段、结局分支、RP 可切入点。
- `power-systems/`：能力体系、规则、限制、代价、技能/等级/强度分层。
- `factions/`：组织层级、成员、目标、冲突关系、势力演变。
- `locations/`：国家、城市、基地、异世界区域、旅行路线、剧情发生地。
- `relationships/`：人物关系网、阵营关系、亲属/师徒/敌对/情感线。
- `lore/`：历史、神话、科技、魔法、宇宙论、种族生态。
- `rp-notes/`：推荐开局、玩家可插入身份、时期选择、禁改核心、可改写空间、风格注意。

扩展规则：资料少的世界只保留最小框架；资料丰富的世界应补充可选模块。新增扩展文件必须在 `README.md` 或 `curation-notes.md` 中说明来源、可信度、未解决问题，并尽量在 `source-registry.json` 中保留来源引用。

## 当前状态

- 世界数：63
- 标准产物：63 × 7 = 441
- 原始素材：未包含

## 使用建议

运行时查询世界信息时，先读 `manual-curation/INDEX.md`，再进入对应 `worlds/<world-slug>/curated/` 按需读取。
