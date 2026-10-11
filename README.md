# Advanced CNNs and Transfer Learning

## Overview

This repository contains the implementation and experiment analysis for the Advanced CNNs and Transfer Learning ssignment. The experiments use a 10-class subset of the Oxford-IIIT Pet dataset to compare training from scratch, transfer learning, fine-tuning, data augmentation, and an alternative pretrained architecture.

## Dataset

The project uses a selected subset of 10 classes from the Oxford-IIIT Pet dataset:

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

The selected dataset contains 1,996 images, split into training, validation, and test sets:

- Training set: 1,397 images (70%)
- Validation set: 299 images (15%)
- Test set: 300 images (15%)

A leakage check was performed to confirm that the split indices are disjoint across the three sets.

The notebook uses `torchvision.datasets.OxfordIIITPet` and applies the preprocessing and data augmentation configurations described in each experiment.

## Experiments

| Experiment | Approach | Description |
|---|---|---|
| B1 | ResNet18 from scratch | Train ResNet18 without pretrained weights. |
| B2 | ResNet18 feature extraction | Use ImageNet pretrained weights, freeze the backbone, and train the classifier head. |
| B3 | ResNet18 progressive fine-tuning | Use pretrained weights and train `layer4` together with the classifier head. |
| B4a | Feature extraction without augmentation | Train the classifier head without training-time augmentation. |
| B4b | Feature extraction with augmentation | Apply image augmentation to training data while keeping evaluation preprocessing separate. |
| B5 | EfficientNet-B0 feature extraction | Use ImageNet pretrained weights, freeze the backbone, and train the classifier head. |

The notebook evaluates models using accuracy and Macro F1, compares training behavior, and examines misclassified test images.

## Repository Contents

Example structure:

```text
.
├── README.md
├── requirements.txt
├── <notebook-name>.ipynb
├── <report-name>.pdf
└── <training-metrics>.csv
```

Replace the placeholder filenames with the actual filenames in your repository. Include the report and metric log only if those files are part of the repository.

## Environment Setup

Use the Python version required by your notebook or course environment. PyTorch and Torchvision installation commands may differ depending on whether you use CPU or CUDA.

1. Clone the repository:

   ```bash
   git clone <your-repository-url>
   cd <repository-folder>
   ```

2. Create and activate a virtual environment (optional but recommended):

   ```bash
   python -m venv .venv
   ```

   On Windows:

   ```powershell
   .venv\Scripts\activate
   ```

   On macOS/Linux:

   ```bash
   source .venv/bin/activate
   ```

3. Install dependencies:

   ```bash
   pip install -r requirements.txt
   ```

4. Open the notebook in Jupyter Notebook, JupyterLab, or VS Code and run the cells in order.

### PyTorch and CUDA

Install a PyTorch build compatible with your system using the official selector:
https://pytorch.org/get-started/locally/

A CPU build is sufficient for execution, though training may take longer. For GPU execution, confirm that PyTorch supports your CUDA setup and that `torch.cuda.is_available()` returns `True`.

## Reproducibility Notes

- The experiments use random seed `42` as configured in the notebook.
- Keep the dataset subset and class-to-label mapping consistent across training, validation, testing, and error analysis.
- Apply training augmentation only to the training dataset. Validation and test data should use evaluation preprocessing.
- Verify the metrics in the report against the executed notebook outputs and raw training logs.
- Runtime and model performance may vary with hardware, package versions, and execution environment.

## Results

The report contains the consolidated B1–B5 metrics, training curves, misclassification analysis, and model recommendation. Keep the reported metrics consistent with the notebook outputs and metric logs.

## References

- Oxford-IIIT Pet Dataset: https://www.robots.ox.ac.uk/~vgg/data/pets/
- PyTorch documentation: https://pytorch.org/docs/stable/index.html
- Torchvision documentation: https://pytorch.org/vision/stable/index.html

## AI Use Disclosure

AI assistance was used for concept clarification, code debugging support, and improving the clarity and organization of explanations. Verify experiment results against the executed notebook and recorded metrics. Treat interpretations of model errors as hypotheses unless confirmed through dataset annotations or further testing.
