# Novel Scout Preference Guide

> 目标：让“适不适合我”简单可执行。偏好只影响优先级和建议，绝不反过来改变事实判断。

## 1. Purpose

taxonomy 描述“书里有什么”，preference 描述“用户能不能接受”。

不要默认用户讨厌后宫、系统、慢热或任何其他属性。

## 2. Profile Loading

- 用户配置：`config/preferences.yaml`。
- 没有配置 → 继续做客观排雷，不报错、不加载 example 当真实偏好。
- 用户本次明确说的偏好优先于文件配置，但默认不写回文件。

无配置时可简短说明：

> 未配置个人偏好，本次只做客观排雷。

## 3. Profile Fields

```yaml
version: 1
spoiler_level: light
detail_level: normal

hard_no: []
strong_dislike: []
dislike: []
neutral: []
like: []

output:
  show_confidence: true
  show_sources: true
```

含义：

- **hard_no**：确认命中即可不推荐。
- **strong_dislike**：明显降低建议。
- **dislike**：普通减分项。
- **neutral**：不影响建议。
- **like**：亮点提示；不能抵消 hard_no。

无法识别的偏好项不要猜映射，报告中提示“未能匹配”。

### 3.1 Preference Label ↔ Taxonomy Mapping

| 偏好标签 | 对应结果 |
|---|---|
| ntr | `ntr = confirmed`；possible/disputed 按争议处理 |
| harem | `harem = H1`；H2 只提示后宫倾向/争议 |
| heavy-protagonist-abuse | `protagonist-abuse = heavy` |
| severe-saintliness | `saintliness = high / extreme` |
| widely-disliked-ending | `ending-reception = negative` 且社区证据较一致 |
| heavy-system | `system-intensity = heavy` |
| heavy-filler | `filler = high` |
| obvious-plot-logic-problems | `plot-logic = weak / inconsistent` 且问题明显 |
| slow-burn | `slow-burn = high` |
| single-romance | `romance-structure = single` |
| pausing | `serialization-status = hiatus` |
| light-saintliness | `saintliness = light` |
| large-worldbuilding | `worldbuilding-scale = large / very-large` |
| coherent-power-system | `power-system-consistency = strong / normal` |
| intelligent-protagonist | `protagonist-iq = strong / normal` |
| kingdom-building / exploration / mysteries / foreshadowing | 兴趣描述，只作为 like 提示，不参与硬规则 |

匹配时先看**客观 Dimension Result**，再套本表；不要拿偏好标签直接判断小说事实。

## 4. Matching Rules

### 4.1 hard_no + CONFIRMED

→ **建议 = 不推荐。**

世界观好、主角强、文笔好等优点不能把硬雷平均掉。

### 4.2 hard_no + UNKNOWN / WEAK

→ **建议偏谨慎。**

推荐措辞：

> 这个高优先级雷点目前无法可靠确认，建议谨慎。

不能说“放心，没有”；也不能无证据直接定罪。

### 4.3 hard_no + DISPUTED

把争议提前，简要给出双方依据，建议偏向 **谨慎**。不要多数投票。

### 4.4 Preference vs Evidence

用户喜欢或讨厌某属性，都不能改变事实结论。

例如用户雷后宫，不会把“多女好感但无多伴侣关系”升级成 harem；用户喜欢后宫，也不能降低 harem 的确认门槛。

### 4.5 Preference Boundary

偏好可以影响：

- 搜索优先级；
- 报告排序；
- 风险提示；
- 最终建议。

偏好不能影响：

- 小说事实；
- taxonomy 分类；
- evidence confidence；
- 来源可靠性标准。

## 5. Search Priority

FIT_CHECK 的搜索顺序保持简单：

1. hard_no；
2. 用户本次明确问的项；
3. strong_dislike / dislike；
4. 有助于决定是否开书的 like / 其他信息。

如果 hard_no 已 CONFIRMED 且用户只问“适不适合我”，可以直接判不推荐，不需要为了完整画像继续深挖低价值字段。

## 6. Output Scale

最终建议只用这一套：

> **推荐 / 可以尝试 / 观望 / 谨慎 / 不推荐**

不用百分比、星级或“匹配度 83%”。

用自然语言解释原因，例如：

> 世界观和主角风格符合你的偏好，但踩中后宫 hard_no，因此不推荐。

### 6.1 Preference → Report

| 情况 | 输出重点 |
|---|---|
| hard_no CONFIRMED | 放最前；不推荐 |
| hard_no UNKNOWN / WEAK | 放前；谨慎 |
| hard_no DISPUTED | 放前；展示争议；谨慎 |
| strong_dislike | 明显提醒，建议下调 |
| dislike | 列为减分项 |
| like | 列为亮点，不抵消硬雷 |
| 无法匹配 | 明确告诉用户 |

## 7. Edge Cases

- **连载中**：适配结论写“截至 YYYY-MM-DD”，后续可能变化。
- **无配置**：只做客观排雷。
- **同名小说**：先消歧再做偏好匹配。
- **自由文本兴趣**：只作 like 提示；没有 taxonomy 对应时不硬造分类。
