# Exercises - Partitioning

1. Create the directory `/user/aluno/rafael/data/birth` on HDFS.

```bash
hdfs dfs -mkdir /user/aluno/rafael/data/birth
```

2. Create and use the database `rafael`.

```sql
-- the db is already created from the previous exercise.
use rafael;
```

3. Create an external table on Hive with the parameters:
      1. Table name: `birth`.
      2. Fields: name (string), sex (string) e frequency (int).
      3. Partition: year.
      4. Delimiters:
         1. Field `,`.
         2. Line `\n`.

      5. Save options:
         1. File type: text.
         2. HDFS location: `/user/aluno/rafael/data/birth`.

```sql
create external table birth
(
  name string,
  sex string,
  frequency int
)
partitioned by (year int)
row format delimited
fields terminated by ','
lines terminated by '\n'
stored as textfile
location '/user/aluno/rafael/data/birth';
```

4. Add the partition `year=2015`.

```sql
alter table birth add partition (year=2015);
```

5. Send the local file `input/exercises-data/names/yob2015.txt` to the HDFS on the directory `/user/aluno/rafael/data/birth/ano=2015`.

```bash
# on the namenode bash:
hdfs dfs -put /input/exercises-data/names/yob2015.txt /user/aluno/rafael/data/birth/year=2015
```

6. Select the first 10 rows of the table `birth` on Hive.

```sql
select * from birth limit 10;
-- output:
-- +-------------+------------+------------------+-------------+
-- | birth.name  | birth.sex  | birth.frequency  | birth.year  |
-- +-------------+------------+------------------+-------------+
-- | Emma        | F          | 20435            | 2015        |
-- | Olivia      | F          | 19669            | 2015        |
-- | Sophia      | F          | 17402            | 2015        |
-- | Ava         | F          | 16361            | 2015        |
-- | Isabella    | F          | 15594            | 2015        |
-- | Mia         | F          | 14892            | 2015        |
-- | Abigail     | F          | 12390            | 2015        |
-- | Emily       | F          | 11780            | 2015        |
-- | Charlotte   | F          | 11390            | 2015        |
-- | Harper      | F          | 10291            | 2015        |
-- +-------------+------------+------------------+-------------+
```

7. Repeat the step 4 to 6 with 2016 and 2017.

```sql
-- creating the partitions on hive:
alter table birth add partition (year=2016);
alter table birth add partition (year=2017);
```

```bash
# loading the data to the hdfs directory:
hdfs dfs -put /input/exercises-data/names/yob2016.txt /user/aluno/rafael/data/birth/year=2016
hdfs dfs -put /input/exercises-data/names/yob2017.txt /user/aluno/rafael/data/birth/year=2017
```

```sql
-- selecting the first 10 lines
select * from birth where year = 2016;
-- output:
-- --+-------------+------------+------------------+-------------+
-- | birth.name  | birth.sex  | birth.frequency  | birth.year  |
-- +-------------+------------+------------------+-------------+
-- | Emma        | F          | 19471            | 2016        |
-- | Olivia      | F          | 19327            | 2016        |
-- | Ava         | F          | 16283            | 2016        |
-- | Sophia      | F          | 16112            | 2016        |
-- | Isabella    | F          | 14772            | 2016        |
-- | Mia         | F          | 14415            | 2016        |
-- | Charlotte   | F          | 13080            | 2016        |
-- | Abigail     | F          | 11747            | 2016        |
-- | Emily       | F          | 10957            | 2016        |
-- | Harper      | F          | 10773            | 2016        |
-- +-------------+------------+------------------+-------------+
select * from birth where year = 2017;
-- output:
-- --+-------------+------------+------------------+-------------+
-- | birth.name  | birth.sex  | birth.frequency  | birth.year  |
-- +-------------+------------+------------------+-------------+
-- | Emma        | F          | 19738            | 2017        |
-- | Olivia      | F          | 18632            | 2017        |
-- | Ava         | F          | 15902            | 2017        |
-- | Isabella    | F          | 15100            | 2017        |
-- | Sophia      | F          | 14831            | 2017        |
-- | Mia         | F          | 13437            | 2017        |
-- | Charlotte   | F          | 12893            | 2017        |
-- | Amelia      | F          | 11800            | 2017        |
-- | Evelyn      | F          | 10675            | 2017        |
-- | Abigail     | F          | 10551            | 2017        |
-- +-------------+------------+------------------+-------------+
```

