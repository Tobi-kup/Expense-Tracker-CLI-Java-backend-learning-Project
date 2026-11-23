# Expense Tracker (Java CLI)

A small command-line expense tracker. No external dependencies

## Build

```
javac -encoding UTF-8 Expense.java ExpenseStore.java ExpenseTracker.java
```

## Usage

```
java ExpenseTracker add     --description "Lunch" --amount 12.50 [--category Food]
java ExpenseTracker update  --id 1 [--description "..."] [--amount 15] [--category Food]
java ExpenseTracker delete  --id 1
java ExpenseTracker list    [--category Food]
java ExpenseTracker summary [--month 8] [--category Food]
java ExpenseTracker budget  --month 8 --amount 500
java ExpenseTracker export  [--file out.csv] [--category Food]
java ExpenseTracker help
```

- `summary` without options shows the total of all expenses plus a per-category breakdown.
- `summary --month N` covers month N (1-12) of the current year and shows the budget status if one is set.
- A warning is printed whenever a month's spending exceeds its budget (after `add`, `update`, `budget` and `summary`).
- Categories are optional (default: `General`) and filtering is case-insensitive.

## Data

Files are created in the directory you run the program from:

- `expenses.csv` – `id,date,description,amount,category`
- `budgets.csv` – `month,budget` (budgets apply to the current year's months)

## Validation

Rejected with a clear message: non-positive or non-numeric amounts, more than 2 decimal places,
empty descriptions, unknown/non-numeric IDs, months outside 1-12, missing option values,
unknown commands, and corrupt data files.

## Code layout

- `Expense.java` – data model
- `ExpenseStore.java` – CSV persistence, validation and business logic (add/update/delete/totals/budgets/export)
- `ExpenseTracker.java` – argument parsing, output formatting, command dispatch
