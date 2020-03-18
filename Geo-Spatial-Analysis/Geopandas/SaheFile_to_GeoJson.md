


> Written with [StackEdit](https://stackedit.io/).

### How to install GeoPandas in Windows

You need to follow the steps on this webpage to install GeoPandas and all its dependencies on a Windows machine. 

- [Using geopandas on Windows](https://geoffboeing.com/2014/09/using-geopandas-windows/)

### How to plot a GeoJson with MapPlotLib

- [Getting Started on Geospatial Analysis with Python, GeoJSON and GeoPandas](https://www.twilio.com/blog/2017/08/geospatial-analysis-python-geojson-geopandas.html)

- [Plot a GeoJSON map using GeoPandas](https://medium.com/@h4k1m0u/plot-a-geojson-map-using-geopandas-be89e7a0b93b)

- [Plotting GeoJson Files with Matplotlib](https://medium.com/@tmango/plotting-geojson-files-with-matplotlib-5ed87df570ab)

### How to create a GeoJson file from a ShapeFile

- [Shapefile into geojson conversion python 3](https://stackoverflow.com/questions/43119040/shapefile-into-geojson-conversion-python-3)

Importing libraries:
```python
import shapefile
from json import dumps
import geopandas as gpd
import seaborn as sns
import warnings
import matplotlib.pyplot as plt
from shapely.geometry import Point
import descartes
%matplotlib inline
```
Read ShapeFile:

```python
# read the shapefile
reader = shapefile.Reader("cb_2018_us_state_5m.shp")
fields = reader.fields[1:]
field_names = [field[0] for field in fields]
buffer = []
for sr in reader.shapeRecords():
    atr = dict(zip(field_names, sr.record))
    geom = sr.shape.__geo_interface__
    buffer.append(dict(type="Feature", geometry=geom, properties=atr)) 
```
Write the GeoJson file:
```python
# write the GeoJSON file
geojson = open("cb_2018_us_state_5m.geojson", "w")
geojson.write(dumps({"type": "FeatureCollection", "features": buffer}, indent=2) + "\n")
geojson.close()
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE3NzYyMjk0ODJdfQ==
-->