# Walmart Sales Forecasting

## Project Overview
This project predicts weekly sales for 45 Walmart stores and 81 departments across different regions. It tests multiple machine learning models to help store managers plan inventory and staffing accurately.

---

## Key Findings

- **Random Forest Performs Best:** The Random Forest model achieved the highest test accuracy with an R-squared score of 0.971 and the lowest test error of $3,881. It predicts weekly store sales with high precision.
- **Linear Models Fail on Complex Trends:** Ridge and Lasso regression scored poorly (R-squared of about 0.08). Simple straight-line formulas cannot capture seasonal jumps in retail sales.
- **Holidays Drive Massive Spikes:** Major holiday weeks like Thanksgiving and Christmas show huge jumps in customer purchases. Proper holiday preparation makes the biggest difference to total annual revenue.
- **Store Size and Location Matter:** Larger stores (Type A) consistently record much higher weekly revenue than smaller stores. Floor space directly influences customer footfall and total sales volume.
- **Specific Departments Drive Most Sales:** A handful of departments generate the majority of total store income. Managers must prioritize stock for these critical departments.

---

## Model Performance Summary

| Model | Test RMSE | Test R-Squared | Outcome |
| :--- | :--- | :--- | :--- |
| **Ridge Regression** | $21,812 | 0.085 | Poor |
| **Lasso Regression** | $22,092 | 0.061 | Poor |
| **Decision Tree** | $4,889 | 0.954 | Very Good |
| **Random Forest** | **$3,881** | **0.971** | **Best** |

---

## Concepts Used in This Project

### 1. Data Cleaning
Data cleaning finds and fixes missing values, wrong formats, and errors in raw tables. Clean data prevents computer programs from crash events and stops wrong calculations.

### 2. Exploratory Data Analysis (EDA)
Exploratory data analysis uses charts and summary numbers to inspect raw data. It reveals hidden patterns, peak periods, and unusual values before model building.

### 3. Feature Engineering
Feature engineering creates new helpful variables from existing columns, such as week numbers extracted from dates. Better inputs allow algorithms to detect annual sales cycles easily.

### 4. Train-Test Split
Train-test split divides all available records into two separate groups. The model learns from the first group and proves its real skill on the unseen second group.

### 5. Linear Regression
Linear regression tries to draw a single straight line through data points. It works well for simple trends but fails on seasonal retail spikes.

### 6. Ridge and Lasso Regression
These techniques add simple penalties to linear equations to control runaway numbers. They keep formulas stable but still fail on non-linear sales problems.

### 7. Decision Tree Regressor
A decision tree makes predictions through a step-by-step series of simple yes-no questions. It handles complex data easily but sometimes memorizes training records too closely.

### 8. Random Forest Regressor
Random forest combines predictions from dozens of different decision trees at the same time. The team of trees reduces errors and delivers balanced, accurate forecasts.

### 9. Hyperparameter Tuning (GridSearchCV)
Hyperparameter tuning tests multiple computer settings automatically to find the best setup for a model. It selects the exact values that produce the lowest prediction error.

### 10. Root Mean Squared Error (RMSE)
RMSE measures the average dollar gap between predicted sales and actual sales. Lower values mean the model made closer guesses.

### 11. R-Squared Score (R2)
The R-squared score shows what fraction of total sales changes the model explains. A score near 1.0 means the model tracks customer demand almost perfectly.

---

## How to Run
1. Place `train.csv`, `stores.csv`, and `features.csv` in the project root folder.
2. Open `Walmart_Sales_Forecasting.ipynb` in VS Code or Jupyter Notebook.
3. Run all notebook cells to inspect charts and train the forecasting models.
