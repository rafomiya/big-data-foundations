# Export data

   In Sqoop, the process of exporting data will always be from the HDFS to the RDBMS.

   To do so, we need a few key informations:

1. Where our data is stored? (HDFS directory);
2. Which SGBD is being used;
3. Username and password;
3. Which database;
4. Which table; and
5. Which data.

## The `export` command

​	Example:

```bash
sqoop --export \
<...> \
```

​	The `export` command has a few flags to set up its behavior:

- `--export-dir <path>`: specifies the directory to be read from the HDFS.
- `--table <tbname>`: defines the name of the table on the SGBD.
- `--update-mode`: specified how the data will be added into the SGBD.
  - `updateonly` (default): simply adds the rows to the SGBD. Each row will be converted into a `insert`. This can cause exceptions involving the `unique` fields.
  - `allowinsert`: if the row already exists, update the data. Else, just insert the line. This takes more time than the default mode.

​	Before the export, the table schema must already exist on the SGBD.

### Full example:

```bash
sqoop export \
--connect jdbc:mysql://database/employees \
--username root \
--password secret \
--export-dir /user/root/recommender_output \
--update-mode allowinsert \
--table product_recomendation
```

