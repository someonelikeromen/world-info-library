# date-a-live curation notes

## 人工阅读记录

本次为手工归纳，未使用脚本自动抽取/分类/生成正文。已阅读/抽查：

- `campaigns/world-library/manual-curation/PLAN.md`
- `campaigns/world-library/worlds/date-a-live/manifest.json`
- `campaigns/world-library/worlds/date-a-live/source-registry.json`
- `campaigns/world-library/worlds/date-a-live/world/world.json`
- `campaigns/world-library/worlds/date-a-live/characters/characters.json`
- `campaigns/world-library/worlds/date-a-live/factions/factions.json`
- `campaigns/world-library/worlds/date-a-live/power-systems/power-systems.json`
- `campaigns/world-library/worlds/date-a-live/locations/locations.json`
- `campaigns/world-library/worlds/date-a-live/canon-reference/plot-summary.json`

## 主要判断

1. **默认基线**：采用主线天宫市世界观，核心是空间震、精灵、封印、Ratatoskr/AST/DEM 对立和始源精灵因果。
2. **精灵名单**：来源状态栏明确以十位精灵为主要监控对象：折纸、二亚、狂三、四糸乃、琴里、六喰、七罪、八舞姐妹、美九、十香；curated 将八舞姐妹拆为耶俱矢与夕弦，同时保留合并关系。
3. **士织处理**：来源将士织单列并有“精灵 Doppelganger”等表述。为避免 RP 混淆，本次将士织定义为五河士道的女装/变身/伪装身份，而非默认独立人物。
4. **玩家身份分支**：来源含“你是同班同学”“你是 DEM 社 BOSS”“你是同班同学+真士转生”“你是士道”等入口。curated 默认不采纳为正史，仅记录为可选 sandbox/IF。
5. **临界支线**：时崎狂三、绯衣响、白之女王、临界其他配角被纳入 Date A Bullet/邻界支线层；默认不覆盖主线天宫市层。
6. **成人向来源内容**：源文件分类中存在大量 `character-nsfw`、`nsfwRules`、露骨身体描写和互动规则。curated 标准产物未沿用这些内容，仅保留创伤、关系、能力、组织冲突等世界观必要信息。

## 译名与命名统一

- `氷芽川四糸乃` 统一作 `冰芽川四糸乃`，保留日文/罗马别名。
- `鏡野七罪` 统一作 `镜野七罪`。
- `阿尔缇米希亚·贝尔·阿シュクロフト` 统一作 `阿尔缇米希亚·贝尔·阿修克罗夫特`，保留来源混写。
- `本条二亚` 保持常用译名；来源首行存在引号缺失，不影响人物归纳。
- `Ratatoskr` 中文常见为 `拉塔托斯克`，文件中保留英文组织 ID 以便和来源一致。

## 低置信/待补项

| 项目 | 置信 | 说明 |
| --- | --- | --- |
| 维斯考特细节 | C | 来源中主要以玩家“DEM BOSS”分支出现，仍按常见主线反派整理，但需官方来源补证。 |
| 崇宫真士/士道转生关系 | C | 来源有真士转生玩家分支；默认作为 GM-only 因果信息，不作为玩家身份。 |
| 临界其他配角 | C | 来源有集合条目，未逐名展开。 |
| 白之女王能力细节 | C | 来源摘要级，需 Date A Bullet 专门资料。 |
| 阿尔缇米希亚能力细节 | B/C | 来源列为重点角色但细节少于主线精灵。 |
| 澪的具体天使名称与终局机制 | B/C | 来源出现澪条目但本次未完整阅读全部后段自动归档，避免过度断言。 |

## 冲突处理

- **主线 vs IF**：主线士道为默认；玩家替代身份均为可选。
- **组织标签 vs 个人转变**：折纸、真那等角色有 AST/DEM/Ratatoskr 多阶段经历，characters-index 用多阵营记录并在 notes 中说明。
- **八舞姐妹合并 vs 拆分**：来源为合并条目；为关系图谱和人物索引可用性，拆为耶俱矢、夕弦，并记录姐妹/半身边。
- **成人向内容 vs 世界观档案**：不纳入 curated，避免污染默认 RP 规则。

## 标准产物完成情况

- [x] `README.md`
- [x] `world.json`
- [x] `source-registry.json`
- [x] `characters-index.json`
- [x] `knowledge-graph.json`
- [x] `relationship-graph.json`
- [x] `curation-notes.md`

## 范围确认

- 未修改 `raw/`。
- 未修改 `imports/`。
- 未修改既有自动归档文件。
- 仅创建 `campaigns/world-library/worlds/date-a-live/curated/` 下标准产物。

## 关于总索引

上层 Objective 提到“刷新总索引”，但本 step 的 mutation scope 明确限制为只能创建或修改：

`campaigns/world-library/worlds/date-a-live/curated/`

因此本步骤未修改 `campaigns/world-library/manual-curation/INDEX.md` 或其他 curated 目录外文件。