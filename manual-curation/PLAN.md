# 世界观手工框架化整理计划

## 授权与方式

- 执行方式：全自动批执行，不再逐步询问确认。
- 整理方式：禁止用脚本自动抽取/改写正文；由 agent 阅读已有归档与原始世界书条目后手工归纳。
- 可用 Pi 机制：使用 `agent_team` 子代并行阅读、整理、写入。
- 写入范围：`campaigns/world-library/worlds/<worldSlug>/curated/` 与 `campaigns/world-library/manual-curation/`。
- 保护原则：不覆盖 `raw/`、`imports/raw/`、既有自动归档分类文件；手工整理结果单独落在 `curated/`。

## 需要遵循的规则

- `skill/world-source-ingestion.md`
- `skill/graph-management.md`
- `rules/rp-core-rules.md`
- `rules/rp-combat-rating-rules.md`
- `templates/rp-framework/world-template.json`
- `templates/rp-framework/source-registry-template.json`
- `templates/rp-framework/knowledge-graph-template.json`
- `templates/rp-framework/relationship-graph-template.json`

## 每个世界的标准产物

当前标准产物是世界/角色数据的**最小可运行框架**，不是最终固定上限。每个 `campaigns/world-library/worlds/<worldSlug>/curated/` 至少输出：

1. `README.md`
   - 本世界整理状态、来源范围、未解决问题、下一步。
2. `world.json`
   - 按 `rp-world-v1` 结构整理世界基础信息、力量体系、势力、能量环境、世界规则、地点、公开/隐藏事件。
3. `source-registry.json`
   - 按 `rp-source-registry-v1` 记录来源、可信度、适用对象、冲突。
4. `characters-index.json`
   - 详细人物清单：人物、别名、身份、阵营、能力、关系、可见性、来源。
5. `knowledge-graph.json`
   - 按 `rp-knowledge-graph-v1` 建节点和边。
6. `relationship-graph.json`
   - 按 `rp-relationship-graph-v1` 建人物/势力节点和关系边。
7. `curation-notes.md`
   - 人工判断、冲突、低置信、未归类项。

### 可选扩展产物

如果源信息足够完整详细，应在当前结构上增加扩展模块，而不是把所有信息强行压缩进 7 个基础文件。可选扩展包括但不限于：

- `timeline.*` / `timeline/`：正史时间线、前传事件、篇章顺序、角色状态变化、关键历史节点。
- `arcs.*` / `plot-arcs/`：剧情篇章、阶段冲突、分支结局、RP 切入点。
- `power-systems/`：能力体系、规则、限制、代价、技能与强度分层。
- `factions/`：组织层级、成员、目标、冲突关系、势力演变。
- `locations/`：国家、城市、基地、异世界区域、旅行路线、剧情发生地。
- `relationships/`：人物关系网、阵营关系、亲属/师徒/敌对/情感线。
- `lore/`：历史、神话、科技、魔法、宇宙论、种族生态。
- `rp-notes/`：推荐开局、玩家可插入身份、时期选择、禁改核心、可改写空间、风格注意。

扩展原则：资料少的世界只保留最小框架；资料丰富的世界应补充可选模块。新增扩展文件必须在 `README.md` 或 `curation-notes.md` 中说明来源、可信度、未解决问题，并尽量在 `source-registry.json` 中保留来源引用。

## 人物清单字段

`characters-index.json` 使用：

```json
{
  "schema": "rp-characters-index-v1",
  "worldId": "",
  "characters": [
    {
      "id": "",
      "name": "",
      "aliases": [],
      "visibility": "public/private/gm-only/locked/false-rumor",
      "summary": "",
      "roles": [],
      "factions": [],
      "locations": [],
      "powerSystems": [],
      "abilities": [],
      "items": [],
      "relationships": [],
      "importance": "low/medium/high/critical",
      "evidenceLevel": "S/A/B/C/D/E",
      "sourceRefs": [],
      "notes": ""
    }
  ],
  "indices": {
    "byFaction": {},
    "byPowerSystem": {},
    "byVisibility": {},
    "majorCharacters": []
  }
}
```

## 分批策略

### Batch A：大体量/优先样板

- type-moon-nasuverse
- honkai-impact-3rd
- danmachi
- naruto
- high-school-dxd
- dungeon-fighter-online
- tokyo-ghoul
- evangelion
- kimetsu-no-yaiba
- marvel-cinematic-universe

### Batch B：中高体量战斗/力量体系世界

- dragon-ball
- negima-uq-holder
- kenichi
- senran-kagura
- seikoku-no-dragonar
- campione
- strike-the-blood
- record-of-ragnarok
- black-bullet
- gundam-seed

### Batch C：中体量/机制清晰世界

- gate-jsdf
- hidan-no-aria
- cross-ange
- ikki-tousen
- saijaku-muhai-bahamut
- d-gray-man
- to-love-ru
- kekkaishi
- toriko
- madan-no-ou

### Batch D：中小体量世界

- rozen-maiden
- elemental-gelade
- sekirei
- kaguya-sama
- absolute-duo
- omamori-himari
- spice-and-wolf
- rakudai-kishi
- dantalian-no-shoka
- date-a-live

### Batch E：小体量/轻设定世界

- sora-no-otoshimono
- overlord
- monster-hunter
- sword-art-online
- xianjian-1
- cheng-long-adventures
- world-god-only-knows
- blue-archive
- persona-5
- majo-no-tabitabi

### Batch F：剩余与特殊库

- infinite-stratos
- kill-la-kill
- akame-ga-kill
- taimanin
- chunibyo
- jojo
- bocchi-the-rock
- haganai
- zero-no-tsukaima
- claymore
- toaru
- acg-character-database

## 验收标准

单个世界视为阶段完成，需要满足：

- 有 `curated/README.md` 标记来源和整理程度。
- 有可读的世界主档 `world.json`。
- 有详细人物清单 `characters-index.json`。
- 有来源索引 `source-registry.json`。
- 有知识图谱和关系图谱。
- 有冲突/低置信/未解决记录。
- 不覆盖原始归档。
