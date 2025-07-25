# AI Development Workflow Assignment Report  
**Course:** AI for Software Engineering  
**Student:** Kgololosego Moleba  
**Email:** kgolomoleba@gmail.com  

---

## Table of Contents  
- [Part 1: Short Answer Questions (30 points)](#part-1-short-answer-questions-30-points)  
- [Part 2: Case Study Application (40 points)](#part-2-case-study-application-40-points)  
- [Part 3: Critical Thinking (20 points)](#part-3-critical-thinking-20-points)  
- [Part 4: Reflection & Workflow Diagram (10 points)](#part-4-reflection--workflow-diagram-10-points)  
- [References](#references)  

---

## Part 1: Short Answer Questions (30 points)

### 1. Problem Definition (6 points)

**Hypothetical AI Problem:**  
Predicting student dropout rates in a university setting.

**Objectives:**  
- Identify students at high risk of dropping out early in the semester.  
- Enable early interventions through targeted counseling and academic support.  
- Improve overall student retention rates and academic performance.

**Stakeholders:**  
- University administration (decision-makers who allocate resources).  
- Students (who receive interventions and support services).

**Key Performance Indicator (KPI):**  
- Prediction accuracy of dropout risk — percentage of correctly identified at-risk students before dropout occurs.

---

### 2. Data Collection & Preprocessing (8 points)

**Data Sources:**  
- Academic records: grades, attendance logs, exam scores.  
- Demographic information: age, gender, socioeconomic background.

**Potential Bias:**  
- Socioeconomic bias: Students from low-income backgrounds might be underrepresented or disproportionately flagged due to systemic inequalities reflected in the data.

**Preprocessing Steps:**  
1. **Handling Missing Data:** Impute missing values using median for numerical data or mode for categorical data.  
2. **Normalization:** Scale numerical features (e.g., GPA, attendance rate) to a 0-1 range for uniformity.  
3. **Encoding Categorical Variables:** Apply one-hot encoding to categorical data such as program enrolled or ethnicity.

---

### 3. Model Development (8 points)

**Chosen Model:**  
Random Forest classifier.  
*Justification:* Effectively handles heterogeneous data types, reduces overfitting through ensemble averaging, and provides insights via feature importance.

**Data Splitting:**  
- Training Set: 70% of data, used for model fitting.  
- Validation Set: 15%, used for hyperparameter tuning.  
- Test Set: 15%, used for final model evaluation.

**Hyperparameters to Tune:**  
- `n_estimators` (number of trees): More trees improve accuracy but increase computation.  
- `max_depth` (tree depth limit): Controls model complexity to avoid overfitting.

---

### 4. Evaluation & Deployment (8 points)

**Evaluation Metrics:**  
- **Accuracy:** Overall proportion of correct predictions.  
- **F1-Score:** Harmonic mean of precision and recall, useful in cases with imbalanced classes.

**Concept Drift:**  
- The phenomenon where statistical properties of input data change over time, causing model performance degradation.  
- *Monitoring:* Continuously track model prediction performance metrics and retrain with new data when significant drift is detected.

**Deployment Challenge:**  
- Scalability: The system must handle prediction requests for thousands of students in real-time during the semester without latency.

---

## Part 2: Case Study Application (40 points)

**Scenario:** A hospital wants an AI system to predict patient readmission risk within 30 days of discharge.

---

### Problem Scope (5 points)

**Problem Definition:**  
Develop a predictive AI model to identify patients at high risk of readmission within 30 days after hospital discharge.

**Objectives:**  
- Reduce unnecessary readmissions to improve healthcare efficiency.  
- Optimize resource allocation for follow-up care.  
- Enhance patient health outcomes by early intervention.

**Stakeholders:**  
- Healthcare providers (doctors, nurses, case managers).  
- Hospital administrators and policy makers.

---

### Data Strategy (10 points)

**Data Sources:**  
- Electronic Health Records (EHRs): diagnoses, procedures, lab results, medication history.  
- Patient demographics: age, gender, socioeconomic status, lifestyle data.

**Ethical Concerns:**  
1. **Patient Privacy:** Strict adherence to HIPAA to protect sensitive patient information.  
2. **Bias:** Historical data might underrepresent minority groups, leading to unfair predictions.

**Preprocessing Pipeline:**  
- **Data Cleaning:** Remove duplicate entries and correct inconsistent values.  
- **Feature Engineering:** Create new features such as count of previous admissions, average length of stay, number of medications.  
- **Normalization & Encoding:** Scale numerical features; encode categorical data such as diagnosis codes with one-hot or label encoding.

---

### Model Development (10 points)

**Chosen Model:**  
XGBoost (Gradient Boosted Trees).  
*Justification:* High predictive accuracy on structured data, robustness to missing values, and capability to handle feature interactions.

**Hypothetical Confusion Matrix:**

| Actual \ Predicted | Readmitted | Not Readmitted |  
|--------------------|------------|----------------|  
| Readmitted         | 35 (TP)    | 5 (FN)         |  
| Not Readmitted     | 8 (FP)     | 52 (TN)        |  

**Calculations:**  
- **Precision:** 35 / (35 + 8) ≈ 0.81 (81%)  
- **Recall:** 35 / (35 + 5) = 0.875 (87.5%)

---

### Deployment (10 points)

**Integration Steps:**  
- Package the model as a RESTful API hosted on secure hospital infrastructure.  
- Integrate with hospital EHR systems for automatic prediction on discharged patients.  
- Setup alert systems for clinicians for high-risk patient follow-ups.

**Compliance with Regulations:**  
- Use HIPAA-compliant cloud or on-premises servers.  
- Data encryption at rest and in transit.  
- Role-based access control and detailed audit logging.

---

### Optimization (5 points)

**Method to Address Overfitting:**  
- Apply k-fold cross-validation during training to ensure model generalization.  
- Use regularization parameters (`lambda` and `alpha`) in XGBoost to penalize complexity.

---

## Part 3: Critical Thinking (20 points)

### Ethics & Bias (10 points)

**Effect of Biased Training Data:**  
- Biased data may cause the model to overpredict risk for certain populations, leading to unnecessary interventions or denial of care for others, exacerbating healthcare disparities.

**Mitigation Strategy:**  
- Employ fairness assessment tools like IBM AI Fairness 360 to detect bias metrics (e.g., disparate impact).  
- Implement reweighting or data augmentation to balance representation.

---

### Trade-offs (10 points)

**Model Interpretability vs Accuracy:**  
- Transparent models (e.g., logistic regression) enable clinician trust and understanding but may sacrifice some accuracy.  
- Complex models (e.g., ensembles or deep learning) improve accuracy but reduce explainability, potentially limiting clinical adoption.

**Impact of Limited Computational Resources:**  
- Constraints may necessitate simpler models with faster inference times, sacrificing predictive power for deployment feasibility.

---

## Part 4: Reflection & Workflow Diagram (10 points)

### Reflection (5 points)

**Most Challenging Part:**  
Balancing ethical considerations such as bias mitigation with the goal of high predictive accuracy, especially given sensitive healthcare data and limited representation.

**Improvements with More Resources:**  
Access to larger, diverse datasets and investment in explainability tools (e.g., SHAP values) would improve fairness and clinician trust.

---

### Workflow Diagram (5 points)

```mermaid
flowchart LR
  A[Problem Definition] --> B[Data Collection]
  B --> C[Data Preprocessing]
  C --> D[Model Development]
  D --> E[Model Evaluation]
  E --> F[Deployment]
  F --> G[Monitoring & Maintenance]
References
IBM AI Fairness 360 Toolkit: https://aif360.mybluemix.net/

Health Insurance Portability and Accountability Act (HIPAA): https://www.hhs.gov/hipaa/index.html

CRISP-DM Framework Documentation: https://www.datascience-pm.com/crisp-dm-2/

Chen, T., & Guestrin, C. (2016). XGBoost: A scalable tree boosting system. KDD.

Kaggle Breast Cancer Dataset: https://www.kaggle.com/datasets
