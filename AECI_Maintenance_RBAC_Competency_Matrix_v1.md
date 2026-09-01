# AECI Maintenance — RBAC, Scope, Competency & Authorization Matrix v1.1

**Status:** Authoritative authorization baseline for AMOS

---

# 1. Authorization Principle

A successful access/operation decision may require all of:

`authenticated identity + role permission + tenant/BU/site scope + object relationship + data classification + current posting/assignment + competency/technical authorization + segregation of duty + object-state policy`

RBAC permission alone never proves competence or authorization to perform technical work.

---

# 2. Core Roles

## Field and maintenance
- Technician / Artisan
- Senior Technician / Lead Artisan
- Auto Electrician / Electrical Technician
- Fitter / Mechanical Technician
- Instrumentation / Controls Technician
- Driver / Operator where in scope
- Site Supervisor / Foreman
- Maintenance Planner / Scheduler
- Maintenance Engineer
- Reliability Engineer
- Workshop Technician
- Workshop Supervisor
- QA/Test Releaser

## Support
- Stores Controller / Supervisor
- Buyer / Procurement Officer / Approver
- SHERQ Officer / Manager
- Training / Competency Administrator
- Fleet Administrator
- Compliance Administrator
- Document Controller
- Calibration / Tool Custodian
- Engineering Change Approver
- Contract / SLA Manager

## Management/platform
- Site Maintenance Manager
- Regional Maintenance Manager
- Business Unit Manager
- Executive Viewer
- Security Administrator
- Tenant / Platform Administrator
- Integration Administrator
- Audit / Read-only Reviewer
- DDE Implementation Administrator

Actual AECI job titles map to these capability roles during configuration.

---

# 3. Scope Model

Permissions are evaluated against:

- tenant;
- business unit;
- country/region;
- customer;
- site;
- department/team;
- current technician posting;
- asset responsibility;
- explicit work assignment;
- temporary delegation;
- record/document classification;
- object state.

A role granting `asset.view` does not grant national unrestricted asset access.

---

# 4. Technician / Artisan

Default scope: current authorized site posting + My Assets/service responsibility + assigned jobs.

Can normally:

- view My Assets and authorized site assets;
- view current applicable manuals/procedures;
- view/execute assigned Digital Job Card Packs subject to competence/safety gates;
- create self-initiated breakdown work against authorized assets;
- create Autonomous Maintenance work only for approved task classes;
- capture approved donor forms/reports required by role;
- enter timesheets/checklists/measurements/evidence;
- raise defects/unusual occurrences/near misses;
- request technical escalation;
- acknowledge notifications/shift handover;
- view their own explainable performance measures;
- use authorized surface Blast Module only when separately authorized.

Cannot by default:

- approve their own independent QA where separation is required;
- modify controlled donor templates/procedures;
- self-award competence;
- bulk export restricted records;
- view unrelated site employee/performance data;
- modify retention/security policy;
- bypass permit/LOTO/safety stops.

---

# 5. Site Supervisor / Foreman

Scope: assigned site/team unless explicitly delegated broader scope.

Can:

- view site asset register and asset responsibility assignments;
- create/assign/reassign supervisor-created work;
- triage breakdowns and defects;
- review job-pack readiness;
- review/accept shift handover;
- approve configured work/QA/return-to-service actions where authorized;
- view contextual team performance;
- manage temporary asset responsibility delegation within authority;
- view due obligations/forms/notifications;
- review blast-service status where authorized;
- route unusual occurrence/near-miss records.

Cannot self-grant higher technical competence or erase audit/history.

---

# 6. Planner / Scheduler

Can:

- plan/schedule work;
- create planned work and schedules;
- bind job plans/procedures/risk requirements;
- reserve parts/tools;
- inspect competence/availability needed for scheduling;
- create reporting obligations;
- view due PM/calibration/trip-test/report information.

Cannot mark a person competent or perform physical safety verification merely because they can schedule work.

---

# 7. Maintenance / Reliability Engineer

Can:

- view engineering/reliability history;
- run recurrence/bad-actor/rework analysis;
- create/manage RCA/FMEA/CAPA/PM optimization/engineering change;
- review maintenance-induced failure/NFF;
- approve technical changes within delegated authority;
- define controlled formulas/limits only through governed document/configuration change with approved source evidence.

Cannot silently modify historical finalized records.

---

# 8. Document Controller

Can:

- receive/quarantine donor PDFs;
- edit draft form schemas/coordinate maps;
- coordinate human review;
- run/inspect fidelity tests;
- approve/publish/supersede templates within delegated document-control authority;
- manage document applicability/revision/classification/retention metadata.

Cannot alter finalized historical form instances by editing a template.

Maker-checker can require template mapper and publisher to be different actors.

---

# 9. Tool / Calibration Custodian

Can:

- register controlled tools/instruments;
- manage custody/issue/return;
- perform/record toolbox audits;
- upload calibration/inspection evidence;
- quarantine expired/failed equipment;
- initiate out-of-tolerance impact assessment.

Cannot restore calibration validity without governed evidence/authorization.

---

# 10. SHERQ / Compliance

Can within scope:

- manage risk/HIRA/JSA/PPE policy;
- review near misses/unusual occurrences/incidents;
- manage CAPA/compliance registers;
- review permit/LOTO policy records;
- access restricted safety records according to need-to-know;
- manage or approve classification/retention requirements where delegated.

Sensitive event visibility may be narrower than ordinary site-maintenance visibility.

---

# 11. Surface Blast Module Authorization

Blast Module access is not implied by being a millwright/technician alone.

Required policy can include:

- current allowed site posting;
- permitted role;
- Blast Module authorization;
- applicable technical training/competence;
- data-classification scope.

Capabilities are separable:

- `blast.view`
- `blast.create_event`
- `blast.capture_charge`
- `blast.capture_quality`
- `blast.log_event`
- `blast.link_breakdown`
- `blast.generate_report`
- `blast.review`
- `blast.approve`
- `blast.export`

No AMOS permission confers statutory blasting authority outside AECI/host-mine rules.

---

# 12. Security Administrator

Can through privileged audited interfaces:

- administer permission roles/scopes;
- manage security policy/configuration;
- review sessions/devices/audit/security alerts;
- manage certificate/key/integration-trust configuration within delegated boundaries;
- initiate/review access recertification.

High-impact changes can require dual control.

Security Administrator cannot normally:

- delete audit history;
- rewrite finalized maintenance records;
- automatically access every business record merely by holding the admin role;
- bypass legal/evidence hold.

---

# 13. Platform Administrator

Infrastructure/platform administration is separated where practical from business-content authority.

Admin actions are audited. Direct production database/storage access is tightly controlled and exceptional; AMOS must not depend on infrastructure administrators routinely reading operational records.

---

# 14. Export Permissions

Export/download/print is separate from view for classified records.

Examples:

- `record.view`
- `record.export`
- `record.bulk_export`
- `record.print`

RESTRICTED or high-volume bulk export can require additional approval.

---

# 15. Donor Form Permissions

Separate capabilities:

- `template.view`
- `template.map_draft`
- `template.review`
- `template.publish`
- `template.supersede`
- `form.create`
- `form.edit_draft`
- `form.submit`
- `form.sign`
- `form.approve`
- `record.view`
- `record.export`
- `record.amend`

A user may capture an approved donor form without any right to modify its template.

---

# 16. My Assets Authorization

`My Assets` is a derived access projection, not a manual favourites list.

Sources:

- current site posting;
- craft/team responsibility;
- explicit asset assignment;
- temporary delegation with expiry.

Scope re-evaluates when posting/delegation changes. Historical records remain stored but current visibility follows policy.

---

# 17. Work-Origin Permissions

### Scheduled / Planned
Generated by scheduler/planner/system trigger under an approved maintenance strategy.

### Technician Breakdown
Technician may create against authorized assets. Creation does not automatically grant competence to perform every resulting repair.

### Technician Autonomous Maintenance
Allowed only for configured low-level task classes and authorization boundaries.

### Supervisor / Management Created
Requires work-create authority within organizational/site scope.

All origins converge on the same downstream job-pack, safety and competence rules.

---

# 18. Competency Model

Competencies are typed/scoped.

### Technical trade
Mechanical, electrical, instrumentation/controls, hydraulics, pumps, hoses/pressure, welding/fabrication where applicable, PLC/CAN diagnostics, vehicle maintenance, calibration discipline.

### Asset/model authorization
MMU/MCU/RRS/tanker/EVDS/silo/specific OEM model/component family as configured.

### Safety authorization
LOTO, isolation verification, electrical switching/isolation, confined space, work at height, lifting/rigging, hot work, pressure systems, chemical handling, hazardous-area work/device use.

### Site/legal eligibility
Site induction, medical fitness where law/policy permits/requires, driver licence/professional status, mine appointments and explosives-related authorizations where applicable.

### Blast Module competence
Any AECI-defined role/training needed to capture/review specific blast/quality records.

---

# 19. Competency Status and Scope

Statuses:

- PENDING
- VALID
- EXPIRING
- EXPIRED
- SUSPENDED
- REVOKED
- NOT_APPLICABLE

Scope can be tenant, BU, site, asset class/model, component family, procedure, task or permit type.

Specific scope takes precedence where policy requires it.

---

# 20. Assignment and Execution Revalidation

Before assignment evaluate:

- role permission;
- site/object scope;
- roster availability;
- required trade/model authorization;
- safety authorization;
- site induction/access;
- medical/legal eligibility where applicable;
- working-time/fatigue policy if configured;
- conflicting assignments.

Eligibility is revalidated again at `StartWork` because competence/access can change after scheduling.

Results: `ELIGIBLE`, `ELIGIBLE_WITH_WARNING`, `INELIGIBLE`. Warnings never downgrade a hard requirement.

---

# 21. Temporary Posting / Delegation

Requires:

- grantor;
- recipient;
- scope/site/assets/permissions;
- reason;
- start;
- expiry;
- approval where required;
- audit event.

Temporary support must not create unintended permanent access.

---

# 22. Data Classification Interaction

Record classes:

- PUBLIC
- INTERNAL
- CONFIDENTIAL
- RESTRICTED
- HIGHLY_RESTRICTED

Classification can restrict:

- view scope;
- offline cache eligibility;
- export/print;
- notification detail;
- AI indexing/retrieval;
- retention/hold handling.

---

# 23. Segregation-of-Duty Examples

- technician cannot self-approve independent QA where required;
- template mapper cannot publish own mapping when maker-checker enabled;
- purge requester and purge approver can be separated;
- high-impact permission grants can require independent approval;
- tool-audit exception cannot be silently removed without resolution evidence;
- security/platform admin cannot fabricate operational safety approvals.

---

# 24. Audit Requirement

Material authorization decisions should be reconstructable with:

- actor;
- action/object;
- role/scope;
- competency outcome/evidence where relevant;
- data classification;
- policy version;
- allow/deny result;
- timestamp/correlation.

---

# 25. Implementation Acceptance

The authorization subsystem is not complete until tests prove:

1. expired/suspended competence blocks as configured;
2. role permission cannot bypass competence;
3. competence cannot bypass object/site scope;
4. My Assets changes with posting/delegation;
5. technician cannot access unrelated-site restricted records by direct ID;
6. Blast Module requires separate authorization;
7. export permission is separately enforced;
8. document capture permission does not allow template modification;
9. admin cannot forge operational approval through generic CRUD;
10. schedule-time eligibility is revalidated at work start;
11. offline client cannot continue using revoked/stale authorization beyond configured validity;
12. API/search/export/offline/RAG paths enforce equivalent or stricter policy than the visible UI.
