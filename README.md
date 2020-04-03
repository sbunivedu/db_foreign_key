# Foreign Key Constraints
You can setup the sample data with [this script](script.txt).

You can query the structure of a table using the SQL statement (in SQLite):
```sql
SELECT sql
FROM sqlite_master
WHERE name = 'Categories';
```
and get
```sql
CREATE TABLE Categories (
  id int unsigned PRIMARY KEY,
  name varchar(255)
)
```


You can check database content as follows:
```
SELECT * FROM Categories;
+----+------+
| id | name |
+----+------+
|  1 | red  |
|  2 | blue |
+----+------+

SELECT * FROM Products;
+----+---------+
| id | name    |
+----+---------+
|  1 | mittens |
|  2 | boots   |
+----+---------+

SELECT * FROM Categories_Products;
+-------------+------------+
| category_id | product_id |
+-------------+------------+
|           1 |          1 |
|           1 |          2 |
|           2 |          1 |
|           2 |          2 |
+-------------+------------+
```
Use the data to answer the following questions.
* What categories are the "mittens" product in?
* What products are in the "blue" category?

Experiment with foreign key constraints
* Delete  a primary key
```sql
DELETE FROM Categories WHERE (id = 2);
SELECT * FROM Categories;
SELECT * FROM Categories_Products;
```
* Update a primary key
```sql
UPDATE Categories SET id=3 where id=1;
SELECT * FROM Categories;
SELECT * FROM Categories_Products;
```
* Insert a new foreign key
```sql
INSERT INTO Categories_Products (category_id, product_id) values (4, 1);
```
* Update a foreign key
```sql
UPDATE Categories_Products SET category_id=4 where category_id=3;
```
