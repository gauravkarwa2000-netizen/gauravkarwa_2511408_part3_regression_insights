# Final Business Recommendation

## Context

This recommendation is based on regression analysis of 320 store-month observations across 80 stores in 4 regions (East, North, South, West) and 4 store types (Residential, High Street, Airport, Mall). The final model (Model 3 – Multiple Regression) explains **82.2% of the variation in monthly sales** using 9 predictors.

---

## 1. Which Factors Appear Most Strongly Associated with Monthly Sales?

Based on statistical significance and coefficient magnitude, the strongest predictors are:

| Rank | Factor | Evidence |
|---|---|---|
| 1 | **Footfall (customer visits)** | Largest single predictor; R² = 0.73 alone; coefficient = £33.51 per visitor; p < 0.001 |
| 2 | **Store Type (Airport > Mall > High Street > Residential)** | Airport stores outperform Residential by ~£38,825/month; Mall by ~£26,402; High Street by ~£16,295; all highly significant |
| 3 | **Inventory Availability %** | Each 1pp improvement in stock availability = ~£2,954 additional sales; p < 0.001 |
| 4 | **Customer Rating** | Each 1-point improvement in rating = ~£12,809 additional sales; p < 0.01 |
| 5 | **Marketing Spend** | Each additional £1,000 in marketing = ~£1,174 additional sales; p < 0.001 |

---

## 2. Which Variables Should Leadership Focus On?

**Priority actions:**

### A. Drive Footfall — The #1 Lever
- Footfall is the strongest driver of sales by a significant margin
- Leadership should invest in footfall-generating strategies: in-store events, loyalty programmes, local advertising, improved accessibility (parking, public transport links), and window displays
- Every additional 1,000 visitors per month generates approximately £33,500 in sales

### B. Maximise Inventory Availability
- Stockouts cost money directly — a store at 80% availability vs 90% loses approximately £29,544/month in expected sales
- Leadership should prioritise supply chain reliability, replenishment speed, and safety stock levels especially for high-traffic stores

### C. Improve Customer Satisfaction
- Customer rating is significantly associated with sales — suggesting that satisfied customers spend more, return more often, and recommend the store
- Investment in staff training, store environment, and service quality is commercially justified

### D. Prioritise High-Performing Store Types
- Airport and Mall stores outperform Residential stores significantly, even after controlling for footfall and marketing
- New store opening decisions should favour Airport and Mall locations where possible

### E. Optimise Marketing Spend
- Marketing has a positive but modest coefficient (£1.17 per £1 spent after controlling for other factors)
- Marketing spend should be evaluated on ROI rather than volume — increasing spend without increasing footfall will have diminishing returns
- Consider whether marketing budget is more effective at driving footfall vs directly driving sales

---

## 3. Which Variables Should NOT Be Over-Interpreted?

| Variable | Caution |
|---|---|
| **avg_discount_pct** | Not statistically significant (p = 0.125). The negative coefficient suggests discounting may not help — but the result is not reliable enough to act on strongly. Further A/B testing of discount strategies is recommended before changing policy. |
| **holiday_flag** | Marginally significant (p = 0.098). Public holidays appear to boost sales, but the effect is not conclusive with this dataset size. |
| **marketing_spend** | The coefficient drops from £2.05 (simple regression) to £1.17 (multiple regression) once footfall is controlled for — suggesting some of marketing's apparent effect was really just correlating with stores that already have high traffic. |
| **customer_rating** | While significant, this variable had 8 missing values, slightly reducing sample size. Results should be validated with a complete dataset. |

---

## 4. What Business Action Would You Recommend?

### Immediate (0–3 months)
1. **Footfall audit:** Identify the 10 lowest-footfall stores and investigate why traffic is low. Develop store-specific footfall improvement plans.
2. **Inventory review:** Identify stores below 85% inventory availability and work with supply chain to improve replenishment cycles.
3. **Marketing reallocation:** Redirect marketing spend from stores where footfall is already high (and returns are diminishing) to stores with low footfall but high sales potential.

### Medium-term (3–12 months)
4. **Customer experience programme:** Launch staff training and store environment improvements, targeting stores with customer ratings below 3.5.
5. **Discount strategy review:** Commission controlled experiments (A/B testing) on discount levels to understand whether discounting drives incremental footfall and revenue or simply cannibalises margin.
6. **Store type portfolio:** In new store planning, prioritise Airport and Mall sites over Residential formats where economically viable.

### Longer-term
7. **Build a richer dataset:** Collect data on store size (sq ft), local competition score, product range breadth, and demographics to improve model accuracy.
8. **Repeat regression quarterly:** Update the model with new data to track whether the relationships remain stable over time.

---

## 5. Risks and Limitations Leadership Should Keep in Mind

| Risk | Explanation |
|---|---|
| **Omitted variables** | The model does not include store size, local population density, competition intensity, or product mix — these may be important drivers that confound current estimates |
| **Short time horizon** | Only 4 months of data (Jan–Apr 2025) are available. Seasonal effects (e.g. Christmas trading, summer patterns) are not captured |
| **Multicollinearity** | Footfall and staff_count are likely correlated; marketing_spend and footfall may be correlated. This can make individual coefficients less stable |
| **Non-linearity** | The model assumes linear relationships. In reality, the return from each additional customer visit or marketing pound likely diminishes at scale |
| **Data quality** | 14 records were excluded due to missing values. If missing data is not random, this could introduce bias |
| **Single country/chain** | Results apply to this specific retail chain's context and may not generalise to other retail environments |

---

## 6. Why Regression Shows Association, Not Causation

Regression analysis identifies **statistical associations** between variables — it does not prove that changing one variable **causes** a change in another. Several reasons prevent causal inference:

### A. Reverse Causation
- Higher-sales stores may attract more marketing investment (reverse: sales → marketing, not marketing → sales)
- High-traffic locations may attract more stores (location determines footfall, not the store creating footfall)

### B. Confounding Variables
- A third variable (e.g. affluent neighbourhood) may simultaneously drive high footfall AND high sales — making it appear that footfall "causes" sales when both are actually caused by affluence

### C. Selection Bias
- Stores were not randomly assigned to regions or types — Airport stores tend to be in high-traffic locations, Mall stores in commercial areas. The store type effect may partially reflect location quality, not format advantage

### D. Correlation ≠ Intervention Effectiveness
- Even if footfall and sales are strongly correlated historically, doubling footfall by offering a loss-leader product may not double sales if customers only come for the discounted item

**What regression does provide:** A reliable, data-driven basis for identifying *where to look* and *what hypotheses to test*. It narrows the field of variables worth investing in and provides a quantified starting point for business cases.

**Recommended next step for causal evidence:** Run controlled experiments (e.g. split-test marketing campaigns, controlled discount trials, targeted inventory improvements) to build causal evidence on top of the associational findings from this regression model.

---

## Summary

The regression evidence clearly points to **footfall, inventory availability, customer experience, and store type** as the key commercial drivers. Leadership should act on these levers while treating the discount and holiday findings with appropriate caution. All business decisions should be framed as hypotheses to be tested — the regression provides the starting map, not the final answer.
