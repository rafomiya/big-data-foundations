# Repair tables

​	When manipulating tables in Hive, we might have need to repair our tables and partitions.

​	That can happen for two reasons:

1. our table couldn't find a partition; or
2. we need to sync our table with the Metastore.

​	The command to do so is also very simple:

```sql
msck repair table <tbname>;
```

​	This command will verify if the partitions stored in the HDFS are in sync with Hive's metadata.
