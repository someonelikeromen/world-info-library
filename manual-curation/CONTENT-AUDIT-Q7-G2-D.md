# Q7A 全量内容完整度审计｜第2组 D（jojo / kaguya-sama / kekkaishi）

**审计目标**：逐个通读指定世界的 `curated/README.md`、`curation-notes.md`、`characters-index.json`，必要时参考其他 curated 文件判断缺口，列出自适应扩充清单。

**写入范围**：仅本报告；未修改世界正文。

---

## 总体结论

三套世界均已具备 curated 骨架，但内容完整度差异明显：

- `worlds/jojo`：已覆盖第 1～3 部核心主线、能力体系和跨代关系，但 README/notes 仍是摘要级，人物卡缺外观、服装、气质、招式演出、敌方替身使者群与事件节点；世界地点/事件字段几乎空。
- `worlds/kaguya-sama`：结构最轻，适合“校园恋爱喜剧”初始检索，但只保留学生会核心六人，缺大量家庭、同学、学园活动、后期成长线；人物外观/服装/说话风格/喜剧节奏基本未结构化。
- `worlds/kekkaishi`：世界结构相对最完整，已覆盖乌森、结界术、主要势力与关键人物；但仍偏设定骨架，夜行/里会/扇家/黑芒楼/宙心丸历史线需要细化，人物视觉与战斗演出缺口同样明显。

### 共同缺口

1. **人物视觉信息不足**：`appearance`、`outfit`、`visualMarkers`、年龄感、体型、发色/瞳色、标志物普遍缺失。
2. **气质/说话风格不足**：多数只用 `summary`、`role`、`notes` 说明功能，未记录第一印象、台词风格、动作习惯、喜剧/压迫感。
3. **能力表现偏摘要**：能力名称已列，但缺实战动作、限制、代价、典型战例与 RP 可触发场景。
4. **事件链不足**：现有内容多是“设定结论”，缺可回放的场景节点、章节/篇章推进、冲突开场。
5. **关系动态不足**：关系图多记录亲属/敌对/同伴关系，缺误会、竞争、情感转折、阵营政治等动态变化。

---

## 1) `worlds/jojo`

### 已审计文件

- `worlds/jojo/curated/README.md`
- `worlds/jojo/curated/curation-notes.md`
- `worlds/jojo/curated/characters-index.json`
- 参考：`worlds/jojo/curated/world.json`
- 参考：`worlds/jojo/curated/knowledge-graph.json`
- 参考：`worlds/jojo/curated/relationship-graph.json`

### 现状判断

- `README.md` 仅说明整理对象、标准产物与整理重点，是目录说明而非世界百科。
- `curation-notes.md` 明确本地源主要覆盖第一至第三部：乔纳森/迪奥、乔瑟夫/柱之男、承太郎/埃及远征。
- `characters-index.json` 已列 18 名左右核心角色，涵盖乔斯达血脉、迪奥、波纹导师、柱之男代表、第三部远征队。
- `world.json` 有 `eras`、`powerSystems`、`factions`，但 `locations`、`publicEvents`、`hiddenEvents` 为空。
- `knowledge-graph.json` 有石鬼面、波纹、柱之男、替身、时间停止、埃及等核心节点，但粒度很粗。
- `relationship-graph.json` 覆盖家族、师徒、敌对、远征队关系，但关系动态仍偏单句摘要。

### 主要缺口

#### 人物覆盖缺口

当前覆盖重点是第 1～3 部主线，但仍缺：

- 第一部：艾莉娜、史比特瓦根、达利欧、布拉霍、塔卡斯等。
- 第二部：史特雷、史摩基、修特罗海姆、艾西迪西、瓦姆乌、桑塔纳、苏西 Q 等。
- 第三部：安、荷尔·荷斯、J·盖尔、佩特夏、达比兄弟、瓦尼拉·艾斯、恩多尔、玛莱雅、阿雷西等关键敌方替身使者。
- 第四部以后：未覆盖，若世界目标是“JOJO 全系列”，还缺东方仗助、乔鲁诺、徐伦、乔尼、定助等后续主角和体系扩展。

#### 角色信息缺口

核心角色普遍缺：

- **外表**：乔纳森/乔瑟夫/承太郎/迪奥等体型、面部轮廓、发型、年龄段差异。
- **服装**：第一部贵族/冒险装、第二部训练/军装风格、第三部校服与旅装、迪奥各时代服饰。
- **气质**：乔纳森的绅士感、乔瑟夫的机智轻浮、承太郎的冷峻寡言、迪奥的支配欲与邪魅感未结构化。
- **战斗演出**：波纹动作、替身出拳、时间停止表现、柱之男身体能力缺典型镜头。
- **台词/行为习惯**：JOJO 系列高度依赖姿势、宣言、口癖与夸张演出，目前未收录。

#### 世界设定缺口

- **地点**：英国乔斯达宅邸、风骑士之镇、游轮、纽约、罗马/威尼斯、柱之男遗迹、日本、香港、印度、巴基斯坦、埃及、开罗等未结构化。
- **事件**：石鬼面觉醒、乔纳森牺牲、柱之男复苏、波纹训练、卡兹究极生命化、荷莉病倒、埃及远征、DIO 决战等未进入事件表。
- **组织/阵营**：史比特瓦根财团、纳粹军方、迪奥替身使者网、塔罗牌/埃及九荣神敌人分组缺失。
- **规则**：替身射程、破坏力/速度等参数、替身相互可见规则、波纹训练限制、石鬼面/红石机制仍是摘要。

### 自适应扩充清单

1. 先按“第一部 / 第二部 / 第三部”补全篇章事件表与地点表。
2. 为主角与主要反派新增 `appearance`、`outfit`、`aura`、`mannerisms` 字段。
3. 为替身使者补“替身外观 + 能力限制 + 代表战斗 + RP 场景钩子”。
4. 补充史比特瓦根财团、柱之男完整成员、迪奥替身使者网等组织节点。
5. 将 `world.json.locations`、`publicEvents`、`hiddenEvents` 从空数组扩展为可检索条目。
6. 若目标扩展为全 JOJO，应按部数建立分层索引，避免第 1～3 部与后续设定混淆。

### 优先级

- **高**：乔纳森、迪奥、乔瑟夫、承太郎、远征队成员的视觉/服装/气质补全。
- **高**：地点与事件表补全。
- **中高**：第三部敌方替身使者和替身能力细化。
- **中**：第 4 部以后内容扩展，取决于是否定义为全系列世界。

---

## 2) `worlds/kaguya-sama`

### 已审计文件

- `worlds/kaguya-sama/curated/README.md`
- `worlds/kaguya-sama/curated/curation-notes.md`
- `worlds/kaguya-sama/curated/characters-index.json`
- 参考：`worlds/kaguya-sama/curated/world.json`
- 参考：`worlds/kaguya-sama/curated/knowledge-graph.json`
- 参考：`worlds/kaguya-sama/curated/relationship-graph.json`

### 现状判断

- `README.md` 只有一段状态说明，指出来源包含秀知院学园、学生会、恋爱头脑战与主要人物条目。
- `curation-notes.md` 很短，只列人工判断、低置信和验证状态。
- `characters-index.json` 仅 6 人：白银御行、四宫辉夜、藤原千花、石上优、伊井野弥子、早坂爱。
- `world.json` 已有非超自然定位、恋爱头脑战、秀知院学生会、秀知院学园、学生会活动室、学生会日常、告白与身份压力。
- `knowledge-graph.json` 只有恋爱头脑战、秀知院学园、学生会 3 个节点。
- `relationship-graph.json` 仅 3 条核心关系：白银-辉夜、辉夜-早坂、石上-伊井野。

### 主要缺口

#### 人物覆盖缺口

作为《辉夜大小姐》世界，当前角色覆盖明显偏少，缺：

- 四宫家线：四宫雁庵、四宫黄光、四宫云鹰、四宫青龙等家族压力来源。
- 白银家线：白银圭、白银父亲、白银母亲相关背景。
- 藤原家线：藤原萌叶、藤原丰实等家庭/政治背景。
- 学园同学与社交圈：柏木渚、田沼翼、子安燕、大佛小钵、纪可怜、巨濑绘理香等。
- 教师/校方/活动相关角色：校长、学园活动组织者等。
- 后期关键人物与大学/毕业相关线未覆盖。

#### 角色信息缺口

6 名核心角色均缺：

- **外表**：发型、发色、身高感、表情特征、年龄/年级视觉感。
- **服装**：秀知院制服、私服、礼服、活动服、伪装服/工作装等。
- **气质**：白银的努力型紧绷感、辉夜的大小姐冷感与动摇反差、千花的天然破坏力、石上的阴沉吐槽、伊井野的正义感与脆弱感、早坂的多重伪装人格。
- **说话风格**：恋爱喜剧非常依赖内心旁白、误会推进、吐槽节奏，目前未结构化。
- **关系细节**：只记录了主关系，缺藤原与辉夜/白银的训练与扰局、石上成长线、伊井野与大佛/石上的三角张力、早坂与四宫家的压力。

#### 世界设定缺口

- **地点**：秀知院不同教室、学生会室细节、体育馆、文化祭场地、天文台/告白场景、四宫宅、白银家、早坂活动地点等未展开。
- **事件**：学生会选举、烟花篇、体育祭、文化祭、修学旅行、圣诞/情人节、毕业与留学等关键篇章未结构化。
- **组织**：四宫财阀、白银家庭、藤原政治家族、风纪委员、应援团/社团、学生会历届结构缺失。
- **规则**：恋爱头脑战只有一句定义，缺“误会—试探—反噬—旁白裁定”的喜剧运行机制。

### 自适应扩充清单

1. 为六名核心角色补 `appearance`、`outfit`、`aura`、`speechStyle`、`mannerisms`。
2. 扩充人物索引：四宫家、白银家、藤原家、柏木/翼、子安燕、大佛小钵等至少作为二线角色入库。
3. 建立“学园事件表”：选举、烟花、体育祭、文化祭、修学旅行、毕业/留学。
4. 扩充地点：学生会室细节、秀知院校内区域、四宫宅、白银家、活动场地。
5. 将恋爱头脑战规则拆成 RP 可执行模板：目标、诱导、误会、旁白裁判、失败反噬、喜剧打断。
6. 在关系图中补充藤原千花与主线二人的扰局关系、石上成长线、伊井野/大佛/子安燕相关动态。

### 优先级

- **高**：核心六人的外观/服装/气质/说话风格。
- **高**：四宫家与白银家压力线。
- **中高**：学园活动事件表与关键地点。
- **中**：后期毕业/大学路线，需避免把固定结局强写进开放沙盒。

---

## 3) `worlds/kekkaishi`

### 已审计文件

- `worlds/kekkaishi/curated/README.md`
- `worlds/kekkaishi/curated/curation-notes.md`
- `worlds/kekkaishi/curated/characters-index.json`
- 参考：`worlds/kekkaishi/curated/world.json`
- 参考：`worlds/kekkaishi/curated/knowledge-graph.json`
- 参考：`worlds/kekkaishi/curated/relationship-graph.json`

### 现状判断

- `README.md` 明确状态为 `manual-initial-expanded（chunk-1）`，整理重点为乌森之地、墨村/雪村、结界术、夜行、里会、黑芒楼与历史真相。
- `curation-notes.md` 已记录关键人工判断：乌森作为地点兼力量节点、结界术步骤、间时守/守美子/宙心丸线保持 GM-only/待补。
- `characters-index.json` 已列 17 名左右人物/式神/敌方，覆盖良守、时音、正守、志志尾、长老、守美子、犬神、黑芒楼、夜行、扇七郎、龙姬、间时守。
- `world.json` 已有较完整的力量体系、势力、地点和战斗规则。
- `knowledge-graph.json` 覆盖乌森、结界术、墨村/雪村、夜行、里会、黑芒楼、妖怪生态等，但部分节点是 minimal repair 补丁型摘要。
- `relationship-graph.json` 有主角搭档、兄弟、式神、正守-志志尾、志志尾-火黑、间时守-良守等关系；守美子、公主/黑芒、扇七郎仅为最小节点，无边。

### 主要缺口

#### 人物覆盖缺口

当前人物清单较好，但仍需扩充/细校：

- 夜行：大量成员只列刃鸟美希、细波慧，其他成员、能力分工、组织层级未覆盖。
- 里会：干部、议会结构、总帅/管理层、内部斗争线不足。
- 扇家：扇七郎只有单条摘要，扇一族关系、能力体系、政治位置未展开。
- 黑芒楼：公主/黑芒、白/白沼、火黑已列，但其他干部、妖怪组织结构、黑芒楼内部关系仍薄。
- 宙心丸：curation-notes 明确未单列成角色，是核心待补缺口。
- 墨村/雪村家族：父母、兄弟姐妹、家族日常与继承制度仍可补。

#### 角色信息缺口

主要人物均缺：

- **外表**：良守、时音、正守、志志尾、守美子、火黑等视觉识别点未结构化。
- **服装**：校服、夜间战斗装、夜行制服/任务服、里会服饰、妖怪形态装饰未列。
- **气质**：良守的执拗与温柔、时音的冷静严厉、正守的压抑野心、志志尾的孤独感、守美子的神秘超然、火黑的战斗狂气未形成字段。
- **能力演出**：结界术虽有“方围、定础、结、灭”，但人物级战斗差异、速度/精度/领域感、异能者具体能力缺少战例。
- **GM-only 分层**：间时守、守美子、宙心丸线已标注风险，但公开/隐藏信息如何逐步揭露还未拆成事件节点。

#### 世界设定缺口

- **地点细化**：乌森学园夜间区域、屋顶/校庭/旧址、墨村家/雪村家内部、夜行据点、里会设施、黑芒楼空间结构仍是名称级。
- **事件链**：志志尾篇、黑芒楼篇、里会政治篇、扇家篇、乌森真相/宙心丸篇未形成时间线。
- **组织结构**：夜行编制、里会权力结构、黑芒楼指挥关系、墨村/雪村继承规则仍需展开。
- **规则细化**：乌森强化机制、妖怪进化风险、结界术高级应用、异能者分类、土地神/灵地生态缺少细颗粒条目。

### 自适应扩充清单

1. 为良守、时音、正守、志志尾、守美子、火黑、间时守、扇七郎补人物视觉三件套：`appearance` / `outfit` / `aura`。
2. 扩充夜行成员表：成员、能力、任务分工、与正守关系、是否公开。
3. 扩充里会/扇家政治线：组织层级、关键人物、派系冲突、后期事件。
4. 将宙心丸单列为 GM-only 或 spoiler 分层角色/核心节点，并补与乌森、间时守、守美子的关系。
5. 为黑芒楼补完整干部与妖怪生态，包括内部服从关系、目标、入侵乌森的事件顺序。
6. 把 `publicEvents` / `hiddenEvents` 从空数组扩展为：夜间守护日常、志志尾事件、黑芒楼入侵、里会冲突、乌森真相揭露。
7. 将乌森学园、夜行据点、里会设施、黑芒楼等地点从名称级扩展为场景级描述。

### 优先级

- **高**：良守、时音、正守、志志尾、守美子、火黑的外观/服装/气质与战斗演出。
- **高**：宙心丸与乌森历史真相的 GM-only 分层补全。
- **中高**：夜行、里会、扇家组织结构。
- **中**：黑芒楼干部与妖怪生态细化。

---

## 按世界完整度分级

| 世界 | 骨架完整度 | 人物细节 | 世界事件/地点 | 主要风险 |
|---|---:|---:|---:|---|
| `jojo` | 中 | 中低 | 低 | 覆盖仅第 1～3 部；地点/事件为空；视觉与替身战斗演出缺失 |
| `kaguya-sama` | 中低 | 低 | 低 | 只列学生会核心六人；家庭/同学/活动线缺口大 |
| `kekkaishi` | 中高 | 中低 | 中 | 世界骨架好，但后期政治/历史线和人物视觉仍待补 |

---

## 统一补全建议模板

建议后续角色条目统一增加以下可选字段：

```json
{
  "appearance": {
    "ageImpression": "",
    "build": "",
    "hair": "",
    "eyes": "",
    "visualMarkers": []
  },
  "outfit": {
    "default": "",
    "combatOrWork": "",
    "formalOrSpecial": ""
  },
  "aura": {
    "firstImpression": "",
    "temperamentKeywords": [],
    "speechStyle": "",
    "mannerisms": []
  },
  "rpHooks": []
}
```

如需压缩，至少保证核心人物有：

1. 1 条外观识别点；
2. 1 条常见服装/战斗服/制服说明；
3. 1 条气质或说话风格；
4. 1 条可直接开局的 RP 钩子。

---

## 验证状态

已读取并审计以下必读文件：

- `worlds/jojo/curated/README.md`
- `worlds/jojo/curated/curation-notes.md`
- `worlds/jojo/curated/characters-index.json`
- `worlds/kaguya-sama/curated/README.md`
- `worlds/kaguya-sama/curated/curation-notes.md`
- `worlds/kaguya-sama/curated/characters-index.json`
- `worlds/kekkaishi/curated/README.md`
- `worlds/kekkaishi/curated/curation-notes.md`
- `worlds/kekkaishi/curated/characters-index.json`

为判断缺口，另参考：

- `worlds/jojo/curated/world.json`
- `worlds/jojo/curated/knowledge-graph.json`
- `worlds/jojo/curated/relationship-graph.json`
- `worlds/kaguya-sama/curated/world.json`
- `worlds/kaguya-sama/curated/knowledge-graph.json`
- `worlds/kaguya-sama/curated/relationship-graph.json`
- `worlds/kekkaishi/curated/world.json`
- `worlds/kekkaishi/curated/knowledge-graph.json`
- `worlds/kekkaishi/curated/relationship-graph.json`

未运行 JSON schema 校验；本报告只做内容完整度审计，不修正文档。
