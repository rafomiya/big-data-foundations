# Hive structure

## What is Hive?

​	Apache Hive is a big data tool for data analysis. It was created by Facebook in 2007, to speed up their queries.

​	Other tools for data analysis:

- Hive.
- Impala.
- Presto.
- Spark.

​	Hive can be used as a data access layer to read and manipulate the data stored in a HDFS, and the language used on it is SQL.

## Hive's use cases

​	Hive was made to be used with a large amount of data, scalable to terabytes or petabytes. If we use Hive with small amounts of data, it won't be as performative as it would be, because it uses partitioning to subdivide the data in smaller groups.

​	Hive isn't made to deliver real-time responses. To achieve that, we'd usually use other technologies, such as Impala.

## Hive components

- HCatalog: another layer to access Hive's HDFS data. It makes possible for different data processing tools to read and write the data.
- WebHCat: web server that will connect with the Metastore Hive.
- HiveServer2 (HS2): service that allows clients to execute Hive queries.
- Metastore is the place where all the tables' and partitions' metadata will be stored.
  - There are three main ways to configure your Metastore:
    - Embebbed Metastore.
    - Local Metastore.
    - Remote Metastore.
- Beeline: it is the Hive client, the one we will use to access our HiveServer2. It uses the JDBC to do so.

## Data format and structure

### Data format

- There is not a `.hive` file format.
- That is because Hive is a connector for other formats, such as:
  - CSV.
  - Parquet.
  - ORC.
  - AVRO.
  - JSON.
  - etc.

### Data structure

- The data can be structured or semi-structured.
- Data hierarchy:
  - Databases contains tables;
  - Tables contains partitions;
    - Partitions are the columns of our databases after the conversion to a directory system.
    - e.g.: if we have a `id` field in a table, this `id` will become a partition as a directory.
  - Partitions contains buckets.
- Path example: `/user/hive/warehouse/database.db/table/data=010119/000000_0`.

### Hive language

​	Hive uses the Hive Query Language, also known as HiveQL.

​	They are internally transformed into MapReduce jobs.

## Database commands

### Visualization

- `show databases`: lists all the created databases. 
- `desc database <dbname>`: describes the structure of a database.
- `show tables`: lists all the tables of the current database.
- `desc <tbname>`: describes the structure of a table (fields and data types).
- `desc formatted <tbname>`: shows the tables partitions and other configurations.
- `desc extended <tbname>`: shows even more informations about the table, such as the table location, table size, etc.

### Creating a database

- `create database <dbname>`: creates a new database in the default directory: `/user/hive/warehouse/`.
- `create database <dbname> location "/dir"`: creates a new database at the specified location.
- `create database <dbname> comment "description"`: creates a database with a comment. It's a cool way to document your code.

### Creating a table

​	Tables can have two types in Hive: internal or external.
​	It can also be partitioned or not. If it is partitioned, its partitions can be dynamic or static.

- `create table <tbname>(field1 type, field2 type)`: creates an internal table, such as in the usual SQL relational databases.
  - `drop table <tbname>`: deletes the table's data and all of its metadata.
- `create external table <tbname>(field1 type, field2 type) location '/path'`: creates an external table, that maps the contents of another table, referenced on the location path.
  - `drop table <tbname>`: deletes all the table's metadata, but the data contained on the internal tables stills intact.

​	External tables are made to share its data through other tools.

#### Data types

​	Our tables can have multiple fields, each of them with a data type. These are some of the available data types, depending on the version of Hive we are using:

​	Primitive data types:

- `INT`.
- `SMALLINT`.
- `TINYINT`.
- `BIGINT`.
- `BOOLEAN`.
- `FLOAT`.
- `DOUBLE`.
- `DECIMAL`.
- `STRING`.
- `VARCHAR`.
- `CHAR`.

​	Complex data types:

- `ARRAY`: sequence of values.
  - e.g.: `ARRAY<INT>`.
- `MAP`: key-value structure.
  - e.g.: `MAP<STRING, INT>`.
- `STRUCT`: works similarly to a class on object-oriented programming. You can define attributes to an instance of that struct.
  - e.g: `STRUCT<A: INT, B: STRING>`.
- `UNION`: makes possible for a field to have more than one data type.
  - e.g: `UNIONTYPE<INT, ARRAY<STRING>`.

#### Reading data

​	When reading a file, we can define the delimiters of each field and row. The default delimiters are '`,`' for fields and '`\n`' for lines.
​	To change the default delimiters, we can add the following commands to the end of the `create table` statements:

- `row format delimited`
- `fields terminated by <delimiter>`
- `lines terminated by <delimiter>`

#### Full example

```sql
create external table user
(
	id int,
    name string,
    age int
)
row format delimited
fields terminated by '\t'
lines terminated by '\n'
stored as textfile
location '/user/cloudera/data/client';
```

### Inserting and loading data

​	To insert data into our tables, we use the classic `insert into` SQL command. However, we may have some small differences, specially because of the partition system and other things that are specific from Hive.

#### Examples

- `insert into user values (10, 'Flávia'), (11, 'Thiago');`
- `insert into user partition(data=now()) values (10, 'Flávia'), (11, 'Thiago');`
- `insert into user select * from client;`
  - In this last example, `client` would be another internal table, with partitions, optimizations, etc. In the meanwhile, `user` would be a table that reads informations from files, for example.

​	Another thing we can do is to load the data from other directories (HDFS or local).

#### Examples

- `load data inpath <path> into table <tbname>;`
- `load data local inpath '/home/cloudera/data/test' into table student;`
- `load data inpath '/user/cloudera/data/test' overwrite into table student partition(id);`

### Reading data

​	In Hive, we can use all the SQL that we are already used to, like:

- `where`
- `group by`
- `having`
- `order by`
- `limit`
- `inner join`
- `left join`
- `right outer join`

​	We can also create views:

```sql
create view <viewname> as
select
	...
```

