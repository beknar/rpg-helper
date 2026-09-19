# Recap Format

What the one file looks like. Read before drafting.

## Frontmatter

```yaml
---
type: document
doc_type: journal
canon_status: DRAFT
dry_run: true
recap_of: "[[Dry Run - {Name} - YYYY-MM-DD]]"
campaign: "[[Campaign Overview]]"
created_by: dry-run-recap
lastUpdated: "YYYY-MM-DD"
tags:
  - "dry-run"
  - "non-canon"
  - "player-recap"
---
```

**Check `_meta/entity-types.md` first.** If the vault declares a type
for a player-facing session summary, use it instead of `document` /
`journal`. `type` and `canon_status` are required everywhere; every
other field above is additive.

**`canon_status` is `DRAFT`, and you do not change it.** Promotion is
the GM's, and promoting a test run would make it canon. See the
SKILL.md §Publishing.

## Body

```markdown
# Dry Run Recap — {Name}

> [!info] Dry run — not campaign canon
> A test play of {encounter} on YYYY-MM-DD, written up for players.
> Nothing here happened in the campaign.

## The Party
Who was there — name, class and level, one line each, from the sheets.

## What Happened
The scene in order, in past tense, third person. Built from the
narration the table heard. Headings per beat if the run was long.

## How It Ended
The party's end state as they know it: hit points if they were
told, what fell, what they found, XP.

## How This Was Run
The showcase section. See below.

## Provenance
One or two lines: which run this recaps, whether it was built from
the live narration or rebuilt from notes.
```

**Tense and person change.** At the table the narration is second
person, present tense, to the players. The recap is **past tense,
third person**, about the characters: *"Kess heard nothing false in
it"*, not *"You hear nothing false in it"*.

**Link sparingly.** A wiki-link to a PC, an NPC the party met or a
place they stood is fine. A link to a creature file or an encounter
plan is not: on a published site it leads the reader to the prep.

## How This Was Run — the Showcase Section

This is what makes a recap a demonstration rather than just a story.
**Describe the mechanism, never the hidden content.**

| Say | Do not say |
|---|---|
| "Run in relay mode: one operator relayed the table's decisions; the players rolled every die." | Which rolls were asked for and what DCs they were against |
| "When the fight began, Claude handed the operator both creatures' statistics and the table ran the combat, relaying only the result." | The statistics, or the conditions under which the second creature would have fled |
| "A Perception check split the table: two characters heard through the mimicry and one did not." | The Deception total they were beating |
| "The session ran to about forty minutes." | Anything from the Play Notes' "For the GM" list |

**Name the feature being shown if the user named one.** If the run
was testing something specific — a new handoff format, a named
session, a cold open — say what it was and that it worked, in one
line. If it did not work, a showcase recap is the wrong document;
say so to the user rather than writing around it.

## Worked Example

Play Notes excerpt (GM document):

```markdown
- Lure: voice in the trees east. Deception 16 vs passives Kess 13,
  Alder 11 — both fooled. The mother (hidden, 20 ft behind) joins
  only if the lure is killed outright.
- Alder: active Perception 17, sees through it. Kess 14, does not.
- CONFLICT: file gives no flee threshold for the mother; ruled below
  20 HP.
- Combat handoff: lure dead round 1; mother charged, dead round 2.
  Kess took 3. XP 500, 100 each.
```

Recap, same events:

```markdown
## What Happened

On the second watch, Kess and Alder heard a child crying somewhere
out in the trees. It sounded real to both of them. Alder listened
harder and caught the flaw in it, a sob that repeated itself
exactly; Kess still heard a frightened child.

The party held the camp and opened fire into the treeline. The
crying stopped in the first volley. A moment later something far
larger broke from the trees at a run, and the party brought it down
before it could do more than wound Kess.

## How It Ended

Kess finished the night 3 hit points down; everyone else was
untouched. Each character earned 100 XP.
```

What was dropped, and why: the Deception total and passive scores
(never told to players), the mother's hiding place and her trigger
(the party only saw her charge), the flee threshold and the
`CONFLICT` (operator material), and her hit points.
