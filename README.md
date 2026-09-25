# Telco customer churn analysis

## Decision supported

Explore which historical customer characteristics are associated with churn and whether a logistic model can rank customer risk. This is an independent IBM Telco dataset study, not a deployed retention system or a measurement of saved customers.

## Evidence to review

Open [the notebook](Telco_customer_churn.ipynb): it contains profiling of 7,043 customer records, explicit removal of churn-label/reason/score features, a preprocessing pipeline, a fixed stratified split, training cross-validation, a precision–recall curve and an exploratory threshold comparison.

Saved outputs report test ROC-AUC 0.849 and mean training CV ROC-AUC 0.859. At the explored 0.4 threshold, recall is 0.668 and precision 0.577. Those threshold statistics reuse test labels for selection; they are not an untouched final evaluation or a proven business optimum.

## Limits and next decision

- Verify the scoring-time construction of CLTV and the assumption that missing Total Charges mean zero before considering operational use.
- Validate thresholds on separate development data; retain fresh evaluation data. No new validation run is claimed here.
- A risk score does not estimate the effect of a retention offer. Use contact capacity, intervention cost and incremental retention to design a future controlled pilot.
- Sensitive attributes and proxies need review before customer targeting. No fairness audit, probability-calibration study or performance confidence intervals were completed in this notebook.

## Reproduction

The notebook was built in Google Colab and mounts a personal Google Drive path. Supply an authorized copy of the IBM Telco dataset variant with the documented columns, then update `file_path` in the loading cell. The source CSV and a pinned environment are not included in this repository, so exact reproduction cannot currently be guaranteed.

Imports include pandas, NumPy, SciPy, matplotlib, seaborn and scikit-learn. The split uses `random_state=42`. Run cells in order after confirming source columns. Published outputs are historical; the comparison-table output is cleared because that cell now computes metrics from the existing predictions instead of hand-entered values.

The complete assumptions, evaluation boundary and handoff notes are at the end of the notebook.
