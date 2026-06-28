# Survival Analysis of Heart Failure Clinical Records

## Overview

This repository contains a survival analysis project for the `heart_failure_clinical_records_dataset.csv` data set. The analysis studies time to death among heart-failure patients using nonparametric survival estimators, parametric accelerated failure time models, a Bayesian extension, and semiparametric Cox proportional hazards models.

The repository is a curated version of the final coursework project. It combines the final notebooks and presentation deliverables with the newer corrected tables, figures, and LaTeX Beamer source from the working directory.

## Methods

The project covers four main modelling blocks:

1. nonparametric survival analysis with Kaplan-Meier and Nelson-Aalen estimators;
2. group comparisons with nonparametric tests for censored survival data;
3. parametric and Bayesian survival models, including Weibull AFT profiles;
4. Cox proportional hazards modelling, proportional-hazards diagnostics, Schoenfeld residuals, influential observations, and a time-interaction extension.

## Mathematical formulation

For a non-negative event time $T$, the survival function and cumulative hazard are

$$
S(t)=\Pr(T>t), \qquad H(t)=\int_0^t h(u)\,du.
$$

The Kaplan-Meier estimator used in the nonparametric notebook is

$$
\widehat S(t)=\prod_{t_j\le t}\left(1-\frac{d_j}{n_j}\right),
$$

where $d_j$ is the number of events at time $t_j$ and $n_j$ is the risk-set size just before $t_j$.

The Cox model is specified as

$$
h(t\mid x)=h_0(t)\exp(x^\top\beta),
$$

so that $\exp(\beta_k)$ is interpreted as a hazard ratio for a one-unit increase in covariate $x_k$, holding other covariates fixed.

## Repository structure

```text
data/                         input heart-failure data set
notebooks/                    final executable analysis notebooks
presentation/                 Beamer source and final presentation PDF
reports/                      supplementary interpretation notes
tables/                       corrected LaTeX result tables
figures/                      corrected model and diagnostic figures
results/                      compact run summary metadata
```

Recommended review order:

1. `presentation/survival_analysis_presentation.pdf` for the final project deck;
2. `notebooks/01_nonparametric_survival_analysis.ipynb`;
3. `notebooks/02_parametric_and_bayesian_survival_models.ipynb`;
4. `notebooks/03_cox_semiparametric_model_diagnostics.ipynb`;
5. `reports/interpretation_notes.pdf` for supplementary interpretation comments.

## Reproducibility

Install the Python dependencies:

```bash
pip install -r requirements.txt
```

Run the notebooks from the repository root so that relative paths resolve against `data/`, `tables/`, and `figures/`.

The presentation can be rebuilt from the `presentation/` directory with a LaTeX installation that supports Beamer:

```bash
cd presentation
pdflatex main.tex
pdflatex main.tex
```

## Data

The repository includes `data/heart_failure_clinical_records_dataset.csv`. The run summary records:

- observations: 299;
- observed deaths/events: 96;
- censored observations: 203;
- presentation slides: 61.

## Main outputs

Key outputs include Kaplan-Meier survival curves, Nelson-Aalen cumulative hazards, actuarial life-table summaries, parametric model comparisons, Bayesian traceplots, Cox coefficient estimates, proportional-hazards diagnostics, and predicted survival profiles for clinical risk profiles.

## References

- Cox, D. R. (1972). Regression models and life-tables. *Journal of the Royal Statistical Society: Series B*.
- Kaplan, E. L., & Meier, P. (1958). Nonparametric estimation from incomplete observations. *Journal of the American Statistical Association*.
- Nelson, W. (1972). Theory and applications of hazard plotting for censored failure data. *Technometrics*.
- Davidson-Pilon, C. et al. `lifelines` Python survival analysis library documentation.
