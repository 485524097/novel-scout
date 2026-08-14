[中文](README.md) · English

# Novel Scout — a spoiler-aware novel risk checker AI Skill

> Vet the landmines before you sink 50 hours into a novel.

Novel Scout is a **low-spoiler AI Skill for Chinese web novel risk checking**. Give it a novel, and it first searches and verifies real public information, then checks common reader deal-breakers — harem, NTR, saintly protagonist, protagonist torture, slow burn, filler, ending controversy — and advises whether this novel fits your reading preferences.

It never concludes from "model memory" alone — **evidence first, conclusion second**.

## Try it in 30 seconds

Send any of these to an Agent that supports Skills:

```text
排雷《玄鉴仙族》  (vet this novel)
Does 《XXX》 have a harem?
Does 《XXX》 have NTR?
Is 《XXX》 heavy on protagonist abuse?
Is 《XXX》 right for me?
```

## Sample output (fictional example, format only)

```text
《雾城拾荒记》(fictional example, not a real verdict)

Harem: low risk
NTR: no clear evidence found
Protagonist abuse: moderate
Protagonist style: fairly decisive
Status: serializing

Conclusion: If you mind harem and NTR, no obvious high-risk items found in public information.

Spoiler level: light
```

## Features

- 🔎 **Web-verified**: searches and opens real pages — an evidence-based novel review, not model memory
- 🚧 **Low spoiler / spoiler-free by default**: answers *whether* a deal-breaker exists and how severe it is, not *which chapter* it happens in
- ⚠️ **Covers common web-novel deal-breakers**: harem, NTR, system mechanics, saintliness, protagonist torture, IQ inconsistency, slow burn, filler, bad ending
- 🎯 **Specific risk queries**: ask about one deal-breaker and get a focused answer
- 👤 **Reading-preference aware**: configurable hard-no list to judge fit
- 📚 **Identity-first**: disambiguates same-title novels so it never vets the wrong book

## Quick Start

**Full path (from first GitHub visit to first use):**

```bash
# 1. Get the repo
git clone https://github.com/485524097/novel-scout.git

# 2. Install into Claude Code Skills
mkdir -p ~/.claude/skills
cp -r novel-scout ~/.claude/skills/novel-scout

# 3. Launch Claude Code and type:
排雷《小说名》
```

Only `SKILL.md` and `references/` are required at runtime; `config/preferences.yaml` is optional. The steps above are the Claude Code install path that has actually been validated; the repo is a standard Agent Skill directory and other Skill-compatible hosts may try the same copy method, but they have not been individually validated.

## Common requests

The request text is in Chinese, matching the skill's trigger words:

| Request | Effect |
|---|---|
| `排雷《XXX》` | Full vet by default (light spoilers, normal detail) |
| `无剧透排雷《XXX》` | Full vet with zero spoilers |
| `《XXX》有后宫吗？` | Answers only this one question, lightweight & fast |
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

## What it is NOT

Novel Scout is **not**:

- a novel downloader;
- a novel reader;
- an auto-update tracker;
- just a novel summarizer;
- a general book recommendation system.

Its single job: **help you decide, before or while reading, whether a novel contains the deal-breakers you care about.**

## Personal preferences (optional)

You don't need preferences to use it — without them it outputs an objective reading profile. For personalized advice, copy and edit the template:

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
- **Current request wins**: saying "slow burn is fine this time" overrides the config for this request; the config file is never auto-modified

## Spoiler control

- `none`: no spoilers (withholds key deaths, final partner, final boss, identity twists, and ending events)
- `light`: light spoilers (default; allows structure-level direction)
- `full`: full spoilers (only when you explicitly ask)

Reports open with the current spoiler level and the information cutoff date.

## Evidence & sources

- All conclusions are grounded in real retrieved evidence; important strong claims are preferably verified against opened pages
- Official, reliable secondary, community, and weak sources are distinguished; search snippets are never presented as pages that were actually opened
- When a source title itself could spoil, the report redacts it
- Serialized works are marked "as of YYYY-MM-DD"; the current state is never written as permanent fact

## Limitations (please read first)

Novel Scout's judgment **depends on public web information**:

1. **Niche novels may only get UNKNOWN** — when data is insufficient, it honestly says "can't confirm" rather than guessing
2. **A serialized novel's romance line / deal-breakers may change as the plot develops** — conclusions carry a time bound and may go stale
3. **Community discussion can be misreported** — "no evidence found" is not strictly "definitely absent"
4. **High-risk conclusions come with sources and confidence** — but "good or not" and "bad ending or not" are community reception tendencies, not objective truth
5. **The Skill does not download or parse full novel text** — the investigation is based on public material
6. **V1 does not recommend novels or compare multiple novels** — vetting only, no reading lists; "which fits me better" requires vetting each individually

> Don't treat it as a 100%-accurate vetting machine. It helps you filter out likely deal-breakers and honestly tells you what it doesn't know.

## FAQ

### Will Novel Scout spoil the story?

By default, no. It answers *whether* a deal-breaker exists and roughly how severe it is, not what happens in which chapter. Full spoilers are only given when you explicitly ask.

### How reliable is its information?

It prioritizes real public web evidence and never treats model memory as fact. When sources conflict, it presents both sides instead of voting for you; when evidence is insufficient, it clearly says "cannot confirm".

### Can I query just one deal-breaker?

Yes. Ask "Does 《XXX》 have a harem?" or "Does 《XXX》 have NTR?" and it investigates only that risk and answers directly.

### Can I save my reading preferences?

Yes. Write `hard_no` / `dislike` / `like` into `config/preferences.yaml` and the Skill reads it whenever needed, persisting your reading preferences across sessions. Note:

- Temporary preferences stated in the current chat take priority over the config file (e.g. saying "slow burn is fine this time");
- The Skill never auto-modifies `preferences.yaml` after a single conversation;
- It also works without a config (generic objective vetting).

## How it works (short version)

1. Confirm *which* novel you mean (identity first; same-title works prompt disambiguation)
2. Search official and reader sources, open real pages to verify
3. Distinguish fact, reader opinion, and model judgment, recording sources item by item
4. Cross-validate conflicting information, classify by a strict standard, and mark confidence
5. If preferences are configured, judge whether it trips your deal-breakers (preferences never alter the factual finding)
6. Generate a vet report at the requested spoiler level

Core principle: **evidence before conclusion** — never conclude from model memory, one reader comment ≠ community consensus, and **UNKNOWN is a valid result**.

## novel-scout-roast (optional variant)

`novel-scout-roast` uses the **exact same** evidence standards and research workflow as the main Skill; only the report layer changes to a **roast-style voice** (rigorous evidence + snarky commentary).

- **Dependency**: it needs the main `novel-scout` `references/` (taxonomy / source-policy / search-playbook / preference-guide) plus its own `references/report-format-roast.md`
- **Install**: copy the whole repo into your Skills directory (roast automatically reuses the sibling `references/`); or install `novel-scout` and `novel-scout-roast` as sibling directories under `~/.claude/skills/`
- **Use**: `锐评《XXX》` / `《XXX》毒舌点评` (trigger words in its SKILL.md)

## Docs for developers

Regular users don't need these; advanced/developer readers should see:

- `docs/`: design (DESIGN), development rules (DEVELOPMENT), output examples (OUTPUT-EXAMPLES)
- `references/`: taxonomy, source policy, search playbook, preference guide, report format
- `evals/`: trigger tests, behavior tests, real-world evaluations
- See [CHANGELOG](CHANGELOG.md) for history and [CONTRIBUTING](CONTRIBUTING.md) for contribution guidelines

## License

[MIT](LICENSE)
