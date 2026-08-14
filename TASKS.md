# Novel Scout Tasks

开发流程依据：`docs/DESIGN.md`（设计）与 `docs/DEVELOPMENT.md`（开发规则）。

当前状态见 `STATUS.md`。每个 CHECKPOINT 必须人工确认后才能进入下一 Stage。

## Stage 0 — 项目初始化

- [x] T001 创建项目目录结构（references/ config/ evals/ docs/）
- [x] T002 创建 SKILL.md 最小骨架（不实现完整工作流）
- [x] T003 创建 README.md 基础结构（完整内容 Stage 8 完善）
- [x] T004 创建 CHANGELOG.md 与 LICENSE
- [x] T005 创建 .gitignore
- [x] T006 保存完整设计至 docs/DESIGN.md
- [x] T007 创建 docs/DEVELOPMENT.md（开发规则）
- [x] T008 创建 TASKS.md（本文件，Stage 0~8 任务化）
- [x] T009 初始化 STATUS.md
- [x] T010 创建 config/preferences.example.yaml 空骨架
- [x] T011 创建 PROPOSALS.md（改进建议登记）
- [x] T012 修正 docs/DESIGN.md 缺失章节（补全原始设计三十九~六十四）
- [x] T013 统一文档引用规范（规则名称优先，消除 §编号 引用）
- [x] **CHECKPOINT-0**（历史人工确认已完成；当前发布状态以 Post-optimization Revalidation 为准）

## Stage 1 — 领域规则建立（编号以原始执行规范 T101~T111 为准）

- [x] T101 建立 taxonomy.md 基础结构（Purpose / 通用分类原则 / 术语对照骨架）
- [x] T102 定义感情关系类雷点（romance-level / romance-structure / harem H1~H3 与示例 / ntr / romance-drama）
- [x] T103 定义主角行为类雷点（saintliness / protagonist-iq / decisiveness / morality-tone）
- [x] T104 定义剧情体验类雷点（system-intensity / protagonist-abuse / slow-burn / filler / repetitive-patterns / plot-logic）
- [x] T105 定义世界观与力量体系类标签（worldbuilding-scale / power-system-consistency 含 not-applicable）
- [x] T106 定义连载与结局相关标签（serialization-status / ending-reception / 烂尾判定边界）
- [x] T107 建立雷点判定等级与 UNKNOWN / POSSIBLE / DISPUTED / MIXED 规则（Confidence Interaction）
- [x] T108 建立 source-policy.md（Tier A~D / 证据标签 / 冲突处理 / 独立来源 / 搜索摘要 / AI 来源 / 时效性）
- [x] T109 建立 preference-guide.md（hard_no~like / 硬雷优先 / 证据不足与争议处理 / 偏好影响边界）
- [x] T110 内部一致性检查与抽象情景示例测试（CORE/AUXILIARY 划分、误判示例库覆盖核对）
- [x] T111 更新项目状态与变更记录（TASKS / STATUS / CHANGELOG）
- [x] **CHECKPOINT-1（REVISION 1）**（历史人工确认已完成）

## Stage 2 — 搜索与证据系统（编号以原始执行规范 T201~T212 为准）

- [x] T201 建立 search-playbook.md 基础结构（Purpose / 原则 / Request Modes / 禁止行为）
- [x] T202 设计小说身份确认与消歧流程（Identity Resolution：候选提取 / 查询 / 确认标准 / 消歧 / 身份与风险优先级联动）
- [x] T203 设计查询生成策略（每维度查询模板 / 查询分组 / 正反平衡 / 中文小说搜索特征）
- [x] T204 设计用户意图与偏好驱动的搜索优先级（FULL_SCAN / SPECIFIC_RISK / FIT_CHECK 三种 base_mode 与 P0~P6 优先级表）
- [x] T205 设计 Evidence Ledger 证据记录模型（claim / dimension / claim_type / 来源 / 独立性分组 / supports / spoiler_level 等字段）
- [x] T206 设计证据升级与可信度规则（Claim Verification：单来源 WEAK / 独立多来源 / 升级路径 / 交叉确认）
- [x] T207 设计冲突解决与来源独立性判断（Conflict Resolution：先后顺序 / 同书不同期 / 术语 / 同源链 / 输出并存）
- [x] T208 设计时效性、连载状态与剧透处理（Recency / 模型记忆不可靠 / Spoiler 隔离与标题脱敏）
- [x] T209 设计搜索预算、停止条件与失败降级（软预算表 / 9 条停止条件 / 无网络与页面失败降级）
- [x] T210 进行真实/模拟研究流程验证（3 本真实小说模拟，记录于 docs/RESEARCH-SIMULATIONS.md）
- [x] T211 完成搜索策略内部一致性检查（Query Bias / Preference Bias / Evidence Leakage / 来源独立性等 10 项）
- [x] T212 更新 TASKS / STATUS / CHANGELOG
- [x] **CHECKPOINT-2**（历史人工确认已完成）

## Stage 2 — REVISION 1（CHECKPOINT-2 人审修正，编号 T213~T220）

- [x] T213 Evidence Ledger 原子化（one evidence item = one source-evidence pair；新增 evidence_id / claim_id / access_mode）
- [x] T214 分离 Dimension Value / Evidence Confidence / Agreement State；引入 Claim Synthesis 层（Evidence → Claim → Dimension Result）
- [x] T215 重构 Request Mode 为 Base Mode（FULL_SCAN / SPECIFIC_RISK / FIT_CHECK）+ Modifiers（spoiler_level / detail_level），playbook 全文同步
- [x] T216 重构 Stop Condition：Dimension Stop 与 Task Stop 分离；hard_no 不再无条件 TASK STOP（含三种 base_mode 处理表）
- [x] T217 审计 Research Simulations 来源元数据（URL / access_mode / source_date / access_date / tier / independence；起点两书页面级核验、七星阁假 URL 移除、《剑来》精确完结日期删除）
- [x] T218 审计 AI/SEO 来源规则（按具体页面评价，不建立域名黑名单）
- [x] T219 重新执行内部一致性检查（12 项全 PASS，记录于 RESEARCH-SIMULATIONS.md §5）
- [x] T220 更新 TASKS / STATUS / CHANGELOG
- [x] **CHECKPOINT-2 — REVISION 1**（历史人工确认已完成）

## Stage 2 — REVISION 2（最后一次一致性修正，编号 T221~T226）

- [x] T221 统一 Evidence Confidence 枚举（只保留 CONFIRMED / LIKELY / WEAK / UNKNOWN；HIGH / MEDIUM / LOW 不再作为 evidence confidence）
- [x] T222 清理非法 taxonomy value（无自创枚举；saintliness 案例改为合法值 unknown + agreement DISPUTED；未表达情形登记 PROPOSALS）
- [x] T223 恢复默认剧透等级与 DESIGN.md 一致（default spoiler_level = light，detail_level = normal）
- [x] T224 修正《剑来》Research Simulation 完结日期证据（中国小说学会榜单页面级核验：2025-01-24 完结，CONFIRMED / CONSISTENT）
- [x] T225 全项目 Stage 2 术语扫描（CONFIRMED/LIKELY/WEAK/UNKNOWN、HIGH/MEDIUM/LOW、四态 agreement、MIXED、no-official-romance、NO_SPOILER、DETAILED、spoiler_level、detail_level）
- [x] T226 更新 TASKS / STATUS / CHANGELOG
- [x] **CHECKPOINT-2 — REVISION 2**（历史人工确认已完成）

## Stage 3 — 输出体系、个人偏好配置与用户体验设计

- [x] T301 建立 references/report-format.md 基础结构（Purpose / Report Principles / Information Priority）
- [x] T302 设计默认排雷报告（FULL_SCAN 模板：先看结论 / 核心排雷 16 字段 / 最需要注意 / 和你的偏好 / 有争议无法确认 / 依据）
- [x] T303 设计 SPECIFIC_RISK 输出（远短于 FULL_SCAN，只答单一问题）
- [x] T304 设计 FIT_CHECK 输出（匹配度五档 + 建议五档 + 冲突区优先 + 无偏好降级）
- [x] T305 设计 spoiler_level 输出规则（none / light 默认 / full 仅显式允许；头部标注剧透等级）
- [x] T306 设计 detail_level 输出规则（normal 300~700 字 / detailed 700~1500 字软目标）
- [x] T307 完成 config/preferences.example.yaml 完整模板（version / spoiler_level / hard_no~like / interests / output）
- [x] T308 设计 Preference → Report 映射规则（报告落点表，preference-guide §6.1 补充）
- [x] T309 设计 Confidence / Agreement 用户显示（已确认 / 较可信 / 证据较弱 / 无法确认 等用户可见措辞）
- [x] T310 设计 UNKNOWN / DISPUTED / DIVIDED 用户体验（争议双方并列不选边 / 冷门措辞 / 连载时点结论）
- [x] T311 建立 docs/OUTPUT-EXAMPLES.md（五例：普通 / 无剧透 / 指定雷点 / 详细+偏好 / 冷门未知）
- [x] T312 执行输出一致性与可读性检查（12 项全 PASS，记录于 OUTPUT-EXAMPLES.md）
- [x] T313 更新 TASKS / STATUS / CHANGELOG
- [x] **CHECKPOINT-3**（历史人工确认已完成）

## Stage 3 — REVISION 1（CHECKPOINT-3 验收缺口修正，编号 T314~T319）

- [x] T314 补齐第 6 个 OUTPUT Example（示例 F：FULL_SCAN + detailed + light，ending-reception = mixed / CONFIRMED / DIVIDED，"评价分化"语义验证）
- [x] T315 补齐 T312 一致性检查至 16 项（16 / 16 PASS，记录于 OUTPUT-EXAMPLES.md）
- [x] T316 审计 preferences.example.yaml（interests 删除 → PROPOSALS V1.1 候选；output 收敛为 show_confidence / show_sources；spoiler_level / detail_level 权威位置顶层唯一）
- [x] T317 明确 RESEARCH COVERAGE 与 REPORT VISIBILITY 分离（normal 6~10 行 + 合并行，禁止固定 16 行数据库式报告）
- [x] T318 合并推荐尺度与匹配度（只保留 Recommendation Scale 五档；匹配用自然语言描述）
- [x] T319 更新 TASKS / STATUS / CHANGELOG
- [x] **CHECKPOINT-3 — REVISION 1**（历史人工确认已完成）

## Stage 4 — Skill Integration（编写真正可安装的 SKILL.md）

- [x] T401 审计 Stage 1~3 runtime references（5 个 references/ 为 runtime；docs/ 四个文件确认为 DEVELOPMENT/EVALUATION，正常执行不得读取）
- [x] T402 定稿 SKILL.md frontmatter（name / description / compatibility / metadata.version，保持既有骨架约定）
- [x] T403 设计 Skill 触发边界（Use when / Do NOT use when / 模糊请求"这本书怎么样"判定）
- [x] T404 设计请求解析与运行上下文（8 字段提取；3 Base Mode；2 Modifiers；当前请求覆盖配置；临时偏好不写回）
- [x] T405 设计 progressive disclosure / reference loading（场景→reference 映射表；每任务每文件只读一次；docs/ 与 example 配置不加载）
- [x] T406 编写核心执行工作流（编号式 12-step，非平级 bullet）
- [x] T407 整合 Evidence → Claim → Dimension 流程（one item = one source-evidence pair；SUPPORT/REFUTE/CONTEXT；access mode 禁静默升级）
- [x] T408 整合 Preference 与剧透规则（Evidence→Dimension→Preference 严格顺序；Recommendation Scale 唯一；hard_no 封顶；spoiler 默认 light + none 禁令）
- [x] T409 整合输出与来源规则（第一屏结论；图标 = user impact；Generic Mode 画像；SPECIFIC_RISK 直答；来源脱敏）
- [x] T410 编写失败降级与反幻觉规则（无网络降级文案；UNKNOWN 合法；冷门/AI SEO 规则；Non-negotiable Rules 十条）
- [x] T411 完成 SKILL.md 静态一致性审查（30 项清单，30/30 PASS；第 28 条可见性规则编写后补入）
- [x] T412 执行最小 dry-run 验证（5 个静态请求，5/5 PASS，记录于 STATUS.md）
- [x] T413 更新 TASKS / STATUS / CHANGELOG
- [x] **CHECKPOINT-4**（历史人工确认已完成）

## Stage 5 — Trigger Evaluation（触发路由评估）

- [x] T501 建立 Trigger Evaluation 规范（evals/trigger-cases.yaml，schema：id/category/prompt/context/expected/critical/reason）
- [x] T502 创建显式正例（POS-001~008：排雷/毒点/详细/无剧透/值不值得开/能看吗/劝退点，8 例）
- [x] T503 创建隐式正例（POS-009~015：无"排雷"字样的阅读前判断，7 例）
- [x] T504 创建 SPECIFIC_RISK 正例（POS-016~023：后宫/NTR/系统/圣母/虐主/水文/慢热/结局，8 例）
- [x] T505 创建 FIT_CHECK 正例（POS-024~028：适不适合/按口味/偏好条件，5 例）
- [x] T506 创建上下文依赖/模糊案例（CTX-001~008：“怎么样/好看吗/你知道…吗”+ 上下文变体，8 例）
- [x] T507 创建创作类负例（NEG-001~004：写/续写/设计世界观/润色，4 例）
- [x] T508 创建文学分析/总结负例（NEG-005~008：主题/叙事结构/总结正文/写书评，4 例）
- [x] T509 创建推荐/书单负例（NEG-009~011：推荐/书荒找书/相似书，3 例；含多书比较判定 NEG-018/019）
- [x] T510 创建其他边界负例（NEG-012~017：元数据/下载/全文/最新章节，6 例）
- [x] T511 安装或加载 Skill 真实 Trigger Smoke Test（宿主检查：无既有副本、无 skills 目录、本会话无法观察自动触发 → 记录 NO，见 TRIGGER-EVALUATION.md）
- [x] T512 执行完整 Trigger Evaluation（55 例静态路由：Round 1 55/55）
- [x] T513 分析误触发/漏触发原因（无 case FAIL；发现 2 处边界薄弱点：元数据查询、多书比较）
- [x] T514 修正 SKILL.md Trigger Boundary（Do NOT list 增加元数据查询与多书比较两条显式排除；description 未改）
- [x] T515 重新执行回归测试（全部 55 例重跑，Round 2：55/55；10 关键 case ×2 稳定性一致）
- [x] T516 更新 TASKS / STATUS / CHANGELOG / PROPOSALS（multi-novel comparison → V1.1 候选）
- [x] **CHECKPOINT-5**（历史人工确认已完成；Runtime Trigger 仍为独立 PENDING Gate）

## Stage 6 — Behavior Evaluation（行为评估，编号 T601~T618）

- [x] T601 建立 Behavior Case Schema（evals/behavior-cases.yaml：id / category / critical / description / request / runtime / research_state / expected / reason；NO REAL WEB REQUIRED 原则）
- [x] T602 创建 Request Parsing Cases（RP-001~004：默认 FULL_SCAN / SPECIFIC_RISK+none / FIT_CHECK+full+detailed / 当前请求覆盖配置不写回）
- [x] T603 创建 Identity Resolution Cases（IDENTITY-001~005：HIGH 继续 / 同名消歧 / author_hint / LOW 不强结论 / evidence wins；002/005 critical）
- [x] T604 创建 Evidence / Access Mode Cases（EVID-001~005：Tier A CONFIRMED / snippet 禁升级 / search-result 只引导 / 同源合并 / 三方证据全考虑；002/004/005 critical）
- [x] T605 创建 Claim / Dimension Classification Cases（CD-001~004：多女暧昧≠harem / 面板≠heavy / 成长挫折≠虐主 / 长≠水；001 critical）
- [x] T606 创建 Conflict / Agreement Cases（CONFLICT-001~004：禁多数投票 / mixed+CONFIRMED+DIVIDED / unknown+DISPUTED / 单来源 INSUFFICIENT；001 critical）
- [x] T607 创建 Recency / Ongoing Cases（REC-001~003：新覆盖旧 / 连载时间边界 / 预测非结局事实）
- [x] T608 创建 Preference Cases（PREF-001~006：hard_no 封顶 / UNKNOWN 谨慎 / 不污染证据 / 规模≠质量 / 临时偏好 / Generic Mode；001/002/003 critical）
- [x] T609 创建 Spoiler Cases（SPOILER-001~004：none 抽象 / 标题脱敏 / light 结构级 / full 不倾倒；001/002 critical）
- [x] T610 创建 Stop Condition Cases（STOP-001~003：FIT_CHECK 早停 / FULL_SCAN 仅维度停 / SPECIFIC_RISK 轻量终止；002/003 critical）
- [x] T611 创建 UNKNOWN / Failure Degradation Cases（FAIL-001~004：无 Web 降级 / 冷门不降标 / 页面失败保持 snippet / 全同源不宣称共识；001/002 critical）
- [x] T612 创建 Report / UX Cases（REPORT-001~004：首句直答 / 不打印 16 行 / 中性画像 / 内部术语不泄漏）
- [x] T613 执行 Behavior Evaluation Round 1（EXPLICIT SKILL BEHAVIOR TEST 静态口径：46/46 PASS，0 Critical）
- [x] T614 分析所有 Behavior Failures（0 FAIL；2 个观察项记录——IDENTITY-004 场景命名、REPORT-004 术语禁令依赖 report-format，判定规则表达充分）
- [x] T615 修正 Skill / references（**No runtime-rule changes required**；46 例 expected 全部由既有规则直接推出）
- [x] T616 执行完整 Behavior Regression（全部 46 例重跑：46/46 PASS，与 Round 1 一致）
- [x] T617 执行 Critical Behavior Stability Review（16 critical 独立重推 16/16 PASS；明确 STATIC STABILITY REVIEW 口径）
- [x] T618 更新 TASKS / STATUS / CHANGELOG
- [x] **CHECKPOINT-6**（历史人工确认已完成；当前 Behavior Gate 已扩展至 58 cases）

## Stage 7 — Real-world End-to-End Evaluation（任务书全文见 evals/STAGE7-SPEC.md）

已完成的批次以 `evals/real-world-cases.yaml` 状态与 `evals/REAL-WORLD-EVALUATION.md` 为准；每批独立新会话 + 接龙提示词见 STATUS.md。

- [x] T701 设计 Real-world Case Schema（evals/real-world-cases.yaml：12 对象 / schema 含 preferences / why_selected / critical_dimensions / manual_ground_truth / status / efficiency）
- [x] T702 选择最终测试小说集（RW-01~07 + HL-01~03 + SM-01~02；HL-02/03 书名 TBD 待 B7 前填）
- [x] T703 执行 Case A（RW-01《凡人修仙传》FULL_SCAN/light/normal）：**PASS**（evidence/core-a.md）
- [x] T704 执行 Case B（RW-02《宿命之环》，RECENCY 重点）—- B1（历史执行已完成，产物已落盘）
- [x] T705 执行 Case C（RW-03《庆余年》，感情结构争议）—- B2（历史执行已完成，产物已落盘）
- [x] T706 执行 Case D（RW-04《完美世界》，评价两极）—- B3（历史执行已完成，产物已落盘）
- [x] T707 执行 Case E（RW-05《幽冥仙途》，冷门/UNKNOWN 防胡猜）—- B4（**PASS**；本会话为复核已落盘产物 + 补齐写回，evidence/core-e.md 与 EVALUATION Case E 段为既有落盘）
- [x] T708 执行 Case F（RW-06《斗罗大陆》，SPECIFIC_RISK 轻量）—- B5（**PASS**；复核已落盘产物 + 补齐写回，evidence/core-f.md、EVALUATION Case F 段、yaml RW-06 done）
- [x] T709 执行 Case G（RW-07《斗破苍穹》，FIT_CHECK + hard_no）—- B6（**PASS**；复核已落盘产物 + 补齐写回，evidence/core-g.md 含复核记录、EVALUATION Case G 段、yaml RW-07 done；修正 2 处 MINOR 事实）
- [x] T710 执行 No-spoiler 专项审计（2 个真实 Case 重生成 none）—- B8（**PASS**；REAL-WORLD-EVALUATION.md 已落盘：RW-01 + RW-02 重生成 none 人工对照 6/6×2，major spoiler 泄漏 = 0，useful abstraction 保持；1 项 none 边界观察登记待 PROPOSALS）
- [x] T711 执行 Source Integrity 专项审计（≥20 条重要 Evidence 抽查）—- B9（**PASS**；REAL-WORLD-EVALUATION.md 已落盘：25/25 条抽查，真实 URL 25/25、fake source = 0、page/snippet 标注一致、summary fidelity 100%）
- [x] T712 执行 Manual Ground-truth Review（人工复核每本 3~6 关键维度）—- B10（35 个维度抽查 7 本全一致，major/minor disagreement = 0，记录于 REAL-WORLD-EVALUATION.md §Manual Ground-truth Review）
- [x] T713 汇总 Round 1 Failures（按 14 类分类）—- B11（0 FAIL/0 CRITICAL_FAIL，全 PASS；14 类中 0 类存在 runtime rule 缺陷，记录于 REAL-WORLD-EVALUATION.md §Round 1 Failure Summary）
- [x] T714 必要时修正 Skill / references（最小化；每处记录 case/file/before/after/why）—- B11（**No runtime-rule changes required**——全部问题为 OBS/先例性 MINOR，既有规则已覆盖）
- [x] T715 执行 Real-world Regression（受影响真实 Case + 对应 Stage 6 Critical Cases）—- B11（T714 未改 runtime rule → 无需重跑）
- [x] T716 执行 Hallucination Challenge（HL-01~03，必须 3/3 PASS）—- B7（**3/3 PASS**；evidence/core-h.md + EVALUATION §Hallucination + yaml HL-01~03 done 已落盘；无 fake source / fake identity / wrong same-title classification）
- [x] T717 执行最终 V1 Smoke Test（SM-01 雪中悍刀行 / SM-02 全职高手；不进入修改循环）—- B12（**2/2 PASS**；evidence/core-sm1.md + core-sm2.md + EVALUATION §Fresh Smoke Tests + yaml SM-01/02 done 已落盘；SM-01 5q/1p、SM-02 2q/0p，均无过拟合迹象）
- [x] T718 更新 TASKS / STATUS / CHANGELOG + 创建 evals/manual-smoke-tests.md + 输出 CHECKPOINT-7 报告 —- B13
- [x] **CHECKPOINT-7**（历史人工确认已完成；其 READY 含义已被 post-optimization revalidation supersede）

## Stage 8 — V1 Finalization / Release Preparation（任务书：CHECKPOINT-7 通过后执行）

- [x] T801 最终项目结构审计（实际结构与 DESIGN.md 目标结构一致；新增 evals/evidence/、evals/STAGE7-SPEC.md、RELEASE-CHECKLIST.md 为合理产物；未创建空文件）
- [x] T802 完善 README.md（正式用户首页：What it does / Quick Start（中文示例）/ What it checks / How it works / Personal Preferences / Spoiler Control / Evidence & Sources / Limitations / Project Structure / Evaluation / Development Status / License）
- [x] T803 完善 docs/DEVELOPMENT.md（追加 §9 Development Stages（Stage 0~8）/ §10 Evaluation Gates（含 Runtime Trigger Pending 准确解释）/ §11 Runtime vs Development Artifacts / §12 Release Process / §13 Known Pending）
- [x] T804 编写安装与使用说明（README Quick Start + 安装说明：复制到宿主 Skills 目录；不编造宿主路径，标注"以对应宿主文档为准"；安装后最小检查 5 项写入 README）
- [x] T805 编写 Personal Preferences 使用说明（README 一节：复制 preferences.example.yaml → preferences.yaml；example ≠ 真实偏好；当前请求优先；临时偏好不写回）
- [x] T806 编写 Capability / Limitation 说明（README Limitations 9 项，具体不空泛；不承诺推荐/多书比较/书架等 V1 外能力）
- [x] T807 审计 SKILL.md 与 references 断链（SKILL.md 引用 5 个 runtime reference 全部存在、大小写一致；config/preferences.example.yaml 存在；references 内部互引全部有效；0 断链）
- [x] T808 审计全部配置与文档一致性（Terminology Audit：FULL_SCAN/SPECIFIC_RISK/FIT_CHECK、none/light/full、normal/detailed、CONFIRMED~UNKNOWN、CONSISTENT~INSUFFICIENT、五档建议均为冻结体系；废弃术语 NO_SPOILER/DETAILED/strong_like/no-official-romance/HIGH-MEDIUM-LOW confidence/伪精确评分仅在"禁止"语境出现）
- [x] T809 审计 eval / docs runtime 边界（SKILL.md 无 evals/ 引用；docs/ 仅声明"不得读取"；README 将 docs/evals 标注为开发验证资料；SKILL.md 不加载任何 eval YAML）
- [x] T810 执行最终 Scope Audit（*.py = 0 / *.js = 0 / *.sh = 0 / scripts/ = 0；无 Web 前端/后端/数据库/RAG/推荐/书架/追更/爬虫；仅静态 MD/YAML）
- [x] T811 执行最终 Anti-hallucination Audit（Never invent source/URL/fact、Model memory is not evidence、snippet ≠ page、one comment ≠ consensus、UNKNOWN is valid、same-title 消歧、preferences 不降低证据标准——8 条硬规则全部存在于 SKILL.md/source-policy/search-playbook 且无冲突）
- [x] T812 执行最终 Spoiler / Preference Audit（default spoiler_level = light ✓；default detail_level = normal ✓；current request > configuration ✓；hard_no + CONFIRMED → 不推荐 ✓）
- [x] T813 执行 Manual Smoke Checklist 整理（evals/manual-smoke-tests.md 扩展为 9 项：新增 Smoke 8 负例推荐不触发 / Smoke 9 负例续写不触发；7 项标注［Runtime Trigger］用于宿主自动路由补测；10~15 分钟执行）
- [x] T814 定稿 CHANGELOG（版本段 `[1.0.0] - Unreleased`；Stage 8 Added/Changed/Fixed 记录；不宣称 Released）
- [x] T815 定稿版本信息（Product Version = 1.0.0，Release Status = Release Candidate；SKILL.md metadata.version = "1.0.0" 保持既有格式不强行改 RC 后缀；README/CHANGELOG/STATUS 版本表述一致）
- [x] T816 创建 Release Checklist（RELEASE-CHECKLIST.md：Product Logic Gates 与 Host Integration Gate 分离；Runtime Trigger PENDING 不勾 PASS；发布动作列明须人工确认）
- [x] T817 执行最终 V1 Acceptance Review（17 项：16 PASS / 1 WARN（Runtime Trigger PENDING）/ 0 FAIL）
- [x] T818 更新 TASKS / STATUS（本文件 Stage 8 段重写 + STATUS.md 更新 + 输出 CHECKPOINT-8 READY 报告）
- [ ] **CHECKPOINT-8 / FORMAL RELEASE APPROVAL**（仅正式发布时由人工确认；不阻塞本地显式使用与 RC 体验）

## Post-optimization Revalidation（当前阶段）

- [x] R001 统一未发布版本线：SKILL metadata = `1.0.0`，撤销内部 1.0.2 对外状态漂移
- [x] R002 统一 Evidence 模型：`source_tier` 与 `access_mode` 正交；snippet 上限 WEAK
- [x] R003 增加 Web Prompt Injection 防线 + SEC-001 critical case
- [x] R004 `.gitignore` 忽略 `docs/history-session/`
- [x] R005 修 Preference：pausing / light-saintliness 映射 + show_sources=false 行为
- [x] R006 修 Taxonomy H3：single / no-romance 双路径
- [x] R007 优化 frontmatter trigger description + compatibility
- [x] R008 Behavior cases 52→59，critical 19→21；Post-optimization Static Contract Regression PASS（含 EVID-008 多 snippet 累加升级 critical 回归）
- [x] R009 修正已知旧评测违规：core-sm2 snippet-only 强结论降为 WEAK；manual smoke 标记 historical
- [x] R010 重新执行受影响 Real E2E / Evidence Integrity 回归并恢复 Gate（10/10 ledger re-audit + 3/3 fresh targeted live Web regression PASS）
- [ ] R011 在可观察宿主完成 Runtime Trigger Gate（可选发布验证；PENDING 不阻塞显式使用，但不得宣称自动触发已验证）
- [ ] R012 正式发布前重新执行 Final Acceptance / Release Checklist（release-time task，不在当前体验阶段执行）

## V1 Runtime Simplification / Experience Freeze（当前阶段）

- [x] S001 简化 `SKILL.md`：保留三模式、联网核验、偏好、剧透、UNKNOWN、minimum sufficient fetch；移除过细 section routing / P0~P6 / 形式化 Stop 状态
- [x] S002 简化 `references/search-playbook.md`：移除 ACTIVE/OPPORTUNISTIC/ESCALATED、Evidence ID/Claim ID/independence_group 与数据库式 Ledger 要求
- [x] S003 简化 `references/source-policy.md`：取消 Page Anchor 术语与复杂矩阵，冻结为“snippet=WEAK；重要强结论打开 1~2 个关键页面”
- [x] S004 `report-format.md` 改用“内部证据笔记”措辞，不再要求正式 Evidence Ledger
- [x] S005 保留现有 59 个 Behavior Case 作为回归保险，并把 FULL_SCAN 用例改成自然语言规则，不再反向驱动 Runtime 增长
- [x] S006 执行 Simplification Regression：YAML / frontmatter / reference / behavior contract / runtime size 一致性检查 PASS（59 cases / 21 critical；Runtime 旧优化术语清零）
- [x] S007 精简 `report-format.md`：约 15.9KB → 6.2KB，保留原 section 编号与行为语义
- [x] S008 精简 `preference-guide.md`：约 9.7KB → 4.7KB，保留 V1 映射与偏好规则
- [x] S009 新增 SPECIFIC_RISK Fast Path：短执行卡 + 目标 taxonomy + 单项报告规则
- [x] S010 第二轮结构回归 + 12 个受影响 Preference/Report behavior contract 复核 PASS
- [x] S011 高频单雷点最小本地规则路径测量：约 9.6KB / 5.45k chars（partial read；不含 Web）
- [ ] S012 **真实使用体验**：正常使用 Novel Scout；只根据真实 Bug / UX 反馈决定后续 1.0.x 修改

## 规则提醒

- 到达任何 CHECKPOINT 后必须停止，等待用户确认"继续"。
- 未经确认不得跨 Stage。
- 建议写入 PROPOSALS.md，不得擅自扩大范围。