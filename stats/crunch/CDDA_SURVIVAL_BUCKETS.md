# CDDA Survival Systems: Dependency Analysis & Implementation Buckets

> Companion to `CDDA_SURVIVAL_SYSTEMS.md`.
> Answers: which systems are truly interdependent, and which can be implemented in separate buckets?

---

## Verdict

The cross-system interaction diagram (Section 13 of the reference doc) looks like a hairball, but most connections are **one-directional reads of a single value** (a rate multiplier, a threshold check). That's an interface, not entanglement.

There is **one truly entangled cluster**. Everything else is separable.

---

## The Entangled Core

**Digestion + Calories/Weight + Hunger Display** are one system in practice.

- Hunger display reads stomach fullness *and* stored calories *and* BMI.
- Calories flow through the two-compartment digestion pipeline.
- BMI is derived from stored calories.
- You cannot implement any of the three without the other two.

This is Bucket 0. Everything else plugs into it.

---

## Separable Buckets

| Bucket | Inputs from other systems | Coupling |
|--------|---------------------------|----------|
| **Thirst** | Water from stomach (simple `add_water(mL)` call), sleep flag (0.5x mult) | **Weak** |
| **Vitamins** | Vitamin units from digestion (same `add` interface) | **Weak** — entirely self-contained after ingestion |
| **Sleepiness / Sleep** | Stim level (one int, delays passout) | **Weak** — mostly *outgoing* influence (modifies other systems' rates, not vice versa) |
| **Stamina** | Cardiofit (own stat), stim level (one int) | **Weak** — self-contained pool with regen |
| **Weariness** | Activity level (enum), calorie intake (one int) | **Weak** — parallel tracker, not interleaved with digestion |
| **Body Temperature** | Metabolic rate, sleep flag, BMI — all single reads | **Medium** — many *inputs*, but almost nothing depends on its *output* except morale and frostbite |
| **Lifestyle** | Food `healthy` field, BMI, activity level | **Weak** — slow-moving accumulator, reads snapshots |
| **Morale** | Food fun, body temp stress, wetness, cravings | **Weak** — pure aggregator; no system reads morale except Focus (outside survival scope) |
| **Stimulants** | Nothing (set by consumption, decays on its own) | **Trivial** — just an int that ticks toward 0 |

---

## Suggested Implementation Order

```
Bucket 0 — Core (must be first)
    Digestion Pipeline + Calories/Weight + Hunger Display

Bucket 1 — Easy, no deps on each other
    Thirst        needs add_water() from Bucket 0
    Vitamins      needs add_vitamin() from Bucket 0
    Stimulants    standalone int counter

Bucket 2 — Need activity-level concept
    Stamina       needs cardiofit + stim
    Weariness     needs activity level + calorie intake

Bucket 3 — Read from multiple buckets
    Sleepiness/Sleep      once implemented, retrofits 0.5x multipliers onto Buckets 0/1
    Body Temperature      reads from many, outputs little

Bucket 4 — Long-term accumulators, add last
    Lifestyle     reads snapshots from everything
    Morale        aggregator, pure output
```

Each bucket can be implemented with **stub multipliers** (all 1.0) for systems that don't exist yet, then wired up as later buckets come online.

---

## Why This Works: The Rate-Multiplier Pattern

The key architectural insight from CDDA (Section 14.5 of the reference doc) is that systems communicate through **rate multipliers** collected in a `needs_rates` struct. Sleep doesn't *call into* the hunger system — it sets `hunger_rate = 0.5`. Body temperature doesn't *invoke* the calorie system — it reads `metabolic_rate` as a float.

This means:
- Connections between buckets are **config, not control flow**.
- Each bucket can run in isolation with default multipliers.
- Wiring a new bucket in means updating a few multiplier sources — not refactoring the consumer.
- Testing a bucket means injecting known multiplier values.

---

## Dependency Graph (Simplified)

```
                    ┌──────────────────────────┐
                    │  BUCKET 0: Core          │
                    │  Digestion + Calories +  │
                    │  Weight + Hunger Display  │
                    └─────┬──────┬──────┬──────┘
                          │      │      │
              ┌───────────┤      │      ├───────────┐
              │           │      │      │           │
              ▼           ▼      │      ▼           ▼
         ┌─────────┐ ┌────────┐ │ ┌─────────┐ ┌────────────┐
         │ Thirst  │ │Vitamins│ │ │  Stim   │ │  (activity │
         └─────────┘ └────────┘ │ └────┬────┘ │   level)   │
                                │      │      └──┬────┬────┘
                                │      │         │    │
                                │      ▼         ▼    ▼
                                │  ┌────────┐ ┌──────────┐
                                │  │Stamina │ │Weariness │
                                │  └────────┘ └──────────┘
                                │
                     ┌──────────┴──────────┐
                     │                     │
                     ▼                     ▼
              ┌─────────────┐     ┌──────────────┐
              │ Sleep /     │     │  Body        │
              │ Sleepiness  │     │  Temperature │
              └──────┬──────┘     └──────┬───────┘
                     │                   │
                     ▼                   ▼
              ┌─────────────┐     ┌──────────────┐
              │ Lifestyle   │     │  Morale      │
              └─────────────┘     └──────────────┘
```

Arrows mean "reads a value from." No arrow = no dependency.
