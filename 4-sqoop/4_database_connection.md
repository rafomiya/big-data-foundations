# Database connection

## What is as connection string?

​	Connection strings are what we use to connect to a database.

​	The connection string can be divided in four key parts:

- SGBD (MySQL, SQLServer, PostgreSQL, etc).
- Hostname.
- Port number.
- Database name.

​	Parameters:

```bash
--connect <conn> \
--username <user> \
--password <pw>
```

| SGBD       | Connection string  |
| ---------- | ------------------ |
| HSQLDB     | `jdbc:hsqlbd:*//`  |
| MySQL      | `jdbc:mysql://`    |
| Oracle     | `jdbc:oracle:*//`  |
| PostgreSQL | `jdbc:postgres://` |
| CUBRID     | `jdbc:cubrid:/*`   |

## Example

### List databases

```bash
sqoop list-databases \
--connect jdbc:mysql://database \
--username user \
--password password
```

### List tables

```bash
sqoop list-tables \
--connect jdbc:mysql://database/employees \
--username user \
--password password
```

### Making queries or execute statements

```bash
sqoop eval \
--connect jdbc:mysql://database/employees \
--username user \
--password password \
--query "select * from employees limit 10"
```

​	Note that the `--query` parameter contains any SQL statement, not only the `select` statement.
