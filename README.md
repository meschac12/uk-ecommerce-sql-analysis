# UK E-Commerce Sales & Customer Analysis (SQL)

## Overview

This project analyses two years of transactional data from a UK-based online retailer to answer commercial questions a business stakeholder would actually ask: where is revenue coming from, which customers matter most, and where is the business losing customers.

The analysis is written entirely in SQL (SQLite, via `ipython-sql` in Jupyter), structured around six business questions rather than open-ended exploration. Each query is paired with a short interpretation of what the result means for the business — not just what the numbers are.

**Dataset:** [Online Retail II (UCI Machine Learning Repository)](https://archive.ics.uci.edu/dataset/502/online+retail+ii) — ~1 million transaction-level records from a UK-based online retailer, December 2009 to December 2011. Each row represents one product line within an invoice, including invoice number, product code, description, quantity, invoice date, unit price, customer ID, and country.

## Business Questions Answered

1. **Revenue trends** — How is revenue moving month over month, and what does the growth rate tell us?
2. **Customer segmentation (RFM)** — Which customers are most valuable, using Recency, Frequency, and Monetary value?
3. **Top products** — What sells the most by volume versus by revenue, and why do the two answers differ?
4. **Customer retention** — What percentage of customers return after their first purchase?
5. **Regional performance** — Which countries drive the most revenue, and is the business overly reliant on one market?
6. **Churn risk** — Which previously active customers have gone quiet, and should be flagged for re-engagement?

## Techniques Used

- Multi-table joins
- Aggregations: `SUM`, `COUNT`, `AVG`, `GROUP BY`, `HAVING`
- Window functions: `RANK()`, `LAG()`, running totals
- Common Table Expressions (CTEs) for readable, layered logic
- Date-based filtering and time-series aggregation
- Subqueries for cohort-style retention analysis

## Tools

- Python, Jupyter Notebook
- SQLite (via `ipython-sql` / `%%sql` magic)
- Pandas (for lightweight result formatting and chart prep)
- Matplotlib/Seaborn (for visualising query outputs)

## Files

- `notebook.ipynb` — Full analysis: setup, all six business questions, query outputs, and written interpretation of each result
- `data/online_retail_II.csv` — Source dataset (not committed if over GitHub's size limit; download link provided in notebook)
- `requirements.txt` — Python dependencies

## Key Findings

| Question | Finding |
|---|---|
| Revenue trend | Strong Q4 seasonality — November is the peak month in both years (£1.17M in Nov 2010, £1.16M in Nov 2011) |
| Customer segmentation | The top 30% of customers ("Champions" by RFM score) generate ~81% of total revenue (£14.4M of £17.7M) |
| Top products | Revenue leaders and volume leaders are different products — e.g. a 3-tier cake stand leads on revenue, while a low-cost novelty item leads on units sold |
| Retention | 72.39% of customers are repeat buyers — retention is a strength of the business, not a weak point |
| Regional performance | 82.98% of revenue comes from the UK alone — a real market concentration risk |
| Churn risk | 384 previously loyal customers (3+ past orders) have gone quiet for 90–180 days, including accounts worth over £26K in lifetime value |

## How to Run

1. Clone this repository
2. Install dependencies: `pip install -r requirements.txt`
3. Download the dataset from the UCI link above (or [Kaggle mirror](https://www.kaggle.com/datasets/lakshmi25npathi/online-retail-dataset)) and place the `.xlsx` file in `data/online_retail_II.xlsx` — the raw file is ~45MB and not committed to this repository
4. Open `notebook.ipynb` and run all cells — this rebuilds the SQLite database from scratch on each run

> **Note:** The notebook in this repository has already been run once with full outputs visible, so the analysis can be reviewed directly on GitHub without re-running it.
