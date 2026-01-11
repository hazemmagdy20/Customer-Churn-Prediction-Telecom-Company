# Customer-Churn-Prediction-Telecom-Company
This project aims to predict whether a customer will leave the company (Churn) or not, allowing the business to take proactive retention actions.

## 📌 Project Overview
- Customer churn is one of the biggest challenges for telecom companies.

- This project aims to predict whether a customer will leave the company (Churn) or not, allowing the business to take proactive retention actions.

## 🎯 Goal

- Predict customer churn using machine learning.

  ```python
  Churn = Yes → Customer will leave
  Churn = No → Customer will stay

- Each column in the dataset represents a potential reason why a customer might leave or stay.


## 🏢 Business Context

- Define Company, Problem, Target.
  ```python
   Company: Telecom Company
   Problem Type: Binary Classification
   Target Variable: Churn

- Reducing churn directly improves:
  ```python
  Revenue retention
  Customer lifetime value
  Marketing efficiency

## 📂 Dataset Information

- Rows: 7,043 customers
- Columns: 21 features
- Target: Churn (Yes / No)

## 🧾 Dataset Columns Explanation  

## 1️⃣ CustomerID
- Meaning: Unique customer identifier
- Purpose: Tracking only
- ML Usage: ❌ Removed (no predictive value)

## 2️⃣ Gender (Male / Female)
- Type: Demographic feature
- Why included: Behavioral analysis
- Impact: Usually weak, but retained

## 3️⃣ SeniorCitizen (0 / 1)
- Binary numerical feature
- Older customers may:
- Prefer stability
- Or use fewer services

## 4️⃣ Partner
- Indicates if customer has a partner
- Customers with partners tend to be more stable

## 5️⃣ Dependents
- Indicates children/dependents
- Family responsibility can reduce churn

## 6️⃣ Tenure ⭐
- Months with the company
- One of the strongest predictors
- Low tenure → High churn
- High tenure → Loyalty

## 7️⃣ PhoneService
- Whether customer has phone service
- Fewer services → Higher churn risk

## 8️⃣ MultipleLines
- Yes / No / No phone service
- Reflects service usage level

## 9️⃣ InternetService
- DSL / Fiber optic / No internet
- Fiber optic users show higher churn

## 🔟 OnlineSecurity
- Add-on service
- More services → stronger attachment

## 1️⃣1️⃣ OnlineBackup
- Backup service
- Improves customer stickiness
  
## 1️⃣2️⃣ DeviceProtection
- Device insurance
- Paying more → less likely to churn

## 1️⃣3️⃣ TechSupport ⭐
- One of the most important features
- No tech support → high churn

## 1️⃣4️⃣ StreamingTV
- Lifestyle / usage intensity feature

## 1️⃣5️⃣ StreamingMovies
- Similar to StreamingTV
- Weak alone, useful combined

## 1️⃣6️⃣ Contract ⭐⭐⭐
- Month-to-month ❌
- One year
- Two year ✅
- Top churn driver

## 1️⃣7️⃣ PaperlessBilling
- Behavioral feature
- Digital users churn slightly more

## 1️⃣8️⃣ PaymentMethod ⭐
- Electronic check ❌ (high churn)
- Automatic payments ✅ (low churn)

## 1️⃣9️⃣ MonthlyCharges
- Monthly bill amount
- Higher charges → dissatisfaction

## 2️⃣0️⃣ TotalCharges
- Total amount paid
- Correlated with tenure & monthly charges

## 2️⃣1️⃣ Churn (TARGET)
- Yes / No
- What we predict


## 🛠️ Project Workflow (Steps Done)

- Data Loading & Exploration
  ```python
  Imported required libraries
  Loaded dataset
  Checked shape and data info
  Identified data types & missing values

- Data Cleaning
  ```python
  Converted TotalCharges from object → numeric
  Replaced missing values with median
  Removed CustomerID

- Exploratory Data Analysis (EDA)

- 📌 Overall Churn Rate
   ```python
   No: 73.46%
   Yes: 26.54%
   ⚠️ Dataset is imbalanced

- 📌 Churn vs Contract
  
  | Contract       | Churn Rate  |
  | -------------- | ----------- |
  | Month-to-month | **42.7% ❌** |
  | One year       | 11.3%       |
  | Two year       | **2.8% ✅**  |

  ➡️ Contract type is a critical churn driver

- 📌 Churn vs Tenure

  | Churn | Mean Tenure |
  | ----- | ----------- |
  | No    | ~38 months  |
  | Yes   | ~18 months  |

  ➡️ New customers churn more

- 📌 Churn vs Payment Method

   | Payment Method       | Churn Rate  |
   | -------------------- | ----------- |
   | Electronic check     | **45.3% ❌** |
   | Mailed check         | 19.1%       |
   | Bank transfer (auto) | 16.7%       |
   | Credit card (auto)   | **15.2% ✅** |

   ➡️ Automatic payments improve retention

- 📌 Churn vs Internet Service

   | Internet Service | Churn Rate  |
   | ---------------- | ----------- |
   | Fiber optic      | **41.9% ❌** |
   | DSL              | 18.9%       |
   | No internet      | **7.4% ✅**  |

   ➡️ Premium service ≠ lower churn

- 🔥 High-Risk Customer Profile
  ```python
  Month-to-month contract
  Short tenure
  Electronic check
  Fiber optic

- Data Preprocessing
  ```python
  Label Encoding for categorical features
  Train-test split
  Feature scaling using StandardScaler

- Model Training
  ```python
  RandomForestClassifier
  class_weight = 'balanced'

- Model Evaluation (Before SMOTE)
  ```python
  Class 1 (Churn):
  Precision = 0.61
  Recall    = 0.46
  F1-score  = 0.53
  Accuracy  = 0.78

  ⚠️ Issues:
  Imbalanced data
  Model biased toward non-churn
  Misses many churners

  ❌ Business Impact:
  Customers leave without intervention
  Revenue loss

- Apply SMOTE (Oversampling)
  ```python
  Balanced minority class
  Retrained model

- Model Evaluation (After SMOTE)
  ```python
   Class 1 (Churn):
   Precision = 0.55
   Recall    = 0.58
   F1-score  = 0.56
   Accuracy  = 0.77

   SMOTE now provides artificial churn examples.
   The model now sees churn patterns more clearly.
   It is now bolder in predicting churn.

   Key changes:
   Recall ↑ from 0.46 → 0.58
   F1-score ↑ from 0.53 → 0.56
   Precision ↓ slightly (expected)

## 📊 Before vs After Comparison

| Metric            | Before | After    | Interpretation       |
| ----------------- | ------ | -------- | -------------------- |
| Recall (Churn)    | 0.46   | **0.58** | Capture more churn ✅ |
| Precision (Churn) | 0.61   | 0.55     | More false alarms ⚠️ |
| F1-score          | 0.53   | **0.56** | Better balance ✅     |
| Accuracy          | 0.78   | 0.77     | Not important        |

## 🏆 Final Conclusion

Applying SMOTE significantly improved the model’s ability to detect churners by increasing recall and F1-score, which is more aligned with real business objectives where missing a churner is more costly than false alarms.

## 💾 Deployment Preparation
- Saved trained model
- Saved scaler for future inference & deployment

## 🚀 Future Improvements
- ROC & PR curves
- Threshold tuning
- SHAP feature importance
- Trying other models like XGBoost / LightGBM 
