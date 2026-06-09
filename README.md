# SQL Case Studies

A portfolio project working through 5 SQL case studies using **PostgreSQL** and **Jupyter notebooks** with the `%%sql` magic command.

## Tech Stack

- **Database**: PostgreSQL
- **Notebook engine**: Jupyter (via `jupysql` / `%%sql` magic)
- **Environment**: Python 3.12 managed by `uv`
- **Editor**: VSCode

## Project Structure

```
.
├── case_study_1/
│   ├── schema.sql        # DDL + seed data
│   └── solution.ipynb    # Questions + SQL answers
├── case_study_2/
├── case_study_3/
├── case_study_4/
├── case_study_5/
├── pyproject.toml        # uv dependencies
├── .env.example          # Postgres connection template
└── README.md
```

## Setup

### 1. Clone & install dependencies

```bash
git clone <repo-url>
cd "SQL Case Studies"
uv sync
```

This creates a `.venv/` and installs all dependencies pinned in `pyproject.toml`.

### 2. Configure Postgres connection

```bash
cp .env.example .env
# Edit .env with your local Postgres credentials
```

Create the database:

```bash
psql -U postgres -c "CREATE DATABASE sql_case_studies;"
```

### 3. Load schema for a case study

```bash
psql -U postgres -d sql_case_studies -f case_study_1/schema.sql
```

### 4. Open the notebook in VSCode

- Open `case_study_1/solution.ipynb`
- When prompted for a kernel, pick the `.venv` interpreter
- Run all cells

## Case Studies

| # | Case Study | Skills | Status |
|---|------------|--------|--------|
| 1 | [IPL 2025 Player Auction](case_study_1/solution.ipynb) | Window functions, CTEs, correlated subqueries, conditional aggregation | Completed |
| 2 | [T20I Match Analysis (2024)](case_study_2/solution.ipynb) | Window functions (`RANK`), CTEs, string parsing (`split_part`), date functions, `UNION`, win-rate calculation | Completed |

More case studies will be added as they are completed.

### Case Study 1 — IPL 2025 Player Auction

Analysis of the 2025 IPL player auction (228 players across 10 franchises) covering team spending patterns, player valuation by role, and Indian vs. overseas pricing. Ten questions answered in PostgreSQL using window functions (`ROW_NUMBER`, `FIRST_VALUE`, `SUM/AVG OVER`), CTEs, correlated subqueries, and conditional aggregation with `CASE` expressions. Each query is paired with the thought process behind it and a short interpretation of the result.

### Case Study 2 — T20I Match Analysis (2024)

Analysis of international T20I match results from 2024 covering head-to-head records, team win rankings, winning-margin trends, chasing performance, and venue dominance. Ten questions answered in PostgreSQL using window functions (`RANK` with `PARTITION BY`), CTEs, string parsing with `split_part` to extract numeric margins from text, date functions, `UNION`-based match counting, and null-safe win-rate calculation. Each query is paired with the reasoning behind it and a short interpretation of the result.

## How `%%sql` Magic Works

Each notebook loads the SQL extension and connects to Postgres:

```python
%load_ext sql
%sql postgresql://user:pass@localhost:5432/sql_case_studies
```

Then run any SQL query in a cell with `%%sql`:

```sql
%%sql
SELECT * FROM customers LIMIT 5;
```

Results render as a pandas-style table inline.
