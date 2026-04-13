# Case Study: EquiHire Recruitment Platform

### Applying the Playbook Across Multi‑Team Systems with Timelines and Team Requirements

## Context

EquiHire operates a multi‑team AI recruitment platform with four core teams:

- Team A: CV Parsing & Sourcing
- Team B: Screening & Ranking Model
- Team C: Interview Scheduling & Candidate Communication
- Team D: Analytics, Reporting & Monitoring

The platform was classified as **high‑risk** under the EU AI Act due to automated candidate screening. Leadership requested a unified fairness implementation approach across all teams.

---

## Phase 1: Governance Setup (Weeks 1–2)

A Fairness Steering Committee was formed, including:

- Product Director (chair)
- Data Science Lead
- ML Engineering Lead
- Compliance Officer
- HR/DEI Partner

**Outputs:**

- Fairness objectives (equal opportunity, demographic parity bounds)
- Risk classification
- Human oversight checkpoints
- Approval workflow for model changes

---

## Phase 2: Backlog Integration (Weeks 2–4)

Each team integrated fairness into their sprint processes using the Fair AI Scrum Toolkit.

**Examples of fairness user stories:**

- “As a candidate, I want a clear explanation for why I was not shortlisted.”
- “As compliance, I need audit logs for all ranking decisions.”

**Outputs:**

- Fairness‑tagged backlog items
- Sprint‑level fairness acceptance criteria
- Cross‑team fairness review cadence

---

## Phase 3: Architecture Decisions (Weeks 4–8)

Using the Advanced Architecture Cookbook, the teams selected fairness‑aligned patterns.

**Key decisions:**

- Centralized fairness monitoring service
- Explainability microservice for candidate‑facing explanations
- Post‑processing layer for fairness‑constrained ranking
- Data lineage tracking for all training datasets

**Outputs:**

- Architecture diagrams
- Trade‑off logs
- Updated CI/CD fairness gates

---

## Phase 4: Compliance Mapping (Weeks 6–10)

The Regulatory Compliance Guide was used to map EU AI Act requirements to engineering tasks.

**Outputs:**

- DPIA
- Model cards
- Data governance logs
- Human oversight documentation
- Evidence repository for audits

---

## Phase 5: Implementation & Testing (Weeks 8–14)

Teams executed the fairness backlog items.

**Examples:**

- Bias assessment for CV parsing model
- Fairness regression tests for ranking model
- Explainability API integration
- Monitoring dashboards for fairness drift

---

## Phase 6: Deployment & Monitoring (Weeks 14–20)

A unified monitoring layer was deployed.

**Outputs:**

- Fairness drift alerts
- Incident response workflow
- Monthly fairness reports
- Quarterly governance review

---

## Outcome

- 23% reduction in demographic disparity in ranking outcomes
- Full traceability from fairness objectives → backlog → implementation → evidence
- Faster regulatory response due to structured documentation
- Clear accountability across teams
