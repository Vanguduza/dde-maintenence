# DDE — Zimbabwe Market Entry Research (Planning-Phase Evidence Pack)

**Document status:** Desk-research assessment of Zimbabwe as the first reference market for the DDE Asset Operations Intelligence Platform. Companion to `DDE_Maintenance_Intelligence_ERP_Master_Plan_v2.md` and `DDE_Industry_Simulation_Research.md`.
**Date:** 22 August 2026
**Method:** Targeted web research across mining-sector trade press (Mining Weekly, Mining Zimbabwe, Equity Axis, SMM), primary legal sources (POTRAZ regulations SI 155/2024; Mines and Minerals Act framework; Auditor-General report), central-bank statements (RBZ 2026), utility and infrastructure reporting (ZESA parliamentary evidence, 2026), and government enforcement reporting. Evidence grades assigned per section; limitations in §9.

---

# 1. Why Zimbabwe, and What Question This Answers

Zimbabwe is a plausible first reference market: the user's operating context is Zimbabwean, the mining sector is in a capital-investment boom, the fleet-heavy equipment profile matches DDE's J1939/CAN-FD DNA, and English-language operations reduce localization cost. But plausibility is not viability. This document answers four questions the master plan requires before naming any first market: (1) is there a reachable buyer with money and a maintenance problem? (2) can a foreign SaaS lawfully sell and get paid there? (3) does the operating environment (power, connectivity, skills) break the product's assumptions? (4) does the compliance framework extend cleanly? Each answer is graded, and §8 states what changed in the master plan as a result.

**Headline verdict:** Zimbabwe is a **viable first reference market with a specific, evidence-backed entry profile** — but only via a two-tier strategy (large formal miners as lighthouse customers; mid-tier and Chinese-operated miners reached through partners), with USD pricing, offline-first as a hard requirement, and a compliance addendum covering POTRAZ data-controller licensing, SI 109/1990 safety regulations, and NSSA obligations. It is a beachhead for proof, not for revenue scale; the revenue-scale market remains the broader SADC region.

# 2. The Mining Sector: Scale, Buyers, and Equipment Reality

**Evidence grade: B+ (multiple independent trade sources, 2025–2026, directionally consistent).**

## 2.1 Sector scale and trajectory

- Mining = **~14.5% of GDP, ~80% of export earnings, ~19% of government revenue**; sector grew 7% in 2025 with ~10% projected for 2026. Mineral exports: $5.9B (2024) → $6.2B (2025) est.; **$5.73B in H1 2026 alone**, tracking toward a $3.5B+ second half. Long-run projection to $21B if projects complete.
- **Lithium boom is the growth engine:** Zimbabwe is Africa's leading lithium producer; Chinese firms (Zhejiang Huayou Cobalt — Arcadia; Sinomine — Bikita; Sichuan Yahua — Kamativi) control >80% of lithium production and have invested ~$2B since 2021, with $1.45B more committed to beneficiation plants. Government policy (Critical Minerals Declaration, 22 May 2026; NDS2) mandates in-country beneficiation — concentrate exports phase out by January 2027 — locking in multi-year plant construction and commissioning activity.
- **PGM expansion:** Zimplats (Impala Platinum subsidiary) has invested >$750M in expansion/beneficiation/energy; Phase 3 underground expansion at Ngezi adds a **new fleet of 28 Sandvik underground units**; Mimosa investing >$200M; smelting capacity tripled to 380kt/yr; $190M Base Metal Refinery revival.
- **Equipment imports are surging:** April 2026 alone: $23.2M tunnelling machinery + $17.2M earthmoving equipment. New $3.52B in mining licences issued since 2023.

## 2.2 Buyer segmentation (who actually buys maintenance software)

| Tier | Examples | EAM/CMMS state | DDE fit |
|---|---|---|---|
| **Tier 1 — Major formal miners** | Zimplats, Mimosa, Unki (Anglo), RioZim, Kuvimba (Great Dyke) | SAP or Maximo estates, corporate IT from SA parents, established reliability teams | Mode A overlay on existing SAP/Maximo; slow procurement but referenceable; Zimplats' new Sandvik fleet = concrete telematics + maintenance-intelligence use case |
| **Tier 2 — Mid-tier and junior miners** | Caledonia (Blanket Mine), Prospect Lithium Zimbabwe, Bikita Minerals, Kamativi | Partial or no CMMS; spreadsheets + paper; fast-growing fleets with young maintenance systems | **Primary DDE target:** greenfield maintenance digitalization; faster decisions (site GM authority); Chinese owners demand cost efficiency |
| **Tier 3 — Chinese-operated lithium/chrome operations** | Huayou, Sinomine, Sichuan Yahua sites; numerous chrome operators | Minimal formal systems; equipment dominated by **SANY, XCMG, Shantui, LiuGong** (J1939-standard but Chinese OEM telematics ecosystems) | Reachable only via partners (see §2.3); price-sensitive; strong fit for aftermarket-gateway data path |
| **Tier 4 — Artisanal/small-scale** | Thousands of small gold operations | None | Not addressable now; ignore for planning |

## 2.3 Equipment and data-access reality

- Fleet mix is bifurcated: Tier 1 runs Sandvik/Epiroc/CAT with established OEM telematics (Sandvik OptiMine, Epiroc); Tiers 2–3 run Chinese OEMs whose telematics ecosystems are closed or poorly integrated with Western platforms — **the aftermarket CAN gateway path (master plan §17.11 Path 2) is not just the default but effectively the only path for Tier 3**.
- J1939 compliance on Chinese equipment is generally good at the engine/powertrain layer (common with Cummins/Weichai/Deutz engines), making gateway-based ingestion feasible; proprietary body/attachment electronics vary.
- Spares supply chains run through South Africa (and directly from China for Chinese OEMs), making stock-out risk and lead-time variability severe — exactly the stores-intelligence problem DDE models.

## 2.4 Maintenance pain signals (documented)

- Ministerial public criticism of **unqualified foreign mine managers** (June 2026: managers appointed without First Blasting Licence/Mine Blasting Licence competency), unsafe tailings dams, unsecured open pits — with a **$2M national safety enforcement blitz**, new district mining officers, and inspector vehicles pledged. Enforcement intensity is rising from a low base.
- Auditor-General report on mining OSH: of 51 mines inspected, **73% had workers with inadequate PPE**; inspector capacity chronically limited; accident investigation timelines (24h for fatals under SI 109/1990 s.269) often unmet.
- Practical implication: safety-compliance pressure is a **growing but immature** demand driver — buyers may not yet pay for safety software voluntarily, but enforcement risk is rising, and DDE's statutory-register engine (inspection certificates, manager competency tracking, accident reporting timelines) maps directly onto SI 109/1990 duties.

# 3. Legal & Compliance Environment

**Evidence grade: A− (primary legal sources read directly).**

## 3.1 Data protection — Cyber and Data Protection Act [Chapter 12:07] (2021) + SI 155/2024

- **POTRAZ is the Data Protection Authority.** Licensing regime in force since 12 Sep 2024: any entity processing personal data of **50+ data subjects** must register; commercial-scale controllers must obtain a **data controller licence** (tiered 1–4 by data-subject count, annual renewal, fees per Second Schedule). Unlicensed processing is a criminal offence: fine up to level 11 and/or **up to 7 years' imprisonment**.
- **Mandatory DPO** for licensed controllers (deadline was 12 Dec 2024).
- **Breach notification within 24 hours to POTRAZ** — described by trackers as the tightest deadline on the continent.
- **Cross-border transfers restricted** — authorisation/adequacy conditions apply; no blanket localisation mandate, but POTRAZ holds transfer-regulation authority.
- **DDE obligations:** DDE (as processor) must sign POTRAZ-compliant processing contracts with each Zimbabwean customer (controller); customer-facing materials must support the customer's licensing, DPO and 24-hour breach workflow; a Zimbabwe data-residency option (hosting in South Africa at minimum, with transfer authorisation analysis) should be productized; workforce analytics module (§11) inherits the same licensing logic.

## 3.2 Mining safety law — Mines and Minerals Act [Chapter 21:05] + Mining (Management and Safety) Regulations, SI 109/1990

- SI 109/1990 is the operational core: mine manager competency and appointment (FBL/MBL), PPE duties (ss.47–48), accident reporting and investigation timelines (s.269: fatal accidents reported to inspector and police without delay; investigations within 24h), inspection regimes by the Ministry of Mines' Inspectorate.
- **DDE obligations:** the statutory-register engine (master plan §15.6) needs a **Zimbabwe jurisdiction template**: manager competency/certificate tracking (FBL/MBL), PPE issue records, accident/near-miss reporting with SI 109 timelines, ventilation/dust monitoring registers (Pneumoconiosis Act medical certificates with expiry — fits the competency/expiry engine directly).
- NSSA (Accident Prevention and Workers Compensation Scheme) adds employer registration, contribution records, and workplace inspection duties (5,059 national workplace inspections Jan–Sep 2025; 217 in mining) — NSSA inspection findings are another evidence surface DDE can help customers answer.
- Pneumoconiosis Act: periodic medical fitness certificates for mining workers — expiry tracking fits DDE competency module out of the box.

## 3.3 Other legal surfaces

- **E-signatures:** Zimbabwe's Electronic Transactions and Electronic Commerce Act framework gives legal effect to electronic records/signatures (with exclusions); permit/isolation sign-offs should default to strong (attribution-capable) signature flows; counsel confirmation required before relying on e-signatures for statutory records.
- **Labour Act [Chapter 28:01]:** works-council/worker-consultation culture exists; the §11 workforce governance default-off posture applies cleanly.
- **Sanctions/OFAC:** Zimbabwe is under US targeted sanctions (specific designated persons/entities, incl. some mining-adjacent SDNs) rather than comprehensive country sanctions — but **over-compliance by US cloud/payment providers is real** (payment rails and SaaS platforms occasionally block Zimbabwe-linked transactions). DDE must screen customers against SDN lists and choose payment/hosting infrastructure resilient to over-compliance (see §4).

# 4. Economic & Payment Environment

**Evidence grade: B+ (RBZ statements and financial press, 2026).**

- **Deep dollarisation persists:** >80% of transactions and deposits in USD; ZiG (introduced April 2024) is stable but conditions-based de-dollarisation has no fixed date (2030 statutory deadline exists but RBZ publicly abandoned time-binding). Exporters receive 30% of earnings in ZiG; small-scale gold miners 90/10 USD/ZiG.
- **Pricing implication (binding):** DDE must price in USD, contract in USD, and accept USD payment rails. ZiG-denominated pricing would create instant credibility damage given 2023–24 memory of ZWL collapse.
- **Payment mechanics:** international card rails and SWIFT work but are unreliable for recurring SaaS billing (forex allocation queues, RBZ prioritisation of fuel/medicine/raw materials, occasional bank over-compliance with sanctions). **Practical mechanisms used by existing SaaS vendors in Zimbabwe: annual upfront invoicing (not monthly card billing), USD Nostro-account invoicing, regional reseller/partner of record (South African entity), and mobile-money/interbank transfer reconciliation.** DDE billing must support: annual prepay default, invoice-based USD settlement to a Nostro account, and a reseller-of-record option.
- **Government/State-linked customers:** documented arrears to contractors — avoid public-sector-dependent revenue models; private miners pay in export USD.

# 5. Infrastructure Environment

**Evidence grade: B (utility/telecom reporting, 2026).**

- **Power:** ZESA reports 138–188 consecutive days without nationwide load-shedding (as of mid-2026), aided by a $210M Afreximbank facility for SAPP power trading; 1,365MW new capacity targeted by December (635MW under private construction). But dependable capacity (1,200–1,600MW) still runs below ~2,000MW peak demand; a single 330kV line fault (Warren-Alaska, 6 July 2026) severed regional interconnection for ~4 hours. **Planning stance: assume daily outages are possible at any site; grid recovery ≠ uptime.**
- **Connectivity:** >70,000km national fibre, 400+ 5G towers, growing cross-border corridors (Powertel–Paratus Plumtree–Bulawayo phase). Urban/industrial fibre is good by regional standards; **remote mine sites still depend on LTE/VSAT with real outage frequency.** Mobile money (EcoCash etc.) is ubiquitous for payments.
- **Implication:** the offline-first architecture (master plan §13) is not a differentiator in Zimbabwe — it is the entry ticket. Edge buffering at site level (§27 of v1) matters for sensor continuity during both power and connectivity gaps; tablet battery + solar charging assumptions belong in field-deployment specs.

# 6. Competitive Reality in Zimbabwe

**Evidence grade: C+ (inference from regional market structure; no direct Zimbabwe-specific competitive research found — flagged as a gap).**

- Tier 1 miners inherit corporate standards from South African/Japanese/Australian parents (SAP PM, Maximo, Pronto Xi — Pronto is notably common in mid-tier African mining via the RIB/Softtech channel).
- Regional SaaS CMMS presence (Fiix, Limble, UpKeep) exists but with thin local support; **no evidence of an AI-maintenance incumbent with Zimbabwe field presence.** The realistic competition is: (a) spreadsheets + paper, (b) Pronto/legacy local systems, (c) South African consultancies doing bespoke dashboards (Power BI over spreadsheets).
- **Chinese OEM ecosystems (SANY OptSy, XCMG XCMG-Cloud etc.)** provide telematics portals for Tier 3 fleets but no CMMS/maintenance-intelligence layer — coexistence rather than competition.
- Gap to close with groundwork: a named-account mapping of the top 30 Zimbabwe mining operations' current EAM state (only physical groundwork can settle this).

# 7. Skills, Labour & Change Environment

- Strong mining engineering tradition (University of Zimbabwe Mining Engineering; Zimbabwe School of Mines; large Zimbabwean diaspora in regional mining returns with modern-systems exposure).
- **1.5 Million Coders national digital-skills program** and growing local ICT services sector mean local implementation talent is hireable — supports a Harare-based implementation/support pod (cost advantage vs SA for support-tier roles).
- Change-management reality from the Industry Simulation (30–40% technician reversion risk) is amplified where maintenance records culture is paper-based; the maintenance-champion clause (§14.5) and technician-co-design are *more* important here, not less.
- Language: English is the business language — no localization cost for v1. Shona/Ndebele voice interfaces are a future differentiator, not a launch requirement.

# 8. What Changed in the Master Plan (see also §19 evidence base)

1. **§14.2 beachhead:** Zimbabwe named as candidate first reference market within the mobile-fleet beachhead, with the two-tier entry strategy (§2.2 above) and explicit "proof market, not revenue market" framing; SADC expansion path (Zambia, Botswana, SA) follows.
2. **§14.1 billing:** USD annual-prepay default, Nostro invoicing, reseller-of-record option added to billing requirements.
3. **§15 compliance:** Zimbabwe addendum — POTRAZ controller-licensing support obligations, 24h breach workflow support, cross-border transfer analysis, SI 109/1990 statutory template (FBL/MBL competency, PPE, accident timelines), Pneumoconiosis certificate expiry tracking, NSSA inspection evidence, e-signature counsel confirmation, SDN screening.
4. **§17.11 fleet pack:** Chinese-OEM telematics coexistence noted; aftermarket gateway path confirmed as the only viable path for Tier 3; Chinese OEM portal integration added to connector backlog (not MVP).
5. **§13/edge:** power-outage resilience (site edge buffering, tablet charging) elevated from "nice" to required in Zimbabwe deployment spec.
6. **§16 Phase 1 pilot design:** pilot target profile defined as a Tier 2 lithium or gold operation (50–200 mobile units, greenfield maintenance digitalization) with Zimplats-class Tier 1 as the lighthouse overlay conversation running in parallel.

# 9. Limitations & What Only Groundwork in Zimbabwe Can Settle

- No Zimbabwe-specific competitive intelligence was found (grade C+ section); named-account EAM mapping, incumbent-consultant landscape and pricing sensitivity require on-the-ground discovery.
- POTRAZ licensing practice (fees, transfer-authorisation processing times) is young and unpublished; requires local counsel engagement.
- Actual willingness of Chinese-operated miners to adopt third-party software (and their group-IT approval chains, which often sit in China) is unknowable from desk research.
- Real OEM telematics API terms for Sandvik/Epiroc/CAT and Chinese OEMs in the Zimbabwe context need commercial confirmation.
- Payment-rail reliability for specific banks requires transaction-level testing.
