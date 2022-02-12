# Exercises - Read Hive data

1. Select the first 10 rows of the table `birth` by the year of 2016.

```sql
select * from birth
where year = 2016
limit 10;
-- output:
-- +-------------+------------+------------------+-------------+
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
```

2. Count the amount of names of child born in 2017.

```sql
select
  count(distinct name) as `count_names_2017`
from birth
where year = 2017;
-- output:
-- +-------------------+
-- | count_names_2017  |
-- +-------------------+
-- | 29910             |
-- +-------------------+
```

3. Count the amount of child born in 2017.

```sql
select
  count(*) as `count_2017`
from birth
where year = 2017
limit 1;
-- output:
-- +-------------+
-- | count_2017  |
-- +-------------+
-- | 32469       |
-- +-------------+
```

4. Count the amount of child born by sex in 2015.

```sql
select
  count(case when sex = 'F' then 1 end) as `amount_female`,
  count(case when sex = 'M' then 1 end) as `amount_male`
from birth
where year = 2015;
-- output:
-- +----------------+--------------+
-- | amount_female  | amount_male  |
-- +----------------+--------------+
-- | 19074          | 14024        |
-- +----------------+--------------+
```

5. Show, ordering by decreasing year, the amount of childs born by sex.

```sql
select
  year,
  count(case when sex = 'F' then 1 end) as `amount_female`,
  count(case when sex = 'M' then 1 end) as `amount_male`
from birth
group by year
order by year desc;
-- output:
-- +-------+----------------+--------------+
-- | year  | amount_female  | amount_male  |
-- +-------+----------------+--------------+
-- | 2017  | 18309          | 14160        |
-- | 2016  | 18817          | 14162        |
-- | 2015  | 19074          | 14024        |
-- +-------+----------------+--------------+
```

6. Show, ordering by decreasing year, the amount of child born by sex with name starting with ‘A’.

```sql
select
  year,
  count(case when sex = 'F' then 1 end) as `amount_female`,
  count(case when sex = 'M' then 1 end) as `amount_male`
from birth
where name like 'A%'
group by year
order by year desc;
-- output:
-- +-------+----------------+--------------+
-- | year  | amount_female  | amount_male  |
-- +-------+----------------+--------------+
-- | 2017  | 2927           | 1574         |
-- | 2016  | 3038           | 1548         |
-- | 2015  | 3067           | 1505         |
-- +-------+----------------+--------------+
```

7. Show the name and amount of the 5 most frequent child names born in 2016.

```sql
select
  name,
  frequency
from birth
where year = 2016
order by frequency desc
limit 3;
-- output:
-- +---------+------------+
-- |  name   | frequency  |
-- +---------+------------+
-- | Emma    | 19471      |
-- | Olivia  | 19327      |
-- | Noah    | 19082      |
-- +---------+------------+
```

8. Show the name and amount of the 5 most frequent child names born in 2016 by sex, male and female.

```sql
select
  name as `female_names`,
  frequency as `amount`
from birth
where year = 2016 and sex = 'F'
order by frequency desc
limit 5;
-- output:
-- +---------------+--------+
-- | female_names  | amount |
-- +---------------+--------+
-- | Emma          | 19471  |
-- | Olivia        | 19327  |
-- | Ava           | 16283  |
-- | Sophia        | 16112  |
-- | Isabella      | 14772  |
-- +---------------+--------+
select
  name as `male_names`,
  frequency as `amount`
from birth
where year = 2016 and sex = 'M'
order by frequency desc
limit 5;
-- output:
-- +-------------+--------+
-- | male_names  | amount |
-- +-------------+--------+
-- | Noah        | 19082  |
-- | Liam        | 18198  |
-- | William     | 15739  |
-- | Mason       | 15230  |
-- | James       | 14842  |
-- +-------------+--------+
```