# VIEWS

Ansichten auf Deutsch 

###### tags: `DataBase`


**A view is a virtual table** based on the result-set of an SQL statement.
The fields in a view are fields from one or more real tables in the database.


You can add SQL statements and functions to a view and present the data as if the data were coming from one single table as the following 
![](https://i.imgur.com/DeRrWon.png)


Good Sides
> **Using view is good for hiding the information to keep it inaccessible**
> Most of the views can only do 
> Make records (information in database) more readable for the users 
> For programmer it also makes Structure of Database maintainable 


Bad Sides
> Efficiency sucks


General Syntax
```sql=
CREATE VIEW View_Name 
AS
SELECT column1, column2, ...
FROM Base_Table
WHERE condition;
```



## Create View with multiple base tables 

```sql=
CREATE VIEW STUDENTGRADES
AS
SELECT Name,CourseName,Grade
FROM Student AS s, CoursesSelection AS cs , Courses AS c
WHERE s.ID = cs.ID AND c.CourseID = cs.CourseID
```