# CLAUDE.md

Guidance for Claude Code when working **on this repository**. This is a
Claude Code plugin, not a campaign — for how to *use* the skills, see `README.md`.

## What this repo is

A plugin containing **three D&D 5e (2014) skills** that operate on an Obsidian
campaign vault. There is **no application code** — it is markdown instructions
that Claude loads and follows.

| Skill | Claude's role | Who decides the PCs' actions |
|---|---|---|
| `narrate-encounter` | Dungeon Master | **A human.** Always |
| `simulate-encounter` | Combat simulator | **Claude.** Nobody is playing |
| `dry-run-recap` | Writer, after the fact | Nobody — the dry run is over |

**The first two differ on who decides the PCs' actions, and that
distinction is the plugin's spine.** Every ambiguity about which of them
applies resolves to that one question. Do not blur it.

`dry-run-recap` is the odd one out: it plays nothing. It turns a finished
dry run's GM-only Play Notes into a player-facing page.

## Layout

```text
.claude-plugin/plugin.json      manifest — name, description, version
.claude-plugin/marketplace.json for installing this repo as a marketplace
skills/<name>/SKILL.md          the skill: frontmatter + main instructions
skills/<name>/references/*.md   loaded on demand by the SKILL.md that names them
```

## Invariants — do not break these

**YOU MUST keep the skills campaign-neutral.** They were extracted from one
specific campaign and generalised. Do not reintroduce a campaign's proper
nouns, file counts, or party composition. Worked examples use invented
placeholders (`Varn` the guide, `Kess`, `Alder`, the Cracked Tankard) and
should stay that way.

**IMPORTANT: `simulate-encounter` writes exactly one file** — a report in
`<vault>/_QA/Simulations/`. It must never edit a PC sheet, a creature file,
`_World/_flags.md`, a session file, or anything else. That guarantee is the
reason the skill exists separately from `narrate-encounter`; if an edit would
weaken it, the edit is wrong.

**IMPORTANT: `dry-run-recap` writes exactly one file** — a recap in
`<vault>/Dry Runs/` — and nothing in it may be something no player heard
or saw at the table. That rule is the skill. It must never edit the Play
Notes, a sheet, the publish manifest or the vault's config, and it must
never promote a recap past `DRAFT`: that would make a test run canon.

**The edition is 5e 2014, never 2024.** The differences that matter are listed
in `skills/simulate-encounter/references/combat-engine.md` §2014 vs 2024.
gm-apprentice's `ttrpg-expert` ships 2024 — treat it as a different system.

**`narrate-encounter` must never decide a PC's actions.** See
`references/table-management.md` §Absent Players. Requests to simulate both
sides belong to the other skill.

**Do not hard-code vault contents.** Coverage varies wildly between vaults —
some give every creature a `## Tactics` section, some give it to a handful.
Write "check the vault" rather than a number.

**Campaign specifics belong in the vault's `_meta/table-notes.md`, not in
the skills.** That optional file is how a campaign supplies its own
register, audit questions, clocks, safety list, spoiler surfaces and
creature-file layout; format in
`skills/narrate-encounter/references/table-notes.md`. When a user wants
the skills to know something about *their* campaign, the answer is that
file. **Its precedence is fixed**: it replaces a generic sketch, and it
never outranks `_World/_flags.md`, `vault-config.md`, an encounter file or
a stat block.

## Editing a skill

**The `description:` in SKILL.md frontmatter is the routing surface.** It is
the only part Claude sees before deciding whether to load the skill, so it
carries the trigger phrases and the explicit NOT-for list. Changing behaviour
usually means changing the description too.

**Keep SKILL.md as the spine and push detail into `references/`.** The main
file should be readable start to finish; a reference is loaded only when the
SKILL.md points at it for a specific job.

**Prose conventions:** wrap around 72 columns, bold the load-bearing clause
rather than whole paragraphs, and prefer a concrete worked example to an
abstract rule. State *why* a rule exists where the reason is not obvious —
these files are read by someone deciding whether to follow them.

## Testing a change

There is no test suite. Verify by running it:

```bash
claude                          # from a directory containing a campaign vault
/skills                         # confirm all three skills are listed
```

Then invoke the skill and check the behaviour you changed. For
`simulate-encounter`, **verify the non-canon guarantee held**:

```bash
git status --porcelain <vault>/Characters   # must be empty
```

A simulation that modified a character sheet is a release blocker, not a bug.

## Dependencies

**Soft dependency on `gm-apprentice`** for the vault schema these skills read
(`_meta/`, `_Campaign/`, `Characters/PCs/`, `Creatures/`, frontmatter
conventions, the session document chain). The skills do not call its code and
work against any vault with that shape, but the folder names come from it.

**No runtime dependencies.** No Python, no npm, no build step.

## What not to do

- **Do not add a dice-rolling script** without being asked. The current design
  rolls in-model by deliberate choice; the tradeoff (not reproducible, but no
  tooling and handles any homebrew) is recorded in the README.
- **Do not fold `dry-run-recap` back into `narrate-encounter`.** It was split
  out so that `narrate-encounter` keeps its one-file rule and so a recap can
  be asked for directly, on any old run.
- **Do not merge the two table skills.** They differ on exactly one thing and that
  thing is the point.
- **Do not add campaign content** — encounters, monsters, settings. This is a
  plugin, not a module.
