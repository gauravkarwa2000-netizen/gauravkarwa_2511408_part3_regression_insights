# Residual Analysis

## Overview

This document presents the residual analysis for **Model 3 (Multiple Regression)** — the final selected model. Residuals are calculated as:

> **Residual = Actual Monthly Sales − Predicted Monthly Sales**

A positive residual means the store **outperformed** the model's prediction. A negative residual means the store **underperformed** relative to what the model expected.

---

## Model Performance Summary

| Metric | Value |
|---|---|
| R-squared | 0.8222 |
| Adjusted R-squared | 0.8168 |
| Observations used | 306 (after removing 14 rows with missing values) |
| Dependent Variable | monthly_sales |

---

## Top 5 Records with Largest Positive Residuals

*(Store outperformed model prediction — actual sales were much higher than predicted)*

| Store ID | Actual Sales (£) | Predicted Sales (£) | Residual (£) | Store Type | Region |
|---|---|---|---|---|---|
| STR-1028 | 713,611 | 610,719 | +102,892 | Mall | East |
| STR-1069 | 686,738 | 585,971 | +100,767 | High Street | West |
| STR-1030 | 820,519 | 723,692 | +96,827 | Residential | West |
| STR-1059 | 723,305 | 631,961 | +91,344 | Residential | West |
| STR-1075 | 763,162 | 673,604 | +89,558 | High Street | West |

### Business Interpretation – Positive Residuals

Stores with large positive residuals are **systematically outperforming** what their observable characteristics (footfall, marketing, inventory, store type) would predict. This can mean:

- **Unmeasured advantages:** These stores may benefit from local factors not captured in the dataset — e.g., nearby transport hubs, demographic affluence, or strong store manager performance
- **Loyalty effects:** Long-established stores with a loyal customer base may convert higher revenue per visit
- **Product mix advantages:** A well-curated product range not reflected in the dataset could drive premium spending
- **West region outperformance:** 4 of the 5 top positive residuals are in the West region, suggesting the model may be slightly under-predicting West region stores — a possible systematic pattern

**Action:** Leadership should investigate these stores as potential case studies and "best practice" benchmarks. What are they doing differently that others can replicate?

---

## Top 5 Records with Largest Negative Residuals

*(Store underperformed model prediction — actual sales were much lower than predicted)*

| Store ID | Actual Sales (£) | Predicted Sales (£) | Residual (£) | Store Type | Region |
|---|---|---|---|---|---|
| STR-1017 | 685,379 | 844,579 | −159,200 | High Street | West |
| STR-1023 | 627,172 | 761,203 | −134,031 | Mall | South |
| STR-1012 | 595,468 | 707,298 | −111,830 | Residential | West |
| STR-1009 | 641,865 | 742,894 | −101,029 | Residential | North |
| STR-1007 | 800,452 | 898,283 | −97,831 | Mall | West |

### Business Interpretation – Negative Residuals

Stores with large negative residuals are **underperforming** relative to their predicted potential. Given their traffic, marketing, and inventory levels, the model expected higher sales. Possible explanations include:

- **Operational issues:** Poor customer experience or checkout inefficiencies that reduce conversion rate despite high footfall
- **Conversion rate gaps:** High footfall but low purchase conversion — customers visiting but not buying
- **Product mix mismatch:** Store may be stocked with wrong items for the local demographic
- **External shocks:** Local construction, road closures, or competition not captured in the model
- **High discount backfiring:** Some underperforming stores may have relied on deep discounting that eroded revenue despite traffic

**Action:** Leadership should investigate these stores for operational or structural issues. A site visit and conversion rate audit may reveal actionable improvements.

---

## Systematic Patterns in Residuals

| Observation | Finding |
|---|---|
| West region bias | Positive residuals cluster in West; some large negatives also in West — the West region has high variance not fully captured |
| Mall stores | Mall stores appear in both tails — the model's average "Mall premium" (£26,402) masks significant individual store variation |
| High Street | STR-1017 has the largest underprediction, suggesting a single month or operational issue rather than a structural flaw |
| Model under-predicts | 5 positive residuals range from £89K to £103K; 5 negative residuals range from £98K to £159K — suggesting the model underestimates variance at extremes |

---

## Under-Prediction vs Over-Prediction Patterns

**The model appears to slightly under-predict stores in the West region** (4 of top 5 positive residuals) and **over-predict high-footfall stores that have low conversion** (STR-1017, STR-1007 — high footfall Mall/High Street stores with unexpectedly low sales).

This suggests two possible model improvements:
1. Adding a **West region dummy** variable to capture region-specific effects beyond store type
2. Including a **conversion rate** variable (sales per footfall visit) as a predictor, if data becomes available

---

## Conclusion

The residual analysis confirms that Model 3 performs well overall but reveals that store-level idiosyncrasies — particularly in the West region and among high-footfall stores — are not fully explained by the included predictors. These residuals are valuable diagnostic signals for leadership to act upon at the individual store level.
