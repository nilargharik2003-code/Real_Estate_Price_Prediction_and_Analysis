# Real_Estate_Price_Prediction_and_Analysis
# Real Estate Price Prediction Using Multiple Linear Regression 🏠

This project focuses on predicting residential property prices using **Multiple Linear Regression (MLR)**. The analysis uses the Ames Housing dataset and examines how different property characteristics such as overall quality, living area, garage capacity, basement area, and other structural features influence house prices.

The project includes exploratory data analysis, data preprocessing, feature engineering, correlation analysis, outlier removal, multiple linear regression modelling, model evaluation, and residual diagnostics.

## 💾 Data Description

The analysis uses the **Ames Housing Dataset**, containing information about residential properties and their sale prices.

### Dataset Information

* **Number of observations:** 1460
* **Original number of variables:** 81
* **Target Variable:** `SalePrice`
* **Primary objective:** Predict house sale prices using multiple property-related features.

### Target Variable

* **`SalePrice`**: The final sale price of the residential property.

The dataset contains numerical and categorical variables describing various aspects of each property, including quality, size, construction year, garage, basement, rooms, and other features.

***

## 🛠️ Methodology Summary

The machine learning pipeline involved several key stages:

### 1. Data Preprocessing

* Loaded the Ames Housing dataset using **Pandas**.
* Removed the `Id` column as it does not provide meaningful predictive information.
* Examined the distribution of `SalePrice`.
* The original `SalePrice` variable was found to be positively skewed, with a skewness of approximately **1.8829**.
* Applied a **log transformation** using `np.log1p()` to reduce skewness.
* The skewness after transformation decreased to approximately **0.1213**.

### 2. Missing Value Treatment

Missing values were handled according to the meaning of each feature:

* Categorical variables where missing values represent the absence of a feature were assigned `"None"`.
* Numerical variables where missing values represented the absence of a feature were assigned `0`.
* `LotFrontage` was imputed using the median value within the corresponding `Neighborhood`.
* Remaining categorical missing values such as `Electrical` were filled using the mode.
* After imputation, the dataset contained **no missing values**.

### 3. Feature Engineering and Encoding

* Ordinal quality-related features such as `ExterQual`, `KitchenQual`, `BsmtQual`, and `GarageQual` were converted into numerical values using a quality scale from **0 to 5**.
* Remaining categorical variables were converted into numerical variables using **One-Hot Encoding** with `drop_first=True`.
* After encoding, the dataset contained **231 variables**.

### 4. Correlation Analysis

Correlation analysis was performed to identify variables strongly associated with house prices.

The most strongly correlated features included:

* `OverallQual`
* `GrLivArea`
* `ExterQual`
* `KitchenQual`
* `GarageCars`
* `GarageArea`
* `TotalBsmtSF`
* `1stFlrSF`
* `BsmtQual`
* `FullBath`
* `YearBuilt`

`OverallQual` showed the strongest correlation with `SalePrice` among the main property features, with a correlation of approximately **0.80 after outlier removal**.

Correlation analysis also identified potential **multicollinearity**, particularly between `GarageCars` and `GarageArea`.

### 5. Outlier Detection and Removal

The relationship between `GrLivArea` and `SalePrice` was examined to identify potential outliers.

Observations with:

* `GrLivArea >= 4000`
* `GrLivArea <= 500`

were removed.

The number of observations decreased from **1460 to 1453** after outlier removal.

### 6. Model Training

* The target variable was set as the log-transformed `SalePrice_log`.
* The predictor matrix contained the remaining property features.
* The dataset was divided into:
  * **80% Training Data**
  * **20% Testing Data**
* `random_state=42` was used to ensure reproducibility.
* A **Multiple Linear Regression** model from `sklearn.linear_model` was trained on the training dataset.

### 7. Model Evaluation

The trained model was evaluated on the held-out test set using:

* **R² Score**
* **Root Mean Squared Error (RMSE)**

An Actual vs Predicted plot was also created to visually examine the model's prediction performance.

### 8. Regression Diagnostics

A detailed Ordinary Least Squares (OLS) model was additionally fitted using `statsmodels` to examine regression statistics.

The analysis included:

* R² and Adjusted R²
* Statistical significance of coefficients
* Durbin-Watson statistic
* Residual analysis
* Q-Q plot
* Shapiro-Wilk normality test

***

## 📊 Results Summary

| Metric / Analysis | Result |
| :--- | :--- |
| **Original Observations** | 1460 |
| **Observations After Outlier Removal** | 1453 |
| **Features After One-Hot Encoding** | 231 |
| **Training Observations** | 1162 |
| **Testing Observations** | 291 |
| **Original SalePrice Skewness** | 1.8829 |
| **Log-Transformed Skewness** | 0.1213 |
| **Test R² Score** | 0.9189 |
| **Test RMSE** | 0.1104 |
| **OLS R²** | 0.945 |
| **Adjusted R²** | 0.932 |
| **Durbin-Watson Statistic** | 1.965 |
| **Shapiro-Wilk Statistic** | 0.9340 |
| **Shapiro-Wilk p-value** | < 0.001 |

***

## 🔍 Observation

The exploratory analysis showed that the original `SalePrice` distribution was strongly **right-skewed**, with a skewness of approximately **1.8829**. Applying a logarithmic transformation reduced the skewness substantially to approximately **0.1213**, producing a distribution much closer to symmetry.

Correlation analysis showed that property quality and size-related variables were among the strongest predictors of sale price. In particular, **OverallQual** and **GrLivArea** showed strong positive relationships with house prices.

After removing extreme observations based on `GrLivArea`, the dataset contained **1453 observations**. The Multiple Linear Regression model achieved an **R² score of 0.9189** and an **RMSE of 0.1104** on the test set.

The OLS model produced an **R² of 0.945** and an **Adjusted R² of 0.932**, indicating that the selected predictors explained a substantial proportion of the variation in the log-transformed sale prices.

The **Durbin-Watson statistic of 1.965** was close to 2, suggesting little evidence of strong first-order autocorrelation in the residuals.

However, the **Shapiro-Wilk test produced a p-value below 0.001**, leading to rejection of the null hypothesis of normally distributed residuals. Therefore, the residuals do not strictly follow a normal distribution despite the strong predictive performance of the model.

Overall, the results demonstrate that **Multiple Linear Regression can effectively model and predict residential property prices using structural, quality, and location-related features from the Ames Housing dataset**.

***

## 🧰 Tools & Libraries

* **Python**
* **Pandas** – Data loading, preprocessing, and manipulation
* **NumPy** – Numerical computations and log transformation
* **Matplotlib** – Data visualization
* **Seaborn** – Statistical visualization and correlation analysis
* **Scikit-learn** – Train-test splitting, Linear Regression, R², and RMSE
* **Statsmodels** – OLS regression and regression diagnostics
* **SciPy** – Skewness and Shapiro-Wilk statistical testing
