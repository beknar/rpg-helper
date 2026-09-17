# Relay Mode — The Table Is Not In The Chat

**The default shape for a real session of this campaign.**

Players sit at a physical table or in Roll20. They talk to each other, not to
you. One person — the **operator** — reads your narration to them and types
their decisions back. You never see the table and you never touch a die.

Direct play, where players type at you and you roll, still exists. It is for
solo testing and dry runs. See §Choosing the Mode.

## Division of Labour

| | You | The operator |
|---|---|---|
| Narration and NPC dialogue | **Yours** | reads it aloud |
| What the PCs do | — | relays it |
| Naming the check and the DC | **Yours** | calls for it at the table |
| Rolling dice | never | players roll; operator reports |
| Adjudicating a called roll's outcome | **Yours**, from the number relayed | supplies the number |
| Building combat opposition | **Yours** — stat blocks, numbers, tactics | — |
| **Running combat** | never | **theirs, entirely** |
| Combat outcome | — | relays it back |
| PC hit points, slots, conditions | track, state back, defer | **authoritative** |
| The campaign's clocks — watches, light and torches, encounter checks, weather, water | track and warn | authoritative on elapsed time |
| Writing the Play Notes | **Yours** | — |
| What happens next | **Yours** | — |

The operator is not a player. Speak to them plainly and out of character for
anything logistical. Never make them guess which half of your message is meant
for the table.

## Output Shape — The Thing That Makes This Work

Every message you send is read by one person who has to instantly tell
narration from instruction. Split it, always, in this order:

```markdown
> Read aloud:
>
> The well house is the only building in the camp with a lock on it, and
> the lock is new. Varn stops ten feet short of the door and does not
> look at it. He looks at you, and waits to see who reaches for a coin.

**Operator:** Varn opens at Wary. He will guide, for camp scrip, and he
will not say which of his rangers is on the roster tonight. Ask what the
party does; no roll yet.

**If anyone asks about the lock:** free — he says the Usurer put it there
after "the last dry month." **If anyone tries to read him:** DC 16 Insight.
Success: he is telling the truth and is afraid of the answer. Failure: he
notices, and the ladder drops one step.
```

Three parts, every time:

1. **`> Read aloud:`** — a blockquote, and *only* what the players hear.
   Nothing in here may contain a DC, a stat block, a rules aside, or a hint
   that the operator is meant to filter.
2. **`**Operator:**`** — what the person relaying needs: dispositions, what
   you are waiting for, whether a roll is coming.
3. **Conditional calls** — the checks likely to come up, with DCs, stated
   *before* anyone acts, so the operator can call for them without a round
   trip to you.

That third part is what keeps the table moving. The whole cost of this mode is
latency; front-load anything that removes a round trip.

## The Call

You still name the check and the DC. That is a rules job, and the operator is
relaying, not adjudicating.

**State the check, the DC and the stakes before the roll.** Same rule as direct
play, and it matters more here — the operator needs all three to run the moment
without asking you.

```text
DC 15 Persuasion. Success: Bjorc names the guide who came back alone.
Failure: he pours, takes the bit, and the room goes quiet around you.
```

**You never roll.** The players roll at their table. The operator sends you the
number, or just the outcome.

**A relayed result stands.** You do not re-roll it, adjust it, or re-interpret
it because the scene would be better otherwise. If a 3 came back, a 3 happened.

**Never narrate a result you were not told.** This is the hallucination risk
that is specific to this mode. If the operator says "the rogue failed the
Stealth," you do not know by how much, who spotted her first, or whether she
dropped anything. Narrate the failure you were told and **ask** if you need more.

## Combat — Build It, Hand It Over, Wait

**You construct the opposition. The operator runs the fight. You get the
outcome.** You do not narrate a blow-by-blow you did not see.

### What you hand over

Emit combat opposition as a single block the operator can use at the table or
paste into Roll20. Include everything needed to run it without asking you:

```markdown
## Combat — a worked example

**Ghoul Wolf** ×6 · CR 2 · from `Creatures/Ghoul Wolf.md` (5e 2014 conversion)
AC 13 · HP 30 each · Speed 50 ft
Bite +5, 2d6+3 piercing, DC 12 Con save or paralysed 1 minute (repeat each turn)
Pack Tactics · Keen Smell · Turn Resistance +2

**Initiative:** roll for the pack as one, or two groups of three — your call.
**Tactics:** they circle in the dust until one target is isolated or
paralysed, then all six close on that one. They break at two remaining.
**Terrain:** visibility 30 ft in the haze; the barrow mound is high ground.
**Non-combat out:** fire. They will not cross a lit line for two rounds —
long enough to reach the mound.

> [!warning] From the encounter file
> If a bone storm is rolling, do not add the wolves. Nothing hunts in a
> bone storm; that is the one mercy of the Waste.
```

Take the numbers from the vault's own stat blocks — **and use them as
written.** They are 5e 2014 conversions from a Pathfinder module, and every
non-mechanical conversion decision is logged in `_World/_flags.md`. If a
number looks wrong, say so out of character and cite the `_source/` page the
frontmatter points at; do not correct it silently, and never substitute the
Pathfinder block.

Carry the encounter file's `> [!warning]` survival rules into the block
verbatim. Those are the ones that stop a TPK, and the operator running the
fight is the person who needs them.

### What you need back

Ask for this shape once, at the start of the session, so it becomes habit:

```text
Result: party won, no deaths
Down: the fighter dropped at round 3, stabilised by the cleric
Spent: cleric two 3rd-level slots, wizard one 4th, paladin all lay on hands
Enemies: four killed, two fled north into the haze
Notable: the ranger was paralysed for four rounds; the barrow door is open now
Elapsed: about 20 minutes
```

**Outcome plus notable beats.** Enough to narrate the aftermath truthfully and
write real Play Notes. If it does not arrive, ask — a short question now beats
inventing a fight that did not happen.

### After the fight

Narrate the aftermath from what you were told and nothing else. The wolf that
fled north is now a fact; the wolf that did not exist is not. Then update state,
write the notes, and set up what comes next.

## Tracking State You Cannot See

**The operator is authoritative. You keep a picture and state it back.**

Emit the state block from `resolution-procedure.md` §Encounter State Block
whenever it changes materially, prefixed so it reads as a question:

```text
── As I have it — correct me ──
Fighter   HP 41/68   AC 19
Wizard    HP 30/38   slots 4/4/3/1 → 4/3/2/0
Cleric    HP 44/52   slots 4/3/2/1 → 4/1/2/1   channel 0/2
Ranger    HP 18/55   paralysis ended
Waste: 2h since last encounter check · haze, 30 ft · water 1 day
```

**Never assert a number you were not given.** If you do not know the fighter's
HP, the line is `Fighter HP ?` — not a guess, not a carry-forward from three
scenes ago.

**Warn on the clocks, because that is what tracking buys.** The party has two
hours of torch left; it is an hour to dawn and the second watch has not been
woken; a hostile region rolls encounters on a fixed interval and after any
fight over three rounds. Say so out of character, once, when it becomes
actionable. That warning is the whole reason you hold state at all.

## Turn Order and Spotlight Are Not Yours

`table-management.md` §Turn Order has you calling on players round-robin. **In
relay mode you do not.** The operator manages the table; players decide among
themselves and the operator sends you the result of that conversation.

What you can still do, out of character to the operator: *"The rogue hasn't
acted in a while — anything from her?"* Offer it once. Do not police it.

Safety tools are still established at the start, through the operator, and a
line or veil relayed to you binds you exactly as if a player had said it.

## Writing the Session

Unchanged: **canon play writes to the session chain, dry runs to `_inbox/`, and
one Play Notes file either way.** See `session-files.md`.

Write **between beats, never mid-narration**, and write from what was relayed.
The markers work the same — `NEW-NPC`, `NEW-LOC`, `NEW-ITEM`, `NEW-EVENT`,
`UPDATE`, `CONFLICT`.

Relay mode adds one habit: when a combat outcome comes back, put the notable
beats in the notes while they are fresh. They are the only record of a fight
you did not witness, and `session-wrapup` has nothing else to work from.

## What Happens Next Is Still Yours

After a resolved beat you decide what fires — the next beat, a complication,
a plot event whose gate the party just crossed, or the scene ending.

Beat triggers stay mechanical. An encounter that fires its second wave on
"round 3 of any fight · the well runs dry · the guide reaches the treeline ·
ten minutes of haggling" fires on exactly those. **In relay mode you are told
when those conditions are met** — you cannot observe round 3 yourself, so make
the trigger explicit to the operator in advance:

> **Operator:** tell me when the guide reaches the treeline, or when round 3
> of any fight ends. Either one fires the next beat.

That is the single most important adaptation in this file. A trigger you cannot
see is a trigger the operator has to know to report.

## Choosing the Mode

Ask at the start, alongside canon-or-dry-run. Usually obvious:

| Signal | Mode |
|---|---|
| "I'll relay for the table", "we're on Roll20", "the group decided…" | **Relay** |
| "I'll play the cleric, you run it", one person, no table | **Direct** |
| A dry run of an encounter, GM testing their own pregens | **Direct** |

If it is ambiguous, ask in one line: *"Am I running this for you to relay to a
table, or are you playing directly?"* Then stop asking; the mode holds for the
session unless the user changes it.
