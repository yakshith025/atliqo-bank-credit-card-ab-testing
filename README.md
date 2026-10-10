# AtliQo Bank: Credit Card Launch Analysis and A/B Test

End-to-end banking analytics project: find the right customer segment for a new credit card, then prove with a statistically powered A/B test that the card increases spending.

## Results at a glance

- **Target segment:** customers aged **18–25 (~25% of the base)** are under-served. They rarely pay by credit card, earn under ₹50k, have thin credit history, and spend mostly on electronics, fashion and beauty via Amazon, Flipkart and Alibaba.
- **A/B test:** the new card raised the mean daily average transaction from **₹221.18 to ₹235.98**. A right-tailed two-sample Z-test gave **Z = 2.75, p = 0.003**, so the uplift is significant.

## Phase 1: Customer analysis

- **Data:** 1,000 customers, their credit profiles and 500,000 transactions (CSV files, or a MySQL dump).
- **Cleaning:** occupation-wise median imputation of missing income; outlier and zero handling for age, credit limit and transaction amount.
- **EDA:** demographic, income, credit-limit and spending-category breakdowns to locate the under-served segment above.

## Phase 2: A/B test

- **Power analysis** (α = 0.05, power = 0.8): detecting a 0.4 SD effect needs about 100 customers per group, which fits the campaign budget.
- **Campaign:** 2 months (Sep–Oct 2023). Compared the daily average transaction amount of control and test groups.

| Group | Mean daily avg transaction | SD |
|---|---|---|
| Control (existing card) | ₹221.18 | 21.36 |
| Test (new card) | ₹235.98 | 36.66 |

Right-tailed two-sample Z-test: **Z = 2.75** (critical value 1.645), **p = 0.003**. The null hypothesis is rejected.

## Repository structure

```
code/
├── phase1_customer_analysis.ipynb   EDA, cleaning, target segment
├── phase2_ab_test.ipynb             power analysis + Z-test
└── analysis.png, image.png          figures embedded in phase 2
data/
├── customers.csv, credit_profiles.csv, transactions.csv
├── avg_transactions_after_campaign.csv
└── E_MasterCardDump.sql             same data as a MySQL dump (optional)
```

## Getting started

```bash
pip install -r requirements.txt
cd code
jupyter notebook
```

Run the notebooks from inside `code/`; they read `../data/`. The MySQL import is optional and needs `mysql-connector-python`.

## Tools

Python, pandas, NumPy, Matplotlib, seaborn, statsmodels, SciPy, MySQL
