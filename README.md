# Metamorphic assurance of multi-view ECG feature pipelines (PTB-XL / PTB-XL+)
Repository: https://github.com/hembabu78github/multiview_ecg  (archive DOI: to be added after Zenodo release)
## Setup
    pip install -r repo/requirements.txt
Download from PhysioNet (free account; check each licence) and place in `data/`:
`ptbxl_database.csv`, `scp_statements.csv` (PTB-XL 1.0.3) and `features/12sl_features.csv`, `features/ecgdeli_features.csv`, `features/unig_features.csv`, `feature_description.csv` (PTB-XL+ 1.0.1), renamed as `data/12sl_features.csv`, `data/ecgdeli_features.csv`, `data/unig_features.csv`, `data/feature_description.csv`.
Paths are relative to the repository root (override with `JBHI_ROOT`). No data are redistributed.
## Reproduce
    cd code && bash rerun_all_ext.sh     # models, scenarios, monitors, decision metrics, fusion, abstention
    python run_experiments.py --split val ; python run_experiments.py --split test
    bash run_rot_all.sh                  # ten-fold rotation (sensitivity analysis)
    python run_benign.py 100 ; python monitors_matched.py ; python cost_ratio_sens.py ; python cost_timing.py
    python verify.py test ; python verify_ext.py ; python -m pytest tests
Seeds are fixed in `common.py`. Trained models and scenario arrays are regenerated, not shipped.
## Protocol sequence
Design frozen on folds 1-8 / fold 9; fold 10 evaluated as the confirmatory test; ten-fold rotation and all later analyses (cost ratios, matched false-alarm comparison) are post-hoc sensitivity analyses.
Clinical review: see `review/CLINICAL_REVIEW_PROVENANCE.md`.
