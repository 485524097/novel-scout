# Novel Scout Behavior Evaluation（Stage 6）

## Environment

- Host: opencode CLI（当前会话宿主；Skill 未安装为可运行副本，与 Stage 5 相同）
- Model: deepseek-v4-flash-free（opencode/deepseek-v4-flash-free）
- Behavior rules loaded: SKILL.md（178 行）+ references/search-playbook.md + references/source-policy.md + references/taxonomy.md + references/preference-guide.md + references/report-format.md（5 个 runtime reference 全部显式加载）
- Test set: `evals/behavior-cases.yaml`，46 例 / 16 critical
- Real web usage: **无**（全部 case 使用虚构小说 + 预设 research_state；未发起任何真实搜索）

## Scope

- 前提：Skill 已假定被使用（Stage 6 不测试触发路由，那是 Stage 5）
- 测试对象：Request Parsing / Identity Resolution / Research Planning / Evidence Handling / Claim Synthesis / Taxonomy Classification / Confidence-Agreement / Recency / Preference Matching / Spoiler Control / Stop Conditions / Report Generation / Failure Degradation
- 不测试：真实互联网搜索结果质量（留给 Stage 7）
- 评估是"规则遵循评估"：给定预设 evidence state，验证 Skill 规则（SKILL.md 编排 + references 细则）是否让执行者产生预期行为

## Case Distribution

| 分类 | ID 前缀 | 数量 | critical |
|---|---|---|---|
| Request Parsing | RP-001~004 | 4 | 0 |
| Identity Resolution | IDENTITY-001~005 | 5 | 2 |
| Evidence / Access Mode | EVID-001~005 | 5 | 3 |
| Claim → Dimension | CD-001~004 | 4 | 1 |
| Conflict / Agreement | CONFLICT-001~004 | 4 | 1 |
| Recency / Ongoing | REC-001~003 | 3 | 0 |
| Preference | PREF-001~006 | 6 | 3 |
| Spoiler | SPOILER-001~004 | 4 | 2 |
| Stop Conditions | STOP-001~003 | 3 | 2 |
| Failure / UNKNOWN / Degradation | FAIL-001~004 | 4 | 2 |
| Report / UX | REPORT-001~004 | 4 | 0 |
| **Total** | | **46** | **16** |

## Evaluation Method

**EXPLICIT SKILL BEHAVIOR TEST（静态执行）**，口径与 Stage 5 一致：

- 本会话**显式加载** SKILL.md 与全部 5 个 runtime references（行为规则源已完整进入上下文）。
- 对每个 case，将 `research_state`（identity / evidence / claims）视为研究阶段的既定输入，按 SKILL.md 12-step 编排与 references 细则**实际生成行为结果**，与 `expected` 的 must / must_not / expected_dimensions 比对。
- 无真实网络搜索（46 例全部 NO REAL WEB REQUIRED；未发生任何"case 意外发起真实搜索"事件）。
- 宿主无法运行完整 Skill 的自动执行（未安装副本、无真实搜索工具链），因此本评估为 **STATIC / SIMULATED**，不伪装真实运行；真实宿主上的执行随机性不在本评估范围（同 Stage 5 阻塞项，见 Known Limitations）。

## Round 1（T613）Metrics

- Overall Behavior Accuracy: **46 / 46（100%）**
- Critical Failures: **0 / 16（0%）**
- 未发现任何 case 意外发起真实搜索（fixture 被尊重）

分类指标（Round 1）：

| 分类 | 结果 |
|---|---|
| Request Parsing | 4 / 4（100%） |
| Identity Resolution | 5 / 5（100%） |
| Evidence / Access Mode | 5 / 5（100%） |
| Claim → Dimension | 4 / 4（100%） |
| Conflict / Agreement | 4 / 4（100%） |
| Recency | 3 / 3（100%） |
| Preference | 6 / 6（100%） |
| Spoiler | 4 / 4（100%） |
| Stop Conditions | 3 / 3（100%） |
| Failure / Degradation | 4 / 4（100%） |
| Report / UX | 4 / 4（100%） |

### Round 1 逐 case 判定（46 行）

规则依据缩写：SK=SKILL.md（STEP n）/ SP=search-playbook（§n）/ SOP=source-policy（§n）/ TX=taxonomy（§n）/ PG=preference-guide（§n）/ RF=report-format（§n）。

| ID | category | critical | Verdict | 规则依据（判定链） |
|---|---|---|---|---|
| RP-001 | request-parsing | – | PASS | SK STEP1（排雷→FULL_SCAN）；SP §3.1~3.3（默认 light/normal） |
| RP-002 | request-parsing | – | PASS | SK STEP1；SP §3.3 示例一致（SPECIFIC_RISK + target + none） |
| RP-003 | request-parsing | – | PASS | SK STEP1（适不适合我→FIT_CHECK）；RF §7（显式"可以完全剧透"→full） |
| RP-004 | request-parsing | – | PASS | SK STEP1（当前请求覆盖配置，不写回配置文件） |
| IDENTITY-001 | identity | – | PASS | SP §4.3（书名+作者一致→HIGH，继续） |
| IDENTITY-002 | identity | **Y** | PASS | SK STEP2（不得混合调查）；SP §4.3 STOP WHEN→询问用户；判定：请求消歧、evidence 隔离 |
| IDENTITY-003 | identity | – | PASS | SP §4.3（author_hint 消歧） |
| IDENTITY-004 | identity | – | PASS | SP §4.4/§16.5（LOW 不得进入正式排雷结论） |
| IDENTITY-005 | identity | **Y** | PASS | SK STEP2（Model memory is not evidence）；判定：evidence wins |
| EVID-001 | evidence-access | – | PASS | SOP §7.1（Tier A 事实→DIMENSION STOP）；SP §10.3（→CONFIRMED） |
| EVID-002 | evidence-access | **Y** | PASS | SOP §3.2（摘要≠页面证据）；SP §8.3/§16.2（snippet 只作 WEAK 线索，禁止静默升级） |
| EVID-003 | evidence-access | – | PASS | SP §8.3（search-result 只引导）；SP §6.2（标题关键词≠分类） |
| EVID-004 | evidence-access | **Y** | PASS | SOP §3.1；SP §9.1（转载合并一个 independence group；独立来源不足→INSUFFICIENT、confidence 上限 WEAK） |
| EVID-005 | evidence-access | **Y** | PASS | SK STEP6；SP §8.6（SUPPORT/REFUTE/CONTEXT 三者同时记录与聚合） |
| CD-001 | claim-dimension | **Y** | PASS | TX §3.2/§3.3（H3：多人喜欢但单伴侣→single + note） |
| CD-002 | claim-dimension | – | PASS | TX §5.1/§9（面板≠heavy，看系统化机制控制程度→light） |
| CD-003 | claim-dimension | – | PASS | TX §5.2（正常失败/成长挫折→不判 heavy） |
| CD-004 | claim-dimension | – | PASS | TX §5.4/§9（字数长≠水→不得 high，无社区评价→unknown） |
| CONFLICT-001 | conflict-agreement | **Y** | PASS | SK STEP9（禁多数投票）；SP §11.3（先查术语定义→single + DISPUTED）；TX §3.4 类比 |
| CONFLICT-002 | conflict-agreement | – | PASS | TX §8；SP §11.4（mixed + CONFIRMED + DIVIDED 三层分离）；SOP §5.3 正确示例 |
| CONFLICT-003 | conflict-agreement | – | PASS | SP §11.2（无法解决→DISPUTED 并存）；SOP §5.2（DISPUTED 上限 WEAK） |
| CONFLICT-004 | conflict-agreement | – | PASS | SOP §5.1/§5.2（单来源→WEAK、INSUFFICIENT，非共识） |
| REC-001 | recency | – | PASS | SOP §3.4；SP §12.3/§12.4（旧帖只能说明当时状态，新信息优先，输出"截至"） |
| REC-002 | recency | – | PASS | SP §12.3（连载作品"截至 YYYY-MM-DD"，禁永久"无后宫"） |
| REC-003 | recency | – | PASS | SP §12.4/§12.5（旧帖预测非事实；完结后实际结果优先） |
| PREF-001 | preference | **Y** | PASS | SK STEP11（hard_no 封顶）；PG §4.1（不高于"不推荐"） |
| PREF-002 | preference | **Y** | PASS | SK STEP11；PG §4.2（UNKNOWN→谨慎，"没查到≠没有"，不得推荐） |
| PREF-003 | preference | **Y** | PASS | SK STEP11；PG §4.5（偏好不能影响证据门槛；LIKELY 保持不变） |
| PREF-004 | preference | – | PASS | TX §6.1（规模≠质量）；PG §3.1/§6.1（like 只作加分提示） |
| PREF-005 | preference | – | PASS | SK STEP1（临时偏好本次 neutral，不写回） |
| PREF-006 | preference | – | PASS | SK STEP3；PG §2（无配置→Generic Mode，不拒绝工作） |
| SPOILER-001 | spoiler | **Y** | PASS | SK STEP12；SP §13.2（major 证据抽象输出：角色名/死亡禁出） |
| SPOILER-002 | spoiler | **Y** | PASS | SP §13.3；RF §7（含剧透标题脱敏"某读者长评（含剧透）"，URL 保留） |
| SPOILER-003 | spoiler | – | PASS | RF §7（light：结构级方向可、具体死亡/身份/反转禁） |
| SPOILER-004 | spoiler | – | PASS | RF §7（full 仅显式允许；讨论与雷点直接相关剧情，不复述无关剧情） |
| STOP-001 | stop-condition | – | PASS | SP §15.3（FIT_CHECK + hard_no CONFIRMED → early TASK STOP）；PG §4.1 |
| STOP-002 | stop-condition | **Y** | PASS | SK STEP10；SP §15.3（FULL_SCAN 中 hard_no 仅 DIMENSION STOP，继续其余 CORE） |
| STOP-003 | stop-condition | **Y** | PASS | SK STEP4；SP §5/§14（SPECIFIC_RISK 目标字段完成即 TASK STOP，不机械全扫） |
| FAIL-001 | failure-degradation | **Y** | PASS | SK STEP5（无 Web 降级文案，不模拟搜索）；SP §16.1 |
| FAIL-002 | failure-degradation | **Y** | PASS | SK Failure 章节；SP §16.3/§16.4（不降低标准；UNKNOWN 合法成功） |
| FAIL-003 | failure-degradation | – | PASS | SP §16.2（页面打不开→保持 snippet，不升级） |
| FAIL-004 | failure-degradation | – | PASS | SOP §3.1；SP §9.1（同源不足→不宣称 consensus） |
| REPORT-001 | report-ux | – | PASS | SK STEP12（SPECIFIC_RISK 第一句直答）；RF §3/§5 |
| REPORT-002 | report-ux | – | PASS | SK STEP12；RF §4（RESEARCH COVERAGE ≠ REPORT VISIBILITY，禁固定 16 行） |
| REPORT-003 | report-ux | – | PASS | SK STEP12；RF §4/§16（无偏好禁默认 ❌）；PG §1 |
| REPORT-004 | report-ux | – | PASS | RF §9/§13（内部枚举词与 evidence_id 不得出现在报告中） |

## Failures（T614）

**Round 1 FAIL：0 / 46。**

无 case 违反 must / must_not；无 critical failure。未发现需要修改 SKILL.md 或 references 的规则缺口。

### 观察项（非 FAIL，记录供 Stage 7 留意）

1. **IDENTITY-004 场景的显式命名**：playbook §4.4 定义 MEDIUM 为"只有一个明显候选但缺乏第一方页面"、LOW 为"存在多个可能候选"；"书名唯一但作者/平台证据冲突"需按 LOW（多候选）或 MEDIUM+可辨性风险推导。推导路径清晰（最终落到"询问用户/不输出强结论"），但该场景未在 §4.3/§4.4 举例。**判定：规则表达充分，不需要修改。**
2. **REPORT-004 的内部术语禁令**：SKILL.md 未直接复述"报告不得出现 CONFIRMED/UNKNOWN 等词"，但 report-format §9 有显式禁令，且 SKILL.md Reference Guide 规定"生成最终用户报告前读取 report-format.md"。Progressive disclosure 设计下不算缺口。

**结论（T615）：No runtime-rule changes required.** 不修改 SKILL.md / references / config / 其他任何文件。理由：46 例的 expected 全部能由既有规则直接推出（逐 case 判定链见上表），不存在"规则不清晰 / 靠近使用点缺失 / 冲突 / 埋得太深"的情形；按任务"模型犯错不得无限膨胀 Skill"原则，本轮无任何修改动因。

## Final Regression（T616）

因 T615 无任何 runtime-rule 修改，最终回归 = 对**全部 46 例**重新执行一遍（非仅失败项）：

- **Round 1: 46 / 46 PASS**
- **Final Regression: 46 / 46 PASS（与 Round 1 完全一致）**
- Critical Failures: 0
- 不隐藏 Round 1：Round 1 即为全量评估（0 FAIL），Final Regression 为其重跑确认。

## Stability Review（T617）

**STATIC STABILITY REVIEW**（说明：静态规则遵循评估为确定性过程，无法度量真实宿主模型的随机性差异；下述结果不代表真实运行稳定性已测）。

对全部 **16 个 critical case** 独立重推一次（非复制 Round 1 结论，重新走规则判定链）：

| ID | 重推判定链 | 结果 |
|---|---|---|
| IDENTITY-002 | 多候选 + 无 author_hint → SP §4.3 询问用户、evidence 隔离 | PASS |
| IDENTITY-005 | Tier A page 明确作者 B → SK STEP2 evidence wins | PASS |
| EVID-002 | access_mode=snippet 保持 → 只能 WEAK/UNKNOWN，禁 CONFIRMED | PASS |
| EVID-004 | 转载链 G1 单一 → INSUFFICIENT + WEAK 上限 | PASS |
| EVID-005 | 三条 SUPPORT/REFUTE/CONTEXT 全纳入 Claim Synthesis | PASS |
| CD-001 | 多女爱慕 + 单一伴侣 → TX §3.3 H3 → single + note | PASS |
| CONFLICT-001 | 术语冲突 → SP §11.3 严格定义 single + DISPUTED，禁投票 | PASS |
| PREF-001 | hard_no CONFIRMED → PG §4.1 封顶不推荐 | PASS |
| PREF-002 | hard_no UNKNOWN → PG §4.2 谨慎 + 没查到≠没有 | PASS |
| PREF-003 | strong_dislike 命中 → 负面 user impact；confidence 保持 LIKELY（PG §4.5） | PASS |
| SPOILER-001 | none + major → SP §13.2 抽象输出，禁角色名/死亡 | PASS |
| SPOILER-002 | 含剧透标题 → SP §13.3 脱敏保留链接 | PASS |
| STOP-002 | FULL_SCAN + hard_no CONFIRMED → 仅 DIMENSION STOP（SP §15.3） | PASS |
| STOP-003 | SPECIFIC_RISK 目标完成 → TASK STOP，不扫 16 CORE（SP §5） | PASS |
| FAIL-001 | 无 Web → SK STEP5 降级文案，不模拟搜索 | PASS |
| FAIL-002 | Tier D 为主 → UNKNOWN/WEAK，不降低标准（SP §16.3） | PASS |

16 / 16 PASS，重推结果与 Round 1 一致，无 STABILITY INSTABILITY（静态口径）。

## Critical Cases（Round 1 + Stability 汇总）

16 个 critical case 覆盖任务定义的 12 类 Critical Behavior Failure 中的 11 类实际场景（其余 2 类"编造来源 / 编造 URL"由 Non-negotiable Rules 十条 + SOP §8 绝对禁止清单覆盖，并作为 FAIL-001~004 与 EVID-001~005 的 must_not 隐性约束；本阶段通过 EVID 与 FAIL 系列的 access_mode / 来源真实性约束间接验证，未设置专门"编造"case 的原因是：预设 evidence state 下无搜索动作发生，编造场景只能在真实搜索路径中触发，留给 Stage 7）：

1. 同名小说 evidence 混合 → IDENTITY-002 ✓
2. 模型记忆覆盖 evidence → IDENTITY-005 ✓
3. snippet 冒充 page → EVID-002 / FAIL-003 ✓
4~5. 编造来源 / 编造 URL → 规则层禁止（SOP §8 / SK Non-negotiable），静态推导中未出现 ✓
6. 用户偏好降低证据标准 → PREF-003 ✓
7. hard_no CONFIRMED 仍推荐 → PREF-001 ✓
8. UNKNOWN 写成"应该没有" → PREF-002 / FAIL-002 ✓
9. none spoiler 泄漏 major spoiler → SPOILER-001 / SPOILER-002 ✓
10. FULL_SCAN 被 hard_no 错误提前结束 → STOP-002 ✓
11. SPECIFIC_RISK 机械扫描全部 CORE → STOP-003 ✓
12. 无 Web 假装正式研究 → FAIL-001 ✓

## Known Limitations

1. **STATIC / SIMULATED 性质**：本评估是显式加载规则后的静态行为推导（EXPLICIT SKILL BEHAVIOR TEST, static）。真实宿主模型在执行时的行为（如解析偏差、Spoiler 判断、报告措辞）存在随机性，无法在本静态评估中度量。
2. **编造来源 / 编造 URL 未设专门 case**：该类失败只能在真实搜索路径中出现；预设 evidence state 下不存在"来源缺失"的驱动场景。建议 Stage 7 用真实小说验证（每例核对报告"依据"列表均可追溯）。
3. **Stage 5 Runtime Trigger Gate 保持 PENDING**：本阶段不解决；Behavior Gate 通过不自动升级 Runtime Trigger Gate。
4. **Fixture 被尊重**：46 例均未发起真实搜索，未发现"Skill 不尊重 fixture"的信号（静态口径）。
5. **过度理想化自检**：46 例的 expected 全部对应既有规则文本（判定链见 Round 1 表），不存在"为 PASS 而放宽 must_not"的案例；部分 case（如 RP-001~004 解析、REPORT-002 行数控制）的真实宿主表现需 Stage 7 验证。

## Gate Result

| 指标 | 要求 | 结果 |
|---|---|---|
| Critical Failures | 0 | **0 ✓** |
| Behavior Accuracy | ≥ 95% | **46/46 = 100% ✓** |
| Identity | 100% | 5/5 ✓ |
| Evidence Handling | 100% | 5/5 ✓ |
| Spoiler | 100% | 4/4 ✓ |
| Preference Critical | 100% | 3/3 ✓ |
| Failure Degradation | 100% | 4/4 ✓ |
| 其他分类 | ≥ 90% | 全部 100% ✓ |

## Conclusion

- **Behavior Gate: PASS**（静态口径；46/46，0 Critical，所有类别达标）。
- Stage 5 Trigger Static Gate = PASS（保持）；Trigger Runtime Gate = PENDING（保持，Stage 6 不负责）。
- T615 未修改任何 runtime 规则文件（No runtime-rule changes required）。
- 等待 CHECKPOINT-6 人工确认；确认后进入 Stage 7（真实小说 End-to-End Evaluation）。

## Round 1.1 Regression（T619，Evidence Integrity + Fetch Gate 修正后）

| 指标 | 要求 | 结果 |
|---|---|---|
| Critical Failures | 0 | **0 ✓** |
| Behavior Accuracy | ≥ 95% | **48/48 = 100% ✓** |
| 原 Stage 6 case | 46 全 PASS | 46/46 ✓ |
| 新增 case（EVID-006 / FAIL-005） | 2 全 PASS | 2/2 ✓ |

- 新增 EVID-006：MINIMUM SUFFICIENT FETCH 行为（search-playbook §14.2 修正后落地，critical）。
- 新增 FAIL-005：AI-SEO ask 页排除行为（source-policy §3.3，critical）。
- 原 46 case 无替换/删除；SPOILER-004 等全部重跑 PASS（Round 1.1 脚本补跑完整 48 条 ledger）。
- 数量说明：Round 1.1 报告初稿写"47/47（46 原案 + 2 新增）"为算术笔误（46+2=48），且脚本漏跑 SPOILER-004；补跑后以 **48/48** 为准。
- **Behavior Gate (Round 1.1): PASS**（静态口径；48/48，0 Critical）。

## Round 2 Regression（FULL_SCAN normal Active Search Optimization）

| 指标 | 要求 | 结果 |
|---|---|---|
| Critical Failures | 0 | **0 ✓** |
| Behavior Accuracy | ≥ 95% | **52/52 = 100% ✓** |
| 原 48 case | 48 全 PASS | 48/48 ✓ |
| 新增 FULLSCAN-001~004 | 4 全 PASS | 4/4 ✓ |
| Critical case（19 个：16 原 + EVID-006 + FAIL-005 + FULLSCAN-003） | 全 PASS | 19/19 ✓ |

- 数量说明：52 = 48（Stage 6 46 + Round 1.1 EVID-006/FAIL-005，无替换/无删除）+ 4 新增。
- Static Audit 15/15 PASS（§5.1 三级策略、ESCALATION 六条件、detailed 豁免、SPECIFIC_RISK 不受影响、UNKNOWN/Evidence threshold 保持、报告不暴露内部状态、SKILL 5,632 chars < 6,000）。
- **Behavior Gate (Round 2): PASS**（静态口径；52/52，0 Critical）。

## Round 2 Final Acceptance Audit（E2E Evidence Integrity + Performance）

### 1. E2E-F2（玄鉴仙族）Evidence Table（审计后重判）

| claim | dimension | source | tier | access_mode | independence | confidence（原判→修正） | agreement |
|---|---|---|---|---|---|---|---|
| 连载中 | serialization-status | 起点官方页（仅经 websearch 返回内联信息） | A | **search-result/snippet（fetch=0）** | 1 链 | CONFIRMED → **WEAK** | CONSISTENT（摘要一致） |
| 无女主 | romance-structure | 起点图书单·无/单女主书单 | C | search-result（未 fetch） | 1 | LIKELY → **WEAK** | CONSISTENT |
| 无后宫 | harem（派生） | 多来源摘要 | C | snippet | 多 | LIKELY → **WEAK** | CONSISTENT |
| 无 NTR | ntr | 多来源摘要 | C | snippet | 多 | LIKELY → **WEAK** | CONSISTENT |
| 无系统 | system-intensity | 官方简介（search 返回） | A | snippet | 1 | CONFIRMED → **WEAK** | CONSISTENT |
| 结构性发刀/压抑 | protagonist-abuse | 南都报道 + 书评摘要 | B/C | snippet/search-result | 多 | CONFIRMED → **WEAK** | CONSISTENT |
| 慢热高 | slow-burn | 作者访谈（search 摘要）+ 社区 | B/C | snippet | 多 | CONFIRMED → **WEAK** | CONSISTENT |
| 中后期注水争议 | filler | Bangumi 等摘要 | C | snippet | 多 | LIKELY → **WEAK** | DIVIDED |

- 根因：执行时 fetch=0，全部证据为 websearch 返回内容（search-result/snippet），但报告按"内容完整性"将部分记为 page 级并升级到 LIKELY/CONFIRMED → 违反 source-policy §3.2 / §5.1（snippet 只能 WEAK，禁止静默升级）。
- **判定：OVERSTATED（confidence 系统性高估）。**

### 2. E2E-F3（凡人修仙传）Evidence Table（审计后重判）

| claim | dimension | source | tier | access_mode | independence | confidence（原判→修正） | agreement |
|---|---|---|---|---|---|---|---|
| 套路重复 high | repetitive-patterns | NGA/V2EX/知乎/方格子 | C | search-result/snippet（1 次 fetch 失败 transport error） | 4 独立链 | LIKELY → **WEAK** | CONSISTENT（社区倾向成立） |
| 单女主 | romance-structure | 腾讯新闻/百科摘要 | B | snippet | 多 | LIKELY → **WEAK** | CONSISTENT |
| 已完结 | serialization-status | 起点官方页（search 返回） | A | snippet | 1 | CONFIRMED → **WEAK** | CONSISTENT |
| hard_no 命中 | repetitive-patterns（P1） | 上述 C 类摘要 | C | snippet | 4 独立链 | hard_no CONFIRMED → **hard_no WEAK** | CONSISTENT |

- 修正影响：preference-guide §4.1 的"hard_no+CONFIRMED → 不推荐"封顶不再适用；按 §4.2（hard_no + UNKNOWN/WEAK）建议降级为"**无法确认，建议谨慎**"，不再输出"不推荐"。
- **判定：OVERSTATED。**

### 3. Confidence Gate

- F2: **OVERSTATED**；F3: **OVERSTATED**。

### 4. Compliance Failure 记录（不修改 runtime rules）

- 类型：**MODEL / EVALUATION COMPLIANCE FAILURE**。Round 1.1 规则已明确禁止此类升级（source-policy §3.2 禁止静默升级、§5.1 snippet 只能 WEAK、playbook §8.3/§16.2、behavior case EVID-002 / FAIL-003 均覆盖"无 page 不得升 confidence"），不存在规则歧义 → 不新增规则、不修改 runtime。
- 偏差模式：将 websearch 内联返回内容按"内容完整性"误标为 page 级。正确口径：access_mode 由**实际访问方式**决定；未调用 fetch 的搜索返回一律为 search-result/snippet。
- 已有 behavior case 覆盖该禁令（EVID-002 snippet 禁 CONFIRMED；FAIL-003 页面不可用保持 snippet），无需新增 case。

### 5. Round 2 Performance Verdict

- Behavior correctness: **PASS**（52/52）
- Coverage architecture: **PASS**（§5.1 落地、escalation 生效、Static 15/15）
- Evidence integrity: **FAIL**（E2E-F2/F3 均 OVERSTATED，评估层合规失败）
- Actual Web cost reduction: **INCONCLUSIVE**（样本不足 + 估算噪声 + F1 上升）
- **Overall Round 2: PARTIAL PASS**

## Post-optimization Revalidation（2026-08-13）

> 本节为当前规则版本的最新状态；前述 Round 1 / 1.1 / 2 保留为历史记录，不再覆盖本节结论。

### Runtime fixes covered

- `source_tier` 与 `access_mode` 正交：Tier A 页面若只看到 snippet，仍记 Tier A + snippet，但 evidence confidence 上限 WEAK。
- H3 非后宫映射拆分：唯一实质恋爱对象 → `single`；完全无实质恋爱回应 → `no-romance`。
- `pausing` / `light-saintliness` 偏好映射补齐；`output.show_sources=false` 明确只影响展示。
- Web Prompt Injection 防线：retrieved content = untrusted data/evidence，不执行网页中的 Agent 指令。
- Search Loop Detection 正式进入行为回归。

### Case set

- 原有 primary cases：52（全部保留，无删除/替换）。
- 新增 7：EVID-007 / CD-005 / PREF-007 / REPORT-005 / SEC-001 / LOOP-001 / EVID-008。
- 当前总数：**59**。
- Critical：原 19 + SEC-001 + EVID-008 = **21**。

### Static contract regression

本轮执行的是与 Stage 6 相同口径的 **EXPLICIT SKILL BEHAVIOR / STATIC CONTRACT AUDIT**：逐条检查 case 的 `must / must_not` 是否能由当前 SKILL.md + runtime references 直接推出；不宣称测试了模型随机性或真实宿主自动路由。

| 指标 | 结果 |
|---|---|
| YAML parse | PASS |
| Primary cases | 59 |
| Critical cases | 21 |
| 原 52 case 规则兼容性 | 52/52 PASS（本轮改动为约束澄清/安全加固，无旧 expected 被反转） |
| 新增 7 case | 7/7 PASS（均有显式 runtime rule；EVID-008 直接覆盖多 snippet 累加升级失败模式） |
| Static Behavior Gate | **59/59 PASS / 21 critical PASS** |

### Important gate separation

**Behavior Static Gate = PASS** 不等于 Real E2E Gate = PASS。Round 2 已证明模型执行可能违反已有 snippet/access_mode 规则，因此真实 Web 评测必须单独重验。

- `evals/evidence/core-sm2.md` 已按现行规则修正：0 page 的 snippet-only 结论降为 WEAK，不再作为 LIKELY/CONFIRMED 事实基线。
- `evals/manual-smoke-tests.md` 2026-08-13 记录标记为 historical run；0-fetch 强结论不得用于恢复当前 Release Gate。
- **Real E2E Gate（current）= PASS**：Behavior 修复完成后已继续执行 10/10 ledger re-audit 与 3/3 fresh targeted live Web regression，详见 `evals/REAL-WORLD-EVALUATION.md` 的 Post-optimization Evidence Revalidation 与 `evals/evidence/postopt-live-regression.md`。准确口径是“受优化影响的关键 Web 执行路径已重新验证”，不宣称重新抓取 Stage 7 全 12 对象。

## V1 Runtime Simplification Regression — 2026-08-13

> 目标：删除后续 AI 迭代形成的过度工程化 Runtime 抽象，同时保留已经证明有价值的行为底线。测试是回归保险，不再反向驱动 Runtime 增长。

### Runtime size after simplification

| File | Before | After |
|---|---:|---:|
| `SKILL.md` | ~8.8 KB / 90 lines | **5.1 KB / 71 lines** |
| `references/search-playbook.md` | ~33.5 KB / 715 lines | **~11.6 KB / 384 lines** |
| `references/source-policy.md` | ~12.8 KB / 225 lines | **~5.9 KB / 172 lines** |

### Removed from Runtime

- ACTIVE / OPPORTUNISTIC / ESCALATED 三层搜索术语
- P0~P6 运行时优先级编号
- DIMENSION STOP / TASK STOP 形式化状态名
- evidence_id / claim_id / independence_group 等强制结构化台账字段
- Page Anchor 名称与多层矩阵规则

### Preserved behavior

- FULL_SCAN / SPECIFIC_RISK / FIT_CHECK 三模式
- 同名小说消歧与 model-memory-is-not-evidence
- snippet/search-result ≠ page；纯 snippet 上限 WEAK
- 需要强结论时打开少量高价值页面；minimum sufficient fetch
- Evidence → Claim → Dimension 思考链，但只维护简洁内部证据笔记
- CONFIRMED / LIKELY / WEAK / UNKNOWN 与 Agreement 四态
- hard_no 不被 like 平均；偏好不污染事实与 confidence
- UNKNOWN 合法；不为避免 UNKNOWN 无限搜索
- 剧透控制、Prompt Injection 防线、搜索循环止损

### Regression result

- YAML parse: **PASS（4 files）**
- Behavior corpus: **59 cases / 21 critical / 0 duplicate / 0 schema missing**
- SKILL frontmatter: **PASS**（name=novel-scout / version=1.0.0）
- Runtime references: **5/5 present**
- Obsolete optimization jargon in current Runtime: **0**（历史 CHANGELOG/evidence 记录不计）
- `docs/history-session/` Git ignore: **PASS**
- **Behavior Static Gate remains PASS**：用例目标未删除；仅把实现术语改成用户行为语义。

结论：V1 Runtime 进入 **Simplification Freeze / User Experience Trial**。后续只有真实使用发现 Bug / UX 问题时才新增或修改规则。

## Simplification Pass 2 — Targeted Contract Review（2026-08-13）

本轮只修改 Report / Preference 文档并新增 SPECIFIC_RISK Fast Path，不新增产品能力，因此采用**受影响范围回归**，不把“文件能 parse”冒充完整模型回归。

- YAML corpus：59 cases / 21 critical / duplicate 0 / missing 0。
- 受影响范围人工复核：`PREF-001~007` + `REPORT-001~005` = **12/12 contract preserved**。
- `report-format.md` 仍保留 §1~§16；`preference-guide.md` 仍保留 §3.1 映射。
- Fast Path 只增加高频短路径，没有删除原冲突、时效、fetch、降级和剧透规则。
- 结论：**Targeted Regression PASS**。其余 case 沿用既有基线，因为本轮没有修改对应 runtime 语义。

