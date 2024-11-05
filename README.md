#### LITA_PROJECT_CUSTOMER_DATA-ANALYSIS

### Project Title: Customer Data For Subscription Services

### Project Overview: 
Analysis of Customer Data for a Subscription Service to Identify Segments, Trends, Patterns, and Insights that inform business decicions, improve sales strategies, and enchance customer relationships.

### Tools Used
- Excel
- SQL
- Power BI


### Project Structure:
- Excel: Contains Excel files for data analysis.
- SQL: Contains SQL queries for data extraction.
- Power BI: Contains Power BI dashboard files.
- Data: Contains customer data(XLXS & CSV) files.


### Excel Files:
- Subscription Patterns: Pivot tables analyzing subscription patterns.
- Average Subscription Duration: Calculations for average subscription duration.

### SQL Queries:
- customer_insights: Queries for total customers by region, popular subscription types, canceled subscriptions, average subscription duration, short and long-term subscriptions, total revenue, and subscription cancellations.

### Power BI Dashboard:
- Subscription Service Dashboard: Visualizations of key customer segments, cancellations, and subscription trends.

### Data Files:
- customer_data: Customer data used for analysis.


### Instructions:

1. Clone the repository.
2. Load the customer data into your SQL Server environment.
3. Run SQL queries to extract insights.
4. Open Excel files to view pivot tables and calculations.
5. Open Power BI dashboard file to visualize insights.

### SQL Queries Documentation:
CREATE DATABASE RUTH_02
```
Select * From [dbo].[CUSTOMER'S DATA1]
```

--------Total number of Customers from each Region---------

```
Select Region, Count(CustomerName) as 
Total_Customer
From [dbo].[CUSTOMER'S DATA1]
Group By  Region;
```

-------Most popupar subscription type by number of customer-------

```
Select SubscriptionType, Count(CustomerName) as Total_Customer
From[dbo].[CUSTOMER'S DATA1]
Group By SubscriptionType
Order By Total_Customer desc;
```

-----Customer who canceled their subscription within 6 months-------

```
Select customerid,subscriptionstart, subscriptionend
From [dbo].[CUSTOMER'S DATA1]
Where subscriptionend IS NULL AND
DATEDIFF(month, SubscriptionStart, SubscriptionEnd) <= 180;
```

--------Average subscription duration for all Customers-------------

```
Select AVG(DATEDIFF(day, subscriptionstart, isnull(subscriptionend,
getdate ()))) as avgsubscriptionduration
From [dbo].[CUSTOMER'S DATA1];
```


------- Customers With subscription longer than 12months---------

```
Select 
     customerid,
	 subscriptionstart,
	 subscriptionend
From [dbo].[CUSTOMER'S DATA1]
Where
     DATEDIFF(Month, subscriptionstart, isnull(subscriptionend, getdate())) > 365;
```


------------Calculate total revenue by subscriptiontype---------

```
Select subscriptiontype, Sum(Revenue) as Total_Revenue
from [dbo].[CUSTOMER'S DATA1]
Group By subscriptiontype;
```

----------Top 3 Regions by subscription Cancellation-----------

```
Select Region,Count(*) as Total_Cancellations
From [dbo].[CUSTOMER'S DATA1]
Where subscriptionend IS NULL
Group By Region 
Order By Total_Cancellations desc;
```


----------------Total number of active and canceled subscriptions
Select Sum(CASE WHEN subscriptionend IS NULL THEN 1 ELSE 0 END) as Active_Subscription,
SUM(CASE WHEN subscriptionend IS NOT NULL THEN 1 ELSE 0 END) as Canceled_Subscription
From [dbo].[CUSTOMER'S DATA1]
```


### Visualiztion
