# Mobile Sales Dashboard Onyx Challenge May 2025

### Interactive Dashboard : 
#### https://app.powerbi.com/view?r=eyJrIjoiY2U0NDg4OWYtYTQwOC00NTRiLTg2NzgtYWI1NjAwMWU0YTcxIiwidCI6IjQ2NTRiNmYxLTBlNDctNDU3OS1hOGExLTAyZmU5ZDk0M2M3YiIsImMiOjl9
![Image](https://github.com/user-attachments/assets/bfc1fdb8-bb41-404e-9a9d-4c2a39b3ffc0)
## Introduction
I recently participated in the May 2025 ZoomCharts Mini Challenge, which is part of the global DataDNA Dataset Challenge organized by Onyx Data.

This month’s challenge focused on analyzing mobile phone sales data from 2024 — a rich dataset covering product specifications, customer demographics, pricing, sales channels, and geographic locations across multiple countries.


## Problem Statement
*"You are a data analyst for a major mobile phone retailer operating across multiple countries. You’ve been given a 2024 sales dataset, containing detailed records of mobile phone transactions, customer demographics, product specifications, and geographic locations. The dataset combines information about the models sold, their prices, storage sizes, colors, operating systems, and customer demographics like age group and gender. It also captures where and how the sales were made - online, through partners, or in-store, and the type of payment used.
Your goal is to build a report that tells the story of mobile sales across different regions, highlights best-selling products and trends, and helps the business understand customer behavior better."*

## Sales Dashboard Output

This dashboard helps the mobile sales team understand their customers, revenue trends, and performance gaps more clearly.

It provides actionable insights such as:

🔍 The *26–33 age group contributed the highest total revenue ($2.93M)*, accounting for 19.68% of all revenue—highlighting this group as a key customer segment to focus on.

💸 Most purchases happened via *Cash*, especially among consumers aged *26–33 and 34–42*, showing that offline payment methods still dominate.

🛍️ *OnePlus 12 Pro* was the *top-selling model*, contributing 21.65% of total units sold.

📦 *256GB storage and White color combinations generated the highest revenue*, making them the most popular configurations.

🌐 The *Online channel* led all others with 61.63% of total revenue, showing the growing importance of digital sales.

📅 *January* was the best-performing month, generating $1.41M in revenue—135.48% higher than November, the lowest month.

## Files Included

### Mobile Sales .xlsx: 
Contains raw transactional data with details on demography, sales report, product details, etc.

### Mobile sales .pbix: 
Power BI report file with interactive dashboards and visualizations on revenue, osales insight, and customer insight based on the dataset. 

## Data Dictionary:
- Transaction_ID: Unique transaction ID
- Transaction_Date: Date the transaction occurred
- Mobile_Model: Model of the smartphone sold
- Brand: Smartphone brand
- Price: Price of the smartphone
- Units_Sold: Units sold in transaction
- Total_Revenue: Total revenue (Price * Units Sold)
- Customer_Age: Customer's age
- Customer_Age_Group: Age group bucket
- Customer_Gender: Customer's gender
- Country: Country of transaction
- City: City of transaction
- Latitude: City's latitude
- Longitude: City's longitude
- Sales_Channel: Sales channel used
- Payment_Type: Method of payment
- End of Month: Month-end date for aggregation
- Storage_Size: Device storage configuration
- Color: Color variant of the device
- Operating_System: Operating system of the phone

### Steps followed 

- Step 1 : Load data into Power BI Desktop, dataset is a .xlsx file.
- Step 2 : Open power query editor & in view tab under Data preview section, check "column distribution", "column quality" & "column profile" options.
- Step 3 : Also since by default, profile will be opened only for 1000 rows so you need to select "column profiling based on entire dataset".
- Step 4 : It was observed that in none of the columns errors & empty values were present.
- Step 5 : To clean the data, remove the duplicates from the dataset of "Fact_Sales".
- Step 6 : Update the header in 3 datasets as per requirement and load the dataset into Power BI.
- Step 7 : To organise the report, at first text box is inseted in the report to write the TITLE of the page. Name the report as **"Mobile Sales Report"**.
- Step 8 : In the report view, under the insert tab, using image option company's logo was added to the report design area at the left corner. Here is visual outcome:
![Image](https://github.com/user-attachments/assets/5ed1353e-606f-44af-b976-0c17e9d09b16)
- Step 9 : In order to navigate the report add the another three "Action" button as *"Revenue"*, *"Sales Insight"*, and *"Customer Insight"* at the right corner. 

 ![Image](https://github.com/user-attachments/assets/4b2cac32-bccd-42f3-994a-fbc99aa0d0f4)
- Step 10 : Make the duplicate of the page for three times to create the separate Canvas for each part.
- Step 11 : Visual Slicers were added for three fields for "Country", "Storage Size", & "Months".













































# Snapshot of Revenue Dashboard

![Image](https://github.com/user-attachments/assets/a502c1ea-0209-48db-a135-1c5516db9b21)

# Snapshot of Sales Insight Dashboard

![Image](https://github.com/user-attachments/assets/8662b37c-329e-4a9e-947e-76c19d3dc7d3)

# Snapshot of Customer Insight Dashboard

![Image](https://github.com/user-attachments/assets/88ac8d9b-5857-41c4-b58c-e3f6ae55d240)
