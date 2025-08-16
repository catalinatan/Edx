# Basketball Performance Classifier

## Overview

This project builds classification models to predict the postseason performance of NCAA Division I college basketball teams based on regular season statistics. Using historical data covering five seasons and 354 teams, several machine learning algorithms are applied to identify the best model for forecasting the round in which a team is eliminated in the NCAA March Madness tournament.

---

## Dataset Description

The dataset (`cbb.csv`) contains performance data of college basketball teams for five seasons and includes the following fields:

| Field      | Description                                                                                         |
|------------|---------------------------------------------------------------------------------------------------|
| TEAM       | Division I college basketball school                                                              |
| CONF       | Athletic Conference (e.g., ACC, B12, BE, SEC, etc.)                                               |
| G          | Number of games played                                                                             |
| W          | Number of games won                                                                               |
| ADJOE      | Adjusted Offensive Efficiency (points scored per 100 possessions vs average Division I defense)   |
| ADJDE      | Adjusted Defensive Efficiency (points allowed per 100 possessions vs average Division I offense)  |
| BARTHAG    | Power Rating (chance of beating an average Division I team)                                       |
| EFG_O      | Effective Field Goal Percentage Shot                                                              |
| EFG_D      | Effective Field Goal Percentage Allowed                                                           |
| TOR        | Turnover Percentage Allowed (turnover rate)                                                      |
| TORD       | Turnover Percentage Committed (steal rate)                                                       |
| ORB        | Offensive Rebound Percentage                                                                      |
| DRB        | Defensive Rebound Percentage                                                                      |
| FTR        | Free Throw Rate                                                                                   |
| FTRD       | Free Throw Rate Allowed                                                                           |
| 2P_O       | Two-Point Shooting Percentage                                                                     |
| 2P_D       | Two-Point Shooting Percentage Allowed                                                            |
| 3P_O       | Three-Point Shooting Percentage                                                                   |
| 3P_D       | Three-Point Shooting Percentage Allowed                                                          |
| ADJ_T      | Adjusted Tempo (estimated possessions per 40 minutes)                                            |
| WAB        | Wins Above Bubble (cutoff threshold for NCAA Tournament inclusion)                                |
| POSTSEASON | Round where the team was eliminated or ended season (R68, R64, R32, S16, E8, F4, 2ND, Champion)   |
| SEED       | Tournament Seed                                                                                   |
| YEAR       | Season year                                                                                      |

---

## Objectives

- Create and evaluate classification models to predict tournament outcomes.
- Apply the following algorithms:
  - K-Nearest Neighbors (KNN)
  - Decision Tree
  - Support Vector Machine (SVM)
  - Logistic Regression
- Evaluate models using accuracy, Jaccard index, F1 score, and log loss.
- Select the best performing model for this specific dataset.

---

## Data Preprocessing

1. Add a `windex` column indicating if Wins Above Bubble (`WAB`) is greater than 7.
2. Filter dataset to teams reaching Sweet Sixteen (`S16`), Elite Eight (`E8`), or Final Four (`F4`).
3. Convert categorical fields to numeric where necessary.
4. Normalize features using standard scaling (zero mean, unit variance).

---

## Features Used

Predictor features (`X`):

- G, W, ADJOE, ADJDE, BARTHAG, EFG_O, EFG_D, TOR, TORD, ORB, DRB, FTR, FTRD, 2P_O, 2P_D, 3P_O, 3P_D, ADJ_T, WAB, SEED, windex

Target label (`y`):

- POSTSEASON (tournament round outcome)

---

## Model Training and Validation

- Data split into training (80%) and validation (20%) sets.
- Models trained and tuned on training set.
- Model performance evaluated on validation set.

Summary of hyperparameter tuning:

- KNN: Tested k values from 1 to 15.
- Decision Tree: Tested max_depth from 1 to 14.
- SVM: Tested kernels - linear, poly, rbf, sigmoid.
- Logistic Regression: Regularization parameter C=0.01.

---

## Results on Validation Set

| Algorithm          | Best Parameter               | Accuracy     |
|--------------------|------------------------------|--------------|
| K-Nearest Neighbor  | k=5                          | 66.67%       |
| Decision Tree      | max_depth=1                  | 66.67%       |
| Support Vector Machine | Kernel = 'poly'             | 66.67%       |
| Logistic Regression | C=0.01                      | 58.33%       |

---

## Model Evaluation on Test Set

Applied models on unseen test data for additional evaluation using:

- Accuracy
- Jaccard Index
- F1 Score (micro average)
- Log Loss (not applicable for all models due to label types)

| Algorithm          | Accuracy    | Jaccard    | F1-Score   | Log Loss           |
|--------------------|-------------|------------|------------|--------------------|
| K-Nearest Neighbor  | 62.86%      | 0.4583     | 0.6286     | Not applicable     |
| Decision Tree      | 64.29%      | 0.4737     | 0.6429     | Not applicable     |
| Support Vector Machine (poly kernel) | 68.57%      | 0.5217     | 0.6857     | Not applicable     |
| Logistic Regression | 68.57%      | 0.5217     | 0.6857     | Computed but ignored|

*Note:* Log loss metric requires probability predictions which are not supported directly for string class labels in this dataset.

---

## Important Notes

- Sports outcome prediction is inherently difficult due to many unpredictable game factors.
- In sports betting contexts, an accuracy above 55% is often considered successful as it suggests profitability.
- Decisions on model choice should consider both accuracy and interpretability.

---

## Installation

Make sure to have Python 3 installed and then install the required packages:

