# 丹特丽安的书架 / Dantalian no Shoka curated 档案

整理状态：已补齐标准 curated 产物（2026-06-22）。

## 来源范围

- `src-dantalian-no-shoka-001`：用户提供世界书/角色卡世界书《丹特丽安的书架 幻書啟示錄》，归档于 `campaigns/world-library/worlds/dantalian-no-shoka/` 下的自动分类文件。
- 本次人工整理主要阅读：
  - `manifest.json`
  - `source-registry.json`
  - `world/world.json`
  - `characters/characters.json`
  - `factions/factions.json`
  - `power-systems/power-systems.json`

## 当前默认基线

默认采用战后近代欧陆/英伦风格的原作式主线：修伊继承祖父宅邸与钥匙，成为黑之读姬妲丽安的钥匙守护者，巡回处理散落世间的幻书事件。RP 中允许 OC 作为受害者、调查者、收书人、军警、神秘术师、船客、学校相关者等介入，但不得默认取代“钥匙守护者”身份，除非剧情明确赋予钥匙碎片、副馆权限或等价契约。

## 产物

- `world.json`：世界主档、力量体系、势力、地点、事件与 RP 约束。
- `source-registry.json`：来源登记与人工整理依据。
- `characters-index.json`：详细人物清单。
- `knowledge-graph.json`：世界知识图谱。
- `relationship-graph.json`：人物与势力关系图谱。
- `curation-notes.md`：人工判断、低置信与后续事项。

## 未解决问题

- 现有导入为单一世界书来源，可靠度为 B；部分译名在条目间混用（妲丽安/达利安、哈尔·卡姆赫德/卡姆霍德、芙兰/芙兰卑尔奇等），本 curated 采用统一主名并将异名放入 aliases。
- 自动分类中包含 NSFW/角色卡控制文本，本次只抽取世界观与 RP 安全可用事实；不沿用露骨化指令。
- 第 6-8 卷人物较多，已列主要角色与关键事件人物，支线路人可后续扩展。

## 下一步

- 如需更高精度，可逐卷补充所有幻书条目与事件 NPC 的完整索引。
- 可继续为每本幻书创建独立 `items`/`lore` 子表，但本次 mutation scope 仅要求标准产物。
