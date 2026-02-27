# CDDA Survival Systems Topology

> Reference document for reimplementing CDDA-style survival mechanics.
> Describes the **contour** (architecture, thresholds, data flow) rather than exhaustive content.
> Based on CleverRaven/Cataclysm-DDA as of 2026-02-27.

---

## System Map

```
                         ┌──────────────┐
                         │  FOOD ITEM   │
                         │  (calories,  │
                         │   vitamins,  │
                         │   quench,    │
                         │   fun, stim) │
                         └──────┬───────┘
                                │ consume
                                ▼
┌─────────────────────────────────────────────────────────┐
│                    STOMACH (2500 mL)                     │
│  Tracks: solids volume, water volume, calories, vitamins │
│  Drugs absorbed instantly here                           │
└─────────┬──────────────────────────────┬────────────────┘
          │ solids + nutrients           │ water
          │ (every 30 min)              │ (every 5 min)
          ▼                              ▼
┌──────────────────┐            ┌──────────────────┐
│   GUTS (24 L)    │            │  THIRST STAT     │
│  Further digest  │            │  (-100 to 1200)  │
└────────┬─────────┘            └──────────────────┘
         │ absorb (every 5 min)
         ▼
┌──────────────────────────────────────────┐
│           BODY STORAGE                    │
│  stored_calories  (fat reserves)          │
│  vitamin_levels   (per-vitamin counters)  │
│  lifestyle        (long-term health)      │
└──────────────────────────────────────────┘
         │
         │ burned by BMR × activity_level
         ▼
┌──────────────────────────────────────────┐
│         DERIVED EFFECTS                   │
│  hunger display, weight/BMI, stat mods,  │
│  healing rate, disease resistance         │
└──────────────────────────────────────────┘
```

---

## 1. Digestion Pipeline

### 1.1 Two-Compartment Model

The digestive system has two containers that food passes through sequentially:

| Compartment | Capacity | Role |
|-------------|----------|------|
| **Stomach** | 2500 mL (modifiable by mutations) | Receives food; fast water absorption; drug absorption |
| **Guts** | 24,000 mL | Slow nutrient extraction; calorie/vitamin absorption into body |

Minimum stomach capacity floor: **250 mL** (even with shrinking mutations).

### 1.2 Food Item Properties

Every consumable has these survival-relevant fields:

| Field | Type | Purpose |
|-------|------|---------|
| `calories` | int (kcal) | Energy content |
| `quench` | int | Thirst reduction (1 unit = 5 mL water); can be negative |
| `vitamins` | map<vitamin_id, int> | Micronutrient content |
| `fun` | int | Morale effect when eaten |
| `stim` | int | Stimulant level (affects fatigue/sleep) |
| `healthy` | int | Long-term lifestyle/health modifier |
| `sleepiness_mod` | int | Direct sleepiness adjustment |
| `spoils` | duration | Time until spoilage |
| `comesttype` | enum | FOOD, DRINK, or MED |
| `parasites` | int | Chance of parasite infection (0 = never) |
| `monotony_penalty` | int | Fun reduction for eating the same thing repeatedly |

### 1.3 Ingestion

When food is eaten:
1. Effective volume computed (modified by traits/mutations)
2. If character has **tapeworm**: nutrients halved
3. Food added to stomach via `stomach.ingest(food_summary)`
4. If stomach would exceed capacity: vomit check triggers
   - Vomit chance: random roll `[capacity/2, current_volume] > capacity`

### 1.4 Digestion Tick (every 5 minutes)

**Stomach digest rates:**
| What | Rate | Notes |
|------|------|-------|
| Solids | capacity/6 per 30 min | ~3 hours to empty full stomach |
| Water | 250 mL per 5 min | Very fast; goes directly to thirst |
| Calories | max(5 kcal, 16.7% of stomach cal) per 30 min | Minimum floor prevents stalling |
| Vitamins | max(1 unit, 16.7% of stomach vit) per 30 min | Same minimum floor |
| Drug-type vitamins | 100% instant | Absorbed directly from stomach, bypass guts |

**Guts digest rates:**
| What | Rate | Notes |
|------|------|-------|
| Water | 250 mL per 5 min | Same as stomach |
| Calories | BMR-dependent × hunger modifier | Scales with metabolic state |
| Vitamins | Proportional to hunger modifier | Same scaling |

**Pipeline per tick:**
```
Stomach.digest() → nutrients move to Guts
Guts.digest()    → nutrients move to Body
Body burns       → BMR / (12×24) per 5-min tick
```

### 1.5 Starting State

New character begins with:
- Stomach: 800 kcal + 475 mL solids
- Guts: 300 kcal

---

## 2. Hunger System

### 2.1 How Hunger Works

Hunger is **not a simple counter**. It's a derived display state computed from:
- Current stomach fullness (volume vs capacity)
- Time since last meal
- Whether the character has a calorie deficit (stored < healthy calories)
- BMI/weight category

### 2.2 Hunger Display States

From most fed to most starved:

| State | Condition | Effects |
|-------|-----------|---------|
| **Engorged** | Stomach >= 5/6 capacity | -10 speed, +2 sleepiness, vomit chance (1/500 per tick), +3 pain |
| **Full** | Stomach >= 3/4 capacity | -2 speed, +1 sleepiness |
| **Satisfied** | Recently ate + stomach > 1/2 | None (comfortable) |
| **Blank** | Normal state, no deficit | No display, no effects |
| **Hungry** | Empty stomach or mild deficit | Mild annoyance |
| **Very Hungry** | Ate >15 min ago + deficit | Activity interruption |
| **Famished** | Long time since eating + deficit | Stronger penalties |
| **Near Starving** | Underweight BMI + deficit | Severe penalties |
| **Starving** | Emaciated BMI + deficit | Critical; approaching death |

### 2.3 Decision Tree (with calorie deficit)

```
stomach >= capacity        → Engorged
stomach >= 3/4 cap         → Full
just_ate AND > cap/2       → Satisfied
just_ate                   → Hungry
recently_ate (< 3 hrs)     → Very Hungry
BMI < underweight          → Near Starving
BMI < emaciated            → Starving
else                       → Famished
```

---

## 3. Calorie & Weight System

### 3.1 Stored Calories

- Internal unit: **1/1000 of a kcal** (millikcal)
- `stored_calories`: current fat reserves
- `healthy_calories`: target for "normal" weight
- Ratio `stored / healthy` = calorie percentage (drives hunger display and stat effects)

### 3.2 Metabolic Rate

**Base metabolic rate (BMR):** 2500 kcal/day (standard)

**Activity level multipliers** (applied to BMR for calorie burn):

| Level | Multiplier | Example |
|-------|------------|---------|
| SLEEP | 0.85x | Sleeping |
| NO_EXERCISE | 1.0x | Standing idle |
| LIGHT | 2.0x | Walking, light tasks |
| MODERATE | 4.0x | Jogging, moderate labor |
| BRISK | 6.0x | Running |
| ACTIVE | 8.0x | Heavy labor, combat |
| EXTRA | 10.0x | Sprinting, extreme exertion |

### 3.3 Body Weight Categories (BMI-based)

| Category | BMI Threshold | Gameplay Impact |
|----------|---------------|-----------------|
| Emaciated | < 1.0 | Starving state; severe penalties |
| Underweight | < 2.0 | Near-starving; stat penalties |
| Normal | < 3.0 | No penalties |
| Overweight | < 5.0 | Slight stamina penalty |
| Obese | < 10.0 | Lifestyle penalty, extra body heat |
| Very Obese | < 15.0 | Larger penalties |
| Morbidly Obese | >= 20.0 | Severe penalties |

Conversion constant: **7716 kcal per kg** of body fat (`3500 kcal/lb × 2.205`).

---

## 4. Vitamin / Micronutrient System

### 4.1 Architecture

Each vitamin is a data-driven definition with:

| Field | Purpose |
|-------|---------|
| `id` | Unique identifier (e.g., `iron`, `vitC`, `calcium`) |
| `vit_type` | VITAMIN, TOXIN, DRUG, or COUNTER |
| `min` / `max` | Accumulation bounds |
| `rate` | Passive decay/consumption rate (time per unit) |
| `deficiency` | Effect applied when level <= min threshold |
| `excess` | Effect applied when level >= max threshold |
| `disease` | Severity tiers for deficiency (list of threshold → effect pairs) |
| `disease_excess` | Severity tiers for excess |
| `decays_into` | Other vitamins this converts to over time |

### 4.2 Vitamin Types

| Type | Behavior | Examples |
|------|----------|---------|
| **VITAMIN** | Depletes over time; deficiency causes disease | iron, calcium, vitC |
| **TOXIN** | Accumulates from consumption; excess causes harm | — |
| **DRUG** | Absorbed instantly from stomach (bypasses guts); decays | ethanol, BAC, caffeine |
| **COUNTER** | Generic tracker for game mechanics | mutagen, blood volume, allergens |

### 4.3 Key Vitamins

| ID | Min | Max | Rate | Deficiency | Excess |
|----|-----|-----|------|------------|--------|
| `iron` | -24000 | 3600 | 15 min/unit | anemia | — |
| `vitC` | -5600 | 0 | 15 min/unit | scurvy | — |
| `calcium` | -48000 | 0 | 15 min/unit | — | — |
| `ethanol` | 0 | 1000 | 1 sec/unit | — | drunk |
| `BAC` | 0 | 10000 | 24 sec/unit | — | drunk |
| `blood` | -50000 | 0 | -6 sec/unit | hypovolemia | — |
| `mutagen` | 0 | 2500 | 1 hr/unit | — | mutation trigger |

### 4.4 Disease Severity

Vitamins can define multiple severity tiers. As the level moves further past the threshold, higher-severity effects activate. This allows progressive symptoms (e.g., mild anemia → severe anemia).

---

## 5. Thirst / Hydration System

### 5.1 Core Stat

- **Range:** -100 (overhydrated) to 1200 (death)
- Stored as simple integer `thirst`
- "Instant thirst" display accounts for water currently in stomach: `thirst - stomach_water/10`

### 5.2 Thirst Levels

| Threshold | Label | Color |
|-----------|-------|-------|
| < -60 | Turgid | Green |
| -60 to -20 | Hydrated | Green |
| -20 to 0 | Slaked | Green |
| 0 to 40 | (none) | White |
| 40 to 80 | Thirsty | Yellow |
| 80 to 240 | Very Thirsty | Yellow |
| 240 to 520 | Dehydrated | Light Red |
| > 520 | Parched | Light Red |

### 5.3 Thirst Effects

| Threshold | Effect |
|-----------|--------|
| > 40 | Speed penalty begins (linear: -25 at 300, -50 at 600, -75 at 1200) |
| >= 200 | All stats (STR/DEX/INT/PER) penalized: `-thirst/200` |
| > 520 | Activity interruption ("dangerously dehydrated") |
| 600-1200 | Warning messages at increasing severity |
| >= 1200 | **Death by dehydration** |

### 5.4 Thirst Rate

**Base:** configurable option (default 1.0 per 5-min tick)

**Modifiers:**
| Condition | Multiplier |
|-----------|------------|
| Sleeping | 0.5x |
| Hibernating | 0.286x (2/7) |
| TRANSPIRATION trait | Temperature-dependent: `(temp_F - 32.5) / 40` |
| Enchantments | Arbitrary modifier |

### 5.5 Water Absorption

- 1 quench unit = 5 mL water in stomach
- Water absorbed from stomach at 250 mL per 5-min tick
- Each mL absorbed reduces thirst by 1/5

---

## 6. Sleepiness / Sleep System

### 6.1 Sleepiness (Fatigue Counter)

A single integer that accumulates while awake and decreases while sleeping.

**Thresholds:**

| Level | Value | Focus Cap | Key Effect |
|-------|-------|-----------|------------|
| Alert | < 191 | 100% | Normal |
| Tired | 191 | 80% | Yawning; `lack_sleep` effect applied |
| Dead Tired | 383 | 60% | Microsleeps: 1/(100+INT) chance per action |
| Exhausted | 575 | 40% | Involuntary 30-second naps |
| Massive | 1000+ | 20% | **Forced sleep** (character passes out) |

### 6.2 Sleep Deprivation (Separate Timer)

Tracks **cumulative minutes without proper sleep**. Separate from sleepiness — stimulants can keep you awake while deprivation climbs.

| Stage | Duration | Effects |
|-------|----------|---------|
| Harmless | 2 days | Mild messages, +1 sleepiness |
| Minor | 4 days | Foggy mind, -1 daily health, stimulants delay passout |
| Serious | 7 days | -2 daily health, increased microsleep chance |
| Major | 10 days | -5 daily health guaranteed, 20-hour forced sleep |
| Massive | 14 days | Guaranteed collapse |

**Stimulant interaction:** `stim >= 30` delays forced passout until Major stage.

### 6.3 Sleep Quality & Recovery

Recovery rate while sleeping depends on:

**Comfort levels:**

| Level | Value | Recovery Multiplier |
|-------|-------|---------------------|
| Impossible | -999 | Cannot sleep |
| Uncomfortable | -7 | < 1x |
| Neutral | 0 | 1x |
| Slightly Comfortable | 3 | 2x |
| Sleep Aid | 4 | — (item bonus) |
| Comfortable | 5 | 2.5x |
| Very Comfortable | 10 | 3x |

Comfort comes from: terrain, furniture, vehicle parts, character traits, sleep aid items.

**Additional recovery modifiers:**
- Cold body parts: -5% per cold part
- Pain: -1/60 per pain point
- Disrupted sleep / coughing: 0.5x
- Melatonin effect: 0.8x (trades speed for reliability)
- STOP_SLEEP_DEPRIVATION bionic: 3x multiplier

**During sleep:**
- Hunger rate: 0.5x (hibernation: 2/7x)
- Thirst rate: 0.5x (hibernation: 2/7x)
- Sleep deprivation recovers at 2x the sleepiness recovery rate

### 6.4 Sleepiness Accumulation Rate

- Base: configurable option (PLAYER_SLEEPINESS_RATE)
- Modified by traits, enchantments, tree communion activity
- Characters that don't need food cap at TIRED level

---

## 7. Weariness / Exertion System

### 7.1 Overview

Separate from sleepiness. Tracks **physical exhaustion from activity** via an `activity_tracker`.

### 7.2 Data Model

```
tracker:    int  — Accumulated exertion deficit
intake:     int  — Calorie intake counter (offsets tracker)
current_activity:  float — Current activity level
low_activity_ticks: float — Accumulated rest ticks
```

### 7.3 Weariness Calculation

```
if intake > tracker:
    weariness = tracker / 2000
else:
    weariness = (tracker - intake * 0.5) / 1000
```

Key insight: **eating reduces effective weariness**. Calorie intake directly offsets the exertion tracker.

### 7.4 Recovery

- Requires sustained low activity (below LIGHT_EXERCISE threshold)
- Recovery per rest tick: `1/6 of (BMR or current tracker)` × recovery multiplier
- Sleeping provides **2x recovery bonus**
- Intake decays gradually: `intake *= (1 - recovery_mult)^(1/12)`

---

## 8. Stamina System

### 8.1 Core Mechanic

An integer pool that depletes with physical actions and regenerates during rest. **Not the same as weariness** — stamina is short-term burst capacity; weariness is long-term exhaustion.

### 8.2 Maximum Stamina

```
max = BASE + (SCALING × cardiofit) + enchantments
```

- `cardiofit` represents cardiovascular fitness (1000–3000 range)
- Typical scaling: +5 stamina per cardiofit point

### 8.3 Stamina Costs

| Action | Cost Formula |
|--------|-------------|
| Movement | `base_burn_rate × (1 + excess_weight/max_weight)` |
| Swimming | `100 / 1.1^swim_skill` (deeper = more) |
| Melee attack | `(weapon_weight/16g + 50) × cost_modifier` |
| Active muscle bionics | ~2x burn rate |

### 8.4 Stamina Regeneration

- Base: configurable rate × `cardiofit / cardio_base`
- Positive stim: `+min(5, stim/15)` per turn
- Negative stim: penalty scaled by current stamina %
- **Winded debuff** (stamina hits 0): regeneration drops to 0.1x

### 8.5 Stamina Thresholds

| Threshold | Effect |
|-----------|--------|
| < 50% | Flag set (tracking) |
| < 25% | Daily health penalty (up to 5 ticks) |
| <= 0 | **Winded effect** applied to all body parts; stamina clamped to 0 |

---

## 9. Body Temperature System

### 9.1 Per-Body-Part Tracking

Each of 12 body parts (head, eyes, mouth, torso, L/R arms, L/R hands, L/R legs, L/R feet) tracks:
- `temp_cur`: Current temperature
- `temp_conv`: Target/equilibrium temperature (what it's moving toward)
- `frostbite_timer`: Accumulator for frostbite progression

### 9.2 Temperature Constants

| Name | Value (C) | Meaning |
|------|-----------|---------|
| FREEZING | 28 | Most aggressive cold effects |
| VERY_COLD | 31 | Frostbite possible |
| COLD | 34 | Cold morale penalties begin |
| NORMAL | 37 | Baseline |
| HOT | 40 | Heat stress level 1 |
| VERY_HOT | 43 | Heat stress level 2 |
| SCORCHING | 46 | Heat stress level 3; death at 57 |

### 9.3 Equilibrium Temperature Inputs

The converging temperature is computed from ~11 additive factors:

1. **Ambient air temperature** (scaled /5 for legacy reasons; replaced by water temp if submerged)
2. **Hunger/starvation warmth:** `4 × min(metabolic_rate, 1.0) - 4` (starving = colder)
3. **Sleepiness warmth:** `-1.725 × (sleepiness / EXHAUSTED)` when awake; neutral when asleep
4. **Sunlight:** +3 C max if exposed outdoors (scaled by irradiance)
5. **Floor/furniture warmth:** bonus when lying on warm furniture
6. **Body part intrinsic warmth:** per-part min/max values from data
7. **Clothing insulation:** per-part warmth value, scaled logarithmically by current temp
8. **Windchill:** function of wind speed, temperature, humidity; reduced by clothing wind resistance (0-100%)
9. **BMI heat bonus:** `+0.1 × sqrt(max(0, bmi_fat - 8))` (obesity = warmer)
10. **Mutation heat modifiers:** trait-based min/bonus heat
11. **Heat radiation:** from fires, lava, etc.

### 9.4 Frostbite

Applies to: **mouth, hands, feet** only.

| Risk Level | Ambient Conditions | Timer Rate |
|------------|-------------------|------------|
| Low (frostnip) | 30F to 10F | +3/tick |
| Medium (frostbite) | 10F to -5F | +8/tick |
| High (severe) | Below -5F with wind | +72/tick |
| Recovery | Outside risk zones | -3/tick |

**Progression:** Timer 0→1800 = frostnip; 1800→3600 = light frostbite (recoverable); >=3600 = severe (permanent). Cap at 3 hours.

### 9.5 Wetness

- Evaporation cools body: `-0.008 C × clothing_mult` per turn when wet
- Drying rate scales with ambient temperature and clothing

---

## 10. Lifestyle ("Healthy") Stat

### 10.1 What It Is

A hidden long-term health score reflecting diet, exercise, and body composition.

- **Range:** -200 to +200
- Separate `daily_health` variable for short-term fluctuations that converges toward `lifestyle`

### 10.2 What Modifies It

| Input | Direction |
|-------|-----------|
| Eating nutritious food | + |
| Eating junk food | - |
| Physical activity (appropriate level) | + |
| Sleep / rest | + |
| Drug use, infections, radiation | - |
| Overweight penalty | `-5 per BMI point over obese` |
| Underweight penalty | `-50 per BMI point under normal` |

### 10.3 What It Affects

| Output | Formula/Effect |
|--------|----------------|
| Max HP per body part | `+ lifestyle × part_health_mod` |
| Disease resistance | Higher lifestyle = higher threshold to resist |
| Natural healing rate | `2^(lifestyle/50)` multiplier |
| Sleep healing bonus | `× (1 + lifestyle/200)` |
| Medicine effectiveness | `× (1 + lifestyle/200)` if positive; `/400` if negative |

### 10.4 Health Categories (Display)

| Range | Label |
|-------|-------|
| <= -100 | Very Bad |
| -100 to -50 | Bad |
| -50 to -10 | Fine |
| -10 to 10 | (neutral) |
| 10 to 50 | Good |
| 50 to 100 | Very Good |
| >= 100 | Great |

---

## 11. Morale (Survival-Related)

### 11.1 Architecture

Each morale modifier is a `morale_point` with: type, bonus value, max, duration, decay_start, age.
- **Permanent:** duration = 0 (persists until removed)
- **Temporary:** decays after `decay_start`, removed at `duration`

### 11.2 Food Morale Types

| Type | Trigger | Sign |
|------|---------|------|
| `food_good` | Positive fun value food | + |
| `food_bad` | Negative fun value food | - |
| `food_hot` | Hot meal | + |
| `honey` | Eating honey | + (permanent) |
| `sweettooth` | Sugar for sweet-tooth trait | + |
| `antimeat` / `antiveggy` / `antijunk` / `antiwheat` | Trait-opposing food | - |
| `lactose` | Lactose for intolerant characters | - |
| `cannibal` / `demicannibal` | Human flesh (positive for psychopaths) | +/- |
| `no_digest` | Indigestible food | - |
| `monotony` | Repeated identical meals | - (cumulative) |

### 11.3 Environmental Morale

| Type | Trigger |
|------|---------|
| `cold` / `hot` | Body part temperature stress (per-part weighted) |
| `wet` | Being drenched |
| `dried_off` | Becoming dry |
| `craving_*` | Addiction withdrawal (nicotine, caffeine, alcohol, opiates, etc.) |

### 11.4 Personality Multipliers

| Trait | Good Morale | Bad Morale |
|-------|-------------|------------|
| Optimistic | 1.2x | 0.8x |
| Bad Tempered | 0.8x | 1.2x |
| Numb | 0.25x | 0.25x |
| On Prozac | 1.0x | 0.25x |

---

## 12. Stimulants

### 12.1 Core Stat

Simple integer `stim` that decays toward 0 over time (±1 per tick).

### 12.2 Effects

| Range | Effect |
|-------|--------|
| Positive | Delays sleep, boosts stamina regen (+min(5, stim/15)/turn) |
| >= 30 | Prevents passout until Major sleep deprivation |
| > 250 | **Heart attack** (overdose) |
| Negative | Stamina regen penalty (withdrawal) |
| < -200 | **Stops breathing** (lethal withdrawal) |

---

## 13. Cross-System Interactions

```
Activity Level ──→ Calorie Burn Rate ──→ Stored Calories ──→ BMI/Weight
     │                                         │                  │
     ├──→ Weariness Tracker                    │                  ├──→ Body Temp (heat bonus)
     │                                         │                  ├──→ Lifestyle Penalty
     ├──→ Stamina Drain                        │                  └──→ Hunger Display
     │                                         │
     └──→ Sleepiness Rate                      └──→ Metabolic Rate ──→ Digestion Speed

Sleep ──→ Sleepiness Recovery (comfort-modified)
   │  ──→ Sleep Deprivation Recovery
   │  ──→ Weariness Recovery (2x bonus)
   │  ──→ Reduced Hunger/Thirst Rate (0.5x)
   │  ──→ Reduced Calorie Burn (0.85x)
   └──→ Body Temp (different comfort baseline: 31C vs 19C awake)

Eating ──→ Stomach Contents ──→ Hunger Display
   │   ──→ Calories ──→ Guts ──→ Stored Calories
   │   ──→ Water ──→ Thirst Reduction
   │   ──→ Vitamins ──→ Deficiency/Excess Effects
   │   ──→ Fun ──→ Morale
   │   ──→ Healthy ──→ Lifestyle
   │   ──→ Stim ──→ Stimulant Level
   └───→ Weariness Intake Offset (calories eaten reduce weariness)

Lifestyle ──→ Max HP
         ──→ Healing Rate
         ──→ Disease Resistance

Morale ──→ Focus (not covered here, but morale feeds into skill learning speed)
```

---

## 14. Key Design Patterns

### 14.1 Tiered Thresholds with Named States
Nearly every system uses named tiers (not smooth curves) with hard threshold values. This makes the systems readable in UI and creates distinct gameplay states.

### 14.2 Dual-Clock Processing
The 5-minute tick handles fast processes (water absorption, metabolic burn, sleepiness gain). The 30-minute tick handles slow processes (solid digestion, stomach-to-guts transfer).

### 14.3 Data-Driven Definitions
Vitamins, effects, food items, morale types, and comfort values are all defined in JSON. The C++ code provides the engine; content is modular.

### 14.4 Competing Counters
Weariness uses `tracker` vs `intake`; hunger uses `stored_calories` vs `healthy_calories`; vitamins use level vs min/max bounds. This pattern of two competing values creating a ratio drives most displays.

### 14.5 Multiplier Stacking
Rates (hunger, thirst, sleepiness, calorie burn) are computed as a base × chain of multipliers from: traits, activity level, sleep state, enchantments, options. The `needs_rates` struct centralizes these.

### 14.6 Separation of Sensation vs Reality
"Instant thirst" shows stomach water as immediate relief even before absorption. Hunger display depends on stomach fullness (sensation) even when stored calories (reality) are fine. This creates a more immersive experience.

---

## Appendix: File Map

| File | Contains |
|------|----------|
| `src/stomach.h/.cpp` | `stomach_contents`, `nutrients`, `food_summary`, digestion logic |
| `src/character.h` | `needs_rates`, sleepiness enums, KCAL_PER_KG, character stat storage |
| `src/character_body.cpp` | `update_stomach()`, temperature calculations, hunger display logic |
| `src/character_health.cpp` | Lifestyle, stamina, sleepiness processing, sleep recovery, thirst damage |
| `src/consumption.cpp` | Food consumption, morale from eating, nutrient calculation |
| `src/activity_tracker.h/.cpp` | Weariness tracking and recovery |
| `src/sleep.h/.cpp` | Comfort system, sleep aid detection |
| `src/itype.h` | `islot_comestible` food item structure, BMR constant |
| `src/game_constants.h` | Activity levels, weight categories, health thresholds |
| `src/vitamin.h/.cpp` | Vitamin class, loading, RDA conversion |
| `src/display.cpp` | Thirst/hunger display text and colors |
| `src/morale.h/.cpp` | Morale data structure and processing |
| `data/json/vitamin.json` | All vitamin definitions |
| `data/json/effects.json` | All effect definitions (hunger states, frostbite, etc.) |
| `data/json/morale_types.json` | Morale type definitions |
| `data/core/game_balance.json` | Tuning constants (stamina base, regen rates, etc.) |

---

## 15. TLG (Cataclysm: The Last Generation) Delta

> Comparison methodology: funnel-sieve diff of all survival-system files between
> CleverRaven/Cataclysm-DDA and Cataclysm-TLG/Cataclysm-TLG, both at HEAD as of 2026-02-27.
> Only topology-level differences are documented; cosmetic renames and code reorganization are noted but not detailed.

### 15.1 Verdict: Structurally Identical, Minor Extensions

The survival system topology in TLG is **the same as DDA**. The two-compartment stomach, vitamin system, thirst, hunger display logic, sleep/comfort, stamina, lifestyle, morale, and body temperature systems are all present and architecturally unchanged. The digestion pipeline, threshold values, and cross-system interactions documented above all apply to TLG.

The differences are:

### 15.2 Naming: "Sleepiness" → "Fatigue"

TLG uses the older CDDA terminology. The enum is `fatigue_levels` (not `sleepiness_levels`) and the cap is `MASSIVE_FATIGUE` (not `MASSIVE_SLEEPINESS`). **Threshold values are identical:** TIRED=191, DEAD_TIRED=383, EXHAUSTED=575, MASSIVE=1000.

### 15.3 New Activity Level: EXPLOSIVE_EXERCISE (12.0x)

TLG adds a 8th activity level above EXTRA_EXERCISE:

| Level | DDA | TLG |
|-------|-----|-----|
| EXTRA_EXERCISE | 10.0x (max) | 10.0x |
| EXPLOSIVE_EXERCISE | — | **12.0x** (new) |

### 15.4 Weariness: Intensity-Scaled Malus for High Activity

This is the most significant mechanical change. In DDA, all activity levels contribute equally to weariness per calorie burned. In TLG, **high-intensity activity incurs bonus weariness**:

| Activity Level | DDA Weariness Bonus | TLG Weariness Bonus |
|----------------|---------------------|----------------------|
| BRISK | 0 | +12.5 per accumulated unit |
| ACTIVE | 0 | +25.0 per accumulated unit |
| EXTRA | 0 | +50.0 per accumulated unit |
| EXPLOSIVE | N/A | +120.0 per accumulated unit |

TLG tracks cumulative time at each high-intensity level separately (`brisk_activity`, `active_activity`, `extra_activity`, `explosive_activity`) and applies the malus on each 5-minute tick. This means sprinting is disproportionately more tiring than walking the same calorie cost.

TLG also adds an `output` counter (calories burned) alongside `intake` (calories eaten), giving the weariness formula a third variable.

### 15.5 Weariness Recovery: Simplified

- DDA: `try_reduce_weariness(bmr, sleepiness_mod, sleepiness_regen_mod)` — recovery scales with fatigue state
- TLG: `try_reduce_weariness(bmr)` — recovery uses a **fixed multiplier of 0.05** (hardcoded, not an option), and the sleepiness/fatigue modifier is removed. Recovery is simpler and not gated by how tired you are.

### 15.6 Vitamin Roster: Minor Content Differences

| Change | Detail |
|--------|--------|
| Removed | `bad_food`, `mutagenic_slurry`, `mutagen_spider`, `triffid_fiber` |
| Added | `mutagen_aranean` (replaces `mutagen_spider`) |
| Renamed | `veggy_allergen` → `vegetable_allergen` |

Core nutritional vitamins (iron, calcium, vitC, etc.) are unchanged.

### 15.7 Morale Types: Minor Content Differences

| Removed from DDA | Added in TLG |
|------------------|--------------|
| `morale_applied_makeup` | `morale_faction_member_died` |
| `morale_bad_protein_bar` | `morale_perm_fancy` |
| `morale_bile` | `morale_perm_pessimist` |
| `morale_demicannibal` | |
| `morale_fun_craft` | |
| `morale_killer_has_killed` / `need_to_kill` | |
| `morale_perm_badtemper` / `perm_hoarder` / `perm_noface` | |
| `morale_shitty_craft` | |
| `morale_sunrise` / `morale_sunset` | |

Renamed: `morale_antiveggy` → `morale_antivegetable`, `morale_craving_opiate` → `morale_craving_opioid`.

The food morale architecture is identical; only the specific type catalog differs.

### 15.8 Code Organization

- DDA's `character_health.cpp` does not exist in TLG. The logic is distributed across other `character_*.cpp` files (likely `character.cpp`, `character_body.cpp`, and the new `character_morale.cpp`).
- DDA's `data/core/game_balance.json` (stamina/regen tuning constants) is absent from TLG core; balance values may be hardcoded or located elsewhere.

### 15.9 Stomach / Digestion / Thirst / Temperature

**No topology changes.** The `stomach.h` diff is purely a C++ type change (`std::array` → `std::vector` for mass units). Digestion rates, stomach capacity, thirst thresholds, thirst display levels, hunger decision tree, body temperature constants, and frostbite mechanics are all identical between DDA and TLG.
