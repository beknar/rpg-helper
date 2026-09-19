# Table Notes — Format

`_meta/table-notes.md` is an **optional** file a vault carries to tell
this plugin's skills what its campaign is like. The skills are written
for any campaign; this file is where one campaign says what "low
tier", "the signature threat" and "the settlement" mean for it.

Read by `narrate-encounter` (all sections), `simulate-encounter`
(§Creatures) and `dry-run-recap` (§Spoilers). **Every section is
optional.** Write the ones that differ from the generic references and
leave the rest out.

## Precedence

**It replaces the generic sketch it covers**, and nothing else.

| Wins over table notes | Loses to table notes |
|---|---|
| `_World/_flags.md` | The generic register sketches in `narration-craft.md` |
| `_meta/vault-config.md` | The generic audit questions in `party-audit.md` |
| An encounter file, a stat block, a chapter file | The generic clocks in `resolution-procedure.md` |
| The Session Zero safety list, where one exists | The generic safety candidates in `table-management.md` |

It is **guidance on how to run the campaign, not a record of what is
true in it.** A fact belongs in an entity file; a ruling belongs in
`_flags.md`. If a table note and a vault file disagree, the vault file
is right and the note is stale.

## Frontmatter

```yaml
---
type: meta
purpose: table-notes
lastUpdated: "YYYY-MM-DD"
---
```

Use whatever type the vault's `_meta/` files already use. It is
GM-only and should never be published; `_meta/` is excluded from
publishing by default.

## Sections

```markdown
# Table Notes — {Campaign}

## Register
The campaign's voice: scale, stakes, what the ordinary looks like, one
or two concrete tone rules. Named example NPCs to model voice on.

## Party Audit
The capability questions that decide this campaign's fights, and the
binding constraint to expect at its opening level.

## Clocks
What to track here: light, rest rules, travel checks, weather,
supplies, condition clocks the local threat imposes.

## Safety
Where the vault's own lines-and-veils list lives, plus anything it
does not spell out — a monster ability, a keyed room.

## Spoilers
Which GM-only mechanisms this vault uses, with counts if you have
them, and a worked example of a secret that is easy to walk past.

## Creatures
Block format (fenced or markdown), how many carry `## Tactics`, where
a shared shelf lives, and any entries with damaged or missing numbers.

## Danger
Where the campaign is lethal, and what a party that arrives early
walks into.
```

**Keep it short.** A page or two. It is read at the start of every
session, alongside the schema and the ruling log.

**Keep it current.** Counts drift as a vault grows. Date the file, and
prefer "check X" to a number where the number will not stay true.
