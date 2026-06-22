# REPAIR-Q5-UNRESOLVED-REFERENCE

检查日期：2026-06-22  
步骤：`q5-unresolved-reference`  
范围：Q4 后仍存在 `unresolved-reference` 的 8 个世界：`acg-character-database`、`blue-archive`、`cheng-long-adventures`、`monster-hunter`、`overlord`、`rakudai-kishi`、`sora-no-otoshimono`、`sword-art-online`。

## 处理原则

- 只把能够唯一映射到现有 `characters-index` / `knowledge-graph` / `source-registry` 的节点转成真实实体。
- 已转正节点补 `sourceRefs`、`evidence`、`resolutionNotes`，并把 `metadata.q4SourceRiskReview.status` 改为 `resolved-by-curated-index-match`。
- 无法唯一映射的集合、群体、泛称边端点保留 `unresolved-reference`，但补 `resolutionNotes`、`sourceVerification: not-verified`、`runtimeUse: structural-edge-endpoint-only`，避免被误当作已核实事实。
- 不新增 canon 断言；对组织/群体角色仅使用现有 curated 条目或知识图谱锚点。

## 本轮结果

### 已转正为真实实体

- `blue-archive`
  - `老师/夏莱` → `sensei` / `character`
  - `茶会` → `tea-party-host` / `organization-role`
  - `研讨会` → `millennium-seminar` / `organization-role`
  - `万魔殿` → `pandemonium-member` / `organization-role`
  - `风纪委员会` → `prefect-team-student` / `organization-role`
  - `温泉开发部` → `hot-spring-dev` / `organization-role`
  - `C&C` → `c-and-c-agent` / `organization-role`
  - `玄龙门` → `genryumon-member` / `organization-role`
  - `玄武商会` → `genbu-merchant` / `organization-role`
  - `联邦学生会`、`三一综合学园`、`格黑娜学园`、`千禧年科学学院` 保持既有已解析状态并补充 `sourceRefs`
- `overlord`
  - `雅儿贝德`、`迪米乌哥斯`、`夏提雅·布拉德弗伦`、`科塞特斯`、`娜贝拉尔·伽玛`、`塞巴斯·蒂安`、`琪雅蕾`、`索留香·艾普西隆`、`安莉·艾默特`、`恩弗雷亚·巴雷亚雷`、`露普丝雷其娜·β`、`葛杰夫·史托罗诺夫` 转为 `character`
  - `蜥蜴人部落` 保留为非角色实体锚点，补了 source 说明
- `sword-art-online`
  - `桐人`、`亚丝娜`、`克莱因`、`阿尔戈`、`希兹克利夫`、`莉兹贝特`、`西莉卡`、`幸`、`启太`、`辛卡`、`由莉耶儿` 转为 `character`
  - `微笑棺木成员`、`攻略组` 转为组织级实体
- `monster-hunter`
  - `主角猎人/OC猎人`、`艾露猫伙伴`、`加工屋工匠`、`村长`、`王立书士队学者`、`古龙观测员`、`保守派长老`、`激进派技师`、`生态顶点怪物`、`区域村落` 转为现有角色/生态类型
- `rakudai-kishi`
  - `黑铁一辉`、`史黛菈·法米利昂`、`黑铁珠雫`、`有栖院凪`、`黑铁严`、`黑铁王马`、`绫辻绚濑`、`仓敷藏人`、`东堂刀华`、`爱德怀斯`、`月影总理`、`新宫寺黑乃`、`紫乃宫天音`、`莎拉·布拉德莉莉`、`风祭凛奈`、`御祓泡沫`、`贵德原彼方`、`碎城雷`、`兔丸恋恋` 转为 `character`
- `sora-no-otoshimono`
  - `樱井智树`、`伊卡洛斯`、`见月楚原`、`守形英四郎`、`五月田根美香子`、`代达罗斯`、`妮姆芙`、`阿斯特蕾亚`、`卡奥斯`、`风音日和`、`空之主`、`奥勒冈`、`美兰`、`塞壬`、`萨月义经`、`樱井智藏` 转为 `character`
  - `万能天使群` 保留为群体实体
- `cheng-long-adventures`
  - `阿奋/拉苏/周/阿福` 保留为群体实体，不强拆成单人角色

### 保留为 `unresolved-reference`

- `blue-archive` 仍保留 4 个结构性端点：`各学园`、`各校学生`、`阿里乌斯分校`、`三一各派系`。
- 这些节点是跨校/集合/历史裂痕类端点，没有唯一且安全的单一 canon 实体可落点，因此按结构边端点保留，并补了防误用元数据。

## 风险与决定

- 本轮优先清理“可唯一映射”的尾项，而不是把所有群体词硬塞进单人角色，避免制造伪事实。
- 蓝档中 `茶会`、`研讨会` 等虽然在角色索引中有对应组织角色条目，但在关系图里被保留为结构代理节点，只是转成了可审计实体，并不表示补写了新的 canon 设定。
- `sourceRefs` / `evidence` 采用现有 curated 文件路径，不新增外部事实来源。

## 验证状态

- 已验证：`overlord`、`sword-art-online`、`monster-hunter`、`rakudai-kishi`、`sora-no-otoshimono`、`cheng-long-adventures` 的 `relationship-graph.json` 中 `unresolved-reference` 为 0。
- 已验证：`blue-archive` 的 `relationship-graph.json` 中仍有 4 个 `unresolved-reference`，均为结构性集合端点。
- 已验证：蓝档关键已解析节点存在 `sourceRefs`、`evidence`、`resolutionNotes`，且 `metadata.q4SourceRiskReview.status` 为 `resolved-by-curated-index-match`。
- 未运行全仓 QA；本记录只复核本轮目标 8 世界的 unresolved-reference 收敛结果。
