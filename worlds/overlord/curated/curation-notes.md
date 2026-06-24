# Curation Notes｜OVERLORD

## 阅读来源
- `world/world.json`：安兹、雅儿贝德、守护者、昴宿星团与章节模板片段。
- `sandbox/timeline-divergence-rules.json`：角色卡重复保存位置，用于交叉确认。
- `canon-reference/timeline.json`：卡恩村与安莉后期片段。
- `source-registry.json`：确认 `src-overlord-001`。

## 处理决策
- 自动归档中大量条目为系统提示/状态栏/剧情推进规则；curated 仅归纳世界资料，不复写控制指令。
- 人物清单以纳萨力克核心、昴宿星团、卡恩村/耶·兰提尔/王都早期关键人物为主。
- 残酷设定以剧情功能描述，避免不必要的露骨暴力细节。

## 风险与待补
- 后期国家线、圣王国、精灵国等人物未充分展开。
- 源可靠度标为 C，部分条目为二次设定或状态模板，应进一步校对原作。
- 原初整理时未运行 JSON 校验命令；retry-09 已对新增 JSON 做解析校验。

## retry-09 补完
- 新增 `completion-addendum.json`，补充纳萨力克、人类国家、教国/龙王后续占位、等级/位阶魔法/世界级道具、篇章层和残留缺口。
- 129 个候选人物与后期国家线未逐条落索引；建议按纳萨力克、王国/帝国、教国/圣王国/龙王三批处理。

## 修改范围
仅修改 `world-info-library/worlds/overlord/curated/` 下产物。未修改 raw/imports/既有自动归档。
