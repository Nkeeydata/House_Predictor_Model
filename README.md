[README.md](https://github.com/user-attachments/files/29502243/README.md)
# House_Predictor_Model


## Project Overview

This project predicts residential **house sale prices** using a structured housing dataset of 545 properties, with the goal of helping real estate stakeholders estimate fair market value from a property's physical and locational characteristics. The dataset includes features such as lot area, number of bedrooms/bathrooms, stories, parking, and amenities (air conditioning, hot water heating, proximity to main road, preferred area, furnishing status). A Linear Regression model and a Random Forest Regressor were trained and compared; Linear Regression performed best, explaining roughly **65% of the variance in price (R² = 0.65)** with a mean absolute error of about **₦970,000** on held-out test data.

## Business Understanding

Stakeholders for this project include real estate agencies, property valuation firms, mortgage lenders, and individual home buyers/sellers who need a fast, data-driven way to estimate a property's fair market price rather than relying solely on manual comparables or appraiser judgment. Accurate, transparent pricing models help agents set competitive listing prices, help buyers avoid overpaying, and help lenders sanity-check valuations before approving loans. Mispricing — listing too high or too low — directly costs stakeholders time on market or lost revenue, making a reliable predictive pricing tool valuable to the business.

## Data Understanding

The dataset (`Housing.csv`) contains **545 property records** with **13 columns**: the target variable `price`, along with `area`, `bedrooms`, `bathrooms`, `stories`, `parking`, and a set of binary amenity indicators (`mainroad`, `guestroom`, `basement`, `hotwaterheating`, `airconditioning`, `prefarea`), plus a categorical `furnishingstatus` (furnished, semi-furnished, unfurnished). The data is clean with **no missing values**. No explicit date/timeframe field is provided, so the data should be treated as a cross-sectional snapshot rather than a time series — a key limitation, since it cannot capture market trends, inflation, or seasonal price shifts. Other limitations include the absence of location/neighborhood-level detail beyond `prefarea`, and a moderate sample size that limits model generalizability to broader markets.

Exploratory analysis showed `area` (correlation ≈ 0.54) and `bathrooms` (≈ 0.52) as the features most strongly correlated with price, followed by `airconditioning` and `stories`. Unfurnished homes showed a negative correlation with price (≈ -0.28), suggesting furnishing status is a meaningful price driver.

## Modeling and Evaluation

Categorical variables were encoded (binary yes/no mapped to 1/0; `furnishingstatus` one-hot encoded), and the data was split 80/20 into training and test sets. Two models were trained and evaluated on the test set:

- **Linear Regression**: R² = 0.65, MAE ≈ ₦970,000, RMSE ≈ ₦1,324,000
- **Random Forest Regressor** (300 trees): R² = 0.62, MAE ≈ ₦1,012,000, RMSE ≈ ₦1,393,000

Linear Regression slightly outperformed Random Forest on this dataset, likely due to the relatively small sample size and mostly linear relationships between features and price. Feature importance from both models converged on `area`, `bathrooms`, and `airconditioning` as the strongest predictors, consistent with the correlation analysis.

## Conclusion

The Linear Regression model offers a reasonably strong baseline (R² ≈ 0.65) for estimating house prices from structural and amenity features, and could support stakeholders in generating quick, defensible price estimates. For production use, I'd recommend treating model output as a starting point alongside human appraisal rather than a final price. Future steps include collecting more granular location data (e.g., neighborhood, distance to city center), gathering a larger and more recent dataset with sale-date information to capture market trends, engineering interaction features (e.g., area × stories), and testing regularized models (Ridge/Lasso) or gradient boosting (XGBoost) to improve predictive accuracy.
