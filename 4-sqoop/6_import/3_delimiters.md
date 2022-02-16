# Specifying File Delimiters

​	Sqoop's imports generates files inside the HDFS. These files have a specific format:

- Fields separated by '`,`'
- Rows separated by '`\n`'

​	To change this default setting, we can use the `--fields-terminated-by` and `--lines-terminated-by` flags at the end of our imports:

```bash
sqoop import \
<...> \
--fields-terminated-by ';' \
--lines-terminated-by '&'
```

