# AASS Framework Stress Test — Residual Findings

## What This File Is

An adversarial agent attacked the AASS (Actors — Attributes — Systems — Space) world model in DESIGN.md across 8 dimensions, producing 28 findings (1 CRITICAL, 11 SIGNIFICANT, 16 MINOR). A defender agent then evaluated each finding. A synthesis identified genuine gaps vs. phantom problems.

The genuine gaps were resolved in commit A33 (Shared Situation Space) and associated edits. **This file contains only the findings that were NOT resolved by that commit** — either because the defender successfully argued they're already handled, because they're simulation-layer concerns rather than ontological gaps, or because they're content-level detail that doesn't need framework changes.

Each finding includes the adversary's claim, the defender's verdict, and severity. Use this as a reference when doing detailed card design, simulation design, or content authoring — these are the places where the framework is adequate but the implementation needs to be thoughtful.

## How to Read Severity Ratings

- **SIGNIFICANT** — Important real-world phenomenon that the framework CAN represent but where the representation is non-obvious, underspecified, or depends on careful implementation choices.
- **MINOR** — Real phenomenon that maps cleanly onto existing categories. Listed for completeness; no action typically needed.

(The original critique's sole CRITICAL finding — System-System interaction edge — was resolved by A33.)

## How to Read Defender Verdicts

- **REFUTED** — The framework already handles this. No action needed unless you're doing content design in this area (in which case, the adversary's examples are useful reference).
- **CONTEXTUALIZED** — The framework handles this but the adversary identified genuine implementation complexity. Worth attention during simulation or card design.
- **PARTIALLY ACCEPTED** — Part of the finding was addressed by the plan; a residual concern remains.

---

## Remaining SIGNIFICANT Findings (5)

### 1.1 Technology Platforms as Quasi-Sovereign Actors
**Defender: CONTEXTUALIZED**

Meta, Google, TikTok, Starlink operate with quasi-sovereign characteristics that don't cleanly fit "Economic Actors." They control informational territory (Informational/Virtual Space), set normative rules within their domains (content moderation as legislation), command populations larger than most nations, and make foreign policy decisions (Starlink limiting coverage in Crimea, Meta throttling Russian state media globally). A multinational oil company and Meta operate in fundamentally different strategic registers.

**Why it's residual, not resolved:** The defender correctly argues that multi-faceting handles this ontologically — a tech platform is an Economic Actor whose platform is Informational/Virtual Space and whose infrastructure contribution is an Infrastructure System. No new Actor subcategory is needed. However, when designing entity cards (A29) for tech platforms, their tag/counter profiles must reflect their distinctive mechanical behavior (informational control, platform governance, infrastructure dependency). This is a card-design task, not a framework task.

**When this matters:** Designing entity cards for non-state actors. Tech platform cards need different tags and counter profiles than traditional corporate entity cards.

### 2.3 Technological Capacity / Innovation Ecosystem
**Defender: CONTEXTUALIZED**

R&D ecosystems, university-industry linkages, patent systems, STEM workforce, venture capital infrastructure, and basic research institutions are not explicitly addressed. The US-China technology competition (chip export controls, AI race) is a defining geopolitical dynamic from the 2020 start. Technology transfer, theft, and denial are major diplomatic and intelligence tools.

**Why it's residual, not resolved:** The defender argues multi-faceting is working as intended: R&D spending is an Economic Attribute, STEM workforce is a Demographic Attribute, institutional support is a Political Condition, research network participation is a System position. A24 already has "technology frontier" as a global derived variable. A monolithic "innovation score" would be less expressive than the decomposed representation. The risk is that this decomposition makes the US-China tech competition hard to see as a unified strategic contest — the player needs to understand that chip export controls, STEM immigration policy, university funding, and R&D tax credits are all fronts in the same competition. That coherence must come from situation design, not framework changes.

**When this matters:** Designing the technology-competition situation templates. Situations involving tech competition must draw cards from multiple Attribute subcategories simultaneously to create the compound feeling of a unified contest.

### 2.4 Food, Water, and Energy Security
**Defender: CONTEXTUALIZED**

Resource security — the degree to which a nation can feed, hydrate, and power itself — is a compound variable that drives enormous geopolitical behavior. Russia's invasion of Ukraine created a global food crisis (~30% of global wheat). Water conflicts (Nile, Mekong, Indus) are major geopolitical drivers. Energy dependence (Europe on Russian gas) shapes alliance behavior. These are existential national conditions with unique urgency.

**Why it's residual, not resolved:** Resource security is a derived variable: the relationship between need (Demographics + Economic Attributes) and supply (resource deposits in Space + Market Systems + Infrastructure Systems). It should be a computed variable in the simulation layer that generates forced situation cards when thresholds cross. The framework captures all the components; the simulation must compute the compound. The challenge: resource insecurity situations must feel existentially different from ordinary economic situations — a nation facing water scarcity doesn't weigh it against other economic concerns, it faces potential state failure.

**When this matters:** Simulation layer design and situation-template authoring. Resource security thresholds need dedicated situation templates that convey existential urgency, distinct from routine economic situations.

### 3.1 Intelligence-Sharing Networks
**Defender: CONTEXTUALIZED**

Five Eyes, SIGINT agreements, intelligence-sharing within NATO, and bilateral intelligence relationships (US-Israel, US-Saudi) don't fit existing System subcategories cleanly. They are trust architectures that determine information flow between actors. The UKUSA Agreement IS a formal agreement (Institutional System) — it is simply classified. But their distinctive mechanical effect is information sharing rather than rule-setting.

**Why it's residual, not resolved:** The defender is right that these are Institutional Systems ontologically. But mechanically, intelligence-sharing arrangements connect to the open question of cross-actor tableau visibility (D3). If the US shares intelligence with the UK, the UK effectively gains partial visibility into situations and actor behaviors it couldn't observe independently. When D3's visibility question is resolved, intelligence-sharing arrangements should be modeled as system cards (A33 shared-space cards) that modify the visibility rules between participating actors.

**When this matters:** Resolving D3's cross-actor tableau visibility question. Intelligence capability (now in Capabilities/Assets examples) interacts with intelligence-sharing system cards to determine what each actor can see.

### 4.1 Orbital Space (LEO, GEO, Cislunar)
**Defender: PARTIALLY ACCEPTED**

Orbital space has its own geography (orbital slots as chokepoints, debris fields as hazards, Lagrange points as strategic positions), economics (satellite communications, Earth observation), governance (Outer Space Treaty), and commercialization trajectory. Currently listed only as "space" under Strategic Domains.

**Why it's residual, not resolved:** Covered by Strategic Domains + Capabilities/Assets, but the spatial geography of orbit is underspecified. Over a decades-long campaign from 2020, space becomes increasingly significant. The examples under Strategic Domains should be expanded to acknowledge orbital geography. Does not require a new Space subcategory, but does require more explicit treatment within existing subcategories when the military layer (D2) and combat resolution (D5) are designed.

**When this matters:** Designing D2 (Military Layer) and D5 (Combat Resolution). Space as an operational theater needs spatial characteristics beyond "it exists."

---

## Remaining MINOR Findings (13)

### Actors

**1.2 Epistemic/Expert Communities** — IPCC, nuclear scientific communities, epidemiological networks exercise influence through knowledge production. *Defender: REFUTED — covered by Transnational Networks and International Organizations. No action needed.*

**1.3 Private Intelligence/Security Firms** — Palantir, NSO Group straddle Economic Actors and security functions. *Defender: REFUTED — NSO is an Economic Actor whose product is a Capability/Asset. Handled by multi-faceting.*

**1.4 Religious Authorities with Transnational Political Power** — Sistani, the Dalai Lama exercise political influence through religious authority without state power. *Defender: CONTEXTUALIZED — Sistani is a Sub-state Political Entity with transnational influence effects. Dalai Lama is a Transnational Network node. Worth noting when designing entity cards for religious figures.*

**1.5 Diaspora Political Organizations** — AIPAC, Overseas Friends of BJP are organized actors distinct from diasporas as demographic facts. *Defender: REFUTED — demographics are Attributes, organizations are Sub-state Political Entities with transnational connections via Relational Attributes.*

### Attributes

**2.5 Social Cohesion / Fragmentation** — Trust in institutions, intergroup relations, shared national narrative, resilience to information warfare. Explains why some nations fracture (Yugoslavia, Libya) while others absorb shocks (Japan, Finland). *Defender: REFUTED — derived variable computed from Demographics + Political Conditions interaction. Simulation design concern.*

**2.6 Corruption** — Not explicitly mentioned anywhere. Has distinctive mechanical effects: resource siphoning, military degradation (Russia 2022 performance), information distortion, external leverage for intelligence agencies. *Defender: CONTEXTUALIZED — subsumed under institutional quality in Political Conditions. Specific effects expressible through counters on institutional and capability cards (low institutional quality = high corruption = degraded readiness counters, reduced effectiveness).*

### Systems

**3.2 Global Knowledge/Research Networks** — Global scientific research, academic publishing, standards-setting bodies (IEEE, IETF, ISO, 3GPP). 5G standards fight is a real geopolitical battleground. *Defender: REFUTED — CERN is an International Organization, IEEE is an Institutional System, technology frontier is in A24.*

**3.3 Global Migration Systems** — Labor migration, refugee flows, brain drain/gain. 2015 European migration crisis reshaped European politics for a decade. *Defender: REFUTED — emergent outcome of Demographics + Environmental Systems + Institutional Systems. The framework generates this from component interactions, not a dedicated system.*

**3.5 Supply Chain Networks** — Semiconductor supply chain is geopolitically distinct from shipping routes. COVID and Ukraine demonstrated supply chain fragility. "Friend-shoring" and "decoupling" are strategic responses. *Defender: CONTEXTUALIZED — covered by Market/Exchange Systems + Infrastructure Systems. Fragility is a derived property. Worth attention when designing economic situation templates.*

### Space

**4.2 Electromagnetic Spectrum** — Contested resource: radio frequencies, radar bands, electronic warfare. *Defender: REFUTED — simulation-layer detail. Capability/Asset (EW equipment) within Strategic Domains.*

**4.3 Arctic as Contested Space** — Rapidly changing, multiple great power claims, Northern Sea Route as alternative to Suez. *Defender: REFUTED — covered by existing categories. The Arctic is exactly the kind of emergent situation the framework should generate from Physical Geography + Political Geography + Environmental Systems interaction.*

**4.4 Undersea Domain** — Undersea cables (99% of intercontinental data), deep-sea minerals, submarine warfare, Nord Stream sabotage. *Defender: REFUTED — covered across Infrastructure Geography, Physical Geography, and Strategic Domains.*

### Modern/Near-Future

**8.1 AI as a Geopolitical Force** — Transforms military capability, intelligence, economic productivity, information warfare, governance, and technology competition simultaneously. General-purpose technology that changes what capabilities, systems, and attributes mean. *Defender: CONTEXTUALIZED — AI is a Capability/Asset whose effects propagate through other categories. The "technology frontier" in A24 is its ontological home. Nuclear weapons and the internet also transformed every category — representable without special mechanisms. The challenge is content design: AI capability cards need to mechanically modify other cards' counters across domains.*

---

## Grandchild Example Gaps (not yet added to DESIGN.md)

The plan added intelligence apparatus, information/influence operations, state capacity, civil-military relations, and historical grievances. These further examples were identified as potentially worth adding during detailed design:

| Subcategory | Suggested additions | Notes |
|-------------|-------------------|-------|
| Capabilities/Assets | Special operations forces, diplomatic corps capacity, strategic reserves (oil/grain/forex), space launch capability | SOF distinct from conventional military; diplomatic capacity determines embassy network and negotiation bandwidth |
| Demographics | Health indicators (life expectancy, disease burden), refugee/displaced populations, diaspora populations, income inequality/class structure | Health indicators critical for pandemic scenarios from 2020 start (A12 COVID) |
| Political Conditions | Media freedom, judicial independence, electoral system characteristics | Electoral systems determine how demographic attributes translate into political power |
| Ideational Attributes | National identity strength/contested nature, attitudes toward specific nations, scientific/technological self-image | Attitudes toward specific nations (anti-Americanism, Russophobia) are persistent directional ideational attributes |
| Normative Systems | Environmental norms (Paris Agreement), laws of armed conflict (Geneva Conventions), freedom of navigation norms | Laws of armed conflict affect military card resolution; freedom of navigation critical for South China Sea |
| Environmental/Physical Systems | Natural disaster dynamics (earthquake zones, volcanic activity), ecological systems (fisheries collapse, deforestation) | Natural disasters are geological, not climatic — distinct from climate system |

---

## Ontological Boundary Problems (all defended, none requiring action)

These were identified and the defender successfully argued that multi-faceting handles all of them. Listed for reference only — they demonstrate where the framework is philosophically interesting but mechanically sound.

- **International Organizations: Actor or System?** (NATO as Actor + System + Relational Attribute) — Acknowledged in DESIGN.md. Implementation challenge when designing NATO's card manifestation.
- **Cyber: Space + Capability + System** — Quadruple categorization is a strength. Integrated cyber operations require card-slot resolution to compose across all four categories.
- **Economy across multiple categories** — Deliberately multi-faceted, explicitly defended in DESIGN.md's oil analogy.
- **Ideology: Attribute or System?** — Pan-Arabism, Political Islam exist simultaneously as Ideational Attribute + Normative System + Transnational Network. Multi-faceting handles it.

---

## Interaction Edge Residuals (all defended, none requiring action)

- **Time-Dependent Dynamics** (hysteresis, thresholds, lag) — Simulation-layer concerns for D1, not ontological gaps.
- **Multi-Category Emergent Phenomena** (state failure, revolution, proxy wars requiring 3-4 category interactions) — The pairwise edge descriptions are for human comprehension. The simulation processes all categories simultaneously through card-slot resolution. These phenomena should emerge naturally from the mechanics.
