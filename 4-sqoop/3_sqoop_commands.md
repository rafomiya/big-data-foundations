# Sqoop Commands

​	Sqoop's commands are used for 3 basic tasks:

- Import data;
- Export data; and
- Automatize this process.

```bash
sqoop <command>
```

​	Replace `<command>` with one of the following commands:

- `help <command>`: displays the documentation of each command. If no command is specified, it will list all the commands.
- `version`: displays the Sqoop version. 
- `import`: imports data from the RDBMS to HDFS.
- `import-all-tables`: works just like `import`, but with more tables.
- `export`: exports data from the HDFS to a RDBMS.
- `validation`: validates the copied data (imported or exported) based on the count of rows.
- `job`: manages saved jobs.
- `create-hive-table`: creates a Hive table.
- `list-databases`: lists the databases.
- `list-tables`: lists the tables from the database.
- `eval`: executes queries on the database through Sqoop.
- `metastore`
- `merge`
- `codegen`

