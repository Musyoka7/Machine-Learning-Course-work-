# Triple-MNIST Multi-Label Classification

A comprehensive machine learning project demonstrating **problem diagnosis**, **model development**, and **architectural innovation** to solve a deliberately challenging image classification task.

## 🎯 The Challenge

The Triple-MNIST dataset contains **84×84 grayscale images with 3 handwritten digits** per image. The twist: **zero label overlap** exists between training, validation, and test sets.

| Split | Images | Unique Labels | Overlap with Training |
|-------|--------|---------------|----------------------|
| Train | 64,000 | 640 | — |
| Validation | 16,000 | 160 | **0%** |
| Test | 20,000 | 200 | **0%** |

This means a model trained to recognise "797" will never see that combination in validation or test. Traditional classification approaches **cannot work**.

## 📊 Results Summary

| Approach | Test Accuracy | F1 Score | Key Insight |
|----------|---------------|----------|-------------|
| Logistic Regression | 0.00% | 0.00 | Cannot generalise to unseen combinations |
| Baseline CNN | 0.00% | 0.00 | Same architectural limitation |
| CNN + Dropout | 0.00% | 0.00 | Regularisation doesn't solve the core problem |
| CNN + Augmentation | 0.00% | 0.00 | Augmentation corrupts 3-digit spatial structure |
| **Digit-Splitting CNN** | **97.60%** | **0.9853** | ✅ Compositional generalisation |
| Multi-Output CNN | 90.50% | 0.9412 | Multi-task learning approach |
| GAN Augmentation | Failed | — | Mode collapse; documented as negative result |

## 💡 Key Technical Achievements

### 1. Problem Diagnosis
- Identified that 0% validation accuracy from epoch 1 indicates an **architectural constraint**, not overfitting
- Recognised this as a **compositional generalisation** problem requiring structural redesign

### 2. Digit-Splitting Solution (97.60% accuracy)
- Split 84×84 images into three 28×28 digit regions
- Trained single-digit classifier (10 classes instead of 640)
- Achieved **19,200 training samples per class** vs 100 for full-image approach
- Model generalises to **any** 3-digit combination, including unseen ones

### 3. Multi-Output Architecture (90.50% accuracy)
- Single CNN with **3 parallel output heads**
- Shared feature extraction with task-specific classification
- Demonstrated multi-task learning principles (Caruana, 1997)

### 4. GAN Experimentation
- Implemented DCGAN for synthetic data generation
- Documented training instability and mode collapse
- Valuable negative result showing limits of brute-force augmentation

## 🛠️ Technical Stack

- **Deep Learning:** TensorFlow/Keras, CNN architectures, GANs
- **Machine Learning:** Scikit-learn, Logistic Regression, hyperparameter tuning
- **Data Science:** NumPy, Pandas, Matplotlib, Seaborn
- **Evaluation:** Accuracy, F1 Score, Confusion Matrices, Training Curves
- **Environment:** Python 3.13, Jupyter Notebooks

## 📁 Repository Structure

```
├── notebooks/
│   └── Code.ipynb                    # Complete implementation (all 5 tasks)
├── data/
│   └── triple_mnist/                 # Dataset (train/val/test splits)
├── Machine Learning report - final.pdf  # Full written analysis
├── ML-Assignment-2025.pdf            # Assignment specification
├── requirements.txt                  # Python dependencies
└── README.md
```

## 🚀 Quick Start

```bash
# Clone and setup
git clone <repo-url>
cd "Machine Learning Course work"
python -m venv .venv
source .venv/bin/activate  # Windows: .venv\Scripts\activate
pip install -r requirements.txt

# Run notebook
jupyter notebook notebooks/Code.ipynb
```

## 📈 Skills Demonstrated

| Skill | Evidence |
|-------|----------|
| **Problem Analysis** | Diagnosed zero-overlap as architectural issue, not training issue |
| **Model Development** | Logistic Regression, CNNs, Multi-output networks, GANs |
| **Experiment Design** | Systematic comparison of 6+ approaches with controlled variables |
| **Technical Writing** | Comprehensive report explaining methodology and results |
| **Critical Thinking** | Recognised when to pivot approach vs optimise existing solution |
| **Debugging ML Models** | Analysed training curves, identified mode collapse in GANs |

## 📝 Key Learnings

1. **Architecture matters more than hyperparameters** when facing fundamental data constraints
2. **Compositional generalisation** enables models to handle novel combinations of known components
3. **Negative results are valuable** — the GAN failure informed the architectural solution
4. **Understanding the problem** often leads to simpler, more effective solutions than brute-force approaches

## 👤 Author

**Alex Musyoka**  
University of Hull — Machine Learning Module (662086)

## 🙏 Acknowledgements

- Prof. Adil Khan (Module Leader)
- University of Hull, Department of Computer Science
