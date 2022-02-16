# Creating the databases

1. Copy the input files to the docker container.

```bash
docker cp input/exercises-data/db-sql/ database:/
```

2. Access the `database` container.

```bash
docker exec -it database bash
```

3. Execute the SQL scritps.

```bash
cd /db-sql/sakila/
mysql -psecret < sakila-mv-schema.sql
mysql -psecret < sakila-mv-data.sql
```