# DDE AECI Operations Pack — Configuration Specification v1.0

**Document status:** Customer-specific pack configuration for the DDE Asset Operations Intelligence Platform, configured for **AECI Mining Explosives Zimbabwe** operations (surface open-pit service sites nationwide + underground operations at Zimplats Ngezi). Built on the master-plan architecture (`DDE_Maintenance_Intelligence_ERP_Master_Plan_v2.md` §17.22 Modular Platform & White-Label Architecture) — every customization below is expressed as configuration (pack bundle + integration manifest + register jurisdiction template), not code forks.
**Customer evidence base:** `DDE_AECI_Zimbabwe_Customer_Research.md`.
**Date:** 22 August 2026
**Status note:** Per user direction, additional operational context will be supplied later; fields marked **[PENDING CONTEXT]** are deliberate extension points in this version.

---

# 1. Scope Statement

This pack configures DDE so that AECI Zimbabwe's technicians can run the full maintain-and-servicing lifecycle for their three stated asset families — **charging units, transfer pumps, storage facilities** — plus the mobile road fleet that carries them, across:

- **Surface:** open-pit service deployments at customer mines around Zimbabwe (Eureka/Guruve confirmed publicly; lithium-belt and Midlands sites expected per research §4).
- **Underground:** the Zimplats Ngezi Mining Division estate (Bimha, Mupani, Mupfuti, Rukodzi, Ngwarati portals + concentrator), where AECI supplies and services bulk-emulsion delivery capability.
- **Supporting infrastructure:** Harare head office/workshop, road tankers and support vehicles, and (status pending confirmation) the in-country bulk emulsion plant.

The pack adds three things beyond generic maintenance: **(A)** an explosives-service-provider asset taxonomy and failure-mode library, **(B)** a Zimbabwe road-fleet statutory register set (VID Certificate of Fitness, ZINARA licensing, insurance, speed-governor certification), **(C)** a Ministry-of-Mines manufacturing-licence register with plant compliance conditions — all integrated *alongside* (not replacing) the security systems AECI already subscribes to.

---

# 2. Tenancy, Branding & Deployment Shape

| Parameter | Configuration |
|---|---|
| Tenant hierarchy | `AECI Group → AECI Mining Explosives (Southern Africa region) → Zimbabwe business unit → site → area → asset` |
| White label | AECI branding tokens (logo, palette, terminology glossary: "charging unit", "MMU", "silos", "blast window"); AECI SHEQ language ("Zero Harm") used in UI microcopy |
| Deployment shape | Hybrid cloud core (SA-hosted region preferred for POTRAZ transfer posture per market-entry research §3.1) + site edge nodes at Harare workshop and each resident service site; offline-first tablets per master plan §13 |
| Modes | Start **Mode C standalone** (own WO system of record for the delivery-equipment estate) with **Mode A overlay connectors** available for host-mine contexts (read-only SAP awareness at Zimplats-class hosts); write-back to any host system prohibited by default (rule 19) |
| Language | English v1 |

---

# 3. Asset Model & Taxonomy

Canonical classes configured in this pack (each with template PM programs, failure modes, and component trees):

## 3.1 Charging units

| Class | Config notes |
|---|---|
| **MMU** (mobile manufacturing unit, ~20 t class) | Treat as *vehicle + process skid* composite: chassis/drive line follows the road-fleet register logic (§5); the payload module (emulsion tank, AN prill tank, sensitizer system, pumps, hoses/reels, auger, PLC dosing controls, metering) follows process-equipment logic. Component tree keyed by serial number (pump, hose reel, flow meter, load cells). QC stream ingestion: density/viscosity tests per charge become structured condition records tied to the metering/pump components |
| **MCU** (mobile charging unit, underground) | Smaller skid/trailer-mounted pumping units; duty-cycle-hour-based component lives; confined to underground zones — location model uses mine levels/portals |
| **PCU** (portable charging unit) | Man-portable; high manual-handling damage class; kit-level checkouts rather than vehicle PM |
| **RRS / re-pump units** (rapid re-loaders) | High-throughput transfer duty; pump seals/valves/meters on accelerated wear curves |

## 3.2 Transfer & delivery chain

| Class | Config notes |
|---|---|
| **Road tankers** (dedicated emulsion tankers) | Dual-register assets: road-fleet statutory (§5) + product-transfer integrity (hose burst history, valve seals, bottom-loading adaptors, metering) |
| **Fixed transfer pumps** (silo offload, recirculation, EVDS feed) | Progressive-cavity/gear pump templates; seal/hose wear models driven by run-hours from edge sensors or operator logs where instrumentation absent |
| **EVDS strings** (vertical drop reticulation) | Modeled as linear assets with station nodes (surface tank → piping string → UG receiving station → valves/instrumentation); pressure/integrity checks as statutory-style inspections |

## 3.3 Storage facilities

| Class | Config notes |
|---|---|
| **Emulsion silos** (site-based) | Inventory reconciliation feeds (level instruments/manual dips), containment checks, agitator/heating elements where fitted, condition of valves and fittings |
| **Licensed magazines** (detonators/cartridge product) | Licence-bound objects: every magazine record carries its Explosives Act licence number, permitted quantities/classes, expiry, inspection cadence (see §6 Register C) |
| **Bulk plant equipment** [conditional] | If/when the in-country manufacturing plant is confirmed active: reactors/mixers, day tanks, loading bays, laboratory QC instruments — governed additionally by Register B (§6) |
| **Surface/UG EVDS receiving stations** | Tank + valve + instrumentation bundles at each mining level |

**Failure-mode library seed (pack ships with priors; refined by Federated Learning over time):** pump seal leakage → emulsion spill/loss of prime; hose fatigue/burst at reels; meter drift → billing + blast-quality errors; crystallization/settling blockages in lines during idle periods; sensitizer dosing deviation; PLC/communication faults on smart-MMU modules; tanker offload coupling wear; silo valve seizure; corrosion under insulation on fixed lines.

---

# 4. Location Hierarchy & Site Registry

```
Zimbabwe BU
├── Harare Head Office & Regional Workshop        [owned premises]
├── Bulk Emulsion Plant (Kwekwe-area)             [PENDING CONTEXT — activate Register B if confirmed]
├── Zimplats – Ngezi Mining Division              [host-owned site, AECI-resident team]
│   ├── Open-pit remnant operations
│   ├── Bimha / Mupani / Mupfuti / Rukodzi / Ngwarati portals
│   ├── UG emulsion storage & reticulation stations
│   └── Ngezi Concentrator vicinity staging
├── Eureka Mine (Guruve)                          [customer site, surface]
├── Lithium belt deployments                      [PENDING CONTEXT — Bikita/Arcadia/Kamativi as confirmed]
├── Midlands deployments (Unki/Shurugwi area)     [PENDING CONTEXT — VDS status confirmation]
└── Distributor network touchpoints               [stock-only visibility, no maintenance scope v1]
```

Site object attributes include: host-customer name, hazardous-area classification map (zones around charging/storage activities), connectivity class (LTE/VSAT/offline), travel distance from Harare workshop, applicable statutory overlays (mine-site regulations + explosives regs + road regs at gates).

---

# 5. Register A — Road Fleet Statutory Compliance (VID / ZINARA / Insurance)

**Legal basis (desk-verified):** Vehicle Registration and Licensing Act [Chapter 13:14]; Vehicle Registration & Licensing Regulations SI 427/1999 as amended (incl. SI 2024-067 fee schedule); Road Traffic Act [Chapter 13:11] (heavy vehicle = >2,300 kg nett mass); VID Certificate of Fitness regime for commercial/heavy vehicles (annual); ZINARA licensing administered via registering officers (ZIMPOST agency); mandatory third-party insurance; speed monitoring + limiting devices mandatory ≥4,600 kg NVM.

Every road-going asset (MMUs, tankers, crew buses, LDVs, trailers ≥551 kg) carries a **fleet-compliance passport** with these tracked credentials:

| Credential item | Issuing authority | Cadence | DDE behavior |
|---|---|---|---|
| Certificate of Fitness (COF) | VID (Vehicle Inspection Department) | Annual (commercial vehicles) | Expiry countdown; renewal job auto-created 45 days out; **operational gate**: expired COF ⇒ vehicle flagged not-for-road-use, work assigned only within site boundaries |
| Vehicle licence disk | ZINARA (via registering officer) | Annual (mass-class tariffed) | Expiry tracking; renewal task includes document checklist (registration book, valid insurance, current COF — all prerequisites pulled from DDE records) |
| Third-party insurance | Insurer | Annual | Expiry tracking; hard gate on dispatch if lapsed |
| Speed governor / monitoring device certification | Approved fitment centre | On fitment + periodic verification | Certificate on file; verification task annually; applies to all units ≥4,600 kg NVM (all MMUs/tankers qualify) |
| Registration book / gross mass certificate | CVR (Central Vehicle Registry) | Point-in-time + change events | Document store; change-of-details workflow |
| Driver competency linkage | VID/licensing authority | Per driver | Job-dispatch eligibility: Class requirements matched to vehicle class; professional-driver status tracked |

**Pack-specific rules:**
- COF/ZINARA renewals are modeled as **maintenance jobs with evidence capture** (photo of disk, stamped COF) feeding the compliance wallboard — one system answers "is any unit illegal on the road today?"
- Trailer population (light ≤550 kg vs heavy >550 kg classification) captured at asset creation to avoid silent misclassification fines.
- Fuel/mileage ingestion (manual or telematics) drives both service-interval engines and COF-supporting usage records.
- **[PENDING CONTEXT]:** whether AECI subscribes to a fleet-management/telematics provider whose API should be the ingestion path (vs gateway retrofit on older units).

---

# 6. Register Set — Explosives-Specific Statutory Compliance

## Register B — Manufacturing Licence (Ministry of Mines)

**Legal basis:** Explosives Act [Chapter 10:08] empowers ministerial regulation of the conditions under which explosives may be manufactured; manufacture requires ministry authorization/licence with attached conditions. Applies to the in-country bulk emulsion plant operation (and, contractually relevant, to MMU on-bench mixing practices which are themselves "manufacture" events under the two-component doctrine).

Tracked objects:

| Object | Content | Gates/alerts |
|---|---|---|
| Manufacturing licence | Licence number, issuing ministry office, licensed activities (bulk emulsion manufacture/loading), premises boundary, authorised capacity, issue/expiry dates | T-120/T-90/T-60 expiry ladder (long-lead government renewal); expired ⇒ plant production tasks frozen pending legal review flag |
| Licence conditions schedule | Each condition as a discrete obligation record (quantity limits, storage co-location rules, reporting duties, inspection access) | Condition-level compliance checklist with periodic attestation tasks; breaches logged as incidents |
| Plant inspection evidence | Ministry/third-party inspection reports, corrective-action tracking | Inspection-due scheduler; CAPA closure linked to WOs |
| QC/calibration records | Daily pH/viscosity/density testing at plant; instrument calibration chains (lab instruments, MMU meters) | Calibration-before-use gating on GMP-style logic repurposed from Pharma Pack mechanics; out-of-tolerance impact reconstruction ("which charges used this meter since last good calibration?") |
| Associated environmental/OSH overlays | EMA obligations for the plant; NSSA registration; SI 109/1990 duties at the plant as an industrial workplace | Carried in Register D/E below |

**[PENDING CONTEXT]:** exact licence class/number, conditions schedule copy, whether manufacture currently occurs in-country or solely at MMU level from imported base emulsion.

## Register C — Storage Licences (Explosives Act + SI 72/1989)

Per-magazine/per-silo records: licence number, permitted explosive classes and maximum quantities, construction/approval plans on file, separation distances, fencing/locking/security arrangements, inspection cadence, deterioration/shelf-life tracking, destruction/disposal event records, loss/theft detection records (stock reconciliation between deliveries, consumption, silo levels).

Alert semantics: licence expiry ladder; quantity-limit proximity warnings when live inventory (silo monitoring feed) approaches licensed maxima; overdue-inspection escalation to regional manager level.

## Register D — Mine Safety Obligations (SI 109/1990 + NSSA)

Carried from the market-entry pack's Zimbabwe template: FBL/MBL-type competency appointments for supervising persons, PPE issue records, accident/near-miss timelines, NSSA contributions/inspections — applied to AECI staff embedded at customer sites and at own premises.

## Register E — Platform-Side (DDE obligations, not customer-visible registers)

POTRAZ processor-contract posture, 24-hour breach workflow support, USD annual-prepay billing, SDN screening — per market-entry research §§3–4. Listed here so the pack manifest carries its own compliance metadata.

---

# 7. Integration With Existing Security Systems (Coexistence Layer)

Per user direction, DDE sits **in addition to** AECI's subscribed security systems — it does not replace them. The pack defines a security-events ingestion and correlation layer:

| Existing system (typical for this profile) | DDE integration posture |
|---|---|
| Magazine/site security (guards, CCTV, access control, intrusion alarms) | Event subscription where APIs exist (door events, arm/disarm, tamper) → mapped to asset security-state timeline on magazine records; unexplained access outside scheduled servicing windows raises a review flag correlating with stock reconciliation |
| Group supply-chain portal (track-and-trace, PoD, silo monitoring) | Read-path ingestion of silo levels and movement events → inventory reconciliation engine (Register C loss/theft detection) + consumption-vs-blast-plan variance signals |
| Host-mine permit-to-work systems (e.g., Zimplats SAP-based permits) | Technician job packs carry a **permit reference field** (offline-readable); DDE never asserts a permit exists (rule: software state ≠ physical safety state) — it records the host permit ID and expiry shown to the technician, enforced at dispatch as a completeness check |
| Group SHEQ incident management | Bidirectional option: incident IDs referenced from DDE events; DDE-generated near-miss/equipment-event records exportable in group format |
| Blast initiation ecosystem (IntelliShot/BlastHub side) | Out of maintenance scope; blast-schedule *dates* may be consumed read-only to power readiness-gate timing (equipment availability assurance before windows) |

Correlation value proposition: no single subscribed system answers "was this magazine accessed, was stock reconciled, was the pump that failed recently serviced, and was the vehicle legal on that date?" — DDE's canonical graph joins them.

**[PENDING CONTEXT]:** named vendor list of AECI's actual subscribed security systems and available APIs/API costs.

---

# 8. Core Workflow Configuration

## 8.1 Technician execution (Field Experience layer, glove-friendly tablet/kiosk)

- **Daily start-of-shift readiness check** per site: charging-unit walkaround (fluids, hose condition, meter zero-check), pump prime checks, silo/valve visual + level log, vehicle documents spot-card (COF disk, licence disk, insurance, governor cert visible on screen).
- **Job packs:** offline-first; each task card carries SOP steps, torque/pressure values, photo/video evidence prompts, consumable scan-out, and signature wrap (identity + intent + hash binding per master plan §15.10).
- **Underground variant (Ngezi):** level-aware location picking; low-bandwidth sync profile; permit-reference enforcement; MCU component hour-log capture at point of work.
- **Breakdown response:** guided troubleshooting seeded by failure-mode library; "blast window risk" banner when the affected asset has scheduled charge support within 72 h — routes priority accordingly.

## 8.2 Planning & scheduling

- PM program templates per asset class (run-hour, calendar, and condition-triggered mixes); duty-cycle weighting for pumps/hoses.
- **Readiness gate:** composite asset-readiness score per site combining PM currency, open defects, statutory credential validity (COF/licence/insurance/governor), and spares availability for known wear items → displayed against upcoming blast schedule.
- Stores intelligence: wear-parts kits (seal kits, hose assemblies, meters, filters) with min/max per site; lead-time modeling on SA supply corridor.

## 8.3 Compliance operations

- Renewal calendar wallboard across Registers A–D (single pane: every expiring credential nationally, color-coded urgency, owner assignment).
- Evidence-pack generator: one-click inspector/audit bundle (licence copies + inspection histories + servicing evidence + QC records for any asset or magazine).
- Incident hooks: equipment-involved events auto-create investigation shells with SI 109-aligned timelines.

---

# 9. Role Dashboards

| Role | Surface(s) | Key content |
|---|---|---|
| Technician | Kiosk/tablet app | Assigned packs, asset passports, credential spot-cards, offline queue health |
| Site supervisor / foreman | Supervisor app | Crew dispatch, stuck-board, permit completeness, daily readiness sign-off |
| Regional manager (Harare) | Web console | Multi-site readiness heat map, renewal calendar, bad-actor list, SLA/KPI scorecard (feeds AECI's contractual KPI defence) |
| MD / group visitors | Executive wallboard | National uptime, compliance posture (all registers green?), cost-per-delivered-tonne-of-emulsion trend |
| DDE implementation pod | Admin | Manifest/config promotion, connector health, data-quality engine |

---

# 10. Economics Configuration (§8 Profiler inputs)

Cost-of-failure model tuned to this business: **missed/slid blast window** as the primary consequence unit (customer SLA exposure, demobilization costs, rescheduling knock-ons), secondary: product loss (spills), regulatory penalty exposure (expired credentials operating on road = fines/grounding; licence-condition breach = existential), recovery costs (vehicle recovery from remote pits). Baseline measurement protocol captures current downtime frequency/causes during pre-pilot weeks. All economics carry lineage + confidence per rule 16.

**[PENDING CONTEXT]:** internal cost figures, SLA penalty structures, historical breakdown data sample.

---

# 11. Data Acquisition Plan

1. **Manual-first (week 1):** structured operator logs (hour meters, dip readings, walkarounds) via tablet — instant value, zero install risk.
2. **Document ingestion:** existing PDF checklists/service sheets through the PDF Conversion Engine into governed digital forms; Excel PM schedules migrated via import wizard.
3. **Sensor/telemetry wave (weeks 4+):** silo-level feeds (portal API or local sensor), MMU smart-module data where API-accessible, aftermarket CAN gateway fallback for older units, simple edge counters on fixed transfer pumps.
4. **Security-event subscription** per §7 once vendor inventory confirmed.

---

# 12. Sequencing & Pilot Shape (aligned to master plan §14.5)

| Step | Content | Exit criteria |
|---|---|---|
| 0. Foundation | Tenant provisioning, branding, asset registry build (workshop data-audit sprint with technicians), register setup with real licence documents | 100% asset census signed off; all live licences loaded |
| 1. Execute | Manual logs + job packs live at 1 anchor site + Harare workshop | ≥80% PM completion-in-window; technician adoption stable |
| 2. Expand | Remaining sites onboarded; document engine converting legacy paperwork; renewal calendar national | Zero missed statutory renewals post-go-live |
| 3. Instrument | Telemetry/silo feeds; predictive pilots on pump seals & hose life | ≥1 validated early-warning with precision SLO met |
| 4. Convert | Production rollout quote per pre-agreed conversion mechanism | Conversion decision recorded |

Pilot pricing/commercial rails: USD annual-prepay, Nostro invoicing, SDN screening, POTRAZ processing contract — carried from the commercial model without modification.

---

# 13. Open Items Awaiting User Context (**[PENDING CONTEXT]** consolidated)

1. Named security-system vendors AECI subscribes to (magazine security, fleet telematics, silo monitoring) + API availability.
2. Actual site list & resident-team rosters; lithium-belt contract confirmations.
3. Bulk plant status and manufacturing licence particulars (number, conditions, expiry).
4. Fleet composition: counts of MMUs/tankers/MCUs/LDVs/trailers; ages; governor fitment status.
5. Current maintenance system of record (group ERP? spreadsheets?) and any group IT constraints from Sandton.
6. Historical breakdown/QC data samples for baseline and failure-mode tuning.
7. Host-mine permit formats (Zimplats) for offline permit-reference design.
8. Hazardous-area classifications per site for device policy (Zone 1/21 + mining Group I certified hardware selection from the rugged matrix).

*This specification will be revised to v1.1 as that context arrives.*
