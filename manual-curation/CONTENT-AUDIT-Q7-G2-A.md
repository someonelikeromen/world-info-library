# CONTENT AUDIT Q7 G2-A

审计范围：`worlds/evangelion/curated/`、`worlds/gate-jsdf/curated/`、`worlds/gundam-seed/curated/`

已逐个读取：
- `README.md`
- `curation-notes.md`
- `characters-index.json`

未修改 curated 正文；本报告仅列出自适应扩充清单、人物外观结构缺口与优先级。

优先级约定：
- **P0**：影响开局/主线一致性或高频 RP 使用，需优先补。
- **P1**：主要人物、派系、地点、机体/能力索引扩展，能显著提升可用性。
- **P2**：细节增强、番外/支线、视觉/检索体验优化。

---

## 1. `worlds/evangelion/curated/`

### 当前完整度判断
- README 标注：已读导入 README、分类报告；2 个 worldbook，88 条保留条目；覆盖 NERV、SEELE、使徒、EVA、AT Field、人类补完计划和主要驾驶员。
- curation-notes 明确风险：TV 版、旧剧场版、新剧场版差异未拆分；开局必须锁定版本。
- `characters-index.json` 当前仅 5 人：碇真嗣、绫波丽、惣流·明日香·兰格雷、葛城美里、碇源堂。
- `indices.byId`、`byName`、`byAffiliation`、`byTag` 为空对象，虽不一定破坏主记录，但不利于检索一致性。

### 扩充缺口清单
| 优先级 | 缺口 | 说明 |
|---|---|---|
| P0 | 时间线/版本分层 | TV、旧剧场版、新剧场版目前混用风险最高；需明确每条角色/事件/机体适用版本，如惣流/式波差异、结局路线、补完机制差异。 |
| P0 | 核心人物缺失 | curation-notes 已点名未列：加持良治、赤木律子、冬月耕造、渚薰；这些对 NERV/SEELE/补完计划/角色关系不可或缺。 |
| P0 | 使徒条目不足 | 当前无独立使徒角色/实体索引；需至少补亚当、莉莉丝、渚薰/Tabris、Sachiel、Ramiel、Zeruel、Arael、Armisael 等高剧情影响对象。 |
| P1 | EVA 机体与量产机细分 | 当前以 items 粗略挂载 EVA 零/初/二号机；缺少 EVA-00/01/02 的魂、暴走、装备、损伤、同步限制，量产机未列。 |
| P1 | SEELE 与 NERV 内部层级 | 源堂、冬月、律子、美里、MAGI、SEELE 委员会之间的权限、隐瞒层级、冲突需更细。 |
| P1 | 关键事件链 | 第二次冲击、零号机启动实验、初号机暴走、加持死亡、中央教条、第三次冲击/补完计划等需要阶段化。 |
| P2 | 支援与家庭人物 | 伊吹摩耶、日向诚、青叶茂、铃原冬二、相田剑介、洞木光、碇唯、赤木直子等可补成中低优先级。 |
| P2 | 地点/设施细节 | 第三新东京市、NERV 本部、GeoFront、Terminal Dogma、LCL/插入栓等可增强 RP 场景。 |

### 人物外观结构缺口
- 当前人物记录没有统一 `appearance` 字段或等价结构。
- 缺少：年龄/年级、身高体型、发色发型、瞳色、常服、校服、驾驶服、NERV 制服、标志性姿态/表情、版本差异外观。
- EVA 特别需要补：驾驶服颜色与款式、角色心理状态下的外显表现、TV/旧剧场/新剧场角色设计差异。
- 建议先为 5 名已收录角色补最小结构：`ageBracket`、`bodyType`、`hair`、`eyes`、`defaultOutfit`、`alternateOutfits`、`visualIdentifiers`、`versionNotes`。

### 推荐执行顺序
1. **P0**：先建“版本锁定/时间线差异”说明，避免混线。
2. **P0**：补加持、律子、冬月、渚薰。
3. **P0/P1**：补核心使徒与 EVA 机体实体索引。
4. **P1**：补关键事件链与 NERV/SEELE 权限关系。
5. **P2**：补外观字段与次要人物、地点细节。

---

## 2. `worlds/gate-jsdf/curated/`

### 当前完整度判断
- README 标注：manual-initial；主来源 `src-gate-jsdf-001`，可信度 B；整理重点包含门/特区、日本自卫队、帝国政治内战、阿尔努斯生活组合、亚神与龙/魔法生态。
- curation-notes 标注：角色名录来源很完整，但 curated 只保留 RP 世界观与关系核心；外传使徒与海自后续未完全展开。
- `characters-index.json` 当前 9 人：伊丹、萝莉、蕾莱、杜嘉、平娜、索沙尔、蒂尤蕾、柳田、吉赛儿。
- 索引结构较完整，`byId`/`byName`/`byAffiliation`/`byTag` 已填充；角色关系采用对象结构且含 resolved 状态，优于另外两组。

### 扩充缺口清单
| 优先级 | 缺口 | 说明 |
|---|---|---|
| P0 | 日本侧核心军政人物不足 | 当前只有伊丹、柳田；缺少狭间浩一郎、栗林志乃、富田章、桑原/第三侦查队成员、外务/内阁关键接口，影响 JSDF 行动链。 |
| P0 | 阿尔努斯核心生活圈不全 | 蕾莱、萝莉、杜嘉已列，但亚欧/雅欧·哈·杜希、德莉拉、猫耳/兔人等协助者缺失；阿尔努斯多种族社区可用性不足。 |
| P0 | 帝国政治谱系不足 | 平娜、索沙尔、蒂尤蕾已列，但皇帝摩尔特、迪亚波、波赛斯/蔷薇骑士团成员、元老院/贵族代表不足；政变与讲和线支撑不够。 |
| P1 | 外传海自篇 | README 已标“下一步：补充外传海自篇”；需补海自舰队、海上投送、异世界海域势力与角色。 |
| P1 | 诸神使徒谱系 | 目前只有萝莉与吉赛儿；需要俄摩拉、汉蒂等神明/使徒体系、亚神晋升规则、使徒间制约。 |
| P1 | 龙/魔法生态 | 炎龙线仅由杜嘉间接覆盖；需补炎龙、龙种分类、魔法学派、魔导师组织与特区生态威胁。 |
| P1 | 帝国贵族封地地图 | README 已点名；需要帝都、伊塔黎卡、阿尔努斯、炎龙区域、属国/封地的政治-军事连接。 |
| P2 | 译名别名整理 | curation-notes 已指出萝莉/罗莉、杜嘉/杜卡、索沙尔/佐尔札尔等译名差异；应扩充 aliases 与 normalization notes。 |
| P2 | 成人/沙盒源内容边界 | 已决定不迁移敏感交互规则；后续扩充仍需保持“只保留 RP 世界观与关系核心”的边界声明。 |

### 人物外观结构缺口
- 当前人物记录没有统一 `appearance` 字段。
- 对《GATE》尤其缺：种族外观、年龄表象 vs 实际年龄、服饰体系、军服/盔甲/神官服/魔导师服、武器携行外观。
- 重点补充对象：
  - 萝莉·麦丘利：少女外表、哥特神官服、巨斧、亚神气质。
  - 蕾莱：魔导师装束、法杖/教材、年轻学者气质。
  - 杜嘉：高等精灵耳型、弓手装备、精神创伤阶段外显。
  - 平娜：皇女/骑士团长服饰切换。
  - 蒂尤蕾：兔族特征、奴役/复仇阶段服饰与状态。
  - 伊丹/柳田：自卫队制服、作战装备、阶级识别。
- 建议最小结构：`species`、`apparentAge`、`actualAgeNote`、`build`、`hair`、`eyes`、`earsOrNonhumanTraits`、`defaultOutfit`、`combatOutfit`、`signatureWeapon`、`visualIdentifiers`。

### 推荐执行顺序
1. **P0**：补 JSDF 第三侦查队/日本侧军政链核心人物。
2. **P0**：补阿尔努斯协助者与帝国皇族/骑士团关键角色。
3. **P1**：扩展诸神使徒、龙种、魔法生态。
4. **P1**：补外传海自篇与帝国封地地图。
5. **P2**：统一 aliases/译名与外观结构。

---

## 3. `worlds/gundam-seed/curated/`

### 当前完整度判断
- README 标注：主来源 `src-gundam-seed-001` 有 128 条，人物 82、势力 86、道具/机体 121；当前手工初版聚焦自然人与调整者战争、ZAFT/地球联合/奥布、MS 技术、SEED 因子、创世纪级战略武器。
- curation-notes 标注：后续应补独立 MS 索引；战略武器和舰队战需与个人 MS 战分层；SEED 因子不能常驻无限加成。
- `characters-index.json` 当前仅 6 人：基拉、阿斯兰、拉克丝、卡嘉莉、玛琉、劳。
- `byId` 使用 id 到数组下标的映射，`byName` 正常；`byAffiliation`、`byTag` 为空。

### 扩充缺口清单
| 优先级 | 缺口 | 说明 |
|---|---|---|
| P0 | 主要驾驶员不足 | 源人物 82 但当前仅 6 人；缺少穆·拉·弗拉格、娜塔尔·巴基露露、伊扎克、迪亚哥、尼科尔、米莉亚莉亚、芙蕾、赛伊等本篇高频人物。 |
| P0 | 三大阵营人物链不足 | ZAFT 仅阿斯兰/劳，地球联合仅玛琉，奥布仅基拉/卡嘉莉；缺少帕特里克·萨拉、乌兹米、阿兹拉艾尔、克鲁泽队、蓝色宇宙等政治/军令核心。 |
| P0 | 机体/道具独立索引 | curation-notes 已点名；强袭、自由、正义、圣盾、神意、大天使号、永恒号、草薙号、创世纪等不应只停留在 items 字符串。 |
| P1 | 战争阶段/战役链 | 赫利奥波利斯、阿尔忒弥斯、沙漠之虎、奥布攻防、JOSH-A、雅金·杜维等阶段需分层，关联角色阵营转换。 |
| P1 | 技术与战力边界 | SEED 因子、调整者、自然人、MS OS、相转移装甲、龙骑兵系统、核动力/中子干扰器需规则化，避免无限加成。 |
| P1 | 舰队战 vs 个人战分层 | README/notes 均提示战略武器与舰队战；需区分个人 MS 对决、舰队火力、战略兵器、生存/补给限制。 |
| P1 | SEED Destiny/外传边界 | 当前名为 gundam-seed，但源条目可能覆盖更广；需明确是否仅本篇，还是纳入 Destiny、Astray 等并标版本。 |
| P2 | 关系网细化 | 基拉-芙蕾-拉克丝、阿斯兰-拉克丝-卡嘉莉、穆-玛琉、娜塔尔-玛琉、ZAFT 红衣队内部关系待补。 |
| P2 | 索引一致性 | `byAffiliation`、`byTag` 为空；`byId` 映射形式与部分世界不一致，可在后续维护中统一。 |

### 人物外观结构缺口
- 当前人物记录没有统一 `appearance` 字段。
- 高达 SEED 需要同时描述：军服/驾驶服/便服、阵营制服颜色、发色瞳色、年龄段、体型、标志性配饰、机体驾驶舱装备。
- 重点补充对象：
  - 基拉：学生服、地球联合驾驶服、三舰同盟阶段外观、自由高达驾驶阶段。
  - 阿斯兰：ZAFT 红衣、驾驶服、正义高达阶段、阵营转换后的服饰差异。
  - 拉克丝：歌姬礼服、PLANT/克莱因派政治象征服饰。
  - 卡嘉莉：奥布公主、沙漠抵抗军、驾驶/战斗装束。
  - 玛琉：地球联合舰长制服、大天使号指挥形象。
  - 劳：面具、ZAFT 指挥官制服、神意高达阶段。
- 建议最小结构：`age`、`build`、`hair`、`eyes`、`defaultOutfit`、`militaryUniform`、`pilotSuit`、`civilianOutfit`、`visualIdentifiers`、`mobileSuitStageNotes`。

### 推荐执行顺序
1. **P0**：补穆、娜塔尔、芙蕾、赛伊、米莉亚莉亚、伊扎克、迪亚哥、尼科尔、帕特里克、乌兹米、阿兹拉艾尔。
2. **P0**：建立独立 MS/舰艇/战略兵器索引，并把人物 items 改为可追踪引用。
3. **P1**：补战役阶段链与阵营转换节点。
4. **P1**：规则化 SEED 因子、调整者、MS 技术、战略武器边界。
5. **P2**：补外观结构、关系网与空索引。

---

## 跨世界共性问题

| 优先级 | 共性缺口 | 涉及世界 | 建议 |
|---|---|---|---|
| P0 | 人物外观结构缺失 | EVA、GATE、Gundam SEED | 建立统一 `appearance` 子结构，同时允许世界特有字段，如 EVA 的 `plugSuit`、GATE 的 `species/nonhumanTraits`、SEED 的 `pilotSuit/mobileSuitStageNotes`。 |
| P0 | 当前 characters-index 远小于来源人物量 | EVA、Gundam SEED；GATE 中等 | 按“主线必需人物→阵营链→支线/番外”分批扩充。 |
| P0 | 版本/阶段边界 | EVA、Gundam SEED | EVA 必须拆 TV/旧剧场/新剧场；SEED 需明确是否含 Destiny/Astray。 |
| P1 | 道具/机体/实体只以字符串出现 | EVA、Gundam SEED；GATE 部分武器 | 建独立实体索引，人物 items 使用 canonical id。 |
| P1 | 战力规则需要分层 | GATE、Gundam SEED、EVA | 区分个人战、机体战、组织/舰队/战略兵器/神性或补完级事件。 |
| P2 | 索引一致性 | EVA、Gundam SEED | 补 `byId`、`byName`、`byAffiliation`、`byTag`，统一映射格式。 |

---

## 验证状态

- 已读取并审计：
  - `worlds/evangelion/curated/README.md`
  - `worlds/evangelion/curated/curation-notes.md`
  - `worlds/evangelion/curated/characters-index.json`
  - `worlds/gate-jsdf/curated/README.md`
  - `worlds/gate-jsdf/curated/curation-notes.md`
  - `worlds/gate-jsdf/curated/characters-index.json`
  - `worlds/gundam-seed/curated/README.md`
  - `worlds/gundam-seed/curated/curation-notes.md`
  - `worlds/gundam-seed/curated/characters-index.json`
- 写入文件：`manual-curation/CONTENT-AUDIT-Q7-G2-A.md`
- 未读取额外 curated 文件；现有 README/notes/index 已足够判断本轮缺口。
- 未修改任何世界 curated 内容。
