# AECI Maintenance — Operational Workflow Acceptance Addendum v1.0

**Purpose:** Add P0/P1 acceptance coverage for operational DDE Maintenance capabilities inherited by AECI Maintenance but previously under-specified in the AMOS baseline.

**Rule:** A green demo of a work-order happy path is not sufficient. Applicable P0 scenarios below must pass before the corresponding capability is considered complete.

---

# 1. Digital Job Card Pack

## JCP-P0-001 — Complete safety-bound work pack
**Given** a hazardous maintenance job requiring an approved procedure, HIRA/JSA, PPE, permit and LOTO,
**when** the planner releases the job,
**then** the technician receives one revision-pinned job card pack containing all required objects and cannot enter hazardous execution until configured mandatory prerequisites are satisfied.

## JCP-P0-002 — Procedure revision pinning
**Given** a released job using procedure revision 4,
**when** revision 5 is approved during execution,
**then** the active job does not silently switch revisions; policy determines continue/suspend/reissue and the audit trail records the decision.

## JCP-P0-003 — Offline job pack completeness
**Given** an assigned technician has synchronized the job,
**when** WAN connectivity is lost,
**then** required procedures, risk controls, PPE requirements, permit references, isolation instructions, drawings, job steps and evidence prompts remain locally available according to offline policy.

## JCP-P0-004 — Competence revalidation at start
**Given** a technician was eligible at assignment,
**when** a required authorization expires before work starts,
**then** AMOS blocks the relevant start transition and explains the expired requirement.

## JCP-P0-005 — Required calibrated instrument
**Given** a task requires a calibrated test instrument,
**when** the selected instrument is expired/quarantined,
**then** the task cannot record it as valid measurement equipment without an explicit governed exception path.

## JCP-P1-006 — Job history context
The job pack exposes recent relevant failure/repair/rework history without forcing the technician to search unrelated screens.

## JCP-P1-007 — Pause/wait reasons
A technician can pause a job using governed reasons; waiting time is separated from active execution time and is visible to planning/performance analytics.

---

# 2. Permit, HIRA/JSA, PPE and LOTO

## SAFE-P0-101 — Permit required
A task configured as permit-required cannot move into hazardous execution without the required valid permit reference/state.

## SAFE-P0-102 — Digital state is not physical proof
The system must not represent QR/NFC/location/digital acknowledgment alone as proof that physical isolation exists.

## SAFE-P0-103 — LOTO sequence and release
A LOTO-required job records isolation points, authorized actors, verification requirement and release/re-energization. Closeout cannot bypass the configured release workflow.

## SAFE-P0-104 — Isolation handover
An active isolation crossing a shift boundary remains active and is explicitly handed over; shift acknowledgment does not release isolation.

## SAFE-P0-105 — PPE gating
A job configured with specialized PPE requirements shows those requirements before execution and blocks work when a configured hard requirement is known to be unmet.

## SAFE-P1-106 — Safety-critical supersession
A newly issued safety-critical procedure/risk control can force suspension/reissue according to policy and leaves a reconstructable audit trail.

---

# 3. Rework and Repair Quality

## RWK-P0-201 — Suspected rework detection
A same/similar asset-component failure inside a configured recurrence window creates a suspected-rework relationship to the prior job instead of an unrelated isolated ticket.

## RWK-P0-202 — No automatic technician blame
Suspected rework does not affect an individual performance score until a governed adjudication classifies the event.

## RWK-P0-203 — Failed functional test
When a post-maintenance functional test fails, the work cannot progress directly to verified/closed; a rework/corrective path is created.

## RWK-P0-204 — Rework cost lineage
Confirmed rework cost can be reconstructed from labour, material, travel/recovery, downtime/service consequence and external cost records where applicable.

## RWK-P1-205 — Original job preserved
The original job is never overwritten by a rework job; both remain independently auditable and linked.

---

# 4. Recurring Breakdowns and Bad Actors

## REC-P0-301 — Recurrence threshold
Configurable asset/component/failure-mode thresholds create repeat-warning, recurring or bad-actor escalation states.

## REC-P0-302 — Recurring failure closure gate
A job that crosses a configured recurring-failure threshold cannot be closed through the ordinary path without the required reliability review/action.

## REC-P0-303 — Failure relationship graph
The asset/component passport can reconstruct failure → job → diagnosis → part → repair → verification → next failure relationships.

## REC-P1-304 — Fleet-wide systemic review
A pattern tied to part batch, supplier, procedure revision or asset family can trigger a fleet-wide applicability review.

## REC-P1-305 — Repeated no-fault-found
Repeated NFF events within policy thresholds escalate to structured technical/reliability investigation rather than repeatedly disappearing into closed history.

---

# 5. Technician KPI and Performance

## KPI-P0-401 — Explainable scorecard
Every displayed KPI exposes its numerator, denominator, period, included/excluded jobs and data-quality state.

## KPI-P0-402 — Delay normalization
Parts, permit, access, customer/production, weather and other governed uncontrollable waits do not count as active execution time against the technician.

## KPI-P0-403 — Rework adjudication dependency
Unadjudicated suspected rework does not reduce technician quality scores.

## KPI-P0-404 — Safety incentive protection
The KPI model must not penalize legitimate stop-work/safety escalation or create a speed metric that rewards bypassing safety gates.

## KPI-P0-405 — Team vs individual attribution
Multi-person jobs do not automatically attribute every outcome identically to every participant; configured responsibility/role attribution is available.

## KPI-P1-406 — Difficulty normalization
Routine inspections and complex breakdown diagnosis are not directly ranked on raw completion counts/durations without task-class/context normalization.

## KPI-P1-407 — Coaching view
Supervisor performance view includes trends, competence gaps and coaching actions, not only ranking.

---

# 6. Tool Control and Audits

## TOOL-P0-501 — Controlled tool identity
A serialized/calibrated controlled tool has unique identity, custodian/location, condition and inspection/calibration status.

## TOOL-P0-502 — Tool audit reconciliation
A toolbox/service-kit audit compares expected vs physically confirmed contents and creates open exceptions for missing/damaged/unserviceable items.

## TOOL-P0-503 — Calibration due gate
Expired or quarantined instruments cannot be selected as valid calibrated equipment for tasks that require calibration.

## TOOL-P0-504 — Out-of-tolerance impact reconstruction
Given an instrument found out of tolerance,
when the last-known-good point is established,
then AMOS can identify jobs/measurements/assets potentially affected and create review/retest/rework actions.

## TOOL-P0-505 — Issue/return custody
Shared/special tools support reservation, issue, job association, return and condition capture with immutable custody history.

## TOOL-P1-506 — Repeated loss/damage trend
Repeated tool loss/damage is visible for management action without silently converting it into technician fault before review.

---

# 7. Shift Handover

## SHIFT-P0-601 — Active risk continuity
Open breakdowns, isolations, suspended permits, temporary repairs, bypasses and critical waiting items remain active across handover.

## SHIFT-P0-602 — Acknowledgment is not closure
Incoming-shift acknowledgment does not close the underlying defect, isolation, permit or work order.

## SHIFT-P0-603 — Unfinished job safe state
A paused job crossing shift boundary records the actual safe state and required restart/revalidation conditions.

---

# 8. Inspection and Deferred Defects

## DEF-P0-701 — Inspection creates structured defect
A failed inspection item can create a traceable defect linked to the inspection, asset/component and evidence.

## DEF-P0-702 — Deferred defect governance
A deferred defect requires reason, risk, controls/operating limits where applicable, owner, review date and corrective-work linkage.

## DEF-P0-703 — No generic override for critical defect
Safety/legal hard-stop defects cannot be deferred using a generic convenience override.

## DEF-P1-704 — Defect aging/escalation
Deferred/open defects age visibly and escalate according to criticality/review policy.

---

# 9. Return to Service and Verification

## RTS-P0-801 — Execution complete is not verified
A configured verification-required job cannot move from execution completion straight to final closure without required testing/verification.

## RTS-P0-802 — Failed test creates corrective path
A failed leak/load/interlock/calibration/roadworthiness/other configured test creates a rework/corrective state, preserving original evidence.

## RTS-P0-803 — Independent QA when required
Jobs configured for independent QA cannot be self-released by the same actor where segregation-of-duty policy forbids it.

## RTS-P1-804 — Verification window
A post-repair monitoring/verification window can detect early recurrence and relate it back to the repair.

---

# 10. Maintenance-Induced Failure and NFF

## MIF-P0-901 — Causal review required
A suspected maintenance-induced failure is flagged for review and linked to preceding work but does not automatically assign blame.

## MIF-P1-902 — Cause taxonomy
Review can classify workmanship, wrong part, contamination, adjustment, procedure, design, external cause, supplier defect or insufficient evidence.

## NFF-P0-903 — NFF evidence
No-fault-found closure records the reported symptom, tests, measurements, conditions and next monitoring action.

---

# 11. Technical Escalation

## ESC-P0-1001 — Context-preserving escalation
A technician escalation carries asset, job, symptoms, measurements, alarms, attempted steps, procedure/drawing revisions and current safe state.

## ESC-P0-1002 — Remote guidance audit
Remote technical guidance is captured as part of the job history with actor/time/source context.

## ESC-P1-1003 — AI cannot authorize
AI guidance cannot perform permit approval, isolation signoff, hazardous-work authorization or return-to-service authorization.

---

# 12. Job Planning and Ready-to-Schedule

## PLAN-P0-1101 — Pack completeness visibility
Planner sees missing scope, procedure, risk assessment, competence, parts, tools, calibration, drawings, access/permit and labour prerequisites separately.

## PLAN-P0-1102 — Capacity uses eligible labour
Schedule capacity is based on actual roster + competence + authorization + access, not headcount alone.

## PLAN-P1-1103 — Blast/service window
AECI service/charging commitments are visible as constraints when scheduling maintenance on supporting assets.

---

# 13. Knowledge Capture

## KNOW-P0-1201 — Closed work creates structured learning
Closed/verified work preserves confirmed failure/remedy, unsuccessful attempts where recorded, labour, parts, measurements and technician feedback.

## KNOW-P0-1202 — Procedure change remains governed
Technician feedback can propose a procedure/job-plan change but cannot directly modify an approved controlled procedure.

## KNOW-P1-1203 — Repeat solution retrieval
Future jobs can retrieve approved relevant prior repair history without exposing superseded/unauthorized controlled content.

---

# 14. Safe Field Device Behavior

## FIELD-P0-1301 — Zone/task restrictions
Configured hazardous-area/task policy can suppress non-critical notifications and restrict camera/voice/device interaction.

## FIELD-P0-1302 — Geolocation is advisory
Geofence/zone inference cannot by itself prove permit, isolation or worker-safe-state completion.

## FIELD-P1-1303 — Offline safety pack
Essential safety and execution information remains accessible during site connectivity loss.

---

# 15. End-to-End Golden Flows

## GOLD-P0-A — Planned hazardous MMU repair
`defect → triage → plan → reserve parts/tools → verify competence → assemble procedure/HIRA/PPE/permit/LOTO pack → release → technician accepts → make safe → execute → measurements/evidence → functional test → release isolation → return to service → follow-up verification → close → learning/history`

Expected result: every transition and revision is auditable; no safety prerequisite is bypassed.

## GOLD-P0-B — Breakdown followed by rework
`breakdown → corrective job → repair → functional test pass → return to service → repeat failure inside window → suspected rework → quality adjudication → confirmed rework → corrective job → RCA threshold → verified fix → performance/reliability update`

Expected result: original repair remains intact, costs are traceable, technician KPI changes only after adjudication.

## GOLD-P0-C — Recurring pump failure
`failure 1 → failure 2 repeat warning → failure 3 recurring threshold → reliability review → RCA → component/part/procedure/PM action → effectiveness review`

Expected result: AMOS cannot represent all three as unrelated closed jobs.

## GOLD-P0-D — Out-of-tolerance instrument
`tool audit/calibration fail → quarantine instrument → identify last-known-good → reconstruct affected jobs/measurements → engineering review → retest/rework actions → close impact assessment`

Expected result: calibration failure has operational consequence traceability.

## GOLD-P0-E — Shift crossing with active isolation
`job in progress → isolation active → shift handover → incoming competent/authorized team accepts → permit/isolation revalidation as configured → resume → test → release → close`

Expected result: no handover action can silently clear the isolation.

---

# 16. Release Gate

A capability area in this addendum is **not complete** until:

- applicable P0 tests pass;
- applicable P1 tests pass or have explicit approved mitigation;
- offline behavior is tested where field execution applies;
- audit reconstruction is possible;
- RBAC and competency are both enforced where relevant;
- AI paths have equivalent or stricter safety boundaries than non-AI paths.
