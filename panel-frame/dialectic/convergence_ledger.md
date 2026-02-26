# Convergence Ledger

## Process Overview

This ledger records the outcome of a four-round dialectic process applied to 75 propositions about the panel frame UI pattern in golden-age strategy games:

- **Round 1**: Three agents independently produced 25 propositions each, scored on four axes (defensibility, specificity, robustness, compatibility) from 0.0 to 1.0. Agent 1 (formalist) focused on definitional structure, Agent 2 (practitioner) on implementation guidance, Agent 3 (failure analyst) on critique and edge cases.
- **Round 2**: A conflict mapper identified 25 tensions between propositions across agents, each assigned a severity score.
- **Round 3**: Each tension underwent prosecution (attacking the weaker position), defense (rebutting the attack), and adjudication (final ruling with score deltas) passes.
- **Round 4** (this document): All adjudicated deltas are applied to initial scores, composites computed, and propositions categorized.

**Scoring axes**:
- **Defensibility** (def): Logical soundness and evidential grounding
- **Specificity** (spc): Actionability -- can a developer implement this?
- **Robustness** (rob): Resistance to counterargument and edge cases
- **Compatibility** (cmp): Coherence with other propositions in the set

**Composite** = arithmetic mean of all four final axis scores.

**Categories**:
- **Survivor**: composite >= 0.75, no axis below 0.50
- **Wounded**: composite 0.50-0.74, or any axis below 0.50
- **Contested**: unresolved tension with severity >= 0.60 AND composite between 0.60-0.80
- **Fallen**: composite below 0.50 or defensibility below 0.30

**Results**: 57 survivors, 18 contested, 0 wounded, 0 fallen out of 75 total.

---

## Final Scoreboard

All 75 propositions ranked by composite score.

| Rank | ID | Composite | Def | Spc | Rob | Cmp | Category |
|------:|:-------|----------:|-----:|-----:|-----:|-----:|:---------|
| 1 | a2-09 | 0.8975 | 0.92 | 0.90 | 0.85 | 0.92 | SURVIVOR |
| 2 | a3-02 | 0.8825 | 0.98 | 0.93 | 0.90 | 0.72 | SURVIVOR |
| 3 | a1-04 | 0.8750 | 0.90 | 0.92 | 0.80 | 0.88 | SURVIVOR |
| 4 | a2-16 | 0.8700 | 0.88 | 0.88 | 0.80 | 0.92 | SURVIVOR |
| 5 | a3-04 | 0.8700 | 0.93 | 0.95 | 0.82 | 0.78 | SURVIVOR |
| 6 | a3-09 | 0.8700 | 0.94 | 0.92 | 0.87 | 0.75 | SURVIVOR |
| 7 | a3-12 | 0.8700 | 0.93 | 0.92 | 0.88 | 0.75 | SURVIVOR |
| 8 | a1-01 | 0.8625 | 0.92 | 0.85 | 0.88 | 0.80 | SURVIVOR |
| 9 | a1-22 | 0.8625 | 0.88 | 0.86 | 0.83 | 0.88 | SURVIVOR |
| 10 | a2-02 | 0.8625 | 0.90 | 0.80 | 0.85 | 0.90 | SURVIVOR |
| 11 | a2-06 | 0.8625 | 0.90 | 0.82 | 0.85 | 0.88 | SURVIVOR |
| 12 | a2-08 | 0.8625 | 0.88 | 0.85 | 0.82 | 0.90 | SURVIVOR |
| 13 | a2-11 | 0.8625 | 0.90 | 0.88 | 0.85 | 0.82 | SURVIVOR |
| 14 | a1-20 | 0.8600 | 0.87 | 0.90 | 0.82 | 0.85 | SURVIVOR |
| 15 | a3-25 | 0.8600 | 0.93 | 0.88 | 0.85 | 0.78 | SURVIVOR |
| 16 | a3-05 | 0.8575 | 0.93 | 0.80 | 0.88 | 0.82 | SURVIVOR |
| 17 | a3-13 | 0.8575 | 0.91 | 0.85 | 0.87 | 0.80 | SURVIVOR |
| 18 | a2-04 | 0.8550 | 0.92 | 0.90 | 0.75 | 0.85 | SURVIVOR |
| 19 | a3-01 | 0.8550 | 0.92 | 0.82 | 0.88 | 0.80 | SURVIVOR |
| 20 | a2-14 | 0.8525 | 0.88 | 0.90 | 0.78 | 0.85 | SURVIVOR |
| 21 | a2-15 | 0.8500 | 0.90 | 0.78 | 0.82 | 0.90 | SURVIVOR |
| 22 | a2-25 | 0.8500 | 0.88 | 0.72 | 0.85 | 0.95 | SURVIVOR |
| 23 | a3-08 | 0.8500 | 0.88 | 0.90 | 0.85 | 0.77 | SURVIVOR |
| 24 | a2-20 | 0.8475 | 0.88 | 0.85 | 0.78 | 0.88 | SURVIVOR |
| 25 | a2-23 | 0.8400 | 0.86 | 0.80 | 0.78 | 0.92 | SURVIVOR |
| 26 | a3-15 | 0.8400 | 0.89 | 0.86 | 0.84 | 0.77 | SURVIVOR |
| 27 | a1-07 | 0.8375 | 0.86 | 0.80 | 0.79 | 0.90 | SURVIVOR |
| 28 | a2-05 | 0.8325 | 0.85 | 0.78 | 0.80 | 0.90 | SURVIVOR |
| 29 | a2-19 | 0.8300 | 0.85 | 0.92 | 0.70 | 0.85 | SURVIVOR |
| 30 | a2-24 | 0.8250 | 0.85 | 0.88 | 0.75 | 0.82 | SURVIVOR |
| 31 | a3-18 | 0.8250 | 0.86 | 0.91 | 0.83 | 0.70 | SURVIVOR |
| 32 | a1-18 | 0.8225 | 0.86 | 0.84 | 0.77 | 0.82 | SURVIVOR |
| 33 | a2-18 | 0.8225 | 0.86 | 0.75 | 0.80 | 0.88 | SURVIVOR |
| 34 | a2-07 | 0.8200 | 0.88 | 0.80 | 0.82 | 0.78 | SURVIVOR |
| 35 | a3-06 | 0.8200 | 0.87 | 0.88 | 0.83 | 0.70 | SURVIVOR |
| 36 | a3-19 | 0.8200 | 0.88 | 0.84 | 0.80 | 0.76 | SURVIVOR |
| 37 | a3-10 | 0.8175 | 0.87 | 0.80 | 0.82 | 0.78 | SURVIVOR |
| 38 | a3-22 | 0.8175 | 0.85 | 0.75 | 0.82 | 0.85 | SURVIVOR |
| 39 | a3-03 | 0.8150 | 0.88 | 0.78 | 0.85 | 0.75 | SURVIVOR |
| 40 | a3-16 | 0.8150 | 0.87 | 0.83 | 0.82 | 0.74 | SURVIVOR |
| 41 | a3-17 | 0.8150 | 0.86 | 0.90 | 0.78 | 0.72 | SURVIVOR |
| 42 | a1-15 | 0.8125 | 0.85 | 0.82 | 0.80 | 0.78 | SURVIVOR |
| 43 | a1-21 | 0.8125 | 0.85 | 0.78 | 0.80 | 0.82 | SURVIVOR |
| 44 | a3-07 | 0.8125 | 0.85 | 0.87 | 0.80 | 0.73 | SURVIVOR |
| 45 | a3-24 | 0.8125 | 0.86 | 0.84 | 0.79 | 0.76 | SURVIVOR |
| 46 | a2-10 | 0.8100 | 0.85 | 0.82 | 0.72 | 0.85 | SURVIVOR |
| 47 | a1-11 | 0.8075 | 0.86 | 0.88 | 0.74 | 0.75 | SURVIVOR |
| 48 | a1-23 | 0.8075 | 0.90 | 0.75 | 0.78 | 0.80 | SURVIVOR |
| 49 | a3-11 | 0.8050 | 0.82 | 0.93 | 0.75 | 0.72 | SURVIVOR |
| 50 | a3-14 | 0.8050 | 0.86 | 0.88 | 0.80 | 0.68 | SURVIVOR |
| 51 | a1-02 | 0.8000 | 0.83 | 0.93 | 0.72 | 0.72 | CONTESTED |
| 52 | a2-03 | 0.8000 | 0.88 | 0.85 | 0.67 | 0.80 | CONTESTED |
| 53 | a1-24 | 0.7975 | 0.83 | 0.77 | 0.79 | 0.80 | SURVIVOR |
| 54 | a1-17 | 0.7950 | 0.83 | 0.87 | 0.73 | 0.75 | CONTESTED |
| 55 | a3-20 | 0.7925 | 0.84 | 0.82 | 0.78 | 0.73 | SURVIVOR |
| 56 | a3-21 | 0.7875 | 0.83 | 0.87 | 0.77 | 0.68 | SURVIVOR |
| 57 | a1-16 | 0.7825 | 0.88 | 0.80 | 0.78 | 0.67 | CONTESTED |
| 58 | a2-22 | 0.7800 | 0.80 | 0.78 | 0.72 | 0.82 | SURVIVOR |
| 59 | a1-06 | 0.7775 | 0.78 | 0.90 | 0.68 | 0.75 | CONTESTED |
| 60 | a1-10 | 0.7750 | 0.82 | 0.85 | 0.65 | 0.78 | CONTESTED |
| 61 | a1-12 | 0.7725 | 0.84 | 0.67 | 0.76 | 0.82 | SURVIVOR |
| 62 | a2-17 | 0.7725 | 0.82 | 0.80 | 0.75 | 0.72 | SURVIVOR |
| 63 | a3-23 | 0.7725 | 0.87 | 0.67 | 0.85 | 0.70 | CONTESTED |
| 64 | a1-05 | 0.7675 | 0.78 | 0.75 | 0.72 | 0.82 | CONTESTED |
| 65 | a1-09 | 0.7675 | 0.82 | 0.72 | 0.68 | 0.85 | CONTESTED |
| 66 | a2-21 | 0.7625 | 0.82 | 0.68 | 0.75 | 0.80 | SURVIVOR |
| 67 | a2-01 | 0.7600 | 0.82 | 0.75 | 0.62 | 0.85 | CONTESTED |
| 68 | a1-14 | 0.7450 | 0.79 | 0.90 | 0.69 | 0.60 | CONTESTED |
| 69 | a1-19 | 0.7450 | 0.82 | 0.85 | 0.68 | 0.63 | CONTESTED |
| 70 | a1-25 | 0.7350 | 0.79 | 0.93 | 0.62 | 0.60 | CONTESTED |
| 71 | a1-08 | 0.7275 | 0.78 | 0.88 | 0.65 | 0.60 | CONTESTED |
| 72 | a1-13 | 0.7275 | 0.80 | 0.82 | 0.64 | 0.65 | CONTESTED |
| 73 | a2-13 | 0.7225 | 0.62 | 0.92 | 0.55 | 0.80 | CONTESTED |
| 74 | a1-03 | 0.6550 | 0.72 | 0.78 | 0.55 | 0.57 | CONTESTED |
| 75 | a2-12 | 0.6325 | 0.67 | 0.75 | 0.51 | 0.60 | CONTESTED |

---

## Survivors (57)

Propositions with composite >= 0.75 and no axis below 0.50. These form the core of the final document.

### a2-09 -- composite: 0.8975

> Every interactive panel element should serve both novice users (who click it) and expert users (who use hotkeys), by printing hotkey letters on icons, maintaining consistent grid positions across all contexts, and making the panel useful as a read-only status display.

Def=0.92 | Spc=0.90 | Rob=0.85 | Cmp=0.92
  Deltas: t-20:robustness(-0.03)

### a3-02 -- composite: 0.8825

> Five of the six high-value factors (viewport partitioning, opacity, permanence, fixed geometry, spatial exclusivity) are entailed by the three-word phrase 'opaque, persistent, non-overlapping' from the boxed definition, making them elaborations rather than independent discriminators.

Def=0.98 | Spc=0.93 | Rob=0.90 | Cmp=0.72
  Deltas: t-01:defensibility(+0.03)

### a1-04 -- composite: 0.8750

> The correct test for whether two factors should remain separate or be merged is: can the two factors be independently violated in at least one historical example?

Def=0.90 | Spc=0.92 | Rob=0.80 | Cmp=0.88
  Deltas: t-22:robustness(-0.05)

### a2-16 -- composite: 0.8700

> Information channels should be separated by cognitive function: the panel carries persistent quantitative data read at the player's initiative, audio carries transient event notifications pushed asynchronously, and viewport overlays carry spatial data contextually attached to world-space entities.

Def=0.88 | Spc=0.88 | Rob=0.80 | Cmp=0.92

### a3-04 -- composite: 0.8700

> The panel frame definition fails to exclude Diablo II in inventory-open state, which meets all stated criteria (persistent bottom panel, opaque inventory panel, viewport budget less than 1.0) yet no one classifies Diablo II as a panel-frame game, revealing that the definition is a snapshot predicate applied to a temporal phenomenon.

Def=0.93 | Spc=0.95 | Rob=0.82 | Cmp=0.78
  Deltas: t-02:defensibility(+0.03)

### a3-09 -- composite: 0.8700

> The definition treats 'panel frame' as a property of a game when it is actually a property of a view or mode within a game, creating confusion for multi-view games like Master of Orion II which has a galaxy view (panel frame), colony screen (different panel frame), ship design screen (modal), and combat screen (yet another panel frame).

Def=0.94 | Spc=0.92 | Rob=0.87 | Cmp=0.75
  Deltas: t-15:defensibility(+0.03)

### a3-12 -- composite: 0.8700

> Viewport budget (viewport_area / display_surface_area) is a systematically misleading metric because two games with identical viewport budgets of 0.70 can have wildly different functional layouts: a tall narrow right sidebar ideal for RTS base management versus a short wide bottom bar ideal for isometric exploration.

Def=0.93 | Spc=0.92 | Rob=0.88 | Cmp=0.75
  Deltas: t-06:defensibility(+0.03)

### a1-01 -- composite: 0.8625

> The panel frame definition should use a hybrid approach: prototype theory with weighted factors for the cluster, but classical necessary-and-sufficient logic for one hard boundary condition (viewport partitioning).

Def=0.92 | Spc=0.85 | Rob=0.88 | Cmp=0.80

### a1-22 -- composite: 0.8625

> Golden-age viewport budgets (0.55-0.85) translate to enormous panel areas at modern resolutions; modern implementations must either fill that space with proportionally more information or adjust the budget upward toward 0.80-0.90.

Def=0.88 | Spc=0.86 | Rob=0.83 | Cmp=0.88

### a2-02 -- composite: 0.8625

> Panel dimensions should be driven by content legibility requirements (the widest content element such as a two-column build grid or minimap), not by proportional ratios of screen space.

Def=0.90 | Spc=0.80 | Rob=0.85 | Cmp=0.90

### a2-06 -- composite: 0.8625

> Panel real-estate allocation should mirror the decision structure of the game: if decisions are primarily 'what to do with this unit,' the command card dominates; if decisions are primarily 'which units to build and where,' stats and production dominate.

Def=0.90 | Spc=0.82 | Rob=0.85 | Cmp=0.88

### a2-08 -- composite: 0.8625

> Viewport overlay systems (like Caesar III's toggleable data visualizations for water, fire, crime, desirability) reduce pressure on panel information density by making the viewport itself carry spatial data that the panel would otherwise need to summarize as numbers.

Def=0.88 | Spc=0.85 | Rob=0.82 | Cmp=0.90

### a2-11 -- composite: 0.8625

> The panel frame pattern requires four implicit input assumptions: high-precision random-access pointing, zero-cost context switching between viewport and panel, screen-edge scrolling, and Fitts's Law dynamics with a free-roaming cursor. Platforms violating these assumptions degrade the pattern.

Def=0.90 | Spc=0.88 | Rob=0.85 | Cmp=0.82

### a1-20 -- composite: 0.8600

> The guidance section should be organized by developer decision points ('how wide should my sidebar be?', 'where should the minimap go?'), not by factors, with each recommendation explicitly citing the factors and analyses it derives from.

Def=0.87 | Spc=0.90 | Rob=0.82 | Cmp=0.85

### a3-25 -- composite: 0.8600

> Information density, the only high-value factor that adds genuinely new discriminatory content beyond the boxed definition, is also the vaguest: it specifies no metric, no baseline for comparison, and could mean display density (pixels of distinct visual information per area), control density (interactive controls per area), or navigation density (spatial affordances per area), each of which would classify panels differently.

Def=0.93 | Spc=0.88 | Rob=0.85 | Cmp=0.78
  Deltas: t-08:defensibility(+0.03)

### a3-05 -- composite: 0.8575

> The canon of 15 exemplar games is a tautological confirmation set that can only test inclusion power, not exclusion power; rigorous testing requires a near-miss set of games that share most but not all panel-frame properties.

Def=0.93 | Spc=0.80 | Rob=0.88 | Cmp=0.82

### a3-13 -- composite: 0.8575

> The viewport budget numbers lack a measurement methodology, failing the basic scientific criterion of reproducibility: whether panels are measured by bounding rectangles or visual boundaries, whether decorative borders count as panel or viewport area, and whether status bars are included are all unspecified.

Def=0.91 | Spc=0.85 | Rob=0.87 | Cmp=0.80

### a2-04 -- composite: 0.8550

> The minimap must be placed in a screen corner because screen corners are 'infinite' Fitts's Law targets in two dimensions -- the cursor physically cannot overshoot -- making the minimap trivially easy to hit with a fast, imprecise mouse flick.

Def=0.92 | Spc=0.90 | Rob=0.75 | Cmp=0.85

### a3-01 -- composite: 0.8550

> The boxed definition of panel frames presents itself as a spatial predicate (area relationship to the display surface) when it actually functions as a functional predicate (the 'main' scrollable, spatially-continuous world view), smuggling in unacknowledged assumptions about continuity, scrollability, and primacy that do the real discriminatory work.

Def=0.92 | Spc=0.82 | Rob=0.88 | Cmp=0.80

### a2-14 -- composite: 0.8525

> Panel scaling should use fixed logical dimensions scaled by integer DPI factors, not proportional screen ratios: a 4K display at 2x scaling should show the same logical layout as 1080p with crisper rendering, and all additional pixels should go to the viewport.

Def=0.88 | Spc=0.90 | Rob=0.78 | Cmp=0.85

### a2-15 -- composite: 0.8500

> The Westwood sidebar declined not because it was aesthetically outdated but because it was optimized for sequential construction from a catalog, and when that interaction pattern ceased to dominate gameplay (as in Generals), the layout ceased to serve.

Def=0.90 | Spc=0.78 | Rob=0.82 | Cmp=0.90

### a2-25 -- composite: 0.8500

> The golden-age panel frame was not one design but a family of designs each optimized for a specific interaction pattern, and the practitioner's task is to identify their game's primary interaction pattern, select the matching layout archetype, then apply the concrete principles (Fitts's Law placement, channel separation, expert/novice divergence, fixed-logical scaling, audio integration, overlay complementarity) to execute it.

Def=0.88 | Spc=0.72 | Rob=0.85 | Cmp=0.95

### a3-08 -- composite: 0.8500

> The opacity binary (opaque panel vs. transparent overlay) forces categorical judgment on a continuous gradient, producing arbitrary classifications for intermediate cases like Total Annihilation's semi-transparent build menus and Warcraft III's transparency-edged panel textures, without the user knowing they are in the arbitrary zone.

Def=0.88 | Spc=0.90 | Rob=0.85 | Cmp=0.77

### a2-20 -- composite: 0.8475

> The idle-villager button in Age of Empires II represents a higher level of information abstraction than raw data display: it is a derived-state indicator that collapses an entire map scan into a single glanceable element, communicating a judgment ('you have villagers doing nothing, which is bad') rather than a number.

Def=0.88 | Spc=0.85 | Rob=0.78 | Cmp=0.88

### a2-23 -- composite: 0.8400

> No single information channel (panel, audio, viewport overlays) should try to carry all three cognitive functions (persistent quantitative data, event notifications, spatial data), because overloading any one channel degrades its primary purpose through clutter, confusion, or visual noise respectively.

Def=0.86 | Spc=0.80 | Rob=0.78 | Cmp=0.92

### a3-15 -- composite: 0.8400

> The definition describes panel frames as static spatial layouts but panels are temporal systems: the StarCraft command card changes contents several times per second, and two panel frames with identical spatial layouts but different update rates create different cognitive loads that the definition cannot distinguish because it has no temporal vocabulary.

Def=0.89 | Spc=0.86 | Rob=0.84 | Cmp=0.77

### a1-07 -- composite: 0.8375

> Archetypes (synchronic structural similarity) and lineages (diachronic design inheritance) are orthogonal classification axes, not competing alternatives, and should both be represented in the bible's taxonomy.

Def=0.86 | Spc=0.80 | Rob=0.79 | Cmp=0.90
  Deltas: t-05:robustness(-0.08), t-05:defensibility(-0.05)

### a2-05 -- composite: 0.8325

> The center information panel optimizes for visual scanning rather than pointing, and this functional decomposition -- edges for interaction targets, center for information display -- is a principled Fitts's Law optimization.

Def=0.85 | Spc=0.78 | Rob=0.80 | Cmp=0.90

### a2-19 -- composite: 0.8300

> Layout archetype selection should be driven by the game's primary interaction pattern: commanding agents requires a bottom-panel triptych, sequential catalog construction requires a sidebar, canvas painting requires a top toolbar, and multi-variable comparison requires floating windows.

Def=0.85 | Spc=0.92 | Rob=0.70 | Cmp=0.85

### a2-24 -- composite: 0.8250

> If a target platform cannot provide a free-roaming cursor with sub-pixel precision, zero-cost viewport-to-panel transitions, and screen-edge scrolling, the panel frame pattern should not be used and a different interaction pattern (radial menus for controllers, gesture-based for touch) should be adopted instead.

Def=0.85 | Spc=0.88 | Rob=0.75 | Cmp=0.82
  Deltas: t-13:robustness(-0.05)

### a3-18 -- composite: 0.8250

> The term 'panel' subsumes wildly different UI elements (a 32-pixel resource bar, a 200x400 command card, a 180x180 minimap, a 120-pixel unit portrait) that have different update rates, interaction models, cognitive load profiles, and design constraints, making the single term analytically useless when designing any one of them.

Def=0.86 | Spc=0.91 | Rob=0.83 | Cmp=0.70

### a1-18 -- composite: 0.8225

> Resolution and display scaling should be handled as a context section preceding factor definitions, not as factors themselves, because resolution is a property of the medium, not of the pattern.

Def=0.86 | Spc=0.84 | Rob=0.77 | Cmp=0.82
  Deltas: t-23:robustness(-0.03)

### a2-18 -- composite: 0.8225

> The interaction's cognitive demand structure determines whether fixed or floating information surfaces are appropriate: comparison-heavy management sims favor floating windows, while rapid spatial action games favor fixed panels.

Def=0.86 | Spc=0.75 | Rob=0.80 | Cmp=0.88

### a2-07 -- composite: 0.8200

> The right sidebar persists in city builders not out of conservatism but because deep hierarchical building categories, absence of unit commanding, deliberate pacing, and persistent tool state all favor a vertical sidebar over a horizontal bottom bar.

Def=0.88 | Spc=0.80 | Rob=0.82 | Cmp=0.78

### a3-06 -- composite: 0.8200

> The canon exclusively comprises English-language PC games from Western studios, systematically excluding Japanese strategy games (Koei's titles) that used panel frames with inverted information hierarchies where the panel was the primary interaction surface and the viewport served as geographic context.

Def=0.87 | Spc=0.88 | Rob=0.83 | Cmp=0.70

### a3-19 -- composite: 0.8200

> The panel frame's importance inverts with player skill: for novices it is the primary learning interface (visible commands, displayed resources, spatial orientation via minimap), while for experts it is largely vestigial (commands via hotkeys, resources tracked mentally, only the minimap retaining high value).

Def=0.88 | Spc=0.84 | Rob=0.80 | Cmp=0.76

### a3-10 -- composite: 0.8175

> Lineage-based organization (Westwood tree, Blizzard tree, Ensemble tree) implies conscious reference to predecessors when actual design causation involves dozens of simultaneous influences (competitor games, platform SDKs, publisher requirements, engine constraints, team size), and without internal design documents, lineage claims are reverse-engineered narratives that privilege visual similarity over actual causal history.

Def=0.87 | Spc=0.80 | Rob=0.82 | Cmp=0.78
  Deltas: t-05:defensibility(+0.03)

### a3-22 -- composite: 0.8175

> The definition's failure modes form a connected topology of mutual reinforcement: definitional circularity prevents excluding borderline cases, which leaves survivorship bias untested, which preserves genre conflation; the viewport budget fallacy combines with temporal blindness and the audio blind spot to capture perhaps 30% of actual information architecture while presenting itself as complete.

Def=0.85 | Spc=0.75 | Rob=0.82 | Cmp=0.85

### a3-03 -- composite: 0.8150

> The redundancy of five factors creates false confidence: a user checking borderline cases will see five factors pass or fail together (because they are the same criterion stated five ways) and one subjective factor (information density), producing spuriously confident binary judgments where uncertain continuous judgments are appropriate.

Def=0.88 | Spc=0.78 | Rob=0.85 | Cmp=0.75

### a3-16 -- composite: 0.8150

> The definition models screen space as the scarce resource (viewport budget) when the actual scarce resource is player attention: a panel operable entirely by keyboard shortcuts imposes zero attention cost from the viewport, making two visually identical panel frames functionally different interfaces for different player populations.

Def=0.87 | Spc=0.83 | Rob=0.82 | Cmp=0.74

### a3-17 -- composite: 0.8150

> The definition classifies decorative surround as a low-value factor, but race-specific panel textures in StarCraft (Zerg organic, Protoss crystalline, Terran metallic) serve a functional purpose in competitive play by instantly communicating race identity, and panel decoration's visual weight affects perceptual boundary strength and thus attention-switching cost.

Def=0.86 | Spc=0.90 | Rob=0.78 | Cmp=0.72
  Deltas: t-25:defensibility(+0.03)

### a1-15 -- composite: 0.8125

> Systemic anti-patterns that reject the entire pattern (like Sacrifice's first-person perspective with spell wheel overlay) deserve standalone treatment separate from inline single-factor anti-patterns.

Def=0.85 | Spc=0.82 | Rob=0.80 | Cmp=0.78

### a1-21 -- composite: 0.8125

> The Berlin Interpretation's failure to include any necessary conditions led to the notorious problem of calling Diablo II a roguelike; the panel frame definition avoids this by admitting exactly one necessary condition.

Def=0.85 | Spc=0.78 | Rob=0.80 | Cmp=0.82

### a3-07 -- composite: 0.8125

> Console strategy games (Advance Wars, Fire Emblem, Final Fantasy Tactics) operated under fundamentally different constraints (lower resolution, no mouse, d-pad navigation) that make the definition's implicit mouse-input and high-resolution assumptions visible, revealing it describes 'the Western PC strategy game panel frame with mouse input' rather than a universal pattern.

Def=0.85 | Spc=0.87 | Rob=0.80 | Cmp=0.73

### a3-24 -- composite: 0.8125

> The definition implicitly privileges the 'main' view of a multi-modal game, but many golden-age strategy games spent significant play-time in secondary views: a Civilization II player might spend more time in city screens than on the main map, creating a mismatch between what the definition describes and what the player experiences.

Def=0.86 | Spc=0.84 | Rob=0.79 | Cmp=0.76

### a2-10 -- composite: 0.8100

> Audio is a first-class information channel that should be designed alongside the panel, not after it: every player-relevant event should be assigned to either panel (persistent, player-initiated) or audio (transient, system-initiated) delivery.

Def=0.85 | Spc=0.82 | Rob=0.72 | Cmp=0.85

### a1-11 -- composite: 0.8075

> The panel frame is a property of the persistent layout, not of the total interface: transient user-invoked windows (like RollerCoaster Tycoon's floating windows) are a separate pattern layered on top and do not affect panel frame classification.

Def=0.86 | Spc=0.88 | Rob=0.74 | Cmp=0.75
  Deltas: t-15:robustness(-0.08), t-15:compatibility(-0.05)

### a1-23 -- composite: 0.8075

> The bible should distinguish between properties that are constitutive of the panel frame pattern and properties that are historically common but contingent, to avoid the Berlin Interpretation's error of conflating historical accident with definitional necessity.

Def=0.90 | Spc=0.75 | Rob=0.78 | Cmp=0.80
  Deltas: t-19:robustness(-0.07)

### a3-11 -- composite: 0.8050

> The bottom-panel layout appeared in Age of Empires (1997), StarCraft (1998), and Dark Reign (1997) within a 12-month window, suggesting convergent evolution driven by shared constraints (higher resolutions making sidebars less efficient) rather than the tree-structured lineage the definition assumes.

Def=0.82 | Spc=0.93 | Rob=0.75 | Cmp=0.72

### a3-14 -- composite: 0.8050

> Grouping RTS panels (200+ APM, instant feedback), city builder panels (5-10 APM, long-term trends), and 4X panels (variable tempo, dual tactical/strategic) under 'panel frame' because they look alike commits the same error as grouping whales and fish because they both swim: the visual similarity is a convergent response to finite display area, not evidence of shared design intent.

Def=0.86 | Spc=0.88 | Rob=0.80 | Cmp=0.68

### a1-24 -- composite: 0.7975

> The morphological space approach accommodates pattern evolution by treating it as movement through the space: post-golden-age trends (higher viewport budgets, contextual panels) are trajectories, not invalidations of the golden-age definition.

Def=0.83 | Spc=0.77 | Rob=0.79 | Cmp=0.80

### a3-20 -- composite: 0.7925

> Golden-age strategy games used audio as an information channel (unit acknowledgments, alert sounds, production-complete jingles) that substitutes for panel space, meaning the viewport budget is not the full information budget: comparing viewport budgets across games without accounting for audio information substitution systematically misestimates information costs.

Def=0.84 | Spc=0.82 | Rob=0.78 | Cmp=0.73

### a3-21 -- composite: 0.7875

> The three 'thin-panel/thick-viewport' (city builders), 'navigation-panel/modal-complexity' (4X games), and 'layered-panel/map-mode' (grand strategy) panel architectures are so architecturally distinct that knowing a game 'uses a panel frame' provides zero design guidance about how its information architecture actually works.

Def=0.83 | Spc=0.87 | Rob=0.77 | Cmp=0.68

### a2-22 -- composite: 0.7800

> A wider, shorter viewport (as produced by a bottom panel) better serves RTS gameplay than a narrower, taller viewport (as produced by a sidebar) because lateral terrain visibility supports the core spatial reasoning tasks of flanking, army positioning, and base layout.

Def=0.80 | Spc=0.78 | Rob=0.72 | Cmp=0.82

### a1-12 -- composite: 0.7725

> The panel frame resolves four fundamental design forces: world visibility vs. state accessibility, information density vs. cognitive load, interaction efficiency vs. learning curve, and aesthetic immersion vs. functional utility.

Def=0.84 | Spc=0.67 | Rob=0.76 | Cmp=0.82
  Deltas: t-24:specificity(-0.03)

### a2-17 -- composite: 0.7725

> Chris Sawyer's floating-window system (Transport Tycoon, RollerCoaster Tycoon) is the most powerful information-comparison architecture of the golden age because it allows simultaneous multi-variable comparison, but its window-management overhead, viewport occlusion, and lack of canonical layout make it unsuitable for rapid spatial action games.

Def=0.82 | Spc=0.80 | Rob=0.75 | Cmp=0.72

### a2-21 -- composite: 0.7625

> The post-golden-age trend is information migration from the panel into the viewport through overlays, contextual tooltips, and strategic zoom, but the panel has not been fully replaced because the three-question decomposition (Where/What/Do) remains cognitively valid even when some answers can be embedded in the viewport.

Def=0.82 | Spc=0.68 | Rob=0.75 | Cmp=0.80

---

## Wounded (0)

No wounded propositions.

---

## Contested (18)

Propositions with unresolved high-severity tensions (>= 0.60) and composite between 0.60-0.80. These require resolution before inclusion in the final document.

### a1-02 -- composite: 0.8000

> Viewport partitioning (viewport_area < display_surface_area) is the single necessary condition for panel frame membership, and it should be the ONLY necessary condition.

Def=0.83 | Spc=0.93 | Rob=0.72 | Cmp=0.72
  **Unresolved tensions**: t-02 (severity 0.90)
  Deltas: t-02:robustness(-0.10), t-02:defensibility(-0.05)

### a2-03 -- composite: 0.8000

> StarCraft's bottom-panel triptych (minimap / info / command card) answers three cognitive questions in left-to-right order -- Where am I? / What am I looking at? / What can I do? -- and this maps onto the decision loop orient-assess-act.

Def=0.88 | Spc=0.85 | Rob=0.67 | Cmp=0.80
  **Unresolved tensions**: t-09 (severity 0.72)
  Deltas: t-09:robustness(-0.05)

### a1-17 -- composite: 0.7950

> The StarCraft triptych (minimap / info display / command card) should be treated as a functional constraint within the Ensemble Bottom Bar archetype -- a pattern nested within a pattern -- not as a top-level definitional element.

Def=0.83 | Spc=0.87 | Rob=0.73 | Cmp=0.75
  **Unresolved tensions**: t-09 (severity 0.72)
  Deltas: t-09:robustness(-0.05)

### a1-16 -- composite: 0.7825

> Information strategies (modal screens, map-as-data, sidebar abstraction) are content patterns orthogonal to the panel frame's spatial layout pattern, and conflating them is a categorical error that would weaken the definition.

Def=0.88 | Spc=0.80 | Rob=0.78 | Cmp=0.67
  **Unresolved tensions**: t-10 (severity 0.75)
  Deltas: t-10:compatibility(-0.05), t-10:robustness(-0.05)

### a1-06 -- composite: 0.7775

> The binary high/low weighting scheme from the Berlin Interpretation should be replaced with a three-tier scheme: necessary (viewport partitioning only), characteristic (opacity, permanence, fixed geometry, spatial exclusivity, information density), and incidental (minimap, contextual sub-panels, decorative surround, resource bar, layout convention, panel-embedded controls).

Def=0.78 | Spc=0.90 | Rob=0.68 | Cmp=0.75
  **Unresolved tensions**: t-08 (severity 0.80), t-25 (severity 0.64)
  Deltas: t-08:robustness(-0.10), t-08:defensibility(-0.05), t-25:specificity(-0.05)

### a1-10 -- composite: 0.7750

> The viewport budget should NOT serve as a scoring axis for pattern membership: a game with budget 0.55 is not 'more of a panel frame' than one with budget 0.80; the budget measures how the pattern is instantiated, not how well.

Def=0.82 | Spc=0.85 | Rob=0.65 | Cmp=0.78
  **Unresolved tensions**: t-06 (severity 0.88)
  Deltas: t-06:robustness(-0.10)

### a3-23 -- composite: 0.7725

> The fundamental meta-failure is that the panel frame bible models a visual layout pattern when the actual design object is a multi-modal, temporally-dynamic, user-dependent, interaction-driven information architecture that happens to have a visual layout as one of its manifestations.

Def=0.87 | Spc=0.67 | Rob=0.85 | Cmp=0.70
  **Unresolved tensions**: t-21 (severity 0.77)
  Deltas: t-21:specificity(-0.05)

### a1-05 -- composite: 0.7675

> Factor granularity serves a diagnostic (prescriptive) function, not just a descriptive (classificatory) function: correlated factors should be preserved because they point to different implementation fixes.

Def=0.78 | Spc=0.75 | Rob=0.72 | Cmp=0.82
  **Unresolved tensions**: t-03 (severity 0.85)
  Deltas: t-03:defensibility(-0.07), t-03:robustness(-0.08)

### a1-09 -- composite: 0.7675

> The viewport budget (viewport_area / display_surface_area) is a proxy for the designer's model of where information lives: high budgets say the world is the primary information display, low budgets say panels provide co-equal information alongside the world.

Def=0.82 | Spc=0.72 | Rob=0.68 | Cmp=0.85
  **Unresolved tensions**: t-06 (severity 0.88)
  Deltas: t-06:robustness(-0.12), t-06:defensibility(-0.05)

### a2-01 -- composite: 0.7600

> The panel frame's opacity is load-bearing: the hard edge between panel and viewport creates two distinct visual fields that the eye processes independently, and softening that edge (e.g., semi-transparency as in Tiberian Sun) degrades both regions' legibility.

Def=0.82 | Spc=0.75 | Rob=0.62 | Cmp=0.85
  **Unresolved tensions**: t-07 (severity 0.83)
  Deltas: t-07:robustness(-0.08)

### a1-14 -- composite: 0.7450

> Anti-patterns should be organized inline with the factors they violate, not in a dedicated section, because a developer reading about a factor should immediately see what happens when it is violated.

Def=0.79 | Spc=0.90 | Rob=0.69 | Cmp=0.60
  **Unresolved tensions**: t-12 (severity 0.65)
  Deltas: t-12:robustness(-0.05), t-12:compatibility(-0.05)

### a1-19 -- composite: 0.7450

> The bible must maintain a strict separation between descriptive content (definition, factors, scoring, canon), analytical content (boundary cases, anti-patterns, context), and prescriptive content (developer guidance), to avoid contaminating the definition with opinions.

Def=0.82 | Spc=0.85 | Rob=0.68 | Cmp=0.63
  **Unresolved tensions**: t-14 (severity 0.62)
  Deltas: t-14:compatibility(-0.05), t-14:robustness(-0.05)

### a1-25 -- composite: 0.7350

> The proposed thirteen-section bible structure (Scope, Forces, Definitions, Necessary Condition, Characteristic Factors, Incidental Factors, Viewport Budget, Morphological Space, Canon, Boundary Cases, Historical Context, Design Guidance, Glossary) moves from theoretical foundation through formal definition through empirical mapping to practical application, with each section building on the previous ones.

Def=0.79 | Spc=0.93 | Rob=0.62 | Cmp=0.60
  **Unresolved tensions**: t-17 (severity 0.78)
  Deltas: t-17:robustness(-0.08), t-17:compatibility(-0.05)

### a1-08 -- composite: 0.7275

> The bible should define a six-dimensional morphological space (panel placement, panel count, functional decomposition, viewport budget, visual grammar, interaction model) where each game occupies a point, archetypes are clusters, lineages are paths, and sub-types are named regions.

Def=0.78 | Spc=0.88 | Rob=0.65 | Cmp=0.60
  **Unresolved tensions**: t-04 (severity 0.68)
  Deltas: t-04:compatibility(-0.08), t-04:robustness(-0.05)

### a1-13 -- composite: 0.7275

> The bible should adopt Christopher Alexander's force-based framing as its theoretical foundation, presented before factor definitions, so that factors become testable consequences of force resolution rather than arbitrary feature checklists.

Def=0.80 | Spc=0.82 | Rob=0.64 | Cmp=0.65
  **Unresolved tensions**: t-21 (severity 0.77)
  Deltas: t-21:robustness(-0.08), t-21:compatibility(-0.05)

### a2-13 -- composite: 0.7225

> The viewport should never consume less than 65% of total screen area; at 1920x1080 reference resolution, the panel may consume at most approximately 350 pixels of height (bottom panel) or 480 pixels of width (sidebar).

Def=0.62 | Spc=0.92 | Rob=0.55 | Cmp=0.80
  **Unresolved tensions**: t-11 (severity 0.70)
  Deltas: t-11:defensibility(-0.08), t-11:robustness(-0.07)

### a1-03 -- composite: 0.6550

> Every additional necessary condition beyond viewport partitioning risks excluding a legitimate edge case; opacity, permanence, fixed geometry, and spatial exclusivity should remain weighted factors, not hard gates.

Def=0.72 | Spc=0.78 | Rob=0.55 | Cmp=0.57
  **Unresolved tensions**: t-01 (severity 0.92), t-07 (severity 0.83)
  Deltas: t-01:robustness(-0.12), t-01:defensibility(-0.08), t-07:compatibility(-0.08), t-07:robustness(-0.05)

### a2-12 -- composite: 0.6325

> The minimap was always a compression artifact -- a small rendering of the map crammed into the panel because the viewport could not show the full map -- and when continuous strategic zoom allows the viewport to show the full map, the minimap becomes redundant.

Def=0.67 | Spc=0.75 | Rob=0.51 | Cmp=0.60
  **Unresolved tensions**: t-16 (severity 0.60)
  Deltas: t-16:defensibility(-0.05), t-16:robustness(-0.07)

---

## Fallen (0)

No fallen propositions.

---

## Tension Resolution Map

For each high-severity tension (severity >= 0.80), how it was resolved and which propositions were affected.

### t-01 (severity: 0.92)

*Tension*: a1-03 argues that opacity, permanence, fixed geometry, and spatial exclusivity should remain as separate weighted factors (not hard gates) to preserve diagnostic granularity. a3-02 demonstrates that five of the six factors are merely restatements of words already in the boxed definition ('opaque, persistent, non-overlapping'), making them redundant elaborations rather than independent discriminators. a3-03 extends this by arguing their redundancy creates false confidence in borderline classifications. The formalist wants to keep these factors as useful separate axes; the failure analyst says they are the same axis stated five times. The final document must decide whether these factors carry independent weight or are definitional tautologies.

- **a1-03** [CONTESTED]: robustness: -0.12, defensibility: -0.08
- **a3-02** [SURVIVOR]: defensibility: +0.03

*Resolution*: The prosecution's core point stands: the five factors do not provide five independent pieces of evidence for classification purposes, and a1-03's claim that they should 'remain weighted factors' overstates their classificatory independence. However, the defense correctly identifies that the prescriptive/diagnostic function (a1-05's argument) partially rescues a1-03's position -- factors can be logically correlated yet prescriptively distinct. The adjudicator applies a significant robustness hit (-0.12) because a1-03's robustness was already its weakest axis and the redundancy argument mater...

### t-02 (severity: 0.90)

*Tension*: a1-02 proposes viewport partitioning (viewport_area < display_surface_area) as the single necessary condition for panel frame membership. a3-01 argues this spatial predicate actually smuggles in unstated functional assumptions (continuity, scrollability, primacy) that do the real discriminatory work. a3-04 provides a concrete counterexample: Diablo II in inventory-open state satisfies the spatial predicate yet no one classifies it as a panel-frame game, because the definition lacks a temporal dimension (persistence across game states, not just within one state). The formalist's clean necessary condition is undermined by both a missing functional foundation and a missing temporal requirement.

- **a1-02** [CONTESTED]: robustness: -0.10, defensibility: -0.05
- **a3-04** [SURVIVOR]: defensibility: +0.03

*Resolution*: The defense makes a critical correct point: a1-02 proposes a necessary condition, not a sufficient one, so the Diablo II counterexample does not refute the proposition's logic -- it only shows the condition is not sufficient, which was never claimed. However, a3-01's critique that the spatial predicate smuggles in unstated functional assumptions is a genuine weakness: the inequality as stated (viewport_area < display_surface_area) does not distinguish between a persistent panel frame and a temporary inventory overlay, meaning the predicate requires unstated qualifiers to function as intende...

### t-06 (severity: 0.88)

*Tension*: a1-09 interprets viewport budget as a proxy for the designer's information model (high budget = world-primary, low budget = panel-co-equal). a1-10 argues viewport budget should not serve as a scoring axis. a3-12 demonstrates the metric is fundamentally misleading because two games with identical viewport budgets (0.70) can have wildly different functional layouts (tall sidebar vs. short bottom bar). a3-13 adds that the metric lacks a reproducible measurement methodology (bounding rectangles vs. visual boundaries, decorative borders, status bars). The formalist builds interpretive theory on a metric that the failure analyst shows is both conceptually flawed (collapses 2D layout to a scalar) and methodologically unspecified.

- **a1-09** [CONTESTED]: robustness: -0.12, defensibility: -0.05
- **a1-10** [CONTESTED]: robustness: -0.10
- **a3-12** [SURVIVOR]: defensibility: +0.03

*Resolution*: The defense correctly notes that proxies can be lossy and within-layout-type comparisons remain meaningful. However, the prosecution's core point is not that the metric is imprecise but that it is categorically misleading: collapsing 2D layout to a scalar loses the functional dimension (sidebar vs. bottom-bar), which is precisely the dimension that matters most for design decisions. a1-09's theory (budget reflects information model) is plausible as a trend observation but is weakened when the metric it interprets cannot distinguish functionally opposite layouts. a1-10's internal inconsisten...

### t-15 (severity: 0.86)

*Tension*: a1-11 argues the panel frame is a property of the persistent layout, and transient user-invoked windows are a separate pattern layered on top. a3-09 argues the definition treats 'panel frame' as a property of a game when it is actually a property of a view or mode, citing MOO2's four architecturally different views. a3-24 extends this by noting players often spend more time in secondary views (Civilization II city screens) than in the 'main' view the definition privileges. The formalist's persistent-vs-transient distinction partially addresses the temporal issue but still operates at the game level, while the failure analyst demands a view-level or mode-level unit of analysis. The document must decide whether 'panel frame' attaches to games, to views, or to persistent layouts within views.

- **a1-11** [SURVIVOR]: robustness: -0.08, compatibility: -0.05
- **a3-09** [SURVIVOR]: defensibility: +0.03

*Resolution*: The defense correctly notes that persistent-vs-transient and game-vs-view are complementary distinctions. However, a1-11 does not explicitly acknowledge the view-level issue -- it frames the panel frame as a property of 'the persistent layout' without specifying which view's persistent layout. This ambiguity is a genuine robustness weakness: a developer applying a1-11 to MOO2 would not know which view to analyze. The compatibility hit reflects that a3-09 and a3-24 demand a more granular unit of analysis than a1-11 provides. a3-09 gets a modest defensibility boost because the MOO2 four-view ...

### t-03 (severity: 0.85)

*Tension*: a1-05 argues that correlated factors should be preserved because they serve a diagnostic (prescriptive) function: 'your panel is not spatially exclusive' and 'your panel is not opaque' are different implementation fixes even if the factors correlate. a3-02 counters that five of the six factors are not merely correlated but logically entailed by the same three-word phrase, making them not just correlated diagnostics but restatements of the same criterion. If factors are truly entailed rather than correlated, the diagnostic-granularity argument collapses: telling a developer to fix 'opacity' and 'spatial exclusivity' separately is meaningless if both reduce to 'make the panel opaque and non-overlapping,' which is already in the definition.

- **a1-05** [CONTESTED]: defensibility: -0.07, robustness: -0.08

*Resolution*: The defense makes a legitimate point about implementation-level distinctness: opacity and spatial exclusivity do map to different code changes. However, this defense only works if the bible explicitly frames these factors as implementation diagnostics rather than classificatory criteria. a1-05 argues for both roles ('diagnostic/prescriptive function, not just descriptive/classificatory'), but the prescriptive role is only rescued if the document clearly separates 'these factors help classify' (where they are redundant) from 'these factors guide implementation' (where they remain distinct). ...

### t-07 (severity: 0.83)

*Tension*: a2-01 argues that opacity is load-bearing and the hard edge between panel and viewport is functionally essential for legibility. a1-03 argues opacity should remain a weighted factor, not a hard gate, to avoid excluding legitimate semi-transparent panel designs. a3-08 argues the opacity binary forces arbitrary categorical judgments on a continuous gradient, citing Total Annihilation's semi-transparent build menus and Warcraft III's transparency-edged textures. Three mutually incompatible positions: opacity is functionally necessary (practitioner), opacity should be a soft factor (formalist), the opacity binary itself is ill-posed (failure analyst). The document cannot adopt all three.

- **a1-03** [CONTESTED]: compatibility: -0.08, robustness: -0.05
- **a2-01** [CONTESTED]: robustness: -0.08

*Resolution*: The defense correctly identifies a viable synthesis (opacity as a high-weight characteristic factor on a gradient), which means the three positions are not fully mutually exclusive -- but they do require each to retreat from its strongest form. a1-03's compatibility drops because the synthesis requires opacity to be a high-weight factor, not just any weighted factor, which is closer to a2-01's position than a1-03 intended. Its robustness takes a smaller hit because the defense's synthesis is available. a2-01's robustness drops because the 'hard edge is essential' claim is empirically falsif...

### t-05 (severity: 0.82)

*Tension*: a1-07 argues that archetypes (synchronic structural similarity) and lineages (diachronic design inheritance) are orthogonal classification axes that should both appear in the taxonomy. a3-10 attacks the lineage axis directly: without internal design documents, lineage claims are reverse-engineered narratives that privilege visual similarity over actual causal history. a3-11 reinforces this with the convergent-evolution evidence: the bottom-panel layout appeared in three studios within 12 months, suggesting shared constraints rather than inheritance. If lineages are epistemologically unreliable, the formalist's dual-axis taxonomy loses one of its two axes.

- **a1-07** [SURVIVOR]: robustness: -0.08, defensibility: -0.05
- **a3-10** [SURVIVOR]: defensibility: +0.03

*Resolution*: The defense correctly distinguishes within-studio lineages (observable, verifiable) from cross-studio lineages (speculative). However, a1-07 explicitly uses cross-studio examples ('Blizzard crossing from right-sidebar to bottom-panel archetype') as its demonstration of orthogonality, which is exactly the kind of claim a3-10 targets. The robustness hit (-0.08) reflects that the lineage axis's evidentiary basis is weaker than claimed for the specific cross-studio comparisons a1-07 relies on. The defensibility hit (-0.05) is moderate because the synchronic/diachronic framework itself remains v...

### t-08 (severity: 0.80)

*Tension*: a1-06 proposes a three-tier weighting scheme where information density is classified as a 'characteristic' factor (the second-highest tier). a3-25 argues that information density is the only high-value factor adding genuinely new discriminatory content, but it is also the vaguest: it could mean display density, control density, or navigation density, each classifying panels differently. The formalist assigns information density a high structural role in the definition, but the failure analyst shows the term is too ambiguous to bear that weight without first resolving a three-way semantic ambiguity.

- **a1-06** [CONTESTED]: robustness: -0.10, defensibility: -0.05
- **a3-25** [SURVIVOR]: defensibility: +0.03

*Resolution*: The defense correctly notes that 'characteristic' placement hedges against vagueness, and that the ambiguity is solvable. However, the prosecution's core point stands: a1-06 assigns a structural role to a term it does not define, and the three-way ambiguity means different readers will apply different criteria when evaluating information density, undermining the scheme's reliability. The robustness hit (-0.10) reflects that the tier assignment is unstable until the term is disambiguated. The defensibility hit (-0.05) is smaller because the scheme's structure (necessary/characteristic/incide...

---

## Synthesis Guidance

Based on the survivors, contested propositions, and tension resolutions, the following concrete directives should guide the final document. Each directive traces to specific proposition outcomes.

**1. The viewport budget metric must be supplemented with shape descriptors.** a3-12 (survivor, 0.87) demonstrated that viewport_area/display_surface_area collapses 2D layout to a misleading scalar -- two games with identical 0.70 budgets can have opposite functional layouts. a3-13 (survivor, 0.86) showed the metric lacks a reproducible measurement methodology. Meanwhile a2-13 (contested, 0.72) had its specific thresholds weakened and a1-09 (contested, 0.77) saw its interpretive theory challenged. The final document should retain viewport budget as a rough indicator but always pair it with panel placement type and viewport aspect ratio.

**2. Factor redundancy must be addressed by restructuring around truly independent axes.** a3-02 (survivor, 0.88) proved that five of six high-value factors restate the boxed definition's three words ('opaque, persistent, non-overlapping'). a3-03 (survivor, 0.81) showed this creates false confidence in borderline judgments. a1-03 (contested, 0.66) -- which defended keeping factors separate -- took the largest composite hit in the entire process. The final document must collapse redundant factors into one spatial criterion and invest the freed definitional space in genuinely independent discriminators: temporal persistence, functional role, and interaction model.

**3. The hybrid definition approach (prototype theory + one necessary condition) survives as the definitional framework.** a1-01 (survivor, 0.86) retained strong scores across all axes. However, the necessary condition (viewport partitioning, a1-02, contested at 0.80) needs explicit temporal qualification to exclude snapshot states like Diablo II's inventory screen, as demonstrated by a3-04 (survivor, 0.87). The necessary condition should read: 'viewport_area < display_surface_area, persistent across normal gameplay states within the classified view.'

**4. The definition must operate at the view/mode level, not the game level.** a3-09 (survivor, 0.87) demonstrated through the MOO2 four-view example that a single game can contain panel-frame views, modal views, and other patterns simultaneously. a3-24 (survivor, 0.81) showed players spend significant time in secondary views. The final document should classify views within games, not games as wholes, and provide guidance for multi-view games.

**5. Layout archetype selection should be driven by interaction pattern, presented as a practitioner lookup table.** a2-19 (survivor, 0.83) provides the actionable four-way mapping (commanding -> bottom triptych, catalog construction -> sidebar, canvas painting -> top toolbar, comparison -> floating windows). a2-25 (survivor, 0.85) frames this as the central organizing principle. The morphological space (a1-08, contested at 0.73) should serve as background theory for analysts, not as the primary navigation tool. Present the lookup table first; let the morphological space explain why it works.

**6. The dual-use novice/expert design principle is the single strongest practitioner proposition.** a2-09 achieved the highest composite score in the entire set (0.90). Its three concrete techniques -- hotkey letters on icons, consistent grid positions, and read-only status utility -- should be presented as mandatory guidance for any panel-frame implementation. The novice-to-expert transition the panel scaffolds (identified by a3-19, survivor at 0.82) should be explicitly acknowledged.

**7. Audio must be treated as a first-class information channel alongside visual panel design.** a2-16's three-channel taxonomy (survivor, 0.87) and a2-10's audio integration principle (survivor, 0.81) both survived strongly. a3-20 (survivor, 0.79) showed that ignoring audio systematically misestimates information costs. The final document must include an information-channel taxonomy (panel for persistent quantitative data, audio for transient event notifications, viewport overlays for spatial data) as a required design step, not an afterthought.

**8. The canon must be expanded to include a near-miss set and non-Western examples.** a3-05 (survivor, 0.86) showed the current 15-game canon only tests inclusion power, not exclusion power. a3-06 (survivor, 0.82) identified systematic exclusion of Japanese strategy games (Koei titles) with inverted information hierarchies. The final document should include: (a) Koei titles and console strategy games as cross-cultural comparisons, (b) near-miss candidates (Dungeon Keeper, Myth, Homeworld, Syndicate) to test boundary conditions, and (c) explicit acknowledgment of the definition's Western-PC-mouse scope.

**9. The three-tier factor scheme (necessary/characteristic/incidental) is structurally sound but requires disambiguated information density.** a1-06 (contested, 0.78) provides the right tiering structure, but a3-25 (survivor, 0.86) proved 'information density' is triply ambiguous (display density, control density, navigation density). Before tier assignments can be finalized, the document must specify which density type is meant for each panel element and provide measurement criteria. Additionally, a3-17 (survivor, 0.81) showed decorative surround can serve functional purposes (race identity in competitive play, perceptual boundary strength), suggesting the incidental tier needs an internal distinction between potentially-functional and purely-decorative features.

**10. The definition should explicitly scope itself to mouse-input platforms rather than claiming universality.** a2-11 (survivor, 0.86) identified four input assumptions (high-precision pointing, zero-cost context switching, screen-edge scrolling, Fitts's Law dynamics). a3-07 (survivor, 0.81) showed these assumptions reveal the definition describes 'the Western PC strategy game panel frame with mouse input.' a2-24 (survivor, 0.82) correctly provides a gating checklist and names alternative patterns for non-mouse platforms. The final document should state this scope in its opening section and provide separate, brief guidance for controller and touch adaptations.
