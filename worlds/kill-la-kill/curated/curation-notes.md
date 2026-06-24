# Kill la Kill curation notes

## retry-07 补完记录
- 已读取说明/登记：`campaigns/world-library/worlds/kill-la-kill/source-registry.json`、`campaigns/world-library/worlds/kill-la-kill/curated/README.md`、`campaigns/world-library/worlds/kill-la-kill/curated/curation-notes.md`、`world-info-library/worlds/kill-la-kill/curated/README.md`、`world-info-library/worlds/kill-la-kill/curated/source-registry.json`。
- 已抽读素材：`canon-reference/arcs.json`、`canon-reference/timeline.json`、`power-systems/power-systems.json`、`factions/factions.json`、`locations/locations.json`、`sandbox/scenario-seeds.json`。
- 原始素材盘点：仅发现导入世界书 `raw/imported-worldbooks/斩服少女.worldbook.json` 与 `raw/original-entry-index.json`；未发现独立小说、动画剧本、游戏原文或官方资料长文。
- 本批扩展：`world.json` 新增/扩展战斗生命纤维、极制服、神衣、反纤维武装、timeline、plotArcs、factions、locations、relationships、worldRules、rpNotes。

## 阅读来源
- `source-registry.json`：确认唯一源 `src-kill-la-kill-001`。
- `world/world.json`：阅读“世界观”“战斗生命纤维”及人物条目片段。
- `characters/characters.json`：定位流子、皋月、真子、针目缝、罗晓、四天王和配角聚合条目。
- `power-systems/power-systems.json`：抽读极制服、战斗生命纤维、源内状态栏等条目，确认污染风险。

## 处理决策
- 源内成人化状态栏、节日活动、跨作品/原创角色和身体细节不纳入 curated。
- “本能字/本能寺”源中用字不一，采用文件中常见“本能字学园”。
- “满舰饰家成员”作为聚合人物条目列出，因源 key 将多名配角合并。
- 对源内 C 级条目仅采纳能与已知主线互相印证的世界观主干。

## 风险
- 部分人物条目混合原作事实与世界书改写内容，curated 尽量回归可用主线。
- 未逐行阅读全文所有长人物内容，仅人工阅读关键片段并交叉定位。
- 源内污染素材量大，后续最好新增 canon/污染/原创支线索引。

## 低置信/待补
- 宝多财阀势力圈、部分社团/区域支线、部分配角条目需继续校验。
- 原始生命纤维、罗晓计划和姐妹真相应按剧情阶段公开，不作为开局常识。

## 验证状态
- retry-07 已运行 JSON 解析验证，详见最终汇报。
