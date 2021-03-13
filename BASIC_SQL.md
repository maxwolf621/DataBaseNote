# Basic SQL
###### tags: `DataBase`

DDL
> To Define Structure of Database, variable's datatype and length

DML
> To modify (manipulate) the data

DCL
> To give authority of the users 


![](https://i.imgur.com/v6rAbRL.png)




## DDL

![](https://i.imgur.com/SGIfZsA.png)


### For DataBase 

To Create A Database
```sql=
/* Syntax*/
create Database [IF NOT EXISTS] Name_Of_DataBase
/* FOR EXAMPLE */
Create Database Courses
```

To Alter A Database
```sql=
Alter Database Name_Of_Database
CHARACTER SET Encode_Name
COLLATE Collation Name
/* FOR EXAMPLE */
Alter Database Courses
CHARACTER SET utf8
```


### For Table
#### To Create A Table
```sql=
Create table tableX
(Attribute{Datatype|Domain}[NULL|NOTNULL][DEFAULT VALUE][RESTRICTION])

/* Cant not be NULL */
RRIMARY KEY(ATTRIBUTE)
/* Can be NULL */
UNIQUE(ATTRIBUTE)
/* Define A attribute in talbeX as FK*/
FOREIGN KEY(ATTRIBUTE) REFERENCE Name_of_Table(ATTRIBUTE) [ON DELETE option] [ON UPDATE option]
```


For example
![](https://i.imgur.com/VfZCdk4.png)

```sql=
/* table student */
CREATE TABLE Student
(
    ID CHAR(8),
    Name CHAR(4) NOT NULL
    Mobile CHAR(12),
    Address CHAR(20),
    PRIMARY KEY(ID),
    UNIQUE(Mobile),
)

/* table Courses */
CREATE TABLE Courses
(
    CourseID CHAR(8),
    CourseName CHAR(20) NOT NULL
    /* Set the default value of  3*/
    Piont INT DEFAULT 3,
    Option CHAR(2),
    PRIMARY KEY(CourseID)
)

/* table CoursesSelection */
CREATE TABLE CoursesSelection
{
    ID CHAR(8),
    CourseName CHAR(5),
    Grade INT NOT NULL,
    /* DATE OF SELECTING COURSE */
    DateSlecteCourse DATETIME DEFAULT CURRENT_TIMESTAMP,
    PRIMARY KEY
    FOREIGN KEY(ID) REFERENCE Student(ID)
    ON UPDATE CASCADE
    ON DELETE CASCADE,
    FOREIGN KEY(CourseID) REFERERRR
}
```
> With ON UPDATE CASCADE and ON DELETE CASCADE means
> when data in table Student have been modified (update or delete ..etc) then corresponding data in table CourseSelection will also be modified


:::info 
Order of creating tables
Student , Courses first
CourseSelection second
:::


#### To Alter Table

with `ALTER TABLE Name_Of_TableX`, we can
```sql=
ADD Name_OF_Attribute {dataType | Domain} [NULL|NOT NULL]
MODIFY Name_OF_Attribute{dataType | Domain} [NULL | NOT NULL]
DROP Name_OF_Attribute
```

For example
add new attribute to table Student
```sql=
ALTER TABLE student 
ADD Email CHAR(50)
ADD Sex CHAR(1) Default 'M'
``` 
modify attribute in table Student
```sql=
ALTER TABLE student
/* Address from CHAR(20) TO CHAR(50) NOT NULL */
MODIFY Address CHAR(50) NOT NULL
```
Drop the Attribute in table Student
```sql=
ALTER TABLE student
DROP Email
```

:::danger
When executing the `DROP` 
DO MAKE SURE THERE ARE NO REFERENCE EXISTING (SAME CONCEPT AS CONSTRUCTOR IN CPP or JAVA)
So the order of DROP is 
CourseSelection  first,
Courses, Student after.
:::

## DML

BASIC COMMAND 
> - INSERT
> - UPDATE
> - DELETE
> - SELECT


Insert values
```sql=
INSERT INTO Name_OF_Table<attribute>
VALUES(<attribute> | <SELECT>)
/* for example */
INSERT INTO Student
VALUES('S001','John','1234567','JAPAN','M');
```

Insert data in the table a to other table b
![](https://i.imgur.com/qEUimbZ.png)

```sql=
INSERT INTO Student
/* Select ALL from oldstudent */
SELECT * FROM OldStudent
```

Update value
```sql=
UPDATE Name_OF_Table
SET {AttributeY=valueY, AttributeX=valueX , .... , AttributeN=valueN }
[WHERE<CONDITION>]
/* for example */
UPDATE Stuent
SET Mobile='1234567'
WHERE Mobile IS NULL and ID='S002'
```

Update multiple records at same time
```sql=
UPDATE Courses
SET Point='4', Option='N'
WHERE CourseName='DataStructure'
```

Update grade
```sql=
UPDATE CourseSelection
SET Grade = Grade*1.2
WHERE Grade<70
```



Delete A student
```sql=
DELETE FROM `Student`
WHERE Name='John'
```


### SELECT
![](https://i.imgur.com/N70G6sQ.png)



## DCL

Grant who has right to access database
```sql=
GRANT {INSERT|UPDATE|DELETE|SELECT} ON NameOfDataBase
TO NameOfTheUser
/* for example */
GRANT SELECT,INSERT ON GUESTS
TO Jian,Domi /*User Jian,Domi can modify data Using SELECT,INSERT only */
GRANT SELECT ON GUESTS
TO PUBLIC /* EVERYONE can modify data Using SELECTG */
```

Revoke(Take back) the authority to access the database from User
```sql=
REVOKE {INSERT|UPDATE|DELETE|SELECT} ON NameOfDataBase
FROM NameOfTheUser
/* for example */
REVOKE INSERT ON GUESTS
FROM Jian 
/* USER Jian cant not modify data with INSERT */
```
