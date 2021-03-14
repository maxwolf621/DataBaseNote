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
CREATE TABLE `Student` (
  `ID` char(8) NOT NULL,
  `Name` char(20) DEFAULT NULL,
  `Mobile` char(12) DEFAULT NULL,
  `Address` char(20) DEFAULT NULL,
  PRIMARY KEY (`ID`),
  UNIQUE KEY `Mobile` (`Mobile`)
) ENGINE=InnoDB DEFAULT CHARSET=latin1

/* table Courses */
CREATE TABLE `Course` (
  `CourseID` char(8) NOT NULL,
  `CourseName` char(20) DEFAULT NULL,
  `Piont` int(11) DEFAULT 3,
  `Option` char(2) DEFAULT NULL,
  PRIMARY KEY (`CourseID`)
) ENGINE=InnoDB DEFAULT CHARSET=latin1

/* table CoursesSelection */
CREATE TABLE `StudentCourse` (
  `ID` char(8) NOT NULL,
  `CourseID` char(8) NOT NULL,
  `Grade` int(11) NOT NULL,
  PRIMARY KEY (`ID`,`CourseID`),
  KEY `CourseID` (`CourseID`),
  CONSTRAINT `StudentCourse_ibfk_1` FOREIGN KEY (`ID`) REFERENCES `Student` (`ID`) ON DELETE CASCADE ON UPDATE CASCADE,
  CONSTRAINT `StudentCourse_ibfk_2` FOREIGN KEY (`CourseID`) REFERENCES `Course` (`CourseID`)
) ENGINE=InnoDB DEFAULT CHARSET=latin1
```
> With ON UPDATE CASCADE and ON DELETE CASCADE means
> when data in table Student have been modified (update or delete ..etc) then corresponding data in table CourseSelection will also be modified

:::info 
Order of creating tables
Student , Courses first
CourseSelection second
:::


#### To Alter Table

with `ALTER TABLE Name_Of_TableX`, we can do 
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
> DO MAKE SURE THERE ARE NO REFERENCE EXISTING (SAME CONCEPT AS CONSTRUCTOR IN CPP or JAVA)

So the order of DROP is 
1. CourseSelection  first,
2. Courses, Student after.
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
VALUES
('001','John','1111','USA'),
('002','Mai','2222','JAPAN')
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
UPDATE Student
SET Mobile='1111'
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
