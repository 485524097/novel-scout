# Novel Scout

> 在你花 50 个小时看一本小说之前，先排个雷。

Novel Scout 是一个「小说阅读前排雷」Agent Skill。给它一本小说，它会先搜索并核验真实信息，再检查后宫、NTR、系统、圣母、虐主、慢热、水文、结局争议等常见阅读雷点，并根据你的阅读偏好给出是否值得尝试的建议。

它不会靠"模型记忆"直接下结论——**先有证据，再有结论**。

## What it does

- 确认你说的是**哪一本**小说（作者、平台、连载状态），避免排错书
- 针对一本具体小说调查阅读雷点
- 区分：**已确认事实 / 较可信推断 / 证据较弱 / 无法确认**
- 对冲突信息做交叉验证，来源说法矛盾时如实并列，不替你"投票"
- 支持无剧透 / 轻度剧透 / 完整剧透三种模式
- 如果配置了个人偏好，判断是否踩你的雷，并给出建议

## Quick Start

将 `novel-scout` 目录安装/复制到你的 Agent 支持的 Skills 目录，并确保宿主能够读取 `SKILL.md` 与 `references/`。安装后直接对 Agent 说：

```
排雷《XXX》
```

下面是一些可以直接使用的请求：

| 请求 | 效果 |
|---|---|
| `排雷《XXX》` | 默认完整排雷（轻度剧透、普通详细度） |
| `无剧透排雷《XXX》` | 完全不剧透的完整排雷 |
| `《XXX》后宫吗？` | 只回答这一个问题，轻量快速 |
| `《XXX》有 NTR 吗？` | 只回答这一个问题，轻量快速 |
| `详细排雷《XXX》` | 更详细的报告 |
| `《XXX》适不适合我？` | 按你的个人偏好判断（未配置偏好时给出通用画像） |

## What it checks

Novel Scout 主要检查这些维度：

- 感情线与后宫（单女主 / 多女暧昧 / 明确后宫 / 无感情线）
- NTR / 感情背叛风险
- 系统存在感
- 主角圣母倾向
- 主角智商与行为逻辑
- 虐主程度
- 慢热 / 水文 / 重复套路
- 剧情逻辑
- 世界观规模
- 力量体系稳定性
- 连载状态与完结信息
- 结局评价（是否两极、是否被普遍视为烂尾）

完整枚举与判定规则见 `references/taxonomy.md`。

## How it works

1. 确认你说的是哪一本小说（身份优先，同名作品会请你消歧）
2. 搜索官方与读者来源，打开真实页面核验
3. 区分事实、读者评价和模型判断（证据台账逐条记录来源）
4. 对冲突信息做交叉验证，多数投票被禁止
5. 按严格 taxonomy 分类，标注置信度与共识状态
6. 如果配置了偏好，再判断是否踩你的雷（偏好不改事实判定）
7. 按剧透等级生成排雷报告

### Evidence before conclusion

Novel Scout 的核心原则是**证据先于结论**：

- 不靠模型记忆直接下结论，所有关键结论都必须有真实来源支撑
- 搜索结果摘要只是线索，不冒充页面证据
- 一个读者评论 ≠ 社区共识
- **UNKNOWN 是合法结果**：如果可靠信息不足，Novel Scout 会直接告诉你"无法确认"，而不是为了填满报告猜一个答案

## Personal Preferences

你可以配置自己的阅读偏好，让报告给出针对你的建议。

复制模板并修改：

```
config/preferences.example.yaml  →  config/preferences.yaml
```

示例（仅展示格式，不是推荐值）：

```yaml
version: 1

spoiler_level: light
detail_level: normal

hard_no:
  - ntr
  - harem

dislike:
  - heavy-system

like:
  - large-worldbuilding

output:
  show_confidence: true
  show_sources: true
```

说明：

- `hard_no` 是硬雷：一旦确认，最终建议直接是"不推荐"，不会被其他加分项抵消
- **`preferences.example.yaml` 只是模板，Novel Scout 不会把它自动当作你的真实偏好**；只有 `config/preferences.yaml` 会被读取
- 没配置偏好也能用——此时输出客观阅读画像，不做个性化建议
- **当前请求优先**：即使配置了 `dislike: [slow-burn]`，本次说"这次慢热没关系"，就以本次请求为准，配置文件不会被自动修改

## Spoiler Control

- `none`：无剧透（不透露关键死亡、最终伴侣、最终 Boss、身份反转、结局事件，但保留有用的结构级结论）
- `light`：轻度剧透（默认，允许结构级方向）
- `full`：完整剧透（仅在你明确要求时使用）

报告开头会标注当前剧透等级与信息截至日期。

## Evidence & Sources

- 所有结论基于真实搜索与页面访问；来源分级（官方页 / 百科 / 社区 / AI 聚合）明确标注
- 来源标题本身可能含剧透时，报告会脱敏处理
- 连载作品会标注"截至 YYYY-MM-DD"，不会把当前状态写成永久事实

## Limitations

诚实说明以下限制：

1. **社区评价本身具有主观性**——"好不好看""是否烂尾"输出的是"社区评价倾向"或"评价两极"，不是客观真理
2. **冷门小说可能只能得到 UNKNOWN**——资料不足时如实说"无法确认"，不会硬猜
3. **连载小说的感情线/雷点可能随剧情变化**——结论带时间边界，可能过时
4. **搜索结果质量取决于可访问的 Web 来源**——中文社区的可用来源分布不均
5. **某些社区页面可能无法访问**——部分网站有反爬限制，此时会降级处理并如实标注，不用摘要冒充页面
6. **Skill 不下载、不解析整本小说正文**——调查基于公开资料，不保证覆盖正文中未被讨论的内容
7. **V1 不提供小说推荐**——只排雷，不生成书单
8. **V1 不做多小说比较**——"哪本更适合我"这类请求需要逐本排雷自行对比
9. **自动触发（Runtime Trigger）尚未在可观测宿主上完成真实验证**——显式请求下 Skill 行为与真实 Web 流程已验证；自动路由需要在你安装的宿主上补测（见 Development Status）

## Project Structure

```
novel-scout/
├── SKILL.md                      # Skill 本体（编排层）
├── README.md                     # 本文件
├── CHANGELOG.md
├── LICENSE
├── .gitignore
├── config/
│   └── preferences.example.yaml  # 偏好模板（≠ 真实偏好）
├── references/                   # 运行时规则（SKILL.md 按需读取）
│   ├── taxonomy.md
│   ├── source-policy.md
│   ├── search-playbook.md
│   ├── preference-guide.md
│   └── report-format.md
├── evals/                        # 评估产物（运行时不需要）
├── docs/                         # 设计与开发文档（运行时不需要）
└── TASKS.md / STATUS.md / PROPOSALS.md
```

**运行时**只需要：`SKILL.md` + `references/` +（用户创建的）`config/preferences.yaml`。`docs/`、`evals/`、`TASKS.md`、`STATUS.md`、`PROPOSALS.md`、`CHANGELOG.md` 是开发与验证资料，正常运行不需要读取。

## Evaluation

Novel Scout 在开发阶段执行了静态与真实环境的评估。下列测试现在主要作为**回归保险**，不会被正常运行时读取，也不应反过来推动 Runtime 不断增加规则：

- 55 个触发路由案例（静态）
- 59 个行为规则案例（静态；21 个 critical）
- 7 个真实小说端到端案例（真实联网）
- 25 条重要证据的来源完整性抽查（fake source = 0）
- 3 个防幻觉挑战（虚构书名 / 极相似标题 / 同名消歧）
- 2 个全新小说冒烟测试

评估详情见 `evals/` 目录。**注意：以上是开发评估集中的结果，不是对真实世界的保证。**

## Development Status

- **Product Version**：1.0.0（Release Candidate / Unreleased）
- **Static trigger routing**：passed
- **Static behavior evaluation**：passed（59/59；21 critical）
- **Real-world web research evaluation**：passed（真实联网 E2E + 后续代表性回归已完成）
- **Automatic runtime trigger selection**：pending validation in a host where routing is observable（当前开发宿主无法观察自动 Skill 路由；这不代表 Skill 不可运行——显式请求下的完整流程已验证）

当前处于 **V1 RC / User Experience Trial**：核心 Runtime 已冻结，不再凭想象继续扩功能或增加规则。现在最重要的是正常用它排雷，记录真实体验中的速度、回答长度、UNKNOWN 比例、搜索质量、偏好匹配与剧透体验。Runtime Trigger 自动路由仍是宿主级 PENDING 项；它不阻塞显式调用与实际体验，但在补测前不能宣称“自动触发已验证”。正式 GitHub Release 仍需人工批准。

高频单雷点请求（例如“《X》后宫吗？”）现在走 **SPECIFIC_RISK Fast Path**：优先只加载短执行卡、目标 taxonomy 小节和单项报告规则；遇到来源冲突、时效或访问异常时才继续读取更多 policy。优化目标是减少固定上下文，不降低证据标准。

## License

[MIT](LICENSE)
