## Data format

​	In Sqoop, we can specify the format our data will be loaded into HDFS. To do so, we use the flags `--as-<format>`:

- ```bash
sqoop import <...> --as-textfile # default
  ```

- ```bash
  sqoop import <...> --as-parquetfile
  ```

- ```bash
  sqoop import <...> --as-avrodatafile
  ```

- ```bash
  sqoop import <...> --as-sequencefile
  ```

## Compression

​	By default, data imported by Sqoop is compressed with GZIP, but the entire list of codecs can be seen on the file `/etc/hadoop/conf/core-site.xml`.

​	To change the codec, use the `--compress` to turn on the compression settings. Then use `--compression-codec <codec> `:

​	Examples:

```bash
sqoop import <...> --compress --compress-codec org.apache.hadoop.io.compress.GzipCodec
sqoop import <...> --compress --compress-codec org.apache.hadoop.io.compress.BZip2Codec
sqoop import <...> --compress --compress-codec org.apache.hadoop.io.compress.SnappyCodec
```

