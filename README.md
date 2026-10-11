# Superstore-Retail-Business-Performance-Analysis-and-Expansion-Strategy
Integrated 50K+ sales orders from three CSVs using Power Query for cleaning and transformation. Built a data model, applied Design Thinking, and developed an interactive Power BI dashboard. Used DAX for key metrics and visualizations, providing insights for market expansion and product optimization.
<img width="1848" height="970" alt="image" src="https://github.com/user-attachments/assets/1aaada6e-3235-45a1-9836-96c778057db5" />
**Author:** Phan Trần Thế Sơn

**Date:** April 2026

**Tools Used:** Power Query, Power BI, SQL

## 📋 Table of Contents

📌 1 - Background & Overview

📂 2 - Dataset Description & Data Structure

🧠 3 - Design Thinking Process

📊 4 - Key Insights & Visualizations

🔎 5 - Recommendation

## 📌 1 - Background & Overview

**🔎 What is this project about?**

This project aims to build a **Power BI dashboard** using the *Global Superstore Sales* dataset, which includes data on transactions (**Orders**), sales representatives (**People**), and product returns (**Returns**). The goal is to provide senior managers with **data-driven insights** to:

- Understand current business performance
- Optimize market expansion strategies
- Identify strategic products for growth
- Support better decision-making to drive revenue and ROI

**👥 Who is this project for?**

✔️ Data analysts & business analysts seeking actionable insights.

✔️ Marketing and sales teams focusing on product performance and market growth.

✔️ Route to market team aiming to improve distribution strategies and market reach.

**❓ What are the business questions?**

✔️ What is the current business performance of Superstore?

✔️ How is business performing across different regional markets, and which market should the business expand into?

✔️ How are different product categories performing, and which should be prioritized for strategic growth?

**🎯 What are the outcomes of the project?**

✔️ Revenue increased significantly, but profit margin remained flat, indicating rising costs and limited operational efficiency gains

✔️ Canada, despite low revenue and profit, emerged as the most profitable market (26%), while EMEA and EU displayed highest revenue growth, revealing expansion potential

✔️ Furniture, despite generating the second highest revenue, has the least profitable (7%). Meanwhile, Technology is the main revenue contributor and has the highest profit margin (14%)

✔️ Total number of orders increased while Return Rate declined over the years, indicating an improvement in efficiency

By aligning regional and product strategies, senior managers can **scale in high-margin markets**, **invest in scalable profitable categories**, and **optimize acquisition and return management**, driving **sustainable long-term growth**.

## 📂 2 - Dataset Description & Data Structure

### **📌 Data Source:**

- Source: Google BigQuery
- Size: The Orders table contains 51,290 records

### **📊 Data Structure & Relationships:**

1️⃣ The dataset consists of four tables:

- **Orders**: Contains detailed transaction and customer information (51,290 records)
<details>
<summary> <strong>Table 1: Orders</strong></summary>

| Column Name       | Data Type   | Description                              |
|------------------|------------|------------------------------------------|
| `Order ID`      | `VARCHAR`   | Unique identifier for each order.       |
| `Order Date`    | `DATE`      | Date when the order was placed.         |
| `Ship Date`     | `DATE`      | Date when the order was shipped.        |
| `Ship Mode`     | `VARCHAR`   | Shipping method used for delivery.      |
| `Customer ID`   | `VARCHAR`   | Unique identifier for each customer.    |
| `Customer Name` | `VARCHAR`   | Full name of the customer.              |
| `Segment`       | `VARCHAR`   | Customer segment (e.g., Consumer, Corporate). |
| `City`         | `VARCHAR`   | City where the order was placed.        |
| `State`        | `VARCHAR`   | State where the order was placed.       |
| `Country`      | `VARCHAR`   | Country where the order was placed.     |
| `Postal Code`  | `VARCHAR`   | Postal code of the shipping address.    |
| `Market`       | `VARCHAR`   | Market region (e.g., APAC, EMEA).       |
| `Region`       | `VARCHAR`   | Geographical region of the order.       |
| `Product ID`   | `VARCHAR`   | Unique identifier for each product.     |
| `Category`     | `VARCHAR`   | Product category (e.g., Furniture, Office Supplies). |
| `Sub-Category` | `VARCHAR`   | Sub-category of the product.            |
| `Product Name` | `VARCHAR`   | Name of the product ordered.            |
| `Sales`        | `DECIMAL`   | Revenue generated from the order.       |
| `Quantity`     | `INT`       | Number of items ordered.                |
| `Profit`       | `DECIMAL`   | Profit earned from the order.           |

</details>

- **Returns**: Stores data on returned orders (1,172 records)
<details>
<summary> <strong>Table 2: Returns</strong></summary>

| Column Name  | Data Type | Description |
|--------------|-----------|-------------|
| `Returned`   | `VARCHAR` | Indicates whether the order was returned (e.g., 'Yes' or 'No'). |
| `Order ID`   | `VARCHAR` | Unique identifier for each order. |

</details>

- **Customers**: Contains data on customer information (1,590 records)
<details>
<summary> <strong>Table 3: Customers</strong></summary>

| Column Name  | Data Type | Description |
|--------------|-----------|-------------|
| `Customer ID`   | `VARCHAR` | Unique identifier for each customer. |
| `Customer Name`   | `VARCHAR` | Full name of each customer. |

</details>

- **Regions**: Contains data on Supervisor of each Region (13 records)
<details>
<summary> <strong>Table 4: Regions</strong></summary>

| Column Name  | Data Type | Description |
|--------------|-----------|-------------|
| `Region`   | `VARCHAR` | The region assigned to each supervisor. |
| `Supervisor`   | `VARCHAR` | Full name of each supervisor. |

</details>

#### Data relationships:
<img width="699" height="718" alt="image" src="https://github.com/user-attachments/assets/c87ea456-1827-47c2-b419-ec1761fd036e" />

| **From Table** | **To Table** | **Join Key**   | **Relationship Type**                                  |
|------------|----------|------------|----------------------------------------------------|
| `fact_Orders`   | `dim_Customers` | `Customer ID`   | Many-to-One (multiple orders belong to one Customer) |
| `fact_Orders`   | `dim_Returns`| `Order ID` | One-to-One or Left Join (not all orders are returned) |
| `fact_Orders`   | `dim_Regions` | `Region`   | Many-to-One (multiple Regions belong to one Supervisor) |
| `fact_Orders`   | `dim_Date`| `Order Date` | Many-to-One |

## 🧠 3 - Design Thinking Process
### 1️⃣ Empathize
<img width="1920" height="1080" alt="Empathize - 5W1H" src="https://github.com/user-attachments/assets/0f9f8197-c3f9-435a-bbc2-41ffae43f880" />

<img width="1920" height="1080" alt="Empathy Map" src="https://github.com/user-attachments/assets/2dc7d61c-6999-4442-9ff8-49d1d129fccf" />

### 2️⃣ Define Point of View
<img width="1920" height="1080" alt="Define POVs" src="https://github.com/user-attachments/assets/2c3d80d1-e8fc-4651-8ead-71a9cbe7a04d" />

### 3️⃣ Ideate
<img width="1920" height="1080" alt="Define POVs (2)" src="https://github.com/user-attachments/assets/04c56858-14fa-4e1c-9dbd-ad79f3abda34" />

<img width="1920" height="1080" alt="Define POVs (3)" src="https://github.com/user-attachments/assets/f9b782dc-912a-41d4-b01e-fe1bb8957c0c" />

## 📊 4 - Key Insights & Visualizations
### I. Overview

<img width="1920" height="1080" alt="7" src="https://github.com/user-attachments/assets/78975b55-6eac-436c-9088-16fb2d959b69" />

#### 📌 Key Findings:
1 - Revenue and Profit surged

- Revenue hit **$12.64M** and Profit hit **$1.47M** in 2014, both increased by approximately 25% compared to the previous year
    
    → **Growth** was primarily driven by **increased order volume**, not by improved operational efficiency (Profit Margin declined by 1.9% compared to previous year)
    

2 - Canada shows highest Profit Margin

- Canada achieved a 27% profit margin despite low revenue. US, EU, and APAC contributed the highest revenue overall
    
    → Suggests Canada has high profitability potential, while the US remains the core market in terms of scale.
    

3 - Technology drives Growth

- Technology products generated the highest revenue across all regions
    
    → Suggests customers have a **strong preference for tech products** over other categories.
    

4 - Furniture generates the least Profit

- Despite ranking second in terms of Revenue, Furniture generates the **thinnest Profit Margin** across all categories
    
    → Indicates high **operating expenses, shipping/logistics overhead, and COGS**
    

5 - Order Delivery Optimization

- **Order volume** scaled consistently over time while the Return Rate showed a downward trajectory
    
    → Demonstrates tighter product quality control and optimized shipping & handling protocols
    

### II. Market Analysis

<img width="1920" height="1080" alt="8" src="https://github.com/user-attachments/assets/f93a0b31-3c94-4c14-8aad-b97a7befdb41" />

#### 📌 Key Findings:

1  - Revenue and Profit Distribution

- Total **Revenue** $12.64M, with APAC ($3.6M), EU ($2.9M), and US ($2.3M) leading
- Canada had the highest Profit Margin (27%), despite low revenue
- EMEA and Africa underperformed with low Revenue and Profit Margins (~5.5 - 12%)

2 - Profit contribution by Market

- APAC, EU, and US contributed the most to profit
- LATAM steady (~ 10%), while Africa and Canada contributed minimally

3 - Market Potential

- Despite recording the lowest Revenue and Profit, EMEA shows the greatest YoY% Revenue Growth, YoY% Profit Growth and Number of Customers

4 - Product Preferences:

- In leading markets (APAC, EU, US), Technology consistently contributed the most to Revenue, with high Profit and Profit Margin
- In emerging markets (Canada, EMEA), Technology was also the main Revenue driver, however:
    - Profit Margin of Technology in Canada was high (27.55%), compared to EMEA’s 5.81%
    → EMEA requires targeted margin turnaround initiatives, specifically auditing fulfillment overhead, local tariffs, and promotional discount strategies.

5 - Expansion Strategies for each Country in each Market, based on Revenue and Profit Margin

<img width="1920" height="1080" alt="9" src="https://github.com/user-attachments/assets/47febe15-359b-40a4-829c-cb6974d7b9e2" />

### III. Product Analysis

<img width="1920" height="1080" alt="10" src="https://github.com/user-attachments/assets/51f37117-f260-49e6-8de6-462f33941982" />

#### 📌 Key Findings:

1 - **Revenue** and **Profit Margin** by Sub-Category

- Phones ($1.7M), Copiers ($1.5M) and Chairs ($1.5M) lead in **Revenue**. Paper (24%), Labels (20%), Envelopes (17%), and Accessories (17%) stand out for **Profit Margins**

2 - Sub-Category Lag: Underperformance in Tables

- The bottom-ranking sub-category across all financial metrics - minimal **Revenue** ($757) and negative profitability (-$64 loss, -8.46% margin)
    
    → Strong correlation with product returns: Tables charts the highest Return Rate (7.54%)
    
3 - Product Expansion Strategy for each Product, in each Sub-Category and Category, based on **Revenue** and **Profit Margin**

<img width="713" height="399" alt="11" src="https://github.com/user-attachments/assets/be08470c-48ef-4af5-a10c-24b468dda5c1" />

## 🔎 5 - Recommendation
| **Strategy**                     | **Insight**                                                                                                                                                       | **Recommendation**                                                                                                                                                                      |
|----------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **🚀 1. Market Expansion Strategy** | - Total **Revenue** $12.64M, with APAC ($3.6M), EU ($2.9M) and US ($2.3M) leading. <br> <br> - **Canada** had the highest **Profit Margin**, despite low **Revenue**.| - Continue operation in APAC, EU and US,. focusing on Countries with High Revenue and High Profit Margin, or Low Revenue but High Profit Margin, with focus on key product categories. <br> <br> - Expand selectively in Canada to maximize profitability |
| **🛒 2. Product Portfolio Optimization** | - **Technology** leads in both **revenue** and **profit**. <br> <br> - Tables generate low **Revenue** but incur losses. <br> | - **Scale Technology**, focusing on high-margin Sub-Categories like Phones, Copiers and Accessories. <br> - Focus on specific products with High Revenue and High Profit Margin, or Low Revenue but High Profit Margin. <br> <br> - Consider removing **Tables** from Product Portfolio due to poor performance.|


