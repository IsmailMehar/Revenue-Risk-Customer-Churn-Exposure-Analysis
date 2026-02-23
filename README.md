# Customer Churn Risk & Revenue Exposure Analysis

**Domain:** Customer Analytics / Commercial Performance  
**Tools:** Power BI, DAX, Power Query  
**Duration:** 1 Week  
**Live Dashboard:** [Power BI Service Link]  
**Dataset:** Synthetic / anonymised transactional data  

---

## Overview

This project quantifies the financial exposure associated with customer churn by linking transaction recency to expected revenue loss.

Rather than reporting churn rate in isolation, the analysis focuses on identifying where revenue is at risk, which customer segments drive expected loss, and when retention interventions should occur.

The dashboard answers:

- How much revenue is already lost vs. at risk?
- How does churn risk escalate as transaction gaps widen?
- Which recency segments contribute most to expected revenue loss?
- What is the optimal trigger point for retention efforts?

---

## Business Problem

The business generates approximately $590M in revenue, yet churn was being tracked only as a percentage metric without financial context.

Leadership needed clarity on:

- The revenue concentration within inactive customers
- The financial magnitude of potential future churn
- Which customer segments should be prioritised for intervention

The objective was to translate churn into revenue exposure and provide a prioritisation framework.

---

## Data & Model Design

### Data

Transactional customer-level dataset including:
- Revenue
- Sessions
- Transaction counts
- Days since last transaction

Data was cleaned and transformed using Power Query. All sensitive information has been anonymised.

### Model Design

A star schema model was implemented with:

- Fact table: Customer transactions
- Dimensions: Customer attributes, recency segmentation

Customers were grouped into **Recency Segments**:
- 0–15 days
- 15–30 days
- 30–45 days
- 45+ days

These segments form the foundation of the risk and exposure analysis.

---

## Key Measures (DAX)

```DAX
Total Revenue = SUM(Fact[Revenue])

Churn Rate % =
DIVIDE(
    [Churned Customers],
    [Total Customers]
)

Revenue At Risk =
CALCULATE(
    [Total Revenue],
    Fact[Recency Segment] IN {"30–45", "45+"}
)

Risk Weighted Revenue =
[Total Revenue] * [Churn Rate %]

Risk Contribution % =
DIVIDE(
    [Risk Weighted Revenue],
    CALCULATE([Risk Weighted Revenue], ALL(Fact[Recency Segment]))
)
```

These measures shift the focus from churn percentage to **expected revenue exposure**.

---

## Analysis & Insights

Churn represents a material financial risk, not merely a behavioural metric.

Approximately **$221M of revenue sits within customers inactive for more than 30 days**, accounting for 37% of total revenue.  

Churn probability increases sharply as inactivity widens. Customers inactive for over 45 days are **2.7x more likely to churn** than recently active customers.  

The **30–45 day segment contributes the largest share of expected revenue loss**, making it the most commercially critical intervention point.

Total expected revenue exposure was estimated at **~$64M**, with a potential recovery opportunity of ~$20M through targeted retention.

---

## Business Impact

This analysis provides a prioritised retention framework based on financial exposure.

Instead of broad campaigns across all customers, the business can:

- Trigger intervention workflows at 30 days of inactivity
- Focus retention spend on high-impact segments
- Reduce expected revenue loss before customers reach high-risk thresholds

The project shifts churn monitoring from reactive reporting to proactive revenue protection.

---

## Repository Structure

```
/customer-churn-revenue-exposure/
│
├── Reports/
│   ├── Churn_Risk_Dashboard.pbix
│   └── Dashboard_Screenshots/
│
├── Data/
│   └── Sample_Anonymised_Data.csv
│
├── Writeups/
│   └── Project_Case_Study.pdf
│
└── README.md
```

---

## Dashboard Preview

*(Insert 2–3 screenshots here)*

- Executive Overview
- Behavioural Drivers
- Revenue Risk Contribution
- Retention Strategy Framework

---

## Assumptions & Limitations

Churn was defined based on inactivity patterns.  
External variables such as pricing, competition, or seasonality were not incorporated.  
Revenue exposure estimates assume historical churn probabilities remain stable.

---

## Skills Demonstrated

- Commercial KPI design
- Recency segmentation logic
- Financial impact modelling
- Risk-weighted revenue calculation
- Executive-level dashboard storytelling
- DAX measure design and optimisation

---

## Contact

For questions or discussion regarding this project:

[LinkedIn Profile Link]  
[Email Address]
