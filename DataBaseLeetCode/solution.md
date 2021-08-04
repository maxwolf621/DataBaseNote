[Easy](https://zhuanlan.zhihu.com/p/265354299)
## [Average Selling Price]()


```
Prices table
+------------+------------+------------+--------+
| product_id | start_date | end_date   | price  |
+------------+------------+------------+--------+
| 1          | 2019-02-17 | 2019-02-28 | 5      |
| 1          | 2019-03-01 | 2019-03-22 | 20     |
| 2          | 2019-02-01 | 2019-02-20 | 15     |
| 2          | 2019-02-21 | 2019-03-31 | 30     |
+------------+------------+------------+--------+
- `(product_id, start_date, end_date)` is the primary key for this table.
- For each product_id there will be no two overlapping periods. That means there will be no two intersecting periods for the same product_id.

UnitsSold table:
+------------+---------------+-------+
| product_id | purchase_date | units |
+------------+---------------+-------+
| 1          | 2019-02-25    | 100   |
| 1          | 2019-03-01    | 15    |
| 2          | 2019-02-10    | 200   |
| 2          | 2019-03-22    | 30    |
+------------+---------------+-------+
- There is no primary key for this table, it may contain duplicates.

Result table:
+------------+---------------+
| product_id | average_price |
+------------+---------------+
| 1          | 6.96          |
| 2          | 16.96         |
+------------+---------------+
- Average selling price = Total Price of Product / Number of products sold.
- Average selling price for product 1 = ((100 * 5) + (15 * 20)) / 115 = 6.96
- Average selling price for product 2 = ((200 * 15) + (30 * 30)) / 230 = 16.96
```

Write an SQL query to find the average selling price for each product.  
- `average_price` should be rounded to 2 decimal places.  

```sql
select UnitsSold.product_id, round(sum(units*price)/sum(units), 2) as average_price
from UnitsSold inner join Prices
on UnitsSold.product_id = Prices.product_id
and UnitsSold.purchase_date between Prices.start_date and Prices.end_date
group by UnitsSold.product_id
```

## [Sales Analysis i](https://code.dennyzhang.com/sales-analysis-i)    

Write an SQL query that reports the best seller by total sales price, If there is a tie, report them all.  
```diff
+------------+--------------+------------+
| product_id | product_name | unit_price |
+------------+--------------+------------+
| 1          | S8           | 1000       |
| 2          | G4           | 800        |
| 3          | iPhone       | 1400       |
+------------+--------------+------------+

Sales table:
+-----------+------------+----------+------------+----------+-------+
| seller_id | product_id | buyer_id | sale_date  | quantity | price |
+-----------+------------+----------+------------+----------+-------+
| 1         | 1          | 1        | 2019-01-21 | 2        | 2000  |
| 1         | 2          | 2        | 2019-02-17 | 1        | 800   |
| 2         | 2          | 3        | 2019-06-02 | 1        | 800   |
| 3         | 3          | 4        | 2019-05-13 | 2        | 2800  |
+-----------+------------+----------+------------+----------+-------+

Result table:
+-------------+
| seller_id   |
+-------------+
| 1           |
| 3           |
+-------------+
```

```mysql
SELECT seller_id
FROM Sales
GROUP BY seller_id
HAVING SUM(price) = (SELECT SUM(price)
                    FROM Sales
                    /** Find the MAX **/
                    GROUP BY seller_id
                    ORDER BY SUM(price) DESC
                    LIMIT 1)
```

## [Product Sales Analysis I](https://zhuanlan.zhihu.com/p/259935444)

Write an SQL query that reports all product names of the products in the Sales table along with their selling year and price.

```diff
Sales table:
+---------+------------+------+----------+-------+
| sale_id | product_id | year | quantity | price |
+---------+------------+------+----------+-------+ 
| 1       | 100        | 2008 | 10       | 5000  |
| 2       | 100        | 2009 | 12       | 5000  |
| 7       | 200        | 2011 | 15       | 9000  |
+---------+------------+------+----------+-------+

Product table:
+------------+--------------+
| product_id | product_name |
+------------+--------------+
| 100        | Nokia        |
| 200        | Apple        |
| 300        | Samsung      |
+------------+--------------+

Result table:
+--------------+-------+-------+
| product_name | year  | price |
+--------------+-------+-------+
| Nokia        | 2008  | 5000  |
| Nokia        | 2009  | 5000  |
| Apple        | 2011  | 9000  |
+--------------+-------+-------+
```

## [Second Highest Salary](https://zhuanlan.zhihu.com/p/250015043)

Write a SQL query to get the second highest salary from the Employee Table.    

For example, given the above Employee table, the query should return 200 as the second highest salary.  
```diff
+----+--------+
| Id | Salary |
+----+--------+
| 1  | 100    |
| 2  | 200    |
| 3  | 300    |
+----+--------+

+---------------------+
| SecondHighestSalary |
+---------------------+
| 200                 |
+---------------------+
- If there is no second highest salary, then the query should return null.

```

```mysql
select ifnull((
       select Salary from Employee
       group by Salary order by Salary desc limit 1,1), null) as SecondHighestSalary

SELECT
 (SELECT DISTINCT Salary
  FROM Employee
  ORDER BY Salary DESC
  LIMIT 1 OFFSET 1) 
AS SecondHighestSalary;
```

## [Duplicate Emails](https://zhuanlan.zhihu.com/p/251960784)

```mysql
SELECT Email FROM
  /**Create A table showing total ount of each mail**/
 (SELECT Email, COUNT(id) AS num FROM Person
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

```diff
Employee
+-------+--------+-----------+--------+
| empId |  name  | supervisor| salary |
+-------+--------+-----------+--------+
|   1   | John   |  3        | 1000   |
|   2   | Dan    |  3        | 2000   |
|   3   | Brad   |  null     | 4000   |
|   4   | Thomas |  3        | 4000   |
+-------+--------+-----------+--------+

Bonus
+-------+-------+
| empId | bonus |
+-------+-------+
| 2     | 500   |
| 4     | 2000  |
+-------+-------+

Result
+-------+-------+
| name  | bonus |
+-------+-------+
| John  | null  |
| Dan   | 500   |
| Brad  | null  |
+-------+-------+
```

- using `IFNULL()`
- using `WHERE ... OR ...`
```mysql
SELECT name, bonus
FROM EmployeeLEFT JOIN Bonus USING (empId)
WHERE IFNULL(bonus, 0) < 1000　　

SELECT a.name, 
b.bonus
FROM Employee AS a
LEFT JOIN Bonus AS b
ON a.empId = b.empId
WHERE b.bonus < 1000 OR b.bonus IS NULL;
```

## [Customer Placing the Largest Number of Orders](https://zhuanlan.zhihu.com/p/258700620)

```
oders table : 
+--------------+-----------------+------------+---------------+--------------+--------+---------+
| order_number | customer_number | order_date | required_date | shipped_date | status | comment |
|--------------|-----------------|------------|---------------|--------------|--------|---------|
| 1            | 1               | 2017-04-09 | 2017-04-13    | 2017-04-12   | Closed |         |
| 2            | 2               | 2017-04-15 | 2017-04-20    | 2017-04-18   | Closed |         |
| 3            | 3               | 2017-04-16 | 2017-04-25    | 2017-04-20   | Closed |         |
| 4            | 3               | 2017-04-18 | 2017-04-28    | 2017-04-25   | Closed |         |
+--------------+-----------------+------------+---------------+--------------+--------+---------+

Sample Output
+-----------------+
| customer_number |
|-----------------|
| 3               |
+-----------------+
```

```mysql
-- +--------------+-----------------+
-- | cout(*)      | customer_number |
-- |--------------|-----------------|
-- | 2            | 3               |
-- | 1            | 2               |
-- | 1            | 1               |
-- +--------------+-----------------+

SELECT customer_number FROM orders
GROUP BY customer_number
ORDER BY COUNT(*) DESC
LIMIT 1;

SELECT customer_number FROM orders 
GROUP BY customer_number
HAVING COUNT(customer_number) >= ALL 
(SELECT COUNT(customer_number) FROM orders GROUP BY customer_number);
```

## [Find Customer Referee](https://zhuanlan.zhihu.com/p/258694894)

Write a query to return the list of customers NOT referred by the person with id '2'.
```
Given a table customer holding customers information and the referee.

+------+------+-----------+
| id   | name | referee_id|
+------+------+-----------+
|    1 | Will |      NULL |
|    2 | Jane |      NULL |
|    3 | Alex |         2 |
|    4 | Bill |      NULL |
|    5 | Zack |         1 |
|    6 | Mark |         2 |
+------+------+-----------+

+------+
| name |
+------+
| Will |
| Jane |
| Bill |
| Zack |
+------+
```

- using `NOT IN`
- using `IS NULL`
- using `IFNULL()`
```mysql
SELECT name FROM customer 
WHERE referee_id <> 2 OR referee_id IS NULL;

// nested query via NOT ... IN
SELECT name FROM customer WHERE
id NOT IN
(SELECT id FROM customer WHERE referee_id = 2);

// using INULL
SELECT name FROM customer
WHERE IFNULL(referee_id,]( 0) <> 2;
```

## [Classes More Than 5 Students](https://zhuanlan.zhihu.com/p/258705251)

Please list out all classes which have more than or equal to 5 students.

```
courses 
+---------+------------+
| student | class      |
+---------+------------+
| A       | Math       |
| B       | English    |
| C       | Math       |
| D       | Biology    |
| E       | Math       |
| F       | Computer   |
| G       | Math       |
| H       | Math       |
| I       | Math       |
+---------+------------+

Should output:
+---------+
| class   |
+---------+
| Math    |
+---------+
```

```mysql
SELECT class 
FROM courses 
GROUP BY class
HAVING COUNT(SELECT DISTINCT student) > 4;
```

## [Friend Requests I: Overall Acceptance Rate](https://zhuanlan.zhihu.com/p/258790804)

## [Consecutive Available Seats](https://zhuanlan.zhihu.com/p/259420594)


Query all the consecutive available seats order by the `seat_id` using the following cinema table?
- The `seat_id` is an auto increment `int`, and free is bool ('1' means free, and '0' means occupied.).
- Consecutive available seats are more than 2(inclusive) seats consecutively available.

```diff
+---------+------+
| seat_id | free |
|---------|------|
| 1       | 1    |
| 2       | 0    |
| 3       | 1    |
| 4       | 1    |
| 5       | 1    |
+---------+------+
 
+---------+
| seat_id |
|---------|
| 3       |
| 4       |
| 5       |
+---------+
```

```mysql
SELECT DISTINCT a.seat_id             
FROM
    cinema a JOIN cinema b ON
    ABS(a.seat_id - b.seat_id) = 1 AND
    /**
      * a.free = TRUE AND b.free = TRUE
      */
    a.free = 1 AND 
    b.free = 1
ORDER BY a.seat_id

SELECT DISTINCT c1.seat_id from cinema c1, cinema c2 
WHERE (c1.seat_id+1=c2.seat_id or c1.seat_id-1=c2.seat_id)
AND(c1.free=TRUE and c2.free=TRUE)
ORDER BY a.seat_id;
```



## [Friend Requests I: Overall Acceptance Rate](https://zhuanlan.zhihu.com/p/258790804)


```diff
friend_request
| sender_id | send_to_id |request_date|
|-----------|------------|------------|
| 1         | 2          | 2016_06-01 |
| 1         | 3          | 2016_06-01 |
| 1         | 4          | 2016_06-01 |
| 2         | 3          | 2016_06-02 |
| 3         | 4          | 2016-06-09 |

request_accepted
| requester_id | accepter_id |accept_date |
|--------------|-------------|------------|
| 1            | 2           | 2016_06-03 |
| 1            | 3           | 2016-06-08 |
| 2            | 3           | 2016-06-08 |
| 3            | 4           | 2016-06-09 |
| 3            | 4           | 2016-06-10 |

|accept_rate|
|-----------|
|       0.80|
```

```mysql
SELECT
ROUND(
    IFNULL(
        (SELECT COUNT(distinct requester_id, accepter_id)
         FROM request_accepted)/ 
        (SELECT COUNT(distinct sender_id, send_to_id)
         FROM friend_request)
    ,0)
,2) accept_rate
```


```mysql
select coalesce(
       round(count(distinct requester_id, accepter_id)/
       count(distinct sender_id, send_to_id),2),
       0) 
       as accept_rate
from friend_request, request_accepted

/** concate **/
select 
round(ifnull((select count(distinct(concat(requester_id,',', accepter_id))) 
from request_accepted) /
(select count(distinct(concat(sender_id,',', send_to_id))) 
from friend_request), 0),2) as accept_rate
```

## [Sales Person](https://zhuanlan.zhihu.com/p/259424830)

Output all the names in the table salesperson, who didn’t have sales to company 'RED'.

```diff
salesperson
+----------+------+--------+-----------------+-----------+
| sales_id | name | salary | commission_rate | hire_date |
+----------+------+--------+-----------------+-----------+
|   1      | John | 100000 |     6           | 4/1/2006  |
|   2      | Amy  | 120000 |     5           | 5/1/2010  |
|   3      | Mark | 65000  |     12          | 12/25/2008|
|   4      | Pam  | 25000  |     25          | 1/1/2005  |
|   5      | Alex | 50000  |     10          | 2/3/2007  |
+----------+------+--------+-----------------+-----------+
                                      ^
company                               |
+---------+--------+------------+     |
| com_id  |  name  |    city    |     |
+---------+--------+------------+     |
|   1     |  RED   |   Boston   |     |
|   2     | ORANGE |   New York |     |
|   3     | YELLOW |   Boston   |     |
|   4     | GREEN  |   Austin   |     |
+---------+--------+------------+     |
                              ^       |
orders                        |       |
+----------+------------+---------+----------+--------+
| order_id | order_date | com_id  | sales_id | amount |
+----------+------------+---------+----------+--------+
| 1        |   1/1/2014 |    3    |    4     | 100000 |
| 2        |   2/1/2014 |    4    |    5     | 5000   |
| 3        |   3/1/2014 |    1    |    1     | 50000  |
| 4        |   4/1/2014 |    1    |    4     | 25000  |
+----------+------------+---------+----------+--------+

Output
+------+
| name | 
+------+
| Amy  | 
| Mark | 
| Alex |
+------+
```

```mysql
SELECT name from salesperson WHERE
SELECT sales_id From orders WHERE com_id NOT IN (SELECT com_id FROM company WHERE CITY = 'RED')
GROUP BY sales_id


SELECT name FROM salesperson
WHERE sales_id NOT IN (
SELECT b.sales_id FROM company AS a
INNER JOIN orders AS b
ON a.com_id = b.com_id
WHERE a.name = 'RED'
);

SELECT name
FROM salesperson
WHERE sales_id NOT IN (SELECT o.sales_id 
                       FROM orders o LEFT JOIN company c ON o.com_id = c.com_id
                       WHERE c.name = 'RED'
                       GROUP BY o.sales_id);
```

## [Triangle Judgement](https://zhuanlan.zhihu.com/p/259435481)  


For the sample data above, your query should return the follow result:

```diff
+----+----+----+
| x  | y  | z  |
|----|----|----|
| 13 | 15 | 30 |
| 10 | 20 | 15 |
+----+----+----+

+----+----+----+----------+
| x  | y  | z  | triangle |
|----|----|----|----------|
| 13 | 15 | 30 | No       |
| 10 | 20 | 15 | Yes      |
+----+----+----+----------+
```


```mysql
SELECT *,
CASE WHEN
(x + y > z) AND (x + z > y) AND (y + z > x) THEN 'Yes'
ELSE 'No' END AS triangle
FROM triangle

select *, 
    IF(x + y > z AND x + z > y AND y + z > x, 'Yes', 'No') as triangle 
    FROM triangle;
```


## [Shortest Distance in a Line]


Table point holds the x coordinate of some points on x-axis in a plane, which are all integers.
Write a query to find the shortest distance between two points in these points.

Write a query to find the shortest distance between two points in these points.
- The shortest distance is '1' obviously, which is from point '-1' to '0'. So the output is as below:

```diff
+-----+
| x   |
|-----|
| -1  |
| 0   |
| 2   |
+-----+

+---------+
| shortest|
|---------|
| 1       |
+---------+
```

```mysql
SELECT MIN(ABS(a.x - b.x)) AS shortest
FROM point AS a
JOIN point AS b
ON a.x <> b.x;
```

## [Biggest Single Number]()

Can Not use `ORDER BY num DESC LIMIT 1`
> if there is no such **bigger single number**
```console
Input: {"headers": {"number": ["num"]}, "rows": {"number": [[8],[1],[8],[3],[4],[3],[1],[4],[5],[5],[6],[6]]}}
Output: {"headers":["num"],"values":[]}
Expected: {"headers":["num"],"values":[[null]]}
```

```diff
+---+
|num|
+---+
| 8 |
| 8 |
| 3 |
| 3 |
| 1 |
| 4 |
| 5 |
| 6 | 
+---+

+---+
|num|
+---+
| 6 |
+---+
```

```mysql
SELECT MAX(num) AS num FROM
(
 SELECT num FROM my_numbers
 GROUP BY num
 HAVING COUNT(*) = 1
) AS x;
```


## [Not Boring Movies](https://zhuanlan.zhihu.com/p/259714269)

Please write a SQL query to output movies with an odd numbered ID and a description that is not 'boring'. Order the result by rating.


- via `mod(attribute, integer) = q`
```mysql
SELECT * FROM cinema
WHERE MOD(id, 2) = 1 AND description <> 'boring'
ORDER BY rating DESC;
```


## [Swap Salary](https://zhuanlan.zhihu.com/p/259763823)

Swap all f and m values (i.e., change all f values to m and vice versa) with a single update statement and no intermediate temp table.  

**Note that you must write a single update statement, DO NOT write any select statement for this problem. **

- via `case when ... then ... else ... end`


## [Actors & Directors Cooperated >= 3 Times](https://zhuanlan.zhihu.com/p/259934531)

Write a SQL query for a report that provides the pairs (actor_id, director_id) where the actor have cooperated with the director at least 3 times.

```mysql
SELECT actor_id, director_id FROM ActorDirector
GROUP BY actor_id, director_id
HAVING COUNT(timestamp) >= 3;
```

## [Product Sales Analysis I](https://zhuanlan.zhihu.com/p/259935444)

Write an SQL query that reports all product names of the products in the Sales table along with their selling year and price.

```diff
  +---------+------------+------+----------+-------+
- | sale_id | product_id | year | quantity | price |
  +---------+------------+------+----------+-------+ 
  | 1       | 100        | 2008 | 10       | 5000  |
  | 2       | 100        | 2009 | 12       | 5000  |
  | 7       | 200        | 2011 | 15       | 9000  |
  +---------+------------+------+----------+-------+

Product table:
  +------------+--------------+
- | product_id | product_name |
  +------------+--------------+
  | 100        | Nokia        |
  | 200        | Apple        |
  | 300        | Samsung      |
  +------------+--------------+

Result table:
  +--------------+-------+-------+
  | product_name | year  | price |
  +--------------+-------+-------+
  | Nokia        | 2008  | 5000  |
  | Nokia        | 2009  | 5000  |
  | Apple        | 2011  | 9000  |
  +--------------+-------+-------+
```

```mysql
--  +---------+------------+------+----------+-------+-------------+
--  | sale_id | product_id | year | quantity | price | product_name|
--  +---------+------------+------+----------+-------+-------------+
--  | 1       | 100        | 2008 | 10       | 5000  | Nokia       |
--  | 2       | 100        | 2009 | 12       | 5000  | Nokia       |
--  | 7       | 200        | 2011 | 15       | 9000  | Apple       |
--  +---------+------------+------+----------+-------+-------------+

SELECT b.product_name, a.year,  a.price
FROM Sales AS a
LEFT JOIN Product AS b
ON a.product_id = b.product_id;
```


## [Product Sales Analysis II](https://zhuanlan.zhihu.com/p/259937061)

Write an SQL query that reports the total quantity sold for every product id.

```mysql
SELECT product_id, SUM(quantity) AS total_quantity
FROM Sales
GROUP BY product_id;
```
## [Project Employees I](https://zhuanlan.zhihu.com/p/259948436)

Write an SQL query that reports the average experience years of all the employees for each project, rounded to 2 digits.

```mysql
SELECT a.project_id, ROUND(AVG(b.experience_years),2) AS average_years FROM Project AS a
JOIN Employee AS b
ON a.employee_id = b.employee_id
GROUP BY a.project_id;
```

## [Project Employees II]()

```diff
  Project table:
  +-------------+-------------+
- | project_id  | employee_id |
  +-------------+-------------+
  | 1           | 1           |
  | 1           | 2           |
  | 1           | 3           |
  | 2           | 1           |
  | 2           | 4           |
  +-------------+-------------+

  Employee table:
  +-------------+--------+------------------+
- | employee_id | name   | experience_years |
  +-------------+--------+------------------+
  | 1           | Khaled | 3                |
  | 2           | Ali    | 2                |
  | 3           | John   | 1                |
  | 4           | Doe    | 2                |
  +-------------+--------+------------------+

  Result table:
  +-------------+---------------+
- | project_id  | average_years |
  +-------------+---------------+
  | 1           | 2.00          |
  | 2           | 2.50          |
  +-------------+---------------+

+ The average experience years for the first project is (3 + 2 + 1) / 3 = 2.00 and for the second project is (3 + 2) / 2 = 2.50
```

```mysql
select project_id, round(avg(experience_years), 2) as average_years
from Project inner join Employee
on Project.employee_id = Employee.employee_id
group by project_id
```

## 1082 Sales Analysis I [Easy]


## 1083 Sales Analysis II [Easy]


## 1084 Sales Analysis III [Easy]


## 1113. Reported Posts [Easy]
## 
## 1141. User Activity for the Past 30 Days I [Easy]
## 
## 1142. User Activity for the Past 30 Days II [Easy]
## 
## 1148. Article Views I [Easy]
## 
## 1173. Immediate Food Delivery I [Easy]
## 
## 1179. Reformat Department Table [Easy]
## 
## 1211. Queries Quality and Percentage [Easy]
## 
## 1241. Number of Comments per Post [Easy]
## 
## 1251. Average Selling Price [Easy]
## 
## 1280. Students and Examinations [Easy]
## 
## 1294. Weather Type in Each Country [Easy]
## 
## 1303. Find the Team Size [Easy]
## 
## 1322. Ads Performance [Easy]
## 
## 1327. List the Products Ordered in a Period [Easy]
## 
## 1350. Students With Invalid Departments [Easy]
## 
## 1378. Replace Employee ID with The Unique Identifier [Easy]
## 
## 1407. Top Travellers [Easy]
## 
## 1435. Create a Session Bar Chart [Easy]
## 
## 1484. Group Sold Products By The Date [Easy]
## 
## 1495. Friendly Movies Streamed Last Month [Easy]
## 
## 1511. Customer Order Frequency [Easy]
## 
## 1517. Find Users With Valid E-Mails [Easy]
## 
## 1527. Patients With a Condition [Easy]
## 
## 1543. Fix Product Name Format [Easy]
## 
## 1565. Unique Orders and Customers Per Month [Easy]
## 
## 1571. Warehouse Manager [Easy]
## 
## 1581. Customer Who Visited but Did Not Make Any Transactions [Easy]
## 
## 1587. Bank Account Summary II [Easy]
## 
## 1607. Sellers With No Sales [Easy]
## 
## 1623. All Valid Triplets That Can Represent a Country [Easy]
