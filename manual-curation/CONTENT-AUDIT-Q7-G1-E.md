# CONTENT AUDIT Q7 G1-E：世界内容完整度审计

审计范围：

- `worlds/danmachi/curated/README.md`
- `worlds/danmachi/curated/curation-notes.md`
- `worlds/danmachi/curated/characters-index.json`
- `worlds/dantalian-no-shoka/curated/README.md`
- `worlds/dantalian-no-shoka/curated/curation-notes.md`
- `worlds/dantalian-no-shoka/curated/characters-index.json`
- `worlds/date-a-live/curated/README.md`
- `worlds/date-a-live/curated/curation-notes.md`
- `worlds/date-a-live/curated/characters-index.json`

必要补读：

- `worlds/danmachi/curated/world.json`
- `worlds/danmachi/curated/knowledge-graph.json`
- `worlds/danmachi/curated/relationship-graph.json`
- `worlds/danmachi/curated/source-registry.json`

审计重点：人物外表、服装、气质/性格、角色可扮演锚点、主要阵营/支线覆盖度。

## 总体结论

| worldId | 完整度判断 | 主要问题 | 优先级 |
| --- | --- | --- | --- |
| `danmachi` | 明显不完整 | 仅 7 名角色；大量核心角色、眷族、敌对势力、异端儿、后期卷、人物外观/服装/气质字段缺失 | P0 |
| `dantalian-no-shoka` | 中高，事件人物覆盖较广 | 40+ 人物但多数缺独立外观/服装/气质字段；第 6-8 卷和幻书索引仍低置信 | P1 |
| `date-a-live` | 中等偏高，主线精灵较完整 | 主线角色齐，但外观/灵装/AST/DEM 装备、气质语气缺独立结构化；支线 Date A Bullet 摘要级 | P1 |

跨世界共同缺口：当前 `characters-index.json` schema 主要有 `summary/roles/factions/abilities/items/relationships/notes`，没有独立 `appearance`、`outfit`、`demeanor/personality`、`speechStyle`、`rpHooks` 等字段。部分外观/气质被塞进 `summary` 或 `notes`，难以稳定供 RP 生成使用。

---

## 1. `worlds/danmachi` / 地错

### 已见事实

- `README.md` 明确写明：已读 4 个 worldbook、874 条保留条目；自动分类数很多：characters 617、factions 517、locations 700、powerSystems 594。
- `curation-notes.md` 明确写明：人物仅覆盖 7 名主要角色；未尽包括洛基眷族全员、芙蕾雅眷族、阿斯特莉亚眷族、异端儿、各卷反派。
- `characters-index.json` 实际仅列：
  - 贝尔·克朗尼
  - 赫斯缇雅
  - 艾丝·华伦斯坦
  - 莉莉露卡·厄德
  - 韦尔夫·克罗佐
  - 琉·璃昂
  - 芙蕾雅
- `relationship-graph.json` 额外有低覆盖节点：洛基、赫菲斯托丝、希儿·福罗瓦、奥塔，但未进入 `characters-index.json` 主体。
- `world.json` 只列 5 个势力：赫斯缇雅眷族、洛基眷族、芙蕾雅眷族、丰饶的女主人、阿斯特莉亚眷族；地点也仅有欧拉丽、巴别塔、地下城、丰饶的女主人、炉灶馆。
- `knowledge-graph.json` 只有 Falna、地下城、异端儿等最小节点，后续 Q5 修补也是 minimal coverage。

### 完整度判定

`danmachi` 明显不完整。证据是：来源规模显示人物类自动条目达 617，但 curated 人物只有 7；`curation-notes.md` 也自认仅覆盖 7 名主要角色。对一个以眷族、冒险者等级、卷别事件、地下城楼层生态为核心的世界来说，目前只能支持最粗略的贝尔/赫斯缇雅/艾丝/芙蕾雅主轴 RP，不能支持全量世界运行。

### 人物外表/服装/气质缺口

当前 7 人均缺独立外观字段。具体：

- 贝尔：缺白发红眼/少年感/轻甲或冒险者装备、赫斯缇雅之刃佩戴方式、战斗状态气质、纯真与勇气的行为锚点。
- 赫斯缇雅：缺经典蓝丝带、黑白连衣裙、幼小外表与女神气场反差、依恋/嫉妒/护短气质。
- 艾丝：缺金发金眼、无表情/天然、剑士服与洛基眷族装备、战斗时冷冽气质。
- 莉莉露卡：缺小人族体型、支援者背包/伪装、警戒心和后期忠诚/参谋气质。
- 韦尔夫：缺红发/铁匠装/武具风格、反魔剑理念、豪爽但认真气质。
- 琉：缺精灵外貌、店员服与冒险者/疾风装备差异、礼貌克制与复仇阴影。
- 芙蕾雅：缺银发美神外貌、服饰与眷族女王气场、魅惑/占有欲/超然审美。

### P0 补全清单

1. 扩充核心角色索引，至少补入：
   - 赫斯缇雅眷族：三条野春姬、命、建御雷相关成员、韦尔夫师承线、后期加入成员。
   - 洛基眷族：洛基、芬恩、里维莉雅、格瑞斯、蒂奥娜、蒂奥涅、蕾菲亚、伯特等。
   - 芙蕾雅眷族：奥塔、艾伦、赫定、赫格尼、格列佛兄弟、赫伦/希儿关联等。
   - 丰饶的女主人：希儿、蜜雅、阿妮雅、露诺娃、克洛伊等。
   - 阿斯特莉亚眷族：阿斯特莉亚、阿莉泽、辉夜、莱拉等，至少用于琉过去线。
   - 异端儿：薇妮、里德、古罗斯、费尔斯/乌拉诺斯关联线。
   - 主要神明/眷族：赫菲斯托丝、建御雷、荷米斯、迦尼萨、伊丝塔等。
   - 黑暗派阀与各卷反派：可按卷别逐步补。
2. 为所有已有人物增加结构化字段或在 notes 中统一格式补写：
   - `appearance`：发色、瞳色、体型、年龄观感、种族特征。
   - `outfit`：日常服、眷族/冒险者装备、战斗服、标志物。
   - `demeanor`：第一印象、性格关键词、常见姿态。
   - `speechStyle`：称呼、语气、口癖、礼貌程度。
   - `rpHooks`：适合触发的委托、关系冲突、秘密、成长目标。
3. 按时间线锁定角色等级与能力：至少建立“动画 S1/S2/S3/S4/小说某卷”分层，避免 Level、技能、装备随进度变化造成矛盾。
4. 扩充地点和地下城生态：地下城楼层、安全楼层、深层、迷宫孤王/楼层主、欧拉丽主要设施、公会、各眷族据点。
5. 扩充关系图：当前只有贝尔-赫斯缇雅、贝尔-艾丝、芙蕾雅-贝尔 3 条核心边，不能反映地错的眷族政治和后宫/同伴关系网。

---

## 2. `worlds/dantalian-no-shoka` / 丹特丽安的书架

### 已见事实

- `README.md` 称已补齐标准 curated 产物，采用战后近代欧陆/英伦风格原作式主线。
- `characters-index.json` 列出 40+ 人物，覆盖主角组、三类读姬/钥匙关系、焚书官、教授/赤之读姬、支线幻书事件人物、第 6-8 卷低置信人物。
- `curation-notes.md` 明确：第 6-8 卷部分人物只读到摘要；幻书名称混用，待建 `phantom-books-index.json`。

### 完整度判定

人物数量和事件覆盖优于 `danmachi`，可支持主线与大量单元剧 RP。但内容仍偏“剧情摘要型”，人物可视化和扮演细节不足。第 6-8 卷与幻书单体信息仍需补证。

### 人物外表/服装/气质缺口

已有少量人物在 `summary` 中带外观：

- 妲丽安：外表十二三岁、黑衣少女、毒舌怕生傲慢、爱炸面包和甜食。
- 哈尔：灰发或白衣美男子。
- 芙兰蓓尔：白色拘束衣、身体/拉链中藏门扉。
- 拉结尔：左眼书架/锁头眼罩、残酷傲慢。
- 卡米拉：活泼金发女性。

但多数支线人物缺外貌、服装、语气、气质，例如蕾斯莉、古雷姆、沙茲、罗伊、梅蓓儿、弗洛伦斯、艾斯提拉、艾拉斯、宝拉、伦茨、维奥拉、麦尔加、阿尔曼、洁西卡、克莉丝托贝尔、菲欧娜、优娜、希德嘉、海灵、艾米莉亚/艾娃、怪盗秘银、莉菲雅等。

### P1 补全清单

1. 主角/高频角色优先补外观服装：
   - 修伊：退役飞行员气质、绅士/调查者服装、持枪/钥匙的视觉锚点。
   - 妲丽安：黑衣、锁、读姬仪式姿态、甜食喜好与傲娇毒舌语气分离记录。
   - 哈尔：焚书官战斗装、灾厄之枝、摩托车、冷酷焚毁理念。
   - 芙兰蓓尔：拘束衣、锁头、拉链门扉、被束缚/毁灭读姬气质。
   - 拉结尔/教授：赤之读姬视觉、教授中性美男子/研究者气质。
2. 为支线人物按“单元剧 NPC 卡”补最低三件套：
   - 外观一句
   - 服装/道具一句
   - 气质/危险点一句
3. 第 6-8 卷低置信人物补证：
   - 雷欧、不死杀手卫斯理、欧立克、奥利佛、亨利·贾威斯顿、高丁、怪盗秘银、莉菲雅。
4. 建议新增或后续规划 `phantom-books-index.json`：幻书名、别名、效果、读者资格、代价、事件人物、危险等级。
5. 关系字段目前多为字符串，如 `"dalian:契约读姬/同伴"`；可逐步规范为对象结构，便于和其他世界统一。
6. 统一 RP 风险标签：精神操控、人体改造、复活腐败、家暴、血亲禁忌、猎奇死亡等应有 `contentWarnings` 或 notes 模板。

---

## 3. `worlds/date-a-live` / 约会大作战

### 已见事实

- `README.md` 称已补齐标准产物，默认基线为主线天宫市，兼容 Date A Bullet/邻界支线。
- `characters-index.json` 覆盖士道、十香、折纸、二亚、狂三、四糸乃/四糸奈、琴里、六喰、七罪、八舞姐妹、美九、澪、真那、艾伦、阿尔缇米希亚、维斯考特、神无月、士织、真士、绯衣响、白之女王、临界配角群。
- `curation-notes.md` 明确：来源有成人向内容但 curated 未沿用；临界支线和部分反派细节低置信。

### 完整度判定

主线角色覆盖基本可用，精灵名单完整度较好；但角色描述偏能力/剧情摘要，缺少 Date A Live 高辨识度的灵装、发色瞳色、气质、语气、日常服/校服/战斗装切换。Date A Bullet 仍只是摘要池。

### 人物外表/服装/气质缺口

高优先级缺口：

- 十香：缺紫发紫眼、校服/灵装、天真吃货与战斗威严反差。
- 折纸：缺白发/银白短发、无表情、AST/DEM 装备、精灵灵装与反转形态视觉。
- 二亚：缺漫画家/修女风格、被囚禁后状态、宅向语言气质。
- 狂三：缺黑红灵装、异色瞳/时钟眼、哥特气质、分身体与本体姿态差异。
- 四糸乃/四糸奈：缺绿色雨衣/兔耳兜帽/手偶视觉、胆怯与手偶毒舌对比。
- 琴里：缺黑白发带模式、司令服/日常装、珍宝珠、妹妹/司令官双模式语气。
- 六喰：缺长发、宇宙漂流/封闭心灵的空灵气质、灵装与封解主视觉。
- 七罪：缺成熟伪装与真实幼小/自卑形态差异、魔女灵装。
- 八舞姐妹：缺耶俱矢中二姿态、夕弦平板语气、风暴灵装和武装差异。
- 美九：缺偶像服/龙胆寺制服、舞台气质、厌男创伤与“达令”语气。
- 澪：缺始源精灵外观、终局形态、慈爱/执着/神性反差。
- DEM/AST 人物：缺 CR-Unit 具体装备外观、军装/作战服、随意领域表现。
- Date A Bullet：绯衣响、白之女王、临界配角群缺基本外观和能力细节。

### P1 补全清单

1. 为主线十位精灵建立统一视觉模板：
   - `appearance`：发色、瞳色、年龄观感、标志特征。
   - `spiritOutfit`：灵装名称/视觉、颜色、武装。
   - `casualOutfit`：校服、日常服、职业装。
   - `demeanor`：初遇态、封印后日常态、反转/失控态。
   - `speechStyle`：称呼士道方式、语气、口癖。
2. 补 AST/DEM 技术装备可视化：CR-Unit、White Lycoris、Mordred、DEM 高端装备、随意领域视觉。
3. 折纸、琴里、士织、七罪等多形态角色应拆出 `forms` 或在 notes 中统一格式记录。
4. 补主线反派/世界真相：维斯考特、澪、真士目前可用但低置信；需官方来源确认天使名、终局机制、与士道/真士因果。
5. Date A Bullet 支线应从集合条目拆分至少核心 NPC：绯衣响、白之女王外，再补主要准精灵角色、邻界规则、空无机制。
6. 关系索引中存在部分 `unresolved` 关系，例如“对三次元人类不信任”“对亲密关系有独占倾向”“八舞姐妹合体能力更强”“澪执着对象”；后续应改为性格/状态字段，不应强行作为关系边。

---

## 建议的统一补字段模板

可在后续 curated 人物补写时采用：

```json
"appearance": {
  "ageLook": "",
  "hair": "",
  "eyes": "",
  "bodyBuild": "",
  "distinctiveFeatures": []
},
"outfits": {
  "default": "",
  "combat": "",
  "casual": "",
  "formalOrWork": ""
},
"demeanor": {
  "firstImpression": "",
  "coreTraits": [],
  "emotionalRange": "",
  "combatPresence": ""
},
"speechStyle": {
  "tone": "",
  "addressing": [],
  "catchphrases": [],
  "taboos": []
},
"rpHooks": []
```

如果 schema 暂不允许新增字段，至少可在 `notes` 中用固定小标题写入：`外观：...；服装：...；气质：...；语气：...；RP钩子：...`。

## 验证状态

- 已逐个读取指定三个世界的 `curated/README.md`、`curated/curation-notes.md`、`curated/characters-index.json`。
- 因 `danmachi` 明显存在覆盖缺口，额外只读了其 `world.json`、`knowledge-graph.json`、`relationship-graph.json`、`source-registry.json` 用于判断缺口。
- 未修改任何 curated 世界文件。
- 本次仅写入：`manual-curation/CONTENT-AUDIT-Q7-G1-E.md`。
