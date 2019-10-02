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
Now we can get access to tables on Hive (DBeaver)

```python
%pyspark
# Import table tenant_insurance_cdsaagy.mrd_agency_itr1 built by Harsha for Agency.
agents = hc.sql(
    """
    select marketer_id,  calendar_year, title_type_name, active_status_src, class_description 
	from tenant_insurance_cdsaagy.mrd_agency_itr1
	where marketer_id = '0123019'
	order by calendar_date
	""")
```
### To start using Python with Pyspark

```python
%pyspark
# Import Python libraries
import pandas as pd
import numpy as np
pd.set_option('display.max_columns', 1000)
pd.set_option('display.max_rows', 1000)
pd.set_option('display.width', 1000)
```
### Using `show()`

```python
%pyspark
agents.show(truncate = False)
```
### Importing tables from HDFS
```python
%pyspark
# Import a Spark session:
from pyspark.sql import SparkSession
```
```python
%pyspark
spark = SparkSession.builder.appName('nlp').getOrCreate()
```
Now we can create a PySpark dataframe:

```python
%pyspark
smg = spark.read.csv("/user/t93kqi0/smg.csv", header = True, inferSchema = True)
```

### Using a Python Pandas function with a PySpark dataframe

Here `smg` is a PySpark dataframe. We can use the pandas `.unique()` function on this `smg` PySpark dataframe using before `.toPandas()`:

```python
%pyspark
smg.toPandas()['PreviousOccupation'].unique()
```
Another example with Pandas' `value_counts()` function:

```python
smg.toPandas()['PreviousOccupation'].value_counts()
```
Output:

```
Unemployed 				 	3004 
Business/Finance/Banking 	1902 
Retail Salesperson 			1736 
Office/Admin Support 		1650 
Insurance Sales/Broker 		1529 
```

### Select some column on a PySpark dataframe

```python
%pyspark
# Select some columns
smgId =  smg.select('MKTRNUM', 'CONTRACTDT', 'PreviousOccupation', 'education', 'graduate', 'week_earn')
```
### Convert a PySpark dataframe into a Python Pandas dataframe
```python
%pyspark
# Let's convert smgId PySpark dataframe into a Python Pandas dataframe
smgIdP = smgId.toPandas() 
```
### Convert a Python Pandas dataframe into a PySpark dataframe
```python
%pyspark
# From Pandas DF to PySpark DF
df = spark.createDataFrame(smgIdP)
```
### Variable types in PySpark dataframe
```python
%pyspark
allAgents.dtypes
```
Output
```
[('marketer_id', 'string'), ('calendar_year', 'string'), ('fyc', 'decimal(26,2)')]
```
### Total obs. in a PySpark dataframe
```python
%pyspark
allAgents.count()
```
### Left Join with PySpark dataframes
```python
%pyspark
# Left join to add allAgents to df
left_join = df.join(allAgents, df.marketer_id == allAgents.marketer_id,how='left') # Could also use 'left_outer'
left_join.show(truncate = False)
```
More here: [Pyspark joins by example](http://www.learnbymarketing.com/1100/pyspark-joins-by-example/)
### Using a User Defined Function UDF in PySpark
Here an example of an UDF. 
- `aux00` is the input table
- `aux01` is the output table
- We want to create a new variable named `Ret_CC` on the `aux01` table. The `Ret_CC` variable takes the values `1` or `0` conditioned to the value of the variable `class_description` on table `aux00`. Because `class_description` has leading and trailing spaces we use `if Current Class' in class_description:`.  
```python
%pyspark
def def_status(class_description):
    if 'Current Class' in class_description:
        status = 1
    else:
        status = 0
    return status

udf_trail_1 = F.udf(def_status)

aux01 = aux00.select('*', udf_trail_1((col('class_description'))).alias('Ret_CC'))

aux01.show()
```
References:

- [User-Defined Functions - Python](https://docs.databricks.com/spark/latest/spark-sql/udf-python.html)
- [How to Turn Python Functions into PySpark Functions (UDF)](https://changhsinlee.com/pyspark-udf/)

Let's compare the above PySpark function to the equivalent function using Python:

```python
def labelValuesEdu(df):
    if df['education'] == 1:
        return 'college or university'
    elif df['education'] == 0:
        return 'high school or trade school'
    else:
        return 'unknown'

merge['education'] = merge.apply(labelValuesEdu, axis=1)
merge.head()
```
Another example in Python with many level:
```python
def labelValuesWeek(df):
    if df['week_earn'] == 1:
        return 'Less than $500'
    elif df['week_earn'] == 2:
        return '$500 to $1,000'
    elif df['week_earn'] == 3:
        return '$1,001 to $1,500'
    elif df['week_earn'] == 4:
        return '$1,501 to $2,000' 
    elif df['week_earn'] == 5:
        return 'Greater than $2,000'         
    else:
        return 'unknown'

merge['week_earn'] = merge.apply(labelValuesWeek, axis=1)
merge.head()
```

### How to publish a PySpark dataframe on Hive (DBeaver)

```python
%pyspark
agent_demographics.registerTempTable('temp')
hc.sql("drop table tenant_insurance_cdsa.agent_demographics purge")
hc.sql('create table tenant_insurance_cdsa.agent_demographics as select * from temp')

```

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTMyNzA4MjIwNiwxMTc5NzQ5NjczLC04Mz
Q1ODcyMjMsLTU4Nzk1NjkzOSwtOTQwMzk5MjAyXX0=
-->