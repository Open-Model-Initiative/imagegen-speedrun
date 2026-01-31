
---

# Image Generation SpeedRun Basic Ruleset Spec

## 1. Motivation

The goal of this spec is to evaluate **sample efficiency in diffusion-based image generation**

This benchmark measures models reaching a specified metric by the **shortest wall clock time**.

This benchmark answers the question:

> *Given the fixed dataset, what is the shortest wall clock time to train a text-to-image model?*

The main task will be t2i generation using clip embeddings.

Note:
- We may or may not resctrict the auto-encoder architecture, which is up to future discussion
- No strong opinions on clip embeddings, we propose to just fix for now, and open to more discussions in the future.

---

## 2. Core Metric

### Primary Evaluation Curve

Each method must report:

```
Sample-wise Metric
^
|                         *
|                   *
|             *
|       *
|  *
+------------------------------------> Wall Clock Time
```

* **x-axis**: Wall Clock Time
* **y-axis**: Sample-wise t2i metrics (GenEval1/2, HPSv3)

**Note**:
- The metric is open to discussion.

---

## 3. Dataset and Task

| Item                 | Specification                          |
| -------------------- | -------------------------------------- |
| Dataset              | ImageNet (train split)                 |
| Resolution           | 256*256 resolution                     |
| Sampling steps (NFE) | 100 (fixed across runs)                |

**Note**:
- Dataset choice is open to discussion.

---

## 4. Model Scaling Policy

### Model Size

* **Model size is not fixed**
* Participants may use any architecture (transformer-based diffusion backbone is the mostly used one)
* Model parameter count must be reported


---

## 5. Training Protocol

### Training Axis Definition

Permitted:

* Any optimizer
* Any precision
* Any batch size

Prohibited:

* Additional labeled data (the dataset/dataloader/ordering is fixed)
* Sampling function should only take random inputs
* External pretrained generative models
* Evaluation-time finetuning

---

## 7. Required Plots and Artifacts

Each submission must include:

1. Wall Clock Time
2. Model architecture changes
3. Model parameter count
4. Samples that used for evaluation

Optional but encouraged:

* Number of samples seen
* Training loss (wandb or any logging links)
* other metrics that the submitter willing to report

---

