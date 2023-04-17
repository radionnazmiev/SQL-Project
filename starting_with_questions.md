Answer the following questions and provide the SQL queries used to find the answer.

    
**Question 1: Which cities and countries have the highest level of transaction revenues on the site?**


* SQL Queries:

```
SELECT city
      , country
      , SUM(transactionrevenue) AS total_revenue
FROM all_sessions
WHERE city != 'not available in demo dataset' 
  AND country != 'not available in demo dataset' 
  AND city != 'not set' AND country != 'not set'
GROUP BY city, country
ORDER BY total_revenue DESC
LIMIT 1;
```


* Answer:

  The city and country with the highest level of transaction revenue on the site is [insert city and country name here], with a total revenue of 1015480000.	



**Question 2: What is the average number of products ordered from visitors in each city and country?**


* SQL Queries:


```
SELECT city
    , country
    , AVG(total_ordered) AS average_products_ordered
FROM all_sessions
WHERE city != 'not available in demo dataset' 
  AND country != 'not available in demo dataset' 
  AND city != 'not set' 
  AND country != 'not set' 
  AND total_ordered != '0'
GROUP BY city, country;
```


* Answer:

  For example, the average number of products ordered by visitors in Melbourne, Australia is 105.00.


**Question 3: Is there any pattern in the types (product categories) of products ordered from visitors in each city and country?**


* SQL Queries:

```
SELECT country
      , city
      , "v2ProductCategory"
      , COUNT(*) AS category_count
FROM all_sessions
WHERE city != 'not available in demo dataset'
AND country != 'not available in demo dataset'
AND city != 'not set'
AND country != 'not set'
AND "v2ProductCategory" IS NOT NULL
GROUP BY country, city, "v2ProductCategory"
ORDER BY country, category_count DESC;
```


* Answer:

  Turned out that the "Home" category had the highest number of product orders in most all cities and countries.



**Question 4: What is the top-selling product from each city/country? Can we find any pattern worthy of noting in the products sold?**


* SQL Queries:


```
SELECT city
      , country, name
      , MAX(total_ordered) as highest_ordered
FROM all_sessions
JOIN sales_report 
  ON all_sessions.productsku = sales_report.productsku 
WHERE city != 'not set' 
  AND country != 'not set'
GROUP BY city, country, name
ORDER BY city, country, highest_ordered DESC;
```


* Answer:

  In Amsterdam, Netherlands, the top-selling product was "Blue Sneakers"


**Question 5: Can we summarize the impact of revenue generated from each city/country?**

* SQL Queries:

```
SELECT country
      , city
      , SUM(transactionrevenue) AS total_revenue
FROM all_sessions
JOIN products 
  ON all_sessions.productsku = products.sku
WHERE country != '(not set)'
  AND city != '(not set)'
  AND city != 'not available in demo dataset'
  AND country != 'not available in demo dataset'
GROUP BY country, city
ORDER BY total_revenue DESC
```

* Answer:

  The USA panned out to had generetad the highest total revenue




