# SHOPIFY ANALYSIS USING POWERBI FOR VISUALISATION
![logo](https://cdn.shopify.com/s/files/1/0070/7032/articles/shopify_20stores_b12b3173-45ab-409a-9d73-d33898cfc696.png?v=1745508583)
## OBJECTIVE: 
- Understanding the steps for Data Management and Visualisation.
- Enhancing the comprehension of Data Connection, Data Cleaning, DAX calculations, Chart creation and formatting
- Gaining insights from the visualisations.

## DATASET
- The dataset is attached to this repository

## BUSINESS REQUIREMENTS 
### KPI and Customer Behavior Requirement
#### Transaction Performance
  The performance is used to evaluate the overall health and the effectiveness of sales operations based on Net Sales, Total Quantity, Net Average Order Value.
  - Net Sales DAX Formula:  `` Net Sales = sum(shopify_sales[Subtotal Price]) ``
  - Total Quantity DAX Formula: `` total quantity = SUM(shopify_sales[Quantity]) `` 
  - Net Average Order Value DAX Formula: `` Net Average Order Value = AVERAGE(shopify_sales[Subtotal Price]) ``

#### Customer Purchase Behavior
  The purpose is to gain an understanding of how customers react to the business based on Total Customers, Single Order Customers, Return Customer.
  - Total Customer DAX: `` Total Customer = DISTINCTCOUNT(shopify_sales[Customer Id]) ``
  - Single Order Customer DAX: `` Single Order Customer = 
CALCULATE(
    COUNTROWS(VALUES(shopify_sales[Customer Id])),
    FILTER(
        VALUES(shopify_sales[Customer Id]),
        CALCULATE(DISTINCTCOUNT(shopify_sales[Order Number])) = 1
    )
) ``
  - Return Customer DAX: `` Return Customer = 
CALCULATE(
    COUNTROWS(VALUES(shopify_sales[Customer Id])),
    FILTER(
        VALUES(shopify_sales[Customer Id]),
        CALCULATE(DISTINCTCOUNT(shopify_sales[Order Number])) > 1
    )
) ``

#### Retention and Value KPI's
  The aim of the visualization is to give insights into the long-term growth and customer values based of Lifetime Value, Repeat Rate, and Purchase Frequency.
  - Lifetime Value DAX: `` Life Time Value = [Net Sales] / [Total Customer] ``
  - Repeat Rate DAX: `` return rate = [Return Customer]/[Total Customer] ``
  - Purchase Frequency DAX: ``Purchase Frequency = DISTINCTCOUNT(shopify_sales[Order Number])/[Total Customer]``

    <img width="436" alt="image" src="https://github.com/user-attachments/assets/3df0f56d-fec2-417e-a391-6b5e5aca3094" />


### Chart Requirement
#### Regional Overview
- The visualizations are designed to display performance based on different provinces, according to the selected measure. Second, the bubble map also gives insights into sales and customer density at a more granular level. Last, the bar chart illustrates the top performance based on the selected KPI.  
<img width="413" alt="Screenshot 2025-06-04 110942" src="https://github.com/user-attachments/assets/488c2299-838d-47ec-989f-c49f75f9ea7d" />

-  DAX Formula for filter: `` Measure = {
    ("Net Sales", NAMEOF('shopify_sales'[Net Sales]), 0),
    ("total quantity", NAMEOF('shopify_sales'[total quantity]), 1),
    ("Total Customer", NAMEOF('shopify_sales'[Total Customer]), 2),
    ("Return Customer", NAMEOF('shopify_sales'[Return Customer]), 3)
   }`` 
- DAX Formula for Dynamics Title:
`` Regional Title = SELECTEDVALUE('Measure'[Dynamic Title]) & " by Regions" ``

#### Sales Trend Over Time

- The area chart is used for trend by day, and the Bar Chart for trend by hour.
- While the purpose of the area chart is to show the daily trend of the selected measure, that of the Bar Chart shows the sales and Customer Activity, which helps reveal the peak periods of customer activity
  
  <img width="445" alt="image" src="https://github.com/user-attachments/assets/9410c646-b8ed-42a9-8e6c-c3f5bde341f0" />

- DAX Formula for Dynamics Title:
  `` Trend Title = SELECTEDVALUE('Measure'[Dynamic Title]) & " Trend Over Time"  ``

  #### Gateway Payment Method and Product Type

- Chart types: the Donut Chart for Gateway and the Bar Chart for Product type
- Purpose: The Gateway exploration provides us with insights into the most and least payment methods which have been used, and the Product Types chart illustrates what types generate the highest revenue and order volume
 <img width="434" alt="image" src="https://github.com/user-attachments/assets/0f9b408c-937a-4618-945a-11bf5b210233" />

- DAX Formula for Dynamics Title: `` Gateway title = SELECTEDVALUE('Measure'[Dynamic Title]) & " By Gateway Payment" ``

## DASHBOARD

 <img width="863" alt="image" src="https://github.com/user-attachments/assets/882cc102-a80b-4907-8a5f-fe1e9488254a" />


