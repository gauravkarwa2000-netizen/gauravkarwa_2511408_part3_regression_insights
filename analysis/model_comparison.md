# Model Comparison

## Overview

Three regression models were built using `monthly_sales` as the dependent variable. This document compares their performance, significant variables, business usefulness, and limitations.

---

## Model 1 – Simple Regression: Footfall

| Item | Detail |
|---|---|
| **Model Name** | Model 1 – Footfall Simple Regression |
| **Dependent Variable** | monthly_sales |
| **Independent Variable** | footfall |
| **R-squared** | 0.7348 |
| **Regression Equation** | monthly_sales = 447,699.03 + 35.64 × footfall |
| **Coefficient (footfall)** | 35.64 |
| **P-value (footfall)** | < 0.001 (highly significant) |
| **Intercept P-value** | < 0.001 |

**Business Usefulness:**
Footfall alone explains 73.5% of variation in monthly sales — a remarkably strong single predictor. This model is intuitive and actionable: the number of customers visiting the store is the dominant driver of revenue. Useful for store traffic planning and location decisions.

**Limitations:**
- Ignores marketing spend, inventory, store type, and other business levers
- Cannot be used to guide decisions on discount strategy or staffing
- Footfall itself may be influenced by other variables (endogeneity)

---

## Model 2 – Simple Regression: Marketing Spend

| Item | Detail |
|---|---|
| **Model Name** | Model 2 – Marketing Spend Simple Regression |
| **Dependent Variable** | monthly_sales |
| **Independent Variable** | marketing_spend |
| **R-squared** | 0.1574 |
| **Regression Equation** | monthly_sales = 567,463.56 + 2.05 × marketing_spend |
| **Coefficient (marketing_spend)** | 2.05 |
| **P-value (marketing_spend)** | < 0.001 (significant) |
| **Intercept P-value** | < 0.001 |

**Business Usefulness:**
Marketing spend is statistically significant but explains only 15.7% of sales variance on its own. The coefficient of 2.05 means every additional £1 spent on marketing is associated with £2.05 in extra monthly sales — a 2:1 ratio that suggests modest but positive return. Useful as a baseline before controlling for other variables.

**Limitations:**
- Low explanatory power — marketing is far from the only driver
- May capture reverse causation: higher-performing stores may spend more on marketing
- Cannot distinguish between marketing-driven footfall and organic footfall

---

## Model 3 – Multiple Regression (Final Model)

| Item | Detail |
|---|---|
| **Model Name** | Model 3 – Multiple Regression |
| **Dependent Variable** | monthly_sales |
| **Independent Variables** | footfall, marketing_spend, inventory_availability_pct, customer_rating, avg_discount_pct, holiday_flag, is_high_street, is_airport, is_mall |
| **R-squared** | 0.8222 |
| **Adjusted R-squared** | 0.8168 |
| **Reference Category (store_type)** | Residential |

### Coefficient Table

| Variable | Coefficient | P-value | Significant? |
|---|---|---|---|
| Intercept | 73,762.67 | 0.1416 | No |
| footfall | 33.51 | < 0.001 | ✅ Yes |
| marketing_spend | 1.17 | < 0.001 | ✅ Yes |
| inventory_availability_pct | 2,954.44 | < 0.001 | ✅ Yes |
| customer_rating | 12,808.63 | 0.0088 | ✅ Yes |
| avg_discount_pct | −57,469.08 | 0.1254 | ❌ No (10%) |
| holiday_flag | 11,148.51 | 0.0982 | ❌ No (marginal) |
| is_high_street | 16,295.03 | 0.0094 | ✅ Yes |
| is_airport | 38,824.96 | < 0.001 | ✅ Yes |
| is_mall | 26,401.95 | 0.0001 | ✅ Yes |

**Business Usefulness:**
This model captures 82.2% of sales variation and identifies multiple actionable levers. Leadership can use it to understand the relative contribution of footfall, marketing, inventory, customer experience, and store type. The inclusion of dummy variables reveals that store type significantly affects sales levels beyond what traffic alone explains.

**Limitations:**
- Does not capture store size, product range, or local demographics
- Only 4 months of data — seasonal patterns may not be fully represented
- avg_discount_pct is not statistically significant — its business role is ambiguous in this model
- Regression identifies association, not proven causation

---

## Summary Comparison Table

| Metric | Model 1 (Footfall) | Model 2 (Marketing) | Model 3 (Multiple) |
|---|---|---|---|
| R-squared | 0.7348 | 0.1574 | **0.8222** |
| Adj. R-squared | — | — | **0.8168** |
| No. of predictors | 1 | 1 | 9 |
| Significant variables | footfall | marketing_spend | footfall, marketing_spend, inventory_availability_pct, customer_rating, is_high_street, is_airport, is_mall |
| Weakest variable | — | — | avg_discount_pct |
| Business usefulness | High (traffic focus) | Moderate (marketing ROI) | **Highest (holistic view)** |
| Recommended for decisions | Footfall strategy | Marketing budget | **All strategic decisions** |

---

## Conclusion

**Model 3 is the recommended final model.** Its Adjusted R² of 0.8168 indicates strong explanatory power with an appropriate number of predictors. It provides leadership with a multidimensional view of what drives monthly sales and is robust enough to support decisions across marketing, inventory, customer experience, and store prioritisation.
