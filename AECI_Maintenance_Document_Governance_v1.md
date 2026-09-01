# AECI Maintenance — Document Governance & Source-of-Truth Map v1.2

**Date:** 1 September 2026
**Purpose:** Prevent contradictory implementation decisions across the growing DDE/AECI document set and establish authority for security, donor documents and AECI field-operation specializations.

---

# 1. Governing Product Source

For AECI Maintenance product behavior and implementation scope, the governing product document is:

`AECI_Maintenance_Operations_System_Master_Plan_v1.md`

AECI AMOS is a complete specialization of DDE Maintenance, not a thin subset. Applicable generic DDE Maintenance capabilities are inherited unless explicitly excluded through governed exclusion.

---

# 2. Authority Order

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
8. **Generic DDE shared architecture/capability catalog**
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

# 3. External Benchmark Evidence vs Product Authority

SAP SuccessFactors is used as an external **security benchmark**, not as AECI AMOS product authority and not as proof that AECI has enabled every available SuccessFactors option.

The benchmark was re-verified against current SAP platform documentation on 1 September 2026 for capabilities including:

- Role-Based Permissions;
- Data Retention Time Management / retention policy controls;
- read/change/general audit retention;
- encryption at rest and advanced/customer-managed key options;
- SAML SSO / SAP Cloud Identity Services;
- MFA/conditional authentication capability;
- mTLS/X.509 and Security Center integration trust controls.

Implementation decisions still require AECI's actual identity/security/document-retention policies before production activation.

---

# 4. Generic Capability Inheritance Rule

Every operationally applicable DDE Maintenance capability is inherited by AECI AMOS unless explicitly listed in a governed Exclusion Register. Silence is not exclusion.

An exclusion requires source capability, rationale, safety/compliance impact, owner, approval and review date.

---

# 5. Document Roles

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

# 6. AECI Donor Documents as Controlled Sources

AECI-approved maintenance/safety/fleet/blast PDFs have two roles:

1. **visual/record authority:** approved layout, document code, revision and signoff structure govern the official generated record;
2. **operational content authority where explicitly approved:** field definitions, controlled limits/formulas/procedure references are mapped from the current approved donor/procedure and never guessed by AMOS.

The donor PDF does not override safety/legal policy merely because text appears on an old form. Superseded donor revisions are retained for historical reconstruction but are not primary sources for new work.

---

# 7. Template Change Control

For every donor PDF:

`receive → immutable hash/retain → validate/sandbox → map schema/coordinates → reviewer verification → golden/fidelity testing → document-controller approval → publish`

A change to donor bytes, field schema, coordinate map, controlled formula, approval structure, classification/retention rule, or material render behavior creates a new governed template revision.

Published revisions are immutable. Historical finalized records remain bound to their original revision.

---

# 8. Security Policy Change Control

High-impact changes require explicit audit and may require dual approval, including cross-site access, restricted offline/RAG enablement, retention reduction, legal-hold release, high-risk export policy, encryption/key posture, privileged administration and audit-integrity configuration.

A feature PR cannot weaken an authoritative security requirement without a separately approved security decision record.

---

# 9. Formula and Technical Value Governance

AMOS must never invent controlled maintenance, quality or blasting values.

Technical formulas/limits/tolerances require source document/procedure reference, revision, approving owner, unit definition, calculation/rounding definition and effective date.

Missing approved source data produces `not configured / cannot calculate` rather than an inferred default.

---

# 10. Discovery vs Production Configuration

Customer research may seed templates but cannot silently become operational truth.

Statuses: `TEMPLATE_UNVERIFIED`, `DISCOVERY_CONFIRMED`, `CUSTOMER_APPROVED`, `PRODUCTION_ACTIVE`, `SUPERSEDED`.

Customer evidence is required before production activation for exact assets/BOMs, rosters/postings, PM intervals, donor PDFs, manuals/SOPs, trip-test/calibration values, blast formulas/limits, permit/LOTO forms, statutory particulars, competence, KPI definitions, retention/classification rules, hazardous-area device policy and external endpoints.

---

# 11. Change Procedure

Material AMOS changes update affected product/master behavior, specialist security/domain spec, realization contract, RBAC/competency policy, acceptance tests, machine-readable pack(s) and customer configuration.

Material includes changes to states, safety/authorization, data ownership, release gates, role authority, readiness, donor records, formulas, offline behavior, system-of-record boundaries, AI authority or SLA behavior.

---

# 12. ADR Requirement

Create an ADR when changing bounded-context boundaries, systems of record, canonical IDs/events, offline conflict strategy, invariants, deployment/data residency/security, donor-render architecture, direct external dependencies or AI autonomy.

---

# 13. Coding-Agent Read Order

1. `AECI_Maintenance_Operations_System_Master_Plan_v1.md`
2. `AECI_Enterprise_Security_Data_Protection_Records_Standard_v1.md`
3. `AECI_Maintenance_DDE_Full_Capability_Inheritance_Spec_v1.md`
4. relevant AECI domain specialization
5. `AECI_Maintenance_Implementation_Realisation_Pack_v1.md`
6. relevant RBAC/acceptance documents
7. implementation issue/epic
8. existing code/ADRs/tests.

The older AECI Operations Pack alone is never the complete feature scope.

---

# 14. Acceptance Precedence

If a feature passes a happy-path demo but violates any applicable P0 scenario, it is not complete. Security and safety P0 failures are release blockers.

---

# 15. Required PR Metadata

Every implementation PR identifies bounded context(s), authoritative specs, inherited capabilities, acceptance IDs, data classifications, offline impact, security/export/RAG impact, donor-template impact, ADR/change decision and external assumptions/fixtures.

---

# 16. Source-of-Truth Principle

AMOS may not drift into parallel undocumented logic. Product rules, donor mappings, authorization, formulas, workflows and acceptance gates belong in governed artifacts and machine-readable configuration where practical.
