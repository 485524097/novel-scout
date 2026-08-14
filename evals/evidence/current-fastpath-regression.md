# Current SPECIFIC_RISK Fast Path — Fresh Web Regression

Date: 2026-08-14

Purpose: validate the current `search-playbook.md §0` Fast Path after Runtime Simplification. This is a narrow fresh regression, not a rerun of the full Stage 7 corpus.

## FCR-01 — 《全职高手》后宫吗？

- Identity: 《全职高手》 / 蝴蝶蓝
- Mode: SPECIFIC_RISK
- Target: harem / romance-structure
- Opened pages:
  - 中国作家网《荣耀征程，初心不改——评网络小说〈全职高手〉》 — https://www.chinawriter.com.cn/n1/2019/1230/c404027-31527871.html
  - 澎湃新闻《剧版〈全职高手〉：当电竞没有爱情，能成爆款吗》 — https://www.thepaper.cn/newsDetail_forward_4001854
- Key evidence:
  - 中国作家网页面直接说明原著是一部“没有爱情线”的小说。
  - 澎湃页面直接说明叶修虽与多名女性角色互动，但没有明确感情线、没有谈恋爱，也没有开后宫。
- Result:
  - `harem = H3`（非后宫）
  - `romance-structure = no-romance`
  - `confidence = LIKELY`
  - `agreement = CONSISTENT`
- Fast Path behavior: 目标结论已由 2 个独立 page 支撑，无需扩展到 FULL_SCAN。
- Status: **PASS**

## FCR-02 — 《斗破苍穹》后宫吗？

- Identity: 《斗破苍穹》 / 天蚕土豆
- Mode: SPECIFIC_RISK
- Target: harem / romance-structure
- Opened pages:
  - 百度百科·萧炎人物页 — https://wapbaike.baidu.com/item/%E8%90%A7%E7%82%8E/5808896
  - 澎湃新闻《剧版〈全职高手〉：当电竞没有爱情，能成爆款吗》 — https://www.thepaper.cn/newsDetail_forward_4001854
- Key evidence:
  - 百度百科人物页直接写明萧炎与薰儿、美杜莎举行婚礼，并称二人为其妻子关系。
  - 澎湃文章在比较男频作品时直接说明《斗破苍穹》男主有两个老婆。
- Result:
  - `harem = H1`
  - `romance-structure = harem`
  - `confidence = CONFIRMED`
  - `agreement = CONSISTENT`
- Fast Path behavior: 2 个独立可靠 page 对明确关系事实直接一致，允许 CONFIRMED；无需继续堆来源。
- Status: **PASS**

## Result

- Fresh Fast Path cases: **2/2 PASS**
- Both cases used actual opened pages; no snippet-only confidence upgrade occurred.
- No unrelated FULL_SCAN expansion occurred.
- Current Fast Path fresh E2E status: **PASS for the two high-frequency harem regression paths above**.

This result does not claim that all Stage 7 objects were freshly rerun.
