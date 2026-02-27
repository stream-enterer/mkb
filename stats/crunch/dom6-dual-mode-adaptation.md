# Adapting Frictional Elements for a Dual-Mode Game

Analysis of how the Dominions stat system (documented in `stat-system-topology.md`) maps
onto a game that swaps between DF-style fortress simulation and roguelike adventure mode,
with solutions for every point of friction. The constraint: preserve all functionality by
modifying the game's structure, not by cutting design elements.

The premise: one game, two modes. **Fortress mode** (top-down simulation, many entities,
indirect control) and **Adventure mode** (direct control of one character on a grid). All
systems must be mechanically identical across both modes — the mode swap changes the camera
and input scheme, not the rules.

---

## 1. Battle Buffs → Engagement-Scoped Buffs

**The problem:** Dom's Layer 3 buffs last "until the battle ends." A dual-mode game has no
discrete battles — combat is continuous and emergent.

**The solution: introduce "engagement" as a first-class runtime state on every entity.**

An entity enters the **engaged** state when any hostile enters its awareness radius (or it
is attacked). It leaves the engaged state when no hostile has been within awareness radius
for a cooldown window (say, 30 seconds of game-time / ~50 ticks at Dom's scale). This is
tracked per-entity, not globally.

Buff lifetimes then map as follows:

| Dom Lifetime | Dual-Mode Equivalent | Rationale |
|---|---|---|
| "Until battle ends" | Until engagement ends | Natural — you cast Quickness when fighting starts, it fades when fighting stops |
| "Until dispelled" | Until dispelled (no change) | Already works |
| "Until caster dies" | Until caster dies OR engagement ends, whichever first | Prevents orphaned buffs lingering forever |
| "While blessed" | While within N tiles of a shrine/priest AND engaged | Blessing becomes spatial, which is more interesting in both modes |

**Why this works in both modes:**
- **Fortress mode:** A siege triggers engagement for all defenders who see attackers. Buffs
  cast by your mages persist through the whole fight and expire naturally when the last
  goblin dies or flees and the cooldown elapses. If a second wave arrives before the cooldown
  ends, the engagement continues and existing buffs persist. This is identical to how Dom
  battles play out.
- **Adventure mode:** You enter a room full of enemies, your pre-cast buffs persist through
  the fight. You kill them all, walk down a hallway for 30 seconds, buffs fade. Enter the
  next room, you need to re-cast. This produces the same "per-encounter resource spend" that
  Dom's battle-scoped system creates — you can't just cast Quickness once and keep it all day.

**Edge case — the long running battle:** If combat drags on for a very long time (e.g., a
massive fortress siege), the engagement never ends and buffs persist. This is correct
behavior — Dom's long battles work the same way.

**Edge case — kiting:** A roguelike player could theoretically run away for 30 seconds to
shed enemy debuffs, then re-engage. This is fine — it costs real time (fatigue recovery is
also happening for enemies, reinforcements may arrive, hunger ticks). It's a tactical
choice, not an exploit.

---

## 2. The 32-Step Defensive Chain → Context-Scaled Steps

**The problem:** Several steps in the chain assume multi-unit engagement. Repel checks
weapon length against an approaching attacker (matters in formation, trivial 1v1).
Harassment applies a penalty for being surrounded (requires 2+ attackers). Shield parry's
3-outcome resolution assumes you might parry one attacker while another hits you.

**The solution: keep all 32 steps, but let each step's inputs scale naturally with the
number of engaged enemies.**

The steps aren't wrong for 1v1 — they're just sometimes degenerate (always pass, always
fail, or always produce the same branch). That's fine. The alternative (maintaining two
parallel resolution chains) is an engineering and balance nightmare. Instead, make the
*inputs* to each step reflect the spatial situation, and the chain works at any scale.

Specific adaptations:

**Repel (step ~2):** In Dom, repel triggers when an enemy closes into melee range and the
defender has a longer weapon. On a grid, this maps to: when an enemy moves from a
non-adjacent tile to an adjacent tile, the defender gets a free repel attack if their
weapon's reach exceeds 1. This works identically whether you're a lone adventurer with a
pike or a fortress guard in a hallway. In fortress mode with formations, multiple defenders
with long weapons each get their repel check — same as Dom.

**Awe (step ~3):** Awe checks the attacker's morale against the defender's awe value. This
is already a per-attacker check. In 1v1, the attacker rolls once. In a group fight, each
attacker rolls independently. No change needed — it scales naturally.

**Harassment / Surround Penalty (step ~10 modifier):** In Dom, being attacked by multiple
enemies applies a defense penalty. On a grid, define it as: **-1 defense per hostile entity
in an adjacent tile beyond the first, up to -5.** In adventure mode, you feel this when
surrounded in a corridor vs. fighting one-on-one. In fortress mode, it applies identically —
a dwarf surrounded by 4 goblins takes -3 defense. The grid makes the count trivial to
compute (just count occupied adjacent tiles with hostiles).

**Shield Parry (step ~10, 3-outcome):** The three outcomes are: clean miss (shield
irrelevant), parried by shield (shield absorbs, shield prot applies), hit past shield
(shield irrelevant). In 1v1, this collapses to a single parry check per attack, which is
fine — it's still meaningful because parried hits use shield protection while un-parried
hits use only body/helmet protection. In multi-attacker scenarios, the shield can only parry
attacks from the direction it's facing (the facing of the last enemy the defender targeted),
which creates a natural directionality. Enemies flanking you bypass the shield. This adds
tactical depth in adventure mode (positioning matters) and creates emergent behavior in
fortress mode (flanking squads are more effective).

**The general principle:** Every step in the chain takes inputs. Those inputs come from the
spatial state of the grid and the entities on it. In a 1v1, many inputs are 0 or 1, which
makes some steps trivially pass. In a 20v20, the same inputs produce rich interactions. The
chain itself never changes.

---

## 3. Squad/Commander Hierarchy → Universal Formation System

**The problem:** Roguelike characters are typically solo. The squad/commander system seems
to have no target.

**The solution: every entity in the game is always a member of exactly one squad, even if
it's a squad of one. The player character in adventure mode is a commander.**

This isn't a hack — it's how Dom already works (single-entity commanders are squads of
size 1). The system scales down to 1 gracefully if you let it.

**In fortress mode:** Works exactly like Dom. You assign military dwarves to squads with
commanders. The commander's leadership stat caps squad size. Commander morale bonus applies.
Kill the commander, the squad's morale breaks. This is literally the DF military system
with Dom's stat model underneath it.

**In adventure mode:** The player is a commander. Their leadership stat determines how many
companions/followers/summons they can maintain. Possible followers:

- Hired mercenaries (uses normal leadership)
- Raised undead (uses undead leadership — requires Death path)
- Summoned creatures (uses magic leadership — requires magic paths)
- Tamed animals (uses a subset of normal leadership)

A pure fighter with high leadership can bring a warband. A necromancer brings undead. A solo
sneaky character with 0 leadership has no followers and that's fine — their squad is just
themselves.

**The "kill the commander" vulnerability:** In fortress mode, enemy commanders are valid
targets — killing them routs their squad, same as Dom. In adventure mode, the *player* is
the commander. If they fall unconscious (fatigue 100), their followers lose the leadership
bonus and make immediate morale checks. Companions might flee. Undead might go berserk.
This creates a genuine "protect yourself" pressure for commander-style builds and is
mechanically identical to what happens in Dom.

**Commander scripts:** In Dom, commanders have 5 scripted action slots. In fortress mode,
you set these the same way (standing orders). In adventure mode, you execute them
manually — the 5 slots become your "prepared spells/tactics" that you can quick-access.
Companion commanders in adventure mode follow their scripts autonomously (you set them
before combat, then they execute), which preserves the indirect-control feel even in
direct-control mode.

---

## 4. Morale → Dual-Scale Morale (Individual + Group)

**The problem:** Dom's morale triggers are all group-level (20% casualties, squad < 5, 50%
army HP, 75% auto-rout). A solo roguelike character can't take 20% casualties.

**The solution: morale operates at two scales simultaneously. Every entity has individual
morale. Every squad has squad morale. Both matter, and they feed into each other.**

**Squad morale** (Dom's existing system, used when squad size > 1):
- Triggers on: 20% squad casualties, squad drops below 5, fear effects on squad members,
  commander death
- Check: `avg_unit_morale + commander_bonus + survivor_bonus + DRN vs 14 + DRN`
- Failure: entire squad routs (flee toward deployment edge / map exit)
- Auto-rout at 75% squad casualties

This works identically in fortress mode. In adventure mode, it applies to the player's
companion squad (if any) and to enemy groups.

**Individual morale** (new, used always):
- Triggers on: taking a hit that deals > 25% of max HP in one blow, witnessing an ally die
  within awareness radius, being alone against 3+ enemies, fear/horror effects, seeing
  something terrifying (undead, demons, for entities that care)
- Check: `individual_morale + DRN vs threat_rating + DRN`
- Failure tiers:
  - **Shaken:** -2 att, -2 def for 10 ticks (minor flinch)
  - **Frightened:** must spend next action moving away from threat source
  - **Panicked:** rout (flee toward nearest exit, dropping held items)
  - **Catatonic:** freeze in place, defense halved (like Dom's horror mark)

The tier reached depends on how badly the check was failed (margin of failure). This
replaces the binary rout/no-rout with a gradient.

**How they interact:**
- A squad morale failure forces individual checks at a penalty (-5). Most units will rout,
  but high-morale individuals might hold.
- Individual routs within a squad count as casualties for squad morale purposes (they're
  effectively gone).
- The player character in adventure mode uses individual morale only (squad of one). A
  player with 15 morale is nearly unbreakable. A player with 8 morale will flinch from big
  hits and panic if surrounded. **This is a stat that matters for character builds**, which
  preserves the dual-nature principle from stat-system-topology.md §7.

**Mindless/undead:** Mindless entities skip individual morale (they don't have it). Undead
are immune to fear triggers but still subject to squad morale via the "leaderless undead
dissolve" rule — if their commander dies, they don't rout, they go berserk for N rounds and
then crumble. This works in both modes and preserves Dom's undead-leadership dynamic.

---

## 5. Communion → Resonance Links (Generalized Cooperative Magic)

**The problem:** Communion assumes multiple friendly spellcasters cooperating in the same
battle. A solo roguelike character can't form a communion.

**The solution: generalize communion into "resonance links" — a system where magic-capable
entities can pool path levels through spatial proximity. Then make it available to players
through multiple channels.**

The core mechanic is unchanged from Dom: one entity is the **master** (receives boosted
path levels), others are **sources** (provide their paths, take fatigue penalties). The
boost formula stays: `+floor(log2(sources))` per path. The fatigue sharing stays: spell
fatigue is distributed across all linked sources.

**In fortress mode:** This is literally communion. Your mages form resonance links during
combat. You script a master and sources. Works identically to Dom.

**In adventure mode, sources can come from:**

1. **Companion mages.** If you have followers with magic paths (via leadership), they can
   serve as resonance sources. A necromancer lord with 3 skeleton mages as followers gets +1
   to Death path from the link (floor(log2(3)) = 1). This rewards the commander-mage build.

2. **Magical locations.** Certain tiles on the map (ley line nodes, altars, standing stones)
   act as passive resonance sources with fixed paths. A mage fighting on a ley line nexus
   gets a path boost. This gives terrain magical significance and rewards exploration — you
   want to fight the boss *here*, not *there*. In fortress mode, building your mage tower on
   a ley line gives your mages a permanent boost during sieges.

3. **Ritual preparation.** Before entering a dangerous area, a mage can spend time and gems
   to inscribe a resonance circle at a location. This acts as a persistent source (lasts
   until the engagement ends or the circle is destroyed). A solo mage can prepare 3 circles,
   then lure enemies into the room and fight at +1 path levels. This converts the "bring
   more mages" strategy into "spend more preparation time," which is a natural roguelike
   resource trade.

4. **Bound entities.** Summoned or bound magical creatures can serve as resonance sources if
   they have matching paths. A nature mage with summoned sprites gets nature path boosting.
   This is already implicit in Dom (summoned mages can join communions) but making it
   explicit and accessible through the summoning system gives solo casters a progression
   path toward communion-equivalent power.

**Why this preserves the design:** Communion's purpose in Dom is to let weaker mages pool
power to cast spells they individually can't. All four channels above achieve the same
thing — they give a caster access to higher-tier magic in exchange for something (leadership
investment, terrain control, preparation time, or summoning resources). The log2 scaling
means the power curve is identical. A solo mage with 4 resonance sources gets +2 path
levels, same as a Dom communion master with 4 slaves.

**The fatigue distribution** also works across all channels. Casting through a resonance
link splits fatigue across sources. Companion mages accumulate fatigue and eventually
collapse. Magical locations are inexhaustible (they're terrain). Ritual circles have a
fatigue pool that depletes. Bound entities take fatigue and may break free if exhausted.
Each source type has its own cost profile, but the underlying math is the same.

---

## Summary

| Friction Point | Dom Design | Dual-Mode Adaptation | What Changed |
|---|---|---|---|
| Buff lifetime | Battle-scoped | Engagement-scoped (awareness radius + cooldown) | Lifetime trigger, not the buff system |
| Defensive chain | 32 fixed steps | Same 32 steps, inputs derived from grid adjacency | Input sources, not the pipeline |
| Squad/Commander | Army hierarchy | Every entity in a squad (even solo = squad of 1) | Nothing — just allow squad size 1 |
| Morale | Group triggers only | Dual-scale: squad triggers + individual triggers | Added individual layer, kept group layer |
| Communion | Multiple friendly mages | Resonance links from companions, terrain, rituals, summons | Source types expanded, math identical |

The core principle in every case: **the combat math doesn't change; the context that feeds
inputs into the math gets richer.** The grid and the dual-mode structure actually give you
*more* input sources (adjacency, facing, terrain tiles, spatial proximity) than Dom's
abstract tactical layer provides, so the system gets more expressive, not less.

---

*Companion document to `stat-system-topology.md`. See that file for the full stat system
description that this document adapts.*
