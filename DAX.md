# Power BI: DAX & Data Modeling – Marketing Campaign Analysis



This document explains the **data modeling** and **DAX logic** used in the Marketing Campaign Analysis Power BI report. It includes the custom tables, measures, and calculated columns that shaped the insights—even those not directly visualized.

---



## Table of Contents



- [1. Measures Table](#1-measures-table)

- [2. Calendar Table](#2-calendar-table)

- [3. Channel Table](#3-channel-table)

- [4. Products Table](#4-products-table)

- [5. Campaigns Table](#5-campaigns-table)

- [6. Custom Columns](#6-custom-columns)

- [7. Notes on Alignment and Best Practices](#7-notes-on-alignment-and-best-practices)



---



## 1. Measures Table


A dedicated **Measures Table** was created to hold all DAX measures for cleaner model management and better readability.



### Key Measures


1. Total Customers = DISTINCTCOUNT(Marketing[ID])


2. Total Accepted Campaigns = 
    SUMX(
        marketing_data,
        marketing_data[Accepted_Campaign1] + 
        marketing_data[Accepted_Campaign2] + 
        marketing_data[Accepted_Campaign3] + 
        marketing_data[Accepted_Campaign4] + 
        marketing_data[Accepted_Campaign5]
    )


3.  Total Discount-Based Purchases:


4.  Discount Purchases = SUM(marketing_data[Discount_Purchases])


5.  Total Spend = 
    SUMX(
        Marketing_Data,
        marketing_data[Fish_Spend] + 
        marketing_data[Fruits_Spend] + 
        marketing_data[Gold_Spend] + 
        marketing_data[Meat_Spend] + 
        marketing_data[Sweet_Spend] +
        marketing_data[Wine_Spend]
    )


6.  Average Income = AVERAGE(marketing_data[Annual Income])


7.  Average Spend = AVERAGEX(marketing_data, [Total Spend])


8.  Average Birth_Year = AVERAGE(marketing_data[Birth_Year])


9.  null Incomes = CALCULATE(COUNTROWS(marketing_data), ISBLANK(marketing_data[Annual Income]))




## 2. Calendar Table


A Calendar Table was created to support time-based analyses, even though it wasn’t directly utilized in this project. Establishing a calendar table is a best practice for enabling robust time intelligence functions.


DAX Code:

Calendar = 
ADDCOLUMNS (
    CALENDAR (MIN(marketing_data[Enrollment Date]), MAX(marketing_data[Enrollment Date])),
    "Year", YEAR([Date]),
    "Month", FORMAT([Date], "MMMM"),
    "Month Number", MONTH([Date]),
    "Year-Month", FORMAT([Date], "YYYY-MM")
)

Note: The calendar table includes a continuous range of dates from the earliest to the latest customer enrollment dates.
This Calendar table wasn't used in this analysis but it was created, alongside some measures for future purpose/references.


## 3. Channel Table

A separate Channel Table was created, Channel data was analyzed using a new data table, a Dax measure was also created seperately for it.

# Table

Channels = 
DATATABLE(
    "Channel", STRING,
    {
        {"Web"},
        {"Catalog"},
        {"Store"}
    }
)

# DAX

Channel Purchases = 
SWITCH(
    SELECTEDVALUE(Channels[Channel]),
    "Web", SUM(marketing_data[Web_Purchases]),
    "Catalog", SUM(marketing_data[Catalog_Purchases]),
    "Store", SUM(marketing_data[Store_Purchases])
)

These Table represent the Channels used by customers to shop various product categories.


## 4. Products Table

A separate Products Table was explicitly created, product-related data was analyzed using a new table, a Dax measure was also created seperately for it.

# Table

Products = 
DATATABLE(
    "Product Name", STRING,
    {
        {"wines"},
        {"Meat"},
        {"Fruits"},
        {"Sweets"},
        {"Fish"},
        {"Gold"}
    }
)

# DAX 

Product Spend =
SWITCH(
    SELECTEDVALUE(Products[Product Name]),
    "Wines", [wine Spend],
    "Meat", [Meat Spend],
    "Fruits", [Fruits Spend],
    "Sweets", [Sweet Spend],
    "Fish", [Fish Spend],
    "Gold", [Gold Spend]
)

These Table represent the amount spent by customers on various product categories.



## 5. Campaign Table

A separate Campaign Table was created using the datatable function, Campaign performance data was analyzed using a new table, a Dax measure was also created seperately for it.


# Table

campaigns = 
DATATABLE(
    "Campaign Name", STRING,
    {
        {"Campaign 1"},
        {"Campaign 2"},
        {"Campaign 3"},
        {"Campaign 4"},
        {"Campaign 5"}
    }
)

# DAX

Accepted Campaign Count = 
SWITCH(
    SELECTEDVALUE(campaigns[Campaign Name]),
    "Campaign 1", SUM(marketing_data[Accepted_Campaign1]),
    "Campaign 2", SUM(marketing_data[Accepted_Campaign2]),
    "Campaign 3", SUM(marketing_data[Accepted_Campaign3]),
    "Campaign 4", SUM(marketing_data[Accepted_Campaign4]),
    "Campaign 5", SUM(marketing_data[Accepted_Campaign5])
)




## 6. Custom Columns

Custom columns were added to enhance the analysis by categorizing and flagging data points.
A Campaign response Custom column(Yes/NO) is embedded within the Marketing table through the following columns using the IF statement:

• Accepted_Campaign1

• Accepted_Campaign2

• Accepted_Campaign3

• Accepted_Campaign4

• Accepted_Campaign5

• Last_Campaign_Response


This column indicates whether a customer accepted a specific campaign.


1. Campaign Accepted



Indicates whether a customer accepted any campaign.



Campaign Accepted = 

IF(

  Marketing[AcceptedCmp1] + 

  Marketing[AcceptedCmp2] + 

  Marketing[AcceptedCmp3] + 

  Marketing[AcceptedCmp4] + 

  Marketing[AcceptedCmp5] + 

  Marketing[Response] > 0, 

  "Yes", 

  "No"

)


2. Customer Age 

This was created using the Customer Birth_Year and the Today() Function

Age = Year(TODAY()) - marketing_data[Birth_Year]

Note: The Age column is calculated as YEAR(TODAY()) - Marketing[Birth_Year].


3. Customer Age Group

Categorizes customers into age groups based on their Age, after getting their Age using their Birth_Year.

Age Group = 
SWITCH(
    TRUE(),
    marketing_data[Age] < 18, "Child",
    marketing_data[Age]>= 18 && marketing_data[Age] <= 24, "Teenager",
    marketing_data[Age] >= 25 && marketing_data[Age] <= 34, "Young Adult",
    marketing_data[Age] >= 35 && marketing_data[Age] <= 49, "Adult",
    marketing_data[Age] >= 50 && marketing_data[Age] <= 64, "Middle Aged",
    marketing_data[Age] >= 65, "Senior"
)




Calculates the total number of purchases made using discounts.






## 7.  Data Model Alignment


The data model is structured to facilitate intuitive analysis:

• Measures Table: Centralizes all DAX measures for easy access and maintenance.

• Calendar Table: Provides a date backbone for time-based analyses.

• Marketing_data Table: Serves as the primary fact table containing customer demographics, purchase behavior, and campaign responses.

• Custom Columns: Enhance the granularity and interpretability of the data.


Relationships between tables are established based on relevant keys to ensure data integrity and support comprehensive analyses.



### Best Practices Followed

• Explicit Measures: All calculations are defined as explicit measures, promoting clarity and reusability.

• Centralized Measures Table: Organizing measures in a dedicated table improves model readability.

• Custom Columns: Adding calculated columns like Campaign Accepted and Customer Age Group enables more nuanced analyses.

• Calendar Table: Even if not directly used, having a calendar table prepares the model for future time-based analyses.

• Data Cleaning: Null values, especially in critical fields like Income, were handled appropriately to ensure accurate insights.



This DAX provides a detailed overview of the DAX components and data model structure used in the Marketing Campaign Analysis Power BI project. It serves as a guide for understanding the analytical framework and for facilitating future enhancements or audits.



---

**Project Built By:** Bakare Sukurat Aderonke 

**Tool Used:** Power BI/Power Query

**Dataset:** Marketing Campaign Dataset (Cleaned & Modeled)


