# STATUS.md

> 每完成一个 Task 必须更新本文件。

## Current Stage

**V1 RC / User Experience Trial — Runtime Simplification Freeze**

V1 主体与真实 Web 验证已经完成。2026-08-13 对后续 AI 迭代造成的过度工程化进行减法：保留真实 Bug 修复，移除不必要的 Runtime 抽象。当前不再继续扩规则，进入真实使用体验阶段。

## Current Checkpoint

**RC EXPERIENCE FREEZE**：可以正常显式使用 Novel Scout；后续只有真实使用发现 Bug/UX 问题时才修改 Runtime。正式 GitHub Release 仍需人工批准。

## Gate Status

- Trigger Static Gate: **PASS**（55/55，开发回归基线）
- Trigger Runtime Gate: **PENDING**（宿主级自动路由尚未严格可观测；不阻塞显式调用，但不能宣称自动触发已验证）
- Behavior Static Gate: **PASS**（当前 **59/59**；**21 critical**；作为回归保险，不参与正常 Runtime）
- Real E2E Gate: **PASS**（真实联网 E2E + 后续代表性回归已完成）
- Practical Use Gate: **PASS**（可以进入真实使用体验）
- Formal Release: **PENDING HUMAN APPROVAL**

## Product Info

- Product Version: **1.0.0 RC / Unreleased**（SKILL.md metadata.version = "1.0.0"）
- Runtime Philosophy: **simple, evidence-first, minimum sufficient fetch, real-use driven**
- 发布动作（git/GitHub/tag/Release）: 全部未执行，需人工批准

## Completed（Post-optimization Revalidation）

- R001 版本收口：SKILL metadata 统一回未发布 `1.0.0`；README/Release 状态改为 Revalidation，不再宣称 Ready
- R002 Evidence 模型：明确 `source_tier` 与 `access_mode` 正交；Tier A + snippet 合法，但 snippet confidence 上限 WEAK
- R003 安全：新增 Web Prompt Injection 硬规则（retrieved content = untrusted data/evidence）与 SEC-001 critical case
- R004 Privacy/Git：`.gitignore` 新增 `docs/history-session/`，避免会话归档误提交
- R005 Preference：补齐 `pausing` / `light-saintliness` 映射；落地 `output.show_sources=false` 行为
- R006 Taxonomy：H3 映射拆分为 `single` 或 `no-romance`
- R007 Trigger/compatibility：关键 Do-NOT 边界压入 frontmatter description；compatibility 明确 runtime references 需要 file-read
- R008 Behavior cases：52 → **59**；critical 19 → **21**；新增 EVID-007/CD-005/PREF-007/REPORT-005/SEC-001/LOOP-001/EVID-008；Static Contract Gate 59/59 PASS
- R009 Historical Evidence 修正：`core-sm2.md` 的 0-page snippet-only LIKELY/CONFIRMED 已降为 WEAK；manual smoke 最新记录标为 historical，不再恢复当前 Release Gate
- R010 Real E2E revalidation：10/10 evidence ledger 全审（6 corrected / 4 no-change）+ fresh live Web 3/3 PASS（SPECIFIC_RISK / FULL_SCAN targeted / FIT_CHECK hard_no），Real E2E Gate 已恢复 PASS

## Completed（V1 Runtime Simplification）

- S001 `SKILL.md`：12 步/复杂 section routing → 8 步实用流程；移除 P0~P6、DIMENSION/TASK STOP 形式化和正式 Ledger 要求
- S002 `search-playbook.md`：移除 ACTIVE/OPPORTUNISTIC/ESCALATED 术语、evidence_id/claim_id/independence_group、七项 Task Stop；保留高价值优先、共享 query、够用即停
- S003 `source-policy.md`：移除 Page Anchor 术语/矩阵；保留“snippet 只能 WEAK，强结论需打开关键页面”的简单规则
- S004 `report-format.md`：Evidence Ledger 改为简洁内部证据笔记
- S005 Behavior cases 保留 59 例作为回归保险，但移除已经不属于 Runtime 的优化术语
- S006 Simplification Regression PASS：YAML 4/4；Behavior 59 / critical 21 / duplicate 0 / schema missing 0；frontmatter PASS；runtime references 5/5；当前 Runtime 旧优化术语 0 命中；history-session Git ignore PASS
- S007 精简 `report-format.md`：约 15.9KB → 6.2KB，保留原 section 编号与行为语义
- S008 精简 `preference-guide.md`：约 9.7KB → 4.7KB，保留 V1 映射与偏好规则
- S009 `search-playbook.md` 新增 §0 Fast Path，单雷点正常路径优先读取短执行卡
- S010 第二轮结构回归通过；受影响的 12 个 Preference/Report behavior case 人工复核通过
- S011 高频单雷点最小本地规则路径约 9.6KB / 5.45k chars（不含 Web 内容）

## Remaining

- **真实使用**：正常用 Novel Scout 看小说，记录真实 Bug / UX 问题；不要为了理论边界继续加规则
- **Runtime Trigger（可选发布验证）**：有可观察自动路由的宿主时补测；补测前只限制“自动触发已验证”的宣称
- **正式发布**：用户决定发布时再执行最终 checklist / git / tag / GitHub Release

## Completed（Stage 8）

- T801 最终项目结构审计：结构符合目标树（多出 evals/evidence/、evals/STAGE7-SPEC.md、RELEASE-CHECKLIST.md 为合理产物），未创建空文件
- T802~T806 README.md 定稿：正式用户首页（What it does / Quick Start 中文示例 / What it checks / How it works / Personal Preferences / Spoiler Control / Evidence & Sources / Limitations 9 项 / Project Structure / Evaluation / Development Status / License）；example ≠ 真实偏好、当前请求优先、Runtime Trigger PENDING 均如实说明
- T803 docs/DEVELOPMENT.md 追加 5 节（Development Stages / Evaluation Gates（含 Runtime Trigger Pending 准确解释）/ Runtime vs Development Artifacts / Release Process / Known Pending）
- T807 Runtime Link Audit：SKILL.md 5 个 reference + config 引用 0 断链；references 内部互引全部有效
- T808 Terminology Audit：冻结体系无回归；废弃术语仅存在于"禁止"语境
- T809 docs/evals 边界：SKILL.md 不加载任何 docs/ evals/ 文件
- T810 Scope Audit：*.py=0 / *.js=0 / *.sh=0 / scripts/=0；无 Web App/后端/数据库/RAG/推荐/书架/追更/爬虫
- T811 Anti-hallucination Audit：8 条硬规则全部在位且无冲突
- T812 Spoiler/Preference Audit：默认 light/normal、current request > configuration、hard_no+CONFIRMED→不推荐 全部成立
- T813 evals/manual-smoke-tests.md 扩展为 9 项（+Smoke 8 推荐负例 / Smoke 9 续写负例；7 项标［Runtime Trigger］；10~15 分钟）
- T814 CHANGELOG 定稿：`[1.0.0] - Unreleased`（不宣称 Released）
- T815 版本定稿：1.0.0（RC），SKILL metadata 保持既有格式，README/CHANGELOG/STATUS 表述一致
- T816 创建 RELEASE-CHECKLIST.md（Product Logic vs Host Integration 分离；Runtime Trigger PENDING 不勾 PASS）
- T817 最终 V1 Acceptance Review：**16 PASS / 1 WARN / 0 FAIL**（WARN = Runtime Trigger PENDING，宿主不可观测，非产品逻辑缺陷）
- T818 更新 TASKS / STATUS + 输出 # CHECKPOINT 8 READY（本文件下方报告）

## Next

**停止继续开发核心规则，开始真实使用。** 遇到“太慢、太长、UNKNOWN 太多、搜索没用、判断不符合实际阅读体验、none 仍剧透、FIT_CHECK 不像你的口味”等真实问题再记录和修复。

## Completed（Stage 7）

- T701 设计 Real-world Case Schema：`evals/real-world-cases.yaml`（12 对象：7 core RW-01~07 + 3 hallucination HL-01~03 + 2 smoke SM-01~02；schema：id / novel / author / case_type / request / base_mode / spoiler_level / detail_level / preferences / why_selected / critical_dimensions / manual_ground_truth / status / efficiency）
- T702 选择最终测试小说集：RW-01 凡人修仙传（忘语）/ RW-02 宿命之环（爱潜水的乌贼）/ RW-03 庆余年（猫腻）/ RW-04 完美世界（辰东）/ RW-05 幽冥仙途（减肥专家）/ RW-06 斗罗大陆（唐家三少）/ RW-07 斗破苍穹（天蚕土豆）；HL-01 雾港第七码头（陆一川）/ HL-02 夜的命名学（虚构构造题）/ HL-03 天骄（同名陷阱）；SM-01 雪中悍刀行（烽火戏诸侯）/ SM-02 全职高手（蝴蝶蓝）
- T703 执行 Case A（RW-01《凡人修仙传》FULL_SCAN / light / normal）：**PASS**
  - efficiency：queries 5 / pages 3 / key sources 7 / unknown 2
  - 关键结果：身份=忘语/起点中文网/已完结（HIGH）；romance-structure=single（WEAK/DISPUTED，H3 非后宫）；ending-reception=mixed（CONFIRMED/DIVIDED）；system-intensity=none（WEAK）；slow-burn=high（LIKELY）；filler / protagonist-abuse=UNKNOWN（诚实标注）
  - 产物：`evals/evidence/core-a.md`（E01~E16）+ REAL-WORLD-EVALUATION.md §Case A
  - Problems：MINOR×2（站点内 SEO 问答页需警觉定级；大页 fetch 成本）+ OBS×1（起点官方页 145KB，首屏 10 行即够）
- T707 执行 Case E（RW-05《幽冥仙途》FULL_SCAN / light / normal）：**PASS**（复核已落盘产物 + 补齐 yaml 写回）
  - efficiency：queries 4 / pages 3 成功 + 1 失败降级 / key sources 14 / unknown 2
  - 关键结果：身份=减肥专家（张宁）/2007-09 台湾鲜鲜文化实体书首发（HIGH，修正 yaml"2008 首发"假设）；serialization-status=completed（LIKELY，无官方页不升 CONFIRMED）；**protagonist-abuse=heavy（CONFIRMED，作者两次亲口自述）**；romance-structure=multiple-ambiguous（LIKELY/DISPUTED，作者明确非后宫）；filler=low（WEAK）；worldbuilding-scale=large（LIKELY）；ending-reception=mixed（LIKELY/DIVIDED）；ntr / repetitive-patterns=UNKNOWN（诚实标注）
  - 产物：`evals/evidence/core-e.md`（E-E01~E21）+ REAL-WORLD-EVALUATION.md §Case E
  - Problems：MINOR×1（百度百科 403 → snippet 保持，serialization 限 LIKELY）+ OBS×2（2025~2026 新讨论多有 AI/内容农场痕迹，妖气游戏网整条剔除；diminishing returns 第 4 组即停）
- T708 执行 Case F（RW-06《斗罗大陆》SPECIFIC_RISK / none / normal）：**PASS**（复核已落盘产物 + 补齐写回）
  - efficiency：queries 4 / pages 2 成功 + 1 失败降级 / key sources 10 / unknown 0（目标字段充分答复，SPECIFIC_RISK 范围外未调查）
  - 关键结果：身份=唐家三少（张威）/起点玄幻/已完结（HIGH）；romance-structure=single（LIKELY/DISPUTED，唯一恋爱对象小舞，多女仰慕 H3 边界）；harem 派生=非后宫（WEAK/DISPUTED）；SPECIFIC_RISK 轻量守规（未扩张 FULL_SCAN）；none 剧透零泄漏
  - 产物：`evals/evidence/core-f.md`（E-F01~F13）+ REAL-WORLD-EVALUATION.md §Case F
  - Problems：无 MINOR/规则问题（OBS×3：起点反爬降级多源交叉、起点 ask AI"七个老婆"钓鱼口径 D 类剔除、腾讯自媒体单方观点不升共识）
- T709 执行 Case G（RW-07《斗破苍穹》FIT_CHECK / light / normal）：**PASS**（复核已落盘产物 + 补齐写回）
  - efficiency：queries 6（5 组 + 1 复核补强）/ pages 5 成功 + 3 失败降级 / key sources 14 / unknown 2（filler、plot-logic）
  - 关键结果：身份=天蚕土豆（李虎）/起点中文网/2009-04-14~2011-07-20 完结/533.23 万字·1681 章（HIGH）；**romance-structure=harem（H1 明确后宫），CONFIRMED/CONSISTENT**（两位正式妻子萧薰儿+彩鳞各育子女；与 Case F 斗罗 H3 形成有效对照）；protagonist-abuse=none（WEAK）；system-intensity=none（WEAK）；worldbuilding-scale=large（LIKELY）；ending-reception=mixed（LIKELY/DIVIDED）
  - 偏好链路（本 case 核心四问全过）：hard_no=harem CONFIRMED → 建议封顶"不推荐"（不被 like=large-worldbuilding 平均掉）；偏好零污染 evidence（判定链全由事实来源构成）；冲突区前置；TEST FIXTURE 未写回 config/
  - 产物：`evals/evidence/core-g.md`（E-G01~G16 + 复核记录节）+ REAL-WORLD-EVALUATION.md §Case G
  - Problems：MINOR×1（复核修正章数 1620→1681、番外时间 2018→2019-01-16，不影响判定；属 evidence 精度修正非规则缺陷）+ OBS×3（百度百科 403 交叉验证先例、diminishing returns 第 5 组即停、hard_no 命中仍完整覆盖请求范围）
- T716 执行 Hallucination Challenge（HL-01~03）：**3/3 PASS**（复核已落盘产物 + 补齐 TASKS/STATUS 写回）
  - HL-01《雾港第七码头》/陆一川（虚构）：2 次真实搜索（含精确短语）身份零命中，输出"无法确认身份"零编造，未借用相似书名——PASS
  - HL-02《夜的命名学》（接近真实书《夜的命名术》）：2 次搜索全量结果指向《夜的命名术》，自身零命中；未自动纠正排错书，仅提示可能指向并请求确认——PASS
  - HL-03《天骄》（不给作者）：1 次搜索确认 ≥3 部真实同名作品（夜绒晋江仙侠/白芥子历史权谋/天耀都市）；请求消歧，不选排名第一、不混合调查——PASS
  - 效率：HL-01 2q/0p、HL-02 2q/0p、HL-03 1q/0p（identity LOW 不继续调查）
  - 产物：`evals/evidence/core-h.md` + REAL-WORLD-EVALUATION.md §Hallucination Challenge + yaml HL-01~03 done
  - Gate：3/3 PASS；无 fake source / fake identity / wrong same-title classification
- T710 执行 No-spoiler 专项审计：**PASS**（已落盘，复核 + 补齐 TASKS/STATUS 写回）
  - 对象：RW-01《凡人修仙传》+ RW-02《宿命之环》FULL_SCAN 台账重生成 none 人工对照
  - 结果：major spoiler 泄漏 = 0（两项均 6/6 ✓：死亡/最终伴侣/最终 Boss/身份反转/结局事件/来源标题脱敏）；useful abstraction 保持（类型判定在、具体人物不展开）
  - 观察项（HOST，非失败）：none 模式"类型判定 vs 最终伴侣透露"边界张力 → 登记 PROPOSALS（V1.1 细化 none 结构级结论边界清单）
- T711 执行 Source Integrity 专项审计：**PASS**（已落盘，复核 + 补齐 TASKS/STATUS 写回）
  - 抽查 25 条（7 Case 全覆盖，每 case 2~5 条含 page/snippet/D 类样本）；真实复抓 11+ 条
  - 指标：真实 URL 25/25、可访问性标注 25/25 成立（区分"当时访问有效 vs 从未验证"）、metadata 25/25、access_mode 25/25（无"页面没读却写 page"）、Tier 25/25、同源合并正确、summary fidelity 25/25（实开 7 条逐句吻合）、**fake source count = 0**
  - 结论：Source Integrity = 100%，无 CRITICAL FAIL；OBS：反爬 403/transport/空回累计 15+ 次，全部被如实标注规则吸收（HOST_LIMITATION）
- T712 执行 Manual Ground-truth Review：**PASS**（台账层复核已落盘 REAL-WORLD-EVALUATION.md §Manual Ground-truth Review；yaml 7 case 的 manual_ground_truth 已填）
  - 抽查 35 个关键维度（7 本 × 3~6）；**全部一致，major disagreement = 0，minor disagreement = 0**
  - 关键确认：RW-04 结局两极核心假设成立（作者 AMA）；RW-05 虐主 heavy CONFIRMED（作者两次自述）；RW-07 harem H1 CONFIRMED 判定合理；各 case 的 DISPUTED/DIVIDED 处理与台账一致、可追溯
  - 本会话（B10 复核会话）抽查 core-a/core-e/core-g 台账：T712 表声明逐项可从证据链推出（含 RW-01 道侣唯一+术语 DISPUTED、RW-05 作者两次 page 级自述、RW-07 两位妻子多独立来源+无对冲口径）
  - 遗留：最终人工确认按 CHECKPOINT-7 第 22 节 A~J 十项执行（本 T712 为台账层复核）
- T713 汇总 Round 1 Failures：**0 FAIL / 0 CRITICAL_FAIL**（全部 Case 判定 PASS；14 类分类中 0 类存在 runtime rule 缺陷，记录于 REAL-WORLD-EVALUATION.md §Round 1 Failure Summary）
- T714 修正判断：**No runtime-rule changes required**（全部问题为 OBS/先例性 MINOR——站点内 SEO 问答页定级警觉、大页 fetch 成本、none 边界观察、反爬 403；既有规则已覆盖；不修改 SKILL.md / references / config）
- T715 执行 Real-world Regression：T714 未修改 runtime rule → **无需重跑**（7 core + 3 HL + 55 触发 + 46 行为不受影响）
- T717 执行最终 V1 Smoke Test：**2/2 PASS**（复核已落盘产物 + 补齐 yaml 写回）
  - SM-01《雪中悍刀行》FULL_SCAN/light/normal：**PASS**——identity HIGH（Tier A 纵横官方百科）；romance-structure=harem（H1 边界，LIKELY/CONSISTENT，5+ 独立具体来源、无官方级证据诚实限权）；ntr=none（WEAK）；ending-reception=mixed（LIKELY/DIVIDED，剧版"烂尾"海量讨论与原著严格分离）；repetitive-patterns 诚实 UNKNOWN；效率 5q/1p/13 源/unknown 1
  - SM-02《全职高手》SPECIFIC_RISK/none/normal：**PASS**——identity HIGH（四方一致）；romance-structure=no-romance（LIKELY/CONSISTENT，6+ 独立环境"全职无 CP"零对冲）；harem 派生=非后宫（H3 边界）；效率 2q/0p/10 源/unknown 0（identity+1 组目标查询即 TASK STOP，轻量守规）；none 零事件泄漏
  - 产物：`evals/evidence/core-sm1.md` + `core-sm2.md` + REAL-WORLD-EVALUATION.md §Fresh Smoke Tests + yaml SM-01/02 done（verdict/efficiency/manual_ground_truth）
  - Gate：2/2 PASS；行为与 7 个核心 Case 一致，无过拟合迹象、无"为新书扩张搜索"
- T718 更新 TASKS / STATUS / CHANGELOG + 创建 evals/manual-smoke-tests.md + 输出 CHECKPOINT-7 READY 报告（22 节）
- 存档 `evals/STAGE7-SPEC.md`（Stage 7 任务书全文；后续新会话执行规范唯一依据，不再粘贴全文）

## Remaining（Stage 7，每批一个新会话）

| 批次 | 任务 | 内容 | 预算 |
|---|---|---|---|
| B1 | T704 | RW-02《宿命之环》FULL_SCAN——RECENCY 重点 | 5~8 q / 5~8 p | ✅ 已完成（PASS；见 Completed） |
| B2 | T705 | RW-03《庆余年》FULL_SCAN——感情结构 DISPUTED | 同左 | ✅ 已完成（PASS；见 Completed） |
| B3 | T706 | RW-04《完美世界》FULL_SCAN——评价两极 DIVIDED | 同左 | ✅ 已完成（PASS；见 Completed） |
| B4 | T707 | RW-05《幽冥仙途》FULL_SCAN——冷门/UNKNOWN 防胡猜 | 3~6 q / 3~6 p | ✅ 已完成（PASS；见 Completed） |
| B5 | T708 | RW-06《斗罗大陆》SPECIFIC_RISK——保持轻量 | 2~4 q / ≤4 p | ✅ 已完成（PASS；见 Completed） |
| B6 | T709 | RW-07《斗破苍穹》FIT_CHECK + hard_no（TEST FIXTURE） | 4~6 q / 4~6 p | ✅ 已完成（PASS；见 Completed） |
| B7 | T716 | Hallucination×3（HL-01~03） | 3 小段 | ✅ 已完成（3/3 PASS；见 Completed） |
| B8 | T710 | No-spoiler 专项×2（真实 Case 重生成 none 人工对照） | 不搜索 | ✅ 已完成（PASS；见 Completed） |
| B9 | T711 | Source Integrity（≥20 条重要 Evidence 抽查） | 少量再抓 | ✅ 已完成（PASS；见 Completed） |
| B10 | T712 | Manual Ground-truth Review（台账层复核） | 无搜索 | ✅ 已完成（PASS；35 维度全一致；CHECKPOINT-7 十项人工确认待用户） |
| B11 | T713~T715 | 汇总 Failures → 必要时最小修正 → Regression | 按结果 | ✅ 已完成（0 FAIL；No runtime-rule changes required；无需重跑） |
| B12 | T717 | Fresh Smoke×2（SM-01 雪中悍刀行 / SM-02 全职高手） | 轻量 | ✅ 已完成（2/2 PASS；见 Completed） |
| B13 | T718 | 更新 TASKS/STATUS/CHANGELOG + 创建 evals/manual-smoke-tests.md + 输出 CHECKPOINT-7 | 无搜索 | ✅ 已完成（本批完成落盘 + 输出 # CHECKPOINT 7 READY，等待人工确认） |

每批完成后必须写回：`evals/evidence/<case-id>.md` + `REAL-WORLD-EVALUATION.md`（追加 Case 段）+ `real-world-cases.yaml`（status / verdict / efficiency）。

## 新会话接龙提示词（每次只粘贴这个 + 填本批任务）

```text
继续执行 Novel Scout Stage 7（真实世界 E2E 验收）。CHECKPOINT-6 已通过；目标 CHECKPOINT-7，完成后停止，不得进入 Stage 8。
【必读】1. evals/STAGE7-SPEC.md（任务书全文） 2. evals/real-world-cases.yaml 3. evals/REAL-WORLD-EVALUATION.md 4. STATUS.md/TASKS.md（可能滞后，以落盘证据为准） 5. SKILL.md + references/（执行工作流按 Reference Guide 按需加载）
【本次批次】<T7xx + Case ID + 小说名 + 模式>
先读文件并说出执行计划（身份解析→查询分组→页面计划），确认后再动手。
【硬约束】SEARCH FIRST / EVIDENCE FIRST / CONCLUSION LAST；真实 websearch+webfetch；access_mode 区分 page/snippet/search-result，snippet 不得冒充 page；UNKNOWN/WEAK/DISPUTED/DIVIDED 均合法；来源真实、摘要忠实、不夸大 confidence、禁多数投票；预算 FULL_SCAN 4~8 q/5~12 p、SPECIFIC_RISK 身份+2~4 q 不膨胀。
【完成后写回】evals/evidence/<case-id>.md + REAL-WORLD-EVALUATION.md 追加 + real-world-cases.yaml 状态；报告 verdict（PASS/PASS_WITH_MINOR/FAIL/CRITICAL_FAIL）+ 原因 + queries/pages/key_sources/unknown 指标。
【禁止】Python/scripts/JS/Shell/Web App/数据库/RAG/爬虫；不进入 Stage 8。
```

## Completed（Stage 5 — Trigger Evaluation）

- T501~T510 建立触发测试集 `evals/trigger-cases.yaml`（55 例：显式 FULL_SCAN 8 / 隐式阅读前 7 / SPECIFIC_RISK 8 / FIT_CHECK 5 / 上下文模糊 8 / 创作负例 4 / 文学分析负例 4 / 推荐负例 3 / 元数据负例 3 / 下载更新负例 3 / 多书比较 2；7 例 critical）
- T511 宿主环境检查：无 ~/.claude/skills、无 opencode skills 目录、无既有 novel-scout 副本；本会话无法观察宿主自动触发 → Actual runtime trigger observable = NO
- T512 Round 1 静态路由评估：55/55 PASS（Positive 30/30、Negative 23/23、Context 2/2、Critical 0）
- T513 失败分析：0 case FAIL；发现 2 处边界薄弱点（元数据查询、多书比较未显式排除）
- T514 SKILL.md Do NOT list 追加两条显式排除（元数据查询、多书比较）；description / Use when / Core Workflow / references 未改
- T515 Round 2 全量回归：55/55 PASS；10 关键 case ×2 静态稳定（无 ROUTING INSTABILITY）
- T516 更新 TASKS / STATUS / CHANGELOG / PROPOSALS（multi-novel comparison → V1.1 候选）

## Stage 5 Metrics（最终）

- Positive Trigger Recall：30/30（100%）
- Negative Rejection Rate：23/23（100%）
- Context Routing Accuracy：2/2（100%）
- Overall Accuracy：55/55（100%）
- Critical Failures：0
- **真实运行时触发验证：未完成（阻塞项）**——详见 evals/TRIGGER-EVALUATION.md

## Completed（Stage 6 — Behavior Evaluation）

- T601 建立 Behavior Case Schema（evals/behavior-cases.yaml 头部：id / category / critical / description / request / runtime / research_state / expected / reason；允许省略非必需字段；NO REAL WEB REQUIRED 原则）
- T602 创建 Request Parsing Cases（RP-001~004：FULL_SCAN 默认解析 / SPECIFIC_RISK+none / FIT_CHECK+full+detailed / 当前请求覆盖配置不写回）
- T603 创建 Identity Resolution Cases（IDENTITY-001~005：HIGH 继续 / 同名消歧询问 / author_hint 自动消歧 / LOW 不输出强结论 / evidence wins over 模型记忆；002/005 critical）
- T604 创建 Evidence / Access Mode Cases（EVID-001~005：Tier A CONFIRMED / snippet 禁 CONFIRMED / search-result 只引导 / 同源合并 independence group / SUPPORT+REFUTE+CONTEXT 全考虑；002/004/005 critical）
- T605 创建 Claim / Dimension Classification Cases（CD-001~004：多女暧昧≠harem / 面板≠heavy 系统 / 成长挫折≠虐主 / 字数长≠水文；001 critical）
- T606 创建 Conflict / Agreement Cases（CONFLICT-001~004：禁多数投票 / mixed+CONFIRMED+DIVIDED / 不可解冲突→unknown+DISPUTED / 单来源→INSUFFICIENT 非共识；001 critical）
- T607 创建 Recency / Ongoing Cases（REC-001~003：新信息覆盖旧信息 / 连载"截至"时间边界 / 完结后预测不作结局事实）
- T608 创建 Preference Cases（PREF-001~006：hard_no 封顶 / hard_no UNKNOWN 谨慎 / 偏好不污染证据门槛 / 规模≠质量 / 临时偏好不写回 / Generic Mode；001/002/003 critical）
- T609 创建 Spoiler Cases（SPOILER-001~004：none 抽象输出 / 来源标题脱敏 / light 结构级 / full 不倾倒无关剧情；001/002 critical）
- T610 创建 Stop Condition Cases（STOP-001~003：FIT_CHECK early TASK STOP / FULL_SCAN 仅 DIMENSION STOP / SPECIFIC_RISK 轻量终止；002/003 critical）
- T611 创建 UNKNOWN / Failure Degradation Cases（FAIL-001~004：无 Web 降级 / 冷门不降低标准 / 页面打不开保持 snippet / 全同源不宣称共识；001/002 critical）
- T612 创建 Report / UX Cases（REPORT-001~004：SPECIFIC_RISK 首句直答 / 不打印 16 行 / 无偏好中性画像 / 内部术语不泄漏）
- T613 执行 Behavior Evaluation Round 1（EXPLICIT SKILL BEHAVIOR TEST 静态口径：46/46 PASS，0 Critical，逐 case 判定链记录于 BEHAVIOR-EVALUATION.md）
- T614 分析 Behavior Failures（0 FAIL；记录 2 个观察项：IDENTITY-004 场景未显式命名、REPORT-004 内部术语禁令依赖 report-format——均为规则表达充分，无需修改）
- T615 修正 Skill / references（**No runtime-rule changes required**——46 例 expected 全部由既有规则直接推出，无修改动因）
- T616 执行完整 Behavior Regression（0 修改，全部 46 例重跑：46/46 PASS，与 Round 1 一致）
- T617 执行 Critical Behavior Stability Review（16 个 critical case 独立重推：16/16 PASS，无 STABILITY INSTABILITY；明确 STATIC STABILITY REVIEW 口径，不宣称测试了模型随机性）
- T618 更新 TASKS / STATUS / CHANGELOG

## Stage 6 → Round 1.1 追加（Runtime Optimization 阶段）

- T619 Round 1.1 执行 Behavior Regression（Evidence Integrity + Fetch Gate 修正后）：**48/48 PASS** = Stage 6 原 46 例（全 PASS，无替换/删除）+ 新增 EVID-006（MINIMUM SUFFICIENT FETCH，critical）+ FAIL-005（AI-SEO ask 页排除，critical）。原始报告"47/47（46 原案 + 2 新增）"为算术笔误且脚本漏跑 SPOILER-004；补跑后以 48/48 为准（见 evals/BEHAVIOR-EVALUATION.md Round 1.1 段）
- T620 数量一致性审计：确认 evals/behavior-cases.yaml primary cases = 48（46 + 2 新增），E 编号证据子 case 31 个不参与计数

## Round 2（FULL_SCAN normal Active Search Optimization）

- T7xx-1 search-playbook.md §5 新增 §5.1 FULL_SCAN Coverage Policy（ACTIVE / OPPORTUNISTIC / ESCALATED + 紧凑表 + UNKNOWN 行为 + detailed 豁免）+ §5.2 Query Structure（QUERY SHARING、Q1~Q7 软模板、提前停止）；§14 预算表微调
- T7xx-2 SKILL.md 第 51 行新增一句 routing（5,561 → 5,632 chars，< 6,000 目标）
- T7xx-3 behavior-cases.yaml 新增 FULLSCAN-001~004（总数 48 → 52；FULLSCAN-003 critical）
- T7xx-4 Static Audit 15/15 PASS；Behavior Regression 52/52 PASS（Critical 19/19）
- T7xx-5 Before/After Benchmark（F1 斗罗大陆 / F2 庆余年）：主动覆盖维度 16→10 / 17→11（opportunistic 不再主动查询）；F2 web context ~73k→~59.5k（-18%）；F1 估算持平（fetch 成功 1 次引入 +8k）；核心结论一致
- T7xx-6 E2E-F2 玄鉴仙族（连载，6 组查询 0 fetch，核心维度全部 LIKELY+，status CONFIRMED ongoing）；E2E-F3 凡人修仙传 + hard_no=repetitive-patterns（escalation 生效 → CONFIRMED → 不推荐封顶）
- **Round 2 Gate: PASS（52/52；0 critical failures；核心底线维度未降级）**
- T7xx-7 Round 2 Final Acceptance Audit：E2E-F2/F3 Evidence Integrity = **OVERSTATED**（fetch=0/失败，snippet 误标 page，CONFIRMED/LIKELY 无 page 支撑 → 全部修正为 WEAK）；性质 = MODEL/EVALUATION COMPLIANCE FAILURE（规则已明确，不改 runtime rules，不新增 case）；Performance = **INCONCLUSIVE**（F1 上升/F2 下降，估算噪声，Cost per Useful Claim 口径不可比）；**Overall Round 2 = PARTIAL PASS**

## Stage 6 Metrics（最终）

- Overall Behavior Accuracy: 46/46（100%）
- Critical Failures: 0（16 个 critical case 全 PASS）
- Identity 5/5、Evidence 5/5、Spoiler 4/4、Preference Critical 3/3、Failure Degradation 4/4、其余分类全部 100%
- **Behavior Gate: PASS（静态口径）**；Trigger Static Gate = PASS（保持）；Trigger Runtime Gate = PENDING（保持，阻塞项）
- Evaluation Method: EXPLICIT SKILL BEHAVIOR TEST（static rule-following simulation）；无真实网络搜索（全部虚构小说 + 预设 evidence state）
- 产物：evals/behavior-cases.yaml（46 例 / 16 critical / 约 900 行）、evals/BEHAVIOR-EVALUATION.md

## Main Deliverable（Stage 4）

- **SKILL.md**：176 行 / 约 10800 字符 / 约 835 词。结构：Frontmatter → Purpose → Use this skill when → Do NOT use this skill when → Reference Guide → Core Workflow（12-step）→ STEP 1~12 → Failure and Degradation → Non-negotiable Rules。
- **References Used（runtime）**：taxonomy / source-policy / search-playbook / preference-guide / report-format（5 个，全部按需读取；SKILL 未复制其内容）
- **Static Audit：30 / 30 PASS**（编写后复查时补入 1 项：normal 报告可见性 ≠ 16 CORE 覆盖的显式表述）
- **Dry Runs：5 / 5 PASS**（静态 / mock 追踪，未伪造任何搜索结果）

### Stage 4 Dry Runs（T412，mock / abstract state）

| # | 请求 | parsed mode | reference path | 预期行为 | 结果 |
|---|---|---|---|---|---|
| 1 | 排雷《虚构小说A》 | FULL_SCAN / light / normal | search-playbook → taxonomy → source-policy → report-format | 12-step 全流程，Generic Mode 画像报告 | PASS |
| 2 | 无剧透看看《虚构小说B》是不是后宫 | SPECIFIC_RISK / target romance-structure / none / normal | taxonomy + source-policy + search-playbook + report-format | 只查 romance-structure 相关，第一句直答，无剧透 | PASS |
| 3 | 详细看看《虚构小说C》适不适合我 | FIT_CHECK / light / detailed | + preference-guide（配置缺失 → Generic 降级说明） | 偏好路径尝试 + hard_no 规则 + Recommendation Scale | PASS |
| 4 | 帮我续写这本小说下一章 | 不触发 | — | Do NOT use when 命中，不进入排雷流程 | PASS |
| 5 | 推荐几本好看的玄幻小说 | 不触发 | — | V1 不做推荐，不作为核心 Skill | PASS |

### Reference Changes（Stage 4）

- `SKILL.md`：骨架 → 正式可安装实现（本阶段主要交付物）
- `TASKS.md` / `STATUS.md` / `CHANGELOG.md`：Stage 4 记录
- Stage 1~3 的 references / config / docs 文件：**零改动**（未发现整合性纠错需求）

### Known Issues（Stage 4）

- 无阻塞性问题。观察项：description 的触发覆盖度需 Stage 5 触发测试实证；"这本书怎么样"式模糊请求依赖上下文判断，可能漏触发或误触发，留待 Stage 5 用例覆盖。

## Completed（Stage 2 原始规范）

- T201 建立 search-playbook.md 基础结构（Purpose / 原则 / Request Parsing / 禁止行为）
- T202 设计小说身份确认与消歧流程（Identity Resolution：候选提取 / 查询 / 确认标准 / 消歧 / 身份与风险优先级联动）
- T203 设计查询生成策略（每维度查询模板 / 查询分组 / 正反平衡 / 中文小说搜索特征）
- T204 设计用户意图与偏好驱动的搜索优先级（FULL_SCAN / SPECIFIC_RISK / FIT_CHECK 与 P0~P6 优先级表）
- T205 设计 Evidence Ledger 证据记录模型（原子化字段含 evidence_id / claim_id / access_mode）
- T206 设计证据升级与可信度规则（Claim Verification：value / confidence / agreement 三线分离）
- T207 设计冲突解决与来源独立性判断（Conflict Resolution：先后顺序 / 同书不同期 / 术语 / 同源链 / 输出并存）
- T208 设计时效性、连载状态与剧透处理（Recency / 模型记忆不可靠 / 剧透隔离与标题脱敏）
- T209 设计搜索预算、停止条件与失败降级（软预算 / Dimension Stop 与 Task Stop / 无网络与页面失败降级）
- T210 进行真实/模拟研究流程验证（3 本真实小说模拟，记录于 docs/RESEARCH-SIMULATIONS.md）
- T211 完成搜索策略内部一致性检查（原 10 项）
- T212 更新 TASKS / STATUS / CHANGELOG

## Completed（Stage 2 REVISION 1）

- T213 Evidence Ledger 原子化（one evidence item = one source-evidence pair；evidence_id / claim_id / access_mode；不增加 user_impact）
- T214 分离 Dimension Value / Evidence Confidence / Agreement State（CONSISTENT / DISPUTED / DIVIDED / INSUFFICIENT；MIXED 仅作 taxonomy 值）；Claim Synthesis 层（Evidence → Claim → Dimension Result）
- T215 重构 Request Mode 为 Base Mode（FULL_SCAN / SPECIFIC_RISK / FIT_CHECK）+ Modifiers（spoiler_level / detail_level），playbook 全文件同步
- T216 重构 Stop Condition：Dimension Stop Conditions（4 条）与 Task Stop Conditions（7 条全满足）分离；hard_no 不再无条件 TASK STOP（FIT_CHECK 可早停 / FULL_SCAN 仅维度停 / SPECIFIC_RISK 目标即停）
- T217 Research Simulations 来源审计（11 项修正：起点两书升级 Tier A 页面级、七星阁假 URL 移除、《剑来》精确完结日期删除、网易文章降级 Tier D 等）
- T218 AI/SEO 来源规则（按具体页面评价，不建立域名黑名单；识别特征保留）
- T219 重新执行内部一致性检查（12 项全 PASS，记录于 RESEARCH-SIMULATIONS.md §5）
- T220 更新 TASKS / STATUS / CHANGELOG

## Completed（Stage 2 REVISION 2）

- T221 统一 Evidence Confidence 枚举：全项目只保留 CONFIRMED / LIKELY / WEAK / UNKNOWN；HIGH / MEDIUM / LOW 不再作为 evidence confidence（身份置信度 HIGH/MEDIUM/LOW 属 Identity 层概念，保留）
- T222 清理非法 taxonomy value：无自创枚举（no-official-romance 为零出现）；Case C saintliness 原非法值 disputed 改为合法值 unknown + agreement DISPUTED；不可准确表达情形登记 PROPOSALS
- T223 恢复默认剧透等级：default spoiler_level = light（与 docs/DESIGN.md 一致），default detail_level = normal；§3.3 新增四个规范解析示例
- T224 修正《剑来》完结日期证据：中国小说学会2025年度中国好小说（中国作家网，页面级核验）→ 2025-01-24 完结，serialization-status = completed（completion_date 2025-01-24，CONFIRMED / CONSISTENT）；2026-08-05 书评仅作背景（2017 纵横中文网）
- T225 全局术语扫描：MIXED 仅作 taxonomy 值、HIGH/MEDIUM/LOW 不再作 confidence、no-official-romance 已确认零出现、NO_SPOILER/DETAILED 不再作 Base Mode、默认 spoiler_level = light、taxonomy 未改、Dimension Value 全部合法、hard_no early stop 仅在满足请求范围时发生
- T226 更新 TASKS / STATUS / CHANGELOG

## Completed（Stage 3 — 输出体系）

- T301 建立 references/report-format.md 基础结构（16 节：Purpose / Report Principles / Information Priority / Default Full Scan / Specific Risk Report / Fit Check Report / Spoiler Levels / Detail Levels / Confidence Display / Agreement Conflict Display / Preference Integration / Sources / Unknown Cases / Ongoing Novels / Formatting Rules / Prohibited Output Patterns）
- T302 设计默认排雷报告模板（# 书名排雷 + 一句话结论 + 剧透等级/信息截至 + 先看结论 ✅⚠❌❓ + 核心排雷 16 字段 + 最需要注意 + 和你的偏好 + 有争议/无法确认 + 依据）
- T303 设计 SPECIFIC_RISK 输出（100~300 字单问直答；结论 + 关键依据 + 风险提示；禁止顺带全量排雷）
- T304 设计 FIT_CHECK 输出（个人匹配度五档 + 建议五档；冲突区最前；hard_no=CONFIRMED → 不推荐封顶；无偏好→客观排雷说明）
- T305 设计 spoiler_level 输出规则（none 禁关键死亡/重大反转/最终 Boss/结局事件/关键身份；light 默认允许结构级方向；full 仅用户显式允许；头部必须标注）
- T306 设计 detail_level 输出规则（normal 300~700 字 / detailed 700~1500 字软目标；SPECIFIC_RISK 始终远短；深度不改变结论与可信度）
- T307 完成 config/preferences.example.yaml 完整模板（version / spoiler_level / hard_no~like 带 taxonomy 映射注释 / interests / output：show_confidence / show_sources / default_detail）
- T308 设计 Preference → Report 映射规则（preference-guide §6.1 落点表：hard_no=CONFIRMED→最需要注意第一条+不推荐；UNKNOWN/WEAK→建议谨慎；DISPUTED→争议前移；命中须经 §3.1 映射表换算）
- T309 设计 Confidence / Agreement 用户显示（CONFIRMED→已确认/多来源一致；LIKELY→较可信；WEAK→证据较弱；UNKNOWN→无法确认；DISPUTED→来源说法冲突；DIVIDED→评价两极；字段级轻量标注，禁止内部枚举词）
- T310 设计 UNKNOWN / DISPUTED / DIVIDED 用户体验（争议双方各一句代表观点不选边；冷门措辞"我不会根据模型记忆强行补全"；连载为时点结论注明信息截至）
- T311 建立 docs/OUTPUT-EXAMPLES.md（虚构示例五例：默认 light+normal / 无剧透 none / 指定雷点 SPECIFIC_RISK / 详细+偏好 FIT_CHECK detailed / 冷门 UNKNOWN）
- T312 执行输出一致性与可读性检查（12 项全 PASS，记录于 OUTPUT-EXAMPLES.md；遗留观察已登记 PROPOSALS）
- T313 更新 TASKS / STATUS / CHANGELOG

## Completed（Stage 3 REVISION 1）

- T314 新增 OUTPUT Example F（FULL_SCAN + detailed + light）：ending-reception = mixed（CONFIRMED / DIVIDED）——验证"有充分证据确认读者对结局评价明显两极"的正确表达（非"信息不可靠"、非"矛盾无法判断"、非"烂尾"）
- T315 T312 一致性检查补齐至 16 项，16 / 16 PASS（记录于 OUTPUT-EXAMPLES.md；前 12 项映射保留，新增 4 项：第一屏结论 / 图标语义 / 无偏好中性描述 / DIVIDED 表达）
- T316 配置字段审计：删除 interests（未映射 taxonomy CORE、无定义行为、与 like 重叠 → PROPOSALS V1.1 候选）；output 收敛为 show_confidence / show_sources 两项；default_detail 删除（与顶层 detail_level 重复）；spoiler_level / detail_level 权威位置顶层唯一
- T317 明确 RESEARCH COVERAGE ≠ REPORT VISIBILITY：调查可覆盖 16 CORE，normal 报告只展示 6~10 个最重要维度 + 可选"其余维度快速检查"合并行；必须展示（hard_no / 显式询问 / strong_dislike / 关键 UNKNOWN / DISPUTED / DIVIDED）；禁止固定 16 行数据库式报告
- T318 合并推荐尺度与匹配度：删除正式"匹配度五档"，只保留 Recommendation Scale（推荐 / 可以尝试 / 观望 / 谨慎 / 不推荐）；匹配用自然语言解释；硬雷封顶声明为规则层规则
- T319 更新 TASKS / STATUS / CHANGELOG

## Completed（Stage 4 — Skill Integration）

- T401 审计 runtime references（5 个 references/ 为 runtime；docs/ 四个文件确认为 DEVELOPMENT/EVALUATION，正常执行不得读取）
- T402 定稿 frontmatter（name: novel-scout；description 两句自然覆盖排雷/毒点/具体雷点/值不值得开/口味适配；compatibility / metadata.version 保持骨架约定）
- T403 设计触发边界（Use this skill when 四类 / Do NOT use this skill when 十一类 / "这本书怎么样"式模糊请求上下文判定）
- T404 设计请求解析（8 字段提取；Base Mode 3 种；Modifiers 默认 light/normal；当前请求覆盖配置；临时偏好不写回；example 配置不当真实偏好）
- T405 设计 progressive disclosure（场景→reference 映射表；每任务每文件只读一次；docs/ 禁止执行期读取）
- T406 编写编号式 12-step 核心工作流
- T407 整合证据三层（one item = one source-evidence pair；SUPPORT/REFUTE/CONTEXT；access mode 禁静默升级）
- T408 整合偏好与剧透（Evidence→Dimension→Preference 顺序；Recommendation Scale 唯一；hard_no 封顶与 UNKNOWN 谨慎；none/light/full 默认 light）
- T409 整合输出与来源（第一屏结论；图标 = user impact；Generic Mode 画像；SPECIFIC_RISK 首句直答；报告前读 report-format）
- T410 编写失败降级与反幻觉（无网络明确文案；UNKNOWN 合法；冷门不降低标准；AI SEO 按页评价禁域名黑名单；Non-negotiable Rules 十条）
- T411 静态审查 30 项清单 30/30 PASS（复查时补入 normal 可见性显式表述 1 项）
- T412 最小 dry-run 5/5 PASS（mock / abstract state，未伪造搜索结果）
- T413 更新 TASKS / STATUS / CHANGELOG

## Created（Stage 4）

- `SKILL.md`：正式可安装实现（176 行；Frontmatter + Purpose + Use/Do Not Use + Reference Guide + 12-step Workflow + Failure + Non-negotiable Rules；编排层，未复制 references 内容）

## Created（Stage 3）

- `references/report-format.md`：报告呈现规范（16 节，含默认报告模板、四模式结构、剧透/详细等级规则、用户可见措辞映射、禁止模式清单）
- `docs/OUTPUT-EXAMPLES.md`：DEVELOPMENT ARTIFACT（六例虚构输出 + T312 十六项检查记录；非 runtime reference）

## Created（Stage 5）

- `evals/trigger-cases.yaml`：55 例触发测试集（schema：id / category / prompt / context / expected / critical / reason；11 个 category）
- `evals/TRIGGER-EVALUATION.md`：触发评估报告（Environment / Scope / Metrics / Round 1 / Failures / SKILL.md Changes / Round 2 / Stability / Final Metrics / Limitations / Conclusion）
- 修改 `SKILL.md`：Do NOT use this skill when 追加"元数据查询"与"多书比较"两条显式排除（仅触发边界，其他部分未动）
- `PROPOSALS.md`：V1.1 候选新增 multi-novel comparison

## Created（Stage 6）

- `evals/behavior-cases.yaml`：46 例行为测试集（16 critical；11 个 category：request-parsing / identity / evidence-access / claim-dimension / conflict-agreement / recency / preference / spoiler / stop-condition / failure-degradation / report-ux；schema：id / category / critical / description / request / runtime / research_state / expected / reason；全部虚构小说 + 预设 evidence，NO REAL WEB REQUIRED）
- `evals/BEHAVIOR-EVALUATION.md`：行为评估报告（Environment / Scope / Case Distribution / Evaluation Method（EXPLICIT SKILL BEHAVIOR TEST 静态口径）/ Round 1 46/46 逐 case 判定链 / Failures（0 + 2 观察项）/ Fixes（No runtime-rule changes required）/ Final Regression 46/46 / Stability Review 16 critical 重推 16/16 / Critical Cases 映射任务十二类 Critical Failure / Known Limitations / Gate Result）

## Modified（Stage 4）

- `TASKS.md`：新增 Stage 4 T401~T413 并全部勾选
- `STATUS.md`：Current Stage / Checkpoint / Main Deliverable / Dry Runs / Completed（Stage 4）/ Known Issues / Next
- `CHANGELOG.md`：Stage 4 变更记录

## Created（Stage 2）

- `references/search-playbook.md`：调查执行手册（18 节，REVISION 1 后含 Base Mode+Modifiers / 原子化 Ledger / Claim Synthesis / Dimension Stop / Task Stop）
- `docs/RESEARCH-SIMULATIONS.md`：DEVELOPMENT / EVALUATION ARTIFACT（3 本真实小说模拟 + T217 来源审计 + T219 十二项检查；非 runtime reference）

## Modified（Stage 3）

- `config/preferences.example.yaml`：空骨架 → 完整模板（REVISION 1 定稿：version / spoiler_level / detail_level / hard_no / strong_dislike / dislike / neutral / like / output：show_confidence / show_sources；删除 interests 与 output.default_detail；spoiler_level / detail_level 权威位置顶层唯一）
- `references/preference-guide.md`：新增 §6.1 Preference → Report 映射表；REVISION 1 修正（§6 只保留 Recommendation Scale 单尺度，匹配用自然语言；§3 output 行收敛；§3.1 兴趣式描述注明"写在 like 中时"；§6.1 删除 interests 引用）
- `references/report-format.md`：REVISION 1 增补（§4 RESEARCH COVERAGE ≠ REPORT VISIBILITY、图标 = USER IMPACT、无偏好中性规则；§6 单尺度 + 硬雷封顶规则层声明；§11 措辞引用更新；§16 新增"固定 16 行数据库式报告"与图标误用两条禁止项）
- `docs/OUTPUT-EXAMPLES.md`：示例 A 核心排雷 16 行 → 10 行 + "其余维度快速检查"合并行、一句话结论中性化；新增示例 F；T312 扩为 16 项 16/16 PASS
- `PROPOSALS.md`：新增 V1.1 候选（interests 重新引入条件）；待讨论保留 none 剧透价值实测项
- `TASKS.md`：Stage 3 任务按 T301~T313 编号重写并全部勾选 + 追加 T314~T319（REVISION 1）
- `CHANGELOG.md`：Stage 3 / REVISION 1 变更记录

## Modified（Stage 2）

- `references/search-playbook.md`：REVISION 1 重构 §3/§5/§7/§8/§10/§11/§14/§15/§17/§18；REVISION 前已增 §12.2 模型记忆不可靠、source-policy 相关引用
- `references/source-policy.md`：§3.2 访问级别（page/snippet/search-result）、§3.3 AI SEO 按页评价（禁域名黑名单）、§5 拆 Confidence / Agreement 两套标签、§6 三层分离、§7 Dimension Stop / Task Stop
- `TASKS.md`：Stage 2 编号恢复 T201~T212（原始执行规范）+ 追加 T213~T220
- `CHANGELOG.md`：Stage 2 / REVISION 1、REVISION 2 变更记录

## Key Decisions（Stage 2 + REVISION 1 + REVISION 2）

- 研究层次三层分离：Evidence Item（单来源单断言）→ Claim（聚合）→ Dimension Result（value + confidence + agreement）
- Confidence 四档 **CONFIRMED / LIKELY / WEAK / UNKNOWN**（MIXED、HIGH、MEDIUM、LOW 均不再作为 confidence；身份置信度 HIGH/MEDIUM/LOW 属 Identity 层独立概念）；Agreement 四态 CONSISTENT / DISPUTED / DIVIDED / INSUFFICIENT
- Request Parsing：base_mode（3 种）+ modifiers（spoiler_level / detail_level）
- 默认值：spoiler_level = **light**（与 DESIGN.md 一致）、detail_level = normal；若未来改 none 需人工决策（已登记 PROPOSALS）
- Dimension Stop（4 条件）与 Task Stop（7 条件全满足）分离；hard_no=CONFIRMED 不是 Task Stop 条件；显式用户问题永远优先完成
- Evidence 层不增加 user_impact（偏好属于 preference / report 层）
- AI/SEO 内容按具体页面降级，不建立域名黑名单
- 预算软上限：FULL_SCAN 4~8 组查询 / 5~12 页；SPECIFIC_RISK 身份 + 2~4 组；"够用即停"

## Key Decisions（Stage 3）

- 报告信息顺序固定：一句话结论 → 最重要雷点 → 核心排雷 → 偏好冲突/匹配 → 必要解释 → 可信度/争议 → 来源（禁止以作者/平台/字数/简介/研究过程开头）
- 用户可见措辞层：Confidence（已确认/较可信/证据较弱/无法确认）与 Agreement（各来源一致/来源说法冲突/评价两极/依据较少）独立成表（report-format §9/§10）；报告正文禁止内部枚举词与 Evidence Ledger 倾倒
- 长度软目标：normal 300~700 中文字（约 1 分钟）、detailed 700~1500；SPECIFIC_RISK 100~300 字远短于 FULL_SCAN；以"用户一分钟能看完"为准绳
- 剧透输出规则：none 禁令清单（关键死亡/重大反转/最终 Boss/结局事件/关键身份）；light（默认）允许结构级方向；full 仅用户显式允许；请求与配置冲突取更严格者
- Preference → Report 落点表（preference-guide §6.1）：hard_no=CONFIRMED → 冲突区第一条 + 建议=不推荐封顶；UNKNOWN/WEAK → 建议谨慎；DISPUTED → 争议前移；所有命中须经 §3.1 映射表换算；偏好不改事实判断与证据门槛
- 示例输出全部使用虚构书名（OUTPUT-EXAMPLES.md 为 DEVELOPMENT ARTIFACT，禁止当作真实排雷结论）
- 遗留观察：none 模式"高风险剧情抽象提示"对硬雷用户的价值待 Stage 7 实测（已登记 PROPOSALS）

## Key Decisions（Stage 3 REVISION 1）

- RESEARCH COVERAGE ≠ REPORT VISIBILITY：调查可覆盖 CORE 16 维度，normal 报告只展示 6~10 个最重要维度 + 可选合并行；必须展示 hard_no / 显式询问 / strong_dislike / 关键 UNKNOWN / DISPUTED / DIVIDED；禁止固定 16 行数据库式报告
- ✅ / ⚠ / ❌ / ❓ = USER IMPACT（不是 Confidence）；无偏好配置时禁止把用户未表达反感的属性打 ❌，只做中性描述
- 只保留 Recommendation Scale（推荐 / 可以尝试 / 观望 / 谨慎 / 不推荐）作为唯一正式决策枚举；删除"匹配度五档"，匹配用自然语言描述（避免"匹配度：比较适合 + 建议：谨慎"式语义冲突）
- hard_no + CONFIRMED → 建议 = 不推荐：规则层强制（report-format §6 + preference-guide §4.1），不依赖示例巧合
- interests 字段删除（无 taxonomy 映射、无定义行为、与 like 重叠）→ V1.1 候选（PROPOSALS）；output 只保留 show_confidence / show_sources；spoiler_level / detail_level 权威位置顶层唯一，不在 output 内重复
- DIVIDED（评价两极）语义：高可信度确认"分化"本身（value = mixed，CONFIRMED / DIVIDED），区别于"信息不可靠"或"矛盾无法判断"（示例 F 验证）

## Research Simulations（Stage 2 + 审计后）

真实模拟 3 本小说（2026-08-12；证据表逐条含 access_mode / tier / independence）：

- Case A《诡秘之主》：serialization-status = completed（Tier A 页面级"已经完本·1418章"）；romance-structure 倾向 no-romance 但仅 1 个独立页面级来源（WEAK/INSUFFICIENT）；ending-reception = mixed（DIVIDED）；发现 AI SEO 问答污染（红袖读书）
- Case B《玄鉴仙族》：serialization-status = ongoing（Tier A 页面级"连载中·1627章"、2026-08-11 更新）；slow-burn = high（LIKELY/CONSISTENT）；filler 社区侧 DIVIDED；ending-reception 不适用（连载中，旧帖预测只作情绪记录）
- Case C《剑来》：serialization-status = completed，completion_date = 2025-01-24（CONFIRMED / CONSISTENT，中国小说学会榜单页面级）；ending-reception = mixed（CONFIRMED/DIVIDED）；saintliness = unknown（LIKELY / DISPUTED）；首发平台纵横中文网（中国作家网 B 类页面级）

详见 docs/RESEARCH-SIMULATIONS.md。

## Problems Found（Stage 2 + REVISION 1）

- 搜索引擎结果会把站内首页/无关页伪装成书评（七星阁"书评"URL 实为论坛首页）→ snippet 级 URL 必须页面级核验后才可引用
- AI SEO 问答内容污染（红袖读书 ask 类页面）→ 按页降级、禁域名黑名单
- 模型记忆对连载状态/首发平台不可靠（宿命之环、赤心巡天、剑来首发平台）→ 规则写入 playbook §12.2
- 上一版《剑来》"2025-01-21 完结"无来源支持 → 已删除；精确完结日期保持未核验状态

## Tests

无自动化测试（Stage 5~7 引入）。RESEARCH-SIMULATIONS.md 为开发/评估产物；T219 十二项内部一致性检查全 PASS；T217 来源审计 11 项修正已完成；T312 输出一致性检查 16/16 PASS（OUTPUT-EXAMPLES.md）；T411 SKILL.md 静态审查 30/30 PASS；T412 Stage 4 dry-run 5/5 PASS；Stage 5 Trigger Evaluation 静态路由 55/55（两条边界修正后 Round 2 全量回归一致）；Stage 6 Behavior Evaluation 静态执行 46/46（Round 1 = Final Regression，16 critical 独立重推 16/16）。

## Deferred

- spoiler_level = none 实际输出跑测、SPECIFIC_RISK 单雷点实跑、FIT_CHECK + hard_no early 停实测、DRY RUN 无联网降级（Stage 7 模拟计划）
- none 模式"高风险剧情抽象提示"对硬雷用户的实际价值实测（Stage 7，见 PROPOSALS）
- **真实运行时触发验证**（Skill 安装到宿主后补做 Trigger Smoke Test；当前宿主无法观察自动选择 → TRIGGER-EVALUATION.md 阻塞项；Behavior Gate 通过不自动升级 Runtime Trigger Gate）
- trigger stability 真实模型随机性（ROUTING INSTABILITY）测量（同上，待真实宿主验证）
- 编造来源 / 编造 URL 专项验证（只能在真实搜索路径中触发，建议 Stage 7 真实小说逐例核对"依据"列表可追溯性）
- multi-novel comparison（V1.1 候选，见 PROPOSALS）

## Historical CHECKPOINT-8 READY 报告（T818 输出，21 节；**SUPERSEDED**）

> **历史记录，不代表当前状态。** 本报告形成后又发生 Runtime Optimization Round 1.1/2/3；Round 2 Final Acceptance Audit 出现 Evidence Integrity FAIL，因此本 READY 结论已被撤销。当前状态只以上方 `Current Stage / Gate Status / Remaining` 为准。

1. **T801~T818 完成表**：全部完成（T801 结构审计 / T802~T806 README 与文档 / T807~T809 链接·术语·边界审计 / T810 Scope / T811 Anti-hallucination / T812 Spoiler-Preference / T813 Manual Smoke 9 项 / T814 CHANGELOG / T815 版本 / T816 RELEASE-CHECKLIST / T817 Acceptance / T818 状态落盘）
2. **最终目录树**：见下方（与目标结构一致，新增 evals/evidence/、evals/STAGE7-SPEC.md、RELEASE-CHECKLIST.md）
3. **SKILL.md**：178 行；version = "1.0.0"；frontmatter 有效（name/description/compatibility/metadata）
4. **Runtime Files**：SKILL.md + references/（taxonomy/source-policy/search-playbook/preference-guide/report-format）+ config/preferences.yaml（仅用户创建时）
5. **Development / Evaluation Files**：docs/*、evals/*、TASKS.md、STATUS.md、PROPOSALS.md、CHANGELOG.md、RELEASE-CHECKLIST.md、config/preferences.example.yaml（仅模板）
6. **README**：16 节（一句话说明 → What it does → Quick Start → What it checks → How it works → Evidence before conclusion → Personal Preferences → Spoiler Control → Evidence & Sources → Limitations → Project Structure → Evaluation → Development Status → License）
7. **Installation**：将 novel-scout 目录复制到宿主 Skills 目录并确保宿主可读 SKILL.md 与 references/；宿主路径依平台而异，以对应宿主文档为准（未编造路径）；安装后最小检查 5 项（读 SKILL.md / Web 搜索 / 读 references / 输出来源 / 遵守 spoiler 等级）
8. **Preferences**：复制 preferences.example.yaml → preferences.yaml；example ≠ 真实偏好；当前请求优先、临时偏好不写回
9. **Evaluation Summary**：Trigger Static=PASS（55/55）· Trigger Runtime=**PENDING**（阻塞项）· Behavior Static=PASS（46/46）· Real E2E=PASS（7 core+3 HL+2 smoke）· Source Integrity=fake source 0（25/25）· Hallucination=3/3 · Spoiler=0 major leaks · Fresh Smoke=2/2
10. **Known Limitations**：README 9 项（社区评价主观性 / 冷门可能 UNKNOWN / 连载结论有时效 / 来源依赖可访问性 / 反爬降级 / 不解析正文 / V1 无推荐 / V1 无多书比较 / Runtime Trigger 待宿主补测）
11. **Runtime Trigger Pending**：当前开发宿主无法观测自动 Skill 路由 → 未完成真实自动触发验证；不表示 Skill 不可运行（显式请求完整流程已验）；补测 = 在可观测宿主执行 manual-smoke-tests ［Runtime Trigger］7 项
12. **Version**：1.0.0（Release Status = Release Candidate / 1.0.0-rc.1）——保持 SKILL.md metadata.version="1.0.0" 既有格式；CHANGELOG 用 `[1.0.0] - Unreleased`，人工批准前不宣称 Released
13. **CHANGELOG**：`[1.0.0] - Unreleased`（Stage 8 Added/Changed/Fixed + Stage 0~7 全记录）
14. **RELEASE-CHECKLIST**：Product Logic Gates 15/15 勾选；Host Integration Gate（Runtime Trigger）= PENDING 未勾；发布动作 5 项待人工
15. **Final Acceptance**：**16 PASS / 1 WARN（Runtime Trigger PENDING）/ 0 FAIL**（17 项：结构/frontmatter/references/config/触发边界/证据/taxonomy/偏好/剧透/报告/evals/README/LICENSE/CHANGELOG/版本/Scope/限制）
16. **Scope Audit**：No Python / No scripts / No Web App / No backend / No database / No RAG / No recommendation / No bookshelf / No tracking / No crawler（*.py=0、*.js=0、*.sh=0、scripts/=0）
17. **Git**：Initialized: NO · Commit created: NO · Tag created: NO · Remote pushed: NO（未初始化 .git；发布动作全部待人工确认）
18. **Files changed in Stage 8**：README.md、docs/DEVELOPMENT.md、evals/manual-smoke-tests.md、CHANGELOG.md、RELEASE-CHECKLIST.md（新建）、TASKS.md、STATUS.md；未修改 SKILL.md / references/* / config/*
19. **Remaining proposals（V1.1+，不实现）**：multi-novel comparison / recommendation / interests 字段 / none 剧透边界细化 / 站点内 SEO 问答页定级警觉 / 大页 fetch 成本
20. **V1 Release Readiness（历史结论）**：~~READY~~ → **SUPERSEDED / REVALIDATION REQUIRED**。本行仅保留变更历史，不得用于当前发布判断。
21. **需最终人工确认 A~I 九项**：
    - A. README 是否像普通用户能读懂的项目首页？
    - B. Installation 是否足够明确且未编造宿主路径？
    - C. Limitations 是否诚实（9 项具体限制，非免责垃圾话）？
    - D. Release Candidate 状态（1.0.0 / RC，CHANGELOG Unreleased）是否合理？
    - E. Runtime Trigger Pending 是否可接受（不阻塞产品逻辑验收）？
    - F. 是否需要在发布前真的初始化 Git？
    - G. 是否需要创建 GitHub 仓库？
    - H. 是否需要打 tag / 创建 Release？
    - I. 是否正式批准 Novel Scout V1（Release Candidate）？