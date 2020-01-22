


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

When using the Python window inside ArcGIS Pro, you don't need to import `arcpy`. 

Let's create an `aprx` project from the current project:

```python
aprx = arcpy.mp.ArcGISProject("CURRENT")
```

A property of `aprx` is the active map that returns a map object. And a property of a map is its name. So, we can print the name for the active map for this project. 

```python
print(aprx.activeMap.name)
```
Output:
```
Map
```
We can rename the active map:

```python
aprx.activeMap.name = "Main Map"
```
Now you can see that the name of the active map changed to "Main Map" instead of "Map".

```python
print(aprx.activeMap.name)
```
Output:
```
Main Map
```
Let's insert a new basemap using the ribbon. Now the new basemap is active. We can rename the basemap:
```python
aprx.activeMap.name = "Overview Map"
```
The active basemap has been renamed. 

The `activeMap` property is read only. So, we cannot use `arcpy` to change which map is active. 

Notice that the catalog pane has a Map folder. Here we have the two mpas. The `aprx` object has a method to list these maps:
```python
print(aprx.listMaps())
```
output:
```
[<arcpy._mp.Map object at 0x000000000032CDE6D8>, <arcpy._mp.Map object at 0x000000000032CDE8D8>]
```
But this list the maps objects without showing the name. To do that we can use list comprehension:

```python
print([map.name for map in aprx.listMaps()])
```
Output:**strong text**
```
['Overview Map', 'Main Map']
```
To look for a map in the list of maps using its name, and to create a map object to work with, we can  use a search to support wildcards and an index. 
```python
mainMap = aprx.listMaps("Main Map")[0]
```
Now that we have a map object named `mainMap`, we can use it a base map method to change the basemap to a light gray canvas. 
```python
mainMap.addBasemap("Light Gray Canvas")
```
We will be over the map that was active. So, to see the change we made to the Main Map view we need to click its tab. Now, if you open the Main Map you can see that the basemap now is light gray canvas. 

To find the names of all other available base maps use the ribbon. Look into the base map gallery. 

We can create, for example, a second map object for the Overview Map and change the base map.
```python
overviewMap = aprx.listMaps("Overview Map")[0]
```
The Overview Map currently has no layers, 


###  My project

- So far I am not sure if you can create maps automatically or you need to create each map using the ribbon. 
- For whatever the reason, I cannot use Atom to add layers to the map. 

```python
aprx = arcpy.mp.ArcGISProject("CURRENT")
print(aprx.activeMap.name)
```
Output 
```
Map1
```

```python
aprx.activeMap.name = "S51"
# check name of active map
print(aprx.activeMap.name)
```
Output 
```
S51
```

```python
# Rename second map
aprx.activeMap.name = "Map2"
aprx.activeMap.name = "S57"
# List all maps names
print([map.name for map in aprx.listMaps()])
```
Output
```
['S51', 'S57']
```
```Python
# Create a map object to work with
S51Map = aprx.listMaps("S51")[0]
```

### Add layers to a map

The layers are added at the bottom. So, first you need to add the layer you one at the bottom, for example the local market, then the agents and then the GO offices.

```python
# Add local market layer to the S51Map
lyrFile = r"C:\Users\T93KQI0\Documents\ArcGIS\Projects\Local_Market_Map_Auto_01\Local_Market_Map_Auto_01.gdb\Polygons_Pop_Den_S51"
S51Map.addDataFromPath(lyrFile)
```
Output
```
<arcpy._mp.Layer object at 0x00000000298E8E80>
````

```python
# Add agents to S51Map
lyrFile=r"C:\Users\T93KQI0\Documents\ArcGIS\Projects\Local_Market_Map_Auto_01\Local_Market_Map_Auto_01.gdb\marketers_S51"
S51Map.addDataFromPath(lyrFile)
```
Output
```
<arcpy._mp.Layer object at 0x00000000723701D0>
```

```python
# Add office location layer to the S51Map
lyrFile = r"C:\Users\T93KQI0\Documents\ArcGIS\Projects\Local_Market_Map_Auto_01\Local_Market_Map_Auto_01.gdb\offices_all_Geocoded"
S51Map.addDataFromPath(lyrFile)
```
Output
```
<arcpy._mp.Layer object at 0x00000000770B3518>
```

Let's add layers to S57 map. You don't need to active S57 map to add layers to this map. 

> Adding layers from `ServiceArea_S51` it is not possible.

```python
lyrFile = r"C:\Users\T93KQI0\Documents\ArcGIS\Projects\Local_Market_Map_Auto_01\Local_Market_Map_Auto_01.gdb\Polygons_Pop_Den_S57"
S57Map.addDataFromPath(lyrFile)
```
Output
```
<arcpy._mp.Layer object at 0x000000002A82DA90>
```

```python
lyrFile = r"C:\Users\T93KQI0\Documents\ArcGIS\Projects\Local_Market_Map_Auto_01\Local_Market_Map_Auto_01.gdb\marketers_S57"
S57Map.addDataFromPath(lyrFile)
```
Output 
```
<arcpy._mp.Layer object at 0x000000006A9AD630>
```

```python
lyrFile = r"C:\Users\T93KQI0\Documents\ArcGIS\Projects\Local_Market_Map_Auto_01\Local_Market_Map_Auto_01.gdb\offices_all_Geocoded"
S57Map.addDataFromPath(lyrFile)
```
Output
```
<arcpy._mp.Layer object at 0x000000006A9AD358>
```

## Lesson 48 Working with Layout and Map Frame classes

let's see what you can and cannot do with `arcpy.md` when you are working with layouts and map frame objects. 

`arcpy` can not be used to insert a layout, so, we need to use we need to use the ribbon. Insert a layout. 

A layout is a white page of pager where you can put multiple layers to create your final map. You can add multiple layouts to your project and each layout can include multiple maps. These multiple maps can appear in multiple layouts too. 

The map element type, that provides the link between which view of the map appears on each layout is called **map frame**.

The first element that I place on my layout will be the S57 map and this cannot be done using code. On the ribbon, insert, then map frame, then S51, the one on the right.

Now that we have a layout and a data frame on it we can start using `arcpy`. 

Let's create now a layout object. We have only one layout for now so, it is easy:

```python
lyt = aprx.listLayouts()[0]
```

Now we can list the elements methods of the layout object to create a map frame object which I'll call `S51MapFrame`. Again, there is only one map frame so we can use index 0. 

```python
lyt = aprx.listLayouts()[0]
S51MapFrame = lyt.listElements('MAPFRAME_ELEMENT')[0]
```
I used it in an interactive map frame element to return only map frame elements because there are many different types of elements and objects that may be found in a layout like legends, text, arrows, scrollbars, etc. 

Let's change the name of the map frame from `map frame` to `S51MapFrameMain`: 

```python
S51MapFrame.name = "S51MapFrameMain"
```

I would now like to use code to start moving and resizing the `S51MapFrame` map frame on my layout. But before doing that I need to know where the anchor point is for the map frame. This cannot be done using code. So go the contents pane and right click the `S51MapFrameMain` to open  properties. Got to the placement tab, and there we can see nine little squares that indicate the possible anchor points with the lower left one colored in blue to indicate its position. I laid the anchor points lower left. But if I had wanted to change it then I could have done so by clicking on one of the alternative anchor points. At the moment, the lower left corner of the main map frame is at 25 millimeters in from the left edge of the last page and 25 millimeters up from the bottom. I move on the format map frame pane over to the left using code so that I can see the properties change.

keep open the properties windows to see how the values change with code. 

I want to make some more room at the bottom of the layout for some other map elements like an overview map and so I'll set the element position y property of the main map frame to be 50. The main frame is going off the page. So, I can reduce to be 45. 

```python
S51MapFrame.elementPositionY = 45
```
I'd also like to move it a bit to the left. So I'll set the L and in position X property of the main map frame to be 15:

```python
S51MapFrame.elementPositionX = 15
```
and I would also like to leave some room on the right hand side of the layout. So I will reduce the element width of the map frame to 150.

```python
S51MapFrame.elementHeight = 150
```

I would like a second frame on my layout but first I'll close the format frame pane. I will insert a new map frame. 

I will create a new map to create an overview map we can use as a second map on the layout. I need to use the ribbon to add a new map. Let's rename the new map.

We can list all maps to see that the new `Map` is there:

```python
# List all maps names
print([map.name for map in aprx.listMaps()])
['Map', 'S51', 'S57']
```
Let's change the name:
```python
# Create a overview map object to work with 
OverviewMap = aprx.listMaps("Map")[0]
# Change the name of the map
OverviewMap.name = "Overview"
```
> Note that following the above code, we can create multiple maps using the ribbon, `Map`, `Map1`, `Map2`, ... . `Map100`, and then use code to rename all of then with the right and unique name. The same for the layouts. 

Now on the overview map we can add the location of each GO office. 

```python
# Add local market layer to the OverviewMap
lyrFile = r"C:\Users\T93KQI0\Documents\ArcGIS\Projects\Local_Market_Map_Auto_01\Local_Market_Map_Auto_01.gdb\offices_all_Geocoded"
OverviewMap.addDataFromPath(lyrFile)
```
> Maybe we can create a square around the query we are working to signal where is our GO office.  

Next, I changed the symbol by using the ribbon. I am using a house symbol to represent. Also, I added the GO code using the ribbon too. 

**Min 7:08 on video**

> **Best approach to automate map creation**:  use  a unique default map and a unique default layout and then include there the layers we want . The loop through each layer. So, you can have a Main map (link on the video) and an Overview map (like on the video) and just loop through each every layer we need to add every time to create each GO map.  
> Update: probably, this above approach won't work because we need to add the Map Frame (the actual map) to the layout by using the ribbon. There is no way to use code for this. 

Now, by using the ribbon, we can add the `OverviewMap`. 

Let's create a map frame object first for the `OverviewMap`:
```python
OverviewMapFrame = lyt.listElements('MAPFRAME_ELEMENT',"Map Frame")[0]
```
I use the current name of that map frame which is map frame as a wildcard to search for it in the list of map frame elements in the layout. To be sure I have the right map frame I'll use its visibility property to turn it off. 
```python
OverviewMapFrame.visible = False
```
Now we can back to visible:
```python
OverviewMapFrame.visible = True
```
I'll change his name to be `OverviewMap` map frame.
```python
OverviewMapFrame.name = "Overview Map Frame"
```
I'd like to place the lower right corner of this map frame 15 millimeters in from the right hand page to the page and 15 millimeters up from the bottom. First are trying is anchor point to the lower right by opening the properties of the "Overview Map Frame" map frame. We can see that it's position Y is 25 millimeters but 115 millimeters. So I'll set that using code. 
```python
OverviewMapFrame.elementPositionY = 15
```
To work out with 50 millimeters from the right hand it is also tracked that from the page width of the layout. 
```python
OverviewMapFrame.elementPositionX = lyt.pageWidth - 15
```











<!--stackedit_data:
eyJoaXN0b3J5IjpbLTg0NTQ3MTgwNyw5MzI0MTI2MTIsMTY2ND
k5ODU5MywtNTY0NTIwMjEyLDQzOTA4NDUwNiwtMTgwOTE2ODQ5
MywtNDc3OTI5NjksNzI1NTc5NzExLC0xNjIyOTg0NDk4LDIwMj
Q5NTQ2OTcsMTU2MTYyNDExMiwxNTg0NjI1NTY4LDU3OTI1Nzkw
OSwxNjg1MzI2MjMwLDE5MjUzNDM0OCw5MDIwMTM0NzksLTE2OD
A5NjEyNzAsLTQ4NjEwODQxNiwtMTIyNzQ0NjE2OCwtMjAzNDk4
Njc5Nl19
-->