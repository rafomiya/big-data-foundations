# Data formats and compression in Hive

## Data formats

​	When creating a table, we can use the `stored as <format>` statement to specify what is the format we want to store our file.

​	Between the available formats, we have:

- `TEXTFILE` (default).
- `SEQUENCEFILE`.
- `RCFILE`.
- `ORC` (Hortonworks).
- `PARQUET` (Cloudera).
- `AVRO` (Kafka).
- `JSONFILE` (very used in data transferences).

## Data compression

​	In Hive, the compression configurations are made inside the `mapred-site.xml` file, but they can also be manually added.

```bash
hive> SET hive.exec.compress.output=true;
hive> SET mapred.output.compression.codec=<codec>;
hive> SET mapred.output.compression.type=BLOCK;
```

​	Replace `<codec>` for one of the following:

- gzip: `org.apache.hadoop.io.compress.GzipCodec`
- bzip2: `org.apache.hadoop.io.compress.BZip2Codec`
- LZO: `com.hadoop.compression.lzo.LzopCodec`
- Snappy: `org.apache.hadoop.io.compress.SnappyCodec`
- Deflate: `org.apache.hadoop.io.compress.DeflateCodec`

### Adding compression to tables

​	Add this to the end of the `create table` statement:

```sql
stored as <file_format> tblproperties('<file_format>.compress'='<compression>');
```

​	Available options to replace `<codec>`:

- GZIP.
- BZIP2.
- LZO.
- SNAPPY.
- DEFLATE.

## Full example

​	Table with partition and compression:

```sql
create table user(
	id int,
    name String,
    age int
)
partitioned by (data String)
clustered by (id) into 256 buckets
stored as parquet
tblproperties('parquet.compress'='SNAPPY');
```
