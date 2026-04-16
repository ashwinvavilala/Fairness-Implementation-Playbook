# Adaptability Guidelines

### Using the Playbook Across Domains and Problem Types

## Domain Adaptation

## Domain Adaptation Example: Healthcare

Explain how fairness objectives change (e.g., harm minimisation, false-negative parity).

List additional sensitive attributes (disability, health status, socioeconomic factors).

Mention regulatory overlays (EU AI Act Annex III, GDPR special category data, HIPAA, AIDA, MHRA/EMA).

Describe how architecture recipes adapt (LLMs for clinical notes, Vision for dermatology, RecSys for treatment recommendations, Multi-modal for imaging + text).

Add example metrics: equalised odds, false-negative parity, calibration across groups.

Highlight stronger human oversight and clinical safety roles.

### What Stays the Same

- Governance structures
- Scrum integration
- Architecture patterns
- Compliance mapping

### What Changes

- Domain‑specific harms
- Regulatory frameworks
- Stakeholders

## Problem Type Adaptation

### Classification

- Equal opportunity, TPR/FPR parity

### Regression

- Error distribution fairness

### Ranking

- Exposure fairness, position bias

### Recommendation

- Diversity constraints, exposure fairness

## Adaptation Checklist

- Redefine fairness objectives.
- Update regulatory mapping.
- Adjust metrics.
- Update architecture patterns.
- Train teams on domain‑specific harms.
