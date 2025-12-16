# Lead-Scoring-Case-Study

## 📌 Project Overview
X Education, an online course provider, suffers from a low lead conversion rate. Although they acquire a high number of leads, only about **30%** convert into paying customers. To improve efficiency, the company aims to identify the "hot leads" (most likely to convert) so the sales team can focus their efforts on them.

**The Goal:** Build a Logistic Regression model to assign a **Lead Score (between 0 and 100)** to each lead. The target is to help the company achieve a lead conversion rate of **80%**.

## 📂 Dataset
The dataset consists of leads acquired by X Education. It includes various attributes such as:
* **Lead Source:** (Google, Direct Traffic, Olark Chat, etc.)
* **Total Time Spent on Website**
* **Total Visits**
* **Last Activity**
* **Demographics:** (City, Country, Occupation)

## 🛠️ Tech Stack
* **Language:** Python 3
* **Libraries:** Pandas, NumPy, Matplotlib, Seaborn, Sklearn, Statsmodels
* **Environment:** Jupyter Notebook

## ⚙️ Project Workflow

### 1. Data Cleaning & Preparation
* **Handling Non-Standard Nulls:** Identified that the value 'Select' in categorical columns was equivalent to a null value and replaced it with `NaN`.
* **Missing Value Imputation:** Imputed missing values in `Lead Source`, `Country`, and `Occupation` with the mode (most frequent value).
* **Dropping Columns:** Removed columns with >30% missing data (e.g., `Tags`, `Lead Quality`) and irrelevant columns (e.g., `Do Not Call`).
* **Outlier Treatment:** Capped outliers in `TotalVisits` and `Page Views Per Visit` to the 99th percentile to prevent model skew.

### 2. Exploratory Data Analysis (EDA)
* Analyzed the correlation between time spent on the website and conversion rates.
* Identified high-performing lead sources (e.g., "Welingak Website") and occupations ("Working Professionals").

### 3. Model Building
* **Preprocessing:** Created dummy variables for categorical features and scaled numeric features using `MinMaxScaler`.
* **Feature Selection:** Used **Recursive Feature Elimination (RFE)** to select the top 15 features.
* **Refinement:** Manually removed features based on high **Variance Inflation Factor (VIF)** (to reduce multicollinearity) and high **P-values** (statistical significance).
* **Algorithm:** Logistic Regression (using `statsmodels` for detailed statistics and `sklearn` for prediction).

### 4. Model Evaluation
* **Metrics:** Focused on **Sensitivity (Recall)** to ensure no potential hot leads were missed.
* **ROC Curve:** Achieved an AUC of ~0.88.
* **Optimal Cutoff:** Determined a threshold of **0.35** based on the intersection of Accuracy, Sensitivity, and Specificity.

## 📊 Model Performance

The model generalizes well on unseen data, showing consistent performance across Train and Test sets.

| Metric | Training Set | Test Set |
| :--- | :--- | :--- |
| **Accuracy** | 79.83% | 80.22% |
| **Sensitivity** | **82.80%** | **83.20%** |
| **Specificity** | 78.01% | 78.39% |

## 💡 Key Business Insights
The Logistic Regression model identified the following key drivers for lead conversion:

1.  **Time Matters:** `Total Time Spent on Website` is the strongest positive predictor. Leads who engage longer are more likely to buy.
2.  **Source Quality:** Leads from **"Welingak Website"** and **"Lead Add Form"** have a very high conversion probability.
3.  **Occupation:** **"Working Professionals"** are far more likely to convert than unemployed leads or students.
4.  **Negative Signals:** Leads who select **"Do Not Email"** or originate from certain lower-intent sources are unlikely to convert.
