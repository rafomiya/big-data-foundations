# Importing data

​	In Sqoop, the process of importing data will always be from the RDBMS to the HDFS.

​	To do so, we need a few key informations:

1. Which JDBC will be used? (RDBMS);
2. User and password of the database;
3. Which database will be used;
4. Which table; and
5. Which data.

## The `import` command

​	Example:

```bash
sqoop import --connect jdbc:mysql://database --username root --password secret
```

​	In this command, we already specified the items 1, 2 and 3 of the list above. Only items 4 and 5 are missing.

### Which data will be imported?

​	To specify what row, column or table will be imported, we use the `--table`, `--columns` or `--where` flags.

​	Examples:

```bash
# 1
sqoop import \
--table employees \
--connect <...>

# 2
sqoop import \
--table <tb_name> \
--connect <...> \
--columns "id,last_name"

# 3
sqoop import \
--table <tb_name> \
--connect <...> \
--where <where_clause>
```
