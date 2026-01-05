# Terry Traffic  Stops: Predicting Arrest Outcomes & Assessing Racial Equity

**Analysis of 65,980 Terry Traffic Stops Conducted by the Seattle Police Department (2015–2026)**


## Project Overview

This project analyzes **Terry Traffic Stops** (Terry_Stops_20260103.csv) (investigative detentions based on reasonable suspicion) conducted by the Seattle Police Department to:
- Predict whether a stop results in an arrest
- Identify the primary factors driving arrest decisions
- Assess potential racial disparities in outcomes

Using machine learning models and comprehensive feature engineering, the analysis reveals that **arrests are overwhelmingly driven by evidentiary factors** (especially weapon presence and call type), rather than subject demographics.

## Key Findings

- **Weapon presence** is the strongest predictor of arrest — dramatically increasing likelihood when present
- **Initial call type** and **patrol sector** are major secondary drivers
- **Demographic factors** (race, age, gender) play a relatively minor role in arrest decisions once a stop occurs
- Black individuals comprise ~30% of stops despite being ~7% of Seattle's population — indicating disproportionality in **who is stopped**
- However, **conditional on being stopped**, arrest outcomes appear largely evidence-based

These insights suggest arrest practices during stops are primarily justified by objective risk indicators, though initial stop selection remains a concern for equity.

## Dataset

- **Source**: Terry Stops dataset (Terry_Stops_20260103.csv)
- **Size**: 65,980 records (2015 – early 2026)
- **Target**: `Arrest Flag` (Y/N) — highly imbalanced (~89% No Arrest, ~11% Arrest)
- **Features**: Subject/officer demographics, time/location, call type, weapon involvement, frisk flag

## Methodology

### Feature Engineering
- Cyclical encoding for time (hour, month, day of week)
- Age estimation from categorical groups + officer-subject age difference
- Interaction flags: Same Race, Same Gender, Minority Interaction (White officer + non-White subject)
- Time-of-day buckets and weekend flag

### Preprocessing
- One-hot encoding for low-cardinality categoricals
- Target encoding for high-cardinality features (Initial Call Type, Weapon Type, Sector)
- Ordinal encoding for Subject Age Group
- Standard scaling for numerical features

### Models Evaluated
| Model                | ROC-AUC | Recall (Arrest) | Key Strength                  |
|----------------------|---------|-----------------|-------------------------------|
| Random Forest        | 0.875   | 0.933           | Best overall balance          |
| Logistic Regression  | 0.871   | 0.926           | Most interpretable            |
| AdaBoost             | 0.778   | 1.000           | Perfect arrest detection      |
| Gradient Boosting    | 0.879   | 0.037           | High precision, low recall    |
| Dummy Baseline       | 0.500   | 0.000           | Majority class predictor      |

**Best Model**: Random Forest (strong discrimination + balanced metrics)  
**Most Interpretable**: Logistic Regression (clear coefficients showing weapon dominance)

## CONCLUSION
This analysis of Seattle Police Department's Terry stops from 2015–2026 reveals that arrests are predominantly driven by evidentiary and situational factors, such as weapon presence and initial call type, rather than subject demographics like race or age. Among the evaluated models, Random Forest performed best overall (ROC-AUC: 0.8754, balanced recall and precision), while AdaBoost excelled in recall (1.00) but at the cost of many false positives. These findings suggest that SPD's practices are largely evidence-based, but the overrepresentation of certain racial groups in stops (e.g., Black or African American at ~30%) warrants further scrutiny to mitigate potential biases.

For stakeholders like SPD, OPA, and community groups, the models can inform targeted reforms, such as enhanced training on call-type responses or audits in high-arrest sectors. Limitations include the class imbalance impacting precision and the lack of causal inference—future work could incorporate external data (e.g., census demographics) for fairness metrics. Overall, this project underscores the value of data-driven insights in promoting equitable policing and public trust.