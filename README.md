# Restaurant Orders Analysis
# Introduction
This project dives into the analysis of a restaurant's order data to uncover insights into menu pricing, customer ordering patterns, and overall restaurant performance. The project is structured to explore the restaurant's menu, analyze order data, and understand customer behavior through SQL queries.
# Background
The objective of this project was to analyze restaurant order data to gain insights into menu item performance, customer preferences, and pricing strategies. By understanding these aspects, the restaurant can optimize its menu offerings and improve customer satisfaction.
# Tools Used
 - **SQL:** SQL was used extensively to query the database and extract valuable insights from the data.
# Analysis
The project was divided into three main objectives:

### Objective 1: Explore the Menu Items
1. Find the number of items on the menu.
```sql
SELECT COUNT(*) FROM menu_items;
```
2. What are the least and most expensive items on the menu?
```sql
-- Least Expensive
SELECT * FROM menu_items
ORDER BY price
LIMIT 5;

-- Most Expensive
SELECT * FROM menu_items
ORDER BY price DESC
LIMIT 5;
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
### Objective 2: Explore the Orders Table
1. What is the data range of the table?
```sql
SELECT MAX(order_date), MIN(order_date)
FROM order_details;
```
2. How many orders were made within this date range?
```sql
SELECT COUNT(DISTINCT order_id)
FROM order_details;
```
3. How many items were ordered within this date range?
```sql
SELECT COUNT(*) 
FROM order_details;
```
4. Which orders had the most number of items?
```sql
SELECT order_id, COUNT(item_id) AS num_items
FROM order_details
GROUP BY order_id
ORDER BY num_items DESC;
```
5. How many orders had more than 12 items?
```sql
SELECT COUNT(*) FROM
	(SELECT order_id, COUNT(item_id) AS num_items
	FROM order_details
	GROUP BY order_id
	HAVING num_items > 12) AS num_orders;
```
### Objective 3: Analyze Customer Behavior
1. Combine the menu_items and orders_details tables into a single table.
```sql
SELECT * 
	FROM order_details od LEFT JOIN menu_items mi
		ON od.item_id = mi.menu_item_id;
```
2. What were the least and most ordered items, and what categories were they in?
```sql
SELECT item_name, category, COUNT(order_details_id) AS num_purchase
	FROM order_details od LEFT JOIN menu_items mi
		ON od.item_id = mi.menu_item_id
	GROUP BY item_name, category
	ORDER BY num_purchase DESC;   -- To know the least and most (just change the DESC (MOST) to ASC(LEAST))
```
3. What were the top 5 orders that spent the most money?
```sql
SELECT order_id, SUM(price) AS total_spend
	FROM order_details od LEFT JOIN menu_items mi
		ON od.item_id = mi.menu_item_id
	GROUP BY order_id
	ORDER BY total_spend DESC
	LIMIT 5;
```
4. View the details of the highest spend order, and what insights can you gather from the result?
```sql
SELECT category, COUNT(item_id) AS num_items
	FROM order_details od LEFT JOIN menu_items mi
		ON od.item_id = mi.menu_item_id
	WHERE order_id = 440
	GROUP BY category;
```
5. View the details of the top 5 highest spend orders, and what insights can you gather from the results?
```sql
SELECT order_id, category, COUNT(item_id) AS num_items
	FROM order_details od LEFT JOIN menu_items mi
		ON od.item_id = mi.menu_item_id
	WHERE order_id IN (440, 2075, 1957, 330, 2675)
	GROUP BY order_id, category;
```
# What I Learned
This project deepened my understanding of SQL and its application in real-world scenarios. I learned how to structure queries to extract meaningful insights from data, as well as the importance of analyzing customer behavior to inform business decisions.

# Conclusion
The analysis of the restaurant's order data revealed important trends in customer preferences and menu performance. By leveraging these insights, the restaurant can refine its offerings and enhance customer satisfaction, ultimately driving growth and profitability.







