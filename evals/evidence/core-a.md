# Case A 证据记录 — 《凡人修仙传》（RW-01）

> Stage 7 Real E2E 证据开发记录。仅保留来源元数据、短摘要、分类结果与证据关系，不复制正文。

## 请求与环境

- Request: 排雷《凡人修仙传》
- base_mode: FULL_SCAN / spoiler_level: light / detail_level: normal
- 偏好: 无（Generic Mode）
- 访问时间: 2026-08-12
- 效率: queries_used = 5 组 / pages_opened = 3（起点官方书页、红袖读书百科页、起点搜索页）/ key_sources_used = 7 / unknown_dimensions = 2（filler、protagonist-abuse）

## Identity Resolution

- 搜索结果一致指向：作者 忘语（本名丁凌滔，维基百科）；首发平台 起点中文网；分类 仙侠·幻想修仙；总字数 767.59 万；状态 已完结。
- 身份置信度：**HIGH**（官方作品页 + 官方问答页 + 维基百科三方一致；无同名歧义作品出现）。
- 范围说明：本名"凡人修仙传"官方含两部——凡人篇（2008-02~2013-09 连载，起点官方问答页）+ 续作《凡人修仙之仙界篇》（2019 完本，起点搜索页显示"完结"）。报告按全系列口径处理，info 截至 2026-08-12。

## Evidence Ledger（精选重要证据）

| ID | dimension | claim_type | source_title | source_url | tier | date | access | indep | supports | summary（自有概括） |
|---|---|---|---|---|---|---|---|---|---|---|
| A-E01 | identity/serialization-status | FACT | 《凡人修仙传》官方作品页（起点） | bookresource.qq.com/book/107580 | A | 访问日 | page | G1 | SUPPORT | 官方页面：作者忘语、已完结、仙侠·幻想修仙、767.59万字 |
| A-E02 | identity / completion | FACT | 忘语作品时间表（起点官方问答） | qidian.com/ask/qtupewzwzen | A | 2024-09-10 | page | G1 | SUPPORT | 官方问答页：凡人修仙传 2008-02 至 2013-09 在起点连载完结 |
| A-E03 | identity | FACT | 凡人修仙傳（中文维基百科） | zh.wikipedia.org/wiki/凡人修仙传 | B | 访问日 | snippet | G2 | SUPPORT | 忘语=丁凌滔；2008-2013 起点连载；2010 出版单行本 |
| A-E04 | serialization-status | FACT | 起点搜索页·凡人修仙传全集 | qidian.com/soushu/凡人修仙传全集.html | A | 访问日 | page | G1 | SUPPORT | 搜索页条目：忘语/仙侠/完结、767.61万字；仙界篇条目 标注完结 |
| A-E05 | romance-structure | FACT | 南宫婉（百度百科） | baike.baidu.com/item/南宫婉/7755569 | B | 访问日 | page | G3 | SUPPORT | "韩立唯一的妻子和道侣"，正式结为道侣并举行双修大典 |
| A-E06 | romance-structure | FACT | 紫灵（百度百科） | baike.baidu.com/item/紫灵 | B | 访问日 | page | G3 | REFUTE | 紫灵词条称"主角韩立的道侣/妻子"，魔陀山后"春风一度"——与 E05 存在"道侣"口径冲突 |
| A-E07 | romance-structure | COMMUNITY_EVALUATION | 网易号：南宫婉为何是第一女主 | 163.com/dy/article/K9BFOBL20552H59B.html | C | 2025-09-13 | page | G4 | SUPPORT | 南宫婉戏份少但第一女主；紫灵、元瑶被描述为"借助韩立"的暧昧/交易型关系 |
| A-E08 | ending-reception | COMMUNITY_EVALUATION | 仙界篇是否烂尾？读者评价褒贬不一（贴吧） | tieba.baidu.com/p/8578880880 | C | 访问日 | snippet | G5 | REFUTE(负面) | 贴吧帖：仙界篇刷多遍仍"稀里糊涂"，存在稀里糊涂之处 |
| A-E09 | ending-reception | COMMUNITY_EVALUATION | 《凡人修仙传》"烂尾"引热议，仙界篇成最大遗憾（贴吧） | tieba.baidu.com/p/6523420562 | C | 访问日 | snippet | G6 | REFUTE(负面) | 仙界篇被指烂尾、结局草率、灰界等坑未填 |
| A-E10 | ending-reception | COMMUNITY_EVALUATION | 仙界篇为什么评价褒贬不一？甚至被称为"烂尾"（头条） | toutiao.com/article/7449539481209782796 | C | 2024-12-18 | snippet | G7 | CONTEXT | 原灵界篇已算大结局（"欢迎道友飞升北寒仙域"），仙界篇为续写，故评价参照系不同 |
| A-E11 | ending-reception | COMMUNITY_EVALUATION | 毁童年的烂尾作（豆瓣书评） | douban.com/book/review/13062773 | C | 2020-12-17 | snippet | G8 | REFUTE(负面) | 仙界后期"草草结尾""没立框架就随心写" |
| A-E12 | ending-reception | COMMUNITY_EVALUATION | 评价凡人修仙传仙界篇（知乎专栏） | zhuanlan.zhihu.com/p/659290111 | C | 2023-10-02 | page | G9 | SUPPORT(正面) | 老读者：初期骂仙界篇，后接受"回归现实"收束，认为全书有完整句号 |
| A-E13 | slow-burn | COMMUNITY_EVALUATION | 盘点50本高质量的仙侠修真小说（搜狐） | sohu.com/a/677967202_121698175 | C | 2023-05-23 | page | G10 | SUPPORT | "凡人流开山之作……慢热型作品，精彩纷呈"；韩跑跑/韩老魔梗 |
| A-E14 | system-intensity | FACT | 网络小说6个能力逆天的金手指（搜狐） | sohu.com/a/301570162_100151658 | C | 2019-03-15 | snippet | G11 | SUPPORT | 金手指为器物型掌天瓶（小绿瓶），未见系统机制描述 |
| A-E15 | system-intensity | FACT | 红袖读书·小说百科《凡人修仙传》 | hongxiu.com/baike/1pcbn19zp4h4g | D | 访问日 | page | G12 | CONTEXT | AI 问答式百科页（模板化 QA 结构），仅作线索：掌天瓶金手指、谨慎主角、凡人流开山 |
| A-E16 | romance-level | COMMUNITY_EVALUATION | 贴吧：韩立感情线分析 | tieba.baidu.com/p/9496040769 | C | 访问日 | snippet | G13 | SUPPORT | "感情本来就是修仙的附属品"，南宫婉存在感低→感情线比重低（辅助判断） |

## Dimension Results

| dimension | value | confidence | agreement | 判定链 |
|---|---|---|---|---|
| identity | 凡人修仙传/忘语/起点 | HIGH | — | E01~E04 三方一致，Tier A 官方页 |
| serialization-status | completed | CONFIRMED | CONSISTENT | E01/E02/E04（Tier A 直接确认 → DIMENSION STOP） |
| romance-structure | single（正式道侣唯一；存在明显多女暧昧） | WEAK | DISPUTED | E05 vs E06 口径冲突（"唯一道侣"vs 紫灵"道侣/妻子"）；按 SP §11.3 输出并存；DISPUTED → confidence 上限 WEAK（SP §10.4） |
| harem（派生） | 倾向 H3 非后宫（正式关系口径存在争议） | **WEAK** | **DISPUTED** | 该项由 romance-structure 派生，confidence/agreement 不得强于基础 claim。E05“唯一妻子/道侣”与 E06“紫灵=道侣/妻子”存在术语冲突，因此不能写 LIKELY/CONSISTENT；按现行规则与基础 claim 一致保持 WEAK/DISPUTED。 |
| system-intensity | none（金手指为器物，非系统机制） | WEAK | INSUFFICIENT | E14/E15 间接证据；无任何"系统流"讨论；诚实标注证据较弱 |
| slow-burn | high | LIKELY | CONSISTENT | E13 + E15(线索) + 知乎动漫讨论旁证；"慢热型"多来源一致 |
| filler | unknown | UNKNOWN | INSUFFICIENT | 未获独立直接证据；不得用"长=水"（TX §5.4） |
| protagonist-abuse | unknown | UNKNOWN | INSUFFICIENT | 无虐主讨论；凡人流设定下不适用强判断 |
| protagonist-iq | strong | WEAK | INSUFFICIENT | 仅红袖 D 类与零星读者言论；"韩跑跑"谨慎型（E13）与智商在线相关性有限 |
| ending-reception | mixed（存在正负两类评价线索） | **WEAK** | DIVIDED | 正面方 E12 为 page；负面方 E08~E11 均仅 snippet。当前 access_mode 不足以把“评价两极”升级到 CONFIRMED/LIKELY；保留 DIVIDED 作为已观察到的口径差异，但 evidence confidence 降为 WEAK。若要恢复强结论，需重新打开至少一条独立负面来源页面核实。 |

## 冲突与处理

- romance-structure 冲突（E05/E06）：检查顺序→同书？是。日期：百科词条同为近期维护。定义："道侣/妻子"词汇口径差异（正式婚姻 vs 恋情）。术语冲突 → 输出并存：正式道侣唯一；存在明显多女暧昧元素（紫灵/元瑶）；个别来源把紫灵称"道侣"——不选边。未做多数投票。
- ending-reception：负面（仙界篇仓促/烂尾）×正面（接受收束）→ DIVIDED。同时明确"凡人篇本身口碑稳定"，区分评价对象，避免把"烂尾"写成客观事实。旧帖（2020 豆瓣）与 2023 知乎并存均属完结后评价，无 recency 冲突。

## Verdict

- 身份正确：PASS
- 用户显式问题（FULL_SCAN 排雷）：已覆盖身份/状态/感情/系统/慢热/结局
- 关键 Dimension 与人工复核对照：见 T712
- 结论待写入 REAL-WORLD-EVALUATION.md：**PASS**（pending 人工复核细节）