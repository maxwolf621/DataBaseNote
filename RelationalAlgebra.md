# Relational Algebra/Calculus
###### tags: `DataBase`

[TOC]

Two Concepts for Storing and retrieving data (of query language) 
1. Relational Algebra 
2. Relational Calculus

## Relationship of SQL instructor and Relational Algebra
![](https://i.imgur.com/J63JAJp.png)


### Operations of relational Algebra
![](https://i.imgur.com/NGpS6jH.png)

> Complete Set
>: 1. SELECT(σ)
>: 2. Projection(π)
>: 3. Rename (ρ)
>: 4. Union operation (υ)
>: 5. Set Difference (-)



## RESTRICT `σ`

- `σ` : the condition

For example  
![](https://i.imgur.com/BOvT5uf.png)  

![](https://i.imgur.com/ytw1zi0.png)  

It can be presented  
$$σ_{height<170 \ AND \ weight < 60 (學生資料表)}$$

```mysql
FROM Student
WHERE Height < 179 AND Weight < 60
```


## Project π

To Create A New Table (projection) with specified attributes from the old one

> A new Table with Atrribute A and B from table R  
> ![](https://i.imgur.com/7dG9aBv.png)  

> Relation Algebra `πA(R)`   
> A : Attribute from table R   

Priority of selection and projection
- It depends on situation

## Union
Merge two tables remove duplicate data 
![](https://i.imgur.com/QK08qqb.png)

> Relation Algebra : $R \cup S$
> : ![](https://i.imgur.com/otdaoWf.png)


## Cartesian Product

It's a set of n attributes from table R merging with m attributes from table S  
![](https://i.imgur.com/4jC4AD6.png)  
> SO we get A merged Table with $n+m = 6$ attributes  
> AND $X \times\ Y = 9$ data  

> Relation Algebra : $R \times\ S$  

```sql
SELECT *
FROM 學生表 , 課程表
/* or */
SELECT *
FROM 學生表 cross join 課程表
```
![](https://i.imgur.com/eJKvDpu.png)  
![](https://i.imgur.com/hQ4LOY1.png)  

## Difference   

Remove the common part of R and S   

![](https://i.imgur.com/lVlsJRj.png)  

For Example
```c
A = {1,2,4,5}
B = {3,4,5,6}
A AND B = {4,5}
so...
A - B ={1,2}
```



> - $R - S% : get the part belonging to R AND no S  
>> ![](https://i.imgur.com/tPm9yMo.png)  
> - $S - R% : get the part belonging to S AND no R  



## JOIN  (WICHTIG)

**Join operation is essentially a Cartesian product followed by a selection criterion.**

Relational Algebra : $R ⨝pS$    

> ![](https://i.imgur.com/9v3HGUy.png)  
> II : inner join  
> I : left outer join    
> III : right outer join    

Inner Join (Condition Join)

![](https://i.imgur.com/IglA41f.png)

An inner join, only those tuples that satisfy the matching criteria are included, while the rest are excluded.  
- Theta join
- EQUI join
- Natural join

An Outer join   
- Left Outer Join
- Right Outer Join
- Full Outer Join

## Inner Join

### Natural Join

```mysql
NATURAL JOIN B
/** is equal **/
From A INNER JOIN B
ON A.c = B.c 
```

![](https://i.imgur.com/Y2dDe14.png)

### Theta Join
Merging two table with operation for theta join
$=,＜,≦,＞,≧,≠$

> Def 
> : The general case of JOIN operation is called a Theta join. It is denoted by symbol θ.

```sql=
(AXB) where A.X θ B.Y 
/* X : attribute of table A */
/* Y : attribute of table B */
```

<font color=red>Caution</font> : Difference from Natural Join, There will be duplicate attributes

### EQUI-JOIN
merging table with Attribute from A $=$ Attribute from B

> Def
> : When a theta join uses only equivalence condition, it becomes a equi join.

<font color=red>Caution</font> : there may have duplicate attributes
```sql=
FROM R,S WHERE (R.c == S.c)
```
For example

![](https://i.imgur.com/qO74Xdb.png)
![](https://i.imgur.com/WdmmXj7.png)


## OUTER JOIN
In an outer join, along with tuples that satisfy the matching criteria, we also include first (left outer join), second (right outer join) or all tuples that do not match the criteria.

**If tuples are not satisfied with the matching criteria , they will be set as NULL by default**

Why we use it?
because we dont want to miss any of information as merging the two different attribute tables

```sql=
SELECT *
FROM TableA [RIGHT|LEFT] [OUTER] [JOIN] TableB
ON TableA.PK = TableB.FK
```

## Left Outter Join
![](https://i.imgur.com/iaiKGHH.png)

```sql=
SELECT *
FROM 老師資料表 AS A LEFT OUTER JOIN 課程資料表 AS B
ON A.老師編號 = B.老師編號
```

if 老師資料表 cant reference the matching records => set NULL by default

![image](https://user-images.githubusercontent.com/68631186/111078928-bff07d00-8532-11eb-9d77-aa6443b9e8f6.png)

if we want to get which teachers dont have a lecture 
```sql=
SELECT *
FROM 老師資料表 AS A LEFT OUTER JOIN 課程資料表 AS B
ON A.老師編號 = B.老師編號
WHERE B.老師編號 IS NULL
```

## Right Outter Join

## Interaction 
Section belonging to both R and S

![](https://i.imgur.com/gJiMj1e.png)


> Relational Algebra\
> : $R \cap S=R-(R-S）$
> ![](https://i.imgur.com/71LOY0u.png)



```sql=
SELECT *
FROM 老師資料表 AS A RIGHT OUTER JOIN 課程資料表 AS B
ON A.老師編號 = B.老師編號
ORDER BY B.課程代碼
```

In B.老師編號 we get only two teachers which are T0001 and T0002

so the 老師編號 from A will be set NULL except T0001 and T0002

![image](https://user-images.githubusercontent.com/68631186/111079068-52911c00-8533-11eb-8d60-2a2b160d41df.png)


## Division 

Remove table R's data that are same as data in table S  

![](https://i.imgur.com/h5XOOMM.png)



Relational Algebra : $R\div S

Using nested query to implement division

for example
```sql=
/* main */
SELECT A.ID, Name
FROM Student AS A, StudentCourse AS B
WHERE A.ID = B.ID 
AND B.CourseID = 
( /* Sub to get specified CourseId from C */
 SELECT C.CourseID FROM Course AS C
 WHERE CourseName = 'Data Base'
)
```

Algo of division
1. taking out whole row in table R that is responding to table S
2. and then remove these data related to table S
> For Example 
> : ![](https://i.imgur.com/n7jefxR.png)
> 1. 
> : ![](https://i.imgur.com/Fuy0DGy.png)
> 2.
> : ![](https://i.imgur.com/UUdCMoR.png)


![](https://i.imgur.com/1BvYwR2.png)

![](https://i.imgur.com/2FnLbOi.png)
![](https://i.imgur.com/i29LNom.png)
![](https://i.imgur.com/IIo3vKt.png)
![](https://i.imgur.com/tSO31sY.png)
![](https://i.imgur.com/Aybv42G.png)
![](https://i.imgur.com/lkUsJHD.png)

This is how we do using nested query concept to implement division

![image](https://user-images.githubusercontent.com/68631186/111079672-e49a2400-8535-11eb-88c0-6b81629ccbc6.png)

Q: To list all students' optional Courses
```sql=
/* We need student to get what optional Courses they chose */

SLEECT 課名
/* Informations for Course is in the table 課程檔 */ 
FROM 課程檔 AS C
WHERE NOT EXISTS
(
  SELECT *
  /* DIVIDED */
  FROM 學生檔 AS A
  WHERE NOT EXISTS
  (
    SELECT *
    /* DIVIDEND */
    FROM 選課擋 AS B
    /* CONDITION */
    WHERE C.課號 = B.課號 AND A.學號 = B.學號
  )
)
```


## REPLACEMENT WITH OPERATIONS

### Jion with selection and product

![](https://i.imgur.com/71c0IOb.png)

### interaction replace with difference
![](https://i.imgur.com/i1zhXEw.png)


### Division (HARD)
![](https://i.imgur.com/Twjwka1.png)
