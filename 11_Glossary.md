# Glossary

A reference guide to key terms used throughout the Fairness Implementation Playbook.

## Fairness Concepts

### Equal Opportunity

A fairness criterion requiring similar true positive rates across demographic groups.

### Demographic Parity

A fairness criterion requiring similar positive prediction rates across groups, regardless of underlying qualification differences.

### Fairness Drift

A change in fairness metrics over time, even when accuracy remains stable. Often caused by data distribution shifts or model degradation.

### Exposure Fairness

A ranking fairness concept ensuring that different demographic groups receive comparable visibility or ranking positions.

### Position Bias

A ranking phenomenon where higher-ranked items receive disproportionately more attention, amplifying unfairness if not controlled.

### Error Distribution Fairness

A regression fairness concept requiring similar error magnitudes and variance across groups.

## Regulatory and Governance Terms

### DPIA (Data Protection Impact Assessment)

A structured assessment required under GDPR to evaluate privacy and data protection risks associated with automated decision-making.

### High-Risk AI System

A classification under the EU AI Act for systems that significantly impact individuals’ rights, safety, or opportunities (e.g., recruitment).

### Human Oversight

A governance mechanism ensuring humans can review, override, or intervene in automated decisions.

### Evidence Repository

A structured collection of documentation, logs, and artifacts used to demonstrate compliance with regulatory requirements.

## Technical Terms

### Sensitive Attributes

Attributes such as gender, ethnicity, age, or disability status that require special handling due to legal or ethical considerations.

### Pre‑Processing

Fairness interventions applied before model training (e.g., reweighing, sampling).

### In‑Processing

Fairness interventions applied during model training (e.g., fairness‑constrained optimization).

### Post‑Processing

Fairness interventions applied after model prediction (e.g., threshold adjustments, score calibration).

### Explainability

The ability to provide understandable reasons for model predictions or decisions, often required for transparency and compliance.

### Data Lineage

A record of where data originated, how it was transformed, and how it was used across the pipeline.
