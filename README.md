# Post-stroke epilepsy study, preliminary analysis code (2020)

Python notebooks written in 2020 for the preliminary analysis of a retrospective cohort of
ischemic stroke patients at Fleni (Buenos Aires, Argentina), presented at the 57th Argentine
Congress of Neurology (Congreso Argentino de Neurología, 2020). The study was later completed
with a larger cohort and published as:

> Alet M, Márquez F, Marone A, Darakdjian M, Sosa F, Bonamico L, Ameriso SF.
> Predictive factors for the development of epilepsy after ischemic stroke.
> *J Stroke Cerebrovasc Dis.* 2022;31(12):106858.
> doi: [10.1016/j.jstrokecerebrovasdis.2022.106858](https://doi.org/10.1016/j.jstrokecerebrovasdis.2022.106858)

This repository contains code only. It holds no patient data, no notebook outputs and no
figures. It is research code from 2020, kept as a record of how the preliminary analysis was
done. It is not maintained, it is not a medical device and it does not reproduce the analysis
of the published article.

## What the notebooks do

The notebook reads four local spreadsheets (a chart-review form export, two extracts of the
institutional stroke registry and an electronic health record search used for case finding)
and then:

1. rename the Spanish column names of the source files;
2. apply the inclusion and exclusion criteria and merge the chart review with the registry;
3. detect and remove readmissions of the same patient;
4. clean erroneous values and impute missing values;
5. build Table 1 with `tableone` (overall and stratified by post-stroke epilepsy);
6. compute Spearman correlations with the outcome;
7. fit a logistic regression with backward elimination.

| Notebook | Content |
|---|---|
| `notebooks/01_post_stroke_epilepsy_analysis.ipynb` | Last version of the analysis notebook (November 2020) |

Narrative cells, headings and comments are in Spanish, as they were written. The first
markdown cell reproduces the abstract submitted to the 2020 congress, verbatim.
Working notes from 2020 were left as they were unless they could reveal counts below five.

## Scope and provenance

The preliminary analysis covered admissions between 2014 and 2019 (196 patients with
complete follow-up). The published article covers January 2012 to June 2020, 691 patients, and
reports a different final model. The final cohort, variables and model were produced later
and are not in this repository.

The notebooks were written in 2020 and run locally against institutional files. This public
copy was prepared in October 2026 from those files: all outputs were stripped, local paths
were replaced by an environment variable, and the commented-out helper code that exported raw
records for manual chart review was removed. The original working history is not included
because it contained outputs.

## Known limitations of the 2020 code

The code is published as it was written, so that the preliminary analysis is traceable. It has
limitations that the published article does not share, and the odds ratios in the 2020
abstract should not be quoted:

- The logistic models are fitted without an intercept (`sm.Logit(y, X)` with no constant
  term), which distorts the estimated odds ratios.
- Variables were selected by backward elimination on p-values.
- After filling some variables from the registry, all remaining missing numeric values were
  set to 0 before modelling, including scale scores.
- `fillna(df.median)` passes the method object instead of the computed medians, so that
  imputation step does not work as intended.
- The abstract cell describes a minimum follow-up of one year while the inclusion-criteria
  cell describes two years; the article defines the final criteria.
- Regenerated Table 1 outputs contain small cells and must not be shared or committed.

## Data, ethics and governance

Patient data are not published. The source spreadsheets are clinical records from the Fleni
stroke registry and the study's chart-review form, and they remain with the institution. This
repository adds no data and makes no claim of its own about the study's approvals. Questions
about ethics approval, data access and governance of the study should be addressed to the
corresponding author of the article.

The `.gitignore` blocks data and image files, and the pre-commit hook (`nbstripout`) strips
notebook outputs before every commit.

## Credit

The study is the work of its seven authors at Fleni: Matías Alet (first author) and
Sebastián F. Ameriso (senior author) at the Centro Integral de Neurología Vascular; Abril
Marone at the Centro Integral de Epilepsia y Unidad de Video EEG; Maximiliano Darakdjian at
the Servicio de Diagnóstico por Imágenes; and Federico Sosa, Lucas Bonamico and Fernando
Márquez at the Centro de Rehabilitación de Adultos (Fleni Escobar). The chart-review form, the
neuroimaging reading and the institutional stroke registry that feed these notebooks were
built and maintained by the study team and the institution's services. The analysis code in
this repository was written by Fernando Márquez. Table 1 uses the `tableone` package by
Pollard and colleagues.

## How to run

```bash
python -m venv .venv
.venv/bin/pip install -r requirements.txt
export PSE_DATA_DIR=/path/to/local/data   # folder with the four spreadsheets below
.venv/bin/jupyter lab notebooks/
```

`PSE_DATA_DIR` must contain `chart_review.xlsx`, `stroke_registry_2016_2020.xlsx`,
`stroke_registry_2015_2016.xlsx` and `ehr_search.xls`, with the original Spanish column names
used in the notebooks. The code was written with pandas 1.x; recent pandas and statsmodels
versions may need small changes. To keep outputs out of version control, install the hook
once: `pip install pre-commit && pre-commit install`.

## How to cite

For any scientific use, cite the published article above. To refer to this code:

> Márquez F. Preliminary analysis code (2020) for the Fleni post-stroke epilepsy cohort study.
> GitHub repository, 2026. https://github.com/fermarquez88/post-stroke-epilepsy-analysis

## License

MIT License. See `LICENSE`.

---

En español: código del análisis preliminar (2020) del estudio de epilepsia post-ACV de Fleni,
publicado en 2022. No contiene datos de pacientes ni salidas de los notebooks. Las consultas
sobre los datos y sus aprobaciones corresponden al autor de correspondencia del artículo.
