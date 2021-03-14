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



## RESTRICT σ

σ : the condition


For example
![](https://i.imgur.com/BOvT5uf.png)

![](https://i.imgur.com/ytw1zi0.png)

It can be presented
$$σ_{height<170 \ AND \ weight < 60 (學生資料表)}$$

```sql=
FROM Student
WHERE Height < 179 AND Weight < 60
```


## Project π
>Def
> : Create A New Table (projection) with specified attributes from the old one
> A new Table with Atrribute A and B from table R
> ![](https://i.imgur.com/7dG9aBv.png)


> Relation Algebra `πA(R)` 
> A : Attribute from table R



### Priority of selection and projection
It depends on situation


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

#### SQL

```sql=
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



## JOIN

Join operation is essentially a Cartesian product followed by a selection criterion.

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

Outer join:
- Left Outer Join
- Right Outer Join
- Full Outer Join

## Inner Join

### Natural Join
```sql
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

if tuples are not satisfied with the matching criteria , they will be set as NULL by default 

and do we use it?
because we dont want to miss any of information as merging the two different attribute tables

```sql=
SELECT *
FROM TableA [RIGHT|LEFT] [OUTER] [JOIN] TableB
ON TableA.PK = TableB.FK
```

## Left Out Join

![](https://i.imgur.com/iaiKGHH.png)

```sql=

```


## Interaction 
Section belonging to both R and S
![](https://i.imgur.com/gJiMj1e.png)


> Relational Algebra\
> : $R \cap S=R-(R-S）$
> ![](https://i.imgur.com/71LOY0u.png)



## Division 

Remove table R's data that are same as data in table S  
![](https://i.imgur.com/h5XOOMM.png)

Relational Algebra : $R\div S$

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


## REPLACEMENT WITH OPERATIONS

### Jion with selection and product

![](https://i.imgur.com/71c0IOb.png)

### interaction replace with difference
![](https://i.imgur.com/i1zhXEw.png)


### Division (HARD)
![](https://i.imgur.com/Twjwka1.png)