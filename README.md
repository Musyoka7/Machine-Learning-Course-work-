# Triple-MNIST Classification

A machine learning project comparing different approaches for multi-label image classification on the Triple-MNIST dataset.

## Problem Statement

The Triple-MNIST dataset extends the traditional MNIST dataset. Instead of single 28x28 digit images, it contains **84x84 grayscale images with 3 handwritten digits** per image. The goal is to predict the sequence of all three digits (e.g., "059", "348").

This transforms a simple 10-class problem into a much more complex multi-label classification challenge.

## Dataset

| Split | Images | Unique Labels |
|-------|--------|---------------|
| Train | 64,000 | 640 |
| Validation | 16,000 | 160 |
| Test | 20,000 | 200 |

**Key Challenge:** There is zero label overlap between train, validation, and test sets. Models must learn to generalize to unseen digit combinations.

## Project Structure

```
.
├── notebooks/
│   └── Code.ipynb          # Main Jupyter notebook with all implementations
├── data/
│   └── triple_mnist/       # Dataset (train/val/test splits)
├── ML-Assignment-2025.pdf  # Assignment specification
├── requirements.txt        # Python dependencies
└── README.md
```

## Tasks Overview

### Task 1: Data Exploration
- Visualize random samples from the dataset
- Analyze label distributions
- Identify how this differs from typical classification (zero label overlap)

### Task 2: Baseline Models
- **Logistic Regression** on flattened images (7,056 features)
- **Convolutional Neural Network (CNN)** on 2D images
- Hyperparameter tuning using validation set
- Evaluation with accuracy, F1 score, confusion matrix

### Task 3: Model Improvement
- Analyze training/validation loss curves for underfitting/overfitting
- Implement improvement techniques:
  - Increased model complexity
  - Data augmentation
  - Dropout layers
  - Regularization methods

### Task 4: Image Splitting Approach
- Split each 84x84 image into three 28x28 digit images
- Train CNN to predict single digits
- Concatenate predictions for final three-digit output

### Task 5: Advanced Techniques
- **(a)** Alternative CNN architecture for multi-label classification without splitting
- **(b)** GAN-based data augmentation using DCGAN to generate synthetic training images

## Technologies Used

- Python 3.13
- TensorFlow / Keras
- scikit-learn
- NumPy
- Matplotlib / Seaborn
- Jupyter Notebook

## Setup

1. Clone the repository
2. Create a virtual environment:
   ```bash
   python -m venv .venv
   source .venv/bin/activate  # On Windows: .venv\Scripts\activate
   ```
3. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```
4. Place the Triple-MNIST dataset in `data/triple_mnist/`
5. Open and run `notebooks/Code.ipynb`

## Key Findings

- **Baseline models achieve 0% validation accuracy** due to zero label overlap between splits
- This is a **zero-shot learning problem** - models must generalize to unseen label combinations
- The image-splitting approach (Task 4) enables generalization by predicting individual digits
- CNNs outperform Logistic Regression due to their ability to learn spatial features

## Author

Alex Musyoka

## Acknowledgments

- University of Hull - Machine Learning Module (662086)
- Prof. Adil Khan (Module Leader)
