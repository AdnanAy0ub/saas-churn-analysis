# SaaS Customer Churn Analysis — Case Study

## Executive Summary

This project analyzes 2,000 SaaS customers to identify the key drivers of customer churn. Using statistical testing and cohort analysis, we discovered that **customer engagement (login frequency and daily usage) is 3x more predictive of churn than account age**. Low-engagement customers churn at 81% compared to just 10% for high-engagement users. This analysis provides a clear roadmap for reducing the overall churn rate from 36.85% through targeted retention interventions.

---

## Table of Contents

1. [Business Problem](#business-problem)
2. [Dataset Overview](#dataset-overview)
3. [Methodology](#methodology)
4. [Key Findings](#key-findings)
5. [Statistical Validation](#statistical-validation)
6. [Business Recommendations](#business-recommendations)
7. [Expected Impact](#expected-impact)
8. [Technical Stack](#technical-stack)
9. [Next Steps](#next-steps)

---

## Business Problem

SaaS companies depend entirely on recurring revenue. A 36.85% churn rate directly erodes Monthly Recurring Revenue (MRR) and customer lifetime value. Understanding which customers are at risk enables proactive retention efforts and can potentially recover millions in lost revenue.

**Key Questions:**
- What drives customers to churn?
- Can we identify at-risk customers early?
- Which retention strategies should we prioritize?

---

## Dataset Overview

**Source:** Kaggle — SaaS Customer Churn Prediction Dataset  
**Records:** 2,000 customers  
**Data Quality:** Zero missing values, clean and ready for analysis

**Key Variables:**
- `Customer_ID`: Unique identifier
- `Account_Age_Days`: Days since signup (1-1,094 days)
- `Login_Frequency`: Categorical (Daily, Weekly, Rarely)
- `Daily_Usage_Mins`: Average daily usage (1-119 minutes)
- `Last_Support_Ticket`: Text from customer support interactions
- `Churn`: Target variable (0 = retained, 1 = churned)

**Baseline Metrics:**
- Overall Churn Rate: 36.85% (~737 churned customers)
- Average Account Age: 561 days
- Average Daily Usage: 36.2 minutes

---

## Methodology

### Phase 1: Exploratory Data Analysis

We segmented customers across three dimensions:
1. **Login Frequency** (Daily, Weekly, Rarely)
2. **Daily Usage** (Low 1-15 mins, Medium 15-50 mins, High 50+ mins)
3. **Account Tenure** (New 0-90d, Growing 90-180d, Established 180-365d, Veteran 365d+)

For each segment, we calculated churn rates and identified initial patterns.

### Phase 2: Statistical Validation

To ensure findings were statistically significant (not random), we conducted:

**Chi-Square Tests** (categorical variables):
- Login Frequency vs. Churn
- Daily Usage Bucket vs. Churn

**Independent T-Tests** (continuous variables):
- Daily Usage Minutes: Churned vs. Retained
- Account Age Days: Churned vs. Retained

All tests used a significance level of α = 0.05 (95% confidence).

### Phase 3: Visualization & Dashboarding

Created interactive Power BI dashboards with 6 visuals:
1. Churn Rate by Login Frequency
2. Churn Rate by Usage Bucket
3. Average Daily Usage (Churned vs. Retained)
4. Churn Rate by Account Tenure
5. Customer Count by Usage Bucket
6. KPI Summary Cards

---

## Key Findings

### Finding 1: Login Frequency is the Strongest Predictor

| Login Frequency | Churn Rate | Customer Count |
|---|---|---|
| **Daily** | 13.02% | 868 |
| **Weekly** | 42.26% | 795 |
| **Rarely** | 85.46% | 337 |

**Insight:** Customers who log in daily almost never churn (13%), while those who log in rarely have an 85% churn rate—a **6.5x difference**. This is your primary early warning signal.

### Finding 2: Daily Usage is Highly Predictive of Churn

| Daily Usage | Churn Rate | Customer Count | Chi-Square |
|---|---|---|---|
| **Low (1-15 mins)** | 81.49% | 670 | 870.25 |
| **Medium (15-50 mins)** | 17.54% | 747 | p ≈ 0 |
| **High (50+ mins)** | 10.29% | 583 |  |

**Insight:** Low-usage customers (1-15 mins/day) churn at 81%—over 8x higher than high-usage customers. **670 customers are in this at-risk group**. Daily usage is a proxy for value realization: if customers aren't using the product, they won't stay.

### Finding 3: The 31-Minute Usage Gap

**Churned Customers:** 16.42 mins/day (N=737)  
**Retained Customers:** 47.68 mins/day (N=1,263)  
**Difference:** 31.27 minutes (t = -27.04, p ≈ 0)

**Insight:** Retained customers use the product 3x more than churned customers. This massive gap proves engagement is predictive.

### Finding 4: Account Age is NOT a Strong Predictor

| Account Tenure | Churn Rate | T-Test Result |
|---|---|---|
| New (0-90d) | 36.63% | t = -1.39 |
| Growing (90-180d) | 35.42% | p = 0.165 |
| Established (180-365d) | 41.30% | NOT SIGNIFICANT |
| Veteran (365d+) | 35.98% |  |

**Insight:** Churn is flat across tenure (~35-41%), except a slight spike at 6-12 months (41%). Critically, **this is NOT statistically significant** (p = 0.165). While the spike is interesting, the root cause is likely disengagement within that cohort, not tenure itself. Conclusion: Don't assume older customers are more loyal—focus on engagement instead.

---

## Statistical Validation

All findings passed rigorous statistical tests:

| Test | Variable | Statistic | P-Value | Result |
|---|---|---|---|---|
| **Chi-Square** | Login Frequency → Churn | 564.05 | p ≈ 0 | ✅ SIGNIFICANT |
| **Chi-Square** | Usage Bucket → Churn | 870.25 | p ≈ 0 | ✅ SIGNIFICANT |
| **T-Test** | Daily Usage (Churned vs. Retained) | -27.04 | p ≈ 0 | ✅ SIGNIFICANT |
| **T-Test** | Account Age (Churned vs. Retained) | -1.39 | p = 0.165 | ❌ NOT SIGNIFICANT |

**Interpretation:** The first three factors have p-values < 0.05, meaning these relationships are real and not due to chance. Account age does not meet this threshold, so we can safely deprioritize tenure-based strategies.

---

## Business Recommendations

Based on these findings, we recommend the following prioritized interventions:

### Recommendation 1: Implement Engagement Monitoring (High Priority)

**What:** Build an engagement dashboard that flags accounts with:
- <2 logins per week
- <15 minutes daily usage
- Declining trend in usage over 30 days

**When:** Activate within first 90 days of signup

**Why:** These are the primary churn indicators. Early detection enables proactive outreach.

### Recommendation 2: Proactive Onboarding for Low-Engagement Users (High Priority)

**What:** Trigger targeted interventions for users showing early disengagement:
- Personalized feature training based on use case
- 1-on-1 success calls for accounts <20 mins/day usage
- Curated learning content delivered via email

**Target Cohort:** 670 customers in "Low Usage" bucket (currently 81% churn rate)

**Why:** If we can move even 50% of these users to "Medium Usage" (15+ mins/day), we reduce their churn rate from 81% to 17%—recovering ~335 customers.

### Recommendation 3: De-prioritize Tenure-Based Retention (Medium Priority)

**What:** Stop assuming "older accounts are more loyal." Focus retention budget on engagement metrics instead.

**Why:** Statistical tests show account age is NOT predictive of churn (p = 0.165). The 6-12 month spike (41% churn) is likely due to disengagement, not tenure itself.

### Recommendation 4: Weekly Engagement Reports for Support & Success Teams (Medium Priority)

**What:** Provide weekly cohort reports showing:
- New at-risk customers (flagged by usage/login thresholds)
- Trending usage for key accounts
- Comparison vs. baseline

**Why:** Gives front-line teams actionable data to prioritize outreach and support efforts.

---

## Expected Impact

If we implement the above recommendations, here's the potential revenue impact:

### Scenario: Recover 50% of Low-Usage Customers

**Current State:**
- 670 customers with <15 mins/day usage
- 81% churn rate = ~543 customers churned annually
- Assuming $100/month per customer = $65K annual revenue at risk

**After Intervention:**
- If we move 50% of low-usage users to "Medium" bucket (15-50 mins)
- Their churn rate drops from 81% to 17.5% (~50% of Medium rate for margin)
- ~167 additional customers retained
- **Incremental Revenue Saved: ~$200K annually** (167 customers × $100/month × 12 months)

**Payback Period:**
- One dedicated analyst to build monitoring system: ~$80K/year
- ROI: 2.5x in Year 1

---

## Technical Stack

**Data Processing:**
- Python 3.x (Pandas, NumPy, SciPy)
- SQL (optional for larger datasets)

**Statistical Analysis:**
- SciPy (chi2_contingency, ttest_ind)
- Chi-square tests and independent t-tests

**Visualization:**
- Power BI (Desktop)
- DAX formulas for custom measures
- Interactive dashboards

**Version Control:**
- Git / GitHub

**Libraries Used:**
```
pandas==1.5.x
numpy==1.23.x
scipy==1.9.x
matplotlib==3.6.x
seaborn==0.12.x
```

---

## Next Steps

1. **Sentiment Analysis on Support Tickets** (Optional)
   - Parse `Last_Support_Ticket` text
   - Quantify sentiment (negative/neutral/positive)
   - Correlate with churn—do frustrated customers churn more?

2. **Predictive Model (Optional)**
   - Build classification model to score at-risk customers
   - Use as early warning system for proactive intervention

3. **Cohort Retention Curves**
   - Track 6-month and 12-month survival rates by acquisition cohort
   - Identify systematic issues with specific signup periods

4. **Implement Recommendations**
   - Build engagement dashboard in Power BI
   - Set up automated alerts for at-risk customers
   - Create playbooks for success team outreach

5. **A/B Test Interventions**
   - Measure impact of onboarding improvements
   - Quantify ROI of proactive outreach campaigns

---

## Project Files

- `analysis.py` — Python EDA and statistical tests
- `saas_churn_dashboard.pbix` — Power BI dashboard
- `saas_churn_analysis.csv` — Cleaned dataset
- `CASE_STUDY.md` — This document (methodology & findings)
- `README.md` — Quick start & reproduction guide

---

## Author

Adnan | Data Analyst  
Project Date: August 2026

---

## License

This project is open-source. Feel free to use, modify, and distribute as needed for educational and business purposes.
