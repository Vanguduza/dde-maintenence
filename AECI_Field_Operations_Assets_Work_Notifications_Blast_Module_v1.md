# AECI Maintenance — Field Operations, Asset Custody, Work Sources, Notifications & Blast Module v1.0

**Status:** Mandatory AECI AMOS operational specialization
**Purpose:** Define the site/artisan experience for asset custody, job origination, notifications and surface-site blast reporting.

---

# 1. Site-Centric Operating Model

Every AECI surface or underground service site is a first-class operational scope containing:

- customer/host site;
- AECI team/roster;
- site supervisor/management chain;
- site asset register;
- local stores/tool locations;
- maintenance backlog;
- planned/scheduled maintenance;
- active breakdowns;
- permits/access constraints;
- procedures/manual applicability;
- document/report obligations;
- notification calendar;
- service/blast windows where applicable;
- site-specific security/data-classification policy.

The system must work when a technician is permanently assigned, temporarily posted or assisting another site.

---

# 2. Site Asset Register

Each site has an authoritative **Asset Register** containing every asset/component under AECI artisan care within the agreed service boundary.

## 2.1 Asset record minimum fields

- asset ID;
- site;
- area/location;
- customer ownership vs AECI ownership;
- asset class/type;
- make/model;
- serial number;
- registration/fleet number where applicable;
- photograph/hero image;
- current condition/state;
- operational/readiness state;
- criticality;
- commissioning/installation data where available;
- parent/child component tree;
- meter/hour/odometer values where relevant;
- current custodian/team;
- notes;
- open defects/issues;
- active work orders;
- planned/scheduled maintenance;
- maintenance history/completed jobs;
- rework/recurring-failure warnings;
- statutory/compliance status where applicable;
- manuals/procedures/drawings;
- calibration/inspection requirements;
- parts/BOM references where available;
- warranty/vendor/OEM references where available;
- linked donor-form records;
- linked blast/service history where applicable.

## 2.2 Asset condition/state

Keep separate fields for:

- physical/technical condition;
- operational state;
- maintenance state;
- safety/compliance state;
- service-readiness state.

Example operational states can include:

- available;
- available with defect/degraded;
- planned maintenance;
- breakdown;
- awaiting parts;
- awaiting tool/vendor;
- workshop;
- test/verification;
- out of service;
- compliance/safety hold.

The UI must explain why an asset is unavailable or degraded.

---

# 3. Asset Page

Each asset page is the technician's single operational passport.

## 3.1 Header

- image;
- asset name/ID;
- serial number;
- site/location;
- condition/state badges;
- current responsibility/custodian;
- critical alerts;
- next scheduled maintenance;
- readiness status.

## 3.2 Tabs/sections

### Overview
- notes;
- meter readings;
- current condition;
- criticality;
- basic identity.

### Maintenance
- upcoming scheduled maintenance;
- historical schedules;
- completed jobs;
- breakdowns;
- autonomous-maintenance jobs;
- rework;
- recurrence/bad-actor history.

### Open issues
- defects;
- deferred defects;
- inspections failed;
- active corrective actions;
- waiting reasons.

### Documents
- repair manuals;
- SOPs;
- drawings/schematics;
- maintenance procedures;
- calibration instructions;
- approved bulletins;
- donor-form records.

Documents shown must be applicable/current and access-controlled.

### Components
- serialized component tree;
- install/remove history;
- component condition;
- failure/rebuild history.

### Reports
- PM sheets;
- trip tests;
- calibrations;
- daily checks;
- unusual occurrences/near misses tied to asset;
- blast records where applicable.

### Telemetry/condition
- manual/sensor readings;
- freshness/quality;
- trends;
- alarms.

---

# 4. My Assets

Field technicians receive a **My Assets** surface showing assets currently under their care.

Assignment is derived from:

`current site posting + team/craft responsibility + asset responsibility rules + temporary assignment/delegation`

## 4.1 My Assets card

Show:

- image;
- asset ID/name;
- serial/fleet number;
- condition/readiness;
- next maintenance due;
- open defects count/severity;
- active job;
- overdue report/checklist indicator;
- urgent notification badge.

## 4.2 Filters

- all;
- due maintenance;
- breakdown;
- degraded;
- awaiting parts;
- inspection/report due;
- compliance hold;
- recurring failure;
- asset class.

## 4.3 Temporary posting

When a technician changes site:

- new site access is time/scope bound;
- My Assets changes accordingly;
- prior restricted offline data expires/removes per policy;
- work history remains enterprise records but is not necessarily visible outside authorization scope.

---

# 5. Three Work/Job Origination Sources

Every job/work order uses one canonical work object but must record its source and source-specific controls.

## 5.1 Source A — Scheduled / Planned

Origin examples:

- calendar PM;
- hour/km/cycle PM;
- statutory inspection;
- calibration due;
- trip test due;
- campaign/shutdown work;
- condition-triggered planned intervention;
- approved follow-up/RCA action.

Workflow:

`schedule trigger → planning → job pack readiness → assignment → release → technician execution → verification → close → next-due update`

## 5.2 Source B — Technician Self-Initiated

Two primary classes:

### Breakdown
Technician identifies/responds to an unplanned equipment failure.

Minimum fast-start path:

`select asset → breakdown/symptom → consequence/safe state → create work intent → supervisor/control notification → safety/competence checks → job pack completion as required → execute/repair`

Emergency capture must be quick, but safety gates are not removed.

### Autonomous Maintenance
Technician initiates an approved low-level inspection/care/defect-correction task within their authorization.

Examples may include approved routine care/check activities configured by AECI.

Autonomous Maintenance cannot be used to bypass planned-work controls for tasks requiring specialist competence, permits, isolation or management approval.

## 5.3 Source C — Supervisor / Management Created

Examples:

- defect follow-up;
- customer complaint;
- audit finding;
- improvement action;
- RCA/CAPA action;
- management instruction;
- campaign/shutdown task;
- compliance action;
- inspection follow-up.

Creator can set priority, required completion date, scope and assignee/team within their authority.

## 5.4 Common source metadata

Each job records:

- `source_type`;
- source actor/system;
- source reference;
- created time;
- asset/site;
- reason;
- priority/consequence;
- originating inspection/report/event if any;
- whether preplanned vs emergent;
- whether it contributes to planned/unplanned KPI categories.

Source never changes the truth/history after creation; reclassification requires an audited correction.

---

# 6. Job Inbox / My Work

Technician Home includes:

- jobs due today;
- overdue jobs;
- planned upcoming jobs;
- active breakdowns;
- autonomous-maintenance drafts;
- jobs awaiting technician acceptance;
- jobs paused/waiting;
- follow-up verification;
- required forms/reports due;
- asset alerts.

Each job opens the full Digital Job Card Pack defined by the capability inheritance specification.

---

# 7. Notification and Obligation Engine

AMOS requires an event/obligation notification engine, not scattered hard-coded reminders.

## 7.1 Notification sources

- PM due/upcoming/overdue;
- calibration due/upcoming/overdue;
- trip test due;
- daily vehicle checklist due/missed;
- timesheet due/missed/returned;
- donor form/report due;
- work assigned/reassigned;
- job priority escalation;
- breakdown created;
- parts/tool ready;
- permit/access change;
- job paused too long;
- follow-up verification due;
- deferred defect review due;
- competency/authorization expiry;
- tool calibration/inspection due;
- toolbox audit due;
- compliance certificate expiry;
- supervisor approval requested;
- unusual occurrence/near miss routing;
- recurring-failure escalation;
- readiness/service-window risk;
- blast record/report due.

## 7.2 Channels

- in-app notification center;
- push notification;
- e-mail where approved/configured;
- future approved enterprise messaging adapters.

Sensitive details remain inside authenticated AMOS; notification previews use data-minimised wording.

## 7.3 Notification rules

Each event defines:

- recipients by role/scope/responsibility;
- severity;
- channel;
- lead time/reminder cadence;
- acknowledgement requirement;
- escalation ladder;
- quiet-hours/shift behavior;
- deduplication key;
- closure condition.

Acknowledging a notification never closes the underlying job/defect/obligation.

## 7.4 Personal daily digest

Optional start-of-shift digest:

- jobs due;
- reports/forms due;
- assets degraded;
- critical alerts;
- tool/competency expiries;
- handover items.

---

# 8. Surface-Site Blast Module

The Blast Module is an **AECI maintenance/quality/service-recording module** for authorized surface-site millwright/technical personnel. It must not become an uncontrolled blast-design system.

It records approved operational data, quality checks, equipment/service events and produces AECI-controlled reports using donor templates.

## 8.1 Authorization

Access requires:

- appropriate AECI role;
- site assignment;
- configured blast-module authorization;
- data-classification permission;
- applicable current competence where required.

The module does not replace statutory blasting authority, host-mine blast design/approval or initiation systems.

---

# 9. Blast Record / Event Identity

Each blast-support event has a unique `BlastRecord` containing:

- blast/event ID;
- customer/site/pit/bench or approved location reference;
- date/time/shift;
- authorized crew;
- charging unit/MMU;
- relevant supporting equipment;
- linked work orders/defects;
- approved source/reference for blast plan metadata if integrated;
- donor reports/forms used;
- event status;
- signatures/approvals.

Sensitive blast details are classified and access-controlled.

---

# 10. Charge-Per-Hole Capture

Authorized users can record approved charge data per hole from donor forms or integrations.

Possible structured fields include those already required by AECI's approved donor/report process, such as:

- hole identifier;
- planned/actual charge fields;
- recorded product amount;
- timestamps;
- equipment/MMU reference;
- operator/technician;
- recorded quality measurements;
- exception/issue code.

The exact schema, formulas, tolerances and operational parameters are imported from AECI-approved donor documents/procedures rather than invented by AMOS.

Repeating rows must remain efficient offline and generate the official donor-format report.

---

# 11. Density / Quality Tracker

The module supports structured quality checks such as density/cup-density records where required by AECI procedure.

Capture can include:

- sample/check timestamp;
- blast/event reference;
- equipment/MMU;
- approved measurement fields;
- measured density value;
- location/hole/group reference where donor requires it;
- technician/operator;
- instrument/method reference where applicable;
- pass/deviation state based only on AECI-approved configured limits;
- comments/actions.

The system must not invent quality limits. Limits are controlled configuration sourced from approved procedures/documents.

## 11.1 Density analytics

For the event the system can calculate and display approved summaries including:

- count of measurements;
- average density;
- min/max;
- deviations/exceptions;
- time trend;
- linkage to equipment/service issues.

---

# 12. Blast Event Logger

Chronological event log records notable operational/service events such as:

- charging started/stopped;
- equipment changeover;
- breakdown/fault;
- repair/intervention;
- product/service interruption;
- quality exception;
- waiting/delay reason;
- resumption;
- completion;
- unusual occurrence/near miss reference;
- supervisor/technical escalation.

Entries retain actor/time and cannot be silently rewritten after finalization.

---

# 13. Equipment Performance Capture

Blast event can record values already required by AECI-approved operating/reporting processes, including configured fields for:

- total emulsion/product used;
- flow-rate records;
- pumping-speed records;
- operating time;
- equipment downtime;
- breakdown duration;
- parts/intervention where applicable;
- quality measurements;
- related defects/work orders.

Operational thresholds/limits come from controlled AECI documentation, not software defaults.

---

# 14. Consolidated Blast Report

On event completion AMOS generates a consolidated blast/service-quality report using the approved AECI donor template.

Report data can include, when present in the approved template/schema:

- event/site/bench identity;
- date/shift;
- personnel;
- MMU/equipment used;
- total emulsion/product used;
- charge-per-hole summary/detail;
- approved powder-factor field/result;
- average cup density and measurement summary;
- recorded flow rate;
- recorded pumping speed;
- charging duration;
- downtime/delay;
- issues/breakdowns;
- corrective maintenance/work-order links;
- unusual occurrences/near misses;
- comments;
- signoff/approval.

Any derived blasting metric, including powder factor, must use a versioned AECI-approved formula/input definition from controlled configuration. AMOS must not guess formulas or default blast-design assumptions.

---

# 15. Automatic Report Assembly

The blast report is assembled from a structured event graph:

`BlastRecord`
`→ charge rows`
`→ density checks`
`→ event log`
`→ MMU/asset data`
`→ work orders/breakdowns`
`→ delay events`
`→ authorized calculations`
`→ signatures`
`→ donor PDF rendering`

The user should not have to retype data already captured elsewhere.

---

# 16. Breakdown Integration From Blast Module

If equipment fails during charging/service support:

1. user logs event in blast timeline;
2. select/create breakdown work intent;
3. asset state changes appropriately;
4. Digital Job Card Pack workflow begins;
5. breakdown/downtime timestamps feed the blast event;
6. repair/verification outcome links back;
7. blast report automatically includes the incident/service interruption summary according to donor/report rules.

This prevents blast reporting and maintenance history from becoming two inconsistent narratives.

---

# 17. Surface vs Underground Applicability

- surface millwright users receive Blast Module when authorized/configured;
- underground sites may use a different approved charge/service reporting pack if AECI supplies it;
- the same generic donor-form engine can digitize underground records;
- no assumption is made that surface blast forms or workflows apply unchanged underground.

---

# 18. Dashboard Views

## Technician
- My Assets;
- My Work;
- reports/forms due;
- current blast/service event where applicable;
- PM/calibration due;
- notifications.

## Site supervisor
- site asset register/readiness;
- planned vs breakdown work;
- overdue PM/forms;
- asset assignment;
- blast-support event status;
- open equipment issues;
- team workload;
- approvals.

## Regional/management
- multi-site asset health;
- PM/report compliance;
- breakdown/rework trends;
- service/blast readiness;
- key quality summaries;
- document/report completion posture.

---

# 19. Key Domain Objects

- `SiteAssetRegister`
- `AssetResponsibilityAssignment`
- `TechnicianPosting`
- `WorkIntent`
- `WorkOrigin`
- `ScheduleTrigger`
- `AutonomousMaintenanceIntent`
- `NotificationRule`
- `NotificationInstance`
- `ReportingObligation`
- `BlastRecord`
- `BlastChargeEntry`
- `BlastQualityCheck`
- `BlastEventLogEntry`
- `BlastEquipmentMetric`
- `BlastDerivedMetric`
- `BlastReportRecord`

---

# 20. Core Events

- `asset.assigned_to_site`
- `asset.responsibility_changed`
- `posting.started`
- `posting.ended`
- `work.created_scheduled`
- `work.created_breakdown`
- `work.created_autonomous`
- `work.created_supervisor`
- `obligation.due`
- `notification.sent`
- `notification.acknowledged`
- `blast.created`
- `blast.charge_recorded`
- `blast.quality_recorded`
- `blast.event_logged`
- `blast.breakdown_linked`
- `blast.completed`
- `blast.report_generated`
- `blast.report_approved`

---

# 21. Acceptance Gates

1. Every site can maintain a complete scoped asset register.
2. Each asset page exposes image, serial number, states, notes, history, open issues, scheduled maintenance and current applicable manuals.
3. My Assets reflects current posting/responsibility and does not expose unrelated restricted site assets.
4. All three job sources create the same governed canonical work object while preserving source provenance.
5. Technician breakdown creation is fast enough for field use but does not bypass safety/competency controls.
6. Notification acknowledgements do not close source obligations.
7. Due PM/reports/calibrations/checklists generate deduplicated, role-scoped notifications.
8. Blast module is unavailable without correct authorization/site scope.
9. Blast data, quality checks and maintenance incidents share common asset/job identities.
10. Consolidated blast report is generated from captured structured data without retyping and rendered through the approved donor template.
11. Derived blast metrics use only explicitly approved/versioned formulas and inputs.
12. Breakdown events created during blast support automatically link to maintenance work and the final event report.
13. Offline surface-site capture survives connectivity loss and synchronizes idempotently.
14. Restricted blast/event data obeys export, offline, retention and RAG classification controls.
