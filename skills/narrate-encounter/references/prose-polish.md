# Prose Polish — Using `humanizer` at the Table

The `humanizer` plugin is installed at user scope and loads in this
repo. It is a marketing-copy editor. This file is the only sanction
for using it here, and it is deliberately narrow.

## The One Permitted Use

**Narration text you are about to say, while it is still in your own
output, before the players read it.**

That is the whole permission. Prose you are composing — a frame, a
consequence, an NPC's line — may be passed through humanizer's
judgement to strip AI tells before you deliver it.

## Forbidden Absolutely

| | Why |
|---|---|
| **File mode** | Humanizer's SKILL.md offers to "rewrite the file in place." Never invoke it that way in this repo, on any file, in any folder. Not the vault, not `skills/`, not `_source/`, not the README. |
| **Any vault file as input** | Entity notes, encounters, `_World/`, handouts, sheets, Play Notes. Not to read, not to "clean up," not to preview. |
| **`_source/`** | Machine conversion of a licensed book. It is not prose to improve; it is evidence. Regenerate it, never edit it. |
| **Read-aloud blocks** | The `Read-Aloud, Rationed` sections in encounters are *authored prose*. Someone chose those words. Deliver them as written or don't use them. |
| **Anything fenced** | Nothing inside `<!-- spoiler -->`, `[!danger] Keeper Only`, `## GM Notes`, or the `secrets` / `gm_notes` / `plan_progress` fields goes through any transformation. Keeper content is not narration input. |
| **Play Notes** | The one file you write is a record, not prose. Markers like `NEW-NPC:` are structured data `session-wrapup` parses. Leave them alone. |

The write rule in `canon-boundaries.md` is unchanged and outranks this
file: **one Play Notes file, nothing else.** Humanizer does not create
an exception, and a skill that offers to write files does not acquire
permission by being installed.

## Where Humanizer Is Wrong For This Vault

Humanizer is tuned for blog posts and landing pages. Several of its
rules are actively wrong here. When they conflict, **the vault wins.**

**Em and en dashes.** Humanizer §14 says to scan the final text and
replace every `—` and `–`. The vault's authored prose uses them as
house voice, and the GM's previous vault carried nearly two thousand.
Ignore §14 completely.

**Marketing mode.** Never applies. There is no CTA, no keyword to rank
for, no conversion. If humanizer starts detecting a landing page, you
have fed it the wrong thing.

**"Add personality."** NPC voice comes from the character's file —
their Wants, their Lines, their manner. It does not come from a style
guide. A polish pass must not make the Usurer chattier or Father
Death warmer. `dialogue.md` governs voice; humanizer does not.

**Rhetorical devices.** Rule of three, deliberate repetition, and a
sentence that lands hard are *craft* in narration, not tells.
`narration-craft.md` decides register here. Do not flatten a good
line because a pattern catalog lists the shape.

## What It Is Actually Good For

The genuinely useful subset, applied to your own draft narration:

- Filler phrases and throat-clearing before the sentence starts working
- Vague attribution — *"some say"*, *"it is believed"* — where the
  vault has a specific source
- Inflated significance: a barrow door is not *a testament to*
  anything
- Superficial `-ing` analysis clauses bolted onto the end of a sentence
- Uniform sentence length across a whole paragraph

That list is short on purpose. If a polish pass is changing more than
the texture of a sentence, stop and keep your draft.

## Practical Rule

You do not need to invoke the skill to benefit from it. Knowing the
tells is enough — write the frame cleanly the first time. **Reach for
humanizer only when you have written something and can hear that it
sounds generated**, and then only against the text in your own
message.

If a player asks you to humanize *their* prose, that is a separate
task outside this skill. Hand off, and do not do it mid-scene.
