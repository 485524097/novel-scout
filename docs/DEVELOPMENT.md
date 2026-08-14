# Novel Scout 开发规则

本文档记录开发过程中的强制规则。所有开发者（Claude 或其他 Agent）必须遵守。

## 1. 阶段开发，禁止一口气交付

- 按照 `docs/DESIGN.md` 与 `TASKS.md` 定义的 Stage 顺序开发（Stage 0 ~ Stage 8）。
- 一次只完成当前 Stage 内的任务；同一 Stage 内可以自动推进。
- 到达任何 CHECKPOINT 必须立即停止，报告 CHECKPOINT READY 并等待人工确认。
- 未经确认不得进入下一 Stage。

## 2. V1 范围红线（绝对禁止）

- 不添加数据库、Web 后端、前端框架、账号系统、RAG 向量库、推荐系统。
- 不调用付费 API，不编写复杂爬虫。
- V1 编写 runtime scripts 的数量为 0。
- 不自行改变项目目标；不新增"像普通软件项目"的组件。
- 发现更好的设计 → 写入 `PROPOSALS.md`，先讨论后实施，不擅自实施。

## 3. 证据与诚实原则

- Skill 优先依赖真实检索证据，而不是模型记忆。
- 搜不到的信息必须允许输出 UNKNOWN / 无法确认。
- 不得伪造来源、网址、读者评价或小说剧情。
- 必须区分：事实信息、社区共识、社区争议、模型推断。

## 4. 报告要求

- 必须支持剧透等级（none / light / full）。
- 不输出伪精确评分（如"匹配度 83.7%"）。
- 硬雷优先：用户 hard_no 项被 CONFIRMED 时，结论不得高于"不推荐"。

## 5. 测试纪律

- 所有重要规则必须有测试（触发测试、行为测试、幻觉测试、人工真实小说测试）。
- 测试失败时，优先修改规则 / SKILL 工作流 / taxonomy / source-policy，禁止"只改测试让测试通过"。
- 不要为了通过测试而降低验证标准。

## 6. 任务跟踪

- 每完成一个 Task 更新 `TASKS.md`（勾选）与 `STATUS.md`（记录变更与下一步）。
- STATUS.md 必须持续反映：Current Stage、Completed、Changed Files、Tests、Known Problems、Next。

## 7. 修改纪律

- 不允许无理由重构项目架构；不删除已有功能。
- 优先最小修改解决问题；保持项目代码风格和命名规范。
- 修改任何重要文件后，在 STATUS.md 中说明修改原因与影响。

## 8. 文档引用规范

- 引用 docs/DESIGN.md 时，**优先写规则名称**（如《V1 验收指标》《禁止 Claude 做的事情》《Claude 自动执行规则》），不要依赖"§XX / 第XX章"这类容易变化的编号引用。
- 规则名称优先取自 DESIGN.md 中的章节标题（"## XXX、" 部分）。
- 只有在编号确实稳定且必要（如 CHECKPOINT 编号）时才使用编号。

## 9. Development Stages（Stage 0~8）

| Stage | 内容 | 关键产物 | 检查点 |
|---|---|---|---|
| 0 | 项目初始化 | 目录结构 / DESIGN / TASKS / STATUS | CHECKPOINT-0 |
| 1 | 领域规则建立 | references/taxonomy.md、source-policy.md、preference-guide.md | CHECKPOINT-1 |
| 2 | 搜索与证据系统（含 REVISION 1/2） | references/search-playbook.md；Evidence/Confidence/Agreement 三层分离 | CHECKPOINT-2 |
| 3 | 输出体系与偏好配置（含 REVISION 1） | references/report-format.md、config/preferences.example.yaml、docs/OUTPUT-EXAMPLES.md | CHECKPOINT-3 |
| 4 | Skill 集成 | SKILL.md（可安装编排层） | CHECKPOINT-4 |
| 5 | 触发评估 | evals/trigger-cases.yaml（55 例）、TRIGGER-EVALUATION.md | CHECKPOINT-5 |
| 6 | 行为评估 | evals/behavior-cases.yaml（当前 59 例，含后续优化回归）、BEHAVIOR-EVALUATION.md | CHECKPOINT-6 |
| 7 | 真实世界 E2E | evals/real-world-cases.yaml（12 对象）、REAL-WORLD-EVALUATION.md、evidence/ | CHECKPOINT-7 |
| 8 | V1 定稿与发布准备 | README / CHANGELOG / RELEASE-CHECKLIST.md | CHECKPOINT-8 |

每个 CHECKPOINT 必须由人工确认后才可进入下一 Stage。

## 10. Evaluation Gates（V1 最终状态）

| Gate | 状态 | 说明 |
|---|---|---|
| Trigger Static Gate | **PASS** | 55/55 静态路由案例 |
| Trigger Runtime Gate | **PENDING** | 当前开发宿主无法观察自动 Skill 路由，尚未完成真实自动触发验证 |
| Behavior Static Gate | **PASS** | 当前 59/59 静态规则案例（21 个 critical 全 PASS） |
| Real E2E Gate | **PASS** | Stage 7 真实联网评估 + 后续代表性 Evidence 回归已通过 |

**Runtime Trigger 为什么 Pending**：这**不**意味着 Skill 无法运行——显式请求下的完整行为与真实 Web 流程已通过全部评估。准确含义是：

> 当前开发宿主无法直接观测自动 Skill routing，因此该项尚未完成真实自动触发验证；显式 Skill 行为与真实 Web E2E 已完成。

补测方式：将 Skill 安装到支持自动路由的宿主（如 Claude Code / OpenCode 等），执行 `evals/manual-smoke-tests.md` 中标记为 "Runtime Trigger" 的案例，观察请求是否被自动路由到 Novel Scout。

## 11. Runtime vs Development Artifacts

**Runtime（正常运行可能需要）**：

- `SKILL.md`
- `references/`（taxonomy / source-policy / search-playbook / preference-guide / report-format）
- `config/preferences.yaml`（仅当用户实际创建）

**Development / Evaluation（运行时不需要）**：

- `docs/*`、`evals/*`、`TASKS.md`、`STATUS.md`、`PROPOSALS.md`、`CHANGELOG.md`、`RELEASE-CHECKLIST.md`
- `config/preferences.example.yaml` 仅作 USER TEMPLATE，**不是**用户真实偏好，不得自动加载

SKILL.md 的 Reference Loading 只要求按任务读取相关 reference；宿主支持 partial read 时优先读取相关 heading。docs/ 与 evals/ 在正常执行中不得读取。

## 12. Release Process

1. Stage 0~7 的开发与真实 Web 基线已经完成；
2. 当前 V1 RC 进入 **Runtime Freeze / User Experience Trial**，不再凭理论场景继续扩规则；
3. 真实使用发现 Bug / UX 问题时，只修改必要规则，并重跑**受影响的回归案例**；只有改动涉及搜索、Evidence 或核心研究流程时才需要补真实 Web 回归；
4. 用户决定正式发布时，再执行最终 Release Checklist / CHECKPOINT-8 人工批准；
5. 人工批准后才允许 git commit / GitHub / tag / Release，开发流程不得自动发布。

## 13. Known Pending（V1 发布时已知遗留）

- **Trigger Runtime Gate = PENDING**：需在可观测自动路由的宿主上补测；它不阻塞显式调用，只限制“自动触发已验证”的发布宣称。
- **Real E2E Gate = PASS**：真实联网基线与代表性 Evidence 回归已经完成。
- **Runtime Simplification Freeze**：不再使用 Page Anchor、正式 Evidence Ledger、ACTIVE/OPPORTUNISTIC/ESCALATED 等框架式 Runtime 抽象；对应历史记录保留在 CHANGELOG/evals 中。
- 其余（multi-novel comparison、recommendation、interests 字段等）均为 V1.1+ 候选，见 PROPOSALS.md。