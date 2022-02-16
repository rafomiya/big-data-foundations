# Import to a directory

​	By default, Sqoop stores data on the HDFS `home` directory.

​	To change this, we use the `--target-dir` flag:

```bash
sqoop import <...> --target-dir /user/root/db
```

​	To specify where the data will be loaded into, we can also use the `--warehouse-dir` flag:

```bash
sqoop import <...> --warehouse-dir /user/root/db
```

## `--target-dir` vs. `--warehouse-dir`

​	The `--warehouse-dir` flag will create a directory to store our table inside the specified directory:

```bash
sqoop import --table employees <...> --warehouse-dir /user/root/db
# the data will be loaded into /user/root/db/employees
```

​	The `--target-dir` flag will simply load the data into the specified directory

```bash
sqoop import --table employees <...> --target-dir /user/root/db
# the data will be loaded into /user/root/db
```

​	Usually (but not always), we will use `--warehouse-dir`.

## Directory already exists

​	To import data to a directory that already exists, we use the `--delete-target-dir` or the `--append` flags:

- `--delete-target-dir`: deletes everything inside the directory and adds the imported data.
- `--append`: adds the data without deleting the data already stored.
