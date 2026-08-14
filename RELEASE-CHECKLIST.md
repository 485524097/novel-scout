# Novel Scout V1 Release Checklist

> 用途：V1.0.0 发布前核查清单。
> 规则：**Product Logic Gates** 与 **Host Integration Gate** 分开判定；任何 PENDING 项不得勾成 PASS。
> 状态：**V1 RC / USER EXPERIENCE TRIAL（2026-08-13）**——核心 Runtime 已简化并冻结，可正常显式使用；正式 GitHub Release 仍需人工批准。

## Product Logic Gates

- [x] CHECKPOINT 0~7 历史流程已完成（历史状态；不等于当前版本重新验收通过）
- [x] SKILL.md frontmatter 有效（name: novel-scout / description / compatibility / metadata.version: "1.0.0"）
- [x] Runtime references 无断链（taxonomy / source-policy / search-playbook / preference-guide / report-format，T807 审计 5/5 存在）
- [x] preferences.example 不会被当真实配置（SKILL.md STEP 3 + README 均明确只读 config/preferences.yaml）
- [x] Trigger Static Gate PASS（55/55，Stage 5）
- [x] Behavior Static Gate PASS（当前 59/59；21 critical）
- [x] Real E2E Gate PASS（post-optimization：10/10 ledger re-audit + 3/3 fresh targeted live Web regression；不宣称重抓 Stage 7 全 12 对象）
- [x] Source Integrity：fake source = 0（25/25 抽查，Stage 7 T711）
- [x] Hallucination Challenge PASS（3/3，Stage 7 T716）
- [x] No-spoiler：major spoiler leak = 0（2 专项 6/6×2 + 真实 Case none 零泄漏，Stage 7 T710）
- [x] Scope Audit PASS（无 Python / scripts / JS / Web App / 数据库 / RAG / 推荐 / 书架 / 追更 / 爬虫，Stage 8 T810）
- [x] README 完整（Quick Start / Preferences / Spoiler Control / Limitations / Evaluation / Development Status）
- [x] LICENSE 存在（MIT）
- [x] CHANGELOG 完整（[1.0.0] - Unreleased，Stage 0~8 记录）
- [x] Manual Smoke Checklist 完整（9 项，evals/manual-smoke-tests.md）

## Host Integration Gate

- [ ] Runtime Trigger Gate — **PENDING**: requires validation on a host where automatic skill routing is observable（当前开发宿主无法观测自动路由；补测方式见 docs/DEVELOPMENT.md §10 与 evals/manual-smoke-tests.md ［Runtime Trigger］标记项）

## Known Pending / Notes

- Trigger Runtime Gate = PENDING；它只阻塞“自动触发已验证”这一宣称，不阻塞显式调用或 RC 真实体验。
- Real E2E Gate = PASS；对应 Evidence Integrity 回归已完成。
- 当前核心 Runtime 进入 freeze：不再因为理论边界继续增加规则；真实使用出现 Bug / UX 问题后再改。
- V1.1+ 候选（不实现，见 PROPOSALS.md）：multi-novel comparison / recommendation / interests / none 剧透边界细化等

## 发布动作（须人工确认后执行，开发流程不得自动执行）

- [x] Post-optimization Real E2E revalidation PASS
- [x] Runtime Simplification completed（保留 Evidence 底线，移除过度工程化 Runtime 抽象）
- [ ] Runtime Trigger Gate PASS（可选；若仍 PENDING，正式发布说明中不得宣称自动触发已验证）
- [ ] CHECKPOINT-8 / Formal Release 人工批准
- [ ] git init（如需）并提交
- [ ] 创建 GitHub 仓库（如需）
- [ ] 打 tag（如 v1.0.0）
- [ ] 创建 GitHub Release
