


> Written with [StackEdit](https://stackedit.io/).

# ArcPy Map Automation Notes

## Resources

- [1]The last chapter of [Python For ArcGIS 1st ed. 2015 Edition](https://www.amazon.com/Python-ArcGIS-Laura-Tateosian/dp/3319183974/ref=sr_1_9?keywords=arcpy&qid=1574267660&sr=8-9) book it is quite informative. 
- [2][Python Scripting for Map Automation - ESRI - 4 hours - free - ArcMap](https://www.esri.com/training/catalog/57630437851d31e02a43f210/python-scripting-for-map-automation/)

- [3] [ArcGIS Pro ArcPy Mapping Documentation](https://pro.arcgis.com/en/pro-app/arcpy/mapping/introduction-to-arcpy-mp.htm)

## Intro

It seems that the `arcpy.mapping` module it is useful when you create only one map manually, using the GUI tool, and then by using `arcpy.mapping`, you can modify that map document programmatically. Therefore, you need to develop a first map manually for a GO office and then, automate for the remaining more than 100 offices. The following map from [2] is clear about this approach:

>_...The arcpy.mapping module has been created to automate map management and output (printing and exporting) workflows. The provided functions focus on modifying existing map layers and layout elements and are not designed as a complete map compilation system. ArcMap is the recommended system for creating **new map documents** and authoring map layers and layouts. However, the layer and layout element modification capabilities of `arcpy.mapping` allow for the creation of map products by modifying the contents of map documents. Being successful in these workflows requires careful map authoring of layers and page layout elements so that they are easily used with your scripts._

Note: the above paragraph comes from the section: _The purpose of `arcpy.mapping` and typical script scenarios_.

What we need is a Map Book, a series of pdfs with a map in each PDF page. 




### Working with objects in the map document

Reference [3]

The objective of `arcpy.mapping` is to simplify the scripting experience. Within your map document, you have many components, or objects, which you can access and change. The map document and the objects you work with inside the map, such as a north arrow or data frame, **must be created before running your script**. After you have created these objects, you can access and work with them through `arcpy.mapping`.

In the following example, a map document named `Schools.mxd` located in the `C:\Maps` folder is accessed through the `arcpy.mapping.MapDocument` class. All the properties and methods associated with the `MapDocument` object are assigned to the variable `mxd`:

```Python
mxd = arcpy.mapping.MapDocument(r"C:\Maps\Schools.mxd")
```

While the map document **cannot be created** with `arcpy.mapping`, you can use your script to access the map document and the objects it contains.

Now you can update the Author property and save your map document using the following code:

```Python
mxd.author = "GIS Department"
mxd.save()
```

### New notes about `arcpy.mp`

References:

- [ArcGIS Pro Python reference](https://pro.arcgis.com/en/pro-app/arcpy/main/arcgis-pro-arcpy-reference.htm)

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEwMzAzNDk0NDIsNDkwNjk3MDI1LC0xMj
UxNjU1ODAzLDE2MDU5MDg3MDYsNjY0MzQ2NzEyLC0yMDE3OTA0
OTMxXX0=
-->