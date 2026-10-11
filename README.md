# Advanced CNNs and Transfer Learning

## Overview

This repository contains the Jupyter Notebook, experiment logs, and report for the **Advanced CNNs and Transfer Learning** assignment. The project compares CNN training strategies for a 10-class image classification task using a selected subset of the Oxford-IIIT Pet dataset.

## Dataset

The notebook combines the official trainval and test portions of the Oxford-IIIT Pet dataset, selects the 10 classes listed below, and creates its own stratified train/validation/test split.

Selected classes:
- Abyssinian
- Bengal
- Birman
- Persian
- Siamese
- Beagle
- Boxer
- Chihuahua
- Pug
- Shiba Inu

The selected subset contains **1,996 images**:
- Training: **1,397 images**
- Validation: **299 images**
- Test: **300 images**

The notebook checks that the indices assigned to the three splits are disjoint. Because the notebook combines the official dataset splits and then creates a new split, the 300-image test set should be described as this project's internal test set, not the original official test split.

The dataset is loaded using `torchvision.datasets.OxfordIIITPet`. The notebook downloads the dataset when needed.

## Experiments

| Experiment | Model and strategy | Description |
|---|---|---|
| B1 | ResNet18 — training from scratch | Initializes ResNet18 without pretrained weights and trains the model for the selected classes. |
| B2 | ResNet18 — feature extraction | Uses ImageNet pretrained weights, freezes the backbone, and trains the classifier head. |
| B3 | ResNet18 — progressive fine-tuning | Uses ImageNet pretrained weights and fine-tunes the final ResNet block together with the classifier head. |
| B4a | ResNet18 — no augmentation | Feature-extraction baseline without training-time data augmentation. |
| B4b | ResNet18 — with augmentation | Uses training-time augmentation while validation and test images use evaluation preprocessing. |
| B5 | EfficientNet-B0 — architecture comparison | Uses ImageNet pretrained weights. Its training strategy is selected using the validation results of the reference experiments; the final feature block is unfrozen if B3 is selected, otherwise the backbone remains frozen and only the classifier is trained. |

The notebook evaluates the models using accuracy and Macro F1, compares validation performance, records training histories, and examines misclassified test images. Model selection is based on validation results; test metrics are for final evaluation.

## Repository Contents

This repository includes:
- notebook/GSLC_DL_S5.ipynb: notebook containing the implementation and experiments.
- logs/: experiment settings, training metrics, comparison results, and failure analysis.
- report/: assignment report in PDF format.
- requirements.txt: Python dependencies needed to run the notebook.

## Requirements and Setup

The main implementation is a Jupyter Notebook. The requirements.txt file lists the Python libraries used by the notebook.

1. Clone the repository:

   ```bash
   git clone <your-repository-url>
   cd <repository-folder>
   ```

2. (Optional) Create and activate a virtual environment:

   ```bash
   python -m venv .venv
   ```

   On Windows PowerShell:

   ```powershell
   .venv\Scripts\Activate.ps1
   ```

   On macOS/Linux:

   ```bash
   source .venv/bin/activate
   ```

3. Install dependencies:

   ```bash
   pip install -r requirements.txt
   ```

4. Open notebook/GSLC_DL_S5.ipynb in Jupyter Notebook, JupyterLab, or VS Code and run the cells in order.

### PyTorch and device support

Install a PyTorch and Torchvision build that matches the intended CPU or CUDA environment. Refer to the official installation selector: https://pytorch.org/get-started/locally/

The notebook selects the available device at runtime. Training may take longer on CPU than on a compatible GPU.

## Reproducibility and Logs

- The notebook sets random seed 42 for the main random-number generators.
- The selected classes and class-to-label mapping should remain consistent across all splits and the failure analysis.
- The split check verifies that train, validation, and test indices do not overlap.
- Data augmentation is intended for training data; validation and test data use evaluation preprocessing.
- logs/training_history.csv stores training-history information, while logs/raw_metrics.csv and logs/raw_metrics.json store experiment metrics.
- logs/experiment_settings.json records experiment settings.
- The B4 and B5 comparison files store their respective comparisons, and logs/failure_analysis.csv records the error-analysis results.
- Use the recorded notebook outputs and logs as the source of truth for the metrics reported in the PDF. Runtime and results may vary with hardware and library versions.

## Report

The report is located at:

report/Tugas05_2802541644_Angelina Jolie Candaya.pdf

It contains the written analysis and results for the assignment. The metrics and discussion should match the executed notebook and the files in logs/.

## References

- Oxford-IIIT Pet Dataset: https://www.robots.ox.ac.uk/~vgg/data/pets/
- PyTorch documentation: https://pytorch.org/docs/stable/index.html
- Torchvision documentation: https://pytorch.org/vision/stable/index.html

## AI Use Disclosure

AI assistance was used for concept clarification and improving the clarity and organization of explanations. Experiment results should be checked against the executed notebook and recorded logs. Explanations of possible causes of misclassification are treated as hypotheses unless supported by further verification.
