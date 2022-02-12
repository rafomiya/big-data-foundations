# HDFS Commands

​	The HDFS commands works on a very similar way to bash. To make any HDFS command, we use `hdfs dfs <command>`.

## Help

- `hdfs dfs -help `: help message.
- `hdfs dfs -help <command>`: help message about the command specified.

## Files & directories

### Manipulating data

- `hdfs dfs -ls`: list all the files and directories.
- `hdfs dfs -mkdir <dir>`: creates a directory with the dirname.
- `hdfs dfs -mkdir -p <dirname>/<dirname>`: creates a new directory structure.
- `hdfs dfs -rm <file>`: removes a file.
  - `hdfs dfs -rm -r <dir>` removes a directory.

- `hdfs dfs -cat <file>`: shows the contents of the specified file.
- `hdfs dfs -checksum <file>`: executes a checksum on the specified file, to verify its integrity.
- `hdfs dfs -tail <file>`: shows the last 1 KB of the specified file.
  - `hdfs dfs -cat <file> | head -n 5`: an alternative to show the first 5 lines of a file, since Hadoop 2 doesn't have a built-in `head` command.

### Accessing and moving data

- `hdfs dfs -put <src> <dtn>`: copies a file from the local workspace to the HDFS (Local -> HDFS).
  - `hdfs dfs -copyFromLocal <src> <dtn>`: does pretty much the same thing.
  - `hdfs dfs -moveFromLocal <src> <dtn>`: works the same way as a `put`, but deleting the file or folder from `<src>`.
- `hdfs dfs -get <src> <dtn>`: copies a file from the HDFS to the local workspace (HDFS -> Local).
  - The `-f` flag will override the file in case there's a file with the same name on the `<dtn>` directory.
  - `hdfs dfs -getmerge <src> <dtn>:`: merges all the files into one.
  - `hdfs dfs -moveToLocal <src> <dtn>`: deletes the file from the HDFS after getting it.
- `hdfs dfs -cp <src> <dtn>`: copies a file from the HDFS to another HDFS directory (HDFS -> HDFS).
  - `hdfs dfs -mv <src1> <src2> <src3> <dtn>`: moves one or more files from the HDFS to another HDFS location.


## Memory

- `hdfs dfs -du -h <dir>`: shows the disk usage of the specified directory.
- `hdfs dfs -df -h <dir>`: shows the free space of the specified directory.
- `hdfs dfs -stat <file>`: shows informations about the specified directory:
  - `hdfs dfs -stat %r name.txt`: replication factor (RF). 
  - `hdfs dfs -stat %o name.txt`: block size.
- `hdfs dfs -count -h <dir>`: shows, in order, the amount of directories, the amount of files and the size of the specified file.
- `hdfs dfs -expunge`: empty trash.

## Location

- `hdfs dfs -find <path> <search>`: searches for a file or directory on the specified path.
  - `hdfs dfs -find / -name data`: displays everything that matches "data".
  - `hdfs dfs -find / -iname Data`: displays everything that matches "Data", but with case insensitivity.
  - `hdfs dfs -find input/ -name \*.txt`: displays all the `.txt` files on the `input/` directory.

## Misc

- `hdfs dfs -setrep <file>`: change the replication factor of the specified file.
- `hdfs dfs -touchz <dir>`: creates a log file with date and time.