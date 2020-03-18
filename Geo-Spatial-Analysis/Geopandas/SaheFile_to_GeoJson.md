


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
Let's see the data

```python
states = gpd.read_file('cb_2018_us_state_5m.geojson')
print(states.head())
````
Output
```
  STATEFP   STATENS     AFFGEOID GEOID STUSPS          NAME LSAD  \
0      31  01779792  0400000US31    31     NE      Nebraska   00   
1      53  01779804  0400000US53    53     WA    Washington   00   
2      35  00897535  0400000US35    35     NM    New Mexico   00   
3      46  01785534  0400000US46    46     SD  South Dakota   00   
4      48  01779801  0400000US48    48     TX         Texas   00   

          ALAND       AWATER  \
0  198956658395   1371829134   
1  172112588220  12559278850   
2  314196306401    728776523   
3  196346981786   3382720225   
4  676653171537  19006305260   

                                            geometry  
0  POLYGON ((-104.05351 41.15726, -104.05267 41.2...  
1  MULTIPOLYGON (((-122.32834 48.02134, -122.3217...  
2  POLYGON ((-109.05017 31.48000, -109.04984 31.4...  
3  POLYGON ((-104.05770 44.99743, -104.05021 44.9...  
4  POLYGON ((-106.64548 31.89867, -106.64084 31.9...
```
The `descartes` package is required for plotting polygons in geopandas. 
```python
ax = states.plot(color='blue')
```
Output
```
the output is a map of the US with all the states
```

We can use [geojson.io](http://geojson.io/#map=3/53.64/-115.49) to plot your GeoJson file too. 

The following code does not work due to the company's firewall:

```python
# import geojsonio
# geojsonio.display(states)
```
But, if you but the content of the geojson file on the webpage, you get the map of all U.S. states too.
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE2NDk2Nzc2MTNdfQ==
-->