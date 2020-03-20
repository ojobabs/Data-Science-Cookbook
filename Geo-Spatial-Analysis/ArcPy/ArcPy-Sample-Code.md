


> Written with [StackEdit](https://stackedit.io/).

### Remove any kind of data from geodatabase

See how we can use the `*` wildcard to remove data:
```python
# Use the ListFeatureClasses function to return a list 
# of feture classes.
featureclasses = arcpy.ListFeatureClasses('location*')

# Iterawte over the dictinory to print the name of each 
# feture class
for fc in featureclasses:
    arcpy.management.Delete(fc)
    print(f'Removing data from geodatabse: {fc}')
```


### Selecting maximum Value based on other field by group?

This code is grouping by one filed and then getting the max value of a numeric field for each group. `ArcPy` do not use `group by` function; therefore, yo need to write this code. This script is efficient because, first it creates a list of all unique groups of agents-locations. Then, it creates another list with the distances for each element on the first  list (agent-location) with the distances by group of agents-locations. Then, it sorts ascending the list of distances and select the last element (the maximum). 

The following algorithm is do the following:

1. It uses the `Intersect()` function from `arcpy` to get all client locations (points) inside the local market (polygon).
2. It uses `SearchCorsor()`  function from `arcpy` to take a list of unique `[marketer_id, address_type]` pair values. We have two locations per agent, the business (location) and the residential location. Therefore, we need to create a list of unique pairs. This is the interesting part of this code. The code on the below reference web page uses one field instead of two. 
3. It uses `SearchCorsor()`  function from `arcpy` for every unique `[marketer_id, address_type]` pair, make a list of unique  distances values and get the maximum value.       

Import modules
```python
# Import modules
import arcpy
import os
import time
import logging
import csv
import statistics
```
Setting variables, current work space path, overwrite feature layers in geodatabase, file location, ArcGIS Pro project location:  
```python
# Variables
go = 'S19'
dt = 60
# Checking and changing working directory
cwd = os.getcwd()
# Setting the current workspace path
arcpy.env.workspace = "C:\\Users\\T93KQI0\\Documents\\ArcGIS\\Projects\\" \
                      "Local_Market_02\\Local_Market_02.gdb"
# Getting the current workspace path
mydir = arcpy.env.workspace
logging.info(f'Current workspace path: {mydir}.')
# Overwrite feature layers in geodatabase
arcpy.env.overwriteOutput = True
# File locaiton
fileloc = "C:\\Users\\T93KQI0\\Documents\\Projects\\" \
          "Geospatial-Analysis\\data_output\\"
geodb = "C:\\Users\\T93KQI0\\Documents\\ArcGIS\\Projects\\" \
        "Local_Market_02\\Local_Market_02.gdb\\"
```
Intersection. Note that here the output is `POINT`. We want points, the location of each client as output. 
```python
# Intersection to get all clients insided LM
input_data_1 = "Local_Market_" + go + "_" + str(dt)
input_data_2 = "clients_" + go
output_data = "clients_inside_lm_" + go + "_" + str(dt)
arcpy.analysis.Intersect([input_data_1, input_data_2],
                         output_data,
                         "ALL",
                         None,
                         "POINT")
```
Create the list of lists for all unique agent-location pair. Notice that we are using `[row1[0], row1[1]]` a list of lists. We could use a list of tuples instead but, the result is the same. Also, notice we are using `if [row1[0], row1[1]] not in AgentLoc:` this line of code to get unique values in our final list of lists.
```python
# Make a list of unique [marketer_id, address_type] pair values
col1 = "clients_match_" + go + "_USER_marketer_id_1"
col2 = "clients_match_" + go + "_USER_address_type_1"
AgentLoc = []
with arcpy.da.SearchCursor(output_data, [col1, col2]) as cur1:
    for row1 in cur1:
        if [row1[0], row1[1]] not in AgentLoc:
            AgentLoc.append([row1[0], row1[1]])

print(AgentLoc)
print(len(AgentLoc))
```
Here, we follow the same approach. One of the key points here is writing correctly the where clause. This code uses two nested loops. The first one iterates over each element of `AgentLoc` list of lists. That is because we need to use `i[0]` and `i[1]` to select the first and second element of each individual list (or tuple). Notice too, that as part of the where clause, we need to use `str(agent)`. 
```python
# For every unique [marketer_id, address_type] pair, make a list of unique
# distances values and get the maximum value
AllDist = []
for i in AgentLoc:
    DistList = []
    agent = i[0]
    location = i[1]
    where_clause = "(clients_match_" + go + "_USER_marketer_id_1 \
                     = " + str(agent) + ") AND \
                     (clients_match_" + go + "_USER_address_type_1 \
                     = \'" + location + "\'" + ")"
    with arcpy.da.SearchCursor(output_data,
                               ["clients_match_" + go + "_distance_1"],
                               where_clause) as cur2:
        for row2 in cur2:
            if row2[0] not in DistList:
                DistList.append(row2[0])

    DistList.sort()
    max_height = DistList[-1]
    AllDist.append(max_height)

print(AllDist)
print(len(AllDist))
```
Finally, we calculate some statistics we will send to a CSV file. 
```Python
# Caluclate statistics for maximum distances for the GO
print(statistics.mean(AllDist)*0.621371)  # in miles
print(statistics.median(AllDist)*0.621371)  # in miles
print(max(AllDist)*0.621371)  # in miles
print(min(AllDist)*0.621371)  # in miles
print(statistics.stdev(AllDist)*0.621371)  # in miles

```
Reference:
- [Selecting maximum Value based on other field using ArcMap?](https://gis.stackexchange.com/questions/110392/selecting-maximum-value-based-on-other-field-using-arcmap)
- [`statistics`](https://docs.python.org/3/library/statistics.html#module-statistics "statistics: Mathematical statistics functions")  — Mathematical statistics functions
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTYyNTM3MzQ0NywxOTc0MzUxNDgyLC0xOD
UyODEyMTY5XX0=
-->