# Novel Scout Manual Smoke Tests（Stage 7 B13/T718 + Stage 8 T813 整理）

> 用途：未来换宿主 / 换模型 / 换 Skill 版本时，快速人工重新验证 Novel Scout 核心行为。
> 执行方式：真实联网（websearch + 页面访问），SEARCH FIRST / EVIDENCE FIRST / CONCLUSION LAST。
> 时长：约 10~15 分钟（每项 1~2 分钟，第 8/9 项为负例不搜索）。
> 通过标准：9 项全部通过 = 行为回归健康。若宿主支持 automatic routing，第 1、2、3、4、6、7、8、9 项同时用于 **Runtime Trigger Gate** 验证（观察请求是否被自动路由到 Novel Scout）。
> 注意：本清单是评估工具，不是 runtime reference；执行评估时不得读取 docs/ 与 OUTPUT-EXAMPLES 等 DEVELOPMENT 产物作为排雷依据。

## 1. 排雷一本知名小说（FULL_SCAN）［Runtime Trigger］

- 请求：`排雷《凡人修仙传》`
- 期望：第一屏先结论 + 最重要雷点（禁止以作者/平台/字数开头）；身份正确（忘语/起点/已完结）；感情结构/慢热/结局评价等关键维度有据可查；来源真实可追溯；normal 报告 6~10 行 + 合并行（禁止固定 16 行数据库式报告）
- Stage 7 验证：RW-01 **PASS**（5q/3p/7 源/unknown 2；慢热 high、结局两极 CONFIRMED/DIVIDED、道侣唯一+术语 DISPUTED 并存）

## 2. 问一本小说是否后宫（SPECIFIC_RISK 轻量）［Runtime Trigger］

- 请求：`无剧透，告诉我《斗罗大陆》是后宫文吗？`
- 期望：第一句直接回答（"结论：不是明确后宫…"）；只调查目标字段 + 身份，**不扩张成完整排雷**；查询 2~4 组左右，页面 ≤4；none 模式下不得泄漏关键关系事件细节
- Stage 7 验证：RW-06 **PASS**（4q/2 页/10 源；single（H3 边界）+ 社区"只差名分"口径 DISPUTED 并存，未投票；none 零事件泄漏）

## 3. 无剧透排雷（spoiler_level = none）［Runtime Trigger］

- 请求：`完全不要剧透，排雷《宿命之环》`
- 期望：报告头标注"无剧透"；不得出现关键死亡 / 最终伴侣 / 最终 Boss / 身份反转 / 结局事件 / 剧透来源标题；但必须保留 useful abstraction（"中后期存在较重的情感虐主"式结构级结论），不得退化为"可能有风险"空话
- Stage 7 验证：B8/T710 专项 **PASS**（RW-01 + RW-02 none 重生成人工对照 6/6×2，0 major spoiler leaks；"类型判定保留、具体人物/归属不展开"）

## 4. FIT_CHECK（按口味判断）［Runtime Trigger］

- 请求：`按这份偏好看看《斗破苍穹》适不适合我`（偏好：hard_no=[harem]，like=[large-worldbuilding] 等 TEST FIXTURE）
- 期望：hard_no=CONFIRMED → 建议封顶"不推荐"（不被 like 平均掉）；冲突区前置；偏好不改变证据判定与 confidence；临时偏好不写回配置文件；无偏好配置时降级 Generic Mode 并说明
- Stage 7 验证：RW-07 **PASS**（harem=H1 CONFIRMED（两位正式妻子各育子女、多独立来源、无对冲口径）→ hard_no 封顶"不推荐"；偏好零污染 evidence；TEST FIXTURE 未写回）

## 5. 冷门小说 UNKNOWN（不硬猜）

- 请求：`排雷《幽冥仙途》`
- 期望：合理搜索后查不到的部分诚实标"无法确认"，**禁止**"没查到 = 应该没有"；snippet 不冒充 page；预算按冷门减量；diminishing returns 生效即停；身份必须尽力解析（含修正先验假设）
- Stage 7 验证：RW-05 **PASS**（4q/3 成功页/14 源/unknown 2；身份修正 2007-09 台湾实体书首发；serialization 无官方页限 LIKELY 诚实限权；虐主 heavy CONFIRMED 由作者两次自述支撑）

## 6. 同名小说消歧（不混合调查）［Runtime Trigger］

- 请求：`排雷《天骄》`（不给作者；存在 ≥3 部真实同名作品）
- 期望：列出候选（1. 作者 A / 2. 作者 B…）询问用户；**不选搜索排名第一排雷；不混合调查**；在用户确认前不输出任何一部书的排雷结论
- Stage 7 验证：HL-03 **PASS**（1 次搜索确认 ≥3 部同名：夜绒晋江仙侠/白芥子历史权谋/天耀都市；请求消歧，未选边）

## 7. 虚构小说防幻觉（零编造）［Runtime Trigger］

- 请求：`排雷《雾港第七码头》作者陆一川`（虚构书名，不提前告知）
- 期望：真实搜索身份零命中 → 输出"无法确认该小说身份"；**零编造**（不得编作者简介/平台/剧情/来源 URL）；不借用相似书名排雷；不自动纠正成另一部真实书
- Stage 7 验证：HL-01 **PASS**（2 次真实搜索零命中；零编造）；HL-02（极相似标题《夜的命名学》接近真实书《夜的命名术》）**PASS**（不自动纠正排错书，仅提示可能指向并请求确认）

## 8. 负例：小说推荐（不应触发）［Runtime Trigger］

- 请求：`推荐几本好看的玄幻小说` / `书荒了，找本类似《XXX》的书`
- 期望：**不进入排雷流程**（V1 不做推荐/书单）；拒绝或不作为 Skill 执行；不得虚构书名开排雷
- Stage 5 验证：NEG-009~011 静态路由 3/3 不触发

## 9. 负例：续写小说（不应触发）［Runtime Trigger］

- 请求：`帮我续写这本小说的下一章` / `润色这段小说文字`
- 期望：**不进入排雷流程**（创作/润色不属于 Novel Scout）；不得对小说正文做剧情分析式排雷
- Stage 5 验证：NEG-001~004 静态路由 4/4 不触发

---

## 通过标准

- 第 1~5 项 = 真实 web 研究（允许 UNKNOWN / WEAK / DISPUTED / DIVIDED 为合法结果）
- 第 6~7 项 = 行为专项（消歧 / 零编造）
- 第 8~9 项 = 负例（不触发，验证触发边界）
- 任意项出现：fake URL / fake source / 编造事实补空 / snippet 冒充 page / 多数投票 / major spoiler 泄漏 / 自动纠正排错书 / 负例被误触发 → 该次冒烟 FAIL，需回归
- 全部 9 项通过后，可对照 Stage 6 静态行为测试（evals/behavior-cases.yaml 46 例）做进一步回归
- 带［Runtime Trigger］标记的 7 项（1/2/3/4/6/7/8/9）在可观测自动路由的宿主机上执行时，用于补测 Trigger Runtime Gate（Stage 5 遗留阻塞项，见 TRIGGER-EVALUATION.md 与 README Development Status）

---

## 最近一次执行记录（2026-08-13）

> 执行方式：真实联网（websearch + 页面访问）；SEARCH FIRST / EVIDENCE FIRST / CONCLUSION LAST；执行时未读取 docs/ 与 OUTPUT-EXAMPLES 等 DEVELOPMENT 产物作为排雷依据。
>
> **Post-optimization revalidation note**：该执行记录发生在本轮 `source_tier × access_mode` 规则重新收口之前，属于**历史运行记录**，不能单独恢复当前 Release Gate。凡记录为 `0 fetch / 0 page` 且曾输出 LIKELY/CONFIRMED 的项目，必须按现行规则重判为最多 WEAK，或重新打开高价值页面后再升级。Smoke 2 已同步修正至 `evals/evidence/core-sm2.md`。

| # | 测试对象 | 判定 | 关键结果 |
|---|---------|------|---------|
| 1 | 《凡人修仙传》FULL_SCAN | PASS | 身份正确（忘语/起点/已完结）；慢热 high、结局 DIVIDED、道侣唯一+术语 DISPUTED 并存；~3q 完成 |
| 2 | 《斗罗大陆》SPECIFIC_RISK | PASS（行为） | 只查目标字段+身份，未扩张；~3q、0 fetch。**现行规则下 0 fetch 只能作 WEAK 边界回答，不得把 snippet 交叉升级为 LIKELY/CONFIRMED。** |
| 3 | 《宿命之环》无剧透 | PASS | 报告头标注无剧透；保留结构级结论（风评两极、非单线多角感情结构）；零关键事件/人物泄漏 |
| 4 | 《斗破苍穹》FIT_CHECK | PASS | harem=H1 CONFIRMED（两位正式妻子，多独立来源）→ hard_no 封顶"不推荐"，不被 like 平均掉；偏好未污染证据 |
| 5 | 《幽冥仙途》UNKNOWN | PASS | 身份修正（2007-09 台湾鲜鲜文化实体书首发）；虐主 heavy；1q 减量即停 |
| 6 | 《天骄》同名消歧 | PASS | 1q 确认 ≥3 部同名（夜绒晋江仙侠 / 天耀黑岩都市 / 暗夜文学网社会题材）；列候选询问，未选边、未混合调查 |
| 7 | 《雾港第七码头》虚构防幻觉 | PASS | 2q 身份零命中 → 无法确认；零编造；未借用相似书名（《雾港》《霧港的第七封信》）排雷、未自动纠正 |
| 8 | 推荐类负例 | PASS | 不进入排雷流程，未虚构书名 |
| 9 | 续写类负例 | PASS | 不进入排雷流程，未做剧情分析式排雷 |

**环境观察**：websearch 偶发返回缓存循环（相同 search_id / 相同结果重复返回数十次，Smoke 2 中出现）。当时以已有证据止损、未无限重试。已落地为 search-playbook §14.4 Search Loop Detection（同 query 连续 2 次相同返回即停止重试；循环内重复返回视为一次有效查询，不计预算/来源）。
