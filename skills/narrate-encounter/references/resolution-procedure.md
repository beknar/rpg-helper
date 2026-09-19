# Resolution Procedure

Full mechanical resolution for **D&D 5e (2014)**. You call the rolls,
you roll them, you apply the rules, you track state.

## Edition

**This skill runs 5e 2014.** Confirm it against the vault —
`_meta/vault-config.md` records the system (`system: dnd-5e-2014`) and
`[[Campaign Overview]]` usually says so too. **If the vault records a
different system, stop and say so**: this skill's resolution rules are
2014 and nothing else.

Other rule sets will be within reach, and none of them is the table's:

- **The source module may be another system entirely.** Where a vault
  was converted, the original text sits in `_source/` — `AC 34 (touch
  2)`, `Fort +12`, `DC 25 Climb`. **None of that resolves anything at
  this table.** An area's DC in the book is an input to a conversion,
  not a number to call.
- **`ttrpg-expert` ships 5e 2024** (`systems/dnd-5e-2024/`). Wrong
  edition for this table.
- **Supplementary bestiary PDFs are often older editions still.**
  Ecology and lore, not stat blocks.

Order of authority:

1. **The encounter's own Stat Blocks section** — the vault's 5e 2014
   conversion, with the source page in its frontmatter
2. **`[[Campaign Rules]]` and `Documents/`** — the vault's digests
3. **`_World/_flags.md`** — GM rulings and conversion decisions,
   which outrank everything
4. **2014 SRD from your own knowledge**
5. **`ttrpg-expert/systems/dnd-5e-2024/`** — only for things the
   editions share (a CR 1/2 Scout is the same in both), and say so
   in brackets when you lean on it
6. **Never `_source/`** for a number. If the vault lacks the block,
   say so out of character and stop; converting is `ttrpg-expert`'s
   job with the GM watching, not yours mid-scene.

Where the editions diverge — weapon mastery, the 2024 rules for
surprise, exhaustion, grappling, ready actions, cantrip scaling,
crit rules — **use 2014**.

## Campaign Rules That Override the Book

**From `_meta/vault-config.md`. Read the file — it is the authority,
and the settings below are only the ones that most often differ from
the book:**

| Setting | Why it matters mid-scene |
|---|---|
| **Flanking** | An optional rule. If the vault does not use it, there is no advantage for surrounding |
| **Inspiration** | Some tables let it stack; the cap changes what a player can spend |
| **Levelling** | Party-together vs individual XP changes what you award and when |
| **Critical hits** | House variants (max damage, double dice, crit tables) are common |
| **Starting level and chapter bands** | The vault's chapter files carry each band as `minimum_level` |

**Never invent a house rule to settle a dispute.** If the file is
silent, use 2014 RAW, say in brackets that you did, and let the GM
make it permanent afterwards.

## When to Call for a Roll

All three must be true:

1. The outcome is **uncertain**
2. **Failure is interesting** — it costs, complicates, or turns
3. The PC is **actually attempting it**

Otherwise say yes and narrate. A 7th-level party can afford a lot;
it cannot afford a tax on every door in a city with a thousand of
them.

## The Call

State ability, skill, DC and stakes **before** the roll.

> *"Insight, DC 16 — and if you're still staring at him when Kess
> comes back in, Varn stops answering questions tonight."*

DCs come from the encounter file where it gives them. Where a file
specifies DC 15 Survival to spot the acid rain forming, use that
number, not your own, and not the book's.

## Rolling

Default: **you roll, in the open, one line, before the narration.**

```text
Insight +5 vs DC 16 → rolled 14+5 = 19, success
Stealth (pack) +3 vs passive Perception 15 → rolled 9+3 = 12, seen
Longsword +9 vs AC 17 → rolled 11+9 = 20, hit
Con save +2 vs DC 12 → rolled 4+2 = 6, fail — paralysed
```

If a player wants to roll their own, that holds for the session — ask
for the total and apply it.

**Rolls you make privately:** only those whose *existence* is secret —
the ghoul pack's approach Stealth, an NPC's Deception the party has no
reason to suspect. Narrate the fiction, not the roll. Never hide a
normal check.

**Never fudge.** A rolled result stands. The levers here are
inspiration (stacks to 3), a Help action, terrain, and the encounter's
own break-off rules — name the one you're using.

**Death saves are the player's.** You don't roll them and you don't
narrate their outcome before they're made.

## Combat

1. **Initiative once**, listed, kept visible.
2. **Round header:** round number, whose turn, standing conditions.
3. **One action → one resolution → one sentence of fiction.**
4. **Obey the encounter's survival rules.** Where a file says two
   fights never run simultaneously, or that enemies break off on a
   condition, that is the design keeping the party alive. Read its
   XP Math section before you deviate.
5. **Describe enemy state qualitatively** in fiction, numerically in
   the state block.
6. **End early.** When the outcome is settled, narrate the finish.

## Environmental Clocks

Campaigns run clocks, and they are not background detail. **Track what
the chapter and encounter files specify**, and the §Clocks list in
`_meta/table-notes.md` where the vault has one — every module puts the
pressure somewhere, and it is rarely the same place twice.

### Low tier — light, rest and the road

- **Torches and darkvision.** A mixed party means someone is always the
  one who cannot see. In a long underground stretch, note who is
  carrying the light and what it costs them to hold it.
- **Watches and interrupted rests.** A night camp is tracked state:
  who is on which watch. **Check the vault's own rest rules** — many
  campaigns adopt the *Xanathar's* sleeping-in-armour variant, where
  medium or heavy armour returns a quarter of spent Hit Dice, minimum
  one, and **no hit points**. At 1st level each PC has exactly one die.
- **Wilderness travel**, with the chapter file's own encounter table
  where one exists.
- **Healing is usually the binding constraint.** At low levels there is
  no reserve — a cleric's slots, one Hit Die each, and whatever potions
  the party carries.

### Hostile environments — the place is itself the clock

- **Random encounter checks on the interval the chapter names**, and
  after any fight that runs long. The chapter file names the table; you
  roll it, or in relay mode you name it and the operator rolls.
- **Weather events are encounters** — storms, acid rain, searing wind,
  quicksand. Each usually has a Survival DC to see it coming and a
  window to prepare. **Track the window.**
- **Water and rations**, wherever the environment supplies neither.
- **Light**, and who is outside cover at night.
- **Condition clocks the local threat imposes** — paralysis rounds,
  exhaustion, disease incubation, and whatever the campaign's
  conversion uses in place of mechanics the edition dropped.

When a clock has moved, say so in the state block. When it is about
to matter, let the fiction say so first — the dust lifting, the
horses refusing — before the mechanics do.

## Encounter State Block

Emit between beats when it changes, at the top of each combat round,
and on request. Under eight lines.

```text
── State ──
Round 3 · Barrow A7, the open waste
Fighter   HP 41/68  AC 19  —
Wizard    HP 30/38  slots 4/3/2/0   (fireball spent)
Cleric    HP 44/52  slots 4/1/2/1   channel 0/2
Ranger    HP 18/55  paralysed (2 rounds left)
Tark wounded · 2 death dogs down · 3 wights engaged
Varn: Wary · Kess: Hostile
Waste: 2h since last check · haze 30 ft · water 1 day
```

NPC disposition is tracked state like anything else — see
`dialogue.md` §The Disposition Ladder.

## Handling the Unplanned

Players will leave the prepped encounter. That is not a failure state.

1. **Search the vault first.** `_meta/index.md` has the live entity
   count — the place or person may already exist. If it exists only
   in `_source/`, say so out of character and offer the GM the choice;
   do not lift it.
2. **If it doesn't, improvise it** and mark it `NEW-NPC` / `NEW-LOC`
   in the Play Notes. Never write an entity file
   (`references/canon-boundaries.md`).
3. **Don't rail them back.** A prepped encounter that still matters
   can find them later.
4. **Respect level gates in fiction, not by fiat.** Check the
   target's CR against the party the audit found — the Brood Mother's
   Pit at CR 12 is lethal to a 7th-level party and a hard day for an
   11th. If the gap is real and they go anyway, the distance, the
   Waste and the guide's refusal are all real obstacles — and if they
   push through all of them, the consequence is real too. Say out of
   character what they're walking into before it kills them.

## Stat Block Cautions

- Blocks are **5e 2014 conversions of Pathfinder originals**. Every
  one carries `source:` with the `_source/` page and, where the
  conversion was not mechanical, a `_World/_flags.md` entry.
- Use the number as written. If it looks wrong, say so in brackets
  and cite the page — do not open the Pathfinder block at the table
  and do not average the two.
- **Never silently correct one.** Fixes happen when the GM asks, and
  get noted.
- A creature the vault has not converted yet is not available. Say
  so; do not improvise a block from its Pathfinder CR.

## Ending

Stop on a beat, not mid-resolution. Then:

- Flush everything since the last write to the Play Notes
- Three lines: where the PCs stand, what's unresolved, what's coming
- Name anything improvised that now needs a file, and anything marked
  `CONFLICT`
- Point at `session-wrapup`
