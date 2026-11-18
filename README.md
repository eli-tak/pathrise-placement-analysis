# Pathrise Placement Classification

An educational analysis of whether information presumed available at the beginning of a job-search program can predict eventual placement. The actual timing and definitions of these fields need verification. This model is not for decisions about individuals.

## Files

- `pathrise_analysis.ipynb`: revised analysis, evaluation and model pipeline.
- `Data_Pathrise.xlsx`: input workbook, required in the notebook directory.
- `requirements.txt`: dependencies for the tested environment.

## Run

With Python 3, install the requirements and start Jupyter from this directory:

```bash
pip install -r requirements.txt
jupyter notebook
```

Open `pathrise_analysis.ipynb` and run all cells in order. Running it creates `models/pathrise_pipeline.joblib`, containing preprocessing and the selected classifier. Load joblib artifacts only from trusted sources.

## Method and results

The analysis excludes unresolved participant statuses, retains withdrawals as non-placement, and sets aside a stratified 20% test split. Missing values and categorical encoding are handled inside each training fold. Five-fold cross-validation selects between logistic regression and random forest using F1; a majority-class baseline is also reported.

In this execution, logistic regression was selected. Test accuracy was 55.9%, ROC AUC 0.565, and placed-class precision and recall were 0.55 and 0.64. Cross-validation F1 was about 0.582 for logistic regression, below the majority baseline of 0.671: the model does not outperform that simple baseline on this metric. The test results are specific to this split and must not be treated as a guarantee.

## Limitations

- Field timing and definitions have not been verified. Confirm that features were available at the intended prediction time.
- The treatment of unresolved participants and withdrawals can bias the study.
- A random split does not establish performance on future cohorts or unseen populations.
- Omitting demographic inputs does not ensure fairness. The model is not suitable for consequential decisions.

## Data provenance

The workbook used in this project was provided as part of a data science course. A similarly structured dataset is available on [Kaggle](https://www.kaggle.com/datasets/sagharganji/pathrise-dataset), where the listing displays an MIT license. The relationship between that listing and the course-provided workbook, the original source, and redistribution rights have not been independently verified. Obtain the workbook separately and place it beside the notebook. Before publishing the workbook, confirm the applicable permissions and check for personal information.
