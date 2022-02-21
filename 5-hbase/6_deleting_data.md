# Deleting Data

​	To delete a value from HBase, we have three options of command:

1. Delete a column

```bash
delete '<tbname>', '<rowkey>', '<columnfamily>:<column>'
```

2. Delete a column family

```bash
delete '<tbname>', '<rowkey>', '<columnfamily>'
```

3. Delete a row

```bash
deleteall '<tbname>', '<rowkey>'
```

