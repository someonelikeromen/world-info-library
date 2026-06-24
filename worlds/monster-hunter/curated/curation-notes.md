# Curation Notes｜怪物猎人

## 阅读来源
- `canon-reference/plot-summary.json`：世界地理概论与“世界巡礼猎人”叙事指导。
- `canon-reference/full-plot.json` / `canon-reference/arcs.json`：猎人公会、王立书士队、古龙观测局、龙历院等组织。
- `power-systems/power-systems.json`：现实化世界观、任务星级、猎人定位、状态栏资料。
- `source-registry.json`：确认 `src-monster-hunter-001`。

## 处理决策
- 源资料更偏世界设定和叙事规则，缺少固定姓名角色；因此“详细人物清单”采用角色类型/组织岗位/生态角色形式，便于RP。
- 强调去游戏化：HR/MR等以任务星级、地区公会认证和现实社会功能解释。
- 怪物被归为生态角色而非恶人。

## 风险与待补
- 若后续需要严格原作NPC姓名，可补充历代村长、受付娘、调查团成员等独立条目。
- 源可靠度为 C，世界整合含大量系列综合设定。
- 未运行 JSON 校验命令。

## 修改范围
仅创建 `campaigns/world-library/worlds/monster-hunter/curated/` 下标准产物。未修改 raw/imports/既有自动归档。

## 运行时门禁补充

- `characters-index.json` 不是完整《怪物猎人》历代固定 NPC 姓名库。
- 猎人、公会、村落、研究机构、古龙/禁忌怪物等条目主要是职业/组织/生态角色槽位。
- 运行时不应把生态角色当作善恶固定人物，也不应从岗位条目推断未登记 canon NPC。
## retry-08 补完
- 重整 `world.json` 为标准 rp-world-v1 字段，补公会/任务、武器锻造、生态追踪、古龙灾害体系、关键地点、怪物分类、篇章与 RP hooks。
- `characters-index.json` 增补代表怪物和古龙/禁忌怪物示例；仍不是完整 NPC 或怪物图鉴。
