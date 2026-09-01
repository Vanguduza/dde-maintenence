# AECI Maintenance Operations System — Engineering Backlog Map v1.1

**Date:** 1 September 2026
**Tracking issue:** #1
**Purpose:** Provide a stable issue/epic map from the AMOS source of truth into implementation work, including the mandatory cross-phase tracks added for full DDE capability inheritance, AECI enterprise security/records, donor PDF fidelity, and AECI field/blast operations.

---

# 1. Programme Issues

## Core phases
- **#3 Phase A — Foundation and master data**
- **#4 Phase B — Safe work execution**
- **#5 Phase C — Planning, shifts and control centre**
- **#6 Phase D — Stores, procurement, workshop and repairables**
- **#7 Phase E — Reliability, RCA and engineering change**
- **#8 Phase F — Contracts, SLA and blast-support readiness**
- **#9 Phase G — Telemetry, condition monitoring and predictive intelligence**
- **#10 Phase H — Governed RAG and maintenance copilots**

## Mandatory cross-phase tracks
- **#11 — Full DDE Maintenance capability inheritance**
- **#12 — Enterprise security, data protection and records hardening**
- **#13 — Donor PDF forms and records fidelity engine**
- **#14 — Site assets, three-source work model, notifications and surface blast reporting**

---

# 2. Cross-Phase Epic Decomposition

## X1 — DDE Capability Inheritance (#11)
Authority: `AECI_Maintenance_DDE_Full_Capability_Inheritance_Spec_v1.md`

Every applicable generic DDE Maintenance capability is inherited unless explicitly excluded through governance.

## X2 — Enterprise Security & Records (#12)
Authority: `AECI_Enterprise_Security_Data_Protection_Records_Standard_v1.md`

- X2.1 enterprise identity federation/provisioning seam;
- X2.2 MFA/step-up integration;
- X2.3 RBAC + ABAC + site/object/data-class policy engine;
- X2.4 encryption of database/object/backups/offline cache;
- X2.5 KMS/key/certificate/workload identity;
- X2.6 tamper-evident audit;
- X2.7 retention/legal hold/purge governance;
- X2.8 export/DLP controls;
- X2.9 managed-device/offline revocation controls;
- X2.10 ACL/classification-aware RAG;
- X2.11 backup/DR/restore verification;
- X2.12 secure SDLC/security testing.

## X3 — Donor PDF Forms & Fidelity (#13)
Authority: `AECI_Donor_PDF_Forms_Records_Fidelity_Engine_v1.md`

- X3.1 donor vault/intake/quarantine/hash;
- X3.2 sandbox parser;
- X3.3 schema extraction/annotation;
- X3.4 coordinate-map editor;
- X3.5 generic web/mobile capture renderer;
- X3.6 auto-population/context binding;
- X3.7 controlled expression/calculation engine;
- X3.8 signatures/approvals;
- X3.9 donor-layout PDF renderer;
- X3.10 structured payload + PDF records vault;
- X3.11 golden/pixel fidelity CI;
- X3.12 revision/supersession lifecycle.

Initial families: maintenance job cards, timesheets, scheduled maintenance, trip tests, calibrations, daily vehicle checks, equipment inspections, Autonomous Maintenance, unusual occurrences, near misses, HIRA/JSA, tool audits, breakdown reports, and blast records/reports.

## X4 — Field Assets, Work Origins, Notifications & Blast (#14)
Authority: `AECI_Field_Operations_Assets_Work_Notifications_Blast_Module_v1.md`

- X4.1 per-site asset register;
- X4.2 asset passport and manuals/history;
- X4.3 technician postings/responsibility/My Assets;
- X4.4 scheduled/planned work origin;
- X4.5 technician breakdown origin;
- X4.6 Autonomous Maintenance origin;
- X4.7 supervisor/management-created origin;
- X4.8 obligation/notification engine;
- X4.9 surface blast-event identity;
- X4.10 charge-per-hole donor capture;
- X4.11 density/quality tracker;
- X4.12 blast event logger;
- X4.13 equipment/service metrics;
- X4.14 breakdown ↔ blast ↔ maintenance linkage;
- X4.15 consolidated donor blast report.

---

# 3. Core Phase Decomposition

## Phase A — Foundation & Master Data (#3)

### A1 Tenant/customer/site foundation
- tenant/business-unit/customer/site hierarchy;
- site connectivity/hazardous-area metadata;
- object scope/canonical external IDs;
- data-classification metadata.

### A2 Site asset/component registry
- per-site asset register;
- asset classes/templates;
- image/serial/state/criticality;
- component tree/versioning;
- install/remove genealogy;
- meter definitions;
- manuals/procedure applicability;
- asset responsibility assignment;
- technician posting;
- import/reconciliation.

### A3 Workforce identity/competence
- person master references;
- role templates;
- competency/authorization;
- expiry/status lifecycle;
- eligibility service.

### A4 Controlled documents/forms foundation
- document/revision lifecycle;
- donor-document identity;
- form-schema/coordinate-map objects;
- applicability;
- classification/retention;
- offline eligibility.

### A5 Audit/import/security foundation
- append-only audit events;
- evidence objects;
- record hashes/provenance;
- batch migration workbench;
- reconciliation queue.

Exit: Phase A plus applicable SEC/PDF/ASSET P0 gates.

## Phase B — Safe Work Execution (#4)

### B1 Work origin gateway
- `SCHEDULED_PLANNED`;
- `TECHNICIAN_BREAKDOWN`;
- `TECHNICIAN_AUTONOMOUS_MAINTENANCE`;
- `SUPERVISOR_MANAGEMENT_CREATED`;
- immutable source provenance.

### B2 Digital Job Card Pack
WO + approved procedure/job plan + HIRA/JSA + PPE + permit + LOTO/isolation + competency + tools/test equipment + parts + drawings/manuals + evidence + testing + return-to-service verification.

### B3 Field execution/offline
- My Work;
- My Assets subset;
- donor-form capture;
- measurements/evidence/signatures;
- pause/wait reasons;
- idempotent sync/conflict handling.

### B4 Repair quality
- functional test;
- return to service;
- follow-up verification;
- suspected rework;
- technical escalation.

Exit: WORKSRC/JCP/SAFE/RWK/RTS/FIELD/PDF P0 gates.

## Phase C — Planning, Shifts, Notifications & Control Centre (#5)

### C1 Backlog/readiness
- job-pack completeness;
- competent labour;
- parts/tools/calibration;
- access/travel/service-window constraints.

### C2 Scheduling
- weekly/daily boards;
- assignments/workload.

### C3 Shift handover
- unfinished jobs;
- isolations/permits;
- temporary repairs;
- abnormal states.

### C4 Notifications/obligations
- PM/report/calibration/checklist/timesheet/trip-test due;
- assignment/breakdown;
- parts/tool ready;
- follow-up/deferred review;
- competency/tool/compliance expiry;
- approvals/near miss/unusual occurrence;
- recurrence/readiness/blast-service risk;
- privacy-minimised channels.

### C5 Technician/team performance
- explainable scorecards;
- context/difficulty/delay normalization;
- rework adjudication dependency;
- coaching/development.

### C6 Maintenance Control Centre
- multi-site asset/readiness;
- obligations;
- breakdown/work states;
- service risk.

Exit: PLAN/SHIFT/KPI/NOTIF/READY/SEC P0 gates.

## Phase D — Stores, Procurement, Workshop, Tools & Calibration (#6)

- item/BOM master;
- inventory ledger;
- reservations/kitting/issues/returns;
- procurement;
- workshop intake/rebuild/test/QA;
- repairables/rotables;
- tool crib/custody;
- toolbox audits;
- calibration/inspection;
- out-of-tolerance impact reconstruction;
- rework cost lineage.

Exit: STORE/WSHOP/TOOL/RWK/SEC P0 gates.

## Phase E — Reliability, RCA, Knowledge & Engineering Change (#7)

- KPI/reliability engine;
- recurrence/bad actors;
- maintenance-induced failure;
- NFF escalation;
- RCA/FMEA/CAPA;
- PM/job-plan optimization;
- engineering change;
- calibration impact follow-up;
- knowledge capture/controlled promotion.

Exit: REL/REC/MIF/NFF/KNOW/CAL/SEC P0 gates.

## Phase F — Contracts, SLA & Surface Blast Reporting (#8)

### F1 Contract/service model
- contract/SLA definitions;
- service windows;
- readiness/consequence lineage.

### F2 Surface blast module
- authorized blast event;
- charge-per-hole records;
- density/quality tracker;
- event log;
- equipment/service metrics;
- maintenance breakdown linkage;
- approved derived metrics only;
- consolidated donor PDF blast report.

Blast functionality is operational reporting/quality/maintenance integration, not an uncontrolled blast-design system.

Exit: READY/KPI/BLAST/PDF/SEC P0 gates.

## Phase G — Condition Monitoring & Predictive Intelligence (#9)

- manual condition readings;
- edge buffering;
- PLC/CAN/J1939 adapters;
- quality/freshness;
- failure/rework correlation;
- predictive pilots;
- model validation/monitoring.

Exit: OT/READY/REC/SEC P0 gates.

## Phase H — Governed RAG & Copilots (#10)

- ACL/classification-aware indexing;
- current revision/applicability filtering;
- job-pack-aware technician support;
- planner/reliability/stores/compliance agents;
- authorized field/blast record retrieval;
- management briefing;
- evaluation/prompt-injection defenses.

Exit: AI/SEC/KNOW/ESC P0 gates.

---

# 4. Dependency Rules

- B requires A canonical identities, asset/posting truth and controlled documents.
- X2 security controls bind every phase and are never deferred as cosmetic hardening.
- X3 donor engine starts in A/B and is consumed by every form-producing module.
- X4 asset/work origin foundations begin in A/B; notification orchestration becomes operational in C; blast reporting becomes productized in F.
- C requires B work-state truth and A competence/posting data.
- D can proceed after B core WO identity but integrates with tools/work/component genealogy.
- E can build against deterministic fixtures before significant production history exists.
- F requires C readiness and donor-form engine; exact blast formulas/limits remain customer-configured.
- G must not block B/C/D.
- H requires controlled documents and ACL/classification infrastructure; AI never blocks core rollout.

---

# 5. Story Template

Every implementation story contains:

- bounded context;
- user role;
- operational problem;
- command/query/event;
- invariant;
- permission/competency rule;
- data classification;
- offline behavior;
- audit/evidence requirement;
- donor-document impact;
- acceptance IDs;
- observability;
- adapter/mock requirement;
- definition of done.

---

# 6. PR Template Expectations

Every AMOS implementation PR states:

1. phase/epic/story;
2. affected contexts;
3. source specifications;
4. schema/API/event changes;
5. security/authorization/data-class impact;
6. offline/conflict impact;
7. donor-template/rendering impact;
8. acceptance IDs;
9. test evidence;
10. migration impact;
11. ADR if required;
12. assumptions/fixtures/deferred customer configuration.

---

# 7. External Inputs That Do Not Block Core Coding

Represent through configuration, fixtures and adapters until supplied:

- real AECI asset census/models/BOMs;
- actual site rosters/postings;
- approved donor PDFs/revisions;
- real PM intervals;
- trip-test/calibration values;
- actual blast/quality formulas and limits;
- repair manuals/SOPs;
- historical breakdown data;
- live stores item master;
- exact competency matrix;
- statutory credentials;
- host permit/LOTO formats;
- customer SLA clauses;
- AECI identity/SuccessFactors integration endpoint details;
- exact retention/classification policies;
- telemetry/security/silo APIs;
- approved production RAG corpus.

Production activation remains gated by customer-approved evidence, but engineering proceeds against versioned internal contracts and fixtures.

---

# 8. Definition of Done

No epic/module is complete unless:

- applicable P0 tests pass;
- P1 passes or has approved mitigation;
- authorization/data-class boundaries are tested;
- offline behavior is tested where applicable;
- donor-record fidelity tests pass where controlled forms are produced;
- audit reconstruction is possible;
- customer-specific values that remain unverified are clearly marked;
- unavailable external APIs/contracts are represented by adapters/fixtures rather than omitted functionality.
