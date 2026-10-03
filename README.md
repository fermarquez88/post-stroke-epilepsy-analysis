# Post-stroke epilepsy: analysis code

Python notebooks from the retrospective cohort study of predictive factors for
epilepsy after ischemic stroke at Fleni (Buenos Aires, Argentina), published as:

> Alet M, Márquez F, Marone A, Darakdjian M, Sosa F, Bonamico L, Ameriso SF.
> Predictive factors for the development of epilepsy after ischemic stroke.
> *J Stroke Cerebrovasc Dis.* 2022;31(12):106858.
> doi: [10.1016/j.jstrokecerebrovasdis.2022.106858](https://doi.org/10.1016/j.jstrokecerebrovasdis.2022.106858)

**Scope.** These notebooks contain the preliminary analysis (2020) that preceded
the article: merging of the chart-review form with the institutional stroke
registry, inclusion/exclusion criteria, de-duplication of readmissions,
cleaning and imputation, Table 1 (`tableone`), Spearman correlations and
logistic regression with backward elimination. The final cohort and model
reported in the article (larger sample, longer recruitment window) were
produced later and are not fully reproduced here.

| Notebook | Content |
|---|---|
| `notebooks/01_post_stroke_epilepsy_analysis.ipynb` | Last version of the analysis notebook (November 2020) |
| `notebooks/00_exploratory_CAN2020.ipynb` | Earlier exploratory version (Argentine Neurology Congress 2020 abstract), kept because it contains code dropped later: labelled Table 1 with automatic normality test, seizure plots, `funpymodeling` profiling |

## Data

**Patient data are not published.** The source spreadsheets contain clinical
records from the Fleni stroke registry and are confidential. This repository
contains code only: all notebook outputs were removed and no data files are
included. Requests about the data should be addressed to the corresponding
author of the article.

## How to run

```bash
python -m venv .venv
.venv/bin/pip install -r requirements.txt
export PSE_DATA_DIR=/path/to/local/data   # folder with the four spreadsheets below
.venv/bin/jupyter lab notebooks/
```

`PSE_DATA_DIR` must contain `chart_review.xlsx`, `stroke_registry_2016_2020.xlsx`,
`stroke_registry_2015_2016.xlsx` and `ehr_search.xls`, with the original
(Spanish) column names used in the notebooks. The code was written in 2020
with pandas 1.x; recent pandas/statsmodels versions may need small changes.

To keep outputs out of version control, install the pre-commit hook once:
`pip install pre-commit && pre-commit install` (it runs `nbstripout`).
