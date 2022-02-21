# Insert and Update Data

​	To insert and update data in HBase, we use the `put` command.

​	Syntax:

```bash
put '<tbname>', '<rowkey>', '<family>:<column>', '<value>'
```

​	Examples:

- `put 'customer', '1', 'address:country', 'BR'`
- `put 'customer', '1', 'address:city', 'SP'`
- `put 'customer', '1', 'address:street', 'Av. Paulista'`
- `put 'customer', '4', 'order:date', '2021-11-26'`

​	To update a cell, all we need to do is `put` the data again, with a new value:

- `put 'customer', '1', 'address:street', 'Av. 25 de Março'`
