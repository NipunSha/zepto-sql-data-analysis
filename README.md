# Zepto SQL Data Analysis (MySQL)

This project analyzes a Zepto product dataset using MySQL. The objective is to clean the data, transform it into an analysis-ready format, and generate basic business insights related to category coverage, revenue potential, and pricing efficiency.

---

## Dataset

- File: `zepto_v2.csv`
- Rows loaded: 3732
- Key fields:
  - Category
  - Product name
  - MRP
  - Discount percent
  - Available quantity
  - Discounted selling price
  - Weight in grams
  - Out-of-stock flag

---

## Tools Used

- MySQL
- MySQL Workbench

---

## Workflow

1. Created staging and final tables (`zepto_raw` and `zepto`) in MySQL  
2. Imported `zepto_v2.csv` into the staging table using MySQL Workbench  
3. Cleaned and transformed the data into the final table  
4. Converted prices from paise to rupees  
5. Ran analysis queries for reporting  
6. Saved results as screenshots

---

## Key Findings

### Top categories by product count (Top 5)

- Cooking Essentials — 514  
- Munchies — 514  
- Ice Cream & Desserts — 388  
- Chocolates & Candies — 388  
- Packaged Food — 388  

---

### Top categories by potential revenue (Top 5)

Potential revenue is calculated as: discountedSellingPrice × availableQuantity (for in-stock items).

- Cooking Essentials — ₹337,369  
- Munchies — ₹337,369  
- Personal Care — ₹270,849  
- Paan Corner — ₹270,849  
- Packaged Food — ₹224,385  

---

### Data Quality Check

- Number of products where discounted price is greater than MRP: 0

---

## Analysis Outputs

Screenshots of the query results are stored in the `screenshots/` folder.

- Category Coverage  
  ![Category Coverage](screenshots/01_category_coverage)

- Potential Revenue by Category  
  ![Potential Revenue](screenshots/02_potential_revenue)

- Best Value Products (Price per Gram)  
  ![Price per Gram](screenshots/03_price_per_gram)

---

## How to Run

1. Create staging and final tables in MySQL  
2. Import `zepto_v2.csv` into `zepto_raw` using MySQL Workbench  
3. Run `zepto_raw_load.sql` to clean and transform data into `zepto`  
4. Run analysis queries in MySQL Workbench  
5. Review results in MySQL Workbench and the `screenshots/` folder  

---

## Author

Nipun Sharma  
SQL Data Analysis Project (MySQL)
