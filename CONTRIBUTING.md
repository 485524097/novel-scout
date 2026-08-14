# 贡献指南

感谢你有兴趣为 Novel Scout 做贡献。这个项目刻意保持「小、明确、实用」——请先理解它不是什么，再决定怎么帮它。

## 项目定位（请先读）

Novel Scout 是一个面向中文网络小说的**低剧透 AI 排雷 Skill**，核心任务只有一个：

> 帮用户在开书前判断这本书有没有他在意的雷。

**明确不做**：小说下载 / 阅读 / 追更、推荐系统、多书比较、数据库、Web 后端、RAG、复杂脚本、评分公式。V1 的 runtime scripts = 0。

在提任何改动前，请先通读：

- `docs/DESIGN.md`（总体设计）与 `docs/DEVELOPMENT.md`（开发规则）
- `SKILL.md` 与 `references/`（运行时行为）
- `RELEASE-CHECKLIST.md`（发布边界）

## 怎么贡献

### 报告 Bug / 体验问题（最有价值）

如实记录：请求原文、宿主环境、发生了什么、期望是什么。注意 Novel Scout 的「无法确认」是合法输出，不是 Bug。

### 提改进建议

直接开 Issue，或按 `PROPOSALS.md` 的格式登记到文档中。大规模改动（新增模式、新增雷点维度、改变证据标准）必须**先讨论再实施**，不要直接改核心逻辑。

### 提交 Pull Request

1. 保持改动最小，不顺手重构无关代码
2. 修改任何 runtime 行为（`SKILL.md` / `references/`）时，附上对应的 `evals/` 案例变化，并说明为什么需要改
3. 修改后更新 `CHANGELOG.md`（按 Keep a Changelog 格式）
4. 不要伪造测试结果，不要为了让测试通过而降低验证标准
5. 遵循项目证据原则：不编造来源、不把模型记忆当事实、搜不到就 UNKNOWN

### 测试你的改动

本仓库无自动化测试 runner，验证方式是：

- `evals/trigger-cases.yaml` / `behavior-cases.yaml` / `real-world-cases.yaml` 的 YAML 结构校验
- `SKILL.md` frontmatter 校验（name / description / compatibility / metadata.version）
- `references/` 五个 runtime 文件的引用完整性
- 真实联网人工冒烟（`evals/manual-smoke-tests.md`）

## 代码风格

- 中文文档为主，README 需要中英双语同步
- 报告与文档：短句、结论先行、不堆内部术语（CONFIRMED / Tier A 等只用于内部规则文件）
- 不添加注释性噪音；改动保持可追溯

## 协议

本项目采用 [MIT](LICENSE)。提交代码即表示你同意按该协议分发。
