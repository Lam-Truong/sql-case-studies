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

| # | Case Study | Status |
|---|------------|--------|
| 1 | IPL 2025 Player Auction | In progress |

More case studies will be added as they are completed.

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
