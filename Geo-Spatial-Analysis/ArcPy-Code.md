
> Written with [StackEdit](https://stackedit.io/).

# ArcPy Notes

### Create a search cursor using an SQL expression

```python
cursor = arcpy.da.SearchCursor(fc, ('OBJECTID', 'Shape', 'SOURCE_ID', 'CLUSTER_ID', 'PROB', 'OUTLIER', 'EXEMPLAR', 'STABILITY', 'COLOR_ID'), """"CLUSTER_ID" <> -1""")

for row in cursor:
    print(row)
```


<!--stackedit_data:
eyJoaXN0b3J5IjpbODgwMzYyNzddfQ==
-->