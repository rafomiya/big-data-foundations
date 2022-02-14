# Exercises - Creating Optimized Tables

1. Use the database `<nome>`.

```sql
use rafael;
```

2. Select the first 10 rows of the table `pop`.

```sql
select * from pop limit 10;
```

3. Create the table `pop_parquet` with parquet format to read the data from the `pop` table.

```sql
create table pop_parquet
(
  zip_code int,
  total_population int,
  median_age float,
  total_males int,
  total_females int,
  total_households int,
  average_household_size float
)
stored as parquet;
```

4. Insert the data of the table `pop` on `pop_parquet`.

```sql
insert into pop_parquet
select * from pop;
```

5. Count the rows of the table `pop_parquet`.

```sql
select
  count(*) as count_pop_parquet
from pop_parquet
limit 1;
```

6. Select the first 10 rows of the table `pop_parquet`.

```sql
select * from pop_parquet limit 10;
```

7. Create the table `pop_parquet_snappy` on the format parquet with Snappy compression to read the data of the table `pop`.

```sql
create table pop_parquet_snappy
(
  zip_code int,
  total_population int,
  median_age float,
  total_males int,
  total_females int,
  total_households int,
  average_household_size float
)
stored as parquet
tblproperties('parquet.compress'='SNAPPY');
```

8. Insert the data of the table `pop` on the table `pop_parquet_snappy`.

```sql
insert into pop_parquet_snappy
select * from pop;
```

9. Count the rows of the table `pop_parquet_snappy`.

```sql
select
  count(*) as count_pop_parquet_snappy
from pop_parquet_snappy
limit 1;
```

10. Select the first 10 rows of the table `pop_parquet_snappy`.

```sql
select * from pop_parquet_snappy limit 10;
```

11. Compare the tables `pop`, `pop_parquet` and `pop_parquet_snappy` on HDFS.

```bash
hdfs dfs -ls -R /user/hive/warehouse/rafael.db/
# output:
# drwxrwxr-x   - root supergroup          0 2022-02-12 23:01 /user/hive/warehouse/rafael.db/pop
# -rwxrwxr-x   3 root supergroup      12183 2022-02-12 23:01 /user/hive/warehouse/rafael.db/pop/populacaoLA.csv
# drwxrwxr-x   - root supergroup          0 2022-02-14 18:44 /user/hive/warehouse/rafael.db/pop_parquet
# -rwxrwxr-x   3 root supergroup       9477 2022-02-14 18:44 /user/hive/warehouse/rafael.db/pop_parquet/000000_0
# drwxrwxr-x   - root supergroup          0 2022-02-14 18:46 /user/hive/warehouse/rafael.db/pop_parquet_snappy
# -rwxrwxr-x   3 root supergroup       9477 2022-02-14 18:46 /user/hive/warehouse/rafael.db/pop_parquet_snappy/000000_0
```
