# Issues I had to address by cleaning the data

### Queries:


1. I checked for any rows in all_sessions that have no relation to products table and removed them

```
DELETE FROM all_sessions
WHERE productSKU IN(
	SELECT all_sessions.productSKU 
	FROM all_sessions
	LEFT JOIN products
	ON all_sessions.productSKU = products.SKU
	WHERE SKU is NULL) 
```

2. All the coutries and cities in all_sessions that had no values need to be removed

```
DELETE FROM all_sessions
WHERE fullvisitorid IN 
	(SELECT fullvisitorid 
	FROM all_sessions
	WHERE (country = '(not set)' 
				OR country = 'not available in demo dataset') 
		 OR (city = '(not set)' 
		 		OR city = 'not available in demo dataset'))
```

3. Moved total_ordered column over to products table as there was no reason for having another products related table

```
SELECT * 
FROM products
LEFT JOIN sales_by_sku
ON products.sku = sales_by_sku.productsku
WHERE products.sku IS NULL

ALTER TABLE products 
ADD COLUMN total_ordered int

UPDATE products
SET total_ordered = (
    SELECT total_ordered
    FROM sales_by_sku
    WHERE products.sku = sales_by_sku.productsku
);

DROP TABLE sales_by_sku
```

4. To merge sales_repot into products table I had to merge tables with a help of natural join

```
SELECT * INTO products2 FROM(
	SELECT productsku
		 , name
		 , orderedquantity
		 , total_ordered
		 , stocklevel
		 , restockingleadtime
		 , sentimentscore
		 , sentimentmagnitude
		 , ratio  
	FROM products 
	NATURAL FULL JOIN sales_report) as sub
	
DROP TABLE products
DROP TABLE sales_report
ALTER TABLE products2 RENAME TO products
```

5. Renamed column names for better readability, fiqured out how ratio colum was calculated and filled in missing values

```
ALTER TABLE products 
RENAME productsku 
TO sku	

ALTER TABLE products 
RENAME orderedquantity 
TO ordered_quantity	

ALTER TABLE products 
RENAME restockingleadtime 
TO restocking_leadtime	

ALTER TABLE products 
RENAME stocklevel 
TO stock_level	

ALTER TABLE products 
RENAME sentimentscore 
TO sentiment_score

ALTER TABLE products 
RENAME sentimentmagnitude 
TO sentiment_magnitude

SELECT * 
FROM products
WHERE ratio IS NULL

UPDATE products
SET ratio = total_ordered/stock_level
WHERE stock_level IS NOT NULL 
	AND ratio IS NULL 
	AND total_ordered IS NOT NULL
```
