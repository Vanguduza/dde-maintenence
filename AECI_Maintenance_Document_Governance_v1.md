# AECI Maintenance — Document Governance & Source-of-Truth Map v1.0

**Date:** 1 September 2026
**Purpose:** Prevent contradictory implementation decisions across the growing DDE/AECI document set.

---

# 1. Governing Product Source

For AECI Maintenance product behavior and implementation scope, the governing document is:

`AECI_Maintenance_Operations_System_Master_Plan_v1.md`

It supersedes the earlier interpretation that the AECI work is only a thin configuration layer. The existing customer pack remains authoritative for customer-specific configuration, research-derived site/asset assumptions and statutory-register templates that are not superseded by the new master.

---

# 2. Authority Order

1. `AECI_Maintenance_Operations_System_Master_Plan_v1.md`
2. `AECI_Maintenance_Implementation_Realisation_Pack_v1.md`
3. `AECI_Maintenance_RBAC_Competency_Matrix_v1.md`
4. `AECI_Maintenance_Acceptance_Test_Catalog_v1.md`
5. `aeci-maintenance.pack.yaml` — machine-readable reflection of the above; prose authority wins if drift is discovered.
6. `DDE_AECI_Operations_Pack_Config_Spec.md`
7. `DDE_AECI_Zimbabwe_Customer_Research.md`
8. `DDE_Maintenance_Intelligence_ERP_Master_Plan_v2.md`
9. `DDE_Field_Experience_Rugged_Hardware_Spec.md`
10. `DDE_Security_Trust_Architecture.md`
11. `DDE_Modular_Platform_White_Label_Spec.md`
12. other market, simulation and vertical research documents.

A stricter specialist security, legal or safety rule remains controlling for that specialist matter unless the master explicitly and validly supersedes it.

---

# 3. Document Roles

| Document | Role | May define product behavior? | May contain unverified assumptions? |
|---|---|---:|---:|
| AMOS Master Plan | Product/operating model SOT | Yes | Only if explicitly marked discovery/config input |
| Implementation Realisation Pack | Engineering contracts/build rules | Yes, subordinate to master | No silent assumptions |
| RBAC/Competency Matrix | Authorization/eligibility rules | Yes, subordinate to master | Job-title mappings may remain configurable |
| Acceptance Catalog | Completion criteria | Yes, test interpretation | Fixtures may be synthetic |
| Pack YAML | Machine-readable manifest | Reflective only | No |
| AECI Operations Pack | Customer-specific configuration/statutory/site template | Yes where not superseded | Yes, only where explicitly pending/unverified |
| Customer Research | Evidence/reference | No direct implementation authority by itself | Yes, with evidence grades/limitations |
| DDE Master Plan | Shared platform architecture | Yes for shared platform | Generic cross-industry assumptions must be specialized through pack |
| Security Trust Architecture | Security controls | Yes for security | No weakening by customer config |
| Rugged Hardware Spec | Device/field UX/hardware | Yes for device domain | Hardware selection may be site-dependent |

---

# 4. Change Procedure

Any material AMOS change must update all affected artifacts:

1. master product behavior;
2. realization contract;
3. RBAC/competency policy if permissions/eligibility changed;
4. acceptance tests;
5. pack YAML if module/state/dependency changed;
6. AECI customer pack if customer-specific configuration changed.

A change is material if it alters:
- a state machine;
- safety/authorization requirement;
- data ownership/invariant;
- release gate;
- role authority;
- readiness semantics;
- offline conflict behavior;
- external system-of-record boundary;
- AI authority/grounding rule;
- customer contract/SLA behavior.

---

# 5. ADR Requirement

Create an Architecture Decision Record when a change:

- changes a bounded-context boundary;
- adds a new system of record;
- changes canonical IDs or event semantics;
- changes offline conflict strategy;
- weakens or replaces an existing invariant;
- introduces a new direct external dependency;
- changes deployment shape;
- changes data residency/security model;
- introduces autonomous AI action beyond current authority limits.

ADR must state:
- context;
- decision;
- alternatives;
- consequences;
- migration impact;
- acceptance-test impact;
- rollback strategy where applicable.

---

# 6. Discovery vs Production Configuration

Customer research may seed templates but cannot silently become operational truth.

Statuses for customer-specific values:

- `TEMPLATE_UNVERIFIED`
- `DISCOVERY_CONFIRMED`
- `CUSTOMER_APPROVED`
- `PRODUCTION_ACTIVE`
- `SUPERSEDED`

Examples requiring customer evidence before `PRODUCTION_ACTIVE`:
- exact asset models/BOMs;
- actual site roster;
- PM intervals;
- permit forms;
- statutory licence numbers/conditions;
- competency requirements;
- contract KPI definitions;
- hazardous-area device restrictions;
- external system endpoints.

---

# 7. Coding-Agent Read Order

Any coding agent working on AECI Maintenance must read in this order:

1. `AECI_Maintenance_Operations_System_Master_Plan_v1.md`
2. `AECI_Maintenance_Implementation_Realisation_Pack_v1.md`
3. the relevant specialist document (RBAC, acceptance, security, rugged field, operations pack)
4. the exact implementation issue/epic
5. existing code/ADRs/tests for the bounded context.

The agent must not use the older AECI Operations Pack alone as the complete feature scope.

---

# 8. Merge Gate for Documentation Changes

A documentation PR changing AMOS behavior must be checked for:

- contradictory state names;
- conflicting source-of-truth claims;
- broken bounded-context ownership;
- missing acceptance updates;
- missing pack manifest update;
- safety/AI authority drift;
- customer assumptions accidentally promoted to facts;
- external contract/API dependencies incorrectly made release blockers.

---

# 9. Current Baseline Declaration

The AMOS v1 baseline consists of:

- comprehensive product master;
- engineering realization pack;
- explicit RBAC/competency authority model;
- acceptance test catalog;
- machine-readable pack manifest;
- this governance map;
- existing AECI customer configuration/research and shared DDE specialist documents.

This baseline is sufficient to begin detailed schema/API/UI implementation without reopening product architecture from scratch. Customer discovery remains necessary to activate real AECI data, procedures, statutory particulars and integrations.
