# AbEvolve: Developability-Guided Antibody Sequence Design

AbEvolve is a machine learning pipeline for designing antibody sequences with improved developability, focusing on thermostability and aggregation risk while preserving structural compatibility. By combining antibody inverse folding, protein language models, and multi-objective optimization, the project aims to prioritize promising therapeutic antibody candidates before costly laboratory testing.

## Problem

Antibody design models can generate sequences compatible with a target protein structure, but these sequences may still have poor thermostability, high aggregation risk, or low expression, making them difficult to manufacture.

AbEvolve addresses this bottleneck by incorporating developability predictions directly into antibody sequence design rather than evaluating these properties only after candidate generation. The project is intended for researchers and engineers working in machine learning, computational biology, and therapeutic antibody discovery.

## Approach

AbEvolve integrates antibody sequence generation, supervised property prediction, iterative optimization, and structural validation into a unified pipeline.

- **Datasets:** GDPa1 / PROPHET-Ab, FLAb2, and GDPa3 for experimental developability measurements; SAbDab2 / PDB for antibody structures.
- **Sequence generation:** AntiFold or AbMPNN generates antibody sequences conditioned on a target backbone.
- **Property prediction:** ESM-family protein language model embeddings are used to train and evaluate Ridge regression and multilayer perceptron (MLP) models for predicting thermostability and a second property, such as aggregation or expression.
- **Multi-objective optimization:** Pareto-based candidate selection and targeted mutations balance predicted developability with structural compatibility.
- **Structural validation:** IgFold is used to assess whether shortlisted sequences retain the target structure. Uncertainty and out-of-distribution checks help flag unreliable predictions.
- **Platform:** A planned React frontend and FastAPI backend will support structure uploads, design constraints, candidate visualization, and sequence export.

The pipeline will be benchmarked against random mutation, one-shot inverse-folding sampling, and top-k selection baselines.

## Results

A preliminary feasibility experiment conducted by the project author found that an ESM-Ridge thermostability model enriched its top-five shortlist by approximately **+2.9°C** and recovered **60% of the experimentally validated top-five antibodies**.

These findings support further investigation of developability-guided candidate selection. The complete optimization pipeline is still subject to systematic evaluation.

Planned evaluation metrics include:

- **Predictive performance:** Median cluster-aware Spearman correlation of at least 0.35.
- **Candidate prioritization:** Precision\@k, Recall\@k, NDCG\@k, and statistical confidence intervals.
- **Optimization:** Target at least a 10% improvement in median two-objective hypervolume over one-shot AntiFold sampling.
- **Structural retention:** Target at least 80% of shortlisted designs achieving a TM-score of at least 0.8 against the target backbone.
- **Reliability:** Calibrated uncertainty flags for generated candidates.
- **System integration:** An end-to-end pipeline and interactive web application.

These are project targets, not achieved results.

## UTMIST metadata

- **Team:** AbEvolve; Bingxuan Yang (project lead) and 6–8 developers across property modeling, developability optimization, and validation/platform engineering. Add confirmed team member names and roles as they are assigned.
- **Term:** Fall 2026 – Winter 2027 (planned; update to reflect the actual project schedule).
- **Type:**
  - [x] Engineering
- **Status:** Exploring / early-stage development. A preliminary thermostability-ranking experiment has demonstrated feasibility. Next steps include establishing reproducible baselines, validating property predictors, integrating sequence generation and optimization, and evaluating structural retention and reliability.

---

## Getting started

This project is built on the [UTMIST ML Seed](https://github.com/UTMIST/utmist-ml-seed). Full documentation lives in [`docs/`](docs/README.md):

- [Setup](docs/setup/installation.md) — install dependencies.
- [Usage](docs/usage/commands.md) — training, evaluation, and configuration commands.
- [Workflows](docs/README.md#documentation) — research versus engineering workflows.
- [Contributing](docs/contributing/guidelines.md) — branch naming, commits, and pull requests.

## License

This repository inherits the [MIT License](LICENSE) from UTMIST ML Seed. Confirm that the license is appropriate for the project and compatible with the licenses of its datasets, models, and dependencies before distribution.
