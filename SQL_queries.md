**Statistics**

```sql
  SELECT MIN(rental_rate) AS min_rent,
       MAX(rental_rate) AS max_rent,
       AVG(rental_rate) AS avg_rent,
	   
	   MIN(length) AS min_length,
   	   MAX(length) AS max_length,
	   AVG(length) AS avg_length,
	   
	   MIN(replacement_cost) AS min_replacement_cost,
	   MAX(replacement_cost) AS max_replacement_cost,
	   AVG(replacement_cost) AS avg_replacement_cost,
       
	   COUNT(rental_rate) AS count_rent_values,
       COUNT(*) AS count_rows
FROM film;									
```
										
**Mode film**

```sql
SELECT MODE() WITHIN GROUP (ORDER BY rating)
       AS modal_value
FROM film;
```	

**Mode customer**

```sql
SELECT MODE() WITHIN GROUP (ORDER BY store_id)
       AS modal_value
FROM customer;
```
		
**Top country**

```sql
SELECT D.country,
	   COUNT(customer_id) AS customer_number
FROM customer A
INNER JOIN address B ON A.address_id = B.address_id
INNER JOIN city C ON B.city_id = C.city_id
INNER JOIN country D ON C.country_ID = D.country_ID
GROUP BY country
ORDER BY customer_number DESC
LIMIT 10
```

**10 cities**

```sql
SELECT C.city, COUNT(customer_id) AS customer_number
FROM customer A
JOIN address B ON A.address_id = B.address_id
JOIN city C ON B.city_id = C.city_id
JOIN country D ON C.country_id = D.country_id
WHERE D.country IN (
    SELECT D.country
    FROM customer A
    JOIN address B ON A.address_id = B.address_id
    JOIN city C ON B.city_id = C.city_id
    JOIN country D ON C.country_ID = D.country_ID
    GROUP BY D.country
    ORDER BY COUNT(customer_id) DESC
    LIMIT 10
)
GROUP BY C.city
ORDER BY customer_number DESC
LIMIT 10;
```
**5 customers**
```sql
SELECT A.customer_id,
	   A.first_name,
	   A.last_name,
	   D.country,
	   C.city,
	   SUM (E.amount) AS total_amount_paid
FROM customer A
JOIN address B ON A.address_id = B.address_id
JOIN city C ON B.city_id = C.city_id
JOIN country D ON C.country_id = D.country_id
JOIN payment E ON A.customer_id = E.customer_id
WHERE D.country IN (
    SELECT D.country
    FROM customer A
    JOIN address B ON A.address_id = B.address_id
    JOIN city C ON B.city_id = C.city_id
    JOIN country D ON C.country_ID = D.country_ID
    GROUP BY D.country
    ORDER BY COUNT(customer_id) DESC
    LIMIT 10
)
GROUP BY A.customer_id, D.country, C.city_id
ORDER BY total_amount_paid DESC
LIMIT 5;
```					
					
					
					
					
					
					
					
					
					
					
					
					
					
					
					
					
					
					
					
					
					
					
					
					
					
	
		
		
		
		
		
		
		
		
		

		
		
										
										
										
										
										
