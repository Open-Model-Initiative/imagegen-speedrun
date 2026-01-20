# Image Model Speedrun — Basic Track (Draft)

## Motivation


The Basic Track instead asks:

> How effectively does a method learn as it consumes training samples?

By measuring progress as a function of **samples seen**, the benchmark avoids the need for strict hardware standardization and enables fair comparisons across diverse implementations.

---

## Task Definition

Participants may choose any **image modeling task**, including but not limited to:
- Image classification
- Image generation
- Reconstruction or autoencoding
- Self-supervised learning with downstream evaluation

**Unlike extended tracks, the Basic Track does not require high-resolution or large-scale generative tasks.**

The task must be clearly defined and consistently evaluated.

---

## Dataset Requirements

Datasets must satisfy the following:
- Publicly available
- Fixed and well-defined train/validation/test splits
- Small enough to train and evaluate on a **limited hardware setting**

**The Basic Track explicitly favors smaller datasets to minimize iteration cost and evaluation overhead.**

Participants must report:
- Dataset name and version
- Image resolution
- Number of training samples

---

## Model and Architecture Scope

The benchmark is **architecture-agnostic**.

Allowed model families include:
- Vision/Diffusion Transformers
- Small generative or latent image models


**There is no minimum or target model size in the Basic Track.**

---

## Compute and Training Constraints

- Single node is preferred
- Mixed precision, compilation, kernel fusion, and checkpointing are allowed
- No requirement to normalize FLOPs or wall-clock time

---

## Primary Measurement Axis: Samples Seen

The x-axis for all comparisons is:

> **Total number of training samples processed**

This includes:
- All epochs
- All dataset repetitions
- All samples contributing to gradient updates

This metric is:
- Simple
- Hardware-agnostic
- Difficult to game without explicit rule violations

---

## Performance Metrics

The y-axis depends on the task, for example:
- Top-1 accuracy or error rate (classification)
- FID, KDD, or related metrics (generation)
- Reconstruction loss or downstream task score

Participants must clearly specify:
- The metric used
- How it is computed
- Evaluation dataset and protocol

---

## Evaluation Protocol

Evaluation should be performed at a **finite set of predefined checkpoints**, such as:
- Fixed multiples of dataset size
- Fixed sample count milestones

Dense or per-step evaluation is not required.

**In the Basic Track, evaluation frequency should be kept low enough that evaluation cost does not dominate training cost.**

For expensive metrics:
- Approximate or low-sample evaluations are acceptable during training
- Full evaluations are only required at final or threshold checkpoints

---

## Summary Metrics and Ranking

Submissions should report one or more of the following:

- **Samples-to-threshold**  
  Number of samples required to reach a predefined performance level
- **Performance at fixed sample budgets**
- Optional **Area Under the Curve (AUC)** up to a fixed sample limit

Leaderboards, if used, should clearly state:
- Dataset
- Metric
- Evaluation checkpoints

---

## Submission Requirements

Each submission must include:

1. Task and dataset description
2. Model architecture and parameter count
3. Training configuration (optimizer, batch size, schedules, augmentations)
4. Evaluation metrics and checkpoints
5. Performance vs. samples seen results
6. Random seed(s)

Optional but encouraged:
- Training curves
- Peak hardware memory usage
- Notes on instability or failure modes

---

## Rules and Anti-Gaming Constraints

To ensure fair comparison:
- No external or proprietary data
- No privileged supervision or oracle signals
- All reported samples must contribute to learning

**The Basic Track prioritizes transparency and reproducibility over aggressive optimization tricks.**

---

## Interpretation of Results

Results should be interpreted as:
- Indicators of early learning dynamics
- Signals of optimization or architectural efficiency
- Diagnostic evidence, not final SOTA claims

**Performance in the Basic Track is not expected to predict large-scale behavior directly**, but to guide further experimentation.

---
