> Written with [StackEdit](https://stackedit.io/).

# ArcGIS Pro Tools Reference

### Clip Tool

The `Input Features` must be the larger layer. The following video explain that clearly:

- [How to Clip a Data Layer in ArcMap 10](https://www.youtube.com/watch?v=6UF0l8Ly2U4)

### Export data in geodatabase: Export a feature layer to a shapefile

To export a feature layer that is part of a geodatabase to a shapefile outside of the geodatabase, go to Catalog, select the feature layer to export, and then select export and then select `Feature Class(es) To Shapefile(s)`.

- [Export data in a geodatabase](https://pro.arcgis.com/en/pro-app/help/data/geodatabases/overview/export-data.htm)

### Obtaining all block groups withing the service area

There are two approaches to get the block groups within the calculated service area:

1. Using clip or intersection tool
2. Using [select by location](http://desktop.arcgis.com/en/arcmap/10.3/map/working-with-layers/using-select-by-location.htm)

By using select by local we have the operators `intersect`, `are within` or `are completely within` to select block groups that intersect with the service are or are withing the service area.

### Density-based Clustering: DBSCAN, HDBSCAN and OPTICS

- [Denisty-based Clustering in ArcGIS PRO](https://pro.arcgis.com/en/pro-app/tool-reference/spatial-statistics/densitybasedclustering.htm)
- [How density-based clustering works ArcGIS Pro](https://pro.arcgis.com/en/pro-app/tool-reference/spatial-statistics/how-density-based-clustering-works.htm)
- [A clear explanation of DBSCAN on YouTube](https://www.youtube.com/watch?v=6jl9KkmgDIw)
- [Another clear explanation of DBSCAN on YouTube](https://www.youtube.com/watch?v=sKRUfsc8zp4)
- [Brian Kent: Density Based Clustering in Python](https://www.youtube.com/watch?v=5cOhL4B5waU). This person has an interesting master or phd thesis about density based clustering [here](https://www.cmu.edu/dietrich/psychology/cognitiveaxon/documents/kent_dissertation.pdf). Also, he wrote some python packages. 

### Transfer local market to a standard geography (block-group)

Aim: once we have the local market polygone obtained by using the Network Analysis tool, we need to translate that polygone into a standard geography - block group level. To to this there are at least two options:

1. Use the [Enrich Layer](https://pro.arcgis.com/en/pro-app/tool-reference/analysis/enrich-layer.htm) tool.  I am using as input the Local Market layer inside the ServiceArea folder. 

- For D21 (New Orleans) the population density is 2399.5. 
- For D18 (Louisiana) the population denis 

2. First, we can download from the U.S. Census Bureau the block-group geometry  shapefiles for each State and then doing a spatial join or something link that get the right shapefile.
3. The ideal tool is [Generate Geographies from Overlay]([https://pro.arcgis.com/en/pro-app/tool-reference/business-analyst/generate-geographies-from-overlay.htm](https://pro.arcgis.com/en/pro-app/tool-reference/business-analyst/generate-geographies-from-overlay.htm)) . But as you can see [here]([https://pro.arcgis.com/en/pro-app/get-started/whats-new-in-arcgis-pro-2-3.htm](https://pro.arcgis.com/en/pro-app/get-started/whats-new-in-arcgis-pro-2-3.htm)) only exist on ArcGIS Pro 2.3. Our current version is 2.2.3. 
4. There is another option, using the [ArcGIS Living Atlas of the World](https://livingatlas.arcgis.com/en/browse/#d=2&q=%22ACS%20Population%20Variables%20-%20Boundaries%22), but the [available layer](https://www.arcgis.com/home/item.html?id=f430d25bf03744edbb1579e18c4bf6b8) doesn't come at Block-Group level.
5. The ideal tool is . But as you can see [here]([https://pro.arcgis.com/en/pro-app/get-started/whats-new-in-arcgis-pro-2-3.htm](https://pro.arcgis.com/en/pro-app/get-started/whats-new-in-arcgis-pro-2-3.htm)) only exist on 
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTA0NzA0NjA3LDEwNzU3MzE3MjcsMTEzNj
E3OTQ0LC0xMDg4MjUzODczLC0xNzE5MDc2MTUxLDc2MTIxNTY4
OCwtMjc3NzE5NTksLTk5NTY5ODE0MiwxODQ3ODkzNDk1LC0xNz
E2MzkyNDM5LDE1OTE0Mjc2NDYsLTEwOTkyODk3NDhdfQ==
-->