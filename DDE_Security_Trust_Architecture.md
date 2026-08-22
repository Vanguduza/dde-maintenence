# DDE — Security & Trust Architecture

**Document status:** Companion specification to `DDE_Maintenance_Intelligence_ERP_Master_Plan_v2.md` (extends §7, §13, §15.2–15.3; summarized as §17.30). Defines the end-to-end security architecture for DDE across all deployment shapes (cloud multi-tenant, dedicated VPC, edge/on-prem/air-gapped), all field surfaces (§17.23), and all data flows (telematics ingestion, offline sync, document engine §17.29, write-back §12.2). Its mandate: customer data must be watertight against external attack **and** against commercial-intelligence exposure — downtime economics, failure libraries and production rates are competitively sensitive assets that DDE never sees beyond need, never repurposes, and can prove it protects.

**Date:** 22 August 2026
**Research basis (verified Aug 2026):** EU Cyber Resilience Act (Regulation 2024/2847) reporting obligations live since 11 September 2026 with full application 11 December 2027; ISO/IEC 27001:2022 is the only valid certification edition since the IAF transition deadline of 31 October 2025 expired; SOC 2 security+availability+confidentiality trust services criteria; IEC 62443-4-1/-4-2 (2018/2019 editions, regionally re-adopted through 2025) with ISASecure SDLA/CSA certification chains; NIST FIPS 203/204/205 (ML-KEM/ML-DSA/SLH-DSA) published August 2024 with hybrid X25519MLKEM768 TLS standardized in RFC 10024 and shipping by default in Chromium-based stacks; OWASP API Security Top 10 (2023 edition current); Android Play Integrity API standard verdicts (MEETS_BASIC / MEETS_DEVICE / MEETS_STRONG_INTEGRITY) replacing deprecated SafetyNet; NIS2 Article 21 supply-chain security obligations flowing down to software suppliers.

---

# 1. Threat Model & Trust Doctrine

## 1.1 Who we defend against

| Adversary | What they want | Primary vectors | Where countered |
|---|---|---|---|
| Opportunistic attackers / ransomware crews | Any foothold → extortion; manufacturing/industrial SaaS is a paying target | Phishing, stolen credentials, unpatched perimeter, supply chain | §§3, 5, 6 |
| Competitor intelligence gathering | Customer production rates, downtime costs, failure patterns, asset locations | Compromised tenant isolation, insider access, analytics leakage, sub-processor chains | §§2, 4, 9 |
| Nation-state / targeted intrusion | Strategic infrastructure visibility via a maintenance platform used at mines/utilities/utilities-scale fleets | Supply-chain implants, long-dwell APT, harvest-now-decrypt-later collection | §§5.5, 6, 10 |
| Malicious insider (DDE or partner staff) | Direct data theft or quiet exfiltration | Over-broad standing access, unlogged data paths | §9 |
| Compromised field device | Kiosk escape, credential harvesting, evidence tampering, lateral movement into OT | Physical access, rogue accessories, ROM tampering, MITM on weak links | §7 |
| Compromised integration peer (OEM cloud, EAM vendor) | Pivot from trusted connector into tenant data | Over-scoped OAuth grants, SSRF via webhooks, unsafe third-party API consumption (OWASP API10) | §8 |

## 1.2 Trust doctrine — five non-negotiables

1. **Tenant data belongs to the tenant.** DDE is custodian, never owner. Every access by DDE personnel is logged, justified, visible to the customer, and alertable.
2. **Competitive intelligence is radioactive.** Aggregates that could reveal a customer's operational position (FLN priors §17.1, benchmarking features, AI training corpora) are protected with differential privacy, consent gates, and per-customer contribution ledgers — the same rigor as personal data under GDPR, applied to *commercial* data.
3. **Safety-relevant systems fail closed.** Write-back (Mode B), permit/isolation objects, and kiosk lockdown degrade to "no action" rather than "default allow" when integrity cannot be verified.
4. **Zero standing privilege.** Human and machine access alike is just-in-time, purpose-bound, time-boxed, and fully journaled.
5. **Evidence over assertion.** Every claim in this document maps to an auditable artifact (SBOM, pen-test report, attestation log, key ceremony record) in the Standards & Audit Evidence Pack (master plan §17.10).

## 1.3 Compliance frame this architecture must satisfy simultaneously

EU CRA (product security + 24h/72h ENISA incident reporting), NIS2 (supply-chain flow-down when selling into EU operators), ISO/IEC 27001:2022 Annex A (the only valid edition since Oct 2025), SOC 2 Security·Availability·Confidentiality, IEC 62443-4-1/-4-2 for the OT-facing components, GDPR/UK-GDPA/POPIA/Zimbabwe CDPA per market (master plan §15.4), plus sector overlays sold as entitlements (Part 11 §17.18, HACCP-evidence integrity §17.19). One control set, many attestations — controls are implemented once and mapped, not forked per framework.

# 2. Data Classification & Competitive-Intelligence Protection

The unique DDE twist: the most sensitive data is often not PII but *commercial*. Classification drives every control below.

## 2.1 Classification scheme

| Class | Examples | Default handling |
|---|---|---|
| C1 Public | Marketing content, published docs | None |
| C2 Internal | Config manifests, non-sensitive ops metadata | Tenant-scoped RBAC |
| C3 Commercial-confidential | Downtime costs, VaR models, maintenance debt, production-linked KPIs, cost-of-inaction figures | Tenant-scoped encryption, ABAC row policies, DDE-staff access gated behind customer-visible break-glass only, excluded from any cross-tenant feature without explicit consent artifact |
| C4 Safety-critical | LOTO state, permit status, isolation verification, Ex-zone registers | Online-gated (never merged offline per §13.1), append-only journals, dual-control where applicable |
| C5 Personal | Technician identity, workforce analytics (gated §11), signatures, EXIF media | Per-jurisdiction controls (§15.4), minimization, retention clocks |

C3 is treated with the same engineering seriousness as C5: field-level encryption context, lineage-tracked derivations (rule 16), and a prohibition register listing exactly which features may never consume C3 across tenants (benchmark leaderboards, FLN raw gradients, sales-analytics pipelines).

## 2.2 The intelligence-protection contract (customer-facing, contractual)

- **No cross-tenant learning without signature.** FLN participation, benchmark comparisons, and model-prior contributions require the data-sharing addendum; opt-out removes future contribution (master plan §17.1).
- **No human eyeballs without break-glass.** DDE support reaching C3/C5 requires time-boxed, ticket-linked, customer-notified elevation; the access event appears in the customer's own audit view within minutes.
- **No sub-processor surprise.** Published sub-processor list with change notification window; regional pinning honored at the storage and processing layer, not just the contract layer (matters for Zimbabwe SDN-screened customers and EU residency deals alike).
- **Deletion is real.** Contract-end tenant wipe executed and certified (key destruction makes encrypted remnants unrecoverable — see §4.3 crypto-shredding), with a certificate of erasure.

# 3. Identity, Authentication & Session Security

## 3.1 Workforce (web/console) access

- SSO-first: SAML 2.0 / OIDC enterprise federation; SCIM provisioning; per-tenant enforced MFA (FIDO2/passkeys preferred; TOTP floor), with phishing-resistant MFA mandatory for administrator and approval roles (permit/isolation approvers, template approvers §17.29.5)
- Step-up authentication (fresh passkey/biometric re-proof) for consequential actions: Mode B write-back approvals, statutory-overdue overrides (which are never allowed anyway), bulk exports, sub-processor changes
- Session hygiene: short-lived access tokens (≤15 min) with rotating refresh, bound to device posture where available; concurrent-session limits; instant global revoke on credential events

## 3.2 Field (kiosk/tablet) access — shared-device reality

- NFC badge tap-in (§17.23) yields a scoped session tied to badge cryptogram + device attestation state; sessions die at badge removal for shared devices
- Device identity precedes user identity: a device that fails attestation (§7.3) cannot authenticate any user, regardless of badge validity
- Offline authentication cache: signed, expiring role assertions let technicians keep working air-gapped for the length of their rostered shift; revocations propagate opportunistically and force re-verification at next sync — safety-role changes (e.g., permit authority revoked mid-shift) always re-check online before any safety object interaction

## 3.3 Machine & service identity

Every non-human actor (connector, edge node, render service, sync worker, FLN aggregator) holds a workload identity: mTLS with SPIFFE-class certificates, short-lived, auto-rotated, scoped to one integration manifest's permissions. No shared service accounts; no static API keys anywhere in the stack (customer legacy systems that only offer static keys get them vaulted and proxied, never propagated).

# 4. Cryptography & Key Management

## 4.1 In transit

- TLS 1.3 everywhere; TLS 1.2 permitted only toward legacy OT/EAM endpoints that cannot do better, inside documented conduits
- **Hybrid post-quantum key exchange (X25519MLKEM768 per RFC 10024) enabled on all internet-facing TLS terminators** — cheap now, and it neutralizes harvest-now-decrypt-later collection against maintenance traffic whose confidentiality horizon (multi-decade asset histories, geology, contracts) genuinely extends past any plausible CRQC date
- Service mesh mTLS internally; cert-pinned sync channels from mobile apps (MDM baseline already pins these, §17.24); J1939 gateway→cloud links use mutual-auth MQTT/TLS with per-device certs

## 4.2 At rest

- AES-256-GCM at the storage layer with **per-tenant envelope keys** (not merely per-database): cloud multi-tenant uses provider KMS with tenant-scoped data keys; dedicated/VPC and on-prem deployments support customer-held root keys (BYOK/HYOK spectrum)
- Field-level encryption for C3/C5 columns so analytics/query workloads never touch cleartext beyond need; document-engine artifacts (signed reports, payloads §17.29.7) encrypted with the tenant key and stored privately (already mandated)
- Database-level activity monitoring on C3 tables; anomalous read patterns (bulk SELECT, off-hours access, new-principal access) page the security team *and* appear in the tenant's audit stream

## 4.3 Key management & lifecycle

- HSM-backed roots (FIPS 140-3 Level 3 class) in cloud; documented key ceremonies for dedicated/on-prem root generation involving the customer
- Separation of duties: no single DDE engineer can combine key-admin and data-plane roles; break-glass decryption requires two-person control and produces an immutable, customer-visible journal entry
- **Crypto-shredding as the deletion primitive:** tenant offboarding destroys data keys, rendering encrypted remnants unrecoverable regardless of backup expiry windows; certificate of destruction issued
- Crypto-agility register: algorithm inventory with migration paths; ML-KEM/ML-DSA adoption tracked against FIPS 203/204 so signature migration is a planned swap, not an emergency

# 5. Application & API Security

## 5.1 Secure SDLC

IEC 62443-4-1-aligned development lifecycle (doubles as CRA Annex I secure-by-design evidence): threat modeling per epic, secure-coding standards, mandatory pre-merge SAST, dependency scanning with SBOM regeneration per build (CRA-ready), secrets scanning, DAST in staging, annual third-party penetration tests plus engagement-triggered tests (new connector class, new deployment shape). Defect SLAs: critical 48h, high 7d.

## 5.2 API defense (OWASP API Top 10 2023 mapped)

- **BOLA/BFLA (API1/API3):** object-level authorization enforced in one shared policy engine (ABAC on tenant/role/classification), never hand-rolled per endpoint; generated policy tests prove every endpoint's matrix
- **Broken auth (API2):** short-lived tokens, audience-restricted scopes per manifest, replay protection (nonce/JTI), anti-brute-force on all credential endpoints including recovery
- **Unrestricted resource consumption (API4):** per-tenant quotas, pagination ceilings, payload caps (document payloads have explicit media budgets per §17.29.4), cost-based rate limiting
- **SSRF (API7):** outbound fetches only through an egress proxy with allow-lists; webhook receivers validate signatures and origins; connector targets pinned by manifest — a connector can only call what its YAML declares (this also enforces §12.2 ownership contracts at the network layer)
- **Unsafe consumption of APIs (API10):** third-party responses parsed with strict schemas; OEM telematics clouds treated as hostile input, not trusted peers

## 5.3 Input & content safety for AI surfaces

Prompt-injection containment for the copilot/agentic features (§17.28): retrieved documents and telemetry are data, never instructions; tool calls execute least-privilege with human confirmation for consequential actions (write-back, scheduling changes); model outputs carry the same authorization checks as human-originated requests — an agent can never read anything its invoking principal couldn't.

## 5.4 Document-engine specific hardening (binds §17.29)

Template PDFs are an attack surface (malicious PDF parsers are classic CVE territory): parsing happens in sandboxed, resource-limited workers; rendered output regenerates from structured data rather than passthrough embedding of untrusted objects; coordinate-map JSON is schema-validated and signed; the render service holds one workload identity with write access to exactly one storage prefix per tenant.

## 5.5 Anti-implant discipline (targeted-adversary resistance)

Reproducible builds; signed release artifacts verified at deploy; runtime integrity monitoring on server images; third-party code allow-list (no transitive dependency lands without review gate); vendor access via just-in-time brokered tunnels, never persistent VPN accounts.

# 6. Infrastructure & Deployment Security

- Hardened golden images; immutable infrastructure; configuration drift detection with auto-revert; CIS-benchmark baselines per component class
- Network segmentation mirroring the 62443 zone/conduit model even in cloud: ingestion plane, analytics plane, OT-write plane, and corporate plane are separate zones; the OT-write conduit (Mode B) additionally requires the destination site's edge node to verify request provenance before execution (§12.2 ownership contract enforced cryptographically, not just logically)
- Edge/on-prem/air-gapped deployments (Zimbabwe load-shedding resilience, §13) ship the same controls containerized: local SIEM forwarding when a link exists, store-and-forward audit export when it doesn't; tamper-evident local audit log (hash-chained) so offline periods still produce court-grade records
- Backup integrity: encrypted, access-separated, restore-tested quarterly (ransomware resilience = tested restores, not backup existence)

# 7. Field Device & Kiosk Security (extends §17.27 hardening)

## 7.1 Layered lockdown recap (from master plan §17.27)

Device-owner COSU lock task, boot-animation suppression, navigation-bar removal, button restrictions, unknown-sources block, hardened-ROM option on unlocked-bootloader Chinese-tier devices (DOOGEE/Ulefone/Blackview lines).

## 7.2 Data protection on device

- SQL Cipher-class encryption of the local op-log and cached job packs; keys in Android Keystore (StrongBox where the SoC provides it)
- Remote wipe + auto-wipe triggers (attestation failure, N failed unlocks, device reported lost via MDM); offline queue is included in wipe scope
- Media (photos, signatures §12.3 of the Field Experience spec) stored app-private, encrypted, never entering device-wide galleries; clipboard blocked in kiosk mode; screenshots disabled on evidence screens (FLAG_SECURE)

## 7.3 Attestation & continuous verification

- Play Integrity standard verdicts checked at sign-in and before sensitive actions; tiered response: MEETS_STRONG_INTEGRITY = full trust; MEETS_DEVICE_INTEGRITY = normal operations; MEETS_BASIC_INTEGRITY = degraded mode (view-only outside safety flows); no verdict = sign-in refused
- Custom-ROM fleets (where Play services are stripped) substitute hardware key attestation chains verified against the DDE-enrolled ROM fingerprint recorded at provisioning — same tiering, different verifier
- Attestation failures trigger admin alerts and forced re-enrollment (existing rule), now extended: the device inventory entry flips to quarantine automatically

## 7.4 Rogue-peripheral defenses

USB in OTG/accessory mode disabled in lock task (blocks BadUSB/keyboard-injection dongles into charging ports); NFC reads restricted to enrolled badge UID ranges plus cryptographic challenge (cloneable UID-only badges rejected); Bluetooth locked out entirely except docked-charging profiles; charging stations at workshops are power-only or data-diode'd.

# 8. Integration & Connector Security (extends §12)

- Manifest-declared scope is enforced end-to-end: credentials vaulted (encrypted with tenant key, never displayed back), egress pinned, field mappings versioned and test-harnessed (§17.22) — a compromised connector can move only within its declared conduit
- OAuth grants toward OEM telematics clouds use least-scope; token refresh audited; OEM-side revocation webhooks honored immediately
- Webhook receivers: signature verification, timestamp windows (replay rejection), source allow-lists, payload size caps
- Partner SDK (§17.7) ships the same policy engine libraries so ecosystem connectors inherit BOLA-safe defaults instead of inventing their own
- Third-party risk tiering: connectors touching C3/C5 data require the vendor's SOC 2 / ISO evidence on file and annual refresh; the connector registry tracks evidence expiry like certificates

# 9. Insider Risk, Monitoring & Detection

- Full audit plane: every read/write of C3–C5 data carries actor, purpose (ticket link), source IP/device, and classification tags; hash-chained log storage; tenant-visible subset streams in near-real-time to the customer's console (trust through transparency, not secrecy)
- UEBA baselines per role (a planner suddenly exporting 40k rows is anomalous; a support engineer touching ten tenants in an hour is anomalous); detections route to a 24/7 on-call with documented escalation; customer-notification clock starts at confirmed-scope assessment to honor the CRA 24h early-warning duty
- Quarterly access recertification; joiner-mover-leaver automation; DDE staff devices managed (MDM, disk encryption, EDR) — the vendor is part of every customer's supply chain, so the vendor holds itself to the NIS2-grade bar it asks of others
- Whistleblower/abuse channel for internal misuse reports (ISO 27001 control alignment)

# 10. Incident Response, Resilience & Breach Duties

- IR plan exercised twice yearly (one tabletop, one technical red-team scenario); roles mirrored for edge deployments where DDE responds jointly with the site
- Regulatory clock discipline: CRA 24h early warning / 72h notification workflow rehearsed with templates pre-drafted; GDPR 72h processor-notification contract terms standard; customer runbooks define who DDE notifies, in what order, with what evidence
- Ransomware playbook: isolate → preserve forensic images → restore from immutable backups (tested quarterly §6) → statutory notifications; recovery objectives per tier (safety dashboards first, analytics last)
- Vulnerability disclosure policy with safe harbor; security.txt; coordinated disclosure credited in advisories — a small company earns disproportionate trust by handling reports professionally
- Post-incident reviews feed the threat model (§1.1) and the control backlog; no blameless-theater — actions tracked to closure with owners

# 11. Born-Compliant Infrastructure — the SF-parity control set, operating from day one

**Doctrine change from the prior roadmap:** DDE does not build first and certify later. The platform launches with the *structure and infrastructure* of a certified system already operating — control set, evidence machinery, audit relationships, and governance cadence live from Phase 0 — so that acquiring each accreditation becomes an application against existing proof, not a remediation project. The reference bar is the SAP cloud portfolio (ISO 27001/27017/27018, ISO 22301, ISO 9001, BSI C5, CSA STAR, SOC 1/2): every control those audits test is implemented and evidenced at launch, plus the OT/device/commercial-intelligence controls SAP's portfolio does not cover.

## 11.1 The continuous-evidence engine (the core mechanism)

Certifications fail or drag because evidence is reconstructed after the fact. DDE inverts this: **every control emits its own evidence as a byproduct of operation**, collected continuously into a compliance data store that any auditor reads on arrival.

- **Controls-as-code registry:** every security control exists as a machine-readable entry (owner, framework mappings — ISO 27001 Annex A / C5 criteria / CSA CCM / SOC 2 TSC / CRA Annex I / 62443-4-1 practices —, test procedure, evidence type). One control implementation maps to many frameworks simultaneously; no forked control sets.
- **Automated evidence collection:** config-drift scans, access-review exports, SBOM per build, scan results, ticket-linked approvals, backup-restore tests, DR-exercise reports, training completions — captured automatically with timestamps into WORM storage.
- **Live control dashboard:** each control shows current pass/fail with last-evidence date. A red control blocks release gates (§14) — the same telemetry auditors will later sample is the telemetry engineers watch daily. Compliance posture is observable, not asserted.
- **Audit-ready export:** any framework section generates its evidence bundle in auditor-consumable form on demand.

## 11.2 Governance & organizational controls (ISO 27001 A.5-class, live at launch)

ISMS scope defined before first customer data: information-security policy set, risk-assessment methodology + living register, Statement of Applicability drafted across all 93 Annex A controls, roles/responsibilities (CRO-equivalent accountability named even if fractional), asset inventory, supplier-security register with tiering, awareness training program with completion tracking, disciplinary process, secure-development policy (62443-4-1 mapped), mobile-device/BYOD/clear-desk policies, HR security joiner-mover-leaver procedure, and management-review cadence scheduled quarterly from day one. ISO 27001's certification requirement of an *operating* ISMS (typically ~3 months of records) is thus satisfied by calendar time, not by a scramble.

## 11.3 Physical & environmental (ISO 27001 A.7 / C5 physical-security criteria)

Cloud regions are provider-attested (inheritance via provider ISO/SOC reports, sub-processor listed); edge/on-prem nodes get site-checklist controls (locked cabinet/room, power protection per Zimbabwe load-shedding reality §13, tamper seals, disposal procedure) shipped as part of deployment runbooks — physical controls exist wherever data lives, not only where DDE's offices are.

## 11.4 What "surpass SF" means structurally

SF-parity covers the classic SaaS surface. DDE's born-compliant baseline additionally operates, from launch, four layers SF's portfolio does not address:

1. **OT-facing product security to 62443-4-1/-4-2** (with ISASecure-ready artifacts maintained continuously)
2. **Field-device fleet attestation** (§7.3 verdict tiering enforced as an auditable control, not just a feature)
3. **Commercial-intelligence isolation** (C3 classification + break-glass + prohibition register as named, evidenced controls)
4. **Regulatory product duties**: CRA technical file + SBOM pipeline maintained current (reporting duties already live since Sep 2026); EU AI Act technical documentation for in-scope model components (§15.16)

## 11.5 Operating rules that keep the claim honest

- No marketing use of any certification name before the certificate exists; the trust center says "controls implemented, audit scheduled [date]" — which enterprise buyers respect more than vaporware
- Control changes flow through change-management with compliance impact noted; drift between declared and actual state auto-gates releases
- Annual internal audit plus surveillance-readiness self-assessment every six months, so external audits confirm rather than discover

## 11.6 Consolidated audit & assessment calendar — full task cadence, daily to yearly

One calendar, owned by the compliance program owner (master plan §15.14). Two layers: the **operational cadence** below is executed as routine work with automated evidence capture per task; the **audits** (bottom block) then *verify* that cadence — internal and external auditors sample task execution records, so every scheduled task is itself audit-covered. Auditor slots pre-booked per §12.

### Operational cadence (evidence captured automatically per task)

| Cadence | Scheduled task | Evidence artifact |
|---|---|---|
| **Continuous (auto)** | Config-drift detection; SAST/secrets scans on merge; dependency + container CVE scanning; audit-stream integrity (hash-chain verification); UEBA detection running | Scan results, pipeline logs, chain attestations |
| **Daily** | Security alert queue triage & sign-off; backup-job completion verification; new-CVE exposure check against deployed SBOM stack; kiosk attestation-failure review; audit-stream completeness spot check | Triage log, backup reports, CVE-match report, device quarantine log |
| **Weekly** | Infrastructure vulnerability scan + patch triage; access-anomaly (UEBA) report review; stale-evidence sweep of the controls registry; vendor/security-advisory watch (CISA, vendors, OEM clouds) | Scan reports, anomaly dispositions, freshness report |
| **Monthly** | Patch-SLA compliance report (critical 48h / high 7d adherence); conformity matrix review (§17.10); UEBA tuning review; key-rotation currency check; trust-center content accuracy check; **security metrics scorecard published** (§11.7); regulatory-watch digest to counsel | Patch dashboard, matrix delta, rotation log, published scorecard |
| **Quarterly** | ISMS management review (metrics-driven agenda §11.7); access recertification (privileged + C3–C5); backup restore test; threat-model refresh for changed data flows; rotating internal control-sample testing; supplier risk review (rolling tier-1 subset); metrics-target review & reset | Review minutes, recert records, restore reports, TM diffs, test samples |
| **Semi-annual** | Surveillance-readiness self-assessment; IR exercise (alternating tabletop / technical red-team scenario); CRA 24h/72h notification drill; policy light-review cycle | Readiness report, exercise reports, drill timelines, change marks |
| **Annual** | Third-party penetration test (+ event-triggered extras); full internal ISMS audit; SOC 2 Type II examination; ISO 27001 surveillance/recertification; C5 re-audit (post-adoption); full policy-set review & re-approval; company-wide security-awareness training refresh; BC/DR full failover exercise (ISO 22301 evidence); supplier tier-1 full review; cyber-insurance posture review | All external audit reports; signed policies; training register; exercise report |
| **Per-event triggers** | New connector class / deployment shape / major architecture change → threat model + targeted pen test; any new market or hardware class → counsel gap review before first sale (§15.14); confirmed incident → post-incident review feeding threat model | Event-linked artifacts |

### Verification layer (the audits themselves)

Internal ISMS audit (annual) and the semi-annual readiness self-assessment explicitly **sample the operational cadence**: did each scheduled task run, on time, with its evidence artifact current? A missed cadence task is an audit finding by definition — the calendar is therefore self-enforcing rather than aspirational. External auditors (SOC 2/ISO/C5) receive the same cadence records through the evidence engine's export.

## 11.7 Security metrics program (what audits and management measure)

Metrics are defined once, collected automatically, and consumed at three altitudes: release gates (§14), monthly scorecard, quarterly management review. Every metric has an owner, an automatic source, and a threshold that triggers documented action when breached.

| # | Metric | Definition | Target / threshold | Frequency |
|---|---|---|---|---|
| 1 | Critical-vulnerability MTTR | Mean hours from disclosed/scan-detected critical to remediated | ≤48h; zero >96h | Weekly roll-up |
| 2 | High-vulnerability MTTR | As above for high severity | ≤7d; zero >14d | Weekly roll-up |
| 3 | Open known-criticals in production images | Count from SBOM×CVE match | 0 without signed exception | Daily |
| 4 | Patch-SLA adherence rate | % vulnerabilities remediated within SLA by severity | ≥95% | Monthly |
| 5 | Asset scan coverage | % of production assets (cloud, edge nodes, devices) scanned ≤7 days | ≥98% | Weekly |
| 6 | MTTD / MTTR (security incidents) | Mean time to detect / to contain+recover, by severity | MTTD ≤24h; MTTR per IR plan tiers; both trending down | Per incident + quarterly trend |
| 7 | Alert true-positive rate | Confirmed-actionable ÷ total security alerts | ≥70% (noise discipline mirrors §10 doctrine) | Monthly |
| 8 | Privileged MFA strength | % privileged accounts on phishing-resistant MFA | 100% | Monthly |
| 9 | Recertification completion | % access reviews completed on schedule incl. revocations actioned ≤5d | 100% on time; revocations ≤5d | Quarterly |
| 10 | Break-glass events | Count of staff emergency-access events to C3–C5 data, each ticket-linked + customer-visible | Every event accounted for; trend flat/down; unexplained = finding | Monthly |
| 11 | Orphaned/stale accounts | Accounts active without owner attestation or beyond leaver SLA | 0 | Monthly |
| 12 | C3/C5 encryption coverage | % classified fields encrypted with tenant envelope keys | 100% | Continuous; verified monthly |
| 13 | Public-exposure findings | Internet-reachable storage/APIs/configs that should be private | 0 | Weekly external surface scan |
| 14 | Key-rotation currency | % keys within rotation window (workload certs, data keys, gateway certs) | 100% | Monthly |
| 15 | Device attestation pass rate | % field devices passing verdict tiering at sign-in, by fleet | ≥97%; failures auto-quarantined | Weekly |
| 16 | Device patch age | Mean days since OS/security patch across device fleets | ≤30d (≤90d hard ceiling per fleet) | Monthly |
| 17 | Kiosk-integrity violations | Attestation failures / tamper alerts per 1,000 device-months | Tracked per fleet; spikes trigger investigation | Weekly |
| 18 | Release-gate security findings | SAST/DAST/policy-test findings per release; % releases shipped with all §14 gates green | Gates-green rate 100%; findings trending down | Per release |
| 19 | Endpoint authorization-test coverage | % API endpoints with generated object-level authz tests passing | 100% | Per release |
| 20 | Secrets-in-build detections | Valid secrets detected in builds/repos | 0 | Continuous |
| 21 | Availability vs SLA | Measured uptime per tenant-facing service tier | ≥99.9% cloud core (per contract tiers) | Monthly |
| 22 | RTO/RPO achievement | Actual recovery point/time in quarterly restore tests vs objectives | 100% within objectives | Quarterly |
| 23 | Backup success rate | Completed + verified backup jobs ÷ scheduled | ≥99.5% | Weekly |
| 24 | Controls-green rate (registry) | % controls green with evidence inside freshness window | ≥98%; red blocks releases per §14.9 | Live; reported monthly |
| 25 | Audit findings aging | Open external/internal audit findings past remediation date | 0 overdue criticals/highs | Monthly |
| 26 | Training completion | % workforce completing security awareness + role-specific modules on schedule | 100% within grace period | Quarterly |
| 27 | Customer-audit outcomes | Findings raised in customer-led vendor audits of DDE; repeat-finding rate | Zero repeats; findings closed ≤30d | Per audit |
| 28 | Tier-1 supplier evidence currency | % tier-1 vendors with current SOC 2/ISO evidence on file | 100% | Quarterly |
| 29 | Model-governance coverage | % production models with current registry entry + evaluation artifacts (§17.4) | 100% | Per model release |
| 30 | AI-control violations | Agent-authority violations, prompt-injection test failures in prod | 0 | Continuous + quarterly injection-test suite |

**Metric governance:** definitions live in the controls-as-code registry (change-controlled like any control); breaches auto-create tracked actions with owners and due dates; the monthly scorecard goes to leadership and the quarterly pack drives the ISMS management-review agenda; a summarized, customer-shareable view (trends, not raw internals) lives in the trust center — metrics become sales evidence too.

# 12. Certification Application Calendar (ready-to-apply milestones)

With §11 operating, each accreditation reduces to scheduling and application. Indicative windows assume Phase 0 = months 0–3:

| Accreditation | Structure ready | Application window | Notes |
|---|---|---|---|
| SOC 2 Type I (Security·Availability·Confidentiality) | Day one (design evidence complete) | Month 3–4 | Design-phase attestation; often the first enterprise ask |
| Penetration test #1 (third party) | Month 2–3 | Month 3–4 | Pre-pilot gate; annual thereafter |
| SOC 2 Type II | After Type I | Observation window months 4–9 → report ~month 9–10 | Effectiveness period runs over real pilot traffic |
| ISO/IEC 27001:2022 Stage 1+2 | ISMS operating ≥3 months with records | Stage 1 month 4–5; Stage 2 month 6–8; certificate ~month 8–9 | Surveillance annually thereafter |
| BSI C5 audit | Post-27001 Stage 1 | Month 8–12 | German-market deals; same evidence engine |
| CSA STAR Level 1 → Level 2 | Registry + CCM mapping complete | Level 1 at launch; Level 2 after Type II | Low-cost registry visibility |
| ISO 27017 / 27018 add-ons | Same ISMS + SoA extensions | Months 9–12 | Ride the 27001 audit cycle |
| ISO 27701 privacy extension | Privacy-ISMS extension documented | After 27001 certificate | Strengthens GDPR posture claims |
| ISO 22301 business continuity | BC plan + exercised DR tests from Phase 0 | Month 12–18 | Needs demonstrated test history |
| ISO 9001 quality management | QMS documented alongside SDLC | Month 12+ | Optional early; matters to pharma/manufacturing buyers |
| SOC 1 Type II | Mode B write-back touching financial-reporting flows | Demand-triggered | When customer auditors require it |
| CRA conformity file (declaration + technical file) | Maintained current from Phase 0 | Statutory full application Dec 2027 | Reporting duties honored from launch |
| EU AI Act conformity documentation | Model-registry artifacts per §17.4 | Tracked against §15.13 risk-tier dates | Documentation-driven |
| ISASecure SDLA (OT components) | 62443-4-1 artifacts kept audit-current | Phase 2–3 | When OT-pack revenue justifies it |

Sequencing logic: buyer demand can pull items forward (a German pilot pulls C5; a pharma pilot pulls the GAMP validation package) — but nothing waits on engineering; everything above is paperwork-plus-scheduling against infrastructure that already operates.

# 13. Honest Limitations of Born-Compliance

Stated plainly so the sales narrative never overreaches:

1. **Operating-effectiveness windows cannot be skipped.** SOC 2 Type II and ISO 27001 require observed operation over time (~3–9 months). Born-compliance compresses *preparation* to near-zero, not the observation clock; certificates land months after launch, not on day one. Early pilots hear "implemented + audit scheduled," which mature buyers accept.
2. **Auditor lead times exist.** Accredited assessors book weeks-to-months out; slots are reserved early precisely so applying stays trivial.
3. **First-year audits cost more than steady state.** Initial certification fees plus remediation of auditor-found gaps are budgeted in Phases 0–1 as a named line item, declining sharply afterward.
4. **Some frameworks need operating history beyond structure** (ISO 22301 wants exercised BC plans; ISASecure wants mature defect-management metrics) — hence their later windows despite ready infrastructure.
5. **Parity ≠ maturity superiority.** SAP's controls have operated for decades; DDE launches with equivalent *structure*, fresher *mechanisms* (PQC-hybrid TLS, tenant-held keys, commercial-intelligence isolation), and younger operational history. The defensible claim is architectural parity-or-better with faster evidence cycles — not incumbent-surpassing maturity at launch.

# 14. Security Acceptance Criteria (gates, not aspirations)

A release cannot ship, and a deployment cannot go live, unless:

1. Threat model updated for every changed data flow; no unresolved high risks
2. Object-level authorization policy tests green for every touched endpoint
3. SBOM regenerated, zero known criticals in first-party image, exception list signed off
4. Secrets scan clean; no static credentials introduced
5. Attestation tiers verified on the release kiosk build (all three verdict classes behave per §7.3)
6. Audit-stream completeness check: sampled actions traceable end-to-end (actor → purpose → record)
7. Restore test passed for the release's data migrations
8. For Mode-B-affecting releases: fail-closed behavior demonstrated under injected fault conditions
9. Compliance-registry check: affected controls show green with fresh evidence in the §11.1 dashboard — no release may turn a control red without a signed exception
