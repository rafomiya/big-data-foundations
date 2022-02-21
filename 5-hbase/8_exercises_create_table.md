# Exercises - Create Table

1. Create the table `control` with the data:

- Row key: `id` .
- Column families: `product` and `provider`.

```
---------------------------------------------------
|     |       product      |      provider        |
| id  |--------------------+----------------------|
|     |  name   |  amount  |  name      |  state  |
|-----+---------+----------+------------+---------|
|  1  |  ram    |  100     |  TI Comp   |  SP     |
|  2  |  hd     |  50      |  Peças PC  |  MG     |
|  3  |  mouse  |  150     |  Inf Tec   |  SP     |
---------------------------------------------------
```

```bash
# create table
create 'control', 'product', 'provider'

# insert the data
put 'control', 1, 'product:name', 'ram'
put 'control', 1, 'product:amount', 100
put 'control', 1, 'provider:name', 'TI Comp'
put 'control', 1, 'provider:state', 'SP'

put 'control', 2, 'product:name', 'hd'
put 'control', 2, 'product:amount', 50
put 'control', 2, 'provider:name', 'Peças PC'
put 'control', 2, 'provider:state', 'MG'

put 'control', 3, 'product:name', 'mouse'
put 'control', 3, 'product:amount', 150
put 'control', 3, 'provider:name', 'Inf Tec'
put 'control', 3, 'provider:state', 'SP'
```

2. List the tables and verify the structure of the table `controle`.

```bash
# list the tables:
list
# output:
# TABLE
# control
# 1 row(s) in 0.0510 seconds

# verify the structure of the table control:
desc control
# output:
# Table control is ENABLED
# control
# COLUMN FAMILIES DESCRIPTION
# {NAME => 'product', BLOOMFILTER => 'ROW', VERSIONS => '1', IN_MEMORY => 'false', KEEP_DELETED_CELLS => 'FALSE', DATA_BLOCK_ENCODING => 'NONE', 
# TTL => 'FOREVER', COMPRESSION => 'NONE', MIN_VERSIONS => '0', BLOCKCACHE => 'true', BLOCKSIZE => '65536', REPLICATION_SCOPE => '0'}            
# {NAME => 'provider', BLOOMFILTER => 'ROW', VERSIONS => '1', IN_MEMORY => 'false', KEEP_DELETED_CELLS => 'FALSE', DATA_BLOCK_ENCODING => 'NONE',
#  TTL => 'FOREVER', COMPRESSION => 'NONE', MIN_VERSIONS => '0', BLOCKCACHE => 'true', BLOCKSIZE => '65536', REPLICATION_SCOPE => '0'}           
# 2 row(s) in 0.1470 seconds
```

3. Count the number of rows of the table `controle`.

```bash
count 'control'
# output:
# 3 row(s) in 0.0460 seconds
```

4. Alter to 3 the versions of the column family `product`.

```bash
alter 'control', {NAME=>'product', VERSIONS=>3}
# output:
# Updating all regions with the new schema...
# 1/1 regions updated.
# Done.
# 0 row(s) in 1.9570 seconds
```

5. Update the amount of the `id` 2 to 200.

```bash
put 'control', 2, 'product:amount', 200
# output:
# 0 row(s) in 0.3660 seconds
```

6. Search the versions of `id` 2 of the column `amount`.

```bash
get 'control', 2, {COLUMNS=>'product:amount', VERSIONS=>2}
# output:
# COLUMN                               CELL
#  product:amount                      timestamp=1645451390032, value=200
#  product:amount                      timestamp=1645450352052, value=50    
# 2 row(s) in 0.0210 seconds
```

7. Delete the `id`s of the `SP` `state`.

```bash
scan 'control', {COLUMNS=>'provider:state', FILTER=>"ValueFilter(=, 'binary:SP')"}
# output:
# ROW                                  COLUMN+CELL
#  1                                   column=provider:state, timestamp=1645450248670, value=SP
#  3                                   column=provider:state, timestamp=1645450354522, value=SP
# 2 row(s) in 0.0720 seconds

deleteall 'control', 1
# output:
# 0 row(s) in 0.0210 seconds

deleteall 'control', 3
# output:
# 0 row(s) in 0.0060 seconds
```

8. Delete the column `state` on the `id` 2.

```bash
delete 'control', 2, 'provider:state'
# output:
# 0 row(s) in 0.0240 seconds
```

9. Scan all the `control` table.

```bash
scan 'control'
# output:
# ROW                                  COLUMN+CELL
#  2                                   column=product:amount, timestamp=1645451390032, value=200
#  2                                   column=product:name, timestamp=1645450352026, value=hd
#  2                                   column=provider:name, timestamp=1645450352070, value=Pe\xC3\xA7as PC
# 1 row(s) in 0.0160 seconds
```
