# Fresh Smoke Test 1 证据记录（SM-01《雪中悍刀行》）

> Stage 7 B12/T717 Smoke 1。FULL_SCAN / light / normal，preferences=null（Generic Mode）。此前从未测试过的新书（过拟合检验）。
> 环境：Host = opencode CLI（macOS）· Model = deepseek-v4-flash-free · Web Search = websearch（真实联网）· Browser/Page = webfetch · Date = 2026-08-12

## 请求与环境

- Request：排雷《雪中悍刀行》
- Parsed：base_mode=FULL_SCAN / spoiler_level=light / detail_level=normal / preferences=null（Generic Mode）
- 效率：queries_used=5 组 / pages_opened=1 成功（纵横官方百科大页，截断后提取关键字段）+ 0 失败 / key_sources_used=13 / unknown_dimensions=1（repetitive-patterns）

## Identity Resolution

- 候选：唯一（书名独特，无同名小说候选；同名电视剧/游戏/同人对象 LOT 过滤）
- 身份置信度：**HIGH**——纵横中文网官方百科 page"玄侠类小说/作者烽火戏诸侯/已完结" + 维基百科（陈政华，2012-06 纵横连载，六卷 461.5 万字，江苏文艺出版社 2013-09 实体书）+ 金石堂台版 20 册（2021）+ 百度百科一致。
- 注：readnovel/czg8 等转载站"连载中/更新 2018"为滞后馆藏数据（LOT 噪音），完结事实以纵横官方为准。

## Evidence Ledger（精选重要证据）

| ID | dimension | claim_type | 来源 | tier | 日期 | access | G | supports | 摘要 |
|---|---|---|---|---|---|---|---|---|---|
| S1-E01 | identity / serialization | FACT | 纵横中文网官方百科（雪中悍刀行 189169） | A | 实时 | page | G1 | SUPPORT | 玄侠类、作者烽火戏诸侯、连载于纵横中文网、"已完结"；2013 江苏文艺出版社实体书 |
| S1-E02 | identity | FACT | 维基百科·雪中悍刀行 | B | 2020-10-27 | snippet | G1 | SUPPORT | 陈政华（烽火戏诸侯），2012-06 纵横首载、六卷共 461.5 万字；实体书 2013-09；武侠/玄幻混搭 |
| S1-E03 | romance-structure | FACT（角色盘点） | 腾讯新闻：徐凤年六个老婆，剧版只剩姜泥 | C | 2022-01-08 | snippet | G2 | SUPPORT | 原著徐凤年有六位正式妻子+侍妾：姜泥（北凉王妃/西楚女帝）、陆丞燕（正妃，八抬大轿）、南宫仆射、王初冬（侧妃）、裴南苇（外室，胭脂郡金屋藏娇）、红薯（生女小地瓜）；剧版删减只剩姜泥 |
| S1-E04 | romance-structure | FACT（角色盘点） | 智德知识库：徐凤年结局和哪些女子在一起了 | C/D | 2026-04-29 | snippet | G2 | SUPPORT | 小说结尾徐凤年有六个女人（姜泥、南宫仆射、陆成燕、王初冬、红薯、裴南苇）；徐骁死；王初冬/陆丞燕随隐居；姜泥“归还”情节 |
| S1-E05 | romance-structure | COMMUNITY_EVALUATION | 腾讯新闻：15 个女人都爱男主 | C | 2021-12-08 | snippet | G2 | SUPPORT | 喜欢徐凤年的女人不下 15 个；女主=姜泥“在正文最后嫁给徐凤年”；红颜各自结局（南宫仆射共同隐居等） |
| S1-E06 | romance-structure | COMMUNITY_EVALUATION | 豆瓣书评：未完待续（雪中悍刀行 13） | C | 2022-02-09 | page 记录 | G2 | SUPPORT | 读者亲历吐槽：“前面确定娶的那些王妃什么的北凉王不做了，王妃也不管了么”“红颜知己到老后徐凤年一个个过来看”——多段婚姻事实佐证 |
| S1-E07 | ending-reception | INTERPRETIVE | 光明网【中国网络小说好看榜】年度混搭系玄幻（付双祺） | B | 2017-01-18 | snippet | G3 | SUPPORT(正面)+REFUTE(负面) | “江湖小说里规模第一”“唯一一本可以读第二遍的网文”，但“写到后期崩得一塌糊涂”“作者功力不足以支撑如此恢宏题材”——同源正负并存 |
| S1-E08 | ending-reception | COMMUNITY_EVALUATION | 百度百科·雪中悍刀行 | B | 词条现版 | snippet | G3 | SUPPORT(正面) | 结局以“小二上酒”呼应开篇，成为经典符号；诗化语言与“以术入道”武学设定广受推崇 |
| S1-E09 | ending-reception | COMMUNITY_EVALUATION | 红袖读书 ask：雪中悍刀行算烂尾 | D | 2025-02-05 | snippet | G3 | REFUTE(负面线索) | 站点内 SEO 问答形态（按先例 D 类仅线索）：场景雕琢有余但情节不连贯、最后十几章无病呻吟、天上仙人/庙堂皇帝结局交代不清、“大结局非常赶落” |
| S1-E10 | filler / slow-burn | COMMUNITY_EVALUATION | 豆瓣书评：雪中悍刀行1：西北有雏凤 | C | 2018-07-17 | snippet | G3 | REFUTE | 1 星书评：无关剧情描写泛滥、华丽辞藻堆砌、枯燥冗长的无趣内容水了一页又一页、松散找不到核心 |
| S1-E11 | filler / slow-burn | COMMUNITY_EVALUATION | uhelp：如何评价烽火的雪中悍刀行 | C | 2022-09 | snippet | G3 | REFUTE | 有时候挺啰嗦、两三章没有主角写风土人情；人物多/情节大/刻画深/文笔妙，但中后期乏力、头重脚轻、连贯性不好 |
| S1-E12 | plot-logic / ending | COMMUNITY_EVALUATION | 豆瓣书评：未完待续 | C | 2022-02-09 | snippet | G3 | REFUTE | “凉莽大战几句话就赢了？”高潮仓促；三位陆地神仙一人站两人就没了；气场/气运设定模糊——“不会写大场面” |
| S1-E13 | system-intensity | FACT | 纵横官方百科 + 全书书评覆盖 | A/C | 实时 | page/snippet | G1/G3 | SUPPORT | 全链路无任何“系统/面板/任务流”讨论（唯一“系统”命中为同人小说对象，LOT）；金手指=家世/武学/气运（“以术入道”） |
| S1-E14 | protagonist-iq / decisiveness | COMMUNITY_EVALUATION | 百度百科 + 光明网 | B | — | snippet | G1/G3 | SUPPORT | “以智谋为刃、杀伐决断、走一步算百步”（百度百科徐凤年词条）；“要权贵就揍死一帮权贵…天下第一”（光明网）——主角塑造正面，无降智成规模指控 |
| S1-E15 | power-system-consistency | FACT | 维基百科·雪中悍刀行 | B | — | snippet | G1 | SUPPORT | 境界体系（金刚/指玄/天象/陆地神仙，一品四境）被百科/读者普遍使用；无“战力崩坏”成规模讨论（战力吐槽集中在剧版打戏，LOT） |
| S1-E16 | ntr | FACT | 专向检索（NTR/绿/牛头人/背叛） | — | — | search-result | G5 | SUPPORT | 零“感情背叛/被绿”指控；闽南网“背叛者”指剧情层间谍/叛变设定（绿蚁/黄瓜间谍、陈芝豹叛变），非感情 NTR；18mh 色情同人页 LOT 剔除 |
| S1-E17 | worldbuilding-scale | INTERPRETIVE | 光明网 + 湖北长江教育报刊传媒集团读书札记 | B | 2017 | snippet | G3 | SUPPORT | “网文江湖小说里规模第一”“庙堂+江湖+国战三位一体”“时间跨度、空间广度、人物故事纷繁复杂程度达到新高度”“完整的世界观、活着的世界” |
| S1-E18 | ending-reception | COMMUNITY_EVALUATION | 湖北长江教育报刊传媒集团读书札记 | B | — | snippet | G3 | SUPPORT(正面) | 构架宏伟、气场十足、文笔优美、角色鲜活；“虽有合理性、连贯性、结局等方面的些许不足，但瑕不掩瑜”“堪称华语网络文学扛鼎之作” |

## Dimension Results

| dimension | value | confidence | agreement | 判定链 |
|---|---|---|---|---|
| identity | 雪中悍刀行/烽火戏诸侯（陈政华）/纵横中文网/玄侠 | HIGH | — | S1-E01~E02/维基/金石堂/百度百科多源一致，Tier A 官方页 |
| serialization-status | completed（2012-06 连载~完结；实体书 2013-09；网络版约 1008 章含番外、六卷 461.5 万字） | CONFIRMED | CONSISTENT | E01（Tier A page"已完结"）+ E02 实体书 + E03 时代背景；转载站"连载中"为滞后馆藏数据 LOT |
| romance-structure | **harem 倾向（H1 边界，证据较弱）**：多个来源摘要与一篇豆瓣 page 均描述复数婚姻/伴侣关系 | **WEAK** | INSUFFICIENT | S1-E03~E06 在台账中均归 G2，同一 independence group；只有 E06 为 page。不能把“多条记录”误当多个独立来源，故降为 WEAK/INSUFFICIENT。 |
| harem（派生） | 倾向后宫（H1 边界，证据较弱） | **WEAK** | INSUFFICIENT | 派生自 romance-structure，不得高于基础 claim。 |
| ntr | none | WEAK | INSUFFICIENT | E16 专向检索零"感情背叛"指控；间谍/叛变剧情设定不构成 NTR（TX §3.4）；按"未发现"措辞输出 |
| system-intensity | none（金手指=家世/武学/气运，"以术入道"，无系统面板） | WEAK | INSUFFICIENT | E13 全链路无系统讨论（同人书的"系统"设定 LOT），否定性判断 |
| saintliness | none（无圣母指控；"纨绔皮囊+杀伐"为主） | WEAK | INSUFFICIENT | 搜索覆盖无指控；剧版"圣母化"吐槽对象是电视剧改编（LOT） |
| protagonist-iq | strong（"以智谋为刃/走一步算百步"，无降智成规模指控） | WEAK | INSUFFICIENT | E14；光明网"正奇相合" + 看片网"原著比剧版智谋更多" |
| decisiveness | high（杀伐决断/敢打敢当） | WEAK | INSUFFICIENT | E14 间接描述为主 |
| morality-tone | gray（纨绔伪装+悲天悯人底色并存） | WEAK | INSUFFICIENT | "江湖正邪不分、庙堂忠奸难辨"（光明网/长江读书札记） |
| protagonist-abuse | none（开局纨绔铺垫→成长，无虐主指控） | WEAK | INSUFFICIENT | 搜索覆盖无"虐主/憋屈"讨论 |
| slow-burn | medium（前期江湖铺垫+章节常有"多个无主角章节"） | WEAK | INSUFFICIENT | E10/E11（"两三章没有主角""剧情时不时慢下来甚至停滞"）；慢热≠水文 |
| filler | medium（文字密度/掉书袋批评，非篇幅级共识） | WEAK | INSUFFICIENT | E10/E11（"无趣内容水了一页又一页""挺啰嗦"）；禁"长=水"（461.5 万字不直接定罪），批评集中于风格密度 |
| repetitive-patterns | unknown | UNKNOWN | INSUFFICIENT | 无套路重复专文或高频讨论 |
| plot-logic | inconsistent（后期结构松散/大场面收束仓促/连贯性批评） | WEAK | INSUFFICIENT | E07（B 类"后期崩得一塌糊涂"）+ E11（"头重脚轻/连贯性不好"）+ E12（"凉莽大战几句话"）；弱证据×3 独立，无权威确认 |
| worldbuilding-scale | very-large（线索） | **WEAK** | INSUFFICIENT | E17/E08 均为 snippet，且台账同归 G3；缺 page anchor 与独立性支撑。 |
| power-system-consistency | normal（金刚/指玄/天象/陆地神仙体系被普遍认可） | WEAK | INSUFFICIENT | E15；零星"一人站两人"式吐槽不足以判 inconsistent |
| romance-level | medium（感情线为重要副线，非主线核心；主线=江湖+家国） | WEAK | INSUFFICIENT | E05（"15 个女人"自媒体口径）+ 大白话"感情细腻贯穿全文"（长江读书札记）；弱证据 |
| ending-reception | **mixed（正负口径线索）** | **WEAK** | INSUFFICIENT | S1-E07~E12 的结局相关记录均未形成两个独立 page 级阵营（多数为 snippet，且台账同归 G3）；不能据此宣称社区评价 LIKELY/DIVIDED。保留 mixed 线索，confidence=WEAK。 |

## 冲突与处理

1. **感情结构术语口径（post-optimization 修正）**：S1-E03~E06 虽有多条记录，但台账均归 G2，同一 independence group；只有 E06 为 page。不能把“条目数量”当独立来源数量，因此当前只保留 `harem 倾向（H1 边界）+ WEAK + INSUFFICIENT`。若要恢复 LIKELY，需要至少再打开一个真正独立的直接关系来源。
2. **结局评价对象分离（post-optimization 修正）**：剧版烂尾讨论继续 LOT；原著正负口径目前主要来自 snippet 且同组，故只能 `mixed + WEAK + INSUFFICIENT`，不再宣称 LIKELY/DIVIDED。
3. **同人/AI 污染**：QQ 阅读百科两页均为"挂着雪中名字的同人书"AI 百科（《诸天：从庆余年明家庶子开始》《综武：木剑游侠客》），整条 LOT 剔除（对象混同 + AI 生成双重身份）；18mh 色情同人页 LOT。
4. **页面失败/大页**：纵横官方百科 65KB 大页 fetch 截断（产出/成本比一般，同 Case A OBS 先例），提取关键字段（作者/类型/状态/简介）足够，未再重抓。

## Verdict

- 身份正确：PASS（HIGH，唯一候选；剧版/游戏/同人 LOT 干净）
- 用户显式问题（FULL_SCAN 排雷）：核心 CORE 覆盖（身份/状态/感情结构/后宫/NTR/系统/虐主/慢热/水文/结局/世界观/战力），repetitive-patterns 诚实 UNKNOWN
- 关键验证点（post-optimization）：identity 与状态仍有官方 page 支撑；harem/ending 因独立性与 page anchor 不足已主动降为 WEAK；D 类 AI/SEO 剔除、转载站状态 LOT、大页降级规则保持。该 Smoke 仍验证“不会硬猜”，但不再作为强社区结论基线。
- **PASS**（pending T712 层人工复核：yaml SM-01 manual_ground_truth 由 CHECKPOINT-7 前人工确认，本台账提供复核素材）

## Unknown 与限制

- repetitive-patterns=unknown（诚实标注）；saintliness/protagonist-abuse/romance-level 等多项基于"搜索覆盖下的否定性"限 WEAK
- 无 Tier A 完结日期精确口径（纵横官方页未给具体日期，不写具体完结日期——不编造）