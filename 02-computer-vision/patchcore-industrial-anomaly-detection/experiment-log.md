# Experiment Log — Bottle Anomaly Detection

This log records the completed baseline and random-memory experiments. Results are based on the notebook outputs and exported CSV files.

## Shared configuration

| Setting | Value |
|---|---|
| Dataset | MVTec AD, bottle category |
| Training images | 168 normal |
| Validation images | 41 normal |
| Test images | 20 normal, 63 defective |
| Split seed | 42 |
| Backbone | Wide ResNet-50-2 |
| Weights | ImageNet V1, frozen |
| Input size | 224 × 224 |
| Feature layers | layer2 and layer3 |
| Feature neighborhood | 3 × 3 |
| Embeddings per image | 784 |
| Embedding dimension | 1,024 |
| Full memory bank | 131,712 vectors; 514.5 MiB |
| Patch score | Nearest-neighbor squared Euclidean distance |
| Image score | Maximum patch score |
| Threshold | Normal-validation 95th percentile, `method="higher"` |
| Decision rule | Flag when `score > threshold` |

## EXP-001 — Initial 1% random-memory baseline

**Status:** completed  
**Sampling seed:** 42

### Question

Can a small random subset of normal training features distinguish normal bottles from defective bottles?

### Configuration

Retain 1% of the full bank:

- 1,317 vectors.
- Approximately 5.14 MiB of feature storage.
- Threshold calibrated using the 41 normal validation images.

### Results

| Measure | Result |
|---|---:|
| Threshold | 3.322491 |
| Normal test images correctly accepted | 20 |
| Normal test images incorrectly flagged | 0 |
| Defects detected | 63 |
| Defects missed | 0 |
| Image-level AUROC | 1.0 |

### Interpretation

This configuration separated all 83 test images correctly. It established a working baseline for this category, but did not establish reliability across other memory samples or datasets.

### Decision

Keep this configuration as the baseline and test smaller memory banks across multiple seeds.

## EXP-002 — Memory size and random-seed comparison

**Status:** completed

### Question

How does reducing normal-feature memory affect detection quality, and how sensitive are the results to random selection?

### Hypothesis

Smaller banks may omit useful normal appearances, increasing score changes and detection errors.

### Controlled settings

The data split, pretrained weights, preprocessing, embedding function, score definition, and threshold-calibration rule remained fixed.

Validation and test embeddings were cached once:

- Validation cache: `(41, 784, 1024)`.
- Test cache: `(83, 784, 1024)`.

These evaluation features were not added to the training memory bank.

### Variables

- Sampling ratios: 0.1%, 0.5%, 1%.
- Seeds: 42, 43, 44.
- A separate threshold was calibrated for every configuration.

Within each seed, the memory subsets were nested.

### Results

Thresholds and metrics below are rounded. Full values are available in the exported CSV.

| Seed | Retained | Vectors | Threshold | Validation false alarms / 41 | Test false alarms / 20 | Missed defects / 63 | Defect recall | AUROC |
|---|---|---:|---:|---:|---:|---:|---:|---:|
| 42 | 0.1% | 131 | 6.9298 | 2 | 1 | 10 | 0.8413 | 0.9405 |
| 42 | 0.5% | 658 | 3.6262 | 2 | 1 | 0 | 1.0000 | 0.9984 |
| 42 | 1% | 1,317 | 3.3225 | 2 | 0 | 0 | 1.0000 | 1.0000 |
| 43 | 0.1% | 131 | 6.8298 | 2 | 0 | 8 | 0.8730 | 0.9381 |
| 43 | 0.5% | 658 | 4.3371 | 2 | 1 | 1 | 0.9841 | 0.9984 |
| 43 | 1% | 1,317 | 3.2518 | 2 | 1 | 0 | 1.0000 | 0.9976 |
| 44 | 0.1% | 131 | 5.9051 | 2 | 1 | 4 | 0.9365 | 0.9817 |
| 44 | 0.5% | 658 | 3.5444 | 2 | 2 | 0 | 1.0000 | 1.0000 |
| 44 | 1% | 1,317 | 3.2963 | 2 | 0 | 0 | 1.0000 | 1.0000 |

### Observations

- The initial 1% / seed 42 result reproduced.
- Every 0.1% run missed defects.
- The 0.5% bank missed zero or one defect.
- Every 1% run detected all defects, although one produced a false alarm.
- Smaller memory banks required higher validation-derived thresholds.
- Results varied with the sampled vectors.

### Interpretation

The results support a memory–detection tradeoff on this category.

A possible explanation is that smaller banks omit legitimate normal patterns, increasing normal-image distances and the calibrated threshold. Some defective images then fall below that threshold. Individual error inspection would be needed to identify the patterns responsible.

The two validation false alarms per run largely follow from the percentile calibration rule and should not be treated as independent estimates of future false-alarm rates.

### Evaluation boundary

The same test set was used across runs and had already been examined during the baseline evaluation. These are follow-up benchmark comparisons.

Settings were not adjusted individually to eliminate test errors. All nine configurations are reported.

### Decision

Compare representative coreset selection against random sampling at the same vector counts. Retain all random-sampling results as the comparison baseline.

## EXP-003 — Visual interpretation

**Status:** completed  
**Purpose:** explain existing results; no new model configuration.

### Visuals

1. [Memory versus detection errors](figures/random_memory_tradeoff.png).
2. [Ranking versus threshold decisions](figures/ranking_vs_threshold_seed44_0p5pct.png).

### Finding

The 0.5% / seed 44 configuration achieved perfect ranking, with AUROC 1.0, while flagging two normal images.

This illustrates the distinction between:

- Ranking quality across thresholds.
- Classification decisions at the selected threshold.

The threshold was retained rather than adjusted using test labels.

## EXP-004 — Approximate coreset versus random sampling

**Status:** completed.

### Question

At equal feature-memory budgets, does representative selection
preserve detection quality better than random sampling?

### Method

- Gaussian random projection: 1,024 → 128 dimensions.
- Greedy farthest-first selection with a random starting vector.
- Budgets: 131, 658, and 1,317 vectors, using nested selections.
- Seeds: 42, 43, and 44.
- Scoring uses the original 1,024-dimensional vectors.
- Each threshold is calibrated on the same 41 normal validation images.
- Selection uses training features only.

The seed changes both the projection and the starting vector.

### Findings

At 131 vectors, coreset missed 0, 1, and 0 defects, compared with
10, 8, and 4 for random sampling.

At 658 vectors, coreset missed no defects across all seeds.
Random sampling missed one defect in one run.

At 1,317 vectors, neither method missed defects. Coreset produced
2, 1, and 1 false alarms, compared with 0, 1, and 0 for random sampling.

Coreset AUROC at 131 vectors was 1.0000, 0.9952, and 1.0000.
At both larger budgets, it was 1.0000 across all seeds.

### Interpretation

The largest benefit appeared under the tightest memory budget.
Coreset did not outperform random sampling on every measure.

Perfect ranking can coexist with false alarms because the decision
threshold is calibrated separately from test evaluation.

### Limitations

The same 83 test images were reused throughout.
No independent-category evaluation, quantitative localization
evaluation, or controlled runtime benchmark was performed.

This sampler approximates representative selection and is not an
exact reproduction of the official PatchCore sampler.

### Evidence

- [Comparison notebook](notebooks/02_coreset_vs_random.ipynb)
- [18-run results](results/random_vs_coreset_comparison.csv)
- [Comparison figure](figures/random_vs_coreset_errors.png)

### Decision

Complete this bottle comparison and move to the all-category dataset
explorer. Reserve new-category test results until the evaluation
procedure is fixed.

### Proposed approach

- Project training vectors from 1,024 to 128 dimensions for selection.
- Apply greedy farthest-first selection in the projected space.
- Use selected original 1,024-dimensional vectors for scoring.
- Compare 131, 658, and 1,317 selected vectors.
- Use seeds 42, 43, and 44.
- Recalibrate thresholds using only the normal validation images.
- Report every predefined configuration.

This will be a documented approximation, not an exact reproduction of the official PatchCore sampler.

## Saved evidence

- [Nine-run comparison](results/random_memory_comparison.csv).
- [Per-image evaluation scores](results/random_memory_comparison_scores.csv).
- [Notebook](notebooks/01_random_memory_baseline.ipynb).

Large memory banks and feature caches remain in Google Drive.

## Reflection

The main learning outcome is understanding how feature representations, memory selection, distance scoring, and threshold calibration interact.

A strong single result was not enough: repeated sampling revealed variability, and visualization helped distinguish ranking quality from decision errors.