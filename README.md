# UK E-Commerce Sales and Customer Analysis (SQL)

SQL analysis of 1M+ UK e-commerce transactions answering six business questions a stakeholder would actually ask — revenue trends, RFM customer segmentation, churn risk, and regional performance — written entirely in SQL using CTEs and window functions.

**The full analysis with query outputs and written interpretations is visible directly in [`notebook.ipynb`](./notebook.ipynb) — no setup needed.**

---

## Dataset

**Online Retail II** (UCI Machine Learning Repository) — approximately 1 million transaction-level records from a UK-based online retailer, December 2009 to December 2011. Each row is one product line within an invoice: invoice number, product code, description, quantity, invoice date, unit price, customer ID, and country.

---

## Business questions answered

Rather than open-ended exploration, the analysis is structured around six questions a business stakeholder would bring to a data analyst:

| # | Question | What it reveals |
|---|----------|----------------|
| 1 | **Revenue trends** | Month-over-month movement and growth rate |
| 2 | **Customer segmentation (RFM)** | Which customers are most valuable by Recency, Frequency and Monetary value |
| 3 | **Top products** | Volume leaders vs revenue leaders — and why they differ |
| 4 | **Customer retention** | What percentage of customers return after their first purchase |
| 5 | **Regional performance** | Which countries drive revenue and whether the business is over-reliant on one market |
| 6 | **Churn risk** | Previously active customers who have gone quiet and should be flagged for re-engagement |

---

## Key findings

| Question | Finding |
|----------|---------|
| Revenue trend | Strong Q4 seasonality — November is the peak month in both years (£1.17M in Nov 2010, £1.16M in Nov 2011) |
| Customer segmentation | The top 30% of customers by RFM score generate 81% of total revenue (£14.4M of £17.7M) |
| Top products | Revenue leaders and volume leaders are completely different products — a 3-tier cake stand leads on revenue while a low-cost novelty item leads on units sold |
| Retention | 72.39% of customers are repeat buyers — retention is a strength, not a weak point |
| Regional performance | 82.98% of revenue comes from the UK alone — a real market concentration risk |
| Churn risk | 384 previously loyal customers (3+ past orders) have gone quiet for 90 to 180 days, including accounts worth over £26K in lifetime value |

---

## SQL techniques used

- Common Table Expressions (CTEs) for layered, readable logic
- Window functions: `RANK()`, `LAG()`, running totals with `SUM() OVER`
- RFM scoring: Recency, Frequency and Monetary value combined into a single customer tier
- Cohort-style retention analysis using subqueries and date filtering
- Time-series aggregation for month-over-month revenue and growth rate
- `HAVING` clauses for filtering on aggregated results
- Multi-step churn identification: loyal customers defined, then filtered for recent silence

---

## Tools

| Tool | Purpose |
|------|---------|
| Python + Jupyter | Analysis environment |
| SQLite via ipython-sql | All queries run as `%%sql` cells directly in the notebook |
| Pandas | Lightweight result formatting |
| Matplotlib / Seaborn | Visualising query outputs |

---

## Files

- `notebook.ipynb` — Full analysis: all six business questions, SQL queries, outputs, and written interpretation of each result. Pre-run with full outputs visible on GitHub.
- `data/online_retail_II.csv` — Source dataset (not committed due to size — download link in notebook)
- `requirements.txt` — Python dependencies

---

## How to run locally

```bash
git clone https://github.com/meschac12/uk-ecommerce-sql-analysis
cd uk-ecommerce-sql-analysis
pip install -r requirements.txt
```

Download the dataset from the [UCI Machine Learning Repository](https://archive.ics.uci.edu/dataset/502/online+retail+ii) and place the `.xlsx` file at `data/online_retail_II.xlsx`. Then open `notebook.ipynb` and run all cells — this rebuilds the SQLite database from scratch on each run.

---

*Built by Meschac Goredji *
