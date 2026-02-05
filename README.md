# Zepto SQL Data Analysis (MySQL)

SQL-based data analysis project on a Zepto product dataset, covering data cleaning, transformation, and business insights using MySQL.

---

## Dataset

- File: `zepto_v2.csv`
- Rows loaded: **3732**
- Data includes:
  - Category
  - Product name
  - MRP
  - Discount percent
  - Available quantity
  - Discounted selling price
  - Weight in grams
  - Out of stock flag

---

## 🛠️ Tools

- MySQL
- MySQL Workbench

---

## Workflow

1. Create database tables:
   - `zepto_raw` (staging table for CSV import)
   - `zepto` (final cleaned table)
2. Import `zepto_v2.csv` into `zepto_raw` using MySQL Workbench
3. Run `zepto_raw_load.sql` to clean and transform data into `zepto`
4. Convert prices from paise to rupees
5. Run analysis queries
6. Save results as screenshots

---

## Key Insights

### 1) Top categories by product count (Top 5)

- Cooking Essentials — **514**
- Munchies — **514**
- Ice Cream & Desserts — **388**
- Chocolates & Candies — **388**
- Packaged Food — **388**

---

### 2) Top categories by potential revenue (Top 5)

*(Potential revenue = discountedSellingPrice × availableQuantity, for in-stock items)*

- Cooking Essentials — **₹337,369.00**
- Munchies — **₹337,369.00**
- Personal Care — **₹270,849.00**
- Paan Corner — **₹270,849.00**
- Packaged Food — **₹224,385.00**

---

### 3) Data quality check

- Rows where `discountedSellingPrice > mrp`: **0**

---

## Analysis Outputs

> These images exist inside the repo in the `screenshots/` folder.

### Category Coverage
![Category Coverage](screenshots/01_category_coverage)

### Potential Revenue by Category
![Potential Revenue](screenshots/02_potential_revenue)

### Best Value Products (Price per Gram)
![Price per Gram](screenshots/03_price_per_gram)

---

## Example Queries

```sql
-- Top categories by product count
SELECT category, COUNT(*) AS products
FROM zepto
GROUP BY category
ORDER BY products DESC
LIMIT 5;

-- Potential revenue by category (in-stock only)
SELECT category,
       SUM(discountedSellingPrice * availableQuantity) AS potential_revenue
FROM zepto
WHERE outOfStock = 0
GROUP BY category
ORDER BY potential_revenue DESC
LIMIT 5;

-- Best value products (price per gram)
SELECT name, category, discountedSellingPrice, weightInGms,
       discountedSellingPrice / NULLIF(weightInGms, 0) AS price_per_gram
FROM zepto
WHERE weightInGms > 0
ORDER BY price_per_gram ASC
LIMIT 20;

-- Sanity check: discounted price should not exceed MRP
SELECT COUNT(*) AS discounted_gt_mrp
FROM zepto
WHERE discountedSellingPrice > mrp;


How to Run

Create tables (staging + final) in MySQL

Import zepto_v2.csv into zepto_raw using MySQL Workbench

Run zepto_raw_load.sql to clean and transform data into zepto

Execute analysis queries from this README or the SQL file

View results in MySQL Workbench and screenshots in screenshots/

Author

Nipun Sharma
SQL Data Analysis Project (MySQL)