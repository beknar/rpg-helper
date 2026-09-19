# Session Files

Where play records go, and how to keep two plays from landing on top
of each other. Read before writing the first note of a session.

## The Unit of Record Is the Session

Not the encounter. `_meta/entity-types.md` treats standalone
encounters as droppable into any area, any session, at the DM's
discretion — an encounter is something that happens **inside** a
session, and the vault has no separate record type for one.

So: **one Play Notes file per session**, however many encounters that
session contains.

## Canon Play or Dry Run

Settle this **before the first frame**, in one question if it isn't
obvious from what the user asked. It decides where everything goes,
and it cannot be fixed cleanly afterwards.

| | Canon play | Dry run |
|---|---|---|
| What it is | A real session of the campaign | Testing an encounter, trying a party, seeing how a scene runs |
| Goes to | The session chain | `_inbox/` |
| Enters canon | Yes, via `session-wrapup` | No |
| `campaign-qa` sees it | As a session needing a wrap-up | As unprocessed inbox material |

Ask plainly: *"Is this a real session, or a test run?"* A GM playing
their own pregens against their own encounter is usually testing. A
group sitting down to play is usually not.

## Canon Play — The Session Chain

Path, per `shared/session-document-chain.md` and the vault's
`_About - Sessions.md`:

```text
Chapters/Chapter N - Title/Sessions/Session NN/
├── Session NN - Title.md                 (index)
├── Session NN - Title - Plan.md          (session-prep's, may not exist)
├── Session NN - Title - Play Notes.md    (yours)
└── Chapter_CC_Session_NN_Wrap_Up.md      (session-wrapup's)
```

**Which session is this?**

1. List the chapter's `Sessions/` folder. The next number follows the
   highest that exists. As of the last vault update no session exists
   anywhere, so the first canon play is **Session 01**.
2. **Which chapter?** The one whose level band holds the party. The
   chapter files carry the band as `minimum_level`. One campaign may run its
   first chapter from 1st, its second from 2nd and its
   third chapter from 4th; another opens at 7th and climbs from there, the
   Temple-City from about 11th and the Citadel above that.
   A standalone encounter from `Encounters/` does not
   change this — it has no chapter of its own, so it is played inside
   whichever session it was dropped into.
3. **Title it after play, not before** — *unless the user names it.*
   Left to you: zero-padded and evocative, `Session 01 - Iron
   Bits.md`, never `Session 01 - Sep 12 2026.md`. If you must create
   the index before you know how the session went, use a provisional
   title and rename at the end. If the user supplies a title, see
   **Naming a Session Yourself** below — theirs wins, always.
4. **If any of this is ambiguous, ask.** A misfiled session is worse
   than a ten-second question.

## Naming a Session Yourself

The user may name a session at invocation, and their name wins over
anything you would have chosen.

*"Run the camp as a session called First Night at the camp"*
*"Name this one 'Tuesday group'"*
*"Dry run, call it usurer-v2"*

**Rules:**

1. **Their title, verbatim** — do not improve it, expand it, or make
   it more evocative. `Session 03 - Tuesday group.md` is correct if
   that is what they said.
2. **You still supply the number.** Numbering is structural and stays
   derived from the folder (see above). The user names the *title*
   half. If they explicitly give a number too — *"make this Session
   07"* — use it, but say plainly what you are skipping if it leaves
   a gap in the chain.
3. **Strip what a filename cannot hold:** `< > : " / \ | ? *`, and
   any leading or trailing whitespace or dot. Tell the user if you
   changed their string, and what to.
4. **A title must be unique in the vault.** Obsidian resolves
   wiki-links by basename, so two `Session 02 - The Well.md` files
   in different chapters silently collide. Check before writing; if
   it is taken, say so and ask for another.
5. **Renaming later is a GM job, not yours.** You may write a session
   under a name; you may not move or rename an existing one. That
   breaks `documents.play_notes` and every inbound wiki-link. Say
   what needs renaming and let `campaign-organizer` do it.

**Named dry runs.** The date-stamped default,
`Dry Run - {Encounter Name} - YYYY-MM-DD.md`, is what you use when
nobody says otherwise. A supplied name replaces the *encounter* half
only — the `Dry Run - ` prefix and the date stay, because they are
what keeps the file identifiable and collision-free:

```text
Dry Run - usurer-v2 - 2026-09-12.md
```

Never drop the prefix. A dry run that does not announce itself in its
own filename is the failure mode this whole split exists to prevent.

## Listing What Exists

The user may ask what has been played without wanting to play
anything: *"what sessions are there"*, *"show me the dry runs"*,
*"where did we leave off"*, *"list sessions"*.

**This is a read-only report. Narrate nothing, write nothing, and do
not run the First Invocation sequence** — no party audit, no safety
tools, no canon-or-dry-run question. Answer and stop.

**Gather:**

1. **Canon sessions** — every `Chapters/*/Sessions/` subfolder.
   Ignore `_About - Sessions.md`; it is a signpost, not a session.
2. **Dry runs** — `_inbox/*.md` with `dry_run: true`, plus anything
   in `_inbox/_processed/`, which is a dry run already ingested.
3. **Status of each** from the session index's `status` field, and
   which of the four chain documents exist — index, Plan, Play Notes,
   Wrap-Up. A session with Play Notes and no Wrap-Up is **awaiting
   wrap-up**, which is normal, not broken.
4. **Unresolved encounters.** Grep the Play Notes for
   `UPDATE: encounter unresolved` — `session-files.md` tells you to
   write that marker when a sitting ends mid-encounter, and it is the
   single most useful thing in this report.

**Report shape** — chapter, session, title, status, and what is
outstanding:

```text
Chapter 1 — The waste
  Session 01 - Iron Bits             played · awaiting wrap-up
    unresolved: two ghoul wolves still standing, Varn at Wary
  Session 02 - The Open Waste        planned · Plan only, not played

Dry runs (not canon)
  Dry Run - The Sip of Blood - 2026-09-10
```

**Say when there is nothing.** "No canon sessions in any chapter; one
dry run" is a complete and useful answer. Do not pad it, and do not
offer to start one unless asked.

**Never infer a session from a file that is not one.** `Session Zero`
in a chapter's `Planning/` is prep with a confusing name — it is a
`plan`, it has no session number, and it does not belong in this
list. Neither does an `Encounters/` file, however often it has been
run.

**Frontmatter you write:**

```yaml
---
type: session-play-notes
session: "[[Session NN - Title]]"
chapter: "[[Chapter N - Title]]"
campaign: "[[Campaign Overview]]"
canon_status: AUTHORITATIVE
created_by: narrate-encounter
lastUpdated: "YYYY-MM-DD"
tags: []
---
```

**Never leave an orphan.** Create the session index alongside the
Play Notes, set `documents.play_notes`, and advance `status` to
`played`. `campaign-qa` validates the chain and flags play notes
without a wrap-up — which is correct and expected until
`session-wrapup` runs, but a Play Notes file with no index at all is
just broken.

## Several Encounters in One Session

They share the file. Give each a heading so `session-wrapup` and you
can tell them apart:

```markdown
## Encounter — The Sip of Blood

NEW-NPC: the one-eyed teamster at the end of the bar — ...

## Encounter — Cold open: the dry wadi

NEW-LOC: the wadi, half a day north of the camp on the old road ...
```

Append in play order. Do not start a second file because a second
encounter began.

## When It's a New Session Instead

A new sitting is a new session and a new file — even if it continues
the same encounter. The test is whether the table got up, not whether
the fiction resolved.

If a session ends mid-encounter, say so in the notes (`UPDATE:
encounter unresolved — two ghoul wolves still standing, Varn at
Wary`) so the next session can pick it up.

## Dry Runs — `_inbox/`

A test play writes **nothing** into `Chapters/`, `Encounters/`, or
any entity folder. It writes one file:

```text
_inbox/Dry Run - {Encounter Name} - YYYY-MM-DD.md
```

```yaml
---
type: session-play-notes
campaign: "[[Campaign Overview]]"
canon_status: DRAFT
created_by: narrate-encounter
dry_run: true
lastUpdated: "YYYY-MM-DD"
tags:
  - "dry-run"
---
```

Open the body with a callout so it can never be mistaken for a
session record:

```markdown
> [!warning] Dry run — not campaign canon
> Test play of [[The Sip of Blood]] on YYYY-MM-DD. No session number,
> no chapter, not in the session chain. Nothing here is canon.
> If this should count, `vault-ingest` promotes it.
```

**No session index, no `status` change, no session number.** The
whole point is that it stays outside the chain.

Content is otherwise the same as canon play notes — the same markers,
the same substance — because a dry run that turns out to have mattered
should be promotable without rewriting it.

**Say at the end** what a dry run produced that might be worth
keeping: an NPC who worked, a beat that didn't, a stat block that
felt wrong for its CR. That is usually the reason the GM ran it.

**Then offer a player recap, once, in one line** — *"Want a
player-facing recap of this for the site?"* The Play Notes can never
be published; the recap can. A yes hands off to the `dry-run-recap`
skill, which writes it.

## Repeat Runs

Running the same encounter twice is normal — a test, then the real
thing; or the same set piece dropped for a different party.

- **Dry runs never collide.** The date is in the filename; a second
  test of the same encounter on the same day gets a `-2` suffix.
- **Canon plays never collide either**, because they are different
  sessions with different numbers.
- **Never overwrite a previous run's notes.** If a file exists at the
  path you were about to write, stop and ask rather than appending to
  something from a different play.

## What You Still Don't Write

Everything in `canon-boundaries.md` holds regardless of which mode
you are in. Play Notes — canon or `_inbox/` — remain the only file
this skill creates. No entity files, no canon promotion, no edits to
`Encounters/`, `Planning/`, sheets, `_source/`, or `_World/_flags.md`.
