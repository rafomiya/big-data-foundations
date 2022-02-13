# Exercises - Inserting data

1. View the description of the table `pop`.

```sql
desc pop;
-- output:
-- +-------------------------+------------+----------+
-- |        col_name         | data_type  | comment  |
-- +-------------------------+------------+----------+
-- | zip_code                | int        |          |
-- | total_population        | int        |          |
-- | median_age              | float      |          |
-- | total_males             | int        |          |
-- | total_females           | int        |          |
-- | total_households        | int        |          |
-- | average_household_size  | float      |          |
-- +-------------------------+------------+----------+
```

2. Select the first 10 rows of the table `pop`.

```sql
select * from pop limit 10;
-- output:
-- +--------+----------------+----------+-----------+-------------+----------------+----------------------+
-- |zip_code|total_population|median_age|total_males|total_females|total_households|average_household_size|
-- +--------+----------------+----------+-----------+-------------+----------------+----------------------+
-- +--------+----------------+----------+-----------+-------------+----------------+----------------------+
```

3. Load the HDFS file `/user/aluno/rafael/data/populacao/populacaoLA.csv` to the Hive table `pop`.

```sql
load data inpath '/user/aluno/rafael/data/populacao/populacaoLA.csv' into table pop;
```

4. Select the first 10 rows of the table `pop` again.

```sql
select * from pop limit 10;
-- output:
-- +--------+----------------+----------+-----------+-------------+-=--------------+----------------------+
-- |zip_code|total_population|median_age|total_males|total_females|total_households|average_household_size|
-- +--------+----------------+----------+-----------+-------------+----------------+----------------------+
-- | 91371  | 1              | 73.5     | 0         | 1           | 1              | 1.0                  |
-- | 90001  | 57110          | 26.6     | 28468     | 28642       | 12971          | 4.4                  |
-- | 90002  | 51223          | 25.5     | 24876     | 26347       | 11731          | 4.36                 |
-- | 90003  | 66266          | 26.3     | 32631     | 33635       | 15642          | 4.22                 |
-- | 90004  | 62180          | 34.8     | 31302     | 30878       | 22547          | 2.73                 |
-- | 90005  | 37681          | 33.9     | 19299     | 18382       | 15044          | 2.5                  |
-- | 90006  | 59185          | 32.4     | 30254     | 28931       | 18617          | 3.13                 |
-- | 90007  | 40920          | 24.0     | 20915     | 20005       | 11944          | 3.0                  |
-- | 90008  | 32327          | 39.7     | 14477     | 17850       | 13841          | 2.33                 |
-- | 90010  | 3800           | 37.8     | 1874      | 1926        | 2014           | 1.87                 |
-- +--------+----------------+----------+-----------+-------------+----------------+----------------------+
```

5. Count the amount of rows of the table `pop`.

```sql
select count(*) from pop;
-- output:
-- +--------+
-- | count  |
-- +--------+
-- | 319    |
-- +--------+
```
