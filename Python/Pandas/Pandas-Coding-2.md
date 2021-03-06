


> Written with [StackEdit](https://stackedit.io/).


### [How to calculate mean values grouped on another column in Pandas](https://stackoverflow.com/questions/30482071/how-to-calculate-mean-values-grouped-on-another-column-in-pandas)

You could  `groupby`  on  `StationID`  and then take  `mean()`  on  `BiasTemp`. To output  `Dataframe`, use  `as_index=False`

```python
In [4]: df.groupby('StationID', as_index=False)['BiasTemp'].mean()
Out[4]:
  StationID  BiasTemp
0        BB       5.0
1     KEOPS       2.5
2    SS0279      15.0
```

Without  `as_index=False`, it returns a  `Series`  instead

```python
In [5]: df.groupby('StationID')['BiasTemp'].mean()
Out[5]:
StationID
BB            5.0
KEOPS         2.5
SS0279       15.0
Name: BiasTemp, dtype: float64
```

Read more about  `groupby`  in this pydata  [tutorial](http://pandas.pydata.org/pandas-docs/stable/groupby.html).

### Replace all spaces in column names with underscores

```python
df.columns = df.columns.str.strip().str.replace(' ', '_')
```

### [How to split data into 3 sets (train, validation and test)?](https://stackoverflow.com/questions/38250710/how-to-split-data-into-3-sets-train-validation-and-test)

The following function was written to handle seeding of randomized set creation. You should not rely on set splitting that doesn't randomize the sets.

```python
import numpy as np
import pandas as pd

def train_validate_test_split(df, train_percent=.6, validate_percent=.2, seed=None):
    np.random.seed(seed)
    perm = np.random.permutation(df.index)
    m = len(df.index)
    train_end = int(train_percent * m)
    validate_end = int(validate_percent * m) + train_end
    train = df.ix[perm[:train_end]]
    validate = df.ix[perm[train_end:validate_end]]
    test = df.ix[perm[validate_end:]]
    return train, validate, test
```

Demonstration

```python
np.random.seed([3,1415])
df = pd.DataFrame(np.random.rand(10, 5), columns=list('ABCDE'))
df

train, validate, test = train_validate_test_split(df)

train

validate

test
```

### [Get list from pandas dataframe column](https://stackoverflow.com/questions/22341271/get-list-from-pandas-dataframe-column)

Pandas DataFrame columns are Pandas Series when you pull them out, which you can then call  `x.tolist()`  on to turn them into a Python list. Alternatively you cast it with  `list(x)`.

```python
import pandas as pd

d = {'one' : pd.Series([1., 2., 3.],     index=['a', 'b', 'c']),
    'two' : pd.Series([1., 2., 3., 4.], index=['a', 'b', 'c', 'd'])}

df = pd.DataFrame(d)

print("Starting with this dataframe\n", df)

print("The first column is a", type(df['one']), "\nconsisting of\n", df['one'])

dfToList = df['one'].tolist()

dfList = list(df['one'])

dfValues = df['one'].values

print("dfToList is", dfToList, "and it's a", type(dfToList))
print("dfList is  ", dfList,   "and it's a", type(dfList))
print("dfValues is", dfValues, "and it's a", type(dfValues))
```

The last lines return:

```python
dfToList is [1.0, 2.0, 3.0, nan] and it's a <class 'list'>
dfList is   [1.0, 2.0, 3.0, nan] and it's a <class 'list'>
dfValues is [ 1.  2.  3. nan] and it's a <class 'numpy.ndarray'>
```

[This question](https://stackoverflow.com/questions/14822680/convert-python-dataframe-to-list)  might be helpful. And the  [Pandas docs](http://pandas.pydata.org/pandas-docs/stable/dsintro.html)  are actually quite good once you get your head around their style.

So in your case you could:
```python
my_list = df["cluster"].tolist()
```
and then go from there.

### Append at the beginning of the list

```python
a = 5
li = [1, 2, 3]
[a] + li  # Don't use 'list' as variable name.
```
output 
```
[5, 1, 2, 3]
```

### Append at the end of the list
```python
a = 5
li = [1, 2, 3]
li.append(a)  # Don't use 'list' as variable name.
```
output 
```
[1, 2, 3, 5]
```

### Export a correlation matrix to a .CSV file

```python
def corr_matrix(file_name):
    df = pd.read_csv('master_train_test/train_' + file_name + '.csv')
    corr = df.corr()
    corr.to_csv('model_output/corr_' + file_name + '.csv')

corr_matrix('K')
corr_matrix('KC')
corr_matrix('KCP')
```

### [Pythonic way to print list items](https://stackoverflow.com/questions/15769246/pythonic-way-to-print-list-items)

How to print the whole content of a super long list:

Assuming you are using Python 3.x:

```Python
print(*myList, sep='\n')
```

### Fill `NaN` values in a columns with the value of another column

```python
# Replace NaN values in Variable Definition by Feature values

matching3['Variable_Definition'] = matching3['Variable_Definition'].fillna(matching3['Feature'])
```

### Replace  underscore by space in pandas dataframe

```python
matching3['Variable_Definition'] = matching3['Variable_Definition'].replace(regex=['_'], value=' ')
```
[more](http://www.datasciencemadesimple.com/replace-a-substring-of-a-column-in-pandas-python/) 

### [Set order of columns in pandas dataframe](https://stackoverflow.com/questions/41968732/set-order-of-columns-in-pandas-dataframe)

Just select the order yourself by typing in the column names. Note the double brackets:

```python
frame = frame[['column I want first', 'column I want second'...etc.]]
```

### [how would you make a comma separated string from a list of strings](https://stackoverflow.com/questions/44778/how-would-you-make-a-comma-separated-string-from-a-list-of-strings)

```python
myList = ['a','b','c','d']
myString = ",".join(myList )
```

This won't work if the list contains numbers.

As  [Ricardo Reyes](https://stackoverflow.com/users/3399/ricardo-reyes)  suggested, if it contains non-string types (such as integers, floats, bools, None) then do:

```python
myString = ','.join(map(str, myList)) 
```

### Add a header to a pandas series

Using `names  = ['marketer_id']` we can add a header to a pandas series 

```python
train_targetMaster = pd.read_csv('target/data_output/train_targetMaster.csv', names = ['marketer_id'])
```

### Best way to concatenate (merge horizontally) two pandas dataframes

```python
train_data = pd.concat([train_targetMaster, train], axis=1)
```
### Loop through the elements of a matrix
Let's say we have matrix with the following elements
```
0:0 0:1 0:2
1:0 1:1 1:2
2:0 2:1 2:2
```
Using Numpy:

```python
x = np.arange(0,3)
a = np.repeat(x, 3).reshape(3,3)
b = np.arange(3)

for x, y in np.nditer([a,b]):
    print("%d:%d" % (x,y), end=' ')
```
output:
```
0:0 0:1 0:2 1:0 1:1 1:2 2:0 2:1 2:2 
```

Another example, to get:

```
1:1 1:2 1:3 1:4 1:5 1:6 1:7 
2:1 2:2 2:3 2:4 2:5 2:6 2:7 
3:1 3:2 3:3 3:4 3:5 3:6 3:7 
4:1 4:2 4:3 4:4 4:5 4:6 4:7 
5:1 5:2 5:3 5:4 5:5 5:6 5:7 
6:1 6:2 6:3 6:4 6:5 6:6 6:7 
```
We can use:

```python
x = np.arange(1,7)
a = np.repeat(x, 7).reshape(6,7)
b = np.arange(1,8)
for x, y in np.nditer([a,b]):
    print("%d:%d" % (x,y), end=' ')
```


references: [1]([https://docs.scipy.org/doc/numpy/reference/arrays.nditer.html](https://docs.scipy.org/doc/numpy/reference/arrays.nditer.html)), [2]([https://docs.scipy.org/doc/numpy/reference/generated/numpy.repeat.html](https://docs.scipy.org/doc/numpy/reference/generated/numpy.repeat.html)).

### Cap target for at 99.5% percentile

#### Calculate 99.5th percentile
```python
train['adj_fyc'].quantile(0.995)
```
Output:
```
156332.76600655002
```
####  Cap `adj_fyc` at 156332
```python
maxVal = 156332.76600655002

train['adj_fyc'] = train['adj_fyc'].where(train['adj_fyc'] <= maxVal, maxVal)
```
#### Let's check
```python
train = train.sort_values(by=['adj_fyc'])

train.tail(100)
```
References:

- [Set maximum value upper bound in pandas dataframe](https://stackoverflow.com/questions/40836208/set-maximum-value-upper-bound-in-pandas-dataframe)
- [Pandas find percentile stats of a given column](https://stackoverflow.com/questions/39581893/pandas-find-percentile-stats-of-a-given-column)

### List unique values in a pandas column

```python
#List unique values in the df['name'] column
df.name.unique()
```
### [How to us mean and sum opperatiors with groupby on different columns at the same time](https://stackoverflow.com/questions/48909110/python-pandas-mean-and-sum-groupby-on-different-columns-at-the-same-time)
Let's say we have the following Pandas datafra:

```
Name    Missed    Credit    Grade
A       1         3         10
A       1         1         12      
B       2         3         10
B       1         2         20
```
And we want to get this:
```
Name    Sum1   Sum2    Average
A       2      4      11
B       3      5      15 
```
We can use:

```python
df = (df.groupby('Name', as_index=False)
       .agg({'Missed':'sum', 'Credit':'sum','Grade':'mean'})
       .rename(columns={'Missed':'Sum1', 'Credit':'Sum2','Grade':'Average'}))
print (df)
```
to get this:
```
  Name  Sum1  Sum2  Average
0    A     2     4       11
1    B     3     5       15
```
Or we can use:

```python
d = {'Missed':'Sum1', 'Credit':'Sum2','Grade':'Average'}
df=df.groupby('Name').agg({'Missed':'sum', 'Credit':'sum','Grade':'mean'}).rename(columns=d)
print (df)
```
To get this:
```
      Sum1  Sum2  Average
Name                     
A        2     4       11
B        3     5       15
```

Another example of aggregate
```python
agg_vars = ['fyp_low', 'fyp_medium', 'fyp_high', 'zipcode_taxable_income_low',
            'zipcode_taxable_income_medium', 'zipcode_taxable_income_high']

end = life_county.groupby(['client_address_county'], as_index=False)[agg_vars].agg('sum')
```


### [delete rows containing numeric values in strings from pandas dataframe](https://stackoverflow.com/questions/50804036/delete-rows-containing-numeric-values-in-strings-from-pandas-dataframe)

Let's say we have the following Pandas dataframe:
```
       text type
       abc    b
    abc123    a
       cde    a
  abc1.2.3    b
     1.2.3    a
       xyz    a
    abc123    a
      9999    a
     5text    a
      text    a
```

```python
df[~df.text.str.contains(r'[0-9]')]
```
We get:

```
   text type
   abc    b
   cde    a
   xyz    a
  text    a
```

### Create a new column based on if then conditions

```python
# Implementation Target 2 Rolling 12 months creation:

def target2Def(df):
    if df['target1Rolling'] == 0:
        return 'Low'
    elif (df['target1Rolling'] == 1 and df['cncl_cd'] == 'QC') or (df['target1Rolling'] == 1 and df['cncl_cd'] == ""):
        return 'Medium'
    else:
        return 'High'

targetAux02['target2Rolling'] = targetAux02.apply(target2Def, axis=1)
``` 

### Count the number of value per category

Here `smg` is a Pandas dataframe. We can use the pandas `.unique()` function on this `smg` Pandas dataframe:

```python
smg['PreviousOccupation'].unique()
```
Another example with Pandas' `value_counts()` function:

```python
smg['PreviousOccupation'].value_counts()
```
Output:

```
Unemployed 				 	3004 
Business/Finance/Banking 	1902 
Retail Salesperson 			1736 
Office/Admin Support 		1650 
Insurance Sales/Broker 		1529 
```
### Groupby one column and return the mean of only particular column in the group

```python
df.groupby('A')['B'].mean()
```
[pandas.core.groupby.GroupBy.mean](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.core.groupby.GroupBy.mean.html)


**[Extract first n Characterss from left of column in pandas]([http://www.datasciencemadesimple.com/return-first-n-character-from-left-of-column-in-pandas-python/](http://www.datasciencemadesimple.com/return-first-n-character-from-left-of-column-in-pandas-python/))**

**str[:n]**  is used to get first n characters of column in pandas
```python
df1['StateInitial'] = df1['State'].str[:2]
```

### [Remove duplicates by columns a keeping the row with the highest](https://stackoverflow.com/questions/12497402/python-pandas-remove-duplicates-by-columns-a-keeping-the-row-with-the-highest)

```python
df.drop_duplicates()
```

### Remove decimal points (.0) from string and add leading zeros to the string

```python
# The markeger_id is a strg type variable and contains decimal points such as
# `.0` for some obs. Therefore, first, we need to remove those decimals.
# MRD table uses leading 0 for marketer_id. We need to add zeros up to 7 fig.
mrd_index_nodup['marketer_id'] = mrd_index_nodup['marketer_id'].str.strip().str.replace('.0', '').str.zfill(7)
```
More:

#### [How to add leading zero formatting to string in Pandas?](https://stackoverflow.com/questions/33651668/how-to-add-leading-zero-formatting-to-string-in-pandas)

### [Python with Pandas: Convert String to Float and other Numeric Types](https://wellsr.com/python/python-convert-pandas-dataframe-string-to-float-int/)

#### Pandas Convert String to Float

```python
import pandas as pd
import numpy as np  # To use the int64 dtype, we will need to import numpy
cols = ['Homework', 'Midterm', 'Project']
for col in cols:
	grades[col] = grades[col].astype(dtype=np.float64)
```
#### Pandas Convert String to Int

```python
import pandas as pd
import numpy as np  # To use the int64 dtype, we will need to import numpy
grades["StudentID"] = grades["StudentID"].astype(dtype=np.int64)
```
[Reference](https://wellsr.com/python/python-convert-pandas-dataframe-string-to-float-int/)

The column `markeger_id` contains strings like `0002345` or `       NaN`. We want to remove the rows with `       NaN` values on that column.

### Filter out observations with `NaN` as part of a string column 
```python
mrd_index_nodup = mrd_index_nodup[mrd_index_nodup['marketer_id'].str.contains("NaN") == False]
```
### Convert floats to integers

```python
mrd_county['County_Res'] = mrd_county['County_Res'].apply(np.int64)
```

This solution doesn't work is you have `NaN` values. 

### Save into a text file a list of values

```python
test_val = mat02['marketer_id'].unique()

with open('../data/unique_marketers.txt', 'w') as f:
    for item in test_val:
        f.write("%s\n" % item)
f.close()       
 ```

### Cleaning a difficult string variable 

```python
# The markeger_id is a strg type variable an contains two differnt types of
# variable format: 1234567.0 or 1234567 and can be somethinglike 1234.0 or
# like this 0034567.
#
# There are values like this
# 438912.0
# 0117085
# 0089964
# 0000944
# 0TASAGT
# 0000032
# 72658.0
# 0142150
#
# - There decimal values to remove .0
# - We need to remove all leading 0, could be  0, 00, 000, etc.
# - There is a unique problematique value to remove 0TASAGT
# - Finally, we need to add leading zeros up to 7 figures


# mat02['marketer_id'] = mat02['marketer_id'].str.strip(
# ).str.replace('.0', '').str.zfill(7)
# https://stackoverflow.com/questions/38706813/how-to-remove-a-substring-of-string-in-a-dataframe-column
# Don't use replace('.0', ''), the . is not recognized as part of the sring and all
# are going to be removed. you need to use replace('\.0', '') instead
#mat02['marketer_id'] = mat02['marketer_id'].str.strip().str.replace('.0', '').str.lstrip("0").str.zfill(7)

test_sample = mat02.head(30)

print(test_sample)

test_sample['marketer_id'] = test_sample['marketer_id'].str.strip(
).str.replace("\.0", "").str.lstrip("0").str.zfill(7)

print(test_sample)
```
More here
- [how-to-remove-a-substring-of-string-in-a-dataframe-column](https://stackoverflow.com/questions/38706813/how-to-remove-a-substring-of-string-in-a-dataframe-column)
- [strip-lstriprstrip-strip-function-python](http://www.datasciencemadesimple.com/strip-lstriprstrip-strip-function-python/)
- [python-remove-character-from-string](https://www.journaldev.com/23674/python-remove-character-from-string)


### [Q: [Pandas] How to efficiently assign unique ID to individuals with multiple entries based on name in very large df](https://stackoverflow.com/questions/45685254/q-pandas-how-to-efficiently-assign-unique-id-to-individuals-with-multiple-ent)

```python
# Create an id variable. One id value for each marketer_id
agent_final['id'] = agent_final.groupby(['marketer_id']).ngroup()
```
Output
```
    marketer_id  life_sales_low_premium  life_sales_medium_premium  life_sales_high_premium  annuities  calendar_year   Cultural_Market      Age Tenure  County_Res     id
0         0000032                     4.0                        1.0                      5.0        2.0         2016.0       UNSPECIFIED  60 - 65   > 11     55009.0      0
1         0000151                     0.0                        0.0                      3.0        NaN         2016.0       UNSPECIFIED  40 - 45   > 11     55025.0      1
2         0000175                     0.0                        1.0                      1.0        3.0         2016.0       UNSPECIFIED  60 - 65   > 11     36103.0      2
3         0000197                     0.0                        1.0                      2.0        2.0         2016.0       UNSPECIFIED  45 - 50   > 11     19061.0      3
4         0000223                     0.0                        0.0                      1.0        NaN         2016.0             OTHER  45 - 50   > 11     24031.0      4
5         0000227                     4.0                        1.0                      1.0        4.0         2016.0       UNSPECIFIED  45 - 50   > 11     19111.0      5
6         0000281                     1.0                        1.0                      0.0        5.0         2016.0       UNSPECIFIED  55 - 60   > 11     20091.0      6
```

### Read first rows bit txt file

```python
N = 10
with open("../data/hhpsp_1949714001_1.txt") as myfile:
    head = [next(myfile) for x in range(N)]
print(head)
```
```
['cl_id_no|PFX_NM|first_name|middle_initial|LST_NM|SFX_NM|STR_ONE_AD|STR_TWO_AD|CTY_AD|ST_CD|ZIP_CD|PSP_FLAG|PSP_CODE\n', '000001003||GWENDOLYN|B|MEYERS||145 HAZELWOOD DR||WASHINGTON|PA|15301|H|20\n'
, '000001005||MINA||NATZMER||2 ORCHARD CT||ESSEXVILLE|MI|48732|H|34\n', '000001015||JOHN|J|HOCHSTETLER||2050 OAK HILL RD||WOOSTER|OH|44691|H|08\n', '000001018||JOSEPH|A|CULKIN|JR|32 JOLLY LN||LEVITTO
WN|PA|19055|A|51\n', '000001026||FRANKLYN|D|RICKER||438 BEAGLE RD||BLISSFIELD|MI|49228|H|56\n', '000001030||THOMAS|H|RYAN||12885 7 MILE RD NE||BELDING|MI|48809|H|32\n', '000001034||THOMAS||BOSTON||PO
 BOX 232|NULL|NEW MATAMORAS|OH|45767|7|56\n', '000001037||LEWIS|R|HERTZOG|JR|167 N BINGAMAN ST||READING|PA|19606|A|31\n', '000001042||SHIRLEY|J|HALL||1280 AYCLIFFE LN||CUYAHOGA FLS|OH|44221|H|42\n']
[t93kqi0@ha20p0014rs src]
```
- [read-first-n-lines-of-a-file-in-python](https://stackoverflow.com/questions/1767513/read-first-n-lines-of-a-file-in-python)

### How to Convert String to Integer in Pandas DataFrame

In this guide, I’ll show you two methods to convert a string into an integer in pandas DataFrame:

**(1) The astype(int) method:**
```python
df['DataFrame Column'] = df['DataFrame Column'].astype(int)
```
**(2) The to_numeric method:**
```python
df['DataFrame Column'] = pd.to_numeric(df['DataFrame Column'])
```
Reference: [String-to-integer-dataframe](https://datatofish.com/string-to-integer-dataframe/)

[https://stackoverflow.com/questions/17950374/converting-a-column-within-pandas-dataframe-from-int-to-string](https://stackoverflow.com/questions/17950374/converting-a-column-within-pandas-dataframe-from-int-to-string)
[https://cmdlinetips.com/2018/02/how-to-subset-pandas-dataframe-based-on-values-of-a-column/](https://cmdlinetips.com/2018/02/how-to-subset-pandas-dataframe-based-on-values-of-a-column/)

### [Pandas make new column from string slice of another column](https://stackoverflow.com/questions/25789445/pandas-make-new-column-from-string-slice-of-another-column)

```python
# Create a new column wit the first 5 digits in comp_gcode
# The first 5 digits represents the county
# First transform comp_code into string
PSYCLE_Premier_CY['county_gcode'] = PSYCLE_Premier_CY['comp_gcode'].apply(str)
# Second get the firt 5 digits from the string
PSYCLE_Premier_CY['county_gcode'] = PSYCLE_Premier_CY['county_gcode'].str[:6]
```


### [Converting a column within pandas dataframe from int to string](https://stackoverflow.com/questions/17950374/converting-a-column-within-pandas-dataframe-from-int-to-string)

### Remove an item from a list in Python (clear, pop, remove, del)

In Python, use  `list`  methods  `clear()`,  `pop()`, and  `remove()`  to remove items from a list. It is also possible to delete items using  `del`  statement by specifying a position or range with an index or slice.

-   Remove all items:  `clear()`
-   Remove an item by index and get its value:  `pop()`
-   Remove an item by value:  `remove()`
-   Remove items by index or slice:  `del`

You can find specific examples here:

[python-list-clear-pop-remove-del](https://note.nkmk.me/en/python-list-clear-pop-remove-del/)

One example:

```python
# Remove the county_gcode column from the list
all_cols.remove('county_gcode')
```

### [summarising-aggregation-and-grouping-data-in-python-pandas](https://www.shanelynn.ie/summarising-aggregation-and-grouping-data-in-python-pandas/)

### [Python pandas dataframe to dictionary](https://stackoverflow.com/questions/18695605/python-pandas-dataframe-to-dictionary)

I've a two columns dataframe, and intend to convert it to python dictionary - the first column will be the key and the second will be the value. Thank you in advance.

Dataframe:

```
    id    value
0    0     10.2
1    1      5.7
2    2      7.4
```
See the docs for  [`to_dict`](http://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.to_dict.html). You can use it like this:

```python
df.set_index('id').to_dict()
```

And if you have only one column, to avoid the column name is also a level in the dict (actually, in this case you use the  `Series.to_dict()`):

```python
df.set_index('id')['value'].to_dict()
```



### [Pandas DataFrame column to list [duplicate]](https://stackoverflow.com/questions/23748995/pandas-dataframe-column-to-list)
  
Use  `.values`  to get a  `numpy.array`  and then  `.tolist()`  to get a list.

For example:

```python
import pandas as pd
df = pd.DataFrame({'a':[1,3,5,7,4,5,6,4,7,8,9],
                   'b':[3,5,6,2,4,6,7,8,7,8,9]})
```

Result:

```python
>>> df['a'].values.tolist()
[1, 3, 5, 7, 4, 5, 6, 4, 7, 8, 9]
```

or you can just use

```python
>>> df['a'].tolist()
[1, 3, 5, 7, 4, 5, 6, 4, 7, 8, 9]
```

To drop duplicates you can do one of the following:

```python
>>> df['a'].drop_duplicates().values.tolist()
[1, 3, 5, 7, 4, 6, 8, 9]
>>> list(set(df['a'])) # as pointed out by EdChum
[1, 3, 4, 5, 6, 7, 8, 9]
```

### Use a list of values to select rows from a pandas `DataFrame`
There are two ways to do this. If one of them does not work you can try with the other:
```python
# Create table for all GOs includd in this experiments
go_list = ['D54', 'S27', 'V68', 'V79', 'V65', 'V73', 'V46', 'S51', 'V61',
           'V56', 'A22', 'V42', 'D57', 'D56', 'S19', 'A64', 'S89', 'A29',
           'S82', 'D07', 'S69', 'S75', 'S68', 'S74', 'D18', 'D21', 'S96',
           'A41', 'A48', 'A37', 'V69']
# First option: 
table_go = offices[offices['go_cd'].isin(go_list)]
# Second option:
table_go = offices[offices['go_cd'] in go_lis]
```
References:
- [Use-a-list-of-values-to-select-rows-from-a-pandas-dataframe](https://stackoverflow.com/questions/12096252/use-a-list-of-values-to-select-rows-from-a-pandas-dataframe)

### Create a new column in a `DataFrame`

```python
# Let's add a new variable go_cd_nm we need in this context
offices['go_cd_nm'] = offices['go_cd'] + "-" + offices['GO_NM']
```
### Read a `.csv` file
```python
exp1 = pd.read_csv('data_output/lm_06_network.csv')
```
### List all column names in a `DataFrame`
```python
# List all columns in the df
cols = [col for col in exp1.columns]
print(cols)
```
Output:
```
['go', 'numCliInsideOne', 'numCliTotalOne', 'prcClientsInsideOne', 'drivingTimeOne', 'popDenOne', 'methodOne']
```
### Rename columns in a `DataFrame`
```python
# Rename variable the columns to surprese blank spaces and suffix for exp one
exp1Fix = exp1.rename(index=str, columns={' numCliInside': 'numCliInsideOne',
                                        ' numCliTotal': 'numCliTotalOne',
                                        ' prc_clients_inside': 'prcClientsInsideOne',
                                        ' driving_time': 'drivingTimeOne',
                                        ' pop_den': 'popDenOne',
                                        ' method': 'methodOne',})
```
### Drop Duplicated lines in a `DataFrame`
```python
# Drop all duplicated records
print(len(exp1Fix))
exp1Fix = exp1Fix.drop_duplicates()
print(len(exp1Fix))
```
### List all unique values from a `DataFrame` column
```python
# Create a list with all go_cd_nm values
gos = [value for value in expOneTwo['go_cd_nm'].unique()]
print(gos)
```
Output:
```
['D54-KANSAS', 'S27-GR. SAN FRANCISCO', 'V68-QUEENS']
```
### Aggregate by one column and get the average for several columns
```python
# Aggregate by drivingTimeOne per prcClientsInsideOne, numCliInsideOne, and popDenOne
# and calculate the mean for the three variables
columns = ['prcClientsInsideOne', 'numCliInsideOne', 'popDenOne']
lm_exp_agg_raw = expOneTwo.groupby('drivingTimeOne', as_index=False)[columns].mean()
```
### Calculate the percentage change between rows for a `DataFrame`

```python
# Include percentage change One
lm_exp_agg_raw['prcChangeOne'] = lm_exp_agg_raw['numCliInsideOne'].pct_change(periods=1)
lm_exp_agg_raw.round(4)
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbNjU2NTI4ODk2LC0yMTIzMTc5NzU4LC0yMD
Y1OTEzOTc2LC04NTMzMDYyODUsNjQxOTk1OTYsODY4NjQ5Mjk3
LC0xNzMyNTE0NDE2LC0xNjczNzg1MTgyLC0yMzcwNjc2ODAsMj
Q5ODUzNTU1LDE2NDQyODI2ODYsMzUyNzIwNTE1LDI1Nzk2OTEx
NywxNjMzNjA3OTY2LDEyNTA3NTc5MzksLTIwNjM0NjkyNDUsLT
EwNzYwNTgzNSwtNTMzNjY4MDYyLDg3NjMxNjgyLDU1MzcxMjkx
M119
-->