


> Written with [StackEdit](https://stackedit.io/).

# Creating Hexagons using ArcGIS Pro 2.2.

To label with the number of points, `Join_Count` those hexagons with more than zero points, use the following Python expression: 
 ```python
 def FindLabel ( [Join_Count] ):
    if [Join_Count] > '0':
        return [Join_Count]
 ```
You need to select Python and Advanced as part of Class. 

## Steps

1. Use zoom to layer to select the area we want to create the tessellation.
2. Open `Generate Tesselation` tool. 
	2.1. Output Feature Class: `GenerateTessellation_D54_D56_D57`. Put here the name you want.
	2.2. Extend: 	`Current Display Extent` to generate a tessallation for the screen. 
	2.3. Shape Type: `Hexagon`
	2.4. Size: `70 Square Miles` for example. You need to choose the right value.
	2.5. Spatial reference: automatically selected.  

<!--stackedit_data:
eyJoaXN0b3J5IjpbMTA2NDUwOTYyOCwtMTYzOTQ2NjEyLDYzMz
A4MDI3M119
-->