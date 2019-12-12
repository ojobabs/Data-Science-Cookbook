
> Written with [StackEdit](https://stackedit.io/).

# ArcPy Notes

## Coursor 

```python
import arcpy, traceback

fc = "agent_add_D21_HDBSCAN_3"
```

### Create a cursor

```python
cursor = arcpy.da.SearchCursor(fc, ['OBJECTID', 'SOURCE_ID', 'CLUSTER_ID'])
```

### Get an individual row

```python
row = cursor.next() # Get an individual row.
row
```
Output
```
(1,1,2)
```
```python
row[0]
row[1]
row[2]
```
Output
```
1
1
2
```

### List all columns

```python
cursor = arcpy.da.SearchCursor( fc, '*')
cursor.fields
```
Output
```
('OBJECTID',
 'Shape',
 'SOURCE_ID',
 'CLUSTER_ID',
 'PROB',
 'OUTLIER',
 'EXEMPLAR',
 'STABILITY',
 'COLOR_ID')
```

### Print the columns of non-geometry non-OID type fields

```python
# Purpose: Print the names of the non-geometry non-OID type
# fields in the input fi le and the value of these
# fields for each record.
# Usage: No script arguments required.
import arcpy
def excludeFields(table, types=[]):
    '''Return a list of fi elds minus those with
       specifi ed fi eld types'''
    fieldNames = []
    fds = arcpy.ListFields(table)
    for f in fds:
        if f.type not in types:
            fieldNames.append(f.name)
    return fieldNames

fc =  "agent_add_D21_HDBSCAN_3"
excludeTypes = ['Geometry', 'OID']
fields = excludeFields(fc, excludeTypes)

with arcpy.da.SearchCursor(fc, fields) as cursor:
    print(cursor.fields)
    for row in cursor:
        print(row)
del cursor
```
Output
```
('SOURCE_ID', 'CLUSTER_ID', 'PROB', 'OUTLIER', 'EXEMPLAR', 'STABILITY', 'COLOR_ID')
(1, 2, 0.13966654011486504, 0.860333459885135, 0, 0.10807001979793433, 2)
(2, 3, 1.0, 0.2651596113994749, 0, 0.15219890050512608, 3)
(3, 3, 1.0, 0.0, 1, 0.15219890050512608, 3)
(4, 2, 0.31609223743405734, 0.6839077625659427, 0, 0.10807001979793433, 2)
(5, 3, 0.18904310607590302, 0.810956893924097, 0, 0.15219890050512608, 3)
(6, 5, 1.0, 0.0, 1, 0.09670983111632385, 5)
```

### Use a SQL query to delete some rows

Let's use a SQL query to delete all rows with `CLUSTER_ID = -1`:

```python
# Purpose: Use a SQL query to select specifi c records.
# Usage: No script arguments needed.
import arcpy, traceback
fc = "agent_add_D21_HDBSCAN_4"
# Create the where_clause
query = "CLUSTER_ID = -1"
try:
    cursor = arcpy.da.UpdateCursor(fc, ['SOURCE_ID', 'CLUSTER_ID', 'PROB', 'OUTLIER', 'EXEMPLAR', 'STABILITY', 'COLOR_ID'], query)
    for row in cursor:
        # Delete this row
        cursor.deleteRow()
        print('Deleted row {0}'.format(row))
    del cursor
except:
    print('An error occurred.')
    traceback.print_exc()
    del cursor
```
Output 

```
Deleted row [25, -1, 0.0, 0.02736943623959565, 0, 0.0, -1]
Deleted row [39, -1, 0.0, 0.8898103180271066, 0, 0.0, -1]
Deleted row [40, -1, 0.0, 0.5447587747526182, 0, 0.0, -1]
Deleted row [56, -1, 0.0, 0.9537611017678214, 0, 0.0, -1]
Deleted row [71, -1, 0.0, 0.012435188764603276, 0, 0.0, -1]
Deleted row [78, -1, 0.0, 0.9453512660486557, 0, 0.0, -1]
Deleted row [96, -1, 0.0, 0.6057312926052147, 0, 0.0, -1]
Deleted row [101, -1, 0.0, 0.08899598854111698, 0, 0.0, -1]
Deleted row [122, -1, 0.0, 0.5415491974278095, 0, 0.0, -1]
Deleted row [127, -1, 0.0, 0.9856162736860503, 0, 0.0, -1]
Deleted row [132, -1, 0.0, 0.8934058794012835, 0, 0.0, -1]
Deleted row [208, -1, 0.0, 0.9857215217045456, 0, 0.0, -1]
Deleted row [249, -1, 0.0, 0.8888859616483176, 0, 0.0, -1]
Deleted row [254, -1, 0.0, 0.13813251782084476, 0, 0.0, -1]
Deleted row [257, -1, 0.0, 0.0016212826972500116, 0, 0.0, -1]
Deleted row [287, -1, 0.0, 0.4678036009205707, 0, 0.0, -1]
Deleted row [300, -1, 0.0, 0.9469689202718985, 0, 0.0, -1]
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTcwNjc4Mjc1MCwyMDc0NTA2ODc1LDg4MD
M2Mjc3XX0=
-->