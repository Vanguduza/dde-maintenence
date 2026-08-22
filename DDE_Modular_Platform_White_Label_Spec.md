# DDE — Modular Platform & White-Label Specification

**Document status:** Companion specification to `DDE_Maintenance_Intelligence_ERP_Master_Plan_v2.md` (§17.15). Defines the modularity architecture that makes client customization a matter of **actioning branding and integration parameters**, not code changes — and defines the guardrails that keep this configurable surface compatible with the compliance framework (master plan §15).
**Date:** 22 August 2026

---

# 1. Prime Directive: Customization Is Configuration, Not Code

Every customer-facing variation — industry, jurisdiction, brand, language, units, integrations, compliance registers — must be expressible as versioned configuration applied to one binary/one codebase. If a requirement cannot be met within the parameter space below, it becomes a roadmap request, not a fork. This is what allows: (a) onboarding a new client in days for standard profiles; (b) partners reselling DDE under their own brand; (c) one engineering team serving ten verticals.

# 2. Tenancy Hierarchy

```
Platform Operator (DDE)
 └─ Partner/OEM brand (optional — white-label reseller, equipment dealer, consultancy)
     └─ Customer Organization (tenant)
         ├─ Site / Plant / Farm / Depot / Portfolio
         │   └─ Area · Line · Asset · Component
         └─ Settings inheritance: brand → org → site → asset class
```

Configuration cascades downward with explicit override points; inherited values are visible and traceable (config lineage mirrors §8 data lineage discipline).

# 3. Branding Layer (Design Tokens)

| Token group | Contents |
|---|---|
| Visual identity | Logo set (light/dark/favicon/app icon), color palette (semantic tokens: primary, danger, success, charts), typography stack, spacing/radius scale |
| Product naming | Display name, product term dictionary (e.g., "Work Order" vs "Job Card" vs "Task"), email sender identity, report/PDF letterhead and footer |
| Domains | Custom domain mapping (`maintenance.client.com`) with automated TLS; branded mobile-app shells generated from the token bundle (store listings managed by the branded build pipeline) |
| Document output | Work-order prints, permit forms, statutory certificates, audit exports rendered with customer/partner letterhead and jurisdiction-required field layouts |
| Localization packs | Language, date/number formats, measurement units (metric/imperial per site class), currency display; terminology dictionary is part of the locale pack |

Constraint: branding changes presentation only. It can never remove, reorder, or weaken compliance-mandatory UI elements (statutory overdue banners, evidence capture prompts, signature blocks, safety gates).

# 4. Integration Parameters (Declarative Connector Manifests)

Connector instances are created by **manifest**, never bespoke code:

```yaml
connector:
  type: opcua | modbus-tcp | j1939-gateway | oem-telematics-api | sap-pm | maximo-rest |
        pi-historian | bms-bacnet | isobus | scada-sparkplug | sftp-reports | webhook
  endpoint: {url|gateway-id}, auth: vault-ref
  parameters:            # protocol-specific, validated against schema
    opcua: node-list, subscription-interval
    modbus: register-map-ref
    j1939: pgn-filter, source-address-map, sample-rate
  direction: read | write-back | bidirectional
  ownership-contract: ref (§12.2)   # required when direction ≠ read
  field-mapping-set: ref (versioned canonical↔external map)
  conflict-routing: queue-owner, sla
  residency-pin: region          # data-residency constraint
  retention-profile: ref
```

Field mapping sets are versioned artifacts with a test harness (sample payloads → expected canonical objects) run automatically on any change. Adding a customer integration = authoring manifests + mappings + running the certification harness — measured in days, not projects. The connector certification program (§17.7) certifies *types*; manifests instantiate them.

# 5. Vertical Packs as Declarative Bundles

A vertical pack (master plan §17.11, §17.13–§17.21) is a signed, versioned bundle:

1. **Schema extensions** — asset subtypes and attribute sets (e.g., transformer → cooling-stage; harvester → header; lift → duty classification)
2. **Failure-mode library slice** — seeded priors per asset family (§17.2)
3. **KPI set** — availability/utilization/cost-per-hour/per-km/per-hectare definitions bound to the canonical model
4. **Workflow templates** — job cards, permits, inspection checklists, shutdown/turnaround or MSS or turnaround calendars
5. **Compliance register templates** — jurisdiction × industry entries from the register library (§6 below)
6. **Economics penalty types** — production-loss, liquidated damages, crop-loss window, SLA credits, margin-per-delivery (§8.2)
7. **Terminology + default theme** — pack ships with locale and token defaults a client may override

Packs compose (a construction contractor with a crane fleet activates Fleet + Construction + Facilities-lifting registers). Precedence rules resolve overlaps deterministically; conflicting compliance intervals always escalate to the stricter interval and flag for counsel review.

# 6. Compliance Register Template Registry

One engine (master plan §15.6), many templates. Each template encodes: legal instrument citation; applicable asset classes; interval table (with monitoring-based extension semantics where law allows, e.g., NERC PRC-005-6 monitored components); evidence requirements (measurements, photos, inspector competency proof); sign-off rules; retention period; export format for the authority. Templates are versioned with effective dates and carry a counsel-review status. Shipping library covers: mining (SI 109/1990, MHSA-class, GISTM), transport (49 CFR 396 App A + eDVIR chain; EU roadworthiness 2014/45/EU; AETR tachograph 56-day retention), facilities (LOLER, PUWER, F-Gas by CO₂e band, RRO 2005 fire regimes, BS 5839-1:2025 servicing, EICR 5-yearly, Legionella L8/HSG274, PSSR, CAR 2012 asbestos, Building Safety Act duties), process (API 510/570/653 under OSHA PSM 1910.119(j)/Seveso III), utilities (NERC PRC-005-6 PSMP, FAC-003-5 vegetation; regional grid-code analogues), pharma (GMP calibration/status registers), food (HACCP/CCP-linked maintenance records, FSMA 21 CFR 117 two-year minimums).

# 7. Edition Entitlements & Governance Gates

Feature flags are license- and governance-bound: commercial entitlements (tier, pack, seat counts) are separate from **governance activations** (§11 workforce view, Mode B write-back, FLN participation) which each require their documented activation ceremony — consent artifacts, works-council review where applicable, executive sign-off — recorded as immutable events. Flags evaluate at runtime per org/site; expired licenses degrade gracefully to read-only rather than locking evidence away.

# 8. Deployment Topologies — One Manifest, Three Shapes

| Shape | Use | Mechanism |
|---|---|---|
| Cloud multi-tenant | Standard clients, partners' tenants | Shared control plane; logical isolation; residency pinning per tenant |
| Cloud dedicated / VPC | Security-sensitive mid-enterprise | Same services, isolated estate; config promoted identically |
| Edge / on-prem / air-gapped | Mine sites, remote fleets, OT-restricted plants, Zimbabwe load-shedding resilience (§13) | Signed configuration bundles synced to site nodes; offline-first core unaffected; config drift detected and reconciled |

Because all three consume identical manifests, a pilot can start air-gapped at a remote site and move to cloud without reconfiguration.

# 9. Configuration Lifecycle (Config-as-Code)

Manifests live in a git-backed configuration repository. Promotion path: **sandbox → staging → production**, each promotion running an automated validation suite (schema conformance, compliance-interval sanity vs register library, connector smoke tests, branding-token linting, accessibility contrast checks) with human diff review. Rollback is a revert. Every production config change is an auditable event (who, what, when, approval) — satisfying both ISO 27001 change control and GAMP-class expectations where activated.

# 10. Guardrails — What Cannot Be Configured

To protect the product's compliance posture and its own accountability:

1. Safety gating logic (offline hazardous-work restrictions, LOTO verification flows) — parametrizable in strictness, never removable
2. Economics lineage enforcement (rule 16) — figures without lineage cannot be displayed, regardless of config
3. Alert precision SLO floors (§10) — tenants may tighten, never loosen below class minimums
4. Audit trails, evidence immutability, signature validity — always on, always tamper-evident
5. Statutory overdue escalation — planners cannot silence; never auto-deferred (§15.6)

White-label means white-*presentation*, not white-*box*: partner-branded deployments retain DDE's conformity artifacts (CRA declaration, SBOM, security attestations). Resellers contractually accept flow-down of these obligations (§15.14 supplier clauses).

# 11. Client Onboarding Wizard (the "Actioning" Experience)

Standard-profile go-live sequence, target **days**: (1) branding kit upload (logo, palette, terms, domain) → instant preview across web/tablet/mobile; (2) pack selection (industry, jurisdictions → registers auto-installed); (3) integration manifests authored from certified templates + field mappings; (4) data migration (assets, history, spares) via migration factory; (5) user import + role templates; (6) UAT checklist runbook → go-live. Deviations beyond the parameter space are logged as roadmap requests with a named owner — keeping SI effort bounded and honest.

# 12. Limitations

- Deep bespoke workflow changes (new business objects, altered state machines) are deliberately outside configuration; the boundary is enforced by the validation suite, not goodwill.
- Branded mobile shells lag the main release train by one store-review cycle per platform.
- Jurisdiction template library depth varies by market at launch; the registry marks counsel-review status per template so sales cannot promise unreviewed registers.
