# [Project name]

> Template: replace bracketed prompts and remove this note before publishing.

**Status:** [Planned / In progress / Complete]  
**Area:** [Learning area]  
**Last updated:** [YYYY-MM-DD]

## Overview

[In two or three sentences: what problem are you addressing, who would use the result, and what does this project deliver?]

## Problem and success criteria

- **Question:** [One specific question.]
- **Intended use:** [The decision or workflow this supports.]
- **Success criterion:** [Metric, baseline, and target; explain why this is meaningful.]
- **Scope:** [What the first version covers and its boundaries.]

## Data

| Item | Details |
| --- | --- |
| Source and citation | [Dataset name, creator, and source link] |
| Access and license | [Download steps, terms, and redistribution restrictions] |
| Version | [Release, retrieval date, or checksum] |
| Unit of observation | [What one row, image, document, or sequence represents] |
| Size and coverage | [Rows/files, time range, populations, or environments] |
| Inputs and target | [Features and prediction target, if applicable] |
| Known limitations | [Missingness, label quality, imbalance, bias, privacy] |

[Explain where data belongs locally. Keep raw data unchanged and document a small synthetic sample if used.]

## Preparation and quality checks

[Describe cleaning, transformations, exclusions, and validation. Include before/after counts when relevant. Explain how steps can be rerun.]

## Evaluation plan

- **Split strategy:** [Train/validation/test proportions or dates; grouping rules.]
- **Leakage prevention:** [How related examples are separated and preprocessing is fitted.]
- **Baseline:** [Simple comparison and why it is appropriate.]
- **Metrics:** [Definitions and why they fit the problem.]
- **Final evaluation:** [When the test set is used and any uncertainty or repeated-run checks.]

[For a pipeline-only project, adapt this section to correctness, quality, and reproducibility checks.]

## Approach

[Explain the main steps and choices in plain language. State whether you use rules, training from scratch, fine-tuning, or a pretrained model, and why.]

## Reproduce the project

**Tested environment:** [OS, language version, CPU/GPU, and relevant memory requirements.]

1. [Install dependencies using the project's actual dependency file.]
2. [Obtain the documented data version and place it in the expected location.]
3. [Run preparation using the exact command or notebook order.]
4. [Run the baseline and main experiment.]
5. [Run evaluation and identify the output files.]

[Add exact commands once implemented. Document random seeds, configuration, approximate runtime, and any paid services. List required environment variable names without including secrets.]

## Results

**Evaluation status:** [Not yet measured / Validation results / Final test results]

| Approach | Split | Metric and direction | Measured value | Notes |
| --- | --- | --- | --- | --- |
| [Baseline] | [Split] | [e.g., MAE, lower is better] | [Not yet measured] | [Context] |
| [Main approach] | [Same split] | [Same metric] | [Not yet measured] | [Context] |

[Explain the comparison. Link to a useful figure or demo. State sample size and variability when relevant. Do not infer operational impact solely from model accuracy.]

## Error analysis and limitations

[Show representative failures, possible causes, where results may not generalize, and what remains untested.]

## Lessons learned

[What changed your understanding? Which experiment failed, and what did you learn? Link to experiment-log.md.]

## Next steps

- [One focused improvement supported by the current evidence.]

## Portfolio summary

[Write a short public-facing paragraph: problem, contribution, measured result if available, and one lesson. Add the public repository or demo link when available.]

## References

[Dataset, paper, code, and model citations. Document attribution and relevant licenses.]

