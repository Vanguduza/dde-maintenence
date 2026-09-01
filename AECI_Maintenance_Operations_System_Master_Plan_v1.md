# AECI Maintenance Operations System — Master Plan v1.0

**Status:** Implementation source of truth for the AECI Zimbabwe maintenance product layer built on DDE Asset Operations Intelligence Platform.
**Date:** 1 September 2026
**Repository:** `Vanguduza/dde-maintenence`
**Branch:** `aeci-maintenance-operations-v1`
**Relationship to existing documents:** This document elevates `DDE_AECI_Operations_Pack_Config_Spec.md` from a customer configuration into a complete operating model for AECI Maintenance. The generic DDE platform remains the shared technical substrate. Existing AECI research, security, rugged field, modular platform, and market-entry documents remain authoritative for their specialist domains unless explicitly superseded here.

---

# 1. Product Definition

AECI Maintenance Operations System (AMOS) is a safety-native, asset-centric maintenance ERP and field operations platform for AECI Mining Explosives Zimbabwe. It is designed around the realities of an explosives-services provider maintaining mobile and fixed delivery equipment across distributed customer mines, workshops and logistics routes.

AMOS is not a generic CMMS and is not a blast-design system. It coordinates the complete maintenance operating model required to keep AECI service-delivery assets safe, legal, reliable, staffed, supplied and ready for customer blast-support commitments.

The system joins the following domains on one canonical operational graph:

- asset and component lifecycle;
- work management;
- planning and scheduling;
- field execution;
- workshop repair and rebuild;
- reliability engineering;
- SHERQ, HIRA/JSA, permits and LOTO;
- people, competence and authorization;
- stores, procurement, repairables and rotables;
- vehicle and statutory fleet compliance;
- explosives-related statutory registers;
- condition monitoring and OT telemetry;
- customer contracts, SLA and blast-support commitments;
- engineering change control;
- documents, SOPs and controlled procedures;
- incidents, RCA and CAPA;
- financial and cost-of-reliability lineage;
- AI/RAG maintenance intelligence;
- reporting, audit and executive decision support.

Every domain references the same tenant, site, asset, component, person, job, document, risk, stock item, supplier, contract and event identities. No module may create shadow master data for these objects.

---

# 2. Product Outcomes

AMOS is successful only when it improves operational outcomes, not merely record-keeping. Product-level outcome measures are:

1. **Zero Harm support:** hazardous work is never presented as ordinary checklist work; risk, permit, isolation, PPE and competency requirements are evaluated before execution.
2. **Blast-support readiness:** managers can see whether upcoming customer service commitments are technically supportable with the available assets, crews, legal credentials and critical spares.
3. **Higher technical availability:** planned maintenance, condition monitoring, rapid breakdown response and defect elimination reduce avoidable downtime.
4. **Lower repeat failure:** the platform converts recurrent faults into engineering actions and verifies effectiveness.
5. **Better wrench time:** planners and supervisors reduce waiting for parts, permits, information, tools and competent labour.
6. **Defensible compliance:** statutory, contractual, calibration and maintenance evidence is reconstructable by asset, date, person and site.
7. **Controlled maintenance cost:** every maintenance event can be traced to labour, parts, vendor services, downtime consequence and contract impact.
8. **Operational learning:** closed work, failures, measurements and successful repairs become reusable governed knowledge.

---

# 3. Scope and Asset Estate

AMOS covers the AECI Zimbabwe maintenance estate already defined in the AECI Operations Pack and extends it into complete lifecycle management.

## 3.1 Mobile manufacturing and charging assets

- MMUs: road vehicle + process skid composite assets.
- MCUs: underground mobile charging units.
- PCUs: portable charging units.
- RRS / rapid reloaders / re-pump units.
- Road tankers and product-transfer vehicles.
- Support fleet: LDVs, crew buses, trailers and mobile workshop assets where brought into scope.

## 3.2 Fixed process and transfer assets

- transfer pumps;
- silo offload and recirculation systems;
- EVDS strings and stations;
- emulsion silos;
- magazines and storage facilities;
- bulk plant equipment when contractually confirmed;
- workshop plant, test benches and calibration equipment.

## 3.3 Component-level lifecycle

The canonical model must support serialized and non-serialized components. High-value or life-limited items such as pumps, motors, flow meters, hose reels, hydraulic assemblies, PLCs, load cells, calibration instruments and selected valves are individually traceable across installation, removal, repair, stores, workshop and reinstallation events.

---

# 4. Operating Model and Role Surfaces

AMOS is delivered as one product with role-specific surfaces rather than disconnected apps.

## 4.1 Technician / artisan

Primary surface: rugged tablet or approved mobile device, offline-first.

Functions:
- assigned work and shift plan;
- start-of-shift equipment checks;
- job packs and controlled SOPs;
- HIRA/JSA and Take 5 where configured;
- permit and isolation references;
- LOTO verification;
- asset passport and drawings;
- guided troubleshooting;
- measurements and meter readings;
- parts issue/return/scanning;
- photo/video/evidence capture;
- breakdown and defect reporting;
- handover notes;
- request for assistance/escalation;
- return-to-service test and sign-off;
- offline queue visibility.

## 4.2 Supervisor / foreman

Functions:
- shift crew board;
- active breakdown board;
- assignment and re-assignment;
- competency and authorization checks;
- permit completeness;
- deferred defects;
- temporary repair controls;
- shift handover acceptance;
- work-quality review;
- backlog triage;
- readiness sign-off;
- escalation of blast-window risk.

## 4.3 Planner / scheduler

Functions:
- backlog management;
- planning templates and job plans;
- labour loading;
- weekly and daily schedule;
- parts reservations;
- tool and service requirements;
- contractor/vendor dependencies;
- statutory due work;
- shutdown/campaign plans;
- schedule compliance;
- kitting and ready-to-schedule gates.

## 4.4 Maintenance engineer / reliability engineer

Functions:
- bad-actor analysis;
- MTBF/MTTR/availability;
- repeat-failure review;
- defect elimination;
- RCA/5-Why/Fishbone;
- FMEA/FMECA;
- Weibull and survival analysis where data quality permits;
- PM optimization;
- maintenance strategy review;
- engineering changes;
- condition-monitoring rules;
- lifecycle cost and cost-of-unreliability;
- effectiveness verification.

## 4.5 Workshop supervisor

Functions:
- incoming queue;
- strip/inspect/diagnose;
- repair authorization;
- parts and external services;
- repair/rebuild routing;
- test and QA hold points;
- calibrated-tool checks;
- component genealogy;
- ready-for-dispatch queue;
- turnaround-time tracking;
- repairable and rotable status.

## 4.6 Stores / procurement

Functions:
- multi-store inventory;
- reservations and kitting;
- min/max and reorder controls;
- critical spares;
- serialized items;
- shelf-life controls;
- repairable/rotable loops;
- requisitions/RFQ/PO/GRN;
- site transfers;
- cycle counts;
- stock-out risk;
- supplier lead-time and quality performance.

## 4.7 SHERQ / compliance

Functions:
- controlled risk assessments;
- PPE matrix;
- permit/LOTO policy configuration;
- incidents and near misses;
- safety observations;
- CAPA;
- competency/medical/induction expiry monitoring;
- road-fleet statutory registers;
- explosives licence registers;
- audit evidence packs.

## 4.8 Regional maintenance manager / business leadership

Functions:
- national maintenance control centre;
- multi-site readiness;
- asset availability and service risk;
- schedule and backlog health;
- safety/compliance posture;
- SLA exposure;
- maintenance cost and budget;
- workforce capacity;
- critical spares risk;
- vendor performance;
- reliability improvement pipeline.

---

# 5. Maintenance Control Centre

The Maintenance Control Centre is the primary operational coordination surface for the Zimbabwe maintenance function.

It shall provide a real-time or last-known-status view of:

- asset availability by site and asset class;
- operational, degraded, out-of-service, isolated, workshop and awaiting-parts states;
- active breakdowns and elapsed downtime;
- open critical defects;
- overdue PM and statutory work;
- vehicles legally road-ready or grounded;
- licence and calibration exposure;
- upcoming blast-support commitments;
- required primary and backup assets;
- technician coverage and competency constraints;
- critical spares and stock-out threats;
- open safety stops and permits;
- customer SLA risk;
- edge/offline sync health.

## 5.1 Readiness states

Every site and critical service commitment receives an explainable readiness state:

- **GREEN — Ready:** no blocking safety, legal, asset, labour or material condition.
- **AMBER — Ready with risk:** service is feasible but one or more non-blocking risks exist.
- **RED — Service at risk:** one or more material constraints threaten execution.
- **BLACK — Safety/compliance stop:** execution must not proceed until the blocking condition is resolved by an authorized human role.

Readiness is never a single opaque AI score. The UI must expose the contributing facts and confidence/age of each signal.

---

# 6. Canonical Asset and Component Digital Passport

Each asset and serialized component receives a digital passport containing:

- unique identity and serial numbers;
- class/model/manufacturer;
- ownership and customer/site relationship;
- parent/child component tree;
- installation and removal history;
- operating hours/kilometres/cycles;
- condition measurements and telemetry;
- PM and inspection program;
- defects and work history;
- failure modes and causes;
- rebuild history;
- calibration history;
- statutory credentials;
- current location and operational state;
- warranty and supplier data;
- BOM and approved alternates;
- controlled drawings/manuals/SOPs;
- cost history;
- photos and evidence;
- engineering changes affecting the asset.

## 6.1 MMU minimum component tree

The MMU template must support, at minimum:

- chassis;
- engine and driveline;
- PTO;
- hydraulic power unit and circuits;
- emulsion tank;
- AN/prill tank where applicable;
- sensitizer circuit;
- water/additive circuits;
- progressive-cavity or product pumps;
- diaphragm/Hydra-Cell type pumps where fitted;
- valves and manifolds;
- auger;
- hose and hose-reel assemblies;
- flow meters;
- load cells;
- PLC and I/O;
- HMI;
- CAN/J1939 interfaces where available;
- electrical distribution;
- emergency-stop and safety circuits;
- GPS/positioning/communications modules where fitted.

The actual template is versioned by MMU model and site configuration; no assumption that every unit has identical hardware is permitted.

---

# 7. Work Management

## 7.1 Work classes

AMOS supports:

- corrective;
- preventive;
- condition-based;
- predictive recommendation converted to approved work;
- inspection;
- calibration;
- statutory;
- breakdown/emergency;
- deferred defect;
- temporary repair;
- engineering modification;
- workshop rebuild;
- campaign/shutdown;
- warranty;
- vendor/OEM service;
- RCA/CAPA action;
- follow-up verification.

## 7.2 Work-order state machine

Minimum controlled lifecycle:

`REQUESTED → TRIAGED → APPROVED → PLANNING → READY_TO_SCHEDULE → SCHEDULED → DISPATCHED → IN_PROGRESS → WAITING → TESTING → COMPLETED_PENDING_REVIEW → CLOSED`

Permitted terminal/exception states:

`CANCELLED`, `REJECTED`, `DEFERRED`, `STOPPED_FOR_SAFETY`.

State transitions are role-gated and event logged. A completed task is not automatically a successful repair; return-to-service and post-repair verification rules may create mandatory follow-up work.

## 7.3 Digital job pack

Every executable job pack can bind:

`asset + symptom + failure hypothesis + risk + permit + isolation + HIRA/JSA + SOP + PPE + tools + calibrated instruments + parts + labour/competence + instructions + hold points + measurements + evidence + test plan + return-to-service + verification`.

Safety-critical fields cannot be silently defaulted from previous work.

---

# 8. Planning, Scheduling and Backlog Control

## 8.1 Backlog quality gates

A work item becomes `READY_TO_SCHEDULE` only when all required planning attributes are complete:

- scope defined;
- job plan selected or authored;
- safety requirements identified;
- labour craft/competency specified;
- estimated duration;
- required parts reserved or available;
- tools/test equipment identified;
- drawings/SOPs linked;
- external service dependencies identified;
- operational access window known where required.

## 8.2 Planning boards

The planning workflow exposes:

`BACKLOG → PLANNED → READY → SCHEDULED → IN_PROGRESS → WAITING → TESTING → CLOSED`.

Views must support site, asset class, priority, criticality, technician, blast window, shutdown and compliance due-date filters.

## 8.3 Capacity model

Scheduling must account for:

- rostered labour hours;
- leave and training;
- site travel;
- permit/access constraints;
- competency and authorization;
- shift pattern;
- planned meetings/toolbox talks;
- expected emergency allowance;
- underground travel time where applicable.

Raw headcount must never be treated as available maintenance capacity.

---

# 9. Shift Operations and Handover

Each site receives a digital shift operating log.

Outgoing shift records:

- active breakdowns;
- isolated equipment;
- temporary repairs/bypasses;
- open permits;
- equipment operating with accepted defects;
- abnormal readings;
- parts awaited;
- work not completed and reason;
- blast/service commitments for the next shift;
- safety or access constraints.

The incoming responsible role explicitly accepts the handover. Material handover items become trackable actions rather than free-text notes only.

---

# 10. Breakdown and Defect Management

Breakdown response must support:

1. fault report from technician/operator/supervisor/telemetry;
2. severity and service-impact triage;
3. safety state check;
4. primary/backup asset substitution assessment;
5. technician dispatch based on competence and proximity/availability;
6. parts/tool availability;
7. guided diagnosis;
8. repair and evidence;
9. return-to-service test;
10. downtime coding;
11. failure mode/cause capture;
12. repeat-failure detection;
13. RCA trigger when threshold exceeded.

Defects can be classified as:

- monitor;
- repair next planned opportunity;
- restricted operation;
- immediate withdrawal from service;
- safety/compliance stop.

Any temporary repair must carry an owner, risk acceptance, expiry/review date, operating restriction and permanent-corrective-action reference.

---

# 11. Reliability Engineering Workspace

Reliability functions include:

- technical availability;
- operational availability;
- MTBF;
- MTTR;
- MTTF where relevant;
- repeat-failure rate;
- planned/unplanned ratio;
- emergency-work ratio;
- schedule compliance;
- maintenance-induced failure;
- no-fault-found events;
- Pareto by failure mode/component/site;
- bad-actor ranking;
- cost of unreliability;
- Weibull/survival analysis where sample size and data quality support it;
- FMEA/FMECA;
- PM optimization;
- defect-elimination register.

## 11.1 RCA to verified improvement loop

`FAILURE → RCA → ACTION → DESIGN/PROCEDURE/PM/TRAINING CHANGE → IMPLEMENTATION → EFFECTIVENESS CHECK → CLOSED`

RCA documents cannot be closed merely because a meeting occurred. Each action has an owner, due date and effectiveness criterion.

## 11.2 PM optimization

PM tasks may be revised when evidence shows over-maintenance, under-maintenance or ineffective inspection. Changes require versioning, engineering approval, impact assessment and preserved history.

---

# 12. Workshop Management and Repairable Assets

## 12.1 Workshop flow

`RECEIVED → QUARANTINED/SAFE → INITIAL_INSPECTION → STRIP → DIAGNOSIS → REPAIR_APPROVAL → WAITING_PARTS/EXTERNAL → REPAIR/REBUILD → TEST → QA_RELEASE → READY_FOR_DISPATCH → DISPATCHED`.

## 12.2 Repairable/rotable loop

`INSTALLED → FAILED/REMOVED → SITE_RETURN → WORKSHOP → REPAIR/REBUILD → TESTED → SERVICEABLE_STOCK → RESERVED → REINSTALLED`.

The system retains component genealogy across every parent asset and site.

## 12.3 Workshop controls

- repair scope and estimate;
- strip report;
- measurements and wear limits;
- replaced parts;
- machine/shop operations;
- external vendor services;
- calibrated test equipment;
- test results;
- QA release;
- warranty on repair;
- turnaround time;
- repair-vs-replace decision;
- repeat-return detection.

---

# 13. Stores, Procurement and Maintenance Supply Chain

AMOS provides a maintenance-specific inventory model across:

- Harare central store;
- site stores;
- technician/vehicle stock;
- workshop stock;
- quarantine;
- repairable/rotable stores;
- consignment stock where applicable.

Core functions:

- item master and BOM;
- serialized and lot-controlled stock;
- shelf-life and hazardous-material attributes;
- criticality;
- min/max;
- reorder point;
- safety stock;
- reservations;
- kitting;
- issues/returns;
- site transfers;
- cycle counts;
- stock adjustment controls;
- obsolete/superseded stock;
- approved alternates;
- requisitions;
- RFQ;
- PO;
- receipt/inspection/GRN;
- supplier quality and lead time;
- emergency procurement;
- warranty recovery.

## 13.1 Critical-spares intelligence

The system identifies service risk from:

`asset criticality × failure probability × installed population × stock on hand × stock reserved × repairable pipeline × supplier lead time × logistics variability × upcoming blast demand`.

AI may recommend, but inventory policy changes require authorized human approval.

---

# 14. SHERQ, HIRA/JSA, Permit and LOTO Integration

Safety is part of the work state machine rather than a parallel document repository.

AMOS supports controlled objects for:

- baseline risk assessment;
- task HIRA/JSA/JHA;
- Take 5 / last-minute risk assessment;
- PPE matrix;
- LOTO/isolation plans;
- isolation points;
- host-mine permit reference;
- hot work;
- confined space;
- working at height;
- lifting;
- electrical work;
- pressure systems;
- chemical exposure;
- hazardous-area restrictions;
- incident/near miss;
- safety observation;
- corrective action;
- toolbox talk;
- safety alert.

## 14.1 Machine-readable safety controls

The system can derive required controls from asset, job-plan and hazard metadata. For example, a pressurized emulsion transfer-pump intervention can require line isolation, depressurization, flushing, specified PPE and a test-before-return sequence.

Derived controls are advisory until validated into an approved procedure. Once approved, they become enforceable workflow gates.

## 14.2 No software substitution for physical safety

A digital permit, checkbox or AI output never proves physical isolation. The product records evidence and human verification; physical safety remains the responsibility of competent authorized people following approved procedures.

---

# 15. Workforce, Competency and Authorization Engine

Role-based access control is necessary but insufficient. AMOS also models whether a person is competent and authorized to perform a specific task.

Person capability records can include:

- trade and class;
- apprenticeship/trade-test status;
- OEM training;
- site induction;
- medical validity;
- driver's licence/class;
- professional driver requirements;
- equipment authorization;
- explosives-related training/authorization;
- LOTO authorization;
- permit authority;
- electrical authorization;
- lifting/rigging competence;
- working-at-height competence;
- confined-space competence;
- first aid;
- calibration competence;
- supervisor/approver authority;
- expiry and renewal dates.

## 15.1 Assignment eligibility

Before dispatch, the system evaluates:

`role + trade + competency + authorization + validity + site induction + medical + shift availability + fatigue/rest policy where configured + location/access`.

Failure of a mandatory criterion blocks automatic assignment and explains the reason.

## 15.2 Training matrix

Managers see current and forecast competency gaps by site, asset class and contract commitment. Training expiry becomes a capacity risk signal, not only an HR reminder.

---

# 16. Fleet Maintenance and Legal Road Readiness

The existing VID/ZINARA/insurance/governor register is preserved and integrated with maintenance operations.

The fleet module adds:

- odometer/hour history;
- service intervals;
- defect reporting;
- tyre history where required;
- fuel and consumption history;
- recovery/towing events;
- accident/damage linkage;
- roadworthiness inspections;
- driver-to-vehicle eligibility;
- workshop planning;
- off-road/site-only operational states.

A vehicle cannot be shown as road-ready when a mandatory legal credential is expired.

---

# 17. Customer Contract, SLA and Service-Delivery Layer

AECI is a service provider; AMOS must therefore model customer commitments, not only equipment uptime.

Each contract/site can define:

- customer;
- site;
- contract period;
- supported asset population;
- AECI-owned/customer-owned boundary;
- resident-team requirement;
- response-time target;
- availability target;
- planned support hours;
- blast-support obligations;
- primary/backup equipment requirement;
- included/excluded maintenance scope;
- chargeable work rules;
- KPI definitions;
- evidence requirements;
- penalty/service-credit exposure where contractually provided.

The system distinguishes:

- technical availability;
- service availability;
- contract KPI result;
- commercial consequence.

---

# 18. Blast-Support Readiness

AMOS does not design blasts or control initiation. It may ingest read-only service schedule data required to assess maintenance readiness.

A blast/service commitment object can include:

- site;
- planned charging window;
- required asset type/count;
- primary units;
- backup units;
- required pumping/delivery capacity;
- product availability signal;
- required competent crew;
- applicable permits/access constraints;
- critical spares kit;
- customer SLA reference.

Readiness output includes:

- asset technical state;
- open defects;
- PM status;
- statutory status;
- crew eligibility;
- spares availability;
- product/transfer readiness if data is available;
- forecasted failure risk when validated models exist;
- confidence and data freshness.

No AI readiness score may override a safety or legal hard stop.

---

# 19. Condition Monitoring and OT Integration

AMOS supports progressive instrumentation rather than making IoT a deployment prerequisite.

## 19.1 Manual-first

- hour meters;
- kilometres;
- pressure;
- flow;
- temperature;
- tank level;
- hose condition/cycles;
- calibration results;
- density/viscosity/QC observations;
- PLC alarm code entry when no interface exists.

## 19.2 Instrumented feeds

Where technically and contractually available:

- CAN/J1939;
- PLC/industrial protocol gateways;
- pressure/flow/temperature sensors;
- motor current;
- vibration;
- hydraulic pressure;
- tank/silo level;
- pump speed;
- dosing ratios;
- load cells;
- GPS/location;
- fuel/vehicle telematics;
- PLC alarms/events.

## 19.3 Edge rules

Site edge nodes buffer telemetry during connectivity loss, timestamp at source where possible, preserve quality flags and never fabricate missing samples.

---

# 20. Engineering Change Control

Changes to safety-critical or production-critical assets require controlled engineering records.

Change objects include:

- problem/opportunity;
- affected assets/models;
- risk assessment;
- technical justification;
- drawings/specification revision;
- BOM change;
- software/PLC configuration effect;
- SOP/job-plan effect;
- spare-parts effect;
- training effect;
- approvals;
- implementation campaign;
- verification;
- rollback where applicable.

The asset passport shows which change level each physical unit has received.

---

# 21. Document and Procedure Control

AMOS stores or references governed maintenance documents:

- OEM manuals;
- drawings;
- hydraulic/electrical schematics;
- SOPs;
- job plans;
- risk assessments;
- calibration procedures;
- inspection sheets;
- service bulletins;
- engineering changes;
- statutory certificates;
- site instructions.

Controlled documents require:

- owner;
- revision;
- approval;
- effective date;
- superseded state;
- applicability by asset/site;
- offline distribution status;
- acknowledgement where required.

Technicians receive the current approved revision applicable to the asset and task. Superseded documents remain auditable but are not presented as current instructions.

---

# 22. Incident, RCA and CAPA

Equipment-related incidents and near misses link directly to:

- asset/component;
- work history;
- person/crew;
- permit/isolation records;
- telemetry;
- parts installed;
- procedure revision;
- training/competence;
- prior defects;
- previous similar events.

CAPA actions can require work orders, engineering changes, training, procedure revision, supplier action or inspection campaigns.

---

# 23. AI and RAG Maintenance Intelligence

AI is an assistance layer over governed operational data, never the system of record and never an autonomous safety authority.

## 23.1 Technician troubleshooting copilot

Grounding sources, in priority order:

1. approved asset-specific SOP and troubleshooting documents;
2. OEM manuals and schematics;
3. validated engineering bulletins;
4. same-model service history;
5. verified resolved failures;
6. current telemetry/measurements;
7. generic engineering knowledge where allowed and clearly distinguished.

Every material recommendation must expose sources and uncertainty.

## 23.2 Planner agent

Can propose:

- job-plan reuse;
- duration estimates from history;
- parts reservations;
- schedule options;
- bundling by asset/access window;
- conflict detection;
- upcoming statutory work.

It cannot approve hazardous work, override competence gates or silently change PM policy.

## 23.3 Reliability agent

Can identify:

- bad actors;
- repeat-failure clusters;
- emerging life patterns;
- anomalous component consumption;
- candidate PM changes;
- candidate RCA triggers.

All engineering strategy changes require human review and version-controlled approval.

## 23.4 Stores agent

Can forecast stock-out risk, identify abnormal consumption and propose reorder/transfer actions. It cannot commit procurement spend without configured authorization.

## 23.5 Compliance agent

Can surface expiring credentials, missing evidence and overdue inspections. It must not claim legal compliance when underlying evidence is incomplete.

## 23.6 Management briefing agent

Produces traceable summaries of readiness, critical failures, backlog, compliance, costs and SLA risks from governed data.

---

# 24. Canonical Data Model

Minimum aggregate roots:

- `Tenant`
- `BusinessUnit`
- `Customer`
- `Contract`
- `Site`
- `Area`
- `Location`
- `Asset`
- `Component`
- `AssetConfiguration`
- `Meter`
- `TelemetryChannel`
- `ConditionReading`
- `Defect`
- `FailureEvent`
- `WorkRequest`
- `WorkOrder`
- `JobPlan`
- `TaskStep`
- `PermitReference`
- `RiskAssessment`
- `IsolationPlan`
- `LOTORecord`
- `Person`
- `Role`
- `Competency`
- `Authorization`
- `Roster`
- `Store`
- `StockItem`
- `InventoryBalance`
- `Reservation`
- `IssueReturn`
- `RepairableInstance`
- `PurchaseRequisition`
- `PurchaseOrder`
- `Supplier`
- `WorkshopJob`
- `CalibrationRecord`
- `ControlledDocument`
- `EngineeringChange`
- `Incident`
- `RCA`
- `CAPAAction`
- `StatutoryCredential`
- `ServiceCommitment`
- `BlastSupportWindow`
- `SLAResult`
- `CostEvent`
- `EvidenceObject`
- `AuditEvent`

## 24.1 Data invariants

- No work history is deleted to simulate a correction; corrections create audited superseding/compensating records.
- Component installation/removal events must preserve genealogy.
- Safety approvals must record actor, authority, time and evidence.
- Work completion does not erase open defects unless an explicit resolution event is recorded.
- Telemetry quality and source are stored with readings.
- AI-derived fields are labeled as derived, include provenance, and never overwrite observed facts.

---

# 25. Event Model

Core domain events include:

- `AssetStateChanged`
- `ComponentInstalled`
- `ComponentRemoved`
- `MeterReadingRecorded`
- `DefectRaised`
- `DefectRiskChanged`
- `WorkRequested`
- `WorkApproved`
- `WorkPlanned`
- `WorkScheduled`
- `WorkStarted`
- `WorkWaiting`
- `WorkTested`
- `WorkCompleted`
- `WorkClosed`
- `SafetyStopRaised`
- `IsolationVerified`
- `PermitReferenced`
- `PartReserved`
- `PartIssued`
- `PartReturned`
- `RepairableSentToWorkshop`
- `RepairableReleased`
- `CredentialExpiring`
- `CredentialExpired`
- `CompetencyExpiring`
- `TelemetryThresholdBreached`
- `FailureDetected`
- `RCARequired`
- `EngineeringChangeApproved`
- `ServiceCommitmentCreated`
- `ReadinessChanged`
- `SLARiskRaised`

Events are idempotent and carry tenant/site/asset correlation identifiers.

---

# 26. Permissions and Segregation of Duties

RBAC is combined with object scope and authority checks.

Examples:

- technician may execute assigned work but not approve own engineering change;
- planner may plan work but not self-certify competence;
- stores issuer may issue stock but inventory adjustments above threshold require approval;
- workshop technician may record rebuild work but QA release requires an authorized releaser when configured;
- engineer may propose PM revision but controlled activation requires designated approval;
- SHERQ may define safety policy and stop work; operational managers cannot bypass hard safety gates through ordinary workflow permissions;
- AI services have no independent approval authority.

---

# 27. Offline-First and Field Resilience

The field experience follows the existing rugged-hardware/offline architecture.

Offline capabilities must include:

- assigned work packs;
- current applicable SOPs/drawings;
- asset passport subset;
- required risk/permit/isolation forms;
- parts issue queue where site policy allows;
- measurements;
- photo/evidence capture;
- signatures;
- handover;
- local job status.

Conflict handling is domain-specific. Safety approvals, inventory balances and component installation history must not use naive last-writer-wins semantics.

---

# 28. Reporting and KPI Framework

## 28.1 Maintenance execution

- PM compliance;
- schedule compliance;
- backlog age;
- ready backlog;
- emergency work ratio;
- wrench-time delay categories;
- job-plan accuracy;
- waiting-for-parts time;
- waiting-for-permit/access time.

## 28.2 Reliability

- technical availability;
- operational availability;
- MTBF;
- MTTR;
- repeat-failure rate;
- bad actors;
- failure-mode Pareto;
- maintenance-induced failures;
- verified defect-elimination benefits.

## 28.3 Stores

- stock accuracy;
- critical stock-outs;
- service level;
- inventory turns;
- obsolete stock;
- repairable turnaround;
- supplier lead-time adherence;
- emergency procurement rate.

## 28.4 Safety/compliance

- overdue safety actions;
- overdue inspections;
- expired/expiring credentials;
- work stopped for safety;
- LOTO/permit completeness;
- procedure acknowledgement;
- competency expiry exposure.

## 28.5 Contract/service

- blast-support readiness;
- SLA response time;
- service availability;
- missed/slid support windows attributable to equipment;
- customer-impact downtime;
- cost of service failure.

Every KPI defines numerator, denominator, inclusion/exclusion rules, time zone, data source and owner. KPI definitions are versioned.

---

# 29. Integration Architecture

AMOS preserves DDE's adapter-only integration rule. Business modules never integrate directly with external vendor APIs.

Integration categories:

- incumbent ERP/EAM/SAP awareness;
- host-mine permit reference systems;
- AECI supply-chain/silo systems;
- telematics;
- PLC/edge gateways;
- identity/SSO;
- HR/roster/competency sources;
- procurement/finance;
- document repositories;
- group SHEQ incident systems;
- notification channels.

Each connector declares:

- system of record;
- read/write authority;
- field mapping;
- sync frequency;
- offline behavior;
- idempotency key;
- retry/dead-letter policy;
- data ownership;
- security classification;
- observability/SLO.

No external contract or unavailable API blocks core production development. Interfaces are implemented against documented internal contracts and configurable adapters; unavailable external systems use fixtures/simulators until credentials/contracts exist.

---

# 30. Implementation Architecture

AMOS is implemented as a customer/vertical domain pack over the DDE modular platform, not a source-code fork.

Recommended bounded contexts:

1. Asset Registry
2. Work Management
3. Planning & Scheduling
4. Safety & Permit
5. Workforce & Competency
6. Stores & Procurement
7. Workshop & Repairables
8. Reliability Engineering
9. Fleet & Compliance
10. Contract & Service Commitments
11. Condition Monitoring
12. Documents & Engineering Change
13. Incident/RCA/CAPA
14. Reporting & Economics
15. AI/RAG Intelligence
16. Integration & Edge

Shared canonical identity/event contracts prevent bounded contexts from owning duplicate master objects.

---

# 31. Release Strategy and Implementation Gates

A green vertical slice proves integration quality, not feature completeness. A module is complete only when its full acceptance matrix passes.

## Phase A — Foundation and master data

Deliver:
- tenant/site/customer/contract hierarchy;
- asset/component registry;
- person/role/competency model;
- document control;
- audit/event substrate;
- offline identity and device posture;
- import tools for assets, PMs, people, spares and documents.

Gate:
- signed asset census;
- component templates versioned;
- user/role/authority model tested;
- import rollback/reconciliation tested;
- offline master-data availability proven.

## Phase B — Safe work execution

Deliver:
- requests/defects;
- work-order state machine;
- job plans;
- HIRA/JSA;
- permit references;
- LOTO;
- PPE requirements;
- field execution;
- evidence/signatures;
- return-to-service.

Gate:
- hazardous job cannot enter execution without configured mandatory prerequisites;
- offline execution and sync conflict tests pass;
- completed repair requires test/verification when template mandates it;
- immutable audit trail verified.

## Phase C — Planning, shifts and control centre

Deliver:
- backlog planning;
- scheduling/capacity;
- shift handover;
- supervisor board;
- maintenance control centre;
- readiness engine.

Gate:
- capacity uses competence/availability rather than headcount;
- readiness explanations match underlying facts;
- stale signals are visibly marked;
- no opaque AI hard stops.

## Phase D — Stores, procurement and workshop

Deliver:
- stores;
- reservations/kitting;
- repairables/rotables;
- procurement workflow;
- workshop routing;
- component genealogy;
- supplier performance.

Gate:
- part issue is traceable to work/person/store;
- rotable genealogy survives multiple repair/install cycles;
- stock conflict handling tested offline;
- workshop QA release enforced.

## Phase E — Reliability and engineering

Deliver:
- reliability metrics;
- bad actors;
- RCA/CAPA;
- PM optimization;
- engineering change;
- calibration impact analysis.

Gate:
- metrics reconcile to source events;
- RCA actions cannot vanish into free text;
- PM changes are versioned/approved;
- engineering change applicability visible per asset.

## Phase F — Contracts and blast-support readiness

Deliver:
- contract/SLA model;
- service commitments;
- blast-support readiness;
- customer impact and economics.

Gate:
- service readiness distinguishes safety/legal hard stops from forecast risk;
- KPI formula versions are explicit;
- contract impact is traceable to technical events.

## Phase G — OT/telemetry and predictive intelligence

Deliver:
- telemetry gateway contracts;
- edge buffering;
- condition rules;
- validated predictive pilots;
- model monitoring.

Gate:
- data quality/freshness visible;
- predictive alerts meet precision/recall SLO before operational escalation;
- model recommendation never directly changes safety state or maintenance policy.

## Phase H — AI/RAG copilots

Deliver:
- governed document retrieval;
- technician troubleshooting;
- planner/reliability/stores/compliance agents;
- management briefing.

Gate:
- source citations required for technical recommendations;
- access controls propagate through retrieval;
- superseded procedures cannot be presented as current;
- evaluations cover hallucination, retrieval quality, unsafe advice, stale data and refusal/escalation behavior.

---

# 32. Definition of Done per Module

A module is not production-complete until all applicable areas are satisfied:

1. user workflows mapped end-to-end;
2. domain model and invariants specified;
3. API/command/event contracts defined;
4. permissions and segregation of duties implemented;
5. offline behavior defined and tested;
6. audit/evidence model complete;
7. notifications/escalations defined;
8. reports/KPIs implemented and reconciled;
9. imports/migration supported;
10. error/retry/conflict paths tested;
11. accessibility/rugged UX requirements met;
12. security/privacy threat cases tested;
13. observability/SLOs instrumented;
14. automated unit/integration/e2e tests green;
15. operator/admin runbook complete;
16. user acceptance scenarios passed;
17. safety-critical assertions reviewed by competent AECI roles before production activation.

---

# 33. Initial Acceptance Scenarios

The implementation program must include at least these end-to-end scenarios:

1. MMU breakdown 8 hours before a customer charging window; backup unit and competent technician identified; parts reserved; readiness changes and recovers.
2. Progressive-cavity pump removed from MMU A, rebuilt in Harare, placed into serviceable stock, later installed on MMU B with full genealogy.
3. Vehicle has valid PM but expired insurance: maintenance status may be healthy, road readiness is BLACK/blocked.
4. Technician is available but site induction expired: automatic dispatch rejected with explanation.
5. Temporary hose repair is accepted for restricted operation; expiry creates mandatory permanent repair before next defined window.
6. Meter calibration is later found out of tolerance; impact reconstruction identifies jobs/charges measured since last known-good calibration.
7. Critical seal-kit stock drops below service-risk threshold while multiple similar pumps are approaching expected life; stores risk escalates.
8. Work is completed offline underground; later sync detects inventory conflict without losing safety/evidence history.
9. Repeated identical failure triggers RCA; engineering change and revised PM are implemented; effectiveness tracked for defined observation period.
10. Superseded SOP remains in archive but technician receives only current approved revision.
11. Blast-support readiness is AMBER due to lack of backup unit, while all safety/legal conditions remain green; explanation is visible.
12. AI troubleshooting answer cites the correct MMU manual and similar resolved faults and refuses to assert isolation is physically complete.

---

# 34. Migration and Adoption

Initial migration sources may include:

- spreadsheets;
- PDF service sheets;
- paper checklists converted through controlled digitization;
- ERP exports;
- asset lists;
- stores lists;
- training matrices;
- statutory document registers;
- workshop repair logs;
- historical breakdown reports.

Migration rules:

- source record retained or hash-referenced;
- duplicate identities resolved through a staging/reconciliation queue;
- asset/component serial conflicts require human resolution;
- no historical record is silently invented to fill missing fields;
- unknown remains `unknown` with provenance.

Adoption uses technician-assisted configuration workshops so job plans, failure codes and asset taxonomies reflect real AECI equipment rather than desk assumptions.

---

# 35. Non-Goals

AMOS v1 does not:

- design or initiate blasts;
- autonomously authorize hazardous work;
- replace physical permits, locks or isolation practice;
- assume ownership of host-mine safety systems;
- require telemetry to function;
- require external APIs/contracts before core features can be built;
- fork DDE per customer;
- use generative AI as an unaudited system of record.

---

# 36. Outstanding AECI Discovery Inputs

The following real-world inputs are still required for final configuration but do not block platform implementation:

- actual Zimbabwe site roster and asset census;
- MMU/MCU/RRS/tanker models and component BOMs;
- current PM schedules and service sheets;
- actual breakdown history and failure coding;
- maintenance team roster, trades, shifts and authorization matrix;
- Harare workshop process and repairable inventory;
- stores structure, item master and supplier lead times;
- current ERP/CMMS and group IT integration constraints;
- actual security/telematics/silo-system vendors;
- host-mine permit formats;
- exact statutory licence records and conditions;
- customer contract/SLA clauses suitable for digitization;
- hazardous-area device restrictions;
- approved SOPs and drawings for RAG grounding.

Each missing input is represented as configurable master data or an adapter boundary, not hard-coded assumptions.

---

# 37. Source-of-Truth Hierarchy

For AECI Maintenance development, the hierarchy is:

1. **This document:** product and operating-model source of truth.
2. `DDE_AECI_Operations_Pack_Config_Spec.md`: Zimbabwe customer-specific configuration, statutory registers and site/asset pack details.
3. `DDE_AECI_Zimbabwe_Customer_Research.md`: research evidence and unresolved customer facts.
4. `DDE_Maintenance_Intelligence_ERP_Master_Plan_v2.md`: shared DDE platform architecture and cross-industry technical rules.
5. `DDE_Field_Experience_Rugged_Hardware_Spec.md`: field UX/device/hardware rules.
6. `DDE_Security_Trust_Architecture.md`: security/trust architecture.
7. `DDE_Modular_Platform_White_Label_Spec.md`: product-pack and no-fork implementation rules.

If these documents conflict on AECI Maintenance product behavior, this document governs unless the conflict concerns a specialist security/safety/legal rule that is explicitly stricter in its authoritative specialist document.

---

# 38. Implementation Directive

The next engineering step is not additional feature ideation. It is to translate this source of truth into:

- bounded-context implementation specifications;
- database schema and migrations;
- API/command/event contracts;
- screen/interaction specifications;
- role/permission matrix;
- acceptance-test catalog;
- integration adapter contracts;
- migration templates;
- seeded AECI asset/job-plan/failure-mode configuration;
- observability and deployment runbooks.

All future AECI Maintenance feature work must map to a canonical object, workflow, role, invariant, acceptance scenario and release gate in this document or add them through a version-controlled change.
