# Unit Stat System Topology

A structural map of the Dominions unit stat system, intended as a blueprint for
implementing a similar system in another game. Focuses on the *shape* of the system —
what categories of stats exist, how they relate, how they combine, and where they flow
into combat resolution — rather than exact numeric values.

---

## 1. Stat Layers

The stat system has four distinct layers, each with different lifetimes and sources.

### Layer 1: Base Stats (immutable template)

Defined per unit type at data-load time. Never change during a game.

```
Unit Template
├── Physical: hp, strength, attack, defense, precision, protection, morale, size
├── Meta: magic_resistance, action_points, encumbrance, eyes
├── Magic Paths: fire, air, water, earth, astral, death, nature, blood, holy (0-N each)
├── Resistances
│   ├── Elemental: fire_res, cold_res, shock_res, poison_res (signed int, can be negative = vulnerability)
│   └── Physical: slash_res, pierce_res, blunt_res (boolean flags)
├── Type Flags: undead, demon, inanimate, mindless, magic_being, sacred, ethereal, flying, ...
├── Combat Abilities: berserk, awe, trample, fear, regeneration, reinvigoration, darkvision, ...
├── Body Type: enum (humanoid, quadruped, snake, bird, ...) → determines hit location table + equipment slots
└── Leadership: normal, undead, magic (separate pools)
```

**Key design insight:** Stats are either *scaled ints* (contribute to rolls) or *boolean
flags* (gate mechanics on/off). There is no middle ground — a stat either participates in
arithmetic or it doesn't.

### Layer 2: Equipment Modifiers (session-persistent)

Applied when a unit equips weapons/armor/items. Persist across battles.

```
Equipment Effects
├── Flat bonuses to base stats: +att, +def, +str, +mr, +morale, ...
├── Flat bonuses to resistances: +fire_res, +cold_res, ...
├── Path level boosts: +1 fire, +2 astral, ...
├── Flag grants: ethereal, flying, regeneration, berserk, ...
├── Protection (armor): per-slot values (head, body), stacks with natural prot via diminishing returns
├── Encumbrance (armor): additive penalty
└── Defense penalty (armor/shield): additive penalty from weight
```

**Stacking rules:**
- Duplicate items of the same type do NOT stack resistance bonuses.
- Different items DO stack.
- All flat stat bonuses stack additively.
- Protection from natural sources and armor sources combine with diminishing returns:
  `total_prot = nat + armor - (nat * armor / 40)`

### Layer 3: Buff/Debuff Modifiers (battle-persistent)

Applied by spells, bless effects, battle enchantments. Last for the battle or until dispelled.

```
Battle Modifiers
├── Flat stat changes: Quickness (+2 att, +2 def), bless bonuses, ...
├── Multiplicative timing: Quickness (0.5x action_time), Slow (2.0x), Frozen (2.0x)
├── Resistance buffs: +5 or +10 to elemental resistances (same-tier buffs don't stack)
├── Path level boosts: from spells (Summon Earthpower), communion, gems
├── Flag grants: mistform, mossbody, luck, twist_fate, mirror_image, fire_shield, ...
├── Protection buffs: Barkskin, Ironskin, etc. (modify natural protection)
└── Debuffs: cursed (+15% affliction chance), slimed (-2 att/-2 def, 2x action_time), ...
```

**Stacking rules for resistance buffs:** Same-magnitude buffs from spells do not stack.
Different magnitudes do stack (+5 and +10 = +15). This is a deliberate design to prevent
trivial immunity stacking while still rewarding diversity.

### Layer 4: Transient Combat State (tick-level)

Changes every tick or round. Resets between battles.

```
Transient State
├── current_hp (decremented by damage)
├── fatigue (incremented by actions, decremented by recovery)
├── position (x, y on grid)
├── delay (tick countdown to next action)
├── afflictions (bitmask, mostly permanent within battle)
├── status flags: is_berserking, is_routing, is_unconscious
├── poison_pool (accumulates, drains over time)
├── entanglement state: webbed, netted, entangled, encased, paralyzed, ...
└── targeting state: current_action, target_unit, squad_id
```

---

## 2. Stat Flow Diagram

How stats actually participate in combat resolution. Each box is a resolution
step; arrows show which stats feed into it.

```
                         ┌─────────────────────────┐
                         │    ATTACK INITIATION     │
                         │  delay reaches 0         │
                         │  ← action_points         │
                         │  ← action_time modifiers │
                         │  ← Quickness/Slow/Frozen │
                         └────────────┬─────────────┘
                                      │
                    ┌─────────────────┬┴──────────────────┐
                    ▼                 ▼                    ▼
           ┌──────────────┐  ┌───────────────┐  ┌──────────────────┐
           │ MELEE ATTACK │  │ RANGED ATTACK │  │   SPELL CAST     │
           │              │  │               │  │                  │
           │ ← unit.att   │  │ ← unit.prec   │  │ ← path_levels   │
           │ ← wpn.att    │  │ ← range        │  │ ← fatigue_cost  │
           │ ← fatigue    │  │ ← fatigue      │  │ ← encumbrance   │
           │   (-1/20fat) │  │ ← wind/rain    │  │ ← gem inventory │
           │ ← berserk    │  └───────┬───────┘  │ ← interrupt chk  │
           │ ← terrain    │          │           │   (dmg/maxhp+25%)│
           │ ← darkness   │          │           └────────┬─────────┘
           │ ← env powers │          │                    │
           └──────┬───────┘          │                    │
                  │                  │                    │
                  ▼                  ▼                    ▼
         ┌─────────────────────────────────────────────────────┐
         │              32-STEP DEFENSIVE CHAIN                │
         │                                                     │
         │  Pre-roll effects (steps 1-9):                      │
         │    repel ← weapon.length, morale                    │
         │    awe ← awe_value vs attacker.morale               │
         │    petrify/curse/vine/slime/horror mark              │
         │                                                     │
         │  Hit roll (step 10):                                │
         │    att + mods + DRN  vs  def + mods + DRN           │
         │    ← fatigue penalties (att: -1/20, def: -1/10)     │
         │    ← shield parry (3-outcome: clean/parried/miss)   │
         │    ← harassment penalty (surrounded)                │
         │    Defender wins ties.                               │
         │                                                     │
         │  Damage roll (step 12):                             │
         │    str + wpn.dmg + DRN  vs  prot + DRN             │
         │    ← hit location (head/body/arms/legs)             │
         │    ← critical hit check (fatigue ≥ 50 → easier)     │
         │    ← damage type modifiers (pierce 0.8x, AP 0.5x)  │
         │    ← charge bonus (first hit only)                  │
         │                                                     │
         │  Post-damage filters (steps 13-32):                 │
         │    physical_res → halve typed physical dmg           │
         │    protective_force → 50% add to prot               │
         │    mirror_image → absorb hit                        │
         │    ethereal → 75% negate non-magic                  │
         │    luck → 75% negate killing blow                   │
         │    mistform → reduce by 25 (min 1)                  │
         │    mossbody → 75% reduce by 15                      │
         │    twist_fate → negate once                         │
         │    retaliatory effects: fire_shield, poison barbs   │
         └─────────────────────────┬───────────────────────────┘
                                   │
                                   ▼
         ┌─────────────────────────────────────────────────────┐
         │              DAMAGE APPLICATION                     │
         │                                                     │
         │  hp -= final_damage                                 │
         │  fatigue += encumbrance (attacker action cost)       │
         │                                                     │
         │  Elemental resistance: flat reduction before prot    │
         │    fire_res, cold_res, shock_res, poison_res        │
         │    (doubles vs fatigue-type elemental damage)        │
         │                                                     │
         │  Magic resistance (binary pass/fail):               │
         │    11 + pen + path/2 + DRN  vs  MR + path/2 + DRN  │
         │    Used by: weapon mrnegates, spell effects         │
         │                                                     │
         │  Affliction check:                                  │
         │    chance = damage / max(current_hp, max_hp) %      │
         │    +15% if cursed                                    │
         │    reduced by regeneration, affliction_resistance    │
         │    result → permanent stat penalties (see §3)        │
         └─────────────────────────┬───────────────────────────┘
                                   │
                    ┌──────────────┴──────────────┐
                    ▼                             ▼
         ┌──────────────────┐           ┌──────────────────┐
         │  FATIGUE SPIRAL  │           │  MORALE CHECK    │
         │                  │           │                  │
         │  -1 def / 10 fat │           │  avg_morale +    │
         │  -1 att / 20 fat │           │  survivor_bonus  │
         │  ≥50: crit vuln  │           │  + DRN           │
         │  ≥100: unconscious│          │  vs 14 + DRN     │
         │  ≥200: hp damage │           │                  │
         │                  │           │  triggers:       │
         │  recovery:       │           │  - 20%+ casualties│
         │  1+reinvig/round │           │  - squad < 5     │
         │  5+reinvig if 100+│          │  - fear effects  │
         └──────────────────┘           │  - 50% army HP   │
                                        │  auto-rout: 75%  │
                                        └──────────────────┘
```

---

## 3. Stat Modification Taxonomy

Every stat modification in the system falls into one of these categories:

| Category | Examples | Stacking | Lifetime |
|----------|----------|----------|----------|
| **Base** | `#hp 15`, `#att 12` | N/A (template) | Permanent |
| **Equipment flat** | Sword +2 att, Armor +18 prot | Additive | While equipped |
| **Equipment flag** | Ring grants ethereal | OR | While equipped |
| **Bless** | F3: +2 att, W3: +2 def | Additive | While blessed in battle |
| **Spell buff (flat)** | Quickness: +2 att, +2 def | Additive | Until dispelled/caster dies |
| **Spell buff (mult)** | Quickness: 0.5x action_time | Multiplicative | Until dispelled/caster dies |
| **Spell resist buff** | Protection from Fire: +10 FR | Additive per tier, same-tier doesn't stack | Until dispelled |
| **Environmental** | Darkness: -6 att/-6 def | Additive | While condition active |
| **Terrain** | Underwater: -3 att/-3 def | Additive | While on terrain |
| **Scale power** | Chaos Power: +N per scale | Additive, context-dependent | While in province |
| **Fatigue penalty** | -1 def/10 fat, -1 att/20 fat | Derived from transient state | Tick-level |
| **Affliction** | Lost Eye: -2 att, -2 def, -3 prec | Additive | Permanent until healed |
| **Status condition** | Webbed: def × 0.25 | Multiplicative override | Until escaped |
| **Experience** | +1 att, +1 def, +1 MR per level | Additive | Permanent |

### Stat Resolution Order

When computing the effective value of a stat for a roll:

```
effective_stat =
    base_stat
  + equipment_bonuses          (flat, additive)
  + bless_bonuses              (flat, additive)
  + spell_buff_bonuses         (flat, additive)
  + experience_bonuses         (+1 per level)
  + environmental_modifiers    (terrain, darkness, scales)
  + affliction_penalties       (permanent debuffs)
  - fatigue_penalty            (derived: fat/10 for def, fat/20 for att)
  then apply multiplicative overrides (webbed: ×0.25, unconscious: =0)
```

---

## 4. The Three Resistance Systems

Dominions has three completely separate damage mitigation systems. They are checked
at different points in the resolution chain and work differently.

### 4a. Protection (armor + natural)

- **What it stops:** All physical and most magical damage
- **How:** Opposed roll: `str + wpn + DRN vs prot + DRN`. Excess = HP damage
- **Diminishing returns:** Natural + Armor - (Natural × Armor / 40)
- **Bypass mechanisms:** Armor Piercing (50% prot), Armor Negating (ignore prot), Pierce (80% prot), Critical Hit (75% prot)
- **Per-location:** Head uses helmet prot, body uses body armor prot. Shield adds on parried hits

### 4b. Elemental Resistance

- **What it stops:** Elemental-typed damage (fire, cold, shock, poison)
- **How:** Flat subtraction from damage after DRN, before prot multipliers
- **Doubles** against fatigue-type elemental damage (heat/chill auras)
- **Vulnerabilities** are negative resistance; double the relevant damage up to the vulnerability value
- **No roll involved** — purely deterministic subtraction

### 4c. Magic Resistance

- **What it stops:** Spell effects tagged `mrnegates` or `mrnegateseasily`
- **How:** Binary pass/fail roll: `11 + penetration + path/2 + DRN vs MR + path/2 + DRN`
- **Does not reduce damage** — either the entire effect applies or it doesn't
- **Bypassed by:** Mindless immunity to `#mind` tagged effects (different check)

### 4d. Physical Resistance (boolean flags)

- **What it stops:** Slash, pierce, or blunt typed damage
- **How:** Halves relevant damage *after* the protection roll
- **Boolean per type** — you either have it or you don't, no scaling

---

## 5. Afflictions as Permanent Stat Damage

Afflictions are the long-term stat degradation system. They function as a *permanent
modifier layer* that accumulates over the course of combat (and persists on the
strategic map).

```
Affliction System
├── Trigger: damage / max_hp = % chance per hit
├── Location-based: head → eye/mind afflictions, chest → wound/disease, legs → limp, arms → weakness
├── Severity tiers: minor (50% weight) vs major (25% weight, italic in table)
└── Effects: flat stat penalties applied to Layer 1 stats

Example affliction stat penalties:
  Lost Eye:     att -2, def -2, prec -3  (stackable per eye)
  Blindness:    att -9, def -9, prec -9  (replaces lost eyes)
  Chest Wound:  enc +5, str -1
  Limp:         combat_speed -50%, att -1, def -1
  Crippled:     combat_speed capped at 2, att -4, def -4
  Weakened:     str -4
  Mute:         leadership -75%, all magic paths -50%
  Feeblemind:   att -1, def -1, prec -1, MR -5, ldr -75%, all magic paths = 0
  Disease:      prevents healing, ongoing HP loss, spawns more afflictions
```

**Design insight:** Afflictions create a *stat entropy ratchet*. Units degrade over
time in ways that make them progressively weaker. Combined with fatigue (temporary
degradation) and morale (flight threshold), this ensures battles always resolve —
there is no equilibrium state.

---

## 6. Fatigue as the Universal Entropy Mechanic

Fatigue is the most important *derived stat* in the system. It touches everything:

```
Fatigue Sources                    Fatigue Sinks
─────────────────                  ──────────────
Melee attack: +encumbrance         Natural: -1/round (-5 if unconscious)
Spell cast: +spell_cost/path_adj   Reinvigoration: -reinvig/round
           +base_enc +2×armor_enc  Life drain: -2×damage_dealt
Being hit by fatigue damage        Relief spell
Berserk: +(berserk+1)/2 per round
Environmental: heat/cold without res

              Fatigue Effects
              ───────────────
              0-49:   -1 def per 10, -1 att per 20
              50-99:  above + critical hit vulnerability
              100:    unconscious (def=0, cannot act)
              200+:   direct HP damage (1 per 50 excess)
```

**Design insight:** Fatigue creates a *tempo economy*. Every action (attacking,
casting, moving in some cases) has a fatigue cost. Heavy armor increases cost.
Reinvigoration offsets cost. The "fatigue neutral" breakpoint (enc = reinvig) is a
critical unit design threshold. Units above it slowly degrade; units below it can
fight indefinitely.

---

## 7. The Dual-Nature of Stats

Most stats serve double duty — they are both *combat roll inputs* and *strategic
identity markers*. This is a core design principle worth preserving:

| Stat | Combat Role | Identity Role |
|------|-------------|---------------|
| **HP** | Damage pool | Durability tier (chaff vs elite vs monster) |
| **Strength** | Damage bonus | Can they hurt armored things? |
| **Attack** | Hit chance | Offensive skill |
| **Defense** | Dodge chance | Defensive skill |
| **Protection** | Damage reduction | Armor class |
| **Morale** | Rout threshold | Reliability (elite vs conscript) |
| **MR** | Spell immunity | Magic tier |
| **Size** | Hit location, trample eligibility | Physical category |
| **Encumbrance** | Fatigue cost per action | Weight class / tempo cost |
| **Action Points** | Movement speed + action rate | Speed class |
| **Magic Paths** | Spell access + fatigue reduction | Caster power tier |

---

## 8. Equipment Slot System

Equipment is constrained by body type and slot count:

```
Body Type → Hit Location Table + Equipment Slots
─────────────────────────────────────────────────
humanoid:         2 hands, 1 head, 1 body, 0 mount
mountedhumanoid:  2 hands, 1 head, 1 body, 1 mount (barding slot)
quadruped:        0 hands, 1 head, 1 body, 0 mount
snake/naga:       2 hands (naga) / 0 (snake), 1 head, 1 body
bird:             0 hands, 1 head, 1 body
misc:             varies

Armor Types:
  shield (type 4):  occupies 1 hand, grants parry + protection
  body (type 5):    occupies body slot, grants protection + encumbrance
  helmet (type 6):  occupies head slot, grants head protection + encumbrance
  barding (type 9): occupies mount slot, grants protection + encumbrance
```

**Armor contributes:** protection (per-location), defense penalty, encumbrance.
**Weapons contribute:** damage, attack bonus/penalty, defense bonus/penalty, length, special flags.
**Shields contribute:** parry value, protection (on parried hits only), defense penalty, potential destruction.

---

## 9. Weapon Stat Decomposition

Weapons are the most complex equipment type. Their stats decompose into several
independent systems:

```
Weapon
├── Accuracy layer
│   ├── attack_bonus: flat add to hit roll
│   ├── defense_bonus: flat add to wielder's defense
│   └── length: affects repel, multi-weapon penalty
│
├── Damage layer
│   ├── base_damage: int
│   ├── str_contribution: full (1.0×) / half (0.5×) / third (0.33×) / none (0×)
│   ├── twohanded: 1.25× strength if true
│   └── charge: adds charge bonus on first hit
│
├── Damage typing (two orthogonal axes)
│   ├── Physical qualifier (pick one): slash / pierce / blunt / none
│   │     → interacts with physical resistance, underwater penalties
│   └── Elemental qualifier (pick any): fire / cold / shock / poison / acid
│         → interacts with elemental resistance
│
├── Damage tags (combinable flags)
│   ├── armor_piercing: prot × 0.5
│   ├── armor_negating: ignore prot
│   ├── magic: bypasses ethereal
│   ├── life_drain: heal attacker
│   ├── internal: bypasses mistform/mossbody
│   └── many more: paralyze, stun, soul_slay, ...
│
├── Special damage type (enum, mutually exclusive)
│   │  Replaces normal damage behavior entirely
│   └── poison / demon / holy / weakness / drain / stun / paralyze / ...
│
├── Targeting layer
│   ├── range: 0 = melee, >0 = ranged (uses precision roll)
│   ├── ammo: ranged ammo count
│   ├── aoe: area of effect radius
│   └── nratt: attacks per round (negative = slower: -2 = every 2 rounds)
│
├── MR interaction
│   ├── mrnegates: target gets MR save
│   ├── mrnegateseasily: easier MR save
│   └── mind: mindless units immune
│
└── Flags
    ├── natural: interacts with bless system
    ├── bonus: reduced multi-weapon penalty
    └── flail: special shield interaction, underwater penalty
```

---

## 10. Magic Path System Topology

Magic paths are stats that gate access to spells and scale spell efficiency:

```
8 elemental paths: F, A, W, E, S, D, N, B  (0-N integer levels)
1 holy path: H (0-N)

Path level determines:
├── Which spells can be cast (minimum path requirement)
├── Spell fatigue: cost / (1 + level - minimum)
│     +1 level = 50% fatigue
│     +2 levels = 33% fatigue
│     +3 levels = 25% fatigue
├── Gem usage cap: max gems per turn = current path level
├── MR penetration: +path/2 to penetration rolls
├── Communion boost: master gains floor(log2(slaves)) path levels
└── Passive resistance bonus: path ≥ 3 grants small matching elemental resistance

Path boosting sources (cumulative):
├── Base path (template)
├── Equipment (items): e.g., Earth Boots +1E
├── Spells: Summon Earthpower +1E
├── Communion: +floor(log2(slaves)) to all paths
├── Gem (one per turn): +1 to one path (Rule of One)
└── Additional gems: boost for fatigue calc only (Rule of Surplus)

Hard constraint: Cannot gain a path you don't have at base level.
```

---

## 11. Organizational Stats (Squad/Commander)

Units don't exist in isolation. The squad/commander hierarchy creates emergent
stats:

```
Commander
├── leadership (int): max units led
│   ├── normal_leadership: for living units
│   ├── undead_leadership: for undead/demons (from Death/Blood paths)
│   └── magic_leadership: for magic beings (from Astral + other paths)
├── morale_bonus: if base leadership ≥ 80, grants morale to led units
├── scripts[5]: ordered spell/action slots
├── inspirational: bonus morale to nearby squads
└── delay: independent random initial delay

Squad
├── units[]: member unit IDs
├── formation: box / line / double_line / sparse / skirmish
├── morale: derived from average unit morale + commander bonus + context
├── delay: shared random initial delay (all members same)
└── order: current combat order (attack, cast, hold, retreat, ...)
```

**Design insight:** Leadership creates a *hierarchy of vulnerability*. Kill the
commander → leaderless units rout or dissolve. This makes the stat system's
organizational layer a valid attack surface, not just a bookkeeping convenience.

---

## 12. Summary: What Makes This System Work

The stat system's power comes from five structural properties:

1. **Orthogonal axes of defense.** Protection, elemental resistance, magic resistance,
   and physical resistance are four independent systems checked at different pipeline
   stages. No single stat grants universal defense.

2. **Entropy guarantees resolution.** Fatigue accumulates, afflictions are permanent,
   morale degrades. Every battle eventually ends because all three ratchet mechanisms
   push toward unit failure.

3. **Stats serve dual purposes.** Every stat matters both in the immediate combat roll
   and in the strategic identity of a unit. There are no "dump stats."

4. **Modifiers are layered with clear precedence.** Base → equipment → buffs →
   environment → fatigue → status. Each layer has defined stacking rules. The system is
   complex but deterministic.

5. **The damage pipeline is a long, ordered chain.** 32 steps in fixed order means
   defensive abilities interact in predictable, composable ways. Each step either
   modifies damage, gates further processing, or triggers a retaliatory effect.

---

*Derived from the Dominions 5/6 combat engine reference library. See `data-model.md` for
exact field definitions, `attack-resolution-pseudocode.md` for the full 32-step pipeline,
and `melee-roll.md` / `damage-roll.md` for roll formulas.*
