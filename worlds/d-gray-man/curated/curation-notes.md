# D.Gray-man curation notes

## 人工判断
- 采用长期连载主线的 RP 可用摘要，不把后期全部反转一次性写死为公开事实。
- 第十四号、阿尔玛、克劳斯的真相线统一记为 GM-only 或低置信阶段信息。
- 黑色教团组织结构按“黑色教团本部/支部/北美分部”三层保留。

## 低置信/待补
- 方舟、北美分部与欧洲总局的出场节点仍可细化。
- 诺亚家族成员与恶魔制造过程的细部适配，后续可再扩。

## 来源追踪
- 主要依据：`src-d-gray-man-001`；分类报告显示 113 条已完整归档。

## 2026-06-22 MED 规范化补记
- `world.json` 中原字符串型 `factions`/`locations` 已规范化为 `{id,name}` 节点，并补入 `bookman-lineage`, `secret-lines` 及若干角色场域地点节点。
- 角色 `locations`/`factions` 已改为 canonical id；原显示名保存在 `metadata.originalReferenceLabels`。
- 未把后期真相扩写为公开 canon，仅做 id 对齐。
