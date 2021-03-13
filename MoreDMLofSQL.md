# More DML of SQL
###### tags: `DataBase`
[TOC]

## SELECT
```sql=
SELECT Attribute1, Attribute2 , ... AttributeN
/* or select All Attributes */
SELECT * 
FROM Table1, Table2, ... , TableN
WHERE CODITION
GROUP BY Attribute1, ... , AttributeN
ORDER BY Attribute1, ... , AttributeN
LIMIT 
```



### AS

> Alias
```sql=
use ex_db;
SELECT CP AS CourseName,point
FROM Courses
```

### Comparison Operation with WHERE
| OP | FUNCTION  | EXAMPLE      |
| -  |  -------  | -------------|
| =  |  Equal    | Grade = 60   |
| <> | Not Equal | Grade <>60   |
| <  | Less Than | Grade < 60   |
| <= | Less Equal| Grade <=60   |
| >  | Large Than| Grade > 60   |
| >= | LargeEqual| Grade >=60   |

```sql=
use ex_db;
SELECT ID,CourseID,Grade
FROM CourseSelection
WHERE Grade < 60
/* 
it would show up a table with 
attributes ID, CourseID and Grade 
corresponding with the condition 
*/
```

### Logical Comparison with WHERE 

For example
```sql=
/* As literally */
WHERE Grade >= 60 AND CourseID='C005'
WHERE CourseID='C004' OR CourseID='C005'
WHERE NOT Grade >=60
```


### IS NULL

For Example
```sas=
use ex_db;
SELECT ID,Name.Grade
FRom CourseSelection
WHERE Grade IS NULL
```
> IS CAN NOT REPLACE WITH =


### Wildcard operation with LIKE, IN, BETWEEN ... IN ...

Wildcard Characters in MS Access
| Symbol | Description| Example |
| -----  |  ----------| ------  |
|* |	Represents zero or more characters	|bl* finds bl, black, blue, and blob
|? |    Represents a single character	    | h?t finds hot, hat, and hit
|[]|	Represents any single character within the brackets |h[oa]t finds hot and hat, but not hit
|! |   Represents any character not in the brackets	|h[!oa]t finds hit, but not hot and hat
|-| Represents a range of characters|c[a-b]t finds cat and cbt
|#|	Represents any single numeric character	|2#5 finds 205, 215, 225, 235, 245, 255, 265, 275, 285, and 295



Wildcard Characters in SQL Server
| Symbol | Description| Example |
| -----  |  ----------| ------  |
| % |	Represents zero or more characters|	bl% finds bl, or bl... |
| _ |   Represents a single character	  | h_t finds hot, hat, and hit .. 
|[] |	Represents any single character within the brackets	| h[oa]t finds hot and hat, but not hit 
|^	|   Represents any character not in the brackets | h[^oa]t finds hit, but not hot and hat
|-  |  Represents a range of characters | 	c[a-b]t finds cat and cbt



With LIKE
```sql=
WHERE Name LIKE 'J_HN'
WHERE Name LIKE '%Y%'
```
With IN
> Def
> : The IN operator allows you to specify multiple values in a WHERE clause.
> : ==The IN operator is a shorthand for multiple OR conditions.==
```sql=
SELECT column_name(s)
FROM table_name
WHERE column_name IN (value1, value2, ...);
/* or */
WHERE column_name=value1 or column_name=value2 or .... ;
/* or using select */
SELECT column_name(s)
FROM table_name
WHERE column_name IN (SELECT STATEMENT);
```

With BETWEEN ... AND ...
```sql=
use ex_db;
SELECT Name, ID, Grade
FROM CourseSelection 
WHERE Grade BETWEEN 60 AND 90 
/* or */
WHERE Grade >= 60 AND Grade <=90
```


## AVG(),SUM(),MIN(),MAX(),COUNT()

[MINandMAX](https://www.w3schools.com/sql/sql_min_max.asp)
[SUM,COUNT,AVG](https://www.w3schools.com/sql/sql_count_avg_sum.asp)

## (sort) ORDER BY ASC OR DESC


ASC (default)
> Ascending

DESC
> Descending

```sql=
ORDER BY ID ASC, Grade DSEC
```
![](https://i.imgur.com/tYINXRX.png)


## LIMIT

select a limited number of records

```sql=
SELECT column_name(s)
FROM table_name
WHERE condition
LIMIT number;
```


```sql=
SELECT 學號,課號,成績
FROM 選課表
WHERE 課號='C005'
ORDER BY 成績 DSEC
LIMIT 2 /* ONLY SHOW UP 2 RECRODS */
```
![](https://i.imgur.com/Ig4xCFO.png)


## GROUP BY
The GROUP BY statement is often used with aggregate functions (COUNT(), MAX(), MIN(), SUM(), AVG()) to group the result-set by one or more columns.

```sql=
SELECT column_name(s)
FROM table_name
WHERE condition
GROUP BY column_name(s)
ORDER BY column_name(s)
```
![](https://i.imgur.com/U1EJCc1.png)


lists numb
```sql=
SELECT COUNT(CustomerID), Country
FROM Customers
GROUP BY Country;
```

## HAVING 

The HAVING clause was added to SQL because the WHERE keyword cannot be used with aggregate functions.

```sql=
SELECT column_name(s)
FROM table_name
WHERE condition
GROUP BY column_name(s)
HAVING condition
ORDER BY column_name(s);
```

Now we can list the number of customers in each country. Only include countries with more than 5 customers
```sql=
SELECT COUNT(CustomerID), Country
FROM Customers
GROUP BY Country
HAVING COUNT(CustomerID) > 5
ORDER BY COUNT(CustomerID) DESC;
```

## SELECT DISTINCT

Forbid showing up duplicate records
It can't work with COUNT(*) , MIN(), MAX()

[EXAMPLE](https://www.w3schools.com/sql/sql_distinct.asp)