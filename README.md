# rpg-helper

Claude at the table. Two **D&D 5e (2014)** skills that read an Obsidian
campaign vault and either run the game or fight it out.

| Skill | What it does | Who plays the PCs |
|---|---|---|
| **`narrate-encounter`** | Claude is the **DM**. Frames scenes, voices NPCs, calls and resolves rolls, tracks combat and canon | **You do** |
| **`simulate-encounter`** | Claude is a **combat simulator**. Fights a party against monsters round by round and says who wins | **Nobody.** Claude plays both sides |

**The whole distinction is who decides what the PCs do.** If a human is
declaring actions, you want `narrate-encounter`. If you want an answer rather
than a game, you want `simulate-encounter`.

---

## Requirements

- **Claude Code.**
- **An Obsidian campaign vault** laid out to the
  [gm-apprentice](https://github.com/AntTheLimey/gm-apprentice) schema —
  `_meta/`, `_Campaign/`, `Characters/PCs/`, `Creatures/`, `Chapters/`, and
  frontmatter with `type:` and `canon_status:`.
- **Stat blocks already converted to 5e 2014.** These skills *run* a campaign;
  they do not convert one.

Installing gm-apprentice itself is recommended but not required — the skills
read the vault directly and call none of its code.

---

## Install

### From a marketplace (recommended)

```text
/plugin marketplace add beknar/rpg-helper
/plugin install rpg-helper@rpg-helper
```

To install from a local clone instead, point the marketplace at the directory:

```text
/plugin marketplace add /e/code/rpg-helper
/plugin install rpg-helper@rpg-helper
```

### Verify

```text
/skills
```

Both `narrate-encounter` and `simulate-encounter` should be listed. If they
are not, the plugin did not load — check `/plugin` for its status.

### Without installing (local development)

Link the skills folder into a project so Claude picks it up directly:

```bash
# macOS / Linux
ln -s /e/code/rpg-helper/skills .claude/skills

# Windows
mklink /J .claude\skills E:\code\rpg-helper\skills
```

Useful while editing the skills, since changes take effect with no reinstall.

---

## Using `narrate-encounter`

### Calling it

Just ask. The skill triggers on natural phrasing:

> *"Be our DM."*
> *"Run the Barrow of the Forgotten Chief for us."*
> *"You DM, I'll play the cleric."*
> *"We need a fight — make us an encounter and run it."*
> *"Take us into the keep."*

Or invoke it explicitly:

```text
/narrate-encounter
```

### What happens

1. **It picks the vault.** One vault, it uses it. Several, it resolves from
   what you named and asks only if genuinely ambiguous.
2. **It asks the mode** — *relay* or *direct* (below).
3. **It asks canon or dry run**, because that decides where the notes go.
4. **It audits the party**, states the binding constraint, asks about lines
   and veils once, and starts.

### The two modes

| | **Relay** (default for real sessions) | **Direct** |
|---|---|---|
| Where the players are | At a table, or in a VTT | Typing at Claude |
| Who rolls | **They do.** Claude names the check and DC | **Claude does**, in the open |
| Who runs combat | They do; Claude builds the opposition | Claude |
| Good for | A real session with an operator relaying | Solo play, dry runs |

Say *"I'll relay for the table"* or *"we're on Roll20"* for relay; *"I'm
playing directly"* for direct.

### What it writes

- **Canon play** → a Play Notes file in the session chain under
  `Chapters/<chapter>/Sessions/`.
- **Dry run** → `_inbox/`, where nothing treats it as canon.

- **A player recap of a dry run**, only when you ask → `Dry Runs/`.
  The dry run's own notes are written for the GM and full of things
  players must not see: stat blocks, DCs, what the monster does if
  they don't take the bait. The recap is a second file written for
  players from the start, for showing a feature off on a published
  campaign site. **Anything no player heard or saw at the table is
  left out.** It stays marked as a dry run and not canon.

  Say *"write a player recap"* or *"recap this for the site"*. It
  doesn't publish anything itself: it tells you what stands between
  the recap and your site, usually a setting that drops drafts.

**It never writes entity files.** Improvised NPCs and locations are marked
`NEW-NPC` / `NEW-LOC` in the Play Notes for you to promote deliberately, with
`session-wrapup`.

---

## Using `simulate-encounter`

### Calling it

> *"Who would win — the party against four ghouls?"*
> *"Is this encounter survivable at 3rd level?"*
> *"Can Azren, Cevis and Darla beat the Acolyte of Orcus?"*
> *"Balance-check this fight, 5 runs."*

Or:

```text
/simulate-encounter
```

### What happens

It loads both sides from the vault, echoes the roster for you to correct, sets
the terms, then fights it out — rolling every attack, save and death save in
the open, and playing both sides as well as their **Intelligence and
equipment** allow.

**Defaults**, all overridable: 10 rounds · 60 ft apart · open flat lit terrain
· no surprise · full hit points and resources · 1 trial.

### The verdict

Not just who won:

- Who won, and **by kill or on points** at the round limit
- Rounds elapsed and casualties on each side
- **What it cost the winners** — hit points, slots, per-rest features. For
  encounter design this is the useful number
- **The turning point** — the one roll the fight hinged on
- **What would change it** — one or two concrete levers

### What it writes

One file: `<vault>/_QA/Simulations/YYYY-MM-DD - <A> vs <B>.md`, carrying the
terms, rosters, the full round-by-round log with every die roll, the verdict
and the caveats.

**Nothing else, ever.** A PC killed in a simulation is untouched on their
sheet — no hit points, slots, conditions, status or XP change anywhere.

---

## What they can't do

Being explicit, because some of these are deliberate refusals rather than
missing features.

### Both skills

- **They don't build a party.** An empty `Characters/PCs/` stops them; that is
  a Session 0 job.
- **They don't convert stat blocks.** If a creature has only a pre-conversion
  block (Pathfinder, 3.5, whatever the vault came from), they say so and stop
  rather than inventing numbers mid-scene.
- **They don't run 5e 2024**, or any other system. If the vault records a
  different system they stop and say so.
- **They don't invent canon.** Improvisation is expected; writing it into
  entity files is not.
- **They aren't a rules lookup.** For that, use gm-apprentice's `ttrpg-expert`
  or `session-play`.

### `narrate-encounter` specifically

- **It will not decide a PC's actions.** A character whose player is absent
  travels along and does nothing; Claude never plays their choices. *This is
  the single hard rule of the skill* — and the reason `simulate-encounter`
  exists.
- **In relay mode it does not roll dice** and does not run combat.
- **It does not read your players' minds about safety.** It asks for lines and
  veils once and takes the answers at face value.

### `simulate-encounter` specifically

- **It is not a statistical engine.** Dice are rolled in-model, so `trials: N`
  is honest in **single digits**. Reports say "won 4 of 5", never "80%". Ask
  for hundreds of runs and it will tell you why it can't and offer the
  deterministic reading instead.
- **A single run is a sample of one.** Every report's Caveats say whether one
  roll decided the fight — read that before designing around the verdict.
- **It can't tell you what your table will do.** It plays both sides near
  optimally, gated by Intelligence. Real players are worse, and its reports
  say so.

---

## Design notes

**Dice are rolled in-model.** The tradeoff is deliberate: no tooling to
install, and it handles any homebrew spell or feature you throw at it — but a
run is not reproducible. Every roll is therefore shown in the log, because the
log is the only thing that makes an in-model simulation checkable.

**Tactical quality is gated by Intelligence.** A zombie (INT 3) attacks the
nearest thing; a lich (INT 20) manages action economy, saves its Legendary
Resistance, and targets concentration. A simulation where every monster plays
like a tactician is not a better simulation — it is a broken one.

**The vault's own `## Tactics` section outranks Claude's optimisation.** Where
the module says what a monster does, that is the author's intent and it wins.

---

## Repository

```text
.claude-plugin/     manifest and marketplace descriptor
skills/             the two skills, each SKILL.md + references/
CLAUDE.md           guidance for working on this plugin
```

See `CLAUDE.md` before editing a skill — it records the invariants, including
the ones that look like details and are not.

---

## Licence

**MIT** — see [`LICENSE`](LICENSE). Use it, fork it, sell it; keep the
copyright notice.

The skills describe D&D 5e (2014) mechanics in their own words and vendor no
third-party text. If you extend them with content from the **SRD 5.1**, note
that it is CC BY 4.0 and requires attribution.

*Dungeons & Dragons and D&D are trademarks of Wizards of the Coast LLC. This
project is unofficial, and is not affiliated with or endorsed by Wizards of
the Coast.*
