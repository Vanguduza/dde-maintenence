# DDE — Field Experience & Rugged Hardware Specification

**Document status:** Companion specification to `DDE_Maintenance_Intelligence_ERP_Master_Plan_v2.md` (§17.23–§17.26, §17.29). Defines the role-specific field applications (technician kiosk/tablet app, supervisor/manager apps, web/desktop console), the dashboard design system for each role, and the certified rugged hardware matrix — devices and carry/mount systems that survive falls, spills, dust, vibration and hazardous zones; plus the client-side rendering of digital forms on converted client documents (§12).
**Date:** 22 August 2026
**Research basis (Aug 2026):** MIL-STD-810H / IP66–68 rugged tablet landscape (Panasonic Toughbook FZ-G2, Getac F110 G6/ZX10 G2/ZX80W, Zebra ET60/ET65, Dell Pro Rugged 10/12); Chinese rugged tablets with unlocked bootloaders for ROM customization (DOOGEE R10/R20, Ulefone Armor Pad Pro, Blackview Active 8 Pro, Oukitel RT3 Plus/RT7, Unihertz/8849 Tank 2 Pro, Hotwav R6 Pro — verified model names and purchase links Aug 2026); intrinsically-safe devices (Aegex100M Zone 0/1, i.safe MOBILE IS940.1 Zone 1/21, IS945.M1 mining Group I, Ecom Tab-Ex 05 DZ1, Getac ZX80W-EX Zone 2/22); mounting/carry ecosystems (Gamber-Johnson vehicle docks with magnet-mount attachments and one-hand docking; InfoCase harness/holster/hand-strap cases); CMMS/mobile dashboard UX research (glove-rated touch targets ≥44px, single-column mobile layouts, stale-while-revalidate offline patterns, 5–8 metric role dashboards); Android kiosk hardening techniques (COSU/device owner mode, custom ROMs with no-boot-flash techniques); tech-expert module enhancements (AI-native predictive maintenance, digital twins, workflow automation, agentic AI).

---

# 1. Design Doctrine: One Platform, Four Surfaces

DDE renders through four purpose-built surfaces on one codebase (per §17.22 modularity). Each surface answers one primary question:

| Surface | Primary user | The question it answers in 15 seconds |
|---|---|---|
| **Tech Kiosk App** (rugged tablet/handheld) | Field technician | "What is my next safe job and what do I need to do it?" |
| **Supervisor App** (tablet + phone) | Maintenance supervisor / foreman | "Who and what is stuck right now?" |
| **Manager Console** (web/desktop) | Planner, reliability engineer, manager | "Where is the risk and what do I commit resources against?" |
| **Executive View** (web + wallboard) | Plant/site leadership, Boardroom (v1 §50) | "Are we winning or losing on availability and cost?" |

Non-negotiable inheritance from the master plan: all surfaces are offline-first (§13), evidence-capturing, safety-gated, and render inside customer branding tokens (§17.22). A metric without lineage never displays (rule 16); an alert below precision SLO never reaches a surface (rule 17).

# 2. Tech Kiosk App (Field Technician)

## 2.1 Interaction constraints that drive every decision
Designed for gloves (mining/construction/food-hygiene), bright sun, noise, one-handed operation at height, and zero connectivity. Therefore: touch targets ≥48px with 8–12px spacing (glove-rated capacitive screens verified during device selection); high-contrast themes (WCAG 2.2 AA minimum, target AAA contrast for outdoor text); voice-to-text for failure descriptions feeding WO Text Intelligence (§17.12); NFC tap-to-identify assets (tap the asset tag to open its job pack — no menu navigation); QR/barcode fallback via integrated imagers; programmable hardware buttons mapped to SOS/lone-worker and "evidence snapshot."

## 2.2 Kiosk mode & assignment
Shared-device model common on sites: the tablet lives in a charging cradle at the shift-start point or workshop entrance. Technician taps badge/NFC → personal profile loads (assignments, competencies, open jobs). Device-lockdown kiosk shell prevents app escape; session auto-locks when badge is removed. Personal-device mode supported where technicians carry their own phones.

## 2.3 Dashboard structure — "My Day" (single column, thumb-reachable)
```
┌──────────────────────────────────────┐
│ SAFE-JOB BANNER (site alerts, active │  ← cannot be dismissed while a
│ permits held by me, weather hold)    │    relevant permit/iso is open
├──────────────────────────────────────┤
│ MY NEXT JOB card: asset, priority,   │  ← one tap opens full job pack
│ location, parts-kitted ✓, permit ✓   │
├──────────────────────────────────────┤
│ TODAY list (5–8 rows max): status    │  ← overdue glows amber/red;
│ chips, swipe → defer w/ reason       │    deferral requires reason code
├──────────────────────────────────────┤
│ ALERTS FOR MY ASSETS (SLO-passed     │  ← silent otherwise (§10)
│ only): acknowledge → convert to job  │
├──────────────────────────────────────┤
│ REQUESTS: raise new fault (voice) ·  │
│ stores pickup ready · my sign-offs   │
└──────────────────────────────────────┘
Data-age banner when offline: "Synced 14 min ago"
```

## 2.4 Job pack execution flow (the core loop)
Open job → **safety gate first** (permit status, isolation/LOTO verification steps per approved site procedure, hazard checklist from HIRA) → guided steps with photo-evidence prompts at defined hold-points → consumables/parts scan (decrements stores in real time when online; queues op-log offline) → failure-code capture assisted by troubleshooting copilot (source-grounded suggestions only) → completion signature → automatic post-task hooks fire per vertical pack (sanitation WO in food plants §17.19; return-to-service QA in pharma §17.18; statutory certificate update in facilities §17.16). Completed WO ≠ successful repair — follow-up verification tasks auto-create per v1 rules.

## 2.5 Field-expert usability features (the differentiators)
- **Offline AI**: on-device copilot caches the site's procedure corpus and asset history subset nightly; works air-gapped
- **Guided isolation sequences** rendered step-by-step; photo comparison against reference images; no device interaction during hazardous work beyond the gated sequence (v1 rule)
- **Torque/spec cards** inline at the exact step needing them; zoomable exploded diagrams from the OEM library (§17.2)
- **Time-motion respect**: every screen answers one question; nothing requires typing where a scan/tap/voice note exists
- **Lone-worker integration**: programmable SOS key (verified on i.safe IS-class devices) triggers site emergency workflow

# 3. Supervisor App ("Who and what is stuck?")

## 3.1 Dashboard structure — shift-control view
```
┌─────────────────────────────────────────────────┐
│ SHIFT PULSE: crew coverage vs demand today ·    │
│ permits awaiting my approval (count → tap)      │
├─────────────────────────────────────────────────┤
│ STUCK BOARD (auto-ranked): jobs blocked on      │
│ parts / access / permit / competency — each row │
│ names THE unblocking action and owner           │
├─────────────────────────────────────────────────┤
│ CREW MAP/LIST: who is on what, since when;      │
│ Wrench-time vs travel signal (capability view)  │
├─────────────────────────────────────────────────┤
│ BREAK-IN ALERTS: emergent failures ranked by    │
│ VaR (§8) — accept into schedule w/ impact view  │
├─────────────────────────────────────────────────┤
│ APPROVAL QUEUE: isolations, deferrals, stores   │
└─────────────────────────────────────────────────┘
```
Phone layout mirrors single-column; tablet adds split-view (stuck board + detail). Every number drills to exactly one "why" screen.

## 3.2 Supervisor-only powers (governed)
Approve/decline permits and isolations with e-signature (§15.10); override deferrals *except* statutory-overdue (never overridable, §15.6); dispatch reassignment with competency check (competency-aware dispatch, Phase 2); initiate LOTO verification spot-checks.

# 4. Manager Console (web/desktop)

## 4.1 Dashboard structure — planner/reliability home
Three-column desktop layout (the only surface allowed density):
1. **Risk column:** top bad actors (Pareto), VaR-at-stake list, alert precision SLO health (§10) — trust metrics are themselves displayed so engineers see the AI's reliability
2. **Flow column:** schedule compliance, backlog aging (weeks by priority band), PM completion vs statutory due calendar
3. **Money column:** maintenance debt trend, cost-of-inaction queue (lineage-tagged), stores risk exposure
Plus: **asset health heat-map** (site → area → asset drill-down), **failure-graph explorer**, **readiness gate panel** (data-quality score per source before AI features unlock, §9).

## 4.2 Manager/expert features
Scenario modeling (defer-this-PMTA impact simulation); RCA workspace with evidence timeline replay; RCM analysis templates seeded from failure library; calibration impact reconstruction ("what else was measured with it", §17.18); audit-pack generator (statutory registers → evidence bundle export); config wizard entry (pack/manifest management per §17.22, admin-gated).

## 5. Executive View & wallboards
Five numbers maximum, each answering "winning or losing?": availability vs target, downtime cost month-to-date (lineage badge), schedule compliance, safety events, statutory compliance % (overdue count — red is possible). Wallboard mode for control rooms: read-only, auto-rotating, no interaction, data-freshness stamp. Boardroom meeting view inherits v1 §50 with these widgets as the default template.

# 6. Cross-surface design system rules
1. **One component library, tokenized** — brand tokens swap instantly (§17.22); components tested against AA contrast in both light/dark and colorblind-safe palettes
2. **Stale-while-revalidate everywhere** — cached data always renders with visible age; never a blank/error screen offline (§13 alignment)
3. **Notification discipline** — push interrupts only for SLO-passed critical alerts, permit approvals, safety recalls; everything else is badge-count. Mirrors §10 silence-is-better-than-noise
4. **Every metric tappable to one "why" screen** — no dead-end numbers
5. **90-day metric rule** — any widget that hasn't changed a decision in 90 days is flagged for removal by the analytics telemetry
6. **Accessibility** — EN 301 549/WCAG 2.2 AA conformance path (§15.11), voice output option for hands-busy/bad-light contexts, localized terminology via pack dictionary

# 7. Rugged Hardware Matrix (certified, current as Aug 2026)

## 7.1 Minimum platform requirements (any DDE field device)
IP65+ sealing (IP66/68 preferred washdown); MIL-STD-810H drop ≥1.2m certified (≥1.8m preferred); operating −20°C to +50°C minimum (−29°C cold-chain variants); sunlight-readable ≥800 nits (≥1000 preferred); glove/wet capacitive touch; hot-swappable or full-shift replaceable battery; Wi-Fi 6 + cellular (5G preferred) + GPS + NFC; integrated or accessory 1D/2D imager; MDM/enterprise enrollment (Android Enterprise / Windows Autopilot); 3-year service cycle minimum.

## 7.2 Recommended devices by environment

| Environment class | Reference devices | Why |
|---|---|---|
| **General industrial / mining surface / construction** | Getac ZX10 G2 (10.1" Android, 1000-nit LumiBond, dual hot-swap batteries, IP66, 6ft drop, optional Class I Div 2); Zebra ET60/ET65 (Android/Windows options, IP66/68, 1000+ nit glove/wet touch, hot-swap); **Chinese rugged Android tablets** (DOOGEE R10/R20, Ulefone Armor Pad Pro, Blackview Active 8 Pro, Oukitel RT3 Plus/RT7 Titan, Hotwav R6 Pro — Mediatek/Unisoc chipsets, unlocked bootloaders, IP68/IP69K, MIL-STD-810H, Android 13–15, purchase links §8.1) | Light enough for walking rounds; Android fleet-management maturity; imager options; Chinese models offer 40–60% cost advantage for ROM-customizable fleets |
| **Vehicle-mounted / heavy plant cabins** | Getac F110 G6 (11.6" Windows, dual LifeSupport hot-swap, Thunderbolt 4); Panasonic Toughbook FZ-G2 (modular expansion bays); Dell Pro Rugged 10/12 (Core Ultra, dual hot-swap, Class I Div 2); **Chinese Android vehicle docks** (Unihertz/8849 Tank 2 Pro with magnetic mount, Ulefone Power Armor 23 with holster) | Gamber-Johnson/Havis dock ecosystems, port replication, keyboard pairing; Chinese dock ecosystems provide equivalent VESA/magnet systems at lower cost |
| **Hazardous Zone 1/21 (process, refining, chemical, underground sumps)** | i.safe MOBILE IS940.1 (Android 14, 5G, Zone 1/21, IP68/MIL-810H, programmable SOS key, VESA mount); Ecom Tab-Ex 05 DZ1 (Zone 1/21 Div 1); Aegex100M (Windows, Zone 1, Zone 0 with case, UL 913) | Intrinsically-safe (Ex ia/ib) certification — the only legal option in classified areas |
| **Mining underground (Group I)** | i.safe IS945.M1 (mining-certified Group I M1/Zone 0 + Zone 1/21) | Mining-specific methane/dust certification |
| **Zone 2/22 (lower-risk hazardous fringes)** | Getac ZX80W-EX (2026, ARM/Windows, ATEX/IECEx Zone 2/22, IP67, lightweight) | Cheaper than Zone 1 kit where zoning allows |
| **Technician pocket tier** | Rugged smartphone class (Zebra TC-series-style handhelds) with same app in phone layout; **Chinese rugged smartphones** (Ulefone Power Armor 23, Blackview BV9300) | Scan-first quick jobs, DVIR-style checks |

Procurement rule: zone classification of the work area decides the device tier — the Safety module flags assets/areas whose zone class requires Ex-certified hardware, and the app refuses sign-in to non-certified devices inside those geofenced areas (enforced, logged).

## 7.3 Carry & mount systems (the ease-of-use layer)
- **Hand-strap + kickstand cases** (InfoCase-class): integrated elastic hand strap, friction kickstand, corner anchor points — the default carry for walking rounds
- **Shoulder harness / holster carriers**: hands-free transport between jobs; quick-release for climb/ladder work
- **Magnetic mount attachments**: stick-to-steel placement at the actual workface (panel, machine frame, vehicle body) — verified available across the Dell/Getac dock ecosystems; magnet rating specified per device SKU
- **Vehicle docks** (Gamber-Johnson/Havis, e-mark certified): one-hand docking/release, port replication (USB/serial/Ethernet), keyed theft lock, VESA patterns; charge-while-docked keeps hot-swap batteries cycling
- **Wall/cradle kiosks** at workshops, permit offices, stores counters: shared-device shift-start points (§2.2), VESA 75/100 compatible
- **Zone-rated accessories only** in classified areas: non-certified metal accessories can void Ex ratings — accessory catalog is zone-filtered by the same geofence logic

# 8. Deployment, Fleet Management & Cost Bands
- MDM policy baseline shipped as a template (kiosk lockdown, cert pinning to DDE sync, remote wipe, OS-update rings); device inventory tracked as assets in DDE itself (dogfooding the canonical model)
- Indicative street pricing bands (budget guidance, verify at procurement): rugged Android tablets ~$1.3–2.5k; Windows fully-rugged ~$2.5–4.5k; Zone 1 intrinsically-safe ~$6–9k; docks/cases/harnesses $150–800/station; **Chinese rugged tier ~$200–630/unit** (verified Aug 2026: Oukitel RT7 5G $419–630, Blackview Active 8 Pro ~$370, Ulefone Armor Pad Pro ~$230, Hotwav R6 Pro ~$270)
- Hardware is customer-procured (DDE never resells margin-dependent hardware); the partner channel (equipment dealers, IT resellers) fulfils; DDE maintains the certified-compatibility matrix and bundle configs per pack

## 8.1 Where to buy — verified purchase links (checked Aug 2026)

**Western rugged-tier devices** — procured through enterprise/IT-reseller channels: Getac via authorized rugged resellers; Panasonic Toughbook via Panasonic business channel or Insight/CDW; Dell Pro Rugged via dell.com or CDW; Zebra ET60/ET65 via zebra.com "find a partner"; i.safe MOBILE / Ecom / Aegex via their regional industrial distributors listed on the vendor sites. Enterprise models are quote-based; direct web checkout is generally not available.

**Chinese rugged tier (direct-checkout friendly) — every link below is a direct product page:**

| Brand | Model in §7.2 | Direct product links | Notes |
|---|---|---|---|
| DOOGEE | R10 (10.4" IP68/IP69K/MIL-STD-810H, ~$159–285) | [DOOGEE official mall — R10](https://doogeemall.com/products/doogee-r10) · [DOOGEE Official Store on AliExpress](https://doogee-official.aliexpress.com/store/5044133) | AliExpress store is brand-official; bulk via Alibaba ~$174–193 — see §8.2 |
| Ulefone | Armor Pad Pro 8" (IP68/IP69K/MIL-STD-810H, ~$230) | [Ulefone official store — Armor Pad Pro](https://store.ulefone.com/products/armor-pad-pro) · [Ulefone UK — Armor Pad Pro](https://ulefone.co.uk/armor-pad-pro/) · [Newegg — Armor Pad Pro 8"](https://www.newegg.com/p/3C6-02S3-00097) | [Authorized reseller list](https://www.ulefone.com/pages/ulefone-authorized-reseller-program); bulk via Alibaba from ~$188/unit — see §8.2 |
| Blackview | Active 8 Pro 10.36" (22000mAh, MIL-STD-810H/IP68/IP69K, hand strap built-in; ~$320–370) | [Blackview global store — Active 8 Pro](https://store.blackview.hk/products/active-8-pro) · [Geekbuying — Active 8 Pro 4G](https://www.geekbuying.com/item/Blackview-Active-8-Pro-4G-Rugged-Tablet-Black-524175.html) · [Blackview Belgium (official EU distributor)](https://www.blackview-belgie.be/en/Blackview-Active-8-Pro-WiFi4G-8GB/256GB-Black) | EU distributor offers 2-year warranty vs 1-year direct |
| Oukitel | RT3 Plus 8" ($199–299) and RT7 Titan 5G 10.1" ($419–630, 32000mAh) | [Oukitel.global — RT3 Plus](https://oukitel.global/products/oukitel-rt3-plus) · [Oukitel.com — RT7 Titan](https://oukitel.com/products/rt7) · [Oukitel UK — RT7 £399](https://oukitel.uk/products/rt7) · [Geekbuying — RT7 5G](https://www.geekbuying.com/item/OUKITEL-RT7-5G-Tablet-10-1-inch-12GB-12GB-RAM-256GB-ROM-Black-521988.html) | Ships from US/EU local warehouses; factory outlet at [ec.oukitel.com — RT7](https://ec.oukitel.com/products/rt7); AliExpress item ref 1005010444608798 (~$338 for 4G/512GB) |
| Unihertz (8849) | Tank 2 Pro 6.79" phone-tablet hybrid (23800mAh, projector; ~$440) | [Unihertz official — Tank 2 Pro](https://www.unihertz.com/products/tank-2-pro) · [8849 factory store — Tank 2 Pro](https://8849tech.com/products/tank-2-pro-rugged-phone-with-23800mah-battery-superior-projection) · [South Africa distributor — Tank 2 Pro](https://unihertz.co.za/products/tank-2-pro-rugged-phone-with-23800mah-battery-superior-projection) | SA warehouse serves the Zimbabwe/Zambia/Botswana procurement path |
| Hotwav | R6 Pro 10.1" (15600mAh, glove mode; ~$237–270) | [Hotwav official — R6 Pro](https://www.hotwav.com/products/hotwav-r6-pro-rugged-tablet) (currently sold out) · [Amazon.de — Hotwav R6 Pro](https://www.amazon.de/HOTWAV-R6-15600mAh-Erweiterbar-Wasserdicht/dp/B0BQR7895C) | Older model; verify current production status before specifying |
| Ulefone (phone tier) | Power Armor 23 / Armor 23 Ultra (rugged smartphone pocket tier) | [Ulefone store — Armor 23 Ultra](https://store.ulefone.com/products/armor-23-ultra) (~$500) · [Amazon US — Armor 23 Ultra](https://www.amazon.com/Ulefone-Armor-23-Ultra-Satellite/dp/B0CR6FPXCF) · [Amazon UK — Armor 23 Ultra](https://www.amazon.co.uk/dp/B0CRH8Z6KH/) | Satellite messaging requires Bullitt subscription — not needed for DDE field use |

AliExpress note: individual item URLs rotate frequently (per-campaign IDs), so the durable deep links are the **brand-official stores** — DOOGEE's is linked above; Ulefone, Blackview and Oukitel run equivalent "Official Store" storefronts reachable via on-site search. Item-level price references captured Aug 2026: Oukitel RT7 4G ~$338 ([price history](https://sv.pricearchive.org/aliexpress.com/item/1005010444608798)), Ulefone Armor Pad Pro [item 1005006612443493](https://www.aliexpress.com/item/1005006612443493.html).

**Procurement cautions for the Chinese tier:** (1) global/unlocked versions only — CN-band variants may lack LTE bands used in target markets (verify Band 20/28 for EU/Africa); (2) bootloader unlock windows on some brands require an official unlock request within days of first boot — do this before MDM enrollment if a custom kiosk ROM is planned (§10); (3) warranty is typically 12 months manufacturer-direct vs 3 years on Western rugged tier; factor a spares-pool strategy per site; (4) Google Play certification varies by model — confirm GMS certification if Play Protect attestation is part of the kiosk verification chain (§10).

## 8.2 Chinese supplier & marketplace channels (bulk and single-unit sourcing)

The brand-direct stores in §8.1 are retail-priced. For fleet-scale procurement (20+ units), the Chinese marketplace channels below typically undercut them 10–30%, offer OEM/ODM customization, and consolidate multi-brand orders into one shipment:

| Channel | Type | Best for | Link |
|---|---|---|---|
| **AliExpress** | B2C marketplace (brand official stores + distributors) | Single units to ~10; buyer protection; global shipping incl. Africa routes | [aliexpress.com](https://www.aliexpress.com/) — search per model; prefer "Official Store" badged sellers |
| **Alibaba.com** | B2B wholesale (factory + trading companies) | Fleet lots 50–1,000+; OEM logo/packaging from MOQ 200–1,000 pcs; volume pricing e.g. Ulefone Armor Pad 5 Pro $388–404 at ≥100 packs, DOOGEE T-series ~$174–193 | [alibaba.com](https://www.alibaba.com/) — filter "Trade Assurance" suppliers; sample orders before commitment |
| **Geekbuying** | China-based e-tailer with US/EU/PL warehouses | Single to small fleets at near-wholesale prices; e.g. Oukitel RT7 5G listed below official-store price | [geekbuying.com](https://www.geekbuying.com/item/OUKITEL-RT7-5G-Tablet-10-1-inch-12GB-12GB-RAM-256GB-ROM-Black-521988.html) |
| **Banggood** | China-based e-tailer with AU/EU/US warehouses | Same profile as Geekbuying; strong rugged-phone category coverage | [banggood.com](https://www.banggood.com/) |
| **DHgate** | B2B/B2C hybrid wholesale | Mid-size lots without Alibaba MOQs | [dhgate.com](https://www.dhgate.com/) |
| **Brand factory outlets** | Direct-from-manufacturer (e.g. Oukitel EC store ¥-priced) | Deepest discounts when buying cross-border direct | [ec.oukitel.com](https://ec.oukitel.com/products/rt7) |

**Sourcing guidance for DDE deployments:** pilot quantities (<20 devices) via brand-direct or Geekbuying/AliExpress for speed and clean warranty chains; production rollouts via Alibaba Trade Assurance suppliers negotiated against the acceptance-test protocol (§9) — require pre-shipment inspection reports, IMEI/serial manifests for asset registration into DDE, and written confirmation of bootloader-unlock policy per unit. Chinese-marketplace purchases settle in USD card/wire; for Zimbabwe-linked procurement, route through the same reseller-of-record mechanism defined in §14.1 of the master plan rather than paying marketplaces directly.

# 9. Acceptance Testing (field-proof gates before rollout)
Per device-model × pack combination: 1.8m drop on concrete ×6 faces while logging evidence upload; water/spill (incl. hydraulic oil, milk-grade organic for food sites) then wet-touch operation; glove operation accuracy ≥98% tap-target hit rate; 12-hour double-shift battery endurance with hot-swap; dock/un-dock 500 cycles; offline→sync integrity after 8-hour disconnect with 200 queued ops; sunlight readability legibility test at 1000 lux; Zone-device certification document verification against the area register.

# 10. Android Kiosk Hardening (device owner & COSU)
To prevent users from exiting the kiosk app, accessing settings, or flashing custom ROMs during boot/use, DDE mandates Android Enterprise device-owner mode with COSU (Corporate-Owned Single Use) lock task — proven techniques include:

- **Device owner provisioning**: via NFC bump, QR code, or zero-touch enrollment at first boot; installs a Device Policy Controller (DPC) that owns the device from power-on
- **Lock task mode whitelist**: only the DDE kiosk app package(s) are allowed in lock task; home, recent, and back buttons are disabled; system UI cannot be escaped
- **Boot animation suppression**: custom ROM (LineageOS/AOSP derivative) with `debug.sf.nobootanimation=1` in init.rc or a blank bootanimation.zip in /data/local — no flashing logos during boot
- **Status/navigation bar removal**: config_showNavigationBar=false and status_bar_height=0dp in device overlay; immersive sticky mode hides system UI completely
- **Physical button restrictions**: via DevicePolicyManager — disable power/volume keys (except long-press for emergency SOS mapped to site workflow); prevent reboot/shutdown from hardware
- **Unknown sources blocked**: install non-play-store apps disabled; ADB disabled in production builds; OTA updates frozen via policy during critical windows
- **Custom ROM friendliness**: unlocked bootloader devices (DOOGEE, Ulefone, Blackview lines) allow flashing a hardened kiosk ROM once; DDE supplies the ROM image with the above hardening baked in and verifiable via attestation
- **Attestation & verification**: SafetyNet Play Integrity API or custom bootloader hash check at launch to confirm the device is in the expected hardened state; any deviation triggers admin alert and forced re-enrollment

# 11. Tech-Expert Module Enhancements (beyond hardware)
Beyond the rugged tablet and kiosk lock, DDE's field modules are enriched with the following AI-native and workflow features that experts repeatedly request in evaluations:

- **AI-native predictive maintenance**: on-device TensorFlow Lite models analyze vibration/temperature/pressure streams weeks before failure; confidence scores and lineage are displayed per rule 16; fallback to cloud when connectivity returns
- **Digital twin integration**: each asset has a live virtual replica synchronised with IoT sensor data; technicians can run what-if maintenance scenarios on the twin before touching physical equipment; remaining useful life forecasts feed the troubleshooting copilot
- **Workflow automation**: AI-generated insights seamlessly trigger work orders, parts reservations, technician scheduling, and procedure guidance without human intervention — closing the loop from prediction to action
- **Agentic AI copilot**: natural-language troubleshooting ("why is this bearing hot?") returns step-by-step guidance with evidence timestamps; learns from closed jobs to improve future suggestions
- **Procedure versioning & gating**: HIRA/JSA checklists are versioned assets; the app enforces the latest approved version before permitting hazardous work; offline sync resolves conflicts via last-writer-wins with ownership per §12
- **Calibration impact reconstruction**: when a tool goes out of tolerance, the app answers "what else was measured with it since the last good calibration" by tracing the dependency graph (§17.18 pharma pack)
- **Voice-to-text for failure logs**: noise-resistant speech-to-text in harsh environments feeds WO Text Intelligence (§17.12) — technicians describe symptoms hands-free

# 12. Digital Forms & Report Capture on Converted Documents (client side of §17.29)

The PDF Document Conversion Engine (§17.29 of the master plan) converts client paper documents into digital forms; this section defines how the field surfaces render and submit them.

## 12.1 Schema-driven dynamic form rendering
One flexible form renderer serves every converted template — no hardcoded layout per document type. The template's approved coordinate map (§17.29.3) drives a typed field model:

```
FieldType: Text · Number · Dropdown(options) · Checkbox · Radio(options)
         · Date · Signature · Photo · Scan(barcode/QR) · Calculation
FieldValue: TextValue(string) | ImageValue(reference) | ScanValue(decoded)
```

- Touch-optimized controls per type (number pads, option chips instead of long dropdowns, date pickers) following the ≥48px glove-target rules in §6
- Voice input available on text fields feeding WO Text Intelligence (§11); scan input on equipment/part identifiers
- Conditional logic shows/hides sections from prior answers; calculation fields compute live (totals, percentages, KPIs) with results stored beside raw inputs

## 12.2 Submit-time durability & sync (the non-negotiables)
- **Submit = synchronous local write** to the on-device durable queue (local ID, payload JSON, created timestamp, status PENDING/SYNCING/FAILED/SYNCED). Nothing is held in memory only — an app close, crash or signal loss at the moment of submission loses nothing
- A background sync worker drains the queue when connectivity returns (periodic + connectivity-constrained scheduling), with retry/backoff and resumable chunked upload for photo/media attachments
- Server re-validates before render — invalid data never reaches a regenerated official document
- **Pending-sync badge** visible per report until SYNCED; the data-age banner rule (§2.3) applies
- Countersign requests arrive as separate append-only records after sync — corrections never overwrite a signed submission (master plan §13.1)

## 12.3 Signatures & photos as compliance objects
Signature fields are wrapped by the platform e-signature layer (master plan §15.10): session-bound signer identity, explicit intent confirmation with meaning-of-signature, and tamper-evident hash binding to the exact payload version — the drawn ink is just the visual artifact. Photos capture full-resolution via FileProvider then compress to the media budget; large images upload by reference rather than base64-in-payload; EXIF location is stripped by default unless the site contract opts in.

## 12.4 Where documents appear in the surfaces
- **Tech Kiosk App:** converted forms open as job-pack steps (checklists, post-maintenance records, statutory test sheets); completion signature rides the same e-signature wrapper; submission emits the domain events that update registers (§15.6) and stores the report against the asset's history
- **Supervisor App:** countersign queue for reports awaiting supervisor sign-off; approval uses the governed e-signature flow (§3.2 powers apply)
- **Manager Console:** report history per asset with download/share; template registry management UI (draft → pending approval → active → retired, master plan §17.29.5); bulk conversion intake for client document estates
- **Executive View:** statutory-compliance % reflects register updates fired by submitted documents in near-real-time

Rendering always executes server-side over the immutable base template (§17.29.1) — template assets and approved coordinate maps never ship inside the kiosk image, so a hardened device (§10) can never leak another tenant's document templates.
