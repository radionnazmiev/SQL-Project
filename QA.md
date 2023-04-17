## Risk areas: Completeness, uniqueness and consistency of data.

### QA process:

1. To ensure completeness: 

	Null value checks for null fields in specific columns of relevant tables.

	```
	SELECT "name" 
	FROM products 
	WHERE "name" IS NULL;
	```

2. To ensure uniqueness: 
	
	Duplicate entries check in specific columns of relevant tables.

	```
	SELECT "SKU"
		  , COUNT("SKU") AS duplicates 
	FROM products 
	GROUP BY "SKU" 
	HAVING COUNT("SKU") > 1 
	ORDER BY duplicates;
	```

2. To ensure consistency: 
	
	Tested that total items ordered are in the correct data type.

	```
	SELECT total_ordered 
	FROM sales_reports;

	```

