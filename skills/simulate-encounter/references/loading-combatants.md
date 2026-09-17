# Loading Combatants

Where the numbers come from, how to read them, and what to do when they
are not there. **Getting a sheet wrong invalidates the whole run**, so
echo the roster back before the first initiative roll.

## Where to Look, In Order

### Side A — usually PCs

| Order | Folder | Notes |
|---|---|---|
| 1 | `Characters/PCs/` | The real party |
| 2 | `Characters/Pregens/` | Book pregens, where the vault ships them |
| 3 | `Characters/NPCs/` | For an NPC fighting on the party's side |

**Count the directory; do not assume a party size.** Some vaults have a
full roster, some have pregens only, some have no PCs at all. If
`Characters/PCs/` is empty and the user named PCs, say so and ask.

**`Characters/Pregens/` is not the party.** It is the book's
pregenerated characters. Field them only if the user names them or asks
for "the pregens".

**Ignore `*_Story.md` files.** Some vaults pair each PC sheet with a
`<Name>_Story.md`; that is narrative background and carries no
mechanics.

### Side B — usually monsters

| Order | Folder | Notes |
|---|---|---|
| 1 | `Creatures/` | The campaign's own creatures |
| 2 | `Characters/NPCs/` | Named antagonists with stat blocks |
| 3 | `_bestiary/` | A reference shelf, if the vault has one |

**A `_bestiary/` shelf is a lookup, not campaign content.** Where one
exists it holds reference stat blocks — often thousands, one folder per
source book — marked `conversion: "5e-reference"`. Those are already 5e
and need no conversion. The shelf may be shared between vaults by a
junction or symlink.

**Prefer the campaign file over the shelf when both exist**, and expect
common names to clash — Goblin, Owlbear, Stirge, Wolf and their kin
appear in both. The campaign file is the one with module context and the
campaign's own conversion; the shelf entry is a generic lookup. If you
deliberately use the shelf entry, say so.

## Reading a PC Sheet

The mechanics live under **`## Stat Block (5e 2014)`** and the two
sections after it. Frontmatter carries `class`, `subclass`, `level`,
`race`, `background`.

What to pull:

- **Armor Class**, **Hit Points**, **Speed**, **Initiative**,
  **Proficiency Bonus**, **Passive Perception**
- **Spell Save DC**, **Spell Attack**, **Spellcasting Ability**
- The **ability score table** — six columns, score and modifier
- **Saving Throws** — which are proficient, and at what bonus
- **Skills**, **Languages**
- **`### Attacks`** — each line gives a to-hit bonus or a save DC, the
  damage dice and the damage type, and the range. This is the menu.
- **`## Spells`** — **Spell slots** by level, then cantrips and each
  spell level. Slots are the resource that decides long fights.
- **`## Features & Traits`** — reactions, per-rest abilities, passives.
  **Read all of them.** Warding Flare, Channel Divinity, Second Wind,
  Relentless Endurance and their kin change outcomes and are easy to
  miss because they are prose rather than a stat line.
- **`## Equipment`** — armour, shield, weapons, consumables, and the
  weapon and armour proficiencies.

**Potions and scrolls in Equipment are usable.** If the sheet lists
them, the character has them; spending one is a legitimate tactical
choice and must be logged.

**`## Current Status` is campaign state, not starting state.** Skip it
unless the user asked to run the fight "as they stand". It records hit
points, location and open threads from live play and has no business in
a sandbox.

## Reading a Creature File

The 5e block is under **`## Stat Block (5e 2014)`**, in standard
*Monster Manual* order: name, size and type, AC, HP, Speed, the ability
row, skills, resistances, immunities, senses, languages, Challenge, then
traits, actions, reactions and legendary actions.

**Vaults format it differently and you must handle both shapes:**

| Layout | What it looks like |
|---|---|
| **Fenced** | inside a ``` block, plain text, *Monster Manual* line order |
| **Markdown** | bold labels (`**Armor Class** 13`) and a pipe table for the ability row |

**These can differ between two vaults in the same workspace**, so look
at the file rather than carrying an assumption across.

**Do not assume a `## Tactics` section exists.** Coverage varies wildly
— some vaults give every creature one, others give it to a handful.
Where there is none you are working from the stat block's own design and
the Intelligence gate in `tactics.md`, and **the report should say so**
rather than implying the vault dictated the doctrine.

**Do not assume every creature has a 5e block either.** In a vault
converted from another system, some entries will still be
pre-conversion. See *When the Numbers Are Not There* below.

**Never read a quarantined pre-conversion block.** A vault converted
from another system keeps the original verbatim under a heading that
says so — `## Stat Block (Pathfinder 1e original, kept for reference)`,
`#### The Pathfinder printing`, or similar. Those numbers are on a
different scale entirely (touch AC, CMB/CMD, Fort/Ref/Will) and are
**not playable in 5e**. If a heading says the block below it is the
original, it is not for you.

**Read `## Tactics` where it exists.** It ranges from "Not described in
the source" to a full doctrine, and where it says something, it governs
— see `tactics.md`.

**Check for a `> [!success] Run this one at the table` callout.** The
conversion notes above a block sometimes record a deliberate departure
from the Monster Manual chassis that matters in play.

## Counts, Duplicates and Naming

Accept "4 poisonbearer ghouls" and field four identical copies. **Give
them letters** — Ghoul A through D — and track each one's hit points
separately. Never pool them; "the ghouls have 312 hit points between
them" destroys the whole point, because focus fire is the single most
important tactic in 5e and it only works against individuals.

Roll initiative **once per group of identical creatures** unless the
user asks otherwise. That is the standard table convention and it keeps
a ten-skeleton fight readable.

## When the Numbers Are Not There

**A creature with only a pre-conversion block.** **Say so and stop.**
Do not convert on the fly: a converted vault has a conversion
procedure, usually a locked DC formula and a ruling log, and a number
invented mid-simulation would be both wrong and untraceable. Offer to
run a different creature, or to convert it properly first as a separate
job.

**A deliberate stub.** Some entities exist only to point at another
product and carry no stats by design. The file will say so.

**A sheet that is damaged or incomplete.** Conversions lose lines — a
missing AC, a missing ability row. Good vaults flag it in the file that
holds it. **If a load-bearing number is missing, name which one and
stop**; do not fill the gap with a plausible guess.

**An entity with no stat block at all.** Deities, historical figures and
pure lore entries have nothing to convert. They cannot fight.

## Inline Combatants

The user may describe a combatant instead of naming one — "four
5th-level adventurers", "a homebrew CR 9 brute". Build it, **show the
block you built**, and mark it clearly in the report as invented rather
than loaded from the vault. It is not canon and must not be written to
`Creatures/`.
