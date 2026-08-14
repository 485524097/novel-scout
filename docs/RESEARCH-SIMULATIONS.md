# Novel Scout Research Simulations

> **定位：DEVELOPMENT / EVALUATION ARTIFACT（开发/评估产物）。**
> 本文件主要服务 Stage 7 回归测试与设计复盘，**不是 runtime reference**。
> 正常 Novel Scout 执行时不需要自动读取本文件；运行时应加载 `references/search-playbook.md` 与 `references/source-policy.md`。
> 验证日期：2026-08-12。所有时间性结论绑定该日期。所有"证据状态"按 T217 审计后的访问级别记录。

## 0. 验证目标与方法

- 目的：检查 search-playbook 是否可执行，不产出正式书评。
- 方法：Request 解析 → Identity → Research Priority → Queries → Evidence Ledger（原子化）→ Claim Synthesis → Dimension Result → Stop。
- 结论必须来自 Search → Page → Evidence Item；禁止用模型记忆预写答案。
- **模型记忆错误（如误判连载状态）是本阶段发现的危害教训，不是测试证据本身。**

## 1. T217 来源审计结果（2026-08-12 复核）

对上一版记录的每条关键证据重新核验（打开页面或核对元数据），修正如下：

| # | 修正 | 说明 |
|---|---|---|
| 1 | 删除"七星阁书评（2025-08-15）"证据 | 其记录 URL `https://www.7xingge.com/review/1.html` 实为该论坛**首页**（Discuz 论坛版面），不存在《诡秘之主》书评；该证据此前仅来自搜索摘要，无法核验 → 移除，不再引用 |
| 2 | 《诡秘之主》状态升级为 Tier A 页面级 | https://m.qidian.com/book/1010868264/catalog/ 实际打开：`已经完本 · 共1418章`，含"完本感言（上/下）" |
| 3 | 《诡秘之主》豆瓣书评（12572058）页面级确认 | 实际打开：2020-05-06 19:42 发布，标题《说说乌贼的〈诡秘之主〉》；页面带"可能有关键情节透露"警告 → spoiler_level = major（结局相关），支持"结局仓促"批评 + "无女主小说"描述 |
| 4 | 中国日报文章（WS5eb3c4f4a310eec9c72b758f）页面级确认 | 2020-05-07 发布，**来源为"江西网络广播电视台"（转载）**，按 §3.1 作为单一转载链引用；确认 2018-04 起连载于起点、2020-05-01 完结 |
| 5 | 微信读书页、维基、Fandom 等此前无 URL 记录 | 无法核验 → 从证据表删除（source_url = none，不编造） |
| 6 | 《玄鉴仙族》状态升级为 Tier A 页面级 | https://m.qidian.com/book/1035420986/catalog/ 实际打开：`连载中 · 共1627章`，最新章节《第一千五百六十四章 誓身》更新于 2026-08-11 20:38:44 |
| 7 | 《玄鉴仙族》作者统一为"季越人" | 起点官方页明确"作者：季越人"；NGA 网友写"寄越人"为同音异写，不是别名 |
| 8 | 《玄鉴仙族》连载起点修正 | 上架/首订 2022-11-25（起点数/www 数据站 qidiantu，snippet 级），表述为"约 2022-11 上架"；删除原"2022-11-01 前后开始连载"的精确说法 |
| 9 | 《剑来》精确完结日期删除 | 上一版"2025-01-21 完结"无来源支持 → 删除。已核验事实：不晚于 2025-02-20 已完结（网易 2025-02-20 文章报道"完结引发两极分化"，页面级）；精确日期未在已核验页面中出现 |
| 10 | 《剑来》网易文章降级 | https://www.163.com/dy/article/JOSFC7DP0552GY5T.html 页面级打开：2025-02-20 22:08 发布，作者为网易号自媒体"落星荷动漫"（无真人署名、无原始出处、模板化结尾）→ Tier D，只作线索与论据结构参考 |
| 11 | 《剑来》中国作家网文章页面级确认 | https://www.chinawriter.com.cn/n1/2026/0805/c404027-40774327.html 实际打开：标题《从"讲故事"到"讲道理"——评烽火戏诸侯〈剑来〉》，来源《青春》杂志，作者 沈如珊，2026-08-05 刊出；确认首发"2017 年纵横中文网"，并承认"中后期节奏拖沓、支线冗杂、行文晦涩" |
| 12 | 《剑来》完结日期页面级确认（T224） | https://www.chinawriter.com.cn/n1/2025/1221/c403994-40628859.html（中国小说学会2025年度中国好小说发布，2025-12-21）实际打开：网络小说榜第 2 名"烽火戏诸侯：《剑来》，纵横中文网，2025年1月24日完结"；澎湃新闻、江苏作家网为同根转载（交叉印证，不另计独立） |

## 2. Case A — 知名已完结小说：《诡秘之主》

### 2.1 证据表（Evidence Ledger，按 T213 原子化）

| evidence_id | claim_id | dimension | claim_type | source | URL | access_mode | source_date | access_date | tier | indep | supports | spoiler |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| E101 | C101 | serialization-status | FACT | 起点目录页 | https://m.qidian.com/book/1010868264/catalog/ | page | 页面实时 | 2026-08-12 | A | G1 | SUPPORT | none |
| E102 | C101 | serialization-status | FACT | 中国日报（转载江西网络广播电视台） | https://cn.chinadaily.com.cn/a/202005/07/WS5eb3c4f4a310eec9c72b758f.html | page | 2020-05-07 | 2026-08-12 | B | G2 | SUPPORT | none |
| E103 | C102 | romance-structure | COMMUNITY_EVALUATION | 豆瓣书评《说说乌贼的〈诡秘之主〉》（proof） | https://book.douban.com/review/12572058/ | page | 2020-05-06 | 2026-08-12 | C | G3 | SUPPORT | major |
| E104 | C103 | ending-reception | COMMUNITY_EVALUATION | 同上（E103） | https://book.douban.com/review/12572058/ | page | 2020-05-06 | 2026-08-12 | C | G3 | SUPPORT | major |
| E105 | C104 | ending-reception | COMMUNITY_EVALUATION | 起点完本感言条目（目录页内"完本感言（上/下）"） | https://m.qidian.com/book/1010868264/catalog/ | page | — | 2026-08-12 | A | G1 | SUPPORT | none |
| E106 | C105 | slow-burn | COMMUNITY_EVALUATION | 中国日报正文（该文引用多篇早期书评背景，无单独读者来源） | （E102） | page | 2020-05-07 | 2026-08-12 | B | G2 | CONTEXT | none |

注：E103/E104 为同一页面两条断言，须分记两条 Evidence（one item = one source-assertion pair 的同一来源复用规则：同一来源可产生多条 Evidence Item，但一条 Item 只含一个来源）。

### 2.2 Claim Synthesis 示例（T213 聚合）

```
C102（romance-structure: "全书无官方向女感情线 / 无女主小说"）
supported_by:
- E103（豆瓣长评；G3 独立；page；SUPPORT：文中明确称"无女主小说〈诡秘之主〉"）
agreement: INSUFFICIENT（仅 1 个独立来源）→ confidence 上限 WEAK
```

### 2.3 Dimension Results（T214 三层分离）

| dimension | value（taxonomy） | confidence | agreement | 说明 |
|---|---|---|---|---|
| serialization-status | completed | CONFIRMED | CONSISTENT | Tier A 页面"已经完本·1418章" + Tier B 媒体（E101/E102） |
| romance-structure | no-romance（倾向） | WEAK | INSUFFICIENT | 仅 1 个独立页面级来源；红袖读书 AI 问答页（Tier D 线索）与"无女主"一致但不算独立读者证据 |
| ending-reception | mixed | LIKELY | DIVIDED | 批评方：豆瓣 2020"匆匆完结、卡了一半剧情"；支持方：同书 2020-05-06 整体"封神之作"定位 + 完本感言的存在性；两极论据均结构性存在（两极事实已确认，但两极各自独立来源数尚少 → LIKELY） |
| slow-burn | medium（偏慢，证据弱） | WEAK | INSUFFICIENT | 本案例未获得独立页面级社区来源，保留 WEAK 并注明 |

### 2.4 阻碍与发现

- 红袖读书 ask 类页面为模板化 AI 问答（"点击链接回归经典作品"式引导语），与真实长评冲突 → 按 §3.3 **具体页面**降级为线索（不进黑名单）。
- 该问题验证了 access_mode 规则：AI 页面当时仅 snippet 级，未升级。

## 3. Case B — 连载中小说（时效性）：《玄鉴仙族》

选书经过（供复盘）：候选《宿命之环》《赤心巡天》经搜索确认均已完结（2025-01 / 2026-05），模型记忆两次误判 → 改选《玄鉴仙族》。

### 3.1 证据表

| evidence_id | claim_id | dimension | claim_type | source | URL | access_mode | source_date | access_date | tier | indep | supports | spoiler |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| E201 | C201 | serialization-status | FACT | 起点目录页 | https://m.qidian.com/book/1035420986/catalog/ | page | 页面实时 | 2026-08-12 | A | G1 | SUPPORT | none |
| E202 | C202 | slow-burn | COMMUNITY_EVALUATION | NGA 帖子《玄鉴仙族真的好看吗，目前10多章节奏比长生文还慢》 | https://bbs.nga.cn/read.php?tid=43809530 | snippet | 2025-04-12 | 2026-08-12 | C | G2 | SUPPORT | none |
| E203 | C202 | slow-burn | COMMUNITY_EVALUATION | 同上帖内多名用户回复（"前期节奏确实很慢""前面600章还是很紧凑"） | （E202） | snippet | 2025-04-12 | 2026-08-12 | C | G2* | SUPPORT | none |
| E204 | C202 | slow-burn | COMMUNITY_EVALUATION | 豆瓣长评《〈玄鉴仙族〉的文学溯源》 | https://book.douban.com/review/16778707/ | snippet | 2025-06-15 | 2026-08-12 | C | G3 | SUPPORT | none |
| E205 | C203 | filler | COMMUNITY_EVALUATION | NGA 帖子（同 E202，被喷水描述） | （E202） | snippet | 2025-04-12 | 2026-08-12 | C | G2* | SUPPORT | none |
| E206 | C203 | filler | COMMUNITY_EVALUATION | NGA 帖子《大家现在觉得玄鉴主要看点》回复（2026-04-30："灌水时候…只有难受了""更新实在不利"） | https://ngabbs.com/read.php?page=1&tid=46682286 | snippet | 2026-04-30 | 2026-08-12 | C | G4 | SUPPORT | none |
| E207 | C204 | ending-reception | COMMUNITY_EVALUATION | NGA 帖子《玄鉴仙族…看评论跌落神坛了？》"必定烂尾"类回复 | https://ngabbs.com/read.php?tid=41786384 | snippet | 2024-09-24 | 2026-08-12 | C | G5 | CONTEXT | none |
| E208 | C205 | filler / 更新 | COMMUNITY_EVALUATION | NGA 帖子（2024-04："懒狗…剧情推进那叫一个慢"） | https://bbs.nga.cn/read.php?page=e&tid=39981831 | snippet | 2024-04-26 | 2026-08-12 | C | G6 | SUPPORT | none |
| E209 | C202 | slow-burn | COMMUNITY_EVALUATION | BookLink 书评（"慢热长卷…拒绝快节奏爽点"） | https://booklink.me/comment-1-1035420986-test0606.html | snippet | 2023-01-12 | 2026-08-12 | C | G7 | SUPPORT | none |
| E210 | C201 | serialization-status | FACT | QQ 阅读数据页（"连载 | 更新时间 2026-02-14"） | https://mdsxx.bookresource.qq.com/book/1035420986/ | snippet | 2026-02-14 | 2026-08-12 | B | G8 | SUPPORT | none |

*G2 组内回复不另算独立来源。

### 3.2 Dimension Results

| dimension | value | confidence | agreement | 说明 |
|---|---|---|---|---|
| serialization-status | ongoing | CONFIRMED | CONSISTENT | Tier A 页面"连载中·1627章"+"2026-08-11 更新"（E201）+ Tier B 数据页（E210）；绑定"截至 2026-08-12" |
| slow-burn | high | LIKELY | CONSISTENT | 2023（E209）、2025（E202）、2025 豆瓣（E204）三个独立讨论环境一致 |
| filler | high（中后期，社区侧） | LIKELY | DIVIDED | 2025-04"被喷水但前面600章紧凑"（E205）；2026-04 仍在吐槽灌水（E206）；官方/媒体侧（B 类）未在本案例中单列 → 社区侧 DIVIDED |
| ending-reception | unknown（连载中） | — | — | 不适用；2024"必烂尾"为预测旧帖（E207, 2024-09），按时效规则（§12.4）只作当时情绪记录 |

## 4. Case C — 明显分类争议小说：《剑来》

### 4.1 证据表

| evidence_id | claim_id | dimension | claim_type | source | URL | access_mode | source_date | access_date | tier | indep | supports | spoiler |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| E301 | C301 | identity（首发平台/起始） | FACT | 中国作家网《从"讲故事"到"讲道理"——评烽火戏诸侯〈剑来〉》（沈如珊，来源《青春》） | https://www.chinawriter.com.cn/n1/2026/0805/c404027-40774327.html | page | 2026-08-05 | 2026-08-12 | B | G1 | SUPPORT | none |
| E302 | C302 | ending-reception（批评方） | COMMUNITY_EVALUATION | 网易号"落星荷动漫"《剑来：作为一本引发热议的玄幻巨作，它的结局真的烂尾了吗？》 | https://www.163.com/dy/article/JOSFC7DP0552GY5T.html | page | 2025-02-20 | 2026-08-12 | D | G2 | SUPPORT | major |
| E303 | C302 | ending-reception（支持方） | COMMUNITY_EVALUATION | 同上（E302 文内转述"悲剧美学""意难平"读者观点） | （E302） | page | 2025-02-20 | 2026-08-12 | D | G2* | SUPPORT | major |
| E304 | C302 | ending-reception | COMMUNITY_EVALUATION | 中国作家网（E301 承认"中后期节奏拖沓、支线冗杂、行文晦涩"，但整体论定"瑕不掩瑜"） | （E301） | page | 2026-08-05 | 2026-08-12 | B | G1 | CONTEXT | none |
| E305 | C303 | saintliness（负面侧） | COMMUNITY_EVALUATION | 豆瓣长评《剑来浪费了一个月的时间》 | https://book.douban.com/review/16300253/ | snippet | 2024-11-16 | 2026-08-12 | C | G3 | SUPPORT | none |
| E306 | C303 | saintliness（正面侧） | COMMUNITY_EVALUATION | 中国作家网（书简湖问心局"规则重构与道义坚守的深度思辨"） | （E301） | page | 2026-08-05 | 2026-08-12 | B | G1 | REFUTE | none |
| E307 | C304 | filler | COMMUNITY_EVALUATION | 网易号"浅评〈剑来〉…最大的问题"（支线过多/视角生硬） | https://www.163.com/dy/article/FTGMQF930517RUP3.html | snippet | 2020-12-11 | 2026-08-12 | D | G4 | SUPPORT | none |
| E308 | C302 | ending-reception | COMMUNITY_EVALUATION | 虎扑帖"今天凌晨正式完结，怎么评价？（又臭又长）" | https://m.hupu.com/bbs/630153860.html | snippet | N/A | 2026-08-12 | C | G5 | SUPPORT | none |
| E309 | C302 | ending-reception | COMMUNITY_EVALUATION | 233乐园（"评价两极"） | https://www.233leyuan.com/post-detail/2061630986327810048 | snippet | 2026-06-01 | 2026-08-12 | D | G6 | SUPPORT | none |
| E310 | C301 | serialization-status（完结日期） | FACT | 中国小说学会2025年度中国好小说发布（中国作家网） | https://www.chinawriter.com.cn/n1/2025/1221/c403994-40628859.html | page | 2025-12-21 | 2026-08-12 | B | G7 | SUPPORT | none |

*G2 为单页自媒体，其转述观点不增加独立性。

### 4.2 Dimension Results

| dimension | value | confidence | agreement | 说明 |
|---|---|---|---|---|
| serialization-status | completed；completion_date = 2025-01-24 | CONFIRMED | CONSISTENT | E310（中国小说学会榜单，页面级：纵横中文网、2025-01-24 完结）+ E301（2026-08-05 作家网书评，背景）→ 绑定"截至 2026-08-12"；2025-02-20 网易文（E302）为次级佐证 |
| ending-reception | mixed | CONFIRMED | DIVIDED | 批评方结构性论据（腰斩承诺剧情/收尾失衡：E302；"又臭又长"：E308）、支持方整体评价（E304 官方媒体"瑕不掩瑜"）；两极均有充分来源，社区确实两极已确认 |
| saintliness | unknown（无法可靠分类） | LIKELY | DISPUTED | 负面（E305 情绪化标签）+ 正面解读（E306 官方媒体）→ 分类边界冲突（"圣母"是否成立），taxonomy 合法值中无可可靠取值 → value = unknown + agreement = DISPUTED，输出并存 |
| filler（中后期） | high（社区侧） | LIKELY | CONSISTENT | E301（官方媒体承认）、E302、E307 跨 B/D 一致 |

## 5. T219 内部一致性检查（Revision 后 12 项）

| # | 检查 | 结果 | 依据 |
|---|---|---|---|
| 1 | 一条 Evidence Item 只对应一个来源 | PASS | §8.1；本次证据表 each row = one source（E103/E104 同一来源分两条断言，规则允许） |
| 2 | Claim 可引用多个 Evidence IDs | PASS | §8.5 C001 聚合示例（E001~E003） |
| 3 | taxonomy value 与 confidence 分离 | PASS | §10（value/confidence/agreement 三列）；Case A/C 的 Dimension Results 表三列独立 |
| 4 | MIXED 语义不再冲突 | PASS | MIXED 仅作 taxonomy 值（ending-reception=mixed）；confidence 无 MIXED；agreement 用 DIVIDED/DISPUTED |
| 5 | NO_SPOILER 已从 Base Mode 移除 | PASS | §3.1 仅 FULL_SCAN/SPECIFIC_RISK/FIT_CHECK；剧透改 spoiler_level modifier |
| 6 | DETAILED 已从 Base Mode 移除 | PASS | §3.2 detail_level modifier；§14 预算表按场景更新 |
| 7 | hard_no 不再错误终止 FULL_SCAN | PASS | §15.3：FULL_SCAN 仅维度停；§7.2 三模式对比 |
| 8 | explicit user question 永远完成 | PASS | §7.3（"我先告诉你是不是重系统"示例） |
| 9 | snippet 不误升级 page evidence | PASS | §8.3 + source-policy §3.2 + §16.2；Case B 的 snippet 级证据均标 WEAK 或注明 |
| 10 | AI SEO 规则不是域名黑名单 | PASS | source-policy §3.3"按具体页面评价"；红袖读书仅具体 ask 页降级 |
| 11 | Research Simulation 来源日期准确 | PASS | T217 审计 11 项修正（见 §1）；七星阁假 URL 删除、剑来精确完结日期未核验 |
| 12 | Stage 1 taxonomy 未被擅自改变 | PASS | 本轮未触碰 references/taxonomy.md、preference-guide.md |

## 6. 共性问题与已落地规则修改（模拟 + Revision 汇总）

1. **AI SEO 问答污染（Case A 实证）** → source-policy §3.3 识别特征 + **具体页面降级、禁止域名黑名单**（T218）。
2. **模型记忆不可靠（两次误判连载状态、未知首发平台）** → search-playbook §12.2："MODEL MEMORY IS NOT EVIDENCE"；作为危害记录，不作为测试证据。
3. **情绪化标签关键词两极（"圣母"）** → Case C 示范：需同时参照 Tier B 深度评论（E306）。
4. **假 URL 风险（搜索摘要诱导）** → 七星阁事件说明 snippet 级 URL 必须页面级核验后才可引用（T217 实证）。
5. **证据原子化** → 每条 Evidence = 单来源单断言；Claim 层聚合（T213）。
6. **三概念分离** → value / confidence / agreement 三列输出（T214）。

## 7. 本文件的限制说明

- 多数社区类结论仍为 **snippet 级**（NGA/豆瓣/BookLink 等未逐页打开），已在证据表逐条标注 access_mode；正式运行时的报告级结论应按 §8.3 升级为 page 级后再引用。
- 未使用任何付费搜索 API、未写任何爬虫脚本；全部为 Agent 原生搜索/抓取。
- 本文件为开发/评估产物，运行时无需加载。

## 8. 后续模拟计划（可选，Stage 3+ 执行）

- spoiler_level = none 的实际输出跑测（检查输出隔离）。
- SPECIFIC_RISK 单雷点实跑（预算裁剪验证）。
- FIT_CHECK + hard_no early TASK STOP 实测。
- DRY RUN（无联网降级路径）。