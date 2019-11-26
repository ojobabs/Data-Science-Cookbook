


> Written with [StackEdit](https://stackedit.io/).

# Using Python code on remote server

### .bash_profile to execute Python code using Anaconda, PySpark and Scala on the remote server

```bash
# .bash_profile 

# Get the aliases and functions
if [ -f ~/.bashrc ]; then
        . ~/.bashrc
fi

# User specific environment and startup programs

PATH=$PATH:$HOME/.local/bin:$HOME/bin

export PATH
export PYSPARK_DRIVER_PYTHON=/nyl/apps/anaconda3/bin/python

export PYSPARK_PYTHON=/nyl/apps/anaconda3/bin/python
export SPARK_HOME=/nyl/apps/spark2/spark_2_3_2_1
export PYTHON3=/nyl/apps/anaconda3/bin
export PATH=$PYTHON3/:$SPARK_HOME/:$PATH
export PATH=/nyl/apps/spark2/spark_2_3_2_1/bin:$PATH:/nyl/apps/anaconda3/bin/
PATH=/usr/local/R_3_4_3/bin:$PATH
export PATH
```

### Executing a Python script on the remote server

Just use on the remote terminal:

```bash
$ python program-name.py
```

### Using Matplotlib package to create, save and see images on the remote server

How to use matplotlib package to create and save images on the remote server (Hadoop). By using the Atom's [ftp-remote-edit](https://atom.io/packages/ftp-remote-edit) it is possible to actually open the image on Atom to see the content. 

```python
# This is an example code about how to save matplotlib images on
# the remote Linux server (R-Edge Node)
# If you are using Atom with the package https://atom.io/packages/ftp-remote-edit
# you can actually open and see the image on the remote Linux server.
# Reference about how to write matplotlib code to save the image:
# https://stackoverflow.com/questions/35737116/runtimeerror-invalid-display-variable

# Import modules
import pandas as pd
import numpy as np
import matplotlib

matplotlib.use('agg')
import matplotlib.pyplot as plt

X = [590,540,740,130,810,300,320,230,470,620,770,250]
Y = [32,36,39,52,61,72,77,75,68,57,48,48]

plt.scatter(X,Y)

plt.savefig('scatterPlot.png')
```

### An example about creating plots using GeoPandas

To create maps using GeoPandas you need to use:

```python
matplotlib.pyplot.switch_backend('agg')
``` 
instead of 

```python
matplotlib.use('agg')
```
As we did above when using matplotlib. 

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

```

## Import libraries on remote server

```python
# Import modules
import pandas as pd
import numpy as np
import matplotlib
matplotlib.use('agg')
import matplotlib.pyplot as plt
import warnings
warnings.filterwarnings('ignore')
from pathlib import Path
from pathlib import Path

# Load the datasets

data_folder = Path("../data/")

mat02 = data_folder / "mat02.csv"

# Loading matc02

mat02 = pd.read_csv(mat02)

print(mat02)

print(len(mat02))
```


<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE0MDA5NTUxODksLTE0MjY0MDU4MDcsOD
A5Njc0NDE3LC0yMDg3NjI5ODMwLC0xMjgwNjY5MDQ4XX0=
-->