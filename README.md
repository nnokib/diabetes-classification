# diabetes-classification
# Clinical Diabetes Classification: Logistic Regression vs. Decision Tree

> A supervised binary classification study on 768 clinical patient records, comparing **Logistic Regression** and **Decision Tree** classifiers with stratified evaluation, feature scaling, and ROC-AUC diagnostics.

---

### 1. Objective
To evaluate and compare interpretable classification models (**Logistic Regression** vs. **Decision Tree**) for predicting diabetes status from routine clinical and demographic measurements, while auditing real-world medical data quality limitations.

### 2. Data Source
* **Dataset:** Clinical Diabetes Survey Dataset (`768` patient records, `8` clinical/demographic predictors, `1` binary target)
* **Target Balance (`Outcome`):**
  * `0` (Non-diabetic): **500** patients (`65.1%`)
  * `1` (Diabetic): **268** patients (`34.9%`)
* **Predictors:** `Pregnancies`, `Glucose`, `BloodPressure`, `SkinThickness`, `Insulin`, `BMI`, `DiabetesPedigreeFunction`, `Age`
* **Data Quality Audit:** Identified physiologically implausible `0` values acting as missing-data placeholders—most notably in `Insulin` (`374` zeros, ~48%) and `SkinThickness` (`227` zeros, ~30%), plus `BloodPressure` (`35`), `BMI` (`11`), and `Glucose` (`5`).

### 3. Tools & Libraries
* **Language:** `Python` (Jupyter Notebook)
* **Data & Visualization:** `pandas`, `NumPy`, `seaborn`, `matplotlib`
* **Machine Learning:** `scikit-learn` (`train_test_split`, `StandardScaler`, `LogisticRegression`, `DecisionTreeClassifier`, `roc_auc_score`, `RocCurveDisplay`)

### 4. Methodology
* **Exploratory Data Analysis:** Analyzed univariate distributions (KDE histograms), bivariate relationships (`Glucose` vs. `BMI` with regression fit), and a Pearson correlation heatmap.
* **Train/Test Split:** Applied a **stratified 70/30 split** (`537` train / `231` test) to preserve the 65/35 class ratio.
* **Leakage-Free Preprocessing:** Fitted `StandardScaler` strictly on the training set and transformed the test set using training parameters.
* **Modelling & Evaluation:** Trained Logistic Regression (`max_iter=1000`) and a Decision Tree classifier, benchmarking both via Confusion Matrix, Accuracy, Precision, Recall, F1-Score, and ROC-AUC.

### 5. Model Performance (Test Set, *n* = 231)

| Model | Accuracy | Precision (Diabetic) | Recall (Diabetic) | F1-Score (Diabetic) | ROC-AUC |
| :--- | :---: | :---: | :---: | :---: | :---: |
| **Logistic Regression** | **77.5%** | **0.74** | 0.56 | **0.63** | **0.87** |
| **Decision Tree** | 70.1% | 0.57 | **0.58** | 0.58 | — |

### 6. Key Insights & Limitations
* **Linear Signal Outperforms Tree Complexity:** **Logistic Regression** achieved higher accuracy (**77.5%** vs. **70.1%**) and strong class discrimination (**ROC-AUC = 0.87**), while generating far fewer false positives (**16 FP** vs. **35 FP** for the Decision Tree).
* **Primary Clinical Predictors:** `Glucose` showed the strongest linear correlation with diabetes (`r ≈ 0.47`), followed by `BMI` (`r ≈ 0.29`), `Age` (`r ≈ 0.24`), and `Pregnancies` (`r ≈ 0.22`).
* **Next Steps:** Future iterations should impute missing-like zeros (e.g., median/KNN imputation) and apply threshold tuning or class-weighting to improve diabetic recall for clinical screening use cases.

### Repository Structure
```text
├── diabetes_classification.ipynb              # EDA, scaling, modelling & ROC-AUC evaluation
├── Clinical_Diabetes_Classification_Report.pdf # Full analytical write-up & critical discussion
└── README.md
