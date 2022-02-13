# Exercises - Hive Commands

1. Send the local file `/input/exercises-data/populacaoLA/populacaoLA.csv` to the HDFS directory `/user/aluno/rafael/data/populacao`.

```bash
docker exec -it namenode bash
# entered namenode terminal
hdfs dfs -put /input/exercises-data/populacaoLA/populacaoLA.csv /user/aluno/rafael/data/populacao
```

2. List the Hive databases.

```bash
docker exec -it hive-server bash
# entered hive-server's container terminal
beeline -u jdbc:hive2://localhost:10000 
# entered hive's terminal
show databases;
# output:
# +----------------+
# | database_name  |
# +----------------+
# | default        |
# +----------------+
```

3. Create the database `rafael`.

```bash
create database rafael;
```

4. Create the table `pop`.

```sql
create table pop
(
  zip_code int,
  total_population int,
  median_age float,
  total_males int,
  total_females int,
  total_households int,
  average_household_size float
)
row format delimited
fields terminated by ','
lines terminated by '\n'
stored as textfile
tblproperties("skip.header.line.count"="1");
```

5. See the description of the table `pop`.

```bash
desc pop;
# +-------------------------+------------+----------+
# |        col_name         | data_type  | comment  |
# +-------------------------+------------+----------+
# | zip_code                | int        |          |
# | total_population        | int        |          |
# | median_age              | float      |          |
# | total_males             | int        |          |
# | total_females           | int        |          |
# | total_households        | int        |          |
# | average_household_size  | float      |          |
# +-------------------------+------------+----------+
```

