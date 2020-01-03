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

### De
<!--stackedit_data:
eyJoaXN0b3J5IjpbMjEyMTkxODY4MSwxODQ3ODkzNDk1LC0xNz
E2MzkyNDM5LDE1OTE0Mjc2NDYsLTEwOTkyODk3NDhdfQ==
-->