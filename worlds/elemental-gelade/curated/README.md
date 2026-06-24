# 武器种族传说 curated 手工整理

状态：Batch D 手工整理完成；2026-06-24 本地复核补完 `completion-index.json`，并重新验证 curated JSON。

来源范围：人工阅读/定位 `characters/characters.json`、`world/world.json`、`power-systems/power-systems.json`、`factions/factions.json`、`locations/locations.json`、`reports/*`；主要来源为 `src-elemental-gelade-001` / `wqzjcs_card.worldbook.json`，包含“世界总纲”“世界知识”与第一至二十六唱剧情条目。

整理范围：艾迪鲁雷德/圣战天使、同契、煌珠猎人、空贼团、保护协会、艾迪鲁庭园与旅途主线。

未解决问题：原归档按动画“唱”组织，漫画差异未拆分；若采用漫画线需另建分支。

## 入口建议
- `world.json`：世界规则、同契/圣战天使/势力与地点入口。
- `timeline.json`：动画唱/旅途线的 RP 时间线入口。
- `completion-index.json`：本地收尾复核、source 覆盖、raw 分离与残余风险记录。

## 验证
2026-06-24 本地验证：`curated/` 下所有 JSON 均可解析；未修改 `campaigns/world-library/worlds/elemental-gelade/` 原始归档。
