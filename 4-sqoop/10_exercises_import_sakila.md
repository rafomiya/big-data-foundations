# Exercises - Import Sakila Database

Do this part using the MySQL CLI.

1. Create the table `cp_rental_append`, containing a copy of the table `rental`, with the fields `rental_id` and `rental_date`.

```mysql
create table cp_rental_append as (select rental_id, rental_date from rental);
```

2. Create the table `cp_rental_id` and `cp_rental_date`, containing copies of the table `cp_rental_append`.

```mysql
create table cp_rental_id as (select * from cp_rental_append);
create table cp_rental_date as (select * from cp_rental_append);
```

Do this part using Sqoop. Import on the warehouse `/user/hive/warehouse/db_test3`.

3. Import  the tables `cp_rental_append`, `cp_rental_id` e `cp_rental_date` with 1 mapper.

```bash
# cp_rental_append
sqoop import \
--connect jdbc:mysql://database/sakila \
--username root \
--password secret \
--table cp_rental_append \
--warehouse-dir /user/hive/warehouse/db_test3 \
--split-by rental_id

# cp_rental_id
sqoop import \
--connect jdbc:mysql://database/sakila \
--username root \
--password secret \
--table cp_rental_id \
--warehouse-dir /user/hive/warehouse/db_test3 \
--split-by rental_id

# cp_rental_date
sqoop import \
--connect jdbc:mysql://database/sakila \
--username root \
--password secret \
--table cp_rental_date \
--warehouse-dir /user/hive/warehouse/db_test3 \
--split-by rental_id
```

Do this part using MySQL CLI.

4. Execute the SQL script `/db-sql/sakila/insert_rental.sql` on the `database` container.

```bash
cd /db-sql/sakila
mysql -psecret < insert_rental.sql
# output:
# rental_id       rental_date
# 15458   2006-02-14 15:16:03
# 13421   2006-02-14 15:16:03
# 15542   2006-02-14 15:16:03
# 15294   2006-02-14 15:16:03
# 13428   2006-02-14 15:16:03
# 12988   2006-02-14 15:16:03
# 12786   2006-02-14 15:16:03
# 13952   2006-02-14 15:16:03
# 12574   2006-02-14 15:16:03
# 14915   2006-02-14 15:16:03
# rental_id       rental_date
# 15458   2006-02-14 15:16:03
# 13421   2006-02-14 15:16:03
# 15542   2006-02-14 15:16:03
# 15294   2006-02-14 15:16:03
# 13428   2006-02-14 15:16:03
# 12988   2006-02-14 15:16:03
# 12786   2006-02-14 15:16:03
# 13952   2006-02-14 15:16:03
# 12574   2006-02-14 15:16:03
# 14915   2006-02-14 15:16:03
```

Do this part using Sqoop. Import on the warehouse `/user/hive/warehouse/db_test3`.

5. Update the table `cp_rental_append` on the HDFS, appending the new files.

```bash
sqoop import \
--connect jdbc:mysql://database/sakila \
--username root \
--password secret \
--table cp_rental_append \
--append \
--warehouse-dir /user/hive/warehouse/db_test3 \
-m 1
```

6. Update the table `cp_rental_id` on the `HDFS`, based on the last `rental_id` row, appending only the new rows.

```bash
sqoop import \
--connect jdbc:mysql://database/sakila \
--username root \
--password secret \
--table cp_rental_id \
--incremental append \
--check-column rental_id \
--last-value 16049 \
--warehouse-dir /user/hive/warehouse/db_test3 \
-m 1
```

7. Update the table `cp_rental_date` on the HDFS, based on the last `rental_date`, updating the rows after this date.

```bash
sqoop import \
--connect jdbc:mysql://database/sakila \
--username root \
--password secret \
--table cp_rental_date \
--incremental lastmodified \
--merge-key rental_id \
--check-column rental_date \
--last-value '2005-08-23 22:50:12.0' \
--warehouse-dir /user/hive/warehouse/db_test3 \
-m 1
```