# ACG 角色心理/类脑数据库（curated）

本目录为手工 curated 归档，基于本地归档文件人工阅读整理。

## 特殊定位

`acg-character-database` **不是单一作品世界**，而是跨作品角色心理模型、类脑角色卡与性格原型数据库。它包含来自游戏、动画、漫画、现实历史、网络模因、成人作品和原创/同人系列的角色条目，也包含“傲娇、御姐、三无、理性、大小姐”等人格模板。

因此 curated 层不强行构造统一地理、国家或单一剧情世界，而按“数据库/参考库”处理：

- 人物索引按来源作品/系列标注。
- 知识图谱记录“角色条目”“心理模型”“人格原型”“跨作品来源”等概念。
- 关系图不虚构跨作品关系，仅保留同作品、同系列或数据库层级关系。

## 读取来源

- `campaigns/world-library/worlds/acg-character-database/source-registry.json`
- `campaigns/world-library/worlds/acg-character-database/characters/characters.json`
- `campaigns/world-library/worlds/acg-character-database/world/world.json`

## Curated 产物

- `world.json`
- `source-registry.json`
- `characters-index.json`
- `knowledge-graph.json`
- `relationship-graph.json`
- `curation-notes.md`
- `completion-expansion.json`：retry-01 补充参考库运行模型、来源分层、代表性人格原型与关系使用策略。

## 内容安全整理

源中部分条目包含成人作品、NTR、性暴力或露骨身体细节；curated 层仅保留条目名称、来源作品、数据库用途与非露骨心理/角色分类信息。