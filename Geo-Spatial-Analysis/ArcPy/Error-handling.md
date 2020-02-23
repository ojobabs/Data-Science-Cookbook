> Written with [StackEdit](https://stackedit.io/).



1. Separate any processes that can generate semi-permanent intermediary files and write them to disk. Do not create them during each iteration.

* For example, split your geocoding processes and write the output to a feature class stored within a file geodatabase.

* Ideally we would store this data in an Enterprise Geodatabase housed in a true RDBMS (such as MSSQL Server, Postgres or Oracle)

* Avoid personal geodatabases (archaic Access databases), shapefiles (better for shipping data than storing)

2. Avoid in memory for most datasets. Write outputs to a scratch geodatabase to keep memory clean and available.

3. Get the script working with a single GO. Let's remove the overhead of batch processing until we have a more efficient base script.

4. You can explore using SelectLayerByAttribute_management and DeleteFeatures_management<[https://desktop.arcgis.com/en/arcmap/10.3/tools/data-management-toolbox/delete-features.htm](https://desktop.arcgis.com/en/arcmap/10.3/tools/data-management-toolbox/delete-features.htm)> in place of a large Update cursor. However, it is likely that DeleteFeatures is using a cursor under the hood.

* Always use the Data Access module cursors. The older cursors are deprecated.

* Try to use a where clause when instantiating the cursor to minimize the size of the iteration

5. I try to wrap my ArcPy functions with another function that allows me to log output, run duration, etc. For example:

* Wrapper:

```python
def handle_arcpy_method(func, msg, logging=True):
	'''
	ArcPy method wrapper for error catching

	Arguments:
	func {function} -- Lambda: arcpy.method to be wrapped
	msg {string} -- Message to be logged

	Keyword Arguments:
	logging {bool} -- Enables logging for method (default: {True})

	Returns:
	object -- ArcPy results object
	'''
	if logging:
		logger.info(f'{msg} : Start')
	try:
		res = func()
	except arcpy.ExecuteError:
		logger.error(arcpy.GetMessages(2))
	if logging:
		logger.info(f'{msg} : Complete')
	return res
```	


* Example use:
def delete_object(in_obj):
'''
Deletes a given object (if exists)

Arguments:
in_obj {obj} -- Object to delete
'''

if arcpy.Exists(in_obj):
handle_arcpy_method(
lambda: arcpy.Delete_management(in_obj),
f'Delete existing {in_obj}.'
)
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbNzc2MzY5ODAwXX0=
-->