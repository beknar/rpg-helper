# Player Recap — A Dry Run Made Publishable

A dry run's Play Notes are written for the GM. They carry stat
blocks, DCs, the monster's retreat conditions, `CONFLICT` markers and
notes on where the plan fell short. **None of that may reach a
player, and no publishing filter can remove it**, because it is
threaded through the prose rather than fenced under a heading.

So a dry run that is meant to be seen gets a **second file, written
for players from the start**: the recap. It exists for two jobs:

- **Showing a feature off** on a published campaign site — this is
  what a relay-mode session looks like, this is a combat handoff, this
  is the table splitting on a question of fact.
- **Recording a feature test** in a form someone other than the GM can
  read.

It is still a dry run. **Nothing in it is canon**, and it says so.

## When to Write One

**Only on request, and only for a dry run.**

- The user asks: *"write a player recap"*, *"recap this for the
  site"*, *"make a publishable version"*, *"write it up for players"*.
- At the end of a dry run, **offer it once, in one line**, after the
  Play Notes are written: *"Want a player-facing recap of this for the
  site?"* Do not offer again if they decline.
- For an **earlier** dry run, the user names it and you work from its
  Play Notes. See §Sources.

**Never for canon play.** A played session reaches players through
`session-wrapup` and the campaign's own publishing, not through this.

## Ask One Thing First

**Who will read it?** If the site's audience includes people who may
later **play** this encounter, the recap is a spoiler for them — what
the voice in the dark really was, where the ambush comes from. Ask in
one line, once:

> *"This recap will give away how the encounter works. Is the site's
> audience anyone who might play it later?"*

If yes, say so plainly and let the user decide. Do not quietly soften
the recap into something vaguer; a vague showcase shows nothing.

## The One Rule

**If no player at the table heard it or saw it by the end of the
scene, it is not in the recap.**

That is the whole test. Everything below is that rule applied.

| In | Out |
|---|---|
| Narration the table heard, including read-aloud blocks you gave | Anything you told **only the operator** |
| What each PC did, as the player declared it | Stat blocks, AC, HP, attack bonuses — unless the players were told the number |
| Rolls the **table** made, and their outcome | DCs, unless you announced them to the players |
| What the PCs learned, and who learned it | Triggers, retreat conditions, tactics, "if they do X, Y happens" |
| Outcomes the party can see: who was hurt, what fell, what they found, XP | Creatures or branches that never appeared, and what would have happened |
| The end state as the party knows it | `NEW-*`, `UPDATE` and `CONFLICT` markers, and notes on gaps in the plan |
| | Your improvised calls flagged "my call, not the file's" |
| | Anything from `secrets`, `## GM Notes`, a spoiler fence, or `_source/` |

**What the party learned only partly stays partial.** If one PC saw
through the lure and another did not, the recap says exactly that and
no more. Do not complete their knowledge for them.

**A monster that revealed itself is fair game; its numbers are not.**
If the second creature charged out of the dark, the recap can describe
it charging. Its hit points were for the operator.

## Never Put Words in a PC's Mouth

The rule from the table holds on the page. **Quote a PC only where
the player gave you the words.** Stated intent stays intent:

- Player said: *"Kess tells the others it isn't a child."* → Kess
  tells the others it isn't a child.
- **Never:** *"'That's no child,' Kess growls."*

Same for feelings. The recap reports what the characters did, not
what they felt.

## Sources, in Order

1. **The narration you gave during this conversation.** If the run is
   still in context, this is the best material there is: it was
   written for the table, it is your own text, and it was already
   filtered for players when you said it.
2. **The run's Play Notes**, for the sequence of events and the
   outcomes. **Read them as a GM document**: every line is operator
   material until the rule above clears it.
3. **Nothing else.** Not the encounter file, not the creature file, not
   `_source/`. The recap tells what happened at the table, and the
   vault's prep is not that. **Never quote the module's own text**;
   it is licensed content even when the vault is private.

**Recapping an earlier run from its notes alone** is allowed, but the
narration is gone. Write it fresh from the notes, and say so in the
Provenance section: *"Rebuilt from the Play Notes; the table's
narration was not preserved."*

## Where It Goes

```text
Dry Runs/Dry Run Recap - {Name} - YYYY-MM-DD.md
```

- **`{Name}` and the date match the Play Notes it recaps**, so the two
  sort together and one leads to the other.
- **`Dry Runs/` at the vault root**, not `_inbox/`. Publishing setups
  routinely exclude `_inbox/` as staging, and a recap is meant to be
  published. Create the folder if it does not exist.
- **The basename must be unique in the vault.** `Dry Run Recap -` is
  deliberately a different prefix from the notes' `Dry Run -`, so the
  two never collide as wiki-link targets.
- **Never overwrite.** If the file exists, stop and ask.

## Frontmatter

```yaml
---
type: document
doc_type: journal
canon_status: DRAFT
dry_run: true
recap_of: "[[Dry Run - {Name} - YYYY-MM-DD]]"
campaign: "[[Campaign Overview]]"
created_by: narrate-encounter
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
the GM's. That has a consequence the user needs to hear — see
§Publishing.

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

**Tense and person change.** At the table you narrate in second
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
| "Run in relay mode: one operator relayed the table's decisions; the players rolled every die." | Which rolls Claude asked for and what DCs they were against |
| "When the fight began, Claude handed the operator both creatures' statistics and the table ran the combat, relaying only the result." | The statistics, or the conditions under which the second creature would have fled |
| "A Perception check split the table: two characters heard through the mimicry and one did not." | The Deception total they were beating |
| "The session ran to about forty minutes." | Anything from the Play Notes' "For the GM" list |

**Name the feature being shown if the user named one.** If the run
was testing something specific — a new handoff format, a named
session, a cold open — say what it was and that it worked, in one
line. If it did not work, a showcase recap is the wrong document;
say so to the user rather than writing around it.

## Check Before Writing

Read the draft once against the Play Notes, looking for leaks:

- **Every number.** Is it a number the players were told? AC, HP,
  DCs and attack bonuses almost never are.
- **Every "if" and "would have".** A conditional is usually a trigger
  or a branch the table never reached.
- **Every creature and NPC.** Did the party actually meet it? A
  creature that stayed hidden is not in the recap, not even as a
  shadow the narrator knows about.
- **Every quotation from a PC.** Did the player say those words?

Then write it with the **Write tool**. Never PowerShell
`Set-Content -Encoding utf8`, `Out-File` or `>`: all three prepend a
BOM, and a BOM before `---` hides the frontmatter from every parser.

## Publishing — What to Tell the User

You write the file. **You do not publish it, add it to a publish
manifest, or edit the vault's publish settings.** Tell the user what
stands between the recap and the site, because the defaults will
usually stop it:

1. **`canon_status: DRAFT`.** A publish setting that drops drafts
   (gm-apprentice calls it `exclude_drafts`) removes it, with no
   per-file override. In a player-mode site the manifest already
   requires every page to be ticked by hand, so the GM may prefer to
   turn the blanket draft filter off there. **Do not suggest promoting
   the recap to `AUTHORITATIVE` to get past it**: that would make a
   test run canon, and a later real session of the same encounter
   would contradict it.
2. **`Dry Runs/` may need adding** to the publish manifest or folder
   map.
3. **The spoiler question** from §Ask One Thing First, if the answer
   was yes.

Say this in a few lines at the end, and hand off to the publishing
skill for the rest.

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
