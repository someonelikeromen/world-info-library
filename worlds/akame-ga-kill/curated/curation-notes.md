# Akame ga Kill curation notes

## 阅读来源
- `source-registry.json`：确认唯一源 `src-akame-ga-kill-001`。
- `world/world.json`：阅读世界观、塔兹米、赤瞳、玛茵、希尔、帝具、帝国、夜袭、狩人等条目片段。
- `characters/characters.json`：定位夜袭、布兰德、雷欧奈、娜洁希坦、拉伯克、须佐之男、威尔、赛琉、Dr.时尚、波鲁斯、兰、奥内斯特、小皇帝等 key。

## 处理决策
- 人名中保留中文译名，aliases 记录源中日文/外文 key。
- 帝具名按常用译名补全；源中若只给人物 key，也纳入人物索引并标注 sourceEntries/sourceStatus。
- 排除无关 UI 或 NSFW 描写。

## 风险
- 源文件较长，未逐行读取全部人物全文；人物能力按源片段和常用设定保守整理。

## 验证状态
- 已创建 7 个 curated 标准文件。
- 未运行 JSON 解析器；JSON 为人工书写。

## retry-01 补完记录

- 新增 `completion-expansion.json`，补足帝具四十八件与奥义代价、危险种素材、夜袭/狩人/帝国/革命军/安宁道结构、帝都/夜袭基地/北方边境等地点、关系锚点与 RP 切入点。
- 将 `user-假面骑士`、`user-叛逃者线`、`帝具-夜煌`、`帝具·帕拉吉之盾` 等源中用户/自制条目标记为 optional variant，不覆盖正史默认。
- 低置信/待复核：源可靠性多为 C，时间线仅高层归纳；漫画/动画差异、安宁道细节、异民族和部分译名需后续复核。