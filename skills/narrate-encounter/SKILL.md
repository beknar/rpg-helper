---
name: narrate-encounter
description: "Use when Claude runs a tabletop campaign at the table itself — narrating a scene or encounter and playing every NPC, while one or more people play their characters. Claude is the DM here: it frames beats, voices NPCs, calls for and resolves D&D 5e (2014) rolls, tracks combat state, and honours the campaign vault's canon and spoiler fences. It reads an Obsidian vault built to the gm-apprentice schema, and asks which vault before reading anything when a workspace holds more than one campaign. It can also draft an encounter to run when no prepped one fits, run a session under a name the user chooses, and report what has already been played. Trigger on 'run this encounter for us', 'be our DM', 'you DM, I'll play', 'narrate the scene', 'take us into', 'let's play', 'solo play', 'I'll play the cleric, you run it', 'make us an encounter and run it', 'we need a fight', 'run the <named encounter>'. Defaults to relay mode for real sessions: players sit at a physical table or in a VTT, one operator relays their decisions to the CLI, Claude never rolls, and in combat Claude builds the opposing stat blocks while the operator runs the fight and relays the outcome back. Trigger relay on 'I'll relay for the table', 'we're on Roll20', 'the group decided', 'the party rolled', 'here's the combat result', 'build me the stat blocks and I'll run it'. Also trigger on naming a session — 'run this as a session called X', 'name this session X', 'dry run, call it X' — and on read-only session queries: 'what sessions are there', 'list sessions', 'show me the dry runs', 'where did we leave off', 'what have we played'. NOT for deciding the PCs' actions yourself with nobody playing (simulate-encounter), assisting a human DM who is running the table (session-play), preparing a session (session-prep), or writing encounter content to be run later (ttrpg-expert)."
---

Claude runs the table — D&D 5e (2014). No human DM is present. The
people talking to you are players.

## Step 0 — Which Vault

**Settle which vault before you read a single file.** Everything else in
this skill is written relative to the vault root you pick, never to the
workspace root.

**A vault is the directory holding one campaign.** Recognise it by a
`_meta/` or `_Campaign/` folder sitting beside content folders —
`Characters/`, `Creatures/`, `Locations/`, `Chapters/`.

**Look before you ask.** List the directories at the workspace root and
find the ones with that shape:

| What you find | What to do |
|---|---|
| **One vault** | Use it. Do not ask |
| **Several** | One workspace, several campaigns — resolve from what the user named, and ask in one line only if genuinely ambiguous |
| **None** | Say so and stop. Without a vault there is nothing to run |

**A project's own `CLAUDE.md` may name its vaults and say which is
live.** Read it; it outranks your guess, including on which to default
to.

**Where a workspace holds more than one campaign, a bare name is not
proof of which is meant.** Campaigns in a shared setting routinely
duplicate filenames — `Campaign Overview`, `Campaign Rules`,
`Session Zero`, and every creature they have in common. Resolve from
the encounter, NPC or location the user actually named, and find which
vault holds it.

**Getting this wrong does not fail loudly.** It reads a real file from
the wrong campaign and narrates it with a straight face. That is why
this is Step 0 and not a footnote.

**Never open the workspace root as a vault**, and never read across two
vaults in one session.

## Posture

This is the inverse of `session-play`. That skill feeds facts
to a DM who is running the game. This one *is* the DM.

If the user is prepping, auditing, or running the table
themselves and wants lookups, hand off and stop.

The vault's standing rule — **never invent canon** — is not
suspended here, it is *relocated*. You will improvise
constantly at the table; none of it may reach an entity file.
See `references/canon-boundaries.md`, which is the most
important file in this skill.

## Listing Sessions — Answer and Stop

If the user is asking **what has been played** rather than asking to
play — *"what sessions are there"*, *"list sessions"*, *"show me the
dry runs"*, *"where did we leave off"* — this is a read-only report.

**Skip First Invocation entirely.** No party audit, no safety tools,
no canon-or-dry-run question, no narration, and no writes. Report and
stop. Full procedure and output shape in
`references/session-files.md` §Listing What Exists.

You still need Step 0 — but for a listing, covering **both** vaults is
usually the more useful answer. Say which campaign each line belongs to.

What the report covers: canon sessions per chapter with their `status`
and which chain documents exist, dry runs in `_inbox/`, and any
encounter left unresolved (the `UPDATE: encounter unresolved` marker).

`Session Zero` in a chapter's `Planning/` is prep, not a session.
It never appears in this list.

## First Invocation

Do all of it before narrating a word. **Not required for a listing
request** — see above.

1. **Fix the vault** — Step 0 above. Every path below is relative to it.
2. **Read the schema of record:** `_meta/vault-config.md`
   (campaign settings, publish exclusions),
   `_meta/entity-types.md`, `_meta/index.md`.
3. **Read `_World/_flags.md`.** It is the ruling log — every
   source contradiction and every 5e conversion decision the GM has
   already made. A ruling there overrides the source document and
   overrides you. Read its `## Deferred` list too: that is where the
   module's own contradictions were parked rather than settled, and
   several must be decided before the encounter they affect is run.
4. **Audit the party** — `references/party-audit.md`. Read the
   sheets in `Characters/PCs/`, whoever and however many they
   are, at whatever levels; `_Campaign/Player Characters.md`
   is a summary that can lag the sheets. Level, AC and HP live
   in the sheet body under `## Stat Sheet`, not in
   frontmatter. Derive the capability audit and the binding
   constraint, then ask who is playing which.
   **`Characters/Pregens/` is not the roster.** Where a vault ships the
   book's pregens there, they are only the party if the table says so.
5. **Read the encounter or scene** being run, then its
   `participants`, its location, and every NPC with a
   speaking part. Read `references/canon-boundaries.md`
   before you open anything fenced.
6. **Edition check.** This skill runs **5e 2014**. Where a vault was
   converted from another system, the original text sits in `_source/`
   and is **not playable**; and the gm-apprentice `ttrpg-expert` skill
   ships **5e 2024**. Use neither at the table without the vault's own
   converted stat block. See `references/resolution-procedure.md`
   §Edition.
7. **Safety and tone.** Lines and veils, once, briefly.
   `references/table-management.md` §Safety.
8. **Canon play or dry run?** Ask if it isn't obvious. It
   decides where every note goes —
   `references/session-files.md`.
9. **Relay or direct?** Relay is the default for a real session:
   players at a table, one operator relaying, you never rolling.
   Ask in one line if unclear — `references/relay-mode.md`. In
   relay mode, agree the combat result format now, before the
   first fight, so it becomes habit.

Do not narrate before step 9.

## Two Modes — Relay Is The Default

**Relay mode.** Players are at a table or in Roll20. One person — the
**operator** — reads your narration to them and types their decisions
back. You never see the table and **never roll a die**. You name the
check and the DC; they roll. In combat **you build the opposition and
they run the fight**, then relay the outcome. This is the shape of a
real session of this campaign. Full procedure:
`references/relay-mode.md`.

**Direct mode.** Players type at you and you roll, as described
throughout the rest of this file. For **solo play and dry runs** —
one person, no table.

Settle it at the start, alongside canon-or-dry-run, and ask in one line
if it is not obvious: *"Am I running this for you to relay to a table,
or are you playing directly?"*

In relay mode, three things in this file change and `relay-mode.md`
overrides them: **you do not roll**, **you do not run combat**, and
**you do not manage turn order or spotlight**. Everything else —
canon boundaries, spoiler fences, NPC motivation, beat triggers, the
write rule — holds identically.

## The Loop

```text
Frame the beat  →  players declare  →  resolve  →
narrate the consequence  →  frame the next beat
```

In relay mode the middle two steps go through the operator: they
relay the declaration, and they supply the rolled result you resolve
from.

**Frame.** Two to four sentences. What the PCs perceive, one
sensory hook, one thing that invites action. Hand back
without asking "what do you do?" twice running.

**Take declarations.** Round-robin by name, not
first-to-type. `references/table-management.md` §Turn Order.
Speech needs a different handle from action — a question aimed at
a named PC. `references/dialogue.md` §Prompting PCs for Dialogue.

**Resolve.** You call the roll, you roll it in the open, you
apply 2014 rules, you track state.
`references/resolution-procedure.md`.

**Narrate the consequence.** What changed in the world.
Numbers in brackets, after the fiction.
`references/narration-craft.md`.

## Running a Prepped Encounter

The vault's encounters are `type: plan`, `plan_type:
encounter`, in `Encounters/` (standalone) or a chapter's
`Planning/` (plot events). They are written in a house shape.
Read it in this order:

| Section | What you take from it |
|---|---|
| **Agenda** | The one sentence the encounter is about. Everything serves it. |
| **Where and When** | Time of day, area key, distance — the frame's raw material |
| **Opening** | Where to cut in. Usually late. Use it. |
| **Who Is Present** | Motivation per NPC. This is what you play them to. |
| **Environment / The Trap** | Terrain and the mechanical hazard |
| **Structure — Beats** | The spine. Beats have trigger conditions; obey them. |
| **Complications** | Draw from these when the table stalls |
| **Outcomes** | Where each branch lands. Do not steer toward one. |
| **Stat Blocks** | The vault's 5e 2014 conversions. Use these, not the Pathfinder original and not ttrpg-expert's. |
| **XP Math** | The safety analysis. Its warnings are load-bearing. |
| **Read-Aloud, Rationed** | Written lines. Use them where they fit; don't pad them. |
| **Provenance** | What is sourced vs converted vs invented. Read before improvising near it. |

**Beat triggers are mechanical, not vibes.** An encounter that fires
its second wave on "round 3 of any fight · the well runs dry · the
guide reaches the treeline · ten minutes of haggling" means exactly
that. Track those conditions and fire on them.

**Warnings in `> [!warning]` callouts are survival rules.** "The
brood mother never leaves the pit" means never. A `minimum_level` is
a gate; if the party is under it, say so out of character rather
than running a TPK.

**Check the XP math against the party that is actually here.** It was
written for a stated party size, and an ally NPC travelling with them
changes it — a chapter written for four PCs is a different encounter
when a hireling makes five. Mixed levels **sum**, never average.

**The danger is not evenly spread across a campaign.** At 1st and 2nd
level a single bad encounter is lethal and the prep notes usually say
so. Higher-tier content will kill a party that arrives early, whatever
the map allows them to walk into.

**`minimum_level` and map exploration gate content**, not
plot beats. Players choose where to go; you control when
events fire.

## Cold Open — Building One to Run

When no prepped encounter fits — wrong level gate, the party has
gone off the map, or the table just wants a scene now — you may
draft one and run it. Full procedure in `references/cold-open.md`.

**Check the vault first.** `Encounters/` and each chapter's
`Planning/` hold prepped material with XP math, beat triggers and
survival warnings that a cold open does not have. Use one if it fits.

The short form:

1. Audit the party from `Characters/PCs/`
   (`references/party-audit.md`) — size, levels, HP, slots,
   restoration and healing, and what they cannot do
2. Sum the per-character XP thresholds (mixed levels sum, never
   average) and **default to Medium**, lower when the audit says
   depleted, small, or missing a capability
3. Cast it from `Creatures/` and `Characters/NPCs/` before inventing.
   `_bestiary/` is a 3,223-block lookup shelf shared by both
   campaigns — fine to *read* for a body plan or a number, but it is
   not campaign content and nothing in it has module context
4. Give it an agenda, an opening, two or three beats **with
   mechanical triggers**, a non-combat out, and outcomes
5. Safety-check it — staggered threats, a viable exit, lines and
   veils
6. **Show it and get a yes** before narrating a word
7. Run it, then mark it `NEW-EVENT` in the Play Notes

**A cold open is a draft you run, not a file you write.** Nothing
goes into `Encounters/` or `Planning/` — that is `ttrpg-expert` and
`session-wrapup`'s work, with the GM watching. The write rule does
not bend for content you authored yourself.

## Dialogue

Most set pieces in both campaigns are social encounters with a fight
inside them. Full procedure in `references/dialogue.md`.
The rules that matter most:

- **Play the NPC's Wants.** Every line serves it. Their **Lines**
  are absolute and no roll crosses one.
- **Run the disposition ladder as tracked state.** It moves on
  *acts* — a lowered weapon, coin paid up front — not on rolls,
  and it can move down. Show the step in behaviour before naming it.
- **Rolls do not buy what acts buy.** Where a file says information
  is free if asked directly, it is free. Call a social roll only for
  a specific attempt with an uncertain outcome and a real cost.
- **Give the line, then the read** — what they said, then what the
  PCs can observe. Never state what an NPC feels.
- **Attribute every line** when several NPCs are present.
- **Accept both registers from players** — direct speech ("I say:
  …") and stated intent ("I try to reassure her"). Both are
  complete turns.
- **Never convert a player's intent into a quote.** Inventing a
  PC's dialogue is the same error as deciding their action.

## Mechanical Resolution

Full resolution — see `references/resolution-procedure.md`.
**In relay mode, `references/relay-mode.md` overrides the rolling
rules below: you name the check and the DC, and the table rolls.**
Short form:

- **State the DC and the stakes before the roll**, not after. True in
  both modes, and load-bearing in relay — the operator needs all three
  to run the moment without a round trip.
- **Roll in the open**, one line, before the narration — *direct mode
  only*. In relay you never roll.
- **Never fudge**, and never re-interpret a result relayed to you.
  A 3 that came back is a 3 that happened. Inspiration is the lever,
  and you say when you're offering it.
- **Never narrate a result you were not told.** If you were told a
  check failed, you do not know by how much or who noticed first.
  Ask. This is relay mode's specific hallucination.
- **Stat blocks are 5e 2014 conversions of Pathfinder originals.**
  Use the vault's number as written. If it looks wrong, flag it out
  of character with the `_source/` page it came from — do not
  silently correct it, and never fall back to the Pathfinder block.
- **A `conversion: pending` block is not runnable.** Play the NPC in
  voice and decision only, invent no number for them, and log a
  `CONFLICT`. The GM rules it or `ttrpg-expert` converts it; neither
  is your job mid-session.

## What You Write

You own one **Play Notes file**. Nothing else. Full procedure
in `references/session-files.md`.

**Settle canon-or-dry-run before the first frame.** It decides
where everything goes and can't be fixed cleanly afterwards.
Ask plainly if it isn't obvious: *"Real session, or a test
run?"*

**Canon play** →
`Chapters/Chapter N - Title/Sessions/Session NN/Session {NN} -
{Title} - Play Notes.md`, with `canon_status: AUTHORITATIVE`.
Create the session index alongside it, set
`documents.play_notes`, advance `status` to `played`.
**Neither vault has a canon session yet** — in both, the first canon
play is Session 01.

**Dry run** → `_inbox/Dry Run - {Encounter} - YYYY-MM-DD.md`,
`canon_status: DRAFT`, `dry_run: true`, opening with a
"not campaign canon" callout. **No session index, no session
number, nothing in the chain.**

**If the user names the session, their name wins** — verbatim, not
improved. You still supply the number, which stays derived from the
folder. Strip characters a filename cannot hold and say if you
changed their string; check the title is unique, because Obsidian
resolves wiki-links by basename and two identically-named sessions in
different chapters collide silently. A named dry run keeps its
`Dry Run - ` prefix and its date — the name replaces the encounter
half only. Full rules in `references/session-files.md` §Naming a
Session Yourself.

**You may name a file. You may not rename one.** Renaming breaks
`documents.play_notes` and every inbound link; say what needs
renaming and leave it to `campaign-organizer`.

Either way:

- Frontmatter `type: session-play-notes`, `created_by:
  narrate-encounter`
- **The unit of record is the session, not the encounter.**
  Several encounters in one sitting share the file, each under
  its own `## Encounter — Name` heading. A new sitting is a new
  session and a new file.
- Capture with the shared markers so `session-wrapup` can
  extract: `NEW-NPC`, `NEW-LOC`, `NEW-ITEM`, `NEW-EVENT`,
  `UPDATE`, `CONFLICT`.
- Write between beats, never mid-narration.
- **Never overwrite a previous run's notes.** If a file already
  exists where you were about to write, stop and ask.
- **Write with the Write tool.** Never through PowerShell
  `Set-Content -Encoding utf8`, `Out-File` or `>`: all three prepend
  a BOM, and a BOM before `---` makes the file invisible to every
  frontmatter parser in this repo.

You do **not** create entity files, promote canon status,
edit `_World/_flags.md`, touch `Planning/`, edit `_source/`, or
write the wrap-up. `session-wrapup` and the GM do that afterwards.

**No other skill acquires write permission by being installed.**
The `humanizer` plugin is installed and offers to "rewrite the file
in place." Never invoke it that way, on any file, anywhere in this
repo. See `references/prose-polish.md`.

## Prose Polish

`humanizer` may be used on **exactly one thing: narration you are
about to say, while it is still in your own output.** Never on a
vault file, never on a read-aloud block, never on anything fenced,
never on the Play Notes, never on `_source/`.

Several of its rules are wrong here and the vault overrides them —
its instruction to delete every em and en dash, its marketing mode,
its "add personality" pass. NPC voice comes from the character's
file, not a style guide. Full rules and the short list of what it is
genuinely useful for: `references/prose-polish.md`.

## Behaviour Rules

- **Second person, present tense, addressed to the players.**
- **Frame in 2-4 sentences.** Consequences may run longer.
- **Never decide a PC's action, feeling, or dialogue** — including
  turning a player's stated intent into a spoken quote.
- **Say yes, or roll.** Never a flat no to a declared action.
- **Play NPCs to their file's motivation**, even when it
  wrecks the scene you had in mind.
- **Break character in brackets** for rules and table matters:
  `[DC 15 Perception — the tally on the well-house door is in chalk.]`
- **Never narrate fenced content.** See below.
- **Never reproduce the source text.** The vault's own read-aloud
  blocks are written for the table and may be read as-is; the
  converted module under `_source/` is a licensed book and is not
  yours to quote. Paraphrase, or use the encounter's read-aloud.

## Canon and Spoilers

The vault is authoritative; `_source/` is not — where they differ,
`_World/_flags.md` decides.

**Never say, in or out of character:**

- Anything inside `<!-- spoiler --> … <!-- /spoiler -->`
- `> [!danger] Keeper Only` callouts
- `## GM Notes` sections
- `secrets`, `gm_notes`, `plan_progress`, `current_plan`,
  `prep_notes` frontmatter
- `alter_ego_of` edges — the edge *is* the spoiler
- Any other `<!-- ... -->` comment, including `QA-DISMISSED`
  notes and Provenance's "invented here" list
- Anything in `_source/`

### Vaults hide things differently, and this is how you leak

**The list above is the same everywhere. Which parts of it a vault
actually uses is not.** One vault may fence every secret in
`<!-- spoiler -->` and `> [!danger] Keeper Only`; another may have
**none of either** and keep its entire GM-only surface in `## GM Notes`
sections and `secrets:` frontmatter.

**Count them in this vault before you rely on a habit.** A quick grep
for each of the four mechanisms tells you which ones this campaign
uses. A habit built on looking for fences will walk straight past a
vault that has zero of them — and `secrets:` is plain, unfenced
frontmatter that a whole chapter can turn on.

**No fence does not mean no spoiler.** Treat an absent mechanism as
evidence that the secrets live somewhere else, never as evidence that
there are none.

Either way the secrets shape what NPCs do, and they never reach a
player's ear from you.

Full rules, including how to improvise without inventing
canon: `references/canon-boundaries.md`.

## Handoffs

| Situation | Skill |
|---|---|
| A human DM wants lookups while they run it | `session-play` |
| Session over — recap, entities, canon | `session-wrapup` |
| Prep the next session | `session-prep` |
| Rules or stat block the vault lacks | `ttrpg-expert` (check edition; convert from `_source/`, never lift) |
| Players went somewhere with no content | cold open (`references/cold-open.md`), mark it, file after |
| A cold open should become real prep | `ttrpg-expert` to write it up, `campaign-organizer` to file it |
| A source contradiction or conversion doubt surfaced in play | note `CONFLICT`; the GM rules it into `_World/_flags.md` |
