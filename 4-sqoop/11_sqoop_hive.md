# Importing data to Hive

​	When using Sqoop to import data to the HDFS, instead of importing to the HDFS and then loading to Hive, we can do this directly to the Hive or HBase databases.

​	To keep a good performance, a common pattern to follow is to use the Parquet format and Snappy compression.

​	To import to Hive, we need to learn a few new flags of the `import` command:

- `--hive-import`: specifies that the imported data is going to a Hive table.
- `--hive-overwrite`: overwrites the rows if the table already exists.
- `--create-hive-table`: with this flag, the `import` command will fail if the table already exists.
- `--hive-table <dbname>.<tbname>`: specifies the Hive table.

​	Full example:

```bash
sqoop import \
--connect jdbc:mysql://database/employees \
--username root \
--password secret \
--warehouse-dir /user/hive/warehouse/test.db \
--hive-import \
--create-hive-table \
--hive-table test.employee
```