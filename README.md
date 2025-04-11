# 🧹 SQL Data Cleaning – Cafe Transactions

This project focuses on cleaning and preparing raw transactional data from a cafe using SQL. The dataset includes item purchases (e.g., coffee, cake, cookies) with details such as quantity, pricing, location, and payment method.

---

## 📂 Project Overview

### 📌 Objective
To clean and standardize a raw dataset for accurate analysis and reporting. This includes:
- Removing inconsistencies
- Handling missing or invalid values
- Formatting fields properly
- Creating clean, analysis-ready tables

---

## 🧾 Data Fields

The dataset contains the following fields:

| Field Name        | Description                                      |
|-------------------|--------------------------------------------------|
| `item`            | Name of the purchased item (e.g., coffee, cake)  |
| `quantity`        | Number of items purchased                        |
| `price_per_unit`  | Price of a single item                           |
| `total_spent`     | Total amount spent in the transaction            |
| `payment_method`  | How the customer paid (e.g., cash, card)         |
| `location`        | Either in store or takeaway                      |
| `transaction_date`| Date of the transaction                          |

---

## 🛠️ Cleaning Tasks Performed

1. **Standardized Text Fields**
   - Trimmed whitespace from `item`, `payment_method`, and `location`.
   - Corrected typos and inconsistent spellings.

2. **Fixed Numeric Fields**
   - Ensured `quantity`, `price_per_unit`, and `total_spent` are stored as numeric types.
   - Recalculated `total_spent` where values were incorrect (`quantity * price_per_unit`).

3. **Handled Missing or Null Values**
   - Imputed or removed rows with missing essential data (e.g., missing `item` or `price`).
   - Replaced empty strings with NULLs where appropriate.

4. **Date Formatting**
   - Converted `transaction_date` into a proper DATE or TIMESTAMP format.
   - Removed or flagged invalid date entries.

5. **Duplicates & Outliers**
   - Identified and removed duplicate transactions.
   - Flagged outliers (e.g., very high quantity or total_spent).

---

## 🧪 Sample Queries Used

```sql
-- Example: Standardizing item names
UPDATE transactions
SET item = LOWER(TRIM(item));

-- Example: Fixing incorrect total_spent
UPDATE transactions
SET total_spent = quantity * price_per_unit
WHERE total_spent IS NULL OR total_spent != quantity * price_per_unit;
