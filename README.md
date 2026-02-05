# Zepto SQL Data Analysis (MySQL)

SQL-based data analysis project on a Zepto product dataset, covering data cleaning, transformation, and business insights using MySQL.

---

## 📦 Dataset

- File: `zepto_v2.csv`  
- Rows loaded: **3732**  
- Data includes:
  - Category
  - Product name
  - MRP
  - Discount %
  - Available quantity
  - Discounted selling price
  - Weight in grams
  - Out of stock flag
  - Quantity

---

## 🛠️ Tools Used

- MySQL  
- MySQL Workbench  

---

## 🔁 Workflow

1. Created database and tables (`zepto_raw` and `zepto`)
2. Imported CSV into staging table (`zepto_raw`)
3. Cleaned and transformed data into final table (`zepto`)
4. Converted prices from paise to rupees
5. Handled nulls, types, and boolean fields
6. Ran analysis queries for business insights

---

## 📊 Key Insights

### 1️⃣ Top Categories by Product Count

- Cooking Essentials — 514  
- Munchies — 514  
- Ice Cream & Desserts — 388  
- Chocolates & Candies — 388  
- Packaged Food — 388  

### 2️⃣ Top Categories by Potential Revenue

- Cooking Essentials — 337,369  
- Munchies — 337,369  
- Personal Care — 270,849  
- Paan Corner — 270,849  
- Packaged Food — 224,385  

### 3️⃣ Data Quality Check

- Products where discounted price > MRP: **0** ✅  
  (No pricing anomalies found)

---

## 📈 Analysis Outputs

### Category Coverage
![Category Coverage](screenshots/01_category_coverage)

### Potential Revenue by Category
![Potential Revenue](screenshots/02_potential_revenue)

### Best Value Products (Price per Gram)
![Price per Gram](screenshots/03_price_per_gram)

---

## 🧪 Example Queries

```sql
-- Top categories by product count
SELECT category, COUNT(*) AS products
FROM zepto
GROUP BY category
ORDER BY products DESC
LIMIT 5;

-- Potential revenue by category
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
