[中文](README.md) · English

# Novel Scout

> Vet the landmines before you sink 50 hours into a novel.

Novel Scout is an Agent Skill for pre-reading "novel vetting". Give it a novel, and it first searches and verifies real information, then checks for common reader deal-breakers — harem, NTR, system, saintly protagonist, protagonist torture, slow burn, filler, ending controversy — and advises whether it's worth starting based on your reading preferences.

It never concludes from "model memory" alone — **evidence first, conclusion second**.

## What it does

- Confirms *which* novel you mean (author, platform, serialization status) so it doesn't vet the wrong book
- Investigates reading deal-breakers for one specific novel
- Distinguishes: **confirmed fact / plausible inference / weak evidence / unconfirmable**
- Cross-validates conflicting information; when sources disagree, it presents both sides rather than "voting" for you
- Supports three spoiler modes: none / light / full
- If personal preferences are configured, judges whether it trips your deal-breakers and gives a recommendation

## Quick Start

Copy/install the `novel-scout` directory into your Agent's supported Skills directory, and make sure the host can read `SKILL.md` and `references/`. Then tell your Agent:

```
排雷《XXX》
```

(vet "XXX" for deal-breakers)

Some ready-to-use requests (the request text itself is in Chinese, matching the skill's trigger words):

| Request | Effect |
|---|---|
| `排雷《XXX》` | Full vet by default (light spoilers, normal detail) |
| `无剧透排雷《XXX》` | Full vet with zero spoilers |
| `《XXX》后宫吗？` | Answers only this one question, lightweight & fast |
| `《XXX》有 NTR 吗？` | Answers only this one question, lightweight & fast |
| `详细排雷《XXX》` | A more detailed report |
| `《XXX》适不适合我？` | Judged against your preferences (generic profile when none configured) |

## What it checks

Novel Scout mainly checks these dimensions:

- Romance line & harem (single heroine / multi-girl ambiguity / explicit harem / no romance)
- NTR / romantic betrayal risk
- System presence
- Protagonist saintliness
- Protagonist intelligence & behavioral logic
- Degree of protagonist torture
- Slow burn / filler / repetitive tropes
- Plot logic
- Worldbuilding scale
- Power-system stability
- Serialization & completion status
- Ending reception (polarized? widely seen as a bad ending?)

Full enumeration and judgment rules are in `references/taxonomy.md`.

## How it works

1. Confirm which novel you mean (identity first; same-title works prompt disambiguation)
2. Search official and reader sources, open real pages to verify
3. Distinguish fact, reader opinion, and model judgment (an evidence ledger records sources item by item)
4. Cross-validate conflicting information; majority voting is forbidden
5. Classify by a strict taxonomy, marking confidence and consensus state
6. If preferences are configured, judge whether it trips your deal-breakers (preferences never alter the factual finding)
7. Generate a vet report at the requested spoiler level

### Evidence before conclusion

Novel Scout's core principle is **evidence before conclusion**:

- Never conclude from model memory; every key conclusion must be backed by a real source
- A search snippet is only a lead, never masquerading as page evidence
- One reader comment ≠ community consensus
- **UNKNOWN is a valid result**: when reliable information is insufficient, Novel Scout tells you "can't confirm" rather than guessing to fill the report

## Personal Preferences

You can configure your own reading preferences so reports give you personalized advice.

Copy the template and edit it:

```
config/preferences.example.yaml  →  config/preferences.yaml
```

Example (format only, not recommended values):

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

Notes:

- `hard_no` is a hard deal-breaker: once confirmed, the final recommendation is directly "not recommended", and other positives can't offset it
- **`preferences.example.yaml` is only a template — Novel Scout never treats it as your real preferences**; only `config/preferences.yaml` is read
- You don't need preferences to use it — the output is then an objective reading profile rather than personalized advice
- **Current request wins**: even if you configured `dislike: [slow-burn]`, saying "slow burn is fine this time" overrides it for this request, and the config file is never auto-modified

## Spoiler Control

- `none`: no spoilers (withholds key deaths, final partner, final boss, identity twists, and ending events, but keeps useful structure-level conclusions)
- `light`: light spoilers (default; allows structure-level direction)
- `full`: full spoilers (only when you explicitly ask)

Reports open with the current spoiler level and the information cutoff date.

## Evidence & Sources

- All conclusions are based on real search and page visits; source tiers (official / wiki / community / AI aggregation) are clearly marked
- When a source title itself could spoil, the report redacts it
- Serialized works are marked "as of YYYY-MM-DD"; the current state is never written as permanent fact

## Limitations

Honestly stated limitations:

1. **Community opinions are subjective** — "good or not", "bad ending or not" are "community reception tendency" or "polarized", not objective truth
2. **Niche novels may only get UNKNOWN** — when data is insufficient, it honestly says "can't confirm" rather than guessing
3. **A serialized novel's romance line / deal-breakers may change as the plot develops** — conclusions carry a time bound and may go stale
4. **Search quality depends on accessible web sources** — availability of Chinese-community sources is uneven
5. **Some community pages may be inaccessible** — some sites have anti-scraping limits; it then degrades gracefully and marks it honestly, never faking page access with snippets
6. **The Skill does not download or parse full novel text** — the investigation is based on public material and doesn't guarantee coverage of content never discussed publicly
7. **V1 does not recommend novels** — vetting only, no reading lists
8. **V1 does not compare multiple novels** — "which fits me better" requires vetting each individually
9. **Automatic triggering (Runtime Trigger) is not yet verified on an observable host** — Skill behavior under explicit requests and the real web flow are verified; automatic routing still needs testing on your host (see Development Status)

## Project Structure

```
novel-scout/
├── SKILL.md                      # Skill body (orchestration layer)
├── README.md                     # This file (中文)
├── README.en.md                  # English version
├── CHANGELOG.md
├── LICENSE
├── .gitignore
├── config/
│   └── preferences.example.yaml  # Preference template (≠ real preferences)
├── references/                   # Runtime rules (SKILL.md reads on demand)
│   ├── taxonomy.md
│   ├── source-policy.md
│   ├── search-playbook.md
│   ├── preference-guide.md
│   └── report-format.md
├── evals/                        # Evaluation artifacts (not needed at runtime)
├── docs/                         # Design & dev docs (not needed at runtime)
└── TASKS.md / STATUS.md / PROPOSALS.md
```

**At runtime** you only need: `SKILL.md` + `references/` + (user-created) `config/preferences.yaml`. `docs/`, `evals/`, `TASKS.md`, `STATUS.md`, `PROPOSALS.md`, `CHANGELOG.md` are development and verification material, not needed for normal operation.

## Evaluation

Novel Scout ran static and real-world evaluations during development. The following tests now mainly serve as **regression insurance** — they aren't read at normal runtime and shouldn't drive the runtime to keep growing rules:

- 55 trigger-routing cases (static)
- 59 behavior-rule cases (static; 21 critical)
- 7 real-novel end-to-end cases (real web)
- 25 source-integrity spot checks on important evidence (fake source = 0)
- 3 anti-hallucination challenges (fictional title / near-identical title / same-title disambiguation)
- 2 fresh-novel smoke tests

Evaluation details are in `evals/`. **Note: the above are results from the development evaluation set, not a real-world guarantee.**

## Development Status

- **Product Version**: 1.0.0 (Release Candidate / Unreleased)
- **Static trigger routing**: passed
- **Static behavior evaluation**: passed (59/59; 21 critical)
- **Real-world web research evaluation**: passed (real-web E2E + follow-up representative regression done)
- **Automatic runtime trigger selection**: pending validation in a host where routing is observable (the current dev host can't observe automatic Skill routing; this doesn't mean the Skill is unrunnable — the full flow under explicit requests is verified)

Currently in **V1 RC / User Experience Trial**: the core Runtime is frozen; no more feature or rule growth from imagination. The priority now is to actually use it to vet novels and record real experience on speed, answer length, UNKNOWN ratio, search quality, preference matching, and spoiler experience. Runtime Trigger auto-routing remains a host-level PENDING item; it doesn't block explicit invocation or real experience, but "auto-trigger verified" can't be claimed until it's tested. Formal GitHub Release still needs human approval.

High-frequency single-deal-breaker requests (e.g. `《X》后宫吗?`) now use the **SPECIFIC_RISK Fast Path**: load only the short execution card, the target taxonomy subsection, and single-item report rules first; read more policy only on source conflicts, freshness, or access anomalies. The goal is to reduce fixed context without lowering evidence standards.

## License

[MIT](LICENSE)
