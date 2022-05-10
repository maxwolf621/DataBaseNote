# DataBaseNote
### Index

- [Linux Command](LinuxSql.sh)
- [Basic SQL](BASIC_SQL.md)
- **[MORE DML](MoreDMLofSQL.md)**
- [ER model](ER_model.md)
- **[Normalization](Normalization.md)**
- **[RelationAlgebra](RelationalAlgebra.md)**
- [VIEW](VIEW.md)
- **[Question](DataBaseLeetCode/solution.md)**

## Difference btw NoSQL and Relational Database
[GeekforGeek](https://www.geeksforgeeks.org/difference-between-relational-database-and-nosql/)

### Relational Database

**Data is store in the form of row that is in the form of tuple.** 
Relational Database contains numbers of TABLE and DATA 

### NoSQL  
NoSQL Database stands for a non-SQL database. 
NoSQL database doesn’t use table to store the data like relational database.  
It is used for storing and fetching the data in database and generally used to store the large amount of data.

### Transaction 

- [Data Base Transaction](https://stackoverflow.com/questions/974596/what-is-a-database-transaction)    
**A transaction is A UNIT of work that you want to treat as A WHOLE.**    
It has to either happen in FULL or NOT AT ALL.     

**Transactions are there to ensure, that no matter what happens, the data you work with will be in SENSIBLE STATE**. For example 
```vim
# operation 1
accountA -= 100;
accountB += 100;

# operation 2
accountB += 100;
accountA -= 100;
```
- If something goes wrong between the first and the second operation in the pair you have a problem - either 100 bucks have disappeared, or they have appeared out of nowhere.

**A transaction is a mechanism that allows you to mark A GROUP OF OPERATIONS and execute them in such a way that either they all execute (`commit`), or the system state will be as if they have not started to execute at all (ROLLBACK).**
```vim
---------- beginTransaction ------------------------   +
accountB += 100;                                       +  A GROUP OF OPERATONS
accountA -= 100;                                       +  A UNIT OF WORK
---------- commitTransaction -----------------------   +
```
- It guarantees that there will NOT be a situation where money is withdrawn from one account, but not deposited to another.
