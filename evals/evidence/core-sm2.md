# Fresh Smoke Test 2 证据记录（SM-02《全职高手》）

> Stage 7 B12/T717 Smoke 2。SPECIFIC_RISK / none / normal，preferences=null。此前从未测试过的新书（过拟合检验，SPECIFIC_RISK+none 组合轻量验证）。
> 环境：Host = opencode CLI（macOS）· Model = deepseek-v4-flash-free · Web Search = websearch（真实联网）· Browser/Page = webfetch · Date = 2026-08-12

## 请求与环境

- Request：无剧透，《全职高手》主角有感情线吗？
- Parsed：base_mode=SPECIFIC_RISK / target=romance-structure(+harem 派生) / spoiler_level=none / detail_level=normal
- 效率：queries_used=2 组（身份 / 感情线）/ pages_opened=0 / key_sources_used=10。**Post-optimization revalidation 修正**：全部关键关系证据均为 snippet，因此只能形成 WEAK 线索，不能以“多 snippet 交叉”为由升级到 LIKELY/CONFIRMED；本历史 case 的正确行为是带证据边界作答，而不是强结论。
- **轻量验证**：2 组查询即 TASK STOP（目标字段 dimension stop + 身份 HIGH + diminishing returns 第 2 组见效），远低于 FULL_SCAN 预算，未扩张任何无关维度

## Identity Resolution

- 候选：唯一（书名独特，同名动漫/电视剧/游戏/电影/舞台剧对象全部 LOT 过滤）
- 身份置信度：**HIGH**——维基百科（蝴蝶蓝/王冬/2011-02-28~2014-04-30 起点连载/1728 章/9.4 分）+ 百度百科（"千盟书"/国家图书馆典藏）+ 优书网（已完结 5349700 字/2014-04-30）+ 作者完本感言（新笔趣阁转载：2014-04-28 完本）多源一致

## Evidence Ledger（精选重要证据）

| ID | dimension | claim_type | 来源 | tier | 日期 | access | G | supports | 摘要 |
|---|---|---|---|---|---|---|---|---|---|
| S2-E01 | identity / serialization | FACT | 维基百科·全职高手 | B | 现版 | snippet | G1 | SUPPORT | 蝴蝶蓝著，起点中文网 2011-02-28 连载 ~ 2014-04-30 完结，1728 章，电子竞技类型，9.4/10 好评指数 |
| S2-E02 | identity | FACT | 百度百科·全职高手 | B | 现版 | snippet | G1 | SUPPORT | 2014-09 首部"千盟书"（1690 盟主）；2013 年度票数总冠军/金键盘奖；2020 国家图书馆永久典藏；电视剧/动画/电影/舞台剧改编列表 |
| S2-E03 | identity / serialization | FACT | 优书网数据页 | C | 2014-04-30 | snippet | G1 | SUPPORT | 起点/游戏分类/已完结/最后更新 2014-04-30/5349700 字 |
| S2-E04 | identity / serialization | FACT | 完本感言（新笔趣阁转载第1728章） | C | 2014-04-28 | snippet | G1 | SUPPORT | 作者亲笔："2011年2月28日，到2014年4月28日，三年零两个月，我写完了《全职高手》" |
| S2-E05 | romance-structure | FACT（社区共识） | 百度知道：全职高手里叶修喜欢谁 | C | 2018-04-16 | snippet | G2 | SUPPORT | "热血竞技类小说，文中并没有明确的感情线，任何 CP 都是 YY 的产物。叶修没有喜欢的人……对苏沐橙的感情更多倾向于陪伴多年的密友和妹妹""原著并没有感情线" |
| S2-E06 | romance-structure | INTERPRETIVE | 明星关系图：叶修苏沐橙到底什么关系 | C | — | snippet | G2 | SUPPORT | "全职没有情侣这种生物，男女之间都是纯洁的兄妹关系……蝴蝶蓝大大……不太会处理感情戏""恋人未满：超越友谊但未达到情侣" |
| S2-E07 | romance-structure | FACT | 快看漫画 qa：叶修和谁在一起了 | C/D | — | snippet | G2 | SUPPORT | "叶修没有和任何人在一起。《全职高手》本身没有感情线，作者没有明写主角叶修和任何人在一起。苏沐橙最后没有和任何人在一起（结局加入兴欣战队）" |
| S2-E08 | romance-structure | INTERPRETIVE | 剧情吧：叶修喜欢陈果还是苏沐橙 | C | — | snippet | G2 | SUPPORT | "原著里面对于叶修的感情戏并没有描述……他（对两人）都不喜欢，都带着各自的责任" |
| S2-E09 | romance-structure | INTERPRETIVE | 新浪：叶修与沐橙是情侣or兄妹 | C | 2019-12-09 | snippet | G2 | SUPPORT | "对于原著小说，很多的网友都说全职无cp。因为原著小说中并没有感情线存在"（暧昧"老夫老妻"表现系动漫表现+网友解读，非原著事实） |
| S2-E10 | romance-structure | COMMUNITY_EVALUATION | 趣历史网：叶修有没有喜欢的人 | C | 2021-04-24 | snippet | G2 | SUPPORT | "小说中叶修并没有感情线，作者也没有明确说明叶修喜欢谁……喜欢叶修的人有很多（苏沐橙/唐柔/陈果）……叶修只对苏沐橙一个人好"（指社交亲密细节：同吃一碗泡面/靠肩睡/玩笑，无恋爱确认） |
| S2-E11 | romance-structure（改编对照） | FACT | 红袖读书 ask | D | 2025-02-23 | snippet | G2 | CONTEXT | 站点内 SEO 问答（按先例 D 类仅线索）：电视剧"没有爱情线的基调一脉相承"；剧版给陈果"修成正果"系改编内容（对象=电视剧，LOT 对照用） |

## Dimension Results

| dimension | value | confidence | agreement | 判定链 |
|---|---|---|---|---|
| identity | 全职高手/蝴蝶蓝（王冬）/起点中文网/游戏竞技 | HIGH | — | E01~E04 多源一致（维基+百科+优书+作者完本感言） |
| serialization-status | completed（搜索摘要口径：2011-02-28~2014-04-28/30，1728 章，约 535 万字） | **WEAK** | CONSISTENT | E01~E04 均为 snippet；来源之间一致，但 access_mode 上限仍为 WEAK。若需要正式确认完结事实，应打开高价值页面后再升级。 |
| romance-structure | **no-romance 倾向（证据较弱）**：多个搜索摘要一致描述原著无明确感情线/无 CP，但未打开原页面核实 | **WEAK** | CONSISTENT | E05~E10 均为 snippet。多独立摘要只能说明线索一致，不能越过 access_mode 上限；按 TX §3.2 可给结构倾向，但必须显式保留“未页面核实”的证据边界。 |
| harem（派生） | **未发现明确后宫证据，倾向 H3 非后宫（证据较弱）** | **WEAK** | CONSISTENT | 由当前 WEAK 的 no-romance 线索派生；不能把派生结论升级到高于基础 claim 的 confidence。 |

## 冲突与处理

1. **"无感情线" vs 网友 CP/暧昧解读（本 case 唯一口径面）**：快看"叶修没有和任何人在一起"+ 新浪"全职无cp（原著）" vs 动漫向解读"老夫老妻"（新浪 E09，明确"抛开原著设定"）+ 红袖 D 类（剧版陈果线）。按 playbook §11.2 顺序：对象（原著小说 vs 动漫/剧版改编）→ 版本（原作 vs 改编刻度）→ 判定动漫/剧版解读 LOT 或仅作改编对照，原著口径无实质冲突 → no-romance + CONSISTENT，无投票问题。
2. **"很多女性角色喜欢叶修"不构成后宫**：E10 承认好感者众（苏沐橙/唐柔/陈果），但按 taxonomy H3（多女喜欢但主角无承诺）→ 非后宫；"好感"≠"感情线"（TX §3.1 存在异性角色≠有感情线）。
3. **页面打开需求评估（修正）**：原记录“6+ 独立 snippet 足以达成 LIKELY、无需 page”违反现行 source-policy §3.2 / playbook §8.3。正确规则是：若用户接受 WEAK 边界，可在 SPECIFIC_RISK 中轻量停止并明确“仅有摘要线索”；若要输出 LIKELY/CONFIRMED，则必须按 Fetch Gate 打开高价值页面核实。

## No-spoiler 专项观察（none）

- 研究阶段材料含人物关系细节（苏沐橙加入兴欣、苏沐秋去世背景等）——输出全部隔离，仅结构级类型判定（"无感情线"本身是结构结论，不涉事件细节）。
- 来源标题均无结局事件（"叶修喜欢谁""有没有感情线"类），无需脱敏处理；D 类红袖 ask 标题"全职高手有没有感情线"中性。

## Verdict

- 身份正确：PASS（HIGH，唯一候选）
- 用户显式问题（"主角有感情线吗"）：第一句直答"《全职高手》主角没有明确感情线"→ 结构级结论 + 依据 → ✓ 无剧透零事件泄漏 ✓
- 核心验证点（Smoke 2 目的）：
  1. **SPECIFIC_RISK 轻量**：identity + 1 组目标查询 = 2 组即 TASK STOP；未查世界观/结局/战力/水文（范围外）✓
  2. **none 剧透隔离**：输出仅"无感情线/非后宫"类型判定 + 密友级羁绊抽象，无任何关系事件细节 ✓
  3. **H3 边界守规**：多女好感 ≠ 后宫；完全无实质恋爱回应时可映射 `no-romance + H3`，不强制 `single` ✓
  4. **Evidence Integrity 修正**：0 page 情况下所有目标结论保持 WEAK，不再以 snippet 数量升级 ✓
- **PASS（规则合规层）**：本 case 仍能作为 SPECIFIC_RISK 轻量/无剧透/H3 边界测试，但**不再作为 LIKELY/CONFIRMED 事实基线**；若发布前需要强事实基线，必须重新执行页面级 Web 验证。

## Unknown 与限制

- 目标字段零 UNKNOWN（SPECIFIC_RISK 目标充分答复）；范围外维度（结局评价、慢热、系统等）按模式未调查（非"省略未查"，模式本身不覆盖）
- 无 page 级打开（命中规则允许：目标字段已充分）——记录以保效率指标透明