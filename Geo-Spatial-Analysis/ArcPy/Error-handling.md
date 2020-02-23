


> Written with [StackEdit](https://stackedit.io/).


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
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE2MDQyMTk1MzJdfQ==
-->