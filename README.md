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

## Steps followed 

- Step 1 : Load data into Power BI Desktop, dataset is a .xlsx file.
- Step 2 : Open power query editor & in view tab under Data preview section, check "column distribution", "column quality" & "column profile" options.
- Step 3 : Also since by default, profile will be opened only for 1000 rows so you need to select "column profiling based on entire dataset".
- Step 4 : It was observed that in none of the columns errors & empty values were present.
- Step 5 : To clean the data, remove the duplicates from the dataset of "Fact_Sales".
- Step 6 : Update the header in 3 datasets as per requirement and load the dataset into Power BI.

### Page Set up
- Step 7 : To organise the report, at first text box is inseted in the report to write the TITLE of the page. Name the report as **"Mobile Sales Report"**.
- Step 8 : In the report view, under the insert tab, using image option company's logo was added to the report design area at the left corner. Here is visual outcome:
![Image](https://github.com/user-attachments/assets/5ed1353e-606f-44af-b976-0c17e9d09b16)
- Step 9 : In order to navigate the report add the another three "Action" button as *"Revenue"*, *"Sales Insight"*, and *"Customer Insight"* at the right corner. 

 ![Image](https://github.com/user-attachments/assets/4b2cac32-bccd-42f3-994a-fbc99aa0d0f4)
- Step 10 : Make the duplicate of the page for three times to create the separate Canvas for each part.
- Step 11 : Visual Slicers were added for three fields for "Country", "Storage Size", & "Months".

### Creating Measure Table:
To develop a dynamic Power BI report on Mobile Sales, I created a dedicated Measure Table to organize and centralize all the key DAX measures at one place.
for creating new Measures Table Table following DAX expression was written;
       
    MeasuresTable = 
    SELECTCOLUMNS(
        FILTER(
            { (1) },
            FALSE()
        ),
        "Measure", [Value]
    )

#### *Step 12: Used DAX expression in Measures Table*
- To calculate *Total Revenue*:

       Total Revenue = SUM(Fact_Sales[Total_Revenue])

- To calculate *Total Units Sold*:

       Total Units Sold = SUM(Fact_Sales[Units_Sold])

- To calculate *Average Order Value*:

      Average Order Value = [Total Revenue]/[Total Units Sold]

- To calculate MoM Revenue Change %:

      MoM Revenue Change % = 
      VAR CurrentMonthRevenue = [Total Revenue]
      VAR PreviousMonthRevenue =
          CALCULATE (
              [Total Revenue],
              DATEADD ( 'Fact_Sales'[Transaction_Date].[Date], -1, MONTH )
          )
      RETURN
          DIVIDE (CurrentMonthRevenue - PreviousMonthRevenue, PreviousMonthRevenue)

- To know total customer, male customer, female customer, and others consumers; count the rows of the customers gender:

      Total Consumer = COUNT(Fact_Sales[Customer_Gender])
        
      Male Consumer = CALCULATE(COUNTROWS(Fact_Sales), Fact_Sales[Customer_Gender]="Male")

      Female Consumer = CALCULATE(COUNTROWS(Fact_Sales), Fact_Sales[Customer_Gender]="Female")

      Others Consumer = CALCULATE(COUNTROWS(Fact_Sales), Fact_Sales[Customer_Gender]= "Other")

- To show the *Top Model Units Sold* as Text:

      Top Model Units Sold = 
      CALCULATE (
        MAX ( Fact_Sales[Mobile_Model] ),
        TOPN (
            1,
            SUMMARIZE (
                Fact_Sales,
                Fact_Sales[Mobile_Model],
                "TotalUnits", SUM ( Fact_Sales[Units_Sold] )
            ),
            [TotalUnits], DESC
        )
      )

- To show the *Top Payment Method* as Text:

      Top Payment Method = 
      CALCULATE (
          MAX ( Fact_Sales[Payment_Type] ),
          TOPN (
              1,
              SUMMARIZE (
                  Fact_Sales,
                  Fact_Sales[Payment_Type],
                  "TotalUnits", SUM ( Fact_Sales[Units_Sold]       )
              ),
              [TotalUnits], DESC
          )
      )

- To show the *Top Selling Month* as Text:

      Top Selling Month = 
      CALCULATE (
          MAX ( Fact_Sales[End of Month].[Month] ),
          TOPN (
              1,
              SUMMARIZE (
                  Fact_Sales,
                  Fact_Sales[End of Month].[Month],
                  "TotalUnits", SUM ( Fact_Sales[Units_Sold] )      
              ),
              [TotalUnits], DESC
          )
      )

- To show the *Top Selling City* as Text:

      Top Selling City = 
      CALCULATE (
          MAX ( Fact_Sales[City] ),
          TOPN (
              1,
              SUMMARIZE (
                  Fact_Sales,
                  Fact_Sales[City],
                  "TotalUnits", SUM ( Fact_Sales[Units_Sold] )
              ),
              [TotalUnits], DESC
          )
      )

- To show the *Top Selling Brand* as Text:
    
      Top Selling Brand = 
      VAR SummaryTable = 
          SUMMARIZE(
              'Fact_Sales',
              'Fact_Sales'[Brand],
              "TotalUnits", SUM('Fact_Sales'[Units_Sold])
          )
      VAR TopBrand = 
          TOPN(1, SummaryTable, [TotalUnits], DESC)

      RETURN
          CONCATENATEX(TopBrand, 'Fact_Sales'[Brand], ", ")

- To show the *Top Sales Channel* as Text:

      Top Sales Channel = 
      CALCULATE (
          MAX ( Fact_Sales[Sales_Channel] ),
          TOPN (
              1,
              SUMMARIZE (
                  Fact_Sales,
                  Fact_Sales[Sales_Channel],
                  "TotalUnits", SUM ( Fact_Sales[Units_Sold] )
              ),
              [TotalUnits], DESC
          )
      )

### Revenue Report Page
The Revenue report page was designed to highlight key insights related to revenue performance following mobile sales, including total revenue, revenue trends, and contribution by product category.

- Step 13 : Four card visuals were added to the page to show MoM Revenue Change %, Average Order Value, Top Selling Brand and Top Model Units Sold (Top selling model)

![Image](https://github.com/user-attachments/assets/05ce63a3-6104-4651-88d2-2c2f0dcfece0)

- Step 14 : The line chart is implemented to analyze *Total Revenue over Time*, using Transaction Date (by month) on the X-axis and Total Revenue on the Y-axis. To provide the high-level summary, added card visual above the chart to display the *total revenue* amount of *$12.16 million*. Additionally, toggle on data labels through the Format pane to show monthly revenue values directly on the chart.

   *While highest revenue genarated in January, November gave the lowest.*

![Image](https://github.com/user-attachments/assets/ebc5f3b7-96e0-4a62-8e66-380b47a0fefe)

- Step 15 : *Total Unit sold* insights were communicated using line chart with the transaction date formatted by month on the X-axis and total unit sold on the Y-axis. The total sold unit of 15.39K was shown through the card visual placed above the chart. From the Format panel, the data label option was toggled on to exhibit each month’s sold unit.
       
  *The chart revealed that the highest selling was in January 2024.*

![Image](https://github.com/user-attachments/assets/4c717aa4-58f5-468b-98dd-bafa789ed114)

- Step 16 : A pie chart was implemented to illustrate *Total Revenue by Sales Channel*. The *Sales Channel* was selected for the category axis and *Total Revenue* for the value metric. This visual made it easy to identify which channels generated the highest revenue share.

  *It was observed that the Online channel generated the highest share of revenue.*

![Image](https://github.com/user-attachments/assets/9a606c99-b4fb-4a61-a2d0-b5634b1be22d)

- Step 17 : *Total Genarated Revenue by Country* was visualized using a ZoomChart Drill Down Combo Bar. Countries were set as the category axis, and total revenue was selected as the series.  This chart enabled interactive exploration through drill-down features, allowing deeper insights into regional revenue performance.

  *Among all countries, India was identified as having the highest revenue contribution, while Pakistan recorded the lowest.*

![Image](https://github.com/user-attachments/assets/31a517ec-25df-47cc-ae70-84b47077e877)

- Step 18 : 
To analyze *Genarated Revenue by Color and Storage Size*, the heat map was added with Color on rows and Storage Size on columns, based on the Total Revenue measure. Green with 256GB recorded the highest value at $990.5K, followed closely by White (256GB) at $964.7K and Blue (128GB) at $922K. Notably, White (64GB) also contributed significantly with $938.6K. 

  *Overall, White emerged as the top-performing color, and 128GB was the most consistent storage size in terms of revenue.*
  
![Image](https://github.com/user-attachments/assets/bd21891a-26db-480d-8073-d20d68dc3da9)


#### Sales Insight Report Page

This Sales Insight dashboard provides a clear view of sales performance, showcasing units sold by month, top mobile models, OS-wise pricing trends, and monthly OS unit sales.

- Step 19 : Four card visuals were added to the page to show MoM Revenue Change %, Average Order Value, Top Selling Brand and Top Model Units Sold (Top selling model)


- Step 20 :


- Step 21 :


- Step 22 :


- Step 23 :



#### Customer Insight Report Page

This Customer Insight report highlights essential analytics on total consumers segmented by color and storage size, customer gender-based brand preferences, OS choices by age, revenue by age group, and preferred payment methods.

- Step 24 :

![Image](https://github.com/user-attachments/assets/afea9c07-0fca-4b65-b0f2-b63f2bd9527e)

- Step 25 : Total consumer preference for mobile storage and color was visualized through a heat map, where color was set on the row axis and storage size on the column axis. The peak was noted for 64GB White (25 consumers), with 128GB Blue and 256GB Green both attracting 24 consumers. Black at 128GB followed with 23. 

  *White and Blue colors demonstrated the highest overall consumer preference, while 256GB showed consistent popularity across options.*

![Image](https://github.com/user-attachments/assets/3a5b311a-5781-4c71-abaa-777e491246cb)

- Step 26 : Brand Preference by Customer Gender

![Image](https://github.com/user-attachments/assets/9f735402-ac07-4c8a-a631-463253505294)

- Step 27 : Preferred Operating System by Age Group

![Image](https://github.com/user-attachments/assets/1f75743a-cb77-44eb-a687-5ed0a4de459c)

- Step 28 : Generated Revenue from Different Age Group

![Image](https://github.com/user-attachments/assets/0b8ea2e4-3611-4873-828d-4df275cd84e6)

- Step 23 : Preferred Payment Type by Different Age Group


![Image](https://github.com/user-attachments/assets/76b84c75-6d7c-42ab-b317-07e795f0c14d)












































# Snapshot of Revenue Page Tab

![Image](https://github.com/user-attachments/assets/a502c1ea-0209-48db-a135-1c5516db9b21)

# Snapshot of Sales Insight Page Tab

![Image](https://github.com/user-attachments/assets/8662b37c-329e-4a9e-947e-76c19d3dc7d3)

# Snapshot of Customer Insight Page Tab

![Image](https://github.com/user-attachments/assets/88ac8d9b-5857-41c4-b58c-e3f6ae55d240)
