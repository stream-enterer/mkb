# Game Design Document

## Epistemic Status Key

Every confirmed design decision is tagged with one of the following:

| Tag | Meaning | Revisable by... |
|-----|---------|-----------------|
| **A** | **Axiomatic** — First-principle commitment from explicit discussion. Not derivable from other axioms. | Direct reconsideration of the commitment. |
| **D** | **Derived** — Follows logically from specified axioms. If those axioms hold, this must hold. | Revising the source axioms. |
| **E** | **Extension** — Confirmed through discussion. Consistent with axioms but not strictly required by them. | Design decision; can be revised without violating any axiom. |

Items in Open Design Spaces are **unresolved** unless explicitly tagged otherwise.

---

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

### A24: Simulation Variable Hierarchy
The simulation's underlying variables are organized in a **layered hierarchy**: bedrock (geography, near-static) → foundation (economic structure, demographics — slow-moving, years/decades) → derived (military, political, ideational — faster-moving). Both national and global dimensions exist at each layer. The foundation layer determines long-term outcomes; the player mostly interacts with derived layers turn-to-turn. *(Full treatment with table: see expanded A24 section below.)*

### A25: Decisions Create Situations, Not Increments
Every player decision should **create a new situation with its own internal tension**, not merely increment a counter or queue a timer. The pattern is: **Commitment → emergent tension → contextual dilemma.** Prior decisions should constrain and enrich future options — your past build affects what you can do now, and that's the fun. The anti-patterns are: clicking the optimal province for a building (optimization without tension), queuing an 8-turn build (commitment without agency during the wait). The positive pattern is: CK3 tournaments (you built combat → you chose to attend → now your prior choices create a dilemma about how hard to push). Quality over quantity of decisions; dilemmas over optimizations. (Derived from: EU4 estates vs buildings, Civ build queues, CK3 tournament/character build layering)

### A26: Economy as Observable System with Selective Intervention
The economic layer is primarily a **complex system the player watches running** — visible data streams, updating indicators, flowing resources — with **occasional, high-impact policy interventions** that cost orders. The player does not micromanage tax percentages or click buildings into provinces. When the player DOES intervene, each intervention should feel like a dilemma (A25), not an optimization. The economy runs every turn whether or not the player touches it (A15). (Derived from: "observe, then selectively intervene"; enjoyment of watching complex systems operate; dislike of micromanagement)

### A27: Card-Slot Interaction Model (Core Mechanic)
The game's primary decision interface is a **card-and-tableau system**. Each actor's strategic position is represented as a **tableau of cards** — visible, specific, and scarce. Situations arise from the simulation as cards with conditions for change (Q43), and actors respond by committing cards from their tableau into sub-slots, making modal choices, or letting situations auto-progress (Q44). Alongside actor tableaux, situations that inherently involve multiple actors exist in a **shared situation space** (A33) — a second zone where no single actor owns the situation, and multiple actors can commit cards to the same situation's sub-slots.

**Cards are broader than actions.** They represent **everything that constitutes what your nation IS and what it CAN DO**. The concrete taxonomy of card types is an **open question** (see D3).

**Unifying insight:** A2 (National Spirits), A18 (Military Systems), A1 (Focus Tree rewards), and A29 (non-governmental actors/estates) are all cards in the same tableau. These were always the same mechanic.

**National identity emerges from your tableau.** Your specific persistent cards, the decisions you've made through A19 chains, and how A28 configures your control surface — this combination is your nation's identity. The player becomes attached because it's THEIR build: their military, their institutions, their relationships, their political path. No dedicated civic-slot structure is needed; identity is the accumulated state of the tableau and the simulation beneath it. (Derived from: Shadow Empire action cards, Cultist Simulator verb-object interactions, EU4 estates, explicit synthesis across multiple discussions)

### A28: Government Type Determines Control Surface
Different government types give the player **different relationships to their own cards**. In a democracy, some institutions act autonomously (the central bank sets its own rates, the judiciary rules independently) — these cards are **automated by the system**. In an autocracy, the player has **direct control** over more cards but may have fewer total institutional cards (because independent institutions have been dismantled). The player literally experiences the difference between governing systems through what they can and cannot control. (Derived from: gap analysis — "depending on government type certain things are automated or player-controllable")

### A29: Non-Governmental Actors as Embedded Entity Cards
Corporations, oligarchs, media organizations, religious institutions, unions, criminal networks, militias, and similar non-governmental power structures are **entity cards deeply embedded in gameplay** — not background flavor. They provide advantages AND disadvantages, have their own dynamics (loyalty, influence, demands), and interact with the institutional structure. Comparable to EU4 Estates: load-bearing parts of the system with real mechanical teeth. (Derived from: "I'd argue they're more like Estates in EUIV... deeply embedded in how the game works")

### A30: Non-State Actors as Independent Simulation Entities
Non-state actors (Hezbollah, Houthis, cartels, PMCs, transnational networks) are **independent entities in the simulation** with their own territory, goals, and capabilities. They are NOT inherently cards in any single actor's collection. A nation's RELATIONSHIP to a non-state actor determines how it manifests mechanically:

- **Patron relationship** (Iran → Hezbollah): Shows up as a deployable proxy-asset card. But the entity has its own interests and isn't perfectly obedient.
- **Host relationship** (Mexico → Sinaloa Cartel): Shows up as a hostile/ambivalent entity card you're forced to manage — an estate with low loyalty.
- **No relationship** (US → Sinaloa Cartel): Not in your collection at all — part of the simulation that generates situations you react to.
- **Relationships can be cultivated, lost, or stolen** through diplomatic, intelligence, and military actions.

This gives **proxy warfare** a natural mechanical expression: deploying your non-state actor cards into situations on someone else's territory. (Derived from: Houthis/Hezbollah/Cartel analysis — "the same entity is different things to different players")

### A31: Symmetric Rules for All Actors
All nations in the simulation — player and AI-controlled — operate under **identical mechanical rules**. AI nations hold the same types of cards, face the same situations, and are subject to the same constraints (including bounded action economy, A3) as the player. There are no hidden bonuses, difficulty-scaling resource cheats, or asymmetric mechanics. All differences between nations emerge from **starting conditions, systemic position, and decisions made within the shared rules** — not from the rules themselves. This directly serves A21: the player can reason about AI behavior using the same mechanical understanding they apply to their own decisions, because the mechanics ARE the same. Surprises come from the system, not from hidden advantages. (Derived from: explicit design philosophy — "I don't like hardcoded resource-cheating AIs... I like the entire game to be equal adversaries under the rules")

### A32: Uniform Card Interface
Within the interaction-mechanics layer, the **card is the only interface** for decision-relevant entities. If an actor must decide what to do with something — commit it, withhold it, deploy it, or lose it — that thing must be a card. There is no second type of decision-relevant object. (Inspired by: Linux's "everything is a file," MTG's unified card interface)

**The card/attribute boundary test:** Can you answer "I am committing THIS thing HERE rather than THERE"? If yes, it's a card — it has positional identity. If no, it's either a simulation-layer variable or a property of a card.

**What is explicitly NOT a card:**
- **Simulation-layer state** — aggregate variables (GDP, population, approval ratings) that feed the simulation. These are the world state that *generates* cards, not cards themselves.
- **Systems-as-world-state** — the abstract dynamics of a system (how global markets function, how climate patterns evolve) remain simulation-layer computation, not cards. The distinction: the simulation computes system dynamics; **shared-space system cards** (A33) are the interface through which actors engage with those dynamics. An actor commits cards TO the WTO dispute resolution system card, not to "the abstract concept of institutional order." The boundary test holds: "I am committing THIS card to the WTO dispute situation rather than the financial crisis situation."
- **Space** (AASS) — the board cards operate on. *Control over* a geographic feature is a card; the feature itself is not.
- **Simulation dynamics** — the rules engine that determines how card-slot interactions resolve.

**Why the uniform interface is load-bearing:**
- **Single scarcity grammar** — cross-domain tradeoffs only work when all decision-relevant entities compete through the same interface. "Do I commit my intelligence apparatus to the domestic crisis or the foreign operation?" requires both options to be cards.
- **A31 compliance** — symmetric rules for all actors are automatically satisfied when all actors interact through the same card interface.
- **A28 implementation** — government type becomes a tag on cards (player-controlled vs. automated), not different automation logic per entity type.
- **A21 legibility** — the player's entire strategic position is readable in one visual language, supporting the assumption gap.

(Derived from: Linux "everything is a file," MTG unified card interface, adversarial stress-testing of card/attribute boundary with 14 edge cases)

### A33: Shared Situation Space
Situations can exist in a **shared space** that is not owned by any actor. Multiple actors can commit cards from their tableaux into a shared situation's sub-slots, subject to **access scope** — a property of each sub-slot that determines which actors can commit to it.

**AASS Systems manifest mechanically as persistent shared-space cards.** The five system subtypes (institutional, infrastructure, market, normative, environmental) plus information/media systems are cards in the shared space. They are persistent (they exist across turns), carry sub-slots with typed access scope, and interact with each other through counter interactions between shared-space cards — no special "system-to-system edge" is needed beyond the standard card interface (A32).

**Access scope forms a gradient:**
- **Environmental** — universal and involuntary. All actors are subject to climate system effects whether they engage or not.
- **Market** — near-universal. Any actor with the prerequisite economic attributes can participate.
- **Normative** — global reach, variable commitment. Actors can engage with or defy normative systems; engagement level is a choice.
- **Infrastructure** — connected actors only. Participation requires physical or technical connectivity (pipeline access, internet backbone connection).
- **Institutional** — members only. Only actors who have joined the institution can commit to its sub-slots (though non-members may commit to situations *about* the institution).

**Non-system situations also live in shared space** when they inherently involve multiple actors: border disputes, humanitarian crises, trade negotiations, regional conflicts, global phenomena. The boundary test for shared vs. actor-only: **can the situation be meaningfully engaged with by more than one actor?** If yes, it belongs in shared space with appropriate access scope on its sub-slots. If no, it belongs in a single actor's tableau.

**The two-zone model:** Each actor has a tableau (their cards — what they own and control). The shared space holds situations and system cards that exist between actors. Cards in an actor's tableau are "yours." Cards in shared space are "the world's." Actors interact with shared-space situations by committing cards FROM their tableau INTO the shared situation's sub-slots. The same card mechanics (Q29 one-place rule, Q31 expenditure modes, Q43 conditions for change, Q44 satisfaction mechanisms) apply identically in both zones.

(Derived from: adversarial stress test of AASS → systems-as-cards insight → Cultist Simulator Mansus analogy → generalization to all multi-actor situations. This is a first-principle commitment: it cannot be derived from A27/A32 alone because those axioms previously excluded systems from card status.)

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
| **Capabilities/Assets** | F-35 squadrons, nuclear arsenal, semiconductor fabs, cyber tools, satellite constellation, intelligence apparatus, information/influence operations capability | Deployable capability cards |
| **Demographics** | Population size, age structure, urbanization, ethnic composition, education level | Simulation substrate that generates condition cards |
| **Political Conditions** | Regime type, domestic political cohesion, public opinion, institutional quality, polarization, state capacity, civil-military relations | Constrains which cards can be played; generates political situation slots |
| **Ideational Attributes** | State ideology, religious composition, cultural soft power, normative commitments, historical grievances | Persistent modifier cards shaping interactions; motivation for AI actors |
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
| **Information/Media Systems** | Global news networks, social media platform dynamics, algorithmic content distribution, attention economy | Emergent from actor content production + platform architecture; can be influenced through content injection and regulation but outcomes not directly controllable; subject to viral cascading and narrative lock-in |

**Design notes:**
- Systems manifest in the interaction-mechanics layer as **persistent shared-space cards** (A33). Each system subtype is a card in the shared situation space, carrying sub-slots that actors commit their own cards into.
- The six subtypes are **mechanically distinct** — their differences now map to three dimensions: **access scope** (who can commit cards — environmental is universal, institutional is members-only; see A33 gradient), **auto-progression dynamics** (markets and climate auto-progress with high autonomy; institutions change primarily through deliberate actor action), and **degree of actor control** over the card's sub-slots (you can reform institutional sub-slots; you can only adapt to environmental ones).
- Systems interact with Actors through **leverage and position**. A nation's position within a system (e.g., US position in global financial infrastructure) is a Relational Attribute that produces cards. Leverage determines what sub-slots an actor can access and with what priority.
- **System-to-system coupling** works through counter interactions between shared-space cards — no special interaction edge is needed. When the global financial system card's instability counter rises, it modifies counters on infrastructure system cards and market system cards through standard card-interaction mechanics (A32).
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

These edges describe how AASS categories constitute each other ontologically — they are not the interaction model. How entities actually interact (including within the same category) is governed by the card-slot layer.

### How AASS Maps to the Card-Slot Model (A27)

**AASS and the card-slot model are different architectural layers.** AASS is the **world-state layer** — it describes what exists and what is true about the world. The card-slot model (A27) is the **interaction-mechanics layer** — it defines how actors engage with and change the world state. Per A32, the card is the **only interface** within the interaction layer — if an actor must decide what to do with something, it is a card. Per A31, all actors (player and AI) interact through the same card-slot mechanics under the same rules.

This distinction matters because:
- **The two layers serve different purposes** — AASS must be *ontologically complete* (capture everything that exists and matters). The card-slot system must be *mechanically coherent* (provide legible, balanced interaction rules for all actors within A3's bounded agency).
- **The same world state can produce different card surfaces for different actors** — A30 already demonstrates this: Hezbollah is a different card (or no card at all) depending on a nation's relationship to it, but it is the same AASS entity regardless. This applies symmetrically to all actors.
- **Government type (A28) configures each actor's card availability** — it determines which cards are directly controllable and which are automated, for player and AI nations alike.
- **The player-specific element is the UI/UX presentation, not the mechanics.** What the player sees on screen is a rendering of their cards and situations. The underlying card-slot mechanics are universal — every nation has cards, faces situations, and operates under the same rules (A31).
- **Category-agnostic interaction** — Within the card-slot layer, a card's originating AASS category is mechanically irrelevant. System-derived cards interact with other System-derived cards through the same interface as with Attribute-derived cards. Within-category interactions (Actor↔Actor, System↔System) need no ontological edges because they resolve through A32's uniform card interface.

The mapping from world state to cards operates across two zones:

**Actor tableaux** contain cards drawn from:
- **Attributes** (primary source): your capabilities, political conditions, ideational character, economic tools, relational leverage
- **Actors** (secondary): allied actors, sub-state factions, proxy relationships you can leverage

**Shared space** contains:
- **System cards** (persistent): institutional, infrastructure, market, normative, environmental, information/media — these are the systems themselves as interactable shared-space cards (A33)
- **Multi-actor situations**: generated by the simulation when conditions affect multiple actors (border disputes, trade negotiations, humanitarian crises, system-level events)

**Situations** are generated when:
- Systemic conditions cross thresholds (Market System instability triggers economic crisis slot)
- Actor interactions create friction (rival Actor's Relational Attributes conflict with yours)
- Spatial conditions change (territorial dispute, resource discovery, climate event)
- Attribute trajectories collide (demographic pressure + economic stagnation + political polarization → instability slot)

**Resolution** of card-slot interactions is determined by:
- The cards' properties (tags and counter values)
- The relevant shared-space system cards — system context is provided by the system cards whose counters and sub-slot states affect the situation being resolved. The relevant systems are the ones the situation interacts with, not an abstract "which systems matter" query.
- The Space context (geographic and strategic constraints)
- Other Actors' responses (their cards in the same or related slots — in shared-space situations, this means all actors who have committed cards)

---

## A24: Simulation Variable Hierarchy (Revised)
The simulation's underlying variables are organized in a **layered hierarchy** with both **national** and **global** dimensions:

| Layer | National (per-state) | Global (shared) |
|-------|---------------------|-----------------|
| **Bedrock** (static/near-static) | Physical Geography, resource deposits, climate zone | Trade route geography, global resource distribution, ocean access |
| **Foundation** (slow-moving, years/decades) | **Economic structure** (lynchpin), demographic structure, institutional quality | Global economic order, financial infrastructure, major alliance architecture |
| **Derived** (faster-moving, shaped by foundation) | Military-industrial capacity, political conditions, ideational character, information environment | International norms, technology frontier, global information environment |

The player mostly interacts with derived layers turn-to-turn, but the foundation layer determines long-term outcomes. Global layers constrain and connect national layers — a nation's economy exists WITHIN the global economic order. This maps to A20: the player can push on surface variables, but deep structural reality (both national and global) resists.

**Note on Environmental/Physical Systems:** These are the one bedrock-layer element that shifts significantly within campaign timescale (~2020 to 2040+). A24's "near-static" characterization of bedrock holds for geography and resource deposits but not for the climate system, which undergoes non-linear change during the game's temporal scope. This makes environmental system cards (A33) uniquely dynamic among bedrock-derived entities — they auto-progress with consequences that cascade through foundation and derived layers.

(Revised from original A24 to incorporate AASS global layer and Attribute categories. Derived from: discussion of economics as lynchpin, globalization analysis, AASS taxonomy development)

---

## Thesis Statement

> *A global sandbox where you govern a real nation, import your real-world assumptions about how geopolitics works, and then watch transparent systems either validate or demolish those assumptions through honest consequences.*

The game is an **argument in interactive form**: that systemic conditions — not great men — produce historical outcomes, and that the gap between what you expect and what actually happens is where insight lives.

---

## Open Design Spaces

*Areas explicitly flagged as needing further exploration. These are not problems — they are where the interesting design work lives.*

### D1: Temporality and Turn Structure — PARTIALLY RESOLVED
The implicit assumption that turns represent fixed calendar periods has been **challenged and found unjustified** — nothing in the confirmed axioms requires it. The modern setting creates a timescale problem: drone strikes happen in minutes, demographic shifts take decades. Fixed calendar turns either compress or stretch everything awkwardly.

**Candidate models to explore when revisiting:**
- **Fixed long periods with limited mid-turn interventions**: Turns are long (years?), but you get interrupt opportunities for crises within them
- **Abstract duration categories**: Effects are tagged short/medium/long rather than tied to calendar months
- **Asynchronous/fragmented turns**: Decision points aren't evenly spaced; the simulation drives when you act
- **Event-driven cycles**: Simulation runs until enough situations accumulate to present a decision point; time is a consequence, not a clock
- **Simultaneous commitment + ordered resolution**: All actors commit cards to situations (both tableau and shared-space) simultaneously. Resolution follows in a deterministic order. (Derived from A33 + A31 + A15: shared situations demand simultaneous input to prevent first-mover information advantage, which would create asymmetry from turn order rather than systemic position — contrary to A31's intent.)

**Confirmed structural constraint:** Regardless of which temporal model is chosen, **the turn has two phases** — a **commitment phase** (all actors assign cards to situations simultaneously, under uncertainty about others' commitments) and a **resolution phase** (situations resolve, effects cascade, new situations spawn). This is confirmed because: A33 requires it (shared situations with multiple actors committing demand simultaneous input), A31 requires it (sequential play on shared situations gives informational advantage not from systemic position but from turn order), and A21 is served by it (the gap between your expected and actual resolution outcome — the moment when other actors' simultaneous commitments are revealed — is the insight-generating moment).

**What IS confirmed:** Turns exist (A9), agency per turn is bounded (A3), the turn boundary forces commitment (A3/A9), and the turn has a commit-then-resolve structure (A33/A31). What a turn REPRESENTS temporally, and the specific resolution ordering rule, remain open.

**Status: PARTIALLY RESOLVED. Turn structure (commit → resolve) is confirmed. What a turn represents temporally, and the specific resolution ordering rule, remain open.**

### D2: Military Layer — The "Deck-Building" Verb
A18 establishes the philosophy (curation, not construction). A27 provides the interaction model. AASS clarifies that military systems are **Capability/Asset Attributes** fielded as cards into conflict slots. The remaining question: what does military curation look like concretely? How do you acquire systems, what does your military collection look like, and what are the slot structures for military situations? **Status: AASS provides the ontological grounding; concrete mechanics needed.**

### D3: Card Taxonomy and Slot Patterns
The card-slot architecture is confirmed (A27). AASS provides the **source categories** for cards: Attributes and Actors populate actor tableaux; Systems manifest as persistent shared-space cards (A33).

**Confirmed mechanics (Situation behavior):** *Items below are **D** (derived) or **E** (extensions) — confirmed through analysis of Cultist Simulator, Paradox event systems, and MTG mechanics, consistent with A27/A25/A32.*

**Situations are cards with conditions for change.** Per A32, situations are cards — they appear in an actor's tableau when generated by the simulation. What distinguishes a situation-card from other cards (capabilities, entities, etc.) is that it carries **conditions for change**: rules governing when and how the situation evolves. Sub-slots are a **feature some cards have**, not the defining characteristic of situations.

Situations vary along two independent dimensions:

- **Demand:** Some situations are **forced** — they carry temporal auto-progression and will change on their own whether or not the actor responds. Others are **optional** opportunities that require active engagement. The mix creates tension.
- **Temporality:** Situations vary in time pressure:
  - **Immediate:** Fires and demands response this turn.
  - **Windowed:** Fires and gives X turns to respond, with the option to respond early. Advance warning you can plan around.
  - **Multi-turn unfolding:** The situation advances or transforms across turns — an ongoing process, not just a deadline.
  - These can overlap.

**Conditions can be satisfied through four mechanisms:**
- **Card commitment** — actor fills the situation's sub-slots with cards from their collection. Sub-slots can be mandatory or optional, type-filtered or open.
- **Modal choice** — actor selects from presented options (OK, Yes/No, A/B/C). No resource commitment — the decision IS the choice.
- **Temporal auto-progression** — condition fires automatically at a time boundary. This is what makes forced situations forced.
- **External trigger** — condition satisfied by outside events (another situation resolving, simulation state change, another actor's action).

These mechanisms compound: a situation can have sub-slots for card commitment AND a temporal deadline that fires a default outcome if no response comes. This resolves the **default outcomes** question — forced situations auto-progress per A15 (the living world moves without you).

**When conditions are met, the situation undergoes one of four change types:**
- **Resolution** — effect fires, situation card consumed.
- **Transformation** — situation card becomes a different card (e.g., multi-stage crisis with different conditions per stage).
- **Modification** — situation persists but properties change (counters shift, new sub-slots open).
- **Null** — preconditions invalidated, situation removed with no effect, committed cards returned. (MTG fizzle.)

**Effects are separate from change types.** A change may produce effects: spawning new situations for this or other actors (Q37), returning cards, modifying simulation state, changing counters on involved cards. Engaging with a situation does not imply resolution — committing cards or choosing may transform or modify the situation rather than close it. Resolution is one outcome among many, not the default. This implements A25: decisions create new situations with their own tension.

**Modal responses resolve binary decisions.** Declarations of war, alliance invitations, and other yes/no decisions are situation-cards with modal conditions rather than sub-slots. They occupy one end of a natural spectrum: pure modal choice → hybrid (choose strategy + commit resources) → pure card commitment.

**Cards can only be in one place at a time.** This is the core scarcity mechanic. Committing a card to one situation makes it unavailable for others. Multi-turn situations lock cards across turn boundaries, meaning long commitments (e.g., military deployments) reduce your available cards for subsequent turns.

**Two independent scarcity dimensions constrain the player:** A3's bounded action economy caps per-turn agency through some mechanism (the specific relationship between orders and card-slotting is an **open question** — see below). The one-place rule caps which cards are available at all. These are confirmed as **separate axes of constraint** that compound. This is load-bearing for difficulty and tension.

**Three card expenditure modes coexist within the same system:**
- **Consumed:** Card is spent and gone (expendable resources, one-time favors).
- **Occupied:** Card is locked into a situation while it resolves, then returned. Unavailable for other use during occupation.
- **Transformed:** Card goes in as one thing, comes back as something different. The input card is gone; a new card is produced.

**Edge case to address in tuning:** If enough forced situations fire simultaneously, the player could run out of available cards. This is a legitimate "you're overwhelmed and losing" state, but may need a safety valve depending on how card counts and situation frequency feel in practice. This is a balance question, not a design flaw.

**Cards carry two distinct types of properties:**
- **Tags** — categorical, mostly stable labels that identify what *kind* of card this is. Tags enable slot filtering (a situation can require a [Military] card in slot 1 and a [Diplomatic] card in slot 2) and determine interaction rules. Analogous to MTG card types/subtypes (Creature — Elf Warrior) and Linux file types (regular, directory, socket). Tags answer: "What is this?"
- **Counters** — numerical, mutable values that track the card's current *state*. Counters change through play: deployment may remove readiness counters, combat may add experience counters, neglect may degrade maintenance counters. Analogous to MTG +1/+1 counters, loyalty counters, charge counters. Counters answer: "How is this right now?"

Tags and counters are **mechanically distinct and non-overlapping**. A card's tags determine *where it can go*. A card's counters determine *how well it performs there*. This resolves the "mutable card state" question without requiring a fourth expenditure mode — a card that returns from a situation with changed counters is using the **occupied** mode (Q31) with counter modification as a side effect of resolution.

**Card existence is a simulation-layer concern.** The simulation (AASS world state) determines which cards are available to each actor based on world-state conditions (GDP thresholds, technological knowledge, institutional prerequisites, demographic conditions). Cards appear in an actor's collection when conditions are met and can disappear when conditions are no longer met. No special card-side gating mechanism is needed — the simulation generates the card surface, and the card surface is what actors interact with. This directly implements A32: the card layer doesn't need to know *why* a card exists; it just needs to present cards for decisions.

**Each actor has a single tableau.** There is no deck, no draw step, no hand size limit, and no separate "play area." All of an actor's cards — capabilities, entities, situations, everything — exist in one visible tableau. Situations are distinguished from other cards by having conditions for change, not by living in a different zone. Cards have two positional states: **available** (in tableau, uncommitted) or **committed** (inside a situation per Q29). The simulation adds and removes cards from the tableau; the actor decides what to do with what's there. This follows the Cultist Simulator model.

**Card lifecycle follows four coexisting patterns:**
- **Persistent** — cards that remain in your collection across turns. Your standing capabilities, institutions, and relationships. An F-35 squadron exists whether or not you deploy it this turn.
- **Generated** — new cards that appear in your collection at turn start, produced by the simulation based on current conditions (world state, existing cards, or any other factor). This is the "draw" — but it's the simulation dealing to you based on what your nation's reality produces, not a random pull from a deck.
- **Returning** — cards that were committed to situations (occupied, per Q31) and return to your collection when the situation resolves or the occupation period ends. Cards refresh at turn start.
- **Consumed** — cards that are gone when used (Q31 consumed mode). The simulation may generate replacements if conditions are met, but the specific card is permanently spent. (Analogous to Cultist Simulator funds.)

These four patterns coexist within the same collection. A nation's tableau at any moment is the sum of its persistent cards, recently generated cards, and recently returned cards, minus whatever is currently committed to situations or has been consumed. **How many cards the simulation generates per turn is an open question** — it connects to the orders ↔ card-slotting relationship and overall scarcity tuning.

**Cross-actor effects route through two mechanisms.** The primary mechanism for situations inherently involving multiple actors is **shared-space situations** (A33) with multi-actor access scope — actors commit to the same situation directly. Border disputes, trade negotiations, system participation, and any symmetric multi-actor interaction use shared-space situations. The secondary mechanism remains **situation spawning** — one actor's card play spawns a forced situation for another actor. Spawning is still needed for asymmetric effects (sanctions targeting a specific nation, covert operations against a target) where the originator acts and the target reacts. Persistent cross-actor effects may be **multi-turn situations** in either zone. Escalation emerges from cascading chains across both mechanisms: a shared-space trade negotiation can spawn asymmetric domestic situations for each participant. This uses the existing situation spawning (Q28), forced demand (Q26), and multi-turn unfolding (Q27) systems alongside A33's shared space.

**Sub-slots carry access scope.** Each sub-slot on a situation card (in shared space or in an actor's tableau) specifies which actors can commit cards to it. Scope is a property of the slot, not the situation — a single situation can have slots accessible to different sets of actors. Scope types include:
- **Single-actor** — domestic situations; only the owning actor can commit.
- **Named-actor** — bilateral disputes or targeted situations; only specifically named actors can commit (e.g., "US and China" on a trade war situation).
- **Conditional** — actors meeting tag/attribute criteria can commit (e.g., "any actor with [Nuclear] capability tag" for a non-proliferation negotiation).
- **Universal** — any actor can commit (e.g., environmental crisis response, open market participation).

This uses the existing tag-filtering mechanism (Q35) extended to actor identity. No new primitives are introduced.

**Situations exist in shared space when they involve multiple actors.** The single-tableau model (Q38) is extended: each actor has a tableau (their cards), and a shared space holds situations and system cards that are not owned by any actor. Actors interact with shared-space situations by committing cards from their tableau into the situation's sub-slots, subject to access scope. The same card mechanics (Q29 one-place rule, Q31 expenditure modes, Q43 conditions for change, Q44 satisfaction mechanisms) apply identically in both zones.

**Remaining open questions:**
- **Orders ↔ card-slotting relationship:** A3 confirms bounded per-turn agency. A27 confirms card-slotting as the interaction mechanic. The relationship between these two is **unresolved**. Possibilities include: orders = card slots (1:1), orders as a superset encompassing non-card actions, card-slotting costing variable order points, or orders and card-slotting as fully orthogonal scarcity axes. This is load-bearing — the answer shapes how the two scarcity dimensions actually compound in play.
- **Card type taxonomy:** Tags (confirmed above) provide the *mechanism* for categorizing cards, but the **concrete set of tags is open**. A previous draft proposed four types (active/deployable, passive/persistent, entity/institutional, expendable/consumed), but this was illustrative, not stress-tested. The taxonomy needs to be derived from AASS Attribute subcategories and validated against gameplay requirements. What tags exist? Which are domain tags (Military, Diplomatic, Economic)? Which are behavioral tags (Deployable, Persistent, Consumable)?
- **Slot shape filtering:** Tags are confirmed as the filtering mechanism. What remains open is **which situations use strict tag-based filtering vs. open-ended slots**, and whether this varies per situation type or follows a general rule.
- **Nation-identity attachment:** Civic slots (A27's original Level 1) have been invalidated — national identity emerges from persistent cards, A19 decision chains, and A28 control surface configuration instead. Is this sufficient for player attachment to their nation's build, or does an additional structural mechanic need to capture the "this is MY nation" feeling?
- How are cards acquired through **gameplay decisions** (focus trees, political transformation, diplomatic deals)? The simulation-driven generation pipeline is confirmed, but player-driven acquisition mechanics are open (connects to D8).
- What are the structurally distinct slot patterns (A23 template diversity applied to situations)?
- **Cross-actor tableau visibility:** Per A14 (legibility through action) and A31 (symmetric rules), to what degree can actors observe each other's tableaux? Full visibility? Partial (only committed cards)? Only situations that affect them? This is an information design question with mechanical implications for AI legibility.
- **Resolution ordering:** When all commitments are simultaneous (D1 confirmed constraint), what determines the order situations resolve in? Urgency-first? Geographic propagation? Cascading (parent before child)? This is a new design lever with major gameplay implications — the ordering rule determines which effects are "already resolved" when later situations process, creating strategic depth around which situations you want to resolve first.

**Status: Situation mechanics confirmed, including situation definition (Q43), condition satisfaction mechanisms (Q44), change types (Q28 revised), and modal responses. Card properties (tags/counters), card existence pipeline, card lifecycle (collection model, four coexisting patterns), cross-actor effects (dual mechanism: shared-space + spawning), sub-slot access scope, and shared-space situation model resolved. Card taxonomy (specific tags), slot pattern design, and resolution ordering are the next major tasks.**

### D4: Economic Layer
Identified as the **lynchpin** of the simulation (A24). A26 establishes the player verb: observe, then selectively intervene. AASS clarifies that the economy spans multiple categories: Economic Attributes (national), Market/Exchange Systems (global), and Infrastructure Geography (spatial). **Remaining questions:** What does the economic simulation look like as a spectacle? How does economic capacity constrain military procurement and political options? What are the high-impact economic intervention cards? **Status: Architecture resolved. Spectacle and card design needed.**

### D5: Combat Resolution
When two nations go to war in a world with nuclear deterrence, what happens mechanically? AASS frames this as: Capability/Asset Attribute cards deployed into conflict slots, resolved within System context (alliance systems, normative systems like the nuclear taboo) and Space context (strategic geography). **Remaining questions:** Auto-resolve vs. map-based? Escalation mechanics? How does nuclear deterrence mechanically constrain conventional warfare? **Status: Ontologically grounded. Mechanics not yet explored.**

### D6: Diplomatic/Geopolitical Layer
Alliances, treaties, sanctions, proxy wars, information warfare. AASS frames diplomacy as operating through **Relational Attributes** (actor-to-actor connections), **Institutional Systems** (UN, treaty regimes), and **Normative Systems** (sovereignty norms, international law).

**Confirmed mechanics (Diplomatic proposal structure):** *All items below are* ***E*** *(extensions) — confirmed through stress-testing bilateral interaction against A27/A32/Q37. No new interaction patterns introduced.*

**Diplomatic interactions are situation-cards with typed slots.** When an actor initiates a diplomatic proposal, they construct a situation-card with two slot types:

- **Offer slots** — filled with the proposer's own cards from their collection. These cards are **committed** (occupied per Q29) for the duration of the proposal, creating real scarcity cost. You cannot offer the same card in two simultaneous proposals.
- **Demand slots** — defined as **tag-filtered requirements** that the recipient must fill with their own cards if they accept. The proposer specifies the slot shape (what types of cards are required); the recipient chooses which specific cards to commit. This preserves recipient agency and uses the existing slot-filtering mechanism (Q35 tags).

This serves multiple axioms simultaneously: **A14** (legibility — the AI's proposal shows actual committed cards, making intent readable through action), **A31** (symmetric — AI constructs proposals identically to the player), **A7** (emotional — an ally's heavy demands are visible and felt), **A21** (transparent — you can reason about what the AI values from what they offer and demand), **A20** (systemic — what an actor can offer is constrained by their systemic position and available cards).

**Diplomatic proposals unfold in phases** (per Q27 multi-turn situations):
1. **Construction** — proposer fills Offer slots with their cards, defines Demand slot shapes
2. **Delivery** — proposal spawns as a forced situation for the recipient (Q37)
3. **Evaluation** — recipient reviews: accept, decline, or counter-offer
4. **Fulfillment** (if accepted) — recipient fills Demand slots with their own cards
5. **Resolution** — cards resolve using existing expenditure modes (Q31)

**Acceptance resolution uses existing mechanics.** Different cards in a deal resolve based on their nature:
- **Fungible resources** (abstracted currency, aid packages) → consumed (Q31). Recipient's simulation generates corresponding benefit.
- **Capability cards** (base construction authority, military training programs) → occupied during fulfillment, then returned. The capability is temporarily committed, not permanently transferred.
- **New persistent entities** → spawned via Q28 side-effect spawning. Example: a "base construction authority" card committed to an accepted deal spawns a new "US Military Base (Kazakhstan)" card. The spawned entity is distinct from anything in the original deal.

**Viable direction (noted, not locked):** Counter-offers may work by the recipient modifying the proposal card and returning it, with the original proposer's offer cards **releasing** when terms change (preventing the gaming exploit of fake proposals to tie up opponent's resources). This needs further development.

**Remaining open questions:**
- **Counter-offer mechanics:** Do original offer cards release when a counter-offer is sent? How many rounds per turn? How to prevent gaming (fake proposals as resource denial)?
- **Action cost per negotiation round:** Does each round consume an action (A3)? Connects to orders ↔ card-slotting (D3) and D1 (temporality).
- **Offer card tie-up duration:** Until end of turn? Until response? Across turns for major deals?
- **Persistent cross-actor entities:** Where does a military base in Kazakhstan "live" mechanically? Cards need spatial positioning beyond collection membership. Cross-depends on D2 (military deployment), D5 (combat spatial mechanics), AASS Space.
- **Binary decisions:** *(Resolved by Q44 — modal situation responses. Declarations of war, alliance invitations, etc. are situation-cards with modal conditions.)*
- **Specific vs general demands:** Can demand slots require a specific named card, or only tag-filtered categories, or both? Connects to D3 slot shape filtering.
- **What subset of diplomatic tools matters most?** Sanctions, alliances, treaties, proxy support, information warfare — which get first-class mechanical treatment?

**Status: Core proposal mechanic confirmed (situation-cards with Offer/Demand slots, multi-phase flow, existing expenditure modes). Counter-offer flow, timing, spatial results, and diplomatic tool prioritization are the open work.**

### D7: The "Small Victories" System
A16 establishes that themed sub-objectives serve as stopping points. **Remaining questions:** What generates them? Per-nation? Procedural from Attribute conditions? How do they interact with the political decision system (A19/D3)? Can the player define their own? **Status: Not yet explored.**

### D8: Focus Tree / Decision Tree Architecture
A1 establishes dual-purpose decision trees. A19 requires deep political transformation. A23 requires template diversity. A27 implies focus trees are a primary mechanism for **acquiring and transforming cards**. AASS grounds the templates in Attribute conditions. **Remaining questions:** What does a focus tree look like in this game? How does it interact with the card-slot system? Is it a tree, a web, or something else? How does it generate cards from systemic conditions? **Status: Principles established. Structural design not yet attempted.**

---

## Resolved Questions

*Previously open questions that have been answered through discussion.*

| # | Status | Question | Resolution |
|---|--------|----------|------------|
| Q1 | **A** | Genre/Scale | Nation-level grand strategy (A10) |
| Q2 | **A** | Setting | Modern/near-future warfare (A8) |
| Q3 | **A** | Real-time vs Turn-based | Turn-based with orders; hard dep from A3 (A9) |
| Q4 | **A** | Single/Multiplayer | Single-player with emotionally engaging AI (A7) |
| Q5 | **A** | Victory condition | No overall victory; small victories as stopping points (A16) |
| Q6 | **A** | Temporal scope | Years to decades from ~2020 start (A12) |
| Q7 | **A** | Geographic scope | Full globe, any nation playable (A11) |
| Q8 | **A** | Player identity | The nation; leaders are mutable (A13) |
| Q9 | **D** | Source of emotional engagement | Observable AI behavior + player-imported assumptions, not prose (A14, A21, A22) |
| Q10 | **D** | Hand-crafted vs procedural content | Condition-driven templates with diverse structures (A23, A24) |
| Q11 | **A** | Foundational philosophical assumption | Systems primacy with constrained agency (A20) |
| Q12 | **A** | Core simulation variable | Economic structure as lynchpin (A24) |
| Q13 | **A** | Economic player verb | Observe complex system, selectively intervene with high-impact dilemmas (A26) |
| Q14 | **A** | Decision interaction model | Card-slot system: accumulated capabilities slotted into situation structures (A27) |
| Q15 | **A** | Decision quality principle | Decisions create situations, not increments; dilemmas over optimizations (A25) |
| Q16 | **A** | Player identity (mechanical) | Acceptable abstraction — you are "the nation," not a specific character (A13) |
| Q17 | **A** | Non-governmental actors | Deeply embedded entity cards with mechanical teeth, like EU4 Estates (A29) |
| Q18 | **D** | Compound decisions | Situations can require cards from multiple domains; resource allocation puzzle (A27) |
| Q19 | **A** | Government type impact on gameplay | Controls which cards are automated vs player-controllable (A28) |
| Q20 | **A** | What cards represent | Broader than "actions" — everything your nation IS and CAN DO (A27 revised) |
| Q21 | **D** | Card system as unifying mechanic | National Spirits, military systems, focus rewards, estates all unified as card types (A27) |
| Q22 | **A** | Non-state actors | Independent simulation entities; relationship determines card manifestation (A30) |
| Q23 | **A** | World model taxonomy | Actors — Attributes — Systems — Space (AASS); adversarially tested |
| Q24 | **D** | Where cards come from | Actor tableaux: primarily Attributes, secondarily Actors. Shared space: system cards (persistent, A33) and multi-actor situations (generated). Space provides context for both zones |
| Q25 | **D** | How globalization is modeled | Global Systems layer parallel to national layers; nations embedded within shared systems; system leverage is a key variable |
| Q26 | **E** | Situation demand model | Situations are either forced (demand card commitment) or optional (opportunities); the mix creates tension (D3) |
| Q27 | **E** | Situation temporality | Immediate, windowed (X turns to respond), or multi-turn unfolding; can overlap (D3) |
| Q28 | **E** | Situation change types | Four types: resolution (consumed), transformation (becomes different card), modification (properties change), null (invalidated, no effect). Effects (situation spawning, card returns, etc.) are separate from change types (D3, A25) |
| Q29 | **E** | Card positional scarcity | Cards can only be in one place at a time; occupation across turn boundaries is possible (D3) |
| Q30 | **D** | Dual scarcity model | Player constrained by both A3's bounded action economy and card availability (one-place rule); these are separate axes that compound. The specific mechanical relationship between orders and card-slotting is **open** (D3) |
| Q31 | **E** | Card expenditure modes | Three modes coexist: consumed (gone), occupied (locked then returned), transformed (becomes different card) (D3) |
| Q32 | **D** | World state vs interaction mechanics | AASS is the world-state layer (what exists). The card-slot model is the interaction-mechanics layer (how all actors engage with world state). Both are universal per A31; the player-specific element is the UI/UX presentation, not the mechanics. |
| Q33 | **A** | AI mechanical symmetry | All nations operate under identical rules. No hidden bonuses or asymmetric mechanics. Differences emerge from starting conditions and systemic position, not from the rules themselves (A31). |
| Q34 | **A** | Uniform card interface | Within the interaction layer, the card is the only interface for decision-relevant entities. Boundary test: "Can I commit THIS thing HERE rather than THERE?" Simulation state, systems-as-world-state (abstract dynamics), Space, and simulation dynamics are explicitly not cards; systems-as-interactable-entities are shared-space cards (A32 revised, A33). |
| Q35 | **E** | Card properties: tags and counters | Cards carry tags (categorical, stable, for slot filtering) and counters (numerical, mutable, for state tracking). These are distinct and non-overlapping. Tags answer "what is this?", counters answer "how is this right now?" (D3) |
| Q36 | **D** | Card existence pipeline | The simulation layer determines which cards exist based on world-state conditions. No card-side gating mechanism needed; the simulation generates the card surface (A32, AASS). |
| Q37 | **E** | Cross-actor card effects | Two mechanisms: (1) **Shared-space situations** (A33) — actors commit to the same situation directly; primary for symmetric multi-actor interactions (border disputes, trade negotiations, system participation). (2) **Situation spawning** — one actor's play generates a forced situation for another; primary for asymmetric effects (sanctions, covert ops). Escalation emerges from cascading chains across both mechanisms. Persistent effects modeled as multi-turn situations in either zone (D3, Q28, A33). |
| Q38 | **E** | Tableau + shared space model | Each actor has a single tableau containing all their cards. Alongside actor tableaux, a **shared situation space** holds unowned situations and system cards (A33). Cards in an actor's tableau are available or committed. Commitment can be to situations in the actor's own tableau (domestic) or to situations in shared space (multi-actor). The Cultist Simulator single-zone model is extended to a two-zone model, not replaced — the single-tableau principle still holds for each actor's own cards (D3, A33). |
| Q39 | **E** | Card lifecycle patterns | Four coexisting patterns: persistent (across turns), generated (simulation adds at turn start), returning (occupied cards refresh), consumed (gone forever). Turn start is the refresh/generation point (D3, Q31). |
| Q40 | **E** | Diplomatic proposal structure | Proposals are situation-cards with Offer slots (proposer's committed cards, occupied per Q29) and Demand slots (tag-filtered requirements the recipient fills on acceptance). No new interaction patterns (D6). |
| Q41 | **E** | Diplomatic multi-phase flow | Construct → deliver → evaluate → fulfill → resolve. Maps to Q27 multi-turn unfolding. Delivery via Q37 cross-actor situation spawning (D6). |
| Q42 | **E** | Diplomatic acceptance resolution | Existing expenditure modes apply per card type: consumed (fungible resources), occupied+returned (capabilities), side-effect spawning via Q28 (new persistent entities like military bases) (D6). |
| Q43 | **D** | Situation definition | Situations are cards (A32) with conditions for change; sub-slots are a card feature, not a situation-defining characteristic (A32, A27) |
| Q44 | **E** | Condition satisfaction mechanisms | Four mechanisms: card commitment (sub-slots), modal choice, temporal auto-progression, external trigger; these can compound. Modal responses resolve binary decisions (D3, D6) |
| Q45 | **D** | Systems as shared-space cards | AASS Systems manifest mechanically as persistent shared-space cards (A33). Systems pass A32's boundary test: actors commit cards TO them ("I am committing THIS card to THIS system"). The simulation still computes system dynamics; the cards are the interface through which actors engage. Derived from A33 + A32 revised (A33, A32). |
| Q46 | **E** | Access scope on sub-slots | Sub-slots carry access scope determining which actors can commit. Scope types: single-actor, named-actor, conditional (tag/attribute criteria), universal. Uses existing tag-filtering mechanism (Q35) extended to actor identity. Gradient for system cards: environmental (universal) → market (near-universal) → normative (variable) → infrastructure (connected) → institutional (members). Consistent with A33 but not strictly required by it (A33, Q35). |
| Q47 | **D** | Simultaneous commitment + ordered resolution | All actors commit cards to situations (tableau and shared-space) simultaneously during a commitment phase. Resolution follows in a deterministic order during a resolution phase. Sequential play on shared situations would give informational advantage from turn order rather than systemic position, violating A31/A15. Derived from A33 + A31 + A15 (A33, A31, A15, D1). |
| Q48 | **E** | Information/media domain resolution | The information/media domain is modeled as a shared-space system card (Information/Media Systems in AASS), not a new framework subcategory. Actors interact with it by committing cards (content production, regulation, platform manipulation) into its sub-slots. Resolves the adversarial finding that information warfare lacked mechanical grounding, using A33's mechanics rather than framework expansion (A33, AASS). |
