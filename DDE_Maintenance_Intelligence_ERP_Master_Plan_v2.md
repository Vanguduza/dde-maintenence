# DDE Asset Operations Intelligence Platform
## Master Product & Delivery Plan — Version 2.0 (Gap-Closed Enhancement)

**Document status:** Master plan — supersedes the v1 consolidated feature vision (`DDE_Maintenance_Intelligence_ERP_Product_Features.md`), which is retained as the capability catalog input.
**Date:** 22 August 2026
**Planning directive for this version:** The MVP scope is intentionally **maximal** — it includes every capability identified in v1 **plus** research-derived additions — so that planning is done in full and trimming happens later as an explicit, evidence-based decision. A separate mandatory sequencing gate (Section 4) converts this full catalog into a shippable release order; the trim decision itself is deferred by design.

**What changed from v1:** This version closes all twelve gaps identified in the independent evaluation of v1:

| # | v1 Gap | Closed in |
|---|--------|-----------|
| 1 | No MVP / cut line | §4 Full-Scope MVP + §4.4 Sequencing Gate |
| 2 | Zero competitive analysis | §3 Competitive Landscape & Differentiation Thesis |
| 3 | Economics engine lacks data sourcing | §8 Economics Data Model |
| 4 | Model cold start unaddressed | §9 Cold Start Strategy |
| 5 | Alert-fatigue risk ignored | §10 Alert Precision & Trust Management |
| 6 | Technician scoring culture risk | §11 Workforce Intelligence Governance Charter |
| 7 | Integration reality understated | §12 Integration & Write-Back Architecture |
| 8 | Offline sync conflicts unsolved | §13 Offline-First Sync & Conflict Resolution |
| 9 | No commercial model | §14 Commercial Model |
| 10 | Standards mapping missing | §15 Compliance & Regulatory Framework (standards, legislation, regulators, deadline calendar) |
| 11 | Hardware-heavy features in scope | §4.4 Sequencing Gate + §16 Delivery Phases |
| 12 | Naming risk | §2 Naming & Positioning Decision |

Plus **thirteen research-derived capability additions** (§17) that v1 did not identify — including the **full industry pack suite** (§17.11, §17.13–§17.21: Fleet & Telematics, Construction, Transport, Agriculture, Facilities, Energy & Utilities, Pharma/GMP, Food & Beverage, Mining, Manufacturing & Process) so every industry DDE serves has named, researched operational features and compliance registers, the **Modular Platform & White-Label Architecture** (§17.22) that makes per-client customization a matter of actioning branding and integration parameters rather than code, and the **Field Experience layer** (§17.23–§17.26): role-specific kiosk/tablet/web/desktop applications with structured role dashboards, a certified rugged-hardware compatibility program (MIL-STD-810H/IP66+, intrinsically-safe Zone 1/21 and mining Group I devices), and carry/mount ecosystems (hand straps, harnesses, magnetic workface mounts, vehicle docks, wall kiosks) proven against drops, spills and washdowns. Also includes **WO Text Intelligence** (§17.12), added after the Industry Simulation Research (`DDE_Industry_Simulation_Research.md`) showed free-text work-order descriptions are the most recoverable data source at typical sites, where structured failure codes are the least reliable.

---

# 1. Executive Summary

DDE is an AI-native, safety-first, asset-centric operational platform that connects assets, people, procedures, risks, sensors, stores, production and finance into one continuously learning system. It operates standalone (Mode C), as an intelligence overlay above incumbent EAM/ERP systems (Mode A), or as an operational orchestrator between those poles (Mode B).

v1 established a credible, domain-deep product vision. This v2 makes it executable and defensible: it names the competitors and states why DDE wins; it specifies where every economic number comes from; it solves cold start, alert fatigue, write-back conflicts and offline merge before they kill adoption; it governs workforce analytics to the standard regulators and works councils will demand; it prices the product; and it maps every obligation to the standards that appear in target-customer RFQs.

Per the planning directive, the MVP defined in §4 is the **full catalog** (all v1 sections 1–77 plus the §17 additions). The sequencing gate is the mechanism by which this full plan becomes a series of shippable increments; nothing in the catalog is silently dropped.

# 2. Naming & Positioning Decision

**Decision:** The market-facing name is **DDE Asset Operations Intelligence Platform**. The internal working name "DDE Maintenance Intelligence ERP" is retired from all external material.

Rationale and rules:

- "ERP" is retired from external use. It invites a like-for-like comparison against SAP S/4HANA in procurement evaluations that DDE cannot win and does not want. v1 §76 itself proposed "Asset Operations Intelligence Platform"; this version adopts it.
- The acronym **DDE must be expanded on first use in every document** ("DDE — *Digital Diagnostics Engine*" as the working expansion, to be confirmed by trademark search before any public use). v1 never expanded it; the expansion must also be checked for collision with the legacy Dynamic Data Exchange protocol and trademark registers in target markets (US, EU, AU, ZA, BR) before launch.
- Positioning sentence for all external material: *"The intelligence layer that makes your existing maintenance systems, sensors and people measurably safer and more reliable — and proves it."*
- Category language: "Asset Operations Intelligence," not "ERP replacement." The replacement conversation (Mode C) is earned later, per §16.

# 3. Competitive Landscape & Differentiation Thesis

*(Closes gap #2. Research basis: public product documentation and 2026 market analyses of IBM Maximo MAS 9.x, SAP Joule/S/4HANA 2025–2026 agents, Siemens Senseye, Augury, AVEVA/GE Vernova APM, Aspen Mtell, Fiix/Rockwell, MaintainX, Limble, Tractian, Factory AI, Samotics, Petasense, Nanoprecise, Uptake/Bosch, C3.ai.)*

## 3.1 Incumbent EAM+AI stacks

| Competitor | What they ship in 2026 | Their structural weakness |
|---|---|---|
| **IBM Maximo Application Suite 9.x** | Manage (EAM), Monitor (IoT/anomaly), Health (condition scores), Predict (failure probability + auto-WO), Visual Inspection, Safety (permits), Assist (AR); "Condition Insight" agentic AI layer (late 2025, matured in MAS 9.2, June 2026) that produces natural-language condition summaries and corrective-action recommendations; AI Service LLM gateway; MCP server for third-party agents | Suite complexity and AppPoints licensing; OpenShift infrastructure burden; AI grounded in Maximo's own data model — cross-system correlation (ERP + OT + stores + production) is weak; overlay on non-Maximo estates is not their motion |
| **SAP** | Joule conversational AI embedded in S/4HANA Asset Management (2025): NL work-order creation, time confirmation, maintenance events; 2026 agentic wave — Asset Health Agent (predicts failure, triggers PM WOs), Alert Processing Agent, Field Service Dispatcher Agent (GA Q2 2026); Asset Performance Management with anomaly detection and failure-curve analysis | Grounded only in SAP data; requires RISE/BTP commercial constructs; OT/protocol depth is thin; asset intelligence stops at the SAP boundary; ECC customers face 2027 deadline pressure that consumes their budget |
| **Siemens (Senseye)** | Cloud PdM on existing historian/SCADA data, no proprietary sensors; RUL forecasts; EU-data-centre residency in writing; strong multi-site fleet standardization | PdM advisory only — no CMMS/EAM depth, no field execution, no safety/LOTO/permits, no stores; Siemens-ecosystem gravity |
| **GE Vernova APM / AVEVA Predictive** | Fleet reliability analytics deep in power/utilities and PI-historian estates respectively | Vertical-locked; advisory analytics, not operational orchestration |

## 3.2 Pure-plays and CMMS-attached challengers

| Competitor | What they ship | Their structural weakness |
|---|---|---|
| **Augury** | Hardware+software machine health (vibration/ultrasonic) on rotating equipment; human-verified diagnostics; 2026 agentic WO creation into connected CMMS | Proprietary sensor lock-in; 2–4 month deployments; no published EU residency; no CMMS/EAM of its own |
| **Fiix (Rockwell)** | CMMS with FactoryTalk/PLC-native integration; Foresight ML add-on | AI is shallow; Rockwell-ecosystem-bound |
| **MaintainX, Limble, UpKeep, Tractian** | Modern mid-market CMMS, mobile-first, fast setup; Tractian adds sensors + pretrained models | Mid-market depth; limited enterprise governance, OT protocol breadth, safety/LOTO, economics |
| **Aspen Mtell / AVEVA / Samotics / Petasense / Nanoprecise** | Process-failure signatures (Mtell), historian-native PdM (AVEVA), electrical-signature analysis (Samotics), retrofit sensing (Petasense, Nanoprecise) | Point solutions; each solves one slice |
| **Factory AI** | Sensor-agnostic PdM + native CMMS, 14-day deployment for brownfield mid-market | Mid-market focus; limited enterprise integration and governance |

## 3.3 Cautionary cases (design constraints, not just history)

- **Uptake** (founded 2014, once valued >$1B): pivots across industries, dashboard-without-workflow positioning, and dependence on partners' data access ended in acquisition by Bosch (2025–2026) to feed Bosch's telematics ecosystem. Lesson: **insights must land inside the work-execution workflow, and data access must be owned, not rented.**
- **C3.ai**: 2026 revenue collapse (−46%) after a forced consumption-pricing transition; pilots that did not convert. Lessons: **predictable enterprise pricing beats speculative consumption models in this segment, and pilots must be designed to convert, not to impress.**
- **Generic PdM alert products**: repeatedly died of alert fatigue (see §10). Lesson: **precision targets and trust metrics are product features, not tuning details.**

## 3.4 Differentiation thesis — where DDE wins, and why it is defensible

1. **Cross-system causal dependency graph (v1 §13, §65).** Every competitor's AI is grounded in *its own* data model (Maximo's AI reads Maximo; Joule reads SAP). DDE's canonical model correlates EAM + OT + stores + production + finance *regardless of incumbent*. This is the core defensible asset and the reason Mode A is viable against every incumbent simultaneously.
2. **Safety-native execution (v1 §21–23, §73).** No PdM vendor and no mid-market CMMS ships LOTO, permits, dynamic JSA and safe-device modes as first-class objects. Incumbents bolt permits on (Maximo Safety). DDE makes safety the spine of execution.
3. **Economic consequence engine with auditable inputs (§8).** Competitors show risk scores; none connect them to customer-specific production-loss economics with confidence intervals. DDE's VaR/Maintenance Debt numbers carry their data lineage — that is what survives a CFO review.
4. **Overlay neutrality.** IBM and SAP monetize staying inside their stack; their overlay story for *other* incumbents is structurally weak. DDE is system-of-record-agnostic by design (v1 rule 6/8).
5. **Field execution depth.** Offline-first job packages, evidence engine, competency-aware dispatch — the mid-market CMMSs have usability but not governance depth; the incumbents have governance but poor field UX.

**Competitive kill criteria (self-honesty clause):** If within 18 months DDE cannot demonstrate at least one of (a) a cross-system dependency insight that no single-system vendor could produce, (b) a safety-governed execution workflow incumbents lack, or (c) an economics number a CFO accepts — the differentiation thesis is wrong and strategy must be revisited.

# 4. Full-Scope MVP Definition

**Planning directive:** The MVP for this planning phase includes **all** capabilities from v1 (§1–77) plus the research-derived additions (§17). The purpose is to plan in full and trim later through an explicit gate, not to silently descope. This section inventories the full scope; §4.4 defines how it becomes shippable increments; §16 defines the delivery phases.

## 4.1 Capability inventory — inherited from v1 (complete, by v1 section)

| Domain | v1 sections included in full-scope MVP |
|---|---|
| Asset digital twin & graphs | 5, 65 (asset/failure/evidence/dependency graphs, reliability memory) |
| Maintenance core | 6, 7, 8, 9 (work lifecycle, constraint-based planning, job packs, SOP engine) |
| AI & knowledge | 10, 63, 64 (knowledge ingestion, layered AI, decision engine, agents) |
| Reliability & condition | 11, 12, 41, 42, 43, 44, 45 (RCM/FMEA/Weibull, PdM, MI-failure, PM optimisation, bad actors, temp-repair detection) |
| Dependency & economics | 13, 14, 15, 16, 46, 47, 48, 52, 53, 56, 57 (knock-on engine, dynamic criticality, risk economics, debt, opportunity engine, bottleneck, decision intelligence, scenarios, repair-vs-replace, budget optimisation) |
| Workforce & competency | 17, 18 (technician intelligence, competency) — governed per §11 |
| Field execution | 19, 20, 23, 24, 25 (tablet, evidence, safe device use, voice, location) |
| Safety | 21, 22 (HIRA/SHERQ, LOTO) |
| Connectivity & edge | 26, 27 (protocol fabric, edge nodes) |
| Stores, procurement, warranty, contractors | 28, 29, 35, 36 |
| Engineering & lifecycle | 30, 31, 32, 33, 34, 39, 40, 55 (MOC, maintainability, DfM, shutdowns, quality/metrology, master data, CAPEX handover, lifecycle) |
| Collaboration & management | 49, 50, 51 (War Room, Boardroom, situation room) |
| Data & platform | 38, 59, 60, 61, 62 (data quality, security, integration, migration, API platform) |
| Experimentation & environment | 54, 58 (maintenance experimentation, environmental intelligence) |

**Nothing from v1 is excluded.** Every item above enters engineering planning with a specification task, an owner and an estimate; exclusions happen only through the §4.4 gate with recorded rationale.

## 4.2 Research-derived additions (must-have capabilities absent from v1)

The following sixteen capabilities are **added to the MVP scope** because the competitive and regulatory research (§3, §15) shows they are required for credibility, compliance or adoption. Full specifications in §17.

1. **Federated Reliability Learning Network** — cross-customer cold-start priors (§9, §17.1)
2. **OEM Failure Mode Library Program** — licensed/curated failure-mode and interval priors (§9, §17.2)
3. **Alert Trust & Suppression System** — precision SLOs, feedback loop, suppression workflows (§10, §17.3)
4. **Model Governance & AI Conformity Pack** — EU AI Act-ready documentation, human-oversight workflow, logging (§15.2, §17.4)
5. **Works Council / Privacy Pack for Workforce Analytics** — consent, transparency, aggregation defaults (§11, §17.5)
6. **Integration Conflict Resolution Engine** — dual-master write-back with explicit ownership and merge rules (§12, §17.6)
7. **Connector Certification & Self-Service SDK Program** — partner-built certified connectors (§12.4, §17.7)
8. **Customer Economics Profiler** — guided onboarding that sources production-loss and cost inputs with lineage (§8.4, §17.8)
9. **Pilot-to-Production Conversion Framework** — exit-criteria-based pilot design that converts (C3.ai lesson) (§14.5, §17.9)
10. **Standards & Audit Evidence Pack** — ISO 55001, IEC 62443, SOC 2, functional-safety mapping artifacts (§15, §17.10)
11. **Fleet & Telematics Vertical Pack** — mobile-equipment beachhead packaging (CAN/J1939 DNA) with a dual-path data strategy — OEM telematics APIs *and* aftermarket CAN gateways as the default pilot path — because equipment-data rights are commercially contested and OEM portals charge API fees and throttle third-party access (§14.2, §17.11)
12. **WO Text Intelligence** — Technical-Language-Processing extraction of failure modes, components, detection methods and costs from free-text work-order histories; evidence shows structured failure codes are the least reliable field at typical sites (~48% of breakdown WOs lack usable descriptions; cost fields historically ~20% populated) while free text is information-rich (§3.1 data-reality findings)
13. **Multi-Vertical Pack Architecture** — vertical-neutral core with a **complete industry pack suite** (Fleet §17.11, Construction §17.13, Transport §17.14, Agriculture §17.15, Facilities §17.16, Energy/Utilities §17.17, Pharma/GMP §17.18, Food & Beverage §17.19, Mining §17.20, Manufacturing & Process §17.21) so all v1 §70 industries are served by one product with named operational features and compliance registers; construction co-beachhead (`DDE_Multi_Vertical_Strategy.md`)
14. **Modular Platform & White-Label Architecture** — customization-as-configuration: branding design tokens, declarative integration manifests, signed pack bundles, config-as-code promotion, three deployment shapes on one manifest; client onboarding becomes an actioning exercise in days (§17.22, `DDE_Modular_Platform_White_Label_Spec.md`)
15. **Field Experience Applications & Rugged Hardware Program** — four role surfaces (technician kiosk app, supervisor app, manager web/desktop console, executive wallboard) with structured role dashboards built on field-expert UX rules (≥48px glove targets, stale-while-revalidate offline, SLO-gated notifications); certified rugged-device matrix including intrinsically-safe Zone 1/21 and mining Group I tablets; carry/mount ecosystem with magnetic workface mounts and vehicle docks; per-device acceptance protocol (§17.23–§17.26, `DDE_Field_Experience_Rugged_Hardware_Spec.md`)
16. **PDF Document Conversion Engine** — AI-assisted conversion of PDF documents (checklists, scheduled maintenance reports, work orders, safety certificates) into governed digital input forms with field mapping, validation rules, and conditional logic; field technicians/supervisors enter data via touch/voice that populates structured databases while the Template Overlay render engine (immutable approved PDF + versioned coordinate map + backend render) regenerates reports that match the original approved PDFs pixel-for-pixel; offline-first capture, e-signature-wrapped signatures, private storage with payload lineage, and event hooks into WO/economics/registers (§17.29, integrated architecture from `digital-maintenance-report-architecture.pdf`)
17. **Security & Trust Architecture** — watertight protection of customer data against external attack and commercial-intelligence exposure: five-pillar trust doctrine (custodianship, radioactive competitive intelligence, fail-closed safety, zero standing privilege, evidence over assertion); C1–C5 classification with commercial-confidential handling; PQC-hybrid TLS + per-tenant envelope encryption + crypto-shredding; OWASP-API-mapped defense and attestation-tiered field devices; CRA/NIS2/ISO 27001:2022/SOC 2/62443 assurance roadmap sequenced to revenue stages (§17.30, `DDE_Security_Trust_Architecture.md`)

## 4.3 Non-negotiable product rules (carried forward from v1 §73, unchanged)

All fifteen v1 rules remain binding. Restated compactly: traceable governed safety AI; no silent procedure modification; AI never the authoritative record; software location never proof of physical safety state; LOTO verification per approved site procedure; offline by design; protocol logic below the canonical layer; integration as core capability; evidence and audit trail on important decisions; difficulty-aware technician assessment; completed WO ≠ successful repair; RCA closure ≠ failure elimination; inventory decisions weigh operational consequence; minimal device interaction during hazardous work. **New rules added by this version:**

16. **Every AI-derived economic figure must carry machine-readable data lineage and a confidence statement, or it must not be displayed.**
17. **No predictive alert reaches a human without meeting the active precision SLO for its class (§10) — silence is preferable to noise.**
18. **Technician performance data is used for capability and coaching by default; any evaluative use requires the §11 governance activation.**
19. **Write-back actions are governed by explicit ownership contracts (§12.2); DDE never writes to a system where ownership is undefined.**

## 4.4 Sequencing Gate (how the full catalog becomes shippable increments)

The full-scope MVP is a *planning* construct. Delivery proceeds through a mandatory gate applied to every capability:

- **Gate inputs:** customer-validated value per capability, dependency map, build cost, regulatory deadlines, competitive urgency.
- **Gate outputs:** a numbered release order (Release 1..N) with recorded rationale for every deferral. Deferral is a decision with an owner and a date, not an omission.
- **Standing trim candidates** (pre-registered, to be cut *first* if capacity binds, per the evaluation's recommendation): Boardroom meeting-AI integrations beyond one platform; UWB/RTLS beyond BLE+QR; hands-free voice beyond push-to-talk; device-prohibited modes; maintenance experimentation engine (§54); environmental intelligence (§58); DDE-native conferencing (§50).
- **Standing protected core** (never cut from Release 1): connectors (one incumbent), canonical model, asset+work-history graph, bad-actor analytics, source-grounded troubleshooting, readiness gate, data-quality engine, evidence capture, safety objects (HIRA/LOTO/permits), §8 economics lineage, §10 alert trust, §11 governance, §12 conflict engine, §13 offline sync.

# 5. Personas & Buying Center

*(New — required to make §14 commercial and §16 pilot design concrete.)*

- **Field Technician** (primary user): wants less screen time, clear instructions, offline reliability, no surveillance. Success: job done right first time.
- **Maintenance Planner/Scheduler**: wants ready work, fewer break-ins, stable schedule. Success: schedule compliance, wrench time.
- **Reliability Engineer**: wants bad actors, RCM tooling, failure elimination verified. Success: MTBF trend, repeat-failure rate.
- **Maintenance/SHERQ Manager**: wants safe, compliant, executed work. Success: zero harm, permit/LOTO compliance.
- **Stores/MRO Manager**: wants critical spares right-sized. Success: stock-out rate vs inventory value.
- **Plant/Operations Manager** (economic buyer): wants availability and production. Success: OEE, downtime cost.
- **CFO/Finance** (economic approver): wants auditable numbers. Success: defensible cost-of-inaction and ROI.
- **IT/OT Security** (technical approver): wants 62443-aligned, isolated, auditable integration. Success: clean security review.
- **Works Council/HR** (EU gatekeeper): wants lawful, transparent workforce analytics. Success: §11 pack satisfied.

# 6. Product Principles

All v1 §3 principles carry forward unchanged (Zero Harm, Reliability First, Evidence-Based Decisions, AI Augments People, Offline-First, System-of-Record Agnostic, Human-Centred Field Execution, Continuous Learning, Configurable Across Industries), augmented by the new rules 16–19 in §4.3.

# 7. Architecture (carried forward, with three mandatory additions)

The v1 §4 architecture (Experience / Intelligence / Collaboration above Asset-Knowledge Core, Operations Core, Connectivity Fabric, Physical World) carries forward unchanged, with these mandatory additions:

1. **Economics Data Layer** between the Dependency Graph and the Economic Engine (§8) — every monetary output is computed from versioned, sourced inputs.
2. **Trust & Governance Plane** alongside the Intelligence layer — alert precision SLOs, suppression, model registry, conformity documentation, AI decision logs (§10, §15.2, §17.3, §17.4).
3. **Sync & Conflict Subsystem** in the Connectivity Fabric — op-log based CRDT/last-writer-wins-with-ownership merge for offline clients and write-back (§12, §13).

# 8. Economics Data Model

*(Closes gap #3 — the single most important credibility fix. Implements new rule 16.)*

## 8.1 Principle

No monetary figure is displayed anywhere in DDE unless every input is traceable to a versioned source with an explicit confidence. A number without lineage is treated as a defect, not a feature.

## 8.2 Input catalog and sourcing

| Input | Used by | Primary source | Fallback when absent |
|---|---|---|---|
| Production loss per hour (per line/plant) | VaR, cost-of-inaction, debt | Finance/ops interview via Economics Profiler; margin-per-hour from ERP (COGS, throughput × contribution margin) | Industry benchmark ranges, displayed as *benchmark estimate* with wide confidence band |
| Downtime duration & frequency history | All downtime-cost math | Work-order downtime records from incumbent EAM; production stoppage logs; telematics (fleet) | Explicit "insufficient history" state — no number displayed |
| Failure probability | VaR | DDE predictive models with model-confidence metadata (§9) | Failure-mode library prior (§17.2), labeled as prior |
| Consequence severity (safety/environmental) | Risk economics | HIRA/BRA records, consequence matrices from customer safety library | Customer must supply; DDE never invents safety consequences |
| Energy & consumables cost | Environmental & lifecycle economics | Utility bills / energy meters / telematics fuel data | Benchmark band |
| Secondary damage probability | Cost-of-inaction | Failure-graph conditional frequencies from customer history | Reliability-engineer estimate, recorded as such |
| Contractual penalty exposure | Cost-of-inaction | Customer contract abstracts (SLA/penalty clauses) via Profiler | Not modeled; shown as "not quantified" |
| Emergency premium (expedited freight, overtime) | Cost-of-inaction, stores risk | Historical emergency PO data from ERP | Benchmark band |
| Asset replacement cost & remaining life | Repair-vs-replace, lifecycle | Asset master + procurement records; depreciation schedules from finance | Supplier quotes; labeled as estimate |

**Finance-first sourcing rule (evidence-derived):** historical work-order cost fields are unreliable at typical sites (studied cases: ~20% populated before remediation), so cost inputs are sourced from finance systems (POs, invoices, depreciation) wherever possible; WO cost fields are used only after the data-quality engine validates their completion rate. **Sanity bands (from Siemens/Senseye True Cost of Downtime 2024 and mining-sector benchmarks):** manufacturing downtime $36k–$2.3M/hr; mining/heavy $190k–$300k/hr; SME ≤$150k/hr; sector variance ≈60:1. Profiler values outside these bands trigger review flags. Benchmark figures may be displayed only as labeled ranges, never point estimates.

## 8.3 Computation & display contract

- Every computed economic object (VaR, Maintenance Debt, cost-of-inaction, avoidable exposure) stores: inputs used, source of each input, input versions/timestamps, model version if model-derived, confidence interval, and a plain-language "how this was calculated" explanation.
- UI renders confidence visually (e.g., range, not point) whenever input confidence is below "high."
- Benchmark-sourced figures are always labeled "Benchmark estimate — replace with your data" and are excluded from Boardroom/Board-level rollups until customer-validated.
- Aggregations (e.g., "$410k exposure" style figures from v1 §51) are only computed over customer-validated inputs.

## 8.4 Customer Economics Profiler (§17.8)

Guided onboarding workflow (workbook + in-app wizard) that walks the customer's finance/ops/reliability trio through the §8.2 catalog, records lineage, sets confidence ratings, and produces a signed **Economics Baseline** document. Pilot ROI (§14.5, §16) is measured against this baseline. Without a completed Profiler for a site, economic features operate in "lineage-limited" mode: only lineage-complete figures display.

# 9. Cold Start Strategy

*(Closes gap #4. Research basis: cold-start fault-detection literature, transfer-learning surveys, negative-transfer risk; competitor pattern — Tractian/Augury pretrain on fleet data, Senseye models from existing historian data.)*

## 9.1 Tiered knowledge bootstrap

A new site never starts from zero. Model confidence is explicit at every tier:

- **Tier 0 — Physics & engineering priors:** sensor limits, degradation mechanisms, failure-mode libraries (§17.2), FMEA templates per asset family. Available day 0; produces *rule-based* condition flags only.
- **Tier 1 — Fleet priors (Federated Reliability Learning Network, §17.1):** anonymized/aggregated failure signatures and interval statistics from consenting DDE customers and OEM library data. Produces *probabilistic* flags labeled "fleet prior — not yet validated on your site."
- **Tier 2 — Site normal-behavior baselining:** 2–6 weeks of unsupervised learning on the site's own telemetry establishes normal-operation envelopes; anomaly detection activates with site-specific thresholds.
- **Tier 3 — Site-supervised models:** as site failure/repair events accumulate, supervised and semi-supervised models (transfer-learned from Tier 1 with negative-transfer guards: domain-similarity screening, IQR-overlap filtering, human-in-the-loop validation per the research) progressively replace fleet priors.

## 9.2 Honest degradation of ambition

- Until Tier 3 maturity is reached for an asset class, DDE displays **rule + prior based guidance** with explicit confidence labels, and never claims prediction.
- RUL estimates require demonstrated site-level model validation (backtesting against ≥N observed events, precision/recall targets met) before display; otherwise the field shows "insufficient evidence."
- The UI carries a persistent **model maturity indicator** per asset class (Tier 0–3) so planners and reliability engineers always know what they are looking at.

## 9.3 Data acquisition acceleration

Because Tier 3 needs labeled failures, DDE treats failure labeling as a product feature: structured failure coding at WO closure (v1 §11.2 taxonomy), technician one-tap confirmation of predictive alerts (§17.3 feedback loop), and RCA outputs written back into the failure graph. Every completed intervention improves both the site model and (with consent, §17.1) the fleet network.

# 10. Alert Precision & Trust Management

*(Closes gap #5. Research basis: alert-fatigue as primary PdM adoption killer; confidence-scored context-aware alerting and technician feedback loops as the established remedies.)*

## 9.10 Alert Trust & Suppression System (summary; full spec §17.3)

- **Precision SLO per alert class** (e.g., bearing anomaly ≥70% confirmed-actionable at 30 days; safety-adjacent alerts have no SLO — they are deterministic rule outputs, not ML). Alerts below SLO maturity are quarantined to a review queue, never pushed to technicians.
- **Every alert carries:** evidence (sensor traces, trend charts), the model/tier that produced it (§9.2 maturity indicator), confidence, and recommended action with source citation.
- **One-tap technician verdict** (confirmed / false positive / not applicable) captured at execution; verdicts feed model retraining (§9.3) and the public **trust dashboard**: precision, false-positive rate, alerts-suppressed count, time-to-acknowledge — visible to management and, in summary form, to technicians.
- **Suppression workflows:** zone/equipment suppression (planned work in progress), temporary suppression with expiry and reason, systemic suppression proposals when a class breaches SLO (auto-quarantined until retrained).
- **Noise budget:** a hard ceiling on alerts-per-technician-per-shift; exceeding it auto-ranks and truncates the queue to the highest expected-value alerts. Silence is preferable to noise (new rule 17).

# 11. Workforce Intelligence Governance Charter

*(Closes gap #6. Implements new rule 18. Research basis: EU AI Act Annex III high-risk classification for worker performance evaluation/task allocation — conformity deadline extended to 2 December 2027 by the Digital Omnibus (in force 27 July 2026), with the emotion-recognition ban, AI-literacy duty (Art. 4) and transparency duties already in force; works-council realities in mining/energy/manufacturing verticals.)*

## 11.1 Purpose split (enforced in data model and permissions)

- **Capability view (default, always on):** competency records, expiry tracking, expertise graph for assignment (v1 §18, §17.3) — these are *qualifications*, not performance judgments.
- **Performance view (dormant by default):** the v1 §17 technician metrics exist in the schema and analytics engine but are **not activated** for any customer until that customer completes §11.3 activation.

## 11.2 Design commitments (product-level, non-configurable)

- Difficulty-adjusted scoring (v1 §17.2) is the *only* scoring mode; raw comparative leaderboards are not shipped.
- Individual performance scores are never shown to peers; visibility is role-gated (supervisor+).
- No biometric or emotion inference anywhere (EU AI Act prohibited-practice compliant by design).
- Technicians see their own full record, the same data supervisors see, and the reasoning behind any score.
- Coaching workflow is the primary surface: identified gaps generate training/assignment recommendations, not disciplinary artifacts.

## 11.3 Activation & compliance workflow (per customer)

1. **Transparency package** delivered to customer: what is measured, why, data flows, retention, model logic summary (AI-literacy support material included).
2. **Worker-representative notification pack** — drafted for the customer's works council/union consultation (Art. 26(7)-equivalent duty prepared ahead of the Dec 2027 deadline).
3. **Human-oversight designation:** named roles; every AI-influenced people decision has a documented human reviewer with override authority and access to the reasoning (Art. 14/26 pattern).
4. **Logging:** ≥6-month retention of AI decision logs for any evaluative use (Art. 26(6) pattern).
5. **FRIA support:** fundamental-rights impact assessment template and data export to support the customer's Art. 27 assessment where required.
6. **Signed activation record**, then the Performance view unlocks, configured to the customer's lawful use case. Customers who do not activate get the capability view only — the product remains fully functional for planning, assignment (by competency), scheduling and safety.

## 11.4 Data residency & privacy

Workforce data is partitioned by tenant and region; EU customers get EU-resident processing; aggregation thresholds prevent re-identification in small teams; retention is configurable with documented defaults; GDPR lawful-basis documentation is part of the activation pack.

# 12. Integration & Write-Back Architecture

*(Closes gap #7. Implements new rule 19.)*

## 12.1 Integration tiers (honest effort model)

- **Tier 1 — Certified connectors (productized, upgrade-safe):** SAP (PM/QM/MM via released APIs/OData; ECC and S/4; on-prem and RISE), IBM Maximo (Manage + MAS APIs), IFS, Oracle EAM/Cloud, Dynamics 365 F&O/CE. Versioned contracts, deprecation policy, automated regression suite per connector, certification badge per release.
- **Tier 2 — Standard adapters (configurable):** ServiceNow, Infor, eMaint, Fiix, Limble, UpKeep, MaintainX (via their public APIs); historian adapters (PI, Aspen IP.21, InfluxDB, Timescale); generic REST/OData/SQL/file/webhook.
- **Tier 3 — Custom (services-assisted):** SDK + recipe library for the long tail; partner program (§17.7).

## 12.2 Ownership contract for write-back (Mode B crux)

Every writable object type in every connected system has an **Ownership Contract** in the canonical model:

- **System of record** per field/object (e.g., WO status: incumbent EAM is master; DDE-created recommendations: DDE is master until accepted; measurement records: DDE is master, mirrored to EAM).
- **Allowed operations** in each direction, with idempotency keys and exactly-once delivery semantics.
- **Conflict policy** per field: incumbent-wins / DDE-wins / field-level merge / human queue.
- Every write-back is journaled (source, target, payload, result, correlation ID) and reversible per the ownership contract; unresolvable conflicts land in a **human resolution queue** with full context — the system never silently picks a winner for consequential objects.

## 12.3 Reference deployment patterns

Documented, tested patterns per incumbent: read-only overlay (Mode A) with change-data-capture or scheduled sync; orchestrator (Mode B) with event-driven write-back and the §12.2 contracts; standalone (Mode C) with migration tooling (v1 §61). Each pattern ships with a security architecture (§15.2), a sizing guide, and an estimated implementation-effort range so sales cannot promise "a connector" as a two-week exercise.

## 12.4 Connector Certification & Partner SDK (§17.7)

Published SDK, conformance test suite, certification levels (Certified / Silver / Registered), marketplace listing, and revenue-share program. Rationale: connector breadth is the #1 scale bottleneck in Mode A/B; the partner program converts it from a services sink into an ecosystem moat.

# 13. Offline-First Sync & Conflict Resolution

*(Closes gap #8.)*

## 13.1 Architecture

- **Client op-log:** every offline mutation is a signed, timestamped, causally-ordered operation (device ID, Lamport/HLC clock, entity, field, value) in local durable storage; server assigns vector-clock positions at sync.
- **Deterministic merge:** per-entity-type merge policy — CRDTs for additive evidence (photos, notes, measurements — union semantics); field-level last-writer-wins with *ownership rules from §12.2* for structured records; safety-critical objects (LOTO state, permit status, isolation verification) are **never merged offline** — they are online-gated or require explicit re-verification on reconnect, because physical state may have changed while disconnected (consistent with v1 rule 5 and rule 6).
- **Store-and-forward with progress guarantees:** job packages, SOPs, drawings, site maps and asset knowledge are pre-staged on device (v1 §19.2); evidence captured offline is upload-queued with resumable chunked transfer; sync status is visible per object.
- **Submit-time durability (document-capture surfaces):** for forms, checklists and report submissions (§17.29), the write to local durable storage happens synchronously with the submit action — never queued in memory; a background sync worker guarantees eventual upload across app restarts and reboots. Reports are single-author documents, so server-authoritative last-write-wins is sufficient *for the submission itself*; supervisor countersigns/corrections are **append-only signed records** that never overwrite or merge away an earlier signed state. Anything touching live safety state still routes through the online-gating rule above.

## 13.2 Conflict UX

When a structured-record conflict survives automatic merge, the resolving user sees a side-by-side diff with source, timestamp, author and business context, and picks per-field. Safety-relevant fields always route to the permit/isolation authority role, not to whoever syncs first.

## 13.3 Offline AI

On-device models (quantized anomaly detection, offline speech-to-text, cached retrieval over the job's document set) provide Tier-0/2-level guidance offline; anything requiring fleet/cloud models is explicitly marked unavailable offline rather than silently degraded.

# 14. Commercial Model

*(Closes gap #9. Research basis: C3.ai consumption-pricing failure; Fiix/Limble/MaintainX per-user benchmarks; Augury/Senseye enterprise-quote norms; Uptake's partner-data dependence.)*

## 14.1 Packaging

| Package | Contents | Pricing model |
|---|---|---|
| **DDE Field** | Technician kiosk/tablet app (§17.23): job packs, SOPs, guided safety gates, evidence capture, offline AI, "My Day" dashboard; shared-device kiosk mode; rugged-device compatibility program (§17.24); Android kiosk hardening (§17.25); tech-expert module enhancements (§17.26); **digital forms & report capture on converted client documents (§17.29) — offline-first, e-signature-wrapped** | Per named technician / month (band: $40–75; benchmarked against Fiix $45–75, MaintainX, Limble tiers) |
| **DDE Reliability** | Overlay intelligence: connectors, asset graph, bad actors, condition/PdM, troubleshooting copilot, data-quality engine | Per asset-under-management / month tiered by asset count + criticality class |
| **DDE Operations** | Mode B orchestration: write-back, scheduling optimization, stores/procurement intelligence, economics engine | Per asset AUM premium tier **plus mandatory site platform fee (entry: $3–15k/site/mo)** — benchmarked to the Senseye/AVEVA/GE-APM class ($3–30k/site/mo), which buyers already pay for orchestration-grade asset intelligence |
| **DDE Enterprise (Mode C)** | Full standalone ERP capability set, migration factory, Boardroom, multi-site | Site/enterprise subscription + implementation |
| **Vertical packs** | Full suite (§17.11, §17.13–§17.21): Fleet & Telematics, Construction, Transport, Agriculture, Facilities, Energy & Utilities, Pharma/GMP, Food & Beverage, Mining, Manufacturing & Process — signed, versioned, composable bundles (§17.22) | Per-site add-on |
| **White-label / OEM** | Partner-branded deployment: branding tokens, custom domain, branded mobile shells, partner-letterhead certificates; conformity flow-down contracted (§17.22, §15.14) | Per-brand platform fee + per-seat/per-asset revenue share |
| **Platform add-ons** | Edge nodes (per node), Federated Learning Network participation (discount in exchange for pooled priors consent), premium connectors | Usage/site |

Design rules: predictable fixed-subscription backbone (C3.ai lesson); value metric aligns with customer scale (technicians, assets) not raw usage; no consumption-only pricing; pilot pricing pre-defined in §14.5 so pilots are sales instruments, not experiments. **Billing for frontier markets (evidence-driven, Zimbabwe research §4): USD-denominated contracts only; annual-prepay invoicing as default (recurring card billing is unreliable where forex allocation is queued); settlement to USD Nostro accounts; reseller/partner-of-record option (South African entity) where payment rails or over-compliance blockages demand it; SDN screening of all customers given US targeted-sanctions over-compliance risk.**

## 14.2 Beachhead selection

Primary beachhead: **mobile-equipment-intensive operations (mining fleets, heavy construction, industrial field service)** — rationale: v1's CAN/J1939/CAN-FD protocol DNA is a genuine differentiator there; downtime cost per hour is high and measurable (telematics provide objective baselines); incumbent EAM coverage of mobile fleets is weakest; and the buyer (maintenance manager + fleet manager) is reachable without 18-month IT cycles in mid-size fleets. **First reference market: Zimbabwe (see `DDE_Zimbabwe_Market_Entry_Research.md`) — a two-tier strategy: Tier 2 lithium/gold operations (50–200 mobile units, greenfield maintenance digitalization, site-GM decision authority) as pilot customers; Tier 1 majors (Zimplats-class SAP/Maximo estates) as parallel lighthouse overlay conversations. Zimbabwe is the proof market, not the revenue market — the revenue-scale path is SADC expansion (Zambia, Botswana, South Africa) using Zimbabwe references.** **Co-beachhead: construction fleets (see `DDE_Multi_Vertical_Strategy.md` §2.2) — same geography, same gateway hardware, overlapping buyer persona; downtime economics are strong ($500–$1,000+/hr per machine; $2–10k/day once idle crews, rentals and milestone penalties count) and telematics+CMMS integration evidence shows 40–48% unplanned-downtime reduction; requires the §17.13 pack (project/cost-code linkage, rental-asset handling). Two packs on one pilot platform halve the cost of proof.** Secondary: process manufacturing lines with PI-historian estates. Tertiary (later): utilities/power (long cycles, high governance burden).

**Vertical scope statement (corrects any mining-only reading): DDE is a vertical-neutral platform serving all ten v1 §70 industries — mining, manufacturing, energy, utilities, transport, construction, agriculture, facilities, heavy equipment, and processing. Verticals are packaging (packs on the common core) and sequencing choices, never product boundaries. Vertical-by-vertical verdicts, evidence grades, and phase entries: `DDE_Multi_Vertical_Strategy.md`.**

Selection criteria locked for any future vertical change: downtime cost per hour > $5k; brownfield CMMS present (integration story exists); telemetry available or cheap to add; ≤3 signatures on initial purchase; referenceable community reachable.

## 14.3 Land-Expand motion

Land: 1 site, 50–300 critical assets or 20–100 mobile machines, DDE Field + DDE Reliability overlay. Expand: Mode B orchestration on proven assets → additional sites → stores/procurement → Mode C where incumbent is end-of-life. Expansion triggers are codified in the account plan template (e.g., alert precision SLO met for 2 consecutive quarters → propose orchestration).

## 14.4 TAM framing

Bottom-up per vertical: number of target sites × assets AUM × blended ARPU. Directionally: mid-size mining/heavy-fleet operations, construction contractors with 50+ machine fleets, and mid-market process manufacturers in AU/ZA/NA/CL/ID/PE as first geographies (English/Spanish/Portuguese-speaking, high downtime cost across all served verticals — mining $5–10k/hr haul trucks, manufacturing $36k–$2.3M/hr, chemical/refining $100k–$500k/hr). Full TAM model is a §18 deliverable (GTM spec); this plan locks the *method* and the *beachhead*, not the number.

## 14.5 Pilot-to-Production Conversion Framework (§17.9)

- **Pre-pilot:** Economics Baseline signed (§8.4); 3–5 measurable KPIs with baseline values; named executive sponsor; **named customer-side maintenance champion with defined weekly time commitment** (survey evidence: change-management investment correlates with ~3× adoption; without it, 30–40% of technicians revert to paper by month three); conversion criteria written *into the pilot contract* (e.g., "≥15% downtime reduction on pilot fleet within 90 days → auto-quote for 12-month production rollout at pre-agreed pricing"). Pilot KPI targets anchor to the conservative evidence band (30–50% downtime reduction; 10–25% maintenance-cost reduction) — never maturity-stage vendor claims (70–90%).
- **In-pilot:** weekly value scorecard against baseline; §10 trust dashboard reviewed jointly; success criteria cannot be changed mid-pilot without mutual sign-off.
- **Exit:** conversion decision meeting with measured before/after (v1 §69 Phase 3 metric list); either conversion quote, remediation plan, or structured exit with documented lessons fed to product.
- Anti-patterns explicitly prohibited: open-ended pilots, unmeasured pilots, pilots without a pre-agreed conversion mechanism (C3.ai lesson).

# 15. Compliance & Regulatory Framework — Standards, Legislation & Regulators

**Purpose.** The product must be lawful and certifiable in every market it is sold into, and must actively help customers meet *their* statutory maintenance obligations. Compliance is treated as a product feature with an owner, a living register and a deadline calendar — not a sales checkbox. This section is a planning-grade register: every market entry requires counsel sign-off before first sale (launch gate §15.1).

## 15.1 Compliance governance model

- **Accountability:** named Head of Product Compliance (Phase 0 mandate); every capability with a regulatory dimension names a compliance counterpart.
- **Regulatory watch:** quarterly external counsel review plus continuous monitoring of the instruments in §15.2–§15.12; changes enter the backlog with severity and deadline.
- **Per-market launch gate:** no first sale in a jurisdiction until the market checklist (data protection, safety legislation, statutory registers, e-signature validity, accessibility, procurement certifications) is counsel-approved.
- **Conformity matrix:** the living artifact in §17.10 maps every obligation → product capability → evidence artifact → owner → status.
- **Deadline calendar:** §15.13, reviewed monthly; hard dates drive phase gates (§16).
- **Flow-down:** supply-chain obligations DDE's customers face (NIS2, CRA) are mirrored into DDE's own supplier contracts.

## 15.2 International bodies & industry frameworks

| Body / framework | Domain | DDE engagement |
|---|---|---|
| ISO TC 251 — ISO 55000/55001 | Asset management systems | Alignment matrix; lifecycle, criticality & MOC objects (§15.15) |
| ISO TC 108 — ISO 14224 + vibration/condition standards | Reliability data taxonomy | Spine of failure taxonomy and libraries (§17.2) |
| IEC TC 65 / ISA99 — IEC 62443, OPC UA (IEC 62541) | Industrial automation & OT security | Zones/conduits architecture, SL targets (§15.15); product-side engineering to 62443-4-1 with component requirements per -4-2 — full security architecture in §17.30 |
| IEC TC 44 — IEC 61508/61511, ISO 13849 | Functional safety | Boundary statement: DDE is not a SIF (§15.15) |
| SAE International — J1939 / CAN family | Fleet protocols | Fleet Pack protocol layer (§17.11) |
| AEM + ISO 15143-3/-4 | Equipment telematics data exchange | Telematics connector standards for Fleet Pack (§17.11) |
| EMESRT / ICMM / GISTM | Mining safety & assurance | TMM control-level support (§15.5); tailings inspection registers |
| OIML + national legal-metrology authorities | Measurement in trade | Calibration traceability (§15.8) |
| IECEx / ATEX notified bodies | Hazardous-area equipment | Ex inspection registers; device policy in Ex zones (§15.5, v1 §23) |
| ENISA + national CSIRTs | EU cyber incident reporting | CRA/NIS2 reporting interfaces (§15.3, §15.13) |
| EDPB + national data-protection authorities | EU data protection | DPIA templates, residency defaults (§15.4) |
| Accreditation bodies (UKAS, ANAB, SANAS, DAkkS) | Certification trust | Certification roadmap (§15.15) |

## 15.3 EU single market — product, cyber & AI legislation

| Instrument | Status / dates (verified Aug 2026) | DDE obligation |
|---|---|---|
| **Cyber Resilience Act (EU) 2024/2847** | Art. 14 reporting live **11 Sep 2026** (24 h early warning → 72 h notification → final report via the ENISA Single Reporting Platform; applies to products already on the EU market); full essential requirements + CE marking **11 Dec 2027**; fines up to €15 M / 2.5 % turnover | Applies to DDE edge nodes/gateways and shipped software: SBOM, secure-by-default configuration, vulnerability handling, published support period, coordinated vulnerability disclosure policy, 24-hour reporting runbook — built in Phase 0 and drilled before 11 Sep 2026 |
| **Machinery Regulation (EU) 2023/1230** | Applies **20 Jan 2027** (replaces Machinery Directive 2006/42/EC; explicitly accommodates digital instructions / information for use) | SOP/document engine must deliver OEM digital instructions compliantly (availability, versioning, language, accessibility) |
| **NIS2 Directive (EU) 2022/2555** | Transposed in ~23/27 member states by mid-2026; Commission referred FR, IE, NL, ES to the CJEU on **8 Jul 2026**; essential-entity fine ceilings ≥€10 M / 2 % | DDE is a supplier to essential/important entities (energy, mining, water, transport customers): supply-chain security clauses, incident cooperation with customers' 24 h/72 h duties; own-entity registration where applicable |
| **Data Act (EU) 2023/2854** | Applied **12 Sep 2025** | Connected-product (edge/telematics) data access and portability APIs; fair data-sharing contract terms |
| **EU AI Act (EU) 2024/1689** | Prohibitions, AI-literacy and transparency duties already in force; Annex III high-risk obligations **2 Dec 2027** | See §15.16 and §17.4 |
| **General Product Safety Regulation (EU) 2023/988** | Applied 13 Dec 2024 | If/when DDE distributes hardware: traceability and recall readiness |
| **Accessibility Act (EU) 2019/882** | Applied 28 Jun 2025 | Narrow B2B scope, but EN 301 549 conformance is a de-facto EU procurement filter (§15.11) |
| **eIDAS 910/2014 + 2024/1183** | In force | Advanced/qualified e-signature support where customers execute permits and approvals electronically (§15.10) |
| **Seveso III (2012/18/EU), ATEX workplace (1999/92/EC), PED (2014/68/EU)** | In force (customer-side duties) | DDE must *support* customer obligations: MOC evidence, safety-critical equipment inspection registers, Ex inspection codes, pressure-system examination schemes (§15.6) |

## 15.4 Data protection & privacy by jurisdiction

| Market | Law | DDE posture |
|---|---|---|
| EU/EEA | GDPR | Regional residency; DPIA templates (mandatory for workforce analytics); SCC/BCR transfer framework |
| UK | UK GDPR + DPA 2018 | UK residency option; IDTA contracts |
| South Africa | POPIA | Residency option; operator agreements; retention discipline enforced by configurable retention defaults |
| **Zimbabwe** | **Cyber and Data Protection Act [Ch. 12:07] (2021) + SI 155/2024** | POTRAZ is the DPA; customers processing 50+ data subjects need controller licences; DDE supports customer licensing/DPO workflows and the **24-hour POTRAZ breach-notification duty** (tightest in Africa); cross-border transfers restricted (authorisation/adequacy analysis for ZA/EU hosting); criminal penalties incl. up to 7 years for unlicensed processing |
| Australia | Privacy Act 1988 + APPs (2022–24 amendment regime) | APP transparency notices; notifiable-breach procedure |
| Brazil | LGPD | Residency option; DPO designation; ANPD-aligned impact assessment |
| Canada | PIPEDA + Quebec Law 25 | Law 25 privacy impact assessment for workforce analytics; French-language UI where required |
| US | State privacy laws (CCPA/CPRA and successors) | No sale/share of personal data; state-by-state matrix in the §17.5 pack |

Cross-cutting: lawful-basis mapping per module; retention defaults per region; data-subject request tooling (export/erase) for workforce records; sub-processor register with customer notification duties.

## 15.5 Occupational & process safety legislation by market

| Market | Key instruments | What DDE must do |
|---|---|---|
| South Africa | **MHSA 1996 + Chapter 8 regulations** — 8.10.1.2(b)/8.10.2.1(b) TMM collision avoidance effective **21 Dec 2022** (EMESRT Level 9 automatic intervention); Driven Machinery Regulations (lifting tackle); General Machinery Regulations; s.54 stoppage powers | Fleet Pack: PDS/CAS event-log ingestion and retention, intervention-event evidence packs; statutory inspection registers (lifting, electrical); inspector-grade exports |
| United States | OSHA 29 CFR 1910.147 (LOTO: procedure, periodic inspection, training records); **1910.119 PSM** — 1910.119(j) mechanical integrity (inspections/tests, QA of maintenance materials — direct maintenance-software territory); MSHA 30 CFR Parts 56/57 (equipment examination records) | LOTO object models the periodic-inspection duty; PSM/MI inspection schedules, thickness-measurement histories, fit-for-service records; MSHA examination logs |
| EU | Seveso III national transpositions; Work Equipment Directive 2009/104/EC; national regimes (DE BetrSichV, NL Arbowet, FR equipment-in-workplace decrees) | Safety-critical equipment registers; inspection/usage regimes per national transposition |
| UK | PUWER 1998; LOLER 1998 (thorough examination at 6/12-month intervals + reports); PSSR 2000 (written scheme of examination); COMAH 2015 | Statutory due-date engine with legal intervals; examination report storage; COMAH safety-report evidence |
| Australia | WHS Act/Regulations (registered plant; major hazard facilities); state mining regulations (NSW WHS (Mines) Reg 2022 statutory functions; WA MSIR) | Statutory-function competency tracking; registered-plant registers |
| Canada | Provincial OHS; CSA Z460 (LOTO), CSA Z462; mining regulations (e.g., Ontario O. Reg 854) | Jurisdiction templates at market entry |
| Brazil | NR-12 (machinery safety), NR-13 (pressure vessels: registration + periodic examination), NR-35 (work at height) | NR-13 equipment register and examination scheduling; competency/artifact records |
| Other targets (CL, ID, PE) | Mining safety codes with statutory examination regimes (e.g., Sernageomin in Chile) | Counsel gap review before first sale (launch gate §15.1) |
| **Zimbabwe** | **Mines and Minerals Act [Ch. 21:05] + Mining (Management & Safety) Regulations SI 109/1990**; Pneumoconiosis Act; NSSA Accident Prevention & Workers Compensation Scheme; Labour Act [Ch. 28:01] | Zimbabwe jurisdiction template for the statutory-register engine: mine-manager competency/certificate tracking (FBL/MBL — enforcement actively rising, incl. a USD 2M national safety blitz, 2026), PPE issue records (SI 109 ss.47–48), accident/near-miss reporting with s.269 timelines (fatals to inspector + police without delay; investigation within 24h), Pneumoconiosis medical-fitness certificate expiry tracking (fits competency engine), NSSA inspection-evidence exports |

## 15.6 Statutory inspection & certification registers (product requirements)

One register engine, jurisdiction templates. **Shipping template library by vertical (each template: legal citation, asset classes, interval table with monitoring-extension semantics where law allows, evidence requirements, sign-off rules, retention, authority export format, counsel-review status):**
- **Mining:** SI 109/1990 (ZW), MHSA-class statutory appointments and examinations, GISTM tailings/water-retaining structures, hazardous-area (Ex) inspections
- **Transport:** US 49 CFR 396 App A annual inspection (13 systems, 14-month retention, inspector-qualification evidence) + eDVIR chain per 396.11/396.13 (e-DVIR explicitly authorized effective 23 Mar 2026); EU roadworthiness 2014/45/EU; AETR tachograph 56-day retention
- **Facilities:** LOLER (6-monthly lifting), PUWER, F-Gas by CO₂e band (≥500t quarterly / 50–500t 6-monthly / 5–50t annual), RRO 2005 fire regimes + BS 5839-1:2025 servicing, EICR 5-yearly, Legionella L8/HSG274, PSSR pressure systems, CAR 2012 asbestos, Building Safety Act (higher-risk buildings); US: ASME A17.1, NFPA cycles
- **Process/chemical:** API 510 (vessels) / API 570 (piping) / API 653 (tanks) under OSHA PSM 1910.119(j) and Seveso III
- **Energy/utilities:** NERC PRC-005-6 PSMP (component-type interval tables; monitoring-status attribute with interval extension only where alarm attributes qualify; time-based vs performance-based programs per Attachment A; dated evidence per requirement), FAC-003-5 vegetation management; regional grid-code analogues on the same engine
- **Pharma/GMP:** GMP calibration-status registers, equipment qualification states, Part 11/Annex 11 record controls (§15.10)
- **Food:** HACCP/CCP-linked maintenance records, post-maintenance sanitation verification, allergen-changeover procedures, FSMA 21 CFR Part 117 two-year minimum retention
- **Cross-vertical:** lifting tackle; cranes/hoists; electrical verification and test-and-tag; fire and gas systems; roadworthiness per fleet jurisdiction

Engine requirements: statutory due-date engine with legal intervals per template; certificate and report storage with tamper-evidence; inspector identity and competency validation at sign-off; overdue escalation that planners cannot silence — **statutory overdue work is never auto-deferred**; template versioning with effective dates; **pack-composition conflict rule: overlapping compliance intervals resolve to the stricter interval with a counsel-review flag (§17.22)**.

## 15.7 Environmental & sustainability

Industrial Emissions Directive (maintenance evidence supporting BAT); US SPCC/CWA containment inspections; hazardous-waste manifests (Basel-consistent tracking in v1 §58); EU Battery Regulation 2023/1542 and WEEE/RoHS for any DDE hardware; CSRD/ESRS data hooks (energy and emissions export) — timelines evolving under the 2025–26 Omnibus, so DDE ships exportable data rather than hard-coded reports. Alignment: ISO 14001, ISO 50001.

## 15.8 Quality, metrology & calibration

ISO 9001 (customer QMS integration); ISO/IEC 17025 (calibration certificate handling); ISO 10012 (measurement management systems); legal metrology (OIML/national) where measurements feed trade or billing. Calibration traceability chains and out-of-tolerance consequence tracking (v1 §34) must satisfy audit reconstruction: "what did we measure with, and what else has been affected since the last good calibration."

## 15.9 Interoperability & data standards

ISA-95/IEC 62264 (enterprise-to-control integration); ISO 22400 (manufacturing KPIs); OPC UA companion specs; MQTT/Sparkplug B; SAE J1939; ISO 15143-3/-4 (AEM telematics exchange — Fleet Pack); ISO 8000 (data quality). The canonical model (v1 §26.4) remains authoritative; standards are import/export and adapter targets, never the internal schema.

## 15.10 Electronic signatures, records & evidence legality

eIDAS (EU, incl. the 2024/1183 amendments), US ESIGN/UETA, South African ECTA 2002, Australian ETA 1999: the DDE signature layer must support the required signature levels per market for permits, isolations, quality hold-points and approvals. Records management aligned to ISO 15489; WORM/immutable storage options for safety-critical evidence; long-term signature validation; export formats that preserve evidential weight. **Pharma extension (§17.18): 21 CFR Part 11 controls (signature manifestations, meaning-of-signature, record retention for the equipment lifetime) and EU GMP Annex 11 validation expectations ship as an entitlement-gated capability layer — the e-signature/audit-trail architecture keeps this option open without burdening non-GMP customers.**

**Signature-capture rule for documents and forms (binds §17.29):** a drawn/typed signature image on a generated report is *not* by itself a legal e-signature. Wherever a signature field appears in a converted template, the platform wraps it with the compliance layer: authenticated signer identity (session-bound, not device-shared), explicit intent capture ("I sign as…", meaning of signature), tamper-evident binding of the signature record to the exact document hash and payload version, and trusted timestamp — producing an advanced/attributable signature record alongside the visual ink on the PDF. Regulated-vertical tenants receive the Part 11 manifestation set via the pharma entitlement layer; all other tenants still get identity + intent + hash binding as the floor, so no DDE-generated "signed" document is ever merely an unattributable image.

## 15.11 Accessibility & public procurement

Target WCAG 2.2 AA / EN 301 549 conformance for web and tablet surfaces; published VPAT/ACR for US public-sector and EU tenders; Section 508/ADA posture for US deals; national procurement certifications (cloud registries) tracked per market.

## 15.12 Employment & works-council law (workforce module)

Beyond the EU AI Act (§15.16): member-state co-determination and monitoring law (e.g., Germany BetrVG §87), national consultation duties, and per-country lawful-basis variance. The §17.5 Works Council Pack carries a per-country activation matrix; default-off (§11) remains the global posture.

## 15.13 Regulatory deadline calendar (verified 22 Aug 2026)

| Date | Event | Owner action |
|---|---|---|
| **11 Sep 2026** | CRA Art. 14 reporting live (ENISA SRP) | Runbook drilled; CVD policy published; SBOM pipeline live — **imminent: Phase 0 gate** |
| Rolling 2026–27 | NIS2 national regimes (23/27 transposed; CJEU referrals 8 Jul 2026) | Customer supply-chain clause pack; own-entity registration per member state |
| **20 Jan 2027** | Machinery Regulation 2023/1230 applies | Digital-instructions delivery validated in the SOP engine |
| **2 Dec 2027** | EU AI Act Annex III conformity | §17.4 pack audit-ready; §11 activation lawful in all member states |
| **11 Dec 2027** | CRA full application + CE marking | Edge/app conformity assessments complete; declaration of conformity + CE |
| Watch | AI Act harmonized standards (Omnibus ~6-month fuse); CSRD/ESRS Omnibus; NIS2 national annexes | Quarterly counsel review items |

## 15.14 Compliance program operations

Named owner; quarterly counsel review; automated regulatory watch; per-market launch gates; conformity matrix (§17.10) reviewed monthly; CRA drills (24-hour clock) twice yearly; supplier flow-down clauses; audit calendar for SOC 2 / ISO 27001; AI-literacy training records; standing change trigger — any new market or new hardware triggers a counsel gap review before first sale.

## 15.15 Certification posture

Born-compliance doctrine (§17.30): the full control set behind every certification in the SAP-parity portfolio operates from Phase 0, with the continuous-evidence engine emitting audit artifacts continuously; the application calendar and recurring audit schedule live in `DDE_Security_Trust_Architecture.md` §12/§11.6.

| Standard / certification | Relevance | DDE response |
|---|---|---|
| **SOC 2 Type I → Type II** | SaaS procurement checkbox | Type I design evidence complete at launch (apply month 3–4); Type II observation window over pilot traffic, report ~month 9–10; annual thereafter |
| **ISO/IEC 27001:2022** | Global enterprise security certification | ISMS operating from Phase 0; Stage 1 month 4–5; certificate ~month 8–9; annual surveillance + 3-year recertification |
| **BSI C5** | German-market cloud deals | Post-27001 audit month 8–12; annual re-audit |
| **ISO 27017 / 27018 / 27701** | Cloud + PII extensions | Add-on audits riding the 27001 cycle, months 9–12+ |
| **CSA STAR** | Registry visibility | Level 1 at launch; Level 2 after Type II |
| **ISO 22301 / ISO 9001** | Continuity / quality (pharma & manufacturing buyers) | Months 12–18 as demand requires |
| **ISASecure SDLA** | OT development lifecycle certification | Phase 2–3 when OT-pack revenue justifies |
| **CRA conformity** | EU statutory product duty | Technical file maintained current from Phase 0; declaration per statutory path before Dec 2027 |

All non-certification standards (ISO 55001, ISO 14224, IEC 62443, functional-safety boundary, statutory inspection regimes) are governed by the tables in §15.2–§15.8; the conformity matrix in §17.10 remains the single source of truth mapping obligations → capabilities → evidence.

## 15.16 EU AI Act posture (expanded; as of Aug 2026)

- **In force now and designed-in:** prohibited-practice compliance (no emotion recognition in the workplace — §11.2), AI-literacy support (Art. 4 — §11.3 training material), transparency to users interacting with AI systems (Art. 50 — all DDE AI surfaces labeled, including chat and voice).
- **Annex III high-risk (worker performance evaluation / task allocation):** full conformity obligations apply from **2 December 2027** (Digital Omnibus extension). DDE's §17.4 Model Governance & AI Conformity Pack (technical documentation, risk-management file, data-governance records, logging, human-oversight workflow) is maintained to that standard *continuously*; the §11.3 activation workflow mirrors deployer obligations (Art. 26): worker/representative notification, competent human oversight, ≥6-month log retention, FRIA support.
- **Classification discipline:** DDE's condition-monitoring and maintenance-decision AI is *not* Annex III high-risk; only the workforce Performance view can enter Annex III scope, and only through customer activation — this boundary is documented and defended in the conformity pack (misclassification in either direction is a legal risk).
- **Watch items:** harmonized standards under the Omnibus flexibility mechanism (~6-month fuse once published); the pending EU AI Liability Directive direction — evidence-grade AI decision logs (rule 10, §17.4) double as the liability-defense artifact.

# 16. Delivery Phases

The full-scope catalog (§4.1–4.2) is delivered through phases. The sequencing gate (§4.4) assigns capabilities to phases; the protected core is Release 1; standing trim candidates land last if at all. Phases are capacity-shaped, not scope-shaped — the catalog is fixed, the calendar flexes.

- **Phase 0 — Foundations (months 0–3):** canonical domain model; connector framework + first certified connector (beachhead-aligned: SAP *or* Maximo per design-partner estate, plus telematics ingestion for fleets); asset/work-history graph; data-quality engine; evidence store; safety objects (HIRA/LOTO/permits schema); Economics Profiler v1; security architecture (62443 zones/conduits design); **§17.30 security foundation: data-classification scheme with commercial-confidential tier, per-tenant envelope encryption, audit-plane schema, secure-SDLC + SBOM pipeline operational (CRA technical-file prerequisite), workload identity system; born-compliance infrastructure live from day one — controls-as-code registry with framework mappings, automated evidence collection into WORM storage, ISMS policies + SoA drafted across all 93 Annex A controls, quarterly management-review cadence, SOC 2 Type I design evidence complete at launch, auditor slots pre-reserved**; §11 governance schema; §10 alert framework schema; §13 sync engine core. **Modularity foundation lands here by design (§17.22): tenancy hierarchy, branding token service, integration-manifest format, config-as-code promotion — because every later pack ships through this mechanism, building it first is what keeps the full-scope catalog deliverable by one team. Field experience skeleton also starts here: design system with glove-rated components, Tech Kiosk App shell + "My Day" dashboard, device compatibility program seeded with beachhead-market models and acceptance protocol (§17.23–§17.26). Document engine foundation also lands here (§17.29): template-overlay render service (pdfme-based) with private storage + audit-row persistence, and the offline submit-queue pattern proven on one converted template — because the render engine and durability guarantee are prerequisites for every later capture surface, not features.** *Exit: one design-partner site reading real data; lineage-complete economics on one line; governance/conformity skeletons reviewed by external counsel; a second site onboarded via wizard-only configuration as the modularity acceptance test; one real client document converted, captured offline, and regenerated pixel-true.*
- **Phase 1 — Intelligence overlay (months 3–9):** bad-actor/Pareto/reliability analytics; source-grounded troubleshooting copilot; Tier 0–2 cold start (§9); alert trust system live with SLOs (§10); readiness gate; asset health scores; offline tablet with job packs and evidence (§13); **Supervisor App and Manager Console live (stuck board, approvals, three-column console); rugged fleet deployed with carry/mount kits; first field acceptance protocol runs completed**; Fleet Vertical Pack v1 (J1939 ingestion, telematics KPIs); **Construction Pack v1 (project/cost-code WO linkage, rental-asset handling — §17.13); Mining Pack formalized (§17.20); white-label pilot with first partner brand**; Economics engine with lineage display; **PDF Document Conversion Engine v1 live (§17.29): AI-assisted template conversion with human review studio, full field types (signatures/photos/conditional logic/calculations), e-signature-wrapped completions, submission→register event hooks**. *Exit: pilots live on beachhead fleet/site with §14.5 contract; precision SLO being met; measured baseline vs actual scorecard running; third-party penetration test completed with criticals remediated, SOC 2 Type I issued and Type II observation window running, ISO 27001:2022 Stage 1 passed, customer-facing trust center live (§17.30 born-compliance calendar).*
- **Phase 2 — Orchestration (months 9–18):** Mode B write-back with ownership contracts and conflict queue (§12.2); constraint-based scheduling, frozen schedule, backlog intelligence; stores/MRO intelligence, reservations; competency-aware dispatch (capability view); Workforce Performance view available behind §11 activation; migration tooling; second/third certified connectors; partner SDK beta (§17.4/§17.7); **Transport Pack live (eDVIR chain, App A register — §17.14); Food & Beverage Pack v1 (sanitation-maintenance workflow — §17.19); Manufacturing & Process Pack v1 with API mechanical-integrity templates ahead of chemical entry (§17.21)**; **document engine governance depth: template registry workflow (draft→approved→retired with effective dating), countersign chains, scheduled digests, WO/economics/register event integrations at scale (§17.29.5, §17.29.7)**. *Exit: first Mode B customer in production; write-back conflict rate below agreed threshold; expansion quote generated from pilot data; SOC 2 Type II report issued, ISO/IEC 27001:2022 certified, CSA STAR Level 2 listed (§17.30 calendar).*
- **Phase 3 — Enterprise depth (months 18–30):** shutdown/turnaround; Boardroom/War Room (one meeting platform first); procurement intelligence; warranty; contractor lifecycle; CAPEX handover; maintainability/DfM; experimentation engine; environmental intelligence; voice beyond push-to-talk; UWB/RTLS where a customer funds it; Mode C standalone with migration factory; Federated Learning Network opened to consenting customers. **Pack completions: Agriculture Pack (ISOBUS, season calendars — §17.15), Facilities Pack (BMS/BACnet connector + full statutory library — §17.16), Energy & Utilities Pack (PRC-005-6 PSMP register semantics, DGA program — §17.17), Pharma/GMP entitlement layer with validation package (§17.18).** **Document engine scale-out: per-brand template registries at partner level (§17.22), bulk conversion batches for client template estates, Part 11-grade signature evidence for the pharma entitlement (§17.18), iOS client only if a customer demands it (§17.29.8).** *Exit: Mode C reference customer; FLN contributing priors; full SAP-parity certification portfolio achieved and surpassed on OT/product duties: ISO/IEC 27001:2022 certified with 27017/27018 add-ons, BSI C5 audited, ISO 22301 (BC plan exercised), ISO 9001 (quality) as buyer demand requires, SOC 2 Type II current, ISASecure SDLA for OT components, CRA conformity file complete ahead of Dec 2027 (§17.30 born-compliance calendar).*

**Federated Learning Network gate:** FLN participation (§17.1) launches only after: differential-privacy/aggregation design passes external review; consent artifacts pass customer legal review in ≥2 geographies; and ≥3 customers sign the data-sharing addendum. Until then, Tier 1 priors come solely from OEM libraries (§17.2).

# 17. New Capability Specifications (Research-Derived Additions)

## 17.1 Federated Reliability Learning Network (FLN)
Cross-customer model-prior network. Each customer site trains local models; only privacy-preserving aggregates (gradient/statistical summaries with differential privacy, never raw data) contribute to shared priors per asset family/failure mode. Opt-in per customer with explicit data-sharing addendum; per-jurisdiction legal review; customer-visible "contribution ledger" showing what their data improved; opt-out removes their contribution from future prior releases. Governance board with customer representatives approves prior releases. *Closes the cold-start gap at fleet scale without creating a data-trust liability; also a retention moat (network effects).*

## 17.2 OEM Failure Mode Library Program
Licensed and curated failure-mode/interval libraries per asset family (aligned to ISO 14224), covering: common failure modes, mechanisms, symptoms, diagnostic tests, P-F intervals, recommended tasks. Sources: OEM technical publications, reliability literature, engineering partners, DDE's own RCA corpus over time. Versioned, citation-carrying, and clearly labeled as priors in all outputs. Feeds Tier 0/1 cold start (§9), RCM templates, and the troubleshooting engine's seed graph.

## 17.3 Alert Trust & Suppression System
Full specification of the §10 system: precision SLO registry per alert class; quarantine queue; evidence bundles; one-tap verdict capture; retraining pipeline from verdicts; trust dashboards (per site/class/model); suppression objects (planned-work, temporary-with-expiry, systemic-proposal); noise budget enforcement; alert-value ranking (expected cost avoided per interruption). KPIs: confirmed-actionable precision, false-positive rate, mean time-to-acknowledge, suppression rate, technician trust index (survey + behavioral proxy: % alerts acknowledged vs dismissed).

## 17.4 Model Governance & AI Conformity Pack
Continuous artifact set per model: intended purpose, training-data lineage, evaluation results (precision/recall/calibration per segment), known limitations, drift monitoring, version history, human-oversight design, decision logs (≥6-month retention for evaluative uses), and the EU AI Act Annex III technical-documentation skeleton maintained to Dec-2027 readiness. Includes model registry with stage gates: no model output reaches production surfaces without registry entry, evaluation evidence, and an owner.

## 17.5 Works Council / Privacy Pack for Workforce Analytics
The customer-facing artifact bundle for §11: transparency documentation, worker-representative notification drafts, lawful-basis worksheets (GDPR Art. 6/9 analysis where applicable), retention/aggregation configuration presets per jurisdiction, technician self-service data access, and an activation audit trail. Sold as *reducing the customer's legal burden* — a differentiator, not overhead.

## 17.6 Integration Conflict Resolution Engine
The runtime implementing §12.2: ownership-contract registry, idempotent write pipeline with exactly-once semantics, field-level conflict detection, policy-driven auto-resolution for low-consequence fields, human resolution queue with side-by-side context for consequential fields, full journaling and reversibility, and conflict-rate analytics per connector (a connector health KPI sold into IT reviews).

## 17.7 Connector Certification & Partner SDK
Public SDK (canonical-model typed API, sandbox tenants, conformance test suite), certification tiers with published registry, marketplace listing, and partner revenue share on marketplace connectors. Target: by end of Phase 2, ≥5 partner-built certified connectors covering mid-market CMMSs and regional ERPs that DDE will never build itself.

## 17.8 Customer Economics Profiler
The §8.4 onboarding product: structured workbook + in-app wizard; interviews finance/ops/reliability; captures the §8.2 input catalog with lineage and confidence; validates against sanity ranges; produces the signed Economics Baseline; supports re-profiling (versioned) as the customer's data improves; feeds pilot KPI baselines (§14.5) and Boardroom rollups (only lineage-complete inputs).

## 17.9 Pilot-to-Production Conversion Framework
The §14.5 commercial product: pilot contract templates with pre-agreed conversion pricing and criteria; baseline measurement protocol; weekly value scorecard generator; exit-meeting toolkit; lessons-learned pipeline into product and sales enablement. KPI: pilot→production conversion rate (target ≥60% by end of Phase 2).

## 17.10 Standards & Audit Evidence Pack
The living conformity artifact set, now the single source of truth behind §15: per-obligation matrix (obligation → capability → evidence artifact → owner → status); ISO 55001 alignment matrix; ISO 14224 mapping tables; IEC 62443 zone/conduit architecture document with SL targets per component and the seven foundational requirements mapping; SOC 2 control mapping and ISO 27001 statement of applicability draft; functional-safety boundary statement (DDE is not a SIF); EU AI Act conformity pack (§17.4) cross-referenced; statutory inspection regime templates per jurisdiction (§15.5–15.6); CRA technical file and SBOM inventory for edge/app products; e-signature validity notes per market; accessibility conformance reports. Maintained by product compliance; consumed by sales (RFQ checklists), delivery and auditors.

## 17.11 Fleet & Telematics Vertical Pack
Beachhead packaging of existing DNA: J1939/CAN-FD parameter ingestion (fault codes, fuel, hours, GPS), **dual-path data acquisition** — (a) OEM telematics APIs (budget per-OEM API fees as pass-through line items; equipment-data rights are contested and OEM portals may throttle third-party access), and (b) aftermarket CAN gateway/loggers as the *default pilot path* (full-rate raw data, no OEM fee, works on modem-less legacy machines), plus neutral aggregator support where fleets already subscribe — mobile-equipment asset model (machine → component → attachment), fleet KPIs (availability, utilization, cost-per-hour, planned-vs-unplanned ratio), component life tracking by serial number, and mobile-crew workflows (field service trucks, remote sites, offline-first emphasis). Sales objection kit for "the OEM portal already gives me this": no cross-OEM unification, no work-history fusion, no predictive layer. This pack is the fastest route to a measurable pilot because telematics provide an objective, pre-DDE baseline for downtime and cost-per-hour.

## 17.12 WO Text Intelligence
Technical-Language-Processing pipeline over free-text work-order descriptions and completion notes (historical and incoming): extracts failure modes, components, detection methods, actions and cost signals; reconciles them against structured failure codes and flags systematic misclassification (e.g., unflagged failures that distort MTBF); feeds the data-quality score, the failure graph, cold-start Tier 2/3 training labels, and the troubleshooting engine's case base. Rationale: peer-reviewed studies show ~48% of breakdown WOs lack usable failure descriptions, detection-method fields are empty in 60–98% of cases, and cost fields were historically ~20% populated at studied sites — while free text remains information-rich. Structured codes alone cannot seed the reliability memory at most sites; text is where the recoverable signal lives.

## 17.13 Construction Vertical Pack
Co-beachhead packaging on the common core (evidence and verdicts: `DDE_Multi_Vertical_Strategy.md` §2.2): work orders roll up to **projects/cost codes** (not only assets/locations) so maintenance cost lands where contracts see it; **rental & mixed-ownership fleet handling** (owned vs rented vs subcontractor machines; rental-cost lines feeding the Economics Profiler); **contract-penalty economics input** — liquidated damages / milestone penalties as a first-class downtime cost type alongside production loss (§8.2 supports this already); site-based location hierarchy replacing plant hierarchy; utilization analytics tuned to construction benchmarks (industry average 30–40% untracked vs 80%+ best-in-class telematics-tracked). Shares the Fleet Pack's J1939/gateway ingestion unchanged — construction mobile equipment is CAN-standard. Weather-as-schedule-constraint context surfaces from v1 §7.3.

## 17.14 Transport & Logistics Fleet Pack (fully specified)
Profile of the Fleet Pack (§17.11) reusing J1939/FMS ingestion unchanged, plus transport-specific operations: **driver vehicle inspection reports (eDVIR)** with the defect→repair→next-driver-acknowledgement chain enforced in workflow (US final rule effective 23 Mar 2026 explicitly authorizes electronic DVIRs under 49 CFR 396.11/396.13); **annual periodic inspection register** per 49 CFR 396 Appendix A (13 systems, no partial inspections, 14-month report retention, inspector-qualification evidence) and CVSA Level I equivalence; **tachograph/driving-time data handling** (AETR 56-day retention for EU/UK international work; driver-privacy separation per §11 — driving-time data used for compliance, not performance, unless §11 activated); roadworthiness regimes per jurisdiction (EU 2014/45/EU class); **per-km/per-delivery economics** with SLA-credit penalty type (§8.2); trailer/dolly as individually inspected units; maintenance-cost-per-mile benchmarking. Sweet spot: regional carriers and bus/coach operators without OEM walled-garden leverage.

## 17.15 Agriculture Pack (fully specified)
**Season-aware maintenance scheduling** — the pack's defining feature: critical-window calendars (planting/spraying/harvest) during which planned maintenance is auto-deferred to off-peak and predictive alerts escalate with window-adjusted urgency (harvest-season combine downtime runs up to ~$1,500/hr in lost yield, labor and expediting); **ISOBUS (ISO 11783) ingestion** alongside J1939 — tractor-implement pairing, task data, implement health from the same diagnostic-socket gateway hardware as the Fleet Pack (plug-and-play 9-pin); mixed-fleet economics per hectare/per engine-hour; **seasonal asset dormancy workflows** (pre-season recommissioning checklists, storage-condition inspections, post-season defect harvesting); implement/attachment tracking by serial number; fuel-theft/anomaly signals where telematics report fuel; FMIS (farm management information system) export hooks. Compliance: light (agricultural exemptions dominate), so the pack sells on season economics, not registers. Channel-led go-to-market via equipment dealers; direct sales only for large corporate farms.

## 17.16 Facilities & Buildings Pack (fully specified)
**Statutory compliance is the wedge** (downtime economics are weak; certificate deadlines are the pain): the register library ships facilities templates — LOLER lifting inspections (6-monthly), PUWER work-equipment regimes, **F-Gas leak-check intervals by CO₂e charge band** (≥500t: 3-monthly; 50–500t: 6-monthly; 5–50t: annual), fire safety under the Regulatory Reform Order 2005 + Fire Safety Regs 2022 (FRA annual, monthly system checks, BS 5839-1:2025 servicing alignment), EICR 5-yearly electrical verification, Legionella L8/HSG274 control regimes, PSSR pressure systems, CAR 2012 asbestos registers, Building Safety Act duties for higher-risk buildings; US equivalents (ASME A17.1 elevators, NFPA cycles, state boiler rules). **BMS/BACnet connector** converts building-system alarms into tracked work orders (v1 §7 protocols already list BACnet); contractor-oversight features (statutory certificates held centrally regardless of who performs work — dutyholder liability sits with the client, not the lift contractor); portfolio-level compliance dashboards per building and per certificate cycle; FCI (facility condition index) reporting for capex planning; SFG20-style maintenance-regime mapping as import format. Opportunistic entry via clients who already run DDE elsewhere (mining/construction camps, plants with admin estates).

## 17.17 Energy & Utilities Pack (fully specified)
**Protection System Maintenance Program register** built to NERC PRC-005-6 semantics: component-type interval tables (Tables 1-1–1-5, Table 2/3, 4-1–4-3, Table 5), **monitoring-status attribute per component with monitoring-based interval extension only where the standard's alarm attributes are met**, time-based vs performance-based program support (Attachment A segment logic), dated-evidence generation per requirement — a missed interval is a violation regardless of asset failure, so the due-date engine treats PRC-005 dates with the same non-deferrable severity as statutory safety registers (§15.6). **Transmission vegetation management** (FAC-003-5): line patrol scheduling, LiDAR/inspection-result ingestion, clearance-defect work orders. **Transformer condition program**: DGA (dissolved-gas) trend ingestion via lab feeds and online monitors → investigation work orders on rising-gas trends; SCADA alarm → WO conversion; oil-quality test history. Substation asset model (bay → protection system → component with monitoring attributes); grid-code/region-specific analogues templated (NERC is the reference implementation; EU/SA grid codes map onto the same register engine); outage/switching coordination hooks (planned-outage requests linked to maintenance windows). Entry remains Phase 3: long sales cycles, incumbent APM mindshare — but the pack is *specified now* because PRC-005-class register semantics validate the register engine's design generality.

## 17.18 Pharma & GMP Pack (fully specified — validation-ready posture)
The highest-compliance-burden vertical, planned in full so the architecture never precludes it: **GAMP 5 (2nd ed.) Category 4 configured-product posture** with a maintained validation evidence package — Validation Plan, URS, IQ/OQ/PQ protocol templates customers execute, traceability matrix, supplier assessment pack (auditors assess the vendor; DDE ships the evidence rather than becoming the audit obstacle); **21 CFR Part 11 / EU GMP Annex 11 controls**: enforced audit trails on GxP-relevant records, e-signature integrity (§15.10 layer extended with Part-11 semantics: signature manifestations, meaning-of-signature, re-validation on change), ALCOA+ data-integrity rules in record handling, access control with periodic review; **calibration management depth** (v1 §34 extended): calibration traceability chains, out-of-tolerance impact reconstruction ("what else was measured with it since the last good calibration"), calibration-before-use gating on GMP assets; **maintenance→quality handoffs**: post-maintenance QA return-to-service sign-off, GMP-critical asset classification driving documentation depth; CSA (Computer Software Assurance) alignment — the Feb 2026 final FDA CSA guidance enables risk-based, unscripted assurance where DDE's evidence capture automates the record. Sold only with a validation-services partner; entry gated on ≥2 regulated-industry references from adjacent packs (food, process).

## 17.19 Food & Beverage Pack (fully specified)
**Sanitation-maintenance integration is the pack's core workflow** (the classic audit failure is a closed maintenance WO with no sanitation handoff): automatic **post-maintenance sanitation work order** on every food-contact/CCP asset, sequenced before production restart — line restart is *system-blocked* until sanitation sign-off (method, chemical concentration, contact time, rinse verification, ATP swab results where used); **Master Sanitation Schedule** as an auto-generating WO stream (overheads, drains, HVAC, equipment teardowns by hygienic zone); **CCP asset register** linking metal detectors, magnets, sieves, X-ray, pasteurizers to HACCP control limits and monitoring frequencies; **allergen-changeover cleaning procedures** as enforced WO templates; **food-grade lubricant registry** (H1 lubricants only on food-contact equipment, enforced at parts-assignment); PM deferrals on compliance-critical assets require documented risk assessment + rescheduled date (SQF Ed. 9 / FSSC 22000 v6 expectation); audit-evidence generator producing the PM-completion, calibration-compliance and planned-vs-reactive reports GFSI auditors (SQF/BRCGS/FSSC 22000) request at audit opening; records retained ≥2 years (FSMA 21 CFR Part 117 minimum) with contemporaneous-recording discipline. Shares the cold-chain/refrigeration condition monitoring with the Facilities pack's HVAC/BMS connector.

## 17.20 Mining & Resources Pack (formalized)
The original beachhead vertical pack, previously implicit: SI 109/1990 (Zimbabwe) and MHSA-class statutory templates (§15.5); GISTM tailings and water-retaining structure registers (§15.6); mobile-fleet economics at mining downtime bands ($5k–$10k/hr haul trucks); Chinese-OEM dual-path telematics reality (§17.11); contractor-management workflows for mining service ecosystems; blast-area/hazardous-zone location model. Formalized as a pack so it composes with Fleet + Construction under the same bundle mechanism — no special-casing.

## 17.21 Manufacturing & Process Pack (formalized)
Discrete + process manufacturing profile: OEE-linked downtime accounting (ISA-95/ISO 22400 alignment per §15.9); **process-industry mechanical-integrity templates** (API 510/570/653 under OSHA PSM 1910.119(j) / Seveso III) with inspection-history-per-circuit views; turnaround/shutdown program management (v1 §33) with scope-growth tracking; rotating-equipment failure-library priority (pumps/compressors/agitators dominate process failure cost); historian connectors (PI/Aspen-class) for overlay mode; bad-actor/Pareto analytics tuned to line-level granularity; SPC/quality-hold hooks for regulated lines. This pack serves the Phase 1–2 manufacturing core and the Phase 2 chemical/process entry (verdicts: `DDE_Multi_Vertical_Strategy.md` §2.3–2.4).

## 17.22 Modular Platform & White-Label Architecture (the customization mechanism)
**Prime directive: customization is configuration, not code.** Every customer-facing variation — industry pack, jurisdiction registers, brand, language, units, integrations, deployment topology — is expressed as versioned configuration applied to one codebase. Full specification: `DDE_Modular_Platform_White_Label_Spec.md`. Summary of the mechanism:

- **Tenancy hierarchy:** platform → partner brand (optional white-label) → customer org → site → asset class, with cascading, lineage-traced settings inheritance.
- **Branding layer:** design tokens (logo, palette, typography, terminology dictionary — "Work Order" vs "Job Card"), custom domains with automated TLS, branded mobile shells, letterhead-rendered statutory certificates and audit exports, localization packs. Presentation-only constraint: branding can never weaken compliance-mandatory UI.
- **Integration manifests:** connectors instantiated by declarative YAML (type, endpoint, vault-ref auth, protocol parameters, direction, ownership contract per §12.2, versioned field-mapping sets with automated test harness, residency pin). Adding a customer integration = authoring manifests + mappings + certification harness — days, not projects.
- **Packs as signed versioned bundles:** schema extensions + failure-library slices + KPI sets + workflow templates + register templates + penalty types + locale defaults; packs compose (Fleet + Construction + Facilities-lifting for a crane contractor); compliance-interval conflicts resolve to the stricter interval with counsel-review flag.
- **Edition entitlements:** commercial flags (tier, packs, seats) separated from governance activations (§11 workforce view, Mode B write-back, FLN) which require their documented activation ceremonies as immutable events.
- **One manifest, three deployment shapes:** cloud multi-tenant, cloud dedicated/VPC, edge/on-prem/air-gapped (Zimbabwe load-shedding resilience per §13) — identical configuration promotes across all three.
- **Config-as-code lifecycle:** git-backed manifests, sandbox→staging→production promotion with automated validation (schema conformance, register-interval sanity, connector smoke tests, token linting), auditable change events (ISO 27001 / GAMP-class expectations).
- **Non-negotiable guardrails:** safety gating, economics lineage (rule 16), alert SLO floors (§10), audit-trail immutability, and statutory-overdue escalation are parametrizable in strictness but never removable — white-label means white-presentation, not white-box; resellers accept conformity flow-down (CRA declaration, SBOM, attestations).
- **Onboarding wizard:** standard-profile go-live in days — branding kit upload → pack selection → manifest authoring → migration factory → role templates → UAT runbook. Deviations beyond the parameter space become roadmap requests with named owners, keeping SI effort bounded.

## 17.23 Field Experience Applications (role surfaces & dashboards)
Four purpose-built surfaces on one codebase, each answering one 15-second question — full specification in `DDE_Field_Experience_Rugged_Hardware_Spec.md`: **Tech Kiosk App** ("what is my next safe job and what do I need to do it?") — shared-device kiosk model with NFC badge sign-in at workshop cradles; "My Day" single-column dashboard (safe-job banner that cannot be dismissed while relevant permits/isolations are open → next-job card with parts-kitted/permit status → today list max 5–8 rows with reason-coded deferrals → SLO-passed alerts only → requests); guided job-pack execution flow: safety gate first (permit/LOTO verification per site procedure), photo-evidence hold-points, parts scanning decrementing stores, voice-to-text failure capture feeding WO Text Intelligence (§17.12), automatic post-task hooks per vertical pack (sanitation WO in food §17.19, QA return-to-service in pharma §17.18, statutory certificate updates in facilities §17.16); **Supervisor App** ("who and what is stuck right now?") — auto-ranked stuck board naming the unblocking action and owner, crew coverage vs demand, VaR-ranked break-in alerts accepted into schedule with impact view, governed approvals (e-signature permits/isolations; deferral overrides except statutory-overdue which is never overridable); **Manager Console** (web/desktop, the only density-allowed surface) — three-column risk/flow/money layout: bad actors + VaR-at-stake + alert-SLO health (trust metrics displayed to engineers), schedule compliance + backlog aging + statutory due calendar, maintenance debt + cost-of-inaction queue with lineage badges; scenario modeling, RCA evidence-timeline replay, audit-pack generator, config-wizard entry; **Executive View/wallboard** — five numbers maximum (availability vs target, downtime cost MTD lineage-badged, schedule compliance, safety events, statutory compliance %), wallboard mode auto-rotating read-only for control rooms. Cross-surface design rules: ≥48px glove-rated touch targets, WCAG 2.2 AA+ contrast, stale-while-revalidate offline rendering (never a blank screen; visible data age), notification discipline mirroring §10 silence-over-noise, every metric tappable to exactly one "why" screen, 90-day widget-retirement rule enforced by usage telemetry.

## 17.24 Rugged Hardware Compatibility Program
Certified-compatibility matrix of field devices meeting DDE's minimum platform bar (IP65+, MIL-STD-810H drop ≥1.2m certified, −20°C to +50°C operation, ≥800-nit sunlight-readable displays, glove/wet touch, hot-swappable or full-shift batteries, Wi-Fi 6/cellular/GPS/NFC, MDM enrollment): reference classes — **general industrial** (Getac ZX10 G2 Android 1000-nit dual hot-swap; Zebra ET60/ET65 IP66/68), **vehicle-mounted** (Getac F110 G6 Thunderbolt 4 dual LifeSupport batteries; Panasonic Toughbook FZ-G2 modular bays; Dell Pro Rugged 10/12 Class I Div 2), **intrinsically safe Zone 1/21** (i.safe MOBILE IS940.1 Android 14 5G with programmable SOS key; Ecom Tab-Ex 05 DZ1; Aegex100M Windows Zone 1/Zone 0-with-case UL 913), **mining underground Group I** (i.safe IS945.M1), **Zone 2/22 fringe areas** (Getac ZX80W-EX, 2026 ARM/Windows ATEX/IECEx certified), plus a rugged-handheld pocket tier for scan-first quick jobs. Safety integration: the zone-classification layer flags assets/areas requiring Ex-certified hardware and **enforces device-tier geofencing — non-certified devices cannot sign in inside classified areas (logged)**. Hardware is customer-procured through the dealer/IT-reseller channel; DDE maintains the matrix, bundle configs per pack, and an MDM policy baseline template (kiosk lockdown, cert-pinned sync, update rings). Indicative budget bands shipped for procurement guidance ($1.3–2.5k rugged Android / $2.5–4.5k Windows fully-rugged / $6–9k Zone 1 IS).

## 17.25 Carry & Mount Ecosystem
Hands-free and workface-placement systems as first-class productized accessories within the compatibility program: hand-strap + kickstand cases (default walking-rounds carry), shoulder harnesses/holsters with quick-release for climb work, **magnetic mount attachments for stick-to-steel placement at the actual workface**, vehicle docks (Gamber-Johnson/Havis-class: one-hand docking/release, port replication, keyed theft lock, charge-while-docked keeping hot-swap batteries cycling), wall/cradle kiosks at workshops/permit offices/stores counters serving as the shared-device shift-start points. Zone-aware accessory catalog: non-certified metal accessories void Ex ratings, so the catalog filters by area classification using the same geofence logic as §17.24.

## 17.26 Field Acceptance Test Protocol
Per device-model × pack combination before rollout: 1.8m concrete drop ×6 faces mid-evidence-upload; spill/washdown testing including hydraulic oil and food-grade organics followed by wet-touch operation checks; ≥98% tap-target accuracy gloved; 12-hour double-shift endurance with hot-swap cycling; 500 dock/un-dock cycles; offline→sync integrity after 8-hour disconnect with 200 queued operations; sunlight legibility at 1000 lux; Ex-certificate document verification against the area register. Results recorded in the compatibility-matrix entry — a device is not "supported" until its protocol row exists.

## 17.27 Android Kiosk Hardening (device owner & COSU)
To prevent users from exiting the kiosk app, accessing settings, or flashing custom ROMs during boot/use, DDE mandates Android Enterprise device-owner mode with COSU (Corporate-Owned Single Use) lock task — proven techniques include:

- **Device owner provisioning**: via NFC bump, QR code, or zero-touch enrollment at first boot; installs a Device Policy Controller (DPC) that owns the device from power-on
- **Lock task mode whitelist**: only the DDE kiosk app package(s) are allowed in lock task; home, recent, and back buttons are disabled; system UI cannot be escaped
- **Boot animation suppression**: custom ROM (LineageOS/AOSP derivative) with `debug.sf.nobootanimation=1` in init.rc or a blank bootanimation.zip in /data/local — no flashing logos during boot
- **Status/navigation bar removal**: config_showNavigationBar=false and status_bar_height=0dp in device overlay; immersive sticky mode hides system UI completely
- **Physical button restrictions**: via DevicePolicyManager — disable power/volume keys (except long-press for emergency SOS mapped to site workflow); prevent reboot/shutdown from hardware
- **Unknown sources blocked**: install non-play-store apps disabled; ADB disabled in production builds; OTA updates frozen via policy during critical windows
- **Custom ROM friendliness**: unlocked bootloader devices (DOOGEE, Ulefone, Blackview lines) allow flashing a hardened kiosk ROM once; DDE supplies the ROM image with the above hardening baked in and verifiable via attestation
- **Attestation & verification**: SafetyNet Play Integrity API or custom bootloader hash check at launch to confirm the device is in the expected hardened state; any deviation triggers admin alert and forced re-enrollment

## 17.28 Tech-Expert Module Enhancements (beyond hardware)
Beyond the rugged tablet and kiosk lock, DDE's field modules are enriched with the following AI-native and workflow features that experts repeatedly request in evaluations:

- **AI-native predictive maintenance**: on-device TensorFlow Lite models analyze vibration/temperature/pressure streams weeks before failure; confidence scores and lineage are displayed per rule 16; fallback to cloud when connectivity returns
- **Digital twin integration**: each asset has a live virtual replica synchronised with IoT sensor data; technicians can run what-if maintenance scenarios on the twin before touching physical equipment; remaining useful life forecasts feed the troubleshooting copilot
- **Workflow automation**: AI-generated insights seamlessly trigger work orders, parts reservations, technician scheduling, and procedure guidance without human intervention — closing the loop from prediction to action
- **Agentic AI copilot**: natural-language troubleshooting ("why is this bearing hot?") returns step-by-step guidance with evidence timestamps; learns from closed jobs to improve future suggestions
- **Procedure versioning & gating**: HIRA/JSA checklists are versioned assets; the app enforces the latest approved version before permitting hazardous work; offline sync resolves conflicts via last-writer-wins with ownership per §12
- **Calibration impact reconstruction**: when a tool goes out of tolerance, the app answers "what else was measured with it since the last good calibration" by tracing the dependency graph (§17.18 pharma pack)
- **Voice-to-text for failure logs**: noise-resistant speech-to-text in harsh environments feeds WO Text Intelligence (§17.12) — technicians describe symptoms hands-free

## 17.29 PDF Document Conversion Engine (integrated with the Template Overlay render architecture)

AI-powered system that converts PDF documents (checklists, scheduled maintenance reports, work orders, safety certificates, regulatory forms) into digital input forms with intelligent field mapping, validation rules, conditional logic, and calculations; enables field technicians/supervisors to enter data via touch/voice/kiosk that populates structured databases while producing regenerated reports/documents that match the original approved PDFs. The engine is composed of two halves — **authoring/conversion** (AI-proposed, human-approved) and **runtime capture/render** (the Template Overlay Pattern) — plus a governed template lifecycle.

### 17.29.1 Core concept — Template Overlay Pattern (adopted from `digital-maintenance-report-architecture.pdf`)

The regeneration guarantee ("looks exactly like the original") is achieved by construction, not by re-implementing print layouts:

1. **Base Layer** — the existing approved PDF template used as an immutable background asset; never regenerated, only overlaid
2. **Coordinate Map** — a versioned JSON schema defining the exact position of every dynamic field: text, numbers, dropdown selections, checkboxes/radios, signatures, photos
3. **Data Capture** — the mobile/kiosk app captures technician input per §17.23 flows, including non-text data (signatures, photos, scans)
4. **Render Engine** — a backend service merges captured data onto the background template via a PDF generation library and outputs a flattened, uneditable official document

### 17.29.2 Render method decision

Four candidate methods were assessed against control, cost, setup effort and native signature/photo handling; **Method A (pdfme) is the production default**, with Method B as a fallback for customer-supplied fillable PDFs:

| Method | Control | Cost | Setup | Verdict |
|---|---|---|---|---|
| **A — pdfme (open-source TypeScript generator + WYSIWYG designer)** | Full | Free, self-hosted (MIT) | Medium | **Default.** MIT license permits commercial embedding; its WYSIWYG web designer doubles as the human review studio in §17.29.3; maps signature/photo as image-type fields natively |
| B — pdf-lib / AcroForms | Full | Free | Medium–high (requires Acrobat authoring) | **Fallback** when a client already supplies fillable PDFs; fields are named to match DDE data keys and flattened on generation; per-template Acrobat licensing is friction at scale |
| C — DocuSeal | Medium | Free self-host / paid cloud | Low–medium | **Rejected as system of record** — duplicates the §15.10 e-signature layer and forks the audit trail; acceptable only as an edge integration target |
| D — Managed APIs (CraftMyPDF-class) | Low | Usage-based | Lowest | **Pilot-only at most** — external data processing fails regulated-vertical residency requirements (§15.4), per-tenant white-label branding (§17.22), and cost predictability (§14.1 design rules) |

### 17.29.3 Authoring pipeline — analyze → define → review → approve (extends the source document)

The source document assumes hand-mapping every template in a WYSIWYG designer; DDE keeps the human-confirmed map but removes the manual toil:

1. **Analyze:** CV + layout analysis segments the PDF (lines, boxes, labels, tables); LLM pairing proposes field candidates with type guesses (text/number/dropdown/signature/image/calculation)
2. **Define:** proposed coordinate map + validation rules + conditional logic + calculation expressions generated as draft JSON
3. **Review:** human confirmation in a pdfme-designer-style studio — drag/nudge fields over the rendered template page, adjust types/options/rules side-by-side
4. **Approve:** the confirmed map is published as a signed, versioned tenant template (§17.29.5) — the runtime never trusts an unapproved map

### 17.29.4 Runtime capture & validation

- **Dynamic form generation**: one schema-driven screen set renders any converted template — touch-optimized with voice-input support, barcode/QR scanning, photo capture, and GPS tagging (field types: text, number, dropdown, checkbox, radio, date, signature, photo, calculation, scan)
- **Validation engine**: business rules, data-type constraints, range checks and cross-field dependencies enforced client-side with real-time feedback, and **re-validated server-side before render** — invalid data can never reach an official document
- **Conditional logic**: sections show/hide based on prior answers (permit escalation paths, safety hold-points, pass/fail branch inspection criteria)
- **Calculation fields**: totals, percentages, KPIs and cost impacts computed at entry; expression results stored alongside raw inputs so later template versions can recompute
- **Media handling budget**: photos captured full-resolution via FileProvider, compressed server-side to a defined budget; large media upload by reference URL rather than base64-in-payload; EXIF location stripped unless the site contract explicitly opts in (privacy default, §11.4 posture)
- **Countersign flows**: supervisor countersign steps append a separate signed record — corrections never overwrite an already-signed submission (audit trail preserved)

### 17.29.5 Template lifecycle governance

Templates are governed assets, not files:

- **Registry states:** draft → pending approval → active → retired, with effective dating and per-tenant visibility through the §17.22 tenancy hierarchy (brand-level template overrides supported; compliance-mandatory fields never removable by branding — same presentation-only constraint)
- **Change control:** edits create new versions; in-flight submissions finish on their starting version; historical reports always regenerate against the version they were submitted on (payload retained per §17.29.6 makes this possible)
- **Approval workflow:** template activation requires a named approver with e-signature (§15.10); pharma/GMP tenants additionally get Part 11-style approval evidence (§17.18 entitlement layer)
- **Deprecation:** retired templates remain renderable read-only for the statutory retention period of the relevant vertical/jurisdiction

### 17.29.6 Offline-first operation & durability (source-document pattern adopted verbatim where compatible)

- **Submit = synchronous local write.** Every submission is persisted immediately to durable local storage (op-log entity per §13.1: local ID, payload JSON, created timestamp, sync status PENDING/SYNCING/FAILED/SYNCED) — nothing is lost on app close, crash or signal loss
- **Background sync worker** (WorkManager-class periodic + connectivity-constrained) drains the queue with retry/backoff; resumable chunked transfer for media per §13.1 store-and-forward
- **Conflict stance:** single-author reports need no merge — server-authoritative last-write-wins suffices; supervisor countersigns are append-only records (never merged away); anything touching live safety state routes through §13.1's online-gating rule instead
- **UI truth:** a visible pending-sync badge per report until SYNCED; data-age banner per §17.23 cross-surface rules

### 17.29.7 Storage, lineage & distribution

- **Dual retention:** every report stores the flattened PDF *and* the raw capture payload (JSON + media references) — enabling regeneration under changed templates, comparison, and template-version archaeology; this is the §12 data-lineage principle applied to documents
- **Access control:** finished reports live in **private storage with short-lived signed URLs and RBAC** — public URLs are prohibited (compliance documents carry signatures and asset condition data)
- **Distribution:** automated email/notification on submission (supervisor/classic-recipient friction path), in-app history view per equipment/asset with share-sheet export, scheduled digests for management reporting; every artifact is also addressable by asset ID so it appears in the job pack and audit packs (§17.10)
- **Integration hooks (events, not dead-ends):** submission emits domain events consumed by WO Text Intelligence (§17.12 — failure descriptions feed the corpus), economics engine (§8 — measured quantities feed consumption models), compliance registers (§15.6 — completed certificates update statutory status), and the asset knowledge graph

### 17.29.8 Platform strategy & client architecture

Android-first native (Kotlin + Jetpack Compose) aligned with the §17.24 rugged-device matrix and §17.27 kiosk hardening; the form-rendering logic and offline-sync layer stay in a platform-neutral module so an iOS/Kotlin-Multiplatform port remains low-cost if a customer demands it (Compose Multiplatform reached stable May 2025 — viable when needed, not before). Rendering executes in the backend tier (Edge-Function-class), not on-device, so template assets and approved maps never ship inside the kiosk image.

### 17.29.9 Phased delivery (reordered — offline-first is Phase 1, not Phase 3)

| Phase | Scope | Correction vs source document |
|---|---|---|
| 1 — MVP | Template Overlay render (pdfme); dynamic form with text/number/dropdown; **offline-first queue + private storage + audit row from day one**; e-signature-wrapped completion signatures | Source doc's online-only MVP and email-only output rejected: weak shop-floor connectivity is the norm (§13), and unstored submissions are a data-loss risk |
| 2 — Rich capture | Signature pads, photo capture, conditional logic, calculation fields, validation rules per template | Sound slice as written; each new field type ships with its validation ruleset |
| 3 — Governance depth | Template registry workflow UI, countersign chains, digest scheduling, domain-event integrations (WO/economics/registers) | Moved earlier than a pure "nice-to-have" slotting because register updates (§15.6) depend on it |
| 4 — Scale-out | Per-brand template registries at partner level (§17.22), bulk conversion batches for client template estates, iOS if demanded | Cross-platform remains demand-triggered |

Key capabilities carried forward unchanged from the prior §17.29 definition: smart field detection (CV+NLP), dynamic form generation, validation engine, conditional logic, calculation fields, offline-first operation, pixel-faithful regenerated output with embedded lineage/validation metadata, version-controlled template management, and integration hooks — now bound to concrete mechanisms above.

## 17.30 Security & Trust Architecture (watertight data protection, external and commercial)

End-to-end security architecture for all deployment shapes and surfaces; full specification in `DDE_Security_Trust_Architecture.md`. Mandate: customer data is watertight against external attack **and** against commercial-intelligence exposure — downtime economics, failure libraries and production rates are competitively sensitive assets that DDE never sees beyond need, never repurposes, and can prove it protects. Pillars:

- **Trust doctrine (five non-negotiables):** tenant data owned by the tenant (DDE is custodian); competitive intelligence treated as radioactive — cross-tenant learning only via signed consent artifacts with differential privacy and contribution ledgers (§17.1); safety systems fail closed; zero standing privilege (just-in-time, purpose-bound, journaled); evidence over assertion (every claim maps to an auditable artifact in §17.10)
- **Data classification with a commercial tier:** C1–C5 scheme where C3 *commercial-confidential* (downtime costs, VaR, maintenance debt) gets the same engineering rigor as personal data — per-tenant envelope encryption, ABAC row policies, DDE-staff access only via customer-visible break-glass, prohibition register for cross-tenant feature consumption
- **Identity:** SSO/passkey-first with phishing-resistant MFA mandatory for admin/approval roles; step-up auth on consequential actions; field access = device attestation before user identity, offline-scoped signed role assertions that always re-verify online before safety-object interaction; workload identities (mTLS, short-lived certs) for every service — no static API keys anywhere
- **Cryptography:** TLS 1.3 everywhere with hybrid post-quantum key exchange (X25519MLKEM768, RFC 10024) on internet-facing terminators — neutralizes harvest-now-decrypt-later against multi-decade-horizon asset data; AES-256-GCM at rest with per-tenant envelope keys and BYOK/HYOK options on dedicated/on-prem; HSM-backed roots with two-person-control break-glass; crypto-shredding as the certified deletion primitive; FIPS 203/204-tracked crypto-agility register
- **Application/API defense:** 62443-4-1-aligned SDLC doubling as CRA secure-by-design evidence; OWASP API Top 10 (2023) mapped to controls — object-level authorization in one shared policy engine, egress-proxy SSRF defense wired to integration manifests, third-party API responses treated as hostile input; prompt-injection containment for agentic AI (retrieved content is data never instructions; agent authority ≤ invoking principal); sandboxed PDF-template parsing for the document engine (§17.29.4 hardening)
- **Field device security:** layered kiosk lockdown (§17.27) plus encrypted local op-log (Keystore/StrongBox keys), FLAG_SECURE evidence screens, remote/auto wipe including the offline queue, Play Integrity verdict tiering (STRONG=full trust → DEVICE=normal → BASIC=view-only → none=refused) with hardware-key-attestation substitution for custom-ROM fleets, BadUSB/rogue-peripheral defenses (OTG blocked, challenge-response NFC, Bluetooth locked out)
- **Insider risk & detection:** hash-chained audit plane with tenant-visible near-real-time stream (trust through transparency); UEBA anomaly detection on C3/C5 access patterns; quarterly access recertification; DDE holds itself to the NIS2-grade bar it asks of customers
- **Incident response:** CRA 24h/72h reporting workflow rehearsed with pre-drafted templates; ransomware playbook anchored on quarterly-tested immutable restores; vulnerability disclosure policy with safe harbor
- **Assurance roadmap sequenced to revenue stages:** SBOM pipeline + secure SDLC (Phase 0) → pen test + SOC 2 Type I + trust center (Phase 1) → SOC 2 Type II (Phase 2) → ISO/IEC 27001:2022 certification + ISASecure SDLA + CRA conformity file before Dec 2027 (Phase 3). Security acceptance criteria are release gates, not aspirations (§12 of the spec)

**Born-compliance doctrine (upgraded from sequenced-certification):** the platform launches with the *structure and infrastructure* of a certified system already operating — a continuous-evidence engine where every control emits audit evidence as a byproduct of operation (controls-as-code registry mapped once to ISO 27001 Annex A / BSI C5 / CSA CCM / SOC 2 TSC / CRA Annex I / 62443-4-1), an ISMS with drafted SoA across all 93 Annex A controls live before first customer data, and quarterly management-review cadence from day one. The reference bar is the full SAP cloud portfolio (ISO 27001/27017/27018, 22301, 9001, C5, CSA STAR, SOC 1/2): every control those audits test operates at launch, plus OT (62443-4-1/-4-2), field-device attestation, commercial-intelligence isolation, and CRA/AI-Act product duties that SAP's portfolio does not cover. Acquiring each accreditation becomes scheduling + application against existing proof — SOC 2 Type I at month ~3, ISO 27001:2022 certificate ~month 8–9, C5/27017/27018/27701 riding the same cycle — not a remediation project. Honest limits documented: observation windows (~3–9 months) cannot be skipped, so certificates land months after launch; no certification name is marketed before it exists.

**Full task cadence & security metrics:** compliance audits cover the entire operational cadence — continuous/daily/weekly/monthly/quarterly/semi-annual/annual scheduled tasks plus per-event triggers (§11.6 of the security spec), each with automatic evidence capture; internal and external auditors sample cadence execution records directly, so a missed scheduled task is an audit finding by definition. A 30-metric security metrics program (§11.7: vulnerability MTTR, patch-SLA adherence, scan coverage, MTTD/MTTR, break-glass events, encryption coverage, device attestation pass rates, controls-green rate, audit-finding aging, AI-control violations, etc.) drives monthly scorecards, quarterly management reviews, release gates, and a customer-shareable trust-center view.

This capability closes the residual exposure in §15.2 by binding the compliance framework's legal obligations to concrete engineering mechanisms.

# 18. Remaining Deliverables (from v1 §77, updated)

The v1 list of follow-on specifications stands, re-sequenced behind the decisions in this plan and with three additions:

1. Canonical Domain Model & Database Specification *(now includes ownership contracts, lineage schema, sync op-log, model registry)* — **first deliverable**
2. Connector & Integration Architecture (per-incumbent patterns, certification program)
3. Safety/HIRA/JSA/LOTO/PPE Specification (extends v1)
4. Technician Tablet & Offline Architecture (extends §13)
5. Economics Engine Specification (extends §8)
6. AI/ML & Agent Architecture (extends §9, §10, §17.1–17.4)
7. Industrial Connectivity & Edge Architecture (extends 62443 design)
8. Maintenance Planning & Scheduling Engine Specification
9. Stores/MRO & Procurement Specification
10. Boardroom/Collaboration Architecture
11. Migration Architecture
12. Cybersecurity & OT Security Architecture (extends §15.2)
13. **GTM & Pricing Specification** (extends §14: TAM model, channel, sales playbook)
14. **Pilot Measurement & ROI Framework** (extends §17.9)
15. **Workforce Analytics Governance Specification** (extends §11/§17.5)
16. **Vertical Pack Content Specifications** (extends §17.11, §17.13–§17.21: failure-library slices, register templates per jurisdiction, workflow templates per pack)
17. **Configuration & White-Label Platform Specification** (extends §17.22: manifest schemas, validation suite, branded-build pipeline, onboarding wizard)
18. **Field Experience & Device Program Specification** (extends §17.23–§17.26: design-system component library, dashboard wireframe sets per role, compatibility-matrix data model, MDM baseline)
19. **Document Engine & Template Registry Specification** (extends §17.29: coordinate-map schema, validation-rule DSL, render-service API, template registry workflow, bulk-conversion tooling, pdfme-based review studio build/buy confirmation)
20. **Security & Trust Architecture Implementation Specification** (extends §17.30: policy-engine control matrices, key-ceremony runbooks, UEBA detection catalogue, IR playbooks, trust-center build-out, certification audit program)

# 19. Decision Log & Open Questions

Decisions taken in this version: naming/positioning (§2); full-scope MVP with sequencing gate (§4); differentiation thesis and kill criteria (§3.4); economics lineage rule (§8); cold-start tiering (§9); alert SLOs (§10); workforce governance default-off (§11); ownership contracts (§12.2); offline safety-gating (§13.1); pricing architecture and beachhead (§14); **compliance treated as a governed product function with per-market launch gates (§15)**; phase structure (§16); FLN launch gate (§16); **full industry pack suite specified for all ten verticals with researched operational features and compliance registers (§17.11, §17.13–§17.21); customization-as-configuration architecture adopted — branding + integration parameters, not code forks (§17.22)**; **document engine render method decided — pdfme (Method A) as production default with AcroForm fallback, managed-API providers rejected for production on residency/branding grounds, DocuSeal rejected as system of record (§17.29.2); Template Overlay Pattern adopted as the §17.29 regeneration mechanism with AI-assisted authoring replacing hand-mapping (§17.29.1–17.29.3); offline-first capture moved to document-engine Phase 1 with submit-time durability guarantee added to the offline doctrine (§13.1, §17.29.6, §17.29.9); signature fields e-signature-wrapped platform-wide (§15.10); finished reports stored privately — public URLs prohibited (§17.29.7)**; **security & trust architecture adopted — commercial-confidential data classification with break-glass-only staff access and cross-tenant prohibition register, zero standing privilege, PQC-hybrid TLS on internet-facing terminators, per-tenant envelope encryption with crypto-shredding as the certified deletion primitive, attestation-tiered field-device access, security acceptance criteria as release gates (§17.30)**; **born-compliance doctrine adopted in place of sequenced-certification — the SAP-parity control set plus continuous-evidence engine operates from Phase 0 so every accreditation reduces to scheduling + application against existing proof (SOC 2 Type I ~month 3–4; ISO 27001:2022 certificate ~month 8–9; C5/27017/27018/27701/22301/9001 riding the same evidence cycle; ISASecure when OT-pack revenue justifies); certification names never marketed before issued (§17.30, `DDE_Security_Trust_Architecture.md` §11–§13)**.

Open questions requiring owner decisions before Phase 1 exit: trademark clearance result for the DDE expansion (§2); first certified connector target confirmed by design partners (§16 Phase 0); FLN external privacy review completion (§16); pilot contract legal template sign-off (§14.5); works-council pack review by EU employment counsel (§11.3, §15.12); **CRA reporting readiness confirmation ahead of the 11 Sep 2026 go-live (§15.13) — counsel + security sign-off that the ENISA reporting runbook and SBOM pipeline are operational;** statutory-register template priority order confirmed against first design-partner jurisdictions (§15.6); **OEM telematics API commercial terms obtained for ≥2 priority OEMs in the beachhead geography (§17.11); aftermarket CAN gateway hardware partner selected and unit economics modeled (§17.11).** **Multi-vertical additions: construction-sector sizing in the first reference market (contractor registries, fleet counts — the vertical strategy doc flags this as its only Zimbabwe-specific gap, §7); dedicated evidence passes for transport/agriculture/facilities before their phase entries (`DDE_Multi_Vertical_Strategy.md` §7).** **Modularity additions: white-label partner contract template with conformity flow-down clauses drafted (§17.22); branded mobile-store publishing pipeline proven end-to-end before the first partner go-live; register templates counsel-reviewed for the first two jurisdictions per pack before that pack is sold (§15.6).** **Field-experience additions: beachhead-market rugged-device SKUs and Ex-certified models confirmed procurable in-market (lead times, duty/tax impact on budget bands — §17.24); device acceptance protocol executed on the two pilot-fleet device choices before Phase 1 exit (§17.26).** **Document-engine additions: pdfme long-term maintenance posture re-verified before Phase 1 commit (activity, license, roadmap — with pdf-lib fallback plan documented, §17.29.2); first five client documents converted end-to-end as the Phase 0 acceptance test, including one with signature and photo fields; signature-wrapper legal sufficiency reviewed per launch jurisdiction (advanced-signature equivalence under eIDAS/ESIGN/ECTA, §15.10); media retention/EXIF policy defaults confirmed against first-market privacy counsel (§15.4).** **Security additions: external penetration test scheduled and remediation budgeted before first pilot go-live (§17.30 roadmap); key-management design (HSM provider vs on-prem HSM for edge deployments) selected; break-glass access workflow legal-reviewed per market (customer-notification wording, §17.30 §2.2); Play-Integrity-tier policy thresholds confirmed against the pilot device matrix — including custom-ROM fleets where hardware key attestation substitutes (§7.3 of the security spec); cyber-insurance posture scoped against the CRA 24h/72h reporting duties (§15.13, §17.30); born-compliance budget line item named in Phase 0–1 planning (initial certification fees + auditor remediation reserve — security spec §13.3) and SOC 2/ISO 27001 assessor slots reserved early so application windows hold (§17.30 calendar).**

## Evidence base

The evidence base now includes seven companion documents: **`DDE_Industry_Simulation_Research.md`** (global evidence: buyer-adoption surveys (osapiens × Fraunhofer IML, n=407, Jul 2025; 2025 industry aggregations), peer-reviewed maintenance-data-quality studies (NIST; PHM Society; academic CMMS analyses), Siemens/Senseye True Cost of Downtime 2024, equipment-data-rights legal analyses, and published EAM/CMMS pricing and sales-cycle benchmarks), **`DDE_Zimbabwe_Market_Entry_Research.md`** (first-market assessment: mining-sector scale and buyer segmentation, POTRAZ data-protection licensing, SI 109/1990 safety regulations, RBZ dual-currency and USD-payment mechanics, ZESA power and connectivity constraints, Chinese-OEM fleet reality), **`DDE_Multi_Vertical_Strategy.md`** (all-industry scope correction: vertical-by-vertical evidence and verdicts across all ten v1 §70 industries — construction downtime/utilization economics ($500–$1,000+/hr; $2–10k/day; 40–48% downtime reduction from telematics+CMMS integration) supporting co-beachhead status, chemical/process mechanical-integrity compliance wedge (OSHA PSM 1910.119(j); API 510/570/653) as the Phase 2 entry, transport/agriculture/facilities/pharma sequencing verdicts, and the vertical-neutral-core architecture principle), **`DDE_Modular_Platform_White_Label_Spec.md`** (customization-as-configuration mechanism: tenancy hierarchy with partner branding, declarative integration manifests, signed pack bundles, config-as-code promotion across cloud/dedicated/edge deployment shapes, guardrails preserving compliance invariants), **`DDE_Field_Experience_Rugged_Hardware_Spec.md`** (field-experience layer: four role surfaces with dashboard structures, glove-rated UX rules, offline rendering discipline; certified rugged-device matrix as of Aug 2026 — Getac ZX10 G2/F110 G6/ZX80W-EX (Zone 2/22), Zebra ET60/65, Panasonic Toughbook FZ-G2, Dell Pro Rugged 10/12 (Class I Div 2), intrinsically-safe i.safe IS940.1 Zone 1/21 / IS945.M1 mining Group I / Aegex100M UL 913 Zone 0-1; carry/mount ecosystems via Gamber-Johnson/InfoCase-class hand straps, harnesses, magnet mounts, vehicle docks; device acceptance protocol; verified purchase links and bulk-sourcing channels for the Chinese rugged tier), **`digital-maintenance-report-architecture.pdf`** (document-engine architecture source: Template Overlay Pattern with coordinate-map JSON schema; four render methods assessed — pdfme/AcroForms/DocuSeal/managed APIs — with signature-and-photo handling per method; Kotlin/Compose dynamic-form capture with full field types; Room + WorkManager offline-first durability pattern with submit-time local write and background sync worker; payload-plus-PDF dual retention for regeneration/audit; Supabase-class storage/distribution flow; Android-first vs KMP platform analysis with Compose Multiplatform stability assessment — integrated into §17.29 with corrections: offline-first moved to Phase 1, private storage mandated over public URLs, e-signature wrapper added, template governance registry added), and **`DDE_Security_Trust_Architecture.md`** (security layer: threat model spanning opportunistic through nation-state adversaries with commercial-intelligence theft named as a first-class threat; five-pillar trust doctrine; C1–C5 classification with commercial-confidential tier and cross-tenant prohibition register; PQC-hybrid TLS (X25519MLKEM768/RFC 10024) + per-tenant envelope encryption + HSM two-person-control + crypto-shredding; OWASP API Top 10 (2023) control mapping; Play Integrity verdict tiering with hardware-key-attestation substitution for custom-ROM fleets; rogue-peripheral defenses; insider-risk UEBA with tenant-visible audit streaming; CRA 24h/72h rehearsed IR; **born-compliance infrastructure: controls-as-code registry mapped once across ISO 27001 Annex A/BSI C5/CSA CCM/SOC 2 TSC/CRA Annex I/62443-4-1, automated evidence collection, certification application calendar targeting the full SAP cloud portfolio (ISO 27001/27017/27018/22301/9001/C5/CSA STAR/SOC 1-2) with SOC 2 Type I ~month 3–4 and ISO 27001:2022 certificate ~month 8–9, honest-limits section acknowledging non-skippable observation windows** — verified facts as of Aug 2026: ISO 27001:2013 certificates invalid since the 31 Oct 2025 IAF deadline, CRA reporting obligations live since 11 Sep 2026, FIPS 203/204/205 published Aug 2024).

Key evidence-driven changes: WO Text Intelligence added (§17.12); dual-path fleet data strategy with gateway-default pilots — confirmed as the *only* viable path for Chinese-OEM fleets in the first reference market (§17.11); Operations site platform fee restructured (§14.1); finance-first economics sourcing rule and sanity bands (§8.2); maintenance-champion clause and conservative pilot KPI targets (§14.5); right-to-repair legislative watch (§15.14); Zimbabwe named first reference market with two-tier entry strategy (§14.2); frontier-market USD annual-prepay billing rules (§14.1); POTRAZ licensing support obligations and SI 109/1990 statutory template added to compliance framework (§15.4–15.5); power-outage resilience elevated to a required deployment characteristic for the first market (§13); **vertical scope statement added correcting any mining-only reading (§14.2); construction promoted to co-beachhead with a dedicated pack (§17.13); full industry pack suite researched and specified — Transport eDVIR/App A registers (§17.14), Agriculture ISOBUS + season-aware scheduling (§17.15), Facilities statutory library + BACnet (§17.16), Energy/Utilities PRC-005-6 PSMP register semantics + DGA program (§17.17), Pharma GAMP 5 Cat-4 validation posture + Part 11/Annex 11 controls (§17.18), Food & Beverage sanitation-maintenance integration + CCP register (§17.19), Mining and Manufacturing/Process formalized as packs (§17.20–17.21); modular white-label platform architecture adopted so client customization = branding + integration parameter actioning (§17.22); document engine integrated — Template Overlay render architecture, pdfme render decision, AI-assisted authoring pipeline, submit-time durability rule in the offline doctrine, e-signature wrapper for all signature fields, template lifecycle registry, private storage + payload lineage, and reordered delivery phases placing offline-first capture at Phase 1 (§13.1, §15.10, §16, §17.29)**. Residual items that only physical groundwork can settle are listed in each document's limitations section — for Zimbabwe specifically: named-account EAM mapping of the top ~30 operations, POTRAZ licensing practice in action, Chinese group-IT approval chains, real OEM telematics API terms, and payment-rail reliability testing; for the multi-vertical expansion: construction-sector sizing in Zimbabwe; for the pack suite: jurisdiction template counsel review per market before sale, and branded-store publishing lead times; for the document engine: pdfme long-term posture re-verification and signature-wrapper legal sufficiency per launch jurisdiction (§19); **for security: penetration-test cadence and remediation budget, key-ceremony runbook sign-off, break-glass workflow legal review, and attestation-policy thresholds for the pilot device matrix — all listed as Phase 1-exit open questions above**.
