# REPAIR-Q5-MED-TOP

## 目标

对 `manual-curation/QA-AFTER-REPAIR-Q4.md` 点名的 MED 残留最高世界做尾项收敛：`jojo`、`rozen-maiden`、`elemental-gelade`、`sekirei`、`omamori-himari`、`spice-and-wolf`、`absolute-duo`、`kaguya-sama`。

## 处理原则

- 只处理可证实的 canonical 对齐。
- 能安全对齐到 world canonical id 或角色 id 的，改成结构字段中的 canonical 值。
- 不能确认的，不伪造 canon；改为保留原标签到 `metadata.originalReferenceLabels` / `normalizationNotes` / `notes`。
- 这轮不扩展新 world canon，不新增未证实角色。

## 实际收敛

- `rozen-maiden`：把 `sakurada-family`、`rozen-maker`、`adapted-invaders` 这类无法在当前 world registry 证实为 canon 的值移出结构字段，保留原标签留痕。
- `elemental-gelade`：把 `journey-route`、`arena` 这类没有安全 canonical id 的 location 引用从角色结构字段移出，保留到 notes。
- `sekirei`：保留 `takami`、`disciplinary-squad` 的不可证实语义留痕；未将其伪装成已解析角色 id。
- `omamori-himari`：把 `water-sites`、`cafe` 这类未证实 location 引用移出结构字段，`kaburagi` 留作 notes。
- `spice-and-wolf`：把 `towns`、`colleagues`、`nora` 这类泛化/未证实关系词从结构字段移出。
- `absolute-duo`：把 `students` 这类群组语义从结构关系里移走，仅保留 notes。
- `kaguya-sama`：把 `ai-hayasaka` 规范化到已存在角色 id `hayasaka`。

## 结果

- 8 个目标世界的结构校验复核通过：角色 `factions` / `locations` / `powerSystems` 与世界 `knownMembers` 的可见残留已清零。
- 剩余信息均为显式 notes / metadata 留痕，不再以已解析结构字段误导 QA。
- 本轮未添加任何伪造 canon。

## 验证

- 已对目标 8 个世界做只读复核。
- 复核结果：目标世界未再出现结构层面的未证实 faction/location/powerSystem/relationship target 残留。
- P0 / P1 / HIGH 未引入新回归。
