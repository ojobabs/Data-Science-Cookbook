


> Written with [StackEdit](https://stackedit.io/).

# Using PySpark on the remote server

### Execute a PySpark script on the remote server

To run a PySpark script on the remote Linux (Hadoop) environment you need write the PySpark code on a `.py` Python file. You can write here Python code too. 

 ```bash
 $ spark-submit name_of_program.py
 ```

To run on the cluster mode you need to use:

`/nyl/apps/spark2/current/bin/spark-submit --master yarn --deploy-mode cluster script_name.py`

> Note that the first approach by using `spark-submit` you are running on local mode. On local mode you can see on the terminal the output of the run code. By using the cluster mode, you cannot see the output of the execution. 

### The header part to write PySpark code from Atom on the remote server must be like that

```python
### import modules ###
# I think you don't need this first line:
from pyspark import SQLContext, HiveContext, SparkConf, SparkContext

### Import Modules & Read Data ###

from pyspark import SQLContext
from pyspark import SparkConf, SparkContext
from pyspark.sql import HiveContext, Row
from pyspark.sql.functions import col
from pyspark.sql.functions import udf, col, lit, countDistinct, monotonically_increasing_id
from pyspark.sql.types import LongType, StringType
from subprocess import (PIPE, Popen)
conf = (SparkConf().setAppName("cdsa123"))
sc = SparkContext(conf=conf)
sqlContext = HiveContext(sc)
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbNzM0NjE2NzU3LDIwMDUxMDAwNzcsNTE2Nj
M5NzExXX0=
-->