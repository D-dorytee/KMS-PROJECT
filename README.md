-- 📊 **KMS SQL Case Study Analysis**

WHAT I DID

```sql
-- 🔍 View the entire dataset
SELECT *
FROM [KMS Sql Case Study1];

-- 🏆 Product category with the highest number of orders
SELECT TOP 1 [Product_Category], COUNT([Product_Category]) AS [Product Count]
FROM [KMS Sql Case Study1]
GROUP BY Product_Category
ORDER BY [Product Count] DESC;

-- 🌍 Top 3 regions by total sales
SELECT TOP 3 [Region], SUM([Sales]) AS [Total Sales]
FROM [KMS Sql Case Study1]
GROUP BY Region
ORDER BY [Total Sales] DESC;

-- 🌍 Bottom 3 regions by total sales
SELECT TOP 3 [Region], SUM([Sales]) AS [Total Sales]
FROM [KMS Sql Case Study1]
GROUP BY Region
ORDER BY [Total Sales] ASC;

-- 🧾 Total sales in Ontario region
SELECT Region, SUM(Sales) AS [Total Sales]
FROM [KMS Sql Case Study1]
WHERE Region = 'ontario'
GROUP BY Region;

-- 💡 Bottom 10 customers by sales
SELECT TOP 10 [Customer_Name], SUM([Sales]) AS [Total Sales]
FROM [KMS Sql Case Study1]
GROUP BY Customer_Name
ORDER BY [Total Sales] ASC;
```

**📝 Recommendation:**
> To improve revenue from these customers:
> - Offer targeted promotions or bundle deals
> - Reconnect via direct calls/emails
> - Analyze past buying behavior
> - Provide better delivery/after-sales service
> - Use loyalty programs and surveys

```sql
-- 🚚 Shipping method with the highest cost
SELECT TOP 1 [Ship_Mode], SUM([Shipping_Cost]) AS [Total Shipping Cost]
FROM [KMS Sql Case Study1]
GROUP BY Ship_Mode
ORDER BY [Total Shipping Cost] DESC;

-- 👑 Most valuable customers and what they purchase
SELECT [Customer_Name], Product_Name, SUM(Sales) AS [Total Sales]
FROM [KMS Sql Case Study1]
GROUP BY Customer_Name, Product_Name
ORDER BY [Total Sales] DESC;

-- 🧍‍♂️ Highest sales by a small business customer
SELECT TOP 1 Customer_Name, Customer_Segment, SUM([Sales]) AS [Total Sales]
FROM [KMS Sql Case Study1]
WHERE Customer_Segment = 'Small Business'
GROUP BY Customer_Name, Customer_Segment
ORDER BY [Total Sales] DESC;

-- 🏢 Most orders by a corporate customer (2009–2012)
SELECT TOP 1 Customer_Name, Customer_Segment, COUNT([Order_ID]) AS [Total Orders]
FROM [KMS Sql Case Study1]
WHERE Customer_Segment = 'Corporate' AND Order_Date BETWEEN '2009' AND '2012'
GROUP BY Customer_Name, Customer_Segment
ORDER BY [Total Orders] DESC;

-- 💰 Most profitable consumer segment customer
SELECT TOP 1 Customer_Name, Customer_Segment, SUM([Profit]) AS [Total Profit]
FROM [KMS Sql Case Study1]
WHERE Customer_Segment = 'Consumer'
GROUP BY Customer_Name, Customer_Segment
ORDER BY [Total Profit] DESC;

-- 🔄 Customers who returned items and their segments
SELECT Customer_Name, Customer_Segment, [Status]
FROM [KMS Sql Case Study1]
JOIN [dbo].[Order_Status]
  ON [KMS Sql Case Study1].Order_ID = [dbo].[Order_Status].Order_ID;

-- ⚖️ Alignment between shipping method and order priority
SELECT Order_Priority, Ship_Mode,
       COUNT([Order_ID]) AS [Order Count],
       SUM(Sales - Profit) AS [Estimated Shipping Cost],
       AVG(DATEDIFF(DAY, [Order_Date], [Ship_Date])) AS [Avg Ship Time]
FROM [KMS Sql Case Study1]
GROUP BY Order_Priority, Ship_Mode
ORDER BY Order_Priority, Ship_Mode DESC;
```

**💡 Insight:**
> Express Air (faster) was underused for urgent orders, while Delivery Truck (cheaper) was overused.
> This mismatch resulted in delayed deliveries and inefficient spending.

```sql
-- 🧮 Total sales by customer segment
SELECT Customer_Segment, SUM(Sales) AS [Total Sales]
FROM [KMS Sql Case Study1]
GROUP BY Customer_Segment
ORDER BY [Total Sales] DESC;
```



