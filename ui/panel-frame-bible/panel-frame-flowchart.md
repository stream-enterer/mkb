# Panel Frame Design Flowchart

A decision sequence for designing a panel frame UI, distilled from the
panel frame definition.

---

## 1. Gate: Input Assumptions

Confirm all four. If any fails, do not use a panel frame.

```
[ ] High-precision random-access pointing (any pixel in one motion)
[ ] Zero-cost context switching between viewport and panel (no mode change)
[ ] Screen-edge scrolling (pointing device also navigates)
[ ] Fitts's Law dynamics (edges = infinite targets)
```

Mouse: all four satisfied. Proceed.
Controller: none satisfied. Use radial menus or other pattern.
Touch: partial (1, 2 only). Use gesture-based pattern.

---

## 2. Identify the Primary Interaction Pattern

What does the player do most?

```
Command autonomous agents ──────> RTS Bottom Triptych
  (select unit, issue order)

Build from a catalog ────────────> Right Sidebar
  (pick category, drill down,
   place sequentially)

Paint/zone a canvas ─────────────> Top Toolbar + Toolbox
  (select tool, apply repeatedly)

Compare multiple variables ──────> Toolbar + Floating Windows
  (inspect, cross-reference)

Inspect map, manage via modals ──> 4X Map Panel
  (click entity, enter modal
   for detailed management)

Read terrain/unit stats, ────────> Wargame Frame
  commit orders carefully
```

---

## 3. Set the Viewport Budget

```
Target at 1920x1080 reference:  0.80 -- 0.90
Golden-age range (640x480):     0.55 -- 0.85
```

Panel dimensions are driven by content, not ratios. Size the panel to
fit its widest content element (e.g., 160 logical px for a two-column
icon grid at 32px per icon), then the viewport gets everything else.

---

## 4. Determine Panel Placement

Based on archetype from Step 2:

```
Bottom Triptych
├── Primary panel: full-width bottom bar
├── Minimap: bottom-left CORNER (Fitts's Law: infinite target in 2D)
├── Info panel: bottom-center
├── Command card: bottom-right (near corner)
└── Optional: thin top resource bar

Right Sidebar
├── Primary panel: right edge, full height
├── Minimap: top of sidebar
├── Build menus: below minimap (vertical hierarchy)
├── Overlay toggles / advisor buttons: below menus
└── Optional: thin top resource bar

Top Toolbar + Toolbox
├── Primary panel: top edge toolbar with small icons
├── Toolbox: side or bottom, shows options for active tool
├── No minimap (viewport-as-data carries spatial info)
└── Floating windows for detailed inspection

4X Map Panel
├── Variable: right sidebar or top/bottom + side combo
├── Minimap with click-to-navigate
├── Selected-entity summary (enough to decide: drill deeper or move on)
└── High-level controls (end turn, diplomacy, tech tree)

Wargame Frame
├── Variable: right sidebar, top + side, or full border
├── Terrain info + unit stats (attack/defense/movement)
├── Turn-phase controls
└── High display density (numerical stats)
```

---

## 5. Satisfy the Characteristic Factors

Check each. All six are strong indicators; none is strictly required
beyond viewport partitioning.

```
                        NECESSARY CONDITION
                    ┌───────────────────────┐
                    │  Viewport partitioning │
                    │  viewport_area <       │
                    │  display_surface_area  │
                    │  (persistent in view)  │
                    └───────────┬───────────┘
                        Must pass.
                        If not: it is not a panel frame.
                                │
              ┌─────────────────┼─────────────────┐
              │                 │                  │
              ▼                 ▼                  ▼
     CHARACTERISTIC      CHARACTERISTIC     CHARACTERISTIC
    ┌──────────────┐   ┌──────────────┐   ┌──────────────┐
    │   Opacity    │   │  Permanence  │   │    Fixed     │
    │              │   │              │   │   Geometry   │
    │ Panels fully │   │ Panels never │   │ Panels don't │
    │ opaque. No   │   │ appear/hide  │   │ resize, drag,│
    │ game world   │   │ contextually │   │ collapse, or │
    │ visible      │   │ within the   │   │ reposition   │
    │ through them.│   │ classified   │   │ during play. │
    │              │   │ view.        │   │              │
    └──────────────┘   └──────────────┘   └──────────────┘

              ┌─────────────────┼─────────────────┐
              │                 │                  │
              ▼                 ▼                  ▼
     CHARACTERISTIC      CHARACTERISTIC     CHARACTERISTIC
    ┌──────────────┐   ┌──────────────┐   ┌──────────────┐
    │   Spatial    │   │ Information  │   │  Functional  │
    │ Exclusivity  │   │   Density    │   │    Role      │
    │              │   │              │   │Heterogeneity │
    │ No z-overlap │   │ High on at   │   │ Panels serve │
    │ between panel│   │ least one:   │   │ 2+ of:       │
    │ and viewport.│   │ - display    │   │ - telemetry  │
    │ Every pixel  │   │ - control    │   │ - control    │
    │ belongs to   │   │ - navigation │   │ - navigation │
    │ exactly one. │   │              │   │ - context    │
    └──────────────┘   └──────────────┘   └──────────────┘
```

---

## 6. Assign Information to Channels

For every piece of information the player needs, ask three questions:

```
Is it persistent or transient?
Is it spatial or abstract?
Is it player-initiated or system-pushed?

        Persistent + Abstract + Player-initiated
        ──────────────────────────────────────────> PANEL
        (resource counts, HP, unit stats,
         production queue)

        Transient + System-pushed
        ──────────────────────────────────────────> AUDIO
        ("base under attack", production complete,
         unit acknowledgment)

        Spatial + Continuous + Context-attached
        ──────────────────────────────────────────> VIEWPORT OVERLAY
        (health bars, selection circles,
         rally-point flags, coverage zones)

        Spatial + Player-toggled
        ──────────────────────────────────────────> VIEWPORT AUGMENTATION
        (data overlays: water coverage, fire risk,
         desirability -- Caesar III model)
```

Rule: no single channel carries all content types. Overloaded panel =
clutter. Overloaded audio = confusion. Overloaded viewport = noise.

---

## 7. Design for Dual Use (Novice + Expert)

Every interactive panel element must serve both populations:

```
NOVICE reads the panel           EXPERT glances at the panel
  clicks buttons to command        uses keyboard shortcuts
  discovers abilities              checks cooldowns / availability
  learns build options             monitors production state

Techniques:
  Hotkey letters printed on icons ─── visual label / binding reminder
  Consistent grid positions ──────── discoverable / muscle-memorizable
  Audio acknowledgment ───────────── confirms click / confirms hotkey
  Read-only status utility ───────── shows availability / shows state
```

The minimap retains high interaction value at all skill levels.

---

## 8. Scale for Resolution

```
1. Design at 1920x1080 reference resolution.
2. Fix panel LOGICAL dimensions (points), not pixel dimensions.
3. Scale by integer DPI factor for higher resolutions.
   (4K at 2x = same logical layout, crisper rendering)
4. All extra pixels go to the viewport.
5. Never let the viewport shrink below reference size.
6. Adjust viewport budget upward (0.80--0.90) at modern resolutions.
```

---

## Quick Checklist

```
[ ] All four input assumptions confirmed
[ ] Primary interaction pattern identified
[ ] Archetype selected from lookup table
[ ] Viewport budget set (content-driven, not ratio-driven)
[ ] Panel placement follows archetype convention
[ ] Minimap in a screen corner (if applicable)
[ ] Necessary condition met: viewport < display surface, persistent
[ ] Opacity: panels fully opaque
[ ] Permanence: panels always visible in classified view
[ ] Fixed geometry: panels do not move/resize
[ ] Spatial exclusivity: no panel/viewport z-overlap
[ ] Information density: panels justify their area cost
[ ] Role heterogeneity: panels serve 2+ cognitive functions
[ ] Information channels assigned (panel / audio / overlay / augmentation)
[ ] No single channel overloaded
[ ] Dual-use design: every element serves novice and expert
[ ] Resolution scaling: logical dimensions, integer DPI factor
[ ] Panel allocation mirrors the game's core decision structure
```
