# 🌲 Forest Cover Type Prediction
### Capstone Project — M.S. in Artificial Intelligence

> **Classifying forest cover types across the Roosevelt National Forest using machine learning, ensemble methods, and advanced feature engineering.**

---

## 👤 Author
**Schoheib Bafaiz**  
M.S. Artificial Intelligence | [LinkedIn](https://www.linkedin.com/in/YOUR-LINKEDIN) | [GitHub](https://github.com/YOUR-USERNAME)

---

## 📌 Project Overview

This capstone project tackles a real-world ecological classification problem: predicting the type of forest cover for 30m x 30m patches of land in the Roosevelt National Forest of northern Colorado, using only cartographic and terrain-based features — no satellite imagery, no direct observation.

The dataset originates from a classic Kaggle competition and contains over **580,000 observations** across **7 forest cover types**, including Spruce/Fir, Lodgepole Pine, Ponderosa Pine, and Krummholz.

---

## 🎯 Objective

Build a robust, reproducible machine learning pipeline that:
- Performs in-depth **Exploratory Data Analysis (EDA)**
- Engineers new features from domain knowledge
- Trains and compares multiple classification models
- Optimizes model performance through **hyperparameter tuning**
- Leverages **ensemble methods** for maximum accuracy

---

## 🗂️ Dataset

| Split | Observations | Features |
|-------|-------------|----------|
| Train | 15,120 | 55 + target |
| Test  | 565,892 | 55 |

**Key Features:**
- Elevation, Aspect, Slope
- Horizontal & Vertical Distance to Hydrology
- Horizontal Distance to Roadways & Fire Points
- Hillshade at 9am, Noon, 3pm
- 4 Wilderness Area binary columns
- 40 Soil Type binary columns

**Target — 7 Forest Cover Types:**
1. Spruce/Fir
2. Lodgepole Pine
3. Ponderosa Pine
4. Cottonwood/Willow
5. Aspen
6. Douglas-fir
7. Krummholz

---

## 🔍 Exploratory Data Analysis

- **Scatter plots** of Elevation vs. Aspect and Elevation vs. Slope revealed distinct clustering by cover type
- **K-Means Clustering** (k=8) applied to terrain features to identify natural geographic groupings
- **3D interactive visualizations** (Plotly) showing Cluster and Cover Type distributions
- **Heatmaps** of Aspect vs. Elevation density
- **Pairwise plots** across key terrain features
- **Feature importance analysis** using Random Forest to rank predictors

> Key insight: **Elevation** was the single most important predictor, followed by distance to roadways and hydrology features.

---

## ⚙️ Feature Engineering

Three new features were engineered to capture terrain complexity:

| Feature | Formula | Rationale |
|---------|---------|-----------|
| `Hydrology_Distance` | √(H² + V²) | Euclidean distance to nearest water source |
| `Elevation_Slope_Interaction` | Elevation × Slope | Captures rugged terrain complexity |
| `Hillshade_Difference` | Hillshade_3pm − Hillshade_9am | Sun exposure change throughout the day |

---

## 🤖 Models Trained

### Baseline Models

| Model | Accuracy |
|-------|----------|
| **XGBoost** | **86.9%** |
| Random Forest | 86.3% |
| SVM (RBF Kernel) | 72.6% |
| Logistic Regression | 69.2% |

### After PCA (95% variance retained, 42 components)

| Model | Accuracy |
|-------|----------|
| XGBoost (PCA) | 80.9% |
| Random Forest (PCA) | 80.6% |
| SVM (PCA) | 69.4% |
| Logistic Regression (PCA) | 67.2% |

### Ensemble Methods

| Method | Accuracy |
|--------|----------|
| **Voting Classifier** (RF + XGBoost, soft voting) | **86.7%** |
| Stacking Classifier (RF + XGBoost → Logistic Regression) | 86.2% |

---

## 🔧 Hyperparameter Tuning

Used **Randomized Search CV** for computational efficiency:

**Best Random Forest Parameters:**
- `n_estimators`: 300
- `max_depth`: None (full depth)
- `min_samples_split`: 2
- `min_samples_leaf`: 1

**Best XGBoost Parameters:**
- `n_estimators`: 200
- `learning_rate`: 0.2
- `max_depth`: 10
- `subsample`: 0.8
- `colsample_bytree`: 1.0

---

## 🛠️ Tech Stack

![Python](https://img.shields.io/badge/Python-3.12-blue?logo=python)
![scikit-learn](https://img.shields.io/badge/scikit--learn-ML-orange?logo=scikit-learn)
![XGBoost](https://img.shields.io/badge/XGBoost-Gradient%20Boosting-red)
![Pandas](https://img.shields.io/badge/Pandas-Data%20Analysis-150458?logo=pandas)
![Plotly](https://img.shields.io/badge/Plotly-Visualization-3F4F75?logo=plotly)
![Google Colab](https://img.shields.io/badge/Google%20Colab-Notebook-F9AB00?logo=googlecolab)

**Libraries:** `pandas` · `numpy` · `scikit-learn` · `xgboost` · `lightgbm` · `matplotlib` · `seaborn` · `plotly` · `scipy`

---

## 📊 Key Results & Takeaways

- 🏆 **Best Model:** XGBoost — **87% accuracy** on the validation set
- 📈 **Most Important Feature:** Elevation — confirming ecological theory that altitude drives vegetation zones
- 🔻 **PCA trade-off:** Reduced computational cost but dropped accuracy ~6%, not worth it for this dataset
- 🤝 **Ensemble methods** did not significantly outperform tuned individual models, suggesting XGBoost was already near its ceiling
- ✅ **Easiest to classify:** Ponderosa Pine & Douglas-fir (F1 > 0.95)
- ⚠️ **Hardest to classify:** Spruce/Fir & Lodgepole Pine — overlapping terrain profiles caused confusion

---

## 🚧 Challenges & Solutions

| Challenge | Solution |
|-----------|----------|
| High-dimensional data (55 features) increased training time | Applied PCA for dimensionality reduction experiments |
| Hyperparameter space too large for Grid Search | Used Randomized Search CV for efficient tuning |
| Class overlap between Spruce/Fir and Lodgepole Pine | Feature engineering + ensemble voting to reduce misclassification |

---

## 📁 Repository Structure

```
forest-cover-type-prediction/
│
├── Capstone_Project.ipynb   # Full notebook: EDA → Modeling → Results
├── README.md
└── data/                    # Dataset files (not included — see Kaggle link below)
    ├── train.csv
    ├── test.csv
    └── sampleSubmission.csv
```

---

## 📦 How to Run

```bash
# Clone the repo
git clone https://github.com/YOUR-USERNAME/forest-cover-type-prediction.git

# Install dependencies
pip install pandas numpy scikit-learn xgboost lightgbm matplotlib seaborn plotly scipy

# Open the notebook
jupyter notebook Capstone_Project.ipynb
```

> 💡 Alternatively, open directly in [Google Colab](https://colab.research.google.com/drive/1XFv00WdL57LlxllM3rz2pUufLauGwbRb)

---

## 📚 Data Source

[Kaggle — Forest Cover Type Prediction](https://www.kaggle.com/c/forest-cover-type-prediction)  
Study area: Roosevelt National Forest, Northern Colorado

---

## 🎓 Academic Context

**Program:** Master of Science in Artificial Intelligence  
**Project Type:** Capstone — Final Semester  
**Environment:** Google Colab (Python 3.12)

---

*Built with rigorous methodology, reproducibility, and a genuine passion for applied machine learning. — Schoheib Bafaiz 🌲*
