NIKE VS ADIDAS EXECUTIVE DASHBOARD - PORTFOLIO DATASET
============================================================

All data in this package is SYNTHETIC / DEMO DATA created for portfolio and dashboard practice.
Do not present it as actual Nike or Adidas financial, market-share, sales, or customer data.

STAR-SCHEMA RELATIONSHIPS
-------------------------
dim_brand.Brand_ID       1 -> many dim_product.Brand_ID
dim_category.Category_ID 1 -> many dim_product.Category_ID
dim_product.Product_ID   1 -> many fact_sales.Product_ID
dim_date.Date_ID         1 -> many fact_sales.Date_ID
dim_region.Region_ID     1 -> many fact_sales.Region_ID
dim_channel.Channel_ID   1 -> many fact_sales.Channel_ID

dim_brand.Brand_ID       1 -> many fact_marketing.Brand_ID
dim_date.Date_ID         1 -> many fact_marketing.Date_ID
dim_region.Region_ID     1 -> many fact_marketing.Region_ID

dim_product.Product_ID   1 -> many fact_reviews.Product_ID
dim_date.Date_ID         1 -> many fact_reviews.Date_ID
dim_brand.Brand_ID       1 -> many fact_reviews.Brand_ID
dim_category.Category_ID  1 -> many fact_reviews.Category_ID

dim_product.Product_ID   1 -> many fact_inventory.Product_ID
dim_date.Date_ID         1 -> many fact_inventory.Date_ID
dim_region.Region_ID     1 -> many fact_inventory.Region_ID

PORTFOLIO ANALYSIS IDEAS
------------------------
1. Revenue vs Units Sold
2. Price vs Units Sold (scatter / relationship)
3. Marketing Spend vs Revenue
4. Discount vs Units Sold
5. Product Rating vs Revenue
6. Positive Sentiment vs Revenue
7. Gross Profit and Gross Margin by Brand
8. Revenue by Category and Region
9. Inventory Stockouts vs Lost-sales proxy
10. Top products by revenue / profit
11. Monthly revenue growth
12. Brand market-position comparison

KEY POWER BI MEASURES
---------------------
Total Revenue = SUM(fact_sales[Revenue_USD])
Total Units = SUM(fact_sales[Units_Sold])
Gross Profit = SUM(fact_sales[Gross_Profit_USD])
Gross Margin % = DIVIDE([Gross Profit], [Total Revenue])
Average Selling Price = DIVIDE([Total Revenue], [Total Units])
Marketing Spend = SUM(fact_marketing[Spend_USD])
ROAS = DIVIDE([Total Revenue], [Marketing Spend])
Positive Sentiment % =
    DIVIDE(
        CALCULATE(COUNTROWS(fact_reviews), fact_reviews[Sentiment]="Positive"),
        COUNTROWS(fact_reviews)
    )

RECOMMENDED MODEL
-----------------
Use the dim_* tables as dimensions and fact_* tables as facts.
Use single-direction 1-to-many relationships from dimensions to facts.
Avoid creating direct fact-to-fact relationships.
