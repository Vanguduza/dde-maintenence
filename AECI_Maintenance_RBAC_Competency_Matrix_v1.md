# AECI Maintenance Operations System — RBAC, Competency & Authority Matrix v1.0

**Status:** Production design baseline.
**Date:** 1 September 2026
**Applies to:** AECI Maintenance Operations System (AMOS).

---

# 1. Control Model

AMOS uses four independent but composable controls:

1. **Role permission:** may the user perform this class of action?
2. **Object scope:** may the user act on this business unit/site/store/asset/customer?
3. **Competency/authorization:** is the person technically/safety-qualified for this task?
4. **Segregation-of-duty rule:** is the action prohibited because the same person performed an incompatible prior step?

An action is permitted only when all mandatory controls pass.

`ALLOW = ROLE ∧ SCOPE ∧ COMPETENCE_WHERE_REQUIRED ∧ SOD ∧ OBJECT_STATE_POLICY`

---

# 2. Core Roles

## Field and maintenance roles

- Technician / Artisan
- Senior Technician
- Auto Electrician / Electrical Technician
- Fitter / Mechanical Technician
- Instrumentation / Controls Technician
- Driver / Operator (where in platform scope)
- Site Supervisor / Foreman
- Maintenance Planner
- Maintenance Engineer
- Reliability Engineer
- Workshop Technician
- Workshop Supervisor
- QA/Test Releaser

## Support roles

- Stores Controller
- Stores Supervisor
- Buyer / Procurement Officer
- Procurement Approver
- SHERQ Officer
- SHERQ Manager
- Training / Competency Administrator
- Fleet Administrator
- Compliance Administrator
- Document Controller
- Engineering Change Approver
- Contract / SLA Manager

## Management and platform roles

- Site Maintenance Manager
- Regional Maintenance Manager
- Business Unit Manager
- Executive Viewer
- Tenant Administrator
- Integration Administrator
- Security Administrator
- Audit/Read-Only Reviewer
- DDE Implementation Administrator

Roles are templates. Actual AECI job titles map to these capabilities during discovery.

---

# 3. Permission Matrix

Legend: `R` read, `C` create, `U` update/execute, `A` approve/release, `X` no permission by default.

| Domain / Action | Technician | Supervisor | Planner | Engineer/Reliability | Workshop Sup. | Stores | SHERQ | Regional Mgr | Admin |
|---|---:|---:|---:|---:|---:|---:|---:|---:|---:|
| Asset passport | R | R | R | R/U governed fields | R | R | R | R | U config |
| Raise defect/request | C | C | C | C | C | C limited | C | C | C |
| Approve work | X | A scoped | X | A engineering scope | A workshop scope | X | X | A | X |
| Plan work | X | U limited | C/U | U | U workshop | X | X | R | X |
| Schedule work | X | U site | C/U | R | U workshop | X | X | R | X |
| Execute assigned work | U competent | U competent | X | U if competent | U competent | X | X | X | X |
| Complete work | U own | U own/crew where policy | X | U own | U own/crew | X | X | X | X |
| Close work | X | A | X | A engineering work | A workshop | X | X | A exception | X |
| Safety stop | C | C | C | C | C | C | C/U/A | C | X |
| Approve risk assessment | X | scoped | X | scoped engineering | scoped | X | A | X | X |
| Verify isolation | competent only | competent only | X | competent only | competent only | X | audit | X | X |
| Change competency | X | X | X | X | X | X | R | X | U/A via training admin |
| Issue stock | X or field scan request | X | X | X | X | C/U | X | X | X |
| Inventory adjustment | X | X | X | X | X | U below threshold/A supervisor | X | X | X |
| Create PR | C request | C request | C request | C request | C request | C/U | X | C | X |
| Approve procurement | X | X | X | X | X | scope dependent | X | A threshold | X |
| RCA | contribute | contribute | contribute | C/U | contribute | contribute | contribute/A safety | A review | X |
| PM change proposal | X | C | C | C/U | C | X | C safety aspect | R | X |
| PM activation | X | X | X | A designated | X | X | A safety concurrence where required | A policy | X |
| Engineering change | X | C | X | C/U/A by authority | C | X | A safety concurrence | A threshold | X |
| Workshop QA release | X | X | X | X | A if authorized | X | X | X | X |
| Statutory credential update | X | C evidence | X | X | X | X | C/U/A scoped | R | X |
| Contract/SLA config | X | X | X | R | X | X | R relevant | C/U/A | X |
| Readiness override | X | X | X | X | X | X | X | X | X |
| Readiness acknowledgement | R | U | R | U | U | R | U | U | X |
| Connector config | X | X | X | X | X | X | X | X | U integration admin |
| User/role config | X | X | X | X | X | X | X | X | U tenant/security admin |

There is deliberately no generic readiness override. Blocking facts are resolved in their source domains.

---

# 4. Competency Model

Competencies are typed and scoped.

## 4.1 Technical trade competence

Examples:
- mechanical maintenance;
- electrical maintenance;
- instrumentation/control;
- hydraulics;
- pneumatics;
- process-pump maintenance;
- hose/pressure-system inspection;
- welding/fabrication where applicable;
- PLC diagnostics;
- CAN/J1939 diagnostics;
- vehicle maintenance;
- calibration discipline.

## 4.2 Asset/model authorization

Examples:
- MMU general maintenance;
- specific MMU model authorization;
- MCU authorization;
- RRS/re-pump authorization;
- tanker product-transfer system;
- EVDS station maintenance;
- silo transfer systems;
- specific OEM pump family.

## 4.3 Safety authorization

Examples:
- LOTO authorized person;
- isolation verifier;
- electrical switching/isolation level;
- confined-space entrant/standby/supervisor;
- work-at-height;
- lifting/rigging;
- hot-work permit receiver;
- pressure-system work;
- chemical handling;
- hazardous-area device/work authorization.

## 4.4 Site and legal eligibility

Examples:
- site induction;
- medical fitness;
- driving licence class;
- professional driving requirement;
- explosives-related appointment/authorization where applicable;
- mine-specific permits/appointments.

---

# 5. Competency Scope

Competency can apply at one or more scopes:

- tenant-wide;
- Zimbabwe business unit;
- site;
- asset class;
- model;
- component family;
- procedure;
- task type;
- permit type.

Specific scope takes precedence over generic scope.

Example: `MMU_MAINTENANCE = valid` does not imply authorization for a new model if the model policy requires a dedicated authorization.

---

# 6. Competency Status

Statuses:

- `PENDING`
- `VALID`
- `EXPIRING`
- `EXPIRED`
- `SUSPENDED`
- `REVOKED`
- `NOT_APPLICABLE`

Expiry warning thresholds are configurable by competency type.

Suspension/revocation takes immediate precedence over an otherwise valid expiry date.

---

# 7. Assignment Policy

Before work assignment, evaluate:

1. role permission;
2. site/object scope;
3. roster availability;
4. required trade;
5. mandatory model/asset authorization;
6. safety authorization;
7. site induction;
8. medical validity;
9. legal driver requirements if driving is part of assignment;
10. working-time/fatigue constraint if configured;
11. conflicting active assignments;
12. supervisor-to-technician coverage requirements where configured.

Results:
- `ELIGIBLE`
- `ELIGIBLE_WITH_WARNING`
- `INELIGIBLE`

Warnings cannot be used to downgrade a hard requirement.

---

# 8. Execution-Time Revalidation

Eligibility is revalidated at `StartWork`, not only at schedule time.

Reasons:
- competence may expire between planning and execution;
- site access can be revoked;
- medical/authorization status can change;
- work scope may change;
- safety policy revision may add requirements.

If eligibility changed, the system blocks execution and explains the exact missing control.

---

# 9. Segregation of Duties

Minimum rules:

1. A technician cannot independently approve and close a high-risk engineering modification they executed.
2. A person cannot self-award or self-renew competency.
3. Inventory adjustments above configured threshold require a second approver.
4. Repair/rebuild QA release requires a different authorized person where asset criticality or workshop policy mandates independence.
5. Engineering change proposal and final approval must be separated above configured risk threshold.
6. Safety incident investigator independence rules can be configured for serious incidents.
7. Procurement requester and approver separation follows value thresholds.
8. Tenant/security administrators cannot use administrative privilege to fabricate operational safety approvals.

---

# 10. Safety Authority Hierarchy

AMOS distinguishes:

- **work performer** — executes work;
- **work supervisor** — controls work execution;
- **permit authority/receiver** — references/accepts host process according to site model;
- **isolation authorized person** — performs/controls isolation steps;
- **isolation verifier** — confirms according to approved procedure;
- **SHERQ authority** — can issue policy-level stops/actions;
- **return-to-service authority** — releases equipment where required.

One person may hold multiple authorities only where policy explicitly permits it.

---

# 11. Competency Evidence

Competency records can require evidence:

- certificate;
- trade-test record;
- licence;
- training attendance;
- assessment result;
- supervisor sign-off;
- OEM certificate;
- induction record;
- medical certificate reference.

Evidence expiry and competency expiry are linked but not assumed identical unless configured.

---

# 12. Training Matrix

Required views:

- person × competency;
- site × required competency coverage;
- asset class × authorized maintainers;
- expiry calendar;
- next 30/60/90 day capacity risk;
- contract/service commitment × competent crew availability;
- missing competency preventing schedule readiness.

A future expiry that leaves a site without minimum competent coverage is a planning risk and must surface before the expiry date.

---

# 13. Example Eligibility Rules

## MMU process-pump repair

Required:
- mechanical/process-pump trade competence;
- MMU or applicable model authorization;
- site induction;
- medical valid;
- LOTO authorization if performer is required to isolate;
- chemical/pressure-system procedure acknowledgement where configured.

## Road deployment of MMU

Required for driver:
- correct licence class;
- professional driver status if required;
- site/route policy prerequisites;
- vehicle itself must be legally road-ready.

Person eligibility does not override vehicle legal status.

## PLC diagnostic work

Required:
- electrical/instrumentation role;
- controls competence;
- applicable isolation authority;
- model-specific authorization where configured.

---

# 14. Administrative Controls

Competency administrators may manage records but cannot bypass evidence/approval rules.

Administrative override, where legally and operationally permissible, must require:

- explicit override authority;
- reason code;
- free-text justification;
- second approval for high-risk competence;
- expiration time;
- immutable audit event.

No override path is provided for statutory/legal requirements that do not permit organizational waiver.

---

# 15. Audit Requirements

Every permission/competency-sensitive decision records:

- person/action;
- object;
- evaluated policies;
- role(s);
- scope;
- competency evidence IDs;
- pass/fail predicates;
- policy version;
- timestamp.

This allows reconstruction of why a person was considered eligible at the time of work.

---

# 16. Implementation Acceptance

The RBAC/competency subsystem is not complete until tests prove:

1. expired induction blocks assignment/start;
2. suspended competence blocks immediately;
3. role permission alone cannot bypass competency;
4. competency alone cannot bypass object scope;
5. planner cannot self-award competence;
6. admin cannot forge operational approval through generic CRUD;
7. schedule-time pass is revalidated at work start;
8. future competency expiry appears as capacity risk;
9. audit trail explains every eligibility failure;
10. offline client cannot start a task using stale cached competence beyond configured validity policy.
