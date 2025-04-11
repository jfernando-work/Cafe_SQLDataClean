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
| `location`        | Either In-Store or Takeaway                      |
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
   - Calculated `price_per_unit` for any fields that were left empty.
   - Replaced empty strings with NULLs where appropriate.
   - Calculated any instances where `quantity` was missing.

4. **Date Formatting**
   - Converted `transaction_date` into a proper DATE or TIMESTAMP format.
   - Made sure `price_per_unit` field had the correct number of decimals.
   - Removed or flagged invalid date entries.
   - Extracted Day and Month values from the `transaction_date` field.

5. **Duplicates & Outliers**
   - Identified and removed duplicate transactions.

---

## 🧪 Sample Queries Used

```sql
-- Subquery to create a table with items / pries. Join that back with all rows.
UPDATE public."Cafe_Sales" AS cs
SET "PricePerUnit_Cleaned" = prices."PricePerUnit_Cleaned"
FROM (
    SELECT DISTINCT "Item_Cleaned", "PricePerUnit_Cleaned"
    FROM public."Cafe_Sales"
    WHERE "Item_Cleaned" IS NOT NULL
    AND "PricePerUnit_Cleaned" IS NOT NULL
) AS prices
WHERE cs."Item_Cleaned" = prices."Item_Cleaned" 
AND cs."PricePerUnit_Cleaned" IS NULL;


-- Calculate the PricePerUnit_Cleaned for missing values.
UPDATE public."Cafe_Sales"
SET "PricePerUnit_Cleaned" = ROUND("TotalSpent_Cleaned" / "Quantity_Cleaned", 1)
WHERE "PricePerUnit_Cleaned" IS NULL;
