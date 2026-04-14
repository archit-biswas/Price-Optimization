# Price Optimization using Python

## Project Overview

This project demonstrates a comprehensive, end-to-end price optimization strategy using Python. It combines exploratory data analysis, competitive benchmarking, price elasticity modeling, dynamic pricing simulation, and machine learning-based demand forecasting to determine optimal pricing for retail products. The goal is to maximize revenue and market share by accounting for market demand, competition, costs, and customer behavior.

---

## Dataset

**File:** `Competition_Data.csv`  
**Size:** 100,000 rows × 9 columns

| Column | Description |
|---|---|
| `Index` | Row index |
| `Fiscal_Week_ID` | Fiscal week identifier (format: YYYY-WW) |
| `Store_ID` | Unique store identifier (10 stores) |
| `Item_ID` | Unique product identifier (176 items) |
| `Price` | Store's selling price (range: $47.70 – $310.66) |
| `Item_Quantity` | Quantity of the item sold |
| `Sales_Amount_No_Discount` | Sales amount before discounts |
| `Sales_Amount` | Final sales amount after discounts |
| `Competition_Price` | Competitor's price for the same item |

---

## Methodology

### 1. Data Loading and Exploration
- Loaded `Competition_Data.csv` into a Pandas DataFrame.
- Inspected data structure using `df.head()` and `df.info()`, confirming 100,000 entries with no missing values and correct data types.

### 2. Price Distribution Analysis
- Visualized price distributions for both the store and competition using histograms.
- **Observation:** Competition prices peaked around the $100–150 and $200–250 ranges, while the store's prices were more evenly distributed across $50–300.

### 3. Price vs. Sales Amount Relationship
- Examined the relationship between price and sales using scatter plots.
- **Observation:** The store showed high dispersion with no clear price-sales trend; competition showed denser clustering at higher sales amounts.

### 4. Price Changes Over Time
- Converted `Fiscal_Week_ID` to datetime and plotted average weekly prices for both parties.
- **Observation:** Competition maintained consistently higher, more stable average prices; the store experienced more fluctuations.

### 5. Price Elasticity of Demand
- Calculated period-over-period price elasticity: `elasticity = qty_change / price_change`
- **Observation:** High variability in elasticity indicates that sales are influenced by multiple factors beyond price alone (e.g., promotions, seasonality).

### 6. Total Sales and Price Bracket Comparison
- Compared total revenue between the store (~$114M) and competition (~$696M).
- Segmented sales into price brackets ($0–50 through $451–500) to identify performance gaps.
- **Observation:** Competition outperformed the store across all major price brackets, particularly in lower-to-mid ranges.

### 7. Dynamic Pricing Model
- Segmented items into **Low**, **Medium**, and **High** tiers based on average item price.
- Computed average elasticity per segment to guide pricing rules:
  - **Medium segment** (~0.154 avg elasticity): Price increased by **5%** (relatively inelastic demand).
  - **High segment** (~0.148 avg elasticity): Price decreased by **10%** (to test price sensitivity).
- Simulated dynamic pricing, resulting in a projected total sales amount of ~$622.7M vs. ~$114.1M under existing pricing.

### 8. Feature Engineering for ML Models
- Created lag features (`qty_lag1`, `qty_lag2`) and rolling averages (`qty_rolling4`).
- Engineered a `price_gap` feature (store price minus competition price) and a `week_num` feature.
- Label-encoded `Store_ID` and `Item_ID` for use in tree-based models.

### 9. Baseline: Linear Regression
- Trained a Linear Regression model on a time-based 80/20 train-test split.
- **Results:** MAE = **13.94**, R² = **0.89**

### 10. XGBoost Regression
- Trained an XGBoost Regressor (300 estimators, learning rate 0.05, max depth 6) on the same split.
- Visualized feature importances to identify key demand drivers.
- **Results:** MAE = **11.88**, R² = **0.92** — a meaningful improvement over the baseline.

### 11. Prophet Time Series Forecasting
- Aggregated weekly `Item_Quantity` totals and trained a Prophet model to capture trend and seasonality.
- Evaluated on an 8-week holdout set.
- **Note:** Prophet performance was limited due to the short time range in the dataset (only 5 fiscal weeks), making it less suitable than regression models here.

### 12. Revenue Projection with Dynamic Pricing + XGBoost
- Applied the dynamic pricing rules to the feature set and used the trained XGBoost model to re-predict demand.
- **Results:**
  - Existing Revenue: ~$194.7M
  - Forecast-adjusted Dynamic Pricing Revenue: higher projected uplift

### 13. Revenue Sensitivity Analysis
- Simulated uniform price adjustments from **–10% to +15%** across all items using the XGBoost model.
- **Observation:** Helped identify a potentially optimal uniform price adjustment and highlighted the non-linear relationship between price changes and total revenue.

---

## Model Performance Summary

| Model | MAE | R² |
|---|---|---|
| Linear Regression | 13.94 | 0.89 |
| XGBoost | 11.88 | 0.92 |
| Prophet | Limited* | — |

*Prophet performance was constrained by the limited date range in the dataset.

---

## Key Findings

- **Competitive Gap:** Competition consistently achieved higher average prices, more stable pricing, and significantly greater total revenue (~6× the store's sales amount).
- **Inconsistent Demand Response:** High elasticity variability suggests promotions, seasonality, and other factors strongly influence sales beyond price alone.
- **Dynamic Pricing Effectiveness:** Segment-based pricing adjustments projected a massive revenue uplift — from ~$114M to ~$623M under a rule-based simulation.
- **ML-Driven Forecasting:** XGBoost outperformed Linear Regression on demand prediction (R² 0.92 vs. 0.89), with `qty_lag1`, `qty_lag2`, and `price_gap` being top features.
- **Revenue Sensitivity:** Sensitivity analysis showed that modest upward price adjustments can increase total revenue — but the optimal level depends on segment-level elasticity.

---

## Future Improvements

- **Richer Features:** Incorporate promotions, seasonality indicators, and inventory levels for more accurate demand modeling.
- **Advanced Elasticity Modeling:** Use regression analysis to capture non-linear elasticity and interactions between variables.
- **Hyperparameter Tuning:** Systematically tune XGBoost and LightGBM hyperparameters using cross-validation.
- **LightGBM Comparison:** Benchmark LightGBM against XGBoost for speed and performance at scale.
- **A/B Testing:** Design real-world experiments to validate dynamic pricing recommendations before full deployment.
- **Cost Integration:** Incorporate cost data to ensure price adjustments maintain healthy profit margins, not just maximise top-line revenue.
- **Extended Time Series:** Collect more historical data to improve Prophet's seasonal decomposition and forecasting accuracy.
- **Real-Time Pricing:** Build a pipeline for live data ingestion and automated price adjustments in response to market changes.

---

## How to Run

### 1. Clone the Repository
```bash
git clone <repository_url>
cd <project_directory>
```

### 2. Ensure Data Availability
Place `Competition_Data.csv` in an accessible path and update the file path in Cell 2:
```python
pricing_data = pd.read_csv("path/to/Competition_Data.csv")
```

### 3. Install Dependencies
```bash
pip install pandas matplotlib scikit-learn xgboost lightgbm prophet
```
> These are typically pre-installed in Google Colab. Run the `!pip install prophet xgboost lightgbm` cell in the notebook and **restart the runtime** before continuing.

### 4. Run the Notebook
Open `price_optimization.ipynb` in Google Colab or Jupyter and execute cells sequentially from top to bottom.

---

## Technologies Used

| Library | Purpose |
|---|---|
| Python 3 | Core language |
| Pandas | Data manipulation and analysis |
| Matplotlib | Data visualization |
| Scikit-learn | Linear Regression, train/test split, evaluation metrics |
| XGBoost | Gradient boosting demand prediction |
| LightGBM | Alternative gradient boosting (installed, available for extension) |
| Prophet | Time series forecasting |

---

## Conclusion

This project delivers a complete, data-driven price optimization pipeline — from competitive analysis and elasticity modeling through to ML-based demand forecasting and revenue projection. The dynamic pricing simulation demonstrated significant revenue potential, and the XGBoost model proved the strongest predictor of item-level demand. Together, these components form a solid foundation for building a production-ready pricing recommendation system.
