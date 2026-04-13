# Regulatory Compliance Guide

### Mapping Legal Requirements to Engineering Tasks

## Purpose

This guide translates regulatory obligations—primarily the EU AI Act and GDPR—into concrete engineering tasks, documentation requirements, and validation activities. It ensures that fairness implementation is not only technically sound but also compliant, auditable, and aligned with legal expectations for high‑risk AI systems such as recruitment platforms.

---

# 1. Regulatory Obligations

## EU AI Act (High‑Risk Systems)

High‑risk AI systems must comply with the following obligations:

- Data governance: high‑quality, representative, bias‑assessed datasets
- Documentation and transparency: technical documentation, model cards, logs
- Human oversight: override mechanisms, escalation paths
- Robustness and accuracy: performance monitoring, stress testing
- Post‑deployment monitoring: drift detection, incident reporting
- Traceability: complete audit trails for decisions and model changes

## GDPR Alignment

Recruitment systems must also comply with GDPR:

- Data minimization
- Right to explanation
- Automated decision‑making safeguards (Art. 22)
- DPIA (Art. 35)
- Lawful basis for processing

---

# 2. Risk Classification Framework

A structured risk scoring system determines which compliance controls apply.

## Scoring Formula

**Total Risk Score (TRS) = (P × S) + E – M**

- **P – Probability of Harm (1–5)**
- **S – Severity (1–5)** based on Annex III categories
- **E – Exposure (1–3)** based on number of EU citizens affected and duration
- **M – Mitigation Readiness (0–4)** based on existing controls

## Risk Tiers and Governance Gates

| TRS Range | Tier              | Governance Gate                            | Required Artifacts                                        |
| --------- | ----------------- | ------------------------------------------ | --------------------------------------------------------- |
| ≥ 22      | Critical (Tier 1) | External conformity assessment             | DPIA, independent bias audit, model card, monitoring plan |
| 15–21     | High (Tier 2)     | Internal conformity + external peer review | DPIA, model card, fairness tests                          |
| 8–14      | Moderate (Tier 3) | Product Director self‑assessment           | Model card, monitoring plan                               |
| ≤ 7       | Low (Tier 4)      | Lightweight checklist                      | Minimal documentation                                     |

## Trigger Conditions

A TRS calculation is required for:

- New features
- Material model changes
- Data pipeline changes
- Deployment to new jurisdictions

---

# 3. EU AI Act → SDLC Mapping Matrix

A detailed mapping ensures traceability from legal requirements to engineering tasks.

| SDLC Phase        | Article       | Requirement             | Control Activity                              | Validation              | RACI                         |
| ----------------- | ------------- | ----------------------- | --------------------------------------------- | ----------------------- | ---------------------------- |
| Data Ingestion    | Art. 10(2)(f) | Bias detection          | Automated bias scan in pipeline               | Bias report stored      | DS (R), Compliance (C)       |
| Model Training    | Art. 11(2)    | Technical documentation | MLflow run capture, auto‑generated model card | Model card completeness | DS (R), Eng (C)              |
| Pre‑Deployment    | Art. 14(4)(d) | Human oversight         | Override UI with reason logging               | Manual override test    | Product (A), Eng (R)         |
| Deployment        | Art. 15       | Robustness              | Stress tests, adversarial checks              | Test results archived   | Eng (R), QA (C)              |
| Post‑Deployment   | Art. 61       | Monitoring              | Fairness drift job, dashboards                | Drift alerts reviewed   | Platform (R), Compliance (C) |
| Incident Response | Art. 54       | Reporting               | Incident workflow                             | Incident log            | Compliance (A), DS (R)       |

---

# 4. Documentation Templates

## Model Card Template

### Header

- Model ID / Hash
- Commit SHA
- Dataset Version
- Legal Profile: Risk Tier, TRS, Annex III Category
- DPIA ID
- GDPR Lawful Basis
- Intended Use / Out‑of‑Scope Scenarios

### Performance & Fairness Benchmarks

- Overall metrics
- Slice metrics
- Thresholds and justification
- Link to risk‑benefit analysis

### Human Oversight Plan

- Roles
- Escalation ladder
- Override mechanisms

### Change‑Log (Auto‑Appended)

- Date
- Commit
- Author
- Change summary
- Reviewer

---

## DPIA Annex Shortcut

A one‑page add‑on covering:

- Personal data categories
- Purpose of processing
- Risk assessment
- Mitigation measures
- Link to AI Act Art. 10 + GDPR Art. 35

This prevents duplicate work between legal and engineering teams.

---

# 5. Audit‑Trail System Architecture

A robust audit trail ensures traceability and regulatory defensibility.

## Architecture Flow

User Action → Decision Engine → Event Broker (Kafka) →  
Immutable Log (Iceberg table, WORM policy, hash‑chain) →  
Monitoring API (InfluxDB) →  
Evidence Graph (Neo4j)

## Evidence Node Example

| Field            | Example             | Retention                 | Access          |
| ---------------- | ------------------- | ------------------------- | --------------- |
| risk_assessment  | TRS JSON            | 10 years                  | Compliance, DPO |
| model_metric     | TPR by gender       | 5 years                   | DS, Compliance  |
| override_event   | decision ID, reason | 5 years                   | Compliance      |
| dataset_snapshot | S3 URI + hash       | Life of product + 2 years | DS              |

## Tamper‑Proofing

- Daily Merkle‑root pinned to public blockchain (optional)
- Hash‑chain linking all events

## Evidence Graph API

Allows auditors to reconstruct:

- Full lineage of any decision
- Model version used
- Data snapshot
- Fairness metrics at time of decision

---

# 6. Stage‑Gate Compliance Checklist

| Gate            | Exit Criteria                                     | Evidence          |
| --------------- | ------------------------------------------------- | ----------------- |
| G0 – Ideation   | TRS draft completed                               | Risk Ticket       |
| G1 – Design     | Controls mapped, templates instantiated           | FDR‑017           |
| G2 – Build      | Unit tests ≥ 80%, fairness tests pass             | CI Build          |
| G3 – Validation | Independent QA sign‑off, DPIA approved            | Conformity Report |
| G4 – Launch     | Monitoring live, on‑call rotation set             | Change Request    |
| G5 – Operate    | Monthly fairness review, alerts < 2 critical/week | Ops Report        |
| G6 – Retire     | Data deletion plan executed                       | Tombstone Log     |

---

# 7. Quick‑Start Guide

1. Clone the template repository.
2. Run the TRS wizard to generate risk ticket and governance gate.
3. Follow the SDLC → Gate mapping (tasks auto‑populate).
4. Commit code; CI blocks until required artifacts are uploaded.
5. Deploy and monitor fairness drift dashboards.

Average overhead after first project: **~4 hours per feature**, typically offset by avoiding late‑stage legal rework.

---

# 8. Inputs & Outputs

## Inputs

- Architecture decisions
- Governance policies
- Fairness objectives

## Outputs

- DPIA
- Model cards
- Data governance logs
- Human oversight documentation
- Audit‑ready evidence

---

# 9. Integration with Other Components

- **Feeds into:**
  - Sprint tasks (01)
  - Governance reviews (02)
  - Architecture constraints (03)
  - Workflows (05)

- **Receives inputs from:**
  - Risk classification
  - Architecture decisions
  - Fairness objectives
