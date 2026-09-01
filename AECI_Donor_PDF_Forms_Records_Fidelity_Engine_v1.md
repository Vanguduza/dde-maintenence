# AECI Maintenance — Donor PDF Forms & Records Fidelity Engine v1.0

**Status:** Mandatory AECI AMOS document digitisation and report-generation specification
**Purpose:** Convert AECI's existing approved maintenance PDFs into secure digital data-capture experiences while preserving the exact approved donor-document appearance in generated reports.

---

# 1. Core Requirement

AECI already uses controlled forms and reports for maintenance, safety, fleet, calibrations and operations. AMOS must **digitise those documents without redesigning them away**.

The original AECI PDF is the **donor template**. The system derives a machine-readable capture schema and rendering map from the donor, presents a practical mobile/web capture form, and then renders the captured data back into the approved donor layout.

The final report must be visually equivalent to the approved donor PDF to the level required by AECI document-control acceptance.

## 1.1 Two-surface model

1. **Capture surface:** ergonomic, responsive, field-friendly digital form generated from the donor schema. It may reorganise interaction for usability, conditional logic and mobile screens.
2. **Record surface:** exact/fidelity rendering onto the donor PDF layout for the official saved/printed report.

The capture UX does not replace the donor layout. It is an input interface for producing the controlled record.

---

# 2. Initial AECI Donor Document Families

The engine must support at minimum:

- maintenance job cards/work reports;
- artisan timesheets;
- scheduled/planned maintenance sheets;
- trip-test reports;
- calibration records/certificates;
- daily vehicle checklists;
- equipment inspection checklists;
- autonomous-maintenance forms;
- unusual-occurrence reports;
- near-miss reports;
- HIRA/JSA/task risk forms;
- toolbox/tool-audit forms;
- breakdown/failure reports;
- shift handover forms where AECI uses controlled documents;
- blast charge-per-hole records;
- density/quality-control records;
- blast event logs;
- consolidated blast reports;
- any future AECI donor PDF approved through the template-publishing workflow.

No document type should require a new hard-coded application screen if the generic schema can represent it.

---

# 3. Template Lifecycle

Canonical lifecycle:

`DONOR_RECEIVED → QUARANTINED → VALIDATED → EXTRACTED → MAPPED → REVIEWED → FIDELITY_TESTED → APPROVED → PUBLISHED → ACTIVE → SUPERSEDED/RETIRED`

## 3.1 Donor intake

On upload/import:

- store original bytes immutably;
- calculate cryptographic hash;
- capture document title/code;
- donor revision/version;
- effective date;
- owner/department;
- site/business-unit applicability;
- page count/page dimensions;
- confidentiality classification;
- retention class;
- required approval roles;
- whether signatures are required;
- whether attachments/photos are permitted;
- whether the document is safe/eligible for offline use.

## 3.2 Quarantine and validation

- parse only inside sandboxed workers;
- reject/enforce review for active JavaScript, embedded executable content, unsupported encryption or malformed structures;
- never trust AcroForm field metadata without validation;
- preserve donor visual page content but not unsafe active objects.

---

# 4. Donor-to-Schema Conversion Pipeline

## 4.1 Extraction sources

The converter may use:

- AcroForm field metadata if present;
- PDF text boxes and coordinates;
- vector lines/tables;
- font/label positions;
- human-assisted field annotation;
- AI-assisted field inference;
- OCR only where necessary for scanned donor documents;
- manually defined calculated/conditional fields.

AI/OCR output is always provisional until human template review.

## 4.2 Generated form schema

Each field records at minimum:

- stable field ID;
- business meaning/name;
- label;
- data type;
- required/optional;
- page;
- donor coordinate rectangle;
- font family/size/style used for output where required;
- alignment;
- line wrapping rules;
- allowed values/options;
- validation rules;
- unit;
- decimal precision;
- calculation expression if governed;
- dependency/conditional visibility;
- source (`manual`, `sensor`, `asset`, `user`, `job`, `calculated`, `integration`);
- editability;
- signature requirement;
- audit sensitivity;
- data classification;
- retention behavior.

Supported field types include:

- text;
- multiline text;
- integer/decimal;
- currency;
- date/time/datetime;
- checkbox;
- radio/select/multi-select;
- yes/no/NA;
- signature;
- employee/user reference;
- asset/component reference;
- job/work-order reference;
- site/location reference;
- serial number;
- measurement + unit;
- photo/evidence reference;
- table/repeating row;
- calculated field;
- derived KPI/summary;
- approval/signoff block.

---

# 5. Coordinate Map and Render Contract

For every output field the engine retains a page coordinate map independent of the capture UX.

Example logical mapping:

```yaml
field: vehicle_registration
page: 1
rect_pt: [412.4, 62.2, 531.0, 84.0]
font:
  family: Helvetica
  size: 9
alignment: left
overflow: shrink_then_wrap
```

The coordinate map itself is:

- schema validated;
- versioned;
- hashed;
- approved with the donor template;
- immutable once published.

Changes create a new template revision.

---

# 6. Capture Form Generation

One generic renderer creates data-capture pages from the schema.

## 6.1 Field technician mode

Optimised for:

- gloves/large touch targets;
- limited typing;
- offline execution;
- numeric keypad for measurements;
- barcode/QR asset selection;
- auto-populated employee/site/asset/job details;
- progressive sections rather than full PDF page scrolling;
- save draft;
- required-field validation;
- conditional fields;
- signatures;
- safe photo capture where permitted;
- voice notes where site/device policy permits.

## 6.2 Desktop/supervisor mode

Supports:

- table/repeating-row editing;
- review of original donor and capture fields side-by-side;
- approval/signoff;
- exception comments;
- report preview;
- version comparison.

## 6.3 Exact-donor preview

At any point after sufficient data is available, the user may preview the record rendered against the donor PDF so they can see the official output before submission.

---

# 7. Auto-Population and Context Binding

The engine can populate donor fields from trusted AMOS objects:

- employee name/ID/role;
- site;
- date/shift;
- asset ID;
- asset description;
- serial number;
- meter/odometer/hour reading;
- work-order number;
- planned maintenance reference;
- procedure revision;
- permit reference;
- supervisor;
- customer;
- vehicle registration;
- calibration tool ID;
- blast ID;
- calculated totals/averages.

Auto-populated values remain visible to the user and retain provenance.

---

# 8. Calculations

Calculated fields use a controlled expression engine, not arbitrary code.

Requirements:

- deterministic;
- formula versioned with template;
- units explicit;
- rounding explicit;
- missing-input behavior explicit;
- calculations reproduced server-side before finalization;
- calculation provenance included in audit metadata.

The engine supports sums, averages, min/max, counts, ratios and domain-approved formulas.

---

# 9. Signatures and Approvals

Signature objects bind:

- signer identity;
- role/authority;
- intent (`prepared`, `checked`, `approved`, `received`, etc.);
- timestamp;
- template revision;
- payload hash;
- generated PDF hash or pre-finalization hash sequence;
- optional device/session context.

A drawn signature image alone is not the security control; identity and cryptographic/audit binding are.

Multi-stage approval is supported.

---

# 10. Final PDF Rendering

## 10.1 Fidelity objective

Generated official records must preserve:

- donor page dimensions;
- logos;
- lines;
- boxes;
- headings;
- fonts/typographic appearance as permitted by available/licensed fonts;
- document numbers/revision markings;
- field placement;
- tables;
- signature blocks;
- pagination.

Captured data is overlaid into approved coordinate regions.

## 10.2 No redesign by default

The final report must not substitute a new branded template merely because it is easier to render. A modern capture screen may exist, but the official record uses the donor layout.

## 10.3 Overflow policy

If captured content exceeds a donor field:

1. enforce configured max length where the original form expects it;
2. shrink within approved minimum font threshold where permitted;
3. wrap within the mapped box;
4. if still impossible, require user correction or create a controlled continuation/appendix only when the donor policy allows it.

Never silently clip legally/operationally material text.

---

# 11. Fidelity Acceptance Testing

Every published donor template must pass:

- page count comparison;
- page dimension comparison;
- static donor-layer hash/visual comparison;
- field-coordinate tolerance checks;
- font/size checks where controlled;
- sample-data golden render;
- pixel/image-diff threshold test;
- manual document-controller signoff.

A template is not production-approved merely because the data is technically readable.

## 11.1 Pixel-diff golden set

Maintain canonical sample payloads and expected renders per template revision. CI/regression testing renders those samples and compares output against approved golden images/PDFs within configured tolerances.

Any rendering-library/font upgrade that changes official appearance triggers document-engine regression testing.

---

# 12. Structured Payload + PDF Dual Record

For each finalized form retain:

1. structured data payload;
2. generated official PDF;
3. donor template revision/hash;
4. coordinate-map/schema revision/hash;
5. signatures/approvals;
6. evidence references;
7. renderer build/version;
8. audit trail.

Why both are required:

- PDF satisfies human/audit/document continuity;
- structured data enables dashboards, search, KPI, recurrence, scheduling and AI;
- regeneration can be verified;
- corrupted/missing PDF can be detected against hash;
- source data does not need to be scraped back out of a PDF.

---

# 13. Report Retention and Records Vault

Finalized forms enter a controlled records vault indexed by:

- record type;
- document code/revision;
- date/period;
- employee/team;
- site;
- asset;
- job/work order;
- blast ID where applicable;
- status;
- signatures/approvals;
- retention class;
- legal hold;
- classification.

Records remain available according to AECI retention policy and permissions.

---

# 14. Timesheets

Timesheet donor forms may auto-populate:

- technician identity;
- site;
- date/shift;
- jobs/time entries from AMOS;
- active/wait/travel/training categories;
- overtime where configured;
- supervisor approval.

System-derived hours must remain reviewable before submission. Final PDF uses the approved AECI timesheet donor.

---

# 15. Scheduled Maintenance Forms

Scheduled maintenance donor forms can bind to:

- PM schedule;
- asset/component;
- planned date;
- procedure/job plan;
- required readings/checklist;
- parts/tools;
- technician;
- findings/defects;
- verification;
- next due date/reading.

Completion can automatically update PM compliance and next-due logic only after configured verification/approval.

---

# 16. Trip Tests and Calibration Forms

Trip-test/calibration records bind to:

- asset/instrument;
- test instrument used;
- instrument calibration status;
- procedure revision;
- setpoints/actual readings;
- tolerance;
- pass/fail;
- corrective work if failed;
- technician/checker/approver;
- next due date.

Failed test/calibration automatically creates/links the required defect/work/rework path where configured.

---

# 17. Vehicle Daily Checklists

Daily vehicle donor forms bind to the vehicle asset and can include:

- driver/technician;
- registration/fleet ID;
- odometer;
- tyres;
- lights;
- fluids;
- brakes;
- fire/safety equipment;
- leaks/damage;
- statutory document checks;
- defect severity;
- roadworthiness/dispatch gate.

Safety-critical defects can drive readiness/dispatch stops.

---

# 18. Unusual Occurrence and Near-Miss Forms

These forms must support restricted classification and strict need-to-know scope.

Data may include:

- event time/location;
- people/asset involved;
- description;
- immediate actions;
- potential consequence;
- photos/evidence;
- supervisor/SHERQ routing;
- investigation reference;
- corrective action/CAPA.

Notifications must not leak detailed event content onto lock screens/e-mail previews.

---

# 19. Autonomous Maintenance Forms

Self-initiated Autonomous Maintenance may use donor forms generated from the relevant inspection/maintenance template. It can create structured defects or follow-on jobs without bypassing safety/competency requirements.

---

# 20. Template Administration UI

Document-controller/admin workspace:

- donor upload;
- security validation result;
- page preview;
- field auto-detection;
- drag/resize coordinate mapping;
- field properties;
- form grouping/conditional logic;
- formula builder;
- auto-population source mapping;
- signature/approval configuration;
- offline eligibility;
- classification/retention;
- sample fill;
- rendered preview;
- pixel-diff comparison;
- reviewer comments;
- approval/publish;
- supersession.

Changes are governed; normal technicians cannot modify templates.

---

# 21. API/Domain Objects

Core objects:

- `DonorDocument`
- `DonorRevision`
- `FormSchema`
- `CoordinateMap`
- `FormInstance`
- `FormDraft`
- `FormSubmission`
- `FormSignature`
- `FormApproval`
- `GeneratedRecord`
- `EvidenceObject`
- `RetentionPolicyRef`
- `FidelityTestRun`

Key events:

- `donor.received`
- `donor.validated`
- `template.mapped`
- `template.approved`
- `template.published`
- `template.superseded`
- `form.draft_saved`
- `form.submitted`
- `form.signed`
- `form.approved`
- `record.rendered`
- `record.finalized`
- `record.amended`

---

# 22. Acceptance Gates

1. Original donor bytes remain retrievable and unchanged.
2. Generated form can be completed without hard-coded document-specific application logic.
3. Official output reproduces the approved donor layout within accepted visual tolerance.
4. Output values are sourced from the stored structured payload, not scraped from intermediate PDFs.
5. Every final record identifies donor/schema/map/renderer revisions.
6. Template changes cannot alter already finalized historical records.
7. Offline forms synchronize idempotently without duplicate official records.
8. Unauthorized users cannot view restricted donor records through form search, direct URL or AI retrieval.
9. Calculated fields are deterministic and versioned.
10. Pixel/fidelity regression tests block renderer changes that materially alter controlled documents.
