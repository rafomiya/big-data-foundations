# Hive partitioning

## What is a Hive partition?

​	A partition is pretty much a way to optimize Hive's queries, dividing the data contained in a table in more directories.

​	Hive's tables are divided in two types:

- Non-partitioned: queries made on those tables needs to verify every row of it.
  - Can be incredibly slow on big tables.

- Partitioned: queries made on those tables needs to verify only a specific part of it.
  - We can use any field to create partitions on our tables.
  - Partitions works like directories, dividing the rows of a table in groups.
  - A common field to be partitioned is the `date`.


## Creating a partition

- Fields used to make partitions aren't on the table structure.
- Partitions are only a way to organize the data of our table, but it doesn't really change the way we access this data. That means our `SELECT` statements are still going to be the same.
- When creating a partition, **pick the field that uses the `WHERE` clause the most**.

```sql
create table tbname
(
    ...
    ...
) ...
partitioned by (<field> <datatype>);
```

## Buckets

- Buckets are a way of subdivide the data inside each partition.
- They represent the amount of data each partition will store.
- Ideally, the field picked to do so is a increasing numerical value or alphabetic value.

```sql
create table tbname
(
    ...
    ...
) ...
clustered by (<field>) into <amount> buckets;
```

 ## Example

```sql
create table user
(
	id int,
    name string,
    age int
)
partitioned by (birth date)
clustered by (id) into 4 buckets;
```

## Partitioning types

### Static partitioning

- In this type of partitioning, each partition is manually created, and its data is also manually added.

- To create new partitions:

  - ```sql
    alter table <tbname> add partition(<partition>="<value>");
    ```

- e.g:

  - ```sql
    alter table logs add partition(date="2019-04-15");
  ```

### Dynamic partitioning

- In this type of partitioning, new partitions are created automatically in loading time.

- Partitions are created:

  - Based on the last value of the field.
    - If the partition doesn't exist, a new partition will be created.
    - If the partition does exist, the data will be inserted into this partition.

- e.g:

  - ```sql
    insert overwrite table user_city partition (city) select * from user;
    ```

- By default, the dynamic partitioning is disabled. To enable it, run the following on the Hive server:

  - ```bash	
    SET hive.exec.dynamic.partition = true;
    SET hive.exec.dynamic.partition.mode = nonstrict;
    ```

## Some commands

- See partitions:

  - ```sql
    show partitions <tbname>;
    ```

- Delete partitions from a table

  - ```sql
    alter table <tbname> drop partition (<field>, <value>);
    ```

- Change the name of a partition in a table

  - ```sql
    alter table <tbname> partition <oldname> rename to partition <newname>;
    ```

- When creating new partitions, **never** do it through the HDFS `mkdir` command.
