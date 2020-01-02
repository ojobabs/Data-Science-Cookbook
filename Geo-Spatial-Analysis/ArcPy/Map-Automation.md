


> Written with [StackEdit](https://stackedit.io/).

# ArcPy Map Automation Notes

## Resources

- [1]The last chapter of [Python For ArcGIS 1st ed. 2015 Edition](https://www.amazon.com/Python-ArcGIS-Laura-Tateosian/dp/3319183974/ref=sr_1_9?keywords=arcpy&qid=1574267660&sr=8-9) book it is quite informative. 
- [2][Python Scripting for Map Automation - ESRI - 4 hours - free - ArcMap](https://www.esri.com/training/catalog/57630437851d31e02a43f210/python-scripting-for-map-automation/)

## Intro

It seems that the `arcpy.mapping` module it is useful when you create only one map manually, using the GUI tool, and then by using `arcpy.mapping`, you can modify that map document programmatically. Therefore, you need to develop a first map manually for a GO office and then, automate for the remaining more than 100 offices. The following map from [2] is clear about this approach:

>_...The arcpy.mapping module has been created to automate map management and output (printing and exporting) workflows. The provided functions focus on modifying existing map layers and layout elements and are not designed as a complete map compilation system. ArcMap is the recommended system for creating **new map documents** and authoring map layers and layouts. However, the layer and layout element modification capabilities of `arcpy.mapping` allow for the creation of map products by modifying the contents of map documents. Being successful in these workflows requires careful map authoring of layers and page layout elements so that they are easily used with your scripts._
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTM4NTQxNjQ4NywtMjAxNzkwNDkzMV19
-->