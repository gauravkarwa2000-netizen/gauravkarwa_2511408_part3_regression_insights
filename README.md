# gauravkarwa_2511408_part3_regression_insights# Part 3: Regression-Based Business Insights & Model Interpretation

## Business Problem Summary

A retail chain leadership team wants to understand what factors are driving **monthly sales performance** across their stores. The goal is to use regression analysis to identify the strongest predictors of sales so that leadership can make informed decisions about marketing spend, inventory, staffing, discounting, and store type prioritisation.

---

## Dataset Description

- **File:** `data/business_regression_data.xlsx`
- **Sheet:** `store_performance`
- **Records:** 320 rows (80 stores × 4 months: Jan–Apr 2025)
- **Missing values:** `competitor_distance_km` (6 missing), `customer_rating` (8 missing) — handled by listwise deletion, leaving 306 clean rows for modelling

| Column | Type | Description |
|---|---|---|
| store_id | Categorical | Unique store identifier |
| month | Date | Month of observation |
| region | Categorical | East, North, South, West |
| store_type | Categorical | Residential, High Street, Airport, Mall |
| marketing_spend | Numerical | Monthly marketing budget (£) |
| footfall | Numerical | Number of customer visits |
| avg_discount_pct | Numerical | Average discount rate applied |
| staff_count | Numerical | Number of staff in store |
| inventory_availability_pct | Numerical | % of SKUs available in stock |
| competitor_distance_km | Numerical | Distance to nearest competitor (km) |
| holiday_flag | Binary | 1 if month includes public holiday |
| customer_rating | Numerical | Average customer satisfaction score |
| **monthly_sales** | **Numerical** | **Dependent variable (£)** |
| monthly_profit | Numerical | Not used — would cause data leakage |

---

## Dependent and Independent Variables

**Dependent Variable:** `monthly_sales`

**Independent Variables used in models:**
- Numerical: `footfall`, `marketing_spend`, `inventory_availability_pct`, `customer_rating`, `avg_discount_pct`
- Binary: `holiday_flag`
- Dummy: `is_high_street`, `is_airport`, `is_mall` (from `store_type`)

**Variables excluded from regression:**
- `store_id`, `month` — identifiers, not predictors
- `monthly_profit` — derived from sales; would cause leakage
- `staff_count` — high collinearity with footfall; excluded to keep model parsimonious
- `competitor_distance_km` — low predictive signal in exploratory analysis

---

## Regression Approach

Three models were built:

| Model | Type | Variables |
|---|---|---|
| Model 1 | Simple | footfall → monthly_sales |
| Model 2 | Simple | marketing_spend → monthly_sales |
| Model 3 | Multiple | footfall + marketing_spend + inventory_availability_pct + customer_rating + avg_discount_pct + holiday_flag + store_type dummies |

All models use **Ordinary Least Squares (OLS)** regression.

---

## Dummy Variable Approach

The categorical variable `store_type` (4 levels) was converted into 3 dummy variables:

| Dummy Variable | Value = 1 when |
|---|---|
| `is_high_street` | store_type == "High Street" |
| `is_airport` | store_type == "Airport" |
| `is_mall` | store_type == "Mall" |

**Reference category:** `Residential` (omitted to avoid the dummy variable trap)

Coefficients for `is_high_street`, `is_airport`, `is_mall` represent the **average sales difference compared to a Residential store**, holding all other variables constant.

---

## Model Comparison Summary

| Model | R² | Key Significant Variables |
|---|---|---|
| Model 1 – Footfall | 0.7348 | footfall (p < 0.001) |
| Model 2 – Marketing Spend | 0.1574 | marketing_spend (p < 0.001) |
| Model 3 – Multiple | **0.8222** | footfall, marketing_spend, inventory_availability_pct, customer_rating, is_high_street, is_airport, is_mall |

---

## Final Model Selected

**Model 3 – Multiple Regression** was selected as the final model (Adjusted R² = 0.8168).

It explains **82.2% of variation** in monthly sales and includes both numerical and categorical predictors with strong business interpretability.

---

## Business Recommendation

1. **Footfall is the single strongest predictor** — every additional 1,000 customers visiting a store is associated with approximately £33,500 in additional monthly sales. Leadership should prioritise footfall-driving initiatives (location, access, events).

2. **Marketing spend has a positive but smaller effect** — each additional £1,000 in marketing spend is linked to ~£1,174 in sales. Marketing should be evaluated on ROI rather than scale.

3. **Inventory availability matters** — a 1 percentage point improvement in stock availability is associated with ~£2,954 additional monthly sales. Reducing stockouts has direct revenue impact.

4. **Airport stores outperform Residential stores by ~£38,825/month** on average, followed by Mall stores (+£26,402) and High Street stores (+£16,295), all else equal.

5. **Discounting appears counterproductive** (negative coefficient, though not statistically significant at 5% level) — leadership should review the discounting strategy.

---

## Assumptions and Limitations

- The model assumes **linear relationships** between predictors and sales — non-linearities may exist
- **Correlation ≠ Causation** — regression identifies associations, not proven causal effects
- Only 4 months of data are available — **seasonality** may not be fully captured
- **Omitted variable bias** — factors like local demographics, store size, and product range are not included
- Model residuals should be checked for heteroscedasticity and normality for full statistical validity

---

## Screenshots Included

| File | Description |
|---|---|
| `screenshots/simple_regression_output.png` | Model 1 – Footfall simple regression output |
| `screenshots/multiple_regression_output.png` | Model 3 – Multiple regression coefficient table |
| `screenshots/residuals_preview.png` | Predicted vs actual values and residuals |
| `screenshots/model_comparison_preview.png` | Side-by-side model comparison table |
