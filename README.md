# Customer Churn Analysis

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/profpius/customer-churn-analysis/blob/main/churn_analysis.ipynb)
![Python](https://img.shields.io/badge/Python-3.10-blue?logo=python&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-150458?logo=pandas&logoColor=white)
![Seaborn](https://img.shields.io/badge/Seaborn-Visualization-4C72B0)
![Status](https://img.shields.io/badge/Status-Complete-brightgreen)

**Author:** Pius Victor &nbsp;|&nbsp; March 2026

---

## What This Project Is About

This is my first data project and honestly the one where things started clicking for me.

I wanted to work on something that felt like a real business problem, not just a clean textbook dataset. Customer churn made sense because almost every company deals with it and the data is messy in ways that actually teach you something.

The question I was trying to answer: *what separates customers who stay from customers who leave, and can we spot the difference before it's too late?*

The dataset has 36,992 customer records across 24 features including demographics, transaction history, engagement behaviour, support complaints, and feedback. The target variable is `churn_risk_score` (0 = stayed, 1 = churned).

---

## Tools I Used

- **Python 3.10**
- **Pandas** — for cleaning and wrangling the data
- **NumPy** — for handling the numerical stuff
- **Matplotlib & Seaborn** — for visualisations
- **Google Colab** — where I ran everything

Nothing really fancy. Just the fundamentals, used properly.

---

## The Data Was a Mess (And That Was the Point)

Before any analysis, I had to deal with a bunch of real data quality issues. This part took longer than I expected but taught me a lot:

- Some columns were completely useless (`Unnamed: 0`, `security_no`, `referral_id`) and I dropped them
- `avg_frequency_login_days` had non-numeric values hiding in it — I coerced it to numeric and replaced errors with the median
- `days_since_last_login` had `-999` as a placeholder for missing data — I replaced it with the median
- `avg_time_spent` had negative values which made no sense for time, so I capped them at the median of valid values
- Missing categorical fields got filled with `'Unknown'` so I didn't lose entire rows
- Remaining numerical nulls got median imputation

I used median over mean throughout because the data had outliers that would've skewed the mean, which I learnt the hard way while practising.

---

## What I Found

### The headline number

**54.1% of customers churned.** That's not a small edge case — that's more than half the customer base gone.

---

### Membership tier was the biggest signal

This surprised me with how clean the split was:

| Membership Tier | Churn Rate |
|---|---|
| No Membership | 97.1% |
| Basic Membership | 96.8% |
| Silver Membership | 42.8% |
| Gold Membership | 37.0% |
| Platinum Membership | 0.0% |
| Premium Membership | 0.0% |

The split is dramatic. No Membership and Basic customers churn at almost 97% — they are essentially guaranteed to leave. Platinum and Premium members churn at 0% — perfect retention. The loyalty programme works at the top but completely fails to catch customers at the bottom.

---

### Age had almost no effect

Churn rate was essentially flat across all age groups:

| Age Group | Churn Rate |
|---|---|
| Under 20 | 53.2% |
| 20-30 | 54.1% |
| 30-40 | 55.0% |
| 40-50 | 53.7% |
| 50+ | 54.5% |

The variation is just 1.8 percentage points across the entire range. Age is not a useful predictor of churn in this dataset.

---

### Complaint history was a major signal

Customers who filed a complaint churned at **71.7%** vs **36.9%** for those who didn't. That's a 34.8 percentage point gap and one of the clearest signals in the data. If a customer raised a complaint and it wasn't resolved well, they were far more likely to leave.

---

### Why customers actually said they left

| Feedback Reason | Churned Customers |
|---|---|
| Poor Product Quality | 5,642 |
| Poor Customer Service | 4,758 |
| No reason specified | 3,609 |
| Too many ads | 2,763 |
| Products always in Stock | 1,182 |
| Reasonable Price | 997 |
| User Friendly Website | 571 |
| Quality Customer Care | 385 |

Not pricing. Not competition. The basics.

---

## What the Business Should Do About It

1. **Target no-membership and basic-tier customers first.** These two groups have the highest churn rates (62% and 59.6%). Even moving a fraction of them to the next tier would make a measurable dent.
2. **Fix product quality and customer service.** These are the two most cited reasons churned customers gave. They are not abstract problems — they are fixable with the right internal buy-in.
3. **Take complaint resolution seriously.** The 71.7% churn rate among customers with complaints vs 36.9% without tells you that how you handle a complaint matters as much as whether it was filed.

---

## How to Run It

Clone the repo and you're good to go — the dataset is included.

```bash
git clone https://github.com/profpius/customer-churn-analysis.git
cd customer-churn-analysis
pip install -r requirements.txt
jupyter notebook churn_analysis.ipynb
```

Or hit the **Open in Colab** badge at the top.

---

## Folder Structure

```
customer-churn-analysis/
│
├── README.md                  # You're reading it
├── churn_analysis.ipynb       # The full notebook
├── churn.csv                  # Dataset used for the analysis
├── requirements.txt           # Project dependencies
└── churn_analysis_charts.pdf  # All 5 charts exported from the notebook
```

---

## A Note on Where I Am

This is my first GitHub project and I'm still building. There's a lot more I want to add to projects like this — modelling, feature importance, maybe a dashboard. But I believe in documenting what I learn as I go, not waiting until everything is perfect.

If you have feedback or just want to connect, find me on [LinkedIn](https://linkedin.com/in/victor-pius-4061a9332).
