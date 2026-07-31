# Bank Marketing Term Deposit Subscription Prediction using Logistic Regression

## 1. Background

Direct marketing campaigns remain a critical channel for retail financial institutions to acquire new customers and promote term deposit products. However, blanket cold-calling campaigns are costly, resource-intensive, and often result in low response rates and customer fatigue. By evaluating customer demographic profiles, financial indicators, and past interaction histories, financial institutions can leverage predictive modeling to target high-propensity clients, optimize resource allocation, and improve conversion rates.

---

## 2. Objectives

* **Predictive Modeling:** Build a binary Logistic Regression model to predict whether a customer will subscribe to a term deposit (`subscribed` = `yes` or `no`).
* **Feature Interpretation:** Identify key drivers (demographic, financial, and campaign interaction indicators) that positively or negatively influence a client's subscription likelihood.
* **Strategic Insights:** Provide actionable recommendations for optimizing marketing outreach strategies based on empirical evidence.

---

## 3. Dataset Description

The dataset comprises **45,211 records** and **14 variables** relating to direct marketing campaigns of a banking institution.

### Variable Breakdown

| Feature | Data Type | Role | Description |
| :--- | :--- | :--- | :--- |
| `subscribed` | Binary Categorical | Target Variable | Has the client subscribed to a term deposit? (`yes`, `no`) |
| `age` | Numerical (Integer) | Feature | Age of the client |
| `job` | Nominal Categorical | Feature | Type of job (e.g., `management`, `blue-collar`, `technician`) |
| `marital` | Nominal Categorical | Feature | Marital status (`married`, `single`, `divorced`) |
| `education` | Ordinal Categorical | Feature | Level of education (`primary`, `secondary`, `tertiary`, `unknown`) |
| `default` | Binary Categorical | Feature | Has credit in default? (`yes`, `no`) |
| `balance` | Numerical (Integer) | Feature | Average yearly balance (in Euros) |
| `housing` | Binary Categorical | Feature | Has a housing loan? (`yes`, `no`) |
| `loan` | Binary Categorical | Feature | Has a personal loan? (`yes`, `no`) |
| `contact` | Nominal Categorical | Feature | Contact communication type (`cellular`, `telephone`, `unknown`) |
| `duration` | Numerical (Integer) | Feature | Last contact duration in seconds |
| `pdays` | Numerical (Integer) | Feature | Days passed after previous campaign contact (`-1` means not previously contacted) |
| `previous` | Numerical (Integer) | Feature | Number of contacts performed before this campaign |
| `poutcome` | Nominal Categorical | Feature | Outcome of the previous marketing campaign (`unknown`, `other`, `failure`, `success`) |

---

## 4. Data Analysis

The binary classification model uses an end-to-end Machine Learning pipeline featuring:
1. **Target Encoding:** Binary conversion (1 for `yes`, 0 for `no`).
2. **Preprocessing:** Standard scaling for numerical variables and One-Hot Encoding (with baseline drop) for categorical variables.
3. **Model Evaluation:** Stratified 80-20 train-test split evaluated via **AUC-ROC**, Precision, Recall, and Confusion Matrix.

### Model Performance Metrics

* **ROC-AUC Score:** `0.8863` (Strong discriminatory ability between subscribers and non-subscribers).
* **Overall Accuracy:** `90.0%`
* **Confusion Matrix:**
  * **True Negatives (TN):** 7,800
  * **False Positives (FP):** 185
  * **False Negatives (FN):** 729
  * **True Positives (TP):** 329

### Top Feature Drivers (Odds Ratio & Coefficients)

| Feature | Coefficient ($\beta$) | Odds Ratio ($e^\beta$) | Interpretation |
| :--- | :---: | :---: | :--- |
| **`poutcome_success`** | $+2.3510$ | $10.496$ | Clients who subscribed in previous campaigns are **~10.5x** more likely to subscribe again. |
| **`duration`** | $+1.0538$ | $2.868$ | Longer conversation length significantly increases subscription probability. |
| **`job_student`** | $+0.4993$ | $1.647$ | Students display higher baseline conversion likelihood. |
| **`job_retired`** | $+0.4223$ | $1.525$ | Retirees show a strong positive tendency to subscribe. |
| **`housing_yes`** | $-0.7554$ | $0.470$ | Having an active housing loan decreases subscription likelihood by **~53%**. |
| **`contact_unknown`** | $-1.1358$ | $0.321$ | Unknown contact channels severely hinder campaign conversion. |

---

## 5. Conclusion & Recommendations

### Key Findings
1. **Previous Success is the Strongest Predictor:** Success in prior campaigns (`poutcome_success`) is by far the strongest indicator ($\beta = 2.3510$), increasing subscription odds by over tenfold.
2. **Engagement Duration Matters:** Longer phone calls strongly correlate with successful conversions ($\beta = 1.0538$).
3. **Financial Liabilities Limit Participation:** Clients with active housing loans ($\beta = -0.7554$) or personal loans ($\beta = -0.5646$) are substantially less likely to lock up funds in term deposits.
4. **Demographic Targets:** Students and retired individuals demonstrate higher propensity towards term deposit products compared to other occupational groups.

### Strategic Recommendations
* **Prioritize High-Propensity Segment Leads:** Re-engage clients who participated successfully in past campaigns before pursuing uncontacted leads.
* **Filter Out High-Debt Prospects:** Filter marketing lists to deprioritize clients carrying existing housing or personal loans.
* **Improve Call Quality and Engagement:** Train representatives on qualitative engagement tactics to maintain longer, higher-value interactions with potential clients.
* **Target Specific Demographics:** Tailor deposit offerings and messaging specifically to students and retirees seeking lower-risk savings instruments.
