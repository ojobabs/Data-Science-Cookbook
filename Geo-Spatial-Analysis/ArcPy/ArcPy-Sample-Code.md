


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

The following algorithm is do the following:

1. It uses the `Intersect()` function from `arcpy` to get all client locations (points) inside the local market (polygon).
2. It uses `SearchCorsor()`  function from `arcpy` to take a list of unique `[marketer_id, address_type]` pair values. We have two locations per agent, the business (location) and the residential location. Therefore, we need to create a list of unique pairs. This is the interesting part of this code. The code on the below reference web page uses one field instead of two. 
3. It uses `SearchCorsor()`  function from `arcpy` for every unique `[marketer_id, address_type]` pair, make a list of unique  distances values and get the maximum value.       

```python
# Import modules
import arcpy
import os
import time
import logging
import csv
import statistics
# Variables
# gos = ['D54', 'S27', 'V68', 'V79', 'V65', 'V73', 'V46', 'S51', 'V61', 'V56',
#        'A22', 'V42', 'D57', 'D56', 'S19', 'A64', 'S89', 'A29', 'S82', 'D07',
#        'S69', 'S75', 'S68', 'S74']
# driving_time = [20, 30, 40, 50, 60, 70, 80, 90, 100, 110, 120]
go = 'S19'
dt = 60
# Checking and changing working directory
cwd = os.getcwd()
logging.info(f'Working directory: {cwd}.')
# Setting the current workspace path
arcpy.env.workspace = "C:\\Users\\T93KQI0\\Documents\\ArcGIS\\Projects\\" \
                      "Local_Market_02\\Local_Market_02.gdb"
# Getting the current workspace path
mydir = arcpy.env.workspace
logging.info(f'Current workspace path: {mydir}.')
# Overwrite feature layers in geosdatabase
arcpy.env.overwriteOutput = True
# File locaiton
fileloc = "C:\\Users\\T93KQI0\\Documents\\Projects\\" \
          "Geospatial-Analysis\\data_output\\"
geodb = "C:\\Users\\T93KQI0\\Documents\\ArcGIS\\Projects\\" \
        "Local_Market_02\\Local_Market_02.gdb\\"
# Intersection to get all clients insided LM
input_data_1 = "Local_Market_" + go + "_" + str(dt)
input_data_2 = "clients_" + go
output_data = "clients_inside_lm_" + go + "_" + str(dt)
arcpy.analysis.Intersect([input_data_1, input_data_2],
                         output_data,
                         "ALL",
                         None,
                         "POINT")
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
    with arcpy.da.SearchCursor(output_data, ["clients_match_S19_distance_1"],
                               where_clause) as cur2:
        for row2 in cur2:
            if row2[0] not in DistList:
                DistList.append(row2[0])

    DistList.sort()
    max_height = DistList[-1]
    AllDist.append(max_height)

print(AllDist)
print(len(AllDist))
# Caluclate statistics for maximum distances for the GO
print(statistics.mean(AllDist)*0.621371)  # in miles
print(statistics.median(AllDist)*0.621371)  # in miles
print(max(AllDist)*0.621371)  # in miles
print(min(AllDist)*0.621371)  # in miles
print(statistics.stdev(AllDist)*0.621371)  # in miles
```
Reference:
- [Selecting maximum Value based on other field using ArcMap?](https://gis.stackexchange.com/questions/110392/selecting-maximum-value-based-on-other-field-using-arcmap)
<!--stackedit_data:
eyJoaXN0b3J5IjpbNzA5NTM1NjUwLC0xODUyODEyMTY5XX0=
-->