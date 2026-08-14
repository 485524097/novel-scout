[中文](README.md) · English

# Novel Scout

> Vet the landmines before you sink 50 hours into a novel.

Novel Scout is an Agent Skill for pre-reading "novel vetting". Give it a novel, and it first searches and verifies real information, then checks common reader deal-breakers — harem, NTR, system, saintly protagonist, protagonist torture, slow burn, filler, ending controversy — and advises whether it's worth starting based on your reading preferences.

It never concludes from "model memory" alone — **evidence first, conclusion second**.

## What it does

- Confirms *which* novel you mean (author, platform, serialization status) so it doesn't vet the wrong book
- Investigates reading deal-breakers for one specific novel
- Distinguishes: **confirmed fact / plausible inference / weak evidence / unconfirmable**
- Cross-validates conflicting information; when sources disagree, it presents both sides rather than "voting" for you
- Supports three spoiler modes: none / light / full
- If personal preferences are configured, judges whether it trips your deal-breakers and gives a recommendation

## Quick Start

### Installation

Copy the `novel-scout` directory into your Agent's supported Skills directory. At runtime you only need:

- `SKILL.md` (required)
- `references/` (required)
- `config/preferences.yaml` (optional, personal preferences)

For example, in Claude Code, copy it to `~/.claude/skills/novel-scout/`, then tell your Agent "排雷《XXX》" (vet "XXX" for deal-breakers).

### Common requests

The request text is in Chinese, matching the skill's trigger words:

| Request | Effect |
|---|---|
| `排雷《XXX》` | Full vet by default (light spoilers, normal detail) |
| `无剧透排雷《XXX》` | Full vet with zero spoilers |
| `《XXX》后宫吗？` | Answers only this one question, lightweight & fast |
| `《XXX》有 NTR 吗？` | Answers only this one question, lightweight & fast |
| `详细排雷《XXX》` | A more detailed report |
| `《XXX》适不适合我？` | Judged against your preferences (generic profile when none configured) |

## What it checks

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

## How it works

1. Confirm which novel you mean (identity first; same-title works prompt disambiguation)
2. Search official and reader sources, open real pages to verify
3. Distinguish fact, reader opinion, and model judgment, recording sources item by item
4. Cross-validate conflicting information
5. Classify by a strict standard, marking confidence and consensus state
6. If preferences are configured, judge whether it trips your deal-breakers (preferences never alter the factual finding)
7. Generate a vet report at the requested spoiler level

### Evidence before conclusion

Novel Scout's core principle is **evidence before conclusion**:

- Never conclude from model memory; every key conclusion must be backed by a real source
- A search snippet is only a lead, never masquerading as page evidence
- One reader comment ≠ community consensus
- **UNKNOWN is a valid result**: when reliable information is insufficient, Novel Scout tells you "can't confirm" rather than guessing to fill the report

## Personal Preferences

Configure your reading preferences so reports give you personalized advice.

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
- **`preferences.example.yaml` is only a template** — only `config/preferences.yaml` is treated as your real preferences
- You don't need preferences to use it — the output is then an objective reading profile rather than personalized advice
- **Current request wins**: even if you configured `dislike: [slow-burn]`, saying "slow burn is fine this time" overrides it for this request, and the config file is never auto-modified

## Spoiler Control

- `none`: no spoilers (withholds key deaths, final partner, final boss, identity twists, and ending events)
- `light`: light spoilers (default; allows structure-level direction)
- `full`: full spoilers (only when you explicitly ask)

Reports open with the current spoiler level and the information cutoff date.

## Evidence & Sources

- All conclusions are based on real search and page visits; source tiers (official / wiki / community / AI aggregation) are clearly marked
- When a source title itself could spoil, the report redacts it
- Serialized works are marked "as of YYYY-MM-DD"; the current state is never written as permanent fact

## Limitations

1. **Community opinions are subjective** — "good or not", "bad ending or not" are community reception tendencies, not objective truth
2. **Niche novels may only get UNKNOWN** — when data is insufficient, it honestly says "can't confirm" rather than guessing
3. **A serialized novel's romance line / deal-breakers may change as the plot develops** — conclusions carry a time bound and may go stale
4. **The Skill does not download or parse full novel text** — the investigation is based on public material
5. **V1 does not recommend novels** — vetting only, no reading lists
6. **V1 does not compare multiple novels** — "which fits me better" requires vetting each individually

## License

[MIT](LICENSE)
