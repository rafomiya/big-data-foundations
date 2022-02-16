# Exercises - Sqoop Commands

1. Show all databases.

```bash
sqoop list-databases \
--connect jdbc:mysql://database/ \
--username root \
--password secret
# output:
# information_schema
# employees
# hue
# mysql
# performance_schema
# sakila
# sys
```

2. Show all tables from the database `employees`.

```bash
sqoop list-tables \
--connect jdbc:mysql://database/employees \
--username root \
--password secret
# output:
# current_dept_emp
# departments
# dept_emp
# dept_emp_latest_date
# dept_manager
# employees
# employees_2
# titles
```

3. Insert the values `('d010', 'BI')` on the table `departments` from the database `employees`.

```bash
sqoop eval \
--connect jdbc:mysql://database/employees \
--username root \
--password secret \
--query "insert into departments values ('d010', 'BI')"
# output:
# 22/02/16 03:29:45 INFO tool.EvalSqlTool: 1 row(s) updated.
```

4. Select all the rows from the table `departments`.

```bash
sqoop eval \
--connect jdbc:mysql://database/employees \
--username root \
--password secret \
--query "select * from departments"
# output:
# -------------------------------
# | dept_no | dept_name            | 
# -------------------------------
# | d010 | BI                   | 
# | d009 | Customer Service     | 
# | d005 | Development          | 
# | d002 | Finance              | 
# | d003 | Human Resources      | 
# | d001 | Marketing            | 
# | d004 | Production           | 
# | d006 | Quality Management   | 
# | d008 | Research             | 
# | d007 | Sales                | 
# -------------------------------
```

5. Create the table `benefits(cod int(2)  AUTO_INCREMENT PRIMARY KEY, name varchar(30))` on the database `employees`.

```bash
sqoop eval \
--connect jdbc:mysql://database/employees \
--username root \
--password secret \
--query "create table benefits(cod int(2) auto_increment primary key, name varchar(30))"
```

6. Insert the values `(null,'food vale')` on the table `benefits`.

```bash
sqoop eval \
--connect jdbc:mysql://database/employees \
--username root \
--password secret \
--query "insert into benefits values (null, 'food vale')"
# output:
# 22/02/16 03:37:44 INFO tool.EvalSqlTool: 1 row(s) updated.
```

7. Select all the rows from the table `benefits`.

```bash
sqoop eval \
--connect jdbc:mysql://database/employees \
--username root \
--password secret \
--query "select * from benefits"
# output:
# -----------------------------
# | cod | name                 | 
# -----------------------------
# | 1  | food vale            | 
# -----------------------------
```
