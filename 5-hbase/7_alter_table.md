# Alter Table

​	When altering a table schema in HBase, we have no access to the columns itself, only to the column families.

## Examples

1. Update the number of versions of a column family:

```bash
alter '<tbname>', {NAME=>'<columnfamily>', VERSIONS=>5}
```

2. Add a new column family:

```bash
alter '<tbname>', {NAME=>'<columnfamily>'}
```

3. Delete a column family:

```bash
alter '<tbname>', 'delete'=>'<columnfamily>'
```

## Counting the data

​	In HBase, there is a specific command for counting the amount of rows of a table:

```bash
count '<tbname>'
```

