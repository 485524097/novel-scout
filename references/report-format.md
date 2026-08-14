# Novel Scout Report Format

> 目标：让用户先看到“能不能看 / 有没有这个雷”，而不是研究过程。证据规则见 `source-policy.md`，搜索规则见 `search-playbook.md`，偏好规则见 `preference-guide.md`。

## 1. Purpose

报告只服务三个问题：**结论是什么、对我有什么影响、依据够不够。**

## 2. Report Principles

- 结论先行，来源放后。
- 用户显式询问项 / hard_no / strong_dislike 靠前。
- normal 一分钟内读完；SPECIFIC_RISK 更短。
- 不输出搜索流水账、内部证据结构、伪精确评分。
- 输出必须服从 spoiler_level。

## 3. Information Priority

默认顺序：

```text
一句话结论
→ 最重要雷点
→ 核心结果
→ 偏好匹配（如有）
→ 争议 / UNKNOWN
→ 关键来源
```

作者、平台、字数等身份信息只在有助于消歧或理解状态时简短出现。

## 4. Default Full Scan

FULL_SCAN normal **只展示重要结果**，通常 6~10 项；不要固定打印全部 CORE。

优先展示：

- 用户显式询问项；
- hard_no / strong_dislike 命中；
- 明显影响开书决策的雷点；
- 关键 DISPUTED / DIVIDED / UNKNOWN。

其余无明显风险项可以合并成一句“其余快速检查”。

示例结构：

```md
# 《XXX》排雷

一句话结论：……
剧透等级：轻微剧透｜信息截至：YYYY-MM-DD

## 先看结论
- ⚠ 主要注意：……
- ✅ 明确没有 / 较符合：……
- ❓ 暂时无法确认：……

## 核心排雷
- 感情结构：……
- NTR：……
- 系统：……
- 主角体验：……
- 节奏：……
- 结局评价：……

## 依据
- 来源 1
- 来源 2
```

图标表示**对用户的影响**，不是 confidence；无偏好时不要擅自把后宫、系统、慢热等打成 ❌。

## 5. Specific Risk Report

目标：**100~300 字左右直答，不返回完整排雷报告。**

第一句必须直接回答：

> 是。 / 不是。 / 目前无法确认。

随后只补：

1. 一句必要解释；
2. confidence / 争议边界；
3. 1~3 个关键来源。

不要顺带展开世界观、战力、慢热、结局等无关字段。

## 6. Fit Check Report

最终建议只使用：

> **推荐 / 可以尝试 / 观望 / 谨慎 / 不推荐**

推荐结构：

```md
# 《XXX》适不适合我？

建议：不推荐
一句话：踩中你的后宫 hard_no；其他优点不能抵消该硬雷。

## 与你的偏好
- [硬雷] 后宫：已确认
- [加分] 世界观：较符合

## 依据
- ……
```

规则：

- hard_no + CONFIRMED → 不推荐；
- hard_no + UNKNOWN / WEAK → 谨慎；
- hard_no + DISPUTED → 把争议提前并偏向谨慎；
- 没有个人配置时，只做客观排雷，不伪造“适合度”。

## 7. Spoiler Levels

- **none**：只给结构级结论；禁止关键死亡、重大反转、最终身份、具体结局事件。来源标题有剧透时脱敏。
- **light（默认）**：可说雷点类型和大致阶段，不展开关键事件。
- **full**：用户明确允许后才能详细说剧情。

用户当场明确“可以剧透”可以升级；否则默认取更保守的输出。

研究阶段可阅读必要剧透材料，但输出仍受本节约束。

## 8. Detail Levels

- **normal**：FULL_SCAN 约 300~700 中文字；SPECIFIC_RISK 更短。
- **detailed**：约 700~1500 中文字，可增加解释和来源，但仍不贴研究流水账。

字数只是软目标；优先保证清楚和不重复。

## 9. Confidence Display

内部标签对用户轻量显示：

| 内部 | 用户可见 |
|---|---|
| CONFIRMED | 已确认 / 多来源一致 |
| LIKELY | 较可信 |
| WEAK | 证据较弱 |
| UNKNOWN | 无法确认 |

若 `output.show_confidence: false`，普通项可隐藏这些措辞；争议和 UNKNOWN 仍需说明。

不要直接把 `CONFIRMED / LIKELY / WEAK / Tier A` 等内部术语倾倒给普通用户。

## 10. Agreement / Conflict Display

| 内部 | 用户可见 |
|---|---|
| CONSISTENT | 各来源基本一致 |
| DISPUTED | 存在说法冲突 |
| DIVIDED | 读者评价明显两极 |
| INSUFFICIENT | 依据不足 |

DISPUTED / DIVIDED 时，简短列出双方**具体差异**，不要多数投票，也不要模糊成“可能都有道理”。

## 11. Preference Integration

偏好只改变：

- 哪些雷点放前面；
- 哪些项重点提示；
- 最终建议。

不能改变事实、taxonomy、confidence 或来源标准。无法映射的偏好项要告诉用户，不静默丢弃。

## 12. Sources

- normal 通常列 2~5 个真正支撑结论的关键来源。
- 优先列实际打开并核验的页面；snippet 不冒充“已页面核验”。
- 不贴内部字段、证据编号或完整搜索清单。
- `output.show_sources: false` 可隐藏常规来源列表；但用户显式追问依据、存在 hard_no 争议或关键 UNKNOWN 时，仍给最小必要来源说明。
- URL 不确定就不编。

## 13. Unknown Cases

UNKNOWN 是合法结果。

推荐措辞：

- “目前无法可靠确认，公开资料较少。”
- “只找到摘要级线索，暂时不把它当成确定结论。”
- hard_no： “这个硬雷目前无法确认，建议谨慎。”

不要把“没搜到”改写成“应该没有”。

## 14. Ongoing Novels

连载作品的感情结构、NTR、状态等动态结论注明：

> 截至 YYYY-MM-DD。

连载中的“可能烂尾”只能写成读者担忧，不能当 ending-reception 事实。

## 15. Formatting Rules

- 中文、短句、少段落。
- 最多三级标题。
- ✅ / ⚠ / ❌ / ❓ 表示用户影响，不表示证据强度。
- 不用百分比、星级、8/10 等伪精确评分。
- 不写“综上所述”“希望能帮到你”等 AI 套话。

## 16. Prohibited Output Patterns

- SPECIFIC_RISK 输出完整 16 维报告。
- 固定打印所有 CORE 字段。
- 结论放在作者简介和研究过程之后。
- 把社区评价写成绝对事实。
- 把单条评论写成社区共识。
- hard_no 已确认仍给推荐 / 可以尝试。
- 无剧透模式泄露关键事件。
- 强行补全 UNKNOWN。
- 倾倒内部证据笔记、搜索日志或模型推理过程。
