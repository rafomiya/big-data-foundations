# Incremental Load

​	Let's picture this situation:

​	You have already imported the first 3 rows of a table:

```
----------------------------------------------
|  id  | dept_name            | modify_date  |
----------------------------------------------
|    1 | BI                   | 2022-01-15   |
|    2 | Customer Service     | 2021-11-18   |
|    3 | Development          | 2021-12-22   |
----------------------------------------------
```

​	Then, after this first import, someone has inserted 4 new rows to this table. So now, you need to do the import again, but without the rows you have already imported.

​	To do so, you can use incremental loads.

## `append` mode

​	The first way to do incremental loads is through `append`. This will just add the new values to the HDFS, without modifying the old values. If a row is updated, this row won't be added to the incremental import.

```bash
sqoop import <...> \
--incremental append \
--check-column id \
--last-value 3
```

- `--check-column`: the column used know which rows to import.
- `--last-value`: the last value of the check column.

## `lastmodified` mode

​	The second way to do incremental loads is through `lastmodified`. This will update the HDFS file that contains the data, instead of just adding a new one. This mode should be used if the table can be updated, and if the update `timestamp` is stored in a field of the table.

```bash
sqoop import <...> \
--incremental lastmodified \
--merge-key id \
--check-column modify_date \
--last-value '2021-11-27'
```

