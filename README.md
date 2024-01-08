Exercise Description:
Suppose we have two tables: Employees and Departments. The Employees table contains information about company employees, and the Departments table contains details about different departments within the company. You are tasked with creating these tables and establishing a relationship between them using primary and foreign keys.

1. Create the Departments table- colums -> department id,department name(should not be null),location
2.  Create the Employees table: colum: employee id , employee name(should not be null) and one foreign key that is department id from department table
3. Populate the Departments table with some sample data:
4. Populate the Employees table with sample data:

   Exercise Tasks:
1.Add a new department called 'IT' in the Departments table and assign an employee (e.g., EmployeeID 106, 'David Wilson') to this department in the Employees table.

2.Update the location of the 'HR' department from 'New York' to 'Chicago'.

3.Delete the employee named 'Michael Brown' from the Employees table.

Expected Results:
Task 1 should successfully add the 'IT' department and assign an employee to it.
Task 2 should update the location of the 'HR' department.
Task 3 should remove the employee 'Michael Brown' from the table.
You can practice these tasks and SQL statements against the created tables to understand how primary keys (PKs) and foreign keys (FKs) work together to establish relationships between tables in a database.




mysql> CREATE DATABASE pf_exercise1;
Query OK, 1 row affected (0,02 sec)

mysql> USE pf_exercise1;
Database changed

mysql> CREATE TABLE Department (departmentId INT NOT NULL PRIMARY KEY AUTO_INCREMENT, departmentName VARCHAR(50) NOT NULL, location VARCHAR(100));
Query OK, 0 rows affected (0,03 sec)

mysql> CREATE TABLE Employee (employeeId INT NOT NULL PRIMARY KEY AUTO_INCREMENT, employeeName VARCHAR(100) NOT NULL, departmentKEY INT);
Query OK, 0 rows affected (0,04 sec)

mysql> ALTER TABLE Employee ADD FOREIGN KEY(departmentKEY) REFERENCES Department(departmentId);
Query OK, 0 rows affected (0,06 sec)
Records: 0  Duplicates: 0  Warnings: 0

mysql> DESCRIBE Employee;
+---------------+--------------+------+-----+---------+----------------+
| Field         | Type         | Null | Key | Default | Extra          |
+---------------+--------------+------+-----+---------+----------------+
| employeeId    | int          | NO   | PRI | NULL    | auto_increment |
| employeeName  | varchar(100) | NO   |     | NULL    |                |
| departmentKEY | int          | YES  | MUL | NULL    |                |
+---------------+--------------+------+-----+---------+----------------+
3 rows in set (0,00 sec)

mysql> INSERT INTO Department (departmentName, location)
    -> VALUES ('IT', 'New York'), ('IT', 'Los Angeles'), ('HR', 'NEW YORK'), ('HR', 'Boston'), ('Marketing', 'Los Angeles');
Query OK, 5 rows affected (0,01 sec)
Records: 5  Duplicates: 0  Warnings: 0

mysql> SELECT * FROM Department;
+--------------+----------------+-------------+
| departmentId | departmentName | location    |
+--------------+----------------+-------------+
|            1 | IT             | New York    |
|            2 | IT             | Los Angeles |
|            3 | HR             | NEW YORK    |
|            4 | HR             | Boston      |
|            5 | Marketing      | Los Angeles |
+--------------+----------------+-------------+
5 rows in set (0,01 sec)

mysql> INSERT INTO Employee (employeeName, departmentKEY)
    -> VALUES ('David Wilson', 1), ('Pluto Burlau', 2), ('Vanessa Versace', 3), ('Baba Papa', 4), ('Dirk Bogade', 2), ('Silke Smith', 5), ('Ben Meyer', 1);
Query OK, 7 rows affected (0,01 sec)
Records: 7  Duplicates: 0  Warnings: 0

mysql> SELECT * FROM Employee;
+------------+-----------------+---------------+
| employeeId | employeeName    | departmentKEY |
+------------+-----------------+---------------+
|          1 | David Wilson    |             1 |
|          2 | Pluto Burlau    |             2 |
|          3 | Vanessa Versace |             3 |
|          4 | Baba Papa       |             4 |
|          5 | Dirk Bogade     |             2 |
|          6 | Silke Smith     |             5 |
|          7 | Ben Meyer       |             1 |
+------------+-----------------+---------------+
7 rows in set (0,00 sec)

mysql> UPDATE Department SET location = 'Chicago' WHERE departmentId = 3;
Query OK, 1 row affected (0,02 sec)
Rows matched: 1  Changed: 1  Warnings: 0

mysql> SELECT * FROM Department;
+--------------+----------------+-------------+
| departmentId | departmentName | location    |
+--------------+----------------+-------------+
|            1 | IT             | New York    |
|            2 | IT             | Los Angeles |
|            3 | HR             | Chicago     |
|            4 | HR             | Boston      |
|            5 | Marketing      | Los Angeles |
+--------------+----------------+-------------+
5 rows in set (0,00 sec)

mysql> INSERT INTO Employee (employeeName, departmentKEY)
    -> VALUES ('Michael Brown', 3), ('Hanna Bobby', 2);
Query OK, 2 rows affected (0,00 sec)
Records: 2  Duplicates: 0  Warnings: 0

mysql> SELECT * FROM Employee;
+------------+-----------------+---------------+
| employeeId | employeeName    | departmentKEY |
+------------+-----------------+---------------+
|          1 | David Wilson    |             1 |
|          2 | Pluto Burlau    |             2 |
|          3 | Vanessa Versace |             3 |
|          4 | Baba Papa       |             4 |
|          5 | Dirk Bogade     |             2 |
|          6 | Silke Smith     |             5 |
|          7 | Ben Meyer       |             1 |
|          8 | Michael Brown   |             3 |
|          9 | Hanna Bobby     |             2 |
+------------+-----------------+---------------+
9 rows in set (0,00 sec)

mysql> DELETE FROM Employee WHERE employeeId = 8;
Query OK, 1 row affected (0,01 sec)

mysql> SELECT * FROM Employee;
+------------+-----------------+---------------+
| employeeId | employeeName    | departmentKEY |
+------------+-----------------+---------------+
|          1 | David Wilson    |             1 |
|          2 | Pluto Burlau    |             2 |
|          3 | Vanessa Versace |             3 |
|          4 | Baba Papa       |             4 |
|          5 | Dirk Bogade     |             2 |
|          6 | Silke Smith     |             5 |
|          7 | Ben Meyer       |             1 |
|          9 | Hanna Bobby     |             2 |
+------------+-----------------+---------------+
8 rows in set (0,00 sec)

mysql> SELECT * FROM Employee LEFT JOIN Department ON Employee.employeeId = Department.departmentId;
+------------+-----------------+---------------+--------------+----------------+-------------+
| employeeId | employeeName    | departmentKEY | departmentId | departmentName | location    |
+------------+-----------------+---------------+--------------+----------------+-------------+
|          1 | David Wilson    |             1 |            1 | IT             | New York    |
|          2 | Pluto Burlau    |             2 |            2 | IT             | Los Angeles |
|          3 | Vanessa Versace |             3 |            3 | HR             | Chicago     |
|          4 | Baba Papa       |             4 |            4 | HR             | Boston      |
|          5 | Dirk Bogade     |             2 |            5 | Marketing      | Los Angeles |
|          6 | Silke Smith     |             5 |         NULL | NULL           | NULL        |
|          7 | Ben Meyer       |             1 |         NULL | NULL           | NULL        |
|          9 | Hanna Bobby     |             2 |         NULL | NULL           | NULL        |
+------------+-----------------+---------------+--------------+----------------+-------------+
8 rows in set (0,00 sec)
