# Select 
__1757. Recyclable and Low Fat Products__

Write a solution to find the ids of products that are both low fat and recyclable.
Return the result table in any order.

Input: 
Products table:
+-------------+----------+------------+
| product_id  | low_fats | recyclable |
+-------------+----------+------------+
| 0           | Y        | N          |
| 1           | Y        | Y          |
| 2           | N        | Y          |
| 3           | Y        | Y          |
| 4           | N        | N          |
+-------------+----------+------------+
Output: 
+-------------+
| product_id  |
+-------------+
| 1           |
| 3           |
+-------------+

__Solution:__
```sql
SELECT product_id
FROM products
WHERE low_fats = 'Y'
  AND recyclable = 'Y'
```

