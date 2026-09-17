# Cold Open

Building an encounter to run when the vault doesn't have one that
fits. Read when the players want to play and no prepped encounter
matches where they are, what level they are, or what they want.

**This produces a draft you run, not a file you write.** Nothing goes
into `Encounters/` or `Planning/`. See `canon-boundaries.md` — that
rule does not bend for content you authored yourself.

## When to Cold Open

- No prepped encounter is gated at the party's level
- The party has gone somewhere the vault doesn't cover
- The table wants a fight, a social scene, or a hazard *now*
- You're testing a situation before committing it to prep

**Check the vault first.** `Encounters/` holds standalone set pieces
and each chapter's `Planning/` holds its plot events, gated by
`minimum_level`. Use one if it fits — a prepped encounter has XP math,
beat triggers and survival warnings that a cold open does not.

**Then check whether `_source/` covers it.** This module keys nearly
every hex and every building. If the party has walked into an area
the book details and the vault has not converted, that is not a cold
open — it is unconverted content, and lifting it live means running
Pathfinder numbers as if they were 5e. Say so out of character and
offer the GM the choice: pause and convert, improvise around it, or
turn the party elsewhere in fiction.

## The Procedure

### 1. Audit the party

**Run `party-audit.md` first.** Read the sheets in `Characters/PCs/`
— whoever is actually there, at whatever levels — and derive the
capability audit and the binding constraint. Do not assume a party
size, a level, or a roster from anything but the sheets.

You need: each character's level, current HP, remaining spell slots,
what restoration they have left, and what the party as a whole can
and cannot do.

### 2. Set the budget

5e (2014) DMG thresholds are **per character**. Take each PC's own
row and **sum the columns** — this is how mixed-level parties work;
never average the levels.

| Level | Easy | Medium | Hard | Deadly |
|---|---|---|---|---|
| 1 | 25 | 50 | 75 | 100 |
| 2 | 50 | 100 | 150 | 200 |
| 3 | 75 | 150 | 225 | 400 |
| 4 | 125 | 250 | 375 | 500 |
| 5 | 250 | 500 | 750 | 1100 |
| 6 | 300 | 600 | 900 | 1400 |
| 7 | 350 | 750 | 1100 | 1700 |
| 8 | 450 | 900 | 1400 | 2100 |
| 9 | 550 | 1100 | 1600 | 2400 |
| 10 | 600 | 1200 | 1900 | 2800 |
| 11 | 800 | 1600 | 2400 | 3600 |
| 12 | 1000 | 2000 | 3000 | 4500 |
| 13 | 1100 | 2200 | 3400 | 5100 |
| 14 | 1250 | 2500 | 3800 | 5700 |
| 15 | 1400 | 2800 | 4300 | 6400 |
| 16 | 1600 | 3200 | 4800 | 7200 |
| 17 | 2000 | 3900 | 5900 | 8800 |
| 18 | 2100 | 4200 | 6300 | 9500 |
| 19 | 2400 | 4900 | 7300 | 10900 |
| 20 | 2800 | 5700 | 8500 | 12700 |

Worked examples:

- Four 1st-level PCs → **Easy 100 · Medium 200 · Hard 300 · Deadly 400**
- Four 3rd-level PCs → **Easy 300 · Medium 600 · Hard 900 · Deadly 1600**
- Four 7th-level PCs → **Easy 1400 · Medium 3000 · Hard 4400 · Deadly 6800**
- One 9th + two 7th → Medium 1100 + 750 + 750 = **2600**
- Five 11th-level PCs → Medium 1600 × 5 = **8000**

**The low bands are unforgiving and the arithmetic hides it.** At 1st level
Deadly is 400 XP — two CR 3 creatures with the ×1.5 pair multiplier clear it
outright. A margin that reads as a rounding error at 7th level is a dead PC at
1st. A low-tier campaign can spend three chapters down here.

Apply the multiplier to the monsters' **total XP** before comparing:

| Monsters | ×  |  | Monsters | × |
|---|---|---|---|---|
| 1 | 1 | | 7–10 | 2.5 |
| 2 | 1.5 | | 11–14 | 3 |
| 3–6 | 2 | | 15+ | 4 |

Party of 1–2 PCs: use the next higher multiplier. Party of 6+: the
next lower.

**Default to Medium**, and go below it when the audit says the party
is depleted, small, or missing a capability the encounter would key
on. A Hard encounter fought on spent slots is a Deadly one, and in
the waste there is no inn between fights.

### 3. Cast it from the vault

Pull creatures from `Creatures/` and people from `Characters/NPCs/`
before inventing anything. Reusing a bestiary entry keeps the fiction
consistent and gives you a stat block that's already been converted
and through QA.

If you must invent an NPC, give them a want, a refusal and one verbal
habit — nothing more (`narration-craft.md` §Voicing NPCs). For a
social encounter, give them the vault's fuller shape as well: a
price, a Line, and what is free versus earned
(`dialogue.md` §Reading an NPC for Conversation).

**Stat block caution applies:** vault blocks are 5e 2014 conversions
from Pathfinder. Use the numbers as written. A creature the vault has
not converted is not castable — do not invent a block from its
Pathfinder CR, and do not reach for `ttrpg-expert`'s 2024 block
without saying so in brackets.

### 4. Give it the house shape

A cold open is a thin version of the vault's encounter format. Write
out — for yourself, before play — at minimum:

- **Agenda.** One sentence: what this encounter is *about*. If you
  can't write it, the encounter is just monsters.
- **Opening.** Where you cut in. Late.
- **Two or three beats**, each with a **mechanical trigger** — a
  round number, a completed action, a failed check, a stated span of
  table time. "When it feels right" is not a trigger.
- **A non-combat out.** The party must be able to leave, talk, or
  refuse. An encounter with one exit is a corridor.
- **Outcomes.** Where each branch lands. Do not steer toward one.

### 5. Safety-check it

Before you show it to anyone, answer these:

- Does the multiplied XP land where you intended?
- **Can two threats arrive at once?** If so, stagger them — this is
  the single rule that keeps parties alive, and it is why the vault's
  encounter files forbid stacking a wandering pack onto a set-piece
  fight.
- Can the party disengage? By what route, at what cost?
- Does anything here key on restoration, turning, or darkvision the
  party doesn't have?
- Does it cross a line or veil from the session opening?

### 6. Show it and get a yes

Present it out of character, compactly — agenda, cast, beats and
triggers, budget line — and wait for approval before narrating.

```text
[Cold open — Medium for this party (four 7th-level PCs, 3000 XP).
Agenda: the camp sells you a guide, and the Waste sells the guide you.
Cast: 4 × Ghoul Wolf (CR 2, 450 XP × 4 = 1800 × 2 = 3600 adj.) — a
touch over Medium, so they come in two pairs a round apart.
Beat 1: the guide stops and won't say why. Beat 2 fires on any PC
leaving the road, or round 2 of waiting. Beat 3 fires when one wolf
drops — the guide runs, and not toward the camp.
Out: the barrow mound at 60 ft, high ground and one door.
Run it?]
```

If the player is also the GM, that yes is theirs to give. If the
table is players only, present it as a difficulty check — "this'll be
a real fight, still want it?" — not as a design review.

### 7. Run it

Same loop as any prepped encounter. Your own beat triggers bind you
exactly as a vault file's would.

## Afterwards

A cold open that happened is now something that happened. In the Play
Notes — under its own `## Encounter — ` heading if the session already
ran something else (`session-files.md`):

- `NEW-EVENT` the encounter itself, with its agenda in one line
- `NEW-NPC` / `NEW-LOC` every named person and place
- Note that it was improvised, not drawn from prep

At session end, tell the GM plainly: *this was a cold open, nothing
about it is in the vault, and if you want it to exist,
`session-wrapup` will file the entities and `ttrpg-expert` will write
the encounter up properly.* Then stop. Filing it is not your job.

## What This Is Not

- **Not a replacement for prep.** A cold open has no clue structure,
  no arc placement, no `leads_to`, and no QA pass. It is a scene, not
  a chapter.
- **Not a way around level gates.** If the party wants the tar dragon
  at 7th level, a cold open does not make that survivable and must
  not quietly weaken it.
- **Not a way around conversion.** If the book has it and the vault
  doesn't, the answer is "not yet," not a Pathfinder block read at
  the table.
- **Not canon.** Nothing you author here binds the vault, and nothing
  in it may contradict what does.
