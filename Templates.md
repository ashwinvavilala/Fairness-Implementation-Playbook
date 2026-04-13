# Templates

Reusable templates to support consistent fairness implementation across teams.

## Fairness-Aware User Story

**Template**
As a \<stakeholder\>, I want \<behaviour/outcome\> so that \<fairness or transparency benefit\>.

**Example**
As a candidate, I want a clear explanation for why I was not shortlisted so that I can understand and trust the recruitment process.

---

## Fairness Acceptance Criteria

- Fairness metric X is computed for groups A/B.
- Difference between groups is below threshold T.
- Results are logged with timestamp, model version, and dataset.
- Any fairness regression triggers a review before deployment.

---

## Sprint Fairness Checklist

- Have fairness metrics been reviewed this sprint?
- Have any new features introduced fairness risks?
- Are fairness incidents or complaints pending?
- Has the compliance officer reviewed high‑risk changes?
- Are monitoring dashboards updated?

---

## Architecture Decision Record (ADR)

**Decision:**  
\<Describe the architecture decision\>

**Context:**  
\<Why this decision is needed\>

**Alternatives Considered:**  
\<List alternatives and trade‑offs\>

**Rationale:**  
\<Why this option was selected\>

**Consequences:**  
\<Positive and negative impacts\>

---

## Fairness Incident Report

**Date / Time:**  
**System / Model:**  
**Trigger:** (metric drift, complaint, audit finding)  
**Impact:**  
**Root Cause:**  
**Mitigation:**  
**Follow‑up Actions:**  
**Owner:**

---

## Compliance Evidence Checklist

- DPIA completed and approved
- Model card updated
- Data governance logs stored
- Human oversight checkpoints documented
- Fairness metrics archived
- Deployment decision logged
- Monitoring configuration validated

---

## New Project Fairness Kickoff Template

**Project Name:**  
**Owner:**  
**Risk Classification:**  
**Fairness Objectives:**  
**Stakeholders:**  
**Sensitive Attributes:**  
**Regulatory Requirements:**  
**Architecture Constraints:**  
**Monitoring Requirements:**  
**Evidence Requirements:**
