# Novel Scout V1.0 总体设计

> 本文档为 V1.0 项目的完整设计，是后续所有开发的最高依据。
> 修改本文档属于重大变更，必须经过人工确认。

## 一、项目目标

项目名称：**Novel Scout**，Skill 名称：`novel-scout`。

项目定位：一个面向网络小说读者的小说排雷 Skill。它不是小说推荐机器人，也不是小说总结机器人。

V1 只解决一个问题：

> 当用户准备阅读一本小说时，通过联网检索小说基本信息、读者评价和争议信息，判断该小说是否存在用户在意的雷点，并给出有证据、有置信度、控制剧透程度的排雷报告。

典型使用：

```
排雷《小说名》
《小说名》能看吗？
帮我看看《小说名》有没有后宫。
无剧透排雷《小说名》
详细排雷《小说名》
《小说名》适不适合我？
```

目标不是回答得"像懂小说"，而是：

```
查得到 → 有依据地说
不同来源冲突 → 明确告诉用户有争议
查不到 → 明确说无法确认
绝对不能：模型凭记忆随便判断
```

## 二、V1 产品原则

### 原则 1：证据优先于模型记忆

对于以下信息：是否完结、是否后宫、女主数量、是否存在系统、是否烂尾、是否虐主、是否有 NTR、主角性格、是否慢热、是否水文。

- 如果具备联网能力：**必须搜索**。
- 如果不具备联网能力：**必须说明**："当前无法联网检索，因此无法可靠完成排雷。我可以仅基于已有知识进行低可信度讨论，但不会把它当作确认事实。"

默认情况下不要偷偷使用模型记忆替代检索。

## 三、V1 功能边界

### V1 必须实现

- **F01 小说身份确认**：书名、作者、平台（能确认时）、类型、当前状态。防止同名小说搞错。
- **F02 基本信息检查**：作者、连载/完结、小说类型、作品平台、大致规模、简介。属于事实型信息。
- **F03 核心雷点检查**（默认检查）：感情线、后宫、NTR/感情背叛、系统、主角圣母程度、主角智商表现、虐主、降智、慢热、水文、套路重复、世界观、力量体系稳定性、结局情况、烂尾争议。不是所有项目都必须有结论，"后宫：无法可靠确认"是允许的。
- **F04 用户偏好匹配**：个人偏好 → 小说排雷结果 → 适配判断。用户强雷（如后宫、NTR、严重圣母、严重虐主、烂尾）且检测到高可信确认时，最终直接"不推荐"，不因其他优点给高分。
- **F05 信息可信度**：已确认 / 高可信 / 中可信 / 低可信 / 存在争议 / 无法确认。
- **F06 剧透控制**：支持 none（无剧透）/ light（轻微剧透，默认）/ full（完整剧透）。
- **F07 来源展示**：报告最后提供来源依据，有 URL 时给 URL，没有可靠 URL 时不得编造。

### V1 明确不做什么

禁止加入：自动推荐小说、小说书架、阅读进度记录、自动追更、小说下载、正文爬取、小说全文分析、RAG、向量数据库、用户账号、数据库、Web 后端、APP、复杂 Python 服务。也不做"根据我看过的小说自动推荐下一本"（V2）。

> V1 宁可把一个功能做好，也不要堆功能。

## 四、总体架构

```
novel-scout/
│
├── SKILL.md
├── README.md
├── CHANGELOG.md
├── LICENSE
├── .gitignore
├── references/
│   ├── taxonomy.md
│   ├── source-policy.md
│   ├── search-playbook.md
│   ├── preference-guide.md
│   └── report-format.md
├── config/
│   └── preferences.example.yaml
├── evals/
│   ├── trigger-cases.yaml
│   ├── behavior-cases.yaml
│   └── manual-smoke-tests.md
└── docs/
    ├── DESIGN.md
    └── DEVELOPMENT.md
```

V1 不需要 `scripts/`。核心能力（搜索、阅读、证据判断、综合、输出）由 Agent 完成。未来出现稳定、重复、适合确定性程序化的步骤，再考虑增加 scripts。

## 五、各文件职责

- **SKILL.md**：项目核心。只负责：什么时候使用、执行流程、必须遵守的规则、什么时候读取哪个 reference、最终行为约束。不塞雷点定义、搜索规则、几十条例子、报告详细格式。
- **references/**：领域规则库，SKILL.md 按需读取。
- **config/**：个人偏好配置。
- **evals/**：测试体系。
- **docs/**：设计与开发文档。

## 六、SKILL.md 设计

Frontmatter 建议：

```yaml
---
name: novel-scout
description: Researches and evaluates a specific novel for potential reading deal-breakers and reader concerns, including romance structure, harem, NTR, system mechanics, protagonist behavior, abuse of the protagonist, slow pacing, filler, plot logic, ending quality, and other common "雷点/毒点". Use when the user asks whether a novel is worth reading, asks to 排雷/查毒点, asks whether a novel contains a specific trope or problem, or asks whether a novel fits their reading preferences.
compatibility: Requires web search or browser access for reliable research. File read access is optional and enables loading a personal preference profile.
metadata:
  version: "1.0.0"
---
```

目标：Claude Code 可用 + 其他 Agent Skills 客户端也尽可能可用。不使用过多专属 frontmatter。

## 七、SKILL.md 工作流程

```
STEP 1  理解用户请求
STEP 2  确定剧透等级
STEP 3  识别具体小说
STEP 4  确认小说身份
STEP 5  读取用户偏好
STEP 6  制定搜索重点
STEP 7  搜索事实型信息
STEP 8  搜索雷点评价
STEP 9  交叉验证
STEP 10 判定可信度
STEP 11 结合用户偏好
STEP 12 生成排雷报告
```

## 八、STEP 1：解析用户意图

- **A 标准排雷**（如"排雷《诡秘XXX》"）：执行完整核心雷点检查。
- **B 指定雷点**（如"《XXX》是不是后宫？"）：只重点搜索相关维度，顺带必要基本信息，不浪费资源。
- **C 无剧透排雷**（如"无剧透看看《XXX》怎么样"）：禁止输出关键人物死亡、重大反转、最终 Boss、结局具体事件、关键身份。
- **D 详细排雷**（如"详细排雷《XXX》"）：允许更多社区评价、争议点、依据、详细解释，但仍受剧透等级约束。
- **E 是否适合我**（如"《XXX》适不适合我？"）：必须优先读取个人偏好文件。

## 九、STEP 2：剧透等级

- **none**：只允许基本信息、标签、大方向评价、雷点存在与否（如"存在明显虐主剧情"），不解释发生什么。
- **light（默认）**：可以说明中期虐主、"是肉体虐/情感虐/事业挫折"，但不写关键人物和重大剧情结果。
- **full**：仅当用户明确表示"可以剧透/随便剧透/详细说"才允许进入。

## 十、小说身份确认机制

不能用户输入书名就直接认为知道是哪本。应该搜索书名、作者、平台、简介、类型，建立 identity：

```yaml
title:
author:
platform:
genre:
status:
aliases:
identity_confidence:
```

发现两本以上同名小说时，根据作者、平台、用户上下文自动判断；仍无法确定才询问用户（A. XXX，作者 XXX / B. XXX，作者 XXX）。绝不能把两本小说的信息混起来。

## 十一、来源等级系统（source-policy.md）

- **Tier A 第一方/官方来源**：官方小说平台作品页、作者主页、作者公告、出版社、官方简介。适合确认作者、状态、类别、章节情况、简介、作品名称。优先级最高。
- **Tier B 较可靠二手资料**：大型图书数据库、百科、正规图书介绍、可靠媒体采访。补充作品背景、出版信息、基本事实。
- **Tier C 社区评价**：知乎、贴吧、豆瓣、Reddit、论坛、书评社区、平台评论区。主要用于水不水、慢不慢、虐不虐、圣母、降智、烂尾争议、后宫争议等主观判断。社区来源不能假装成绝对事实。
- **Tier D 弱来源**：搜索摘要、自动聚合页面、营销文章、内容农场、无来源转载。只能用于寻找线索，不能单独作为高可信结论。

## 十二、事实和评价必须分离

"《XXX》已经完结"是事实型信息；"《XXX》后期很水"是评价型信息。报告不能写"后期很水"，应该写"社区评价倾向：部分读者认为中后期节奏有所拖慢"或"社区评价较一致：中后期存在较明显的篇幅膨胀问题"。

## 十三、证据标签

内部统一使用：`CONFIRMED / LIKELY / MIXED / WEAK / UNKNOWN`。

- **CONFIRMED 强证据**：如"官方平台显示已完结"。
- **LIKELY**：多个独立来源相互支持。
- **MIXED**：不同来源明显存在不同看法。
- **WEAK**：只有少量弱证据。
- **UNKNOWN**：无法可靠确认。

最终中文显示：已确认 / 较可信 / 存在争议 / 证据较弱 / 无法确认。

## 十四、绝对禁止的错误

1. 模型记忆冒充检索结果（"我记得这本应该是单女主"→"单女主 ✅"）。
2. 单个评论代表所有读者（一条"后期烂完了"→"❌ 烂尾"）。
3. 把搜索摘要当确定事实。
4. 编造来源（"据知乎网友普遍认为……"但实际没读过知乎）。
5. 编造 URL。
6. 为了填满报告而强行判断（UNKNOWN 完全合法）。

## 十五、雷点分类体系（taxonomy.md）

建立标准 ID，所有分析使用统一词汇。

### Relationship 感情相关

- **romance-level**：`none / low / medium / high / unknown`（感情线比重）。
- **romance-structure**：`no-romance / single / multiple-ambiguous / harem / unknown`。注意 `multiple-ambiguous` 与 `harem` 必须分开：多个女性角色有暧昧不等于明确后宫。
- **ntr**：`none / possible / confirmed / disputed / unknown`。不能因"女角色喜欢过别人"就判定 NTR。

### 主角相关

- **saintliness（圣母倾向）**：`0 无明显 / 1 轻微 / 2 中等 / 3 明显 / 4 极强 / unknown`。"善良"不等于"圣母"；只有出现不合理自我牺牲、反复放过严重威胁、明显违背角色利益的道德行为并持续造成严重后果，才能提高等级。
- **protagonist-iq**：`strong / normal / inconsistent / poor / unknown`。
- **decisive**：`low / medium / high / unknown`。"杀人多"不自动等于"杀伐果断"。

### 剧情结构雷点

- **system**：`none / light / medium / heavy / unknown`。判断系统存在感，不只是有没有系统。
- **protagonist-abuse（虐主）**：`none / light / medium / heavy / unknown`，可备注 `physical / emotional / career / relationship / mixed`。
- **slow-burn**：`low / medium / high / unknown`。
- **filler**：`low / medium / high / unknown`，只能主要依据社区评价。
- **repetitive-patterns**：反复打脸、反复副本、反复升级循环、重复套路。
- **plot-logic**：`strong / normal / inconsistent / weak / unknown`。

### 世界观相关

- **worldbuilding**：`small / medium / large / very-large / unknown`。
- **power-system-consistency**：`strong / normal / inconsistent / weak / unknown`，主要用于玄幻、仙侠、升级流。

### 结局相关

- **serialization-status**（尽量使用事实来源）：`ongoing / completed / hiatus / discontinued / unknown`。
- **ending-reception**：`positive / mostly-positive / mixed / mostly-negative / negative / unknown`。"烂尾"是非常强的判断，不因有人不喜欢结局就判烂尾；推荐输出"结局评价：存在较明显争议"。

## 十六、个人偏好系统

文件：`config/preferences.example.yaml`。模板建议：

```yaml
version: 1

spoiler_level: light

hard_no:
  - ntr

strong_dislike:
  - harem
  - heavy-protagonist-abuse
  - severe-saintliness
  - widely-disliked-ending

dislike:
  - heavy-system
  - heavy-filler
  - obvious-plot-logic-problems

neutral:
  - slow-burn
  - single-romance
  - kingdom-building

like:
  - large-worldbuilding
  - exploration
  - coherent-power-system
  - intelligent-protagonist
  - mysteries
  - foreshadowing

output:
  show_confidence: true
  show_sources: true
  default_detail: normal
```

这是示例，不能假定用户一定讨厌后宫/系统，必须让用户自己配置。

## 十七、个人配置加载规则

存在 `config/preferences.yaml` 则读取；不存在则使用通用排雷模式，不因没有 preference 拒绝工作。"匹配度"部分变成"未配置个人偏好，因此本次只进行客观排雷，不进行个人适配评分"。

## 十八、Preference 影响搜索顺序

若用户 `hard_no: [ntr, harem]`，Skill 应优先搜索 NTR、后宫、女主、感情线。因为若已发现明确硬雷，没必要先花大量时间研究世界观。搜索原则：高价值信息优先。

## 十九、搜索策略（search-playbook.md）

- **Phase A 身份确认**：`"小说名" 作者`、`"小说名" 官方`、`"小说名" 小说`。目标：书名、作者、平台。
- **Phase B 基本事实**：`"小说名" 完结`、`"小说名" 作者`、`"小说名" 作品页`。确认：状态、平台、类型。
- **Phase C 核心雷点**（根据用户偏好动态生成）：后宫、单女主、女主、NTR、圣母、主角性格、虐主、毒点、雷点、烂尾、结局、书评等。
- **Phase D 平衡检索**：不能只搜负面关键词（烂尾/毒点/垃圾），否则产生选择偏差；还要搜书评、评价、优点、缺点、推荐，获得完整社区评价。

## 二十、搜索预算

普通模式：搜索查询 4~8 次，页面阅读 5~12 个。详细模式可适当增加。原则"够用即停"：官方来源确认 + 多个社区来源一致时无需继续无限搜索。

## 二十一、冲突处理机制

来源 A"单女主"、来源 B"多女主"、来源 C"暧昧很多但最终单女主"——不能简单多数投票，应进一步调查"多女主指感情互动还是正式伴侣"。最终可能输出："感情结构：单女主，但存在多名女性角色的明显暧昧互动。可信度：中高。如果你雷后宫结局，问题不大；如果你连多女暧昧都雷，需要谨慎。"

## 二十二、排雷报告默认格式（report-format.md）

```
# 《XXX》排雷报告

一句话结论：……
剧透等级：轻微剧透
信息更新时间：YYYY-MM-DD

## 基本信息（作者/状态/类型/平台）
## 核心排雷（感情线/后宫/NTR/系统/圣母倾向/虐主/降智/慢热/水文/结局）
## 重点雷点（✅/⚠/❌/❓）
## 争议信息
## 和你的偏好匹配
## 最终建议（适合/谨慎/结论：推荐/可以尝试/观望/谨慎/不推荐）
## 信息依据（1. 2. 3. …）
```

## 二十三、不要伪造精确评分

不使用"匹配度 83.7%"这类伪精确数字。使用"很适合/比较适合/一般/比较不适合/明显不适合"或"推荐/可以尝试/观望/谨慎/不推荐"。

## 二十四、硬雷优先机制

用户配置 NTR = hard_no 且 NTR = CONFIRMED 时，最终建议不得高于"不推荐"。不因世界观、战斗、主角聪明而给出高分。

## 二十五、报告信息顺序

正确顺序：一句话结论 → 高危雷点 → 核心雷达 → 解释 → 来源。不要先长篇介绍作者历史背景。

## 二十六、特殊场景设计

- **A 冷门小说**：搜不到足够信息时输出"目前只确认到基本作品信息……其他项目暂时标记为无法确认。我不会根据模型记忆强行补全。"
- **B 正在连载**："截至当前公开剧情，未发现明确后宫结构。作品仍在连载，后续可能发生变化。"不能说成永久事实。
- **C 评价两极分化**：输出"该项目存在明显争议"，分别说明正反双方主要观点，不替用户选择哪一方是真的。
- **D 不同版本**：网络版、实体出版版、修订版必须区分。
- **E 同名作品**：必须身份消歧。

## 二十七、README 设计

面向普通使用者，建议结构：Novel Scout 是什么 / 为什么需要它 / 安装 / 快速开始 / 常见使用方式 / 个人偏好设置 / 剧透模式 / 可信度说明 / 示例 / 限制 / FAQ / 开发说明。

首页示例：

```markdown
# Novel Scout

> 在你花 50 个小时看一本小说之前，先排个雷。

Novel Scout 是一个 Agent Skill，用于调查一本小说是否包含你在意的阅读雷点。
```

## 二十八、测试体系（四类）

1. **触发测试**（evals/trigger-cases.yaml）：应该触发（排雷《XXX》、《XXX》怎么样？、《XXX》有后宫吗？、这本小说适合我吗？、无剧透看看……等）；不应该触发（帮我写一篇玄幻小说、给我续写这一章、润色小说、总结这章内容、设计世界观、取名）。
2. **行为测试**（evals/behavior-cases.yaml），至少 10 个 CASE：
   - CASE 01 正常知名小说：身份正确、来源正确、报告完整。
   - CASE 02 同名小说：必须消歧。
   - CASE 03 冷门小说：不知道就 UNKNOWN。
   - CASE 04 连载小说：不能把当前状态说成永久事实。
   - CASE 05 社区评价冲突：必须 MIXED。
   - CASE 06 用户强雷后宫 + 小说确认后宫：最终不推荐。
   - CASE 07 用户强雷后宫 + 证据不足：不能直接不推荐，应"高风险项目无法确认，建议谨慎"。
   - CASE 08 无剧透模式：不得泄露重大人物死亡、结局、最终反派、关键身份反转。
   - CASE 09 只有一个极端社区评价：不能升级成社区共识。
   - CASE 10 没有网络工具：Skill 正确降级。
3. **幻觉测试**（最关键）：故意提供几乎搜不到的虚构小说名，期望"无法确认该作品"，而不是编造作者/类型/后宫。
4. **人工真实小说测试**（evals/manual-smoke-tests.md）：2 本知名、2 本连载、1 本争议较大、1 本感情线复杂、1 本冷门。人工检查是否搞错书、编造事实、过度剧透、抓到真实雷点、反映来源争议。

## 二十九、V1 验收指标

小说身份错误 0；虚构来源 0；虚构 URL 0；明显无证据事实判断 0；强争议内容当作确定事实 0；无剧透模式重大剧透 0。触发测试正例基本全部触发、负例基本不触发。真实测试至少 7 本小说，通过人工检查后才允许发布 V1。

## 三十、开发流程与阶段

采用：Claude 主执行 + 阶段自动开发 + 关键节点人工确认。不要一次性生成整个项目。

- **Stage 0 项目初始化**：创建仓库、目录、基础文件、TASKS.md、STATUS.md。不写复杂 Skill 内容。→ CHECKPOINT 0
- **Stage 1 领域规则建立**：taxonomy.md、source-policy.md、preference-guide.md。先定义什么叫后宫/NTR/圣母/虐主/烂尾/证据充分，不先写 SKILL.md。→ CHECKPOINT 1
- **Stage 2 搜索与证据系统**：search-playbook.md、source-policy.md 完善，设计身份/基本事实/雷点/社区交叉搜索、冲突处理、停止条件，用 2~3 本真实小说手工模拟。→ CHECKPOINT 2
- **Stage 3 输出体系**：report-format.md、preferences.example.yaml，输出普通/无剧透/指定雷点/详细四种示例报告。→ CHECKPOINT 3
- **Stage 4 编写真正的 SKILL.md**：短、清楚、动作明确、知道何时读 references，不复制 references 内容。→ （进入 Stage 5）
- **Stage 5 Skill 触发测试**：安装到测试位置（如 `~/.claude/skills/novel-scout/`），测该触发时触发、不该触发时不触发。→ CHECKPOINT 4
- **Stage 6 行为测试**：跑 10+ behavior cases，逐项记录 PASS/FAIL/原因/修改。禁止遇到失败只改测试，优先修改规则、Skill 工作流、taxonomy、source-policy。
- **Stage 7 真实小说测试**：至少 7 本，重点人工检查书名/作者/完结状态/感情结构/明显雷点/争议/结局评价。→ CHECKPOINT 5（正式发布前最重要的人审节点）
- **Stage 8 文档与发布**：完善 README、CHANGELOG、LICENSE、安装说明、示例，版本 v1.0.0。

## 三十一、任务管理与状态跟踪

- **TASKS.md**：项目根目录，Stage 0~8 全部任务化，带复选框与 CHECKPOINT。
- **STATUS.md**：每完成任务更新 Current Stage / Current Task / Completed / Changed Files / Tests / Known Problems / Next。避免长时间自动开发后不知道做到哪里。

## 三十二、Claude 自动执行规则

- 一次完成当前 Stage 内的 Task，允许在同一个 Stage 内自动推进。
- 遇到 CHECKPOINT 立即停止，输出"CHECKPOINT N READY"（已完成、主要设计、需要人工确认、未继续执行后续 Stage），等待用户"继续"。

## 三十三、禁止 Claude 做的事情

自行改变项目目标；自行增加数据库、Web 后端、前端框架、账号系统、RAG、推荐系统；自行调用付费 API；自行加入复杂爬虫；自行大规模重构已通过人工验收的阶段。发现更好设计时写入 `PROPOSALS.md`，不擅自实施。

## 三十四、DeepSeek 模型适配原则

不依赖 Claude 特有的复杂 prompt hack、动态注入、子 Agent frontmatter、实验特性。Skill 本体只使用 Agent Skills 通用 SKILL.md、普通 Markdown instructions、references、普通文件读取、联网搜索/浏览工具。保证 DeepSeek / Claude / Codex / 其他 Agent 切换后核心设计可复用。

## 三十五、第一版不写脚本

V1：`scripts = 0`。只有当实际使用证明某步骤模型每次重复做且适合确定性程序化，才能进入 V1.1 考虑脚本。

## 三十六、V1 使用体验目标（成功标准）

```
《XXX》排雷

结论：比较适合，可以开。
高危雷点：
✅ 未发现明确 NTR
⚠ 感情线存在多角色暧昧
⚠ 前期明显慢热
❌ 中后期部分读者认为篇幅偏水

核心信息：
后宫：存在争议
系统：无
圣母倾向：低
虐主：轻
慢热：高
结局：已完结
烂尾争议：中

你最需要注意：
如果你雷"明确后宫"，目前证据不足以认为它属于后宫。
但如果你连"多女角色长期暧昧"也不能接受，这本需要谨慎。

来源：……
```

## 三十七、版本路线

- **V1.1**：更方便的偏好配置。
- **V1.2**：只查一个雷点，优化搜索成本。
- **V1.3**：两本书比较（《A》和《B》哪个更适合我？）。
- **V2**：书荒模式（"我刚看完《XXX》，找本新的"：提取喜欢的特点 → 搜索候选 → 逐本排雷 → 最终推荐）。
- **V3**：个人书架（已看/想看/弃书）。

## 三十八、最终开发原则

Novel Scout 的竞争力不是"AI 知道很多小说"，而是：

> AI 不确定的时候敢说不知道，确定的时候能够告诉用户依据是什么。

最终价值：用户准备花几十小时看一本小说之前，用几十秒先确认它有没有自己完全不能接受的雷点。

---

# 第二部分：开发执行规范（原始设计 三十九~六十四）

> 本部分为原始总体设计的后半部分，按原始编号逐节保存。
> 其中三十九~六十为详细版执行规范，覆盖并细化第一部分同名主题章节（如《Claude 自动执行规则》《禁止 Claude 做的事情》等）；六十一~六十四为本项目总控执行指令，是开发过程的最高执行依据。

## 三十九、V1 验收指标

正式 V1 必须满足：

```text
小说身份错误：0
虚构来源：0
虚构 URL：0
明显无证据事实判断：0
强争议内容当作确定事实：0
无剧透模式重大剧透：0
```

触发测试目标：正例基本全部触发、负例基本不触发。真实测试至少 7 本小说，通过人工检查后才允许发布 V1。

## 四十、开发流程

采用：Claude 主执行 + 阶段自动开发 + 关键节点人工确认。不要让 Agent 一口气生成整个项目然后宣布完成，采用阶段开发。

## 四十一、开发阶段 Stage 0：项目初始化

Claude 执行：创建仓库、创建目录、创建基础文件、建立 TASKS.md、建立 STATUS.md。此阶段不写复杂 Skill 内容。

完成以后进行 **CHECKPOINT 0**：用户人工检查目录是否合理、是否擅自增加后端、是否擅自增加 Web、是否出现范围膨胀。通过后继续。

## 四十二、Stage 1：领域规则建立

Claude 创建：taxonomy.md、source-policy.md、preference-guide.md。重点：先建立什么叫后宫、什么叫 NTR、什么叫圣母、什么叫虐主、什么叫烂尾、什么叫证据充分。不要先写 SKILL.md——如果概念本身没定义清楚，SKILL.md 再漂亮也没有意义。

完成以后进行 **CHECKPOINT 1**：人工重点检查雷点定义是否符合正常小说读者理解、是否过度绝对化、是否存在明显错误定义。

## 四十三、Stage 2：搜索与证据系统

Claude 创建：search-playbook.md、source-policy.md 完善。设计：身份搜索、基本事实搜索、雷点搜索、社区交叉搜索、冲突处理、停止搜索条件。然后用 2~3 本真实小说手工模拟。

完成以后进行 **CHECKPOINT 2**：人工检查有没有真的查网页、有没有只看搜索摘要、有没有单一来源下结论。

## 四十四、Stage 3：输出体系

Claude 创建：report-format.md、preferences.example.yaml。然后输出普通模式、无剧透模式、指定雷点模式、详细模式的示例报告。

完成以后进行 **CHECKPOINT 3**：人工重点看这个报告你自己愿不愿意看、是不是太长、真正关心的雷点是不是放前面、有没有 AI 味特别重的废话。

## 四十五、Stage 4：编写真正的 SKILL.md

此时才编写 SKILL.md。SKILL.md 应：短、清楚、动作明确、知道什么时候读 references。不要复制 references 内容。结构：Frontmatter、Purpose、When to use、Core workflow、Spoiler handling、Preference handling、Evidence rules、Failure handling、Reference loading guide、Output rules。

## 四十六、Stage 5：Skill 触发测试

安装到测试位置（个人 Claude Code 环境可测试 `~/.claude/skills/novel-scout/`），然后测试"排雷《XXX》"与"帮我写小说"，验证该触发时触发、不该触发时不触发。

完成以后进行 **CHECKPOINT 4**。

## 四十七、Stage 6：行为测试

跑 10+ behavior cases，逐项记录 PASS / FAIL / 原因 / 修改。禁止遇到失败只改测试；优先修改规则、Skill 工作流、taxonomy、source-policy。

## 四十八、Stage 7：真实小说测试

至少 7 本，重点人工检查：书名、作者、完结状态、感情结构、明显雷点、争议、结局评价。

完成以后进行 **CHECKPOINT 5**。这是正式发布前最重要的人审节点。

## 四十九、Stage 8：文档与发布

完善：README、CHANGELOG、LICENSE、安装说明、示例。版本 v1.0.0。

## 五十、任务管理格式

项目根目录建立 TASKS.md，示例：

```text
# Novel Scout Tasks

## Stage 0
- [x] T001 Create repository structure
- [x] T002 Create base documentation
- [ ] CHECKPOINT-0

## Stage 1
- [ ] T101 Design taxonomy
- [ ] T102 Design source policy
- [ ] T103 Design preference system
- [ ] CHECKPOINT-1

## Stage 2
- [ ] T201 Design search workflow
- [ ] T202 Design conflict handling
- [ ] T203 Run research simulations
- [ ] CHECKPOINT-2
```

## 五十一、STATUS.md

Claude 每完成任务更新：Current Stage、Current Task、Completed、Changed Files、Tests、Known Problems、Next。目的：避免长时间自动开发以后 Claude 自己都不知道做到哪里。

## 五十二、Claude 自动执行规则

Claude 必须：一次完成当前 Stage 内的 Task；允许在同一个 Stage 内自动推进；遇到 CHECKPOINT 立即停止。输出：

```text
CHECKPOINT 2 READY

已完成：
...

主要设计：
...

需要人工确认：
1.
2.
3.

当前未继续执行后续 Stage。
```

然后等待用户"继续"，再进入下一阶段。

## 五十三、禁止 Claude 做的事情

Claude 在开发过程中禁止：自行改变项目目标、自行增加数据库、自行增加 Web 后端、自行增加前端框架、自行增加账号系统、自行增加 RAG、自行做推荐系统、自行调用付费 API、自行加入复杂爬虫、自行大规模重构已经通过人工验收的阶段。如果发现更好的设计：可以写到 PROPOSALS.md，但不能直接实施。

## 五十四、DeepSeek 模型适配原则

因为执行模型不是原生 Claude，项目设计不要依赖 Claude 特有的复杂 prompt hack、Claude 特有动态注入、Claude 特有子 Agent frontmatter、Claude 特有实验特性。Skill 本体只使用：Agent Skills 通用 SKILL.md、普通 Markdown instructions、references、普通文件读取、联网搜索 / 浏览工具。这样即使以后 DeepSeek、Claude、Codex、其他 Agent 切换，核心设计依然能够继续复用。

## 五十五、第一版不要写脚本

Claude 很可能看到完整 Skill 就想写 Python、写 API、写数据库、写搜索服务——明确禁止。V1：`scripts = 0`。只有当实际使用证明某个步骤模型每次重复做、且适合确定性程序化，才能进入 V1.1 考虑脚本。

## 五十六、V1 使用体验目标

理想使用：

```text
用户：排雷《XXX》

Novel Scout：《XXX》排雷

结论：比较适合，可以开。
高危雷点：
✅ 未发现明确 NTR
⚠ 感情线存在多角色暧昧
⚠ 前期明显慢热
❌ 中后期部分读者认为篇幅偏水

核心信息：
后宫：存在争议
系统：无
圣母倾向：低
虐主：轻
慢热：高
结局：已完结
烂尾争议：中

你最需要注意：
如果你雷"明确后宫"，目前证据不足以认为它属于后宫。
但如果你连"多女角色长期暧昧"也不能接受，这本需要谨慎。

来源：……
```

这就是 V1 最终成功标准。

## 五十七、V1.1 以后再考虑

V1 稳定以后：

- **V1.1**：增加更方便的偏好配置。
- **V1.2**：增加只查一个雷点，优化搜索成本。
- **V1.3**：增加两本书比较，例如《A》和《B》哪个更适合我？

## 五十八、V2

才考虑书荒模式："我刚看完《XXX》，找本新的。"工作流：提取喜欢的特点 → 搜索候选小说 → 逐本 Novel Scout 排雷 → 最终推荐。

## 五十九、V3

才考虑"已看 / 想看 / 弃书"个人书架。

## 六十、最终开发原则

整个项目必须始终记住：Novel Scout 的竞争力不是"AI 知道很多小说"，而是"AI 不确定的时候敢说不知道，确定的时候能够告诉用户依据是什么"。

最终价值：用户准备花几十小时看一本小说之前，用几十秒先确认它有没有自己完全不能接受的雷点。

## 六十一、给 Agent 的总控执行 Prompt

将以下内容作为整个开发项目的最高执行指令：

```text
你现在负责开发一个 Agent Skill 项目：Novel Scout。

请首先完整阅读项目中的 DESIGN.md、TASKS.md 和已有文件。
你的任务不是一次性生成整个项目，而是按照 TASKS.md 中定义的 Stage 顺序开发。

执行原则：

1. 严格保持 V1 范围。
2. 不添加数据库。
3. 不添加 Web 后端。
4. 不添加前端框架。
5. 不添加 RAG。
6. 不添加小说推荐系统。
7. V1 不编写 runtime scripts，除非项目设计明确修改。
8. Skill 必须优先依赖真实检索证据，而不是模型记忆。
9. 搜不到的信息必须允许输出 UNKNOWN。
10. 不得伪造来源、网址、读者评价或小说剧情。
11. 必须支持剧透等级。
12. 必须区分事实信息、社区共识、社区争议和模型推断。
13. 所有重要规则必须有测试。
14. 不要为了让测试通过而降低验证标准。
15. 每完成一个 Task 更新 TASKS.md 与 STATUS.md。
16. 同一个 Stage 内可以自动继续。
17. 到达任何 CHECKPOINT 后必须停止执行，不允许进入下一 Stage。
18. CHECKPOINT 时向我报告：完成了什么、修改了哪些文件、当前设计是什么、测试结果、需要我人工确认什么。
19. 未经确认，不得越过 CHECKPOINT。
20. 如果你发现项目设计存在问题，将建议写入 PROPOSALS.md，不要擅自扩大范围。

开发目标：最终交付一个真正能够安装使用的 novel-scout Agent Skill。

用户应该能够直接说"排雷《小说名》"，Skill 就能够：确认小说身份 → 联网调查 → 搜索用户关心的雷点 → 对来源进行交叉验证 → 控制剧透 → 区分事实、社区评价、争议和未知 → 结合个人偏好 → 给出简洁可信的小说排雷报告。

现在不要直接实现整个项目。从 Stage 0 开始。执行 Stage 0 所有任务。完成后停止在 CHECKPOINT 0。
```

## 六十二、Stage 0 给 Agent 的第一条实际任务

```text
开始执行 Novel Scout Stage 0。

要求：

1. 创建项目基础目录。
2. 创建：SKILL.md、README.md、CHANGELOG.md、LICENSE、.gitignore、TASKS.md、STATUS.md。
3. 创建 references/。
4. 创建 config/。
5. 创建 evals/。
6. 创建 docs/。
7. 将当前完整设计保存为 docs/DESIGN.md。
8. 创建 docs/DEVELOPMENT.md，用于记录开发规则。
9. SKILL.md 当前只建立最小骨架，不实现完整工作流。
10. preferences.example.yaml 当前可以为空骨架。
11. 创建完整 TASKS.md，将 Stage 0~8 转换成任务。
12. 初始化 STATUS.md。

不要：写 Python、创建前端、创建后端、增加数据库、开始实现 Stage 1。

完成后：输出 CHECKPOINT 0 READY。同时给出目录树、新增文件、每个文件用途、需要我人工确认的项目。然后停止。
```

## 六十三、第一阶段人工验收标准

当 Agent 返回 CHECKPOINT 0 READY 时，只检查五件事：

```text
① 目录有没有乱加东西
② 有没有偷偷变成一个普通软件项目
③ SKILL.md 是否仍然只是 Skill
④ Stage 是否拆好了
⑤ Agent 有没有停下来
```

通过后只需要说："CHECKPOINT 0 通过，进入 Stage 1。"后面的开发即可继续。

## 六十四、项目最终定义

Novel Scout V1.0 完成时，它应该满足：

```text
小：没有后台，没有数据库，没有一堆程序。
完整：有 Skill、有知识规则、有个人配置、有测试、有文档。
真正可用：能联网调查一本小说并排雷。
可信：不会把不知道的东西说成知道。
可扩展：以后可以自然发展成淘书、续粮和个人书架。
可学习：非常适合作为从零学习 Agent Skills 的第一个完整案例。
```
