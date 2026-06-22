# Infinite Stratos curation notes

## 阅读来源
- `source-registry.json`：确认 `src-infinite-stratos-001`，标题为“无限斯特托拉斯”。
- `world/world.json`、`characters/characters.json`、`factions/factions.json`：人工阅读到大量写卡/游戏模式/状态栏/性癖核心等技术模板，以及可用的 IS 机体、学园、角色关系、机体展开细节。

## 处理决策
- 源文件人物 keys 多为空，人物索引以源内明确出现的“一夏、IS、学园、机体展开细节中的角色名”和 RP 常用 IS 核心人物补全，并标注 sourceStatus。
- “青羽学园”可能为世界书改写舞台称呼；curated 主条采用“IS学园”，在 world.json 中记录源称呼。
- 排除所有源内成人化状态栏、用户控制模板和提示词，不作为世界观规则。

## 风险
- 自动分类文件把大量技术模板归入 characters/world/factions，需后续人工二次清理更细。
- 人物条目部分为常识性补全，非所有角色都有独立源 key。

## 验证状态
- 已创建 7 个 curated 标准文件。
- 未运行 JSON 解析器；JSON 为人工书写。