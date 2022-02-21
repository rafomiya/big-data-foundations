# Exercises - Import to Hive and Export

1. Import the MySQL table `employees.titles` to the directory `/user/aluno/rafael/data`, with 1 mapper.

```bash
sqoop import \
--connect jdbc:mysql://database/employees \
--username root \
--password secret \
--table titles \
-m 1 \
--warehouse-dir /user/aluno/rafael/data
```

2. Import the MySQL table `employees.titles` to a Hive table on the database `rafael`, with 1 mapper.

```bash
sqoop import \
--connect jdbc:mysql://database/employees \
--username root \
--password secret \
--table titles \
-m 1 \
--hive-import \
--create-hive-table \
--hive-table rafael.titles
```

3. Select the first 10 rows of the table `rafael.titles` on Hive.

```sql
use rafael;
select * from titles limit 10;
-- output:
-- +----------------+------------------+-------------------+-----------------+
-- | titles.emp_no  |   titles.title   | titles.from_date  | titles.to_date  |
-- +----------------+------------------+-------------------+-----------------+
-- | 10001          | Senior Engineer  | 1986-06-26        | 9999-01-01      |
-- | 10002          | Staff            | 1996-08-03        | 9999-01-01      |
-- | 10003          | Senior Engineer  | 1995-12-03        | 9999-01-01      |
-- | 10004          | Engineer         | 1986-12-01        | 1995-12-01      |
-- | 10004          | Senior Engineer  | 1995-12-01        | 9999-01-01      |
-- | 10005          | Senior Staff     | 1996-09-12        | 9999-01-01      |
-- | 10005          | Staff            | 1989-09-12        | 1996-09-12      |
-- | 10006          | Senior Engineer  | 1990-08-05        | 9999-01-01      |
-- | 10007          | Senior Staff     | 1996-02-11        | 9999-01-01      |
-- | 10007          | Staff            | 1989-02-10        | 1996-02-11      |
-- +----------------+------------------+-------------------+-----------------+
```

4. Delete the rows of the MySQL table `employees.titles` and verify if they were deleted, using Sqoop.

```bash
sqoop eval \
--connect jdbc:mysql://database/employees \
--username root \
--password secret \
--query "delete from titles"
# output:
# 22/02/20 16:57:04 INFO tool.EvalSqlTool: 443308 row(s) updated.
```

5. Export the data from the directory `/user/hive/warehouse/rafael.db/data/titles` to the MySQL table `employees.titles`.

```bash
sqoop export \
--connect jdbc:mysql://database/employees \
--username root \
--password secret \
--export-dir /user/aluno/rafael/data/titles \
--table titles
```

6. Select the first 10 rows of the table `employees.titles` of MySQL.

```bash
sqoop eval \
--connect jdbc:mysql://database/employees \
--username root \
--password secret \
--query "select * from titles limit 10"
# output:
# -- +-------------+----------------------+------------+------------+
# -- | emp_no      |   title              | from_date  | to_date    |
# -- +-------------+----------------------+------------+------------+
# -- | 10001       | Senior Engineer      | 1986-06-26 | 9999-01-01 |
# -- | 10002       | Staff                | 1996-08-03 | 9999-01-01 |
# -- | 10003       | Senior Engineer      | 1995-12-03 | 9999-01-01 |
# -- | 10004       | Engineer             | 1986-12-01 | 1995-12-01 |
# -- | 10004       | Senior Engineer      | 1995-12-01 | 9999-01-01 |
# -- | 10005       | Senior Staff         | 1996-09-12 | 9999-01-01 |
# -- | 10005       | Staff                | 1989-09-12 | 1996-09-12 |
# -- | 10006       | Senior Engineer      | 1990-08-05 | 9999-01-01 |
# -- | 10007       | Senior Staff         | 1996-02-11 | 9999-01-01 |
# -- | 10007       | Staff                | 1989-02-10 | 1996-02-11 |
# -- +-------------+----------------------+------------+------------+
```