# At-Risk Student Prediction

A machine learning project developed during the **Samsung Innovation Campus (SIC) – AI Program** to identify students at risk of failing before the examination period and highlight the factors associated with academic performance.

## Project Overview

Academic failure is often recognized only after it occurs. This project uses academic, behavioral, lifestyle, and wellbeing-related data to predict whether a student is likely to **Pass** or **Fail**, enabling earlier and more targeted support.

### Objectives

- Detect students who may be at risk before exam season.
- Identify the main factors associated with student failure.
- Compare multiple classification models using metrics suitable for imbalanced data.
- Provide actionable recommendations for educational institutions.

## Dataset

- **Source:** [Student Exam Performance and Success Dataset – Kaggle](https://www.kaggle.com/datasets/mobeenfatimah/student-exam-performance-and-success-dataset)
- **Records:** 100,000 students
- **Original columns:** 44
- **Predictor variables used:** 39
- **Features after one-hot encoding:** 62
- **Target:** `pass_status` (`Pass` / `Fail`)
- **Class distribution:**
  - Pass: 77.39%
  - Fail: 22.61%

> The dataset should be downloaded directly from Kaggle and is not included in this repository unless its license permits redistribution.

## Project Workflow

1. Data inspection and validation
2. Exploratory data analysis
3. Missing-value handling
4. Leakage prevention
5. Categorical feature encoding
6. Numerical feature scaling
7. Stratified train/test split
8. Model training and comparison
9. Final model evaluation
10. Interpretation and business recommendations

## Data Preprocessing

- Verified that the dataset contained no duplicate rows or duplicate student IDs.
- Used an 80/20 stratified train/test split.
- Imputed numerical features using the median.
- Imputed categorical features using the mode.
- Applied one-hot encoding to categorical variables.
- Maintained scaled and unscaled feature versions where appropriate.
- Removed leakage-related columns, including:
  - `student_id`
  - `questions_attempted`
  - `questions_correct`
  - `exam_score`
  - `performance_grade`
  - `performance_level`

## Models Evaluated

- Logistic Regression
- Decision Tree
- Random Forest
- Gradient Boosting
- XGBoost
- Soft-voting ensemble using Random Forest and XGBoost

## Model Performance

| Model | Accuracy | Fail Precision | Fail Recall | Fail F1-score |
|---|---:|---:|---:|---:|
| Tuned Logistic Regression | 79.64% | 53.22% | **82.15%** | 64.59% |
| Decision Tree | 77% | 49% | 79% | 61% |
| Random Forest | 79.50% | 53.14% | 78.88% | 63.50% |
| Gradient Boosting | 85.23% | 71.83% | 57.05% | 63.59% |
| Ensemble: RF + XGBoost | 84.63% | 66.13% | 65.59% | **65.90%** |

## Final Model

**Tuned Logistic Regression** was selected as the final model because the main goal was to identify as many at-risk students as possible. It achieved the highest recall for the `Fail` class.

### Final Results

- **Accuracy:** 79.64%
- **Fail precision:** 53.22%
- **Fail recall:** 82.15%
- **Fail F1-score:** 64.59%
- **ROC-AUC:** 0.89
- **PR-AUC:** 0.7202
- **Detected fail cases:** 3,715 out of 4,522

Although some alternative models achieved higher overall accuracy, Logistic Regression was more aligned with the project objective because missing a student who is genuinely at risk was considered more costly than incorrectly flagging a student for additional support.

## Key Findings

- Previous exam score and previous GPA were the strongest predictors of future exam performance.
- Exam preparation days, daily study hours, self-study hours, and completed practice tests were important predictors.
- Attendance and assignment completion provided useful indicators of academic engagement.
- Sleep quality, stress, and exam anxiety added relevant wellbeing information.
- Accuracy alone was not sufficient because the target classes were moderately imbalanced.

## Recommendations

Educational institutions could use the model as part of an early-warning system with three risk levels:

- **Low risk:** Regular academic support
- **Medium risk:** Additional monitoring and academic guidance
- **High risk:** Immediate intervention and personalized support

Possible interventions include tutoring, structured revision plans, practice examinations, attendance monitoring, time-management guidance, stress-management resources, and academic counseling.

## Repository Structure

```text
.
├── data/               # Dataset files, if redistribution is permitted
├── notebooks/          # EDA, preprocessing, and modeling notebooks
├── reports/            # Project report and presentation
├── src/                # Reusable Python modules, if available
├── requirements.txt    # Python dependencies
└── README.md            # Project documentation
```

> Update this section so that it matches the actual files and folders in the repository.

## Installation and Usage

### 1. Clone the repository

```bash
git clone https://github.com/YOUR-USERNAME/YOUR-REPOSITORY.git
cd YOUR-REPOSITORY
```

### 2. Create a virtual environment

```bash
python -m venv .venv
```

Activate it on Windows:

```bash
.venv\Scripts\activate
```

Activate it on macOS or Linux:

```bash
source .venv/bin/activate
```

### 3. Install the required packages

```bash
pip install -r requirements.txt
```

### 4. Download the dataset

Download the dataset from Kaggle and place it in the `data/` directory, then update the dataset path inside the notebook if necessary.

### 5. Run the project

```bash
jupyter notebook
```

Open the main notebook and run its cells in order.

## Limitations

- The analysis uses a single structured dataset, which may not represent all institutions or student populations.
- Missing values may influence model performance despite preprocessing.
- Feature importance represents predictive relationships, not causal effects.
- The model should support human decision-making rather than independently determine student outcomes.

## Future Work

- Validate the model using data from different institutions and academic years.
- Incorporate real-time academic and behavioral data throughout the semester.
- Predict failure probabilities and risk levels instead of only Pass/Fail labels.
- Apply explainability methods such as SHAP to support individual predictions.
- Deploy the model through a dashboard or web application for educators.
- Monitor fairness, model drift, and performance after deployment.

## Team

- Abdallah Hesham AbdelSadek
- Retaj Abdelrady Abdelraheem
- Nadeen Hany Mohamed
- Eyad Ahmed Abdelkareem

## Acknowledgment

This project was completed as **Project 2** during the **Samsung Innovation Campus – AI Program**.

## License

This repository is intended for educational and portfolio purposes. Add an appropriate open-source license only after confirming that all included code, data, reports, and presentation assets can be redistributed.
