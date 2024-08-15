# Restaurant Orders Analysis
# Introduction
This project dives into the analysis of a restaurant's order data to uncover insights into menu pricing, customer ordering patterns, and overall restaurant performance. The project is structured to explore the restaurant's menu, analyze order data, and understand customer behavior through SQL queries.
# Background
The objective of this project was to analyze restaurant order data to gain insights into menu item performance, customer preferences, and pricing strategies. By understanding these aspects, the restaurant can optimize its menu offerings and improve customer satisfaction.
# Tools Used
 - **SQL:** SQL was used extensively to query the database and extract valuable insights from the data.
# Analysis
The project was divided into three main objectives:

**Objective 1: Explore the Menu Items**
1. Find the number of items on the menu.
```sql
SELECT COUNT(*) FROM menu_items;
```
2. What are the least and most expensive items on the menu?
```sql
SELECT * FROM menu_items
ORDER BY price;

SELECT * FROM menu_items
ORDER BY price DESC;
```
3. How many Italian dishes are on the menu?
```sql
SELECT COUNT(*) FROM menu_items
WHERE category = 'Italian'
```
4. What are the least and most expensive Italian dishes on the menu?
```sql
SELECT * FROM menu_items
WHERE category = 'Italian'
ORDER BY price;

SELECT * FROM menu_items
WHERE category = 'Italian'
ORDER BY price DESC;
   ```
5. How many dishes are in each category?
```sql
SELECT category, COUNT(menu_item_id) AS num_items
FROM menu_items
GROUP BY category;
   ```
6. What is the average dish price within each category?
```sql
SELECT category, ROUND(AVG(price),1) AS avg_price
FROM menu_items
GROUP BY category;
   ```
**Objective 2: Explore the Orders Table**
1. What is the data range of the table?
2. How many orders were made within this date range?
3. How many items were ordered within this date range?
4. Which orders had the most number of items?
5. How many orders had more than 12 items?

**Objective 3: Analyze Customer Behavior**
1. Combine the menu_items and orders_details tables into a single table.
2. What were the least and most ordered items, and what categories were they in?
3. What were the top 5 orders that spent the most money?
4. View the details of the highest spend order, and what insights can you gather from the result?
5. View the details of the top 5 highest spend orders, and what insights can you gather from the results?





