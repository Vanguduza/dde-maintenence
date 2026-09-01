# AECI Maintenance — Enterprise Security, Data Protection & Records Standard v1.0

**Status:** Mandatory AECI AMOS security and records baseline
**Purpose:** Define the minimum security, privacy, document-protection and evidentiary controls for the AECI Maintenance Operations System (AMOS).
**Benchmark posture:** SAP SuccessFactors is used as a minimum enterprise benchmark for identity, role-based access, auditability, retention and encryption. AMOS must meet or exceed those control objectives where technically applicable to a maintenance platform.

---

# 1. Security Objective

AECI Maintenance handles operationally sensitive information: maintenance records, equipment condition, failures, blast-support data, safety events, near misses, employee activity, timesheets, permits, calibrations, site layouts, fleet data, procedures, manuals and potentially security-sensitive explosives-service information. The platform therefore adopts **security-by-default, least-privilege, zero-trust and records-integrity** principles from inception.

AMOS must never treat security as an admin-console feature added after implementation. Every bounded context, API, offline cache, generated PDF, search index, AI retrieval path and integration adapter inherits the same policy model.

---

# 2. SAP SuccessFactors Benchmark and AMOS Superset

Current SAP SuccessFactors platform capabilities used as benchmark include:

- suite-wide role-based permissions (RBP), including role/group/target-population controls;
- configurable data-retention management and purge workflows;
- read/change/general audit logging with configurable audit retention;
- encryption of stored data by default, with optional customer-managed/tenant-specific encryption keys;
- SSO via enterprise identity providers, commonly SAML 2.0;
- MFA, conditional/risk-based authentication through SAP Cloud Identity Services;
- TLS-protected communications and mTLS/X.509 options for service integrations;
- security-center management of keys, certificates, OAuth configurations and integration trust.

AMOS treats these as a floor, not a ceiling.

## 2.1 AMOS controls that deliberately go beyond the benchmark

1. **RBAC + ABAC + object scope + competency separation.** Role permission is necessary but not sufficient. Access can also depend on tenant, business unit, site, asset responsibility, employment/contract status, work assignment, data classification, time-bound elevation and technical authorization.
2. **Per-record and per-field classification.** Data classes drive access, offline eligibility, exportability, retention and AI-indexing rules.
3. **Append-only security audit stream.** Security-relevant events are written to an immutable audit/event substrate; administrators cannot silently rewrite history.
4. **Content-addressed records.** Controlled donor PDFs, generated reports and evidence objects are hashed; signatures bind user identity, intent, timestamp, object revision and hash.
5. **Dual-control for destructive/high-risk administration.** Security-policy changes, retention-policy reductions, mass export, legal-hold release, encryption-key changes and high-impact privilege grants can require maker-checker approval.
6. **Offline security parity.** Cached field data remains encrypted and policy-scoped; offline mode is not a weaker security mode.
7. **Device trust.** Managed tablets can enforce PIN/biometric/device encryption, kiosk restrictions, application attestation, compromised-device blocking, remote session/token revocation and data wipe policies.
8. **AI security propagation.** RAG/search results inherit source ACLs and classification. AI cannot use inaccessible documents to answer an otherwise permitted user.
9. **No silent purge.** Retention/purge produces auditable preview, authorization and completion records and respects legal holds/evidence preservation.
10. **Evidence-grade document lineage.** Every submitted maintenance form can prove donor-template version, data payload, renderer version, signer(s), source job/asset and generation time.

---

# 3. Security Architecture Principles

## 3.1 Zero-trust

Every request is evaluated on:

`identity + authenticated session + device posture + role + scope + object relationship + data classification + requested action + current authorization + contextual policy`

Network location alone never grants trust.

## 3.2 Least privilege

- deny by default;
- minimum role bundles;
- site-scoped access by default for field teams;
- enterprise/regional visibility only where required;
- just-in-time elevation for exceptional administrative actions;
- automatic expiry of temporary grants;
- periodic access recertification;
- orphaned access removed when role/site/employment status changes.

## 3.3 Segregation of duties

Examples:

- technician executes; configured QA/supervisor verifies where independence is required;
- requester cannot self-approve selected purchases;
- tool custodian cannot conceal audit exceptions;
- security administrator cannot delete audit evidence;
- retention-policy approver is distinct from policy editor for high-impact changes;
- mass export can require independent approval.

---

# 4. Identity, Authentication and Federation

## 4.1 Enterprise identity first

AMOS should integrate with AECI's approved enterprise identity provider rather than creating a separate unmanaged identity island. Supported architecture seams include:

- SAML 2.0;
- OIDC/OAuth 2.0;
- SCIM or approved provisioning APIs;
- SuccessFactors/HR directory adapter where contract/API access permits.

External identity integration is adapter-based and may be simulated during development.

## 4.2 Authentication controls

Configurable baseline:

- enterprise SSO;
- MFA for privileged roles and optionally all users;
- phishing-resistant MFA where identity provider/device support permits;
- step-up authentication for sensitive actions;
- session risk checks;
- secure password policy only for break-glass/local fallback accounts;
- short-lived access tokens;
- refresh-token rotation;
- immediate token/session revocation;
- account disable propagation;
- brute-force/rate-limit defenses;
- anomalous login detection.

## 4.3 Service-to-service identity

Prefer:

- workload identities;
- mTLS/X.509;
- short-lived credentials;
- scoped OAuth client credentials;
- secret rotation;
- no long-lived credentials embedded in mobile apps or source code.

---

# 5. Authorization Model

Authorization is evaluated across layers:

1. tenant;
2. business unit;
3. site;
4. department/team;
5. role;
6. job assignment;
7. asset responsibility (`my assets`);
8. data classification;
9. competency/authorization;
10. action (`view`, `create`, `edit`, `approve`, `export`, `delete/purge`, `administer`);
11. current object state.

Examples:

- a technician can see maintenance data for assets assigned to their current site/team but not unrestricted national records;
- an artisan can execute an authorized job but cannot approve their own independent QA checkpoint if policy requires separation;
- a site supervisor can view team performance at their site but cannot automatically view unrelated HR data;
- a blast module user needs both site assignment and applicable role/authorization;
- records classified as security-sensitive may be excluded from offline storage or AI indexing.

---

# 6. Data Classification

Minimum classes:

| Class | Example | Default handling |
|---|---|---|
| PUBLIC | approved public material | ordinary controls |
| INTERNAL | routine non-sensitive operating data | authenticated AECI access |
| CONFIDENTIAL | maintenance history, employee timesheets, commercial/SLA data | scoped access, encrypted, export controlled |
| RESTRICTED | near-miss investigations, security-sensitive plant/site information, certain blast/service data | strict need-to-know, limited offline/export, enhanced audit |
| HIGHLY_RESTRICTED | credentials, cryptographic material, security administration, legally protected evidence | dedicated stores/keys, no normal user export, dual control where appropriate |

Classification is stored as machine-readable policy metadata, not a visual label only.

---

# 7. Encryption and Key Management

## 7.1 In transit

- TLS 1.3 preferred; current approved secure TLS baseline enforced;
- HSTS for web surfaces;
- certificate validation and rotation;
- mTLS for high-trust integration channels where feasible;
- no plaintext operational API traffic.

## 7.2 At rest

- encrypted primary database;
- encrypted object/document storage;
- encrypted backups;
- encrypted search/vector indices where technology permits;
- encrypted device/local offline databases using platform secure storage/key hardware;
- envelope encryption for sensitive blobs;
- tenant/data-class key separation where architecture supports it.

## 7.3 Key management

Target architecture supports:

- KMS/HSM-backed keys;
- rotation;
- versioned keys;
- separation between data keys and key-encryption keys;
- BYOK/customer-managed key option where hosting model and AECI security governance require it;
- cryptographic deletion option for selected isolated datasets only where lawful and compatible with retention requirements;
- complete key administration audit trail.

---

# 8. Document and Record Integrity

Every controlled record supports a provenance chain:

`donor template hash + donor revision + form schema version + coordinate map hash + submitted structured payload hash + evidence hashes + signer identity + timestamps + renderer version + generated PDF hash`

## 8.1 Immutable donor originals

Original AECI donor PDFs are retained unchanged in a controlled template vault. They are never overwritten. A replacement becomes a new template revision.

## 8.2 Generated record immutability

Once finalized/signed:

- report content becomes immutable;
- corrections occur through governed amendment/superseding record rather than editing history;
- original payload and rendered PDF remain linked;
- audit trail records who viewed/exported/changed metadata where applicable.

## 8.3 Evidence

Photos, signatures, calibration certificates, attachments and other evidence are stored as content-addressed objects where practical. Deletion follows retention/legal-hold policy.

---

# 9. Audit Logging

Security and business audit streams cover at least:

- login/logout/authentication failure;
- MFA/step-up events where exposed by IdP;
- role/permission/scope changes;
- privilege elevation;
- record view for restricted classes where required;
- create/update/approve/sign/close/reopen;
- export/print/download;
- donor-template publish/retire;
- retention/hold/purge actions;
- integration authentication/configuration changes;
- encryption/certificate/key administration;
- AI retrieval and high-risk assistant actions;
- offline sync conflict/reconciliation;
- device registration/revocation;
- bulk operation.

Audit event requirements:

- timestamp;
- actor/workload identity;
- tenant/site scope;
- action;
- object/type;
- previous/new state reference where appropriate;
- device/session/request correlation;
- reason/approval reference for privileged actions;
- tamper-evident storage.

---

# 10. Retention, Legal Hold and Purge

Retention policies are per record class and jurisdiction/customer requirement, not one global duration.

Required features:

- retention schedule registry;
- minimum/maximum policy limits;
- effective-date versioning;
- legal/evidence hold;
- purge preview;
- maker-checker approval for sensitive purge classes;
- immutable purge request/result log;
- cryptographic/document lineage retained to the extent permitted after purge;
- backup-expiry alignment;
- search/vector index purge propagation;
- offline-device purge propagation;
- AI-derived caches removed with source when policy requires.

The platform must support retaining AECI forms for the exact periods prescribed by AECI policy, contract, law or audit requirements once supplied.

---

# 11. Backup, Recovery and Resilience

Minimum production controls:

- encrypted backups;
- point-in-time recovery for transactional stores where supported;
- geographically appropriate redundancy;
- defined RPO/RTO by data class/service tier;
- quarterly restore testing minimum unless AECI requires more frequent tests;
- immutable/isolated backup tier for ransomware resilience;
- documented disaster-recovery exercises;
- backup access separated from production administrators where practical;
- donor-template vault and finalized records included in recovery validation.

A backup that has never been restored successfully does not count as a verified recovery control.

---

# 12. Mobile/Offline Security

Field offline requirements must not weaken enterprise security.

Controls include:

- OS/device encryption required;
- application secure storage;
- encrypted local database;
- application-scoped document cache;
- no shared external-storage plaintext files;
- local data subset restricted to assigned jobs/assets/forms;
- configurable offline TTL;
- remote token/session revocation;
- remote app data wipe when managed-device infrastructure supports it;
- compromised/rooted-device policy;
- screen capture/export restrictions for selected classifications where platform policy permits;
- biometric/device PIN protected re-entry;
- attachment sanitization;
- secure local log redaction;
- background sync with authenticated, idempotent operations.

---

# 13. Secure PDF/Form Engine Controls

Donor PDFs are untrusted input until validated.

- parsing/rendering in sandboxed resource-limited workers;
- malware/static checks where available;
- no active JavaScript/macros/embedded executable content carried into production templates;
- no passthrough of untrusted embedded objects into generated reports;
- coordinate-map/schema validation;
- template, map and schema signing/hashing;
- render workers granted access only to required tenant/template/output prefixes;
- output regenerated from known donor page graphics + structured values;
- renderer has no general database access;
- generation is deterministic where fonts/render stack allow;
- generated PDF and structured payload are both retained;
- fidelity/pixel-regression tests mandatory before template publication.

---

# 14. DLP, Export and Sharing Controls

Configurable per data class:

- export permission separate from view permission;
- watermarking of non-final/confidential exports where appropriate;
- signed/final record indication;
- bulk export limits;
- dual approval for high-volume/high-classification export;
- expiring signed links rather than public URLs;
- no anonymous document buckets;
- e-mail/notification messages should avoid sensitive payloads and deep-link to authenticated records;
- clipboard/share restrictions on managed devices where supported;
- export audit.

---

# 15. Notifications and Privacy

Notifications contain minimum necessary information.

Example push notification:

`PM due for MMU-014 tomorrow — open AMOS`

not a sensitive technical failure dump on a lock screen.

User/site policy controls push, e-mail and in-app notification channels. Restricted details require authenticated application access.

---

# 16. AI/RAG Security

- ACL-aware retrieval;
- classification-aware indexing;
- tenant/site isolation;
- prompt/output logging policy with sensitive-data minimization;
- no unrestricted embedding of HIGHLY_RESTRICTED content;
- source citations/revision identity for technical guidance;
- superseded controlled documents excluded from primary guidance;
- no external model provider receives AECI data unless explicitly approved under contract/policy;
- local/self-hosted model option for restricted workloads;
- prompt injection/document poisoning defenses;
- tool invocation subject to the same authorization layer as UI/API calls;
- AI cannot bypass approval workflows.

---

# 17. Security Administration and Evidence

Security admin surface must provide:

- permission-role and scope matrix;
- privileged-account list;
- access recertification;
- device inventory;
- active sessions/tokens where available;
- certificate/key expiry dashboard;
- integration credentials/trust posture;
- audit search;
- retention/hold dashboard;
- bulk export/purge history;
- security alerts;
- backup/restore verification status;
- vulnerability/dependency posture;
- security-policy version history.

---

# 18. Secure SDLC

Required engineering controls:

- protected branches and reviewed PRs;
- mandatory automated tests for authorization boundaries;
- dependency scanning;
- secret scanning;
- SAST;
- infrastructure-as-code scanning where applicable;
- SBOM generation;
- signed release artifacts where deployment chain supports it;
- production configuration change history;
- vulnerability remediation SLOs by severity;
- penetration testing before production and periodically thereafter;
- threat modeling for high-risk domains (identity, offline, PDF parser, RAG, blast records, integrations);
- no production secrets in repository;
- test data must not be uncontrolled copies of sensitive production records.

---

# 19. External Standards Target

AMOS should be architected to support evidence required for enterprise control frameworks such as:

- ISO/IEC 27001-aligned ISMS controls;
- ISO/IEC 27017 cloud-security practices where cloud deployed;
- ISO/IEC 27018 privacy controls where personal data is processed in public cloud;
- SOC 2 trust-service criteria evidence where commercial strategy requires attestation;
- OWASP ASVS/MASVS-aligned application/mobile security;
- applicable Zimbabwe data-protection requirements and AECI internal policies;
- customer-mine contractual/security requirements.

Architecture alignment does not constitute certification; certification/attestation requires formal external processes.

---

# 20. Non-Negotiable Security Acceptance Rules

1. No user can access another site/tenant's restricted record merely by guessing an ID.
2. Revoked role/site access stops new access immediately and removes offline eligibility.
3. Finalized records cannot be silently edited.
4. Every finalized PDF is verifiably linked to its exact donor revision and structured payload.
5. A privileged administrator cannot erase the security audit trail through normal product APIs.
6. Export is separately authorized and audited.
7. Legal hold blocks purge.
8. AI retrieval cannot surface documents the requesting user could not access directly.
9. Offline cache is encrypted and scope-limited.
10. High-risk administrative changes are auditable and can require dual approval.
11. Donor-PDF parsing occurs in a sandbox and active/untrusted content is not propagated to generated records.
12. Backup restore must be demonstrated, not assumed.
