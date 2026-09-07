# Experiment log — [Project name]

Copy this file into a project folder. Add an entry for every meaningful experiment, including failures. Record what actually happened; use “not yet measured” for missing results.

Use validation data to guide experiments. Reserve the final test set for evaluating the selected approach.

## Experiment index

| ID | Date | Question or change | Outcome | Decision |
| --- | --- | --- | --- | --- |
| [EXP-001] | [YYYY-MM-DD] | [Baseline question] | [Not yet run] | [Pending] |

## [EXP-001] — [Short title]

**Date:** [YYYY-MM-DD]  
**Status:** [Planned / Running / Completed / Failed]

### Question and hypothesis

[What are you testing? What result do you expect, and why?]

### Baseline or previous comparison

[Reference the baseline or earlier experiment ID. Explain what stays the same.]

### Change being tested

[Describe one main change. If several things change together, acknowledge that their effects cannot be isolated.]

### Reproduction details

- **Code:** [Commit ID, or clearly identify uncommitted changes.]
- **Data:** [Source version, subset, and preparation version.]
- **Split:** [Split identifier, date boundaries, or grouping method.]
- **Method:** [Model/version, preprocessing, and main parameters.]
- **Randomness:** [Seed or seeds; note nondeterministic behavior.]
- **Environment:** [Dependency versions and CPU/GPU.]
- **Run:** [Exact command or notebook and execution order.]
- **Resources:** [Runtime and cost, if relevant.]
- **Artifacts:** [Paths to configuration, outputs, or figures; avoid secrets and large files.]

### Results

| Metric | Baseline value | This experiment | Split and notes |
| --- | --- | --- | --- |
| [Metric and preferred direction] | [Not yet measured] | [Not yet measured] | [Context] |

[Record actual measurements and any failed runs. Include variability if measured.]

### Observations and errors

[What worked? Which examples failed? Were there unexpected data or implementation issues?]

### Interpretation

[Does the evidence support the hypothesis? Separate observations from possible explanations.]

### Decision and next step

**Decision:** [Keep / Reject / Investigate / Inconclusive]  
**Reason:** [Evidence supporting this choice.]  
**Next step:** [One focused action.]

---

Copy the experiment entry above for the next run and update the index.

