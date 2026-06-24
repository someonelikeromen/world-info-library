# CONTENT-AUDIT-Q7-G1-F：第1组世界内容完整度审计

审计范围：
- `worlds/dragon-ball/curated/README.md`
- `worlds/dragon-ball/curated/curation-notes.md`
- `worlds/dragon-ball/curated/characters-index.json`
- `worlds/dungeon-fighter-online/curated/README.md`
- `worlds/dungeon-fighter-online/curated/curation-notes.md`
- `worlds/dungeon-fighter-online/curated/characters-index.json`
- `worlds/elemental-gelade/curated/README.md`
- `worlds/elemental-gelade/curated/curation-notes.md`
- `worlds/elemental-gelade/curated/characters-index.json`

辅助只读：各世界 `world.json`、`knowledge-graph.json`、`relationship-graph.json`、`source-registry.json`，用于判断缺口，不作修订。

审计结论总览：三个世界的 `characters-index.json` 均偏“跑团可操作摘要”，没有独立的 `appearance` / `outfit` / `demeanor` / `personality` / `voice` 等人物表现字段；服装、外貌、气质只零散地隐含在 `summary`、`roles`、`notes` 中，无法直接支撑立绘、出场描写或一致扮演。建议下一轮扩充优先为主要角色补充“外表/服装/气质/常态姿态/阶段差异/禁用误写”字段，并同步补齐角色覆盖、关系边与地点归一。

---

## 1. `worlds/dragon-ball`

### 已有内容状态

- `README.md` 标记为 Batch B 手工初版完成，重点整理了气/战斗力、赛亚人变身、龙珠许愿、融合、神/界王体系、红缎带与人造人、弗利萨军、魔人布欧时间线。
- `curation-notes.md` 明确当前目标是“可操作规则”而非完整百科，并提示剧场版异闻、GT/超/剧场版取舍需跑团前锁定。
- `characters-index.json` 当前收录 7 人：`son-goku`、`vegeta`、`son-gohan`、`piccolo`、`bulma`、`frieza`、`majin-buu`。
- `world.json` 已有力量体系、阵营、地点与战斗规则；`relationship-graph.json` 仅覆盖核心关系边；`source-registry.json` 显示主来源为 `src-dragon-ball-001`，可靠性 B。

### 主要缺口

#### A. 人物外表/服装/气质字段缺口（高优先级）

当前 7 名角色均没有结构化外观字段，需逐一补齐：

- `son-goku`：缺少成年/少年阶段体型差异、橙色道服、龟/界王/悟字标识阶段、黑发与超级赛亚人发色变化、天真好战但善良的气质描写。
- `vegeta`：缺少战斗服/训练服/布欧篇常服差异、竖立发型、矮壮精悍体态、王子式傲慢与克制怒意的气质描写。
- `son-gohan`：缺少幼年、少年沙鲁篇、青年学者/赛亚蒙面超人、神秘悟饭等阶段外观与服装差异；气质需区分温和学者、责任感爆发、战斗时潜力觉醒。
- `piccolo`：缺少绿色那美克星人体貌、触角、披风头巾、紫色道服、冷峻导师气质与后期守护者气质。
- `bulma`：缺少频繁换装、蓝发/发型变化、胶囊公司科技感服饰、聪明强势与现实主义后勤气质。
- `frieza`：缺少多阶段形态外观、白紫终形态、机械弗利萨/黄金形态是否纳入的阶段边界；气质需补“优雅残酷、帝王式轻蔑”。
- `majin-buu`：缺少胖布欧/恶布欧/小布欧等形态外观、服饰、体态、表情与人格气质差异；需明确各形态不应混写。

建议新增或约定字段：`appearance`、`defaultOutfit`、`alternateOutfits`、`demeanor`、`speechStyle`、`stageVariants`、`visualDonts`。

#### B. 角色覆盖缺口（高优先级）

`README.md` 已提“补齐更多次要人物”，当前 7 人不足以覆盖龙珠常用 RP。建议补入：

1. Z 战士与地球阵营：克林、天津饭、饺子、雅木茶、龟仙人、琪琪、撒旦先生、比迪丽、特兰克斯、孙悟天。
2. 神系与那美克星：神、丹迪、内鲁、界王、界王神、老界王神。
3. 红缎带/人造人：格罗博士、人造人16号、17号、18号、沙鲁。
4. 赛亚人与弗利萨篇：拉蒂兹、那巴、巴达克、基纽特战队、库尔德王。
5. 布欧篇：巴比迪、达普拉、贝吉特/悟天克斯是否作为独立合体角色节点。
6. 可选分支：布罗利、邪念波、GT/超相关角色需先按时间线策略决定是否纳入。

#### C. 阶段/时间线缺口（高优先级）

- `curation-notes.md` 明确 GT/超/剧场版取舍未锁定；角色强度与外观高度依赖阶段。
- 需建立 `timelineProfile` 或 `stageVariants`：少年篇、赛亚人篇、那美克星篇、人造人/沙鲁篇、布欧篇、剧场版异闻、超/GT可选线。
- 悟空、贝吉塔、悟饭、弗利萨、布欧尤其需要阶段化强度、形态、服装与人格状态。

#### D. 关系与地点补全（中优先级）

- `relationship-graph.json` 只列核心边，缺少布尔玛-特兰克斯、悟饭-琪琪/比迪丽、比克-神/那美克星、弗利萨-军团成员、人造人-红缎带等重要关系。
- 角色 `relationships` 当前为字符串格式，部分可读但不利于解析；后续可统一为对象格式。
- 地点已有补节点，但 `king-kai-world-kaioshin-realm` 与拆分节点并存，需继续检查是否重复使用。

### 龙珠补全清单

- [ ] 为 7 名现有角色补 `appearance/defaultOutfit/demeanor/stageVariants`。
- [ ] 按时间线冻结默认 RP 阶段，或为每名角色提供阶段档。
- [ ] 补齐 Z 战士、红缎带/人造人、沙鲁、布欧篇配角、神系角色。
- [ ] 明确剧场版、GT、超是否作为可选分支独立索引。
- [ ] 扩展关系图至家庭、师徒、宿敌、阵营上下级、融合关系。
- [ ] 为高阶角色增加 RP 安全限制：地图耐久、复活规则、星球级攻击许可。

---

## 2. `worlds/dungeon-fighter-online`

### 已有内容状态

- `README.md` 显示已读 2 个 worldbook、629 条保留条目，分类规模很大：characters 275、locations 284、factions 245、powerSystems 197。
- `curation-notes.md` 说明当前人物抽样只采用“冒险家”代表职业主角，并列赛丽亚与主要使徒；未展开所有职业导师、NPC、区域领主。
- `characters-index.json` 当前收录 6 个角色/概念：`player-adventurer`、`seria-kirmin`、`sirocco`、`ozma`、`bakal`、`kazan`。
- `world.json` 地点为字符串列表，角色索引大量 `locations` 未解析；`source-registry.json` 明确职业分支与版本剧情跨度大，resolution 为 unresolved。

### 主要缺口

#### A. 人物外表/服装/气质字段缺口（高优先级）

当前所有角色均缺少结构化外观、服装与气质：

- `player-adventurer`：作为聚合角色无法提供外观；必须拆成职业/转职角色模板。需为鬼剑士、格斗家、神枪手、魔法师、圣职者等基础职业及代表转职补默认体型、武器、服装轮廓、觉醒视觉特征与气质。
- `seria-kirmin`：缺少标志性服饰、发色/发型、温柔引导者气质、不同版本/活动装束边界。
- `sirocco`：缺少使徒形态、女性/精神/变异相关视觉、悲鸣洞穴相关压迫感与神秘气质；需按版本核对。
- `ozma`：缺少混沌之神外观、伪装者/黑色大地视觉、污染氛围、宗教灾厄气质。
- `bakal`：缺少爆龙王/龙族暴君体貌、火焰与天界统治视觉、王者压迫感。
- `kazan`：缺少鬼神/传说状态外观、鬼手诅咒表现、狂暴与毁灭性气质。

建议：对 DFO 不宜只补个人字段，应建立“职业外观模板 + 代表 NPC 外观 + 使徒形态档”。

#### B. 角色覆盖缺口（极高优先级）

与源规模相比，当前 6 条索引严重不足。建议分批扩充：

1. 玩家职业模板：鬼剑士、女鬼剑士、格斗家、神枪手、魔法师、圣职者、暗夜使者、魔枪士、枪剑士、弓箭手等；每类至少基础职业 + 代表转职。
2. 引导/城镇 NPC：赛丽亚之外补林纳斯、风振、凯丽、莎兰、歌兰蒂斯、土罐等常见导师/功能 NPC。
3. 使徒：除希洛克、奥兹玛、巴卡尔外，补卡恩、赫尔德、罗特斯、狄瑞吉、安徒恩、卢克、普雷、米歇尔等，且需标版本与阵营复杂度。
4. 地区势力人物：德洛斯帝国、贝尔玛尔、公国、暗精灵、天界、魔界、虚祖相关核心人物。
5. 副本领主/区域 Boss：按地区和版本分批，不宜一次性扁平导入。

#### C. 聚合角色拆分缺口（高优先级）

- `player-adventurer` 目前承担所有玩家职业，导致能力、外观、服装、气质、武器都不可用。
- 建议将 `player-adventurer` 保留为群体概念，同时新增 `male-slayer-template`、`female-mage-template` 等职业模板，再为转职建立子节点。
- 每个职业模板应包含：`bodySilhouette`、`weaponStyle`、`combatDemeanor`、`defaultOutfit`、`awakeningVisuals`、`classFantasy`。

#### D. 地点与关系归一缺口（中高优先级）

- 6 名角色 `locations` 均为空，原地点保存在 `metadata.originalReferenceLabels`，包括“阿拉德”“旅店/城镇”“悲鸣洞穴/相关副本”“黑色大地”“天界/龙之领域”“传说/封印”。
- `world.json` 的 `locations` 是字符串列表，不是 `{id,name}` 节点；需统一 canonical id。
- `relationship-graph.json` 节点已补 `michael`、`adventurers`、`heaven`、`ghostblade-line`，但边只有 2 条；奥兹玛-米歇尔、巴卡尔-天界、卡赞-鬼剑士源流等关系未形成正式边。
- `characters-index.json` 的 `indices.byId/byName/byAffiliation/byTag` 为空，需重建索引。

### DFO 补全清单

- [ ] 将冒险家拆为职业模板与代表转职，补外观/武器/觉醒视觉/气质。
- [ ] 为赛丽亚、希洛克、奥兹玛、巴卡尔、卡赞补外表、服装/形态、气质、版本差异。
- [ ] 扩充使徒全员与关键 NPC，按版本分批。
- [ ] 将字符串地点规范化为 canonical location id，并回填角色 `locations`。
- [ ] 扩展关系图：冒险家-各导师、使徒之间、帝国/天界/魔界势力、奥兹玛-米歇尔、巴卡尔-天界。
- [ ] 重建空的 `byId/byName/byAffiliation/byTag` 索引。
- [ ] 为职业强度建立按转职、觉醒、装备分层的 RP 评级规则。

---

## 3. `worlds/elemental-gelade`

### 已有内容状态

- `README.md` 标记 Batch D 手工整理完成初版，来源包含动画第一至二十六唱剧情条目。
- `curation-notes.md` 说明以动画“唱”结构为主；薇罗、拉萨蒂等篇章人物细节需继续阅读原条目；漫画/动画差异未拆。
- `characters-index.json` 当前收录 7 人：`coud`、`ren`、`cisqua`、`rowen`、`kuea`、`rasati`、`viro`。
- `world.json` 对同契/React、艾迪鲁雷德、保护协会、艾迪鲁庭园有良好初版框架；`relationship-graph.json` 仅覆盖库德-蕾、罗温-奇雅、希丝卡-保护协会。

### 主要缺口

#### A. 人物外表/服装/气质字段缺口（高优先级）

当前 7 名角色均无结构化视觉字段；本作以“同契武器化”和旅途队伍辨识度为核心，外观缺口会直接影响 RP 描写。

- `coud`：缺少空贼少年体貌、常服/旅行装、武器使用姿态、莽撞但真诚的少年气质。
- `ren`：缺少七煌宝树/艾迪鲁雷德外貌、发色服饰、核石位置/表现、武器化形态、沉静寡言与逐渐信任库德的气质变化。
- `cisqua`：缺少保护协会制服/装备、枪械与重火器携行方式、精明强势、爱钱/任务导向但重情的气质。
- `rowen`：缺少协会成员服饰、沉稳礼貌的仪态、与奇雅同契时的战斗姿态。
- `kuea`：缺少艾迪鲁雷德外貌、食量大/直率活泼的表情与肢体语言、武器化形态。
- `rasati`：目前只有“赌斗场相关少女/斗士”，缺少外貌、斗士服装、人物关系与篇章动机；证据等级 C。
- `viro`：身份与阵营反转仅概述，缺少外貌、伪装/真实状态差异、同契能力表现与气质反转。

建议对艾迪鲁雷德角色增加专属字段：`humanAppearance`、`coreStone`、`weaponForm`、`reactSongMood`、`contractDemeanor`。

#### B. 篇章角色覆盖缺口（高优先级）

- `README.md` 称来源覆盖第一至二十六唱，但索引只收 7 人。
- `curation-notes.md` 已点名薇罗、拉萨蒂细节不足；还需要按每“唱”补旅途篇章人物、敌对同契者、猎人、协会成员、艾迪鲁庭园相关人物。
- 拉萨蒂 notes 提到 `lilia` 不是当前 canonical character id，说明丽莉娅/相关角色缺索引。
- 需要补充红山猫空贼团成员、煌珠猎人、保护协会上层/其他成员、艾迪鲁庭园关键人物。

#### C. 同契与武器化细节缺口（高优先级）

- `world.json` 有 React 总规则，但 `characters-index.json` 没有把每对搭档的武器形态、属性、歌、同步限制结构化。
- 库德-蕾、罗温-奇雅是核心搭档，需补：武器类型、属性、触发台词/歌唱氛围、战斗风格、反噬/疲劳表现。
- 薇罗等反转角色需补“公开身份”和“真实身份/真实阵营”的可见性分层，防剧透误用。

#### D. 地点、关系与索引缺口（中优先级）

- 多数角色地点为空或 notes 中残留 `locations unresolved (no safe canonical id): journey-route/arena`；但 `world.json` 只有 `edel-garden`、`airship` 两个地点对象，缺少 `journey-route`、`arena` canonical 节点。
- `relationship-graph.json` 没有 `rasati`、`viro` 节点，也没有库德队伍内部除核心同契外的旅伴关系边。
- `characters-index.json` 的 `indices.byId/byName/byAffiliation/byTag` 为空，需重建。

### 武器种族传说补全清单

- [ ] 为 7 名现有角色补外表、服装、气质；艾迪鲁雷德额外补核石与武器化形态。
- [ ] 重点补 `rasati`、`viro` 的篇章信息、外观、动机、关系与证据来源。
- [ ] 补 `lilia` 等拉萨蒂篇相关角色，并建立 canonical id。
- [ ] 按二十六唱分批补旅途篇章人物、煌珠猎人、保护协会、艾迪鲁庭园人物。
- [ ] 为库德-蕾、罗温-奇雅建立结构化同契档：武器形态、属性、同步条件、弱点。
- [ ] 增补 `journey-route`、`arena` 等地点 canonical 节点并回填角色地点。
- [ ] 将薇罗等反转角色做公开/GM 真相分层。
- [ ] 重建空的 `byId/byName/byAffiliation/byTag` 索引。
- [ ] 若采用漫画线，另建分支，避免与动画“唱”归档混写。

---

## 跨世界共同补全建议

### 建议统一人物表现字段

为后续全库一致性，建议对角色索引扩展或在附属档中统一以下字段：

```json
{
  "appearance": "常态外貌与体态",
  "defaultOutfit": "默认服装/装备",
  "alternateOutfits": ["阶段或场景换装"],
  "demeanor": "气质、姿态、表情倾向",
  "speechStyle": "说话方式/称呼习惯",
  "stageVariants": [
    {
      "id": "arc-or-form-id",
      "appearance": "阶段外观",
      "outfit": "阶段服装",
      "powerNotes": "阶段强度/能力差异",
      "personalityShift": "阶段人格或情绪差异"
    }
  ],
  "visualDonts": ["避免误写或混线的视觉设定"]
}
```

### 优先级排序

1. **第一优先级**：现有角色补外表/服装/气质字段，避免核心角色不可描写。
2. **第二优先级**：按世界特性补阶段/形态：龙珠补时间线形态，DFO补职业/觉醒模板，武器种族传说补同契武器化。
3. **第三优先级**：扩充缺失人物与关系边。
4. **第四优先级**：地点 canonical id 与空索引重建。
5. **第五优先级**：版本/分支冲突拆分：龙珠剧场版/GT/超，DFO版本剧情，武器种族传说动画/漫画。

## 验证状态

- 已逐个读取指定三世界的 `curated/README.md`、`curated/curation-notes.md`、`curated/characters-index.json`。
- 已辅助读取三世界的 `world.json`、`knowledge-graph.json`、`relationship-graph.json`、`source-registry.json` 判断缺口。
- 本次未修改 curated 内容，仅写入本审计文件。
- 未运行 schema 校验；本报告为内容完整度人工审计清单。
