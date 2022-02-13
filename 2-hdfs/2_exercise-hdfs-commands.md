# Exercises - HDFS Commands

1. Create the directory structure below:

  >```
  > user/
  >   └── aluno/
  >         └── <nome>/
  >               ├── data/
  >               ├── recover/
  >               └── delete/
  >```

  ```bash
  hdfs dfs -mkdir -p /user/aluno/rafael/data
  hdfs dfs -mkdir /user/aluno/rafael/recover
  hdfs dfs -mkdir /user/aluno/rafael/delete
  ```

2. Send the directory `/input/exercises-data/escola` and the file `/input/exercises-data/entrada1.txt` to `data`.

  ```bash
  hdfs dfs -put /input/exercises-data/escola /user/aluno/rafael/data
  hdfs dfs -put /input/exercises-data/entrada1.txt /user/aluno/rafael/data
  ```

3. Move the file `entrada1.txt` to `recover`.

  ```bash
  hdfs dfs -mv /user/aluno/rafael/data/entrada1.txt /user/aluno/rafael/recover/
  ```

4. Download the file `escola/aluno.json` to the local workspace `/`.

```bash
hdfs dfs -get /user/aluno/rafael/data/escola/alunos.json /
```

5. Delete the folder `recover`.

  ```bash
  hdfs dfs -rm -r /user/aluno/rafael/recover/
  # output:
  # 22/02/09 17:29:55 INFO fs.TrashPolicyDefault: Namenode trash configuration: Deletion interval = 0 minutes, Emptier interval = 0 minutes.
  # Deleted /user/aluno/rafael/recover
  ```

6. Permanently delete the `delete` folder.

  ```bash
  hdfs dfs -rm -skipTrash -r /user/aluno/rafael/delete/
  # output:
  # Deleted /user/aluno/rafael/delete
  ```

7. Look for the file `alunos.csv` inside `/user`.

  ```bash
  hdfs dfs -find /user -name alunos.csv
  # output:
  # /user/aluno/rafael/data/escola/alunos.csv
  ```

8. Show the last 1KB of the file `alunos.csv`.

  ```bash
  hdfs dfs -tail /user/aluno/rafael/data/escola/alunos.csv
  # output:
  # NHO KANAREK",2018,0,N,2081113,2399342
  # 26660,"PIETRA DE SOUZA MATANA",2019,0,N,2081113,2399351
  # 11693,"PIETRA MARINÉE ZAMIN",2016,1,G,62151,62474
  # 573,"PIETRA PERES SCHLUMPF",2015,,M,2081113,3402
  # 23268,"PIETRA SOUTO LEMBERCK",2018,0,N,2081113,2399362
  # 17350,"PIETRO ANTUNES MACHADO",2017,,M,37350,511414
  # 27185,"PIETRO BORGES TIECHER",2019,0,N,2081113,2399346
  # 486,"PIETRO CORADINI FOLETTO",2015,,M,2081113,3402
  # 26272,"PIETRO EGLON DOLMAZE DE MEDEIROS",2019,0,N,2081113,2399335
  # 24473,"PIETRO HENRIQUE SILVA DOS SANTOS",2018,0,N,2081113,2399355
  # 4364,"PLINIO BITENCURT FINAMOR",2014,1,T,37350,39
  # 2084,"POLIANA GRAUPE DE ALMEIDA",2012,0,M,37350,1117
  # 21855,"POLIANA WAHLBRINCK VOLZ",2018,0,N,2081113,2399327
  # 1528,"POLYANA FOLETTO PRAUCHNER",2014,0,M,37350,1212
  # 21162,"POLYANA FOLETTO PRAUCHNER",2018,1,G,5997,712452
  # 21672,"POLYANA FUCILINI",2018,0,N,2081113,2399116
  # 20089,"PRAXEDES RODRIGUES DE RODRIGUES",2017,,M,37350,3763
  # 27509,"PRECILA FRANCESCKI TURRA",2019,1,T,2081111,34236
  # 1345,"PREDON DE SOUZA DA SILVA",2015,,M,37350,11442
  ```

9. Show the first 2 lines of the file `alunos.csv`.

  ```bash
  hdfs dfs -cat /user/aluno/rafael/data/escola/alunos.csv | head -n 2
  # output:
  # id_discente,nome,ano_ingresso,periodo_ingresso,nivel,id_forma_ingresso,id_curso
  # 18957,"ABELARDO DA SILVA COELHO",2017,1,G,62151,76995
  ```

10. Make the checksum of the file `alunos.csv`.

  ```bash
  hdfs dfs -checksum /user/aluno/rafael/data/escola/alunos.csv | head -n 2
  # output:
  # /user/aluno/rafael/data/escola/alunos.csv	MD5-of-0MD5-of-512CRC32C	000002000000000000000000164b9235a4d65a1e8ebfe12eb97ac471
  ```

11. Create an empty file called `test` on the directory `data`.

```bash
hdfs dfs -touchz /user/aluno/rafael/data/test
```

12. Change the replication factor of the file `test` to 2.

```bash
hdfs dfs -setrep 2 /user/aluno/rafael/data/test
# output:
# Replication 2 set: /user/aluno/rafael/data/test
```

13. Show informations about the file `alunos.csv`.

```bash
hdfs dfs -stat /user/aluno/rafael/data/escola/alunos.csv
# output:
# 2022-02-09 17:23:16
hdfs dfs -stat %r /user/aluno/rafael/data/escola/alunos.csv
# output:
# 3
hdfs dfs -stat %o /user/aluno/rafael/data/escola/alunos.csv
# output:
# 134217728
```

14. Show the `data`'s disk usage.

```bash
hdfs dfs -du -h /user/aluno/rafael/data/
# output:
# 533.9 M  /user/aluno/rafael/data/exercises-data
# 0        /user/aluno/rafael/data/test
hdfs dfs -df -h /user/aluno/rafael/data/
# output:
# Filesystem               Size     Used  Available  Use%
# hdfs://namenode:8020  198.2 G  539.7 M    130.3 G    0%
```

