# 蔚蓝档案 curation notes

## 阅读来源

- `source-registry.json`
- `world/world.json`：人工阅读了基沃托斯总述、三一综合学园、格黑娜学园、千禧年科学学院、山海经高级中学等条目。
- `characters/characters.json`：确认 `entryCount: 0`。
- `raw/imported-worldbooks/鸡窝托斯.worldbook.json`、`factions/factions.json`、`locations/locations.json`。

## 归纳决策

- 因原人物分类为空，`characters-index.json` 明确用 `sourceStatus` 标注：哪些是归档直接提及姓名（如空崎阳奈、莉音、龙华妃咲），哪些是组织岗位或 RP 常用身份（如老师、风纪委员会学生）。
- 学园自治、武装日常、学生耐久、近未来科技与“神秘”是世界规则核心。
- 未把未读到的具体学生大量扩展为 canon 详表，避免伪造来源。

## 风险与验证

- JSON 为人工编写，未运行机器校验。
- 角色表偏“RP 角色类型索引”，不是完整 Blue Archive 全角色数据库。
- 未修改 raw/imports/既有自动归档文件。

## 运行时门禁补充

- `characters-index.json` 不是完整 Blue Archive 官方固定人物库。
- 岗位角色、组织角色与 RP 常用身份仅表示可用角色槽位；除明确姓名/`sourceStatus` 标注外，不应当作固定 canon NPC。
- 运行时应保留“老师/先生”为成人调停者/保护者定位，不从岗位条目推断额外 canon 学生。
