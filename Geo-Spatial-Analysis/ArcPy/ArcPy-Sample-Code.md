


> Written with [StackEdit](https://stackedit.io/).

### Remove any kind of data from geodatabase

See how we can use the `*` wildcard to remove fea:
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
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTkyMDIxMjQ2M119
-->