
---

# Sample-Efficiency Benchmark (Image Generation)

## 1. Motivation

The goal of this benchmark is to evaluate **sample efficiency in diffusion-based image generation**

This benchmark proposes using **algorithmic learning efficiency** by plotting **generation quality as a function of the number of training samples seen**, in addition with **Wall Clock Time**, as the main metric for measuring successful innovation.

This benchmark answers the question:

> *Given the same amount of data, which method learns useful visual representations earlier?*

---

## 2. Core Metric

### Primary Evaluation Curve

Each method must report:

$$
[
\textbf{FID} ; \text{vs.} ; \textbf{Number of Training Samples Seen}
]
$$
* **x-axis**: total number of image samples processed during training
  (equivalently epochs × dataset size)
* **y-axis**: Fréchet Inception Distance (FID) or Kernel Dino Distance (KDD)


The full curve must be reported, not only a single endpoint.

---

### Threshold-Based Summary Metric

For leaderboard summarization, an optional scalar metric may be derived:

> **Samples-to-FID-τ**

Defined as the **minimum number of samples required to reach**:

$$
[
\text{FID} \le \tau
]
$$

Default threshold:

* **τ = 2.0**

This scalar is derived *only* from the reported FID-vs-samples curve.

---

## 3. Dataset and Task

| Item                 | Specification                          |
| -------------------- | -------------------------------------- |
| Dataset              | ImageNet (train split)                 |
| Resolution           | 64×64 or 128×128 (reported separately) |
| Conditioning         | Class-conditional                      |
| Evaluation set       | ImageNet (train split)              |
| Sampling steps (NFE)     | 100 (fixed across runs)                 |
| Number of samples    | 50,000                                 |

---

## 4. Model Scaling Policy

### Model Size

* **Model size is not fixed**
* Participants may use any architecture (transformer-based diffusion backbone is the mostly used one)
* Model parameter count must be reported

This benchmark explicitly encourages **scaling analysis**.

Results should ideally include **multiple model sizes**, enabling analysis of:

* Sample-efficiency scaling
* Whether REPA benefits grow, shrink, or remain constant with scale

---

## 5. Training Protocol

### Training Axis Definition

* Progress is measured **only** by number of samples seen

Permitted:

* Any optimizer
* Any precision
* Any hardware
* Any batch size

Prohibited:

* Additional labeled data
* External pretrained generative models
* Evaluation-time finetuning

---

## 6. REPA-Specific Reporting Requirements

For methods using REPA or related representation alignment techniques, the following must be reported:

* Target encoder architecture (e.g., DINOv2-B/14)
* Aligned DiT layer(s)
* Alignment loss type (cosine, MSE, etc.)
* Loss weighting schedule
* Whether target features are frozen or EMA-updated

This ensures interpretability of representation-learning effects.

---

## 7. Required Plots and Artifacts

Each submission must include:

1. **FID vs. samples curve**
2. **Samples-to-FID-τ value**
3. Model parameter count
4. Training configuration
5. Random seed(s)
6. Wall Clock Time

Optional but encouraged:

* Multiple seeds with confidence bands
* Multiple model sizes on the same plot

---

