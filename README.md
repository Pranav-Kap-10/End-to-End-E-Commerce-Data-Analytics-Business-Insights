# 🛒 E-commerce Sales Analysis & Power BI Dashboard
> A complete end-to-end **E-commerce Sales Analytics System** that extracts messy, multilingual, and non-relational data from publicly available Olist datasets, transforms it using Python, and visualizes insights through interactive Power BI dashboards.

---

## 🚀 Overview  

This project covers the **full analytics lifecycle**:

- **Data Extraction** – Load CSV datasets into Microsoft SQL Server  
- **Data Cleaning & Transformation** – Handle messy, multilingual (Portuguese) data with Python  
- **Data Integration** – Merge customers, orders, products, sellers, reviews, and geolocation datasets  
- **Business Insights** – Sales, churn, product category contribution, price analysis, BOGO simulation, seasonality, payments  
- **Data Visualization** – Power BI dashboards with cards, charts, conditional formatting, and matrix visuals  
- **Market Basket Analysis** – Identify product pairs, support, confidence, and lift for cross-selling  

The system eliminates spreadsheet dependency and enables:

✔ Data-driven decision-making  
✔ Product and category performance tracking  
✔ Customer retention and churn analysis  
✔ Pricing and promotional impact evaluation  
✔ Market basket and association rule insights  

---

## 📂 Dataset  

- Source: Olist Public E-commerce Datasets  
- Records: Multiple datasets with real structure, anonymized values  
- Files Imported: 9 CSV files  
- Key Tables & Columns:

### 1️⃣ olist_customers_dataset.csv
- customer_id, customer_unique_id, customer_zip_code_prefix, customer_city, customer_state

### 2️⃣ olist_geolocation_dataset.csv
- geolocation_zip_code_prefix, geolocation_lat, geolocation_lng, geolocation_city, geolocation_state

### 3️⃣ olist_orders_dataset.csv
- order_id, customer_id, order_status, order_purchase_timestamp, order_approved_at, order_delivered_carrier_date, order_delivered_customer_date, order_estimated_delivery_date

### 4️⃣ olist_order_items_dataset.csv
- order_id, order_item_id, product_id, seller_id, shipping_limit_date, price, freight_value

### 5️⃣ olist_order_payments_dataset.csv
- order_id, payment_sequential, payment_type, payment_installments, payment_value

### 6️⃣ olist_products_dataset.csv
- product_id, product_category_name, product_name_lenght, product_description_lenght, product_photos_qty, product_weight_g, product_length_cm, product_height_cm, product_width_cm

### 7️⃣ olist_sellers_dataset.csv
- seller_id, seller_zip_code_prefix, seller_city, seller_state

### 8️⃣ product_category_name_translation.csv
- product_category_name (Portuguese), product_category_name_english

### 9️⃣ olist_order_reviews_dataset.csv
- review_id, order_id, review_score, review_comment_title, review_comment_message, review_creation_date, review_answer_timestamp  

**Challenges with datasets**:  
- Portuguese language, messy city names, inconsistent product categories, missing or null values, non-relational structure  

---

## 🏗 Database Architecture  

CSV (Olist Datasets)  
        ↓  
Microsoft SQL Server (SSMS Staging Tables)  
        ↓  
Python Data Cleaning & Transformation  
        ↓  
Normalized Tables Merged for Analysis  
        ↓  
Power BI Dashboard Visualizations  

**Key Table Relationships in Power BI**:  

- `customers.customer_id` → `orders.customer_id`  
- `orders.product_id` → `products.product_id`  
- `orders.seller_id` → `sellers.seller_id`  
- `orders.order_id` → `reviews.order_id`  
- `customers.customer_zip_code_prefix` → `geo.geolocation_zip_code_prefix`  

---

## 🛠 Tech Stack  

- **Database**: Microsoft SQL Server  
- **Query Tool**: SQL Server Management Studio (SSMS)  
- **Language**: Python 3.11 (pandas, numpy, unidecode, pyodbc)  
- **Visualization**: Power BI Desktop  
- **Techniques Used**:
  - Data Cleaning & Standardization
  - Data Transformation using Python
  - Conditional Formatting in Power BI
  - DAX Measures & Calculated Columns
  - Market Basket Analysis (Support, Confidence, Lift)
  - BOGO Simulation & Profit Impact

---

## 🧱 Data Cleaning & Transformation  

### ✔ City Name Standardization
- Remove numbers, special characters, accents  
- Capitalize city names consistently  
- Remove leading `*` or `...`  

### ✔ Product Category Translation
- Portuguese → English mapping  
- Replace missing translations with appropriate category  

### ✔ Orders Filtering
- Remove canceled or invalid orders  
- Ensure shipping & delivery dates are logical  
- Aggregate order items by `order_id` for quantity, price, and freight  

### ✔ Payment Processing
- Aggregate payment values by type per order  
- Drop unnecessary columns (`payment_sequential`, `payment_installments`)  

### ✔ Review Handling
- Filter reviews for valid orders  
- Drop unnecessary columns (`review_comment_title`)  
- Convert review response timestamp to date  

### ✔ Python Integration with Power BI
- Configured Power BI Python scripting to use Python 3.11  
- Loaded datasets separately to reduce refresh time  
- Applied transformations before visualization  

---

## 📊 Analytics & Dashboard Features  

### General KPIs
- Total Customers (distinct from orders)  
- Total Orders  
- Total Sales (sum of order prices)  
- Average Order Value (Total Sales / Total Orders)  
- Inactive Customers in last 12 months  

### Product Category Contribution
- % of total sales per category  
- Conditional formatting: Green (>5%), Cream (3-5%), Yellow (<3%)  
- Blue gradient for percentage comparison  

### Customer Churn Analysis
- Year-wise churn based on last purchase year  
- Customers without orders in following year  

### Quantity vs Product Photos
- Line chart for average quantity vs product photos  
- Insight: higher photos lead to higher average quantity  

### Market Basket Analysis
- Support, Confidence, Lift metrics  
- Identifies common product pairings for cross-selling  
- Filtered low-frequency pairs for matrix visualization  

### New Product Performance
- Identify products launched in last 6 months  
- Total sales & orders for new products  

### Seasonality Analysis
- Identify monthly sales trends per category  
- Toys: Sept-Dec peak, Stationery: Jan-Feb & Nov-Dec  

### Price Fluctuation Analysis
- Average price change per category year-over-year  
- Impact on sales analyzed  

### Payment Method Analysis
- Distribution of sales across payment types  
- Pie chart visualization  

### BOGO (Buy One Get One) Simulation
- Impact on top 10 selling products  
- Calculated simulated revenue, profit, and percentage impact  

### Delivery Performance & Reviews
- On-time vs Late delivery review scores  
- On-time: higher rating, Late: lower rating  

### Order Fulfillment Time Analysis
- Approval, shipping, and delivery times in hours  
- Insight into operational efficiency  

### Product Lifecycle Revenue
- Revenue comparison from first 90 days vs most recent 90 days  
- Identify product maturity trends  

### Seller Performance Analysis
- Identify highly-rated (>4.5) sellers underperforming locally (<10% sales in own state)  

---

## 📌 Problems Solved

| Problem | Solution |
|---------|----------|
| Messy multilingual city names | Python cleaning & unidecode |
| Missing product category translations | Mapped Portuguese → English |
| Invalid orders/dates | Filtered orders with incorrect timestamps |
| Duplicate payment entries | Aggregated by payment type |
| Sparse transactional data | Market basket analysis filtering |
| Complex sales calculations | DAX measures & Python aggregation |
| Large datasets in Power BI | Separated loading to improve refresh |
| Churn & lifecycle analysis | Year-wise calculated columns |
| Promotional impact simulation | BOGO model implemented via DAX |

---

## 📈 Business Impact

- Identified top-performing products & categories  
- Optimized marketing strategies via churn and basket analysis  
- Improved pricing strategy with price fluctuation insights  
- Predicted seasonal demand patterns  
- Simulated promotion impact (BOGO) for profitability insights  
- Enhanced decision-making through interactive Power BI dashboards  

---

## 🔹 Author  

👤 Pranav Kapoor  
Data Analyst | Python Developer | Power BI Specialist  

---

