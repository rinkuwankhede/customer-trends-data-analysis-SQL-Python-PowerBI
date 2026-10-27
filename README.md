# Customer-trends-data-analysis-SQL-Python-PowerBI
# 🛍️ Customer Shopping Behavior Analysis
End-to-end analytics project: **Python (EDA + feature engineering) → PostgreSQL (business questions) → Power BI (dashboard)**.

Dataset: 3,900 customer purchases, 18 columns (age, gender, category, item, purchase amount, season, subscription, discount, shipping type, previous purchases, review rating, etc.).

---

## 🧰 Tools Used

- **Python** – pandas, SQLAlchemy, psycopg2 (Jupyter Notebook)
- **PostgreSQL** – pgAdmin, SQL (CTEs, window functions)
- **Power BI** – DAX measures, KPI cards, slicers, charts

---

## 🔄 Project Workflow

1. **Data modelling + EDA** in Jupyter Notebook
2. **Feature engineering** – created new columns needed for analysis
3. **Created a new PostgreSQL database** and connected Jupyter to it
4. **Solved 10 business questions** in SQL
5. **Connected the data to Power BI** → created measures → built KPIs and charts

---

## ✨ Features

### 1. Data Cleaning & EDA (Python)
- Checked data with `head()`, `info()`, `describe()`, `isnull()`
- Found **37 missing values** in `review_rating` → filled using the **median rating of each product category**
- Cleaned column names (lowercase, underscores, `purchase_amount_(usd)` → `purchase_amount`)

### 2. New Columns Created

### 3. Python → PostgreSQL
- Created a `customer_behavior` database in PostgreSQL
- Loaded the cleaned dataframe into a `customer` table using SQLAlchemy `to_sql()`

### 4. SQL Analysis (10 business questions)
| # | Question |
|---|---|
| 1 | Revenue by gender |
| 2 | Discount users who still spent more than average |
| 3 | Top 5 products by average review rating |
| 4 | Average spend: Standard vs Express shipping |
| 5 | Do subscribers spend more? |
| 6 | Top 5 products by % of discounted purchases |
| 7 | **Customer segments: New / Returning / Loyal (using a CTE)** |
| 8 | Top 3 most purchased products in each category (CTE + `ROW_NUMBER()` window function) |
| 9 | Are repeat buyers also subscribers? |
| 10 | Revenue contribution by age group |

**Customer segmentation logic (CTE):**
- **New** → 1 previous purchase
- **Returning** → 2 to 10 previous purchases
- **Loyal** → more than 10 previous purchases

### 5. Power BI Dashboard
**Measures created (DAX):**
- `Number of Customers` = `COUNT(customer_id)`
- `Average Purchase amount` = `AVERAGE(purchase_amount)`
- `Average Review Rating` = `AVERAGE(review_rating)`

**KPI cards:** Number of Customers · Average Purchase Amount · Average Review Rating

**Slicers (filters):** Subscription Status · Gender · Category · Shipping Type

---

## 📊 Dashboard Walkthrough

![Customer Shopping Behavior Dashboard](https://github.com/rinkuwankhede/customer-trends-data-analysis-SQL-Python-PowerBI/blob/main/Customer%20Shopping%20Behavior%20Dashboard.png)

1. **Header + KPI cards (top)** – quick health check: **3,900 customers**, **average purchase $59.76**, **average rating 3.75 / 5**
2. **Left filter panel** – slice the whole dashboard by subscription, gender, category and shipping type
3. **Donut chart – % of Customers by Subscription Status** – shows how many customers are subscribed vs not
4. **Column chart – Revenue by Category** – which category brings the most money
5. **Column chart – Sales by Category** – how many customers buy from each category
6. **Bar chart – Revenue by Age Group** – which age group spends the most
7. **Bar chart – Sales by Age Group** – how many customers are in each age group

---

## 💡 Key Insights

**Revenue & customers**
- Total revenue is **$233,081** from 3,900 customers; average purchase is about **$60**
- **Male customers = 68%** of the base and bring **$157,890 (68%)** of revenue; female customers bring $75,191
- Spend per purchase is almost the same for both: **$59.54 (male) vs $60.25 (female)** → male revenue is higher because there are *more male customers*, not because they spend more

**Categories**
- **Clothing is the star , then Accessories , Footwear , Outerwear 
- Top sellers: Blouse and Pants (Clothing, 171 orders each), Jewelry (Accessories, 171)

**Subscription**
- Only **27% of customers are subscribed** (1,053 vs 2,847)
- **Subscribers do not spend more**: $59.49 average vs $59.87 for non-subscribers → subscription is not driving higher spend
- Even among repeat buyers (5+ previous purchases), **72% are not subscribed** → big chance to convert loyal buyers

**Customer loyalty (CTE segmentation)**
- **Loyal 3,116 (80%)**, Returning 701 (18%), New 83 (2%) → strong repeat base, but very few new customers coming in

**Discounts**
- **43% of purchases used a discount** (1,677) and 839 of them still spent above the average
- Highest discount-rate products: **Hat (50%), Sneakers (49.7%), Coat (49.1%), Sweater (48.2%), Pants (47.4%)**
- Discount buyers spend about the same ($59.28) as non-discount buyers ($60.13) → discounts may be cutting margin without lifting spend

**Age groups**
- Fairly balanced: **Young Adult 26.7%**, Middle-aged 25.4%, Adult 24.0%, Senior 23.9% of revenue → no single age group dominates

**Shipping & ratings**
- Average spend barely changes by shipping type ($58.5 – $60.7); 2-Day Shipping is highest, Standard lowest
- Top-rated products: **Gloves (3.86), Sandals (3.84), Boots (3.82), Hat (3.80), Skirt (3.79)** – ratings are all close, so no product is a clear outlier

---

## 🚀 Business Recommendations
- Push **Clothing & Accessories** (76% of revenue) in campaigns
- Run subscription offers aimed at **repeat/loyal customers** – most aren't subscribed yet
- Review the **discount strategy** – discounts don't increase spend per order
- Work on **acquiring new customers** – only 2% are in the "New" segment
- Find ways to attract more **female customers** (only 32% of base)

---
