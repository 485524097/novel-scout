# Novel Scout Trigger Evaluation（Stage 5）

## Environment

- Host: opencode CLI（当前会话宿主；`opencode` 二进制不在 PATH，`~/.config/opencode/skills/` 不存在）
- Model: deepseek-v4-flash-free（opencode/deepseek-v4-flash-free）
- Skill loading method: 宿主 Skill 注册表（当前主机未安装任何 Skill 副本）
- Skill path: `/Users/admin/Projects/skill2/novel-scout/`（开发项目位置）
- Actual runtime trigger observable: **NO**

> 检查了 `~/.claude/skills/`（不存在）、`~/.config/opencode/skills/`（不存在）、全盘 novel-scout 目录（仅开发项目本身）。
> 本会话由模型自身执行评估，**无法从会话内部观察宿主对 Skill 的自动选择**，也无法以不可观察的方式伪造"已触发"。
> 因此本次执行 **STATIC ROUTING EVALUATION**（逐条对照 SKILL.md description / Use When / Do NOT Use 做路由判定）。
> 真实运行时触发验证未完成 → 已列为阻塞项（见 Remaining Limitations）。未安装任何副本到用户宿主配置目录（无既有副本可更新，且安装后本会话仍无法观察触发）。

## Evaluation Scope

- 只评估"Should Novel Scout be used?"（触发路由）
- 不评估排雷事实正确性、证据完整性、报告质量（Stage 6~7）
- 测试集：`evals/trigger-cases.yaml`，55 例（30 TRIGGER / 23 DO_NOT_TRIGGER / 2 CONTEXT_DEPENDENT；7 critical）

## Metrics

- Positive Trigger Recall：触发正例中路由为 TRIGGER 的比例
- Negative Rejection Rate：负例中路由为 DO_NOT_TRIGGER 的比例
- Context Routing Accuracy：CONTEXT_DEPENDENT 案例按给定上下文路由正确的比例
- Overall Accuracy：全部 55 例（含按上下文展开后的判定）路由正确的比例
- Critical Failure Count：critical 案例中路由错误的数量

## Round 1（T512，静态路由）

### Positive Cases（30/30）

- 显式 FULL_SCAN（POS-001~008）：全部路由 TRIGGER（description 覆盖 排雷/毒点/值不值得开/能不能看/劝退点）
- 隐式阅读前（POS-009~015）：全部 TRIGGER（description 的 before-reading / worth-starting / deal-breakers 语义覆盖）
- SPECIFIC_RISK（POS-016~023）：全部 TRIGGER（含无"排雷"字样的"后宫/NTR/圣母/虐主/水文/慢热/结局不满"直问）
- FIT_CHECK（POS-024~028）：全部 TRIGGER
- 7 个 critical 正例（POS-001 / POS-016 / CTX-001）全部通过

### Negative Cases（23/23）

- 创作类（NEG-001~004）、文学分析/总结（NEG-005~008）、推荐/书单（NEG-009~011）、元数据（NEG-012~014）、下载/更新（NEG-015~017）、多书比较（NEG-018~019）：全部路由 DO_NOT_TRIGGER

### Context Cases（2/2）

- CTX-001（准备开书 + "怎么样？"）→ TRIGGER
- CTX-003 / CTX-006（无上下文"怎么样？/好看吗？"）→ CONTEXT_DEPENDENT（不硬触发也不硬拒绝）
- CTX-002 / CTX-004 / CTX-007 / CTX-008 → DO_NOT_TRIGGER（文学分析 / 知识询问 / 闲聊 / 文笔讨论语境）

## Failures

**Round 1 无 case FAIL（55/55）**，但静态检查暴露 2 处**边界薄弱点**（设计缺口，非 case 失败）：

1. **元数据查询边界不显式**：SKILL.md Do NOT 清单未列出"作者是谁 / 什么时候完结"（内部使用 ≠ 用户触发能力的原则未落盘）。NEG-012/013 静态判定不触发，但依赖 description 未覆盖而非显式排除，防御性不足。
2. **多书比较边界不显式**：multi-novel comparison 未在 Do NOT 清单出现（"哪本更适合/哪本雷更多"）。NEG-018/019 静态判定不触发，但边界需显式化并登记 PROPOSALS。

## SKILL.md Changes

| 位置 | Before | After | Reason |
|---|---|---|---|
| Do NOT use this skill when | - 下载小说、查最新章节/更新状态 | + 查询作者、完结日期、平台等作品元数据（非阅读决策语境） | 元数据查询边界显式化（Round 1 薄弱点 1） |
| Do NOT use this skill when | （无比较条目） | + 多本小说相互比较（V1 未设计；可逐本排雷） | multi-novel 边界显式化（薄弱点 2） |

未修改：frontmatter.description（触发覆盖已达标且保持自然）、Use this skill when、Core Workflow、references 全部文件。

## Round 2（T515，回归）

- 修改后对 **全部 55 例** 重新路由（非仅失败项）：**55 / 55 PASS**
- 指标不变：Positive 30/30、Negative 23/23、Context 2/2、Overall 55/55、Critical 0

## Stability Check

对 10 个关键 case（POS-001 / POS-006 / POS-016 / POS-024 / CTX-001 / CTX-002 / CTX-003 / CTX-006 / NEG-002 / NEG-009）重复路由判定 2 次：

- 静态判定为确定性过程，10×2 结果一致，无 ROUTING INSTABILITY。
- 说明：静态评估无法度量真实宿主模型的随机性差异；"《示例小说》怎么样？/好看吗？"在真实宿主上的稳定性需真实触发验证（阻塞项）。

## Final Metrics

- Positive Trigger Recall: **30 / 30（100%）**
- Negative Rejection Rate: **23 / 23（100%）**
- Context Routing Accuracy: **2 / 2（100%）**
- Overall Accuracy: **55 / 55（100%）**
- Critical Failures: **0**

## Remaining Limitations（阻塞项）

1. **真实运行时触发验证未完成**：宿主未安装 Skill 副本、本会话无法观察自动触发。CHECKPOINT-5 结论为"静态路由评估通过 + 真实触发验证延期"，正式安装后需补做 Smoke Test（建议在宿主环境安装副本后，用 CTX-001/003/006 与 NEG-002/009 快速验证）。
2. Trigger stability 只做了确定性静态判定；真实模型随机性（ROUTING INSTABILITY）未测。
3. Reference-loading 观察：Stage 4 "每任务每 reference 只读一次"的绝对措辞在静态审查中未发现阻塞场景，故未改动；若真实运行出现"需要回看具体 section"的场景，按 PROPOSALS 思路放宽为 "by default once; revisit only when needed"。

## Conclusion

- Trigger Boundary（description / Use When / Do NOT Use）在静态路由评估下全部达标：0 critical failures、显式正例 100%、显式负例 100%、上下文 100%、总准确率 100%（55/55）。
- **Gate（静态）：PASS；真实运行时触发验证列为阻塞项，Checkpoint 结论按"静态通过、运行时待验"记录。**