# HW5 — Advanced SQL with PostgreSQL

## Overview

This project demonstrates advanced SQL techniques using PostgreSQL. The notebook implements a multi-stage analytical pipeline for customer behavior analysis, recursive queries, materialized views, and query execution plan analysis.

The project uses the Brazilian E-Commerce Public Dataset by Olist when the dataset is available. A deterministic synthetic dataset is used as a fallback when the original data cannot be downloaded.

## Technologies

- Python
- PostgreSQL 16
- SQLAlchemy
- pandas
- psycopg2
- Google Colab

## Implementation

### 1. Multi-Stage CTE Pipeline

The analytical pipeline uses Common Table Expressions (CTEs) to organize the transformations into logical stages:

- Order-level monetary calculations
- Customer RFM (Recency, Frequency, Monetary) features
- Customer cohort analysis by quarter
- Rolling 30-day average order value
- Customer cancellation rate
- Revenue analysis by product category
- Preferred product category identification

A stable reference date is used to ensure reproducible recency calculations.

### 2. Recursive CTE

A recursive Common Table Expression explores referral relationships. The implementation includes cycle prevention and a maximum recursion depth to avoid infinite traversal.

### 3. Materialized View

A materialized view stores the results of the analytical pipeline. A unique index supports concurrent refresh operations.

The notebook demonstrates refreshing the view with:

`REFRESH MATERIALIZED VIEW CONCURRENTLY`

### 4. Query Performance Analysis

The notebook uses `EXPLAIN` to inspect query execution plans for:

- The full analytical pipeline
- Queries against the materialized view

The plans can be used to compare execution strategies and understand the potential performance benefits of precomputed results.

## How to Run

1. Open the notebook in Google Colab.
2. Run the setup cells to install the required Python packages and PostgreSQL 16.
3. Start PostgreSQL and create the project database.
4. Load the Olist dataset, or use the fallback synthetic dataset if the original files are unavailable.
5. Execute the notebook cells in order.
6. Review the validation results, recursive query output, materialized view, and `EXPLAIN` plans.

**Note:** The notebook is designed for Google Colab. PostgreSQL must be running before the database queries are executed. Database objects are created within the PostgreSQL instance started by the notebook.

## Repository Contents

- `HW5_Olist_SQL.ipynb` — notebook containing the implementation, validation queries, and performance analysis.
- `README.md` — project overview and execution instructions.

## Results and Reflection

The notebook validates the generated customer-level features and demonstrates the use of CTEs, recursive queries, materialized views, and execution plans.

The final reflection should be based on the actual query plans and execution results obtained during the notebook run. Performance conclusions should reflect the observed output rather than assumed improvements.

## Author

Completed as part of an SQL assignment on advanced PostgreSQL features.
