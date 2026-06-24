# 型月 curation notes

## 人工处理
- 已人工阅读导入 README、分类报告、冲突/低置信报告，并抽读 `characters/characters.json`。
- 大体量世界仅做主框架和主要人物抽样，未用脚本抽取。

## 抽样范围
- 收录 FSN 核心、FGO 迦勒底核心共 9 人。
- 未尽：月姬、空之境界、Fate/Zero 全员、FGO 大量从者、妖精国与魔法少女伊莉雅完整人物。

## 冲突/风险
- 同一角色在不同路线、灵基、Alter、平行世界中差异巨大。
- 神秘、魔法、权能、宝具不能混同；战斗评级需逐状态建立。

## 下一步
1. 按作品线拆分子索引。
2. 建立从者职阶/宝具表。
3. 对冬木圣杯战争、迦勒底、人理/异闻带分别建事件图谱。

## 2026-06-22 MED 规范化补记
- 已将可明确对应的 world registry 条目规范化为 canonical id，并同步更新角色字段。
- 原始显示名保存在角色 `metadata.originalReferenceLabels` 与 `normalizationNotes` 中；无法确定的条目未硬改。
- 已补足 `waver-velvet` 与 `romani-archaman` 以对齐 `knownMembers`。

## retry-14 补完记录

- 已确认 `audit-completion-modules.json` 承载多作品路由、Fate/stay night、Fate/Zero、FGO/迦勒底、魔法少女伊莉雅、月姬/空境、妖精国的保守路线锁。
- 已按 campaigns 大体量源只抽取高层规则、势力与 RP 边界；813 个角色、543 条力量体系和多灵基版本未扁平合并，避免路线混同。
- 残留缺口：从者职阶/宝具表、Fate/Zero 全员、月姬/空境人物、FGO 各章角色与 LB6 妖精国仍需分批子索引。
- 验证：2026-06-24 使用 Node.js 解析本目录 JSON，包含本文件相邻 6 个 JSON，全部有效。
