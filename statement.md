# Project Statement - FinTrack

## Problem Statement
Students and young professionals often lose track of where their money goes. Notes apps and
memory do not give a reliable monthly picture, spreadsheets need manual formulas, and most
finance apps are heavy, account-based and require internet access. As a result people overspend
in a category (food, entertainment, transport) and only find out at the end of the month.

**FinTrack** is a lightweight, offline, command-line application written in pure Python that lets a
user record expenses, set monthly category budgets, receive instant overspending alerts and view
analytical reports - all stored safely in a local SQLite database.

## Scope
**In scope**
- Add, view, search, filter, sort, update and delete expenses
- Monthly budget per category with OK / WARNING (80 %) / EXCEEDED status and instant alerts
- Monthly summary, category breakdown, spending trend and text-based bar charts
- CSV / JSON export and CSV import with row-level error reporting
- Input validation, error handling, rotating log file, automated unit tests

**Out of scope (future enhancements)**
- Multi-user accounts and authentication, cloud sync, graphical or web interface
- Multi-currency conversion, receipt scanning, bank integration

## Target Users
- College students managing a monthly allowance
- Early-career professionals who want a simple private budget tool
- Beginners who want a clean example of a modular Python application

## High-Level Features
1. **Expense Management** - full CRUD, keyword search, date/category filters, sorting
2. **Budget Management** - per-category monthly limits, status tracking, real-time alerts
3. **Reports & Analytics** - monthly summary, category share, trend over months, top expenses
4. **Import / Export** - CSV and JSON export, CSV import that skips and reports bad rows
5. **Cross-cutting** - validation, custom exceptions, logging, parameterised SQL, unit tests
