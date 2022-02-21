# HBase Commands

​	First of all, to acces the HBase commands, we will need the HBase Shell or a Java API.
​	We will learn the HBase Shell:

```bash
hbase shell
```

## General commands

- `status`: shows statuses of the HBase execution, such as the number of servers.
- `version`: displays the HBase version.
- `table_help`: shows a help message about table commands.
- `whoami`: displays informations about the current user.
- `help <command>`: displays a help message about the specified command.

## Table manipulation commands

- `create`: creates a table.
- `list`: lists all the tables.
- `disable`: disables a table. This is necessary if you want to delete the table, for instance.
- `is_disabled`: verifies if the table is disabled.
- `enable`: enables a previously disabled table.
- `is_enabled`: verifies if the table is enabled.
- `describe`: describes a table, showing details about its structure and other informations.
- `alter`: alters a table with the specified new settings.
- `exists`: verifies if the table exists.
- `drop`: drops the specified table.
- `drop_all`: drops all the tables matching a given regular expression.

## Data manipulation commands

- `put`: inserts or updates data.
- `get`: returns the data of a specific row.
- `delete`: deletes data of a column.
- `deleteall`: deletes data of an entire row.
- `scan`: returns the data of more than one row.
- `count`: returns the amount of rows of a table.
- `truncate`: disables and recreates the table.
