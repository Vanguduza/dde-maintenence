# AECI Maintenance Operations System — Implementation Realisation Pack v1.0

**Status:** Engineering execution companion to `AECI_Maintenance_Operations_System_Master_Plan_v1.md`.
**Date:** 1 September 2026
**Purpose:** Convert the product source of truth into buildable bounded contexts, service contracts, screens, persistence rules, offline behavior, integration seams, test obligations and release increments.

---

# 1. Engineering Principles

1. **No customer code fork.** AECI behavior is enabled through DDE vertical/customer pack configuration, policy, seed data and adapters.
2. **Canonical identities.** Asset, component, person, site, stock item, work order, contract and document identities are shared across contexts.
3. **Append-only operational truth.** Corrections create superseding events/records; destructive history edits are prohibited for operational evidence.
4. **Safety state is explicit.** Safety/permit/LOTO requirements are domain objects and workflow gates, not free-text attachments.
5. **Observed vs derived data separation.** AI, forecasts and readiness computations cannot overwrite measured or human-recorded facts.
6. **Offline first.** Core field execution must continue without WAN connectivity.
7. **Adapter isolation.** External systems are only accessed through typed integration adapters.
8. **Idempotent commands/events.** Mobile retries, edge replay and connector retries may not duplicate operational outcomes.
9. **Explainability by construction.** Readiness, alerts, recommendations and KPI values expose their source facts.
10. **Configuration before customization.** Site-, model-, customer- and contract-specific differences are data/configuration wherever technically safe.

---

# 2. Bounded Context Map

| Context | Owns | References | Must not own |
|---|---|---|---|
| Asset Registry | assets, components, configurations, meters, installation/removal genealogy | site, document, supplier | work history, stock balances |
| Work Management | work requests, defects, WOs, job plans, task execution, tests | asset, person, safety, stock | person competency master, inventory master |
| Planning & Scheduling | backlog planning, schedule, capacity allocations | WO, roster, competency, stock reservations | WO truth, HR truth |
| Safety & Permit | risk assessments, PPE rules, isolation plans, permit refs, safety stops | asset, work, person | physical permit system state unless connector-sourced |
| Workforce & Competency | skills, trade, authorization, induction, medical/credential validity, roster eligibility inputs | person, site, asset class | payroll |
| Stores & Procurement | item master, stores, balances, reservations, issues/returns, PR/PO/GRN | work, asset, supplier | asset genealogy except serialized inventory state transition |
| Workshop & Repairables | workshop jobs, strip/inspect/rebuild/test/QA, repairable lifecycle | component, stock, supplier, work | master component identity |
| Reliability Engineering | failure analysis, RCA, PM optimization proposals, bad actors, reliability models | asset, work, condition, cost | raw work records |
| Fleet & Compliance | fleet legal credentials, road readiness overlays, vehicle-specific service data | asset, driver competency | generic work-order ownership |
| Contract & Service | contracts, SLA definitions, support commitments, blast windows, customer service risk | customer, site, asset, workforce | blast design/initiation |
| Condition Monitoring | telemetry channels, readings, quality, thresholds, edge ingestion | asset, meter | asset master |
| Documents & Engineering Change | controlled documents, approvals, engineering changes, applicability | asset model, job plan | binary storage implementation details |
| Incident/RCA/CAPA | incident shell, investigation, CAPA action orchestration | work, safety, asset, people | raw sensor truth |
| Reporting & Economics | KPI definitions, calculation snapshots, cost events/lineage | all canonical IDs | source-of-record operational edits |
| AI/RAG Intelligence | retrieval indexes, prompt policies, evals, recommendations | governed read models | system-of-record approvals |
| Integration & Edge | connector configs, sync cursors, edge buffers, dead-letter queues | all typed contracts | business rule ownership |

---

# 3. Repository/Code Structure Target

Reference layout for implementation inside the DDE codebase:

```text
packages/
  domain/
    asset-registry/
    work-management/
    planning-scheduling/
    safety-permit/
    workforce-competency/
    stores-procurement/
    workshop-repairables/
    reliability/
    fleet-compliance/
    contract-service/
    condition-monitoring/
    documents-engineering-change/
    incident-capa/
    reporting-economics/
  application/
    commands/
    queries/
    policies/
    orchestration/
  infrastructure/
    persistence/
    event-bus/
    object-storage/
    search/
    offline-sync/
    adapters/
      sap/
      telematics/
      silo-monitoring/
      identity/
      notifications/
  ai/
    retrieval/
    agents/
    evaluations/
  verticals/
    aeci-zimbabwe/
      manifest/
      asset-templates/
      failure-modes/
      job-plans/
      safety-policy/
      registers/
      dashboards/
      terminology/
apps/
  field/
  supervisor/
  planner/
  workshop/
  web-console/
  admin/
```

Actual language/framework paths may differ; ownership boundaries must remain equivalent.

---

# 4. Entity Specifications

## 4.1 Asset

Required fields:

- `id`
- `tenant_id`
- `site_id`
- `asset_class`
- `model_id`
- `serial_number?`
- `ownership_type`
- `owner_customer_id?`
- `criticality`
- `operational_state`
- `road_state?`
- `commissioned_at?`
- `retired_at?`
- `current_configuration_version`
- `source_system`
- `external_ids[]`
- `created_at`, `updated_at`

Unique constraints are tenant-scoped. Serial uniqueness is policy-driven because legacy estates can contain malformed duplicates requiring reconciliation.

## 4.2 Component

- `id`
- `component_type`
- `model_id`
- `serial_number?`
- `repairable_policy`
- `life_meter_type?`
- `warranty_expiry?`
- `current_status`
- `current_parent_asset_id?`
- `current_store_id?`

Invariant: a serialized component cannot be simultaneously installed on two assets.

## 4.3 WorkOrder

Core fields:

- `id`
- `work_type`
- `priority`
- `state`
- `asset_id`
- `component_id?`
- `defect_id?`
- `service_commitment_id?`
- `job_plan_revision_id?`
- `planned_start?`
- `planned_duration_minutes?`
- `actual_start?`
- `actual_end?`
- `failure_mode_id?`
- `cause_code_id?`
- `downtime_start?`
- `downtime_end?`
- `safety_profile_id`
- `planner_id?`
- `supervisor_id?`
- `verification_required`
- `source_system`
- `version`

## 4.4 Competency

- `person_id`
- `competency_type`
- `scope`: global/site/asset-class/model/task
- `level`
- `issued_at`
- `expires_at?`
- `issuer`
- `evidence_document_id?`
- `status`

## 4.5 ServiceCommitment

- `contract_id`
- `site_id`
- `window_start`
- `window_end`
- `required_asset_capabilities[]`
- `required_primary_count`
- `required_backup_count`
- `required_competencies[]`
- `critical_spares_profile_id?`
- `customer_reference?`
- `status`

---

# 5. Work Command Contracts

Commands are intention-bearing and validate policy before mutation.

## 5.1 `CreateWorkRequest`

Inputs:
- asset/component reference;
- symptom/description;
- requester;
- observed safety condition;
- evidence;
- source timestamp;
- idempotency key.

Outputs:
- work request ID;
- triage state;
- any immediate safety stop raised.

## 5.2 `ApproveWork`

Preconditions:
- approver authority;
- triage complete;
- work type/priority classified.

## 5.3 `PlanWork`

Requires planned labour profile, parts/tools, documents, safety requirements and estimated duration before `READY_TO_SCHEDULE` transition.

## 5.4 `AssignWork`

Policy evaluation:
- person is rostered/available;
- trade/competency valid;
- authorization valid;
- site induction/medical valid where configured;
- no conflicting assignment above capacity threshold.

Returns explicit failed predicates when assignment is blocked.

## 5.5 `StartWork`

Hard preconditions are generated from job/safety policy. Examples:
- mandatory permit reference present;
- required isolation verification recorded;
- required risk assessment accepted;
- assigned technician eligible;
- current approved job-plan revision available.

## 5.6 `CompleteWork`

Requires:
- task-step completion;
- mandatory measurements/evidence;
- parts consumption capture;
- failure/cause coding when configured;
- technician completion signature.

It may transition only to `TESTING` or `COMPLETED_PENDING_REVIEW`, not directly to `CLOSED` where verification is required.

## 5.7 `CloseWork`

Requires supervisor/reviewer authority and all mandatory verification hooks.

---

# 6. Safety Policy Engine

Safety requirements are resolved from layered policy:

1. legal/statutory hard requirements;
2. AECI corporate policy;
3. site policy;
4. asset/model safety profile;
5. job-plan requirements;
6. dynamically added task hazards.

Conflict resolution uses the stricter requirement unless an explicitly approved exception policy exists.

Example policy output:

```json
{
  "permit_reference_required": true,
  "isolation_plan_required": true,
  "loto_verification_required": true,
  "risk_assessment": "JSA",
  "ppe": ["chemical_gloves", "face_shield", "safety_glasses"],
  "competencies": ["process_pump_maintenance", "site_induction"],
  "hold_points": ["zero_pressure_verified", "line_flushed"]
}
```

The JSON above is illustrative; production identifiers are governed reference data.

---

# 7. Competency Eligibility Engine

`Eligibility(person, task, site, time)` returns:

- `eligible: boolean`
- `blocking_reasons[]`
- `warnings[]`
- `evidence_refs[]`
- `evaluated_at`
- `policy_version`

Blocking reasons must be deterministic and human-readable, such as:

- `SITE_INDUCTION_EXPIRED`
- `MEDICAL_EXPIRED`
- `MODEL_AUTHORIZATION_MISSING`
- `DRIVER_CLASS_INSUFFICIENT`
- `LOTO_AUTHORIZATION_EXPIRED`

The system may suggest eligible alternatives but cannot invent competence.

---

# 8. Readiness Engine

The readiness engine composes facts from multiple contexts.

## 8.1 Inputs

- primary asset state;
- backup asset state;
- open critical defects;
- maintenance overdue status;
- road/statutory status;
- crew eligibility;
- spares availability;
- service-window timing;
- site access/permit prerequisites if known;
- telemetry risk indicators;
- data freshness.

## 8.2 Hard-stop precedence

Any active hard safety/legal stop yields `BLACK` regardless of forecast score.

## 8.3 Deterministic risk rules

Examples:
- primary ready + backup unavailable => AMBER when contract requires backup;
- primary failed + eligible backup ready => AMBER or RED according to remaining capacity and SLA;
- required competent crew unavailable => RED;
- expired insurance for road deployment => BLACK for road use;
- stale telemetry alone cannot create BLACK.

## 8.4 Output

```json
{
  "state": "AMBER",
  "reasons": [
    {"code": "BACKUP_UNIT_UNAVAILABLE", "severity": "warning"}
  ],
  "facts": [...],
  "forecast": {...},
  "data_freshness": {...},
  "evaluated_at": "...",
  "rule_version": "..."
}
```

---

# 9. Stores and Repairable Contracts

## 9.1 Inventory operations

All inventory-affecting commands are ledgered:

- receive;
- inspect/accept;
- reserve;
- release reservation;
- issue;
- return;
- transfer dispatch;
- transfer receipt;
- adjustment;
- quarantine;
- scrap;
- move to repair;
- return from repair.

Balances are projections of ledger entries, not manually mutable counters.

## 9.2 Offline stock conflict

Mobile may record an intended issue while offline. On sync:

- if balance is sufficient, post issue;
- if balance is insufficient but policy allows negative provisional balance, create reconciliation exception;
- otherwise reject inventory posting but preserve field evidence and create supervisor/stores reconciliation task.

Never discard the technician's offline work record because the stock projection changed.

## 9.3 Serialized repairables

Status values:

`SERVICEABLE_STOCK`, `RESERVED`, `INSTALLED`, `FAILED`, `REMOVED`, `IN_TRANSIT`, `AWAITING_REPAIR`, `IN_REPAIR`, `AWAITING_TEST`, `QUARANTINED`, `SCRAPPED`.

Each transition emits a genealogy event.

---

# 10. Workshop API/Workflow Contracts

## 10.1 `ReceiveRepairable`
- validates component identity;
- records source asset/site;
- records contamination/safety handling state;
- captures reason for removal;
- creates workshop job.

## 10.2 `RecordStripInspection`
Captures measurements, photos, damage codes, reusable/scrap parts, probable failure mode and repair recommendation.

## 10.3 `ApproveRepairScope`
Applies authorization and cost threshold policy.

## 10.4 `RecordRebuildStep`
Tracks replaced parts, dimensions, torque, fitment values and technician identity.

## 10.5 `ReleaseRepairable`
Requires test results and QA authority where policy mandates. Produces a new serviceable state without erasing previous life history.

---

# 11. Reliability Contracts

## 11.1 Failure event creation

A `FailureEvent` is created from a breakdown or verified defect and references:
- asset/component;
- symptom;
- failure mode;
- cause;
- environmental/duty context;
- downtime;
- related WO;
- parts replaced;
- evidence.

## 11.2 RCA trigger policy

Configurable examples:
- safety-related failure;
- repeat same mode within N operating hours;
- downtime above threshold;
- high-cost event;
- customer SLA breach;
- regulatory event;
- management escalation.

## 11.3 PM change proposal

Reliability may propose changes but activation requires:
- engineering justification;
- affected model population;
- risk review;
- approver;
- effective date;
- prior revision retained.

---

# 12. Condition Monitoring Data Contract

Every reading carries:

- channel ID;
- asset/component/meter reference;
- source timestamp;
- ingest timestamp;
- value;
- unit;
- quality flag;
- source type (manual/PLC/CAN/gateway/import);
- source identifier;
- sequence/idempotency key where available.

Quality flags include:
- `GOOD`
- `STALE`
- `BAD_SENSOR`
- `OUT_OF_RANGE`
- `ESTIMATED`
- `MISSING_INTERVAL`

Estimated values are never silently presented as observed measurements.

---

# 13. Document Control and RAG Contract

Documents have lifecycle:

`DRAFT → REVIEW → APPROVED → EFFECTIVE → SUPERSEDED → ARCHIVED`.

RAG indexing rules:
- only approved/effective technical documents are eligible for primary technician guidance;
- superseded documents remain searchable only in audit/research contexts and are clearly labeled;
- document ACLs propagate to chunks/embeddings;
- chunk metadata includes document ID, revision, effective date, applicability and page/section reference;
- retrieval must prefer exact asset-model applicability before generic sources.

AI answer object stores:
- user query;
- retrieved source IDs;
- model/config version;
- response;
- confidence/uncertainty metadata;
- safety escalation flags;
- feedback/outcome when available.

---

# 14. Screen Inventory

## 14.1 Field app

1. Login/device unlock
2. Site/shift context
3. My shift
4. Assigned jobs
5. Start-of-shift inspection
6. Asset passport
7. Work job pack
8. Safety prerequisites
9. Isolation/LOTO verification
10. SOP/task steps
11. Measurement capture
12. Parts scan/issue
13. Troubleshooting copilot
14. Defect/breakdown report
15. Return-to-service test
16. Completion/signature
17. Shift handover
18. Offline sync/status
19. Safety stop/emergency escalation

## 14.2 Supervisor

1. Shift control board
2. Breakdown board
3. Crew/competency matrix
4. Work approval/triage
5. Assignment board
6. Safety/permit exceptions
7. Handover review
8. Deferred defects
9. Temporary repairs
10. Site readiness
11. Schedule compliance

## 14.3 Planner

1. Backlog
2. Job planning workspace
3. Ready backlog
4. Weekly schedule
5. Daily schedule
6. Labour/capacity board
7. Parts reservations/kitting
8. Compliance due work
9. Shutdown/campaign planner
10. Planning KPI dashboard

## 14.4 Workshop

1. Incoming repairables
2. Workshop routing board
3. Strip inspection
4. Repair scope approval
5. Rebuild workbench
6. External services queue
7. Testing/QA
8. Serviceable repairables
9. Dispatch
10. Turnaround/repeat-return analytics

## 14.5 Reliability

1. Reliability overview
2. Bad actors
3. Failure Pareto
4. Asset/component history explorer
5. RCA workspace
6. FMEA/FMECA
7. PM optimization
8. Engineering change pipeline
9. Life analysis
10. Cost of unreliability

## 14.6 Stores/procurement

1. Stock overview
2. Critical spares
3. Reservations/kits
4. Issue/return
5. Transfers
6. Repairables
7. Cycle count
8. Requisitions
9. RFQ/PO/receipts
10. Supplier performance

## 14.7 Control centre/web console

1. National readiness map/list
2. Asset state heatmap
3. Active breakdowns
4. Blast/service commitments
5. Compliance wallboard
6. Fleet road readiness
7. Workforce capacity
8. Critical spares exposure
9. SLA risk
10. Cost and reliability trends
11. Integration/edge health

---

# 15. Navigation and Cross-Linking Rules

Any operational object must expose contextual navigation without duplicating data.

Examples:
- asset → open work, history, components, documents, telemetry, costs, compliance;
- work order → asset, defect, person, safety, parts, evidence, service commitment;
- component → installation history, workshop history, failures, costs;
- person → competence, current assignments, training expiry;
- stock item → BOM usage, open reservations, supplier, failure consumption trend;
- service commitment → asset readiness, crew, parts, defects, SLA.

---

# 16. Notifications and Escalation

Notification policy is event-driven and configurable by severity/role/channel.

Candidate triggers:
- critical breakdown;
- readiness RED/BLACK transition;
- service window risk;
- safety stop;
- statutory credential approaching expiry;
- competency expiry causing future capacity gap;
- critical spare below threshold;
- overdue RCA/CAPA;
- repairable turnaround breach;
- sync/edge outage exceeding threshold.

Escalation must be rate-limited and de-duplicated. Repeated sensor samples must not create alert storms.

---

# 17. Audit and Evidence

Audit records include:

- actor/service identity;
- action;
- object;
- before/after references or event payload;
- timestamp;
- device/source;
- reason/comment where required;
- correlation ID;
- signature/evidence hash when applicable.

Evidence objects are immutable by default. Redaction or retention actions require explicit governance workflow.

---

# 18. Offline Sync Design

## 18.1 Mobile operation log

Each offline mutation records:
- local operation ID;
- command type;
- payload;
- local timestamp;
- actor;
- device;
- base object version where applicable;
- attachments pending upload.

## 18.2 Merge strategy classes

- **append-safe:** measurements, photos, comments, evidence;
- **optimistic-versioned:** work metadata, assignments;
- **ledger/reconciliation:** inventory;
- **authority-sensitive:** safety approvals, competency changes;
- **sequence-constrained:** component install/remove, workshop state.

No single global conflict algorithm is acceptable.

---

# 19. Integration Adapter Contract

Every adapter implements:

- `health()`
- `capabilities()`
- `pull(cursor)` where applicable
- `mapInbound()`
- `push(event/command)` where approved
- `idempotencyKey()`
- `retryPolicy()`
- `deadLetter()`
- `auditContext()`

Fixtures and simulators must exist for external systems whose credentials/contracts are not yet available. This keeps build and automated tests unblocked.

---

# 20. Security Controls

Minimum implementation controls:

- tenant isolation;
- least privilege;
- role + object scope + authority policy;
- device registration for field clients;
- encrypted local store;
- short-lived session tokens with offline-safe strategy defined by security architecture;
- secure attachment upload;
- tamper-evident audit events;
- secret isolation in connector runtime;
- RAG ACL propagation;
- no secrets in pack manifests;
- log redaction for credentials/tokens;
- backup/restore testing;
- privileged action monitoring.

---

# 21. Observability and SLOs

Track at minimum:

- API latency/error rate;
- event processing lag;
- sync success/failure;
- offline queue age;
- connector health;
- telemetry ingest lag;
- readiness calculation age;
- notification delivery;
- RAG retrieval latency and source-hit rate;
- AI evaluation failures;
- inventory reconciliation exceptions;
- audit pipeline completeness.

Safety/compliance-critical workflows receive dedicated alerts and dashboards.

---

# 22. Seed Configuration for AECI Zimbabwe

The vertical pack must ship with configurable seeds for:

- MMU/MCU/PCU/RRS/tanker/silo/EVDS/pump classes;
- initial component-tree templates;
- failure-mode starter library;
- Zimbabwe road-fleet credential types;
- explosives/storage/manufacturing register templates;
- AECI terminology and Zero Harm wording;
- baseline role templates;
- initial dashboard definitions;
- sample job-plan shells;
- sample safety policy shells;
- SLA/readiness rule templates.

All seeds are clearly marked `TEMPLATE/UNVERIFIED` until reviewed against real AECI data.

---

# 23. Migration Workbench

Provide staged import for:

- assets;
- components;
- people;
- competencies;
- PM schedules;
- work history;
- stock/items/BOMs;
- suppliers;
- documents;
- statutory credentials;
- workshop repairables;
- contracts/service commitments.

Workflow:

`UPLOAD → PARSE → MAP → VALIDATE → DEDUPLICATE → PREVIEW → APPROVE → COMMIT → RECONCILE`.

Imports are reversible at batch level through compensating records where safe; operational history is never silently rewritten.

---

# 24. Test Architecture

## 24.1 Unit tests

- state transitions;
- safety policy resolution;
- competency eligibility;
- readiness rules;
- inventory ledger math;
- repairable state machine;
- KPI formulas;
- document applicability;
- idempotency.

## 24.2 Integration tests

- work ↔ safety;
- work ↔ inventory;
- work ↔ competency;
- workshop ↔ component genealogy;
- service commitment ↔ readiness;
- telemetry ↔ condition alerts;
- document control ↔ RAG;
- offline sync ↔ server conflicts.

## 24.3 End-to-end tests

Automate the acceptance scenarios from the master plan using deterministic fixtures.

## 24.4 AI evaluations

Evaluation suites must test:
- retrieval relevance;
- current-revision preference;
- unsupported technical claim rate;
- correct safety escalation;
- stale/insufficient-data behavior;
- permission leakage;
- citation/source correctness;
- refusal to assert physical isolation/permit completion.

---

# 25. Delivery Epics

## Epic A1 — Tenant/site/customer foundation
## Epic A2 — Asset/component registry and genealogy
## Epic A3 — People/role/competency/authorization
## Epic A4 — Controlled documents and SOP distribution
## Epic B1 — Defect/work request lifecycle
## Epic B2 — Work planning/job plans
## Epic B3 — Safety/HIRA/permit/LOTO gates
## Epic B4 — Field execution and offline evidence
## Epic B5 — Test/return-to-service/review
## Epic C1 — Backlog/scheduling/capacity
## Epic C2 — Shift handover
## Epic C3 — Supervisor control board
## Epic C4 — Readiness engine/control centre
## Epic D1 — Inventory ledger and stores
## Epic D2 — Reservations/kitting
## Epic D3 — Procurement
## Epic D4 — Workshop routing
## Epic D5 — Repairable/rotable genealogy
## Epic E1 — Reliability metrics/bad actors
## Epic E2 — RCA/CAPA
## Epic E3 — PM optimization
## Epic E4 — Engineering change
## Epic F1 — Contract/SLA model
## Epic F2 — Service/blast-support commitments
## Epic F3 — Customer-impact economics
## Epic G1 — Edge telemetry contracts
## Epic G2 — Condition monitoring
## Epic G3 — Predictive validation
## Epic H1 — Governed RAG
## Epic H2 — Technician copilot
## Epic H3 — Planner/reliability/stores/compliance agents
## Epic H4 — Management briefing and AI evaluation operations

---

# 26. Engineering Gate Checklist

Every epic must demonstrate:

- schema migration reviewed;
- domain invariants unit-tested;
- API/command authorization tested;
- audit events emitted;
- telemetry/logging available;
- offline behavior documented where applicable;
- accessibility/rugged UX reviewed;
- failure/retry paths tested;
- fixture data supplied;
- documentation updated;
- acceptance tests linked;
- no direct external vendor calls from business domain code;
- security review complete for privileged/safety-impacting actions.

---

# 27. Build Order

Recommended build order preserving usable vertical slices:

1. identity/site/asset/component + document subset;
2. defect → work → safe execution → test/close;
3. competence eligibility + assignment;
4. planner/backlog/schedule + shift handover;
5. control centre/readiness with manual data;
6. stores/reservations + work consumption;
7. workshop/repairables;
8. reliability/RCA/PM changes;
9. contract/service commitments;
10. telemetry/condition monitoring;
11. RAG/copilots;
12. predictive models after sufficient validated history.

This order prevents AI/IoT from becoming prerequisites for basic operational value.

---

# 28. Coding-Agent Directive

A coding agent implementing AMOS must:

1. read the Master Plan and this Realisation Pack first;
2. map each change to one bounded context;
3. preserve canonical IDs and event contracts;
4. avoid introducing duplicate master data;
5. add tests before marking an epic complete;
6. use mock adapters for unavailable external contracts;
7. never infer safety/legal truth from absence of data;
8. preserve offline operation for field-critical flows;
9. expose sources for AI-generated technical guidance;
10. update the acceptance matrix whenever behavior changes.

Any architectural deviation must be documented as an ADR and explicitly state which invariant is being changed and why.
