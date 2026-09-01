# AECI Maintenance Operations System — Engineering Backlog Map v1.0

**Date:** 1 September 2026
**Tracking issue:** #1
**Purpose:** Provide a stable issue/epic map from the AMOS source of truth into implementation work.

---

# 1. Programme Issues

- **#3 Phase A — Foundation and master data**
- **#4 Phase B — Safe work execution**
- **#5 Phase C — Planning, shifts and control centre**
- **#6 Phase D — Stores, procurement, workshop and repairables**
- **#7 Phase E — Reliability, RCA and engineering change**
- **#8 Phase F — Contracts, SLA and blast-support readiness**
- **#9 Phase G — Telemetry, condition monitoring and predictive intelligence**
- **#10 Phase H — Governed RAG and maintenance copilots**

---

# 2. Epic Decomposition

## Phase A

### A1 Tenant, customer and site foundation
- tenant/business-unit/customer/site hierarchy;
- site attributes/connectivity/hazardous-area metadata;
- object scoping and canonical external IDs.

### A2 Asset/component registry
- asset classes/templates;
- component tree/versioning;
- installation/removal genealogy;
- meter definitions;
- import/reconciliation.

### A3 Workforce identity and competence
- person master references;
- role templates;
- competency/authorization records;
- expiry/status lifecycle;
- eligibility query service.

### A4 Controlled documents
- revision lifecycle;
- applicability;
- offline distribution subset;
- audit/version retention.

### A5 Platform audit/import foundation
- audit events;
- evidence objects;
- batch migration workbench;
- reconciliation queue.

## Phase B

### B1 Defect/work request
### B2 Work-order state machine
### B3 Job plans and task steps
### B4 Safety policy resolution
### B5 HIRA/JSA and PPE
### B6 Permit reference and LOTO/isolation
### B7 Technician field execution
### B8 Offline operation log/sync
### B9 Return-to-service and supervisor review
### B10 Failure/downtime coding

## Phase C

### C1 Backlog quality gates
### C2 Labour/capacity model
### C3 Weekly/daily schedule
### C4 Digital shift handover
### C5 Supervisor control board
### C6 Maintenance Control Centre
### C7 Readiness engine and explanations
### C8 Alert/escalation policy

## Phase D

### D1 Item/BOM master
### D2 Inventory ledger
### D3 Reservations and kitting
### D4 Issue/return/transfer
### D5 Critical-spares intelligence
### D6 PR/RFQ/PO/receipt workflow
### D7 Supplier performance
### D8 Workshop intake/routing
### D9 Strip/inspection/rebuild
### D10 Test/QA release
### D11 Repairable/rotable lifecycle
### D12 Repair-vs-replace analytics

## Phase E

### E1 Reliability KPI engine
### E2 Bad-actor/failure Pareto
### E3 RCA workspace
### E4 CAPA orchestration
### E5 PM optimization/versioning
### E6 Engineering change control
### E7 Calibration lifecycle/impact reconstruction
### E8 Effectiveness verification

## Phase F

### F1 Contract/customer service model
### F2 SLA/KPI definition/versioning
### F3 Blast-support/service commitment object
### F4 Primary/backup asset requirements
### F5 Crew/material readiness
### F6 Customer-impact timeline
### F7 Cost-of-unreliability/contract consequence lineage

## Phase G

### G1 Manual condition readings
### G2 Edge buffering/sync
### G3 PLC/CAN/J1939 adapter contracts
### G4 Telemetry quality/freshness
### G5 Threshold/anomaly rules
### G6 Predictive pilot framework
### G7 Model validation/monitoring

## Phase H

### H1 Governed document indexing
### H2 Retrieval applicability/ACL rules
### H3 Technician troubleshooting copilot
### H4 Planner agent
### H5 Reliability agent
### H6 Stores agent
### H7 Compliance agent
### H8 Management briefing agent
### H9 AI evaluation/feedback operations

---

# 3. Dependency Rules

- B requires A canonical identities and controlled documents.
- C requires B work-state truth and A competence data.
- D can proceed after B core WO identity but must integrate with work and component genealogy.
- E requires enough B/D operational history for meaningful calculations, but schema/UI can be built against deterministic fixtures.
- F requires C readiness orchestration and D material truth.
- G requires A asset/meter identity; it must not block B/C/D.
- H requires controlled documents plus B/E read models; AI does not block core maintenance rollout.

---

# 4. Story Template

Every implementation story should contain:

- bounded context;
- user role;
- operational problem;
- command/query/event affected;
- data invariant;
- permission/competency rule;
- offline behavior if field-relevant;
- audit/evidence requirement;
- acceptance IDs;
- observability requirement;
- external adapter/mock requirement;
- definition of done.

---

# 5. PR Template Expectations

Every AMOS implementation PR should state:

1. phase/epic/story;
2. affected bounded contexts;
3. schema/API/event changes;
4. security/RBAC implications;
5. offline/conflict implications;
6. acceptance IDs implemented;
7. test evidence;
8. migration impact;
9. ADR link if architectural boundary/invariant changed;
10. known gaps/deferred items.

---

# 6. External Inputs That Do Not Block Coding

These are represented through configuration, fixtures and adapters until supplied:

- real AECI asset census/models/BOMs;
- actual PM intervals;
- historical breakdown data;
- workshop repair rules;
- live stores item master;
- exact competency matrix;
- exact statutory credentials;
- host permit formats;
- customer SLA clauses;
- telemetry/security/silo vendor APIs;
- approved technical documents for production RAG.

Production activation of affected configuration remains gated by customer-confirmed evidence, but engineering implementation proceeds against versioned internal contracts.
