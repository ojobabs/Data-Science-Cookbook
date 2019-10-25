


> Written with [StackEdit](https://stackedit.io/).

# Example of long and short code

## Long code

```python
# PROJECT NAME : NYU-Capstone-project
# CODE NAME: `data_prep_13.py`
# AUTHOR: Marcos Keyser
# AIM: Using `life_02.csv` (output of `data_prep_04.py`) as input table (comes
# with LIFE obs. only and `fyp` takes values `Low`, `Medium`, `High`) add (from
# code `data_prep_09.py`) the code we need to map P$ycle variables to 10 levels
# ('C3B', 'B3A', ...).
#
# INPUT DATA: Create Number of Life and Annuities by customer segment
# (10 new variables)
#
# - `/data/life_02.csv`
#
# The above data is the output of the code `src/data_prep_04.py`
#
# OUTPUT DATA:
#
# - `/data/map_segments_and_fyp.csv`
#
# The bove data is the input of the code `data_prep_13.py`

# Import modules
import matplotlib.pyplot as plt
from pathlib import Path
import warnings
import pandas as pd
import numpy as np
import matplotlib
matplotlib.use('agg')
warnings.filterwarnings('ignore')

# Load the datasets

data_folder = Path("../data/")

all = data_folder / "map_segments_and_fyp.csv"

# Loading all

all = pd.read_csv(all)

# Select variables we need

all = all[['client_address_county', 'fyp', 'psycle_segment_name']]

print(all.head())

print(len(all))

##### from code 10

# Let's create 10 new columns for ech segment

########################## psycle_segment_C3B #################################

def fypVars(df):
    if (df['psycle_segment_name'] == 'C3B' and df['fyp'] == 'Low'):
        return 1
    else:
        return 0

all['psycle_segment_C3B_pyc_Low'] = all.apply(fypVars, axis=1)

def fypVars(df):
    if (df['psycle_segment_name'] == 'C3B' and df['fyp'] == 'Medium'):
        return 1
    else:
        return 0

all['psycle_segment_C3B_pyc_Medium'] = all.apply(fypVars, axis=1)

def fypVars(df):
    if (df['psycle_segment_name'] == 'C3B' and df['fyp'] == 'High'):
        return 1
    else:
        return 0

all['psycle_segment_C3B_pyc_High'] = all.apply(fypVars, axis=1)

########################## psycle_segment_C2C #################################

def fypVars(df):
    if (df['psycle_segment_name'] == 'C2C' and df['fyp'] == 'Low'):
        return 1
    else:
        return 0

all['psycle_segment_C2C_pyc_Low'] = all.apply(fypVars, axis=1)

def fypVars(df):
    if (df['psycle_segment_name'] == 'C2C' and df['fyp'] == 'Medium'):
        return 1
    else:
        return 0

all['psycle_segment_C2C_pyc_Medium'] = all.apply(fypVars, axis=1)

def fypVars(df):
    if (df['psycle_segment_name'] == 'C2C' and df['fyp'] == 'High'):
        return 1
    else:
        return 0

all['psycle_segment_C2C_pyc_High'] = all.apply(fypVars, axis=1)


########################## psycle_segment_C1D #################################

def fypVars(df):
    if (df['psycle_segment_name'] == 'C1D' and df['fyp'] == 'Low'):
        return 1
    else:
        return 0

all['psycle_segment_C1D_pyc_Low'] = all.apply(fypVars, axis=1)

def fypVars(df):
    if (df['psycle_segment_name'] == 'C1D' and df['fyp'] == 'Medium'):
        return 1
    else:
        return 0

all['psycle_segment_C1D_pyc_Medium'] = all.apply(fypVars, axis=1)

def fypVars(df):
    if (df['psycle_segment_name'] == 'C1D' and df['fyp'] == 'High'):
        return 1
    else:
        return 0

all['psycle_segment_C1D_pyc_High'] = all.apply(fypVars, axis=1)

########################## psycle_segment_B3B #################################

def fypVars(df):
    if (df['psycle_segment_name'] == 'B3B' and df['fyp'] == 'Low'):
        return 1
    else:
        return 0

all['psycle_segment_B3B_pyc_Low'] = all.apply(fypVars, axis=1)

def fypVars(df):
    if (df['psycle_segment_name'] == 'B3B' and df['fyp'] == 'Medium'):
        return 1
    else:
        return 0

all['psycle_segment_B3B_pyc_Medium'] = all.apply(fypVars, axis=1)

def fypVars(df):
    if (df['psycle_segment_name'] == 'B3B' and df['fyp'] == 'High'):
        return 1
    else:
        return 0

all['psycle_segment_B3B_pyc_High'] = all.apply(fypVars, axis=1)

########################## psycle_segment_A2B #################################

def fypVars(df):
    if (df['psycle_segment_name'] == 'A2B' and df['fyp'] == 'Low'):
        return 1
    else:
        return 0

all['psycle_segment_A2B_pyc_Low'] = all.apply(fypVars, axis=1)

def fypVars(df):
    if (df['psycle_segment_name'] == 'A2B' and df['fyp'] == 'Medium'):
        return 1
    else:
        return 0

all['psycle_segment_A2B_pyc_Medium'] = all.apply(fypVars, axis=1)

def fypVars(df):
    if (df['psycle_segment_name'] == 'A2B' and df['fyp'] == 'High'):
        return 1
    else:
        return 0

all['psycle_segment_A2B_pyc_High'] = all.apply(fypVars, axis=1)

########################## psycle_segment_A2C #################################

def fypVars(df):
    if (df['psycle_segment_name'] == 'A2C' and df['fyp'] == 'Low'):
        return 1
    else:
        return 0

all['psycle_segment_A2C_pyc_Low'] = all.apply(fypVars, axis=1)

def fypVars(df):
    if (df['psycle_segment_name'] == 'A2C' and df['fyp'] == 'Medium'):
        return 1
    else:
        return 0

all['psycle_segment_A2C_pyc_Medium'] = all.apply(fypVars, axis=1)

def fypVars(df):
    if (df['psycle_segment_name'] == 'A2C' and df['fyp'] == 'High'):
        return 1
    else:
        return 0

all['psycle_segment_A2C_pyc_High'] = all.apply(fypVars, axis=1)

########################## psycle_segment_B2C #################################

def fypVars(df):
    if (df['psycle_segment_name'] == 'B2C' and df['fyp'] == 'Low'):
        return 1
    else:
        return 0

all['psycle_segment_B2C_pyc_Low'] = all.apply(fypVars, axis=1)

def fypVars(df):
    if (df['psycle_segment_name'] == 'B2C' and df['fyp'] == 'Medium'):
        return 1
    else:
        return 0

all['psycle_segment_B2C_pyc_Medium'] = all.apply(fypVars, axis=1)

def fypVars(df):
    if (df['psycle_segment_name'] == 'B2C' and df['fyp'] == 'High'):
        return 1
    else:
        return 0

all['psycle_segment_B2C_pyc_High'] = all.apply(fypVars, axis=1)

########################## psycle_segment_B1D #################################

def fypVars(df):
    if (df['psycle_segment_name'] == 'B1D' and df['fyp'] == 'Low'):
        return 1
    else:
        return 0

all['psycle_segment_B1D_pyc_Low'] = all.apply(fypVars, axis=1)

def fypVars(df):
    if (df['psycle_segment_name'] == 'B1D' and df['fyp'] == 'Medium'):
        return 1
    else:
        return 0

all['psycle_segment_B1D_pyc_Medium'] = all.apply(fypVars, axis=1)

def fypVars(df):
    if (df['psycle_segment_name'] == 'B1D' and df['fyp'] == 'High'):
        return 1
    else:
        return 0

all['psycle_segment_B1D_pyc_High'] = all.apply(fypVars, axis=1)

########################## psycle_segment_B1A #################################

def fypVars(df):
    if (df['psycle_segment_name'] == 'B1A' and df['fyp'] == 'Low'):
        return 1
    else:
        return 0

all['psycle_segment_B1A_pyc_Low'] = all.apply(fypVars, axis=1)

def fypVars(df):
    if (df['psycle_segment_name'] == 'B1A' and df['fyp'] == 'Medium'):
        return 1
    else:
        return 0

all['psycle_segment_B1A_pyc_Medium'] = all.apply(fypVars, axis=1)

def fypVars(df):
    if (df['psycle_segment_name'] == 'B1A' and df['fyp'] == 'High'):
        return 1
    else:
        return 0

all['psycle_segment_B1A_pyc_High'] = all.apply(fypVars, axis=1)

########################## psycle_segment_B3A #################################

def fypVars(df):
    if (df['psycle_segment_name'] == 'B3A' and df['fyp'] == 'Low'):
        return 1
    else:
        return 0

all['psycle_segment_B3A_pyc_Low'] = all.apply(fypVars, axis=1)

def fypVars(df):
    if (df['psycle_segment_name'] == 'B3A' and df['fyp'] == 'Medium'):
        return 1
    else:
        return 0

all['psycle_segment_B3A_pyc_Medium'] = all.apply(fypVars, axis=1)

def fypVars(df):
    if (df['psycle_segment_name'] == 'B3A' and df['fyp'] == 'High'):
        return 1
    else:
        return 0

all['psycle_segment_B3A_pyc_High'] = all.apply(fypVars, axis=1)

########################## psycle_segment_Missing ##############################

def fypVars(df):
    if (df['psycle_segment_name'] == 'missing' and df['fyp'] == 'Low'):
        return 1
    else:
        return 0

all['psycle_segment_missing_pyc_Low'] = all.apply(fypVars, axis=1)

def fypVars(df):
    if (df['psycle_segment_name'] == 'missing' and df['fyp'] == 'Medium'):
        return 1
    else:
        return 0

all['psycle_segment_missing_pyc_Medium'] = all.apply(fypVars, axis=1)

def fypVars(df):
    if (df['psycle_segment_name'] == 'missing' and df['fyp'] == 'High'):
        return 1
    else:
        return 0

all['psycle_segment_missing_pyc_High'] = all.apply(fypVars, axis=1)

print(all)

# let's aggregate by county

agg_vars = ['psycle_segment_C3B_pyc_Low',
            'psycle_segment_C3B_pyc_Medium',
            'psycle_segment_C3B_pyc_High',
            'psycle_segment_C2C_pyc_Low',
            'psycle_segment_C2C_pyc_Medium',
            'psycle_segment_C2C_pyc_High',
            'psycle_segment_C1D_pyc_Low',
            'psycle_segment_C1D_pyc_Medium',
            'psycle_segment_C1D_pyc_High',
            'psycle_segment_B3B_pyc_Low',
            'psycle_segment_B3B_pyc_Medium',
            'psycle_segment_B3B_pyc_High',
            'psycle_segment_A2B_pyc_Low',
            'psycle_segment_A2B_pyc_Medium',
            'psycle_segment_A2B_pyc_High',
            'psycle_segment_A2C_pyc_Low',
            'psycle_segment_A2C_pyc_Medium',
            'psycle_segment_A2C_pyc_High',
            'psycle_segment_B2C_pyc_Low',
            'psycle_segment_B2C_pyc_Medium',
            'psycle_segment_B2C_pyc_High',
            'psycle_segment_B1D_pyc_Low',
            'psycle_segment_B1D_pyc_Medium',
            'psycle_segment_B1D_pyc_High',
            'psycle_segment_B1A_pyc_Low',
            'psycle_segment_B1A_pyc_Medium',
            'psycle_segment_B1A_pyc_High',
            'psycle_segment_B3A_pyc_Low',
            'psycle_segment_B3A_pyc_Medium',
            'psycle_segment_B3A_pyc_High',
            'psycle_segment_missing_pyc_Low',
            'psycle_segment_missing_pyc_Medium',
            'psycle_segment_missing_pyc_High']

all = all.groupby(['client_address_county'], as_index=False)[agg_vars].agg('sum')

print(all)

print(len(all))
# 690

# Save
all.to_csv('../data/psycle_segment_by_pyc.csv', index=False)
```
## Short code

```python
# PROJECT NAME : NYU-Capstone-project
# CODE NAME: `data_prep_13.py`
# AUTHOR: Marcos Keyser
# AIM: Using `life_02.csv` (output of `data_prep_04.py`) as input table (comes
# with LIFE obs. only and `fyp` takes values `Low`, `Medium`, `High`) add (from
# code `data_prep_09.py`) the code we need to map P$ycle variables to 10 levels
# ('C3B', 'B3A', ...).
#
# INPUT DATA: Create Number of Life and Annuities by customer segment
# (10 new variables)
#
# - `/data/life_02.csv`
#
# The above data is the output of the code `src/data_prep_04.py`
#
# OUTPUT DATA:
#
# - `/data/map_segments_and_fyp.csv`
#
# The bove data is the input of the code `data_prep_13.py`

# Import modules
import matplotlib.pyplot as plt
from pathlib import Path
import warnings
import pandas as pd
import numpy as np
import matplotlib
matplotlib.use('agg')
warnings.filterwarnings('ignore')

# Load the datasets

data_folder = Path("../data/")

all = data_folder / "map_segments_and_fyp.csv"

# Loading all

all = pd.read_csv(all)

# Select variables we need

all = all[['client_address_county', 'fyp', 'psycle_segment_name']]

print(all.head())

print(len(all))

# from code 10

# Let's create 10 new columns for ech segment


def fypVars(df, var_1, var_2):
    """This funciton creates a new column per each P$ycle level (10 levels)
       and premium level (3 levels). It assigns 1 to the observations if a
       contract is present, it assigns 0 otherwise.
    Parameters
    ----------
    df : pandas dataframe
        input / output dataframe `df`.
    var_1 : str
        Levels of P$ycle segment `var_1`.
    var_2 : str
        Levels of premium fyp `var_2`.

    Returns
    -------
    pandas dataframe
        A new column for each combination segent, premium.
        The column contain1 or ).
    """
    if (df['psycle_segment_name'] == var_1 and df['fyp'] == var_2):
        return 1
    else:
        return 0


varA = ['C3B', 'C3B', 'C3B', 'C2C', 'C2C', 'C2C', 'C1D', 'C1D', 'C1D', 'B3B',
        'B3B', 'B3B', 'A2B', 'A2B', 'A2B', 'A2C', 'A2C', 'A2C', 'B2C', 'B2C',
        'B2C', 'B1D', 'B1D', 'B1D', 'B1A', 'B1A', 'B1A', 'B3A', 'B3A', 'B3A',
        'missing', 'missing', 'missing']

varB = ['Low', 'Medium', 'High', 'Low', 'Medium', 'High', 'Low', 'Medium',
        'High', 'Low', 'Medium', 'High', 'Low', 'Medium', 'High', 'Low',
        'Medium', 'High', 'Low', 'Medium', 'High', 'Low', 'Medium', 'High',
        'Low', 'Medium', 'High', 'Low', 'Medium', 'High', 'Low', 'Medium',
        'High']

for item in zip(varA, varB):
    all["psycle_segment_%s_pyc_%s" % (item)] = all.apply(
        fypVars, args=(item), axis=1)

print(all)


agg_vars = []

for item in zip(varA, varB):
    agg_vars.append("psycle_segment_%s_pyc_%s" % (item))

print(agg_vars)

# let's aggregate by county

all = all.groupby(['client_address_county'], as_index=False)[
    agg_vars].agg('sum')

print(all)

print(len(all))
# 690

# Save
all.to_csv('../data/psycle_segment_by_pyc.csv', index=False)
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE5NjMyOTk2NjcsLTE2NzMwODUwNTNdfQ
==
-->