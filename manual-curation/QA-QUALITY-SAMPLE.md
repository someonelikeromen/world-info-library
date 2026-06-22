# QA-QUALITY-SAMPLE：人工高风险质量抽样复核

日期：2026-06-22  
复核人：quality-sample 子任务  
范围：仅人工阅读重点世界 `curated/README.md`、`characters-index.json`、`world.json`、`curation-notes.md`；必要时参考图谱入口说明，但未改动任何 `worlds/*/curated` 正文。

## 结论总览

- 本轮抽样覆盖 12 个世界：补齐组 4 个（`dantalian-no-shoka`, `date-a-live`, `toriko`, `madan-no-ou`）与高风险/特殊组 8 个（`acg-character-database`, `blue-archive`, `monster-hunter`, `infinite-stratos`, `taimanin`, `testament-sister-new-devil`, `toaru`, `jojo`）。
- 未发现 curated 正文中存在会被运行时直接执行的明显系统级控制文本；多数高风险世界在 notes/README 中明确把源内状态栏、变量、输出格式、成人向规则、`{{user}}` 玩家设定排除。
- 主要风险不是 JSON 结构本身，而是：单源世界书可靠度、原作/IF/玩家替代线混杂、成人向源材料的 SFW 化边界、跨作品数据库被误当单一世界、以及人物索引中“角色类型/岗位”与“ canon 固定人物”混合。
- 未运行机器 JSON/schema 校验；本报告为人工抽样质量判断，不替代 schema 校验与交叉引用校验步骤。

## 抽样明细

### 1. `dantalian-no-shoka`

- 阅读文件：`worlds/dantalian-no-shoka/curated/README.md`、`characters-index.json`、`world.json`、`curation-notes.md`。
- 控制文本残留：未见明显可执行控制文本。README/notes 明确说明源中曾有 NSFW/角色卡控制文本，但 curated 只保留世界观与 RP 安全事实。
- 二创/IF 与原作边界：边界处理较好；默认采用战后近代欧陆/英伦式原作主线，坏结局、回溯提示与 IF 归为 sandbox。需要注意“教授/哈尔”称谓混用已人工拆分。
- 人物索引质量：较高。主要人物、支线事件人物、势力、能力、visibility、evidenceLevel、sourceRefs 均较完整；读姬/钥匙守护者/焚书官/窃贼/教授轴线清晰。
- 低置信项：第 6-8 卷若干人物与事件（不死杀手卫斯理、欧立克、奥利佛、怪盗秘银、莉菲雅等）标 B/C 或 notes 待补；幻书名称存在中译/音译/意译混用。
- RP 调用注意：OC 不应默认取代修伊钥匙守护者身份；幻书能力须受媒介、仪式、代价、读者资格限制；血腥、精神操控、人体改造、血亲禁忌等应作为哥特悬疑元素而非露骨化内容。

### 2. `date-a-live`

- 阅读文件：`worlds/date-a-live/curated/README.md`、`characters-index.json`、`world.json`、`curation-notes.md`。
- 控制文本残留：未见明显可执行控制文本；notes 明确排除大量 `character-nsfw`、状态栏、成人向身体描写和互动规则。
- 二创/IF 与原作边界：处理较清楚。默认主线为天宫市、精灵、空间震、Ratatoskr/AST/DEM；玩家为士道/DEM BOSS/真士转生/同班同学等入口被列为可选 sandbox/IF，不写作正史。Date A Bullet/邻界支线作为可选层。
- 人物索引质量：主线精灵与核心组织人物齐全，八舞姐妹拆分合理，士织作为士道变体处理避免误列独立人物。visibility 对澪、维斯考特、真士等剧透控制较好。
- 低置信项：维斯考特、真士转生关系、白之女王、临界其他配角、阿尔缇米希亚、澪终局机制多为 B/C 或摘要级。
- RP 调用注意：精灵封印需情绪稳定与关系建立，不能简化成无成本能力；DEM 实验和创伤线要避免成人化/强制化描写；主线与邻界支线默认不自动混线。

### 3. `toriko`

- 阅读文件：`worlds/toriko/curated/README.md`、`characters-index.json`、`world.json`、`curation-notes.md`。
- 控制文本残留：未见明显控制文本残留。文件内有“取代/共存模式”提示，但作为 RP 使用说明而非指令。
- 二创/IF 与原作边界：默认原作主线；阿虏是否被用户取代由外部模式决定，curated 不强绑用户身份。终局剧透（阿卡西亚、NEO、八王菜单）以 gm-only/骨架保留。
- 人物索引质量：核心人物较完整，包含阿虏、小松、四天王、一龙、次郎、三虎、阿卡西亚、乔亚等；后续厨师榜单和美食会干部覆盖程度取决于源。
- 低置信项：单源；八王、全套菜单、NEO 终局线仍偏骨架；个别厨师译名差异未充分展开。
- RP 调用注意：捕获等级不应简单等同数值战力，应结合生态、环境、料理准备；高端战力不宜低威胁场景降格；食欲恶魔与美食细胞应保留代价和失控风险。

### 4. `madan-no-ou`

- 阅读文件：`worlds/madan-no-ou/curated/README.md`、`characters-index.json`、`world.json`、`curation-notes.md`。
- 控制文本残留：未见明显可执行控制文本。
- 二创/IF 与原作边界：重点风险已被明确处理。本篇《魔弹之王与战姬》为 canonical main；《冻涟的雪姬》IF 单独列入 alternateContinuities；取代/共存模式不强加堤格尔身份。
- 人物索引质量：七战姬、堤格尔、布琉努/吉斯塔特政治人物、黑弓/龙具/魔物关系较清楚；强调战姬是政治军事领袖，不是单纯感情附庸。
- 低置信项：若干后期或分散人物（巴多兰、葛雷亚斯特、撒迦利亚、尤金、琉蒂、桂妮薇亚等）待补；米莉兹/米莉札译名浮动；乌鲁斯、拉娜在本篇与 IF 中状态冲突。
- RP 调用注意：调用前必须确定本篇还是冻涟 IF；黑弓真实来历、蒂尔·纳·法、凡伦蒂娜王位野心、圣窟宫终局默认 GM-only；龙技有体力/恢复代价。

### 5. `acg-character-database`

- 阅读文件：`worlds/acg-character-database/curated/README.md`、`characters-index.json`、`world.json`、`curation-notes.md`。
- 控制文本残留：未见可执行控制文本。README/notes 明确源含成人作品、NTR、性暴力、露骨身体细节，curated 仅保留名称、来源作品、心理/角色分类。
- 二创/IF 与原作边界：特殊风险最高之一：它不是单一世界，而是跨作品角色心理/类脑数据库。world.json 已明确 `isSingleFictionalWorld: false`，不构造统一地理/剧情。
- 人物索引质量：以 observed 清单为主，覆盖大量跨作品角色与人格模板；适合作索引/参考库，不适合作统一 RP 世界。关系图不应虚构跨作品关系。
- 低置信项：原始库巨大且重复；2月/3月/心理模型包多版本未完全去重；成人作品来源名保留但不代表露骨内容可用。
- RP 调用注意：运行时必须把它当“参考库/人格原型库”，禁止自动把不同作品角色合并进同一 continuity；涉及未成年或成人源角色时只能调用非露骨人格/语气参考。

### 6. `blue-archive`

- 阅读文件：`worlds/blue-archive/curated/README.md`、`characters-index.json`、`world.json`、`curation-notes.md`。
- 控制文本残留：未见明显控制文本。
- 二创/IF 与原作边界：人物分类原为空，curated 以世界设定与组织岗位补角色；这是合理但需明确不是完整官方角色库。
- 人物索引质量：索引偏“RP 角色类型/组织岗位”，明确标注 sourceStatus；直接提及姓名如空崎阳奈、莉音、龙华妃咲，其他多为风纪委员、修女会、温泉开发部等岗位角色。
- 低置信项：角色表不是完整 Blue Archive 全角色数据库；老师/先生是 RP 常用核心身份而非由原 characters 分类直接提供；未运行 JSON 校验。
- RP 调用注意：基沃托斯枪战应按光环/神秘与超常耐久处理，避免现实致死化；老师作为成人调停者须保持保护与信任边界；学院自治与社团政治是核心，不宜只写成普通校园。

### 7. `monster-hunter`

- 阅读文件：`worlds/monster-hunter/curated/README.md`、`characters-index.json`、`world.json`、`curation-notes.md`。
- 控制文本残留：未见明显控制文本。
- 二创/IF 与原作边界：系列综合/现实化叙事而非单一代作品剧情；以猎人公会、生态调查和区域巡礼为核心。
- 人物索引质量：源缺少固定姓名角色，索引以职业/岗位/生态角色为主（猎人、受付员、公会主管、村长、加工屋、艾露猫、观测员、古龙、禁忌怪物等）。作为 RP 可用，但不是 NPC 姓名表。
- 低置信项：源可靠度 C；若需要严格 canon NPC，需补历代村长、受付员、调查团成员等姓名条目；未运行 JSON 校验。
- RP 调用注意：怪物不是恶人；狩猎应强调准备、观察、道具、装备制作与生态平衡。HR/MR 等游戏化机制应转译为任务星级/地区认证。

### 8. `infinite-stratos`

- 阅读文件：`worlds/infinite-stratos/curated/README.md`、`characters-index.json`、`world.json`、`curation-notes.md`。
- 控制文本残留：curated 正文未保留可执行成人模板；README/notes 明确源含写卡、游戏模式、状态栏、成人偏好等，已排除。
- 二创/IF 与原作边界：主条采用 IS 学园，记录源内“青羽学园”可能为改写舞台称呼；人物部分含 RP 常用补全。
- 人物索引质量：核心角色与机体关系可用（织斑一夏、千冬、箒、塞西莉亚、铃音、夏洛特、拉芙拉、更识姐妹、山田真耶、束、亡国机业角色等），但字段相对简略，无 visibility/evidenceLevel。
- 低置信项：自动分类将大量模板归入 characters/world/factions；部分人物为常识性补全，并非每个都有独立源 key。
- RP 调用注意：不要继承源内成人化状态栏或玩家控制模板；IS 训练赛要围绕机体核心、护盾、同步率、国家技术博弈；织斑一夏男性驾驶者身份是世界秩序风险点，不应随意复制给 OC，除非模式明确。

### 9. `taimanin`

- 阅读文件：`worlds/taimanin/curated/README.md`、`characters-index.json`、`world.json`、`curation-notes.md`。
- 控制文本残留：高风险但处理清楚。characters-index 明确 `excludedEntries` 包含 `{{user}}寄生魔设定`、`{{user}}状态栏`、`NPC状态栏`；source policy/notes 说明成人化玩家设定和状态栏控制文本未纳入。
- 二创/IF 与原作边界：当前基于单一世界书且角色较少；部分设定可能是世界书改写版本，后续需官方向资料拆分版本。
- 人物索引质量：主要 SFW 人物可用：井河阿莎姬、水城雪风、秋山凛子、高坂静流、水城不知火及相关家族人物。五车学园被标注为非人物但核心机构，透明度较好。
- 低置信项：角色数量少；不知火“任务失败后魔化”等源语境原本成人向，curated 只保留剧情事实，仍需谨慎。
- RP 调用注意：只调用五车学园训练、魔界裂隙侦察、潜入/救援、家族忍法等 SFW 任务线；不得恢复源内寄生魔玩家设定、状态栏或成人向堕落描写。

### 10. `testament-sister-new-devil`

- 阅读文件：`worlds/testament-sister-new-devil/curated/README.md`、`characters-index.json`、`world.json`、`curation-notes.md`。
- 控制文本残留：未见可执行控制文本；notes 明确将“原作主角完全替换”“双主角并行”、输出格式、变量规则视为技术/玩法控制文本；成人化契约与攻略法则不纳入正文。
- 二创/IF 与原作边界：现代校园、勇者/魔族/神族政治与主从契约被保留；成人化契约触发机制被剥离。替换/并行主角玩法已排除。
- 人物索引质量：人物清单覆盖较广，含刃更、澪、万理亚、柚希、胡桃、洁丝特、长谷川、雷欧哈特、拉斯、东城迅、枢机院等；部分角色仅简述。
- 低置信项：部分人物如瑟菲雅、拉法艾琳、露绮亚、加尔多等需后续细分阵营与剧情；源剧情摘要含成人化措辞，SFW 抽取可能遗漏细节。
- RP 调用注意：主从契约只能作为保护、定位、能力联系与誓约绑定机制；不得调用露骨触发。魔王之力、多族血脉和枢机院政治适合 GM 控制揭露节奏。

### 11. `toaru`

- 阅读文件：`worlds/toaru/curated/README.md`、`characters-index.json`、`world.json`、`curation-notes.md`。
- 控制文本残留：未见可执行控制文本；notes 明确排除 `[InitVar]`、变量更新、剧情规则、输出格式。
- 二创/IF 与原作边界：覆盖旧约早期至 9月30日前后，兼容超炮相关角色；欧提努斯等超出旧约早期主线的角色被注明。
- 人物索引质量：较完整，科学侧/魔法侧主要人物、暗部 ITEM/SCHOOL、英国清教、罗马正教、神之右席、木原等均有索引；非人物节点如幻想杀手、个人现实、妹妹计划排除到知识节点。
- 低置信项：不是全系列完整设定；个别译名按源保留；角色覆盖偏旧约前中期与部分角色卡。
- RP 调用注意：科学侧与魔法侧法则不同，避免混成单一魔法系统；幻想杀手不是万能胜利键；Level 5、魔神、亚雷斯塔、神之右席等需要分层剧透与战力约束。

### 12. `jojo`

- 阅读文件：`worlds/jojo/curated/README.md`、`characters-index.json`、`world.json`、`curation-notes.md`。
- 控制文本残留：未见成人化、状态栏或技术控制内容；notes 明确替身/波纹/石鬼面不列为人物。
- 二创/IF 与原作边界：当前本地源主要覆盖第一至第三部，world.json 也只建三段 eras；不应把后续部默认纳入。
- 人物索引质量：对 1-3 部核心人物可用，含乔纳森、迪奥、齐贝林、乔瑟夫、莉莎莉莎、卡兹、承太郎、远征队与恩雅等；来源是长篇剧情说明拆分而非独立角色卡。
- 低置信项：未覆盖第四部以后；人物字段简洁，sourceEntries 为条目编号，缺少更细 visibility/evidenceLevel。
- RP 调用注意：调用前确认时代：石鬼面/波纹（1-2部）与替身（3部）不要无说明混用；DIO 时间停止、柱之男究极生命等高危能力需要严格限制；后续部人物不应从此档案推断。

## 横向风险与建议

1. **控制文本残留**：`taimanin`, `testament-sister-new-devil`, `toaru`, `infinite-stratos`, `date-a-live` 均明确识别并排除源内状态栏/变量/输出格式/成人向规则。运行时仍建议检索层优先读取 `curation-notes.md` 中的排除说明。
2. **成人向源材料风险**：`taimanin`, `testament-sister-new-devil`, `date-a-live`, `acg-character-database`, `infinite-stratos`, `dantalian-no-shoka` 都有源内成人/NSFW/露骨化背景；curated 已 SFW 化，但生成侧必须避免从 raw/imports 回流这些内容。
3. **IF/替代线风险**：`madan-no-ou`、`date-a-live`、`toriko`、`infinite-stratos` 明确存在取代/共存/IF/玩家身份入口。调用前需要 continuity 参数，否则容易把 IF 写成正史。
4. **非标准人物索引**：`acg-character-database` 是跨作品参考库；`blue-archive` 与 `monster-hunter` 人物表大量为岗位/角色类型；`jojo` 是剧情拆分索引。检索器不应把这些等同于完整 canon 角色数据库。
5. **低置信/单源问题**：多数文件 notes 均写明未运行机器 JSON 校验，且部分世界单源。后续 schema/交叉引用校验应重点检查字段名差异（如 `worldId` vs `worldSlug`、schema 名称差异）和角色/势力引用。

## 验证状态

- 已完成：人工阅读 12 个世界的 4 类重点 curated 文件并形成抽样报告。
- 未完成/不在本 step 范围：未修改任何 `worlds/*/curated` 正文；未运行 JSON/schema 解析器；未做全量交叉引用自动校验；未刷新总索引。
- 本 step 唯一写入文件：`manual-curation/QA-QUALITY-SAMPLE.md`。
