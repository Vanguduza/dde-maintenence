# AECI Maintenance — Document Governance & Source-of-Truth Map v1.1

**Date:** 1 September 2026
**Purpose:** Prevent contradictory implementation decisions across the growing DDE/AECI document set and establish authority for security, donor documents and AECI field-operation specializations.

---

# 1. Governing Product Source

For AECI Maintenance product behavior and implementation scope, the governing product document is:

`AECI_Maintenance_Operations_System_Master_Plan_v1.md`

AECI AMOS is a complete specialization of DDE Maintenance, not a thin subset. Applicable generic DDE Maintenance capabilities are inherited unless explicitly excluded through governed exclusion.

---

# 2. Authority Order

For AECI AMOS implementation, use this precedence:

1. **Safety, security, data-protection and legal controls**
   - `AECI_Enterprise_Security_Data_Protection_Records_Standard_v1.md`
   - `DDE_Security_Trust_Architecture.md`
   - applicable law, AECI approved policy and host-site policy once supplied
2. **AECI product source of truth**
   - `AECI_Maintenance_Operations_System_Master_Plan_v1.md`
3. **Full DDE capability inheritance**
   - `AECI_Maintenance_DDE_Full_Capability_Inheritance_Spec_v1.md`
   - `aeci-maintenance-capability-inheritance.yaml`
4. **AECI domain specializations**
   - `AECI_Donor_PDF_Forms_Records_Fidelity_Engine_v1.md`
   - `AECI_Field_Operations_Assets_Work_Notifications_Blast_Module_v1.md`
   - `DDE_AECI_Operations_Pack_Config_Spec.md`
5. **Engineering realization**
   - `AECI_Maintenance_Implementation_Realisation_Pack_v1.md`
   - `AECI_Maintenance_Engineering_Backlog_v1.md`
   - `aeci-maintenance.pack.yaml`
6. **Access and authority model**
   - `AECI_Maintenance_RBAC_Competency_Matrix_v1.md`
7. **Acceptance contracts**
   - `AECI_Maintenance_Acceptance_Test_Catalog_v1.md`
   - `AECI_Maintenance_Operational_Workflow_Acceptance_Addendum_v1.md`
   - `AECI_Security_Forms_Field_Blast_Acceptance_Addendum_v1.md`
8. **Generic DDE master architecture/capability catalog**
   - `DDE_Maintenance_Intelligence_ERP_Master_Plan_v2.md`
   - `DDE_Field_Experience_Rugged_Hardware_Spec.md`
   - `DDE_Modular_Platform_White_Label_Spec.md`
   - other generic DDE documents
9. **Research/evidence packs**
   - `DDE_AECI_Zimbabwe_Customer_Research.md`
   - `DDE_Zimbabwe_Market_Entry_Research.md`
   - other research inputs

Research is evidence, not permission to override approved AECI policy or product decisions.

---

# 3. Generic Capability Inheritance Rule

Every operationally applicable DDE Maintenance capability is inherited by AECI AMOS unless explicitly listed in a governed Exclusion Register. Silence is not exclusion.

An exclusion requires source capability, rationale, safety/compliance impact, owner, approval and review date.

---

# 4. Document Roles

| Document | Role | May define behavior? | Notes |
|---|---|---:|---|
| AMOS Master Plan | Product/operating model SOT | Yes | Customer values can remain pending where marked |
| Enterprise Security Standard | Security/data protection/records control | Yes | Cannot be weakened by customer pack convenience |
| Full Capability Inheritance | DDE capability applicability | Yes | Silence does not exclude a generic capability |
| Donor PDF Fidelity Engine | Controlled AECI form digitisation/output | Yes | Donor layout remains record authority |
| Field Operations/Blast Spec | Site asset/work/notification/blast specialization | Yes | Controlled values come from AECI sources |
| Realisation Pack | Engineering contracts/build rules | Yes, subordinate to above | No silent assumptions |
| RBAC/Competency Matrix | Authorization/eligibility | Yes | RBAC does not equal competence |
| Acceptance Catalogs | Completion criteria | Yes | P0 failures block release |
| Pack YAMLs | Machine-readable reflection | Reflective | Prose authority wins if drift is discovered |
| AECI Operations Pack | Customer-specific configuration/statutory/site template | Yes where not superseded | Pending context remains unverified |
| Customer Research | Evidence/reference | No direct authority | Evidence grades/limitations apply |
| DDE Master Plan | Shared platform architecture | Yes for shared platform | AECI specialization can tighten it |
| Security Trust Architecture | Shared security controls | Yes | Stricter AECI rule wins |
| Rugged Hardware Spec | Device/field UX/hardware | Yes | Device selection may be site dependent |

---

# 5. AECI Donor Documents as Controlled Sources

AECI-approved maintenance/safety/fleet/blast PDFs have two roles:

1. **visual/record authority:** approved layout, document code, revision and signoff structure govern the official generated record;
2. **operational content authority where explicitly approved:** field definitions, controlled limits/formulas/procedure references are mapped from the current approved donor/procedure and never guessed by AMOS.

The donor PDF does not override safety/legal policy merely because text appears on an old form. Superseded donor revisions are retained for historical reconstruction but are not primary sources for new work.

---

# 6. Template Change Control

For every donor PDF:

`receive → immutable hash/retain → validate/sandbox → map schema/coordinates → reviewer verification → golden/fidelity testing → document-controller approval → publish`

A change to any of these creates a new governed template revision:

- donor PDF bytes;
- field schema;
- coordinate map;
- controlled calculation/formula;
- approval/signature structure;
- material classification/retention rules;
- output rendering rule that changes official appearance.

Published revisions are immutable. Historical finalized records remain bound to their original revision.

---

# 7. Security Policy Change Control

High-impact security changes require explicit audit and may require dual approval, including:

- broadening cross-site/enterprise access;
- enabling restricted data for offline storage or AI indexing;
- reducing retention periods;
- releasing legal/evidence hold;
- changing high-risk export policy;
- changing encryption/key-management posture;
- granting privileged security administration;
- changing audit retention/integrity configuration.

A feature PR cannot weaken an authoritative security requirement without a separately approved security decision record.

---

# 8. Formula and Technical Value Governance

AMOS must never invent controlled maintenance, quality or blasting values.

Technical formulas/limits/tolerances used in execution or reporting require:

- source document/procedure reference;
- revision;
- approving owner;
- unit definition;
- calculation/rounding definition;
- effective date.

Missing approved source data produces `not configured / cannot calculate` rather than an inferred default.

---

# 9. Discovery vs Production Configuration

Customer research may seed templates but cannot silently become operational truth.

Statuses:

- `TEMPLATE_UNVERIFIED`
- `DISCOVERY_CONFIRMED`
- `CUSTOMER_APPROVED`
- `PRODUCTION_ACTIVE`
- `SUPERSEDED`

Examples requiring customer evidence before `PRODUCTION_ACTIVE`:

- exact asset models/BOMs;
- current site rosters/postings;
- PM intervals;
- donor PDFs and revisions;
- repair manuals/procedures;
- trip-test/calibration limits;
- blast/quality formulas and limits;
- permit/LOTO forms;
- statutory licence particulars;
- competency requirements;
- contract KPI definitions;
- retention/classification rules;
- hazardous-area device restrictions;
- external system endpoints.

---

# 10. Change Procedure

Any material AMOS change must update affected artifacts:

1. product/master behavior;
2. specialist security/domain spec;
3. realization contract;
4. RBAC/competency policy if permissions/eligibility changed;
5. acceptance tests;
6. machine-readable pack(s);
7. AECI customer pack if customer-specific configuration changed.

A change is material if it alters a state machine, safety/authorization requirement, data ownership/invariant, release gate, role authority, readiness semantics, donor record, calculation, offline behavior, external system-of-record boundary, AI authority or customer SLA behavior.

---

# 11. ADR Requirement

Create an Architecture Decision Record when a change:

- changes a bounded-context boundary;
- adds a new system of record;
- changes canonical IDs/event semantics;
- changes offline conflict strategy;
- weakens/replaces an invariant;
- introduces a new direct external dependency;
- changes deployment/data-residency/security shape;
- changes donor-record rendering architecture;
- introduces autonomous AI action beyond current limits.

ADR states context, decision, alternatives, consequences, migration impact, acceptance impact and rollback strategy where applicable.

---

# 12. Coding-Agent Read Order

Any coding agent working on AECI Maintenance must read:

1. `AECI_Maintenance_Operations_System_Master_Plan_v1.md`
2. `AECI_Enterprise_Security_Data_Protection_Records_Standard_v1.md`
3. `AECI_Maintenance_DDE_Full_Capability_Inheritance_Spec_v1.md`
4. relevant AECI domain specialization (donor PDF / field operations / operations pack)
5. `AECI_Maintenance_Implementation_Realisation_Pack_v1.md`
6. relevant RBAC/acceptance documents
7. exact implementation issue/epic
8. existing code/ADRs/tests for the bounded context.

The older AECI Operations Pack alone is never the complete feature scope.

---

# 13. Acceptance Precedence

If a feature passes a happy-path demo but violates any applicable P0 scenario in the AECI acceptance catalogs, it is not complete.

Security and safety P0 failures are release blockers regardless of product-demo status.

---

# 14. Required PR Metadata

Every implementation PR identifies:

- bounded context(s);
- authoritative specification(s);
- inherited DDE capability domains;
- relevant acceptance IDs;
- data classifications touched;
- offline behavior impact;
- security/export/RAG impact;
- donor-template impact if any;
- ADR/change decision;
- external assumptions/fixtures used.

---

# 15. Source-of-Truth Principle

AMOS may not drift into parallel undocumented logic. Product rules, donor mappings, authorization, formulas, workflows and acceptance gates belong in governed artifacts and machine-readable configuration where practical.
