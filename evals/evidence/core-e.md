# Case E 证据记录 — 《幽冥仙途》（RW-05）

> Stage 7 Real E2E 证据开发记录。仅保留来源元数据、短摘要、分类结果与证据关系，不复制正文。
> 本 case 核心验证点：冷门/资料稀缺书的诚实降级——查不到时标 UNKNOWN/WEAK；snippet 不得冒充 page；diminishing returns 停止逻辑。
> 2026-08-12 会话真实 websearch + webfetch 执行生成。

## 请求与环境

- Request: 排雷《幽冥仙途》
- base_mode: FULL_SCAN / spoiler_level: light / detail_level: normal
- 偏好: 无（Generic Mode）
- 访问时间: 2026-08-12
- 效率: queries_used = 4 组（4 次调用）/ pages_opened = 3 成功 + 1 失败（百度百科 403 降级 snippet）/ key_sources_used = 14 / unknown_dimensions = 2

## Identity Resolution

- 搜索结果一致指向：作者 减肥专家（张宁，山东菏泽人，纵横中文网签约作家）；实体书 台湾鲜鲜文化事业有限公司 2007-09 出版（豆瓣条目元数据"时间 2007 / 鲜鲜文化事业有限公司"，百度百科同）；网络版 约 2010-10-28 前后完本（优书网数据页），2022 年前后平台精改全集（微信读书"作者亲自精改全集终版"、百度百科"2022年4月网文版完结"口径）。
- 身份置信度：**HIGH**（书名+作者唯一候选；中国作家网官方访谈 page + 豆瓣条目 + 百度百科/搜狗百科/微信读书多源一致）。
- **yaml 假设修正**：case 描述"2008 年首发"→ 真实证据为 **2007-09 台湾鲜鲜文化实体书首发**；网络连载晚于实体出版（作者自述当时"作品一直是在台湾出版"）。身份解析纠正了日期假设。
- 范围说明：无同名动画/游戏/影视对象污染；转载站（华为小说/第三中文网等）显示"连载中"为数据混乱噪音（Tier D），与完结事实冲突按 LOT 处理。

## Evidence Ledger（精选重要证据）

| ID | dimension | claim_type | source_title | source_url | tier | date | access | indep | supports | summary（自有概括） |
|---|---|---|---|---|---|---|---|---|---|---|
| E-E01 | identity / protagonist-abuse / morality-tone / serialization | FACT + INTERVIEW | 中国作家网：我想写一些无懈可击的作品——减肥专家访谈录 | chinawriter.com.cn/n1/2017/1001/c405057-29570861.html | A | 2015-08-30 访谈（2017-10-01 发布） | page | G1 | SUPPORT | 作者本人：写作《幽冥仙途》时"写到主角特别憋屈的那段情节之后风格就走偏了"；"我也想写得不那么虐，但是主角在这本书里已经有一定的行为逻辑了"；"这个主角本身为人不是太好"；《幽冥仙途》在台湾出版；写结尾时"写得很痛苦"；"我的读者群比较小众……看完我的书有 5000 人左右"；"一直被夸着，一边被骂着"；作品刻意不按爽点节奏写 |
| E-E02 | identity / serialization-status / worldbuilding | FACT | 百度百科·幽冥仙途 | baike.baidu.com/item/幽冥仙途/9119415 | B | 词条现有（页面 403） | snippet | G2 | SUPPORT | 减肥专家创作、融合修真与武侠；2007-09 台湾鲜鲜文化出版；"2022年4月网文版完结，总字数165.15万字"（该条采集口径存疑，记录不深究）；人间界/通玄界/仙界三界+三十三宗门+宇内七妖；主角李珣、与水蝶兰建立情感羁绊；结局与青吟飞升计划的终局对决 |
| E-E03 | identity | FACT | 搜狗百科·幽冥仙途 | baike.sogou.com/v261052.htm | B | 词条现有 | snippet | G3 | SUPPORT | 2007 年鲜鲜文化出版；主角李珣意外加入幽魂噬影宗门卷入诡秘任务 |
| E-E04 | identity / serialization-status | FACT | 微信读书·减肥专家作者页/作品页 | weread.qq.com/web/search/books?author=减肥专家 | B | 访问日 | snippet | G4 | SUPPORT | 减肥专家=张宁、纵横中文网签约作家；《幽冥仙途（全集终结版）》"作者亲自精改全集终版"、推荐值 73.4%——冷门受众佐证 |
| E-E05 | identity / ending-reception | FACT + COMMUNITY | 豆瓣条目页《幽冥仙途》 | book.douban.com/subject/2354896/ | C | 2007 | snippet | G5 | SUPPORT | 条目元数据：2007/鲜鲜文化/160 台币；379 条短评、30 篇书评；书评标题池含多篇结局/暗黑主题（"论结局和钟老板""本土暗黑仙侠扛鼎之作"等） |
| E-E06 | romance-structure / protagonist-abuse / worldbuilding-scale | COMMUNITY_EVALUATION | 豆瓣书评：本土暗黑仙侠类作品中的扛鼎之作 | book.douban.com/review/6671957/ | C | 2014-05-17 | snippet | G6 | SUPPORT | "暗黑风格……黑暗程度比《诛仙》更甚"；"没有意淫种马，没有主角光环，主人公从开篇伊始就在正与邪的夹缝中苦苦挣扎"；"构架出了一个恢宏庞大，宗派、人物、法宝众多……的仙侠世界"；“对主人公的塑造……阴险毒辣、两面三刀、城府深沉、工于心计" |
| E-E07 | power-system-consistency / plot-logic / ending-reception | COMMUNITY_EVALUATION | 豆瓣书评：幽冥仙途（李寻幽 2022） | book.douban.com/review/14312542/ | C | 2022-04-01 | snippet | G7 | REFUTE | 缺点："后期忽高忽低的战力""作者对战斗场景描写水平不足……偏偏战斗占据的篇幅又大""外挂太大。天冥珠……正常来说根本不会出现在设定严谨的小说里""古音这个boss太怪" |
| E-E08 | ending-reception | COMMUNITY_EVALUATION | 豆瓣书评：幽冥仙途简评 | book.douban.com/review/6725788/ | C | 2014-07-04 | snippet | G8 | SUPPORT | "最喜欢的是结尾……全篇暗黑之间终见一点温情。也很喜欢李珣最后发出的对钟隐的挑战"——结局正面评价 |
| E-E09 | slow-burn | COMMUNITY_EVALUATION | 豆瓣书评：来往幽冥，寻觅自我的旅途 | book.douban.com/review/5537901/ | C | 2012-08-08 | snippet | G9 | SUPPORT | "叙事节奏与传统的网络小说的快节奏相去甚远……需要静下心来，慢慢细看的书"——节奏偏慢线索 |
| E-E10 | romance-structure / protagonist-abuse / identity | INTERVIEW（作者原话） | 豆瓣小组帖：《幽冥仙途》完全透（2007 鲜鲜书友会访谈录） | m.douban.com/group/topic/6565032/ | A（作者层） | 2007-09-16 | page | G10 | SUPPORT | 作者原话（鲜鲜书友会）："后宫PK？哪有这种规模，一个有个性的，不脸谱化的女性，又有谁会喜欢当后宫？"；"主角并不好色，他只是功利"；主角"活的很惨……后面就更惨"；"第二部H场面也加了很多……为了更易于写主角阴谋的爆炸力"；"明玑是光，主角是黑暗"；"黑暗面……想让主角明白，想得到什么，就要付出点儿代价"——非后宫 + 虐主 + 成人向内容多重作者级佐证 |
| E-E11 | protagonist-abuse / plot-logic | COMMUNITY_EVALUATION | 豆瓣书评：由《幽冥仙途》想到的（归梦隐 2018） | book.douban.com/review/9588186/ | C | 2018-08-13 | snippet | G11 | SUPPORT(虐主)/REFUTE(逻辑) | "作者将主角打进了人类伦理的绝境……绝大部分篇幅主角都在算计和被算计中度过，百年人生都在苦苦挣扎"；"确实也很少有网文作者会这样虐待主角"；"小说后半部分则陷入情节展开后因驾驭能力不足所产生的自相矛盾里" |
| E-E12 | romance-structure | COMMUNITY_EVALUATION（调侃体，谨慎） | 豆瓣书评：少食多滋味（本来老六） | book.douban.com/review/2077415/ | C | 2009-06-16 | snippet | G12 | CONTEXT | 以清单调侃式盘点主角女性关系（"妻：宇内七妖水蝶兰；妾：阴散人、秦婉如……奸：……暧昧：……"），结论"很黄很暴力"——复数性关系存在线索，但为调侃体盘点，不作为后宫结构性证据 |
| E-E13 | decisiveness / protagonist-iq | COMMUNITY_EVALUATION | 水木社区 NetNovel 精华区书评 | newsmth.net/bbsanc.php?path=...NetNovel...M.1290170828.X0 | C | 约 2010 | snippet | G13 | SUPPORT | 深度长评："李珣……算计了一遍又一遍，但是行为极其被动"；"虐主情节"对比罗森；"和小白文相比，《幽冥》非常晦涩和深奥"；文中"古音被NTR""妖凤被玉散人NTR"属《无极》桥段映射的喻用表述，非对主角的 NTR 指控 |
| E-E14 | ending-reception | COMMUNITY_EVALUATION | 百度知道：幽冥仙途结局 水蝶兰…… | zhidao.baidu.com/question/223238598.html | C | 2011-02-08 | snippet | G14 | SUPPORT | 读者：结局"算是大完满"；主角"留世三千年"等水蝶兰重生——结局正面社区回声（2011 年网络版已完本佐证） |
| E-E15 | ending-reception | COMMUNITY_EVALUATION | blackbzy 博客：【读后感】幽冥仙途 | blackbzy.com/posts/book-youmingxiantu/ | D | 2026-06-20 | snippet | G15 | REFUTE | 个人博客（D 类线索）："最后的决战阶段……后续的剧情也是匆匆过完，最后仅仅留了一个要找钟影复仇的开放式结局"——结局仓促/开放式批评（单一 D 类来源，不作独立升级） |
| E-E16 | identity / serialization-status / ending-reception / filler | FACT + COMMUNITY | 优书网《幽冥仙途》数据页 | youshu.me/book/1193 | C | 页面"最后更新 2010-10-28"；书评 2025~2026 | page | G16 | SUPPORT + REFUTE | page 级：已完结 / 178.8 万字 / 7.7 分（2107 人评，52% 五星 vs 14% 一星）；最新书评两极（2026-02"绝对的仙草……没有什么特别水的地方，伏笔很多……该填的坑基本都填了" vs 2025-11"古早之雷，慎选"、2025-12"垃圾书"、2025-12"剧情过于枯燥，没有爽感……令我感到不适"、2025-06"主角恶心，世界观模糊……文笔好"） |
| E-E17 | plot-logic | COMMUNITY_EVALUATION | 豆瓣书评：重读第5遍（zhaoliang） | book.douban.com/review/7126432/ | C | 2014-10-12 | snippet | G17 | CONTEXT | 剧情复盘向："一个比较大的漏洞就是最后的决战"——决战分兵无人察觉的漏洞批评（单源弱证据） |
| E-E18 | identity / serialization | FACT | Bangumi 收录《幽冥仙途》 | bgm.tv/subject/536112 | C | 访问日 | snippet | G18 | SUPPORT | "27卷，完"；短评池："大后期不停描写战斗我才有点审美疲劳"（负面）/ "剧情结构扎实，伏笔埋得深……最后两章真是爽的批爆……大爱蝴蝶"（正面结局）/ "恢弘世界观下狭小叙事" |
| E-E19 | romance-structure | COMMUNITY_EVALUATION（AI 低质） | 百度知道：幽冥仙途李珣有几个女人 | zhidao.baidu.com/question/1874235459752255867.html | D | 2025-06-12 | snippet | G19 | CONTEXT | "与三个女性角色有着深厚情感联系：青吟、明璇、玉散人"——角色名错误（明璇=明玑误写、玉散人非女性），判定为低质/AI 内容，仅记存在"三个女性"说法的线索，不采用为证据 |
| E-E20 | serialization-status | FACT（转载噪音） | 华为小说/第三中文网/海马文学等转载站 | 多个 | D | 2024-2024 | snippet | G20 | CONTEXT | 多个转载站显示"连载中/65 章/最新 2024-06"等互相矛盾数据（华为小说 65 章、第三中文网 118 万字与百科 165 万字矛盾）——馆藏数据混乱，LOT 列为噪音；海马文学"第二部第十九集尘埃落定终章"与完结事实吻合 |
| E-E21 | ending-reception | COMMUNITY（AI 张冠李戴） | 妖气游戏网：幽冥仙途各个人物结局 | m.17u1u.com/zonghe/daquan/2753512.html | D | 无精确日 | snippet | G21 | LOT 剔除 | 内容出现"主角冷轩""恋人羽婧月"等与本书无关人物——明显 AI 生成/张冠李戴，整条剔除，绝不引用 |

## Dimension Results

| dimension | value | confidence | agreement | 判定链 |
|---|---|---|---|---|
| identity | 幽冥仙途/减肥专家（张宁）/台湾鲜鲜文化 2007-09 实体书首发，纵横中文网系网络作者，网络版约 2010-10-28 完本、2022 精改全集 | HIGH | — | E01（Tier A 官方访谈 page）+ E02~E05 多源一致；无同名候选；yaml"2008 年首发"假设被证据修正为 2007-09 实体书首发 |
| serialization-status | completed（实体书 2007~2010 年间分卷完本；网络版完本口径 2010-10-28/2022） | LIKELY | CONSISTENT | E16（page 级"已完结"）+ E02/E04/E18（"全集终结版"/"27卷完"）+ E14（2011 年看完全本的提问）一致；转载站"连载中"（E20）为 Tier D 数据噪音 LOT；无官方页 page 级直接证据（百度百科 403），故 LIKELY 不升 CONFIRMED |
| romance-structure | multiple-ambiguous（复数关系线索存在；作者明确否认“后宫规模”） | **WEAK** | DISPUTED | 非后宫侧有 E10 作者 page；复数关系/结局关系侧主要为 E06/E12/E02/E14 snippet。按 Page Anchor，DISPUTED 一侧缺 page 锚点 → confidence 上限 WEAK；保留 multiple-ambiguous 作为当前最谨慎分类。 |
| protagonist-abuse | heavy（类型 mixed：生存/心理/伦理持续压制，部分读者因此不适） | CONFIRMED | CONSISTENT | E01（Tier A 作者自述"我也想写得不那么虐""主角特别憋屈"）+ E10（作者自述"活的很惨"）+ E11（"虐待主角"）+ E06（"夹缝中苦苦挣扎"）+ E16（"生存欲"令部分读者不适）→ 作者亲证 + 多独立读者来源一致且具体；非"先抑后扬"，全程压抑基调（E06/E12 佐证） |
| filler | low | WEAK | INSUFFICIENT | 反证：(E16 2026-02 书评"没有什么特别水的地方。伏笔很多……该填的坑基本都填了"、E18"剧情结构扎实"）；弱批评：（E07"战斗占据的篇幅又大，阅读体验反而不如前期"、E18"大后期不停描写战斗我才有点审美疲劳"）→ 无"水文"共识，长评多称紧凑（"恨此书太短"散见 E-E05 书评池），不判水 |
| worldbuilding-scale | large | LIKELY | CONSISTENT | E02（B 类三界+三十三宗门+宇内七妖结构化）+ E06（"恢宏庞大、宗派人物法宝众多"）+ E18（"恢弘世界观"）+ E16 负面书评也承认"似乎想写宏大世界"（但批评叙事聚焦小众人，属规模≠质量边界）→ 规模大，叙事为群像聚焦式；不升 very-large |
| power-system-consistency | inconsistent | WEAK | INSUFFICIENT | E07（"后期忽高忽低的战力""妖凤杀真人境跟屠狗一样"）+ E11（"后半部分……自相矛盾"）+ E16（"世界观模糊……文笔好"）→ 2+ 独立批评但有具体论据者少（多为 snippet），不升级 |
| plot-logic | inconsistent | WEAK | INSUFFICIENT | E07（"古音这个boss太怪""天冥珠这种东西根本不该出现在设定严谨的小说"）+ E11（"驾驭能力不足产生的自相矛盾"）+ E17（决战漏洞单源批评）→ 弱证据×3 独立，无权威确认 |
| system-intensity | none | WEAK | INSUFFICIENT | 2007 年作品，搜索覆盖内无"系统/面板/任务流"讨论；全部简介与书评无系统元素（E02/E06/E16）→ 描述性一致但非专查 |
| saintliness | none（反向：主角被多方描述为阴险功利） | WEAK | INSUFFICIENT | 无任何圣母指控；E01（"主角本身为人不是太好"）+ E16（"卖师求荣卑鄙下流的主角形象"）等反向塑造多源 |
| protagonist-iq | strong（线索倾向） | **WEAK** | CONSISTENT | E06/E13/E02 均为 snippet；虽然多来源方向一致，但缺 page anchor，按现行规则不得升 LIKELY。 |
| decisiveness | low | WEAK | INSUFFICIENT | E13（"但是行为极其被动"）+ E11（"绝大部分篇幅……在算计和被算计中度过""直到最后几章也在他人算中"）→ 被动受控型主角线索 2 独立源，但判定依赖单一深度书评，不升级 |
| slow-burn | medium | WEAK | INSUFFICIENT | E09（"节奏与传统网文快节奏相去甚远""需要静下心来慢慢细看"）+ E16（"剧情推进没什么趣味性"暗示前段展开慢）→ 直接线索 1~2 条，无"慢热"专文 |
| ending-reception | mixed（正负口径均存在） | **WEAK** | DIVIDED | 支持方有 E16 page + E08/E14/E18 snippet；批评方主要是 E15/E07 等 snippet，E16 的负面条目更多针对整体阅读体验而非结局专项。DIVIDED 关键负面侧缺独立 page 锚点 → confidence 上限 WEAK。 |
| ntr | unknown | UNKNOWN | INSUFFICIENT | 无对主角的 NTR 指控；E13 中"古音被NTR/妖凤被NTR"为《无极》桥段映射的喻用表述（对象非主角），不构成 NTR 证据；未专向检索，诚实标 UNKNOWN |
| repetitive-patterns | unknown | UNKNOWN | INSUFFICIENT | 搜索覆盖无套路重复专文或高频讨论 |
| romance-level | medium | WEAK | INSUFFICIENT | 感情线非主线（E10"主角只是功利"，情感多为工具），但结局水蝶兰线贯穿且重要（E02/E14/E18"大爱蝴蝶"）→ 中期副线定位，证据分散 |
| morality-tone（辅助） | dark | LIKELY | CONSISTENT | E01（作者"李珣是错的""画风比较阴暗"）+ E06（"暗黑风格……更甚"）+ E10（"厚黑学"）+ E16（"卑鄙下流"）→ 多独立来源一致，"暗黑仙侠"代表作口径 |

## 冲突与处理

1. **serialization-status 噪音 vs 事实**：华为小说/第三中文网等转载站标"连载中"（65 章/118 万字/更新时间 2024 等互相矛盾），与"已完结"事实冲突 → 按 playbook §11.2 顺序：同书确认 → 日期（转载站元数据为重新入库时间）→ 版本（实体书/网络版/精改版三版并存）→ 判定 E20 为馆藏数据噪音 LOT；完结事实由 E16（page）+ E02/E04/E18/E14 多独立来源支撑。**结论：completed + LIKELY**（无 Tier A 官方页成功打开，不升 CONFIRMED——冷门书诚实限权）。
2. **romance-structure 口径冲突（本 case 关键）**：作者层（E10"后宫PK？哪有这种规模"）与部分读者（E06"没有意淫种马"）明确"非后宫"；2009 调侃体盘点（E12）列举复数妻妾式关系；百度知道 AI 答案（E19）说"三个女性角色"但角色名错乱。→ 事实层面：复数情感/性关系存在；结构层面：无多伴侣同堂、"最终主线=水蝶兰"（E02/E14）。按 taxonomy：multiple-ambiguous + DISPUTED，不投票、不写 harem。
3. **少量有力证据 vs 大量弱证据的冷门特征**：本书豆瓣 30 篇书评、优书 1048 篇书评（表面很多）但大多为老书评（2009~2014）或转贴；高质量独立"近期讨论"少，2025~2026 新书评多集中在优书网页面（部分内容农场/AI）。处理：不做数量堆积≠共识；两派各取结构性论据（爱者：77 分/仙草书评/老粉丝重读；恶者：评论区两极/古早雷）。符合 Case E 测试目标：不因资料松动而降级标准，也不因资料少而胡猜。
4. **页面失败降级**：百度百科 403 → E02/E03 保持 snippet 级；各转载站正文页（新笔趣阁等 LOT）绝不引用正文内容（合规：Ledger 只有元数据与短摘要）。妖气游戏网"各人物结局"（E21）内容张冠李戴（出现无关人名）→ 判定 AI 生成，整条剔除。

## Verdict

- 身份正确：PASS（HIGH；并修正 yaml"2008 年首发"假设为 2007-09 台湾实体书首发）
- 核心验证点：**冷门书诚实降级成立**——unknown_dimensions=2（ntr、repetitive-patterns），且 serialization-status 因无官方页仅给 LIKELY、filler 因证据不足判 low+WEAK，均为"查不到不硬猜"的合规表达；未出现"没查到 = 应该没有"式输出
- snippet/page 区分：中国作家网访谈（page）、鲜鲜书友会帖（page）、优书网数据页（page）为骨干结论来源；百科/AI 答案（snippet）未升级
- diminishing returns：4 组查询后出现相同来源重复（优书/豆瓣两站循环）即停止，未过度搜索
- **PASS**（pending T712 人工复核）；记录 1 个 OBS + 1 个 MINOR（见 REAL-WORLD-EVALUATION.md Case E 段）