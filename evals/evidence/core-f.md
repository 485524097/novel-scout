# Case F 证据记录 — 《斗罗大陆》（RW-06）

> Stage 7 Real E2E 证据开发记录。仅保留来源元数据、短摘要、分类结果与证据关系，不复制正文。
> 本 case 核心验证点：SPECIFIC_RISK（单雷点"后宫吗？"）保持轻量——identity + 2~4 组查询不扩张成 FULL_SCAN；spoiler_level=none 下只输出结构级结论；strict 定义（H3 边界）vs 社区口径并存。
> 2026-08-12 会话真实 websearch + webfetch 执行生成。

## 请求与环境

- Request: 无剧透，告诉我《斗罗大陆》是后宫文吗？
- base_mode: SPECIFIC_RISK / spoiler_level: none / detail_level: normal
- 偏好: 无（Generic Mode）
- 访问时间: 2026-08-12
- 效率: queries_used = 4 组（4 次调用）/ pages_opened = 2 成功（新浪 page、腾讯新闻 page）+ 1 失败（起点官方页 fetch 空回，降级不升级）/ key_sources_used = 10 / unknown_dimensions = 0（目标字段已充分答复）

## Identity Resolution

- 候选唯一且主流：唐家三少（张威）《斗罗大陆》，起点中文网玄幻，2008-12-14 开始连载，已完结（起点作品页 299.62 万字、完本；百度百科"2010 年 8 月完结×14 卷"；维基百科表格列 2009-12-13 完结——两处精确完结日期口径不一致，非本次目标维度，记录不深挖，完结状态本身多源一致）。
- 身份置信度：**HIGH**（书名+作者唯一候选；起点作者页/作品页 snippet + 维基百科 + 百度百科 + 豆瓣多源一致；无同名小说候选；同名动画/漫画/游戏/同人对象全部 LOT 过滤）。
- 范围说明：自律过滤对象——腾讯 QQ阅读百科"后宫_斗罗：从迎娶比比东开始无敌"（同人作品 AI 页）、快看漫画 QA、起点官方 ask 页"唐三的七个老婆"（站点内 AI SEO 问答，含一条错误列"七位老婆"的 AI 回答）全部按 Tier D / LOT 处理，仅作"社区存在混乱口径"的线索，不作证据。

## Evidence Ledger（精选重要证据）

| ID | dimension | claim_type | source_title | source_url | tier | date | access | indep | supports | summary（自有概括） |
|---|---|---|---|---|---|---|---|---|---|---|
| E-F01 | identity / serialization | FACT | 起点中文网·唐家三少作者页/《斗罗大陆》作品页 | my.qidian.com/author/4921（作品 qidian.com/book/1115277） | A | 访问日；作品页 fetch 空回 | snippet | G1 | SUPPORT | 起点官方：斗罗大陆=唐家三少，玄幻，**完本**，299.62 万字；引子"穿越的唐家三少"（作者代入设定） |
| E-F02 | identity | FACT | 维基百科·唐家三少 | zh.wikipedia.org/zh-hans/唐家三少 | B | 词条现有 | snippet | G2 | SUPPORT | 唐家三少=张威，起点白金作家；《斗罗大陆》起点中文网已完结，表中完结日期列 2009-12-13 |
| E-F03 | identity | FACT | 百度百科·斗罗大陆 | baike.baidu.com/item/斗罗大陆/5313 | B | 词条现有 | snippet | G3 | SUPPORT | 2008-12-14 起点连载、2010-08 完结；14 卷；主角唐三由人修炼为神；唐家三少自述男主角以本人为原型 |
| E-F04 | identity / romance-structure（作者层） | FACT + INTERVIEW | 中国作家网：唐家三少：20年不断更，斗罗世界是自己的幻梦（吉云飞 访谈） | chinawriter.com.cn/n1/2025/1104/c404027-40596020.html | A（官方媒体/作者本人） | 2025-11-04 | snippet | G4 | SUPPORT | 作者层：唐三就是斗罗世界里的"我"（本人化身）；《斗罗大陆V重生唐三》写的是"唐三在小舞去世后为爱人殉情，带着记忆去另一个世界寻找转世的爱人，最后两人在一起"——唐三×小舞为作者设定的单一情感主线（系列口径） |
| E-F05 | romance-structure / harem | COMMUNITY_EVALUATION | 新浪·漫小志（自媒体原创）：《斗罗大陆》唐三为何不开后宫？（2021-03-20） | k.sina.cn/article_6135279929_16db0f13900100rqon.html | C | 2021-03-20 | **page** | G5 | SUPPORT（非后宫/多女仰慕） | 同时期网文"十部有九部都是后宫文，唯独《斗罗大陆》一条纯爱线走到底"；唐三不后宫原因：作者忠贞、小舞人气碾压、"有机会收后宫的两个角色胡列娜和千仞雪都是反派"、已成神后立一夫一妻标杆——多名女性角色仰慕主角但主角单线回应 |
| E-F06 | romance-structure / harem（社区边界口径） | COMMUNITY_EVALUATION（自媒体个人观点） | 腾讯新闻·云漫菌：斗一你不知道的隐秘，唐三有条件开后宫（2024-02-23） | news.qq.com/rain/a/20240223A01MZR00 | C | 2024-02-23 | **page** | G6 | REFUTE（"算不算后宫"边界）/ CONTEXT（唯一妻子） | "都知道三少是纯爱战士，即便是有再多的女配角，最终主角也只能和一个在一起"；但主张"孟依然、胡列娜和千仞雪等这些女人其实都和唐三有直接关系，甚至存在身体接触……有些地方还是写得很露骨的，那些女角色除了没有明媒正娶，其他事唐三该干的一样不少"——【单方自媒体观点，本人自称"有几分真有几分假全凭大家理解"，不构成共识；真实价值=社区"只差明媒正娶=算后宫"式口径的存在证据】 |
| E-F07 | romance-structure（角色关系） | FACT（角色档案） | 百度百科·小舞词条 | baike.baidu.com/item/小舞/3977450 | B | 词条现有 | snippet | G7 | SUPPORT | 小舞=《斗罗大陆》系列女主角；与唐三初识诺丁学院、结伴史莱克七怪；"蓝银皇/修罗鞘"等神位身份；唐三之妻（多条剧情描述含"唐三之妻"称谓及献祭/复活/神界生子事件细节——内部可见，输出按 none 隔离） |
| E-F08 | romance-structure（角色关系） | FACT（角色档案） | 萌娘百科·小舞 | zh.moegirl.org/小舞 | C | 词条现有 | snippet | G8 | SUPPORT | 小舞档案：义兄兼丈夫=唐三；史莱克七怪成员；系列人气女主（"小舞姐"） |
| E-F09 | romance-structure（角色关系） | FACT（角色档案） | 中文百科全书 newton.com.tw·唐三 | www.newton.com.tw/wiki/唐三/64680514 | B | 词条现有 | snippet | G9 | SUPPORT | 角色关系表正向列"小舞 —— 妻子 —— 唐三一生的挚爱"；史莱克其他人（宁荣荣/朱竹清等）均为"队友/好友"非伴侣 |
| E-F10 | romance-structure / harem | COMMUNITY_EVALUATION | 海峡网（媒体盘点）：斗罗大陆原著小说有多少人喜欢唐三 | www.hxnews.com/news/yl/kdsj/202102/24/1965603.shtml | C（媒体/资讯） | 2021-02-24 | snippet | G10 | SUPPORT | "不管是小说还是电视剧里，其实唐三一直只有一个老婆，那就是小舞"；"在书里喜欢唐三的女人还是很多的，只是唐三只对小舞"；"如果是后宫类小说的话，这些（女角色）应该都会进入唐三的后宫，不过唐三的心中只有小舞" |
| E-F11 | romance-structure | FACT + COMMUNITY | 腾讯新闻（资讯）：唐家媳妇不好当 | news.qq.com/rain/a/20200727A05DZ400 | C | 2020-07-27 | snippet | G11 | SUPPORT | 唐三"自然也要安排一个魂兽妻子，小舞就是"；系列历代主角配偶各一（唐三×小舞、唐舞麟×古月娜、蓝轩宇×冻千秋）——系列口径均为单配偶 |
| E-F12 | harem（AI 混乱口径） | COMMUNITY（AI SEO，剔除） | 起点官方 ask：唐三的七个老婆分别是谁 | m.qidian.com/ask/qurgtycenvx | D（AI 问答） | 2024-08 | snippet | G12 | CONTEXT（剔除） | 该站内 ask 页多数回答"唐三只有一个老婆，小舞"（配 AI 推广语），其中一条（2024-06）错误列出"七个老婆：小舞、千仞雪、胡列娜、宁荣荣、朱竹清、比比东、唐月华"→ 模板化 AI 内容（同 Case A/B/C 先例 Tier D），"七个老婆"系钓鱼标题+AI 生成的混乱口径，只记存在不采用 |
| E-F13 | harem（同人 LOT） | COMMUNITY（同人） | QQ阅读百科：后宫_斗罗：从迎娶比比东开始无敌 | book.qq.com/baike/3dyr9wrwwvtdq | D | 访问日 | snippet | G13 | CONTEXT（LOT） | 《斗罗》同人小说（主角非唐三）的"后宫"百科页——对象污染，整条 LOT 剔除 |

## Dimension Results

| dimension | value | confidence | agreement | 判定链 |
|---|---|---|---|---|
| identity | 唐家三少（张威）《斗罗大陆》；起点中文网玄幻；2008-12-14 连载、已完结（299.62 万字/14 卷；精确完结日期口径 2010-08 vs 2009-12-13 未深究） | HIGH | — | E01（A 类 snippet）+ E02/E03（B 类 snippet）+ 豆瓣（G1 检索内）多源一致；无同名候选；动画/漫画/游戏/同人 LOT 过滤 |
| romance-structure | **single**（作品围绕唯一主要恋爱对象小舞展开；多名女性角色对主角有仰慕/互动但主角单线回应） | LIKELY | **DISPUTED** | 事实面多独立来源一致：唯一妻子/女主（E07/E08/E09 角色档案 + E10/E11 媒体 + E05 page）；多女仰慕（E05 page"胡列娜/千仞雪有机会收后宫"、E06 page"孟依然/胡列娜/千仞雪有直接关系"、E10"喜欢唐三的女人还是很多"）；作者层单线（E04 访谈）→ 按 taxonomy H3 边界判 single（多女喜欢主角但主角只选一人 ≠ 后宫）。术语冲突面：E06 自媒体主张"只差明媒正娶=有条件开后宫"，E12 AI 混乱口径"七个老婆"，E05/E10 主流"纯爱一条线/唯一老婆" → 各方口径直接冲突，不投票、并存输出 |
| harem（派生） | **非后宫（H3 边界）**（严格定义：明媒正娶/正式伴侣唯一 = 小舞；多女存在仰慕与互动，未形成多伴侣关系） | WEAK | DISPUTED | 由 romance-structure 派生（taxonomy §12：H3→single）；"是否算后宫"的社区口径存在 E06 式争议 → confidence 限 WEAK，答案以"严格定义非后宫 + 部分社区口径有争议"双线呈现，禁直判"后宫" |

## 冲突与处理

1. **核心术语冲突（是否后宫，按 playbook §11.2 顺序）**：同书确认（全部来源均指唐三《斗罗大陆》小说）→ 日期（2021~2024 来源均为最近稳定口径，无版本差异）→ 版本（小说 vs 动画 vs 同人：E13 同人页 LOT；动画衍生讨论出现但未污染本判定）→ **术语定义**（"唯一明媒正娶"=strict 非后宫 vs "露骨互动只差名分"=社区泛化口径，taxonomy H3 边界成立）→ 独立来源（E05 page / E06 page / E07~E11 独立环境）→ 更直接证据（角色关系档案表 E09）。结论：**双方口径并存**，romance-structure=single（LIKELY）+ harem 派生"非后宫"（WEAK）+ agreement=DISPUTED。无多数投票。
2. **日期口径冲突（完结日期）**：百度百科 2010-08 vs 维基百科 2009-12-13 → 非目标维度，记录存疑不深挖；完结状态本身（起点"完本"+ 多源）无冲突。
3. **AI/SEO 口径剔除**：起点官方 ask（E12）"七个老婆"式答案为模板化 AI 内容（含错误角色名组合），整条仅记线索；QQ 阅读同人百科页（E13）对象污染 LOT。
4. **页面失败降级**：起点官方作品页 fetch 空回（E01 保持 snippet，身份仍由多源 snippet 交叉确认 HIGH，无必要升级为 CONFIRMED 事实层）；百度百科未尝试重复打开（前 5 case 多次 403 先例 + 现有口径已充分，diminishing returns 生效）。
5. **spoiler 隔离（none）**：研究阶段读到大量事件级信息（献祭/复活/成神/结局走向等，E07 等），输出阶段全部隔离——仅输出结构级结论（唯一恋爱对象/多女仰慕/是否后宫的类型判定），不输出任何关系事件细节与结局事件。

## Verdict

- 身份正确：PASS（HIGH，唯一候选无歧义）
- 核心验证点 1（**SPECIFIC_RISK 轻量**）：queries=4 组 / pages=2 成功+1 失败降级，仅调查 identity + romance-structure/harem，未扩张任何 FULL_SCAN 维度（未查世界观/慢热/战力/水文）→ **未失控** ✓；第 4 组后来源开始同口径循环即停，符合"够用即停"
- 核心验证点 2（**strict 定义 vs 社区口径**）：single（H3 边界）+ harem 非后宫（WEAK）+ DISPUTED 并存输出；E06"有条件开后宫"式自媒体口径被如实记录为单方观点不升共识；禁多数投票守规 ✓
- 核心验证点 3（**spoiler= none 合规**）：输出仅结构级类型判定，关系事件细节全部隔离 ✓
- 来源真实：全部 URL 真实（2 次 page 实开核验 + 其余 snippet 来自真实检索结果）；E12/E13 降级未冒充证据 ✓
- **PASS**（pending T712 人工复核）；记录 0 个规则问题（详见 REAL-WORLD-EVALUATION.md Case F 段）