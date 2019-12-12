
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

### 
<!--stackedit_data:
eyJoaXN0b3J5IjpbMjA3NDUwNjg3NSw4ODAzNjI3N119
-->