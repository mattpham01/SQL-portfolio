/* 
Dataset: Customer Shopping Trends Dataset
Source: https://www.kaggle.com/datasets/iamsouravbanerjee/customer-shopping-trends-dataset?select=shopping_trends_updated.csv
Query Editor: pgAdmin 4
/*

--Create table and import that dataset from Kaggle
CREATE TABLE shopping_trends(
  customer_id INTEGER PRIMARY KEY,
  age INTEGER,
  gender TEXT,
  item_purchased VARCHAR(20),
  category VARCHAR(20), 
  purchase_amount INTEGER,
  location VARCHAR(20),
  size TEXT,
  color TEXT, 
  season TEXT,
  review_rating DECIMAL,
  subscription_status TEXT,
  discount_applied TEXT,
  shipping_type VARCHAR(20),
  discount_applied TEXT,
  promo_code TEXT,
  payment_method VARCHAR(20)
  frequency_of_purchases VARCHAR(20)
);

--Busines Questions 
--1. What are the most popular categories of items amongst diffrent age groups?

SELECT age_range, category, COUNT(*) AS purchase_count
FROM(

	SELECT customer_id, age, item_purchased, category,
	CASE
		WHEN (age BETWEEN 18 and 24) THEN '18-24'
		WHEN (age BETWEEN 25 AND 34) THEN '25-34'
		WHEN (age BETWEEN 35 AND 44) THEN '35-44'
		WHEN (age BETWEEN 45 AND 54) THEN '45-54'
		ELSE '55+'
	END AS age_range
	FROM shopping_trends
) AS age_categorized
GROUP BY age_range, category
ORDER BY age_range, purchase_count DESC;


--2. What are the top 5 most frequently purchased items?

SELECT item_purchased, COUNT(*) AS purchase_count
FROM shopping_trends
GROUP BY item_purchased
ORDER BY purchase_count DESC
LIMIT 5;


--3. What is the percentage of one time customers?

SELECT ROUND((COUNT(CASE WHEN previous_purchases = 1 THEN 1 END) * 100.0 / COUNT(*)), 2) AS percentage_one_time_customers
FROM shopping_trends


--4. What is the total purchase amount from each customer?

SELECT customer_id, SUM(purchase_amount) AS total_spent
FROM shopping_trends
GROUP BY customer_id 
ORDER BY total_spent DESC; 


--5. What is the most popular item in each season? 

SELECT season, item_purchased, COUNT(*) AS purchase_count  
FROM shopping_trends  
GROUP BY season, item_purchased  
ORDER BY season, purchase_count DESC;


--6. In which season did customers purchase the most?

SELECT season, COUNT(*) AS total_purchases
FROM shopping_trends
GROUP BY season
ORDER BY total_purchases DESC
LIMIT 1;


--7. What is the average amount spent for customer's that have a subscription? Customer's without a subscription?

SELECT ROUND(AVG(purchase_amount), 2) AS total_spent
FROM shopping_trends 
WHERE subscription_status = 'Yes'

SELECT ROUND(AVG(purchase_amount), 2) AS total_spent
FROM shopping_trends 
WHERE subscription_status = ‘No’


--8. What is the most popular payment method amongst consumers that used promo codes?

SELECT payment_method, COUNT(*) AS usage_count
FROM shopping_trends 
WHERE promo_code = 'Yes'
GROUP BY payment_method
ORDER BY usage_count DESC
LIMIT 1


--9. Identify the top 3 locations where frequent consumers purchase the most

SELECT location, SUM(purchase_amount) AS total_spent 
FROM shopping_trends 
WHERE frequency_of_purchases = 'Weekly'
GROUP BY location
ORDER BY total_spent DESC
LIMIT 3;


--10. Rank the customers based on their total spending

SELECT customer_id, SUM(purchase_amount) AS total_spent,  
       DENSE_RANK() OVER (ORDER BY SUM(purchase_amount) DESC) AS rank  
FROM shopping_trends  
GROUP BY customer_id
ORDER BY rank 


--11. How many high spenders are there? Medium? Low? What's the percentage of each?

WITH customer_segments AS (
    SELECT customer_id, 
           SUM(purchase_amount) AS total_spent,
           CASE 
               WHEN SUM(purchase_amount) > 75 THEN 'High Spender'
               WHEN SUM(purchase_amount) BETWEEN 40 AND 76 THEN 'Medium Spender'
               ELSE 'Low Spender'
           END AS spending_segment
    FROM shopping_trends
    GROUP BY customer_id
)
SELECT spending_segment, 
       COUNT(*) AS customer_count, 
       ROUND((COUNT(*) * 100.0 / (SELECT COUNT(*) FROM customer_segments)), 2) AS percentage
FROM customer_segments
GROUP BY spending_segment
ORDER BY percentage DESC;


