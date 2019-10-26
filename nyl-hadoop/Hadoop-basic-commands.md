


> Written with [StackEdit](https://stackedit.io/).

# Hadoop Basic Commands

#### Move File form local to HDFS
```
$ hdfs dfs -put final data.csv
```

#### Move File form HDFS to local
```
$ hdfs dfs -get final data.csv
```
#### List the content on HDFS
```
$ hdfs dfs -ls
```
#### Remove a file from hdfs
```
$ hdfs dfs -rm /user/data.csv
```
Recursive version of delete
```
$ hdfs dfs -rmr /user/
```
#### See contents of a file on HDFS
```
$ hdfs dfs -cat data.csv
```
#### Copy a file from source to destination
This command allows multiple sources as well in which case the destination must be a directory.
```
Usage:
$ hdfs dfs -cp <source> <dest>
Example:
$ hdfs dfs -cp /user/saurzcode/dir1/abc.txt /user/saurzcode/dir2
```
#### Display last few lines of a file
Similar to tail command in Unix
```
Usage :
hadoop fs -tail <path[filename]>
Example:
hadoop fs -tail /user/saurzcode/dir1/abc.txt
```

<!--stackedit_data:
eyJoaXN0b3J5IjpbNzkwNjY5NjkyXX0=
-->