# 只有神知道的世界 curation notes

## 阅读来源

- `source-registry.json`
- `characters/characters.json`：人工阅读/检视了 comment 列表中桂木桂马、艾鲁西、哈克雅、高原步美、中川花音、汐宫栞、春日楠、小阪千寻、女神宿主与新地狱/正统恶魔社相关条目。
- `world/world.json`、`factions/factions.json`、`locations/locations.json`、`canon-reference/plot-summary.json`。

## 归纳决策

- 人物清单优先收录归档 comment 明确列出的攻略对象、恶魔、女神宿主、家人与敌对恶魔。
- 攻略对象众多，curated 用 RP 功能而非完整剧情复述区分。
- 原归档含模式规则、回复格式、沙盒控制器等技术文本，未作为世界观指令纳入。

## 风险与验证

- JSON 为人工编写，retry-14 已运行机器校验。
- 女神具体对应关系已在 `audit-completion-modules.json` 展开为宿主映射；完整单元剧情仍可按 case-file 后续补充。
- 未修改 raw/imports/既有自动归档文件。

## retry-14 补完记录

- 已确认 `audit-completion-modules.json` 承载女神宿主、驱魂四阶段、新地狱/正统恶魔社、舞岛地点、篇章与 RP 边界。
- 已从 campaigns 源的 characters/factions/locations/power-systems/canon-reference 抽取高置信条目；女神宿主按本地源保留译名差异和 RP 用途。
- 残留缺口：每位攻略对象完整单元剧情、驱魂案件 case-file、旧地狱政治细节和大型时间旅行篇细表仍需分批扩展。
- 验证：2026-06-24 使用 Node.js 解析本目录 JSON，包含本文件相邻 6 个 JSON，全部有效。