# Exercises - Sqoop import

1. Select the first 10 rows of the table `employees` of the database `employees`.

```bash
sqoop eval \
--connect jdbc:mysql://database/employees \
--username root \
--password secret \
--query "select * from employees limit 10"
# output:
# ---------------------------------------------------------------------------------
# | emp_no      | birth_date | first_name     | last_name        | gender | hire_date  | 
# ---------------------------------------------------------------------------------
# | 10001       | 1953-09-02 | Georgi         | Facello          | M | 1986-06-26 | 
# | 10002       | 1964-06-02 | Bezalel        | Simmel           | F | 1985-11-21 | 
# | 10003       | 1959-12-03 | Parto          | Bamford          | M | 1986-08-28 | 
# | 10004       | 1954-05-01 | Chirstian      | Koblick          | M | 1986-12-01 | 
# | 10005       | 1955-01-21 | Kyoichi        | Maliniak         | M | 1989-09-12 | 
# | 10006       | 1953-04-20 | Anneke         | Preusig          | F | 1989-06-02 | 
# | 10007       | 1957-05-23 | Tzvetan        | Zielinski        | F | 1989-02-10 | 
# | 10008       | 1958-02-19 | Saniya         | Kalloufi         | M | 1994-09-15 | 
# | 10009       | 1952-04-19 | Sumant         | Peac             | F | 1985-02-18 | 
# | 10010       | 1963-06-01 | Duangkaew      | Piveteau         | F | 1989-08-24 | 
# ---------------------------------------------------------------------------------
```

2. Import the table `employees`, on the warehouse `/user/hive/warehouse/db_test_a`.

```bash
sqoop import \
--table employees \
--connect jdbc:mysql://database/employees \
--username root \
--password secret \
--warehouse-dir /user/hive/warehouse/db_test_a
```

3. Import all the male employees, on the warehouse `/user/hive/warehouse/db_test_b`.

```bash
sqoop import \
--table employees \
--connect jdbc:mysql://database/employees \
--username root \
--password secret \
--warehouse-dir /user/hive/warehouse/db_test_b \
--where "gender = 'M'"
```

4. Import the first and last name of the employees, separating fields by tabulation, on the warehouse `/user/hive/warehouse/db_test_c`.

```bash
sqoop import \
--table employees \
--connect jdbc:mysql://database/employees \
--username root \
--password secret \
--columns "first_name,last_name" \
--warehouse-dir /user/hive/warehouse/db_test_c \
--fields-terminated-by '\t'
```

5. Import the first and last name of the employees, separating lines by '` : `', on the warehouse `/user/hive/warehouse/db_test_c`.

```bash
sqoop import \
--table employees \
--connect jdbc:mysql://database/employees \
--username root \
--password secret \
--columns "first_name,last_name" \
--warehouse-dir /user/hive/warehouse/db_test_c \
--lines-terminated-by ' : ' \
--append
```
