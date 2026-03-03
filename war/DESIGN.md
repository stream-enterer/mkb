# Game Design Document

## Confirmed Axioms

### A1: Dual-Purpose Decision Trees
Strategic choices must simultaneously serve as **narrative/thematic immersion** AND **mechanical optimization**. Neither should be sacrificed for the other. (Derived from: HOI4 National Focus trees)

### A2: Flavored Modifiers as Planning Incentives
Persistent modifiers on the player's state should be **narratively named and themed**, not raw numbers. These modifiers should interact with the decision tree system (A1) to create visible "carrots" — goals the player plans toward. (Derived from: HOI4 National Spirits)

### A3: Bounded Action Economy
The player's per-turn/per-cycle agency must be **explicitly capped** to prevent micromanagement sprawl. The interesting decision is **what to prioritize**, not whether you can execute everything. (Derived from: Old World orders system)

### A4: No Logistics Micromanagement
Supply, transport, and logistics should either be **abstracted**, **automated**, or **implicit in other systems**. The player should never manually route supply lines or manage transport networks. (Derived from: dislike of HOI4 army logistics)

### A5: Named Archetypes Over Atomic Customization
Units/equipment/entities should have **preset identities** (real or fictional named types) rather than being built from atomic components. The player should think "I want a StuG III" not "I want a heavy chassis + 7.5cm gun + X armor." (Derived from: dislike of HOI4/Stellaris/SMAC designers)

### A6: Modular Customization Within Locked Chassis
Customization exists but operates at the **loadout/outfit level** on top of a fixed core identity. Swap weapons, add subsystems, tune allocations — but the *thing itself* is pre-defined. (Derived from: Starsector outfitting, BTA3062 MechEngineer)

### A7: Emotionally Engaging AI Actors
AI-controlled nations must be **characters the player forms real feelings about** — protective loyalty toward allies, genuine animosity toward enemies. This requires AI actors to have visible personality, consistent motivations, and memorable behavior — not just optimizing hidden utility functions. (Derived from: "I want the player to care about their allies and hate their enemies")

### A8: Modern/Near-Future Warfare Setting
The setting is the **contemporary geopolitical moment**: nuclear deterrence as a ceiling on escalation, drone warfare as the rapidly evolving tactical edge, erosion of the post-WW2 rules-based international order, and decapitation strikes against leadership as an alternative to conventional ground invasion. (Derived from: explicit setting choice)

### A9: Turn-Based with Orders
Turn-based is confirmed, and is a structural requirement of A3 (Bounded Action Economy / Orders system). The turn boundary is what makes prioritization meaningful. (Derived from: Old World dependency + explicit confirmation)

### A10: Nation-Level Grand Strategy
The player controls a **nation-state** across three interlocking layers: **geopolitical** (diplomacy, alliances, international standing), **military** (force projection, deterrence, conflict), and **economic** (production, trade, development). All three layers are present; their relative weight and interaction is TBD. (Derived from: explicit scope choice)

### A11: Global Sandbox Simulation
The game is a **sandbox**, not a scenario. The entire world is simulated. Any nation is playable, from a one-province minor to a superpower. The game is not about a specific conflict or operation — it is about the full possibility space of geopolitics. (Derived from: "I love the global sandbox concept")

### A12: Historical Start, Open Future
The simulation begins at a **historically grounded start date (~2020)** with real nations, leaders, relationships, and conditions (including COVID as a starting condition). From that point forward, history is **unscripted** — the simulation diverges based on AI and player decisions. Campaign length is measured in **years to decades**, Paradox-style. (Derived from: explicit temporal scope)

### A13: Persistent Nation, Mutable Leadership
The player **is the nation**, not the leader. Heads of state change through elections, coups, assassinations, term limits, etc. The player can release nations, potentially switch nations. Player continuity is national, not personal. (Derived from: "think somewhere in the realm of HOI4")

### A14: AI Legibility Through Action, Not Prose
AI personality and intent must be readable through **observable behavior** — troop movements on the map, diplomatic pivots, economic decisions, alliance shifts — not through written event text or flavor prose. Brief, in-character communications are good ("We're being attacked, please help!"). Lengthy narrative events are not. **Show, don't tell.** (Derived from: Escape Velocity example, explicit rejection of prose-heavy approaches, CK3 criticism)

### A15: Decentered Player — Living World
The simulation must feel like it **exists independently of the player**. AI actors have pre-existing relationships, ongoing conflicts, and agendas that the player discovers and navigates rather than triggers. The player is **one actor among many** in a world that is already in motion. The emotional resonance comes from stepping into a living system and finding your place in it. (Derived from: Escape Velocity "pirates attacking merchants" kernel — the event was already happening, you just arrived)

### A16: No Win Condition — Small Victories as Stopping Points
There is **no overall victory**. The game provides themed, optional sub-objectives ("small victories") that serve as **satisfying stopping points** — moments where a player can say "I did the thing" and feel closure without being forced to continue. Players may also set entirely self-directed goals. The anti-pattern is world conquest / total map painting: tedious, time-consuming, and uninteresting. (Derived from: explicit design philosophy, TW:WH3 Expanded Victory Conditions reference)

### A17: Sandbox as Political Expression
The game must be **expressive enough** that players can use it to explore, comment on, or respond to real-world political situations through gameplay. Playing as Greenland to annex the US in response to real-world politics IS the game working as intended. The sandbox is a medium for political imagination and "what-if" exploration grounded in reality. (Derived from: Florryworry/Greenland example — "this is VERY IMPORTANT to me")

### A18: Military Curation, Not Construction
The player's relationship to military systems is **curatorial**: choosing from a catalog of real-world named systems (and speculative extensions as the timeline progresses), like building an MTG Commander deck. The pleasure is in **selecting, combining, and fielding** — not in designing from parts. Real systems at game start (F-35, Bayraktar TB2, S-400, Leopard 2A7); speculative-but-grounded systems as the game diverges from history. (Derived from: MTG Commander analogy, "lean HARD on real-world systems")

### A19: Deep Political Transformation Through Decision Chains
The political decision system must enable **radically different political outcomes** for any nation — not through a single government-swap button (Civ anti-pattern) but through **chains of meaningful decisions** that accumulate into transformation. How this scales to 190+ nations is an **open design space**, not a problem to minimize. (Derived from: explicit rejection of shallow government switching, enthusiasm for scaling challenge)

### A20: Systems Primacy with Constrained Agency
The game's simulation assumes that **historical outcomes are produced by systemic conditions** — economic structures, demographics, geography, institutional configurations — not by exceptional individuals. Leaders are expressions of the systems that produce them. Individuals have **real but constrained choice space** within systemic boundaries. The player's challenge is to understand, navigate, and — with great effort — reshape these systems. (Derived from: explicit philosophical position — "Great Man theory is false, it's all about SYSTEMS")

### A21: The Assumption Gap as Core Experience
The game's central experiential loop is: **Player imports real-world assumptions → acts on them → transparent systems produce honest consequences → consequences diverge from assumptions → player updates their mental model.** There is no randomness or misdirection. All mechanics are fully transparent and legible. The "surprise" comes entirely from the gap between what the player EXPECTED (based on inherited biases) and what the systems ACTUALLY PRODUCE. This gap is where insight, emotion, and fun live. (Derived from: "we get to SEE what actually happens... full mechanic transparency but CHALLENGING OF THE PLAYER'S INHERITED ASSUMPTIONS")

### A22: Named Leaders as Emotional Import Points
Real-world named leaders (Putin, Biden, Xi, etc.) exist in the game and serve as **anchor points where the player imports real-world emotions and assumptions**. The game neither confirms nor denies these imported feelings — it simulates the systemic conditions around those leaders and lets consequences speak. The player WILL have opinions on Putin regardless of his modifier stack. The tension between "how the player feels about a leader" and "what the systems actually produce through that leader" is a feature, not a bug — it fuels A21. (Derived from: "the player is still going to see someone called Vladimir Putin and have OPINIONS ON HIM")

### A23: Template Diversity Over Template Volume
The political decision system (and event/content systems generally) should be built on a **library of structurally distinct templates** instantiated with historically researched specifics. Quality comes from **template diversity** (many genuinely different structural patterns), not from volume of instances of the same pattern. LLM-assisted research can expand the breadth of historically grounded instances, but the design work is in the templates themselves. The anti-pattern is "oatmeal" — 500 instances of the same structure with different names. (Derived from: EU4 Neumark analysis, LLM content generation discussion)

### A25: Decisions Create Situations, Not Increments
Every player decision should **create a new situation with its own internal tension**, not merely increment a counter or queue a timer. The pattern is: **Commitment → emergent tension → contextual dilemma.** Prior decisions should constrain and enrich future options — your past build affects what you can do now, and that's the fun. The anti-patterns are: clicking the optimal province for a building (optimization without tension), queuing an 8-turn build (commitment without agency during the wait). The positive pattern is: CK3 tournaments (you built combat → you chose to attend → now your prior choices create a dilemma about how hard to push). Quality over quantity of decisions; dilemmas over optimizations. (Derived from: EU4 estates vs buildings, Civ build queues, CK3 tournament/character build layering)

### A26: Economy as Observable System with Selective Intervention
The economic layer is primarily a **complex system the player watches running** — visible data streams, updating indicators, flowing resources — with **occasional, high-impact policy interventions** that cost orders. The player does not micromanage tax percentages or click buildings into provinces. When the player DOES intervene, each intervention should feel like a dilemma (A25), not an optimization. The economy runs every turn whether or not the player touches it (A15). (Derived from: "observe, then selectively intervene"; enjoyment of watching complex systems operate; dislike of micromanagement)

### A27: Card-Slot Interaction Model (Core Mechanic)
The game's primary decision interface is a **card-and-slot system** that operates at two levels:

**Level 1 — Nation Build (Civ4 Civics-like):** The player's nation has **institutional/structural slots** (categories defined by government type, national circumstances, etc.) into which civic/policy choices are slotted. This combination defines the nation's **character and identity**, and the player becomes attached to their specific build. Different nations start with different slot structures. Political transformation (A19) changes the slots themselves.

**Level 2 — Situation Response (Cultist Simulator-like):** When situations arise (crises, opportunities, dilemmas), they present **slot structures** that the player fills with **cards from their accumulated collection**. Some situations require cards from multiple domains (Cultist Simulator operations-style), creating a resource allocation puzzle: "I have 3 slots and 7 candidate cards — which combination?"

**Cards are broader than actions.** They represent **everything that constitutes what your nation IS and what it CAN DO**:

- **Active cards**: capabilities you deploy into situations (launch covert op, issue executive order, deploy military system)
- **Passive cards**: persistent modifiers that shape your state (National Spirits — A2 was already this concept). May have active/passive modal toggle.
- **Entity cards**: institutions, factions, estates, non-governmental power structures (oligarchs, corporations, religious bodies, unions) that are **deeply embedded in gameplay** with their own dynamics, advantages, and disadvantages — like EU4 Estates, not optional flavor
- **Expendable cards**: one-time leverage, crisis responses, diplomatic favors — consumed on use

**Unifying insight:** A2 (National Spirits) = passive cards. A18 (Military Systems) = a card category. A1 (Focus Tree rewards) = cards you acquire. These were always the same system.

The combination of your Level 1 build + accumulated Level 2 cards IS your nation's identity. This is why the player feels attached — it's THEIR build, not just a flag on a map. (Derived from: Shadow Empire action cards, Cultist Simulator verb-object interactions, Civ4 civics slotting, EU4 estates, explicit synthesis across multiple discussions)

### A28: Government Type Determines Control Surface
Different government types give the player **different relationships to their own cards**. In a democracy, some institutions act autonomously (the central bank sets its own rates, the judiciary rules independently) — these cards are **automated by the system**. In an autocracy, the player has **direct control** over more cards but may have fewer total institutional cards (because independent institutions have been dismantled). The player literally experiences the difference between governing systems through what they can and cannot control. (Derived from: gap analysis — "depending on government type certain things are automated or player-controllable")

### A29: Non-Governmental Actors as Embedded Entity Cards
Corporations, oligarchs, media organizations, religious institutions, unions, criminal networks, militias, and similar non-governmental power structures are **entity cards deeply embedded in gameplay** — not background flavor. They provide advantages AND disadvantages, have their own dynamics (loyalty, influence, demands), and interact with the institutional structure. Comparable to EU4 Estates: load-bearing parts of the system with real mechanical teeth. (Derived from: "I'd argue they're more like Estates in EUIV... deeply embedded in how the game works")

### A30: Non-State Actors as Independent Simulation Entities
Non-state actors (Hezbollah, Houthis, cartels, PMCs, transnational networks) are **independent entities in the simulation** with their own territory, goals, and capabilities. They are NOT inherently cards in any single player's hand. A nation's RELATIONSHIP to a non-state actor determines how it manifests mechanically:

- **Patron relationship** (Iran → Hezbollah): Shows up as a deployable proxy-asset card. But the entity has its own interests and isn't perfectly obedient.
- **Host relationship** (Mexico → Sinaloa Cartel): Shows up as a hostile/ambivalent entity card you're forced to manage — an estate with low loyalty.
- **No relationship** (US → Sinaloa Cartel): Not in your hand at all — part of the simulation that generates situations you react to.
- **Relationships can be cultivated, lost, or stolen** through diplomatic, intelligence, and military actions.

This gives **proxy warfare** a natural mechanical expression: deploying your non-state actor cards into situations on someone else's territory. (Derived from: Houthis/Hezbollah/Cartel analysis — "the same entity is different things to different players")

### A31: Symmetric Rules for All Actors
All nations in the simulation — player and AI-controlled — operate under **identical mechanical rules**. AI nations hold the same types of cards, face the same situations, and are subject to the same constraints (including bounded action economy, A3) as the player. There are no hidden bonuses, difficulty-scaling resource cheats, or asymmetric mechanics. All differences between nations emerge from **starting conditions, systemic position, and decisions made within the shared rules** — not from the rules themselves. This directly serves A21: the player can reason about AI behavior using the same mechanical understanding they apply to their own decisions, because the mechanics ARE the same. Surprises come from the system, not from hidden advantages. (Derived from: explicit design philosophy — "I don't like hardcoded resource-cheating AIs... I like the entire game to be equal adversaries under the rules")

---

## World Model: Actors — Attributes — Systems — Space (AASS)

*The foundational taxonomy of what the simulation contains and how it behaves — the game's **world-state layer**. Derived from first-principles analysis, adversarial stress-testing (49 critiques), and design-relevance filtering (13 retained). The card-slot model (A27) is a separate **interaction-mechanics layer** through which all actors (player and AI alike, per A31) engage with this world state.*

### Actors
**Entities with interests that take or can take purposive action.**

| Subcategory | Examples | Notes |
|-------------|----------|-------|
| Sovereign States | USA, Russia, Iran, Greenland | Primary game unit; the player controls one |
| International Organizations | NATO, UN, EU, IMF, OPEC | Can also manifest as Systems (dual role) |
| Sub-state Political Entities | Political parties, separatist movements, provincial govts | Internal to nations; shape domestic politics |
| Non-state Armed Groups | Houthis, Hezbollah, PMCs, insurgencies | Independent entities per A30 |
| Economic Actors | Multinational corps, sovereign wealth funds, major banks | Can span multiple nations |
| Transnational Networks | Diasporas, criminal networks, ideological movements | Operate across borders |

**Design notes:**
- Actors can **contain** other actors (NATO contains member states; a state contains political parties). Nesting is modeled through relational attributes.
- Actors can **degrade** — a failing state can lose coherence and become primarily a spatial condition (ungoverned territory) rather than a sovereign agent.
- Actors can **partially capture** systems — the US has disproportionate leverage over SWIFT, Saudi Arabia over oil markets. "No one owns systems" is false; influence over systems is a key strategic variable.

### Attributes
**Properties, resources, capabilities, and conditions that characterize actors and the world state. The primary world state from which the card-slot model (A27) generates cards — what a nation IS and CAN DO at the ontological level.**

| Subcategory | Examples | Card role |
|-------------|----------|-----------|
| **Capabilities/Assets** | F-35 squadrons, nuclear arsenal, semiconductor fabs, cyber tools, satellite constellation | Active cards — things you deploy |
| **Demographics** | Population size, age structure, urbanization, ethnic composition, education level | Simulation substrate that generates condition cards |
| **Political Conditions** | Regime type, domestic political cohesion, public opinion, institutional quality, polarization | Constrains which cards can be played; generates political situation slots |
| **Ideational Attributes** | State ideology, religious composition, cultural soft power, normative commitments | Passive cards shaping all interactions; motivation for AI actors |
| **Economic Attributes** | GDP, industrial base, resource endowment, debt level, trade dependencies | Foundation-layer simulation variables; constrain military and political options |
| **Relational Attributes** | Alliance memberships, rivalries, dependencies, treaty obligations, reputation, proxy relationships | Diplomatic cards; define actor-to-actor connections |

**Design notes:**
- Attributes map onto the **Simulation Variable Hierarchy** (A24): Space provides bedrock; Economic and Demographic Attributes are the foundation layer; Political, Ideational, and Capability Attributes are derived layers.
- **Power** is not a category — it is a **derived variable** computed from the configuration of Attributes + System position. It does not need to be a card; it needs to be calculable.
- The same real-world resource can appear in multiple categories: oil *deposits* are Space, the oil *market* is a System, a nation's oil *reserves and extraction capacity* are an Economic Attribute. This deliberate multi-faceting is a feature, not a bug.

### Systems
**Structures, institutions, patterns, and flows that connect actors and constrain their behavior. Systems exist BETWEEN and ABOVE nations — they are the global layer that no single actor owns (though some have disproportionate leverage).**

| Subcategory | Examples | Mechanical behavior |
|-------------|----------|-------------------|
| **Institutional Systems** | WTO, international law, treaty regimes, financial regulations | Can be built, reformed, captured, or dismantled through actor action |
| **Infrastructure Systems** | Global shipping network, internet backbone, SWIFT, energy pipelines, GPS | Physical/technical connectivity; can be built, damaged, disrupted, or controlled |
| **Market/Exchange Systems** | Global financial markets, commodity markets, labor markets, arms markets | Emergent from actor interactions; can be influenced but not directly controlled; subject to systemic risk and cascading failure |
| **Normative Systems** | Non-proliferation norm, nuclear taboo, human rights regime, sovereignty norms | Can be reinforced or eroded through actor behavior; shape what actions are "legitimate" |
| **Environmental/Physical Systems** | Climate system, ocean currents, disease ecology, resource depletion dynamics | Largely exogenous to actor control; impose constraints and generate crises |

**Design notes:**
- The five subtypes are **mechanically distinct** — they respond to actor action differently. You can capture an institutional system; you can't capture the climate. You can disrupt infrastructure; you can't disrupt a market norm. This matters for card-slot interactions.
- Systems interact with Actors through **leverage and position**. A nation's position within a system (e.g., US position in global financial infrastructure) is a Relational Attribute that produces cards.
- Normative Systems are where **ideology-as-structure** lives (distinct from ideology-as-actor-property, which is an Ideational Attribute). The liberal international order is a Normative System. A nation's commitment to liberalism is an Ideational Attribute.

### Space
**The physical and informational terrain on which everything operates. The most slowly-changing layer — the board the game is played on.**

| Subcategory | Examples |
|-------------|----------|
| **Physical Geography** | Landmasses, oceans, mountains, rivers, climate zones, resource deposits |
| **Political Geography** | Borders, territorial claims, EEZs, occupied territories, disputed zones |
| **Infrastructure Geography** | Transport networks, communication cables, energy grid topology — the physical substrate under Infrastructure Systems |
| **Informational/Virtual Space** | Cyberspace, media environments, information ecosystems |
| **Strategic Domains** | Land, sea, air, space, cyber — as operational theaters for military action |

**Design notes:**
- Space is **bedrock** in the A24 hierarchy. It constrains everything but rarely changes.
- Space determines the **possibility space**: what's adjacent, accessible, defensible, resource-rich.
- Space is what cards operate ON and situations arise WITHIN. It is the context for card-slot resolution.

### AASS Interaction Edges
*How the four categories relate to each other — the "verbs" between the "nouns."*

| Interaction | Description |
|-------------|-------------|
| **Actor ↔ Attribute** | Actors possess Attributes. Attributes enable and constrain actor action. Cards are primarily drawn from Attributes. |
| **Actor ↔ System** | Actors participate in, influence, capture, build, undermine, or are constrained by Systems. Actor position within Systems produces Relational Attribute cards. |
| **Actor ↔ Space** | Actors occupy, control, contest, and project power across Space. Space constrains and enables action. |
| **System ↔ Attribute** | Systems shape what Attributes are possible (trade systems affect economic attributes). Attributes determine system participation and leverage. |
| **System ↔ Space** | Systems operate across Space. Spatial conditions enable or constrain system function (a pipeline needs physical geography). |
| **Attribute ↔ Space** | Demographics are distributed across Space. Resources are located in Space. Capabilities are projected across Space. |

### How AASS Maps to the Card-Slot Model (A27)

**AASS and the card-slot model are different architectural layers.** AASS is the **world-state layer** — it describes what exists and what is true about the world. The card-slot model (A27) is the **interaction-mechanics layer** — it defines how actors engage with and change the world state. Per A31, all actors (player and AI) interact through the same card-slot mechanics under the same rules.

This distinction matters because:
- **The two layers serve different purposes** — AASS must be *ontologically complete* (capture everything that exists and matters). The card-slot system must be *mechanically coherent* (provide legible, balanced interaction rules for all actors within A3's bounded agency).
- **The same world state can produce different card surfaces for different actors** — A30 already demonstrates this: Hezbollah is a different card (or no card at all) depending on a nation's relationship to it, but it is the same AASS entity regardless. This applies symmetrically to all actors.
- **Government type (A28) configures each actor's card availability** — it determines which cards are directly controllable and which are automated, for player and AI nations alike.
- **The player-specific element is the UI/UX presentation, not the mechanics.** What the player sees on screen is a rendering of their cards and situations. The underlying card-slot mechanics are universal — every nation has cards, faces situations, and operates under the same rules (A31).

The mapping from world state to cards:

**Cards** are drawn from:
- **Attributes** (primary source): your capabilities, political conditions, ideational character, economic tools, relational leverage
- **Actors** (secondary): allied actors, sub-state factions, proxy relationships you can leverage
- **Systems** (tertiary): institutional memberships, system positions, infrastructure access

**Slots** (situations) are generated when:
- Systemic conditions cross thresholds (Market System instability triggers economic crisis slot)
- Actor interactions create friction (rival Actor's Relational Attributes conflict with yours)
- Spatial conditions change (territorial dispute, resource discovery, climate event)
- Attribute trajectories collide (demographic pressure + economic stagnation + political polarization → instability slot)

**Resolution** of card-slot interactions is determined by:
- The cards' Attribute values
- The System context (which systems are relevant, who has leverage)
- The Space context (geographic and strategic constraints)
- Other Actors' responses (their cards in the same or related slots)

---

## A24: Simulation Variable Hierarchy (Revised)
The simulation's underlying variables are organized in a **layered hierarchy** with both **national** and **global** dimensions:

| Layer | National (per-state) | Global (shared) |
|-------|---------------------|-----------------|
| **Bedrock** (static/near-static) | Physical Geography, resource deposits, climate zone | Trade route geography, global resource distribution, ocean access |
| **Foundation** (slow-moving, years/decades) | **Economic structure** (lynchpin), demographic structure, institutional quality | Global economic order, financial infrastructure, major alliance architecture |
| **Derived** (faster-moving, shaped by foundation) | Military-industrial capacity, political conditions, ideational character, information environment | International norms, technology frontier, global information environment |

The player mostly interacts with derived layers turn-to-turn, but the foundation layer determines long-term outcomes. Global layers constrain and connect national layers — a nation's economy exists WITHIN the global economic order. This maps to A20: the player can push on surface variables, but deep structural reality (both national and global) resists.

(Revised from original A24 to incorporate AASS global layer and Attribute categories. Derived from: discussion of economics as lynchpin, globalization analysis, AASS taxonomy development)

---

## Thesis Statement

> *A global sandbox where you govern a real nation, import your real-world assumptions about how geopolitics works, and then watch transparent systems either validate or demolish those assumptions through honest consequences.*

The game is an **argument in interactive form**: that systemic conditions — not great men — produce historical outcomes, and that the gap between what you expect and what actually happens is where insight lives.

---

## Open Design Spaces

*Areas explicitly flagged as needing further exploration. These are not problems — they are where the interesting design work lives.*

### D1: Temporality and Turn Structure — DEFERRED
The implicit assumption that turns represent fixed calendar periods has been **challenged and found unjustified** — nothing in the confirmed axioms requires it. The modern setting creates a timescale problem: drone strikes happen in minutes, demographic shifts take decades. Fixed calendar turns either compress or stretch everything awkwardly.

**Candidate models to explore when revisiting:**
- **Fixed long periods with limited mid-turn interventions**: Turns are long (years?), but you get interrupt opportunities for crises within them
- **Abstract duration categories**: Effects are tagged short/medium/long rather than tied to calendar months
- **Asynchronous/fragmented turns**: Decision points aren't evenly spaced; the simulation drives when you act
- **Event-driven cycles**: Simulation runs until enough situations accumulate to present a decision point; time is a consequence, not a clock

**What IS confirmed:** Turns exist (A9), agency per turn is bounded (A3), and the turn boundary forces commitment (A3/A9). What a turn REPRESENTS temporally is open.

**Status: DEFERRED. Revisit after core card-slot mechanics and at least one game layer (military, economic, or diplomatic) are concretely designed, since those will constrain what temporal model works.**

### D2: Military Layer — The "Deck-Building" Verb
A18 establishes the philosophy (curation, not construction). A27 provides the interaction model. AASS clarifies that military systems are **Capability/Asset Attributes** fielded as cards into conflict slots. The remaining question: what does military curation look like concretely? How do you acquire systems, what does your military "hand" look like, and what are the slot structures for military situations? **Status: AASS provides the ontological grounding; concrete mechanics needed.**

### D3: Card Taxonomy and Slot Patterns
The card-slot architecture is confirmed (A27). AASS provides the **source categories** for cards (Attributes primarily, Actors and Systems secondarily).

**Confirmed mechanics (Situation behavior):**

**Situations are slot structures that arise from the simulation.** They vary along two independent dimensions:

- **Demand:** Some situations **force** card commitment (the crisis is happening, something WILL occupy your cards). Others are **optional** opportunities you can engage with or ignore. The mix of forced and optional situations is where tension lives.
- **Temporality:** Situations vary in time pressure:
  - **Immediate:** Procs and demands card commitment this turn.
  - **Windowed:** Procs and gives you X turns to respond, with the option to respond early any turn within that window. This is advance warning — you see the consequence coming and can plan for it.
  - **Multi-turn unfolding:** The situation itself advances or transforms across turns. This is distinct from a windowed deadline — it's an ongoing process where you may commit cards across multiple turns as it evolves.
  - These can overlap: a situation can give a window for initial commitment, then unfold over subsequent turns.

**Slotting a card into a situation does not imply resolution.** Possible outcomes include: the situation advancing or transforming into a new situation, side effects spawning further situations elsewhere, the original situation closing (one outcome among many, not the default). This directly implements A25 — decisions create new situations with their own tension.

**Cards can only be in one place at a time.** This is the core scarcity mechanic. Committing a card to one situation makes it unavailable for others. Multi-turn situations lock cards across turn boundaries, meaning long commitments (e.g., military deployments) reduce your available cards for subsequent turns.

**Two independent scarcity dimensions constrain the player:** A3's bounded action economy caps how many cards you can slot per turn. The one-place rule caps which cards are available at all. These compound — you're constrained both by orders and by card availability. This is load-bearing for difficulty and tension.

**Three card expenditure modes coexist within the same system:**
- **Consumed:** Card is spent and gone (expendable resources, one-time favors).
- **Occupied:** Card is locked into a situation while it resolves, then returned. Unavailable for other use during occupation.
- **Transformed:** Card goes in as one thing, comes back as something different. The input card is gone; a new card is produced.

**Edge case to address in tuning:** If enough forced situations fire simultaneously, the player could run out of available cards. This is a legitimate "you're overwhelmed and losing" state, but may need a safety valve depending on how card counts and situation frequency feel in practice. This is a balance question, not a design flaw.

**Remaining open questions:**
- **Slot shape filtering:** Whether situations require specific card aspects/tags (strict filtering) or are open-ended ("put whatever you want, we evaluate what happens") is explicitly **open and can vary per situation type**.
- What are the concrete card types within each AASS Attribute subcategory?
- How do the two levels (nation-build slots vs. situation-response slots) interact?
- How are cards acquired, lost, and transformed through gameplay progression?
- What are the structurally distinct slot patterns (A23 template diversity applied to situations)?

**Status: Situation mechanics confirmed. Card taxonomy and slot pattern design are the next major task.**

### D4: Economic Layer
Identified as the **lynchpin** of the simulation (A24). A26 establishes the player verb: observe, then selectively intervene. AASS clarifies that the economy spans multiple categories: Economic Attributes (national), Market/Exchange Systems (global), and Infrastructure Geography (spatial). **Remaining questions:** What does the economic simulation look like as a spectacle? How does economic capacity constrain military procurement and political options? What are the high-impact economic intervention cards? **Status: Architecture resolved. Spectacle and card design needed.**

### D5: Combat Resolution
When two nations go to war in a world with nuclear deterrence, what happens mechanically? AASS frames this as: Capability/Asset Attribute cards deployed into conflict slots, resolved within System context (alliance systems, normative systems like the nuclear taboo) and Space context (strategic geography). **Remaining questions:** Auto-resolve vs. map-based? Escalation mechanics? How does nuclear deterrence mechanically constrain conventional warfare? **Status: Ontologically grounded. Mechanics not yet explored.**

### D6: Diplomatic/Geopolitical Layer
Alliances, treaties, sanctions, proxy wars, information warfare. AASS frames diplomacy as operating through **Relational Attributes** (actor-to-actor connections), **Institutional Systems** (UN, treaty regimes), and **Normative Systems** (sovereignty norms, international law). **Remaining questions:** What subset of diplomatic tools matters most? How does it interact with A7 (emotionally engaging AI) and A14 (legibility through action)? **Status: Ontologically grounded. Mechanics not yet explored.**

### D7: The "Small Victories" System
A16 establishes that themed sub-objectives serve as stopping points. **Remaining questions:** What generates them? Per-nation? Procedural from Attribute conditions? How do they interact with the political decision system (A19/D3)? Can the player define their own? **Status: Not yet explored.**

### D8: Focus Tree / Decision Tree Architecture
A1 establishes dual-purpose decision trees. A19 requires deep political transformation. A23 requires template diversity. A27 implies focus trees are a primary mechanism for **acquiring and transforming cards**. AASS grounds the templates in Attribute conditions. **Remaining questions:** What does a focus tree look like in this game? How does it interact with the card-slot system? Is it a tree, a web, or something else? How does it generate cards from systemic conditions? **Status: Principles established. Structural design not yet attempted.**

---

## Resolved Questions

*Previously open questions that have been answered through discussion.*

| # | Question | Resolution |
|---|----------|------------|
| Q1 | Genre/Scale | Nation-level grand strategy (A10) |
| Q2 | Setting | Modern/near-future warfare (A8) |
| Q3 | Real-time vs Turn-based | Turn-based with orders; hard dep from A3 (A9) |
| Q4 | Single/Multiplayer | Single-player with emotionally engaging AI (A7) |
| Q5 | Victory condition | No overall victory; small victories as stopping points (A16) |
| Q6 | Temporal scope | Years to decades from ~2020 start (A12) |
| Q7 | Geographic scope | Full globe, any nation playable (A11) |
| Q8 | Player identity | The nation; leaders are mutable (A13) |
| Q9 | Source of emotional engagement | Observable AI behavior + player-imported assumptions, not prose (A14, A21, A22) |
| Q10 | Hand-crafted vs procedural content | Condition-driven templates with diverse structures (A23, A24) |
| Q11 | Foundational philosophical assumption | Systems primacy with constrained agency (A20) |
| Q12 | Core simulation variable | Economic structure as lynchpin (A24) |
| Q13 | Economic player verb | Observe complex system, selectively intervene with high-impact dilemmas (A26) |
| Q14 | Decision interaction model | Card-slot system: accumulated capabilities slotted into situation structures (A27) |
| Q15 | Decision quality principle | Decisions create situations, not increments; dilemmas over optimizations (A25) |
| Q16 | Player identity (mechanical) | Acceptable abstraction — you are "the nation," not a specific character (A13) |
| Q17 | Non-governmental actors | Deeply embedded entity cards with mechanical teeth, like EU4 Estates (A29) |
| Q18 | Compound decisions | Situations can require cards from multiple domains; resource allocation puzzle (A27) |
| Q19 | Government type impact on gameplay | Controls which cards are automated vs player-controllable (A28) |
| Q20 | What cards represent | Broader than "actions" — everything your nation IS and CAN DO (A27 revised) |
| Q21 | Card system as unifying mechanic | National Spirits, military systems, focus rewards, estates all unified as card types (A27) |
| Q22 | Non-state actors | Independent simulation entities; relationship determines card manifestation (A30) |
| Q23 | World model taxonomy | Actors — Attributes — Systems — Space (AASS); adversarially tested |
| Q24 | Where cards come from | Primarily Attributes, secondarily Actors and Systems; Space provides context |
| Q25 | How globalization is modeled | Global Systems layer parallel to national layers; nations embedded within shared systems; system leverage is a key variable |
| Q26 | Situation demand model | Situations are either forced (demand card commitment) or optional (opportunities); the mix creates tension (D3) |
| Q27 | Situation temporality | Immediate, windowed (X turns to respond), or multi-turn unfolding; can overlap (D3) |
| Q28 | What slotting a card produces | Advancement, transformation, side-effect spawning, or closure — resolution is one outcome, not the default (D3, A25) |
| Q29 | Card positional scarcity | Cards can only be in one place at a time; occupation across turn boundaries is possible (D3) |
| Q30 | Dual scarcity model | Player constrained by both per-turn order cap (A3) and card availability (one-place rule); these compound (D3) |
| Q31 | Card expenditure modes | Three modes coexist: consumed (gone), occupied (locked then returned), transformed (becomes different card) (D3) |
| Q32 | World state vs interaction mechanics | AASS is the world-state layer (what exists). The card-slot model is the interaction-mechanics layer (how all actors engage with world state). Both are universal per A31; the player-specific element is the UI/UX presentation, not the mechanics. |
| Q33 | AI mechanical symmetry | All nations operate under identical rules. No hidden bonuses or asymmetric mechanics. Differences emerge from starting conditions and systemic position, not from the rules themselves (A31). |
