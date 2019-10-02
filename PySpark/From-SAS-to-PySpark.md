> Written with [StackEdit](https://stackedit.io/).
## From SAS to PySpark
Notes about how to transcribe SAS code into PySpark code.

### How to create a SAS data set using SAS
Using the `datalines` option it is possible to create a SAS data set using code:
```sas
data df;
    input id year sales;
    datalines;
    0 2015 100
    1 2016 200
    2 2017 300 
    ;
run;
```
### How to create a PySpark DataFrame using PySpark
Using the `createDataFrame()` method:
```python
df =spark.createDataFrame([
    (0, 2015, 100),
    (1, 2016, 200),
    (2, 2017, 300)],
    ["id","year", "sales"])
```
### How to write a macro using SAS
The following SAS macro creates three SAS data sets:
```sas
%macro sales (year=);
data df_&year;
	set df;
	if year = &year then output;
run;
%mend sales;

%sales(year=2015);
%sales(year=2016);
%sales(year=2017);
```
### How to write a SAS macro using Pyspark





Output:
```
+---+------------------------------------------------------+
|id |document                                              |
+---+------------------------------------------------------+
|0  |This is an apple. An apple is a fruit, not a vegetable|
|1  |Fruits are tasty                                      |
|2  |Vegatables are nasty                                  |
+---+------------------------------------------------------+
```

### Get access to Hive tables

```python
%pyspark
### import modules ###
from pyspark import SQLContext, HiveContext, SparkConf, SparkContext
from pyspark.sql import HiveContext, Row, Window
import pyspark.sql.functions as F
from pyspark.sql.types import LongType, StringType,DoubleType, IntegerType
from pyspark.sql.functions import isnan, when, count, col, length, max, levenshtein, datediff, to_date, lit, year, rank, month
from pyspark.sql.window import Window
hc = HiveContext(sc)
```
### To start using Pytho
<!--stackedit_data:
eyJoaXN0b3J5IjpbMjExODg1NTc5MywtOTQwMzk5MjAyXX0=
-->