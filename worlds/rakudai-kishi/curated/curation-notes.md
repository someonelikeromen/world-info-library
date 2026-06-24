# Curation Notes｜落第骑士英雄谭

## 阅读来源
- `source-registry.json`：确认唯一导入源 `src-rakudai-kishi-001`。
- `world/world.json`：人工阅读卷一至后期卷概要、关键地点与参与人物。
- `characters/characters.json`、`power-systems/power-systems.json`：用于交叉确认角色与能力词。

## 处理决策
- 人物清单优先纳入各卷“参与剧情人物”中反复出现或推动主线者；学生会成员、晓学园成员、国际篇反派也列入。
- 部分条目中含成人/福利导向桥段，curated 仅保留角色关系和剧情功能，不复写露骨描写。
- OC 使用建议保留“可介入但不继承一辉专属招式/命运”的原则。

## 风险与待补
- 自动归档有重复条目，人工整理时按内容去重。
- 后期国际篇人物未完全展开，欧尔·格尔、法米利昂/奎多兰相关人物可在下一轮补充。
- 未运行 JSON 校验命令；文件为手写 JSON，需后续机器校验。

## 修改范围
仅创建 `campaigns/world-library/worlds/rakudai-kishi/curated/` 下标准产物。未修改 raw/imports/既有自动归档。


## 2026-06-24 本地收尾
- `r3` 的 rakudai 子代理步骤因 `Service temporarily unavailable` 失败；本地工具接管收尾。
- 新增 `timeline-index.json`，仅作为 RP 启动/检索索引，不替代 campaign `canon-reference/timeline.json`。
- 新增 `completion-index.json`，记录 source 覆盖、raw/NSFW 分离与残余低置信项。
- 已运行本地 JSON parse 验证，`curated/` 下所有 JSON 均有效；未修改 campaign 原始归档。
