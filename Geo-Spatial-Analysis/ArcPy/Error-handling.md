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

```python
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

<![endif]-->

* Notes:

i. You could extend the handle_arcpy_method() wrapper to include a method to capture the run duration of the method - i.e. time.time()<[https://urldefense.proofpoint.com/v2/url?u=https-3A__stackoverflow.com_questions_7370801_measure-2Dtime-2Delapsed-2Din-2Dpython&d=DwIFAg&c=n6-cguzQvX_tUIrZOS_4Og&r=PbR4ImVx2L_irY4YCDMn5prX5On4LYYOeD7XlqHT-kSpzPWx2nd0cR-gKD-ZF7Yo&m=JN4SWc-ynjZpQmE4hVeG-ZNDkFQvkPleZf8nvogu5Fs&s=o8JZnZUtwKqIKFNrcm59_MX3DrG0fqNKa23FIAQYlbE&e=](https://urldefense.proofpoint.com/v2/url?u=https-3A__stackoverflow.com_questions_7370801_measure-2Dtime-2Delapsed-2Din-2Dpython&d=DwIFAg&c=n6-cguzQvX_tUIrZOS_4Og&r=PbR4ImVx2L_irY4YCDMn5prX5On4LYYOeD7XlqHT-kSpzPWx2nd0cR-gKD-ZF7Yo&m=JN4SWc-ynjZpQmE4hVeG-ZNDkFQvkPleZf8nvogu5Fs&s=o8JZnZUtwKqIKFNrcm59_MX3DrG0fqNKa23FIAQYlbE&e=%20) >

ii. You will also notice I use a logger for my outputs. I can send you my base for that if you'd like.

iii. As a side note, I'd recommend you switch to f-string style formatting if you are using Python 3.6+. More info<[https://urldefense.proofpoint.com/v2/url?u=https-3A__realpython.com_python-2Df-2Dstrings_-23f-2Dstrings-2Da-2Dnew-2Dand-2Dimproved-2Dway-2Dto-2Dformat-2Dstrings-2Din-2Dpython&d=DwIFAg&c=n6-cguzQvX_tUIrZOS_4Og&r=PbR4ImVx2L_irY4YCDMn5prX5On4LYYOeD7XlqHT-kSpzPWx2nd0cR-gKD-ZF7Yo&m=JN4SWc-ynjZpQmE4hVeG-ZNDkFQvkPleZf8nvogu5Fs&s=D6w5u-wh83up8ZQZGTmehfxCVrLZjfroPHoRXpHSCf8&e=](https://urldefense.proofpoint.com/v2/url?u=https-3A__realpython.com_python-2Df-2Dstrings_-23f-2Dstrings-2Da-2Dnew-2Dand-2Dimproved-2Dway-2Dto-2Dformat-2Dstrings-2Din-2Dpython&d=DwIFAg&c=n6-cguzQvX_tUIrZOS_4Og&r=PbR4ImVx2L_irY4YCDMn5prX5On4LYYOeD7XlqHT-kSpzPWx2nd0cR-gKD-ZF7Yo&m=JN4SWc-ynjZpQmE4hVeG-ZNDkFQvkPleZf8nvogu5Fs&s=D6w5u-wh83up8ZQZGTmehfxCVrLZjfroPHoRXpHSCf8&e=%20) >. It is more readable, decreases line length and less verbose to write.

1. Lastly, I'd suggest we limit the maximum drivetime variable for your calculations. Do you already have this limit in place or would the script run indefinitely until it reached the threshold?

What is the source of the road network dataset you are using in your service areas method?

Also, please send me your source for review. This will help me look at the specific logic and tooling you use to suggest targeted efficiency gains.
<!--stackedit_data:
eyJoaXN0b3J5IjpbNTk2MDA0NDFdfQ==
-->