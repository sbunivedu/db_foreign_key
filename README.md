# Foreign Key Constraints

This example demonstrates the use of foreign key constraints on the following database.

* Categories (id, name)
* Products(id, name)
* Categories_Products(category_id, product_id)

The sample data can be found in [this script](script.txt).

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
DELETE FROM Categories WHERE id = 2;
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

The following example demonstrates where the `SET NULL` policy makes more sense than `CASCADE` for a foreign key constraint on the following database:
* Professors(prof_id, name, department_id)
* Departments(department_id, name, chair_id)

The sample data can be found in [this script](script1.txt).

What would happen if we delete a professor?
```sql
DELETE FROM Professors WHERE prof_id = 1;
```

The department remains, but its chair `(chair_id)` should become `NULL`. This makes sense — the department still exists, it just doesn’t currently have a chair.

What happens if we change the policy to `ON DELETE CASCADE`?

Comparison and Summary
| Scenario               | Foreign Key Action                           | What Happens When a Professor Is Deleted? |
| ---------------------- | -------------------------------------------- | ----------------------------------------- |
| **ON DELETE SET NULL** | Keeps the department, sets `chair_id = NULL` | Department remains but has no chair       |
| **ON DELETE CASCADE**  | Deletes the department                       | Department is removed completely          |

* Use `ON DELETE SET NULL` when the relationship is optional — e.g., a department may exist without a chair.
* Use `ON DELETE CASCADE` when the child’s existence depends on the parent — e.g., deleting a customer also deletes their orders.