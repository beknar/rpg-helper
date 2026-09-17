# Party Audit

How to read whatever party is actually in the vault, rather than
assuming the one that was there when this skill was written.

Run this on first invocation, before framing anything, and again if
the party changes mid-campaign. Everything downstream — the XP
budget, the difficulty call, which threats are survivable, whose
spotlight is owed — depends on getting it right.

## Where the Party Lives

**`Characters/PCs/` is the source of truth.** One file per character,
named for the character.

- Read every `*.md` in `Characters/PCs/`
- **Exclude** `_About - PCs.md` and any `{Name}_Story.md` — the Story
  files are narrative companions that `campaign-qa` expects, not
  sheets
- A file with `type: pc` and a `## Stat Sheet` section is a character

**`_Campaign/Player Characters.md` is a summary, not the sheets.** It
carries the roster table, player assignments and party-capability
notes, and it can lag behind the sheets. Read it for who is playing
what and for the GM's own notes; take numbers from the sheets.

Where the two disagree, the sheet wins, and say so once in brackets.

**As of the last vault update there are no PCs.** The directory may
be empty. If it is, say so and stop: a party is a Session 0 job, not
something to invent at the table.

## What to Extract Per Character

The sheets follow a consistent shape under `## Stat Sheet`:

| What | Where |
|---|---|
| Race, class, **level**, background | The bold line under `## Stat Sheet` — e.g. `**Hill Dwarf Cleric 7 (Life)** · Acolyte · Lawful Good` |
| Ability scores and modifiers | The six-column table below it |
| **AC, HP**, Speed, Proficiency, Initiative | The two-column table — `Armor Class`, `Hit Points` |
| Saves, senses, passive Perception | Same table |
| Skills and modifiers | The `**Skills:**` line |
| Class and racial features | The `**Class features**` / `**Racial features**` lists |
| Spells | The sheet's spell section |
| Player | `player_name` in frontmatter — may be empty |
| Alive or not | `status` in frontmatter |

**Level and class are in the body, not the frontmatter.** The PC
template carries no `level`, `class`, `hp` or `ac` field, so parsing
frontmatter alone tells you nothing about capability. Read the Stat
Sheet.

**`status: alive`** — a character marked dead or retired is not in the
party. Check it; getting PC status wrong is a serious error.

## Build the Party Table

Hold this for the session and re-state it when it changes:

```text
── Party ──
<name>    Human Fighter 7 (Battle Master)   AC 19  HP 68/68  PP 13
<name>    High Elf Wizard 7 (Evocation)     AC 13  HP 38/38  PP 14  slots 4/3/3/1
<name>    Hill Dwarf Cleric 7 (Life)        AC 18  HP 52/52  PP 15  slots 4/3/3/1
<name>    Wood Elf Ranger 7 (Hunter)        AC 16  HP 55/55  PP 17  slots 4/3
```

## The Capability Audit

Derive these from the sheets. **Do not carry them over from a
previous party** — this is the step that goes stale first.

| Question | Why it changes the encounter |
|---|---|
| **Who heals?** How much, how often? | A party with no healer cannot take a Medium fight twice, and neither module offers an inn between them |
| **Who sees in the dark?** | Decides who is useful at night and underground, and who is holding a torch that announces the party |
| **What is the front line?** Best AC and HP | Determines whether melee threats are a problem or a formality |
| **Who scouts?** Stealth, passive Perception | Sets whether an ambush is possible at all |
| **What crowd control exists?** | The difference between six of something and six of something at once |
| **Can anyone fly, climb, or breathe water?** | Several set pieces in both campaigns gate on movement, not on damage |
| **What can't they do?** No ranged, no healing, no lockpicking, no one who can talk | Encounters that key on a missing capability are unfair, not challenging |
| **Total party HP** | The number that says whether one bad round ends the session |

### Add the campaign's own questions

**Low tier (roughly levels 1-5).** Low-level parties fail on
attrition, not on capability gaps.

| Question | Why |
|---|---|
| **What is the entire healing reserve?** Slots, Hit Dice, potions | At 1st level that is one cleric's slots and **one Hit Die each**. It is the binding constraint for most of a first chapter |
| **Does an ally NPC carry consumables?** | A hireling holding five potions roughly doubles the reserve, and whether they share freely is a GM decision |
| **Who can open a lock or find a trap?** | In a trap dungeon, a party with nobody to check is on a different difficulty curve entirely |
| **How many light sources, and who holds one?** | A long underground stretch with a mixed-darkvision party is a logistics problem before it is a combat one |

**Higher tier, and campaigns with a signature threat.** The reserve
that runs out is rarely hit points.

| Question | Why |
|---|---|
| **Who can undo what this campaign's monsters do?** Paralysis, disease, exhaustion, whatever the conversion uses in place of level drain — *lesser restoration*, *greater restoration*, *remove curse*, *revivify* | A party with no restoration effect is playing on a shorter clock than it knows |
| **Who can turn or repel the signature enemy?** Channel Divinity, radiant damage, silvered weapons | Decides whether a pack is a fight or a retreat |
| **Who sees in this environment?** | Dust, fog, darkness and depth change the encounter before initiative is rolled |

**State the binding constraint out loud to yourself before designing
anything.** For a 1st-level party it is almost always **raw hit points
and healing** — one bad round ends someone. For a mid-tier party in a
hostile environment it is usually **restoration**: how many times the
cleric can clear a condition before the party has to turn back. For a
different party it will be something else — **find it, do not assume
it.**

## Party Composition Cases

**Any size.** The party is however many sheets there are, minus the
dead and retired, minus absent players' characters
(`table-management.md` §Absent Players). It is not four. The module
was written for four to six; the vault's XP Math sections assume
whatever the GM prepped for, and say so.

**Mixed levels.** 5e (2014) handles this natively: take each
character's own thresholds and **sum them**. A party of a 9th-level
and two 7th-level PCs has a Medium budget of 1100 + 750 + 750 = 2600.
Never average the levels.

**Small parties (1–2 characters).** Use the next higher encounter
multiplier, and lean below Medium. A solo PC has no attrition budget
at all, and this module was not written for one.

**Large parties (6+).** Use the next lower multiplier. Watch the
spotlight rather than the budget — six players is a turn-order
problem before it is a difficulty problem.

**No divine caster.** Flag it once, out of character, at the start.
A party that cannot cure disease or end paralysis will lose someone
to the Waste, and that should be a choice they made knowing it.

**A character you can't parse.** If a sheet is missing its Stat
Sheet, ask for level, AC, HP and the character's one distinguishing
capability. Don't guess and don't average from the others.

## When the Party Changes

Re-run this audit when a PC dies, retires, joins, or levels — and
note the change in the Play Notes with an `UPDATE` marker. **Do not
edit the sheets or the roster file**; that is `session-wrapup`'s
work (`canon-boundaries.md`).

## Feeding the Cold Open

`cold-open.md` step 1 and step 2 take their inputs from here: current
state per character for the budget, the capability audit for what the
encounter can fairly key on, and the binding constraint for how hard
to make it.
