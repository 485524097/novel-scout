# Case C 证据记录 — 《庆余年》（RW-03）

> Stage 7 Real E2E 证据开发记录。仅保留来源元数据、短摘要、分类结果与证据关系，不复制正文。

## 请求与环境

- Request: 排雷《庆余年》
- base_mode: FULL_SCAN / spoiler_level: light / detail_level: normal
- 偏好: 无（Generic Mode）
- 访问时间: 2026-08-12
- 效率: queries_used = 6 组 / pages_opened = 3 成功（起点官方镜像、豆瓣长书评、BookLink 短评页）+ 4 次失败降级（百度百科 403 / 知乎问题 403 / 贴吧 403 / 知乎专栏 403，均保持 snippet）/ key_sources_used = 9 / unknown_dimensions = 1（filler）

## Identity Resolution

- 搜索结果一致指向：作者 猫腻（谢晓峰）；首发平台 起点中文网（2007-05 连载）；分类 历史·架空历史；总字数 395.91 万（833 章）；状态 已完结（约 2009 年初，2009-02 前后）。
- 身份置信度：**HIGH**（起点官方作品页 Tier A 页面级 + 中国作家网文艺报文章 + 快懂百科 三方一致；无同名歧义作品出现）。
- 范围说明：本 case 排雷对象为 2007 年首发原著《庆余年》396 万字本。起点作者页另有 2024 年衍生作《庆余年第三季》（189.7 万字，IP 时代官方衍生创作），不作为排雷主体，仅存档防混淆。电视剧（2019/2024）相关讨论大量存在，一律 LOT 剔除，仅保留剧中"感情线弱化"作为改编对照信息。

## Evidence Ledger（精选重要证据）

| ID | dimension | claim_type | source_title | source_url | tier | date | access | indep | supports | summary（自有概括） |
|---|---|---|---|---|---|---|---|---|---|---|
| C-E01 | identity / serialization-status | FACT | 《庆余年》官方作品页（起点图书镜像） | gsws.bookresource.qq.com/book/114559/ | A | 访问日 | page | G1 | SUPPORT | 官方页：作者猫腻、已完结、历史·架空历史、395.91万字、共833章；简介"积善之家必有余庆" |
| C-E02 | identity | FACT | 猫腻小说《庆余年》：重生文的意义与谨慎的理想主义（中国作家网/文艺报） | chinawriter.com.cn/bk/2014-07-14/76918.html | B | 2014-07-14 | snippet(全文级) | G2 | SUPPORT | 官方文学机构文章：2007年5月起于起点连载、猫腻第三部作品、青架空历史、七卷完本、约390万字 |
| C-E03 | identity / completion | FACT | 《庆余年》快懂百科词条 | baike.com/wikiid/8854131705716092715 | C | 访问日 | snippet | G3 | SUPPORT | 2007-05 连载、2009-02 完结、395.88万字；2020 国家图书馆典藏；人民文学出版社出版 |
| C-E04 | romance-structure（官方口径） | FACT | 林婉儿（百度百科，小说第一女主角词条） | baike.baidu.com/item/林婉儿/24219469 | B | 访问日 | snippet（403 降级） | G4 | SUPPORT(single口径) | "猫腻创作的权谋小说《庆余年》第一女主角……最终成为范闲的正室夫人"——官方百科口径：林婉儿为唯一正妻/第一女主 |
| C-E05 | romance-structure（正文事实） | FACT | 豆瓣长书评：《庆余年》书看完了随便写点 | book.douban.com/review/15138417/ | C | 2023-04-30 | page | G5 | SUPPORT(多伴侣事实) | 读者自述阅读体验时直述范闲"娇妻美妾""有妻妾子女"，确认正文存在妻+妾格局（非纯单女主） |
| C-E06 | romance-structure（社区口径） | COMMUNITY_EVALUATION | 知乎问题：庆余年小说中范闲有五个老婆，为什么电视剧里范闲唯一的老婆只有一个…… | zhihu.com/question/364359081 | C | 2020-01 前后 | snippet（403 降级） | G6 | REFUTE(single口径) | 知乎用户普遍以"五个老婆"称原著感情结构，并以"剧版仅林婉儿"作对照提问——社区术语口径与官方口径直接冲突 |
| C-E07 | romance-structure（媒体盘点） | COMMUNITY_EVALUATION | 《庆余年》原著小说范闲有多少妻子（闽南网，转自古宫历史网） | mnw.cn/dsj/2924271.html | C | 2024-06-04 | snippet | G7 | SUPPORT(多伴侣事实) | 盘点"原著范闲确实共有五个老婆"：林婉儿正妻、柳思思侧室生下女儿、战豆豆女帝为其生女、司理理侧室、海棠朵朵未生子；结局与林婉儿、柳思思隐居 |
| C-E08 | romance-structure（媒体盘点） | COMMUNITY_EVALUATION | 范闲5个老婆3个孩子结局如何？（网易号） | 163.com/dy/article/J37JBUJS0515QRNA.html | C | 2024-05-27 | snippet | G7 | SUPPORT(多伴侣事实) | 独立自媒体同模式盘点：林婉儿生范良、柳思思生范淑宁、战豆豆生红豆饭；司理理入北齐宫为名义皇后；海棠朵朵远赴西胡无子——3 个孩子来自 3 位不同女性 |
| C-E09 | romance-structure（读者感悟） | COMMUNITY_EVALUATION | 《庆余年》读后感（hdh765 收集稿） | hdh765.com/qingyunianxiaoshuoguanhougan | D | 访问日 | snippet | G8 | SUPPORT(多伴侣事实) | 读者感悟原文直述"这是个男性的穿越小说，却裹着言情的感情戏，做着三妻四妾的事实""男主的西门庆属性又裹着糖衣"，并称"这些花花故事的描写并不多" |
| C-E10 | ntr | FACT | 《庆余年》NTR/绿帽 专向检索 | （G4 查询整组） | — | 2026-08-12 | search-result | — | SUPPORT(none) | "庆余年 NTR/绿帽/感情背叛"检索无任何针对原著的"被绿/背叛"指控；命中仅为无关注册页、电视剧宣传与同人站，均与 NTR 定义无关 |
| C-E11 | ending-reception（负面） | COMMUNITY_EVALUATION | 贴吧：庆余年结局被指烂尾，配角比主角更出彩 | tieba.baidu.com/p/7275732676 | C | 访问日 | snippet（403 降级） | G9 | REFUTE(负面) | 贴吧帖：质疑内库/鉴查院/东夷城等资源线"折腾一大圈最后干嘛用了？只是用来保护这些人自己？"；认为结局收束乏力 |
| C-E12 | ending-reception（负面） | COMMUNITY_EVALUATION | 知乎专栏：《庆余年》书评 | zhuanlan.zhihu.com/p/702361782 | C | 2024 | snippet（403 降级） | G10 | REFUTE(负面) | 读者"越靠近尾声越觉得不适"，认为结尾体验不佳（"看什么年代的小说就用那个年代的心态评价"为护辩） |
| C-E13 | ending-reception（负面） | COMMUNITY_EVALUATION | 起点官方问答：庆余年小说烂尾 知乎 | qidian.com/ask/qmizfdynjsk | A(D) | 2024-07-17 | snippet | G11 | REFUTE(负面) | 官方 ask 页（站点内 SEO 问答形态，按先例定级 D 类仅线索）：引述"有读者认为烂尾——庆帝收尾乏力、范闲主角光环过重、决一死战与神庙之行不知所云"。只作负面线索，不作结论依据 |
| C-E14 | ending-reception（正面） | COMMUNITY_EVALUATION | 得到APP《庆余年》评分与书评 | dedao.cn/ebook/reviews?id=N5lDqb9b47pXZxGn1kBzPlMyQArYv0qvdmLWqe85E2aVKdo9jNgOLRmDJ6nXLm16 | C | 2024 前后 | snippet(全文级) | G12 | SUPPORT(正面) | 评分 4.6/1124 评；书评多数 5 星（"很不错的书""经典之作，每年再看一遍""小说比电视剧有意思"），含 1 星差评（"垃圾食品…又臭又长"） |
| C-E15 | ending-reception（正面） | COMMUNITY_EVALUATION | 豆瓣：《庆余年》书看完了随便写点（同 C-E05） | book.douban.com/review/15138417/ | C | 2023-04-30 | page | G5 | SUPPORT(正面) | 同一读者 5 星好评："彻头彻尾的悲剧…看似美好退隐的结局实际上却是如此残忍"——悲怆结局但认可，属"结局有感而发但正面"派 |
| C-E16 | ending-reception（正面） | COMMUNITY_EVALUATION | BookLink《庆余年》短评页 | booklink.me/comment-1-114559-gugugugu.html | C | 2014~2024 | page | G13 | SUPPORT(正面) | 约 12 条短评：6~7 星为主（"猫腻最好的书""装逼流的典范""計謀一環扣一環""好看""仙草"），1 条 ★★★★★ 差评（-14 同意） |
| C-E17 | plot-logic（正） | COMMUNITY_EVALUATION | 官方简介/出版社宣传（起点作品页 C-E01） | gsws.bookresource.qq.com/book/114559/ | A | 访问日 | page | G1 | SUPPORT(正面) | 官方简介定位"谋局布篇功力非凡、故事环环相扣"；南方都市报推广文称"构架如一盘妙棋" |
| C-E18 | plot-logic（负） | COMMUNITY_EVALUATION | 《庆余年》读后感（同 C-E09）+ 得到 1 星书评 | hdh765.com / dedao.cn | D/C | 2024 | snippet | G8/G12 | REFUTE(负面) | 读后感"抄红楼抄得挺生硬""武侠描述现实又干竭"，且"以为三个主角……你读明白就知道写的是谁"；得到 1 星"生搬硬造，文笔拙劣" |
| C-E19 | slow-burn | COMMUNITY_EVALUATION | 豆瓣《庆余年·壹》书评列表 | book.douban.com/subject/3155622/reviews | C | 2009-03 起 | snippet | G14 | SUPPORT | 首批书评"入题太慢，千篇一律的穿越情节实（在无聊）"——前期节奏负面线索 |
| C-E20 | protagonist-iq / decisiveness | COMMUNITY_EVALUATION | 豆瓣长书评（同 C-E05）+ BookLink 短评 | douban.com / booklink.me | C | 2014~2023 | page | G5/G13 | SUPPORT | "杀伐决断、手段狠辣、极端护短、利己主义"（C-E05）；"智谋一环扣一环""装逼流"（C-E16）；孤立负面（起点 ask 引"范闲天真幼稚且主角光环过重"） |
| C-E21 | worldbuilding-scale | FACT | 川观新闻转南方都市报：《庆余年》十四卷出版推广 | cbgc.scol.com.cn/news/5034581 | B/C | 2024-05-26 | snippet | G15 | SUPPORT | 正规媒体报道：操权谋+科幻背景（核爆后新文明/神庙即 AI），"小说四百万字，设定宏大，任务繁多"；人民文学出版社十四卷全本出版 |
| C-E22 | identity / 剧版对照 | FACT | 剧版感情线弱化的媒体表述（同 C-E21） | cbgc.scol.com.cn/news/5034581 | B/C | 2024-05-26 | snippet | G15 | CONTEXT | "剧中为迎合大众口味弱化了范闲的诸多红颜知己的感情线……原著中关系可就精彩复杂得多（如精简掉的柳思思）"——改编对照确认原著感情线远多于剧版 |

## Dimension Results

| dimension | value | confidence | agreement | 判定链 |
|---|---|---|---|---|
| identity | 庆余年/猫腻/起点 | HIGH | — | C-E01~E03 三方一致，Tier A 官方页 |
| serialization-status | completed（约 2009 初完结，395.91 万字） | CONFIRMED | CONSISTENT | C-E01（Tier A 官方页"已完结"）+ C-E02/E03 → DIMENSION STOP |
| romance-structure | **multiple-ambiguous**（正文存在多伴侣事实线索；官方/百科以林婉儿为“第一女主角/正室夫人”口径） | **WEAK** | **DISPUTED** | 多伴侣事实侧有 C-E05 page + 多个 snippet；“唯一第一女主/正室”对冲侧 C-E04 仅 snippet。按 Page Anchor，DISPUTED 两侧若要 confidence ≥ LIKELY 都需 page 锚点，因此当前降为 WEAK/DISPUTED；仍禁止多数投票。 |
| harem（派生） | H1/H2 边界（明确妾室与多女生子事实，无警后同堂结局结构；官方口径单女主） | WEAK | DISPUTED | 派生自 romance-structure；不得直判 harem（TX §3.3：H1 需"结局明确多伴侣"），亦不得以官方口径断言 single 无争议 |
| ntr | none | WEAK | INSUFFICIENT | C-E10：专向检索无任何原著"被绿/背叛"指控；关键字命中仅为同人/他作。按"未发现"措辞输出，不作绝对断言 |
| system-intensity | none | WEAK | INSUFFICIENT | 全链路无任何"系统/面板"设定与讨论（历史权谋+武侠九品体系）；基于搜索覆盖的否定性判断 |
| saintliness | none | WEAK | INSUFFICIENT | 无圣母指控；读者描述相反（杀伐决断、护短、利己，C-E05/C-E20） |
| protagonist-iq | strong | LIKELY | CONSISTENT | C-E17/E20；孤立负面（起点 ask 引"幼稚/光环重"）不构成成规模降智指控 |
| decisiveness | high | LIKELY | CONSISTENT | C-E05/C-E20"杀伐决断、护短、睚眦必报"多来源一致 |
| morality-tone | gray | **WEAK** | INSUFFICIENT | 主要直接依据来自 C-E05 单一 page；其他相关描述未形成独立 page 锚点。描述性标签保留，但按单一 Tier C page 上限降为 WEAK。 |
| protagonist-abuse | none | WEAK | INSUFFICIENT | 无虐主讨论；全书为权谋爽文结构 |
| slow-burn | medium | WEAK | INSUFFICIENT | 仅 C-E19 等零星"入题太慢"线索；无成规模"慢热"标签 |
| filler | unknown | UNKNOWN | INSUFFICIENT | 负面主要集中于"篇幅长/又臭又长"（C-E14 单条 1 星）与节奏，无成规模"注水"直接指控；按 TX §5.4 禁"长=水"，诚实标 UNKNOWN |
| plot-logic | normal | WEAK | DISPUTED(轻度) | C-E17（正：谋局布篇）vs C-E18（负：抄红楼生硬/生搬硬造）+ 结局"不知所云"（E13）→ 正负并存但不足以判 inconsistent/weak；取 normal 并保留负面线索 |
| worldbuilding-scale | large（线索） | **WEAK** | INSUFFICIENT | C-E21 仅 snippet；缺 page 级直接锚点，不能因来源是正规媒体就越过 access_mode 上限。 |
| power-system-consistency | normal | WEAK | INSUFFICIENT | 武侠九品/大宗师体系，无"战力崩"成规模指控 |
| ending-reception | mixed（已观察到正负口径） | **WEAK** | DIVIDED | 正面方有 C-E15/C-E16 page；负面方 C-E11/C-E12 仅 snippet，C-E13 为 D 类线索。按 Page Anchor 规则，DIVIDED 一侧缺 page 锚点 → confidence 上限 WEAK；不把"烂尾"写成客观事实。 |

## 冲突与处理

1. **romance-structure 三方口径冲突（本 case 核心）**：检查顺序 → 同一本书？是。日期：无跨期差异。定义/术语："第一女主角/正室夫人"口径（C-E04）× 正文妻妾事实（C-E05/E07/E08）× 社区"五个老婆/三妻四妾"口径（C-E06/E09）。处理：**不投票、不选边**。多伴侣事实侧有 page 锚点，但对冲侧只有 snippet，因此当前只能输出 `multiple-ambiguous + WEAK + DISPUTED`；若要恢复 LIKELY，需打开独立的对冲侧页面核实。
2. **ending-reception 两极（C-E11~E16）**：已观察到正负两类口径，但负面侧仅 snippet，正面侧有 page。按 Page Anchor → `mixed + WEAK + DIVIDED`；不得继续沿用历史 `LIKELY`。起点官方 ask（E13）仍只作 D 类线索。
3. **同名/影视污染**：剧版（2019/2024）与小说讨论量大，剧版评分/选角/剧情讨论一律 LOT 剔除；仅保留 E22（剧版感情线弱化）作改编对照。电视剧烂尾讨论（E16 起点 ask 首条实为剧版第一季结局争议）与原著烂尾讨论严格分开。

## Verdict

- 身份正确：PASS（HIGH）
- 用户显式问题（FULL_SCAN 排雷）：已覆盖身份/状态/感情结构核心/结局/剧情逻辑等主要 CORE
- 关键 Dimension（post-optimization 重判）：romance-structure=multiple-ambiguous+WEAK+DISPUTED；ntr=none（WEAK）；ending-reception=mixed+WEAK+DIVIDED。历史 T712 人工语义核对仍保留，但 confidence 以当前 access_mode 规则为准。
- 结论待写入 REAL-WORLD-EVALUATION.md：**PASS**（pending 人工复核细节）
- 效率：queries 6 / pages 3 成功 + 4 失败降级 / key_sources 9 / unknown_dimensions 1（filler）