# SaaS Customer Churn Analysis

**Identifying and Preventing Customer Churn in SaaS Using Data Analysis**

A comprehensive analysis of 2,000 SaaS customers to determine what drives churn and actionable recommendations for retention.

---

## Quick Summary

We analyzed 2,000 SaaS customers and discovered:

✅ **Engagement (login frequency + daily usage) is 3x more predictive than account age**

- Daily login users churn at 13% vs. rarely-logging users at 85%
- Low-usage customers (1-15 mins/day) churn at 81% vs. high-usage at 10%
- Retained users average 47.7 mins/day; churned users only 16.4 mins/day

💡 **Actionable Insight:** 670 at-risk customers identified in low-usage cohort. Implementing proactive engagement interventions could recover ~335 customers and save $200K+ annually.

---

## Project Structure

```
saas-churn-analysis/
├── README.md                      # This file
├── CASE_STUDY.md                  # Full methodology & findings
├── CASE_STUDY.docx                # Professional Word version
├── analysis.ipynb                    # Python EDA + statistical tests
├── saas_churn_dashboard.pbix      # Power BI dashboard
├── data/
│   └── saas_churn_analysis.csv    # Cleaned dataset (2,000 rows)
│   └── dashboard data   	   # Data after Python Analysis (2,000 rows)
└── dashboards/
    └── dashboard_screenshot.png   # Dashboard visual
```

---

## Key Findings at a Glance

### 1. Login Frequency Drives Churn
| Frequency | Churn Rate | Interpretation |
|-----------|-----------|---|
| Daily | 13% | 🟢 Keep users engaged |
| Weekly | 42% | 🟡 At-risk, needs attention |
| Rarely | 85% | 🔴 Critical intervention needed |

### 2. Daily Usage is Highly Predictive
| Usage Level | Churn Rate | Customer Count |
|---|---|---|
| Low (1-15 mins) | 81% | 670 (HIGH RISK) |
| Medium (15-50 mins) | 18% | 747 (Safe) |
| High (50+ mins) | 10% | 583 (Loyal) |

### 3. Statistical Significance Confirmed
- **Login Frequency:** χ² = 564, p ≈ 0 ✅
- **Daily Usage:** χ² = 870, p ≈ 0 ✅
- **Account Age:** t = -1.39, p = 0.165 ❌ (NOT significant)

---

## Dashboard

Interactive Power BI dashboard showing:
- Churn rate by login frequency
- Churn rate by usage bucket
- Daily usage distribution (churned vs. retained)
- Churn by account tenure
- Customer count by usage level
- Key metric KPIs

**Screenshot:**
<img width="1513" height="851" alt="dashboard_screenshot" src="https://github.com/user-attachments/assets/3ba32b4f-f0f6-4b9e-90af-38cb6b2d4fcd" />



---

## How to Reproduce

### Prerequisites
- Python 3.8+
- Pandas, NumPy, SciPy
- Power BI Desktop (for dashboard)
- Git

### Step 1: Clone Repository
```bash
git clone https://github.com/AdnanAy0ub/saas-churn-analysis.git
cd saas-churn-analysis
```

### Step 2: Install Dependencies
```bash
pip install pandas numpy scipy matplotlib seaborn
```

### Step 3: Run Analysis
```bash
python analysis.py
```

This will:
- Load the dataset
- Perform exploratory data analysis (EDA)
- Run Chi-square and t-tests
- Generate summary statistics
- Print all findings to console

**Expected Output:**
```
Dataset Shape: (2000, 8)
Overall Churn Rate: 36.85%

Churn by Login Frequency:
Daily      13.02%
Weekly     42.26%
Rarely     85.46%

Statistical Tests:
Login Frequency → Churn: χ² = 564.05, p ≈ 0 ✅ SIGNIFICANT
Daily Usage → Churn: χ² = 870.25, p ≈ 0 ✅ SIGNIFICANT
Account Age → Churn: t = -1.39, p = 0.165 ❌ NOT SIGNIFICANT
```

### Step 4: Open Dashboard
1. Open Power BI Desktop
2. Load `saas_churn_dashboard.pbix`
3. Interact with visuals and filters

---

## Business Recommendations

### Priority 1: Implement Engagement Monitoring
- Flag accounts with <2 logins/week or <15 mins daily usage
- Activate monitoring within first 90 days of signup
- Create automated alerts for success team

### Priority 2: Proactive Onboarding for Low-Usage Users
- Target the 670 customers in "Low Usage" cohort (81% churn)
- Offer personalized training, 1-on-1 calls, curated content
- Goal: Move 50% to "Medium Usage" = recover ~335 customers

### Priority 3: De-prioritize Tenure-Based Retention
- Account age is NOT predictive (statistically insignificant)
- Focus budget on engagement metrics instead

### Expected Impact
- Recover ~335 customers annually from low-usage cohort
- Save ~$200K in annual recurring revenue
- ROI: 2.5x with one dedicated analyst

---

## Dataset

**Source:** [Kaggle SaaS Customer Churn Dataset](https://www.kaggle.com/datasets/suhanigupta04/saas-customer-churn-prediction-dataset)

**Columns:**
- `Customer_ID`: Unique identifier
- `Name`: Customer name
- `Email`: Customer email
- `Account_Age_Days`: Days since signup (1-1,094)
- `Login_Frequency`: Daily / Weekly / Rarely
- `Daily_Usage_Mins`: Average daily usage in minutes (1-119)
- `Last_Support_Ticket`: Text from recent support interaction
- `Churn`: Target (0 = retained, 1 = churned)

**Quality:** 2,000 rows, zero missing values, clean and ready for analysis

---

## Technical Approach

### Analysis Phases
1. **Exploratory Data Analysis (EDA)**
   - Segment customers by login frequency, usage, and tenure
   - Calculate churn rates per segment
   - Identify patterns and anomalies

2. **Statistical Validation**
   - Chi-square tests for categorical variables
   - Independent t-tests for continuous variables
   - Confidence level: 95% (α = 0.05)

3. **Visualization & Dashboarding**
   - Power BI interactive dashboards
   - 6 visuals + 4 KPI cards
   - Drill-down capabilities for deeper exploration

### Tools Used
- **Python:** Data processing and statistical analysis
- **Power BI:** Interactive dashboarding and visualization
- **SciPy:** Chi-square and t-tests
- **Pandas:** Data manipulation and aggregation

---

## Key Insights for Interviews

This project demonstrates:

✅ **End-to-end analytical thinking** — Problem definition → EDA → Hypothesis testing → Recommendations

✅ **Statistical rigor** — Chi-square and t-tests prove findings are significant, not coincidental

✅ **Business acumen** — Moves beyond "here's the data" to "here's what we should DO" with expected ROI

✅ **Technical depth** — SQL, Python, Power BI, statistical testing all in one project

✅ **Communication** — Translates complex statistics into actionable business recommendations

---

## Next Steps

1. **Sentiment Analysis** — Parse support ticket text, correlate sentiment with churn
2. **Predictive Modeling** — Build classification model to score at-risk customers
3. **Retention Curves** — Cohort analysis tracking 6-month and 12-month survival
4. **A/B Testing** — Measure impact of onboarding and engagement interventions
5. **Production Implementation** — Deploy engagement dashboard and automated alerts

---

## Questions?

For methodology details, see `CASE_STUDY.md`

For reproducibility guide, see this README

For professional summary, see `CASE_STUDY.docx`

---

## 📜 License
MIT — feel free to fork, star, and use in your portfolio.


## 🙋 About Me

**ADNAN AYOUB DAR** from Srinagar J&K
| Data Analyst | Passionate about turning raw data into business insights

[![LinkedIn](https://img.shields.io/badge/LinkedIn-Connect-blue?style=flat&logo=linkedin)](https://www.linkedin.com/in/adnan-ayoub-dar-5ba528267/)
[![GitHub](https://img.shields.io/badge/GitHub-Follow-black?style=flat&logo=github)](https://github.com/AdnanAy0ub)

---


**Project Author:** Adnan | Data Analyst  
**Date:** August 2026  
**Dataset:** Kaggle (SaaS Customer Churn)
