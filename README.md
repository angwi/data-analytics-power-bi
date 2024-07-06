# E-Commerce Sales Analysis

### Project Overview
AdventureWorks is a global manufacturer of cycling equipment and accessories.
The management team needs a way to track KPIs (sales, revenue, profit, returns), compare regional performance, analyze product-level trends, and identify high-value customers.

### Data Source
A folder containing raw csv files, which contain information about transactions, returns, customers, and sales territories.

### Data Cleaning and Preparation

The following tasks were performend in the initial data preparation
- Data loading and inspection
- Creating new categorical columns like Order quantity type (Single Item, Multiple Items), customer priority (Standard or Priority) etc
- Creating a Date table (Calendar table)

### Data Modeling
A relational data model was created. Below is the data model created:

<p>
  <img src="https://github.com/angwi/data-analytics-power-bi/blob/main/data-model.png" />
</p>

### DAX Measures
Several DAX measures were created, some of which a listed below:
```java
% of All Orders = DIVIDE([Total Orders], [All Orders])
```
```java
% of All Returns = DIVIDE([Total Returns], [All Returns])
```
```java
10-day Rolling Revenue = 
CALCULATE(
    [Total Revenue],
    DATESINPERIOD(
        'Calendar'[Date],
        MAX(
            'Calendar'[Date]
        ),
        -10,
        DAY
    )
)
```
```java
90-day Rolling Profit = 
CALCULATE(
    [Total Profit],
    DATESINPERIOD(
        'Calendar'[Date],
        MAX(
            'Calendar'[Date]
        ),
        -90,
        DAY
    )
)
```
```java
All Orders = 
CALCULATE(
    [Total Orders],
    ALL('Sales Data')
)
```
```java
All Returns =
CALCULATE(
[Total Returns],
ALL('Returns Data')
)
```
```java
Average Retail Price = AVERAGE('Product'[ProductPrice])
```
```java
Average Revenue Per Customer = 
DIVIDE(
    [Total Revenue], [Total Customers]
)
```
```java
Bike Return Rate = 
CALCULATE(
    [Return Rate], 'Product Categories'[CategoryName] = "Bikes")
```
```java
Bike Returns = 
CALCULATE([Total Returns], 'Product Categories'[CategoryName] = "Bikes")
```
```java
Bike Sales = CALCULATE(
    [Quantity Sold], 'Product Categories'[CategoryName] = "Bikes")
```
```java
Bulk Orders = 
CALCULATE([Total Orders],'Sales Data'[OrderQuantity] > 1)
```

```java
High Ticket Orders = CALCULATE([Total Orders], 
FILTER('Product', 'Product'[ProductPrice] > [Overall Average Price]))
```
```java
Order Target = [Previous Month Orders]*1.1
```
```java
Order Target Gap = [Total Orders] - [Order Target]
```
```java
Overall Average Price = CALCULATE([Average Retail Price], ALL('Product'))
```
```java
Previous Month Orders = 
CALCULATE(
    [Total Orders],
    DATEADD(
        'Calendar'[Date],
        -1,
        MONTH
    )
)
```
```java
Previous Month Profit = 
CALCULATE(
    [Total Profit],
    DATEADD(
        'Calendar'[Date],
        -1,
        MONTH
    )
)
```
```java
Previous Month Returns = 
CALCULATE(
    [Total Returns],
    DATEADD(
        'Calendar'[Date],
        -1,
        MONTH
    )
)
```
```java
Previous Month Revenue = 
CALCULATE(
    [Total Revenue],
    DATEADD(
        'Calendar'[Date],
        -1,
        MONTH
    )
)
```
```java
Profit Target = 
[Previous Month Profit]*1.1
```
```java
Profit Target Gap = [Total Profit] - [Profit Target]
```
```java
Quantity Returned = SUM('Returns Data'[ReturnQuantity])
```
```java
YTD Revenue = 
 CALCULATE(
    [Total Revenue],
    DATESYTD(
        'Calendar'[Date]
    )
 )
```
### Report
A report was created with the following pages:

**_Executive Dashboard_**
  <p>
    <img src ="https://github.com/angwi/data-analytics-power-bi/blob/main/exec-dashboard.png" alt="Executive Dashboard"/>
  </p>
  
**_Map_**
<p>
  <img src="https://github.com/angwi/data-analytics-power-bi/blob/main/map.png" alt="Map"/>
</p>

**_Product Detail_**
<p>
  <img src="https://github.com/angwi/data-analytics-power-bi/blob/main/product-detail.png" alt="Product Detail"/>
</p>

**_Customer Detail_**
<p>
  <img src="https://github.com/angwi/data-analytics-power-bi/blob/main/customer-detail.png" alt="Customer Detail"/>
</p>

**_Dashboard with Slicer Panel open_**
<p>
  <img src="https://github.com/angwi/data-analytics-power-bi/blob/main/slicer-panel.png" alt="Dashboard with Slicer Panel open"/>
</p>
  
