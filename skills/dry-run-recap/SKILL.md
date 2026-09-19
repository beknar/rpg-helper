---
name: dry-run-recap
description: "Use when the user wants a dry run turned into something players can read — a player-facing recap for a published campaign site, to show a feature off or to record a feature test. A dry run's Play Notes (written by narrate-encounter to _inbox/) are a GM document full of stat blocks, DCs, triggers and markers that players must never see; this skill writes a SEPARATE recap, for players from the start, with everything no player heard or saw left out. Writes exactly one file, to the vault's Dry Runs/ folder, still marked as a dry run and not canon. Works on a run still in this conversation (best, because the live narration is available) or on any earlier dry run from its Play Notes. Trigger on 'write a player recap', 'recap this dry run', 'recap this for the site', 'make a publishable version of the dry run', 'write up the dry run for players', 'showcase this run', 'turn the dry run into a site page'. NOT for canon sessions (session-wrapup handles those), for running the table (narrate-encounter), for publishing or building the site itself (publish-site), or for a simulation report (simulate-encounter)."
---

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

## Step 0 — Which Vault, Which Run

**Settle the vault first**, exactly as `narrate-encounter` does: a
vault is a directory with `_meta/` or `_Campaign/` beside content
folders. One vault, use it. Several, resolve from what the user named
and ask in one line only if it is genuinely ambiguous. A project's
own `CLAUDE.md` may name its vaults; it outranks your guess.
**Never read across two vaults.**

**Then settle the run.** Dry runs live in `_inbox/` as
`Dry Run - {Name} - YYYY-MM-DD.md`, with `dry_run: true`.

| What you find | What to do |
|---|---|
| A dry run was played **in this conversation** | Recap that one |
| The user named one | Find it in `_inbox/`, or `_inbox/_processed/` |
| Several candidates, nothing named | List them in one message and ask |
| The named file is **not** `dry_run: true` | Stop. This skill is for dry runs only |

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
| Narration the table heard, including read-aloud blocks | Anything told **only to the operator** |
| What each PC did, as the player declared it | Stat blocks, AC, HP, attack bonuses — unless the players were told the number |
| Rolls the **table** made, and their outcome | DCs, unless they were announced to the players |
| What the PCs learned, and who learned it | Triggers, retreat conditions, tactics, "if they do X, Y happens" |
| Outcomes the party can see: who was hurt, what fell, what they found, XP | Creatures or branches that never appeared, and what would have happened |
| The end state as the party knows it | `NEW-*`, `UPDATE` and `CONFLICT` markers, and notes on gaps in the plan |
| | Improvised calls flagged "my call, not the file's" |
| | Anything from `secrets`, `gm_notes`, `## GM Notes`, a spoiler fence, a `Keeper Only` callout, or `_source/` |

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

1. **The narration given during this conversation**, if the run is
   still in context. It is the best material there is: it was written
   for the table, it is Claude's own text, and it was already filtered
   for players when it was said.
2. **The run's Play Notes**, for the sequence of events and the
   outcomes. **Read them as a GM document**: every line is operator
   material until the rule above clears it.
3. **The PC sheets**, for the one-line party list only — name, class,
   level.
4. **Nothing else.** Not the encounter file, not the creature file, not
   `_source/`. The recap tells what happened at the table, and the
   vault's prep is not that. **Never quote the module's own text**;
   it is licensed content even when the vault is private.

**Recapping from the notes alone** is fine, but the narration is gone.
Write it fresh from the notes, and say so in the Provenance section:
*"Rebuilt from the Play Notes; the table's narration was not
preserved."*

## What You Write

**Exactly one file, and nothing else.**

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
- **Never edit the Play Notes**, a PC sheet, an entity file, the
  publish manifest or the vault's config. The recap reads them; it
  changes none of them.
- **Write with the Write tool.** Never PowerShell
  `Set-Content -Encoding utf8`, `Out-File` or `>`: all three prepend a
  BOM, and a BOM before `---` hides the frontmatter from every parser.

Frontmatter, body layout, the showcase section and a worked example:
`references/recap-format.md`. **Read it before drafting.**

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

## Publishing — What to Tell the User

**You do not publish.** Tell the user what stands between the recap
and the site, because the defaults will usually stop it:

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

Say this in a few lines at the end, then hand off to `publish-site`
for the rest.

## Handoffs

| Situation | Skill |
|---|---|
| Play the dry run in the first place | `narrate-encounter` |
| A canon session needs writing up | `session-wrapup` |
| Build or update the site | `publish-site` |
| The dry run should count as canon after all | `vault-ingest` promotes the Play Notes, not the recap |
