# CONTENT-AUDIT-Q7-G1-D

审计 step：`audit-g1-d`  
审计范围：`worlds/claymore`、`worlds/cross-ange`、`worlds/d-gray-man`  
写入文件：`manual-curation/CONTENT-AUDIT-Q7-G1-D.md`  
审计重点：全量内容完整度；尤其检查人物外表、服装、气质、可视化描写字段缺口。

## 读取与验证状态

已逐个读取以下指定文件：

- `worlds/claymore/curated/README.md`
- `worlds/claymore/curated/curation-notes.md`
- `worlds/claymore/curated/characters-index.json`
- `worlds/cross-ange/curated/README.md`
- `worlds/cross-ange/curated/curation-notes.md`
- `worlds/cross-ange/curated/characters-index.json`
- `worlds/d-gray-man/curated/README.md`
- `worlds/d-gray-man/curated/curation-notes.md`
- `worlds/d-gray-man/curated/characters-index.json`

为判断世界层缺口，额外只读：

- `worlds/claymore/curated/world.json`
- `worlds/claymore/curated/knowledge-graph.json`
- `worlds/cross-ange/curated/world.json`（前 200 行，已覆盖主要世界规则/势力/能力段）
- `worlds/cross-ange/curated/knowledge-graph.json`
- `worlds/d-gray-man/curated/world.json`
- `worlds/d-gray-man/curated/knowledge-graph.json`（前 200 行，已覆盖主要节点/关系段）

尝试读取源文档路径：

- `worlds/claymore/characters/characters.json`
- `worlds/cross-ange/characters/characters.json`
- `worlds/d-gray-man/characters/characters.json`

结果均为 `ENOENT`，当前仓库这些世界目录下仅有 `curated/`，因此本次缺口判断基于 curated 产物与可见 curated world/knowledge 文件。

---

## 总体发现

三部作品的 curated 层均已具备基础世界观、主要人物名单、阵营/能力/地点摘要，但人物卡可用于 RP/视觉生成/角色扮演的“可视化与气质字段”普遍不足。

最突出共性缺口：

1. `characters-index.json` 缺少统一的人物外观结构字段，例如：
   - `appearance` / `visualProfile`
   - `hair`、`eyes`、`heightBuild`、`ageAppearance`
   - `outfit`、`uniform`、`weaponsVisible`
   - `demeanor`、`voiceTone`、`bodyLanguage`
   - `firstImpression`、`visualMotifs`
2. 大多数角色只有 `summary` 或 `role`，难以支持稳定扮演与画面化生成。
3. 阵营制服/制式装备没有沉淀为可复用模板：
   - 《Claymore》大剑制式银甲、白衣、巨剑、银眼等应成为“职业模板”。
   - 《CROSS ANGE》阿尔泽纳尔驾驶服、Para-mail/Ragna-mail 驾驶员装束、皇族礼服、龙族/奥拉之民服饰应分层记录。
   - 《D.Gray-man》黑色教团团服、驱魔师圣洁装备、诺亚一族服饰风格、千年伯爵造型应分层记录。
4. README/curation-notes 多数只说明整理来源与世界重点，未记录“已排除但应补回的 SFW 外观/服装/性格细节”。
5. 角色重要性已分级的世界（cross-ange、d-gray-man）适合按 `critical > high > medium` 分批补全外观；Claymore 目前未使用 importance 字段，建议补。

---

## worlds/claymore 审计

### 已有内容概况

- `README.md` 已定位世界为阴郁残酷的中世纪暗黑奇幻，说明大剑、组织、妖魔、觉醒风险、146 年迪妮莎时代及未来线。
- `curation-notes.md` 说明已读取源注册、角色、世界、势力文件；明确剔除强制叙事、成人/NSFW、状态栏，保留 SFW 世界观结构。
- `characters-index.json` 收录 30 个角色/群体条目，包括迪妮莎、普莉西亚、伊妮莉、苏菲亚、罗亚路、米莉雅、深渊者、未来新一代大剑、组织高层与监察员等。
- `world.json` 有核心规则、时间线、主要地点、组织/大剑/觉醒者/人类聚落等 faction 摘要。
- `knowledge-graph.json` 有组织、大剑、妖魔、觉醒者、深渊者、三大铁律、黑函、皮埃塔、圣都拉波勒等概念节点。

### 主要缺口

#### A. 人物外表/服装/气质字段缺口（高优先级）

`characters-index.json` 当前每个角色主要只有 `id`、`name`、`group`、`role`、`sourceRefs`。缺少结构化可视化字段。尤其《Claymore》角色高度依赖外观区分，但现档几乎未展开。

建议为全部人物至少补：

- `appearance.ageLook`
- `appearance.hair`
- `appearance.eyes`
- `appearance.build`
- `appearance.distinguishingFeatures`
- `outfit.default`
- `outfit.combatGear`
- `demeanor`
- `visualMotifs`

优先补全角色：

1. `teresa` 迪妮莎：需补“微笑的迪妮莎”的视觉表达，包括银眼/金发或浅发系、从容微笑、压迫感与温柔残影的反差、制式大剑装束、巨剑携带方式。
2. `priscilla` 普莉西亚：需补少女/新锐 No.2 的外观年龄感、纯粹与精神不稳定的气质、觉醒前后视觉差异。
3. `irene` 伊妮莉：需补冷峻高速剑士外观、右臂/断臂阶段差异、沉着气场。
4. `sophia`、`noel`：需补臂力型与疾风型的体态差异、表情/站姿、两人竞争关系带来的气质对照。
5. `miria`：需补“幻影”战术领袖气质、冷静指挥型视觉特征。
6. 深渊者：`isley`、`liful`、`luciela`、`rigaldo`、`duff` 需区分人形外表、觉醒者形态、统治气质/怪物压迫感。
7. 新一代大剑：`yuma`、`davi`、`helen`、`tabitha`、`cynthia`、`yuri` 当前描述很薄，需要外观、性格和战斗定位补齐。
8. 组织侧：`chief`、`riful-agent`、`dae`、`inspectors` 需要黑袍/遮面/代理人风格、医生/技术人员视觉特征、威胁气质。

#### B. 制式模板缺口（高优先级）

当前世界规则说明“大剑战士”为半人半妖女性战士，但缺少可复用外观模板。建议补入知识或角色模板：

- 大剑战士制式：银色/白色战斗服、铠甲或轻甲、巨剑、组织标志、银眼、妖力释放时眼色/表情变化。
- 组织代理人制式：黑衣/黑袍、遮面/冷漠、公文式任务传达、黑函递交。
- 妖魔/觉醒者通用视觉层级：伪装人类形态、暴露妖魔形态、觉醒者巨大异形形态、深渊者特征。

#### C. 时间线和阶段形态缺口（中高优先级）

源中存在 146 年迪妮莎时代与 150 年后未来线，但角色索引未统一标记：

- `era` / `firstAvailableArc`
- `stageVariants`：觉醒前、觉醒后、未来幸存/战死、叛逃后等。
- 特别是普莉西亚、伊妮莉、米莉雅、奥菲莉亚、嘉拉迪雅、拉花娜、露西艾拉等需要阶段化。

#### D. 命名与索引风险（中优先级）

- `raki` 条目名称“拉琪”且 role 写为“未来No.5/可能战死人物”，curation-notes 已提示与常见译名“拉基”需核对。建议列为专门待核对项。
- `rigaldo` 源列为“南之深渊者”，与常见认知可能冲突，建议标注低置信并核对。
- `riful-agent` 的 id 与 name “鲁路”可能导致与 `liful`/莉芙露混淆，建议核对命名来源并避免 id 误导。

### Claymore 自适应扩充清单

优先级 P0：

- 为所有 30 个角色补最小可视化字段：外表、服装、气质、标志装备。
- 建立“大剑战士制式外观模板”“组织代理人模板”“觉醒者形态模板”。
- 为 `teresa`、`priscilla`、`irene`、`miria`、`isley`、`liful`、`luciela`、`rafaela` 补阶段化视觉/气质。

优先级 P1：

- 为每名大剑补编号、战斗类型、武器/剑技、妖力释放表现。
- 为深渊者补人形与觉醒形态双版本。
- 增加 `importance`、`visibility`、`era` 字段以便后续分层使用。

优先级 P2：

- 核对译名：拉琪/拉基、罗亚路/Noel、伊妮莉/Irene、嘉拉迪雅/Galatea 等。
- 补地点氛围：组织总部、皮埃塔、圣都拉波勒、西部领地等的视觉风格。

---

## worlds/cross-ange 审计

### 已有内容概况

- `README.md` 显示状态为 `manual-initial-expanded（chunk-1）`，主来源 `src-cross-ange-001`，整理重点覆盖玛那社会、诺玛迫害、阿尔泽纳尔、Para-mail/Ragna-mail、DRAGON、原始地球、恩布利欧和奥拉真相。
- `curation-notes.md` 已指出 Ragna-mail/龙神器驾驶者转移、中队成员与战死节点、政治关系仍待补。
- `characters-index.json` 收录 14 个角色/实体：安琪、塔斯克、萨拉曼蒂妮、恩布利欧、奥拉、萨莉亚、希尔达、吉尔、薇薇安、桃香、朱利奥、西尔维娅、罗莎莉、克莉丝。
- `world.json` 已建立玛那、诺玛因子、Para-mail/Ragna-mail、DRAGON、旧人类技术等 powerSystems，以及米斯尔奇、阿尔泽纳尔、龙族、反恩布利欧阵营等 factions。
- `knowledge-graph.json` 有玛那、诺玛、龙族、阿尔泽纳尔、奥拉、恩布利欧、Ragna-mail、原始地球等关键节点。

### 主要缺口

#### A. 人物外表/服装/气质字段缺口（高优先级）

`characters-index.json` 的结构比 Claymore 完整，有 roles/factions/locations/abilities/items/relationships/importance，但仍缺少 `appearance`、`outfit`、`demeanor` 等字段。对《CROSS ANGE》尤其重要，因为角色身份变化与服装强绑定：皇女、囚犯/诺玛、驾驶员、龙族皇女、骑士团等。

优先补全角色：

1. `ange` 安琪：需补皇女礼装、阿尔泽纳尔制服/驾驶服、战斗状态、表情气质从傲慢皇女到强硬幸存者的阶段变化。
2. `salia` 萨莉亚：需补队长/驾驶员形象、渴望认可的气质、加入钻石玫瑰骑士团后的服装和姿态变化。
3. `hilda` 希尔达：需补不良/强势驾驶员气质、阿尔泽纳尔日常装/驾驶服、后期核心同伴的外显变化。
4. `salamandinay` 萨拉曼蒂妮：需补龙族皇女服饰、人形与龙族身份特征、歌/仪式感、焰龙号驾驶者视觉符号。
5. `embryo` 恩布利欧：需补优雅、支配性、神性/伪救世主气质，以及 Hysterica 相关视觉。
6. `tusk` 塔斯克：需补旧人类后裔/废墟生存者装束、潜入装备、行动风格。
7. `jill` 吉尔：需补司令制服、旧伤/创伤气质、前皇女/前驾驶员的双重形象。
8. `vivian`：需补活泼少女化外观与龙族身份阶段差异。
9. `momoka`：需补侍女服、忠诚支援者气质、非战斗支援视觉。
10. `rosalie`、`chris`：当前中队成员描写较薄，需补外观区分、驾驶员定位与阵营变化后的服装差异。

#### B. 阵营/服装模板缺口（高优先级）

建议建立以下可复用模板：

- 米斯尔奇皇族：礼服、玛那社会高贵/洁净审美、皇室标志。
- 玛那平民/贵族：乌托邦式洁净服饰、歧视诺玛的社会表情与仪态。
- 诺玛/阿尔泽纳尔：囚禁军事基地环境、制服、驾驶服、宿舍/作战整备装。
- Para-mail/Ragna-mail 驾驶员：驾驶姿态、头盔/战斗服、机体配色/个人标识。
- 钻石玫瑰骑士团：恩布利欧侧华丽化服装、Ragna-mail 对应视觉。
- 龙族/奥拉之民：人形服饰、龙形特征、仪式/歌/鳞片或鑨结晶意象。

#### C. 机体与驾驶者关联缺口（高优先级）

curation-notes 已明确“七台 Ragna-mail 与龙神器的驾驶者转移需逐项核对”。当前角色 `items` 中只零散出现 Villkiss、Hysterica、Cleopatra、Theodora、Raisia、焰龙号。建议补：

- 每台 Para-mail/Ragna-mail/龙神器的 `id`、驾驶者、阶段、阵营、外观、能力、剧情限制。
- 驾驶者转移或阶段性持有不要只写在角色 `items`，应有机体索引或 knowledge 节点。
- 安琪、萨莉亚、克莉丝、希尔达、吉尔、恩布利欧、萨拉曼蒂妮的机体关系需优先核对。

#### D. 人物覆盖缺口（中高优先级）

当前 14 人覆盖主线核心，但对 RP 全量内容仍偏少。建议补：

- 阿尔泽纳尔其他中队/教官/指挥链成员。
- 钻石玫瑰骑士团完整成员。
- 米斯尔奇政治人物与罗森布鲁姆王家相关人物。
- 龙族侧人物与奥拉之民社会成员。
- 与战死/叛变节点相关的配角。

#### E. 阶段化与公开度缺口（中优先级）

已有 `visibility` 与 stage-dependent notes，但缺少结构化 `stageVariants`。建议补：

- 安琪：皇女期、阿尔泽纳尔初期、Villkiss 驾驶期、反恩布利欧期。
- 萨莉亚/克莉丝：阿尔泽纳尔期、恩布利欧阵营期、回归/和解期。
- 薇薇安：诺玛驾驶员期、龙族真相公开期。
- 吉尔：司令期、旧计划真相期。

### CROSS ANGE 自适应扩充清单

优先级 P0：

- 为 14 个已索引角色补 `appearance`、`outfit`、`demeanor`、`stageVariants`。
- 建立阿尔泽纳尔制服/驾驶服、米斯尔奇皇族、龙族、钻石玫瑰骑士团四类视觉模板。
- 建立 Ragna-mail/Para-mail/龙神器机体索引，核对驾驶者阶段转移。

优先级 P1：

- 扩充阿尔泽纳尔中队成员、钻石玫瑰骑士团、龙族侧人物。
- 补每名驾驶员的机体配色、战斗风格、常用武装、驾驶时气质。
- 补社会视觉：玛那乌托邦表象 vs 诺玛隔离军事基地的反差。

优先级 P2：

- 细化米斯尔奇/罗森布鲁姆/高卢政治关系。
- 补战死/叛变时间点，与动画分集或源“卷”结构对齐。

---

## worlds/d-gray-man 审计

### 已有内容概况

- `README.md` 显示状态为 `manual-initial-expanded（chunk-1）`，主来源 `src-d-gray-man-001`，重点覆盖黑色教团、圣洁、恶魔、诺亚一族、千年伯爵、第十四号与阿尔玛线。
- `curation-notes.md` 已指出后期真相、宿主/记忆线条高冲突；方舟、北美分部、欧洲总局节点仍需细化；诺亚成员与恶魔制造过程可再扩。
- `characters-index.json` 收录 13 个角色/实体：亚连、神田、李娜丽、拉比、克劳斯、科穆伊、米兰达、柯洛利、千年伯爵、缇奇、罗德、阿尔玛、内亚。
- `world.json` 已有圣洁、诺亚、恶魔制造、驱魔师体系四类 powerSystems；黑色教团、伯爵阵营、诺亚一族、北美分部、欧洲总局、Bookman 系、隐秘线等 factions；多个地点节点。
- `knowledge-graph.json` 有圣洁、诺亚、恶魔、黑色教团、千年伯爵、方舟、内亚等关键节点，并补入规范化地点。

### 主要缺口

#### A. 人物外表/服装/气质字段缺口（高优先级）

`characters-index.json` 已有 roles/factions/locations/abilities/items/relationships/importance/visibility，但仍几乎没有外观与服装。D.Gray-man 的哥特/教团/诺亚视觉风格强烈，缺口明显。

优先补全角色：

1. `allen-walker` 亚连：需补白发、左眼/左臂圣洁、驱魔师团服、温和但负罪感强的气质、Crown Clown/圣洁阶段视觉变化。
2. `kanda-yu` 神田优：需补长发、冷峻剑士姿态、六幻携带方式、第二驱魔师/阿尔玛线阶段气质。
3. `lenalee-lee` 李娜丽：需补黑色教团制服、黑靴、机动战斗姿态、同伴中心型温柔坚韧气质。
4. `lavi` 拉比：需补眼罩/锤/书人学徒风格、轻佻外表与记录者距离感。
5. `cross-marian` 克劳斯：需补放荡导师、枪械、面具/礼帽/长发等标志化视觉；当前 name “克劳斯·马利安/神田十字”疑似混写，需核对。
6. `komui-lee` 科穆伊：需补教团高层/研究主管服装、兄控喜剧气质与行政状态。
7. `miranda-lotto` 米兰达：需补焦虑/疲惫支援者气质、时间能力视觉符号。
8. `crown-clown` 当前 id 与 name 不匹配：id 像亚连圣洁形态，但 name 是“亚歷斯特·柯洛利三世”。需核对并改为 `arystar-krory` 或类似；同时补吸血鬼风格外观。
9. `millennium-earl` 千年伯爵：需补圆胖绅士/高帽/伞/诡异微笑等强标志外观。
10. `tikki-mikk` 缇奇：需补人类轻佻伪装与诺亚觉醒后的视觉差异。
11. `road-kamelot` 罗德：需补少女外观、哥特服饰、梦境空间视觉符号。
12. `alma-karma`、`neal-d-campbell`：需补 GM-only 阶段外观与真相公开限制。

#### B. 组织/阵营视觉模板缺口（高优先级）

建议补以下模板：

- 黑色教团驱魔师团服：黑白色调、十字/玫瑰/教团纹样、长外套、装备携带。
- 科学班/后勤/教团高层：实验服、制服、行政/研究场景。
- 圣洁表现模板：装备型、寄生型、武器型；激活前/激活后视觉变化。
- Akuma 恶魔等级模板：机械外壳、灵魂悲剧感、等级进化差异。
- 诺亚一族：贵族/哥特/日常伪装与诺亚觉醒标记。
- 千年伯爵阵营：诡异童话、马戏/绅士/黑暗玩具风格。

#### C. 人物覆盖缺口（高优先级）

当前角色数量偏少。D.Gray-man 主线 RP 需要更多人物：

- Bookman 本人：当前 `lavi` relationships 中 `bookman` unresolved，明确“not indexed”。应补为角色。
- 黑色教团驱魔师与元帅：如其他重要驱魔师/元帅/科学班核心成员（需按来源核对）。
- 诺亚家族成员：curation-notes 已提示诺亚家族成员仍可再扩，当前只有缇奇、罗德、内亚，加上伯爵阵营，明显不足。
- 北美分部/阿尔玛线相关人物：应补与第二驱魔师、第三驱魔师、实验线有关的人物。
- 伯爵阵营与 Akuma 制造相关 NPC 类型：制造过程、等级恶魔、牺牲者模板。

#### D. ID/命名一致性风险（高优先级）

需要优先核对：

- `crown-clown`：id 应指亚连圣洁“神之道化/Crown Clown”，但 name 是“亚歷斯特·柯洛利三世”。这是实质索引错误风险。
- `cross-marian` 的中文名写为“克劳斯·马利安/神田十字”，其中“神田十字”疑似误译/混入，应核对。
- `neal-d-campbell` 与 knowledge-graph 节点 `nea` 存在 id 不一致：角色索引用 `neal-d-campbell`，知识图谱用 `nea`。建议建立 alias 或统一 canonical id。
- `tikki-mikk` 拼写已规范化，但仍建议统一 Tiki/Tyki/Tikki 的 alias。
- `road-kamelot` 中文“罗德·嘉美”可能需补常见译名 alias。

#### E. 阶段化与可见性缺口（中高优先级）

已有 `visibility`，但需要结构化阶段：

- 亚连：早期驱魔师、方舟后、十四号线觉醒风险、Crown Clown 阶段。
- 神田：普通驱魔师、阿尔玛线、第二驱魔师真相。
- 李娜丽：黑靴状态变化、失去/重获战力阶段。
- 诺亚角色：日常伪装、诺亚觉醒、方舟/后期阶段。
- 千年伯爵/内亚：GM-only 真相分层，避免一次性公开。

### D.Gray-man 自适应扩充清单

优先级 P0：

- 修正/核对 `crown-clown` id 与柯洛利角色错配风险。
- 核对 `cross-marian` 中文名混写风险。
- 为 13 个已索引角色补 `appearance`、`outfit`、`demeanor`、`stageVariants`。
- 建立黑色教团制服、圣洁形态、诺亚觉醒、Akuma 等级、千年伯爵阵营视觉模板。

优先级 P1：

- 补 Bookman 本人，解决 `lavi` 的 unresolved relationship。
- 扩充诺亚家族成员、教团元帅/驱魔师/科学班、北美分部与阿尔玛线人物。
- 统一 `neal-d-campbell` / `nea` canonical id 与 alias。

优先级 P2：

- 细化方舟、北美分部、欧洲总局出场节点。
- 补恶魔制造过程、恶魔等级、牺牲者/悲愿模板，区分公开信息与 GM-only 真相。

---

## 跨世界建议：统一补全字段模板

建议后续扩充时，为 `characters-index.json` 增加统一结构，避免每个世界自由文本漂移：

```json
{
  "appearance": {
    "ageLook": "",
    "hair": "",
    "eyes": "",
    "build": "",
    "heightImpression": "",
    "distinguishingFeatures": []
  },
  "outfit": {
    "default": "",
    "combat": "",
    "formalOrCivilian": "",
    "stageVariants": []
  },
  "demeanor": {
    "firstImpression": "",
    "bodyLanguage": "",
    "voiceTone": "",
    "emotionalTexture": ""
  },
  "visualMotifs": [],
  "stageVariants": [
    {
      "id": "",
      "arc": "",
      "visibility": "public/gm-only",
      "appearanceChanges": "",
      "outfitChanges": "",
      "personalityShift": ""
    }
  ]
}
```

按优先级分批：

1. P0：critical/high 角色与明显索引错误。
2. P1：medium 角色、阵营模板、机体/装备模板。
3. P2：地点氛围、配角、别名译名、章节/时间线校对。

---

## 最终风险清单

- `Claymore`：人物数量较多但结构最薄，几乎全员缺少外观/服装字段；未来线与初始线混放，需阶段化。
- `CROSS ANGE`：世界系统较完整，但驾驶服/机体/阵营服饰和机体驾驶者转移缺口明显；角色覆盖仍偏主线核心。
- `D.Gray-man`：已有规范化痕迹，但存在较高优先级索引风险（`crown-clown`、`cross-marian`、`nea`/`neal-d-campbell`）；诺亚家族与教团人物覆盖不足；视觉模板缺口明显。

验证状态：本次未运行 JSON schema 校验或脚本；仅基于文件读取和人工审计。未修改任何 curated 文件。
