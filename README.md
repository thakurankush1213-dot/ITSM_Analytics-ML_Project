# ABC Technologies — ITSM Predictive Modeling & Analytics

## 📌 Project Overview

An end-to-end **Machine Learning and Time-Series Analytics project** developed for an IT Service Management (ITSM) use case.

The project uses approximately **46,000 historical incident records spanning 2012–2014** to develop predictive and analytical solutions aimed at improving incident prioritization, resource planning, automated ticket routing, change-risk identification, and resolution analysis.

The overall objective is to help transition IT operations from a **reactive support model toward a proactive, data-driven ITSM framework**.

> **Note:** The original client dataset and confidential credentials are not included in this repository.

---

# 🎯 Business Objectives

The project addresses four major ITSM objectives:

### Objective 1 — High Priority Incident Prediction
Predict Priority 1 and Priority 2 incidents so that critical tickets can be identified early and preventive action can be taken.

### Objective 2 — Incident Volume Forecasting
Forecast future incident volumes to support workforce planning, capacity management, budgeting, and operational readiness.

### Objective 3 — Ticket Categorization & Automated Routing
Automate ticket categorization and support-group assignment to reduce manual triage and routing delays.

### Objective 4 — Change Risk & Resolution Analysis
Identify incidents likely to require change-management intervention and analyze resolution categories to understand recurring operational issues.

---

# 🔧 Data Preprocessing & Feature Engineering

A dedicated preprocessing pipeline was developed to improve data quality and prepare the ITSM records for machine learning.

Key steps included:

- Standardization of textual placeholders such as `NA` and `NS`
- Conversion of incident timestamps into datetime format
- Engineering of operational time-based features
- Calculation of `Handle_Time_hrs`
- Removal of invalid records with negative durations
- Conversion of operational counters into appropriate numeric types
- Missing-value analysis and treatment
- Categorical feature encoding
- Frequency encoding of high-cardinality features
- Train-test data preparation
- Separate temporal data preparation for forecasting

A dedicated forecasting dataset was preserved before categorical transformations to maintain chronological integrity.

---

# 🤖 Objective 1 — High Priority Incident Prediction

## Business Goal

Predict whether an incident belongs to **Priority 1 or Priority 2** so that critical incidents can be identified early.

### Models

- Random Forest
- XGBoost

### Key Findings

- Random Forest achieved approximately **79% recall** for High Priority incidents.
- XGBoost achieved approximately **88% accuracy** with a Macro F1 score of approximately **0.47**.
- Threshold optimization improved detection of rare High Priority incidents.
- Feature importance analysis identified **CI_Name, WBS, and CI_Subcat** as important predictors of incident priority.

### Business Impact

The model can support proactive identification of critical incidents at ticket creation time, allowing service teams to prioritize resources and reduce the risk of SLA breaches.

---

# 📈 Objective 2 — Incident Volume Forecasting

## Business Goal

Forecast future incident volumes to support workforce planning and operational capacity management.

### Approach

Historical incidents were aggregated at:

- Monthly level
- Quarterly level
- Yearly level

Time-series forecasting techniques were evaluated to identify future workload patterns.

### Key Findings

- Historical incident volumes showed clear operational trends.
- Monthly forecasting provided the strongest predictive performance.
- Forecasting provides visibility into expected future workload.

### Model Comparison

| Model | MAE | RMSE |
|---|---:|---:|
| Exponential Smoothing | 462.61 | 542.16 |
| SARIMA | 291.71 | 324.03 |

**SARIMA** demonstrated better forecasting performance based on both MAE and RMSE.

### Business Impact

Forecasts can support proactive:

- Staffing decisions
- Resource allocation
- Capacity planning
- Budgeting
- Operational risk management

---

# 🗂️ Objective 3 — Ticket Categorization & Automated Routing

This objective focuses on reducing manual triage and automatically routing incidents to the appropriate category and support group.

## 3A — Category Assignment

### Model

**Random Forest**

### Configuration

- 300 estimators
- Optimized node-splitting constraints
- Threshold optimization

### Performance

| Metric | Result |
|---|---:|
| Accuracy | **97.2%** |
| Macro ROC-AUC | **0.9976** |

### Key Findings

The model demonstrated strong performance across incident categories, including dominant categories such as `application` and `subapplication`.

### Business Impact

Automated category assignment can reduce manual triage effort and accelerate the initial processing of incoming incidents.

---

## 3B — Support Group Assignment

### Model

**XGBoost**

A tuned XGBoost classifier was developed using randomized hyperparameter optimization.

### Key Findings

Threshold optimization improved support-group assignment performance.

Feature importance analysis showed:

| Feature | Importance |
|---|---:|
| CI_Name | **85.17%** |
| WBS | **9.20%** |

Configuration-item information was the dominant routing signal.

### Business Impact

Automated group assignment can:

- Reduce ticket reassignment
- Minimize routing delays
- Improve first-time assignment
- Accelerate incident resolution

---

# ⚠️ Objective 4 — Change Risk & Resolution Analysis

This objective focuses on understanding change-related incidents and resolution patterns.

## 4A — Change Request Trigger Prediction

### Business Goal

Identify incidents that are likely to require formal change-management intervention.

### Key Findings

Change-related incidents showed strong relationships with operational attributes including:

- Priority
- Urgency
- Reassignment counts
- Related interactions
- Configuration Item information

### Business Impact

The predictive approach can help identify potential change-management requirements earlier and support proactive risk assessment.

---

## 4B — Resolution Root Cause Classification

### Business Goal

Predict resolution categories and identify recurring operational failure patterns.

### Key Findings

- Random Forest provided stronger recall for rare but operationally important categories.
- XGBoost provided higher overall accuracy but showed limitations on certain minority classes.
- Model comparison demonstrated the trade-off between overall performance and minority-class detection.

### Business Impact

Resolution classification can provide deeper visibility into recurring incidents and help identify areas for targeted process improvement.

---

# 📊 Project Summary

| Objective | Primary Approach | Key Outcome |
|---|---|---|
| **1. Priority Prediction** | Random Forest / XGBoost | Proactive identification of critical incidents |
| **2. Incident Forecasting** | Exponential Smoothing / SARIMA | Improved workload and capacity planning |
| **3A. Category Assignment** | Random Forest | 97.2% Accuracy, 0.9976 Macro ROC-AUC |
| **3B. Group Assignment** | XGBoost | Routing driven primarily by CI_Name and WBS |
| **4A. Change Trigger Prediction** | Classification Models | Early identification of potential change requirements |
| **4B. Resolution Analysis** | Random Forest / XGBoost | Improved understanding of resolution patterns |

---

# 🧠 Key Technical Concepts

This project demonstrates practical application of:

- Exploratory Data Analysis
- Data Cleaning
- Feature Engineering
- Categorical Encoding
- Frequency Encoding
- Imbalanced Classification
- Random Forest
- XGBoost
- Hyperparameter Optimization
- Probability Threshold Optimization
- Confusion Matrix Analysis
- ROC-AUC
- Precision, Recall & F1-score
- Time-Series Analysis
- Exponential Smoothing
- SARIMA
- Feature Importance
- Business-oriented Model Evaluation

---

# 🛠️ Technology Stack

| Category | Technologies |
|---|---|
| Programming | Python, SQL |
| Data Processing | Pandas, NumPy |
| Visualization | Matplotlib, Seaborn |
| Machine Learning | Scikit-learn, XGBoost |
| Time-Series | Statsmodels |
| Database | MySQL |
| Development | Jupyter Notebook |
| Version Control | Git, GitHub |

---

# 📁 Project Structure

```text
ITSM-ML-Project/
│
├── ITSM_Project.ipynb
├── README.md
├── requirements.txt
└── .gitignore
```

---

# 🔐 Data Privacy

This repository does **not** contain:

- Original client dataset
- Database passwords
- Database credentials
- Connection strings
- Confidential client information

The repository focuses on the analytical methodology, machine learning workflow, model evaluation, and project outcomes.

---

# 💡 Key Business Insight

Across multiple ITSM objectives, configuration-management attributes such as **CI_Name, WBS, CI_Subcat, and related asset information** consistently emerged as important predictive features.

This highlights the importance of maintaining accurate and reliable **Configuration Management Database (CMDB)** information.

High-quality configuration and asset data can significantly improve predictive prioritization, automated routing, change-risk analysis, and operational decision-making.

---

# 🚀 Overall Outcome

The project demonstrates how Machine Learning and Time-Series Forecasting can be applied across multiple stages of the ITSM lifecycle.

The developed solutions provide a foundation for:

- Proactive incident prioritization
- Workload forecasting
- Automated ticket categorization
- Intelligent support-group routing
- Change-risk identification
- Resolution-pattern analysis

Together, these capabilities can help organizations move from **reactive incident management toward a proactive, intelligence-driven ITSM ecosystem**.

---

## 👤 Author

**Ankush Thakur**  
Aspiring Data Scientist & AI Engineer  
Bengaluru, India

GitHub: **thakurankush1213-dot**