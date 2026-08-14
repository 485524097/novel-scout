# Novel Scout Search Playbook

> 目标：用尽可能少但足够可靠的搜索完成小说排雷。不要把搜索做成固定剧本，也不要为了“覆盖完整”机械增加 query。

## 0. Fast Path（高频请求优先）

### SPECIFIC_RISK

只问“后宫吗 / 有 NTR 吗 / 重系统吗 / 虐主吗”等具体雷点时，先按这 6 步执行；**没有冲突或异常时不需要通读本文件其余章节**：

1. 确认书名与作者/平台，避免同名混书。
2. 只搜索目标雷点；关键词只是线索，最终按 taxonomy 定义判断。
3. snippet 只用于筛页面；只有 snippet 时结论最多 WEAK。
4. 需要更强结论时，打开 1~2 个最可能直接解决问题的页面。
5. 得出 `value + confidence + agreement`。快速判定：官方/第一方 page 直接确认简单事实可 `CONFIRMED`；多个独立、可靠 page 对明确关系事实都直接确认时也可 `CONFIRMED`；单个社区 page 通常仍是 `WEAK`；多个真正独立、较可靠来源相互支持且关键内容已实际 page 核验时通常可到 `LIKELY`；证据不足或存在实质冲突时保持 `WEAK / UNKNOWN / DISPUTED`。有冲突不多数投票。
6. 第一句直接回答用户，目标问题答完或明确 UNKNOWN 后停止。

常见异常再跳到对应章节：同名→§4；冲突→§11；连载时效→§12；剧透→§13；搜索/fetch 成本→§14；失败降级→§16。

### FIT_CHECK

先确认身份，再优先核验 hard_no / 用户显式问题 / strong_dislike。若 hard_no 已确认且用户只问“适不适合我”，可以直接给不推荐；不为完整画像额外扫全部维度。

### FULL_SCAN

使用正文 §4~§16 按需执行；仍遵守“共享查询、够用即停”，不按 CORE 数量机械拆查询。

## 1. Request Modes

Novel Scout 只有三种基础模式：

- **FULL_SCAN**：排雷 / 详细排雷 / 值不值得开。
- **SPECIFIC_RISK**：只问一个或几个明确雷点。
- **FIT_CHECK**：适不适合我的口味。

Modifiers：

- spoiler：none / light（默认）/ full
- detail：normal（默认）/ detailed

本次用户请求优先于个人配置。

## 2. Parse the Request

开始前只需要识别：

- title
- author_hint / platform_hint（如果用户提供）
- base_mode
- explicit_risks
- spoiler_level
- detail_level
- temporary_preferences

多雷点问题仍属于 SPECIFIC_RISK，例如“有后宫和 NTR 吗？”——目标是两个字段，**两个都回答完或明确 UNKNOWN 后才停止**。

## 3. What Not to Do

不要把普通推荐、续写、文学分析、下载/更新、纯元数据查询、多书比较扩展成 Novel Scout 调查。

## 4. Identity Resolution

先确认你查的是哪一本书。

推荐顺序：

1. `"书名" 作者`
2. `"书名" 官方 / 平台`
3. 必要时补作者、平台、类型、发布时间等消歧信息

身份置信度：

- **HIGH**：作者/作品信息清楚，最好有第一方或可靠页面。
- **MEDIUM**：只有一个明显候选，但缺第一方确认。
- **LOW**：存在多个合理候选。

`LOW` 时先询问用户，不得混合不同同名小说的资料。

模型记忆只能帮助生成搜索词，不能当当前证据。

## 5. Research Planning

### FULL_SCAN normal

先查真正影响“要不要开书”的内容：

- 身份 / 连载状态
- 感情结构 / 后宫 / NTR
- 系统存在感
- 主角体验：圣母、智商、果断、虐主
- 节奏：慢热、水文
- 已完结作品的结局评价

世界观规模、力量体系、重复套路、剧情逻辑等：

- 高质量来源顺带提到 → 记录；
- 用户明确关心、命中 hard_no/strong_dislike、出现明显大雷、或会改变最终建议 → 再专项搜；
- 否则 normal 模式不需要为了“16 CORE 全覆盖”单独追加 query。

`detailed` 可以主动覆盖更多维度，但仍遵守“够用即停”。

### SPECIFIC_RISK

只查：

> identity + 用户明确问的雷点 + 为解释该雷点真正必要的相关信息。

不要顺手查世界观、战力、结局等无关字段。

### FIT_CHECK

读取偏好后优先：

1. hard_no
2. 用户本次显式问题
3. strong_dislike / dislike
4. 其他有助于判断适配度的核心信息

不需要为了生成“完整画像”把所有维度都搜一遍。

## 6. Query Construction

模板是提示，不是固定脚本。一组查询可以同时服务多个维度。

### 6.1 Metadata

`"书名" 作者` / `"书名" 官方` / `"书名" 完结` / `"书名" 连载`

### 6.2 Romance / Harem

`"书名" 感情线` / `"书名" 女主` / `"书名" 单女主` / `"书名" 后宫`

有争议再补：`暧昧` / `老婆` / `妻子` / `CP`。

“后宫”关键词命中只是线索，必须按 taxonomy 判断正式关系结构。

### 6.3 NTR

`"书名" NTR` / `绿帽` / `牛头人` / `感情背叛`

社区会滥用这些词，关键词命中 ≠ NTR 成立。

### 6.4 System

`"书名" 系统` / `面板` / `任务` / `金手指`

金手指、外挂、天赋、宝物不自动等于“系统文”。

### 6.5 Protagonist

`"书名" 主角 圣母` / `降智` / `智商` / `杀伐果断` / `憋屈` / `虐主`

尽量同时找具体行为描述，而不是只收集标签。

### 6.6 Pacing / Logic

`"书名" 慢热` / `节奏` / `水` / `注水` / `重复套路` / `剧情逻辑` / `战力崩`

“篇幅长”本身不能证明水文。

### 6.7 Ending / Status

`"书名" 完结` / `结局 评价` / `烂尾` / `收尾`

连载中作品不要把“会不会烂尾”的预测当 ending-reception 事实。

## 7. Search Order

简单原则即可：

> 先身份 → 再用户最在意的雷点 → 再影响最终建议的其他高价值信息。

不要用复杂优先级编号驱动搜索。显式问题永远要完成。

## 8. Evidence Notes

研究时只需保留**简洁内部笔记**，不要求正式 Ledger、ID、JSON 或数据库结构。

一条有用证据至少记住：

- 来源是谁 / 页面是什么
- 本次是 `page`、`snippet` 还是 `search-result`
- 它支持还是反对哪个 claim
- 一句话摘要
- 如果是连载信息，必要时记日期

判断链仍然保持：

```text
Evidence
  ↓
Claim
  ↓
Dimension Result
```

但这是**思考结构**，不是要求模型维护复杂字段。

### 8.1 Access Rule

- `page`：实际打开页面，可作为正式页面证据。
- `snippet`：搜索摘要，只能作为 WEAK 线索。
- `search-result`：标题/元数据，主要用于导航。

多个 snippet 不会因为数量多就自动升级。

### 8.2 Positive and Negative Evidence

不要先形成“这书是后宫/烂尾”的印象，然后只搜支持自己印象的内容。重要争议尽量看正反两边。

## 9. Source Selection & Independence

- 官方/第一方优先确认事实。
- 社区来源用于读者体验和争议。
- 同一原帖的转载、洗稿、相互引用不重复计权。
- AI 聚合 / SEO 问答只当线索。
- 一个具体、独立的长评通常比十个同源转载更有价值。

不需要维护 `independence_group` 编号；只要识别明显同源，不把它们算成多个证据即可。

## 10. Claim Verification

Dimension Result 仍使用三个分开的概念：

- **value**：taxonomy 结果
- **confidence**：CONFIRMED / LIKELY / WEAK / UNKNOWN
- **agreement**：CONSISTENT / DISPUTED / DIVIDED / INSUFFICIENT

实用判断：

- 官方 page 直接确认简单事实 → 可以 CONFIRMED 并停止该事实搜索。
- 多个独立可靠来源 + 实际页面核验关键内容 → 通常可 LIKELY。
- 只有 snippet / 单个社区来源 / 弱来源 → WEAK。
- 无法可靠确认 → UNKNOWN。

更详细的来源标准见 `source-policy.md`。

派生结论不能比基础事实更自信。例如 romance-structure 本身是 WEAK/DISPUTED，就不能把派生 harem 写成 CONFIRMED/CONSISTENT。

## 11. Conflict Handling

遇到“单女主 vs 后宫”“烂尾 vs 神作”等冲突：

1. 先确认对象和版本一致。
2. 检查是不是术语不同：女主、妻子、暧昧、红颜、正式伴侣不是同一个概念。
3. 检查信息时间：连载期说法可能已经过时。
4. 检查独立性：多篇转载可能只有一个源头。
5. 如果冲突会影响 hard_no 或最终建议，打开代表性页面核实。

仍然无法解决：

- 分类/事实冲突 → `DISPUTED`
- 社区明显两极 → `DIVIDED`
- 证据太少 → `INSUFFICIENT / UNKNOWN`

禁止简单多数投票。

## 12. Recency

连载作品的状态、感情线、NTR、结局相关信息都可能变化。

动态结论注明：

> 截至 YYYY-MM-DD。

旧连载期预测不能覆盖完结后的实际结果。已完结作品可适当放宽时效要求。

## 13. Spoiler Handling

### Research Spoiler ≠ Output Spoiler

为了确认雷点，内部可以阅读剧透内容；输出必须服从用户的 spoiler_level。

### none

只输出结构级结论，例如：

> 中后期存在与你该雷点相关的重要剧情。

不要写具体死亡、重大反转、最终身份、最终关系变化、结局事件。

若来源标题本身剧透，可写“某读者长评（含剧透）”而不展示完整标题。

### light

可以解释雷点类型和大致阶段，但避免关键反转。

### full

用户明确允许后才给完整剧情说明。

## 14. Search Budget & Minimum Sufficient Fetch

预算是经验范围，不是 KPI：

| 场景 | 常见范围 |
|---|---|
| SPECIFIC_RISK | 身份 + 1~3 组目标查询；通常打开 1~2 个关键页面就够 |
| FIT_CHECK | 身份 + hard_no / strong_dislike 优先；约 2~4 组目标查询 |
| FULL_SCAN normal | 通常 4~7 组共享查询；约 3~8 个真正有价值页面 |
| FULL_SCAN detailed | 可以更多，但仍需停止重复搜索 |

### 14.1 Snippet Pre-filter

先用 snippet 判断一个页面值不值得打开：

- 同人 / 动漫 / 漫画 / 视频搬运 / 无关 SEO / 身份不匹配 → 通常不打开。
- 直接关系事实 / 官方状态 / 有代表性的长评 / 重要冲突 → 优先打开。

### 14.2 Fetch Gate

目标 = **minimum sufficient fetch**。

只问三件事：

1. 当前证据是否已经足够回答？够 → 停。
2. 如果不够，哪个页面最可能直接解决问题？→ 打开它。
3. 打开新页面是否只是重复已有信息？是 → 不打开。

不要追求 zero fetch，也不要为了“来源更多”不断 fetch。

### 14.3 Large Pages

如果一个页面非常大，优先寻找同一官方体系或同等可靠但更轻量的页面。关键事实只有它能确认时再打开。

### 14.4 Search Loop

同一个 query 连续返回相同结果时不要无限重试：

- 已够回答 → 停；
- 不够 → 改写一次 query；
- 仍然重复 → WEAK / UNKNOWN，并结束该方向。

重复结果不算多个独立来源。

## 15. Stop Conditions

### Stop a Dimension

出现以下任一情况即可停止继续查该雷点：

- 可靠证据已经足够回答；
- 争议双方已经看清，可以诚实标 DISPUTED / DIVIDED；
- 合理搜索后仍只有弱证据，可以 WEAK / UNKNOWN；
- 新搜索只是在重复已有信息。

### Stop the Task

满足以下四点即可结束：

1. 身份没有重大歧义。
2. 用户明确问的问题都已回答或标 UNKNOWN。
3. 当前模式真正需要的高优先级内容已完成。
4. 继续搜索预计不会改变结论。

SPECIFIC_RISK 尤其要“答完就停”。

FIT_CHECK 中 `hard_no + CONFIRMED` 已足够判“不推荐”时，如果用户没要求详细排雷，可以提前结束。

## 16. Failure and Degradation

- **无 Web**：说明无法按正式证据标准排雷；默认不做“模型记忆版”。
- **页面打不开**：保持 snippet/WEAK，找可访问替代页面。
- **只有弱来源**：输出 WEAK / UNKNOWN，不降低标准。
- **搜索没结果**：尝试作者、别名、繁简体、平台等；仍无结果 → UNKNOWN。
- **身份不明**：先消歧，不继续正式排雷。

## 17. Minimal Examples

### SPECIFIC_RISK：`《X》后宫吗？`

```text
确认身份
→ 搜感情线/后宫
→ 用 snippet 筛选
→ 打开 1~2 个最有价值页面
→ 按 taxonomy 判断
→ 第一行直接回答
→ 停止
```

### FULL_SCAN：`排雷《X》`

```text
确认身份
→ 几组共享查询覆盖感情/系统/主角/节奏/结局
→ 高质量来源顺带提供其他维度就记录
→ 只对重大或用户关心的缺口追加搜索
→ 输出最重要结果
```

## 18. Prohibited Research Behaviors

- 先形成结论，再只搜支持自己的材料。
- 只搜“毒点 / 垃圾 / 烂尾”等负面词造成确认偏差。
- 关键词命中直接当分类成立。
- 一个评论代表社区共识。
- 同源转载当多个独立来源。
- snippet/search-result 当 page。
- 多个 snippet 靠数量堆成 LIKELY/CONFIRMED。
- AI 聚合内容当独立读者来源。
- 编造来源、URL、剧情或读者评价。
- 为了避免 UNKNOWN 无限搜索。
- 为了形式维护复杂的结构化证据表。
- 用户只问一个雷点时扩张成 FULL_SCAN。
- 同 query 无限重试。
- 身份未确认就正式排雷。
