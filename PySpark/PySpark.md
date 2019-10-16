# PySpark Notes
---

### Start a Spark session REFERENCES:
>  - [ Complete Guide on DataFrame Operations in PySpark](https://www.analyticsvidhya.com/blog/2016/10/spark-dataframe-and-operations/)
> 


In order to actually work with Spark data frames we first need to start a Spark session to do that.
```python
%pyspark
from pyspark.sql import SparkSession
```
To actually start the Spark session let's create a variable that by convention we call `spark`. Give the `appName` whatever the name you want, in this case  `Basics`
```python
%pyspark
spark = SparkSession.builder.appName('Basics').getOrCreate()
```
Now, most likely if you just open up the notebook and you are running this command for the first time it is going to take maybe a minute or two.
### `PySpark` version
```python
%pyspark
sc.version
```
Output
```python
%pyspark
'2.2.1'
```ea a atarame
```python
 =spark.reasnpple.  ae  a fraeale    tara
    eatas e s) met
```
show()`  how DataFrame ctent
```python
inthowtrae  ase``tuti dont        

  h is  ale n ae is a f t atae
 rit a tast   eataesres          
### Create a `DataFrame`

```python
%pyspark
inputDF =spark.createDataFrame([
    (0, "This is an apple. An apple is a fruit, not a vegetable"),
    (1, "Fruits are tasty"),
    (2, "Vegatables are nasty")],
    ["id","document"])
```
### Show `DataFrame` Content
In order to show the data, use the `show()` method

Use `show(truncate=False)` to show the `DataFrame` content without column truncation:
```python
%pyspark
inputDF.show(truncate = False)
```
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
###  Show `DataFrame` schema
Use the `printSchema()` method
```python
%pyspark
df.printSchema()
```
Output:
```
root 
|-- id: long (nullable = true) 
|-- document: string (nullable = true)
```
### Read a `JSON` file:
Use the `.read` method to read different file types
```python
%pyspark
df = spark.read.json('/user/t93kqi0/people.json')
```
Now we have a data frame called `df`
### Read a `CSV` file
Use the `.read` methods to read different file types. Use `header='true'` if the data contains a header. Use `inferSchema = True` to infer data types:
```python
%pyspark
AgentRoster = spark.read.csv('/user/t93kqi0/AgentRoasterAddrs.csv', header='true', inferSchema = True)
```
Now we have a data frame called `AgentRoster`
### Export `DataFrame` in PySpark to CSV
For Apache Spark 2+, in order to save `DataFrame` into single csv file use following command:
```python
%pyspark
AgentAdrsPre.repartition(1).write.csv("/user/t93kqi0/AgentAdrsPre.csv", sep='|', header = True, mode = 'overwrite' )
```
Here `1` indicate that I need one partition of csv only. You can change it according to your requirements.  Use the `header` option if data contains header. Use the `overwrite` option if you need to overwrite a file using the same file name.

### Show `DataFrame` column names
Use the `.column`  attribute meaning you don't need to actually have to close parentheses there.
```python
%pyspark
inputDF.columns
```
Output:
```
['id', 'document']
```
It returns a Python list of all the column names
### Statistical summary of a `DataFrame`
Use `.describe` method to get a statistical summary of the DataFrame
```python
%pyspark
df.describe().show()
```
If you call `describe()` by itself you get back a DataFrame
### Select columns
```python
%pyspark
AgentAdrsPre =  AgentRoaster.select('AgentID', 'GOCode','GO')
```
### Filter the rows of a `DataFrame`
```python
%pyspark
ClientAdrs = Clients.filter(Clients.cl_sts_tp_cd == 'ACTIVE')
```
### Count the total number of observations
```python
%pyspark
ClientAdrs.count()
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
- [pyspark-udfs-and-star-expansion](https://towardsdatascience.com/pyspark-udfs-and-star-expansion-b50f501dcb7b)
- [developing-pyspark-udfs](https://medium.com/@ayplam/developing-pyspark-udfs-d179db0ccc87)
- [future-vision/spark-udfs-we-can-use-them-but-should-we-use-them](https://medium.com/future-vision/spark-udfs-we-can-use-them-but-should-we-use-them-2c5a561fde6d)

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

Let's say we want to save on the following Hive's location `tenant_insurance_cdsa` the following Pyspark `agent_demographics` table I've just created. To to that, follow this steps.

```python
%pyspark
agent_demographics.registerTempTable('temp')
hc.sql("drop table tenant_insurance_cdsa.agent_demographics purge")
hc.sql('create table tenant_insurance_cdsa.agent_demographics as select * from temp')
```
The line:
```python
hc.sql("drop table tenant_insurance_cdsa.agent_demographics purge")
```
it is just to remove an old version of the table is you want to rewrite the same table.

If you use Zeppelin or DBeaver you will see this table published here `tenant_insurance_cdsa`.

### Convert your Zeppelin notebooks to Python or any other formats. 

Our team is one of the largest users of Zeppelin notebook(Spark) and converting the zeppelin notebooks to python or any other formats (.R, .txt, .sql) is a huge challenge till now, but not anymore. I have developed a python library (command line tool) to take care of that process (with inbuilt multiple interpreter support).

Installation: 

`$ pip install Zeppi_Convert`

Anaconda Installation: 

`$ conda install pip`

`$ pip install Zeppi_Convert`

Package: [Zeppi_Convert](https://pypi.org/project/Zeppi_Convert/)

Github: [Zeppi_Convert](https://github.com/kbsriharsha/Zeppi_Convert)

From the command line, use the keyword  zeppi-convert  to convert a zeppelin notebook (.json) to any other format output format

`$  zeppi-convert  -i  <input_filename>  -o  <output_filename>  -int  <interpreter_type>`

Example1: Extract the code from all the cells and output a python file

`$  zeppi-convert  -i  mynotebook.json  -o  mypython.py`

Example2: Convert a zeppelin notebook to any text format

`$  zeppi-convert  -i  mynotebook.json  -o  myfile.txt`

Example3: Extract the code from a specific interpreter cells

`$  zeppi-convert  -i  mynotebook.json  -o  myfile.txt  -int  pyspark`

### Number of columns and number of rows on a PySpark data frame

```python
%pyspark
# Number of columns and number of rows:
print(len(mrc.columns)) 
print(mrc.count())
```
### Using `pprint` function to get the output in table manner in Zeppelin
First import all function on the following script:
```python
sc.addPyFile("hdfs:///tmp/common_functions.py")
from common_functions import *
```
Then, we can use the `pprint` function to 

```python
pprint(mrc, nrows=10)
```
The `common_functions.py` is located on GitLab here:
```
https://nylgit.newyorklife.com/T93KMZT/kuppuluri/blob/master/common_functions.py
```
### Drop one or more columns from PySpark Data Frame

```python
df1 = df0.drop('var01')
df1 = df0.drop(['var01','var02'])
```
or
```python
drop_list = ['a column', 'another column', ...]

df.select([column for column in df.columns if column not in drop_list])
```
[reference](https://stackoverflow.com/questions/29600673/how-to-delete-columns-in-pyspark-dataframe)

### Count the number of observations by variable value

```python
# Using PySpark
df.groupBy('variablename').count().show()
# Using Python with PySpark
df.toPandas()['variablename'].value_counts()
```

### 
<!--stackedit_data:
eyJoaXN0b3J5IjpbNTAwOTgxNzEwLC01Njg3NzA5OTQsLTE2Nj
M2ODk4NiwtMTY2MTcwNjg2NCwyMDQ4NDU5MTU3LDY5ODgyNDcy
NCwtNTE3MDUxOTYxLC0xMjEyODkyNDYsLTIwMDcyNTEzMDVdfQ
==
-->