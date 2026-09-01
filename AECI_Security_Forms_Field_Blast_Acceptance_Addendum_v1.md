# AECI Maintenance — Security, Donor Forms, Field Assets, Notifications & Blast Acceptance Addendum v1.0

**Rule:** Applicable P0 tests below are release blockers.

---

# 1. Security & Data Protection

## SEC-AECI-P0-001 — Cross-site direct-object denial
A technician authorized for Site A cannot retrieve a restricted Site B asset/report by URL/API object ID.

## SEC-AECI-P0-002 — Revocation propagation
Removing a site posting/role prevents new access and causes previously eligible offline records to expire/remove according to policy.

## SEC-AECI-P0-003 — Final record immutability
A finalized/signed maintenance report cannot be silently edited; correction creates an auditable amendment/superseding record.

## SEC-AECI-P0-004 — Export separate from view
A user with view permission but without export permission cannot download/bulk-export the protected record.

## SEC-AECI-P0-005 — Legal hold
A valid legal/evidence hold blocks purge regardless of ordinary retention expiry.

## SEC-AECI-P0-006 — Audit protection
Normal product administrators cannot delete or rewrite security audit history through ordinary application APIs.

## SEC-AECI-P0-007 — AI ACL propagation
RAG/AI cannot retrieve or summarize a source document that the requesting user cannot access directly.

## SEC-AECI-P0-008 — Offline encryption
Device inspection confirms offline database/document cache is not stored as plaintext user-accessible files.

## SEC-AECI-P0-009 — Sensitive notification minimization
Restricted event notifications do not expose sensitive detail on lock-screen/e-mail preview beyond configured minimum information.

## SEC-AECI-P0-010 — Restore verification
A backup/restore test reconstructs finalized donor-template records and validates stored hashes/lineage.

## SEC-AECI-P1-011 — Dual control
Configured high-impact operations such as retention-policy reduction, high-volume export or legal-hold release require independent approval.

## SEC-AECI-P1-012 — Service identity
High-trust integrations can use scoped workload identity/mTLS without secrets embedded in client applications.

---

# 2. Donor PDF Fidelity Engine

## PDF-P0-101 — Immutable donor
After donor publication, the exact original PDF bytes/hash remain available and unchanged.

## PDF-P0-102 — Generic capture renderer
A new donor document can be converted into a usable digital capture form without writing a new document-specific app screen.

## PDF-P0-103 — Exact donor output
Sample payload renders into the approved donor layout and passes configured page-dimension, coordinate and pixel/fidelity tolerances.

## PDF-P0-104 — Dual retention
Every finalized form stores both the structured payload and generated official PDF, linked to donor/schema/map/renderer revisions.

## PDF-P0-105 — Historical revision integrity
Publishing donor revision N+1 does not alter or regenerate finalized records created under revision N.

## PDF-P0-106 — Offline idempotency
Submitting the same offline form operation repeatedly due to network retry creates one canonical finalized record, not duplicates.

## PDF-P0-107 — Formula reproducibility
Calculated donor fields reproduce server-side using the same versioned expression, unit and rounding rules.

## PDF-P0-108 — Sandboxed parsing
Malicious/unsupported active PDF content cannot execute in the application/rendering environment or propagate into generated reports.

## PDF-P0-109 — Unauthorized template record denial
Direct URL/search/AI paths cannot expose restricted donor-form records outside scope.

## PDF-P1-110 — Golden render regression
Changing rendering library/font/runtime triggers golden render tests and blocks publication if controlled appearance drifts beyond tolerance.

---

# 3. Site Asset Register / My Assets

## ASSET-P0-201 — Site register completeness model
Every maintained asset belongs to an authorized site/service boundary and can be represented with identity, serial, state, history, open issues, PM and manuals.

## ASSET-P0-202 — Asset passport history
Asset page shows completed work, upcoming/previous maintenance, open defects, rework/recurrence links and current applicable documents without mixing other asset identities.

## ASSET-P0-203 — My Assets scoping
A technician sees assets under their current posting/responsibility plus explicit temporary delegation, not unrelated national assets.

## ASSET-P0-204 — Posting change
Changing technician posting updates My Assets and access scope while preserving enterprise historical records.

## ASSET-P1-205 — State explainability
Unavailable/degraded state identifies contributing reason rather than only a colour/status label.

---

# 4. Work Origin

## WORKSRC-P0-301 — Scheduled source
A schedule/PM trigger creates canonical work with `source_type=scheduled` and retains schedule provenance.

## WORKSRC-P0-302 — Breakdown self-initiation
A technician can quickly create a breakdown against an authorized asset while preserving safety/competency controls and notifying required supervision.

## WORKSRC-P0-303 — Autonomous Maintenance
Authorized low-level autonomous work can be self-initiated but cannot bypass task-class permit/LOTO/specialist controls.

## WORKSRC-P0-304 — Supervisor-created work
Authorized supervisor/management user can create/assign work with reason, priority and due date while retaining creator/source provenance.

## WORKSRC-P0-305 — Canonical downstream workflow
All three origins enter the same governed work/job-card lifecycle after source-specific creation steps.

## WORKSRC-P1-306 — KPI classification
Planned/unplanned/autonomous categories remain reproducible from source/history and cannot be silently relabelled to improve KPI results.

---

# 5. Notifications

## NOTIF-P0-401 — PM due
Upcoming/due/overdue PM generates one deduplicated obligation notification to correct responsible roles according to policy.

## NOTIF-P0-402 — Report due
Required timesheet/checklist/calibration/trip-test/report obligations create reminders and escalation without closing the obligation on acknowledgement.

## NOTIF-P0-403 — Assignment notification
Work assignment/reassignment reaches the relevant technician and disappears/resolves correctly when assignment changes.

## NOTIF-P0-404 — Notification privacy
Sensitive report/near-miss/blast notifications deep-link into authenticated AMOS and do not expose restricted content in the preview.

## NOTIF-P1-405 — Offline delivery reconciliation
Notifications received while offline reconcile without duplicate alert storms when connectivity returns.

---

# 6. Blast Module

## BLAST-P0-501 — Authorization and site scope
Blast module is inaccessible unless user role, site posting and configured authorization permit access.

## BLAST-P0-502 — Controlled-form lineage
Charge records, quality/density records, event log and consolidated report are tied to approved donor template/schema revisions.

## BLAST-P0-503 — Equipment identity
Blast event links to exact MMU/supporting assets; breakdowns created during the event link to the same canonical asset/work history.

## BLAST-P0-504 — Quality limits governed
The module cannot invent density/quality thresholds; pass/deviation logic requires configured approved source values.

## BLAST-P0-505 — Derived metric governance
Powder factor or any other derived blast metric is calculated only when an approved versioned formula/input definition is configured; missing formula causes unavailable/not-calculated state rather than guessing.

## BLAST-P0-506 — Automated consolidation
Final report pulls captured charge rows, density/quality data, equipment metrics, event log and linked breakdowns without manual retyping of already recorded data.

## BLAST-P0-507 — Donor fidelity
Final blast report passes the same donor-PDF fidelity controls as other AECI official reports.

## BLAST-P0-508 — Breakdown feedback loop
A breakdown logged during the event creates/links maintenance work, records downtime/service interruption and appears in the consolidated event report according to template rules.

## BLAST-P0-509 — Offline event capture
Authorized field users can capture required event/quality/charge records offline and synchronize without duplication.

## BLAST-P0-510 — Restricted data controls
Blast records obey classification, offline eligibility, export, retention and RAG-access policies.

---

# 7. End-to-End Golden Flows

## GOLD-AECI-P0-1 — Scheduled maintenance donor pack
`schedule due → notification → planner/job pack → technician My Work → asset passport → donor PM capture form → safe execution → verification → donor-identical PDF → signed record vault → next-due update`

## GOLD-AECI-P0-2 — Self-initiated breakdown
`technician My Assets → asset → create breakdown → supervisor notification → Digital Job Card Pack → repair → verification → maintenance report donor PDF → recurrence/rework analysis`

## GOLD-AECI-P0-3 — Daily vehicle check failure
`checklist obligation → technician capture donor form → safety-critical defect → vehicle state/readiness hold → supervisor notification → corrective work → verification → finalized checklist + repair record`

## GOLD-AECI-P0-4 — Surface blast support with breakdown
`authorized blast event → charge/quality/event capture → MMU breakdown → linked maintenance work → verified repair/resume → calculations using approved formulas → consolidated donor blast report → signatures → restricted records vault`

## GOLD-AECI-P0-5 — Template revision
`document controller receives new donor revision → quarantine/validate/map → golden fidelity test → approve/publish → old revision superseded for new work → old finalized records remain unchanged`
