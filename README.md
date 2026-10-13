# Customer Retention SQL Database

A relational database for the customer-retention dataset from my MSBA case competition (see
[customer-churn-prediction](https://github.com/SpencerGoss/customer-churn-prediction) for the modeling side).
It takes one flat CSV of 5,636 customers and turns it into a normalized SQLite database that is easier to
query, join and maintain.

## Schema

| Table | Holds |
|---|---|
| `customers` | Demographics and referral activity, one row per account |
| `service_subscriptions` | Internet plan, phone and add-on services, usage |
| `account_contracts` | Contract term, payment method, billing preferences, tenure |
| `billing_fees` | Monthly fee, total billed, refunds and extra charges |
| `churn_data` | Whether the customer left |

Every table links back to `customers` through a foreign key on the account reference, and indexes cover the
columns most used in churn analysis (churn flag, internet plan, contract term, tenure, payment method).

## Files

| Path | What it is |
|---|---|
| `Code/creating_tables.sql` | Table definitions, keys and indexes |
| `Code/load_data.py` | Reads the CSV with pandas and loads each table |
| `Data/retentiondata_case.csv` | The source dataset |
| `Data/retention.db` | The built database |
| `implementation_plan.md` | Design notes and what would change for production use |

## Run it

```bash
sqlite3 retention.db < Code/creating_tables.sql
python Code/load_data.py
```
