


> Written with [StackEdit](https://stackedit.io/).

# Using PySpark on the remote server

### Execute a PySpark script on the remote server

To run a PySpark script on the remote Linux (Hadoop) environment you need write the PySpark code on a `.py` Python file. You can write here Python code too. 

 ```bash
 $ spark-submit name_of_program.py
 ```

### The header part to write PySpark code from Atom on the remote server must be like that

```python
### import modules ###

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
eyJoaXN0b3J5IjpbMTk5NDk5MTM5MCwyMDA1MTAwMDc3LDUxNj
YzOTcxMV19
-->