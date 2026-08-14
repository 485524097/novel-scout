# PROPOSALS

> 开发过程中发现更好的设计时，记录于此。
> 本文件依据《禁止 Claude 做的事情》规则创建：发现更好的设计可以写入 PROPOSALS.md，但不能直接实施。
> 写入本文件 ≠ 立即实施。必须经过人工讨论确认后才能进入实施。

## 待讨论

- **默认 spoiler_level**：Stage 2 REVISION 1 曾实现默认 none，REVISION 2 已恢复为 light（与 DESIGN.md 一致）。若未来认为默认 none 更好，需人工确认后修改。
- **romance-structure 表达"无官配但有官方暧昧互动"**：当前可用 single + multiple-ambiguous 组合 + agreement 表达，无需新枚举；若社区语境确需 no-official-romance 语义，请人工评估后再决定是否新增。
- **none 剧透模式的价值验证（Stage 3 遗留观察）**：none 模式下手写"高风险剧情"抽象提示（示例 B）对硬雷用户的实际价值不明，且会降低无剧透承诺的可信度感知。建议 Stage 7 用真实小说 + 真实用户跑测后再决定是否保留该提示形式。

## V1.1 候选

- **multi-novel comparison（多书比较）**：Stage 5（T509/边界审计）确认"《A》和《B》哪个更适合我/哪个雷更多"不进入 V1 触发能力（trigger-cases NEG-018/019，SKILL.md Do NOT 已显式排除）。V1 可逐本排雷；若 V1.1 引入比较模式，需设计：多目标身份解析、统一报告合并、偏好相对比较语义。
- **interests（题材兴趣字段）**：Stage 3 REVISION 1（T316）已从 `config/preferences.example.yaml` 删除。原因：① 取值（mystery / exploration / kingdom-building 等）多为非 taxonomy CORE；② preference-guide §3.1 仅登记"兴趣式描述"行为（写在 like 中时仅作"可能加分"提示），独立 interests 字段没有定义任何精确行为；③ 与 like 字段功能高度重叠。若 V1.1 需要引入：必须先定义明确行为（如影响搜索优先级、报告"可能加分"提示的固定位置），再重新设计该字段。

## 未来候选（V1 明确不采用）

已由人工在 CHECKPOINT-1 REVISION 1 中确认不进入 V1 CORE taxonomy，记录备选：

- **爽度**：高度个人化，无法可靠定义与取证，不进入 V1；若未来出现可靠衡量方法再讨论。
- **villain-iq（反派智商）**：与主角降智常成对出现，但取证更困难，暂不采用。
- **forced-drama（强行制造冲突）**：与 plot-logic 部分重叠，待 V1 实践验证后再决定是否独立成字段。
