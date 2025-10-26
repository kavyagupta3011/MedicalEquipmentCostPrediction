# MedicalEquipmentCostPrediction

## 1. Task Description

The goal of this project was to predict the transport cost for delivering medical equipment to hospitals. This is a regression problem focused on estimating a continuous numerical output.

---

## 2. Dataset

* train.csv: 5000 rows, 20 features
* test.csv: 500 rows, 19 features

---

## 3. Key Challenges & EDA Findings

* The primary challenge was severe data quality issues and extreme outliers.
Target Skew: The `Transport_Cost` target was highly right-skewed and required a log-transform (`np.log1p`) to model effectively.
* Data Integrity:
    * 493 rows had impossible negative transport costs[cite: 30].
    * 1,774 rows (over 35%) had an `Order_Placed_Date` *after* the `Delivery_Date`.
* Multicollinearity:EDA revealed high VIF scores, such as $\approx 24.9$ for `Equipment_Weight_Log`, indicating strong multicollinearity.

---

## 4. Models & Feature Engineering

A wide range of models was tested, supported by extensive feature engineering (e.g., `Equipment_Volume`, `Cost_per_Day`).

* **Linear Models:** Explored Linear, Ridge, Lasso, and Elastic Net. **Elastic Net** was the top linear performer.
* **Tree/Distance Models:** Standard Decision Trees, Random Forests, and KNN were implemented.
* **Boosting Models:** XGBoost, Gradient Boosting (LightGBM), and AdaBoost were all tuned.

---

## 5. Final Result & Key Observation

**Best Model:** **AdaBoost Regressor**
**Best Kaggle Score:** **4,065,760,976.40**

### Why AdaBoost Won:
* Linear regression assumes linear relationships between features and target — but real-world data is rarely purely linear. AdaBoost, with its adaptive weighted decision trees, can model non-linearities, interactions, and complex feature effects far better. 
* A single decision tree can easily overfit or underfit depending on its depth. AdaBoost reduces variance and improves generalization by combining many weak learners, effectively smoothing the decision boundary. 
* XGBoost and Gradient Boosting are powerful but complex. As our data is small and noisy, XGBoost and Gradient Boosting might be overfitting and  hence are performing slightly lesser than Adaboost Regressor. AdaBoost, using very shallow stumps and exponential weighting, sometimes generalizes better by being simpler and less flexible. AdaBoost can act like a “gentle” booster — less likely to overfit when data volume or quality isn’t great.

## Report:
[https://github.com/nainika0305/MedicalEquipmentCostPrediction/blob/main/ReportML_IMT2023016_034_529.pdf](https://github.com/nainika0305/MedicalEquipmentCostPrediction/blob/main/ReportML_IMT2023016_034_529.pdf)
