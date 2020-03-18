


> Written with [StackEdit](https://stackedit.io/).

This code is a GeoPandas example using NYL Data Hub environment:

```python
# Load all importance packages
import matplotlib.pyplot as plt
import geopandas
import numpy as np
import pandas as pd
from shapely.geometry import Point

#import missingno as msn

import seaborn as sns
from pathlib import Path
import warnings
import matplotlib
warnings.filterwarnings('ignore')
# Choose the number of columns to display
pd.set_option('display.max_columns', 20)

# Getting to know GEOJSON file:

country = geopandas.read_file("../spatial/tl_2018_us_county/")
print(country.head())

print(type(country))

print(type(country.geometry))

print(type(country.geometry[0]))

#re-projecting to WGS84
country = country.to_crs({'init': 'epsg:3857'})
# http://geopandas.org/projections.html#re-projecting
# world.to_crs(epsg=3395) would also work
# Google uses Web Mercator 3857
# WGS84 EPSG 4326

matplotlib.pyplot.switch_backend('agg')

country.plot()

plt.savefig('../imgs/country.png')

# Exclude Alaska and Hawaii for now Alska and Hawaii and others
# https://www.nrcs.usda.gov/wps/portal/nrcs/detail/?cid=nrcs143_013696
country[country['STATEFP'].isin(['02', '15', '60', '66', '69', '72', '78']) == False].plot(
    figsize=(30, 20), color='#3B3C6E')

plt.savefig('../imgs/continental_usa.png')

# GO locations

go = geopandas.read_file("../spatial/GO-Sales-Territories/")
print(go.head())

go = go.to_crs({'init': 'epsg:3857'})

matplotlib.pyplot.switch_backend('agg')

go.plot()

plt.savefig('../imgs/go.png')

# GO locations

#go = geopandas.read_file("../spatial/GO_Addr_v081017")
#print(go.head())
#
#go = go.to_crs({'init': 'epsg:3857'})
#
#matplotlib.pyplot.switch_backend('agg')
#
#go.plot()
#
#plt.savefig('../imgs/go_offices.png')
#
## SLS locations
#
#go = geopandas.read_file("../spatial/SLS_Addr_v081017")
#print(go.head())
#
#go = go.to_crs({'init': 'epsg:3857'})
#
#matplotlib.pyplot.switch_backend('agg')
#
#go.plot()
#
#plt.savefig('../imgs/sls_offices.png')

```
<!--stackedit_data:
eyJoaXN0b3J5IjpbMzM1NDcxMzMzXX0=
-->