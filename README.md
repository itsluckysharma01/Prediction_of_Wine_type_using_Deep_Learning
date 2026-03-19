# Prediction of Wine Type Using Deep Learning

An end-to-end deep learning project to classify wine as Red or White using physicochemical features from the Wine Quality datasets.

[![Python](https://img.shields.io/badge/Python-3.10+-3776AB?logo=python&logoColor=white)](https://www.python.org/)
[![TensorFlow](https://img.shields.io/badge/TensorFlow-2.x-FF6F00?logo=tensorflow&logoColor=white)](https://www.tensorflow.org/)
[![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-F37626?logo=jupyter&logoColor=white)](https://jupyter.org/)

## Quick Navigation

- [Project Overview](#project-overview)
- [Project Structure](#project-structure)
- [How to Run](#how-to-run)
- [Notebook Workflow](#notebook-workflow)
- [Dataset Fix Applied](#dataset-fix-applied)
- [Model Architecture](#model-architecture)
- [Troubleshooting](#troubleshooting)
- [Next Improvements](#next-improvements)

---

## Project Overview

This project combines two wine datasets:

- redwinequality.csv
- whitewinequality.csv

It then trains a neural network to predict wine type:

- 1 -> Red wine
- 0 -> White wine

Main features used include acidity, sugar, chlorides, sulfur dioxide, density, pH, sulphates, alcohol, and quality.

---

## Project Structure

```text
Prediction of Wine type using Deep Learning/
|-- redwinequality.csv
|-- whitewinequality.csv
|-- wine_prediction.ipynb
|-- README.md
```

---

## How to Run

<details>
<summary><strong>1) Install dependencies</strong></summary>

```bash
pip install pandas numpy matplotlib seaborn scikit-learn tensorflow keras joblib
```

</details>

<details>
<summary><strong>2) Launch Jupyter</strong></summary>

```bash
jupyter notebook
```

Open wine_prediction.ipynb and run all cells in order.

</details>

<details>
<summary><strong>3) Expected output</strong></summary>

- Dataset loaded with 6497 rows and 13 columns after preprocessing.
- Alcohol distribution plots for both wine types.
- Model training logs for 10 epochs.
- Predicted labels shown as Red or White.

</details>

---

## Notebook Workflow

1. Import libraries
2. Load red and white datasets
3. Fix dataset structure for proper modeling
4. Visualize alcohol distribution by wine type
5. Split data into train and test sets
6. Build neural network model
7. Train model
8. Predict wine type
9. (Optional) Save model

---

## Dataset Fix Applied

<details open>
<summary><strong>What was fixed</strong></summary>

- CSV delimiter corrected using `sep=';'` while reading both files.
- Added `type` column before concatenation:
  - `1` for red wine
  - `0` for white wine
- Rebuilt combined dataset as `wines`.
- Verified missing values and dataset shape.

</details>

<details>
<summary><strong>Why this matters</strong></summary>

Without these fixes:

- Columns are parsed incorrectly as a single text column.
- Classification target (`type`) is missing.
- Downstream plotting and model training fail.

</details>

---

## Model Architecture

The notebook uses a binary classification neural network:

- Input layer: 12 features
- Hidden layer 1: Dense(12), ReLU
- Hidden layer 2: Dense(8), ReLU
- Output layer: Dense(1), Sigmoid
- Optimizer: Adam
- Loss: Binary Crossentropy
- Metric: Accuracy

Training setup:

- Epochs: 10
- Batch size: 1
- Train-test split: 80-20

---

## Troubleshooting

<details>
<summary><strong>Issue: Data appears in a single column</strong></summary>

Cause: Wrong CSV delimiter.

Fix:

```python
pd.read_csv("redwinequality.csv", sep=';')
pd.read_csv("whitewinequality.csv", sep=';')
```

</details>

<details>
<summary><strong>Issue: "type" column not found</strong></summary>

Cause: Type labels not added before concatenation.

Fix:

```python
red['type'] = 1
white['type'] = 0
wines = pd.concat([red, white], ignore_index=True)
```

</details>

<details>
<summary><strong>Issue: TensorFlow or Keras import errors</strong></summary>

Reinstall dependencies:

```bash
pip install --upgrade tensorflow keras
```

</details>

---

## Next Improvements

- Add feature scaling before training.
- Add confusion matrix and classification report.
- Add model evaluation metrics on test set.
- Save trained model to disk and load for inference.
- Add a small prediction script for new samples.

---

## Status Checklist

- [x] Dataset loading fixed
- [x] Type labeling added
- [x] Visualization working
- [x] Model training completed
- [ ] Model export enabled
- [ ] Advanced evaluation added

---

Built as a beginner-friendly deep learning classification project on wine data.
