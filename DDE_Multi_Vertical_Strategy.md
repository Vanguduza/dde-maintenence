# DDE — Multi-Vertical Strategy (All Industries)

**Document status:** Vertical strategy companion to `DDE_Maintenance_Intelligence_ERP_Master_Plan_v2.md`. Corrects the mining-only impression left by earlier research phases: the DDE platform is a **vertical-neutral core** serving all ten verticals named in master-plan v1 §70 — mining, manufacturing, energy, utilities, transport, construction, agriculture, facilities, heavy equipment, and processing industries. This document defines how each vertical is served, with evidence, and fixes the beachhead language: **verticals are packaging and sequencing choices, not product boundaries.**
**Date:** 22 August 2026
**Method:** Targeted research per vertical (construction downtime/utilization benchmarks; chemical/refinery downtime and mechanical-integrity economics; manufacturing data already established in the Industry Simulation). Evidence grades per section; limitations in §7.

---

# 1. The Architecture Principle: One Core, Many Packs

The master plan's canonical model (asset → component → failure mode → job → part → person → cost) is deliberately industry-agnostic. What varies by vertical is:

1. **Asset families & failure libraries** (§17.2 OEM library program scopes per asset class)
2. **Protocol emphasis** (J1939/CAN for mobile equipment; Modbus/OPC UA/PROFINET/HART for process plants; BACnet/KNX-class for facilities)
3. **Statutory compliance templates** (§15.6 register engine — one engine, many jurisdiction × industry templates)
4. **Workflow emphasis** (turnarounds for process; utilization/dispatch for fleets; validation trails for regulated manufacturing)
5. **Economics sanity bands** (downtime cost per hour differs 60:1 across sectors)

Nothing above requires separate products. It requires **Vertical Packs** — configuration + content + compliance templates on the common core. The master plan already contains this mechanism (§14.1 "Vertical packs," §17.10–17.11); this document generalizes it from two packs to ten verticals with an explicit readiness ranking.

# 2. Vertical-by-Vertical Assessment

## 2.1 Mining & heavy equipment — Beachhead (unchanged)
Covered fully in `DDE_Zimbabwe_Market_Entry_Research.md` and §14.2. Downtime $5k–$10k/hr for large haul trucks; J1939 DNA applies directly. First reference market: Zimbabwe.

## 2.2 Construction & civil contracting — **Co-beachhead (promoted)**
**Evidence grade: B (industry benchmark aggregations; Construction Industry Institute/McKinsey citations).**
- Downtime: **$500–$1,000+/hr per machine; $2,000–$10,000/day** once idle crew wages, rental replacement and milestone penalties are counted; a single critical-path breakdown cascades across 2–4 connected sites (3–5× multiplier).
- Utilization waste is huge: average tracked-fleet utilization 55–65%, untracked 30–40%; best-in-class 80–85% via telematics. Emergency rentals run 20–50% premiums. Telematics+CMMS integration cuts unplanned downtime 40–48%.
- Fit with DDE: mobile assets are J1939-standard; jobs are project-based (the dependency/knock-on engine maps naturally to site→project→contract-penalty chains); offline-first matches remote sites; the fleet pack (§17.11) serves construction nearly unchanged.
- Differences vs mining: shorter asset ownership cycles, rental/subcontractor mixing, weather as schedule constraint (v1 §7.3 lists weather already), liquidated-damages economics instead of production-loss economics. Requires a **Construction Pack**: project/WBS structure on the work-order model, rental-asset handling (owned + rented mixed fleets), contract-penalty input type in the Economics Profiler (already supported: "contractual penalty exposure" row in §8.2), site-based (not plant-based) location hierarchy.

## 2.3 Chemical, oil & gas, processing industries — **Phase 2 target (high value, higher bar)**
**Evidence grade: B− (consistent trade figures; vendor-leaning sources).**
- Downtime: refinery/petrochemical units commonly cited at **$100k–$500k/hr** (daily losses $3.6M–$12M downstream); mid-sized refineries lose $25M–$50M/yr profit to unreliability; rotating equipment (pumps/compressors/agitators) dominates failure cost.
- Compliance is the wedge, not just ROI: OSHA PSM 1910.119(j) **mechanical integrity** mandates written procedures, documented inspections to API 510/570/653, deficiency correction, and records retained for equipment life. Seveso III equivalents in EU. This is *exactly* the statutory-register + evidence engine DDE ships anyway.
- Fit: process-industry protocols (Modbus, OPC UA, HART, PROFINET) are already in the v1 connectivity fabric; shutdown/turnaround management (v1 §33) is a process-industry requirement; bad-actor/Pareto analytics fit rotating-equipment fleets perfectly.
- Higher bar: longer sales cycles, existing APM spend (AVEVA/GE/APM-class at $5–30k/site/mo — which validates pricing but raises proof burden), OT security scrutiny (IEC 62443 posture mandatory — already planned), and safety consequences that demand mature governance. Enter after fleet references exist; lead with mechanical-integrity compliance, sell predictive second.

## 2.4 Manufacturing (discrete + FMCG) — **Core market, Phase 1–2**
Already established in the Industry Simulation ($36k FMCG – $2.3M automotive/hr; 800 hrs/yr average downtime; 70% CMMS adoption with 49% parallel spreadsheets). Fit is broadest: every capability maps. Differentiation vs incumbents (Maximo/Joule agents) rests on the cross-system dependency graph and field-execution depth. Sub-verticals sequence by data availability: food/beverage and consumer goods first (lower IT walls), automotive-tier suppliers next, pharma last (validation overhead — see 2.8).

## 2.5 Energy & utilities — Phase 3 (per original plan)
Long cycles, high governance (NCI/NERC-class regimes in some markets), but enormous asset bases and existing historian estates (PI) that suit the overlay. GE Vernova/AVEVA own mindshare here; enter with reference base from other verticals.

## 2.6 Transport & logistics fleets — **Phase 1–2 natural extension of the Fleet Pack**
Trucking/bus/coach fleets share everything with the construction/mining mobile profile: J1939/FMS-standard data, telematics ubiquity, maintenance-cost-per-km economics, roadworthiness compliance registers (§15.6 already includes them). The v1 CAN DNA applies unchanged. Regional carriers without OEM walled-garden leverage are the sweet spot.

## 2.7 Agriculture — Watch list
Large agri-machinery is increasingly J1939/ISOBUS-standard and downtime is seasonal-critical (harvest windows = extreme downtime cost concentration). But buyer fragmentation, thin margins, and connectivity gaps make this a later-market via dealer/OEM partnerships rather than direct sales. Revisit after Fleet Pack matures.

## 2.8 Facilities management & healthcare/pharma-adjacent — Split verdict
- **Facilities/buildings:** compliant-fit (maintenance + compliance registers) but low downtime economics ($448–$760/day per vehicle; building systems lower still) and crowded CMMS market. Serve opportunistically through the core; no pack before Phase 3.
- **Pharma/regulated manufacturing:** GMP computerized-systems validation (GAMP 5 / 21 CFR Part 11 where US-jurisdiction applies) makes this the highest-compliance-burden entry; deliberately deferred — the e-signature/audit-trail architecture (§15.10) keeps the option open without committing now.

## 2.9 Summary matrix

| Vertical | Downtime economics | Data access | Compliance pull | Sales cycle | Verdict |
|---|---|---|---|---|---|
| Mining/heavy equipment | Very high | Good (gateway path) | Medium-high | Medium | **Beachhead** |
| Construction | Medium-high ($2–10k/day) | Good (telematics standard) | Low-medium | Short-medium | **Co-beachhead** |
| Transport fleets | Medium | Excellent (FMS standard) | Medium (roadworthiness) | Short-medium | Phase 1–2 |
| Manufacturing discrete/FMCG | High | Mixed | Medium | Medium | Phase 1–2 core |
| Chemical/O&G/process | Very high | Excellent (historians) | Very high (PSM/API) | Long | Phase 2 |
| Energy/utilities | Very high | Excellent | High | Long | Phase 3 |
| Agriculture | Seasonal-extreme | Good | Low | Fragmented | Watch list |
| Facilities | Low-medium | Poor (BMS silos) | Medium | Short | Opportunistic |
| Pharma/GMP | High | Good | Extreme | Very long | Deferred |

# 3. Product Implications (What Changes in Build Order)

1. **Work-order/project linkage** gains priority (construction co-beachhead): work orders must roll up to projects/cost codes, not only assets/locations. Small schema addition, big vertical reach.
2. **Rental & mixed-ownership fleet handling** joins the Fleet Pack backlog (owned vs rented vs subcontractor assets; rental-cost lines feeding the economics engine).
3. **Compliance template factory confirmed as multi-vertical from day one:** SI 109/1990 (mining, ZW), roadworthiness schemes (transport), API 510/570/653 mechanical integrity (process), LOLER/PUWER (UK industrial) share one register engine — build the engine generically, templates per vertical/jurisdiction.
4. **Failure-mode library scoping order (§17.2)** follows the verdict matrix: mobile equipment (mining/construction/transport share it) → generic rotating equipment (manufacturing + process) → process-static equipment.
5. **Economics Profiler penalty types** extend: liquidated damages (construction), production-loss (mining/manufacturing/process), margin-per-delivery (transport).

# 4. Go-to-Market Implications

1. **Beachhead becomes a two-pack motion:** Mining (Zimbabwe-first per prior research) + Construction (same geography, same gateway hardware, same buyer persona overlap — fleet managers move between both industries). Two packs on one pilot platform halve the cost of proof.
2. **Messaging spine stays vertical-neutral:** "Know what's breaking, prove what you fixed" works across all ten; vertical packs supply the vocabulary (haul trucks vs excavators vs compressors).
3. **Partner channels differ by vertical and are named now:** construction equipment dealers and rental houses (they already service mixed fleets); Chinese-OEM importers for Tier 2/3 mining and construction; SA-based process consultancies for chemical later.
4. **Pricing unchanged structurally** — Field/Reliability/Operations tiers apply to every vertical; construction uses technician+asset blended bands (crews rotate machines more than plants do).

# 5. Sequencing (Updated Delivery View)

- **Phase 0–1 (unchanged core):** platform + connectors + Fleet Pack; pilots in Zimbabwe mining AND at least one construction fleet (co-beachhead proof).
- **Phase 2 additions:** Construction Pack (project linkage, rentals), Transport Pack profile of the Fleet Pack (roadworthiness registers, per-km economics), Manufacturing overlay plays against SAP/Maximo estates.
- **Phase 3 additions:** Process/Chemical Pack (API mechanical-integrity templates, turnaround module prominence), Utilities/Energy entry, opportunistic facilities deals, agriculture reassessment.

# 6. What Did Not Change

The full-scope MVP directive stands: every v1 capability plus research additions remains in scope for planning; vertical packs are mostly *configuration/content* on the common core. The compliance framework, economics lineage rule, alert-trust system, workforce governance, and sync architecture are all vertical-neutral already — no architectural rules change. §3's three items are small schema/backlog extensions (project linkage, rental handling, penalty types), not new subsystems; they are absorbed into existing pack workstreams rather than expanding MVP scope.

# 7. Limitations

- Construction and chemical figures come from benchmark aggregators with vendor leanings (grade B/B−); directionally consistent across sources but not audited.
- Transport/agriculture/facilities assessments rest partly on structural reasoning rather than dedicated primary research; each needs a targeted pass before its phase entry.
- Zimbabwe-specific evidence exists only for mining; construction-sector sizing in the first market needs groundwork (contractor registries, fleet sizes) before committing pilot inventory.
