
> Written with [StackEdit](https://stackedit.io/).

# ArcPy Notes

### Create a search cursor using an SQL expression

```python
cursor = arcpy.da.SearchCursor(fc, ('OBJECTID', 'Shape', 'SOURCE_ID', 'CLUSTER_ID', 'PROB', 'OUTLIER', 'EXEMPLAR', 'STABILITY', 'COLOR_ID'), """"CLUSTER_ID" <> -1""")

for row in cursor:
    print(row)
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

```
cursor = arcpy.da.SearchCursor( fc, '*')
cursor.fields

### 
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTM3MTAxNjcxOCw4ODAzNjI3N119
-->