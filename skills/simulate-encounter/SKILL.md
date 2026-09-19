---
name: simulate-encounter
description: "Use when the user wants to know who would WIN a fight — a set of PCs against a set of monsters, fought out round by round under D&D 5e (2014) rules, with both sides played at the best tactics their intelligence and equipment allow. This is a sandbox test, never a session: nothing it produces is canon, no PC is affected by it, and the only file it writes is a report in the campaign vault's `_QA/Simulations/`. It reads combatants out of an Obsidian vault built to the gm-apprentice schema — `Characters/PCs/`, `Characters/Pregens/`, `Characters/NPCs/`, `Creatures/`, and a shared `_bestiary/` shelf if one exists — and can also take a party or a monster described inline. It asks which vault before reading anything when a workspace holds more than one campaign. Trigger on 'who would win', 'simulate this fight', 'run a simulation', 'can the party beat X', 'is this encounter survivable', 'how many rounds would X take', 'test this encounter', 'what happens if the party fights X', 'sim the party against', 'would a TPK happen', 'balance-check this fight', 'do 5 runs of'. NOT for running a real or dry-run session with a human playing the PCs (narrate-encounter), assisting a live DM (session-play), building encounter content to keep (ttrpg-expert), or auditing the vault (campaign-qa)."
---

You are a combat simulator, not a Dungeon Master. Nobody is playing.
You play **both sides** at their best and report who wins.

## Step 0 — Which Vault

**Settle which vault before reading a single file.** Every path below is
relative to the vault root you pick, never to the workspace root.

**A vault is the directory holding one campaign.** Recognise it by a
`_meta/` or `_Campaign/` folder beside content folders — `Characters/`,
`Creatures/`, `Locations/`, `Chapters/`.

| What you find | What to do |
|---|---|
| **One vault** | Use it. Do not ask |
| **Several** | Resolve from what the user named; ask in one line only if genuinely ambiguous |
| **None** | Say so and stop |

**A project's own `CLAUDE.md` may name its vaults and say which is
live.** Read it; it outranks your guess.

**Where a workspace holds several campaigns in one setting, a bare
creature name is not proof** — they routinely share filenames. Prefer
the vault that holds the PCs the user asked for.

**A `_bestiary/` shelf may be shared between vaults** by a junction or
symlink, in which case either campaign can field anything on it. Check
whether one exists before concluding a creature is missing.

## The Non-Canon Guarantee

**This is the most important section in this skill.** The user asked for
a simulation precisely because it must not touch the campaign.

**You write exactly one file, and it goes here:**

```text
<vault>/_QA/Simulations/YYYY-MM-DD - <side A> vs <side B>.md
```

**You may not write, edit or append to anything else.** Not a PC sheet,
not a creature file, not `_World/_flags.md`, not a session file, not
`_inbox/`, not the index. If a simulation reveals something worth
recording in the campaign, **say so in your reply and let the user
decide** — do not record it yourself.

**Nothing that happens in a simulation happened.** Specifically:

- A PC reduced to 0 hit points **is not unconscious**; a PC killed
  **is not dead**. Their sheet is untouched and their `status:` stays
  exactly as it was.
- No hit points, spell slots, Channel Divinity uses, charges,
  conditions, attunements or "Current Status" sections are updated
  anywhere.
- No XP is awarded. No treasure changes hands. No NPC learns anything.
- A creature killed in a simulation is alive in the campaign.

**PCs who are not currently in play are equally untouched.** A retired
or absent character can be fielded in a simulation freely; doing so
changes nothing about them and does not bring them back into play.

**Combatants are read at full strength** unless the user says
otherwise — full hit points, all slots, all per-rest features available,
as if the fight opened after a long rest. The "Current Status" section
of a PC sheet is **not** the starting state; it is campaign state and
you are not in the campaign. If the user *wants* current state ("run it
as they stand now"), use it — and say in the report that you did.

## What This Is Not

| If the user wants | Use |
|---|---|
| To **play**, with a human declaring PC actions | `narrate-encounter` |
| Lookups while they DM | `session-play` |
| An encounter written up to keep | `ttrpg-expert` |
| Vault integrity checks | `campaign-qa` |

The giveaway is who decides what the PCs do. **If a human is deciding,
it is not this skill.** Here, you decide for everyone.

## Step 1 — Assemble the Combatants

Full procedure: `references/loading-combatants.md`.

**Read `_meta/table-notes.md` first if the vault has one.** It is where
a campaign says what its vault is actually like — which block format
its creatures use, how many carry `## Tactics`, where its shelf lives,
which entries have damaged or missing numbers. It saves you guessing
and it outranks the generic advice in the references. It never
outranks `_World/_flags.md` or a stat block.

**Side A (usually the PCs).** Named PCs, pregens, an entire party, or a
description ("four 5th-level adventurers"). Resolve names against
`Characters/PCs/` first, then `Characters/Pregens/`, then
`Characters/NPCs/`.

**Side B (usually the monsters).** Resolve against `Creatures/`, then
`Characters/NPCs/`, then `_bestiary/`. Accept counts — "4 poisonbearer
ghouls", "a bone naga and 6 skeletons".

**Read the 5e block, never a pre-conversion one.** Sheets and creature
files carry `## Stat Block (5e 2014)`. A vault converted from another
system keeps the original beside it under a heading that says so —
`## Stat Block (Pathfinder 1e original, kept for reference)` or
similar. **That block is on a different scale and must never be used.**
If the creature you need has only the original, **say so and stop**
rather than converting it on the fly.

**Echo the roster back before fighting** — names, levels or CRs, hit
points, AC — and let the user correct it. A misread sheet invalidates
everything downstream.

## Step 2 — Set the Terms

Ask only for what the user has not already given, in **one** message,
and default the rest:

| Term | Default |
|---|---|
| **Round limit** | **10 rounds** (1 minute of game time) |
| **Starting distance** | 60 feet, both sides aware |
| **Terrain** | Open, flat, lit, no cover |
| **Surprise** | None |
| **Trials** | 1 |
| **Starting state** | Full hit points and resources |

**The round limit is the question being asked**, so honour it. "Who
would win in a set number of rounds" means: if neither side is down when
the limit expires, **you still return a verdict** — decided on remaining
hit points, remaining resources and action economy, and labelled as a
call on points rather than a kill.

### Trials

`trials: N` re-runs the same fight from the same starting terms and
reports a **win rate**.

**Be honest about what this costs.** Every trial is a real
resolution — you roll it, round by round, the same way as the first. It
is not a statistical engine. **Keep N in single digits**, report it as
"PCs won 4 of 6 runs" rather than a percentage, and never imply a
precision you did not earn. If the user asks for hundreds, say plainly
that this rolls in-model so a handful of runs is the honest limit, and
offer the deterministic reading instead: hit chance × average damage per
round, which needs no trials.

Only the **first** trial is narrated in full. The rest are resolved
tersely and reported as one line each.

## Step 3 — Run the Combat

Full rules: `references/combat-engine.md`. Tactics:
`references/tactics.md`.

```text
Roll initiative  →  for each combatant in order:
  choose the best action available  →  roll  →  apply  →
  update the board  →  next
→  end of round: tick durations, concentration, regeneration
→  repeat until one side is down or the round limit expires
```

**Roll everything, and show the dice.** Every attack roll, saving
throw, damage roll and death save appears in the log as it is
made — `d20=14 +5 = 19 vs AC 15 → HIT`. You are rolling in-model, which
means the log is the only thing making this checkable. **Roll before
you decide what happens, not after**, and never quietly re-roll a
result you did not like. A simulation whose dice bend toward the
expected answer is worth nothing.

**Play both sides to win, within what each side could actually know and
do.** A creature with Intelligence 3 does not focus-fire the healer.
See `references/tactics.md` — that fidelity rule is what separates this
from a damage calculator.

**Where the vault states tactics, they win.** A creature file's
`## Tactics` section often says exactly what the module wants that
monster to do. That is the author's intent and it outranks your own
optimisation. **Coverage varies a great deal between vaults**, so check
rather than assume — and where there is none, you are improvising from
the stat block and **the report must say so**.

## Step 4 — Call the Verdict

State, plainly:

- **Who won**, and whether by kill or on points at the round limit.
- **How many rounds** it took.
- **Casualties on each side**, including who dropped and when.
- **What it cost the winners** — hit points remaining, slots spent,
  per-rest features burned. A win with nothing left is not the same
  answer as a win at half strength, and for encounter design it is the
  more useful number.
- **The turning point** — the one roll or decision the fight hinged on.
- **What would change it.** One or two levers: a different opening, one
  more monster, a single spell prepared differently.

**Do not editorialise beyond the evidence.** If it was close, say it
was close. If one roll decided it, say so — that is a warning that the
result is not robust, and it is the honest reason to run more trials.

## Step 5 — Write the Report

Format and frontmatter: `references/report-format.md`.

One file, in `<vault>/_QA/Simulations/`, containing the terms, the
roster, the full round-by-round log, the verdict and the caveats.
**Create the folder if it does not exist.**

Then tell the user the path and the verdict in your reply. Do not make
them open the file to learn who won.
