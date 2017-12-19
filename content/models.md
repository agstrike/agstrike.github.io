+++
title = "Database Models"
date = 2017-12-18T22:05:52+01:00
draft = false

[menu.main]
  name = "Database Models"
  parent = "Contributing"
  weight = 9
+++
In this page you can find documentation on how the data is structured and what the convention behind the values are.

Foreign keys that link to other database models are stored in the database in a colums called `<model_name>_id` so for the category of a Split it would be `category_id`.
In the code you can either use `obj.category` to access the category object, or `obj.category_id` to only get the id of the object.

Decimals are stored in the database with a maximum of ten digits and two decimal places.

There are a couple of integers used that are named for more readability:

### Account Types
| Name | Value | Notes |
| ---- | ----- | ----- |
| Personal | 1 | These are the accounts that are owned by the user |
| Foreign | 2 | All accounts that the user interacts with, but are not his own. |
| System | 3 | Accounts of this type are hidden from users and only used for housekeeping (initial balances, reconcilation, ...) |

### Recurrence Types

| Name | Value | Notes |
| ---- | ----- | ----- |
| Disabled | 0 | Can be used to deactivate recurrences that no longer occur. |
| Weekly | 1 |  |
| Monthly | 2 |  |
| Yearly | 3 |  |

### Transaction Types

| Name | Value | Notes |
| ---- | ----- | ----- |
| Deposit | 1 | A deposit is from a foreign account to a personal account |
| Withdraw | 2 |  A withdraw is from a personal account to a foreign account |
| Transfer | 3 | A transfer involves two personal accounts |
| System | 4 | These transactions involve one System account and are used to satisfy double bookkeeping. It's used in inital balances and reconciliation |

## Account

Represents the accounts that are part in transactions. There can't be multiple accounts with the same name and account_type.
There currently can only be one system account, this is not enforced in the database.

| Attribute | Type | Notes |
| --------- | ---- | ----- |
| name | chars (64) | The name of the account |
| account_type | integer | One of the [account types](#account-types) |
| active | boolean | whether or not the account is shown in forms, etc. Has only effect on personal accounts. |
| last_modified | datetime | Is set automatically and can't be modified |
| show_on_dashboard | boolean | Whether or not to include the account in the account listing on the dashboard. Only affects personal accounts|



## Category

Categories can be used to categorize (duh!) transactions. They are also used during budgeting.

| Attribute | Type | Notes |
| --------- | ---- | ----- |
| active | boolean | Whether or not the category is shown in forms, etc. |
| name | chars (64) | The name of the category |
| last_modified | datetime | Is set automatically and can't be modified |

## Recurring Transaction

Recurring Transactions are used to remind you of them. They can be transfers, deposits or withdrawls.

| Attribute | Type | Notes |
| --------- | ---- | ----- |
| title | chars (64) | Title of the recurrence and transaction that will be created of it |
| amount | decimal | The amount of the transaction |
| date | date | The date of the next expected ocurrence |
| src | [Account](#account) | The account that will loose the money |
| dst | [Account](#account) | The account that will gain the money |
| recurrence | integer | One of the [recurrence types](#recurrence-types) |
| transaction_type | integer | One of the [transaction types](#transaction-types) |
| category | [Category](#category) | The category of the resulting transactions |
| last_modified | datetime | Is set automatically and can't be modified |


## Transaction
| Attribute | Type | Notes |
| --------- | ---- | ----- |
| title | chars (64) | Title of the transaction |
| date | date | the date when the transaction happened |
| recurrence | [Recurring Transaction](#recurring-transaction) | `NULL` if the transaction is not associated with a recurring transaction |
| transaction_type | integer | One of the [transaction types](#transaction-type) |
| notes | Text | |
| last_modified | datetime | Is set automatically and can't be modified |


## Split
| Attribute | Type | Notes |
| --------- | ---- | ----- |
| title | chars (64) | Title of the split, if the transaction is a simple transaction, it should match the title of the transaction |
| amount | decimal | The amount of the transaction.  A positive amount is a deposit into the account, a negative is a withdrawal from the account  |
| date | date | date the transaction was registered in the source account |
| account | [Account](#account) | The account where the amount is added or deducted from. |
| opposing_account | [Account](#account) | The opposing account |
| transaction | [Transaction](#transaction) | The transaction this split belongs to |
| category | [Category](#category) | Optional. Can be used to categorize transactions and to assign budgets to them. |
| last_modified | datetime | Is set automatically and can't be modified |

