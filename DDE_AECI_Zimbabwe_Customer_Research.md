# DDE — AECI Mining Explosives (Zimbabwe) First-Customer Research

**Document status:** Desk-research evidence pack on AECI Mining Explosives Zimbabwe as candidate first customer for the DDE Asset Operations Intelligence Platform. Companion to `DDE_Maintenance_Intelligence_ERP_Master_Plan_v2.md` and `DDE_Zimbabwe_Market_Entry_Research.md`.
**Date:** 22 August 2026
**Method:** Targeted web research: Mining Zimbabwe interview with AECI Mining MD Alois Kwenda (Nov 2023); AECI Mining / AECI World corporate pages (Smart Delivery Systems, Surface Bulk Systems brochure); International Mining & E&MJ coverage of the Zimplats Ngezi contract history; AECI interim results 2024; Zimplats FY2026 quarterly reporting; Unki EVDS launch coverage; Intrachem competitive material; Zimbabwe Explosives Act [Chapter 10:08] and SI 72/1989. Evidence grades assigned per section; limitations in §11.

---

# 1. Why This Customer, and What Question This Answers

> **Configuration note:** The customer-specific platform customization derived from this research is specified in `DDE_AECI_Operations_Pack_Config_Spec.md` (asset taxonomy, statutory registers incl. VID/COF/ZINARA road-fleet compliance and Ministry-of-Mines manufacturing licence, security-system coexistence layer, workflows).

The prior market-entry research (`DDE_Zimbabwe_Market_Entry_Research.md`) treated mines as DDE customers. **AECI Mining Explosives Zimbabwe is a different, arguably better first customer:** it is an explosives *services* provider whose technicians maintain and service the specialized equipment fleet — mobile charging units, transfer pumps, storage facilities — deployed across surface open-pit sites around the country and underground at Zimplats' Ngezi complex. That is exactly the maintenance-execution problem DDE digitizes, concentrated in one customer with a single commercial relationship.

This document answers: (1) who is the customer and how is the Zimbabwe operation structured? (2) what equipment do their technicians maintain, and what does servicing that equipment involve? (3) where are the sites? (4) what regulatory burden shapes their maintenance records? (5) does DDE fit, and what is the entry strategy?

**Headline verdict:** AECI Zimbabwe is a **strong lighthouse-first-customer profile** — a subsidiary of a JSE-listed multinational with deep SLA/KPI culture, a documented 20-year LTI-free safety record, a dispersed multi-site technician footprint, explosive-handling compliance obligations that demand auditable maintenance evidence, and equipment criticality measured in halted blast cycles rather than halted production lines. Desk research confirms structure and context; fleet size, site count and CMMS state require groundwork discovery.

---

# 2. The Customer: Corporate Structure and Zimbabwe Footprint

**Evidence grade: B+ (corporate primary sources + named local leadership).**

## 2.1 Corporate identity

- AECI Mining Explosives is the explosives pillar of **AECI Group** (JSE-listed chemicals group, HQ Woodmead, Sandton): >3,000 employees, 16 businesses, 58 plants, 34 sites across Africa plus South-East Asia, Australia, South America, Europe.
- Manufactures >420,000 t/yr of ammonium nitrate (dense + porous prill), AN solution, and >120M detonator assemblies; operates scalable modular bulk emulsion plants designed for rapid deployment to new regions.
- Formerly **AEL Mining Services** — the name under which most Zimbabwe-specific history was published. Zimbabwe entity historically trades as **AEL Zimbabwe / AECI Explosives Ltd**, Harare.

## 2.2 Leadership and operating model

- **MD AECI Mining Zimbabwe & Mozambique: Alois Kwenda** (mining engineer; joined AECI Zimbabwe 1994; headed company from May 1999; returned August 2018). **Regional Manager (Harare): Moshen Jena** (explosives engineer, ~13+ years in the Zimbabwe business).
- Operating model per Kwenda: "holistic mining solutions" — products + equipment + technical expertise — delivered under **service level agreements with specific KPIs** against which products and services are measured. This SLA/KPI culture matters commercially: a customer that already runs its own business on measured KPIs will understand exactly what DDE's value scorecards measure.
- Safety culture: **20 years LTI-free** in Zimbabwe (2023), multiple AECI SHEQ conference awards; "Zero Harm" driven as organizational culture. A workforce already rewarded for safety ideas is culturally aligned with DDE's safety-native execution spine.

## 2.3 In-country infrastructure

- **In-country bulk emulsion plant + strategically located storage facilities**: announced 2023 as an advanced-stage partnership with local companies targeted for Q2 2024 commissioning. Purpose: local product availability and simplified supply chain/logistics serving multiple mining projects. Status beyond announcement not confirmed in public sources (see §11) — but either way, emulsion is currently trucked in dedicated road tankers from South Africa into site silos, so tanker + silo infrastructure exists regardless of plant status.
- Historically supplied from Johannesburg bulk plant by dedicated road tankers into **on-site storage silos** at Ngezi (Zimplats).
- Small-scale miner segment served through **local distributors supported by AECI technical personnel**.

## 2.4 Competitive context (why this customer's position strengthens the case)

- **Intrachem (est. 1990)** is the main domestic challenger: sole Sasol distributor since 2014, ex-BME agent, new Austin Powder partnership, Kwekwe plant (~$7M, phased: bulk emulsion + detonator assembly), wide branch network, explicit ambition to be "Zimbabwe's premier explosives manufacturer," and a services model ("cutting-edge equipment, highly skilled technicians") directly mirroring AECI's.
- Strategic read: AECI's moat vs Intrachem is technology depth (electronic initiation, Smart Delivery Systems, BlastHub digital ecosystem) and enterprise engineering standards. **Maintenance reliability of the delivery-equipment fleet is part of that moat** — a stalled charging unit or failed transfer pump at a customer mine is an SLA breach. This gives AECI Zimbabwe an internal reason to want better asset operations intelligence, which DDE can arm.

---

# 3. The Equipment: What Their Technicians Actually Maintain

**Evidence grade: B+ (manufacturer product literature + documented installations; exact Zimbabwe unit counts unknown).**

AECI Mining Explosives' "Smart Delivery Systems" portfolio defines the maintained asset classes:

| Equipment class | Function | Maintenance-relevant characteristics |
|---|---|---|
| **Mobile Manufacturing Unit (MMU)** | On-bench manufacture of bulk emulsion (two non-explosive components mixed only at delivery) and pumped/augered delivery into blast holes; surface open pits | Truck-mounted chemical process plant: tanks, pumps, hoses/reels, augers, dosing/sensitizer systems, PLC controls. Current generation 20t payload with higher pumping rates. "Smart MMU" variants add wireless data comms + GPS blast-hole positioning. Fleet refilled on-bench via rapid re-loader system (RRS), re-pump trucks or tankers |
| **Mobile Charging Unit (MCU)** | Underground charging in demanding normal mining conditions; also documented in fleets of five at Unki pre-EVDS | Smaller vehicle-mounted pumping/skidding units for underground development/bord-and-pillar charging |
| **Portable Charging Unit (PCU)** | Narrow-reef mining, development and shaft-sinking, small shaft applications | Man-portable units — pumps, hoses, small hoppers; high wear items, manual handling damage class |
| **Rapid Re-loader System (RRS) / re-pump trucks** | Bench-side refill of MMUs (prill via RRS; emulsion via re-pump/tankers) | High-throughput transfer duty cycle — pump seals, valves, meters |
| **Emulsion Vertical Drop System (EVDS)** | Gravity/piped reticulation of base emulsion + sensitizer from surface storage to underground storage near workings (documented: 184 m drop at Unki 2016; 680 m and 980 m levels at NFCA Zambia) | Fixed plant: surface tanks, vertical piping string, underground receiving stations, valves, instrumentation; frees cage time; enables "emulsion on tap" |
| **Storage silos & magazines** | Emulsion silos at mine sites (Ngezi documented); licensed magazines for detonators/cartridge product; new strategic storage network | Licensed structures under Explosives Act; security, containment, condition of tanks/piping; inventory monitoring feeds AECI's automated supply-chain portal |
| **Transfer pumps & road tankers** | Emulsion movement: manufacturing plant → road tanker → silo → MMU/RRS → blasthole | Positive-displacement/progressive-cavity type duties; seal/valve/hose wear; metering accuracy affects both billing and blast quality |

Cross-cutting reality: every item above handles **ammonium nitrate emulsion (and sensitizers such as sodium nitrite)** — corrosive, abrasive, crystallization-prone media. Pump seals, hoses, valves and tanks fail predictably with duty cycle; density/viscosity QC tests run daily at plants and per-charge at MMUs, generating structured test data DDE could ingest. Product is only manufactured on mixing, so equipment failure modes carry direct blast-cycle and contractual consequences.

## 3.1 Where technicians fit

The user's framing — technicians at these sites responsible for maintaining and servicing charging units, transfer pumps and storage facilities — matches the industry-standard deployment model for explosives service providers: resident technicians/fitters at major serviced sites (e.g., Ngezi-class contracts), regional roving coverage for smaller surface customers, workshop support in Harare. Public postings confirm AECI Zimbabwe employs technical personnel embedded at customer operations; exact headcount and skills mix per site are groundwork questions.

---

# 4. Site Map: Surface Operations and the Zimplats Underground Complex

**Evidence grade: B (documented relationships; current full customer list not public).**

## 4.1 Anchor underground: Zimplats Ngezi Mining Division

- Relationship since **2001** — initial three-year Prime, Load, Tie and Shoot (PLTS) contract for the then-open pit; >70,000 t emulsion and ~60M m³ (bank) blasted using **four AEL MMUs** during the open-pit life; first electronic-detonator user in Zimbabwe.
- Underground transition from 2008–2009: UBS + Tunnelmaster shock tube accepted for bord-and-pillar after trials; SDD bulk emulsion developed as cost-effective alternative to R100G; supply via road tankers into **on-site storage silos**.
- Zimplats today (Implats fact sheet + FY2026 quarterlies): **five underground mines (Bimha, Mupani, Mupfuti, Rukodzi, Ngwarati) + Ngezi concentrator complex**; Mupani replacement project US$364M spent of US$386M budget, on track for 3.6 Mtpa design capacity FY2029; Bimha upgrade complete (design capacity 3.1 Mtpa); short-term open pit producing ore since Feb 2025; 185MW solar program; Selous Metallurgical Complex (concentrator + expanded smelter) 77 km north.
- Implication for DDE: a growing, well-capitalized underground estate where the AECI service footprint (MCUs, possibly EVDS-class reticulation, silos) scales with tonnage through FY2029 — a multi-year expanding asset base at a Tier 1 host.

## 4.2 Documented surface relationships

- **Eureka Mine (Guruve — Dallaglio/Padenga gold):** IntelliShot® electronic initiation rollout (buffer/ore blasting first, then full), contractor-mining model, comprehensive training under Management of Change; described as "blueprint" for the sector. Confirms active AECI service teams at large open-pit gold.
- **Hard-rock open-pit gold mine (Feb 2023 project, unnamed):** fragmentation enhancement, won from competitor, converted to a three-year contract — evidence of competitive displacement wins at open pits.
- **Lithium open pits:** Kwenda publicly targets the lithium boom (multiple new open pits coming online); no named public contracts at Bikita/Arcadia/Kamativi yet, but these are precisely the fast-growing surface sites matching the user's description of "surface operations at different open pit mines around the country."
- **Unki Mine (Shurugwi — Anglo American Platinum):** first Emulsion Vertical Drop System in Zimbabwe launched 2016 (184 m); five MCUs' daily travel cut 110 km→20 km; savings ~$26k/yr plus $10k fuel; safety benefit framed around reduced interface time with explosives. Whether this estate remains AECI-operated currently needs confirmation — but it demonstrates the installed fixed-plant class at Zimbabwean platinum operations.
- **Quarrying/construction:** electronic initiation deployed at Zimbabwean quarry operations (Coedmore is SA; Ngezi is the Zimbabwe reference).

## 4.3 Geographic spread

Harare head office; service reach implied by distributor network and customer geography: Mashonaland West (Ngezi/Zimplats; Guruve/Eureka), Midlands (Shurugwi/Unki; Kwekwe area), Matabeleland (lithium belt: Bikita is Masvingo; Kamativi and Arcadia/Harare region), i.e., a genuinely national service radius — matching the "different open pit mines around the country" framing. Each site = a technician team, an equipment set, travel distances, and a maintenance records problem.

---

# 5. Regulatory Burden: Why Their Maintenance Records Are Compliance Objects

**Evidence grade: A− (primary statute/regulations read directly; SI 109 obligations carried over from prior pack).**

Two statutory layers sit on top of ordinary OSH law:

1. **Explosives Act [Chapter 10:08] (originally Act 9 of 1961) + Explosives Regulations SI 72/1989.** Ministerial regulations explicitly cover: construction and management of magazines and prevention/detection of loss or theft; storage conditions; conditions of manufacture; registers to be kept (s.(m)); licensing of premises with approved plans, quantity limits, separation rules (detonators separate from high explosives), fencing, locking, inspection regimes; deterioration/destruction procedures; loading precautions at magazines; criminal penalties for non-compliance.
   - **DDE mapping:** magazine/silo statutory register (licence numbers, expiry, permitted quantities, inspection evidence); loss/theft detection implies stock reconciliation records; deterioration tracking implies shelf-life/condition monitoring records; manufacture conditions imply plant + MMU calibration/QC evidence trails.
2. **Mining (Management and Safety) Regulations SI 109/1990** (carried from `DDE_Zimbabwe_Market_Entry_Research.md`): competency appointments (FBL/MBL), PPE, accident investigation timelines, NSSA obligations — apply equally to AECI staff embedded at customer sites.

Additional operational overlay: **SHERQ management-system audits within AECI group** (the 20-year LTI record is externally recognized at group SHEQ conferences) mean internal audit evidence demands stack on top of statutory ones — exactly the "audit evidence pack" posture DDE ships.

**Implication:** maintenance records at this customer are not just productivity tools — they are legal and contractual objects. An AI-maintenance platform that produces inspector-ready, hash-bound evidence (DDE §15.6 register engine + §17.29 PDF engine) converts a compliance chore into the platform's beachhead use case.

---

# 6. Digital Environment: Coexistence Analysis

**Evidence grade: B− (vendor marketing + press; actual Zimbabwe deployment depth unverified).**

What AECI Mining Explosives already runs globally:
- **Smart MMUs:** GPS blast-hole positioning, wireless data communication, computer-controlled delivery; autonomous-MMU technology patented/in development.
- **BlastHub™ portal:** predictive blast-design tools; closed loop linking products to performance via cloud.
- **Automated supply-chain exchange portal:** mobile proof-of-delivery, real-time material flow, **silo monitoring**, transport management, PO/delivery-note/invoice three-way match, global track-and-trace.

Interpretation for DDE positioning: AECI's digital layer covers **blast outcomes and logistics**, not **asset maintenance execution**. There is no public evidence of an AECI-branded CMMS/EAM for the delivery-equipment fleet; equipment maintenance is managed with conventional tools (ERP work orders, paper/planned-maintenance systems — Zimplats-class hosts run SAP, and AECI staff at such sites typically live inside the host's permit-to-work systems too). DDE's Mode A/B overlay story therefore applies cleanly: ingest maintenance-relevant signals (MMU telemetry, silo levels, QC density/viscosity results, pump hours) without displacing SAP/BlastHub/supply-chain portal.

Data-path note: Smart MMUs generate machine data (GPS, pump rates, tank states). Whether Zimbabwean-fleet MMUs stream telemetry to a regional platform, and whether API access can be secured, is a §11-grade unknown — the same OEM-telematics-rights question the master plan flags for mining fleets (§17.11 dual-path logic applies: gateway ingestion if OEM APIs are unavailable).

---

# 7. Operating Environment Constraints (carried forward, now applied to AECI)

From `DDE_Zimbabwe_Market_Entry_Research.md` (grades unchanged): USD economy and payment-rail unreliability → USD annual-prepay contracting; ZESA fragility and remote-site connectivity → offline-first is entry ticket; skills base strong (Zimbabwe School of Mines, apprenticeship artisan tradition — Class 1 fitters standard) → technician-facing tablet/kiosk UX viable; English business language → zero localization cost.

Specifically relevant to AECI: their sites are *customer* mines, so field devices must work at third-party sites with variable power/connectivity; technicians move between sites, making mobile/offline job packages the natural fit; blasting windows are schedule-critical, so equipment availability failures have outsized, easily-measured costs (a missed blast window at a mine is a visible SLA event).

---

# 8. Fit Assessment: Where DDE Lands in This Account

## 8.1 Asset scope (from user's brief + research)

- Charging units (MCUs underground at Ngezi; PCUs/MCUs at surface sites), MMU fleet where AECI operates PLTS/bulk delivery, rapid re-loaders/re-pump trucks.
- Transfer pumps (tanker offload, silo recirculation, EVDS strings, bench re-pump).
- Storage facilities (emulsion silos, licensed magazines, EVDS surface tanks and underground stations, planned strategic storage network).

## 8.2 Highest-value DDE capabilities for this account (mapped to master plan)

| AECI Zimbabwe need | DDE capability |
|---|---|
| Statutory magazine/storage registers, licence expiries, inspection evidence | §15.6 register engine with Zimbabwe explosives template (new jurisdiction template required) |
| Auditable servicing evidence per unit for SLA/KPI defence and SHEQ audits | Evidence capture + §17.29 PDF conversion of existing checklists/service sheets |
| Technician workflows across dispersed, low-connectivity sites | Offline-first tablet/kiosk Field Experience layer (§17.23–26), job packs |
| Pump/seal/hose failure patterns across similar units at multiple sites | Cross-site bad-actor analytics + Federated Reliability priors (§17.1) |
| QC test streams (density/viscosity per charge) as early failure signals | Condition-data ingestion; WO Text Intelligence on service notes |
| Availability assurance ahead of scheduled blasts | Readiness gate + dependency view tying equipment state to blast schedule risk |
| Duty-cycle-based component replacement (pumps, hoses) | Component-life tracking by serial number (Fleet Pack mechanics, repurposed to process-mobile assets) |

## 8.3 Commercial shape

Buyer: AECI Mining Zimbabwe (Kwenda/Jena line) with group IT/engineering visibility. Pilot shape consistent with master plan §14.5: one region or one anchor site (e.g., Ngezi underground service crew + one surface site), 90-day exit-criteria pilot with pre-agreed conversion pricing; USD annual-prepay invoicing; SDN screening; POTRAZ processor obligations per prior pack. Success metric candidates: % PM completion within window, pump/charger downtime hours avoided before blast windows, statutory-register completeness, evidence-pack retrieval time for audits.

## 8.4 Risks and disqualifiers to probe

1. **Group IT gravity:** AECI may mandate group-standard systems from South Africa; a local pilot may need Sandton sign-off (slower, but converts bigger if won).
2. **Incumbent ERP:** if Zimbabwe runs group SAP PM for fleet maintenance, DDE enters as overlay/analytics, not system-of-record — acceptable, but changes pilot metrics toward decision intelligence rather than WO capture.
3. **Safety conservatism around intrinsically-safe device policy:** tablets near explosives handling areas face hazardous-area classification questions (Zone 1/21 and mining Group I devices are already in DDE's certified-hardware matrix — lead with certified devices).
4. **Small footprint risk:** if the entire Zimbabwe technician population is <25 people, the account may be a lighthouse reference rather than a revenue anchor — price accordingly and exploit the reference across AECI's 20-country footprint (the real prize: "referenceable multinational whose other subsidiaries become DDE's expansion path").
5. **Competitive sensitivity:** AECI will not adopt tooling that leaks operational data toward Intrachem/Sasol channels — DDE's C-tier commercial-confidentiality doctrine (§17.30) should be pitched explicitly.

---

# 9. What Changed in Strategy Terms (vs prior packs)

1. **Customer-class correction:** prior packs assumed mines buy maintenance software; the AECI thesis shows the *service provider* tier (explosives, drilling services, contractor miners) is a distinct buyer class with concentrated multi-site technician teams and contractual KPI pressure — arguably faster to say yes than a Tier 1 mine IT department.
2. **Beachhead packaging:** a new "Explosives Service Provider" variant of the Mining Pack (§17.20) is warranted: charging-unit/MMU/pump/silo asset templates, explosives-regulation register template (Explosives Act + SI 72/89 alongside SI 109), blast-window readiness gates.
3. **Reference cascade:** winning AECI Zimbabwe opens (a) rest-of-country sites, (b) Mozambique (same MD), (c) AECI group's 20+ country footprint, (d) the serviced mines themselves as second-hop customers — a structurally cheaper expansion path than greenfield mine-by-mine sales.
4. **Pilot sequencing note:** AECI Zimbabwe and a Tier 2 lithium/gold mine (prior pack's recommended pilot) are not mutually exclusive; AECI's presence *at* those mines makes co-selling plausible — one data platform spanning provider + host.

---

# 10. Groundwork Discovery List (questions only a visit can answer)

1. Exact site list, technician counts and skills mix per site; Harare workshop role and capacity.
2. Current maintenance system of record (group SAP? Pronto? spreadsheets?) and who owns fleet maintenance data.
3. Zimbabwe MMU/MCU fleet size, age profile, telemetry fitment; whether Smart-MMU data reaches any regional dashboard.
4. In-country emulsion plant status post-Q2 2024 target (commissioned? scaled back?) and resulting change in silo/tanker/pump estate.
5. Current EVDS-type installations at Zimplats/Unki and pipeline for more.
6. Who signs software procurement locally vs Sandton; existing group digital-vendor framework agreements.
7. Statutory inspection cadence and evidence formats used today (paper registers? photos? PDFs?) — input to the §17.29 template library.
8. Failure-cost anecdotes: recent blast-window misses attributable to equipment — the seed of the Economics Baseline (§8.4).

---

# 11. Limitations & Evidence Gaps

- No AECI Zimbabwe-specific financials or headcount published; site count and fleet size inferred from contract history and product deployments (grade B sections rely on dated sources: Ngezi contract detail is 2001–2010 era; Unki VDS is 2016; Eureka is recent).
- The in-country plant announcement (2023) lacks confirmed commissioning status in public sources found.
- Competitive displacement wins prove capability but the current customer roster (which lithium pits, whether Unki remains AECI-serviced) is unpublished.
- AECI's internal maintenance-system landscape (SAP modules, any group CMMS) could not be verified from public sources.
- All Zimbabwe legal citations (Explosives Act Ch. 10:08; SI 72/1989) reflect desk reading of ZimLII/studylib copies; currency of amendments should be confirmed by local counsel alongside the POTRAZ/SI 109 counsel review already planned in `DDE_Zimbabwe_Market_Entry_Research.md`.
