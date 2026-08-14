# Case G 证据记录 — 《斗破苍穹》（RW-07）

> Stage 7 Real E2E 证据开发记录。仅保留来源元数据、短摘要、分类结果与证据关系，不复制正文。
> 本 case 核心验证点：FIT_CHECK + hard_no（TEST FIXTURE）——①Evidence → Dimension → Preference → Recommendation 链路；②hard_no=harem 若 CONFIRMED 是否封顶"不推荐"（不被 like=large-worldbuilding 平均掉）；③偏好是否污染 Evidence Confidence（证据门槛与偏好无关）；④报告冲突区（hard_no 命中项）前置。
> 2026-08-12 会话真实 websearch + webfetch 执行生成。

## 请求与环境

- Request: 按这份偏好看看《斗破苍穹》适不适合我
- base_mode: FIT_CHECK / spoiler_level: light / detail_level: normal
- 偏好（TEST FIXTURE，仅本次评估用，不写回任何用户配置）: hard_no=[harem] / strong_dislike=[heavy-protagonist-abuse] / dislike=[heavy-system] / like=[large-worldbuilding]
- 访问时间: 2026-08-12
- 效率: queries_used = 5 组（G1 身份 / G2 后宫 / G3 虐主 / G4 世界观·系统 / G5 结局·平衡）+ 1 次复核补强查询（完结日期验证）= 6 次调用 / pages_opened = 5 成功（百度百科 page、搜狐 page、中国作家网 page、虎扑 page、豆瓣书评列表 page）+ 3 失败降级（起点官方页 fetch 空回、今日头条 fetch 空回、维基百科 transport error，均保持 snippet 不升级）/ key_sources_used = 14（+QQ 阅读·起点官方资源镜像页：身份/完结状态复核佐证）/ unknown_dimensions = 2（filler、plot-logic——FIT_CHECK 范围外弱证据，诚实标注不硬猜）

## Identity Resolution

- 候选唯一且主流：天蚕土豆（本名李虎，1989-12-28 生于四川，浙江省网络作家协会副主席，起点白金作家）《斗破苍穹》，起点中文网玄幻·异世大陆，2009-04-14 开始连载，2011-07-20 完结，533.23 万字 / 共 1681 章（起点官方资源镜像页"目录已完结共1681章"）；起点第一部点击量破亿作品、"废柴流"代表作。
- 身份置信度：**HIGH**（起点官方作者页/作品页 snippet "完本·533.23万字" + 百度百科 page + 维基百科 snippet + 中国作家网 page 多方一致；无同名小说候选）。
- 对象过滤：同名动画（2017）/ 电视剧（2018，吴磊）/ 漫画 / 游戏 / 1000+ 部同人小说的讨论全程 LOT 剔除，仅锚定原著小说。知乎"口碑崩塌/烂尾"帖（2021-08-23）与 17173 吐槽（2025-09-19）均为**动画**话题，LOT 剔除；起点 ask"萧炎最后娶了几个老婆"（D 类站内问答）仅作线索。

## Evidence Ledger（精选重要证据）

| ID | dimension | claim_type | source_title | source_url | tier | date | access | indep | supports | summary（自有概括） |
|---|---|---|---|---|---|---|---|---|---|---|
| E-G01 | identity / serialization | FACT | 起点中文网·天蚕土豆作者页/《斗破苍穹》作品页 | qidian.com/book/1209977/（作者 my.qidian.com/author/1019021/） | A | 访问日；fetch 空回 | snippet | G1 | SUPPORT | 起点官方：斗破苍穹=天蚕土豆，玄幻·异世大陆，**完本**，533.23 万字；正文 2009-04-14 连载 ~ 2011-07-20 完结（起点官方资源镜像页 xzxt.bookresource.qq.com/book/1209977/ 佐证"已完结·共1681章"，2019-01-16 更新为《斗帝之路》手游角色传记番外） |
| E-G02 | identity / serialization | FACT | 百度百科·斗破苍穹 | baike.baidu.com/item/斗破苍穹/54134 | B | 词条现有 | **page** | G2 | SUPPORT | 2009-04-14 起点连载、2011-07-20 完结；起点第一部点击破亿；主要角色萧炎、**萧薰儿（"萧炎的两位妻子之一"）**、**彩鳞（"萧炎的两位妻子之一"）**；小医仙/云韵/纳兰嫣然/紫妍/雅妃=“萧炎的红颜知己之一”；构建炼药师体系、异火榜、天鼎榜等设定 |
| E-G03 | identity / romance-structure | FACT（角色档案） | 维基百科·斗破苍穹 | zh.wikipedia.org/wiki/斗破苍穹 | B | 词条现有 | snippet（fetch 失败） | G3 | SUPPORT | 2009-04-14 ~ 2011-07-20 连载于起点；**薰儿：萧炎的青梅竹马、古族大小姐，与萧炎生有一子名萧霖**；**彩鳞（美杜莎女王）：蛇人族女王，因萧炎融合异火后遗症发生关系，与萧炎生有一女名萧潇**；小医仙/云韵=“萧炎的红颜知己之一”/“有过一段感情”（云韵未成婚） |
| E-G04 | identity / author | FACT | 中国作家网·《斗破苍穹》：无法复制的玄幻经典之作（橘子） | chinawriter.com.cn/n1/2020/0113/c425784-31546527.html | A（官方文学媒体） | 2020-01-13 | **page** | G4 | SUPPORT | 天蚕土豆=李虎，1989-12-28 四川，浙江省网络作家协会副主席，起点白金作家；评析：废柴流代表作（开场三年冷落/退婚为铺垫）；“作者更是创设了完整的世界体系”；“前期主角升级过慢”；人物（尤其女性角色）塑造模板化、服务于主角形象 |
| E-G05 | romance-structure / harem | FACT + COMMUNITY | 搜狐·《斗破苍穹》：萧炎的“后宫团”有多炸裂 | sohu.com/a/903407061_568249 | C（自媒体盘点） | 2025-06-11 | **page** | G5 | SUPPORT | 盘点标题用“后宫团/三位正宫女主”，但正文事实：萧薰儿（古族千金，正文与萧炎双修共晋斗帝）、云韵（“与萧炎暗生情愫但未能走到一起，**可惜的是萧炎没把云韵也娶回家**”）、美杜莎（怀孕生女萧潇、激活血脉进化九彩吞天蟒）——正式成婚者实为萧薰儿+美杜莎；“后宫团”系自媒体盘点式称法，非正式结构定性 |
| E-G06 | romance-structure / harem | FACT + COMMUNITY | 今日头条（Messon财知道）：萧炎到底有几个老婆？ | toutiao.com/article/7479633891855270415/ | C | 2025-03-13 | snippet（fetch 空回） | G6 | SUPPORT | “萧炎最终共有两位正式的妻子：萧薰儿和美杜莎女王（彩鳞）……多位红颜知己如云韵、雅妃、小医仙、紫妍等，但并未与她们正式结为夫妻” |
| E-G07 | romance-structure / harem | COMMUNITY_EVALUATION | 腾讯新闻·山治看动漫：官方魔改剧情，后宫变纯爱 | news.qq.com/rain/a/20250612A0716I00 | C | 2025-06-12 | snippet | G7 | SUPPORT | 该文讨论动画改编，但明确指称原著：“斗破苍穹本来就是后宫剧情，因为萧炎拥有两位老婆，美杜莎女王和萧薰儿，还有几个红颜知己（云韵、小医仙、纳兰嫣然、青鳞、紫妍等）”——社区直接使用“后宫”标签指称原著的口径证据 |
| E-G08 | romance-structure | COMMUNITY（电视剧资讯） | 闽南网：小说女主都有谁萧炎有几个老婆 | m.mnw.cn/tv/guonei/1729885.html | C/D | 2017-06-02 | snippet | G8 | SUPPORT | “最后结局萧炎带着几位老婆破空而去进入大主宰世界”——泛称“几位老婆”的后宫化口径（娱乐媒体） |
| E-G09 | harem（AI 口径） | COMMUNITY（AI SEO，线索） | 起点官方 ask：萧炎最后娶了几个老婆 | qidian.com/ask/qkghvtulwyc | D | 2024-06-25 | snippet | G9 | CONTEXT | “萧炎最后娶了两个老婆，分别是萧薰儿（古薰儿）和彩鳞（美杜莎女王）……2 位妻子 4 位红颜知己”——站内 AI SEO 问答形态（Case A/B/C/F 先例），与独立来源一致但定级 Tier D 仅线索，不作独立证据 |
| E-G10 | protagonist-abuse | COMMUNITY_EVALUATION | 中国作家网·类型评价与文本评析 | 见 E-G04 | A | 2020 | page | G4 | CONTEXT | 开场“家族冷落，旁人轻视，被未婚妻退婚……种种打击接踵而至”属废柴流先抑后扬铺垫；“男主很忙……回击总想害他的刁民”“主角平静应对和用实力打脸”=爽文结构；全篇无“虐主”指控 |
| E-G11 | protagonist-abuse | COMMUNITY_EVALUATION | 腾讯新闻·剑客说火影：冰皇海波东的一生有多爽 | news.qq.com/rain/a/20250810A05LQ800 | C | 2025-08-10 | snippet | G10 | CONTEXT | “37 岁成就斗帝的萧炎，在成帝的道路上虽然一直是爽文模式，但其也受到了不少的磨难”——“受磨难”被表述为爽文模式的正常挫折，非长期虐主 |
| E-G12 | system-intensity / worldbuilding | FACT | 笔灵小说·斗破苍穹标准大纲（B站同源） | ibiling.cn/novel-navigation/detail/967（B站 opus/636654220821397526 同文） | D（同源合并） | 2022~2024 | snippet | G11 | SUPPORT（世界观）/ REFUTE（重系统） | 金手指=药老+焚决（进化功法，吞噬异火升级）→ **无系统面板/任务奖励流**；“世界设定：斗气大陆，远古八族鼎立（古/魂/炎/药/石/灵/雷/萧），加玛帝国→中州→大千世界”；全篇无“系统”机制描述 |
| E-G13 | ending-reception | COMMUNITY_EVALUATION（正面方） | 虎扑网络文学区：斗破苍穹小说结局我认为很完美 | bbs.hupu.com/637225252.html | C | 2026-01-30 | **page** | G12 | SUPPORT（正面） | 楼主（注“来源：转载”）称结局“极具分量的圆满句号”：废柴→斗帝逆袭闭环；与萧薰儿爱情修成正果家庭美满；斗气世界升华。0 回复单方帖子，作正面方观点记录不升共识 |
| E-G14 | ending-reception / plot-logic | COMMUNITY_EVALUATION（负面方） | 豆瓣·斗破苍穹全部书评（110 条） | m.douban.com/book/subject/22933018/reviews | C | 2015~2021 | **page** | G13 | REFUTE（“整体烂/战力崩”方）/ SUPPORT（“爽文/励志”方） | 两极并现：负面（chnjames 2017“苦笑一族？这书真的很烂”；豆友 2016“典型的小白文…垃圾”；火烧眉毛 2016“主角光环太强、越级杀敌”；棣棠 2018“前后实力割裂/后期剧情重复”；紫芝 2015“把女人当高级附属品/男权思想”）；正面或辩护（徐衡 2019“斗破在网文中将玄幻写到极致”；等 2021“文学角度确实烂，但它就是一部定位明确的爽文”；宁家桑桑 2017“幼稚但对中小学生足够”）——“读者评价毁誉不一”（法老 2021 原话） |
| E-G15 | ending-reception（负面方线索） | COMMUNITY（搜索标题线索） | B站 视频：烂尾真相：一代神作为何沦为战力崩坏教科书 | search.bilibili.com（视频标题，未打开） | D | 现有 | search-result | G14 | REFUTE（线索） | 标题级线索：存在“烂尾/战力崩坏”盘点视频（未打开，仅 search-result 引导，不升证据） |
| E-G16 | worldbuilding | COMMUNITY_EVALUATION | 87HE/大熊猫文学等转载站简介 | xiaoshuo.87he.com/doupocangqiong | D | 访问日 | snippet | G15 | SUPPORT（线索） | 转载站简介：斗气世界、九个等级、异火/功法/魂殿设定、从萧家到云岚宗到中州——世界观设定广度描述（D 类仅线索，配合 E04/E12 使用） |

## Dimension Results

| dimension | value | confidence | agreement | 判定链 |
|---|---|---|---|---|
| identity | 天蚕土豆（李虎）《斗破苍穹》；起点中文网玄幻·异世大陆；2009-04-14 连载、2011-07-20 完结；533.23 万字 | HIGH | — | E01（A snippet）+ E02（B page）+ E03（B snippet）+ E04（A page）多源一致；无同名小说候选；动画/剧/同人 LOT |
| serialization-status | **completed**（2011-07-20） | CONFIRMED | CONSISTENT | E01（起点“完本”）+ E02（B page 精确日期）+ E03（B snippet）一致 |
| romance-structure | **harem（H1 明确后宫）**：结局明确两位正式妻子（萧薰儿=生一子萧霖、彩鳞/美杜莎=生一女萧潇）；云韵/小医仙/纳兰嫣然/紫妍/雅妃为未娶的红颜知己 | **CONFIRMED** | CONSISTENT | 事实面多独立来源一致且具体：E02（B page“两位妻子之一”×2）+ E03（B snippet 生子/生女）+ E05（C page 云韵未娶+美杜莎怀孕）+ E06（C snippet“两位正式的妻子”）+ E07（C snippet“本来就后宫剧情”）+ E08（C snippet“几位老婆”）；无任何“单女主/官方一妻”对冲口径 → 按 taxonomy H1 正例 1（结局与两位女性成婚、正文明确两段婚姻关系、各有子女）判明确后宫，confidence 依据 source-policy §10.4“多个真正独立可靠来源一致而具体且无实质冲突”→ 未因偏好抬高标准也未降低 |
| harem（派生） | **harem = 明确后宫（H1）**（taxonomy §12：H1→harem） | CONFIRMED | CONSISTENT | 由 romance-structure 派生；自媒体（E07）直接称“本来就是后宫剧情”；无 DISPUTED（不存在“单女主”等对冲口径） |
| protagonist-abuse | **none**（开场三年退婚/冷落=废柴流先抑后扬铺垫；全篇为爽文模式，无社区“虐主”指控） | WEAK | CONSISTENT（间接） | E10（A page 评析为铺垫+爽文结构）+ E11（C snippet“爽文模式但受到不少磨难”）+ E14（豆瓣整体无虐主指控）——无正面直接断言，多为间接 → 保守 WEAK |
| system-intensity | **none**（金手指=药老+焚决+异火，无系统面板/任务奖励流） | WEAK | CONSISTENT（间接） | E12（D 大纲无系统）+ E02 设定描述（无系统词）+ E04 评析（支线目标为“升级目标”非系统任务）——金手指非系统的 taxonomy 判定成立，直接断言少 → WEAK |
| worldbuilding-scale | **large**（斗气大陆：加玛帝国→中州→远古八族/魂殿等多势力；异火榜/丹药/等级体系；结局延伸大千世界） | LIKELY | CONSISTENT | E04（A page“完整的世界体系”）+ E12（D 八族/多地图）+ E02（B page 体系设定）+ E03（B snippet 跨世界）；规模判定保守取 large（未读全文核实是否 very-large） |
| ending-reception | **mixed**（正面“圆满逆袭闭环” vs 负面“烂尾/战力崩/小白文”） | LIKELY | DIVIDED | 正面方 E13（C page 虎扑，单方转载）与辩护方（E14 内“爽文定位”）；负面方 E14（豆瓣多篇：烂/无逻辑/战力崩/后期重复）+ E15（search-result 线索）——两极成立；豆瓣书评多为整体评价，结局专项争议以“部分人认为圆满/部分人认为烂尾”呈现；单帖不升共识、禁多数投票 |
| filler / plot-logic（FIT_CHECK 范围外弱证据） | unknown | UNKNOWN | INSUFFICIENT | 仅豆瓣零散批评（E14：“废话太多”“后期剧情重复”“前后实力割裂”），独立来源不足、非本 case 偏好命中的核心维度 → 诚实 UNKNOWN，不硬猜 |

## 冲突与处理

1. **harem 判定（本 case 核心）**：按 playbook §11.2 顺序——同书确认（全部来源均指原著，动画/剧/同人 LOT）→ 日期（2015~2026 来源横跨十年口径稳定）→ 版本（小说 vs 动画：E07 明确区分“原著本来就是后宫剧情”对照动画魔改）→ 术语定义（自媒体盘点“后宫团/三位正宫”为盘点式称法，正文事实为两位正式妻子+云韵未娶——盘点与事实不冲突；无“单女主”对冲口径）→ 独立来源（E02/E03 两百科 + E05 page + E06~E08 社区 = 6+ 个独立环境）→ 更直接证据（生子/生女/大婚细节）。结论：**无实质冲突**，romance-structure=harem（H1），CONFIRMED / CONSISTENT。禁多数投票原则未触发（非投票问题，独立来源全部一致）。
2. **ending-reception（DIVIDED）**：正面方（E13 虎扑“结局圆满”，注：标注“来源：转载”的单帖，按单方观点处理不升共识）vs 负面方（E14 豆瓣多篇“烂/战力崩/后期重复”+ E15 B站盘点标题）→ mixed + LIKELY + DIVIDED，双方结构性论据并列输出，不选边、不把“烂尾”当客观事实。
3. **动画/剧集/同人污染**：【知乎第四季吐槽】【17173 动画吐槽】【腾讯动漫魔改文】讨论对象为动画/剧，全部 LOT 剔除；E07 仅取其“原著本来就是后宫剧情”的原著层断言（该句指称原著）；起点 ask（E09）D 类仅线索不升级。
4. **页面失败降级**：起点官方页（fetch 空回）、今日头条（fetch 空回）、维基百科（transport error）→ 三条均保持 snippet，未冒充 page；身份与感情结构结论由 page 级来源（百度百科/搜狐/中国作家网/虎扑/豆瓣）交叉成立，未依赖降级源。
5. **偏好不污染证据（专项核验）**：harem=CONFIRMED 的判定链完全由独立来源事实构成（E02/E03/E05~E08），与 TEST FIXTURE 的 hard_no=harem **无关**（判定在偏好匹配之前完成；偏好只影响 P1 优先级把 harem 提前调查，未改变任何 confidence/agreement）。strong_dislike/dislike 同理未参与证据定级。
6. **spoiler 隔离（light）**：输出仅结构级结论（两位妻子、结局评价两极方向），不输出具体结局事件（萧霖/萧潇为角色档案事实可结构级提及，避免具体反转细节）。

## 复核记录（2026-08-12 写回会话，Source Integrity 抽查）

- E-G04 中国作家网 page：真实打开 ✓——身份（李虎/1989-12-28 四川/浙江省网络作家协会副主席/起点白金作家/2009-04 创作）、"完整的世界体系"、"前期升级过慢"、女性塑造模板化等摘要逐句吻合
- E-G05 搜狐 page：真实打开 ✓——2025-06-11 自媒体盘点：薰儿（双修共晋斗帝）、云韵（"可惜萧炎没把云韵也娶回家"）、美杜莎（怀孕生女萧潇/进化九彩吞天蟒）全部吻合
- E-G13 虎扑 page：真实打开 ✓——2026-01-30 单帖 0 回复、正文"来源：转载"标注属实；摘要（逆袭闭环/薰儿修成正果/世界观升华）吻合
- E-G14 豆瓣书评列表 page：真实打开 ✓——110 条书评存在；E14 引用各篇（2016 小白文垃圾/2017 苦笑一族烂/2018 前后实力割裂后期剧情重复/2019 玄幻写到极致/2021 毁誉不一/2021 定位明确爽文）逐条吻合
- E-G02 百度百科 page：复核时 403（anti-bot，历代先例）——词条关键断言（2009-04-14 连载/2011-07-20 完结/533.23 万字）由搜索引擎索引词条内容 + QQ 阅读起点官方镜像 + 豆瓣铁粉更新帖（"09年4月14日开始上传2011年7月20日完结，历时827天，总字数5328025字"）独立交叉验证成立；"两位妻子"事实由搜狐 page（本次实开）覆盖
- E-G03 维基百科 snippet / E-G01 起点官方页 snippet：复核时 transport error / 空回，与当时失败记录一致 → 保持 snippet 标注，未冒充 page ✓
- **修正 2 处 MINOR 事实**：① 身份段"约 1620 章"→ 官方镜像"共 1681 章"；② E-G01 番外更新时间"2018"→"2019-01-16"。均不影响任何维度判定与置信度（身份/完结状态多源一致不变）
- 补强查询 1 次（websearch 完结日期验证）计入 queries_used；QQ 阅读起点官方镜像页（bookresource.qq.com，起点官方资源域名）计入 key_sources

## Verdict

- 身份正确：PASS（HIGH，唯一候选无歧义）
- 核心验证点 1（**Evidence → Dimension → Preference → Recommendation 链路**）：搜索→Ledger→合成→harem（H1，CONFIRMED）→ 偏好匹配 → 建议=不推荐，链路完整 ✓
- 核心验证点 2（**hard_no=CONFIRMED 封顶不推荐**）：harem=CONFIRMED 命中 hard_no → 按 preference-guide §4.1 + report-format §6 硬雷封顶（规则层），建议**不得高于“不推荐”**，不被 like=large-worldbuilding 命中平均掉 ✓（FIT_CHECK 报告“冲突区”前置）
- 核心验证点 3（**偏好不污染 Evidence Confidence**）：证据判定先于偏好匹配且独立完成；置信度按 source-policy 标准给出，无因偏好上调/下调 ✓（见冲突 5）
- 核心验证点 4（**冲突区前置**）：report-format §4 必展示项中 hard_no 命中项置于报告最前 ✓
- 核心验证点 5（**TEST FIXTURE 不写回**）：偏好仅来自 real-world-cases.yaml 的 preferences 字段，未写入 config/ 任何文件 ✓
- 来源真实：全部 URL 真实（5 次 page 实开核验 + snippet/search-result 如实标注；起点 ask 降级 D 类未冒充证据；B站标题明确 search-result）✓
- 效率：5 组查询 / 5 成功页（+3 受控失败），符合 FIT_CHECK 预算 4~6 q / 4~6 p；第 5 组后来源开始循环（豆瓣/虎扑/转载站重复）即停，diminishing returns 生效 ✓
- **PASS**（pending T712 人工复核）；记录 0 个规则问题（详见 REAL-WORLD-EVALUATION.md Case G 段）