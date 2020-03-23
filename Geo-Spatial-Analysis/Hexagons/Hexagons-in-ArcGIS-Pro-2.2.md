


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

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTMwNjMzNTA2Myw2MzMwODAyNzNdfQ==
-->