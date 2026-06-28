# Survival Analysis of Heart Failure Clinical Records

## Overview

This repository contains a survival analysis project based on the `heart_failure_clinical_records_dataset.csv` data set. The study focuses on modelling the time until death among patients with heart failure, using `time` as the duration variable and `DEATH_EVENT` as the event indicator.

The data set contains 299 patient records. There are 96 observed deaths and 203 right-censored observations, so censoring is an important feature of the analysis. The project compares several approaches to survival modelling rather than relying on a single method.

The repository is a cleaned and organised version of the final coursework project. It contains the analysis notebooks, corrected figures and tables, supplementary interpretation notes, and the final presentation materials.

## Data

The analysis uses clinical and laboratory information about patients with heart failure. The most important variables include:

* `time` — follow-up time in days;
* `DEATH_EVENT` — death indicator;
* `age` — patient age;
* `anaemia`, `diabetes`, `high_blood_pressure`, `sex`, `smoking` — binary clinical or demographic variables;
* `ejection_fraction` — heart ejection fraction;
* `serum_creatinine` — serum creatinine level;
* `serum_sodium` — serum sodium level;
* `platelets` — platelet count;
* `creatinine_phosphokinase` — CPK level.

The CPK variable is transformed into `log_cpk` because of its skewed distribution.

## Methods

The project is divided into four main analytical parts.

### Nonparametric survival analysis

The first part estimates survival patterns directly from the data. It includes:

* Kaplan-Meier survival curves;
* Nelson-Aalen cumulative hazard estimates;
* actuarial life-table summaries;
* survival comparisons between clinical subgroups;
* log-rank and Wilcoxon tests.

This part is used as an exploratory baseline. It shows which patient characteristics visibly separate survival curves before moving to regression models.

The strongest subgroup differences are observed for low ejection fraction, elevated serum creatinine, low serum sodium, and hypertension.

### Parametric AFT models

The second part compares parametric accelerated failure time models. The fitted distributions include:

* Weibull;
* log-normal;
* log-logistic;
* exponential baseline model.

The Weibull AFT model is selected as the main parametric model because it gives a good balance between fit, interpretability, and information criteria. A reduced Weibull model is also estimated to remove weak predictors and make the model more stable.

The most relevant predictors in the AFT framework are age, ejection fraction, serum creatinine, hypertension, anaemia, and serum sodium.

### Bayesian Weibull model

The Bayesian part is a simplified extension of the Weibull model. It focuses on three key predictors:

* age;
* ejection fraction;
* serum creatinine.

This model is mainly demonstrative. Its purpose is to show how survival analysis can be expressed in Bayesian terms and how uncertainty in the parameters can be analysed through posterior distributions.

The Bayesian results are directionally consistent with the classical models: higher age and higher creatinine are associated with worse survival, while higher ejection fraction is associated with better survival.

### Cox proportional hazards model

The final modelling block uses the Cox proportional hazards model. This model estimates the effect of patient characteristics on the hazard of death without imposing a fully parametric distribution on survival times.

The Cox model confirms the importance of age, ejection fraction, serum creatinine, and hypertension. It also includes diagnostics based on Schoenfeld residuals and influence analysis.

One important diagnostic result is that the proportional hazards assumption is not perfectly satisfied for ejection fraction. For this reason, the project also tests a time-interaction extension. The extended model does not improve the overall fit enough to replace the baseline Cox model, but it helps interpret the diagnostic issue more carefully.

## Main findings

Across the different modelling approaches, the results are broadly consistent.

The variables most clearly associated with worse survival are:

* higher age;
* lower ejection fraction;
* higher serum creatinine;
* hypertension;
* possibly anaemia and lower serum sodium, although these effects are weaker.

The project also shows that model diagnostics matter. The Cox model gives interpretable hazard ratios, but the proportional hazards assumption should not be accepted automatically. Similarly, parametric AFT models are useful for prediction and scenario analysis, but their conclusions depend on the assumed survival-time distribution.

The analysis should be treated as a methodological coursework project rather than a clinical decision model. The sample is small, the number of observed deaths is limited, and no external validation data set is used.

## Repository structure

```text
data/                         input heart-failure data set
notebooks/                    final executable analysis notebooks
presentation/                 Beamer source and final presentation PDF
reports/                      supplementary interpretation notes
tables/                       corrected result tables
figures/                      corrected model and diagnostic figures
results/                      compact run summary metadata
```

## Recommended review order

1. `presentation/survival_analysis_presentation.pdf` — final project presentation.
2. `notebooks/01_nonparametric_survival_analysis.ipynb` — Kaplan-Meier, Nelson-Aalen, life table, and subgroup tests.
3. `notebooks/02_parametric_and_bayesian_survival_models.ipynb` — AFT models and Bayesian Weibull extension.
4. `notebooks/03_cox_semiparametric_model_diagnostics.ipynb` — Cox model, diagnostics, and predicted risk profiles.
5. `reports/interpretation_notes.pdf` — supplementary interpretation notes.

## Reproducibility

Install the required Python dependencies:

```bash
pip install -r requirements.txt
```

Run the notebooks from the repository root so that relative paths resolve correctly.

The presentation can be rebuilt from the `presentation/` directory:

```bash
cd presentation
pdflatex main.tex
pdflatex main.tex
```

## Main outputs

The repository contains:

* survival curves for the full sample and selected subgroups;
* cumulative hazard estimates;
* actuarial life-table summaries;
* nonparametric tests for subgroup differences;
* AFT model comparison tables;
* Weibull AFT estimates and prediction profiles;
* Bayesian posterior summaries and traceplots;
* Cox model estimates;
* proportional hazards diagnostics;
* influence diagnostics;
* predicted survival and hazard profiles.

## Limitations

The main limitations of the project are:

* small sample size;
* limited number of observed deaths;
* high share of right-censored observations;
* no external validation sample;
* sensitivity of parametric models to distributional assumptions;
* partial violation of the proportional hazards assumption in the Cox model.

## References

* Cox, D. R. (1972). Regression models and life-tables. *Journal of the Royal Statistical Society: Series B*.
* Kaplan, E. L., & Meier, P. (1958). Nonparametric estimation from incomplete observations. *Journal of the American Statistical Association*.
* Nelson, W. (1972). Theory and applications of hazard plotting for censored failure data. *Technometrics*.
* Davidson-Pilon, C. et al. `lifelines` Python survival analysis library documentation.
