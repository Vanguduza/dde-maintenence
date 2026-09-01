# AECI Maintenance — Full DDE Maintenance Capability Inheritance Specification v1.0

**Status:** Authoritative gap-closure specification for the AECI Maintenance Operations System (AMOS)
**Applies to:** `aeci-maintenance-operations-v1`
**Relationship to existing documents:** This specification supplements `AECI_Maintenance_Operations_System_Master_Plan_v1.md`, `AECI_Maintenance_Implementation_Realisation_Pack_v1.md`, `AECI_Maintenance_RBAC_Competency_Matrix_v1.md`, and the generic `DDE_Maintenance_Intelligence_ERP_Master_Plan_v2.md`.

---

# 1. Purpose

The AECI specialization must not be a reduced subset of DDE Maintenance. It is a customer/industry specialization of the complete DDE Maintenance operating model.

The previous AMOS baseline correctly covered the large structural domains — asset registry, work management, safety, stores, workshop, reliability, SLA, telemetry and governed AI — but several deeply operational workflows from the DDE Maintenance capability model were not made explicit enough for implementation. This document closes that gap.

## 1.1 Mandatory inheritance rule

**Every DDE Maintenance capability that is operationally applicable to AECI is inherited by AMOS unless it appears in an explicit Exclusion Register with a rationale, owner, approval and review date. Silence is not exclusion.**

This rule prevents later implementation teams from interpreting an AECI customer pack as permission to omit generic DDE Maintenance capabilities.

## 1.2 Exclusion governance

An AECI capability may only be excluded when all of the following are recorded:

- source DDE capability;
- reason it is not applicable;
- affected roles/sites/assets;
- safety/compliance impact assessment;
- product owner approval;
- AECI/customer validation where customer-specific;
- review date;
- replacement capability if one exists.

No safety, legal, evidence, competency, maintenance-quality or auditability capability may be excluded merely to simplify an MVP.

---

# 2. AECI Maintenance Operating Loop

AMOS inherits the DDE Maintenance operating loop in full:

**SENSE → UNDERSTAND → ASSESS RISK → PREDICT → PLAN → RESOURCE → MAKE SAFE → EXECUTE → VERIFY → MEASURE OUTCOME → LEARN → OPTIMISE**

This loop applies at four levels:

1. **Asset/component** — condition, defect, intervention, verification, life history.
2. **Job/work pack** — plan, resources, safe-state, execution, test, quality, closeout.
3. **Site/service delivery** — readiness, backlog, competence, spares, blast-support risk, SLA.
4. **Enterprise** — reliability trends, fleet strategy, people capability, commercial performance, compliance and learning.

A work order that moves from `IN_PROGRESS` to `COMPLETED` has only completed execution. It does **not** prove the repair is effective. Where policy requires it, a separate verification state and/or follow-up verification task must establish successful return to service.

---

# 3. Digital Job Card Pack — Mandatory AECI Work Execution Unit

The unit delivered to an AECI technician is not a bare work order. It is a **Digital Job Card Pack**.

Every released job pack is an immutable, revision-pinned execution bundle assembled from governed source objects. It must remain usable offline for the assigned execution window.

## 3.1 Job Card Pack contents

Depending on task class and site rules, the pack contains:

### A. Work identity and context
- job card/work-order number;
- customer/site/area/location;
- asset and component identity;
- asset criticality;
- defect/request origin;
- fault description and symptom code;
- priority and consequence;
- reported-by information;
- planned start/end;
- blast/service-window linkage where applicable;
- current asset state and readiness impact;
- recent relevant work history;
- open related defects;
- repeat-failure/rework warning if detected.

### B. Approved procedure and job plan
- controlled SOP/procedure revision;
- job plan task sequence;
- required measurements and acceptance limits;
- torque/pressure/flow/electrical values where approved sources provide them;
- drawings/schematics/manual extracts relevant to the task;
- quality hold points;
- inspection points;
- test/commissioning steps;
- return-to-service criteria.

The system must never generate or silently modify safety-critical procedure values. AI can retrieve and explain governed values but cannot invent them.

### C. Risk and safety pack
- job-specific HIRA/JSA/JHA or task risk assessment;
- baseline-risk references;
- identified hazards;
- required controls;
- PPE matrix;
- hazardous-area/device restrictions;
- work-at-height/confined-space/hot-work/lifting/electrical/pressure/chemical requirements as applicable;
- emergency/escalation instructions;
- stop-work authority reminder.

### D. Permit pack
- required permit type(s);
- permit reference(s);
- issuer/receiver role requirements;
- validity period;
- host-mine permit references where the host owns the permit system;
- suspension/revalidation state;
- handover requirements.

AMOS records and gates the presence/state of required permits. It must never equate a database field with proof of the physical worksite state.

### E. LOTO/isolation pack
- isolation requirement;
- energy-source list;
- isolation points;
- isolation sequence from approved procedure;
- lock/tag identifiers where locally managed;
- responsible/authorized persons;
- zero-energy verification requirement;
- isolation handover state;
- re-energization/release steps;
- evidence/signatures required by site policy.

Location, QR, BLE, NFC or digital acknowledgement may assist evidence but **must not be treated as proof of physical isolation**.

### F. Competency/authorization pack
- required trade/skill;
- required equipment authorization;
- required statutory/site competence;
- permit/isolation authority where applicable;
- site induction/access validity;
- medical/fitness constraints where configured;
- expiry checks at assignment and again at work start.

### G. PPE requirements
- mandatory PPE by task/hazard;
- specialized PPE;
- inspection status where applicable;
- issue/custody evidence for controlled PPE;
- replacement/expiry information where tracked.

### H. Tools and test equipment
- required hand tools;
- required special tools;
- lifting equipment;
- test instruments;
- calibration requirement and due date;
- tool inspection status;
- tool crib reservation/issue status;
- substitution approval if a specified tool is unavailable.

A task requiring calibrated measurement cannot be closed with a known-out-of-calibration instrument unless an approved exception workflow exists and the resulting measurement is clearly invalidated/reworked.

### I. Parts, consumables and materials
- required parts/BOM quantities;
- reserved stock;
- issue/pick status;
- compatible substitutes and approval rules;
- consumables;
- repairable/rotable issue and genealogy requirements;
- expected old-part return where applicable.

### J. Evidence capture
- measurements;
- failure code;
- cause/remedy codes;
- photos/video where safe and policy-approved;
- old/new component serials;
- parts consumed;
- tools used where traceability is required;
- technician notes/voice notes;
- deviation/exception record;
- signatures and timestamps;
- supervisor/QA hold-point approvals.

### K. Completion and verification
- functional test;
- leak/pressure/electrical/PLC/roadworthiness/other appropriate test;
- cleanup and restoration;
- guarding restored;
- isolation release/re-energization;
- worksite housekeeping;
- permit closure/reference;
- return-to-service authorization;
- follow-up verification requirement;
- monitoring period where required.

## 3.2 Job Card Pack lifecycle

Canonical lifecycle:

`REQUESTED → TRIAGED → PLANNED → RESOURCED → SAFETY_PREPARED → READY_TO_RELEASE → RELEASED → ACCEPTED → MAKE_SAFE → IN_PROGRESS → PAUSED/WAITING → EXECUTION_COMPLETE → TESTING → RETURN_TO_SERVICE_PENDING → VERIFIED → CLOSED`

Side states/events include:

- `CANCELLED`;
- `DEFERRED`;
- `AWAITING_PARTS`;
- `AWAITING_TOOL`;
- `AWAITING_PERMIT`;
- `AWAITING_ACCESS`;
- `AWAITING_TECHNICAL_SUPPORT`;
- `REWORK_REQUIRED`;
- `FOLLOW_UP_REQUIRED`;
- `RCA_REQUIRED`.

The implementation may use a smaller physical enum if an event/state projection preserves the same semantics.

## 3.3 Revision pinning

At release, the pack records the exact revisions of:

- procedure/job plan;
- risk assessment;
- PPE requirements;
- drawings/manuals;
- permit template/rules;
- LOTO template;
- acceptance criteria.

If a safety-critical source is superseded during execution, the policy engine decides whether the job can continue, must be suspended, or must be reissued. The system must never silently swap a procedure underneath an active job.

---

# 4. Rework, Failed Repair and Maintenance Quality

AMOS must explicitly model **repair quality**, not just job completion.

## 4.1 Rework definition

A work event becomes `SUSPECTED_REWORK` when configurable rules detect, for example:

- same asset/component + same/similar failure mode within a defined time or operating-hour window;
- a functional test fails after execution completion;
- the customer/operator rejects the return-to-service result;
- the asset breaks down before the verification window expires;
- the original defect was not eliminated;
- an incorrect part, assembly, setting or calibration is discovered;
- workmanship-related defects are found.

## 4.2 Rework adjudication

The system must not automatically punish a technician because a repeat job exists.

A supervisor/quality/reliability workflow classifies the event as one of:

- confirmed rework;
- unrelated new failure;
- progressive underlying failure;
- incorrect original diagnosis;
- defective replacement part;
- external/operator/process cause;
- design/systemic cause;
- maintenance-induced failure;
- no-fault-found/insufficient evidence;
- other governed category.

Only adjudicated outcomes may feed individual performance metrics.

## 4.3 Rework workflow

`repeat event detected → link original WO → preserve evidence → quality review → classify → create corrective job if required → RCA threshold check → verify corrective action → update reliability/performance analytics`

Rework cost must be measurable as:

- labour hours;
- parts/consumables;
- travel/recovery;
- lost availability;
- blast/service-window impact;
- external vendor cost;
- SLA/commercial consequence where defined.

---

# 5. Recurring Breakdowns, Repeat Failures and Bad Actors

AECI operations must not normalize repeated breakdowns as separate unrelated tickets.

## 5.1 Recurrence engine

Rules run against:

- asset;
- serialized component;
- failure mode;
- symptom;
- repair action;
- operating hours/cycles/km;
- time window;
- site/duty context;
- installed-part batch/supplier;
- technician/job-plan history;
- sensor signatures where available.

## 5.2 Escalation levels

Example policy tiers:

- **Level 0 — isolated:** normal corrective workflow.
- **Level 1 — repeat warning:** second similar failure in threshold window; show history to technician/planner.
- **Level 2 — recurring:** reliability review required before ordinary closure.
- **Level 3 — bad actor:** formal RCA/FMEA/strategy review, management visibility, maintenance-plan challenge.
- **Level 4 — systemic:** engineering change, supplier/OEM escalation, fleet-wide applicability review.

Thresholds are configurable by asset class/failure criticality and must not be hard-coded globally.

## 5.3 Recurrence graph

The asset passport must expose a failure/rework graph linking:

`failure → WO → diagnosis → part → technician/team → procedure revision → repair → verification → next failure`

This is essential for distinguishing bad equipment, bad parts, wrong PM strategy, weak procedures, operating abuse and workmanship problems.

---

# 6. Technician KPI, Performance and Development System

AECI AMOS inherits technician performance management, but it must be **context-, difficulty- and exposure-aware**. The system may not reduce artisan performance to job counts or speed.

## 6.1 Performance principles

1. Safety behavior must never be penalized because stopping unsafe work reduces throughput.
2. Difficult/high-criticality jobs must not be compared directly with routine tasks without normalization.
3. Team jobs distinguish team outcomes from individual responsibility.
4. Rework affects a technician only after adjudication.
5. Breakdown frequency is not an individual technician KPI unless causal responsibility is established.
6. Data completeness is separated from technical effectiveness.
7. KPIs support coaching and capability development, not opaque automated discipline.
8. Every score must be explainable to the employee and supervisor.

## 6.2 Balanced technician scorecard

Configurable metrics include:

### Safety & compliance
- pre-job safety-gate completion quality;
- required permit/LOTO adherence;
- stop-work/escalation behavior;
- PPE compliance;
- overdue mandatory competence/authorization issues attributable to the employee;
- quality of hazard/defect reporting.

Safety incident counts alone must not be used as a simplistic personal ranking metric.

### Quality
- first-time-fix/verified repair rate;
- adjudicated rework rate;
- failed functional-test rate;
- maintenance-induced-failure rate;
- repeat-defect escape rate;
- evidence/job-card completeness;
- correct failure/cause/remedy coding;
- QA acceptance rate.

### Delivery
- schedule adherence normalized for access/parts/permit delays;
- response-time performance by priority after excluding uncontrollable delays;
- execution duration vs planned standard, normalized by task complexity;
- backlog completion reliability;
- shift-handover quality.

### Technical effectiveness
- diagnostic accuracy where measurable;
- successful complex repairs;
- defect detection before functional failure;
- quality of technical escalation;
- adherence to controlled procedures;
- appropriate use of measurements and test instruments.

### Reliability contribution
- actionable defect elimination suggestions;
- RCA participation and action closure;
- PM/job-plan improvement suggestions adopted;
- knowledge capture quality;
- recurring-failure identification.

### Development
- competence matrix progress;
- training completed;
- supervised authorization progression;
- cross-skilling;
- coaching/mentoring contributions.

## 6.3 Supervisor view

The supervisor dashboard must show:

- raw measures and denominators;
- confidence/data quality;
- task mix and difficulty distribution;
- controllable vs uncontrollable delay hours;
- team vs individual attribution;
- trend over time;
- rework adjudication status;
- competency gaps;
- coaching actions.

No opaque single-number employee score may be the only view.

---

# 7. Tools, Test Equipment and Tool Audit Control

AMOS must include a complete **Tools & Test Equipment Control** domain.

## 7.1 Tool classes

- personal hand tools;
- company-issued toolboxes;
- shared site tools;
- special service tools;
- lifting/tackling equipment;
- electrical test instruments;
- pressure/flow/temperature instruments;
- torque tools;
- calibration standards;
- intrinsically safe/hazardous-area tools/devices where applicable;
- contractor/vendor tools when controlled by AECI policy.

## 7.2 Tool register

Each controlled tool can carry:

- unique ID/QR/RFID/NFC tag;
- description/category;
- make/model/serial;
- owner/store/site;
- assigned custodian;
- inspection requirements;
- calibration requirements;
- calibration certificate/revision;
- last/next due date;
- condition;
- issue/return history;
- loss/damage history;
- quarantine state;
- replacement cost;
- hazardous-area suitability where applicable.

## 7.3 Tool issue and custody

Workflow:

`reserve → pre-use status check → issue → job association → return → post-use condition → store`

Exceptions:

- lost tool;
- damaged tool;
- incomplete toolbox;
- overdue return;
- failed inspection;
- expired calibration;
- unauthorized substitution.

## 7.4 Toolbox/tool audits

Support:

- scheduled toolbox audits;
- start/end-of-shift spot audits;
- post-shutdown/project audits;
- vehicle/service-kit audits;
- site/tool-crib stocktake;
- supervisor signoff;
- missing/damaged item action;
- repeated-loss trend;
- employee acknowledgment.

An audit must compare the expected kit/BOM against physically confirmed items and create actionable exceptions.

## 7.5 Calibration impact reconstruction

When an instrument is found out of tolerance, AMOS must answer:

- when was the last known-good calibration/verification?;
- which jobs used the instrument after that point?;
- what measurements were recorded?;
- what assets/components may be affected?;
- which jobs require engineering review, retest or rework?

This creates a traceable impact set rather than merely marking the instrument overdue.

---

# 8. Technician Field Experience Workflows

## 8.1 Start of shift

Technician experience includes:

- roster/assignment confirmation;
- critical site notices;
- safety alerts;
- shift handover acceptance;
- priority breakdowns;
- planned jobs;
- competence/authorization expiry warnings;
- toolbox/tool exceptions;
- required permits/access constraints;
- site/asset readiness exceptions;
- offline sync health.

## 8.2 Fault reporting

A technician/operator can raise a defect by minimum-interaction workflow using structured fields, photo or voice where safe:

`asset → symptom → severity/consequence → safe-state/operating status → evidence → submit`

The report can create:

- defect only;
- urgent breakdown request;
- safety stop/escalation;
- inspection follow-up.

## 8.3 Breakdown triage

Breakdown jobs capture:

- breakdown start;
- asset unavailable/degraded state;
- production/blast-service consequence;
- immediate containment;
- remote support/escalation;
- diagnostic steps;
- parts/tools/competency requirements;
- restoration time;
- verification;
- recurrence/rework link.

## 8.4 Pause/wait reasons

Technicians must be able to pause work with governed reason codes such as:

- awaiting spares;
- awaiting tool;
- awaiting permit;
- awaiting isolation;
- awaiting access;
- weather/environment;
- production/customer constraint;
- technical support/OEM;
- additional manpower;
- safety concern;
- other explained reason.

These codes feed planning accuracy and technician KPI normalization.

## 8.5 Safe device use

Field UI must minimize interaction during hazardous work. Site/zone policy can:

- suppress non-critical notifications;
- restrict camera/voice/device use;
- require device stowage during defined task steps;
- switch to kiosk/task-only mode;
- permit hands-free/push-to-talk only where safe and approved;
- respect hazardous-area hardware restrictions.

Geofencing/zone awareness assists policy selection but does not prove the worker's precise physical safety state.

---

# 9. Shift Handover and Continuity of Work

Digital shift handover is a controlled operational object, not a chat message.

It includes:

- active breakdowns;
- open isolations/LOTO;
- suspended permits;
- equipment operating with known defects;
- temporary repairs/bypasses;
- waiting-for-parts/tools/vendor items;
- abnormal readings;
- unfinished jobs and exact safe state;
- critical spares issues;
- blast/service-window risks;
- safety/environmental concerns;
- required follow-ups.

Outgoing and incoming accountable roles acknowledge handover. Material items remain active until explicitly resolved; acknowledgment must not close the underlying issue.

---

# 10. Inspection, Defect and Deferred-Defect Workflow

AMOS must support inspections that produce structured defects.

Examples:

- daily MMU walkaround;
- hose/reel inspection;
- pump inspection;
- silo/storage inspection;
- fleet inspection;
- statutory inspection;
- tool inspection;
- workshop QA inspection.

Defect states:

`NEW → TRIAGED → ACCEPTED → MONITORED/DEFERRED/WORK_PLANNED → REPAIRED → VERIFIED → CLOSED`

A deferred defect requires:

- risk/criticality;
- reason;
- approved operating limits/controls;
- owner;
- review date;
- expiry/escalation;
- linkage to planned corrective work.

Critical/safety/legal defects cannot be deferred through a generic maintenance convenience override.

---

# 11. Job Planning and Pack-Readiness Gate

A planner must see whether a job is genuinely executable.

A job is **ready to schedule** only when configured prerequisites are satisfied, for example:

- scope is clear;
- correct asset/component identified;
- approved procedure/job plan available;
- risk assessment present;
- required competence identifiable;
- parts available/reserved or accepted risk;
- special tools available;
- calibrated test equipment available;
- drawings/manuals available;
- permits/access needs known;
- expected duration/labour defined;
- service/blast-window constraints understood.

The readiness engine must expose missing prerequisites rather than simply returning a boolean.

---

# 12. Quality Assurance and Return to Service

High-risk/critical job classes can require independent QA or supervisor verification.

Examples:

- meter calibration;
- safety-circuit work;
- pressure-system intervention;
- hose/connection integrity;
- hydraulic repairs;
- braking/roadworthiness-related work;
- major pump rebuild;
- PLC safety/interlock changes;
- storage/containment repairs.

Return-to-service evidence may include:

- test values;
- leak checks;
- no-load/load test;
- functional interlock test;
- calibration verification;
- road test;
- supervisor/QA authorization;
- customer/operator acceptance where contractually required.

`work execution complete` and `asset verified for service` remain distinct states.

---

# 13. Maintenance-Induced Failure and No-Fault-Found

Both are explicit failure-quality categories.

## 13.1 Maintenance-induced failure

When evidence suggests maintenance caused or contributed to a later failure, AMOS links the events and triggers appropriate quality/RCA review. Examples may include incorrect assembly, contamination, incorrect adjustment, wrong part, loose connection, omitted fastener or calibration error.

The system must not assume technician fault; causation requires review.

## 13.2 No-fault-found

No-fault-found events capture:

- reported symptom;
- test performed;
- conditions under which symptom could not be reproduced;
- measurements;
- suspected intermittent conditions;
- next monitoring action;
- recurrence link.

Repeated no-fault-found events should escalate rather than disappear into closed history.

---

# 14. Technical Support and Escalation

A technician must be able to request support from within the job pack while preserving context.

Escalation bundle includes:

- asset/component;
- current job;
- fault/symptoms;
- measurements;
- alarms;
- relevant procedure/drawing revision;
- attempted steps;
- photos/video/voice where safe;
- current safe state;
- parts/tools available.

Support paths may include:

- site supervisor;
- maintenance engineer;
- reliability engineer;
- electrical/controls specialist;
- workshop;
- OEM/vendor.

Remote guidance becomes part of the job evidence/history.

---

# 15. Knowledge Capture and Continuous Learning

Closed work must improve the system.

Structured outputs include:

- confirmed failure mode;
- root cause when known;
- successful remedy;
- unsuccessful attempts;
- actual labour;
- parts used;
- tool/instrument use;
- measurements;
- procedure deviations;
- follow-up outcome;
- technician feedback on job-plan quality;
- suggested changes.

Approved learning can update:

- failure libraries;
- troubleshooting guides;
- job plans;
- PM strategies;
- spares forecasts;
- competency/training needs;
- AI retrieval corpus.

No technician feedback may silently alter an approved safety-critical procedure; it enters document/engineering change control.

---

# 16. Planner, Supervisor and Manager Workflow Additions

## 16.1 Planner

Planner workspace includes:

- unplanned backlog;
- age/priority/criticality;
- job-pack completeness;
- waiting reasons;
- parts/tool availability;
- competent labour availability;
- site access/travel;
- blast/service windows;
- schedule compliance;
- PM forecast;
- shutdown/campaign bundling;
- repeat-failure/RCA work;
- deferred-defect review dates.

## 16.2 Supervisor

Supervisor workspace includes:

- crew readiness;
- job acceptance/start status;
- safety-gate completeness;
- open isolations/permits;
- stuck/paused jobs;
- rework alerts;
- repeat failures;
- tool/competency exceptions;
- return-to-service approvals;
- shift handover;
- technician quality/performance trends;
- coaching/actions.

## 16.3 Maintenance manager

Manager workspace includes:

- availability/readiness;
- PM compliance;
- backlog health;
- schedule compliance;
- rework cost/rate;
- recurring failures/bad actors;
- maintenance-induced failures;
- first-time-fix rate;
- labour utilization with contextual delay breakdown;
- technician/team capability gaps;
- tool/calibration audit posture;
- stores/service risk;
- compliance status;
- customer/SLA risk;
- reliability improvement action status.

---

# 17. Additional AECI-Specific Inherited Workflows

## 17.1 MMU/charging-unit daily readiness pack

Combines:

- vehicle walkaround;
- process-skid inspection;
- hose/reel condition;
- pump prime/leak checks;
- meter zero/verification;
- safety/interlock state;
- product-system checks defined by approved AECI procedures;
- statutory road document status;
- known defects;
- required service interval;
- blast-window demand.

## 17.2 Pump removal/rebuild/reinstall genealogy

`failed in asset A → removed → workshop strip report → component findings → parts/rebuild → bench test → QA release → stores/rotable pool → installed in asset B → commissioning test`

Every stage preserves component serial and life history.

## 17.3 Hose life and inspection control

Track hose identity where warranted, installation date, duty/cycles where available, inspection outcomes, damage, retirement reason and burst/failure history. Hose condition is visible in readiness and repeat-failure analysis.

## 17.4 Calibration-linked charging quality

Meter/instrument calibration status links to affected work/charging quality evidence. An out-of-tolerance finding can generate an impact reconstruction set for technical review.

## 17.5 Remote-site recovery workflow

For breakdowns requiring recovery:

- asset safe state;
- site/customer coordination;
- towing/recovery requirements;
- route/legal readiness;
- replacement/backup asset readiness;
- workshop booking;
- travel/recovery cost;
- SLA/blast impact.

---

# 18. Capability Domains That Must Exist in AMOS

The AECI product baseline therefore includes, at minimum:

1. Asset & component registry
2. Defects & inspections
3. Digital Job Card Packs
4. Work management
5. Planning & scheduling
6. Shift handover
7. HIRA/JSA/risk
8. Permits
9. LOTO/isolation
10. PPE control
11. Competency & authorization
12. Tools & test equipment
13. Tool audits & calibration
14. Stores & inventory
15. Procurement
16. Workshop & repairables
17. Quality assurance
18. Return to service & verification
19. Rework management
20. Recurring breakdowns/bad actors
21. Reliability/RCA/FMEA
22. Maintenance-induced failure
23. No-fault-found management
24. Technician KPI/performance/development
25. Supervisor/team performance
26. Controlled procedures/documents
27. Engineering change
28. Fleet/statutory compliance
29. Customer/SLA management
30. Blast-support readiness
31. Condition monitoring
32. OT/edge integrations
33. Maintenance Control Centre
34. Governed RAG/AI copilots
35. Audit/evidence/reporting
36. Offline/sync/conflict management
37. Safe field-device/zone-aware behavior
38. Technical escalation/remote support
39. Knowledge capture/continuous learning
40. Management/reliability analytics

A module list is not enough: each domain must be integrated through the shared asset/work/person/safety/material/document/event graph.

---

# 19. Cross-Domain Rules

1. **Safety before execution.** A job cannot move into hazardous execution without its configured safety prerequisites.
2. **Competence is not RBAC.** Permission to open a screen does not imply authorization to perform work.
3. **Procedure revisions are controlled and pinned.** No silent mid-job mutation.
4. **Completed work ≠ verified repair.** Return-to-service and outcome verification are explicit.
5. **Repeat failures are linked.** The system must not treat recurring breakdowns as unrelated tickets.
6. **Rework is adjudicated before individual attribution.**
7. **Performance is context-aware.** Raw job counts/speed are not sufficient KPIs.
8. **Tools and instruments are governed resources.** Calibration and custody matter.
9. **Inventory is ledgered.** No direct mutable stock balances without movement history.
10. **Offline evidence is first-class.** Sync retries are idempotent and conflicts are domain-specific.
11. **AI is advisory.** It cannot claim physical isolation, approve hazardous work, override legal/safety stops or invent controlled technical values.
12. **Every operational exception remains actionable.** Handover acknowledgement, inspection completion or report generation must not silently close the underlying defect/risk/action.
13. **Learning is governed.** Field experience can propose changes but controlled procedures/PM/engineering baselines change only through approval.

---

# 20. Implementation Consequence

The existing AMOS implementation programme remains valid, but the following capability threads become mandatory cross-phase requirements:

- **Phase A:** tools/test equipment, competency detail, controlled documents, PPE master data, job-pack templates, failure/rework identity.
- **Phase B:** full Digital Job Card Pack, permit/LOTO/HIRA/PPE gating, pause/wait reasons, functional testing, return-to-service verification, rework linkage, technical escalation.
- **Phase C:** shift handover, technician/team performance foundations, job-pack readiness, stuck-work reasons, tool/competence visibility.
- **Phase D:** tool crib/custody/audits/calibration, repairable genealogy, rework cost, parts/tool reservations.
- **Phase E:** recurring breakdown engine, bad actors, maintenance-induced failure, NFF, RCA/CAPA, PM optimization, calibration impact reconstruction.
- **Phase F:** customer-impact and blast-support consequence tied to breakdown/rework/verification.
- **Phase G:** condition data used as evidence, with freshness/quality and recurrence correlation.
- **Phase H:** governed troubleshooting grounded in current applicable procedures, job history, failure/rework graph and technician authorization context.

No phase is considered feature-complete merely because a happy-path job can be demonstrated.

---

# 21. Definition of Done for DDE Capability Inheritance

AECI capability inheritance is complete only when:

- every applicable DDE Maintenance capability is mapped to an AECI implementation owner/context;
- exclusions are explicit and approved;
- Digital Job Card Packs operate end-to-end offline and online;
- rework and recurring failure relationships are persisted and testable;
- technician performance is explainable, normalized and does not create unsafe incentives;
- tool audit/calibration/custody workflows are operational;
- return-to-service verification is distinct from execution completion;
- all applicable P0/P1 acceptance tests pass;
- the capability map is represented in the machine-readable AECI pack so future generators/agents cannot silently omit it.
