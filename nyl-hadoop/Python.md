


> Written with [StackEdit](https://stackedit.io/).

# Using Python code on remote server

### .bash_profile to execute Python code using Anaconda, PySpark and Scala

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
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTU0OTU3NTY0NywtMTI4MDY2OTA0OF19
-->