# The Report

One file per simulation. **It is the only thing this skill writes.**

## Where

```text
<vault>/_QA/Simulations/YYYY-MM-DD - <side A> vs <side B>.md
```

Create `_QA/Simulations/` if it does not exist. Keep the filename short
enough to read in a file list — name the party by its members when there
are four or fewer, otherwise by its size and level:

```text
2026-09-16 - Azren, Cevis, Darla, M'Ari vs 4 Poisonbearer Ghouls.md
2026-09-16 - 6 PCs L8 vs Belishan and 4 Vampire Spawn.md
```

If a file with that name exists, append ` (2)`. **Never overwrite a
previous simulation** — the comparison between two runs is often the
point.

## Why `_QA/` and not `_inbox/`

`_inbox/` is staging for material a human will process into canon, and
both `session-wrapup` and `campaign-qa` treat it as work awaiting a
decision. A simulation is **never** going to become canon, so putting it
there creates a permanent false to-do.

`_QA/` is analysis about the campaign rather than content of it. Note
that `vault_check` **does** scan `_QA/` — it skips only `_Templates/`
and `_inbox/` — so the frontmatter below has to satisfy the schema.

## Frontmatter

```yaml
---
name: "<the filename, without .md>"
type: document
canon_status: DRAFT
doc_type: simulation
source: "Simulation run by simulate-encounter; not module content"
createdSession: ""
asOfSession: ""
lastUpdated: "YYYY-MM-DD"
aliases: []
tags:
  - "simulation"
  - "non-canon"
campaign: "[[Campaign Overview]]"
affects_canon: false
combatants_a: ["[[Azren]]", "[[Cevis]]"]
combatants_b: ["[[Poisonbearer Ghoul]]"]
round_limit: 10
trials: 1
verdict: "Side A, round 7"
relationships: []
---
```

**`canon_status: DRAFT` is a schema requirement, not a claim.** The
validator accepts only `DRAFT`, `AUTHORITATIVE`, `SUPERSEDED` and
`STUB`, and none of them means "sandbox". **`affects_canon: false` and
the `non-canon` tag are what actually carry the meaning**, and the
banner below states it in the body where a reader will see it.

This produces one `WARNING` from `vault_check stale-drafts` for a
missing `createdSession`. That is expected: every one of the vault's
8,747 existing drafts produces the same warning, and the check is not
one of the repo's gates. **`vault_check frontmatter` and both
`graph_check` passes come back clean**, which are.

**Link combatants with real wiki-links** so the graph connects the
simulation to the entities it used. Do **not** add `relationships:`
entries — those are canon edges and a simulation has none.

## Body

````markdown
# <title>

> [!warning] Not canon. Nothing here happened.
> A sandbox test written by `simulate-encounter`. **No PC or creature is
> affected by it** — no hit points, slots, conditions, status or XP
> changed anywhere, and a character who died here is alive and well. See
> [[Campaign Rules]] for what is canon.

## Terms

| | |
|---|---|
| **Round limit** | 10 |
| **Starting distance** | 60 ft., both sides aware |
| **Terrain** | Open, flat, lit |
| **Surprise** | None |
| **Starting state** | Full hit points and resources |
| **Trials** | 1 |

## The Rosters

### Side A — <name>
| Combatant | Level/CR | AC | HP | Init | Key resources |
|---|---|---|---|---|---|
| [[Azren]] | Cleric 2 | 18 | 18 | +2 | 3x 1st slot, Channel Divinity, Warding Flare |

### Side B — <name>
| Combatant | CR | AC | HP | Init | Key traits |
|---|---|---|---|---|---|
| Ghoul A | 4 | 15 | 78 | +4 | Death Spray, poison immunity |

## Opening Tactics

What each side does and why, in two or three sentences each, naming
the `## Tactics` section where one governed.

## The Fight

### Round 1

**Initiative order.** Ghouls (18), Cevis (15), Azren (12), ...

- **Ghoul A** → Cevis. `d20=11 +6 = 17 vs AC 16` → **HIT**, 2d6+3 = 11.
  Cevis 34 → 23.
- **Azren** casts *guiding bolt* at Ghoul A. `d20=18 +5 = 23 vs AC 15`
  → **HIT**, 4d6 radiant = 15. Ghoul A 78 → 63. *Next attack against it
  has advantage.* **1st-level slots: 3 → 2.**

*(Every roll shown as made. Running totals after every hit.)*

### Round 2
...

## Verdict

**Side A, round 7, by kill.**

| | Side A | Side B |
|---|---|---|
| Survivors | 3 of 4 | 0 of 4 |
| Dropped | M'Ari (round 5, stabilised round 6) | all |
| HP remaining | 41 of 96 | — |
| Resources left | 1x 1st slot, no Channel Divinity | — |

**The turning point.** Round 4: Ghoul B failed its save against ...

**What would change it.** ...

## Caveats

- Judgement calls that could plausibly have gone the other way.
- Where the vault was silent on tactics and this run improvised.
- Whether one roll decided it — and therefore how much weight the
  verdict will bear.
````

## Multiple Trials

Narrate **trial 1 in full**. Report the rest as one line each, then a
summary:

```markdown
## Trials

| # | Winner | Rounds | Side A survivors | Note |
|---|---|---|---|---|
| 1 | Side A | 7 | 3 of 4 | narrated above |
| 2 | Side A | 6 | 4 of 4 | Ghoul A dropped round 2 |
| 3 | **Side B** | 8 | 0 of 4 | double crit on M'Ari, round 3 |

**Side A won 4 of 5 runs.** Median 7 rounds.

**Five runs is not a statistic.** These are rolled in-model, one at a
time; treat the spread as a sketch of the range, not a probability.
```

**Never report a percentage from single-digit trials.** "4 of 5" is
honest; "80%" implies a precision that is not there.

## After Writing

Tell the user **the path and the verdict** in your reply, plus the one
sentence that matters most — usually the turning point or the closest
call. Do not make them open the file to find out who won.

If the simulation surfaced something worth recording in the campaign —
an encounter that is unsurvivable as written, a conversion that looks
wrong — **say so and let them decide**. Do not write it to `_flags.md`,
`Encounters/`, or anywhere else yourself.
