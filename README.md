# 🧠 Missing Indicator Imputation  
**📄 AI-Generated README (Custom Prompt for Clarity & Learning)**  

---

## 📌 Overview  
This project demonstrates the use of **Missing Indicator Imputation** — a method that not only fills missing values but also **adds an indicator column** showing where data was missing.  
This helps models learn if missingness itself carries predictive information.  

---

## 🧰 Libraries Used  
- pandas  
- numpy  
- scikit-learn  
- matplotlib.pyplot  

---

## 📂 Dataset Used  
**Titanic Dataset** — available in the repository.  

---

## ⚙️ Steps and Implementation  

### 🔹 Step 1: Simple Imputation (Baseline)
- Selected **`Age`** and **`Fare`** columns.  
- Performed a **train-test split**.  
- Used **SimpleImputer** from `sklearn` to fill missing values.  
- Trained a **Logistic Regression** model.  
- **Accuracy:** `61%`

---

### 🔹 Step 2: Adding Missing Indicator Column
- Used **MissingIndicator** to create a binary array (True/False) for missing values.  
- Added this array as a **new feature** to the dataset.  
- Again used **SimpleImputer** for numerical values.  
- Trained Logistic Regression on the updated dataset.  
- **Accuracy:** `63%`  
  ✅ Small improvement due to the model now learning where data was missing.  

---

### 🔹 Step 3: Simplified Method with `add_indicator=True`
- Instead of manually adding the indicator column, used:  
  ```python
  SimpleImputer(strategy='mean', add_indicator=True)



This automatically creates and attaches the indicator column.

Model accuracy remained the same (63%).

### 🔹 Step 4: Full Pipeline Implementation

Used additional Titanic features for a more robust pipeline.

Features Used:
Pclass, Sex, Age, SibSp, Parch, Fare, Embarked

### 🧱 Pipeline Components:

Numerical Pipeline:

SimpleImputer(strategy='median')

StandardScaler()

Categorical Pipeline:

SimpleImputer(strategy='most_frequent')

OneHotEncoder(handle_unknown='ignore')

ColumnTransformer:
Combined both pipelines (numerical + categorical).

Main Pipeline:
Included the column transformer and Logistic Regression model.

### 🔹 Step 5: Hyperparameter Tuning with Grid Search

Used GridSearchCV to test different imputation strategies.

Parameter Grid:

{
  'preprocessor__num__imputer__strategy': ['mean', 'median'],
  'preprocessor__cat__imputer__strategy': ['most_frequent', 'constant']
}


Results:

Best Cross-Validation Score: 0.78

Best Parameters:

Numerical Imputer → mean

Categorical Imputer → most_frequent

### 📊 Observations
Approach	Accuracy	Remarks
Simple Imputer Only	0.61	Baseline
+ Missing Indicator	0.63	Improved learning
Pipeline with Grid Search	0.78 (CV)	Optimized

Missing indicators improve performance by letting models recognize data patterns where missingness matters.

Pipelines and grid search streamline the process and help find optimal imputation strategies.

📄 This README was AI-generated using a custom prompt for educational clarity and documentation consistency.
