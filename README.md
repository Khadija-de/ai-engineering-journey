# AI Engineering Journey

A hands-on learning portfolio: turning raw data, research ideas, and practical questions into reproducible AI projects.

## Purpose

This repository documents my growth in data engineering, machine learning, and AI systems, with a focus on skills relevant to data and process analytics roles. Each project should explain a problem, show how the data was prepared, evaluate a solution honestly, and communicate what the results mean.

My starting point includes mathematical foundations in machine learning and deep learning, experience cleaning data, and a waste-detection project that used collected images and a model on a robot camera. That experience provides context for this journey; its implementation and results are not yet included here.

**Current status:** repository scaffold. The ideas below are planned learning directions, not completed projects or claimed results.

## Learning philosophy

- **Learn by building.** Start with a small question and a working end-to-end example.
- **Understand the data first.** Inspect quality, labels, missing values, bias, and permission to use the data before modeling.
- **Start simple.** Establish a rule-based or simple statistical baseline before trying a larger model.
- **Experiment deliberately.** Change one main thing at a time and record both useful and unsuccessful experiments.
- **Make results reproducible.** Document data versions, dependencies, preparation steps, settings, and evaluation.
- **Explain the practical value.** Connect technical results to a decision, workflow, or user need.
- **Be honest about limits.** Separate measured results from assumptions and future ideas.

Training from scratch is useful for understanding small models. Using pretrained models or fine-tuning is also valuable engineering practice. Each project should explain the choice and the available computing budget.

## Repository map

| Folder | Focus |
| --- | --- |
| [01-data-engineering](01-data-engineering/) | Data collection, cleaning, validation, and repeatable pipelines |
| [02-computer-vision](02-computer-vision/) | Image classification, detection, and visual inspection |
| [03-nlp](03-nlp/) | Text preparation, classification, and document retrieval |
| [04-time-series](04-time-series/) | Forecasting, temporal evaluation, and anomaly detection |
| [05-generative-ai](05-generative-ai/) | Generation, retrieval-augmented systems, and evaluation |
| [06-robotics](06-robotics/) | Perception, simulation, and robot behavior |
| [07-world-models](07-world-models/) | Learning to predict how environments change |
| [08-embodied-ai](08-embodied-ai/) | Agents that connect observations, goals, and actions |
| [09-capstone-project](09-capstone-project/) | An integrated project addressing a practical problem |
| [docs](docs/) | Reusable documentation and experiment templates |

The numbering organizes topics; it is not a requirement to finish every area in order. Start with data engineering, then choose one area that supports a concrete project. Robotics, world models, and embodied AI can remain longer-term explorations.

## Project workflow

1. **Define the problem.** Write one question, the intended user, and a measurable success criterion.
2. **Find and inspect data.** Record the source, license, version, fields, quality issues, and limitations. Keep raw data unchanged.
3. **Prepare a reproducible pipeline.** Separate raw and processed data; make transformations repeatable.
4. **Plan evaluation.** Split data before learning preprocessing parameters. Keep related examples together and respect time order when needed. Reserve a final test set.
5. **Build a baseline.** Measure a simple approach with a metric suited to the problem.
6. **Run focused experiments.** Record hypotheses, settings, results, and decisions in an experiment log. Use validation data for model selection.
7. **Evaluate and inspect failures.** Compare against the baseline, examine errors, and report final test results after selecting the approach.
8. **Package and communicate.** Add clear run instructions, a small example or demo, findings, limitations, and next steps.

Use [the project template](docs/project-template.md) for each project's README and [the experiment log](docs/experiment-log.md) to track your work.

## Start your first project

A manageable first idea is **a data-quality pipeline for an operational dataset**: load a public CSV, document its schema, handle missing or duplicate records, validate the output, and explain how quality issues affect one useful metric.

1. Create `01-data-engineering/operational-data-quality/`.
2. Copy `docs/project-template.md` into that folder as `README.md`.
3. Copy `docs/experiment-log.md` into that folder.
4. Fill in the problem, dataset, and baseline sections before expanding the scope.
5. Complete one small, reproducible result before starting another project.

Suggested structure inside an individual project:

```text
project-name/
├── README.md
├── experiment-log.md
├── requirements.txt       # Dependencies and tested versions, if using Python
├── data/
│   └── README.md          # Source, license, and download/preparation instructions
├── notebooks/             # Exploration and explanations
├── src/                   # Reusable preparation, training, or evaluation code
├── tests/                 # Meaningful checks as the project develops
└── reports/
    └── figures/           # Small, shareable result images
```

Create only the files needed for the project. This starter repository has no shared runtime or training code; document setup in each project when you add its implementation.

## Portfolio goals

Build a small set of finished projects that demonstrate:

- **Data skills:** cleaning, validation, SQL or equivalent transformations, and reliable pipelines.
- **Analytical judgment:** clear questions, suitable comparisons, and interpretation of results.
- **Engineering practice:** reproducible runs, useful checks, readable code, and documented tradeoffs.
- **Communication:** concise findings that a recruiter or nontechnical colleague can understand.

For GitHub, make each project independently understandable: include setup instructions, data access instructions, a baseline comparison, a result visual when useful, and limitations.

For LinkedIn, share a short account of the problem, your approach, one measured finding, what you learned, and a link to the project. Publish only results you actually obtained. Avoid claiming business impact unless it was measured.

### Project tracker

Add rows as projects begin. Link to the project folder and use a clear status such as planned, in progress, or complete.

| Project | Area | Status | Evidence |
| --- | --- | --- | --- |
| First project — to be selected | Data engineering | Planned | No results yet |

## Data and repository hygiene

- Keep datasets, model weights, credentials, and local environments out of Git.
- Provide data download instructions and license details instead of uploading third-party data by default.
- Fit learned preprocessing on training data only; check for target leakage and duplicate examples across splits.
- Remove private information from outputs, screenshots, and notebook cells before publishing.
- Use a tiny synthetic sample when an example is needed and label it clearly.
- Cite datasets, papers, reused code, and pretrained models in the relevant project.
- Choose a code license before distributing this work for reuse; dataset and model licenses remain separate.

Progress is documented through completed experiments and clear explanations, not the number of topics covered.

