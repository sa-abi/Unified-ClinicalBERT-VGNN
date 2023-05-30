# Unified-ClinicalBERT-VGNN

This repository contains all the necessary scripts for training and preprocessing the data for a Variationally Regularized Graph Neural Network (VGNN) model[^1] with ClinicalBERT[^2] features integrated. It is designed to handle and process EHR, specifically the MIMIC-III dataset, and utilizes features extracted through ClinicalBERT as additional input for the VGNN.

## Repository Structure

Below is a brief overview of the main components of the repository:

```
Unified-ClinicalBERT-VGNN
├── model.py
├── train_combo.py
└── utils.py

preprocess
├── preprocess_GNN
│   └── preprocess_mimic.py
├── preprocess_BERT
│   ├── mk_X_BERT_matched.py
│   └── preprocess_NOTEEVENTS.py
└── get_cls.py

BERT
└── train_BERT.py

data
└── MIMIC-III data
```

## Files and Directories
- `Unified-ClinicalBERT-VGNN` : Folder containing training script for ClinicalBert and VGNN combo
- `model.py`: This file contains the main structure of the Graph Neural Network (GNN) model.
- `train_combo.py`: This script is used for training the GNN model.
- `utils.py`: This file contains utility functions used throughout the repository.
- `preprocess`: This directory should contain your preprocessing files for GNN and ClinicalBERT (MIMIC-III dataset).
- `get_cls.py`: A script for obtaining the [CLS] token as embeddings from the MIMIC data to be fed to the GNN model.
- `preprocess_GNN`: This directory contains script (`preprocess_mimic.py`) for preprocessing MIMIC-III data for GNN and creating mappings of labels for ClinicalBERT.
- `preprocess_BERT`: This directory contains scripts (`mk_X_BERT.py`, `mk_X_BERT_matched.py`, `preprocess_NOTEEVENTS.py`) for preprocessing data with ClinicalBERT.
- `BERT`: This directory contains script (`train_BERT.py`) which is used for fine-tuning training the ClinicalBERT model.
- `data`: This directory should contain your input data (MIMIC-III dataset).

## Usage

First, make sure you download your MIMIC-III data into the `data` directory. The scripts are designed to read from this location. Then, follow the sequence of steps below:

1. Run `preprocess_mimic.py` in `preprocess_GNN`, and `preprocess_NOTEEVENTS.py`, and `mk_X_BERT_matched.py` in `preprocess_BERT` to preprocess your MIMIC-III data.
2. Run `train_BERT.py` in `BERT` to finetune the ClinicalBERT for the same prediction task as the VGNN.
3. Run `get_cls.py` in `preprocess` to obtain the additional features generated by ClinicalBERT.
4. Run `train_combo.py` in `Unified-ClinicalBERT-VGNN` to train your ClinicalBERT + VGNN Combo model.

## Requirements

Please ensure you have the necessary dependencies installed. If not, install them with:
```
pip install -r requirements.txt
```

[^1]: This code was modified from the following repo https://github.com/NYUMedML/GNN_for_EHR/tree/master
[^2]: This code was modified from the following repo https://github.com/EmilyAlsentzer/clinicalBERT