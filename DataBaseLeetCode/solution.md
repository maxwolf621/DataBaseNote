# DataBase Question

[QUESTIONS](https://zhuanlan.zhihu.com/p/265354299)  
[QUESTIONS](https://github.com/kamyu104/LeetCode-Solutions/blob/master/MySQL)  

- [DataBase Question](#database-question)
  - [REVIEW](#review)
  - [Tips](#tips)
  - [!Average Selling Price](#average-selling-price)
  - [!Sales Analysis I](#sales-analysis-i)
  - [Product Sales Analysis I](#product-sales-analysis-i)
  - [!Second Highest Salary](#second-highest-salary)
  - [!Duplicate Emails](#duplicate-emails)
  - [Customers Who Never Order](#customers-who-never-order)
  - [Rising Temperature](#rising-temperature)
  - [!Delete Duplicate Emails](#delete-duplicate-emails)
  - [Game Play Analysis I](#game-play-analysis-i)
  - [Game Play Analysis II](#game-play-analysis-ii)
  - [Employee Bonus](#employee-bonus)
  - [!Customer Placing the Largest Number of Orders](#customer-placing-the-largest-number-of-orders)
  - [Find Customer Referee](#find-customer-referee)
  - [Classes More Than 5 Students](#classes-more-than-5-students)
  - [!Consecutive Available Seats](#consecutive-available-seats)
  - [!Friend Requests I: Overall Acceptance Rate](#friend-requests-i-overall-acceptance-rate)
  - [!Sales Person](#sales-person)
  - [!Triangle Judgement](#triangle-judgement)
  - [!Shortest Distance in a Line](#shortest-distance-in-a-line)
  - [!Biggest Single Number](#biggest-single-number)
  - [!Not Boring Movies](#not-boring-movies)
  - [Swap Salary**](#swap-salary)
      - [Concept](#concept)
  - [!Actors & Directors Cooperated `>= 3` Times](#actors--directors-cooperated--3-times)
  - [Project Employees I](#project-employees-i)
  - [Project Employees II](#project-employees-ii)
  - [Sales Analysis I](#sales-analysis-i-1)
  - [!Sales Analysis II](#sales-analysis-ii)
  - [!ales Analysis III](#ales-analysis-iii)
      - [Concept](#concept-1)
  - [!Reported Posts](#reported-posts)
  - [User Activity for the Past 30 Days I](#user-activity-for-the-past-30-days-i)
  - [User Activity for the Past 30 Days II](#user-activity-for-the-past-30-days-ii)
  - [Article Views I](#article-views-i)
  - [!Immediate Food Delivery I](#immediate-food-delivery-i)
  - [!Reformat Department Table](#reformat-department-table)
      - [Concept](#concept-2)
  - [!Queries Quality and Percentage](#queries-quality-and-percentage)
  - [!Number of Comments per Post](#number-of-comments-per-post)
  - [!Students and Examinations](#students-and-examinations)
  - [!Weather Type in Each Country](#weather-type-in-each-country)
  - [!Find the Team Size](#find-the-team-size)
  - [Ads Performance](#ads-performance)
  - [!List the Products Ordered in a Period](#list-the-products-ordered-in-a-period)
      - [Concept](#concept-3)
  - [Students With Invalid Departments](#students-with-invalid-departments)
      - [Concept](#concept-4)
  - [Replace Employee ID with The Unique Identifier](#replace-employee-id-with-the-unique-identifier)
  - [!Top Travellers](#top-travellers)
  - [!Create a Session Bar Chart](#create-a-session-bar-chart)
  - [!Group Sold Products By The Date](#group-sold-products-by-the-date)
      - [Concept](#concept-5)
  - [Friendly Movies Streamed Last Month](#friendly-movies-streamed-last-month)
  - [!Customer Order Frequency](#customer-order-frequency)
      - [Concept](#concept-6)
      - [ALGO](#algo)
  - [Find Users With Valid E-Mails](#find-users-with-valid-e-mails)
      - [Concept](#concept-7)
  - [Patients With a Condition](#patients-with-a-condition)
      - [Concept](#concept-8)
  - [!Fix Product Name Format](#fix-product-name-format)
      - [Concept](#concept-9)
  - [!Unique Orders and Customers Per Month](#unique-orders-and-customers-per-month)
  - [Warehouse Manager](#warehouse-manager)
  - [!Customer Who Visited but Did Not Make Any Transactions](#customer-who-visited-but-did-not-make-any-transactions)
  - [Bank Account Summary II](#bank-account-summary-ii)
  - [!Sellers With No Sales](#sellers-with-no-sales)
  - [All Valid Triplets That Can Represent a Country](#all-valid-triplets-that-can-represent-a-country)



## REVIEW
- [`RANK OVER()`](https://www.begtut.com/mysql/mysql-rank-function.html)    
- [`HAVING`](https://www.yiibai.com/mysql/having.html)    
- [`JOIN ... WHERE ...` VS `ON` ](https://stackoverflow.com/questions/354070/sql-join-where-clause-vs-on-clause)     
- [`Count`](https://www.fooish.com/sql/count-function.html)   
- [`IFNULL( expr , alt_returned_val_if_expr_is_null`](https://www.w3schools.com/sql/func_mysql_ifnull.asp)  
- [`OUTER JOIN`, `INNER JOIN` and `EQUI JOIN`](https://github.com/maxwolf621/DataBaseNote/blob/main/RelationalAlgebra.md#join)     
  - [`JOIN` and `INNER JOIN`](https://stackoverflow.com/questions/565620/difference-between-join-and-inner-join)      
- [`UNION` and `UNION ALL`](https://github.com/maxwolf621/DataBaseNote/blob/main/RelationalAlgebra.md#union)     
- [Sql Summary](https://towardsdatascience.com/sql-questions-summary-df90bfe4c9c)   

## Tips
- [Ref](https://github.com/shawlu95/Beyond-LeetCode-SQL)
1. Using the `like` operator and wildcards (flexible search)
2. Avoiding the `or` operator, use `in` operator
   - data retrieval is measurably faster by replacing `OR` conditions with the `IN` predicate
3. Avoiding the `HAVING` clause
   1. Try to frame the restriction earlier 
      > `where` clause  
   2. Try to keep `HAVING` clause **SIMPLE** 
      > use constant, not Function  
4. Avoiding large SORT operations
   - It is best to schedule queries with large sorts as periodic batch processes during off-peak database usage so that the performance of most user processes is not affected.

5. Prefer stored procedure  
   - Compiled and permanently stored in the database in an executable format.
6. Disabling indexes during batch loads
   - When the batch load is complete, you should rebuild the indexes.
   - Reduction of fragmentation that is found in the index
7. Cost-based optimization 
   - Check database server manual
8. Use`view`
   - Keep the levels of code in your query as flat as possible and to test and tune the statements that make up your views

## !Average Selling Price

Write an SQL query to find the average selling price for each product.  
- `average_price` should be rounded to 2 decimal places.  

```diff
  Prices table : 
  +------------+------------+------------+--------+
  | product_id | start_date | end_date   | price  |
  +------------+------------+------------+--------+
  | 1          | 2019-02-17 | 2019-02-28 | 5      |
  | 1          | 2019-03-01 | 2019-03-22 | 20     |
  | 2          | 2019-02-01 | 2019-02-20 | 15     |
  | 2          | 2019-02-21 | 2019-03-31 | 30     |
  +------------+------------+------------+--------+
```
- `(product_id, start_date, end_date)` is the primary key for this table.
- there will be no two intersecting periods for the same `product_id`.

---

```diff
  UnitsSold table:
  +------------+---------------+-------+
  | product_id | purchase_date | units |
  +------------+---------------+-------+
  | 1          | 2019-02-25    | 100   |
  | 1          | 2019-03-01    | 15    |
  | 2          | 2019-02-10    | 200   |
  | 2          | 2019-03-22    | 30    |
  +------------+---------------+-------+
```
- There is no primary key for this table

---

```diff
  Result table:
  +------------+---------------+
  | product_id | average_price |
  +------------+---------------+
  | 1          | 6.96          |
  | 2          | 16.96         |
  +------------+---------------+
```
- Average selling price = `Total Price of Product / Number of products sold`.

```sql
SELECT UnitsSold.product_id, 
       ROUND(SUM(units*price)/SUM(units), 2) AS average_price
FROM UnitsSold 
/**
  +------------+------------+------------+--------+---------------+-------+
  | product_id | start_date | end_date   | price  | purchase_date | units |
  +------------+------------+------------+--------+---------------+-------+
  | 1          | 2019-02-17 | 2019-02-28 | 5      | 2019-02-25    | 100   |
  | 1          | 2019-03-01 | 2019-03-22 | 20     | 2019-03-01    | 15    |
  | 2          | 2019-02-01 | 2019-02-20 | 15     | 2019-02-10    | 200   |
  | 2          | 2019-02-21 | 2019-03-31 | 30     | 2019-03-22    | 30    |
  +------------+------------+------------+--------+---------------+-------+
*/
INNER JOIN Prices
ON UnitsSold.product_id = Prices.product_id
AND UnitsSold.purchase_date 
    BETWEEN Prices.start_date AND Prices.end_date
GROUP BY UnitsSold.product_id
```

## !Sales Analysis I

Write an SQL query that reports the best seller by total sales price, If there is a tie, report them all.  
```diff
  Product table:
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

```sql
SELECT seller_id
FROM Sales
GROUP BY seller_id

--In CASE of a tie using HAVING SUM(price) = 2800
HAVING SUM(price) = SELECT SUM(price)
                    FROM Sales
                    GROUP BY seller_id
                    ORDER BY SUM(price) DESC
                    LIMIT 1
```

## Product Sales Analysis I

Write an SQL query that reports **all** product names of the products in the Sales table along with their selling year and price.

```diff
Sales table:                                        Product table:
+---------+------------+------+----------+-------+  +------------+--------------+
| sale_id | product_id | year | quantity | price |  | product_id | product_name |
+---------+------------+------+----------+-------+  +------------+--------------+
| 1       | 100        | 2008 | 10       | 5000  |  | 100        | Nokia        |
| 2       | 100        | 2009 | 12       | 5000  |  | 200        | Apple        |
| 7       | 200        | 2011 | 15       | 9000  |  | 300        | Samsung      |
+---------+------------+------+----------+-------+  +------------+--------------+

Result table:
+--------------+-------+-------+
| product_name | year  | price |
+--------------+-------+-------+
| Nokia        | 2008  | 5000  |
| Nokia        | 2009  | 5000  |
| Apple        | 2011  | 9000  |
+--------------+-------+-------+
```
```sql
SELECT S.product_name, 
       S.year, 
       S.price
FROM Sales 

-- query All Products
LEFT JOIN Product 
ON S.product_id = P.product_id
```
## !Second Highest Salary

Write a SQL query to get the second highest salary from the Employee Table.    
- If there is no second highest salary, then the query should return `null`.
- THINK : a tie existing ?

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
```

```mysql
-- return null if there are no second highest salary
SELECT IFNULL(
      (SELECT Salary 
       FROM Employee
       GROUP BY Salary 
       ORDER BY Salary DESC LIMIT 1,1), NULL) 
AS SecondHighestSalary

SELECT
 (SELECT DISTINCT Salary
  FROM Employee
  ORDER BY Salary DESC
  LIMIT 1 OFFSET 1) 
AS SecondHighestSalary;
```

## !Duplicate Emails

Write a SQL query to find **all** duplicate emails.

```diff
Person Table :
+----+-------------+
| id |   Email     |
+----+-------------+
| 1  | a@b.com     |
| 2  | c@d.com     |
| 3  | a@b.com     |
+----+-------------+
```

```sql
/**
--------------+------+
|  Email      | num  |
--------------+------+
| a@b.com     | 2    |
| c@d.com     | 1    |
+-------------+------+
**/
SELECT Email 
-- Showing Total count of Each E-Mail
FROM (SELECT Email,
             COUNT(id) AS num 
      FROM Person 
      GROUP BY Email) AS tmp
WHERE num > 1;


SELECT DISTINCT p.Email
FROM Person AS p
JOIN Person AS p2
ON p.Email = p2.Email
   AND p.Id <> p2.Id;
```

## Customers Who Never Order

[Write a SQL query to find all customers who never order anything.](https://zhuanlan.zhihu.com/p/251983949)

## Rising Temperature

[Write an SQL query to find all dates' id with higher temperature compared to its previous dates (yesterday).](https://zhuanlan.zhihu.com/p/252403796)  
- [lag Function](https://www.mysqltutorial.org/mysql-window-functions/mysql-lag-function/)  

1. using `JOIN` to compare two same table via function
   > `DATEDIFF(date1, date2) = Difference`   
   > `DATE_SUB`    
   > `DATE_ADD`   
   > `SUB_DATE`    

## !Delete Duplicate Emails

Write a SQL query to `DELETE` all duplicate email entries in a table named Person, keeping only unique emails based on its smallest Id.  
For example, after running your query, the above Person table should have the following rows:  

```diff
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
1. `DELETE FROM table WHERE table.column NOT IN (NESTED QUERY) ` 
2. `DELETE FROM table WHERE ... AND ...`

```sql
DELETE FROM Person AS P
WHERE Id NOT IN
/**
TMP      P
+------+ +----+
|MinId | | Id | 
+------+ +----+
| 1    | | 1  | 
| 2    | | 2  | 
+------+ | 3  | 
         +----+
*/
(SELECT MinId 
 FROM (SELECT MIN(Id) AS MinId
       FROM Person 
       GROUP BY Email) AS TMP)
/**
TABLE P
+----+------------------+
| Id | Email            |
+----+------------------+
| 1  | john@example.com |
| 2  | bob@example.com  |
| 3  | john@example.com |----+
+----+------------------+    |
                             |
TABLE TMP                    |
+----+------------------+    |
| Id | Email            |    |
+----+------------------+    |
| 1  | john@example.com | <--+
| 2  | bob@example.com  |
| 3  | john@example.com |
+----+------------------+
*/
DELETE P 
FROM Person P, Person TMP
WHERE P.Id > TMP.Id 
      AND P.Email = TMP.Email
```

## Game Play Analysis I

Write an SQL query that reports the first login date for each player.

```diff
Activity table:
+-----------+-----------+------------+--------------+
| player_id | device_id | event_date | games_played |
+-----------+-----------+------------+--------------+
| 1         | 2         | 2016-03-01 | 5            *----+
| 1         | 2         | 2016-05-02 | 6            |    |    
| 2         | 3         | 2017-06-25 | 1            * ---|---+     
| 3         | 1         | 2016-03-02 | 0            * ---|---|-----+  
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
```

```sql
/**
Group By player_id
+-----------+-----------+------------+--------------+
| player_id | device_id | event_date | games_played |
+-----------+-----------+------------+--------------+
| 1         | 2         | 2016-03-01 | 5            | 
|           | 2         | 2016-05-02 | 6            | 
|-----------|-----------|------------|--------------|   
| 2         | 3         | 2017-06-25 | 1            |  
|-----------|-----------|------------|--------------| 
| 3         | 1         | 2016-03-02 | 0            | 
|           | 4         | 2018-07-03 | 5            |  
+-----------+-----------+------------+--------------+   


+-----------+-----------------+
| player_id | min(event_date) |
+-----------+-----------------+
| 1         | 2016-03-01      |
| 2         | 2017-06-25      |
| 3         | 2016-03-02      |
+-----------+-----------------+
*/
SELECT player_id, 
       min(event_date) AS first_login
FROM activity 
GROUP BY player_id
ORDER BY player_id;
```

## Game Play Analysis II

Write a SQL query that reports the **DEVICE that is first logged in for EACH player.**
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
```sql
/**
+-----------+-----------+------------+--------------+
| player_id | device_id | event_date | games_played |
+-----------+-----------+------------+--------------+
| 1         | 2         | 2016-03-01 | 5            |
| 2         | 3         | 2017-06-25 | 1            |
| 3         | 1         | 2016-03-02 | 0            |
+-----------+-----------+------------+--------------+
*/
SELECT player_id, 
       device_id 
FROM Activity AS Result
WHERE player_id IN (SELECT player_id, 
                           min(event_date) 
                    FROM Activity AS TMP 
                    GROUP BY player_id )
```

## Employee Bonus

Select **all** employee's name and bonus whose bonus is `< 1000 (or NULL)`.

```diff
Employee                                  Bonus
+-------+--------+-----------+--------+   +-------+-------+
| empId |  name  | supervisor| salary |   | empId | bonus |
+-------+--------+-----------+--------+   +-------+-------+
|   1   | John   |  3        | 1000   |   | 2     | 500   |
|   2   | Dan    |  3        | 2000   |   | 4     | 2000  |
|   3   | Brad   |  null     | 4000   |   +-------+-------+
|   4   | Thomas |  3        | 4000   |
+-------+--------+-----------+--------+

Result
+-------+-------+
| name  | bonus |
+-------+-------+
| John  | null  |
| Dan   | 500   |
| Brad  | null  |
+-------+-------+
```


```sql
SELECT a.name, b.bonus
FROM Employee AS a
/**
+-------+--------+-----------+--------+-------+-------+
| empId |  name  | supervisor| salary | empId | bonus |
+-------+--------+-----------+--------+-------+-------+
|   1   | John   |  3        | 1000   |  NA   |  NA   |
|   2   | Dan    |  3        | 2000   |  2    | 500   |
|   3   | Brad   |  null     | 4000   |  NA   |  NA   |
|   4   | Thomas |  3        | 4000   |  4    | 2000  |
+-------+--------+-----------+--------+-------+-------+
**/
LEFT JOIN Bonus AS b
ON a.empId = b.empId
WHERE b.bonus < 1000 
      OR b.bonus IS NULL;

SELECT name, bonus
FROM Employee
LEFT JOIN Bonus 
USING (empId)
WHERE IFNULL(bonus, 0) < 1000??????
```

## !Customer Placing the Largest Number of Orders
Query the `customer_number` from the orders table for the customer who has placed the largest number of orders.
- It is guaranteed that exactly one customer will have placed more orders than any other customer. (No Tie)

```diff
Order table : 
+--------------+-----------------+------------+---------------+--------------+--------+
| order_number | customer_number | order_date | required_date | shipped_date | status |
|--------------|-----------------|------------|---------------|--------------|--------|
| 1            | 1               | 2017-04-09 | 2017-04-13    | 2017-04-12   | Closed |         
| 2            | 2               | 2017-04-15 | 2017-04-20    | 2017-04-18   | Closed |         
| 3            | 3               | 2017-04-16 | 2017-04-25    | 2017-04-20   | Closed |         
| 4            | 3               | 2017-04-18 | 2017-04-28    | 2017-04-25   | Closed |         
+--------------+-----------------+------------+---------------+--------------+--------+

Sample Output
+-----------------+
| customer_number |
|-----------------|
| 3               |
+-----------------+
```

```sql
/**
  +--------------+-----------------+ 
  |COUNT(*)      | customer_number |
  |--------------|-----------------|
  | 2            | 3               |
  | 1            | 2               |
  | 1            | 1               |
  +--------------+-----------------+
*/
SELECT customer_number 
FROM orders
GROUP BY customer_number 
ORDER BY COUNT(*) DESC
LIMIT 1

/** 
  * Using having 
  **/
SELECT customer_number FROM orders 
GROUP BY customer_number
HAVING COUNT(customer_number) >= ALL(SELECT COUNT(customer_number) 
       FROM orders 
       GROUP BY customer_number
```

## Find Customer Referee

Write a query to return the list of customers NOT referred by the person with id `2`.
Given a table customer holding customers information and the referee.

```diff
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

```sql
SELECT name 
FROM customer 
WHERE referee_id <> 2 OR referee_id IS NULL;

-- NOT IN
SELECT name FROM customer WHERE
id NOT IN (SELECT id 
           FROM customer W
           HERE referee_id = 2);

-- IFNULL
SELECT name FROM customer
WHERE IFNULL(referee_id, 0) <> 2;
```

## Classes More Than 5 Students

Please list out all classes which have more than or equal to `5` students.

Question : is `[student,class]` PK? 

```sql
Courses 
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

Result
+---------+
| class   |
+---------+
| Math    |
+---------+


SELECT class 
+---------+------------+
| student | class      |
+---------+------------+
| A       | Math       |
| C       |            |
| E       |            |
| G       |            |
| H       |            |
| I       |            |
| F       | Computer   |
| D       | Biology    |
| B       | English    |
+---------+------------+
FROM (SELECT class, 
             COUNT(DISTINCT student) AS num
      FROM courses
      GROUP BY class) AS TMP
WHERE num >= 5;
```

## !Consecutive Available Seats

Query all the consecutive available seats order by the `seat_id` using the following cinema table
- The `seat_id` is an auto increment `int`, and free is bool `1` means free, and `0` means occupied.
- Consecutive available seats are **more than 2(inclusive) seats consecutively available.**

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

Find firstly 
1. consecutive seats
2. check free 

```sql
/**
+---------+------+
| seat_id | free |
|---------|------|
| 1       | 1    |
| 2       | 0    |
| 3       | 1    |
| 4       | 1    | 
| 5       | 1    |
+---------+------+     
*/
SELECT DISTINCT a.seat_id             
FROM cinema a 
JOIN cinema b ON
    -- Consecutive seats
    ABS(a.seat_id - b.seat_id) = 1 AND
    -- a.free = TRUE AND b.free = TRUE
    a.free = 1 AND b.free = 1
ORDER BY a.seat_id

SELECT DISTINCT c1.seat_id 
FROM cinema c1, cinema c2 
WHERE (c1.seat_id + 1 = c2.seat_id or c1.seat_id-1 = c2.seat_id) -- consecutive seats
       AND (c1.free=TRUE and c2.free=TRUE)
ORDER BY a.seat_id;
```

## !Friend Requests I: Overall Acceptance Rate

Write a query to find the overall acceptance rate of requests rounded to 2 decimals, which is the number of acceptance divides the number of requests.

```sql
friend_request
+-----------+------------+------------+
| sender_id | send_to_id |request_date|
|-----------|------------|------------|
| 1         | 2          | 2016_06-01 |
| 1         | 3          | 2016_06-01 |
| 1         | 4          | 2016_06-01 |
| 2         | 3          | 2016_06-02 |
| 3         | 4          | 2016-06-09 |
+-----------+------------+------------+

request_accepted
+--------------+-------------+------------+
| requester_id | accepter_id |accept_date |
|--------------|-------------|------------|
| 1            | 2           | 2016_06-03 |
| 1            | 3           | 2016-06-08 |
| 2            | 3           | 2016-06-08 |
| 3            | 4           | 2016-06-09 |
| 3            | 4           | 2016-06-10 |
+--------------+-------------+------------+

RESULT
+-----------+
|accept_rate|
|-----------|
|       0.80|
+-----------+

-- Time:  O(rlogr + aloga)
-- Space: O(r + a)
SELECT
ROUND(
    IFNULL(
    (SELECT COUNT(*) FROM (SELECT DISTINCT requester_id, accepter_id FROM request_accepted) AS r)
    / 
    (SELECT COUNT(*) FROM (SELECT DISTINCT sender_id, send_to_id FROM friend_request) AS a), 0), 2) 
AS accept_rate;


SELECT coalesce(
       ROUND(count(distinct requester_id, accepter_id)/
       COUNT(distinct sender_id, send_to_id),2), 0) 
       AS accept_rate
FROM friend_request, request_accepted


/** 
 concat( ... , ..) 
**/
SELECT 
-- ROUND( IFNULL( expr, nu
ROUND(IFNULL(
         (SELECT COUNT(DISTINCT(CONCAT(requester_id, ',' , accepter_id))) FROM request_accepted) / 
         (SELECT COUNT(DISTINCT(CONCAT(sender_id,',', send_to_id))) FROM friend_request)
         , 0) , 2) 
AS accept_rate
```

## !Sales Person

Output **all** the names in the table salesperson, who didn???t have sales to company `RED`.

```sql 
Salesperson table
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
Company table                         |
+---------+--------+------------+     |
| com_id  |  name  |    city    |     |
+---------+--------+------------+     |
|   1     |  RED   |   Boston   |     |
|   2     | ORANGE |   New York |     |
|   3     | YELLOW |   Boston   |     |
|   4     | GREEN  |   Austin   |     |
+---------+--------+------------+     |
                              ^       |
Orders Table                  |       |
+--------------+------------+---------+----------+--------+
| (PK)order_id | order_date | com_id  | sales_id | amount |
+--------------+------------+---------+----------+--------+
| 1            |   1/1/2014 |    3    |    4     | 100000 |
| 2            |   2/1/2014 |    4    |    5     | 5000   |
| 3            |   3/1/2014 |    1    |    1     | 50000  |
| 4            |   4/1/2014 |    1    |    4     | 25000  |
+--------------+------------+---------+----------+--------+

Output
+------+
| name | 
+------+
| Amy  | 
| Mark | 
| Alex |
+------+

-- Nested Query
SELECT name 
from salesperson 
WHERE (SELECT sales_id From orders WHERE com_id NOT IN 
      (SELECT com_id FROM company WHERE CITY = 'RED')
GROUP BY sales_id);

-- INNER JOIN
SELECT name FROM salesperson
WHERE sales_id NOT IN ( SELECT b.sales_id 
                        FROM company      AS a
                        INNER JOIN orders AS b
                        ON a.com_id = b.com_id
                        WHERE a.name = 'RED');

-- LEFT JOIN 
SELECT name
FROM salesperson
WHERE sales_id NOT IN (SELECT o.sales_id 
                       FROM orders o 
                       /**
                          +----------+------------+---------+----------+--------+---------+--------+------------+     
                          | order_id | order_date | com_id  | sales_id | amount | com_id  |  name  |    city    |     
                          +----------+------------+---------+----------+--------+---------+--------+------------+  
                          | 1        |   1/1/2014 |    3    |    4     | 100000 |   3     | YELLOW |   Boston   | 
                          | 2        |   2/1/2014 |    4    |    5     | 5000   |   4     | GREEN  |   Austin   | 
                          | 3        |   3/1/2014 |    1    |    1     | 50000  |   1     |  RED   |   Boston   |
                          | 4        |   4/1/2014 |    1    |    4     | 25000  |   1     |  RED   |   Boston   |
                          | NULL     |   NULL     |  NULL   |  NULL    |  NULL  |   4     | GREEN  |   Austin   |   
                          +----------+------------+---------+----------+--------+---------+--------+------------+ 
                          **/
                       LEFT JOIN company c 
                       ON o.com_id = c.com_id
                       WHERE c.name = 'RED'
                       GROUP BY o.sales_id);
```

## !Triangle Judgement

```sql
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

CASE WHEN (x + y > z) AND (x + z > y) AND (y + z > x) THEN 'Yes'
          ELSE 'No' END AS triangle
FROM triangle

select *, 
    IF(x + y > z AND x + z > y AND y + z > x, 'Yes', 'No') as triangle 
    FROM triangle;
```


## !Shortest Distance in a Line

Table point holds the x coordinate of some points on x-axis in a plane, which are all integers.

Write a query to find the shortest distance between two points in these points.
- The shortest distance is '1' obviously, which is from point '-1' to '0'. So the output is as below:

```sql
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

```sql
SELECT MIN(ABS(a.x - b.x)) AS shortest
FROM point AS a
JOIN point AS b
ON a.x <> b.x;
```

## !Biggest Single Number

Find The Biggest Single Number

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

```sql
SELECT MAX(num) AS num 
FROM (
       /**
        +---+----+
        |num| cnt|
        +---+----+
        | 8 |  2 |
        | 3 |  2 |
        | 1 |  1 |
        | 4 |  1 |
        | 5 |  1 |
        | 6 |  1 |
        +---+----+
       */
       SELECT num 
       FROM my_numbers
       GROUP BY num
       /**
        +---+----+
        |num| cnt|
        +---+----+
        | 1 |  1 |
        | 4 |  1 |
        | 5 |  1 |
        | 6 |  1 |
        +---+----+
       */
       HAVING COUNT(*) = 1 ) 
```


## !Not Boring Movies

Concept `mod(attribute, integer) = q`

Please write a SQL query to output movies with an odd numbered `id` and a description that is not `boring`. 
- Order the result by rating.

```sql
+---------+-----------+--------------+-----------+
|   id    | movie     |  description |  rating   |
+---------+-----------+--------------+-----------+
|   1     | War       |   great 3D   |   8.9     |
|   2     | Science   |   fiction    |   8.5     |
|   3     | Irish     |   boring     |   6.2     |
|   4     | Ice song  |   Fantasy    |   8.6     |
|   5     | House card|   Interesting|   9.1     |
+---------+-----------+--------------+-----------+

result
+---------+-----------+--------------+-----------+
|   id    | movie     |  description |  rating   |
+---------+-----------+--------------+-----------+
|   5     | House card|   Interesting|   9.1     |
|   1     | War       |   great 3D   |   8.9     |
+---------+-----------+--------------+-----------+


SELECT * 
FROM cinema
WHERE MOD(id, 2) = 1 
      AND description <> 'boring'
ORDER BY rating DESC;
```

## Swap Salary**

#### Concept
- Usage of `CASE WHEN exp THEN ... END`
 
Swap all `f` and `m` values   
(i.e. change all `f` values to `m` and vice versa) with a single `update` statement and no intermediate temp table.  

```diff
+----+------+-----+--------+
| id | name | sex | salary |
|----|------|-----|--------|
| 1  | A    | m   | 2500   |
| 2  | B    | f   | 1500   |
| 3  | C    | m   | 5500   |
| 4  | D    | f   | 500    |
+----+------+-----+--------+

Result
+----+------+-----+--------+
| id | name | sex | salary |
|----|------|-----|--------|
| 1  | A    | f   | 2500   |
| 2  | B    | m   | 1500   |
| 3  | C    | f   | 5500   |
| 4  | D    | m   | 500    |
+----+------+-----+--------+
```
- **Note that you must write a single update statement, DO NOT write any `SELECT` statement for this problem.**

```sql
UPDATE salary 
SET sex = CASE sex 
          WHEN 'm' THEN 'f' 
          WHEN 'f' THEN 'm' 
          END;    
          
-- IF
UPDATE salary 
SET sex = IF(sex = 'm', 'f', 'm');

```

## !Actors & Directors Cooperated `>= 3` Times
Write a SQL query for a report that provides the pairs (`actor_id`, `director_id`) where the actor have cooperated with the director **at least 3 times**.

```diff
ActorDirector table:
+-------------+-------------+-------------+
| actor_id    | director_id | timestamp   |
+-------------+-------------+-------------+
| 1           | 1           | 0           |
| 1           | 1           | 1           |
| 1           | 1           | 2           |
| 1           | 2           | 3           |
| 1           | 2           | 4           |
| 2           | 1           | 5           |
| 2           | 1           | 6           |
+-------------+-------------+-------------+

Result table:
+-------------+-------------+
| actor_id    | director_id |
+-------------+-------------+
| 1           | 1           |
+-------------+-------------+
```

```sql
/**
    +-------------+-------------+-------------+
    | actor_id    | director_id | timestamp   |
    +-------------+-------------+-------------+
    | 1           | 1           | 0           |
    |             |             | 1           |
    |             |             | 2           |
    |-----------------------------------------|
    | 1           | 2           | 3           |
    |             |             | 4           |
    |-----------------------------------------|
    | 2           | 1           | 5           |
    |             |             | 6           |
    +-------------+-------------+-------------+
*/
SELECT actor_id, 
       director_id 
FROM ActorDirector
GROUP BY actor_id, director_id
HAVING COUNT(timestamp) >= 3;
```

## Project Employees I

Write an SQL query that reports **the average experience years of all the employees for each project**, rounded to 2 digits.
```diff
  Project                          Employee (employee_id : PK)
  +-------------+-------------+    +-------------+--------+------------------+
  | project_id  | employee_id |    | employee_id | name   | experience_years |
  +-------------+-------------+    +-------------+--------+------------------+
  | 1           | 1           |    | 1           | Khaled | 3                |
  | 1           | 2           |    | 2           | Ali    | 2                |
  | 1           | 3           |    | 3           | John   | 1                |
  | 2           | 1           |    | 4           | Doe    | 2                |
  | 2           | 4           |    +-------------+--------+------------------+
  +-------------+-------------+


Result table:
  +-------------+---------------+
  | project_id  | average_years |
  +-------------+---------------+
  | 1           | 2.00          |
  | 2           | 2.50          |
  +-------------+---------------+
```

```sql
-- +-------------+--------+-------------------------------+
-- | employee_id | name   | experience_years |project_id  |
-- +-------------+--------+------------------+------------+
-- |     1       | Khaled |         3        | 1          |   
-- |     2       | Ali    |         2        | 1          |
-- |     3       | John   |         1        | 1          |
-- |     1       | Khaled |         3        | 2          | 
-- |     4       | Doe    |         2        | 2          |
-- +-------------+--------+------------------+------------+

-- Time:  O(m + n) 
-- Space: O(m + n) 
SELECT P.project_id, 
       ROUND(AVG(E.experience_years),2) AS average_years 
FROM Project AS P
JOIN Employee AS E
ON P.employee_id = E.employee_id
GROUP BY P.project_id
-- SQL Server also treats NULL values as smaller than any non-NULL values. 
ORDER BY NULL 
```
## Project Employees II 

Write an SQL query that reports **all the projects** that have the most employees.
- may have a tie situation

```diff
  Project table:
  +-------------+-------------+
  | project_id  | employee_id |
  +-------------+-------------+
  | 1           | 1           |
  | 1           | 2           |
  | 1           | 3           |
  | 2           | 1           |
  | 2           | 4           |
  +-------------+-------------+

  Result table:
  +-------------+
  | project_id  |
  +-------------+
  | 1           |
  +-------------+
```

```sql
-- Time:  O(n)
-- Space: O(n)

/** 
  IF THERE IS NO TIE IN THE TABLE
  SELECT project_id 
  FROM   project 
  GROUP  BY project_id 
  +-------------+-------------+
  | project_id  | employee_id |
  +-------------+-------------+
  | 1           | 1           |
  |             | 2           |
  |             | 3           |
  |-------------|-------------|
  | 2           | 1           |
  |             | 4           |
  +-------------+-------------+  
  
  SELECT Count(employee_id) 
  FROM   project 
  GROUP  BY project_id 
  ORDER  BY Count(employee_id) DESC 
  LIMIT  1
  
  +-------------+-------------+
  | Count(employee_id)        |
  +-------------+-------------+
  | 3                         |
  +-------------+-------------+
*/
```

```mysql 
SELECT project_id 
FROM   project 
GROUP  BY project_id 
-- IF TABLE PROJECT HAS THE TIE 
/** 
  FOR EXAMPLE
  +-------------+-------------+
  | project_id  | employee_id |
  +-------------+-------------+
  | 1           | 1           |
  |             | 2           |
  |             | 3           |
  |-------------|-------------|
  | 2           | 1           |
  |             | 3           |
  |             | 4           |
  +-------------+-------------+  
*/
HAVING Count(employee_id) = (SELECT Count(employee_id) 
                             FROM   project 
                             GROUP  BY project_id 
                             ORDER  BY Count(employee_id) DESC 
                             LIMIT  1) 
```

## Sales Analysis I

Write an SQL query that reports the best seller by total sales price, If there is a tie, report them all.

```diff
  Product table:
  +------------+--------------+------------+
  | product_id | product_name | unit_price |
  +------------+--------------+------------+
  | 1          | S8           | 1000       |
  | 2          | G4           | 800        |
  | 3          | iPhone       | 1400       |
  +------------+--------------+------------+

  Sales table(This table has no primary key, it can have repeated rows.)
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
- Both sellers with id `1 `and `3` sold products with the most total price of `2800`.


```sql
WITH tmp AS (
SELECT seller_id, RANK() OVER(ORDER BY SUM(price) DESC) AS rnk 
FROM Sales
GROUP BY seller_id
)

SELECT seller_id FROM tmp
WHERE rnk = 1;
```

```sql
  +-----------+------------+----------+------------+----------+-------+
  | seller_id | product_id | buyer_id | sale_date  | quantity | price |
  +-----------+------------+----------+------------+----------+-------+
  | 1         | 1          | 1        | 2019-01-21 | 2        | 2000  |
  | 1         | 2          | 2        | 2019-02-17 | 1        | 800   |
  | 2         | 2          | 3        | 2019-06-02 | 1        | 800   |
  | 3         | 3          | 4        | 2019-05-13 | 2        | 2800  |
  +-----------+------------+----------+------------+----------+-------+

SELECT seller_id
FROM Sales
GROUP by seller_id
HAVING sum(price) = (
        SELECT sum(price)
        FROM Sales
        GROUP BY seller_id
        ORDER BY sum(price) desc
        LIMIT 1)
```

## !Sales Analysis II

Write an SQL query that reports the buyers who have bought `S8` but not `iPhone`. 
- Note that S8 and iPhone are products present in the Product table.

```diff
  Result table:
  +-------------+
  | buyer_id    |
  +-------------+
  | 1           |
  +-------------+
```

```sql
WITH tmp AS (
  SELECT a.buyer_id, b.product_name 
  FROM Sales AS a
  JOIN Product AS b
  ON a.product_id = b.product_id
)

SELECT DISTINCT buyer_id 
FROM tmp
WHERE buyer_id NOT IN ( SELECT buyer_id 
                        FROM tmp 
                        WHERE product_name = 'iPhone')
                        AND buyer_id IN ( SELECT buyer_id 
                                          FROM tmp 
                                          WHERE product_name = 'S8');
/** nested query with JOIN **/
SELECT distinct buyer_id
FROM Sales 
INNER JOIN Product/
WHERE Sales.product_id = Product.product_id 
      AND Product_name = 'S8'
      -- Buyer that bought no Iphone
      AND buyer_id NOT IN (SELECT distinct buyer_id
                           FROM Sales 
                           INNER JION Product
                           WHERE Sales.product_id = Product.product_id
                                 AND product_name = 'iPhone')
```

## !ales Analysis III

Write an SQL query that selects the `product_id`, `year`, `quantity`, and `price` for the first year of every product sold.
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
  +------------+------------+----------+-------+
  | product_id | first_year | quantity | price |
  +------------+------------+----------+-------+ 
  | 100        | 2008       | 10       | 5000  |
  | 200        | 2011       | 15       | 9000  |
  +------------+------------+----------+-------+
```

```
SELECT product_id,
       min(year) as first_year,
       quantity,
       price
FROM sales
GROUP BY product_id
```

Write an SQL query that reports the products that were only sold in spring `2019`.  
That is, between `2019-01-01` and `2019-03-31` inclusive.   

#### Concept
- `NOT BETWEEN 'YYYY-MM-DD' AND 'YYYY-MM-DD'`
- `> 'YYYY-MM-DD', < 'YYYY-MM-DD'`

```mysql
  Product table:
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
  
SELECT DISTINCT a.product_id, 
       b.product_name 
FROM Sales AS a
JOIN Product AS b
ON a.product_id = b.product_id
WHERE a.product_id NOT IN (SELECT product_id FROM Sales WHERE sale_date < '2019-01-01')
AND a.product_id NOT IN (SELECT product_id FROM Sales WHERE sale_date > '2019-03-31');

-- Without JOIN
SELECT product_id, 
       product_name 
FROM   product 
WHERE  product_id NOT IN (SELECT product_id 
                          FROM   sales 
                          WHERE  sale_date NOT BETWEEN 
                                 '2019-01-01' AND '2019-03-31'); 
```

## !Reported Posts

Assume today is `2019-07-05`.  
- Write an SQL query that reports the number of posts reported yesterday for each report reason.  

```diff
 Actions table:
  +---------+---------+-------------+--------+--------+
  | user_id | post_id | action_date | action | extra  |
  +---------+---------+-------------+--------+--------+
  | 1       | 1       | 2019-07-01  | view   | null   |
  | 1       | 1       | 2019-07-01  | like   | null   |
  | 1       | 1       | 2019-07-01  | share  | null   |
! | 2       | 4       | 2019-07-04  | view   | null   |
+ | 2       | 4       | 2019-07-04  | report | spam   |
! | 3       | 4       | 2019-07-04  | view   | null   |
+ | 3       | 4       | 2019-07-04  | report | spam   |
  | 4       | 3       | 2019-07-02  | view   | null   |
  | 4       | 3       | 2019-07-02  | report | spam   |
! | 5       | 2       | 2019-07-04  | view   | null   |
- | 5       | 2       | 2019-07-04  | report | racism |
! | 5       | 5       | 2019-07-04  | view   | null   |
- | 5       | 5       | 2019-07-04  | report | racism |
  +---------+---------+-------------+--------+--------+
  Result table:
  +---------------+--------------+
  | report_reason | report_count |
  +---------------+--------------+
  | spam          | 1            |
  | racism        | 2            |
  +---------------+--------------+
```

```sql
SELECT extra AS report_reason, 
       COUNT(DISTINCT post_id) AS report_count
FROM Actions
WHERE extra IS NOT NULL 
AND action = 'report'
AND DATEDIFF("2019-07-05", action_date) = 1
GROUP BY extra;
```

## User Activity for the Past 30 Days I   

- Keyword : `DATEDIFF`

Write an SQL query to find the daily active user count for a period of 30 days ending `2019-07-27` inclusively.  

A user was active on some day if he/she made at least one activity on that day.
```
Activity table:
+---------+------------+---------------+---------------+
| user_id | session_id | activity_date | activity_type |
+---------+------------+---------------+---------------+
| 1       | 1          | 2019-07-20    | open_session  |
| 1       | 1          | 2019-07-20    | scroll_down   |
| 1       | 1          | 2019-07-20    | end_session   |
| 2       | 4          | 2019-07-20    | open_session  |
| 2       | 4          | 2019-07-21    | send_message  |
| 2       | 4          | 2019-07-21    | end_session   |
| 3       | 2          | 2019-07-21    | open_session  |
| 3       | 2          | 2019-07-21    | send_message  |
| 3       | 2          | 2019-07-21    | end_session   |
| 4       | 3          | 2019-06-25    | open_session  |
| 4       | 3          | 2019-06-25    | end_session   |
+---------+------------+---------------+---------------+
```
- There is no primary key for this table, it may have duplicate rows. 
- The `activity_type` column is an ENUM of type (`'open_session', 'end_session', 'scroll_down', 'send_message'`).


```sql
Result table:
+------------+--------------+ 
| day        | active_users |
+------------+--------------+ 
| 2019-07-20 | 2            |
| 2019-07-21 | 2            |
+------------+--------------+ 
```
- Note that we do not care about days with zero active users.


```sql
/**
+---------+------------+---------------+---------------+
| user_id | session_id | activity_date | activity_type |
+---------+------------+---------------+---------------+
| 1       | 1          | 2019-07-20    | open_session  |
| 1       | 1          |               | scroll_down   |
| 1       | 1          |               | end_session   |
| 2       | 4          |               | open_session  |
| 2       | 4          | 2019-07-21    | send_message  |
| 2       | 4          |               | end_session   |
| 3       | 2          |               | open_session  |
| 3       | 2          |               | send_message  |
| 3       | 2          |               | end_session   |
+---------+------------+---------------+---------------+ 
**/
SELECT activity_date           AS day, 
       Count(DISTINCT user_id) AS active_users 
FROM   activity 
GROUP  BY activity_date 
HAVING Datediff("2019-07-27", activity_date) < 30 
ORDER  BY NULL 
```

## User Activity for the Past 30 Days II

Write an SQL query to find the **average number of sessions per user for a period of 30 days ending `2019-07-27` inclusively**, rounded to 2 decimal places.  
- The sessions we want to count for a user are those with at least one activity in that time period.

```sql
Activity table:
+---------+------------+---------------+---------------+
| user_id | session_id | activity_date | activity_type |
+---------+------------+---------------+---------------+
| 1       | 1          | 2019-07-20    | open_session  |
| 1       | 1          | 2019-07-20    | scroll_down   |
| 1       | 1          | 2019-07-20    | end_session   |
| 2       | 4          | 2019-07-20    | open_session  |
| 2       | 4          | 2019-07-21    | send_message  |
| 2       | 4          | 2019-07-21    | end_session   |
| 3       | 2          | 2019-07-21    | open_session  |
| 3       | 2          | 2019-07-21    | send_message  |
| 3       | 2          | 2019-07-21    | end_session   |
| 3       | 5          | 2019-07-21    | open_session  |
| 3       | 5          | 2019-07-21    | scroll_down   |
| 3       | 5          | 2019-07-21    | end_session   |
| 4       | 3          | 2019-06-25    | open_session  |
| 4       | 3          | 2019-06-25    | end_session   |
+---------+------------+---------------+---------------+

Result table:
+---------------------------+ 
| average_sessions_per_user |
+---------------------------+ 
| 1.33                      |
+---------------------------+ 
```
- User `1` and `2` each had 1 session in the past 30 days while user 3 had 2 sessions so the average  is `(1 + 1 + 2) / 3 = 1.33.` 


```sql
# Time:  O(n)
# Space: O(n)
SELECT Round(Ifnull(Count(DISTINCT session_id) / 
              Count(DISTINCT user_id), 0), 2) 
       AS average_sessions_per_user 
FROM   activity 
WHERE  Datediff("2019-07-27", activity_date) < 30 
```

## Article Views I

Write an SQL query to find all the authors that viewed at least one of their own articles, **sorted in ascending order by their id**.
- Note that equal `author_id` and `viewer_id` indicate the same person.

```sql
  Views TABLE 
  +------------+-----------+-----------+------------+
  | article_id | author_id | viewer_id | view_date  |
  +------------+-----------+-----------+------------+
  | 1          | 3         | 5         | 2019-08-01 |
  | 1          | 3         | 6         | 2019-08-02 |
  | 2          | 7         | 7         | 2019-08-01 |
  | 2          | 7         | 6         | 2019-08-02 |
  | 4          | 7         | 1         | 2019-07-22 |
  | 3          | 4         | 4         | 2019-07-21 |
  | 3          | 4         | 4         | 2019-07-21 |
  +------------+-----------+-----------+------------+

  Result
  +------+
  | id   |
  +------+
  | 4    |
  | 7    |
  +------+
```

```mysql
SELECT DISTINCT author_id AS id 
/**
  +------------+-----------+-----------+
  | article_id | author_id | viewer_id | 
  +------------+-----------+-----------+
  | 2          | 7         | 7         | 
  +------------+-----------+-----------+
  | 3          | 4         | 4         |
  | 3          | 4         | 4         |
  +------------+-----------+-----------+
*/
FROM Views
WHERE author_id = viewer_id
ORDER BY id;
```

## !Immediate Food Delivery I

Concept : `FROM table1, table2  ...`

Write an SQL query to find the percentage of `immediate` orders in the table, rounded to 2 decimal places.  
- **If the preferred delivery date of the customer is the same as the order date then the order is called `immediate` otherwise it???s called scheduled.**

```diff
  +-------------+-------------+------------+-----------------------------+
  | delivery_id | customer_id | order_date | customer_pref_delivery_date |
  +-------------+-------------+------------+-----------------------------+
  | 1           | 1           | 2019-08-01 | 2019-08-02                  |
- | 2           | 5           | 2019-08-02 | 2019-08-02                  |
- | 3           | 1           | 2019-08-11 | 2019-08-11                  |
  | 4           | 3           | 2019-08-24 | 2019-08-26                  |
  | 5           | 4           | 2019-08-21 | 2019-08-22                  |
  | 6           | 2           | 2019-08-11 | 2019-08-13                  |
  +-------------+-------------+------------+-----------------------------+
  
  Result table:
  +----------------------+
  | immediate_percentage |
  +----------------------+
  | 33.33                |
  +----------------------+
```
- The orders with delivery id `2` and `3` are immediate while the others are scheduled.



```mysql
# Time:  O(n)
# Space: O(1)
SELECT Round(100 * Sum(order_date = customer_pref_delivery_date) / Count(*), 2) 
       AS immediate_percentage 
FROM  delivery;


-- Same as 
SELECT ROUND(100 * o.immediate_order / count(d.delivery_id) , 2) AS immediate_percentage 
FROM Delivery AS d,
     SELECT COUNT(order_date) AS immediate_order
      FROM Delivery
      WHERE order_date = customer_pref_delivery_date AS o
    
```

## !Reformat Department Table

#### Concept
-`CASE WHEN ...`, `IF`

Write an SQL query to reformat the table such that there is a department id column and a revenue column for each month.
```
  Department table:
  +------+---------+-------+
  | id   | revenue | month |
  +------+---------+-------+
  | 1    | 8000    | Jan   |
  | 2    | 9000    | Jan   |
  | 3    | 10000   | Feb   |
  | 1    | 7000    | Feb   |
  | 1    | 6000    | Mar   |
  +------+---------+-------+
- The month has values in ["Jan","Feb","Mar","Apr","May","Jun","Jul","Aug","Sep","Oct","Nov","Dec"].

```

```diff
  Result table:
  +------+-------------+-------------+-------------+-----+-------------+
  | id   | Jan_Revenue | Feb_Revenue | Mar_Revenue | ... | Dec_Revenue |
  +------+-------------+-------------+-------------+-----+-------------+
  | 1    | 8000        | 7000        | 6000        | ... | null        |
  | 2    | 9000        | null        | null        | ... | null        |
  | 3    | null        | 10000       | null        | ... | null        |
  +------+-------------+-------------+-------------+-----+-------------+
- Note that the result table has 13 columns (1 for the department id + 12 for the months).
```

```mysql
/**
  Department table:
  +------+---------+-------+
  | id   | revenue | month |
  +------+---------+-------+
  | 1    | 8000    | Jan   |
  |      | 7000    | Feb   |
  |      | 6000    | Mar   |
  | 2    | 9000    | Jan   |
  | 3    | 10000   | Feb   |
  +------+---------+-------+

*/
SELECT id,
  SUM(CASE WHEN month = 'Jan' THEN revenue ELSE NULL END) AS Jan_Revenue,
  SUM(CASE WHEN month = 'Feb' THEN revenue ELSE NULL END) AS Feb_Revenue,
  SUM(CASE WHEN month = 'Mar' THEN revenue ELSE NULL END) AS Mar_Revenue,
  SUM(CASE WHEN month = 'Apr' THEN revenue ELSE NULL END) AS Apr_Revenue,
  SUM(CASE WHEN month = 'May' THEN revenue ELSE NULL END) AS May_Revenue,
  SUM(CASE WHEN month = 'Jun' THEN revenue ELSE NULL END) AS Jun_Revenue,
  SUM(CASE WHEN month = 'Jul' THEN revenue ELSE NULL END) AS Jul_Revenue,
  SUM(CASE WHEN month = 'Aug' THEN revenue ELSE NULL END) AS Aug_Revenue,
  SUM(CASE WHEN month = 'Sep' THEN revenue ELSE NULL END) AS Sep_Revenue,
  SUM(CASE WHEN month = 'Oct' THEN revenue ELSE NULL END) AS Oct_Revenue,
  SUM(CASE WHEN month = 'Nov' THEN revenue ELSE NULL END) AS Nov_Revenue,
  SUM(CASE WHEN month = 'Dec' THEN revenue ELSE NULL END) AS Dec_Revenue
FROM Department
GROUP BY id;

# Time:  O(n)
# Space: O(n)
SELECT id, 
       SUM(IF(month = 'Jan', revenue, NULL)) AS Jan_Revenue, 
       SUM(IF(month = 'Feb', revenue, NULL)) AS Feb_Revenue, 
       SUM(IF(month = 'Mar', revenue, NULL)) AS Mar_Revenue, 
       SUM(IF(month = 'Apr', revenue, NULL)) AS Apr_Revenue, 
       SUM(IF(month = 'May', revenue, NULL)) AS May_Revenue, 
       SUM(IF(month = 'Jun', revenue, NULL)) AS Jun_Revenue, 
       SUM(IF(month = 'Jul', revenue, NULL)) AS Jul_Revenue, 
       SUM(IF(month = 'Aug', revenue, NULL)) AS Aug_Revenue, 
       SUM(IF(month = 'Sep', revenue, NULL)) AS Sep_Revenue, 
       SUM(IF(month = 'Oct', revenue, NULL)) AS Oct_Revenue, 
       SUM(IF(month = 'Nov', revenue, NULL)) AS Nov_Revenue, 
       SUM(IF(month = 'Dec', revenue, NULL)) AS Dec_Revenue 
FROM   department 
GROUP  BY id;
```

## !Queries Quality and Percentage

Concept 
  - Aggregation function with query : `(round(avg(...), ...)`,`CASE WHEN( IF ... THEN ... ELSE ... END )`

Write an SQL query to find each `query_name`, the `quality` and `poor_query_percentage`. 
- Both `quality` and `poor_query_percentage` should be rounded to 2 decimal places.
- We define query `quality` as: 
  > The average of the ratio between query rating and its position.
- We also define `poor_query_percentage` as: 
  > The percentage of all queries with `rating` less than 3.   
  > if `rating > 3` then `1` else `0`   
 
```diff
  Queries table:
  +------------+-------------------+----------+--------+
  | query_name | result            | position | rating |
  +------------+-------------------+----------+--------+
  | Dog        | Golden Retriever  | 1        | 5      |
  | Dog        | German Shepherd   | 2        | 5      |
  | Dog        | Mule              | 200      | 1      |
  | Cat        | Shirazi           | 5        | 2      |
  | Cat        | Siamese           | 3        | 3      |
  | Cat        | Sphynx            | 7        | 4      |
  +------------+-------------------+----------+--------+

  Result table:
  +------------+---------+-----------------------+
  | query_name | quality | poor_query_percentage |
  +------------+---------+-----------------------+
  | Dog        | 2.50    | 33.33                 |
  | Cat        | 0.66    | 33.33                 |
  +------------+---------+-----------------------+
```
- Dog queries `quality is ( (5 / 1) + (5 / 2) + (1 / 200) ) / 3  = 2.50`
- Dog queries `poor_ query_percentage is (1 / 3) * 100 = 33.33`
- Cat queries `quality equals ((2 / 5) + (3 / 3) + (4 / 7) ) / 3 = 0.66`
- Cat queries `poor_ query_percentage is (1 / 3) * 100 = 33.33`

- [`COUNT(*) VS COUNT(1)`](https://stackoverflow.com/questions/1221559/count-vs-count1-sql-server)
```mysql
SELECT query_name,
       round(avg(rating/position), 2) AS quality,
       round(100 * sum(case when rating < 3 then 1 else 0 end)  / count(1), 2) AS poor_query_percentage
       
/**
  +------------+-------------------+----------+--------+
  | query_name | result            | position | rating |
  +------------+-------------------+----------+--------+
  | Dog        | Golden Retriever  | 1        | 5      |
  |            | German Shepherd   | 2        | 5      |
  |            | Mule              | 200      | 1      |
  | Cat        | Shirazi           | 5        | 2      |
  |            | Siamese           | 3        | 3      |
  |            | Sphynx            | 7        | 4      |
  +------------+-------------------+----------+--------+
 */
FROM Queries
GROUP BY query_name
```

## !Number of Comments per Post

Write an SQL query to find number of comments per each post.  
- Result table should contain `post_id` and its corresponding number of comments, and must be sorted by `post_id` in ascending order.
- You should count the number of unique comments per post.  
- Submissions table may contain duplicate comments.  
- Submissions table may contain duplicate posts. You should treat them as one post.

```diff
  Submissions table:
  +---------+------------+
  | sub_id  | parent_id  |
  +---------+------------+
  | 1       | Null       |
  | 2       | Null       |
  | 1       | Null       |
  | 12      | Null       |
- | 3       | 1          |
+ | 5       | 2          |
- | 3       | 1          |
- | 4       | 1          |
- | 9       | 1          |
+ | 10      | 2          |
  | 6       | 7          |
  +---------+------------+
- sub_id 1,2,12 are submissions
- There is no primary key for this table, it may have duplicate rows.

  Result Table
  +---------+--------------------+
  | post_id | number_of_comments |
  +---------+--------------------+
  | 1       | 3                  |
  | 2       | 2                  |
  | 12      | 0                  |
  +---------+--------------------+
```

Concept
- Nested Query
- `SELECT DISTINCT` TO FIND SUBS
- `LEFT JOIN` 
- `COUNT()` AND `GROUD BY` TO COUNT COMMENTS

```sql
/** 
    +---------+------------+
    | sub_id  | parent_id  |
    +---------+------------+
    | 1       | Null       |
    | 2       | Null       |
    | 12      | Null       | 
    +---------+------------+
                              
    +---------+------------+    
    | sub_id  | parent_id  |  
    +---------+------------+
    | 3       | 1          |
  + | 5       | 2          |
  - | 3       | 1          |
  - | 4       | 1          |
  - | 9       | 1          |
  + | 10      | 2          |
    | 6       | 7          |
    +---------+------------+
  */
SELECT DISTINCT post_id, 
        COUNT(distinct sub_id) AS number_of_comments 
        FROM (
        -- SUBS TABLE
          SELECT DISTINCT sub_id AS post_id 
          FROM submissions 
          WHERE parent_id IS NULL AS P)
-- FOUND COMMENT OF EACH SUBS 
LEFT JOIN submissions C 
ON P.post_id = C.parent_id AS tmp
GROUP BY post_id

# Time:  O(n)
# Space: O(n)
SELECT COMMENTS.sub_id             AS post_id, 
       Count(DISTINCT POST.sub_id) AS number_of_comments 
FROM   submissions COMMENTS
       LEFT JOIN submissions POST
       ON COMMENTS.sub_id = POST.parent_id 
WHERE  COMMENTS.parent_id IS NULL 
GROUP  BY COMMENTS.sub_id 
ORDER  BY NULL 
```

## !Students and Examinations

Write an SQL query to find the number of times each student attended each exam.   
Order the result table by `student_id` and `subject_name`.   

```diff
  Students table:
  +------------+--------------+
  | student_id | student_name |
  +------------+--------------+
  | 1          | Alice        |
  | 2          | Bob          |
  | 13         | John         |
  | 6          | Alex         |
  +------------+--------------+
  
  Subjects table:
  +--------------+
  | subject_name |
  +--------------+
  | Math         |
  | Physics      |
  | Programming  |
  +--------------+
  
  Examinations table:
  +------------+--------------+
  | student_id | subject_name |
  +------------+--------------+
  | 1          | Math         |
  | 1          | Physics      |
  | 1          | Programming  |
  | 2          | Programming  |
  | 1          | Physics      |
  | 1          | Math         |
  | 13         | Math         |
  | 13         | Programming  |
  | 13         | Physics      |
  | 2          | Math         |
  | 1          | Math         |
  +------------+--------------+
  

  Result table:
  +------------+--------------+--------------+----------------+
  | student_id | student_name | subject_name | attended_exams |
  +------------+--------------+--------------+----------------+
  | 1          | Alice        | Math         | 3              |
  | 1          | Alice        | Physics      | 2              |
  | 1          | Alice        | Programming  | 1              |
  | 2          | Bob          | Math         | 1              |
  | 2          | Bob          | Physics      | 0              |
  | 2          | Bob          | Programming  | 1              |
  | 6          | Alex         | Math         | 0              |
  | 6          | Alex         | Physics      | 0              |
  | 6          | Alex         | Programming  | 0              |
  | 13         | John         | Math         | 1              |
  | 13         | John         | Physics      | 1              |
  | 13         | John         | Programming  | 1              |
  +------------+--------------+--------------+----------------+
```
The result table should contain all students and all subjects.
- Alice attended Math exam 3 times, Physics exam 2 times and Programming exam 1 time.
- Bob attended Math exam 1 time, Programming exam 1 time and didn't attend the Physics exam.
+ Alex didn't attend any exam.
+ John attended Math exam 1 time, Physics exam 1 time and Programming exam 1 time.


```mysql 
# Time:  O((m * n) * log(m * n))
# Space: O(m * n)

SELECT a.student_id, 
       a.student_name, 
       b.subject_name, 
       Count(c.subject_name) AS attended_exams 
FROM   students AS a                  
       CROSS JOIN subjects AS b  -- EACH STUDENT TAKES ALL COURSES
       /**
          +------------+--------------+----------------+
          | student_id | student_name |   subject_name |
          +------------+--------------+----------------+
          | 1          | Alice        |   Math         |
          | 1          | Alice        |   Physics      |
          | 1          | Alice        |   Programming  |
          | 2          | Bob          |   Math         |  
          | 2          | Bob          |   Physics      |
          | 2          | Bob          |   Programming  |
          | 13         | John         |   Math         |
          | 13         | John         |   Physics      |
          | 13         | John         |   Programming  |
          | 6          | Alex         |   Math         |
          | 6          | Alex         |   Physics      |
          | 6          | Alex         |   Programming  |
          +------------+--------------+----------------+
          
          
          +------------+--------------+----------------+------------+--------------+
          |a.student_id|a.student_name| b.subject_name |c.student_id|c.subject_name|
          +------------+--------------+----------------+------------+--------------+
          | 1          | Alice        |   Math         | 1          | Math         |
          | 1          | Alice        |   Math         | 1          | Math         |
          | 1          | Alice        |   Math         | 1          | Math         |
          | 1          | Alice        |   Physics      | 1          | Physics      |
          | 1          | Alice        |   Physics      | 1          | Physics      |
          | 1          | Alice        |   Programming  | 1          | Programming  |
          | 2          | Bob          |   Math         | 2          | Math         |
          | 2          | Bob          |   Physics      | NULL       | NULL         |
          | 2          | Bob          |   Programming  | 2          | Programming  |
          | 13         | John         |   Math         | 13         | Math         |
          | 13         | John         |   Physics      | 13         | Programming  |
          | 13         | John         |   Programming  | 13         | Physics      |
          | 6          | Alex         |   Math         | NULL       | NULL         |
          | 6          | Alex         |   Physics      | NULL       | NULL         |
          | 6          | Alex         |   Programming  | NULL       | NULL         |
          +------------+--------------+----------------+------------+--------------+

       
       **/
       LEFT JOIN examinations AS c 
              ON  a.student_id   = c.student_id 
              AND b.subject_name = c.subject_name 
/**
  +------------+--------------+----------------+------------+--------------+
  |a.student_id|a.student_name| b.subject_name | student_id | subject_name |
  +------------+--------------+----------------+------------+--------------+
  | 1          | Alice        |   Math         | 1          | Math         |
  |            |              |   Math         | 1          | Math         |
  |            |              |   Math         | 1          | Math         |
  | 1          | Alice        |   Physics      | 1          | Physics      |
  |            |              |   Physics      | 1          | Physics      |
  | 1          | Alice        |   Programming  | 1          | Programming  |
  | 2          | Bob          |   Math         | 2          | Math         |
  | 2          | Bob          |   Physics      | NULL       | NULL         |
  | 2          | Bob          |   Programming  | 2          | Programming  |
  | 13         | John         |   Math         | 13         | Math         |
  | 13         | John         |   Physics      | 13         | Programming  |
  | 13         | John         |   Programming  | 13         | Physics      |
  | 6          | Alex         |   Math         | NULL       | NULL         |
  | 6          | Alex         |   Physics      | NULL       | NULL         |
  | 6          | Alex         |   Programming  | NULL       | NULL         |
  +------------+--------------+----------------+------------+--------------+
*/
GROUP  BY a.student_id, 
          b.subject_name
ORDER  BY a.student_id, 
          b.subject_name;
```

## !Weather Type in Each Country

Write an SQL query to find the type of weather in each country for `November 2019(2019-11)`.
- The type of weather is 
  > `Cold` if the average weather_state is less than or equal 15,    
  > `Hot` if the average weather_state is greater than or equal 25 and   
  > `Warm` otherwise.     

Return result table in any order.

```diff
  Countries table:
  +------------+--------------+
  | country_id | country_name |
  +------------+--------------+
  | 2          | USA          |
  | 3          | Australia    |
  | 7          | Peru         |
  | 5          | China        |
  | 8          | Morocco      |
  | 9          | Spain        |
  +------------+--------------+
  
  Weather table:
  +------------+---------------+------------+
  | country_id | weather_state | day        |
  +------------+---------------+------------+
  | 2          | 15            | 2019-11-01 |
  | 2          | 12            | 2019-10-28 |
  | 2          | 12            | 2019-10-27 |
  | 3          | -2            | 2019-11-10 |
  | 3          | 0             | 2019-11-11 |
  | 3          | 3             | 2019-11-12 |
  | 5          | 16            | 2019-11-07 |
  | 5          | 18            | 2019-11-09 |
  | 5          | 21            | 2019-11-23 |
  | 7          | 25            | 2019-11-28 |
  | 7          | 22            | 2019-12-01 |
  | 7          | 20            | 2019-12-02 |
  | 8          | 25            | 2019-11-05 |
  | 8          | 27            | 2019-11-15 |
  | 8          | 31            | 2019-11-25 |
  | 9          | 7             | 2019-10-23 |
  | 9          | 3             | 2019-12-23 |
  +------------+---------------+------------+
  
  Result table:
  +--------------+--------------+
  | country_name | weather_type |
  +--------------+--------------+
  | USA          | Cold         |
  | Austraila    | Cold         |
  | Peru         | Hot          |
  | China        | Warm         |
  | Morocco      | Hot          |
  +--------------+--------------+
```
- Average weather_state in USA in November is `(15) / 1 = 15` so weather type is Cold.
- Average weather_state in Austraila in November is `(-2 + 0 + 3) / 3 = 0.333` so weather type is Cold.
- Average weather_state in Peru in November is `(25) / 1 = 25` so weather type is Hot.
- Average weather_state in China in November is `(16 + 18 + 21) / 3 = 18.333` so weather type is Warm.
- Average weather_state in Morocco in November is `(25 + 27 + 31) / 3 = 27.667` so weather type is Hot.
- We know nothing about average `weather_state` in `Spain` in November so we don't include it in the result table. 

```mysql
SELECT c.country_name,
       CASE
           WHEN AVG(w.weather_state * 1.0) <= 15.0 THEN 'Cold'
           WHEN AVG(w.weather_state * 1.0) >= 25.0 THEN 'Hot'
           ELSE 'Warm'
       END AS weather_type
FROM Countries AS c
/**
  +--------------+------------+---------------+------------+
  | country_name | country_id | weather_state | day        |
  +--------------+------------+---------------+------------+
+ | USA          | 2          | 15            | 2019-11-01 |
  | USA          | 2          | 12            | 2019-10-28 |
  | USA          | 2          | 12            | 2019-10-27 |
+ | Australia    | 3          | -2            | 2019-11-10 |
+ | Australia    | 3          | 0             | 2019-11-11 |
+ | Australia    | 3          | 3             | 2019-11-12 |
+ | China        | 5          | 16            | 2019-11-07 |
+ | China        | 5          | 18            | 2019-11-09 |
+ | China        | 5          | 21            | 2019-11-23 |
+ | Peru         | 7          | 25            | 2019-11-28 |
  | Peru         | 7          | 22            | 2019-12-01 |
  | Peru         | 7          | 20            | 2019-12-02 |
+ | Morocco      | 8          | 25            | 2019-11-05 |
+ | Morocco      | 8          | 27            | 2019-11-15 |
+ | Morocco      | 8          | 31            | 2019-11-25 |
  | Spain        | 9          | 7             | 2019-10-23 |
  | Spain        | 9          | 3             | 2019-12-23 |
  +--------------+------------+---------------+------------+
  
  +------------+--------------+---------------+------------+
  | country_id | country_name | weather_state | day        |
  +------------+--------------+---------------+------------+
  | 2          | USA          | 15            | 2019-11-01 |
  | 3          | Australia    | -2            | 2019-11-10 |
  |            | Australia    | 0             | 2019-11-11 |
  |            | Australia    | 3             | 2019-11-12 |
  | 5          | China        | 16            | 2019-11-07 |
  |            | China        | 18            | 2019-11-09 |
  |            | China        | 21            | 2019-11-23 |
  | 7          | Peru         | 25            | 2019-11-28 |
  | 8          | Morocco      | 25            | 2019-11-05 |
  |            | Morocco      | 27            | 2019-11-15 |
  |            | Morocco      | 31            | 2019-11-25 |
  +------------+--------------+---------------+------------+
*/
INNER JOIN Weather AS w 
ON c.country_id = w.country_id
-- WHERE w.day BETWEEN '2019-11-01' AND '2019-11-30'
WHERE LEFT(day, 7) = '2019-11'
GROUP BY c.country_id;
```

## !Find the Team Size

Write an SQL query to find the team size of each of the employees.
- Return result table in any order.
```diff
  Employee Table:
  +-------------+------------+
  | employee_id | team_id    |
  +-------------+------------+
  |     1       |     8      |
  |     2       |     8      |
  |     3       |     8      |
  |     4       |     7      |
  |     5       |     9      |
  |     6       |     9      |
  +-------------+------------+
  Result table:
  +-------------+------------+
  | employee_id | team_size  |
  +-------------+------------+
  |     1       |     3      |
  |     2       |     3      |
  |     3       |     3      |
  |     4       |     1      |
  |     5       |     2      |
  |     6       |     2      |
  +-------------+------------+
```

```mysql
- THINK WHY IT NOT WORKING 
select employee_id , 
       count(team_id) as team_size
from Employee
group by team_id;
```

```mysql
# Time:  O(n)
# Space: O(n)

SELECT t1.employee_id, 
       t2.team_size
FROM Employee as t1
INNER JOIN (/**
                  +------------+-------------+
                  | team_id    | employee_id |
                  +------------+-------------+
                  |     8      |     1       |
                  |            |     2       |
                  |            |     3       |
                  |     7      |     4       |
                  |     9      |     5       |
                  |            |     6       |
                  +------------+-------------+

                  +------------+-------------+
                  | team_id    |  team_size  |
                  +------------+-------------+
                  |     8      |     3       |
                  |     7      |     1       |
                  |     9      |     2       |
                  +------------+-------------+
             */
            SELECT team_id, 
            COUNT(1) AS team_size
            FROM Employee
            GROUP BY team_id) as t2
ON t1.team_id = t2.team_id

---

SELECT employee_id, 
       COUNT(employee_id)OVER(PARTITION BY team_id) AS team_size
FROM Employee
ORDER BY employee_id;
```
## Ads Performance

Write an SQL query to find the ctr of each Ad.  
- Round ctr to 2 decimal points.  
- Order the result table by ctr in descending order and by `ad_id` in ascending order in case of a tie.
```diff
  Ads table:
  +-------+---------+---------+
  | ad_id | user_id | action  |
  +-------+---------+---------+ 
  | 1     | 1       | Clicked | 
  | 2     | 2       | Clicked | 
  | 3     | 3       | Viewed  | 
  | 5     | 5       | Ignored | 
  | 1     | 7       | Ignored | 
  | 2     | 7       | Viewed  | 
  | 3     | 5       | Clicked | 
  | 1     | 4       | Viewed  |  
  | 2     | 11      | Viewed  | 
  | 1     | 2       | Clicked | 
  +-------+---------+---------+
```
- For `crt = round( clicks / (clicks+views) * 100, 2) ` 
  - `ad_id = 1, ctr = (2/(2+1)) * 100 = 66.67`
  - `ad_id = 2, ctr = (1/(1+2)) * 100 = 33.33`
  - `ad_id = 3, ctr = (1/(1+1)) * 100 = 50.00`
  - `ad_id = 5, ctr = 0.00.` 
- Note that `ad_id` has no clicks or views.
- Note that we don't care about `Ignored` Ads.
- Result table is ordered by the `ctr`. 
- In case of a tie we order them by `ad_id`


```mysql
  Result table:
  +-------+-------+
  | ad_id | ctr   |
  +-------+-------+
  | 1     | 66.67 |
  | 3     | 50.00 |
  | 2     | 33.33 |
  | 5     | 0.00  |
  +-------+-------+
```

```mysql
SELECT ad_id,
    (
      CASE WHEN clicks + views = 0 
      THEN 0 
      ELSE round( clicks / (clicks+views)*100, 2) end
    ) AS ctr
FROM 
    ( /**
          +-------+---------+---------+
          | ad_id | user_id | action  |
          +-------+---------+---------+ 
          | 1     | 1       | Clicked | 
          |       | 2       | Clicked | 
          |       | 4       | Viewed  | 
          |       | 7       | Ignored | 
          | 2     | 2       | Clicked | 
          |       | 7       | Viewed  | 
          |       | 11      | Viewed  | 
          | 3     | 3       | Viewed  | 
          | 5     | 5       | Ignored | 
          +-------+---------+---------+
          
          
          
          +-------+---------+---------+
          | ad_id | clicks  | views   |
          +-------+---------+---------+ 
          | 1     | 2       | 1       | 
          | 2     | 1       | 2       | 
          | 3     | 0       | 1       | 
          | 5     | 0       | 0       | 
          +-------+---------+---------+
          
       */
    SELECT ad_id,
           SUM(case when action='Clicked' then 1 else 0 end) as clicks,
           SUM(case when action='Viewed' then 1 else 0 end) as views
    FROM Ads
    GROUP BY ad_id) as t
ORDER BY ctr DESC, 
         ad_id ASC
```

## !List the Products Ordered in a Period

Write an SQL query to get the names of products with greater than or equal to 100 units(` >= 100`) ordered in `February 2020` and their amount.

```diff
  Products table:
  Product_id is PK
  
  +-------------+-----------------------+------------------+
  | product_id  | product_name          | product_category |
  +-------------+-----------------------+------------------+
  | 1           | Leetcode Solutions    | Book             |
  | 2           | Jewels of Stringology | Book             |
  | 3           | HP                    | Laptop           |
  | 4           | Lenovo                | Laptop           |
  | 5           | Leetcode Kit          | T-shirt          |
  +-------------+-----------------------+------------------+
 
  Orders table:
  +--------------+--------------+----------+
  | product_id   | order_date   | unit     |
  +--------------+--------------+----------+
  | 1            | 2020-02-05   | 60       |
  | 1            | 2020-02-10   | 70       |
  | 2            | 2020-01-18   | 30       |
  | 2            | 2020-02-11   | 80       |
  | 3            | 2020-02-17   | 2        |
  | 3            | 2020-02-24   | 3        |
  | 4            | 2020-03-01   | 20       |
  | 4            | 2020-03-04   | 30       |
  | 4            | 2020-03-04   | 60       |
  | 5            | 2020-02-25   | 50       |
  | 5            | 2020-02-27   | 50       |
  | 5            | 2020-03-01   | 50       |
  +--------------+--------------+----------+

  Result table:
  +--------------------+---------+
  | product_name       | unit    |
  +--------------------+---------+
  | Leetcode Solutions | 130     |
  | Leetcode Kit       | 100     |
  +--------------------+---------+

- Products with product_id = 1 is ordered in February a total of (60 + 70) = 130.
Products with product_id = 2 is ordered in February a total of 80.
Products with product_id = 3 is ordered in February a total of (2 + 3) = 5.
Products with product_id = 4 was not ordered in February 2020.
- Products with product_id = 5 is ordered in February a total of (50 + 50) = 100.
```


#### Concept 
- GET DESIRED `product_id` and `order_date` FROM `Orders` table
- INNER JOIN WITH `Product`

```mysql
SELECT product_name, sum(unit) AS unit
FROM Products 
INNER JOIN Orders
ON Products.product_id = Orders.product_id
WHERE left(order_date, 7) = "2020-02"
GROUP BY Products.product_id
HAVING sum(unit)>=100

SELECT product_name, SUM(unit) AS unit FROM Products AS p 
JOIN Orders AS o 
ON p.product_id = o.product_id 
WHERE order_date BETWEEN '2020-02-01' AND '2020-02-29' 
GROUP BY product_name 
HAVING sum(unit) >= 100

# Time:  O(n)  
# Space: O(n)  
SELECT p.product_name, 
       o.unit 
FROM   (
        /** Table with product_id with desired order_Date 
        
        
         
        +--------------+--------------+----------+
        | product_id   | order_date   | unit     |
        +--------------+--------------+----------+
        | 1            | 2020-02-05   | 60       |
        | 1            | 2020-02-10   | 70       |
        | 2            | 2020-01-18   | 30       |
        | 2            | 2020-02-11   | 80       |
        | 3            | 2020-02-17   | 2        |
        | 3            | 2020-02-24   | 3        |
        | 5            | 2020-02-25   | 50       |
        | 5            | 2020-02-27   | 50       |
        +--------------+--------------+----------+
        
        **/
        SELECT product_id, 
               Sum(unit) AS unit 
        FROM   orders 
        WHERE  order_date BETWEEN '2020-02-01' AND '2020-02-29' 
        GROUP  BY product_id 
        HAVING unit >= 100) o 
INNER JOIN products p 
ON o.product_id = p.product_id 
```

## Students With Invalid Departments 

Write a query that student does not exist in the department 

#### Concept
- `WHERE NOT EXISTS( ... )`

```Departments table:
+------+--------------------------+
| id   | name                     |
+------+--------------------------+
| 1    | Electrical Engineering   |
| 7    | Computer Engineering     |
| 13   | Bussiness Administration |
+------+--------------------------+

Students table:
+------+----------+---------------+
| id   | name     | department_id |
+------+----------+---------------+
| 23   | Alice    | 1             | 
| 1    | Bob      | 7             |
| 5    | Jennifer | 13            |
| 2    | John     | 14            |
| 4    | Jasmine  | 77            |
| 3    | Steve    | 74            |
| 6    | Luis     | 1             |
| 8    | Jonathan | 7             |
| 7    | Daiana   | 33            |
| 11   | Madelynn | 1             |
+------+----------+---------------+

Result table:
+------+----------+
| id   | name     |
+------+----------+
| 2    | John     |
| 7    | Daiana   |
| 4    | Jasmine  |
| 3    | Steve    |
+------+----------+
```
- John, Daiana, Steve and Jasmine are enrolled in departments `14`, `33`, `74` and `77` respectively.
department `14`, `33`, `74` and `77` doesn't exist in the Departments table.


```mysql
/**

SELECT s.id, 
       s.name, 
       s.department_id,
       d.id,
       d.name
FROM   students  AS s 
       LEFT JOIN departments AS d 
       ON d.id = s.department_id 
WHERE  d.id IS NULL;

+------+----------+---------------+------+--------------------------+
| id   | name     | department_id | id   | name                     |
+------+----------+---------------+------+--------------------------+
| 23   | Alice    | 1             | 1    | Electrical Engineering   |
| 1    | Bob      | 7             | 7    | Computer Engineering     |
| 5    | Jennifer | 13            | 13   | Bussiness Administration |
| 2    | John     | 14            | null | null                     |
| 4    | Jasmine  | 77            | null | null                     |
| 3    | Steve    | 74            | null | null                     |
| 6    | Luis     | 1             | 1    | Electrical Engineering   |
| 8    | Jonathan | 7             | 7    | Computer Engineering     |
| 7    | Daiana   | 33            | null | null                     |
| 11   | Madelynn | 1             | 1    | Electrical Engineering   |
+------+----------+---------------+------+--------------------------+

**/

# Time:  O(n) 
# Space: O(n) 
SELECT s.id, 
       s.name 
FROM   students s 
       LEFT JOIN departments d 
       ON d.id = s.department_id 
WHERE  d.id IS NULL; 

# Time:  O(n) 
# Space: O(n) 
SELECT s.id, 
       s.name 
FROM   students s
WHERE  NOT EXISTS (SELECT d.id 
                   /** EQUI JOIN **/
                   FROM   departments d
                   WHERE  d.id = s.department_id); 
```

## Replace Employee ID with The Unique Identifier 

A PROBLEM THAT FIND WHO DOESN'T EXIST ON ANOTHER TABLE

Write an SQL query to show the unique ID of each user, If a user doesn???t have a unique ID replace just show `NULL`.
- Return the result table in any order.
```
Employees table:
+----+----------+
| id | name     |
+----+----------+
| 1  | Alice    |
| 7  | Bob      |
| 11 | Meir     |
| 90 | Winston  |
| 3  | Jonathan |
+----+----------+

EmployeeUNI table:
+----+-----------+
| id | unique_id |
+----+-----------+
| 3  | 1         |
| 11 | 2         |
| 90 | 3         |
+----+-----------+

Result 
+-----------+----------+
| unique_id | name     |
+-----------+----------+
| null      | Alice    |
| null      | Bob      |
| 2         | Meir     |
| 3         | Winston  |
| 1         | Jonathan |
+-----------+----------+
```

```mysql
# Time:  O(n)
# Space: O(n)
SELECT u.unique_id, e.name
FROM employees e
LEFT JOIN employeeuni u
ON e.id = u.id
```


## !Top Travellers

Write an SQL query to report the distance travelled by EACH USER.
- Return the result table ordered by `travelled_distance` in **descending order**, if two or more users travelled the same distance, order them by their name in ascending order.
```diff
  Users table( PK : id ) :
  +------+-----------+
  | id   | name      |
  +------+-----------+
  | 1    | Alice     |
  | 2    | Bob       |
  | 3    | Alex      |
  | 4    | Donald    |
  | 7    | Lee       |
  | 13   | Jonathan  |
  | 19   | Elvis     |
  +------+-----------+

  Rides table:
  +------+----------+----------+
  | id   | user_id  | distance |
  +------+----------+----------+
  | 1    | 1        | 120      |
  | 2    | 2        | 317      |
  | 3    | 3        | 222      |
  | 4    | 7        | 100      |
  | 5    | 13       | 312      |
  | 6    | 19       | 50       |
  | 7    | 7        | 120      |
  | 8    | 19       | 400      |
  | 9    | 7        | 230      |
  +------+----------+----------+

  Result table:
  +----------+--------------------+
  | name     | travelled_distance |
  +----------+--------------------+
  | Elvis    | 450                |
  | Lee      | 450                |
  | Bob      | 317                |
  | Jonathan | 312                |
  | Alex     | 222                |
  | Alice    | 120                |
  | Donald   | 0                  |
  +----------+--------------------+
```

```mysql 
SELECT U.name , 
       IFNULL(distance,0) AS travelled_distance 
/**
  +------+-----------+------+----------+----------+
  | id   | name      | id   | user_id  | distance |
  +------+-----------+------+----------+----------+
  | 1    | Alice     | 1    | 1        | 120      |
  | 2    | Bob       | 2    | 2        | 317      |
  | 3    | Alex      | 3    | 3        | 222      |
  | 4    | Donald    | NULL | NULL     | NULL     |
  | 7    | Lee       | 4    | 7        | 100      |
  | 7    | Lee       | 7    | 7        | 120      |
  | 7    | Lee       | 9    | 7        | 230      |
  | 13   | Jonathan  | 5    | 13       | 312      |
  | 19   | Elvis     | 8    | 19       | 400      |
  +------+-----------+------+----------+----------+
*/
FROM Users AS U 
LEFT JOIN 
Rides AS R
OB U.Id = R.user_id
GROUP BY u.name
ORDER BY travelled_distance ASEC, U.name ASEC 
```

## !Create a Session Bar Chart

Write an SQL query to report the (`bin`, `total`) in any order.

```diff
  Sessions table:
  +-------------+---------------+
  | session_id  | duration      |
  +-------------+---------------+
  | 1           | 30            |
  | 2           | 299           |
  | 3           | 340           |
  | 4           | 580           |
  | 5           | 1000          |
  +-------------+---------------+
  
  Result table:
  +--------------+--------------+
  | bin          | total        |
  +--------------+--------------+
  | [0-5>        | 3            |
  | [5-10>       | 1            |
  | [10-15>      | 0            |
  | 15 or more   | 1            |
  +--------------+--------------+
```
- For `session_id` 1, 2 and 3 have a duration greater or equal than 0 minutes and less than 5 minutes.
- For `session_id` 4 has a duration greater or equal than 5 minutes and less than 10 minutes.
- There are no session with a duration greater or equial than 10 minutes and less than 15 minutes.
- For `session_id` 5 has a duration greater or equal than 15 minutes.


```mysql
# Time:  O(n)
# Space: O(1)
SELECT '[0-5>'  AS bin, 
       Count(1) AS total 
FROM   sessions 
WHERE  duration >= 0 
       AND duration < 300 
UNION ALL
SELECT '[5-10>' AS bin, 
       Count(1) AS total 
FROM   sessions 
WHERE  duration >= 300 
       AND duration < 600 
UNION ALL 
SELECT '[10-15>' AS bin, 
       Count(1)  AS total 
FROM   sessions 
WHERE  duration >= 600 
       AND duration < 900 
UNION ALL 
SELECT '15 or more' AS bin, 
       Count(1)     AS total 
FROM   sessions 
WHERE  duration >= 900;

# Time:  O(n)
# Space: O(n)
SELECT
    t2.BIN,
    COUNT(t1.BIN) AS TOTAL
FROM (SELECT
          -- Create A Bin Column
          CASE 
              WHEN duration/60 BETWEEN 0 AND 5 THEN "[0-5>"
              WHEN duration/60 BETWEEN 5 AND 10 THEN "[5-10>"
              WHEN duration/60 BETWEEN 10 AND 15 THEN "[10-15>"
              WHEN duration/60 >= 15 THEN "15 or more" 
              ELSE NULL END AS BIN
      FROM Sessions) t1 
RIGHT JOIN(
    SELECT "[0-5>"        AS BIN
    UNION ALL
    SELECT "[5-10>"       AS BIN
    UNION ALL
    SELECT "[10-15>"      AS BIN
    UNION ALL
    SELECT "15 or more"   AS BIN
) t2
ON t1.bin = t2.bin
GROUP BY t2.bin
ORDER BY NULL;
```

## !Group Sold Products By The Date

Write an SQL query to find for each date, the number of distinct products sold and their names.   

The sold-products names for each date should be sorted lexicographically.   
- Return the result table ordered by `sell_date`.
```
  Activities table:
  +------------+-------------+
  | sell_date  | product     |
  +------------+-------------+
  | 2020-05-30 | Headphone   |
  | 2020-06-01 | Pencil      |
  | 2020-06-02 | Mask        |
  | 2020-05-30 | Basketball  |
  | 2020-06-01 | Bible       |
  | 2020-06-02 | Mask        |
  | 2020-05-30 | T-Shirt     |
  +------------+-------------+

  Result table:
  +------------+----------+------------------------------+
  | sell_date  | num_sold | products                     |
  +------------+----------+------------------------------+
  | 2020-05-30 | 3        | Basketball,Headphone,T-shirt |
  | 2020-06-01 | 2        | Bible,Pencil                 |
  | 2020-06-02 | 1        | Mask                         |
  +------------+----------+------------------------------+
```
- For `2020-05-30`, Sold items were (`Headphone`, `Basketball`, `T-shirt`), we sort them lexicographically and separate them by **comma**.
- For `2020-06-01`, Sold items were (`Pencil`, `Bible`), we sort them lexicographically and separate them by comma.
- For `2020-06-02`, Sold item is (`Mask`), we just return it.

#### Concept 
- `group_concat( [ATTRIBUTE] [ORDER BY] [SEPARATOR 'STRING'])`

```mysql
# Time:  O(nlogn)
# Space: O(n)
SELECT sell_date,
       COUNT(DISTINCT(product)) AS num_sold,        
       /**
            +------------+-------------------------------+
            | sell_date  | products                      |
            +------------+-------------------------------+
            | 2020-05-30 | Basketball, Headphone, T-Shirt|
            | 2020-06-01 | Bible, Pencil                 |
            | 2020-06-02 | Mask                          |
            +------------+-------------------------------+
       **/
       
       GROUP_CONCAT(DISTINCT product ORDER BY product ASC SEPARATOR ',') AS products
FROM Activities
/**
  +------------+-------------+
  | sell_date  | product     |
  +------------+-------------+
  | 2020-05-30 | Headphone   |
  |            | Basketball  |
  |            | T-Shirt     |
  | 2020-06-01 | Pencil      |
  |            | Bible       |
  | 2020-06-02 | Mask        |
  |            | Mask        |
  +------------+-------------+
*/
GROUP BY sell_date
ORDER BY sell_date ASC;
```

## Friendly Movies Streamed Last Month 

Write an SQL query to report the distinct titles of the kid-friendly movies streamed in `June 2020`.
- Return the result table in any order.

```
  TVProgram table:
  +--------------------+--------------+-------------+
  | program_date       | content_id   | channel     |
  +--------------------+--------------+-------------+
  | 2020-06-10 08:00   | 1            | LC-Channel  |
  | 2020-05-11 12:00   | 2            | LC-Channel  |
  | 2020-05-12 12:00   | 3            | LC-Channel  |
  | 2020-05-13 14:00   | 4            | Disney Ch   |
  | 2020-06-18 14:00   | 4            | Disney Ch   |
  | 2020-07-15 16:00   | 5            | Disney Ch   |
  +--------------------+--------------+-------------+

  Content(Pk : content_id) table:
  +------------+----------------+---------------+---------------+
  | content_id | title          | Kids_content  | content_type  |
  +------------+----------------+---------------+---------------+
  | 1          | Leetcode Movie | N             | Movies        |
  | 2          | Alg. for Kids  | Y             | Series        |
  | 3          | Database Sols  | N             | Series        |
  | 4          | Aladdin        | Y             | Movies        |
  | 5          | Cinderella     | Y             | Movies        |
  +------------+----------------+---------------+---------------+
  
  Result table:
  +--------------+
  | title        |
  +--------------+
  | Aladdin      |
  +--------------+
```

```mysql
SELECT DISTINCT c.title 
FROM Content AS c
JOIN TVProgram AS t
ON c.content_id = t.content_id
WHERE c.content_type = 'Movies'
      AND t.Kids_content = 'Y'
      AND LEFT(b.program_date,7) ='2020-06';

/**
  * JOIN The tables implicitly 
  * using FROM multiple tables
  */
SELECT DISTINCT title
FROM Content c, TVProgram tv
WHERE c.content_id = tv.content_id
        and Kids_content = 'Y'
        and content_type = 'Movies'
        and program_date between '2020-06-01' and '2020-06-30'
```

## !Customer Order Frequency 

Write an SQL query to report the `customer_id` and of customers who have spent at least `$100` in each month of June and July 2020.
- Return the result table in any order.

#### Concept
- `EQUI-JOIN THREE TABLES`, `SUM` , `INNER JOIN THREE TABLES`

```diff
  Customers
  +--------------+-----------+-------------+
  | customer_id  | name      | country     |
  +--------------+-----------+-------------+
  | 1            | Winston   | USA         |
  | 2            | Jonathan  | Peru        |
  | 3            | Moustafa  | Egypt       |
  +--------------+-----------+-------------+

  Product
  +--------------+-------------+-------------+
  | product_id   | description | price       |
  +--------------+-------------+-------------+
  | 10           | LC Phone    | 300         |
  | 20           | LC T-Shirt  | 10          |
  | 30           | LC Book     | 45          |
  | 40           | LC Keychain | 2           |
  +--------------+-------------+-------------+

  Orders
  +--------------+-------------+-------------+-------------+-----------+
  | order_id     | customer_id | product_id  | order_date  | quantity  |
  +--------------+-------------+-------------+-------------+-----------+
  | 1            | 1           | 10          | 2020-06-10  | 1         |
  | 2            | 1           | 20          | 2020-07-01  | 1         |
  | 3            | 1           | 30          | 2020-07-08  | 2         |
  | 4            | 2           | 10          | 2020-06-15  | 2         |
  | 5            | 2           | 40          | 2020-07-01  | 10        |
  | 6            | 3           | 20          | 2020-06-24  | 2         |
  | 7            | 3           | 30          | 2020-06-25  | 2         |
  | 9            | 3           | 30          | 2020-05-08  | 3         |
  +--------------+-------------+-------------+-------------+-----------+


  Result table:
  +--------------+------------+
  | customer_id  | name       |  
  +--------------+------------+
  | 1            | Winston    |
  +--------------+------------+ 
```
- Winston spent `$300 (300 * 1)` in June and `$100 ( 10 * 1 + 45 * 2)` in July 2020.
- Jonathan spent `$600 (300 * 2)` in June and `$20 ( 2 * 10)` in July 2020.
- Moustafa spent `$110 (10 * 2 + 45 * 2)` in June and $0 in July 2020.


#### ALGO
1. `EQUI-JOIN` Three tables
2. `GROUP BY` CUSTOMER ID
3. `CASE WHEN ... LIKE ... THEN ... ELSE ... END` to find the month off June and July 2020
   > Or `CASE WHEN LEFT = ... THEN ... ELSE ... END`  

```mysql
# Time:  O(n)
# Space: O(n)
SELECT a.customer_id, a.name
FROM Customers AS a
/**
+--------------+-------------+-------------+-------------+-----------+-----------+-------------+-------------+-------------+
| order_id     | customer_id | product_id  | order_date  | quantity  | name      | country     | description | price       |
+--------------+-------------+-------------+-------------+-----------+-----------+-------------+-------------+-------------+
| 1            | 1           | 10          | 2020-06-10  | 1         | Winston   | USA         | LC Phone    | 300         |
| 1            | 1           | 10          | 2020-06-10  | 1         | Winston   | USA         | LC Phone    | 300         |
| 2            | 1           | 20          | 2020-07-01  | 1         | Winston   | USA         | LC T-Shirt  | 10          |
| 3            | 1           | 30          | 2020-07-08  | 2         | Winston   | USA         | LC Book     | 45          |
| 4            | 2           | 10          | 2020-06-15  | 2         | Jonathan  | Peru        | LC Phone    | 300         |    
| 4            | 2           | 10          | 2020-06-15  | 2         | Jonathan  | Peru        | LC Phone    | 300         |
| 5            | 2           | 40          | 2020-07-01  | 10        | Jonathan  | Peru        | LC Keychain | 2           |
| 6            | 3           | 20          | 2020-06-24  | 2         | Moustafa  | Egypt       | LC T-Shirt  | 10          |
| 7            | 3           | 30          | 2020-06-25  | 2         | Moustafa  | Egypt       | LC Book     | 45          |
+--------------+-------------+-------------+-------------+-----------+-----------+-------------+-------------+-------------+
*/
INNER JOIN (SELECT *
            FROM Orders
            WHERE order_date BETWEEN "2020-06-01" 
                             AND "2020-07-31" ) AS b
ON a.customer_id = b.customer_id
INNER JOIN Product AS c
ON b.product_id = c.product_id
GROUP BY a.customer_id
-- Caculate total amount of the items that each customer bought
HAVING SUM(CASE WHEN LEFT(b.order_date, 7) = "2020-06" THEN c.price * b.quantity ELSE 0 END) >= 100
AND    SUM(CASE WHEN LEFT(b.order_date, 7) = "2020-07" THEN c.price * b.quantity ELSE 0 END) >= 100
ORDER BY NULL;

SELECT o.customer_id, c.name
FROM Customers c, Product p, Orders o
WHERE c.customer_id = o.customer_id AND p.product_id = o.product_id
GROUP BY o.customer_id
      HAVING(SUM(CASE WHEN o.order_date LIKE '2020-06%' THEN o.quantity * p.price ELSE 0 END) >= 100
             AND SUM(CASE WHEN o.order_date LIKE '2020-07%' THEN o.quantity *p.price ELSE 0 END) >= 100)

```

## Find Users With Valid E-Mails

Write an SQL query to find the users who have valid emails.
Return the result table in any order.

A valid e-mail has a prefix name and a domain where:
- The prefix name is a string that may contain letters (upper or lower case), digits, underscore `_`, period `.` and/or dash `-`.
- The prefix name must start with a letter.
- The domain is `@leetcode.com`.

#### Concept
- [`regexp`](https://www.geeksforgeeks.org/mysql-regular-expressions-regexp/)

```
  Users
  +---------+-----------+-------------------------+
  | user_id | name      | mail                    |
  +---------+-----------+-------------------------+
- | 1       | Winston   | winston@leetcode.com    |
  | 2       | Jonathan  | jonathanisgreat         |
- | 3       | Annabelle | bella-@leetcode.com     |
- | 4       | Sally     | sally.come@leetcode.com |
  | 5       | Marwan    | quarz#2020@leetcode.com |
  | 6       | David     | david69@gmail.com       |
  | 7       | Shapiro   | .shapo@leetcode.com     |
  +---------+-----------+-------------------------+

  Result table:
  +---------+-----------+-------------------------+
  | user_id | name      | mail                    |
  +---------+-----------+-------------------------+
  | 1       | Winston   | winston@leetcode.com    |
  | 3       | Annabelle | bella-@leetcode.com     |
  | 4       | Sally     | sally.come@leetcode.com |
  +---------+-----------+-------------------------+
```
- The mail of user 2 doesn't have a domain.
- The mail of user 5 has `#` sign which is not allowed.
- The mail of user 6 doesn't have leetcode domain.
- The mail of user 7 starts with a period.


```sql
SELECT * 
FROM   users AS u   
-- ^ : beginning , $ : tail 
WHERE  u.mail REGEXP '^[a-zA-Z][a-zA-Z0-9._-]*@leetcode.com$'; 
```

## Patients With a Condition 

#### Concept
- `LIKE` , `WILDCARD`

Write an SQL query to report the `patient_id`, `patient_name` all conditions of patients who have `Type I` Diabetes.   

- `Type I Diabetes` always starts with `DIAB1` prefix
- Return the result table in any order.
```
  Patients
  +------------+--------------+--------------+
  | patient_id | patient_name | conditions   |
  +------------+--------------+--------------+
  | 1          | Daniel       | YFEV COUGH   |
  | 2          | Alice        |              |
  | 3          | Bob          | DIAB100 MYOP |
  | 4          | George       | ACNE DIAB100 |
  | 5          | Alain        | DIAB201      |
  +------------+--------------+--------------+

  Result table:
  +------------+--------------+--------------+
  | patient_id | patient_name | conditions   |
  +------------+--------------+--------------+
  | 3          | Bob          | DIAB100 MYOP |
  | 4          | George       | ACNE DIAB100 | 
  +------------+--------------+--------------+
```
- Bob and George both have a condition that starts with `DIAB1`(`LIKE`).
```sql
select *
from Patients
where conditions like "%DIAB1%"
```

## !Fix Product Name Format 

#### Concept
-`SUBSTRING()` , `TRIM()` , `LOWER()`, `ORDER BY 1,2` AND `GROUP BY 1,2` 

Write an SQL query to report
1. `product_name` in lowercase(`LOWER(...)`) without leading or trailing white spaces.
2. `sale_date` in the format (`'YYYY-MM'`) VIA `LEFT(... , ...)` OR ``SUBSTRING(...)`
3. Total the number of times the product(`COUNT(...)`) was sold in this month.
4. Return the result table ordered by `product_name` in ascending order, in case of a tie order it by `sale_date` in ascending order.
```diff
  
  Sales
  +------------+------------------+--------------+
  | sale_id(PK)| product_name     | sale_date    |
  +------------+------------------+--------------+
  | 1          | LCPHONE          | 2000-01-16   |
  | 2          | LCPhone          | 2000-01-17   |
  | 3          | LcPhOnE          | 2000-02-18   |
  | 4          | LCKeyCHAiN       | 2000-02-19   |
  | 5          | LCKeyChain       | 2000-02-28   |
  | 6          | Matryoshka       | 2000-03-31   | 
  +------------+------------------+--------------+

  Result table:
  +--------------+--------------+----------+
  | product_name | sale_date    | total    |
  +--------------+--------------+----------+
  | lcphone      | 2000-01      | 2        |
  | lckeychain   | 2000-02      | 2        | 
  | lcphone      | 2000-02      | 1        | 
  | matryoshka   | 2000-03      | 1        | 
  +--------------+--------------+----------+
```
- In January , 2 LcPhones were sold, 
- In Februery, 2 LCKeychains and 1 LCPhone were sold.
- In March, 1 matryoshka was sold.
- Note that the product names are not case sensitive and may contain spaces.

```mysql
/**
  Def of GROUP BY NUM1, NUM2, ...
    SELECT account_id, open_emp_id
             ^^^^        ^^^^
              1           2

    FROM account
    GROUP BY 1, 2
    ORDER BY 1, 2
*/
  
# Time:  O(nlogn)
# Space: O(n)
SELECT LOWER(TRIM(product_name)) product_name,
       substring(sale_date, 1, 7) sale_date,
       count(sale_id) total
FROM Sales
/**

  +------------+------------------+--------------+
  | sale_id(PK)| product_name     | sale_date    |
  +------------+------------------+--------------+
  | 1          | LCPHONE          | 2000-01-16   |
  | 2          | LCPhone          | 2000-01-17   |
  | 3          | LcPhOnE          | 2000-02-18   |
  | 4          | LCKeyCHAiN       | 2000-02-19   |
  | 5          | LCKeyChain       | 2000-02-28   |
  | 6          | Matryoshka       | 2000-03-31   | 
  +------------+------------------+--------------+


  GROUP BY LOWER(TRIM(product_name)) product_name,
           SUBSTRING(sale_date, 1, 7) sale_date
  +------------------+--------------+
  | product_name     | sale_date    |
  +------------------+--------------+
  | lcphone          | 2000-01      |
  | lcphone          | 2000-01      |
  | lcphone          | 2000-02      |
  | lckeychain       | 2000-02      |
  | lckeychain       | 2000-02      |
  | Matryoshka       | 2000-03      |
  +------------------+--------------+

*/
GROUP BY 1, 2
ORDER BY 1, 2

-- SAME AS 

SELECT LOWER(TRIM(product_name)) AS product_name, 
       LEFT(sale_date, 7) AS sale_date, 
       COUNT(*) AS total FROM Sales
GROUP BY LOWER(TRIM(product_name)), LEFT(sale_date, 7)
ORDER BY product_name, sale_date;
```

## !Unique Orders and Customers Per Month 

Write an SQL query to find the number of **unique orders and the number of unique customers(`DISTINCT`)** with `invoices(Abrechnung) > $20` for each different month.
```diff
  Orders
  +----------+------------+-------------+------------+
  | order_id | order_date | customer_id | invoice    |
  +----------+------------+-------------+------------+
  | 1        | 2020-09-15 | 1           | 30         |
  | 2        | 2020-09-17 | 2           | 90         |
  | 3        | 2020-10-06 | 3           | 20         |
  | 4        | 2020-10-20 | 3           | 21         |
  | 5        | 2020-11-10 | 1           | 10         |
  | 6        | 2020-11-21 | 2           | 15         |
  | 7        | 2020-12-01 | 4           | 55         |
  | 8        | 2020-12-03 | 4           | 77         |
  | 9        | 2021-01-07 | 3           | 31         |
  | 10       | 2021-01-15 | 2           | 20         |
  +----------+------------+-------------+------------+
+ customer_id might contain duplicates

  Result table:
  +---------+-------------+----------------+
  | month   | order_count | customer_count |
  +---------+-------------+----------------+
  | 2020-09 | 2           | 2              |
  | 2020-10 | 1           | 1              |
  | 2020-12 | 2           | 1              |
  | 2021-01 | 1           | 1              |
  +---------+-------------+----------------+
```
- In September 2020(`2020-09`) we have two orders from 2 different customers with `invoices > $20`.
- In October 2020(`2020-10`) we have two orders from 1 customer, and only one of the two orders has `invoice > $20`.
- In November 2020(`2020-11`) we have two orders from 2 different customers but `invoices < $20`, so we don't include that month.
- In December 2020(`2020-12`) we have two orders from 1 customer both with `invoices > $20`.
- In January 2021(`2021-1`) we have two orders from 2 different customers, but only one of them with `invoice > $20`.

```mysql
# Time:  O(n)
# Space: O(n)
SELECT LEFT(order_date, 7) month,
       COUNT(DISTINCT order_id) order_count,
       COUNT(DISTINCT customer_id) customer_count
FROM orders
WHERE invoice > 20
GROUP BY 1
ORDER BY NULL;
```

## Warehouse Manager 

Write an SQL query to report how much cubic feet of volume does the [inventory](https://dictionary.cambridge.org/zht/%E8%A9%9E%E5%85%B8/%E8%8B%B1%E8%AA%9E-%E6%BC%A2%E8%AA%9E-%E7%B9%81%E9%AB%94/inventory) occupy in **each warehouse**.
```diff
Warehouse table:
+------------+--------------+-------------+
| name       | product_id   | units       |

+------------+--------------+-------------+
| LCHouse1   | 1            | 1           |
| LCHouse1   | 2            | 10          |
| LCHouse1   | 3            | 5           |
| LCHouse2   | 1            | 2           |
| LCHouse2   | 2            | 2           |
| LCHouse3   | 4            | 1           |
+------------+--------------+-------------+

Products table:
+------------+--------------+------------+----------+-----------+
| product_id | product_name | Width      | Length   | Height    |
+------------+--------------+------------+----------+-----------+
| 1          | LC-TV        | 5          | 50       | 40        |
| 2          | LC-KeyChain  | 5          | 5        | 5         |
| 3          | LC-Phone     | 2          | 10       | 10        |
| 4          | LC-T-Shirt   | 4          | 10       | 20        |
+------------+--------------+------------+----------+-----------+

Result table:
+----------------+------------+
| warehouse_name | volume     | 
+----------------+------------+
| LCHouse1       | 12250      | 
| LCHouse2       | 20250      |
| LCHouse3       | 800        |
+----------------+------------+
```
- LCHouse1: 1 unit of LC-TV + 10 units of LC-KeyChain + 5 units of LC-Phone.
  > Total volume: `1*10000 + 10*125  + 5*200 = 12250` cubic feet
- LCHouse2: 2 units of LC-TV + 2 units of LC-KeyChain.
  > Total volume: `2*10000 + 2*125 = 20250` cubic feet
- LCHouse3: 1 unit of LC-T-Shirt.
  > Total volume: `1*800 = 800` cubic feet.


```mysql
SELECT name AS warehouse_name, 
       SUM(units*Width*LENGTH*Height) AS volume
FROM Warehouse w
INNER JOIN Products p 
ON w.product_id = p.product_id
GROUP BY name
ORDER BY NULL;


/**  
  JOIN (SELECT product_id, 
               Width*Length*Height AS vol
       FROM Products) p
  ON w.product_id = p.product_id
 +------------+--------------+-------------+------------+
 | name       | product_id   | units       |   vol      |
 +------------+--------------+-------------+------------+
 | LCHouse1   | 1            | 1           |  5*50*40   |    
 | LCHouse1   | 2            | 10          |  5*5*5     |
 | LCHouse1   | 3            | 5           |  2*10*10   |
 | LCHouse2   | 1            | 2           |  5*50*40   |   
 | LCHouse2   | 2            | 2           |  5*5*5     |
 | LCHouse3   | 4            | 1           |  4*10*20   |
 +------------+--------------+-------------+------------+
*/
SELECT name as warehouse_name, 
       sum(units * vol) AS volume
FROM Warehouse w
JOIN (SELECT product_id, 
             Width*Length*Height AS vol
      FROM Products) p
ON w.product_id = p.product_id
GROUP BY name
```

## !Customer Who Visited but Did Not Make Any Transactions 

Write an SQL query to find 
1. the `ID`s of the users who visited (the mall) without making any transactions 
2. the number of times they made these types of visits (count of no transaction of visiters).

- tips :  `left join Transactions` 

```diff
 Visits table
  +-------------+-------------+
  | visit_i(PL) | customer_id |
  +-------------+-------------+
+ | 1           | 23          |
+ | 2           | 9           |
  | 4           | 30          |
+ | 5           | 54          |
  | 6           | 96          |
  | 7           | 54          |
  | 8           | 54          |
  +-------------+-------------+

Transactions
+----------------+----------+--------+
| transaction_id | visit_id | amount |
+----------------+----------+--------+
| 2              | 5        | 310    | -- 54
| 3              | 5        | 300    | -- 54
| 9              | 5        | 200    | -- 54
| 12             | 1        | 910    | -- 23
| 13             | 2        | 970    | -- 9
+----------------+----------+--------+
```
- Customer with `id 23` visited the mall once and made one transaction during the visit with `id = 12`.
- Customer with `id 9` visited the mall once and made one transaction during the visit with `id = 13`.
- Customer with `id 30` visited the mall once and did not make any transactions.
- Customer with `id 54` visited the mall three times. 
  > During 2 visits they did not make any transactions, and during one visit they made 3 transactions.
- Customer with `id : 96` visited the mall once and did not make any transactions.


```diff
Result table:
+-------------+----------------+
| customer_id | count_no_trans |
+-------------+----------------+
| 54          | 2              |
| 30          | 1              |
| 96          | 1              | 
+-------------+----------------+
```
As we can see, users with IDs `30` and `96` visited the mall one time without making any transactions.   
Also user id `54` visited the mall twice and did not make any transactions.

```mysql
/**
 *
   +--------+------------+----------+----------+--------+
   |visit_id| customer_id| trans_id | visit_id | amount |
   +--------+------------+----------+----------+--------+
   |1       | 23         | 12       | 1        | 910    |
   |2       | 9          | 13       | 2        | 970    |
   |4       | 30         | null     | null     | null   |
   |5       | 5          | 2        | 5        | 310    |
   |5       | 5          | 3        | 5        | 300    |
   |5       | 5          | 9        | 5        | 200    |
   |6       | 96         | null     | null     | null   |
   |7       | 54         | null     | null     | null   |
   |8       | 54         | null     | null     | null   |
   +--------+------------+----------+----------+--------+
 
   +--------+------------+----------+----------+--------+
   |visit_id| customer_id| trans_id | visit_id | amount |
   +--------+------------+----------+----------+--------+
   |4       | 30         | null     | null     | null   |
   |6       | 96         | null     | null     | null   |
   |7       | 54         | null     | null     | null   |
   |8       | 54         | null     | null     | null   |
   +--------+------------+----------+----------+--------+
 *
 */
# Time:  O(n)
# Space: O(n)
SELECT DISTINCT customer_id,
                count(customer_id) AS count_no_trans
FROM visits v
LEFT JOIN transactions t 
     ON v.visit_id = t.visit_id
WHERE transaction_id IS NULL
GROUP BY customer_id
ORDER BY NULL;
```

## Bank Account Summary II

Write an SQL query to report the `name` and `balance` of users with a balance higher than 10000(`balance > 1000`).   
- The balance of an account is equal to the sum of the amounts of all transactions involving that account.
- Return the result table in any order.

```diff
Users table:
  +------------+--------------+
  | account    | name         |
  +------------+--------------+
  | 900001     | Alice        |
  | 900002     | Bob          |
  | 900003     | Charlie      |
  +------------+--------------+

Transactions table:
  +------------+------------+------------+---------------+
  | trans_id   | account    | amount     | transacted_on |
  +------------+------------+------------+---------------+
  | 1          | 900001     |  7000      |  2020-08-01   |
  | 2          | 900001     |  7000      |  2020-09-01   |
  | 3          | 900001     | -3000      |  2020-09-02   |
  | 4          | 900002     |  1000      |  2020-09-12   |
  | 5          | 900003     |  6000      |  2020-08-07   |
  | 6          | 900003     |  6000      |  2020-09-07   |
  | 7          | 900003     | -4000      |  2020-09-11   |
  +------------+------------+------------+---------------+

Result table:
  +------------+------------+
  | name       | balance    |
  +------------+------------+
  | Alice      | 11000      |
  +------------+------------+
```

```mysql
SELECT U.name, T.sum(amount) 
FROM User U 
JOIN Transactions T
ON U.account = T.account
GROUP BY U.name
HAVING sum(amount) > 1000;

---
SELECT u.name, balance
FROM (SELECT account, 
             sum(amount) AS balance
      FROM Transactions
      GROUP BY account
      HAVING sum(amount) > 10000) As t
JOIN Users AS u
ON u.account = t.account;
```

## !Sellers With No Sales

Write an SQL query to report the names of all sellers who did not make any sales in 2020.
- Return the result table ordered by `seller_name` in **ascending** order.

```diff
Customer table:
 +----------------+---------------+
 | customer_id(PK)| customer_name |
 +----------------+---------------+
 | 101            | Alice         |
 | 102            | Bob           |
 | 103            | Charlie       |
 +----------------+---------------+

Orders table:
 +-------------+------------+--------------+-------------+-------------+
 | order_id    | sale_date  | order_cost   | customer_id | seller_id   |
 +-------------+------------+--------------+-------------+-------------+
 | 1           | 2020-03-01 | 1500         | 101         | 1           |
 | 2           | 2020-05-25 | 2400         | 102         | 2           |
 | 3           | 2019-05-25 | 800          | 101         | 3           |
 | 4           | 2020-09-13 | 1000         | 103         | 2           |
 | 5           | 2019-02-11 | 700          | 101         | 2           |
 +-------------+------------+--------------+-------------+-------------+
 
Seller table:
 +-------------+-------------+
 | seller_id   | seller_name |
 +-------------+-------------+
 | 1           | Daniel      |
 | 2           | Elizabeth   |
 | 3           | Frank       |
 +-------------+-------------+
 
Result table:
 +-------------+
 | seller_name |
 +-------------+
 | Frank       |
 +-------------+
```
- Daniel made 1 sale in March 2020.
- Elizabeth made 2 sales in 2020 and 1 sale in 2019.
- Frank made 1 sale in 2019 but no sales in 2020.

```mysql
-- Time:  O(nlogm)
-- Space: O(n + m)
SELECT seller_name
FROM seller s
WHERE NOT EXISTS(
    /**
      
     +------------+--------------+-------------+------------+--------------+-------------+-------------+
     |customer_id | customer_name| order_id    | sale_date  | order_cost   | customer_id | seller_id   |
     +------------+--------------+-------------+------------+--------------+---------------------------+
     | 101        | Alice        |  1          | 2020-03-01 | 1500         | 101         |           1 |
     | 102        | Bob          |  2          | 2020-05-25 | 2400         | 102         |           2 |  
     | 103        | Charlie      |  4          | 2020-09-13 | 1000         | 103         |           2 |  
     +------------+--------------+-------------+------------+--------------+-------------+-------------+
      
    */
    SELECT 1
    FROM orders o
    WHERE s.seller_id = o.seller_id 
          AND o.sale_date >= '2020-01-01')
ORDER BY 1;
```

## All Valid Triplets That Can Represent a Country

Write an SQL query to find all the possible triplets representing the country under the given constraints.
- `student_id` and `student_name` from different School can not be the same 
```diff
SchoolA table:
+------------+--------------+
| student_id | student_name |
+------------+--------------+
| 1          | Alice        |
| 2          | Bob          |
+------------+--------------+

SchoolB table:
+------------+--------------+
| student_id | student_name |
+------------+--------------+
| 3          | Tom          |
+------------+--------------+

SchoolC table:
+------------+--------------+
| student_id | student_name |
+------------+--------------+
| 3          | Tom          |
| 2          | Jerry        |
| 10         | Alice        |
+------------+--------------+

Result table:
+----------+----------+----------+
| member_A | member_B | member_C |
+----------+----------+----------+
| Alice    | Tom      | Jerry    |
| Bob      | Tom      | Alice    |
+----------+----------+----------+
```
- `(Alice, Tom, Tom)`
  -  Rejected because `member_B` and `member_C` have the same name and the same ID.
- `(Alice, Tom, Jerry)` --> Valid triplet.
- `(Alice, Tom, Alice)` 
  - Rejected because `member_A` and `member_C` have the same name.
- `(Bob, Tom, Tom)` 
  - Rejected because `member_B` and `member_C` have the same name and the same ID.
- `(Bob, Tom, Jerry)` 
  - Rejected because `member_A` and `member_C` have the same ID.
- `(Bob, Tom, Alice)` --> Valid triplet.

```sql
SELECT a.student_name AS 'member_A',
       b.student_name AS 'member_B',
       c.student_name AS 'member_C'
FROM SchoolA AS a
JOIN SchoolB AS b
ON a.student_id <> b.student_id
   AND a.student_name <> b.student_name
JOIN SchoolC AS c
ON a.student_id <> c.student_id
   AND b.student_id <> c.student_id
   AND a.student_name <> c.student_name
   AND b.student_name <> c.student_name;

# Time:  O(n^3)
# Space: O(n^3)
SELECT a.student_name AS member_A,
       b.student_name AS member_B,
       c.student_name AS member_c
FROM schoola a
INNER JOIN schoolb b ON (a.student_id != b.student_id
                         AND a.student_name != b.student_name)
INNER JOIN schoolc c ON (a.student_id != c.student_id
                         AND a.student_name != c.student_name)
AND (b.student_id != c.student_id
     AND b.student_name != c.student_name);
```
