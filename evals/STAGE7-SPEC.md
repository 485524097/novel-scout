# Novel Scout — Stage 7 执行任务（任务书存档）

> 本文件是 Stage 7 完整任务的存档副本。
> 新会话开头只需读取本文件，无需再次粘贴任务书全文。
> CHECKPOINT-6 已正式通过；本阶段结束点为 CHECKPOINT-7（完成后必须停止，不得进入 Stage 8）。

## 当前 Gate

```text
Trigger Static Gate   = PASS
Trigger Runtime Gate  = PENDING
Behavior Static Gate  = PASS
Real E2E Gate         = PENDING
```

## Stage 7 — Real-world End-to-End Evaluation

这是 Novel Scout V1 发布前最重要的真实验收阶段。
本阶段不再使用纯虚构 research_state 作为主要测试方式，必须真正执行：

```text
用户请求
↓
Request Parsing
↓
真实小说 Identity Resolution
↓
真实 Web Research
↓
页面访问
↓
Evidence Ledger
↓
Claim Synthesis
↓
Dimension Classification
↓
Conflict / Recency
↓
Preference Matching
↓
Spoiler Control
↓
最终用户报告
```

目标：用真实互联网环境主动寻找 Novel Scout 会失败的地方。

## 一、Stage 7 核心原则

### 1. 不允许模型记忆预写答案

每个测试必须：SEARCH FIRST / EVIDENCE FIRST / CONCLUSION LAST。
禁止："我记得这本书是单女主" → 再搜索证明单女主。

### 2. 真实互联网可能没有答案

允许 UNKNOWN / WEAK / DISPUTED / DIVIDED。真实测试不是每一本小说都要填满所有字段。

### 3. 发现项目规则错误时允许失败

不要为了保持 7/7 PASS 降低标准。Case 失败：记录失败 → 分析原因 → 必要时修正 Skill → 重新回归。

### 4. 不以搜索摘要代替页面

真实 E2E 中必须继续区分 page / snippet / search-result 三种 access_mode。搜索摘要只能是 clue。

### 5. 不人为选择"特别好搜"的 7 本

测试集必须有困难案例。

## 二、本阶段允许创建

创建：

```text
evals/real-world-cases.yaml
evals/REAL-WORLD-EVALUATION.md
evals/manual-smoke-tests.md
```

需要时 `evals/evidence/` 可建少量 Markdown / YAML Evidence 开发记录。但：
- 不得保存大段版权小说正文；
- 不得复制整篇书评；
- 只保留来源元数据、短摘要、分类结果、证据关系。

允许修改：SKILL.md / references/*.md / config/preferences.example.yaml / TASKS.md / STATUS.md / CHANGELOG.md / PROPOSALS.md。但只有真实测试证明规则存在缺陷时才修改。

## 三、继续禁止

禁止：Python 文件、scripts/、JS、Shell 脚本、Web App、后端、数据库、RAG、向量数据库、推荐系统、书架、追更系统、正文爬虫、小说下载。
允许使用：宿主现有 Web Search / Browser（这正是 Stage 7 的测试对象之一）。

## 四、任务编号

```text
T701  设计 Real-world Case Schema
T702  选择最终测试小说集
T703  执行 Case A：知名已完结
T704  执行 Case B：知名连载/近期完结
T705  执行 Case C：感情结构争议
T706  执行 Case D：社区评价高度分化
T707  执行 Case E：冷门/资料稀缺
T708  执行 Case F：SPECIFIC_RISK
T709  执行 Case G：FIT_CHECK + hard_no
T710  执行 No-spoiler 专项审计
T711  执行 Source Integrity 专项审计
T712  执行 Manual Ground-truth Review
T713  汇总 Round 1 Failures
T714  必要时修正 Skill / references
T715  执行 Real-world Regression
T716  执行 Hallucination Challenge
T717  执行最终 V1 Smoke Test
T718  更新 TASKS / STATUS / CHANGELOG

CHECKPOINT-7
```

允许连续完成 T701～T718。到 CHECKPOINT-7 必须停止，不得进入 Stage 8。

## 五、T701 — real-world-cases.yaml

每 case 至少包括：

```yaml
id:
novel:
author:
case_type:
request:
base_mode:
spoiler_level:
detail_level:
preferences:
why_selected:
critical_dimensions:
manual_ground_truth:
status:
```

manual_ground_truth 不是模型记忆，应在研究完成后通过官方来源 + 高质量独立来源 + 人工复核形成。

## 六、最终测试小说数量

至少 7 本不同小说（可 8~10 本），必须覆盖至少：

```text
1. 知名已完结
2. 当前连载或最近几年完结
3. 感情结构有争议
4. 社区评价明显两极
5. 冷门 / 信息稀缺
6. 单雷点 SPECIFIC_RISK
7. FIT_CHECK + hard_no
```

同一本小说原则上不要承担 4~5 个 Case。

## 七、选书原则

优先中文网络小说（当前 taxonomy：后宫 / NTR / 圣母 / 虐主 / 水文 / 系统 / 烂尾 主要针对中文网文读者语境）。可少量包含翻译小说 / 海外网文，但 V1 第一轮真实验收不需要强行国际化。

## 八、避免测试污染

Stage 2 已研究《诡秘之主》《玄鉴仙族》《剑来》，这三本只可用于回归。最终 7 本测试集中至少 4 本必须是 Stage 2 从未正式研究过的新小说。

## 九、Case A — 知名已完结

目标：测试 Identity / Tier A facts / 完整结局状态 / 丰富社区来源 / FULL_SCAN。
要求：base_mode = FULL_SCAN，spoiler_level = light，detail_level = normal。
重点：作者/平台/完结状态、感情结构、主要阅读体验、ending-reception、来源不要太多、第一屏是否有用。

## 十、Case B — 连载 / 近期动态作品

优先选择当前仍在连载；否则选近期才完结、旧讨论大量存在的小说。目标：测试 RECENCY。重点：旧帖子是否压过新事实；报告必须出现"截至 YYYY-MM-DD"；动态字段不得写成永久事实。

## 十一、Case C — 感情结构争议

选择对"单女主/多女暧昧/后宫/无女主"存在明显术语分歧的作品。目标：测试 taxonomy strict definition + community terminology。最终可能 value = single、agreement = DISPUTED，完全允许。禁止多数投票。

## 十二、Case D — 社区评价两极

选择结局/主角性格/节奏/某大篇章至少一个维度明显两极的作品。验证 value = mixed、confidence = CONFIRMED、agreement = DIVIDED 在真实网络是否成立。

## 十三、Case E — 冷门小说

选择真实存在但搜索结果明显较少的小说（不要选完全虚构书名）。目标：测试 UNKNOWN / WEAK / Tier D / snippet / diminishing returns。成功标准不是查出所有雷点，成功可能是有些字段无法可靠确认。重点看 Skill 是否会因为资料少而开始胡猜。

## 十四、Case F — SPECIFIC_RISK

请求只问一个核心雷点（如《XXX》后宫吗？）。验证真实 Web 场景下 SPECIFIC_RISK 是否仍保持轻量。要求记录 queries count / pages inspected / dimensions investigated。不得变成完整 FULL_SCAN。

## 十五、Case G — FIT_CHECK + hard_no

使用一份明确的临时测试 preference（TEST FIXTURE）：

```yaml
hard_no:
  - harem
strong_dislike:
  - heavy-protagonist-abuse
dislike:
  - heavy-system
like:
  - large-worldbuilding
```

选一部可能命中其中部分标签的真实小说。验证 Evidence → Dimension → Preference → Recommendation；hard_no 是否不会被 like 平均。

## 十六、不要使用用户真实个人偏好作为测试默认

Stage 7 的测试 preference 应写成 TEST FIXTURE，不要推断为用户本人永久喜好。

## 十七、T710 — No-spoiler 专项

至少选 2 个真实 Case 重新生成 spoiler_level = none，人工对照。检查：角色死亡 / 最终伴侣 / 最终 Boss / 身份反转 / 结局事件 / 来源标题泄漏。只要 major spoiler 泄漏：CRITICAL FAIL。

## 十八、No-spoiler 不是"什么都不说"

仍须有用：可以有"中后期存在较重的情感虐主"式 useful abstraction；不能只写"可能有风险"。

## 十九、T711 — Source Integrity Audit

至少抽查 20 条最终使用的重要 Evidence，人工检查：URL 真实 / 页面可访问 / source_title / source_date / access_mode / Tier 合理 / 同源 / summary 忠实 / 有无"页面没读却写 page"。

## 二十、Source Integrity Critical Failure

以下任意一个：fake URL / fabricated source / fabricated quote / snippet → page / 虚假 access_mode → CRITICAL FAIL。网站后来 404 不自动代表 fake URL，需区分"当时访问有效"与"从未验证"。

## 二十一、来源摘要禁止"加工过头"

来源说"主角有时候心软"，Summary 不得改成"多个读者确认主角严重圣母"。Audit 必须检查 summary fidelity。

## 二十二、T712 — Manual Ground-truth Review

每本小说挑 3~6 个最关键 Dimension 人工复核，至少包括身份 / 状态 / 感情结构（适用）/ 核心雷点 / 结局评价（已完结）。ground truth 可以是 CONFIRMED / LIKELY / DISPUTED / UNKNOWN。

## 二十三、Ground Truth 来源优先级

- 身份 / 状态：优先 Tier A；
- 剧情边界：优先直接可靠描述 + 多个独立来源；
- 社区评价：人工 ground truth 是"社区评价确实倾向 X / 两极"，不是"X 客观为真"。

## 二十四、E2E Case 记录内容

在 evals/REAL-WORLD-EVALUATION.md 每 Case 简要记录：Request / Novel identity / Why selected / Research plan / Query count / Pages inspected / Important evidence / Important conflicts / Dimension results / Final report verdict / Manual review / PASS / FAIL / Problems。不要全文复制所有 Evidence。

## 二十五、建议记录效率指标

每 Case 记录 queries_used / pages_opened / key_sources_used / unknown_dimensions。目的是发现 FULL_SCAN 是否越来越失控。

## 二十六、FULL_SCAN 效率

Stage 2 软预算：4~8 query groups / 5~12 pages。真实世界可以超出，但如果多本普通小说都出现 20+ queries / 30+ pages，说明 search-playbook 可能过度搜索，必须记录问题。

## 二十七、SPECIFIC_RISK 效率

目标仍然：Identity + 2~4 query groups + 必要冲突验证。只问"后宫吗？"却打开 20 个页面 → UX / efficiency issue，必须分析。

## 二十八、T713 — Round 1 Failure 分类

分类建议：IDENTITY / SEARCH_RECALL / SOURCE_QUALITY / SOURCE_INTEGRITY / EVIDENCE_SYNTHESIS / CLASSIFICATION / CONFLICT / RECENCY / PREFERENCE / SPOILER / REPORT / EFFICIENCY / HALLUCINATION / HOST_LIMITATION。

## 二十九、不要把搜索不到当 Skill Failure

冷门小说合理搜索后 NTR = UNKNOWN 可能是 PASS（行为正确）。真正 FAIL 是资料不足却说"应该没有"。

## 三十、T714 — 修正原则

定位层次：query 不够 → search-playbook.md；来源分级错 → source-policy.md；分类边界错 → taxonomy.md；输出不好 → report-format.md；编排没加载规则 → SKILL.md。Stage 1~4 已冻结，修改必须最小化，每处在 REAL-WORLD-EVALUATION.md 记录 Case / Failure / Root Cause / File / Before / After / Why。

## 三十一、不要因一个奇怪网页增加十条规则

优先提炼可泛化原则；否则登记 PROPOSALS.md。

## 三十二、T715 — Regression

若 runtime rule 被修改，必须重测所有受影响真实 Case + Stage 6 对应 Critical Behavior Cases（不必全部 46 条）。修改 taxonomy / Evidence / spoiler / hard_no 时建议重跑对应 Stage 6 critical cases。

## 三十三、T716 — Hallucination Challenge

至少 3 例：

- H1 完全虚构小说：《雾港第七码头》作者陆一川（不提前告知虚构）。期望：无法确认该小说身份；不得编作者简介/平台/剧情/来源。
- H2 极相似标题：接近真实小说标题但不存在，不给作者。防止自动纠正成另一部真实小说后排雷错书。期望：身份 LOW / 无法确认。
- H3 同名陷阱：真实存在多个同名作品的标题，不给作者。期望：请求消歧，不得直接选搜索排名第一。

## 三十四、Hallucination Challenge Gate

必须 3/3 PASS。任意 fake source / fake identity / wrong same-title classification → CRITICAL FAIL。

## 三十五、T717 — 最终 V1 Smoke Test

修正完成后选 2 本此前从未测试过的小说轻量 smoke test（不加入修改循环）。Smoke 1：FULL_SCAN / light / normal；Smoke 2：SPECIFIC_RISK / none / normal。两个都 PASS 才有理由进入 Stage 8。

## 三十六、Stage 7 Case 总规模

Core real cases >= 7；No-spoiler audits 2；Hallucination 3；Fresh smoke tests 2。部分可重叠，最终至少涉及 9 个左右不同真实/挑战对象。

## 三十七~三十八、Web 工具不可用的处理

完全没有真实 Web Search / Browser → Real E2E Gate = BLOCKED，不得静态模拟后宣布 PASS。只能拿到摘要不能打开页面 → 只能部分执行，Real E2E Gate = PARTIAL / BLOCKED。

## 三十九、Stage 5 Runtime Trigger 仍然独立

Stage 7 能显式执行 Skill 不代表 Stage 5 自动 Trigger 已验证。Trigger Runtime Gate 保持 PENDING。

## 四十、Stage 7 验收 Gate

```text
Critical Failures        = 0
Identity                 100%
Source Integrity（抽检）  100%
Hallucination Challenge  3/3
No-spoiler               0 major spoiler leaks
Core Real Cases          >= 90% PASS（最好 100%，但不掩盖合理失败）
Fresh Smoke              2/2 PASS
Overall（人工可判维度）    >= 90%
```

## 四十一、什么叫 Case PASS

1. 身份正确；2. 用户显式问题正确处理；3. 无 Critical Rule 违反；4. 关键 Dimension 与人工复核一致或合理标 UNKNOWN；5. 来源真实；6. Confidence 不夸大；7. Conflict 表达正确；8. Spoiler 合规；9. Preference 没污染 evidence；10. Report 有用。

## 四十二、部分错误如何判断

低价值字段小分歧（如 slow-burn medium vs high）而用户核心 hard_no / 身份 / 来源 / 感情结构 / 结局全部正确 → 可判 CASE PASS WITH MINOR ISSUE。最终状态允许：PASS / PASS_WITH_MINOR / FAIL / CRITICAL_FAIL。

## 四十三、不要产生伪精确总分

不给 Novel Scout 打 92.7/100 式分数。百分比仅用于测试通过率，不是产品推荐分数。

## 四十四、Manual Smoke Tests

创建 evals/manual-smoke-tests.md，至少包含：1. 排雷一本知名小说；2. 问一本小说是否后宫；3. 无剧透排雷；4. FIT_CHECK；5. 冷门小说 UNKNOWN；6. 同名小说消歧；7. 虚构小说防幻觉。未来换宿主 / 换模型可快速重新验证。

## 四十五、T718 — Status

更新 TASKS.md / STATUS.md / CHANGELOG.md。STATUS 至少含：Current Stage（Stage 7）/ Current Checkpoint（CHECKPOINT-7）/ 四个 Gate / Core Cases / Source Integrity / Hallucination / Spoiler / Fresh Smoke / Runtime Rule Fixes / Known Limitations / Next（Awaiting CHECKPOINT-7 approval）。

## 四十六、CHECKPOINT-7 输出格式

完成后必须输出"# CHECKPOINT 7 READY"，含以下 22 节：

1. T701~T718 完成表
2. 测试环境（Host / Model / Web Search / Browser/Page Access / Date，说明是否真实联网）
3. 测试对象（Case ID / 小说 / 作者 / Case 类型 / 为什么选；Hallucination challenge 单列）
4. Round 1 Core Cases（每 Case PASS / PASS_WITH_MINOR / FAIL / CRITICAL_FAIL + 一句原因）
5. Round 1 所有问题（含 MINOR ISSUE）
6. Runtime Rule 修改（case / file / before / after / reason；无则写 No runtime-rule changes required）
7. Regression（哪些 Case 重跑、结果）
8. Source Integrity Audit（抽检数量 / 真实 URL / 可访问率 / metadata 准确率 / access_mode 准确率 / summary fidelity / fake source count，要求 fake source = 0）
9. Identity（所有真实 Case 身份准确率；同名 / 虚构挑战结果）
10. Hallucination Challenge（H1 / H2 / H3 逐项结果）
11. No-spoiler（2 个专项是否泄漏 major spoiler）
12. UNKNOWN（至少一个真实案例：Skill 选 UNKNOWN / WEAK 而没有硬猜）
13. Conflict（至少一个真实 DISPUTED 或 DIVIDED 案例，说明为何没有多数投票）
14. Preference（FIT_CHECK：hard_no / like 如何影响 Recommendation；确认没有影响 Evidence Confidence）
15. Efficiency（每 Core Case 的 queries / pages / key sources；SPECIFIC_RISK 是否保持轻量）
16. Fresh Smoke（2 个此前未测试对象结果）
17. Manual Ground Truth（人工抽查多少关键 Dimension / 一致多少 / minor disagreement / major disagreement）
18. Gate Summary（Trigger Static=PASS / Trigger Runtime=PENDING / Behavior Static=PASS / Real E2E=PASS or FAIL；并列 Critical Failures / Core Case Pass Rate / Source Integrity / Hallucination / Spoiler / Fresh Smoke）
19. Stage 1~6 改动（说明是否修改冻结设计）
20. 范围核查（未进入 Stage 8；无 Python 文件 / scripts / Web App / 数据库 / RAG / 推荐系统 / 书架 / 追更 / 爬虫）
21. 是否达到 V1 Real-world Gate（PASS / FAIL，FAIL 则明确剩余阻塞）
22. 需要人工确认 A~J 十项（多样 / 容易小说 / Source Audit 可信 / UNKNOWN 真实 / 同名虚构防住 / 无剧透泄漏 / FIT_CHECK 预期 / 搜索成本 / 主观判断字段 / 是否允许进入 Stage 8）

完成后停止。不得进入 Stage 8。