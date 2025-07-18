-- KMS SQL Case Study Analysis
WHAT I DID
-- View the entire dataset
SELECT *  
FROM [KMS Sql Case Study1];

-- 1. Which product category has the highest number of sales?
SELECT TOP 1 [Product_Category], COUNT([Product_Category]) AS [Product Count]  
FROM [KMS Sql Case Study1]  
GROUP BY Product_Category  
ORDER BY [Product Count] DESC;

-- 2. What are the top 3 and bottom 3 regions in terms of total sales?

-- Top 3 regions
SELECT TOP 3 [Region], SUM([Sales]) AS [Total Sales]  
FROM [KMS Sql Case Study1]  
GROUP BY Region  
ORDER BY [Total Sales] DESC;

-- Bottom 3 regions
SELECT TOP 3 [Region], SUM([Sales]) AS [Total Sales]  
FROM [KMS Sql Case Study1]  
GROUP BY Region  
ORDER BY [Total Sales] ASC;

-- 3. What were the total sales of applicants in Ontario?
SELECT Region, SUM(Sales) AS [Total Sales]  
FROM [KMS Sql Case Study1]  
WHERE Region = 'ontario'  
GROUP BY Region;

-- 4. Advice to KMS on increasing revenue from bottom 10 customers
SELECT TOP 10 [Customer_Name], SUM([Sales]) AS [Total Sales]  
FROM [KMS Sql Case Study1]  
GROUP BY Customer_Name  
ORDER BY [Total Sales] ASC;

-- Recommendation:
-- To boost sales from the bottom 10 customers, focus on:
-- - Personalized promotions
-- - Contact through calls/emails to understand their experience
-- - Discounts based on previous purchases
-- - Upselling and cross-selling
-- - Improved delivery/support
-- - Surveys to discover needs

-- 5. Which shipping method incurred the most shipping cost?
SELECT TOP 1 [Ship_Mode], SUM([Shipping_Cost]) AS [Total Shipping Cost]  
FROM [KMS Sql Case Study1]  
GROUP BY Ship_Mode  
ORDER BY [Total Shipping Cost] DESC;

-- 6. Who are the most valuable customers and what do they purchase?
SELECT [Customer_Name], Product_Name, SUM(Sales) AS [Total Sales]  
FROM [KMS Sql Case Study1]  
GROUP BY Customer_Name, Product_Name  
ORDER BY [Total Sales] DESC;

-- 7. Which small business customer had the highest sales?
SELECT TOP 1 Customer_Name, Customer_Segment, SUM([Sales]) AS [Total Sales]  
FROM [KMS Sql Case Study1]  
WHERE Customer_Segment = 'Small Business'  
GROUP BY Customer_Name, Customer_Segment  
ORDER BY [Total Sales] DESC;

-- 8. Which corporate customer placed the most number of orders (2009-2012)?
SELECT TOP 1 Customer_Name, Customer_Segment, COUNT([Order_ID]) AS [Total Orders]  
FROM [KMS Sql Case Study1]  
WHERE Customer_Segment = 'Corporate' AND Order_Date BETWEEN '2009' AND '2012'  
GROUP BY Customer_Name, Customer_Segment  
ORDER BY [Total Orders] DESC;

-- 9. Which consumer customer was the most profitable one?
SELECT TOP 1 Customer_Name, Customer_Segment, SUM([Profit]) AS [Total Profit]  
FROM [KMS Sql Case Study1]  
WHERE Customer_Segment = 'Consumer'  
GROUP BY Customer_Name, Customer_Segment  
ORDER BY [Total Profit] DESC;

-- 10. Which customer returned items and what segments do they belong to?
SELECT Customer_Name, Customer_Segment, [Status]  
FROM [KMS Sql Case Study1]  
JOIN [dbo].[Order_Status]  
  ON [KMS Sql Case Study1].Order_ID = [dbo].[Order_Status].Order_ID;

-- 11. Did KMS appropriately spend shipping costs based on order priority?
SELECT Order_Priority, Ship_Mode,  
       COUNT([Order_ID]) AS [Order Count],  
       SUM(Sales - Profit) AS [Estimated Shipping Cost],  
       AVG(DATEDIFF(DAY, [Order_Date], [Ship_Date])) AS [Avg Ship Days]  
FROM [KMS Sql Case Study1]  
GROUP BY Order_Priority, Ship_Mode  
ORDER BY Order_Priority, Ship_Mode DESC;

-- Conclusion:
-- No, KMS did not appropriately allocate shipping costs. Delivery trucks (economical) were overused,
-- even for urgent orders, while express air (costly) was underutilized. This resulted in inefficient spending.

-- 12. Total Sales by Customer Segment
SELECT Customer_Segment, SUM(Sales) AS [Total Sales]  
FROM [KMS Sql Case Study1]  
GROUP BY Customer_Segment  
ORDER BY [Total Sales] DESC;

-- Duplicate of all above added queries (ensure no missing addition):

-- Dataset overview
SELECT *  
FROM [KMS Sql Case Study1];

-- Top product category
SELECT TOP 1 [Product_Category], COUNT([Product_Category]) AS [Product Count]  
FROM [KMS Sql Case Study1]  
GROUP BY Product_Category  
ORDER BY [Product Count] DESC;

-- Top & bottom regions
SELECT TOP 3 [Region], SUM([Sales]) AS [Total Sales]  
FROM [KMS Sql Case Study1]  
GROUP BY Region  
ORDER BY [Total Sales] DESC;

SELECT TOP 3 [Region], SUM([Sales]) AS [Total Sales]  
FROM [KMS Sql Case Study1]  
GROUP BY Region  
ORDER BY [Total Sales] ASC;

-- Ontario sales
SELECT Region, SUM(Sales) AS [Total Sales]  
FROM [KMS Sql Case Study1]  
WHERE Region = 'ontario'  
GROUP BY Region;

-- Bottom 10 customers
SELECT TOP 10 [Customer_Name], SUM([Sales]) AS [Total Sales]  
FROM [KMS Sql Case Study1]  
GROUP BY Customer_Name  
ORDER BY [Total Sales] ASC;

-- Shipping method cost
SELECT TOP 1 [Ship_Mode], SUM([Shipping_Cost]) AS [Total Shipping Cost]  
FROM [KMS Sql Case Study1]  
GROUP BY Ship_Mode  
ORDER BY [Total Shipping Cost] DESC;

-- Valuable customers and products
SELECT [Customer_Name], Product_Name, SUM(Sales) AS [Total Sales]  
FROM [KMS Sql Case Study1]  
GROUP BY Customer_Name, Product_Name  
ORDER BY [Total Sales] DESC;

-- Top small business customer
SELECT TOP 1 Customer_Name, Customer_Segment, SUM([Sales]) AS [Total Sales]  
FROM [KMS Sql Case Study1]  
WHERE Customer_Segment = 'Small Business'  
GROUP BY Customer_Name, Customer_Segment  
ORDER BY [Total Sales] DESC;

-- Top corporate customer by orders (2009–2012)
SELECT TOP 1 Customer_Name, Customer_Segment, COUNT([Order_ID]) AS [Total Orders]  
FROM [KMS Sql Case Study1]  
WHERE Customer_Segment = 'Corporate' AND Order_Date BETWEEN '2009' AND '2012'  
GROUP BY Customer_Name, Customer_Segment  
ORDER BY [Total Orders] DESC;

-- Most profitable consumer
SELECT TOP 1 Customer_Name, Customer_Segment, SUM([Profit]) AS [Total Profit]  
FROM [KMS Sql Case Study1]  
WHERE Customer_Segment = 'Consumer'  
GROUP BY Customer_Name, Customer_Segment  
ORDER BY [Total Profit] DESC;

-- Returned orders and segments
SELECT Customer_Name, Customer_Segment, [Status]  
FROM [KMS Sql Case Study1]  
JOIN [dbo].[Order_Status]  
  ON [KMS Sql Case Study1].Order_ID = [dbo].[Order_Status].Order_ID;

-- Shipping cost analysis by order priority
SELECT Order_Priority, Ship_Mode,  
       COUNT([Order_ID]) AS [Order Count],  
       SUM(Sales - Profit) AS [Estimated Shipping Cost],  
       AVG(DATEDIFF(DAY, [Order_Date], [Ship_Date])) AS [Avg Ship Days]  
FROM [KMS Sql Case Study1]  
GROUP BY Order_Priority, Ship_Mode  
ORDER BY Order_Priority, Ship_Mode DESC;

-- Sales by Segment
SELECT Customer_Segment, SUM(Sales) AS [Total Sales]  
FROM [KMS Sql Case Study1]  
GROUP BY Customer_Segment  
ORDER BY [Total Sales] DESC;
