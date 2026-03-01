# Customer Churn Analysis

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/your-username/customer-churn-analysis/blob/main/churn_analysis.ipynb)
![Python](https://img.shields.io/badge/Python-3.10-blue?logo=python&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-150458?logo=pandas&logoColor=white)
![Seaborn](https://img.shields.io/badge/Seaborn-Visualization-4C72B0)
![Status](https://img.shields.io/badge/Status-Complete-brightgreen)

**Author:** Pius Victor &nbsp;|&nbsp; **MSc Data Science** &nbsp;|&nbsp; March 2026

---

## What This Project Is About

This is my second data project and honestly the one where things started clicking for me.

I wanted to work on something that felt like a real business problem — not just a clean textbook dataset. Customer churn made sense because almost every company deals with it and the data is messy in ways that actually teach you something.

The question I was trying to answer: *what separates customers who stay from customers who leave, and can we spot the difference before it's too late?*

The dataset has 36,992 customer records across 24 features — demographics, transaction history, engagement behaviour, support complaints, and feedback. The target variable is `churn_risk_score` (0 = stayed, 1 = churned).

---

## Tools I Used

- **Python 3.10**
- **Pandas** — for cleaning and wrangling the data
- **NumPy** — for handling the numerical stuff
- **Matplotlib & Seaborn** — for visualisations
- **Google Colab** — where I ran everything

Nothing fancy. Just the fundamentals, used properly.

---

## The Data Was a Mess (And That Was the Point)

Before any analysis, I had to deal with a bunch of real data quality issues. This part took longer than I expected but taught me a lot:

- Some columns were completely useless (`Unnamed: 0`, `security_no`, `referral_id`) — dropped them
- `avg_frequency_login_days` had non-numeric values hiding in it — coerced to numeric and replaced errors with the median
- `days_since_last_login` had `-999` as a placeholder for missing data — replaced with median
- `avg_time_spent` had negative values which don't make sense for time — capped at the median of valid values
- Missing categorical fields got filled with `'Unknown'` so I didn't lose entire rows
- Remaining numerical nulls got median imputation

I used median over mean throughout because the data had outliers that would've skewed the mean — learned that the hard way on my first project.

---

## What I Found

### The headline number
**54.1% of customers churned.** That's not a small edge case — that's more than half the customer base gone.

### Membership tier was the biggest signal
This surprised me with how clean the split was:

| Membership Tier | Churn Rate |
|---|---|
| No Membership | >97% |
| Basic | >96% |
| Silver | Elevated |
| Gold | Moderate |
| Premium | ~0% |
| Platinum | ~0% |

Customers with no membership have almost no reason to stay loyal. Premium and Platinum members barely churn at all. The loyalty programme is clearly doing something right at the top end — but nothing is being done to bring lower-tier customers up.

### Complaints matter, but not in the obvious way
Customers who filed a complaint churned at 54.5% vs 53.7% for those who didn't. The gap is small — but I think that's because it averages out resolved and unresolved complaints together. If you could separate those, I'd expect the gap to be much wider.

### Why customers actually said they left
Looking at feedback from churned customers, the two most common reasons were:
1. Poor product quality
2. Poor customer service

Not pricing. Not competition. The basics.

### City customers churn the most
Urban customers had the highest churn of any region. My guess is more options and higher expectations — but that's worth digging into further.

---

## What the Business Should Do About It

Based on what I found, I'd suggest:

1. **Target the no-membership and basic-tier customers first.** That's where 96%+ of the churn is coming from. Even converting a small % to the next tier would make a real dent.
2. **Fix the complaints process.** Not just logging complaints — actually tracking resolution and following up. That's where the churn risk sits.
3. **Take the feedback seriously.** Product quality and customer service are cited most often. These aren't hard to improve incrementally if there's buy-in from the right teams.
4. **Keep an eye on city customers.** They're the highest-risk group by region and probably the most competitive market to retain.

---

## How to Run It

Clone the repo and you're good to go — the dataset is included.

```bash
git clone https://github.com/your-username/customer-churn-analysis.git
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
├── README.md               # You're reading it
├── churn_analysis.ipynb    # The full notebook
├── churn.csv               # Dataset used for the analysis
├── requirements.txt        # Project dependencies
└── charts/                 # Plots saved during the run
```

---

## A Note on Where I Am

This is my second GitHub project as an MSc Data Science student. I'm still building — there's a lot more I want to add to projects like this (modelling, feature importance, maybe a dashboard). But I believe in documenting what I learn as I go, not waiting until everything is perfect.

If you have feedback or just want to connect — feel free to reach out on [LinkedIn](#).
