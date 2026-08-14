# Changelog

本项目所有重要变更都会记录于此。格式遵循 [Keep a Changelog](https://keepachangelog.com/zh-CN/1.1.0/) 规则，版本遵循 [Semantic Versioning](https://semver.org/lang/zh-CN/)。

## [1.0.0] - Unreleased

> V1 产品版本 = 1.0.0；Release Status = **Release Candidate / Unreleased / User Experience Trial**。此前内部 `1.0.2` 从未正式发布，已统一收回到未发布 1.0.0 版本线。
> 当前：核心 Runtime 已完成 Simplification Freeze；Behavior / Real E2E 作为回归保险保持 PASS；Trigger Runtime = PENDING（只限制“自动触发已验证”的宣称，不阻塞显式使用）；正式 GitHub Release 仍需人工批准。

### Changed (V1 Runtime Simplification — Experience Freeze)

- `SKILL.md`：从约 8.8KB / 90 行压缩到约 5.1KB / 71 行；12 步编排改为 8 步实用流程，移除 P0~P6、复杂 section routing、DIMENSION/TASK STOP 形式化和正式 Evidence Ledger 要求
- `references/search-playbook.md`：约 33.5KB → 11.6KB；移除 ACTIVE / OPPORTUNISTIC / ESCALATED、evidence_id / claim_id / independence_group、七项 Task Stop 等框架式抽象；保留三模式、共享 query、minimum sufficient fetch、冲突/时效/剧透/降级与够用即停
- `references/source-policy.md`：约 12.8KB → 5.9KB；取消 Page Anchor 术语/矩阵，保留核心事实：`snippet/search-result ≠ page`、纯 snippet 上限 WEAK、重要强结论应打开 1~2 个关键页面、多个 snippet 不能靠数量升级
- `references/report-format.md`：Evidence Ledger 统一改为“内部证据笔记”，报告与证据判断不再依赖数据库式结构
- `evals/behavior-cases.yaml`：59 个 case 全部保留作为**回归保险**；FULL_SCAN-001~004 与 EVID-008 改成自然语言规则，测试不再反向驱动 Runtime 增长
- 项目阶段改为 **V1 RC / User Experience Trial**：停止凭想象扩规则，后续 1.0.x 只由真实使用中的 Bug / UX 问题触发

### Changed (V1 Runtime Simplification Pass 2)

- `references/report-format.md`：约 15.9KB → 6.2KB；保留 §1~§16 编号，删除重复模板与重复解释
- `references/preference-guide.md`：约 9.7KB → 4.7KB；保留 §3.1 映射、偏好边界与唯一 Recommendation Scale
- `references/search-playbook.md`：新增 §0 Fast Path；SPECIFIC_RISK 正常路径无需通读完整搜索手册，异常时再跳转冲突/时效/fetch/降级章节
- `SKILL.md`：Reference Loading 增加 SPECIFIC_RISK 快路径，不改变三模式或证据标准
- 受影响的 `PREF-001~007` / `REPORT-001~005` 共 12 个 behavior contract 人工复核通过；YAML/frontmatter/reference 结构校验通过
- 以“《X》后宫吗？”为样本，partial-read 本地最小规则文本约 **9.6KB / 5.45k chars**（不含 Web 内容，不等同 API billing tokens）

### Fixed (Post-optimization Revalidation — Evidence / Release Integrity)

- `SKILL.md`：frontmatter metadata 统一回 `1.0.0`；description 增加推荐/写作/文学分析/纯元数据/更新下载/多书比较等关键排除边界；compatibility 明确 runtime references 需要 file-read；新增 retrieved web content = untrusted data/evidence 的 Prompt Injection 硬规则
- `references/source-policy.md`：明确 `source_tier` 与 `access_mode` 正交；Tier A + snippet 合法但 snippet 仍受 WEAK 上限；新增 Page Anchor 规则——纯 snippet/search-result 无论数量多少都不能升 LIKELY，DIVIDED/DISPUTED 要强置信时双方都需 page 锚点
- `references/taxonomy.md`：修正 H3 映射，区分 `single`（唯一实质恋爱对象）与 `no-romance`（完全无实质恋爱回应）
- `references/preference-guide.md` / `config/preferences.example.yaml`：补齐 `pausing`、`light-saintliness` 映射；`references/report-format.md` 落地 `output.show_sources=false` 的真实行为
- `.gitignore`：新增 `docs/history-session/`，避免本地会话归档/状态误提交
- Evidence Ledger re-audit：修正 `core-a/core-b/core-c/core-e/core-sm1/core-sm2` 中已发现的派生升级、snippet-only 强结论、单侧 page 的 DIVIDED 强结论与独立性误计；历史 manual smoke 标记为 historical run，不再覆盖当前 Gate

### Added (Post-optimization Revalidation — Regression)

- `evals/behavior-cases.yaml`：52 → **59** primary cases；critical 19 → **21**。新增 EVID-007 / EVID-008 / CD-005 / PREF-007 / REPORT-005 / SEC-001 / LOOP-001
- EVID-008 直接覆盖 Round 2 暴露的真实失败模式：**多个独立 snippet 也不得通过数量累加升级到 LIKELY/CONFIRMED**；有高价值页面时继续执行 Fetch Gate
- SEC-001：Web Prompt Injection critical regression；外部页面中的操作性文字只作为不可信数据，不得覆盖 Skill 规则/触发无关敏感操作
- `evals/BEHAVIOR-EVALUATION.md`：新增 Post-optimization Revalidation 段；Static Contract Gate = **59/59 PASS / 21 critical PASS**（静态口径）
- 新增 `evals/evidence/postopt-live-regression.md`：fresh live Web 3/3 PASS——《全职高手》SPECIFIC_RISK（2 page）、《凡人修仙之仙界篇》FULL_SCAN targeted ending（正负双方 page anchor）、《斗破苍穹》FIT_CHECK+hard_no（2 page）；结合 10/10 ledger re-audit 恢复 Real E2E Gate PASS

### Changed (Post-optimization Revalidation — Release Governance)

- `README.md` / `STATUS.md` / `docs/DEVELOPMENT.md` / `RELEASE-CHECKLIST.md` / `TASKS.md`：撤销旧 CHECKPOINT-8 READY 对当前版本的效力；旧 Stage 8 结论保留为历史记录并标记 SUPERSEDED
- 当前发布流程增加强制 Revalidation Gate：Stage 8 后任何 runtime rule 修改，只要出现 Evidence Integrity FAIL，就自动撤销 READY；Real E2E 重新通过前不得 tag / Release
- `TASKS.md` 清理重复旧 Stage 4~7 未完成清单，补齐历史 T704~T706 / CHECKPOINT 状态，并新增 R001~R012 post-optimization revalidation 任务

### Added (Runtime Optimization Round 3 — Manual Smoke Regression)

- `references/search-playbook.md`：§14 新增 §14.4 Search Loop Detection——宿主缓存循环（相同 search_id / 相同结果集重复返回，人工冒烟实测出现数十次）处理规则：循环内重复返回视为一次有效查询（不计预算/不计来源）；证据足够即止损；不足则改写查询重试一次，仍循环按 §16 降级；同 query 连续 2 次相同返回即停止重试。§18 禁止行为表同步新增对应条目
- `evals/manual-smoke-tests.md`：9 项冒烟测试人工执行记录（2026-08-13）：**9/9 PASS**——Smoke 1 凡人修仙传 FULL_SCAN（慢热 high、结局 DIVIDED、道侣唯一+术语 DISPUTED，身份正确）/ Smoke 2 斗罗大陆 SPECIFIC_RISK（single，未扩张）/ Smoke 3 宿命之环 无剧透（结构级结论保留、零关键事件泄漏）/ Smoke 4 斗破苍穹 FIT_CHECK（harem=H1 CONFIRMED → hard_no 封顶不推荐，偏好未污染证据）/ Smoke 5 幽冥仙途 UNKNOWN（2007 台湾实体书首发身份修正、虐主 heavy）/ Smoke 6 天骄 同名消歧（3 候选询问，未选边）/ Smoke 7 雾港第七码头 虚构防幻觉（2q 零命中、零编造）/ Smoke 8-9 负例不触发；与 Stage 7 基线（RW-01/05/06/07、B8/T710、HL-01/03）全部吻合；过程中发现 websearch 偶发缓存循环 → 落地本版本 §14.4 规则

### Added (Runtime Optimization Round 2 — FULL_SCAN normal)

- `references/search-playbook.md`：§5 新增 §5.1 FULL_SCAN Coverage Policy——正式区分 RESEARCH COVERAGE（16 CORE 整体意识）与 ACTIVE SEARCH COVERAGE；ACTIVE（identity/status/romance/ntr/system/abuse/pacing cluster/protagonist cluster/ending when applicable）/ OPPORTUNISTIC（repetitive-patterns/plot-logic/worldbuilding/power-system，默认不单独加 query，已打开来源自然提供则必须记录）/ ESCALATION（explicit/hard_no/strong_dislike/major emerging risk/conflict/recommendation-changing 六条件）；UNKNOWN 行为（不补搜、允许省略）；报告层禁"未主动搜索"机械标注；FULL_SCAN+detailed 不受限。§5.2 Query Structure：QUERY SHARING + Q1~Q7 软模板（通常 4~7 组，3~4 组足够可提前停）。§14 预算表两行微调
- `SKILL.md`：第 51 行 FULL_SCAN 段新增一句 routing（FULL_SCAN normal 使用 playbook §5.1 策略）；5,561 → 5,632 chars（< 6,000 目标，未膨胀）
- `evals/behavior-cases.yaml`：新增 FULLSCAN-001（opportunistic 无证据不补搜）/ FULLSCAN-002（opportunistic 有证据必记录）/ FULLSCAN-003（hard_no 升级 ACTIVE，critical）/ FULLSCAN-004（detailed 不受限）；primary cases = 52（48 无替换/无删除 + 4 新增）
- `STATUS.md`：追加 Round 2 段（T7xx-1~6 + Gate PASS）

### Added (Runtime Optimization Round 1.1 — T619/T620)

- `evals/behavior-cases.yaml`：新增 EVID-006（evidence-access，critical，MINIMUM SUFFICIENT FETCH 行为，落地 search-playbook §14.2 修正）与 FAIL-005（failure-degradation，critical，AI-SEO ask 页排除行为，落地 source-policy §3.3）；primary cases = 48（原 46 无替换/无删除 + 2 新增）
- `evals/BEHAVIOR-EVALUATION.md`：追加 Round 1.1 Regression 段——**Behavior Gate: PASS（静态口径；48/48，0 Critical）**；并修正 Round 1.1 初稿数量笔误（"47/47（46 原案 + 2 新增）"实为 46+2=48，且初稿脚本漏跑 SPOILER-004，补跑后以 48/48 为准）
- `STATUS.md`：追加 T619 / T620 记录（Round 1.1 Behavior Regression 48/48 PASS + 数量一致性审计结论）

### Added (Stage 8 — V1 Finalization)

- 完善 `README.md`：正式用户首页（一句话说明 / What it does / Quick Start（中文示例）/ What it checks / How it works（Evidence before conclusion）/ Personal Preferences / Spoiler Control / Evidence & Sources / Limitations（9 项诚实限制）/ Project Structure / Evaluation（如实标注"开发评估集结果"）/ Development Status / License）；明确 `preferences.example.yaml` 只是模板不会被自动当作真实偏好；明确 Runtime Trigger PENDING 含义
- `docs/DEVELOPMENT.md`：追加 §9 Development Stages（Stage 0~8）/ §10 Evaluation Gates（含 Runtime Trigger 为什么 Pending 的准确解释）/ §11 Runtime vs Development Artifacts / §12 Release Process / §13 Known Pending
- `evals/manual-smoke-tests.md`：扩展为 9 项 Manual Smoke Checklist（新增 Smoke 8 负例：小说推荐不触发 / Smoke 9 负例：续写小说不触发；约 10~15 分钟执行）；7 项标注［Runtime Trigger］用于宿主自动路由补测
- 创建 `RELEASE-CHECKLIST.md`：V1 发布检查清单（Product Logic Gates 与 Host Integration Gate 分离；Runtime Trigger PENDING 不勾 PASS）
- `CHANGELOG.md`：版本段定稿为 `[1.0.0] - Unreleased`

### Changed (Stage 8)

- `STATUS.md`：Current Stage = Stage 8 / Checkpoint = CHECKPOINT-8（PENDING HUMAN APPROVAL）/ Gate 状态（Trigger Static PASS / Trigger Runtime PENDING / Behavior Static PASS / Real E2E PASS）/ Final Acceptance 17 PASS 1 WARN 0 FAIL / Version 1.0.0（RC）
- `TASKS.md`：Stage 8 T801~T818 记录；CHECKPOINT-8 = PENDING HUMAN APPROVAL

### Fixed (Stage 8)

- README.md 由 Stage 0 占位状态补齐为正式 Release Candidate 首页（原"本项目处于开发阶段（Stage 0 已完成）"已过时）

### Added (Stage 7 — Real-world End-to-End Evaluation)

- 创建 `evals/real-world-cases.yaml`：12 个真实对象（7 core：RW-01 凡人修仙传 / RW-02 宿命之环 / RW-03 庆余年 / RW-04 完美世界 / RW-05 幽冥仙途 / RW-06 斗罗大陆 / RW-07 斗破苍穹；3 hallucination：HL-01~03；2 smoke：SM-01 雪中悍刀行 / SM-02 全职高手）；schema 含 manual_ground_truth / status / verdict / efficiency；全部 case 完成并写回
- 创建 `evals/STAGE7-SPEC.md`：Stage 7 任务书存档（新会话执行规范唯一依据）
- 创建 `evals/REAL-WORLD-EVALUATION.md`：真实 E2E 评估记录（Case A~G 每段含 Request/Identity/Research plan/queries/pages/evidence/conflicts/Dimension results/verdict/Problems；Source Integrity 25/25 审计；No-spoiler 2 例 6/6×2；Hallucination 3/3；Manual Ground-truth 35 维度全一致；Round 1 Failure Summary 14 类 0 FAIL；T714 No runtime-rule changes required；T715 无需重跑；Fresh Smoke 2/2）
- 创建 `evals/evidence/core-{a,b,c,d,e,f,g,h,sm1,sm2}.md`：10 份证据台账（Evidence Ledger 含 evidence_id/claim_type/source/tier/date/access_mode/independence_group/supports/summary + Dimension Results + 冲突处理 + Verdict）
- 创建 `evals/manual-smoke-tests.md`：7 项人工冒烟测试清单（知名 FULL_SCAN / 单雷点 SPECIFIC_RISK / 无剧透 / FIT_CHECK / 冷门 UNKNOWN / 同名消歧 / 虚构防幻觉），未来换宿主/模型快速回归用

### Changed (Stage 7)

- `TASKS.md`：Stage 7 任务按 T701~T718 全部勾选（含 B1~B13 批次完成标注）
- `STATUS.md`：Current Stage / Checkpoint（CHECKPOINT-7 READY 已输出）/ Gate Status / Completed（Stage 7 全批次）/ 批次表 B1~B13 全部完成 / 新增 CHECKPOINT-7 READY 报告 22 节 / Next 等待人工确认
- 未修改 `SKILL.md`、references/*.md、config/：Stage 7 全部真实 Case 判定 PASS，T714 确认 No runtime-rule changes required（与 T615 先例一致）

### Fixed (Stage 7)

- 无 runtime rule 修正。真实测试中发现的问题均为 HOST_LIMITATION / 先例性 MINOR / OBS（反爬 403/空回 15+ 次、站点内 SEO 问答页、大页 fetch 成本、none 边界观察），全部由既有规则吸收或登记 PROPOSALS

### Changed (Stage 6 — Behavior Evaluation)

- 创建 `evals/behavior-cases.yaml`：46 例行为测试集（16 critical；11 个 category：request-parsing 4 / identity 5 / evidence-access 5 / claim-dimension 4 / conflict-agreement 4 / recency 3 / preference 6 / spoiler 4 / stop-condition 3 / failure-degradation 4 / report-ux 4；schema：id / category / critical / description / request / runtime / research_state / expected / reason）
- 创建 `evals/BEHAVIOR-EVALUATION.md`：行为评估报告（Environment / Scope / Case Distribution / Evaluation Method（EXPLICIT SKILL BEHAVIOR TEST 静态口径）/ Round 1 46/46 逐 case 判定链（每条含规则依据）/ Failures（0 FAIL + 2 观察项）/ Fixes（No runtime-rule changes required）/ Final Regression 46/46 / Stability Review（16 critical 独立重推 16/16，STATIC 口径）/ Critical Cases 与任务十二类 Critical Behavior Failure 映射 / Known Limitations / Gate Result）

### Changed (Stage 6)

- `TASKS.md`：新增 Stage 6 T601~T618 并全部勾选
- `STATUS.md`：Current Stage / Checkpoint / Gate Status（Trigger Static PASS / Trigger Runtime PENDING / Behavior PASS 静态口径）/ Completed（Stage 6）/ Stage 6 Metrics / Created（Stage 6）/ Tests / Deferred（编造来源专项验证） / Next 同步 Stage 6
- 未修改 `SKILL.md`、references/*.md、config/：Round 1 无 FAIL、无规则缺口，T615 判定 No runtime-rule changes required

### Added (Stage 5 — Trigger Evaluation)

- 创建 `evals/trigger-cases.yaml`：55 例触发测试集（30 TRIGGER / 23 DO_NOT_TRIGGER / 2 CONTEXT_DEPENDENT，7 critical；11 个 category：explicit-full-scan / implicit-pre-read / specific-risk / fit-check / ambiguous-context / creative-writing-negative / literary-analysis-negative / recommendation-negative / metadata-negative / download-update-negative / multi-novel-deferred）
- 创建 `evals/TRIGGER-EVALUATION.md`：触发评估报告（Environment（Host: opencode CLI / Skill loading: 未安装 / Actual runtime trigger observable: NO）/ Metrics / Round 1 静态路由 55/55 / Failures / SKILL.md Changes / Round 2 回归 55/55 / Stability（10×2 静态稳定）/ Final Metrics（Positive 30/30、Negative 23/23、Context 2/2、Overall 55/55、Critical 0）/ Remaining Limitations（真实运行时触发验证为阻塞项）/ Conclusion）

### Changed (Stage 5)

- `SKILL.md`：Do NOT use this skill when 追加两条显式排除——"查询作者、完结日期、平台等作品元数据（非阅读决策语境）"与"多本小说相互比较（V1 未设计 multi-novel comparison）"（仅触发边界；description / Use when / Core Workflow / references 未改）
- `PROPOSALS.md`：V1.1 候选新增 multi-novel comparison（登记触发边界审查结论）
- `TASKS.md`：新增 Stage 5 T501~T516 并全部勾选
- `STATUS.md`：Current Stage / Checkpoint / Completed（Stage 5）/ Stage 5 Metrics / Created / Tests / Deferred / Next 同步 Stage 5

### Fixed (Stage 5)

- 边界薄弱点修复（T513→T514）：元数据查询与多书比较在触发边界中从"隐式不触发"提升为"显式排除"，防止未来模型发挥时误触发（NEG-012/013/018/019 静态通过 + 显式排除双保险）

### Added (Stage 4 — Skill Integration)

- `SKILL.md` 骨架 → 正式可安装实现（176 行 / 约 10800 字符 / 约 835 词）：Frontmatter（name: novel-scout）→ Purpose（UNKNOWN = 合法成功）→ Use this skill when / Do NOT use this skill when（含"这本书怎么样"模糊请求判定）→ Reference Guide（5 个 runtime reference 按需读取映射表；docs/ 四个文件与 preferences.example.yaml 禁止执行期加载）→ Core Workflow（编号式 12-step：Parse → Resolve Identity（IDENTITY FIRST / model memory is not evidence）→ Preferences → Research Plan（P0~P6）→ Research（无网络明确降级）→ Evidence（one item = one source-evidence pair / SUPPORT REFUTE CONTEXT / access mode 禁静默升级）→ Claim Synthesis → Dimension Classification（合法 value 仅 taxonomy / 三轴分离）→ Recency & Conflict（禁多数投票 / 连载时间边界）→ Stop（Dimension vs Task；hard_no 不提前结束 FULL_SCAN）→ Preference Match（Recommendation Scale 唯一 / hard_no 封顶 / UNKNOWN → 谨慎）→ Report（第一屏结论 / 图标 = user impact / Generic Mode 画像 / SPECIFIC_RISK 首句直答 / 来源脱敏））→ Failure and Degradation（冷门 / AI SEO 按页评价 / 身份不明）→ Non-negotiable Rules（十条硬规则）
- `STATUS.md`：新增 Main Deliverable（SKILL Size 176 行）与 Stage 4 Dry Runs 记录（5/5 PASS）

### Changed (Stage 4)

- `STATUS.md`：Current Stage / Checkpoint / Completed（Stage 4）/ Created / Modified / Known Issues / Deferred / Next 同步 Stage 4（Reference Changes：Stage 1~3 文件零改动）
- `TASKS.md`：新增 Stage 4 T401~T413 并全部勾选

### Fixed (Stage 4)

- T411 静态审查中补入 1 项：SKILL.md STEP 12 增加"可见性 ≠ 覆盖：normal 报告禁止固定 16 行数据库式报告"的显式表述（第 28 项检查）

### Added (Stage 3 — 输出体系)

- 创建 `references/report-format.md`：报告呈现规范 16 节（Report Principles / Information Priority / 默认 FULL_SCAN 模板（先看结论 + 核心排雷 16 字段 + 最需要注意 + 和你的偏好 + 有争议无法确认 + 依据）/ SPECIFIC_RISK 100~300 字单问直答 / FIT_CHECK 匹配度五档 + 建议五档 + 无偏好降级 / Spoiler Levels（none 禁令清单、light 默认、full 仅显式）/ Detail Levels（normal 300~700 字、detailed 700~1500 字软目标）/ Confidence 与 Agreement 用户可见措辞表 / Preference Integration / Sources / Unknown Cases（冷门措辞、禁强行补全）/ Ongoing Novels（信息截至、结局暂不评价）/ Formatting Rules / Prohibited Output Patterns（伪精确评分、台账倾倒、AI 废话等））
- 补全 `config/preferences.example.yaml`：空骨架 → 完整模板（version / spoiler_level / hard_no / strong_dislike / dislike / neutral / like / interests / output：show_confidence / show_sources / default_detail，逐项带 taxonomy 映射注释）
- `references/preference-guide.md`：新增 §6.1 Preference → Report 映射表（各命中类型的报告落点与输出逻辑，Stage 3 唯一允许的输出/配置映射补充）
- 创建 `docs/OUTPUT-EXAMPLES.md`：DEVELOPMENT ARTIFACT（虚构示例五例：默认 light+normal / 无剧透 none / 指定雷点 SPECIFIC_RISK / 详细+偏好 FIT_CHECK detailed / 冷门 UNKNOWN；末尾含 T312 十二项一致性检查记录）

### Changed (Stage 3)

- `STATUS.md`：Current Stage / Checkpoint / Completed（Stage 3）/ Created / Modified / Key Decisions / Deferred / Next 同步 Stage 3
- `TASKS.md`：Stage 3 任务按原始执行规范编号 T301~T313 重写并全部完成

### Fixed (Stage 3)

- T312 检查过程中修正：示例 D 原结论"比较适合/可以尝试"违反硬雷封顶规则（hard_no=CONFIRMED → 建议不高于不推荐），改为"比较不适合/不推荐"并展示封顶逻辑；示例 A 水文措辞同步为"已确认"（与示例 D 硬雷命中一致）；示例 D "41 卷开始？——不"草稿式表述删除；示例 B 无偏好语境下"雷发刀"改为客观描述（不假定用户雷什么）

### Added (Stage 3, REVISION 1)

- `docs/OUTPUT-EXAMPLES.md`：新增示例 F（FULL_SCAN + detailed + light，虚构《烬土回响》）——验证 ending-reception = mixed（CONFIRMED / DIVIDED）语义："有充分证据确认读者对结局评价明显两极"，含三点准确含义（确认"分化"本身/两派具体内容/非"信息不可靠"非"矛盾无法判断"非"烂尾"），并演示 §4.4 可见性规则（9 行 + 合并行）
- `PROPOSALS.md`：新增 V1.1 候选（interests 字段重新引入的前提条件）

### Changed (Stage 3, REVISION 1)

- `config/preferences.example.yaml`：删除 `interests`（未映射 taxonomy CORE、无定义行为、与 like 重叠 → PROPOSALS V1.1 候选）；`output` 收敛为 show_confidence / show_sources 两项（`default_detail` 删除，与顶层 detail_level 重复）；新增顶层 `detail_level`；注释声明 spoiler_level / detail_level 权威位置唯一（一个概念一个配置位置）
- `references/preference-guide.md`：§6 删除"个人信息匹配度五档"，只保留 Recommendation Scale（推荐 / 可以尝试 / 观望 / 谨慎 / 不推荐），匹配改用自然语言描述；§3 字段表 output 行收敛；§3.1 兴趣式描述两行注明"写在 like 中时"；§6.1 命中表删除 interests 引用
- `references/report-format.md`：§4 明确 RESEARCH COVERAGE ≠ REPORT VISIBILITY（调查可覆盖 16 CORE，normal 展示 6~10 个最重要维度 + 可选"其余维度快速检查"合并行；必须展示 hard_no / 显式询问 / strong_dislike / 关键 UNKNOWN / DISPUTED / DIVIDED；可按价值省略 not-applicable / neutral 低相关 / 无有效信息辅助维度）；图标语义（✅⚠❌❓ = USER IMPACT，不是 Confidence；无偏好时禁止 ❌ 默认标签）；§6 删除"匹配度五档"模板行，硬雷封顶声明为规则层规则（hard_no + CONFIRMED → 建议 = 不推荐）；§11 措辞引用改为 Recommendation Scale + 自然语言匹配；§16 新增"固定 16 行数据库式报告"与"图标当作证据强度/无偏好打 ❌"两条禁止项
- `docs/OUTPUT-EXAMPLES.md`：示例 A 核心排雷 16 行精简为 10 行 + "其余维度快速检查"合并行（演示可见性规则）；T312 检查扩展为 16 项并逐项标注结果与映射关系

### Fixed (Stage 3, REVISION 1)

- 示例 A 一句话结论原"雷快节奏和爽点密集的请谨慎"在无偏好配置下假定用户雷点 → 改为读者类型双向中性描述（"偏好快节奏、爽点密集的读者可能不适应"）

### Added (Stage 0)

- 初始化项目目录结构：`references/`、`config/`、`evals/`、`docs/`
- 创建 `SKILL.md` 最小骨架（完整工作流将于 Stage 4 编写）
- 创建 `README.md` 基础结构（完整内容将于 Stage 8 完善）
- 创建 `LICENSE`（MIT）
- 创建 `.gitignore`
- 创建 `docs/DESIGN.md`（保存 V1.0 完整设计）
- 创建 `docs/DEVELOPMENT.md`（记录开发规则）
- 创建 `TASKS.md`（Stage 0~8 任务清单）
- 创建 `STATUS.md`（开发状态跟踪）
- 创建 `config/preferences.example.yaml` 空骨架
- 创建 `PROPOSALS.md`（改进建议登记）

### Fixed (Stage 0, REVISION 1)

- 补全 `docs/DESIGN.md`：原仅保存至三十八节，现按原始设计完整补全三十九~六十四节（含 V1 验收指标、Stage 0~8 详细开发流程、CHECKPOINT 机制、TASKS/STATUS 管理规则、Claude 自动执行规则、禁止范围膨胀规则、DeepSeek 适配原则、scripts=0 原则、V1.1~V3 规划、总控执行 Prompt、Stage 0 第一条任务、人工验收标准、项目最终定义）
- 统一文档引用规范：将 TASKS.md 与 preferences.example.yaml 中的"第XX章"编号引用改为规则名称引用，并在 DEVELOPMENT.md 新增《文档引用规范》规则

### Changed (Stage 2, REVISION 2)

- `references/search-playbook.md`：默认 spoiler_level 恢复为 light（与 DESIGN.md 一致，detail_level 默认 normal）；§3.3 增加四个规范解析示例（"排雷/无剧透排雷/详细排雷/完全剧透+详细"）；§10 全部 confidence 由 HIGH/MEDIUM/LOW 统一为 CONFIRMED/LIKELY/WEAK/UNKNOWN；§6.11 NO_SPOILER 表述改为 spoiler_level = none；示例 1 默认参数同步
- `references/source-policy.md`：§5.3 正确示例 confidence: HIGH → CONFIRMED
- `docs/RESEARCH-SIMULATIONS.md`：维度结果表 confidence 统一枚举；Case C saintliness 非法值 disputed → 合法值 unknown（agreement DISPUTED）；新增 E310《中国小说学会2025年度中国好小说》证据（2025-01-24 完结，页面级）
- `STATUS.md`：Current Stage / Checkpoint / Completed / Key Decisions / Simulations 同步 REVISION 2

### Fixed (Stage 2, REVISION 2)

- 《剑来》完结日期证据修正（T224）：删除"精确完结日期未核验"表述，更新为中国小说学会2025年度中国好小说榜单（中国作家网 2025-12-21 页面级核验）：`烽火戏诸侯：《剑来》，纵横中文网，2025年1月24日完结` → serialization-status = completed（completion_date 2025-01-24，CONFIRMED / CONSISTENT）；2026-08-05 作家网书评保留为背景证据（首发平台/连载起点），不再作为完结日期证据
- TASKS.md：T204 任务描述去除 NO_SPOILER / DETAILED（已非 Base Mode）

### Changed (Stage 2, REVISION 1)

- `references/search-playbook.md`：Request Mode 重构为 Base Mode（FULL_SCAN / SPECIFIC_RISK / FIT_CHECK）+ Modifiers（spoiler_level none|light|full / detail_level normal|detailed），全文件同步（§3/§5/§6.11/§13/§14/§17）；Evidence Ledger 原子化（one evidence item = one source-evidence pair，新增 evidence_id / claim_id / access_mode page|snippet|search-result，不增加 user_impact，§8）；新增 Claim Synthesis 层（Evidence → Claim → Dimension Result，§8.5）；§10 拆为 Dimension Value / Evidence Confidence（CONFIRMED/LIKELY/WEAK/UNKNOWN）/ Agreement State（CONSISTENT/DISPUTED/DIVIDED/INSUFFICIENT）三线；§15 重构为 Dimension Stop Conditions（4 条）与 Task Stop Conditions（7 条全满足），hard_no=CONFIRMED 不再是 Task Stop 条件；§11 冲突输出改用三层示例；§18 新增禁止项（多来源合并进一条 Evidence、snippet 静默升级、三概念混用）；§12.4 新增"旧帖预测不是事实"
- `references/source-policy.md`：§3.2 新增访问级别规则（page/snippet/search-result，禁止静默升级）；§3.3 AI SEO 规则改为"按具体页面评价，不建立域名黑名单"；§5 拆分为 Confidence Labels 与 Agreement States 两套标签（MIXED 不再作为 confidence）；§6 冲突处理先定 agreement 再定 taxonomy 值；§7 拆分 Dimension Stop / Task Stop
- `docs/RESEARCH-SIMULATIONS.md`：重写为 DEVELOPMENT / EVALUATION ARTIFACT（定位明确非 runtime reference）；按 T213 原子化证据表（逐条 access_mode / tier / independence_group）；T217 来源审计 11 项修正；T219 十二项检查结果

### Fixed (Stage 2, REVISION 1)

- RESEARCH-SIMULATIONS 来源审计修正（T217）：移除"七星阁书评"（其 URL 实为论坛首页，无法核验）；《诡秘之主》《玄鉴仙族》状态升级为起点 Tier A 页面级核验（已完本·1418章 / 连载中·1627章，2026-08-11 更新）；删除《剑来》"2025-01-21 完结"（无来源支持，改为"不晚于 2025-02-20 完结、精确日期未核验"）；网易《剑来》文章按页降级 Tier D（网易号自媒体"落星荷动漫"）；《玄鉴仙族》作者统一"季越人"（NGA"寄越人"为同音异写）；连载起点改为"约 2022-11 上架（首订 2022-11-25）"
- search-playbook §12 小节编号修正（12.2 模型记忆不可靠 / 12.3 连载作品 / 12.4 旧社区帖子 / 12.5 已完结作品）

### Added (Stage 2)

- 创建 `references/search-playbook.md`：调查执行手册，18 节（Purpose / 原则 / Request Modes / Identity Resolution / Query Strategy / Priority / Evidence Ledger / Verification / Conflict Resolution / Recency / Spoilers / Budget / Stop Conditions / Degradation / Examples / Prohibited Behaviors），IF → THEN / DO / DO NOT / STOP WHEN 形式
- 创建 `docs/RESEARCH-SIMULATIONS.md`：开发期验证记录（Case A《诡秘之主》/ Case B《玄鉴仙族》/ Case C《剑来》三本真实小说模拟、T211 十项一致性检查、共性问题、后续模拟计划）

### Fixed (Stage 2)

- `TASKS.md`：Stage 2 任务编号恢复为原始执行规范的 T201~T212（原误用 T201~T203 自定义编号）
- `references/source-policy.md`：§3.3 AI 生成来源补充 AI SEO 内容识别特征（实证：红袖读书 ask 类页面为模板化 AI 问答，曾与真实读者评价冲突）
- `references/search-playbook.md`：§12 新增"模型记忆不可靠"（实证：《宿命之环》《赤心巡天》模型记忆均为连载中、实际已完结）与"旧帖预测非事实"规则

### Added (Stage 1)

- 创建 `references/taxonomy.md`：统一雷点术语体系（relationship / protagonist / plot / worldbuilding / ending 五大域的 19 个标准 ID、通用分类原则、证据交互规则、边界情况速查、术语对照表）
- 创建 `references/source-policy.md`：来源等级 Tier A~D、事实与评价分离、证据标签 CONFIRMED~UNKNOWN、冲突处理、停止搜索条件、绝对禁止清单
- 创建 `references/preference-guide.md`：偏好配置加载、匹配规则、硬雷优先机制、搜索顺序影响、输出尺度、偏好标签↔taxonomy ID 映射表
- TASKS.md：Stage 1 补充 T104（术语一致性核对）、T105（抽象情景示例库）

### Fixed (Stage 1, REVISION 1)

- TASKS.md：Stage 1 任务编号恢复为原始执行规范的 T101~T111（原误用 T101~T105 自定义编号）
- taxonomy.md：`system` → `system-intensity`（金手指/面板≠系统）、`worldbuilding` → `worldbuilding-scale`（规模≠质量）；power-system-consistency 增加 `not-applicable`；补充虐主（正常困难/失败/成长挫折）、慢热≠水文、水文判定禁令（长≠水）、剧情逻辑（角色选择≠逻辑差）、连载（长期没更新≠太监）、烂尾判定边界（排除清单+证据清单+默认表述）等判定规则；§8 明确 UNKNOWN/POSSIBLE/DISPUTED/MIXED 四者区别与示例；边界情况表与示例库扩充；新增 §12 V1 CORE(16)/AUXILIARY(3) 划分与"毒点不是字段"定义
- source-policy.md：Tier A 明确不能证明评价类信息；Tier B 转载官方简介不算独立来源；Tier C 表达必须为"社区评价/读者反馈"；Tier D 不能单独产生 CONFIRMED；新增来源质量附加规则（独立来源 / 搜索摘要 / AI 生成内容 / 时效性）
- preference-guide.md：hard_no+UNKNOWN → "该高优先级雷点无法确认，建议谨慎"；新增 hard_no+DISPUTED（争议提高至报告前部）；新增 §4.5 偏好影响边界（只能影响 4 项、不能影响 4 项）；映射表更新为新 ID
- PROPOSALS.md：登记未来候选（爽度 / villain-iq / forced-drama，V1 明确不采用）