# Sqoop Jobs

​	Jobs are a Sqoop recourse used to store incremental `import`/`export` commands.

```bash
sqoop job <attributes>
```

​	The possible attributes are:

- `--create <jobid>`: creates a job.

```bash
# example:
sqoop job \
--create myjob \
--import \
--connect jdbc:mysql://database/employees \
--username root \
--password secret \
--table employee \
-m 1
```

- `--list`: see the list of jobs.
- `--show <jobid>`: shows details from a specific a job.
- `--exe <jobid>`: executes the job.
- `--delete <jobid>`: deletes the job.
