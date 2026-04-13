# Advanced Architecture Cookbook

### Architecture‑Specific Fairness Strategies for Complex AI Systems

## How to Use This Cookbook

This cookbook provides engineering teams with fairness strategies tailored to specific AI architectures. Each architecture behaves differently, exhibits unique bias patterns, and requires targeted interventions. Teams should:

- Identify the architecture powering their system (LLM, RecSys, Vision, Multi‑Modal).
- Select the relevant recipe suite.
- Apply the recommended primitives during data preparation, training, decoding, or inference.
- Validate fairness using the architecture‑specific metrics provided.
- Document assumptions, trade‑offs, and validation results in the model card.

This cookbook complements the Fair AI Scrum Toolkit, Governance Toolkit, and Regulatory Compliance Guide by providing technical depth for implementation.

---

# Large Language Model (LLM) Suite

## Common Fairness Issues

LLMs exhibit fairness challenges that differ from traditional classifiers:

- **Stylistic stereotyping:** Different tones or vocabulary for different demographic groups.
- **Representation imbalance:** Over‑representation of certain groups or professions in training data.
- **Toxicity leakage:** Harmful completions triggered by demographic cues.
- **Contextual bias:** Subtle shifts in meaning depending on demographic attributes.

## Frequent Mistakes

- Relying solely on prompt engineering without adjusting training data.
- Using generic toxicity filters that over‑suppress minority dialects.
- Ignoring stylistic bias because accuracy metrics appear stable.

## Why LLMs Are Special

LLMs generate text token‑by‑token, meaning bias can emerge through style, tone, or narrative framing—not just classification outcomes. They also encode demographic information deeply in embeddings, making bias harder to detect.

## Recipe Summary

### Stage: Corpus

- **Primitive:** Dynamic Thematic Balancing
- **Purpose:** Equalize topic‑demographic density
- **Typical Range:** 0.08–0.12 balancing factor

### Stage: Pre‑Training

- **Primitive:** Opposite‑Corpus Blending
- **Purpose:** Inject counter‑stereotypical examples
- **Typical Range:** 10–20% blended corpus

### Stage: Fine‑Tuning

- **Primitive:** RLHF‑F (Fairness‑Optimized RLHF)
- **Purpose:** Reward bias‑free completions
- **Typical Parameter:** Reward threshold ≥ 0.8

### Stage: Decoding

- **Primitive:** Self‑Rerank Diversity
- **Purpose:** Select the fairest of k candidate outputs
- **Typical Range:** Weight 0.3–0.6

### Stage: Post‑Processing

- **Primitive:** Bias Filter
- **Purpose:** Catch residual harms
- **Typical Range:** n/a

## Validation Targets

- BOLD‑NG ≤ 0.05
- Toxicity ≤ 0.5%
- Perplexity Δ ≤ 5%

---

# Recommendation Systems (RecSys) Suite

## Common Fairness Issues

- **Filter bubbles:** Users receive increasingly narrow recommendations.
- **Exposure disparity:** Some groups receive fewer high‑visibility items.
- **Feedback loop amplification:** Historical bias reinforces itself.
- **Opportunity inequality:** Certain groups are shown fewer high‑value opportunities.

## Frequent Mistakes

- Evaluating only click‑through rates (CTR), which hides exposure bias.
- Ignoring long‑term fairness in reinforcement‑learning‑based recommenders.
- Treating demographic attributes as optional metadata.

## Why Recommendation Systems Are Special

RecSys models operate in dynamic environments where user behavior influences future training data. Fairness must consider both **short‑term predictions** and **long‑term exposure dynamics**.

## Recipe Summary

### Stage: Candidate Generation

- **Primitive:** Demographic Exposure Balancing
- **Purpose:** Ensure equal opportunity to appear in candidate sets
- **Typical Range:** Exposure ratio 0.9–1.1

### Stage: Ranking

- **Primitive:** Fairness‑Constrained Ranking
- **Purpose:** Enforce exposure fairness across groups
- **Typical Range:** λ_fairness = 0.2–0.5

### Stage: Feedback Loop Control

- **Primitive:** Counterfactual Logging
- **Purpose:** Capture unbiased user preference signals
- **Typical Range:** 5–10% exploration traffic

### Stage: Post‑Processing

- **Primitive:** Re‑Ranking with Diversity Constraints
- **Purpose:** Prevent filter bubbles
- **Typical Range:** Diversity weight 0.1–0.3

## Validation Targets

- Exposure ratio gap ≤ 5%
- Long‑term fairness drift ≤ 2% per month
- Slice‑wise CTR parity within ±3%

---

# Vision Models Suite

## Common Fairness Issues

- **Skin‑tone accuracy gaps:** Darker skin tones misdetected more often.
- **Background leakage:** Model relies on context (e.g., kitchens, offices) instead of subjects.
- **Attribute leakage:** Embeddings reveal gender/ethnicity unintentionally.
- **Sensor bias:** Camera hardware favors certain tones.

## Frequent Mistakes

- Reporting only overall accuracy.
- Using synthetic augmentation that distorts textures.
- Applying a single threshold across all demographic groups.
- Ignoring lighting variability.

## Why Vision Models Are Special

Bias can originate **before** the model sees the image (sensor, lighting, compression). Vision models also hide demographic information deep in embeddings, making leakage difficult to detect.

## Recipe Summary

### Stage: Augmentation

- **Primitive:** Style‑Transfer Equalizer
- **Purpose:** Normalize lighting and textures
- **Typical Range:** 0.2–0.4 intensity

### Stage: Audit

- **Primitive:** Prototype Leak Probe
- **Purpose:** Quantify demographic leakage
- **Typical Range:** Leakage < 0.02

### Stage: Remediation

- **Primitive:** Layer Reinitialization
- **Purpose:** Remove leaking blocks
- **Typical Range:** n/a

## Validation Targets

- Leak AUC ≤ 0.52
- mIoU gap ≤ 2%
- False‑positive rate gap ≤ 3%

---

# Multi‑Modal Systems Suite

## Common Fairness Issues

- **Bias transfer:** Bias in one modality affects others.
- **Missing modality fallback:** Unequal performance when one stream is unavailable.
- **Inconsistent predictions:** Conflicting cues across modalities.
- **Dominant modality:** One modality overwhelms others.

## Frequent Mistakes

- Ignoring confidence‑based routing.
- Failing to recalibrate after modality dropout.
- Treating modalities as independent rather than interacting.

## Why Multi‑Modal Systems Are Special

Multi‑modal systems fuse text, audio, vision, and other signals into a shared latent space. Bias in one modality can propagate or amplify across the entire system.

## Recipe Summary

### Stage: Fusion

- **Primitive:** Cross‑Modal Consistency Loss
- **Purpose:** Align modalities
- **Typical Range:** 1.0–2.0

### Stage: Runtime

- **Primitive:** Failure‑Route Router
- **Purpose:** Skip unreliable modalities
- **Typical Range:** Confidence ≥ 0.65

## Validation Targets

- Cross‑modal agreement ≥ 0.92
- Bias migration ≤ 1%
- Modality dropout performance gap ≤ 3%

---

# Cross‑Architecture Reusable Primitives

## Group‑Aware Reweighting

Adjusts sample influence to equalize representation across demographic groups.

## Counterfactual Synthesis

Generates swapped‑attribute examples to test and mitigate bias.

## Slice‑Wise Evaluation Harness

Provides a structured template for evaluating fairness across demographic slices.

## Bias‑Sensitive Early Stopping

Stops training when fairness metrics stop improving, even if accuracy continues to rise.

---

# Inputs & Outputs

## Inputs

- Fairness objectives
- Architecture constraints
- Data characteristics
- Governance requirements

## Outputs

- Architecture‑specific fairness strategies
- Validation metrics
- Documentation for model cards
- Evidence for compliance audits

---

# Integration with Other Components

- **Feeds into:**
  - Compliance mapping (04)
  - Workflows (05)
  - Validation (07)

- **Receives inputs from:**
  - Governance objectives (02)
  - Fairness backlog items (01)
  - Risk classification (04)
