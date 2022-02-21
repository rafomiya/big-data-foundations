# Reading Data

​	To query a value from HBase, we have two options of command:

## `get`

​	We use the `get` command when we want to retrieve a specific row of our table.

```bash
# returns all the data associated with that row
get '<tbname>', '<rowkey>'

# returns all the data associated with that row and that column family
get '<tbname>', '<rowkey>', {COLUMNS=>['<columnfamily>']}
# it is possible to add more column families on the []

# returns all the data associated with that row and that column
get '<tbname>', '<rowkey>', {COLUMNS=>['<columnfamily>:<column>']}
```

## `scan`

​	We use the `scan` command when we want to retrieve data from the entire table, not just one specific row.

```bash
# returns all rows and columns of the table
scan '<tbname>'

# returns all the rows of a specific column family
scan '<tbname>', {COLUMNS=>['<columnfamily>']}

# returns all the rows of a specific column
scan '<tbname>', {COLUMNS=>['<columnfamily>:<column>']}
```
