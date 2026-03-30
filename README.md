# Customer Churn Analysis

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/profpius/customer-churn-analysis/blob/main/churn_analysis.ipynb)
![Python](https://img.shields.io/badge/Python-3.10-blue?logo=python&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-150458?logo=pandas&logoColor=white)
![Seaborn](https://img.shields.io/badge/Seaborn-Visualization-4C72B0)
![Status](https://img.shields.io/badge/Status-Complete-brightgreen)

**Author:** Pius Victor &nbsp;|&nbsp; March 2026

---

## What This Project Is About

This is my first data project and the one where things started clicking for me. I wanted to work on something that felt like a real business problem, not just a clean textbook dataset. Customer churn made sense because almost every company deals with it, and the data is messy in ways that actually teach you something.

The question I set out to answer: *what separates customers who stay from customers who leave, and can we spot the difference before it is too late?*

The dataset contains 36,992 customer records across 24 features, including demographics, transaction history, engagement behaviour, support complaints, and feedback. The target variable is `churn_risk_score` (0 = stayed, 1 = churned).

---

## Tools Used

- **Python 3.10**
- **Pandas** for cleaning and wrangling the data
- **NumPy** for handling numerical operations
- **Matplotlib & Seaborn** for visualisations
- **Google Colab** as the runtime environment

Nothing fancy. Just the fundamentals, used properly.

---

## The Data Was a Mess (And That Was the Point)

Before any analysis, I had to work through a number of real data quality issues. This stage took longer than expected but was one of the most instructive parts of the project.

- **Dropped useless columns:** `Unnamed: 0`, `security_no`, and `referral_id` contained no useful information.
- **Fixed a mixed-type column:** `avg_frequency_login_days` had non-numeric values hiding in it. These were coerced to numeric, with errors replaced by the median.
- **Replaced sentinel values:** `days_since_last_login` used `-999` as a placeholder for missing data. These were replaced with the median.
- **Capped invalid values:** `avg_time_spent` had negative values, which make no sense for a time measure. These were capped at the median of valid values.
- **Filled missing categoricals:** Missing categorical fields were filled with `'Unknown'` to avoid losing entire rows.
- **Median imputation throughout:** Remaining numerical nulls received median imputation. The data had enough outliers that using the mean would have skewed results, which I learned the hard way while practising.

---

## What I Found

### The Headline Number

**54.1% of customers churned.** This is not a small edge case. More than half the customer base left, which makes churn the central operational problem for this business.

---

### Membership Tier Was the Strongest Signal

The relationship between membership tier and churn rate was the clearest finding in the dataset. The split is dramatic and almost perfectly monotonic.

| Membership Tier | Churn Rate |
|---|---|
| No Membership | 97.1% |
| Basic Membership | 96.8% |
| Silver Membership | 42.8% |
| Gold Membership | 37.0% |
| Platinum Membership | 0.0% |
| Premium Membership | 0.0% |

Customers without a membership or on the Basic tier churn at nearly 97%. Platinum and Premium members churn at 0%. The loyalty programme works extremely well at the top end but provides no retention benefit for customers at the bottom. This is where the biggest opportunity lies.

---

### Age Had Almost No Effect

Churn rate was essentially flat across all age groups, varying by just 1.8 percentage points across the full range. Age is not a useful predictor of churn in this dataset.

| Age Group | Churn Rate |
|---|---|
| Under 20 | 53.2% |
| 20–30 | 54.1% |
| 30–40 | 55.0% |
| 40–50 | 53.7% |
| 50+ | 54.5% |

---

### Complaint History Was a Major Signal

Customers who filed a complaint churned at **71.7%** versus **36.9%** for those who did not. That is a 34.8 percentage point gap and one of the clearest signals in the data. How a complaint gets handled matters as much as whether it was filed at all.

---

### Why Customers Said They Left

| Feedback Reason | Churned Customers |
|---|---|
| Poor Product Quality | 5,642 |
| Poor Customer Service | 4,758 |
| No reason specified | 3,609 |
| Too many ads | 2,763 |
| Products always in stock | 1,182 |
| Reasonable price | 997 |
| User-friendly website | 571 |
| Quality customer care | 385 |

Not pricing. Not competition. The basics.

---

## What the Business Should Do About It

1. **Target no-membership and basic-tier customers first.** These two groups have churn rates above 96%. Even moving a small fraction of them into the Silver tier would produce a measurable improvement in overall retention.
2. **Fix product quality and customer service.** These are the two most cited reasons churned customers gave. They are specific, operational problems that can be addressed with the right internal prioritisation.
3. **Take complaint resolution seriously.** The gap between 71.7% churn among customers with complaints and 36.9% without shows that unresolved complaints are a direct driver of churn. Improving how complaints are handled is a lever that is available immediately.

---

## How to Run It

Clone the repository and you are good to go. The dataset is included.

```bash
git clone https://github.com/profpius/customer-churn-analysis.git
cd customer-churn-analysis
pip install -r requirements.txt
jupyter notebook churn_analysis.ipynb
```

Alternatively, click the **Open in Colab** badge at the top to run everything in the browser with no local setup required.

---

## Folder Structure

```
customer-churn-analysis/
│
├── README.md                  # You're reading it
├── churn_analysis.ipynb       # The full analysis notebook
├── churn.csv                  # Dataset used for the analysis
├── requirements.txt           # Project dependencies
└── churn_analysis_charts.pdf  # All 5 charts exported from the notebook
```

---

## A Note on Where I Am

This is my first GitHub project and I am still building. There is a lot more I want to add to projects like this, including modelling, feature importance, and possibly a dashboard. I believe in documenting what I learn as I go rather than waiting until everything is polished.

If you have feedback or want to connect, find me on [LinkedIn](https://linkedin.com/in/victor-pius-4061a9332).
