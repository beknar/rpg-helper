# The Combat Engine — D&D 5e (2014)

The rules this simulation runs on. **2014, not 2024.** The vault is a
2014 campaign and `ttrpg-expert` ships 2024, so where they differ, 2014
wins. The differences that bite most often are noted below.

## The Round

```text
Initiative  →  turns in descending order  →  end of round  →  repeat
```

**Initiative.** d20 + Dexterity modifier, once per combatant, or once
per group of identical creatures. Ties go to the higher Dexterity, then
to the PCs. Roll it once and keep the order for the whole fight.

**A turn is:** movement up to Speed (divisible around the action), one
**action**, one **bonus action** if something grants it, and any number
of free object interactions (one per turn without an action). A
**reaction** is once per round and refreshes at the start of your turn.

**End of round:** tick down durations, roll ongoing damage, resolve
regeneration, check concentration that lapsed, and note any effect that
ends "at the start of its next turn".

## Actions Available

Attack · Cast a Spell · Dash · Disengage · Dodge · Help · Hide · Ready ·
Search · Use an Object · plus anything the stat block grants (Multiattack,
breath weapons, Frightful Presence).

**Multiattack is an action, not a bonus.** A creature with Multiattack
makes exactly the attacks listed, no more.

**Dodge is a real answer** and both sides may use it — attacks against
the dodger have disadvantage until its next turn. A wounded PC buying a
round for the cleric is legitimate play, not a wasted turn.

**Two-weapon fighting** costs the bonus action and adds no ability
modifier to the off-hand damage unless a feature says otherwise.

## Attack Rolls

```text
d20 + ability modifier + proficiency (if proficient) + magic bonus
   vs the target's AC
```

- **Natural 20 is a critical hit** — roll the damage **dice** twice, add
  modifiers once. Not "double the total".
- **Natural 1 always misses**, whatever the bonus.
- **Advantage / disadvantage**: roll 2d20 and take the higher / lower.
  They do **not** stack — any number of each cancels to a single normal
  roll. This is one of the most commonly mis-simulated rules in 5e.
- **Cover**: half cover +2 AC, three-quarters +5, total cover cannot be
  targeted.
- **Ranged attacks in melee** have disadvantage when a hostile creature
  is within 5 feet.

## Saving Throws

```text
d20 + ability modifier + proficiency (if proficient)  vs the DC
```

**Spell save DC** = 8 + proficiency + spellcasting ability modifier, and
it is on the PC sheet — use the sheet's number, not a recomputation.

There are **no critical successes or failures on saving throws** in
2014. A natural 20 on a save is just a 20.

**Legendary Resistance**, where a block has it, is spent to turn a
failed save into a success — a finite and precious resource, usually 3
per day. A monster that burns all three in round one has nothing left
for the save that matters.

## Damage, Resistance and Death

**Resistance halves, vulnerability doubles, immunity zeroes.** Apply
resistance **after** all additions; halving rounds down. Resistance and
vulnerability to the same type cancel, and multiple instances of
resistance do not stack further.

**Non-magical weapon resistance is enormous at low tiers** — a party
with no magic weapons against a creature resistant to non-magical
bludgeoning, piercing and slashing is doing half damage with everything.
Check who actually has a magic weapon before assuming the party's
damage output.

**At 0 hit points:**

- A **PC** falls unconscious and makes a **death saving throw** at the
  start of each of its turns: DC 10, three successes stabilise, three
  failures kill, a natural 20 restores 1 hit point, a natural 1 counts
  as two failures. **Damage taken while at 0 is an automatic failure**,
  and two if the attack was a critical hit or the attacker was within
  5 feet.
- **Massive damage** kills outright: leftover damage after reaching 0
  that equals or exceeds the character's hit point maximum.
- A **monster** simply dies unless the block or the vault says
  otherwise.

**Healing from 0** brings the creature to the healed amount and ends
unconsciousness. Death saves reset.

## Conditions That Decide Fights

Model these exactly; they are where simulations most often go wrong.

| Condition | What actually happens |
|---|---|
| **Prone** | Melee attacks against it have advantage, ranged have disadvantage; standing costs half movement |
| **Restrained** | Speed 0, attacks against it have advantage, its attacks have disadvantage, disadvantage on Dex saves |
| **Grappled** | Speed 0; no other penalty by itself |
| **Paralyzed / Stunned** | Incapacitated, no actions, auto-fails Str and Dex saves, attacks against have advantage — and **paralyzed makes any hit from within 5 feet a critical** |
| **Frightened** | Disadvantage on attacks and ability checks while it can see the source; cannot move closer |
| **Charmed** | Cannot attack the charmer; charmer has advantage on social checks |
| **Incapacitated** | No actions and no reactions |
| **Blinded** | Auto-fails sight checks; its attacks have disadvantage, attacks against it have advantage |
| **Unconscious** | Incapacitated, prone, drops what it holds, auto-fails Str and Dex saves, hits within 5 feet are critical |

**Exhaustion is cumulative and hard to shift** — level 1 disadvantage on
ability checks, 2 speed halved, 3 disadvantage on attacks and saves,
4 hit point maximum halved, 5 speed 0, 6 death.

## Spellcasting

**Slots are the resource that decides long fights.** Track them by level
and spend them honestly. Cantrips are free and scale with character
level, not slot level.

**Concentration** — one spell at a time. It ends when the caster casts
another concentration spell, is incapacitated, or dies. **On taking
damage**, a Constitution saving throw at **DC 10 or half the damage
taken, whichever is higher**. Breaking a concentration spell is often
worth more than the damage that breaks it, and both sides should know
that.

**Upcasting** — a spell cast from a higher slot uses the higher effect.
A caster choosing between one big spell and two small ones is a real
decision; make it deliberately.

**Components and range** — a spell with a range of Self does not reach
across the battlefield, and a caster who cannot see the target cannot
target it.

## 2014 vs 2024 — Where It Matters

Do not let 2024 habits leak in:

| | **2014 (use this)** | 2024 |
|---|---|---|
| Surprise | A **surprised creature** cannot act or react on its first turn | Surprise gives disadvantage on initiative |
| Hiding | No fixed rule for hiding in the open | Tightened |
| Exhaustion | Six discrete effects, as above | Flat −N to d20 rolls |
| Two-weapon fighting | Costs the bonus action | Changed |
| Ranger, healing, crits | 2014 values | Reworked |

**Surprise is the biggest one.** In 2014 a surprised combatant loses its
entire first turn, which in an ambush is frequently the whole fight.

## House Rules and Vault Rulings

**`_World/_flags.md` is the ruling log and it outranks the core rules.**
Where a vault keeps one it carries the campaign's parameters, its
mechanics rulings, and often a record of encounters whose difficulty
moved during conversion from another system.

**Read it before simulating anything.** A converted campaign's fights
were frequently built on mechanics that do not survive the edition
change — damage reduction, level drain, ability damage — and the ruling
log is where that is written down. **Simulating such a fight without it
produces a confident wrong answer**, which is the worst thing this skill
can produce.

**Where the log says a question is still open**, say so rather than
picking an answer. Campaigns commonly defer things like play above 20th
level; a simulation that silently resolves an open ruling is inventing
campaign policy.

## What Is Out of Scope

Say so plainly rather than inventing a result:

- **Morale.** 5e has no morale rules. Creatures fight until the block or
  the vault's `## Tactics` says they flee.
- **The environment beyond the stated terms.** If the user did not
  specify terrain, the default is open and flat, and you do not invent a
  chasm that decides the fight.
- **Long-term consequences.** Disease, curses and level drain are
  applied for the duration of the fight and then the simulation ends.
  Nothing persists, because nothing here is canon.
