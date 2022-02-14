# File format and compression

## File formats:

- Text files.
    - Default format for Hive and Sqoop.
- Sequence file.
    - Key-value pairs format.
    - Stored as binary.
    - More efficient than text files.
    - Easier to integrate with other Hadoop tools.
- RC file: stands for Record Columnar file.
    - Formed by groups of columns.
    - Horizontal storage of data.
    - Advantages:
        - Fast to load.
        - Fast to query.
        - Efficient storage space.
    - Disadvantages:
        - Uses more memory and computing.
        - Doesn't support the evolution of the schema.
- ORC file: stands for Optimized Row Columnar file.
    - Has the same characteristics of the RC file, but with some optimizations:
        - The data compacted in a more efficient way, making possible to do faster queries.
        - Made to optimize Hive's performance.
    - It isn't used to non-Hive MapReduce, such as Pig or Impala.
- Avro: data serialization with language neutrality.
    - Data and metadata are stored together.
    - Frequently used to traffic data across the network.
        - e.g: Apache Kafka.
    - Supports MapReduce.
    - Supports updates on the data schema.
- Parquet:
    - Columnar file format: formed by groups of columns.
    - Advantages:
        - Supports Map Reduce.
            - e.g: Pig, Apache Hive, Java.
        - Data processing.
            - e.g: Apache Spark, Impala.
        - Supports the schema's evolution.

## Data compression

​	When it comes to data compression, it is impossible to have everything: we usually need to ask a really important question:

​	What is more important? Storage or velocity of reading?

## Compression libraries

- ZLIB (GZip): slow, but does a deep compression.
- Snappy: fast, but does has a superficial compression.

​	Usually, we use Parquet files compressed with Snappy.
