## Marketing Campaign Analysis Dashboard


This project presents a Marketing Campaign Analysis using Power BI. The goal is to help stakeholders understand customer behavior, evaluate campaign performance, and improve marketing strategies across multiple channels.


## Pages Overview


### 1. Home Page

![Marketing Campaign Home Page](.MC-Home-Page.png)


The **Home Page** provides a high-level view of marketing performance, customer income, purchase behaviors, and top product categories.
This page gives a high-level overview of the marketing performance:

- **Total Customers:** 2,240

- **Null Incomes (Filtered out for Visualization):** 24

- **Total Customer Spend:** 1M

- **Average Customer Income:** $52K

- **Average Spend per Customer:** $606

- **Average Year of Birth:** 1969



#### Key Visuals:

- **Web Purchases by:**

  - Age Group

  - Education Level

  - Marital Status

- **Campaign Success Comparison**

- **Purchases by Marketing Channel** (Store, Web, Catalog)

- **Top Performing Product Categories** (Wines, Meat, Gold, etc.)


---


### 2. Grid Page
![Marketing Campaign Grid Page](.MC-Grid-Page)


The **Grid Page** dives deeper into demographics, customer distribution, and campaign response insights.
This page focuses on customer demographics and deeper campaign insights.


- **Total Customers:** 2,240

- **Null Incomes (Filtered out for Visualization):** 24

- **Total Campaign Responses:** 667

- **Total Discount-Based Purchases:** 5,208

- **Total Customer Spend:** 1M

- **Average Customer Income:** $52K



#### Key Visuals:

- **Customer Distribution by:**

  - Age Group

  - Education

  - Marital Status

  - Country (8 countries)


---


## Measures Created

- **Total Customers**

- **Total Campaign Responses**

- **Total Discount-Based Purchases**

- **Total Customer Spend**

- **Average Spend per Customer**

- **Average Customer Income**

- **Average Year of Birth**



## Custom Columns Created

- **Campaign Accepted** (Yes/No logic for accepted campaigns)

- **Customer Age Group** (Young Adult, Adult, Middle Aged, Senior)

- **Discount Purchases**



## Filters / Slicers Used

- Age Group

- Campaign Response

- Education

- Marital Status

- Channel


---


## Key Insights


1. **Null Values & Outliers:**

   - 24 null income entries were excluded to maintain clean analysis.


2. **Factors Influencing Web Purchases:**

   - Most web buyers are middle-aged, senior, educated, and earn well.

   - Relationship status influences online shopping behavior.


3. **Most Successful Campaign:**

   - Campaign 4 had the highest response rate.

   - Campaign 1 was the least effective.


4. **Customer Profile:**

   - A typical customer is 35+ years, married, educated, and earns a decent income.


5. **Top Products:**

   - Wines lead in sales, followed by Meat, Gold, and Fish.


6. **Channel Preferences:**

   - Store dominates in purchases, followed by Web.

   - Catalog is the least used channel.


7. **Customer distribution by Country:**
  
   - There are 8 Countries in the DataSet in which most customers are from Spain, followed by Saudi-Arabia, Canada, Austrialia, India, Germany, USA. Mexico has the least customers.


---


## Conclusion



This dashboard offers a detailed snapshot of customer behavior and marketing campaign performance. By analyzing customer demographics and spending patterns, it becomes easier to identify what works and where improvements are needed.



The dual layout (Home and Grid) makes navigation intuitive and supports both high-level monitoring and detailed investigation.



---



**Project Built By:** Bakare Sukurat Aderonke 

**Tool Used:** Power BI/Power Query

**Dataset:** Marketing Campaign Dataset (Cleaned & Modeled)



