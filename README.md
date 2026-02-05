# Zepto SQL Data Analysis (MySQL)

SQL-based data analysis project on a Zepto product dataset, covering data loading, cleaning, paise→rupees conversion, and business-focused insights.

## Dataset
- File: `zepto_v2.csv`
- Rows loaded: 3732

## Tools
- MySQL
- MySQL Workbench

## Workflow
1. Load CSV into staging table (`zepto_raw`)
2. Transform and type-cast into final table (`zepto`)
3. Clean invalid rows and convert prices from paise to rupees
4. Run analysis queries for insights

## Key Insights (from analysis)
### Top categories by product count
- Cooking Essentials — 514  
- Munchies — 514  
- Ice Cream & Desserts — 388  
- Chocolates & Candies — 388  
- Packaged Food — 388  

### Top categories by potential revenue (proxy)
- Cooking Essentials — 337,369  
- Munchies — 337,369  
- Personal Care — 270,849  
- Paan Corner — 270,849  
- Packaged Food — 224,385  

### Data quality check
- Products where discounted price > MRP: **0** ✅

## How to run
1. Create tables (staging + final)
2. Import CSV into `zepto_raw` (Workbench import)
3. Run transformation + cleaning SQL
4. Run analysis queries

## Author
Nipun Sharma
