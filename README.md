# FinTrack - Personal Expense Tracker & Budget Analyzer

A lightweight, offline command-line application written in **pure Python (standard library only)**
that helps you record expenses, set monthly category budgets, get instant overspending alerts and
analyse your spending. Built as the *Build Your Own Project* submission for **Python Essentials**.

## Overview
FinTrack stores everything in a local SQLite database. You interact with it through simple
sub-commands (`add`, `list`, `budget`, `report`, `export`, ...). It validates every input, reports
errors in plain language, logs activity to a rotating log file and ships with 38 automated tests.

## Features
| Module | What it does |
|---|---|
| **1. Expense Management** | Add, view, update, delete; filter by category/date, keyword search, sorting, limit |
| **2. Budget Management** | Monthly limit per category, OK / WARNING (>=80%) / EXCEEDED status, instant alert after `add` |
| **3. Reports & Analytics** | Monthly summary, category breakdown, costliest day, spending trend, text bar charts |
| **4. Import / Export** | Export to CSV or JSON; import CSV (bad rows skipped and reported) |

Non-functional qualities: input validation and security (parameterised SQL, whitelists), error
handling with custom exceptions and exit codes, rotating file logging, modular maintainable design,
no third-party dependencies, indexed queries for performance.

## Technologies / Python concepts used
Python 3.8+ | `sqlite3` | `argparse` | `dataclasses` | `logging` (RotatingFileHandler) | `csv` / `json` |
`re` | `datetime` | `collections.defaultdict` | `contextlib` | custom exceptions | `unittest` + `unittest.mock` |
Git. (`matplotlib` is needed **only** to regenerate the documentation diagrams in `docs/`.)

## Project structure
```
fintrack/
├── main.py                  # entry point
├── fintrack/
│   ├── cli.py               # argument parsing, command dispatch, exit codes
│   ├── expense_service.py   # Module 1 - expense CRUD/search
│   ├── budget_service.py    # Module 2 - budgets and alerts
│   ├── report_service.py    # Module 3 - analytics and text charts
│   ├── export.py            # Module 4 - CSV/JSON import & export
│   ├── database.py          # SQLite connection, schema, transactions
│   ├── validators.py        # input validation
│   ├── models.py            # dataclasses: Expense, Budget, BudgetStatus
│   ├── exceptions.py        # custom exception hierarchy
│   ├── formatting.py        # console tables and currency
│   └── logger.py            # rotating log configuration
├── tests/                   # 6 test files, 38 unit tests
├── data/sample_expenses.csv # demo data
├── docs/                    # diagrams, screenshots, generators
├── statement.md             # problem statement, scope, users, features
└── README.md
```

## Installation
```bash
git clone <your-repo-url>
cd fintrack
python --version          # must be 3.8 or newer
# no pip install needed - standard library only
```

## Usage
```bash
# expenses
python main.py add 250 food -d "Lunch" --date 2026-09-01
python main.py list --category food --sort amount
python main.py list --from 2026-09-01 --to 2026-09-30 --search lunch
python main.py update 1 --amount 300
python main.py delete 1

# budgets
python main.py budget set food 1500
python main.py budget status --month 2026-09
python main.py budget list

# reports
python main.py report summary --month 2026-09
python main.py report trend --months 6

# data
python main.py import data/sample_expenses.csv
python main.py export my_expenses.json --format json
```
Use `--db path/to/file.db` (or the `FINTRACK_DB` environment variable) to choose a database file.
Run `python main.py --help` or `python main.py <command> --help` for all options.
Exit codes: `0` success, `1` handled error (bad input, not found), `2` unexpected error.

## Testing
```bash
python -m unittest discover -s tests -t . -v
```
Tests use an in-memory database, so they never touch real data. They cover validators, CRUD,
filters and SQL-injection attempts, budget thresholds, reports, CSV/JSON round-trip and the CLI
(including error paths).

## Screenshots
See `docs/screenshots/` (add/list, budget alert, monthly report, trend/export, error handling)
and `docs/diagrams/` (architecture, workflow, use case, class, sequence, ER).

To regenerate them: `pip install matplotlib` then
`python docs/generate_diagrams.py` and `python docs/make_screenshots.py`.

## Author
Anjistha Sharma (24BCE10037) - VITyarthi, Python Essentials.
