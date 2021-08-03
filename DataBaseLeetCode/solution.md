[Easy](https://zhuanlan.zhihu.com/p/265354299)
## Question 39



- `(product_id, start_date, end_date)` is the primary key for this table.
- Each row of this table indicates the price of the product_id in the period from start_date to end_date.
- For each product_id there will be no two overlapping periods. That means there will be no two intersecting periods for the same product_id.

- There is no primary key for this table, it may contain duplicates.
- Each row of this table indicates the date, units and product_id of each product sold. 
 
### Question
Write an SQL query to find the average selling price for each product.  
- `average_price` should be rounded to 2 decimal places.  

- Average selling price = Total Price of Product / Number of products sold.
- Average selling price for product 1 = ((100 * 5) + (15 * 20)) / 115 = 6.96
- Average selling price for product 2 = ((200 * 15) + (30 * 30)) / 230 = 16.96

### Solution
```sql
select UnitsSold.product_id, round(sum(units*price)/sum(units), 2) as average_price
from UnitsSold inner join Prices
on UnitsSold.product_id = Prices.product_id
and UnitsSold.purchase_date between Prices.start_date and Prices.end_date
group by UnitsSold.product_id
```


## [Find The Bests Seller](https://code.dennyzhang.com/sales-analysis-i)    

```mysql
SELECT seller_id
FROM Sales
GROUP BY seller_id
HAVING SUM(price) = (SELECT SUM(price)
                    FROM Sales
                    GROUP BY seller_id
                    ORDER BY SUM(price) DESC
                    LIMIT 1)
```

## https://zhuanlan.zhihu.com/p/259935444


## [Second Highest Salary](https://zhuanlan.zhihu.com/p/250015043)

Write a SQL query to get the second highest salary from the Employee Table.    

For example, given the above Employee table, the query should return 200 as the second highest salary.  
If there is no second highest salary, then the query should return null.
```mysql
SELECT
 (SELECT DISTINCT Salary
  FROM Employee
  ORDER BY Salary DESC
  LIMIT 1 OFFSET 1) 
AS SecondHighestSalary;
```

## [Duplicate Emails](https://zhuanlan.zhihu.com/p/251960784)

Write a SQL query to find all duplicate emails in a table named Person.  

For example, your query should return the following for the above table:

```mysql
SELECT Email FROM
  /**Create A table showing total ount of each mail**/
 (SELECT Email, COUNT(id) AS num
  FROM Person
  GROUP BY Email) AS tmp
WHERE num > 1;
```

```mysql
SELECT DISTINCT a.Email FROM Person AS a
JOIN Person AS b
ON a.Email = b.Email
AND a.Id <> b.Id;
```
## [Customers Who Never Order](https://zhuanlan.zhihu.com/p/251983949)

Write a SQL query to find all customers who never order anything.  

### Concept 
1. using `LEFT JOIN` 
2. using nested query with `where ... not in (nested query)`


## [Rising Temperature](https://zhuanlan.zhihu.com/p/252403796)  

Write an SQL query to find all dates' id with higher temperature compared to its previous dates (yesterday).

1. using `JOIN` to compare two samae table via function
   > `DATEDIFF(date1, date2) = Difference`   
   > `DATE_SUB`    
   > `DATE_ADD`   
   > `SUB_DATE`    

## [Delete Duplicate Emails](https://zhuanlan.zhihu.com/p/252243481)   


Write a SQL query to delete all duplicate email entries in a table named Person, keeping only unique emails based on its smallest Id. For example, after running your query, the above Person table should have the following rows:

```
+----+------------------+
| Id | Email            |
+----+------------------+
| 1  | john@example.com |
| 2  | bob@example.com  |
| 3  | john@example.com |
+----+------------------+

Result 
+----+------------------+
| Id | Email            |
+----+------------------+
| 1  | john@example.com |
| 2  | bob@example.com  |
+----+------------------+
```

Concept

Zwei Tabellen vergleichen via
1. `DELETE FROM ... WHERE ... NOT IN (NESTED QUERY) ` 
2. `DELETE FROM ... WHERE ... AND ...`

```mysql
-- TABLE B
-- +----+------------------+
-- | Id | Email            |
-- +----+------------------+
-- | 1  | john@example.com |
-- | 2  | bob@example.com  |
-- +----+------------------+

-- TMP      P
-- +----+   +----+
-- |Id  |   | Id | 
-- +----+   +----+
-- | 1  |   | 1  | 
-- | 2  |   | 2  | 
-- +----+   | 3  | 
--          +----+

DELETE FROM Person AS P
WHERE Id NOT IN
(SELECT MinId FROM
 (SELECT Email, MIN(Id) AS MinId FROM Person AS B 
  GROUP BY Email) AS TMP);
  


-- TABLE P
-- +----+------------------+
-- | Id | Email            |
-- +----+------------------+
-- | 1  | john@example.com |
-- | 2  | bob@example.com  |
-- | 3  | john@example.com |----+
-- +----+------------------+    |
                                |
-- TABLE TMP                    |
-- +----+------------------+    |
-- | Id | Email            |    |
-- +----+------------------+    |
-- | 1  | john@example.com | <--+
-- | 2  | bob@example.com  |
-- | 3  | john@example.com |
-- +----+------------------+

DELETE P FROM Person P, Person TMP
WHERE P.Id >  TMP.Id AND P.Email = TMP.Email
```

## [Game Play Analysis I](https://zhuanlan.zhihu.com/p/254355214)


Write an SQL query that reports the first login date for each player.

```diff
Activity table:
+-----------+-----------+------------+--------------+
| player_id | device_id | event_date | games_played |
+-----------+-----------+------------+--------------+
| 1         | 2         | 2016-03-01 | 5            | ---+
| 1         | 2         | 2016-05-02 | 6            |    |    
| 2         | 3         | 2017-06-25 | 1            | ---|---+     
| 3         | 1         | 2016-03-02 | 0            | ---|---|-----+  
| 3         | 4         | 2018-07-03 | 5            |    |   |     |
+-----------+-----------+------------+--------------+    |   |     |
                                                         |   |     |
Result table:                                            |   |     |
+-----------+-------------+                              |   |     |
| player_id | first_login |                              |   |     |
+-----------+-------------+                              |   |     |
| 1         | 2016-03-01  |<-----------------------------+   |     |
| 2         | 2017-06-25  |<---------------------------------+     |
| 3         | 2016-03-02  |<---------------------------------------+
+-----------+-------------+



+-----------+-----------+------------+--------------+
| player_id | device_id | event_date | games_played |
+-----------+-----------+------------+--------------+
| 1         | 2         | 2016-03-01 | 5            | 
| 1         | 2         | 2016-05-02 | 6            |    
| 2         | 3         | 2017-06-25 | 1            |   
| 3         | 1         | 2016-03-02 | 0            | 
| 3         | 4         | 2018-07-03 | 5            |  
+-----------+-----------+------------+--------------+   


+-----------+------------+
| player_id | event_date |
+-----------+------------+
| 1         | 2016-03-01 |
| 2         | 2017-06-25 |
| 3         | 2016-03-02 |
+-----------+------------+

+-----------+-------------+
| player_id | first_login | 
+-----------+-------------+ 
| 1         | 2016-03-01  | 
| 2         | 2017-06-25  | 
| 3         | 2016-03-02  | 
+-----------+-------------+ 
```

```mysql

SELECT player_id, min(event_date) AS first_login
FROM activity 
GROUP BY player_id
ORDER BY player_id;
```


## [Game Play Analysis II](https://zhuanlan.zhihu.com/p/254370126)

Write a SQL query that reports the device that is first logged in for each player.
```diff
Activity table:
+-----------+-----------+------------+--------------+
| player_id | device_id | event_date | games_played |
+-----------+-----------+------------+--------------+
| 1         | 2         | 2016-03-01 | 5            |
| 1         | 2         | 2016-05-02 | 6            |
| 2         | 3         | 2017-06-25 | 1            |
| 3         | 1         | 2016-03-02 | 0            |
| 3         | 4         | 2018-07-03 | 5            |
+-----------+-----------+------------+--------------+

Result table:
+-----------+-----------+
| player_id | device_id |
+-----------+-----------+
| 1         | 2         |
| 2         | 3         |
| 3         | 1         |
+-----------+-----------+
```

```mysql
-- Activity
-- +-----------+-----------+------------+--------------+
-- | player_id | device_id | event_date | games_played |
-- +-----------+-----------+------------+--------------+
-- | 1         | 2         | 2016-03-01 | 5            |
-- | 1         | 2         | 2016-05-02 | 6            |
-- | 2         | 3         | 2017-06-25 | 1            |
-- | 3         | 1         | 2016-03-02 | 0            |
-- | 3         | 4         | 2018-07-03 | 5            |
-- +-----------+-----------+------------+--------------+

-- Table Result
-- +-----------+-----------+------------+--------------+
-- | player_id | device_id | event_date | games_played |
-- +-----------+-----------+------------+--------------+
-- | 1         | 2         | 2016-03-01 | 5            |
-- | 1         | 2         | 2016-05-02 | 6            |----------+
-- | 2         | 3         | 2017-06-25 | 1            |----+     |
-- | 3         | 1         | 2016-03-02 | 0            |--+  |    |  
-- | 3         | 4         | 2018-07-03 | 5            |  |  |    |
-- +-----------+-----------+------------+--------------+  |  |    |
                                                          |  |    |
-- TMP                                                    |  |    |
-- +-----------+-----------+------------+--------------+  |  |    |
-- | player_id | device_id | event_date | games_played |  |  |    |
-- +-----------+-----------+------------+--------------+  |  |    |
-- | 1         | 2         | 2016-03-01 | 5            |<-|--|----+    
-- | 2         | 3         | 2017-06-25 | 1            |<-|--+
-- | 3         | 1         | 2016-03-02 | 0            |<-+
-- +-----------+-----------+------------+--------------+


SELECT player_id, device_id FROM Activity AS Result
WHERE player_id IN (SELECT player_id, min(event_date) from Activity As TMP GROUP BY player_id )
```


## [Employee Bonus](https://zhuanlan.zhihu.com/p/258318063)

Select all employee's name and bonus whose bonus is < 1000.

```mysql
SELECT a.name, 
b.bonus
FROM Employee AS a
LEFT JOIN Bonus AS b
ON a.empId = b.empId
WHERE b.bonus < 1000 OR b.bonus IS NULL;
```

## [https://zhuanlan.zhihu.com/p/258700620](Customer Placing the Largest Number of Orders)


```mysql
SELECT customer_number FROM orders
GROUP BY customer_number
ORDER BY COUNT(*) DESC
LIMIT 1;
```
