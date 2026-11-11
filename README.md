# Telco Churn Prediction and Retention Intelligence System

### Applied Data Mining (402333) — American University of Madaba (AUM)

---

## 👥 Team Information & Project Metadata

* **Institution:** American University of Madaba (AUM)
* **Faculty:** Faculty of Information Technology
* **Course:** Applied Data Mining (402333) — Fall Term 2026/2027
* **Project Deliverable:** Phase 1 Proposal (Idea, Problem Statement, and Setup)
* **Repository Link:** [https://github.com/HamzaShobaki/TelcoChurnPrediction](https://github.com/HamzaShobaki/TelcoChurnPrediction)

| Student Name | Student ID | Academic Email |
| :--- | :--- | :--- |
| **Hamza Shobaki** | 2410171 | *h.shobaki@aum.edu.jo* |
| **Samer Abuzeineh** | 2410385 | *s.abuzeineh@aum.edu.jo* |

---

## 📌 1. Project Proposal & Business Problem Formulation

In the telecommunications sector, intense competition and minimal switching barriers make customer churn a primary driver of recurring revenue loss. Acquiring a new telecom subscriber costs between **5 to 7 times more** than retaining an existing account. 

Conventional retention operations rely primarily on reactive win-back efforts initiated after a cancellation request is already submitted. By developing an automated early-warning predictive system using machine learning classification, telecom operators can identify attrition indicators weeks before contract termination.

### Target Users & Operational Context
* **Customer Retention Specialists & Call Center Agents:** Consume individual churn risk probability scores to offer targeted incentives (e.g., speed upgrades, contract discounts).
* **Marketing Campaign Managers:** Restructure vulnerable package offerings (e.g., month-to-month contracts and electronic check billing).

---

## 🎯 2. Research Question & Metric Justification

> **Quantifiable Research Question:**  
> *"Can a supervised machine learning classification pipeline accurately identify telecom subscribers at risk of churn, achieving a Macro-averaged F1-Score $\ge$ 0.75 and an actionable minority-class Churn Recall $\ge$ 0.80 across diverse customer tenure, contract type, and billing profiles while preventing data leakage?"*

### Metric Selection Rationale
With class imbalance (~26.5% churn prevalence), high **Churn Recall ($\ge$ 0.80)** is essential because the financial cost of a **False Negative** (losing an active account) far exceeds the small operational cost of a **False Positive** (offering a loyalty discount to a customer who planned to stay). A **Macro F1-Score ($\ge$ 0.75)** ensures equal performance across both retained and churned cohorts.

---

## 📊 3. Data Mining Task & Schema Architecture

* **Primary Task:** Supervised Binary Classification (`Churn`: Yes / No).
* **Dataset Benchmark:** IBM Telco Customer Churn dataset (7,043 subscriber records, 21 features).
* **Target Feature Distribution:**
  * **Class 1 (Churn = Yes):** 1,869 subscribers (26.54%)
  * **Class 0 (Churn = No):** 5,174 subscribers (73.46%)

### Dimensional Star Schema (Delta Lake)

| Table Name | Key Attributes & Features | Role in Data Warehouse |
| :--- | :--- | :--- |
| `dim_customer_profile` | `customerID` (PK), `gender`, `SeniorCitizen`, `Partner`, `Dependents` | Demographics Dimension |
| `dim_telecom_services` | `PhoneService`, `MultipleLines`, `InternetService`, `OnlineSecurity`, `OnlineBackup`, `DeviceProtection`, `TechSupport`, `StreamingTV`, `StreamingMovies` | Subscriptions Dimension |
| `dim_contract_billing` | `Contract`, `PaperlessBilling`, `PaymentMethod` | Billing & Contract Settings |
| `fact_customer_churn` | `tenure`, `MonthlyCharges`, `TotalCharges`, calculated charges-per-tenure ratio; **`Churn` (Target)** | Gold Fact Table (ML Ready) |

---

## 🛠️ 4. Technology Stack & Infrastructure

* **Compute & Distributed ETL:** Databricks Community Edition with PySpark 3.x and Apache Spark SQL.
* **Storage Layer:** Delta Lake (Parquet format) for ACID transactions, schema enforcement, and time-travel history.
* **Machine Learning Frameworks:** Python 3.10+, Scikit-Learn 1.3+ (Pipelines, Decision Trees), `imbalanced-learn` (SMOTE), and XGBoost.
* **Experiment Tracking & MLOps:** MLflow for hyperparameter logging and model metric tracking.

---

## 📂 5. Repository Directory Layout

```
TelcoChurnPrediction/
├── README.md                      # Executive repository documentation
├── requirements.txt               # Dependencies list
├── .gitignore                     # Git exclusion rules
├── data/                          # Data files & schemas
│   ├── raw/                       # IBM Telco raw dataset
│   └── delta_schema/              # Data warehouse tables
├── notebooks/                     # Project Jupyter / Databricks Notebooks
│   ├── Phase1_Stack_Setup.ipynb   # Environment verification & Spark setup
│   ├── Phase2_EDA_Cleaning.ipynb  # Preprocessing & Data Warehousing
│   └── Phase3_Model_Tuning.ipynb  # ML Training, SMOTE & Evaluation
└── reports/                       # Formal submission documents
    └── Phase_1_Project_Proposal.docx
```

---

## 🤖 6. AI Tools Disclosure

Generative AI assistance was utilized during Phase 1 solely for initial brainstorming and refining the mining stack setup and architecture recommendations. All selected tools and frameworks are provisional and may be adapted in subsequent project phases as implementation requirements evolve.

---

## 📚 7. Academic References

1. **Amin, A., Shah, B., Khattak, A. M., et al. (2017).** "Cross-company customer churn prediction in telecommunication: a data-driven approach." *Information Sciences*, 385, 320–337. DOI: [10.1016/j.ins.2017.01.003](https://doi.org/10.1016/j.ins.2017.01.003)
2. **Ahmad, A. K., Jafar, A., & Aljoumaa, D. (2019).** "Customer churn prediction in telecom using machine learning in big data platform." *Journal of Big Data*, 6(1), 28. DOI: [10.1186/s40537-019-0191-6](https://doi.org/10.1186/s40537-019-0191-6)
3. **Miguéis, V. L., Camanho, A. S., & Falcão, F. (2013).** "Customer churn in telecommunications: The role of service usage and social networks." *Expert Systems with Applications*, 40(5), 1803–1810. DOI: [10.1016/j.eswa.2012.09.023](https://doi.org/10.1016/j.eswa.2012.09.023)
4. **IBM Cognos Analytics (2018).** *Telco Customer Churn: Focused customer retention programs* [Data set]. Kaggle. [Link](https://www.kaggle.com/datasets/blastchar/telco-customer-churn)
