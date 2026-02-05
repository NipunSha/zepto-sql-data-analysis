# Zepto SQL Data Analysis (MySQL)

SQL-based analysis on a Zepto product dataset, covering **data loading, cleaning, transformations**, and **business insights** using MySQL Workbench.

---

## Dataset

- File: `zepto_v2.csv`
- Rows loaded into final table (`zepto`): **3732**

---

## Tools

- MySQL
- MySQL Workbench

---

## Workflow (what this project does)

1. **Create database + tables**
   - `zepto_raw` (staging table where CSV is imported)
   - `zepto` (final cleaned table)

2. **Import CSV into `zepto_raw`**
   - Done via MySQL Workbench import (since `LOAD DATA LOCAL INFILE` may be disabled)

3. **Transform + clean**
   - Convert numeric columns from text → numeric
   - Convert `outOfStock` into boolean-style 0/1
   - Optional: remove zero/invalid price rows

4. **Convert prices**
   - Prices were in **paise**, converted to **rupees** (`/100`)

5. **Run analysis queries**
   - Category coverage
   - Potential revenue by category
   - Best value products (price per gram)

---

## Key Insights

### 1) Top categories by product count (Top 5)
- Cooking Essentials — **514**
- Munchies — **514**
- Ice Cream & Desserts — **388**
- Chocolates & Candies — **388**
- Packaged Food — **388**

### 2) Top categories by potential revenue (Top 5)
*(Potential revenue = discountedSellingPrice × availableQuantity, for in-stock items)*

- Cooking Essentials — **337,369.00**
- Munchies — **337,369.00**
- Personal Care — **270,849.00**
- Paan Corner — **270,849.00**
- Packaged Food — **224,385.00**

### 3) Data quality check
- Rows where `discountedSellingPrice > mrp`: **0**

---

## Analysis Outputs

> These images should exist inside the repo at `screenshots/` with the exact filenames below.

### Category Coverage
![Category Coverage](screenshots/01_category_coverage.png)

### Potential Revenue by Category
![Potential Revenue](screenshots/02_potential_revenue.png)

### Best Value Products (Price per Gram)
![Price per Gram](screenshots/03_price_per_gram.png)

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

-- Sanity: discounted price should not exceed MRP
SELECT COUNT(*) AS discounted_gt_mrp
FROM zepto
WHERE discountedSellingPrice > mrp;

```md

---

## How to Run

1. Create tables (staging + final) in MySQL
2. Import `zepto_v2.csv` into `zepto_raw` using MySQL Workbench
3. Run `zepto_raw_load.sql` to clean and transform data into `zepto`
4. Execute analysis queries from the README or SQL file
5. View results in MySQL Workbench and screenshots in `/screenshots`

---

## Author

**Nipun Sharma**  
SQL Data Analysis Project (MySQL)
