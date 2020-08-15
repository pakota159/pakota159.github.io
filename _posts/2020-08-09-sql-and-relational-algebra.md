---
layout: post
subtitle: SQL is based on relational algebra
tags: [sql, data]
comments: true
bigimg: /img/sql/bg.jpg
---

When study about SQL, a lot of us start with some statement like *Select*, *FROM*, *WHERE*, but turns out SQL is more than just that. I mean the principle of the query language is based on relational algebra and when I learn about it, I find it way more interesting to understand SQL and how the query works.

So let's discover some of the relational algebra and find out if it makes you learn deeper about SQL.

**Note**: this article is for people who have basic knowledge of SQL and querying database. If you don't have it, you may need to read about basic SQL at first.
___

We start with the **Relational Model**. It's used by all major database systems. It's kind of a concept used to build the world of relational database.

In this model, `Database = set of named relations (or tables)`

Each relation has a set of named **attributes** (or **columns**)

For examle, we have a relation **Student** as below  

| ID        | Name           | Class  |
| ------------- |:-------------:| -----:|
| ... | ... | ... |

The table **Student** has 3 *attributes*: id, name and class.

___

Each **tuple** (or **row**) has a value for each *attributes*

| ID        | Name           | Class  |
| ------------- |:-------------:| -----:|
| 001 | Cuong | A1 |
| 002 | Phong | A2 |

___

**Schema** (of database) is structural description of relations in database.

**Instance** (of database) is actual contents at given point in time. It means the *entire data stored in database* at a particular moment of time.

___

**NULL** is special value for 'unknown' or 'undefined'

**Key** is attribute whose value is unique in each tuple (row). Sometimes, this unique key can be the combination of multiple attributes.

___

Create table in a database by SQL

```sql
CREATE TABLE table_name(
	column1 datatype,
	column2 datatype,
	...
);
```

Some common datatypes (depends on type of DBMS):
- CHAR(size 0-255)
- VARCHAR(size 0-255)
- INT()
- BIGINT()
- FLOAT()
- DOUBLE()

For the *Student* relation, we can write

```sql
CREATE TABLE Student (
	id integer PRIMARY KEY,
	name varchar(255),
	class varchar(255)
);
```

___

**Steps in creating and using a relational database**

1. Design Schema: create using DDl (data definition language)
2. Load initial data (if any)
3. Execute queries and modifications using DML (data manipulation language)

*Queries will return relations*

___

**Query language**:
- Relational Algebra: formal language
- **SQL**: implemented Relational Algebra

___

**Relational Algebra**:

As we said above, Queries on set of relations produces relation as a result.

Imagine we have a booking system, with **User** who select **Product** and then make a **Booking**

The *Schema* of each relation will be something like below (*a very simple version*):  
(Convention: use _ to seperate word)
- *User*: user_id (PK), username, age, city
- *Product*: product_id (PK), product_name, price
- *Booking*: booking_id (PK), user_id, product_id, status

___
**Select** operator ($$\sigma$$): picks certain rows

We want student with *age > 20*, then the formation will be:

$$\sigma_{age > 20} User$$

The operator above will return a relation that contains all rows that has value of age is larger than 20.

If we want to select with multiple conditions, like `age > 20` and `city = 'Hanoi'` we use caret

$$
\sigma_{age > 20 \wedge city = 'Hanoi' } User
$$

___
**Project** operator ($$\Pi$$): picks certain columns.

We only want the columns (attributes) *username* and *age*

$$
\Pi_{username, age} User
$$

Now, we can combine 2 operators above like we want user with *age > 20* and only return column *username, age*

$$
\Pi_{username, age}(\sigma_{age > 20}) User
$$

___
**Cross-product**: combine 2 relations

Imagine we have *User* and *Product* table as below

*User*  

| user_id | username | age | city |
| ------- |:--------:| ---:| ----:|
| 1 | cuong | 20 | Hanoi |
| 2 | phong | 25 | HCM |

*Product*  

| product_id | product_name | price |
| ------- |:--------:| ---:|
| 1 | mac | 2000 |
| 2 | iphone | 1000 |

Then $$User X Product$$ will return a new relation which has 4 rows (2 * 2 rows), and 7 columns (4 + 3 attributes)

| user_id | username | age | city | product_id | product_name | price |
| ------- |:--------:| ---:| ----:| ------- |:--------:| ---:|
| 1 | cuong | 20 | Hanoi | 1 | mac | 2000 |
| 2 | phong | 25 | HCM | 1 | mac | 2000 |
| 1 | cuong | 20 | Hanoi | 2 | iphone | 1000 |
| 2 | phong | 25 | HCM | 2 | iphone | 1000 |

Basically, each row of the User table, will match will all rows of the Product table, and vice versa.

___
Now if user decide to select and buy some products, we will have bookings.

*Booking*

| id | product_id | user_id | status |
| ------- |:--------:| ---:| ---:|
| 1 | 1 | 1 | Done |
| 2 | 2 | 2 | Processing |
| 3 | 2 | 1 | Done |

If we do **Natural Join** between `Booking` and `User`, like $$Booking \|X\| User$$, we will merge the same name column (user_id here) and remove rows that has different value of same attribute (user_id), keep row that user_id values are the same.

First, we do cross product normally

*Booking \|X\| User*

| id | product_id | user_id | status | user_id | username | age | city |
| ------- |:--------:| ---:| ---:| ------- |:--------:| ---:| ----:|
| 1 | 1 | **1** | Done | **1** | cuong | 20 | Hanoi |
| 2 | 2 | 2 | Processing | 1 | cuong | 20 | Hanoi |
| 3 | 2 | **1** | Done | **1** | cuong | 20 | Hanoi |
| 1 | 1 | 1 | Done | 2 | phong | 25 | HCM |
| 2 | 2 | **2** | Processing | **2** | phong | 25 | HCM |
| 3 | 2 | 1 | Done | 2 | phong | 25 | HCM |

As we see above, we have 3 bookings and 2 users, that's why we have 6 rows. But, user_id from Booking and user_id from User actually reflect same thing (identify User), so we merge these 2 columns.

We keep row that has same user_id (bold), because that's the actual **match** between 2 table. We want to know **user_id 1** make which booking, and we identify that by match the user_id between 2 tables.

Final table is below (column **user_id** is merged)

| id | product_id | user_id | status  | username | age | city |
| ------- |:--------:| ---:| ------- |:--------:| ---:| ----:|
| 1 | 1 | **1** | Done | cuong | 20 | Hanoi |
| 3 | 2 | **1** | Done | cuong | 20 | Hanoi |
| 2 | 2 | **2** | Processing | phong | 25 | HCM |

Of course, after natural join 2 tables, we can apply Select and Project to get value we want

$$
\Pi_{id, product\_id, username}(\sigma_{status = 'Done'} (Booking \|X\| User))
$$

| id | product_id | status | username |
| ------- |:--------:| ---:| ---:|
| 1 | 1 | Done | cuong |
| 3 | 2 | Done | cuong |

___
**Theta join** is cross-product with condition.

Image we have a age table like this which defines the min age for user of each city. 
*Age* table

| city | min_age |
| ------- |:--------:|
| Hanoi | 20 |
| HCM | 35 |

So, we want to find users from Hanoi that satisty the condition `age >= min_age`, we will have to do cross-product

| user_id | username | age | city | **city** | **min_age** |
| ------- |:--------:| ---:| ----:| ---:| ----:|
| 1 | cuong | 20 | Hanoi | **Hanoi** | **20** |
| 2 | phong | 25 | HCM | **Hanoi** | **20** |
| 1 | cuong | 20 | Hanoi | **HCM** | **35** |
| 2 | phong | 25 | HCM | **HCM** | **35** |

So if we want the city and age match the condition, we have to eliminate tuple that don't have same city, and age < min_age.

| user_id | username | age | city | **city** | **min_age** |
| ------- |:--------:| ---:| ----:| ---:| ----:|
| 1 | cuong | 20 | Hanoi | **Hanoi** | **20** |

___
**Union** operator:
2 tables with same columns (attributes)

*Car*

| id | name | brand |
| ------- |:--------:| ---:|
| 1 | civic | honda | 
| 2 | glc | mercedes | 

*Bike*

| id | name | brand |
| ------- |:--------:| ---:|
| 1 | air blade | honda | 
| 2 | glc | mercedes |

So the union of 2 tables will be

$$Car \cup Bike$$

| id | name | brand |
| ------- |:--------:| ---:|
| 1 | civic | honda | 
| 2 | glc | mercedes | 
| 1 | air blade | honda | 

**Note:** the primary key (id) seem like duplicate in the union table, that's because they key now is combination of (id, name, brand)

___
**Intersection**
Return tuples which are identical in both tables.

$$Car \cap Bike$$

| id | name | brand |
| ------- |:--------:| ---:|
| 2 | glc | mercedes |

___
**Difference**
Return tuples which are in first table but not in second

$$Car - Bike$$ (row in Car but not in Bike)

| id | name | brand |
| ------- |:--------:| ---:|
| 1 | civic | honda |

___
If we want to do those 3 operators but the name of attributes are different, we can rename it.

$$
\rho_{id, name, brand \rightarrow id, name, new_brand}(Car)
$$

___
**SQL**: based on relational algebra, or you can say it's implemented relational algebra in most of database systems.

**DDL**: (Data definition language) commands that is used to create table, drop table.

**DML**: (Data manipulation language) commands that is used to select, insert, delete, update table.

___
Basic SELECT Statement

```sql
Select A1, A2, ..., An
From R1, R2, ..., Rn
Where condition
```

The order is **From** which identify the relations, then **Where** to validate rows that satisfy the condition, finally **Select** means project columns we want.

In the language of Relational algebra, we have

$$
\Pi_{A1, A2, ..., An} (\sigma_{condition}(R1 X R2 X ... X Rn))
$$

Note: **From** statement means we do cross-product if we add multiple relations.

___
**Subqueries** is a **SQL query nested inside a larger query**

A subquery may occur in:
- SELECT clause
- FROM clause
- WHERE clause

Example: if subquery in WHERE clause, we want to the condition in WHERE clause become some kind of SQL query itself.

```sql
SELECT *
FROM Users
WHERE user_id in (
	SELECT user_id
	FROM Booking
)
```

As the example above, we execute a query before execute the WHERE clause, we get the column user_id from Booking table, then make user_id in that column as a condition for bigger query.

