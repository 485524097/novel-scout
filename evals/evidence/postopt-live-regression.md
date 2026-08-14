# Post-optimization Fresh Live Web Regression — Evidence Ledger

> 执行日期：2026-08-13
>
> 目的：验证 post-optimization `source_tier × access_mode + Page Anchor` 规则在**新的真实 Web 访问**中能执行，而不是只对历史台账做重判。
>
> 范围：3 个代表路径（SPECIFIC_RISK / FULL_SCAN targeted evidence / FIT_CHECK hard_no）。本文件是 evaluation artifact，不是 runtime reference。

## FRESH-R1 — 《全职高手》SPECIFIC_RISK / no-romance

- Request：`无剧透，《全职高手》主角有感情线吗？`
- Target：romance-structure / harem 派生
- Search：`《全职高手》 原著 无感情线 叶修 感情线`
- Page rule：先看 search results，再**实际打开**可直接支撑目标 claim 的页面；不以 snippet 数量升级。

| evidence_id | source | url | tier | access_mode | independence_group | supports | summary |
|---|---|---|---|---|---|---|---|
| FR1-E01 | 中国作家网《荣耀征程，初心不改——评网络小说〈全职高手〉》 | https://www.chinawriter.com.cn/n1/2019/1230/c404027-31527871.html | B | page | FR1-G1 | SUPPORT | 页面明确评价《全职高手》“没有爱情线”，主线为叶修重返荣耀巅峰；原著连载信息同时可核对。 |
| FR1-E02 | 澎湃新闻《剧版〈全职高手〉：当电竞没有爱情，能成爆款吗》 | https://www.thepaper.cn/newsDetail_forward_4001854 | B | page | FR1-G2 | SUPPORT | 文章在讨论原著时明确写叶修虽与多名女性角色互动，但没有明确感情线、没有谈恋爱/开后宫。 |

### Result

- romance-structure = **no-romance**
- harem = **H3 非后宫**（此 H3 属“完全无实质恋爱回应”路径，因此映射 no-romance，不是 single）
- confidence = **LIKELY**
- agreement = **CONSISTENT**
- Page Anchor：2 个独立 page 直接支持，满足社区/解释型 LIKELY 最低要求。
- Verdict：**PASS**（SPECIFIC_RISK 轻量 + H3 新映射 + page-first evidence upgrade 均成立）

## FRESH-R2 — 《凡人修仙之仙界篇》FULL_SCAN targeted ending regression

- Request context：FULL_SCAN normal 的 ending-reception 关键维度复核
- Target：ending-reception
- Search：`《凡人修仙传》 仙界篇 结局 评价 书评`
- 本 case 不重新跑全部 16 CORE；目的只验证此前最容易被 snippet 误升级的 **DIVIDED 两侧 Page Anchor**。

| evidence_id | source | url | tier | access_mode | independence_group | supports | summary |
|---|---|---|---|---|---|---|---|
| FR2-E01 | PTT C_Chat《[心得] 關於凡人修仙傳-仙界篇》 | https://www.pttweb.cc/bbs/C_Chat/M.1780402280.A.C8E | C | page | FR2-G1 | REFUTE | 读者完整看完仙界篇后批评后段副本冗长、升级过快、结局过快、支线/人物未充分收束，同时认为结局本身“还可以”。 |
| FR2-E02 | 得到 APP《凡人修仙之仙界篇》全部书评及评分 | https://www.dedao.cn/ebook/reviews?id=lxaVvndNG6D4kgLJ2OKxqVMmE1zXPwV2k5ZwAdjyQeYR75vbaBnr9ol8pZERLg1m | C | page | FR2-G2 | SUPPORT | 页面存在多条正面评价与高星评论，也有“后期有瑕疵”“不如灵界”等保留意见；可确认正向认可口径真实存在。 |

### Result

- ending-reception = **mixed**
- confidence = **LIKELY**
- agreement = **DIVIDED**
- Page Anchor：批评侧与支持侧各至少 1 个独立 page；不靠 search-result/snippet 拼数量。
- Verdict：**PASS**（DIVIDED 双侧 page anchor 成立；“烂尾”仍只作为读者评价，不转成客观事实）

## FRESH-R3 — 《斗破苍穹》FIT_CHECK / hard_no=harem

- Request：`hard_no=[harem]，看看《斗破苍穹》适不适合我`
- Target：romance-structure / harem → preference recommendation
- Search：`斗破苍穹 萧炎 两位妻子 萧薰儿 彩鳞 原著`

| evidence_id | source | url | tier | access_mode | independence_group | supports | summary |
|---|---|---|---|---|---|---|---|
| FR3-E01 | 百度百科·萧炎词条 | https://wapbaike.baidu.com/item/%E8%90%A7%E7%82%8E/5808896 | B | page | FR3-G1 | SUPPORT | 正文经历段明确写萧炎与薰儿、美杜莎举行婚礼，形成两段明确伴侣关系。 |
| FR3-E02 | 澎湃新闻《剧版〈全职高手〉：当电竞没有爱情，能成爆款吗》 | https://www.thepaper.cn/newsDetail_forward_4001854 | B | page | FR3-G2 | SUPPORT | 文章比较男频作品时明确以《斗破苍穹》为例，称其男主有两个老婆；与 FR3-E01 为独立内容来源。 |

### Result

- romance-structure = **harem（H1）**
- harem = **CONFIRMED / CONSISTENT**（关系事实明确，page 级来源相互支持）
- preference：`hard_no=harem` 命中 → Recommendation Scale 封顶 **不推荐**；其他 like 不得平均掉硬雷。
- Verdict：**PASS**（Evidence → Dimension → Preference 顺序正确；无 0-page 强结论）

## Fresh Regression Summary

| Case | Mode / focus | page anchors | result |
|---|---|---:|---|
| FRESH-R1 | SPECIFIC_RISK / H3 no-romance | 2 | PASS |
| FRESH-R2 | FULL_SCAN targeted / DIVIDED | 2（双方各 1） | PASS |
| FRESH-R3 | FIT_CHECK / hard_no harem | 2 | PASS |

- **Fresh live Web regression = 3/3 PASS**。
- 全部强结论都发生在实际 page 打开之后；没有“多个 snippet 数量累加 → LIKELY/CONFIRMED”。
- 与 `evals/behavior-cases.yaml` EVID-007/EVID-008、CD-005、PREF hard_no 规则一致。
- 本回归与 10/10 Evidence Ledger re-audit 合并后，足以恢复 **Real E2E Gate = PASS（post-optimization targeted regression scope）**；它不等于把 Stage 7 全 12 个对象重新抓取了一遍，历史完整覆盖仍保留在原 Stage 7 记录中。
