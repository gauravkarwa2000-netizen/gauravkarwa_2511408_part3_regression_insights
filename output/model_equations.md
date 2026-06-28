# Model Equations

## Simple Regression Equations

### Model 1 – Footfall

**Equation:**
```
monthly_sales = 447,699.03 + 35.64 × footfall
```

| Term | Value | Explanation |
|---|---|---|
| Intercept (447,699.03) | Base sales | Estimated monthly sales when footfall = 0 (theoretical baseline; not meaningful at footfall = 0 in practice) |
| footfall coefficient (35.64) | Per-customer revenue | Each additional customer visiting the store is associated with £35.64 in additional monthly sales |

**R-squared: 0.7348** — Footfall alone explains 73.5% of the variation in monthly sales.

**Business meaning:** The equation tells us that stores with higher customer traffic tend to generate proportionally higher sales. For every 1,000 additional visitors per month, a store earns approximately £35,640 more in sales.

---

### Model 2 – Marketing Spend

**Equation:**
```
monthly_sales = 567,463.56 + 2.05 × marketing_spend
```

| Term | Value | Explanation |
|---|---|---|
| Intercept (567,463.56) | Base sales | Estimated sales if marketing spend = £0 |
| marketing_spend coefficient (2.05) | Return per £1 | Each additional £1 of marketing spend is associated with £2.05 in additional monthly sales |

**R-squared: 0.1574** — Marketing spend alone explains only 15.7% of sales variation.

**Business meaning:** Marketing has a positive association with sales, but it is a weaker predictor than footfall. The return appears positive (£2.05 per £1 spent), but this must be interpreted cautiously — higher-revenue stores may naturally spend more on marketing, making the relationship partly reverse-causal.

---

## Multiple Regression Equation

### Model 3 – Full Multiple Regression (Final Model)

**Equation:**
```
monthly_sales = 73,762.67
              + 33.51 × footfall
              + 1.17 × marketing_spend
              + 2,954.44 × inventory_availability_pct
              + 12,808.63 × customer_rating
              − 57,469.08 × avg_discount_pct
              + 11,148.51 × holiday_flag
              + 16,295.03 × is_high_street
              + 38,824.96 × is_airport
              + 26,401.95 × is_mall
```

**R-squared: 0.8222 | Adjusted R-squared: 0.8168**

---

## Explanation of Each Coefficient

| Variable | Coefficient | Direction | Business Meaning | P-value | Significant? |
|---|---|---|---|---|---|
| **Intercept** | 73,762.67 | — | Theoretical baseline when all variables = 0; not interpretable in practice | 0.1416 | No |
| **footfall** | 33.51 | Positive | Each additional customer visit is associated with £33.51 more in monthly sales | < 0.001 | ✅ Yes |
| **marketing_spend** | 1.17 | Positive | Each additional £1 in marketing is associated with £1.17 more in monthly sales (after controlling for other factors) | < 0.001 | ✅ Yes |
| **inventory_availability_pct** | 2,954.44 | Positive | A 1 percentage point improvement in stock availability is associated with ~£2,954 more in monthly sales | < 0.001 | ✅ Yes |
| **customer_rating** | 12,808.63 | Positive | A 1-point improvement in customer satisfaction rating is associated with ~£12,809 more in monthly sales | 0.0088 | ✅ Yes |
| **avg_discount_pct** | −57,469.08 | Negative | A 1-unit (100%) increase in average discount is associated with lower sales (net negative); at typical discount ranges (e.g. 0.10), the effect is ~−£5,747 | 0.1254 | ❌ Not significant |
| **holiday_flag** | 11,148.51 | Positive | Months with a public holiday show ~£11,149 more in monthly sales on average | 0.0982 | ❌ Marginal |
| **is_high_street** | 16,295.03 | Positive | High Street stores earn ~£16,295 more per month than Residential stores, all else equal | 0.0094 | ✅ Yes |
| **is_airport** | 38,824.96 | Positive | Airport stores earn ~£38,825 more per month than Residential stores, all else equal | < 0.001 | ✅ Yes |
| **is_mall** | 26,401.95 | Positive | Mall stores earn ~£26,402 more per month than Residential stores, all else equal | 0.0001 | ✅ Yes |

---

## Dummy Variable Explanation

### Why Dummy Variables?

`store_type` is a categorical variable with 4 values: Residential, High Street, Airport, Mall. Regression requires numerical inputs, so we convert this into binary (0/1) dummy variables.

### Dummy Variable Creation

| Dummy Variable | = 1 when | = 0 when |
|---|---|---|
| `is_high_street` | store_type == "High Street" | Any other type |
| `is_airport` | store_type == "Airport" | Any other type |
| `is_mall` | store_type == "Mall" | Any other type |

### Reference Category

**Reference Category = Residential**

This category is intentionally omitted from the regression. All store type coefficients are interpreted **relative to a Residential store**. This avoids the "dummy variable trap" (perfect multicollinearity) that would occur if all 4 dummies were included simultaneously.

**How to read:** If a store is a Residential type, all three dummies equal 0, and it falls into the "baseline" group captured by the intercept.

**Example interpretation:**
- A Mall store in the same conditions as a Residential store earns an estimated **£26,402 more per month**
- An Airport store in the same conditions earns an estimated **£38,825 more per month**

---

## Final Model Selected

**Model 3 – Multiple Regression** is the final selected model.

### Reason for Selection

1. **Highest explanatory power:** R² = 0.8222 vs 0.7348 (Model 1) and 0.1574 (Model 2)
2. **Multiple business levers captured:** Covers footfall, marketing, inventory, customer rating, and store type — enabling leadership to target multiple intervention areas
3. **Dummy variables included:** Store type effects are explicitly quantified, supporting portfolio strategy decisions
4. **Statistically robust:** 7 out of 9 predictors are statistically significant at the 5% level
5. **Adjusted R² (0.8168) remains high:** The penalty for additional predictors barely reduces explanatory power, indicating the variables genuinely contribute

The model is not perfect — avg_discount_pct is not significant and the intercept is marginal — but it represents the best balance of fit, parsimony, and business interpretability available from this dataset.
