# Canon Boundaries

The most important file in this skill. Read before loading any scene.

Every other gm-apprentice skill talks to the GM. This one talks to
players, while reading the GM's private notes in the same turn. That
is the whole risk surface.

## Two Rules That Look Contradictory

The vault says **never invent canon**. Running a table requires
constant improvisation. Both hold, because they govern different
things:

> **Improvise freely in the fiction. Write nothing into canon.**

At the table you may name a bystander, describe the weather, decide
what's on a shelf, and answer a question the module never anticipated.
In the vault you may write to exactly one file — the session's Play
Notes — and every improvisation goes there marked, for a human to
promote or discard later.

The vault's rule exists because this campaign is a conversion of
someone else's 747-page module, where a quiet invention becomes
indistinguishable from source material, and a quiet 5e number becomes
indistinguishable from a deliberate conversion. Play Notes are the
firewall: they are a record of what happened at a table, not a claim
about the world.

## The Three Layers

| Layer | Source | You may |
|---|---|---|
| **Player-facing** | Entity files, `Handouts/`, played sessions, `_Campaign/` overviews | Read and narrate |
| **Keeper-only** | The fences below, and all of `_source/` | Read, play to, never state |
| **Improvised** | Yours, this session | Invent, keep consistent, mark in Play Notes |

## The Fences

This vault's spoiler convention, verbatim from `CLAUDE.md`. Anything
matching is Keeper-only:

- `<!-- spoiler --> … <!-- /spoiler -->` blocks
- `> [!danger] Keeper Only` callouts
- `## GM Notes` sections (excluded by `_meta/vault-config.md`)
- Frontmatter `secrets`, `gm_notes`, `plan_progress`,
  `current_plan`, `prep_notes`
- `alter_ego_of` relationship edges — **the existence of the edge is
  the spoiler**, so never recite an NPC's connections wholesale
- Every other `<!-- ... -->` comment: `QA-DISMISSED` notes, edition
  notes, authoring history
- `_meta/`, `_Templates/`, `_inbox/`, `_QA/`, `_World/_flags.md`
- **All of `_source/` and `_attachments/maps/`** — the converted
  module and its page renders. Keyed maps show players what they
  have not found.
- Anything in `Planning/` — it is prep, `source: prep`, and gated

**Frontmatter is not covered by a body fence.** A fenced `## GM Notes`
section protects nothing in the file's fields. Before reciting any
entity's details to players, check its frontmatter separately.

## The Secrets

The module is built on things the camp knows and will not say, and
things nobody alive knows. The vault lists them, fenced, in
`_Campaign/Campaign Overview.md` and in each chapter file. Read that
list before running anything; do not carry a version of it in your
head from a previous session.

The shape of them, without the content: **the camp's helpful faces
are not all what they claim**, and a guide who offers the safest
route may be walking the party into someone's larder; **the war is
not over** for everything that fought in it; and **the disciples of
the villain withdrew for a reason** the players will spend three
books earning.

It is legitimate and necessary for this to shape what NPCs do. An NPC
who knows acts like someone who knows. What they do not do is explain,
and what you do not do is narrate the mechanism.

## Not-Yet-Known vs Never-Told

- **Not yet known** — discoverable this session. Place the clue, let
  them find it, then narrate it freely once found.
- **Never told** — structural: why the encounter is built this way,
  what `minimum_level` gates it, what the Provenance section says was
  converted or invented, what's coming in the Citadel. This never
  surfaces at all, in character or out.

The Provenance sections are a specific trap. Where an encounter file
lists a name as **invented here** — a guide the module never named, a
bystander the vault added so a scene had someone to talk to — that
person is simply real to the players. Never narrate a character as
fabricated, provisional, or "not in the book."

Conversion is a second trap. An NPC's 5e stat block was derived from
a Pathfinder one and the frontmatter says so. To the players there is
no Pathfinder block. Never mention the original CR, the original
numbers, or the fact of conversion in play.

## Improvising Under Canon

- **Check before you invent.** Search the vault for the thing first —
  a name, a location, a faction. `_meta/index.md` carries the live
  entity count; the thing may exist. If it is not in the vault but is
  in `_source/`, it is not yours to improvise either: say out of
  character that the module covers it and it has not been converted,
  and offer the GM the choice.
- **`canon_status: DRAFT` is still binding at the table.** Everything
  in this vault is DRAFT because nothing has been played, not because
  it's up for grabs. Follow it. If play contradicts it, mark
  `CONFLICT` and let the GM rule.
- **`_World/_flags.md` outranks the source and outranks you.** Every
  ruling there was made deliberately. Do not reopen one mid-scene.
- **Consistency within the session is binding.** Once you name the
  livery hand, that is his name for the rest of the night. Write it
  to Play Notes the moment it outlives its beat.
- **Level gates are canon.** Content gates by party level and map
  exploration. If a 7th-level party walks toward the temple-city's
  gate and the tar dragon on it, that is a fiction problem with a
  fiction answer — the waste, the distance, the guide who
  refuses — not a silent downgrade of the threat and not a rail.

## What You Never Write

You own the Play Notes file. That is the entire list.

- **No entity files.** An improvised NPC gets `NEW-NPC` in the notes,
  not a file in `Characters/NPCs/`. `session-wrapup` creates entities,
  from templates, with the GM watching.
- **No canon promotion.** DRAFT → AUTHORITATIVE is the GM's alone.
- **No edits to `_World/_flags.md`.** Rulings are the GM's. You surface
  the contradiction; you do not resolve it.
- **No edits to `Planning/` or `Encounters/`.** Prep is archived by
  play, not rewritten by it.
- **No edits to `_source/`.** It is machine output from a licensed
  book. Fix the converter, never the text.
- **No stat block corrections.** Conversion decisions are recorded
  in `_World/_flags.md`. Flag, don't fix.
- **No edits to existing entity files** — not even a status the
  session plainly changed. Mark `UPDATE`; wrap-up applies it.

The reason is structural, not tidy. A skill improvising in the
players' service must not be able to write to the record the GM
trusts. Everything it invents passes a human before it becomes canon.

## Conflicts

When play contradicts the vault:

1. **Play wins in the moment.** Don't stop the game.
2. **Mark it:** `CONFLICT: <what the vault says> vs <what happened>`.
3. **Raise it at session end**, in the closing summary — not
   mid-scene, and not as a correction to the players.

## Source Material

The converted module lives in `_source/`, and it is GM-only in
every sense: it is a commercial book, it is Pathfinder, and it keys
every secret to an area number. Vault read-aloud blocks are written
content and may be read as-is; everything else you say is your own
prose. Where `_source/` and the vault disagree, the vault wins; where
the vault is silent, say so and offer options rather than filling the
gap from the book as though it were settled.
