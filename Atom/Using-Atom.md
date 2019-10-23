


> Written with [StackEdit](https://stackedit.io/).

# Using Atom

### Multiple Selectors and Incremental Search

- CTRL + D every time you hit CTRL + D it starts highlighting every single term. Now we can updated in every single place we had it selected. 

The process of finding every single one of these instances is called incremental search and to initiate that you usually highlight over it or you can just hover your mouse over it and every time you hit CTRL + D it will find the next instance. 

Using CTRL + D works really well when we only have a few instances and we really want to find a partial amount of them. 

However, if the file much bigger, we probably want to do an entire select.  And to do that we can use 

[https://flight-manual.atom.io/using-atom/sections/editing-and-deleting-text/](https://flight-manual.atom.io/using-atom/sections/editing-and-deleting-text/)

### Using Snippets

Open the Command Palette using 

```cson
# Your snippets
#
# Atom snippets allow you to enter a simple prefix in the editor and hit tab to
# expand the prefix into a larger code block with templated values.
#
# You can create a new snippet in this file by typing "snip" and then hitting
# tab.
#
# An example CoffeeScript snippet to expand log to console.log:
#
# '.source.coffee':
#   'Console log':
#     'prefix': 'log'
#     'body': 'console.log $1'
#
# Each scope (e.g. '.source.coffee' above) can only be declared once.
#
# This file uses CoffeeScript Object Notation (CSON).
# If you are unfamiliar with CSON, you can read more about it in the
# Atom Flight Manual:
# http://flight-manual.atom.io/using-atom/sections/basic-customization/#_cson
'.source.python':
  'loadLibraries':
    'prefix': 'libraries'
    'body': """
    # Import modules
    import pandas as pd
    import numpy as np
    import matplotlib
    matplotlib.use('agg')
    import matplotlib.pyplot as plt
    import warnings
    warnings.filterwarnings('ignore')
    from pathlib import Path
    """
  'headerCommentaries':
    'prefix': 'header'
    'body': """
    # PROJECT NAME : NYU-Capstone-project
    # CODE NAME: `data_prep_02.py`
    # AUTHOR: Marcos Keyser
    # AIM: Subset South Central zone counties
    #
    # INPUT DATA:
    #
    # - `/data/data_01.csv`
    #
    # The above data is the output of the code `src/data_prep_01.py`
    #
    # OUTPUT DATA:
    #
    # - `/data/data_02.csv`
    #
    # The bove data is the input of the code `data_prep_02.py`
    """
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTk3NjA1MTYyOCwxMjc0NjM0NDI0LDkzMD
E0OTU5MywtMTEwNTY1MTgyMl19
-->