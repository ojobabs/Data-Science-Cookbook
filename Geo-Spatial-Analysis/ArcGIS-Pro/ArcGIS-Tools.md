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

Aim: once we have the local market 
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTM5NzEwMDMwMCwtMjc3NzE5NTksLTk5NT
Y5ODE0MiwxODQ3ODkzNDk1LC0xNzE2MzkyNDM5LDE1OTE0Mjc2
NDYsLTEwOTkyODk3NDhdfQ==
-->