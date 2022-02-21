# Exercises - Optimize Import

## Using MySQL

1. Create the table `cp_titles_date`, containing a copy of the table `titles` with the fields `title` and `to_date`.

```mysql
create table cp_titles_date as (select title, to_date from titles);
-- output:
-- Query OK, 443308 rows affected (1.76 sec)
```

2. Select the first 15 rows of the table `cp_titles_date`.

```mysql
select * from cp_titles_date limit 15;
-- output:
-- -------------------------------------
-- | title                | to_date    |
-- -------------------------------------
-- | Senior Engineer      | 9999-01-01 |
-- | Staff                | 9999-01-01 |
-- | Senior Engineer      | 9999-01-01 |
-- | Engineer             | 1995-12-01 |
-- | Senior Engineer      | 9999-01-01 |
-- | Senior Staff         | 9999-01-01 |
-- | Staff                | 1996-09-12 |
-- | Senior Engineer      | 9999-01-01 |
-- | Senior Staff         | 9999-01-01 |
-- | Staff                | 1996-02-11 |
-- | Assistant Engineer   | 2000-07-31 |
-- | Assistant Engineer   | 1990-02-18 |
-- | Engineer             | 1995-02-18 |
-- | Senior Engineer      | 9999-01-01 |
-- | Engineer             | 9999-01-01 |
-- -------------------------------------
```

3. Update the rows with the field `to_date` to `null` on the table `cp_titles_date` when the `title` is `'Staff'`.

```mysql
update cp_titles_date
set to_date = null
where title = 'Staff';
-- output:
-- Query OK, 107391 rows affected (1.21 sec)
```

## Using Sqoop

Import on the warehouse `/user/hive/warehouse/db_test_<questionno>`.

4. Import the table `titles` with 8 mappers on the format `parquet`.

```bash
sqoop import \
--table titles \
--connect jdbc:mysql://database/employees \
--username root \
--password secret \
--as-parquetfile \
-m 8 \
--warehouse-dir /user/hive/warehouse/db_test_4
```

5. Import the table `titles` with 8 mappers on the format `parquet` and `snappy` compression.

```bash
sqoop import \
--table titles \
--connect jdbc:mysql://database/employees \
--username root \
--password secret \
--as-parquetfile \
-m 8 \
--warehouse-dir /user/hive/warehouse/db_test_5 \
--compress \
--compression-codec Snappy
```

6. Import the table `cp_titles_date` with 4 mappers (error).

```bash
sqoop import \
--table cp_titles_date \
--connect jdbc:mysql://database/employees \
--username root \
--password secret \
-m 4 \
--warehouse-dir /user/hive/warehouse/db_test_6
# output:
# 22/02/19 18:06:55 ERROR tool.ImportTool: Import failed: No primary key could be found for table cp_titles_date. Please specify one with --split-by or perform a sequential import with '-m 1'.
```

- Import the table `cp_titles_date` with 4 mappers divided by the field `title` on the warehouse `/user/hive/warehouse/db_test2_title`.

```bash
sqoop import \
-Dorg.apache.sqoop.splitter.allow_text_splitter=true \
--table cp_titles_date \
--connect jdbc:mysql://database/employees \
--username root \
--password secret \
-m 4 \
--split-by title \
--warehouse-dir /user/hive/warehouse/db_test2_title
```

- Import the table `cp_titles_date` with 4 mappers divided by the field `to_date` on  the warehouse `/user/hive/warehouse/db_test2_date`.

```bash
sqoop import \
--table cp_titles_date \
--connect jdbc:mysql://database/employees \
--username root \
--password secret \
-m 4 \
--split-by to_date \
--warehouse-dir /user/hive/warehouse/db_test2_date
```

What is the difference between the null rows on these importations?

​	When using the `split-by` flag, rows with the specified field set to `null` won't be imported. Since the field `title` is a `not null` field, all the rows will be imported.
