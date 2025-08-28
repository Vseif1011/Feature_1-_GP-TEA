# Symptom Checker (XGBoost)

This folder contains the standalone symptom checker based on XGBoost.

## Contents
- `symptom_checker.py` — Train, save artifacts, evaluate, and interactive prediction
- `preprocess_data.py` — Clean the raw dataset into `cleaned_dataset.csv`
- `evaluate_symptom_checker.py` — Train/test split evaluation
- `requirements.txt` — Minimal dependencies
- (Optional) `cleaned_dataset.csv` — Cleaned dataset for evaluation
- Artifacts after saving:
  - `symptom_model.json` — Trained model
  - `symptom_model.labels.npy` — Label encoder classes
  - `symptom_model.features.txt` — Feature order used by the model

## Setup
```bash
pip install -r requirements.txt
```

## Preprocess (optional)
```bash
python preprocess_data.py --input "Disease and symptoms dataset.csv" --output cleaned_dataset.csv
```

## Train and Save Artifacts (one-time)
```bash
python symptom_checker.py --csv cleaned_dataset.csv --save-prefix symptom_model
```
Creates:
- `symptom_model.json`
- `symptom_model.labels.npy`
- `symptom_model.features.txt`

## Evaluate Saved Model 
```bash
python symptom_checker.py --eval-only --csv cleaned_dataset.csv --artifacts-prefix symptom_model
```
##HERE

## Interactive Predictions
```bash
python symptom_checker.py --interactive-only --artifacts-prefix symptom_model
```
Enter symptoms separated by commas (e.g., `fever, cough, headache`). Type `list` to see features, or `quit` to exit.

## API-Style Predictions (Multiple Output Formats)
```bash
# JSON format (best for web apps/APIs)
python api_symptom_checker.py --symptoms fever cough headache --format json

# CSV format (best for data analysis)
python api_symptom_checker.py --symptoms fever cough headache --format csv

# Simple format (best for CLI)
python api_symptom_checker.py --symptoms fever cough headache --format simple
```

## Notes
- GPU is used automatically if supported by your XGBoost build; otherwise CPU.
- Keep the three artifact files together for evaluation and interactive use.
