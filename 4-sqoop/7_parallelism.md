# Parallelism

​	To optimize our Sqoop imports, we can use parallelism. That means dividing our jobs to more mappers, each of them running Map Reduce jobs inside a datanode.

​	By default, the amount of mappers that will handle a Sqoop job is 4. That means that in an import of 400 rows, each mapper will handle 100 rows, making that division based on the primary key of the table.

​	To change the number of mappers for a Sqoop import, we use the `-m` flag:

```bash
sqoop import <...> -m 2
```

## Handling the primary key

​	If the primary key does exist, Sqoop will successfully know how to divide the job to the mappers. However, if the primary key doesn't exist, Sqoop won't know how to do it. For that reason, we can use the `--auto-reset-to-one-mapper` flag:

```bash
sqoop import <...> -m 8 --auto-reset-to-one-mapper
```

​	In this example, the number of mappers can be `1` or `8`, depending on wheter the table have a primary key or not.

​	In other cases, if we try to specify a number of mappers without a primary key, Sqoop will recommend us to use `split-by`.

### `--split-by`

​	Uses a specified non-key field to divide the job to the mappers.

```bash
sqoop import <...> --split-by <field>
```

​	If the field has null values, these rows are simply not gonna be imported.

## Importing null values

​	When importing a null value, we can use the flags `--null-string` and `--null-non-string` to specify how to handle null values.

​	`--null-string`: used when the field is string. All null values are gonna be replaced by the inputed parameter from this flag.
​	`--null-non-string`: used when the field isn't a string. All null values are gonna be replaced by the inputed parameter from this flag.

    Example:

```bash
sqoop import <...> --null-string 'none'
```