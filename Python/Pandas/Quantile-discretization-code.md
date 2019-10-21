


> Written with [StackEdit](https://stackedit.io/).

```python
# PROJECT NAME : `Credit-Scoring-Toolkit`
# CODE NAME: `bucketing.py`
# AUTHOR: Marcos Keyser
# AIM: Implement bucketing continuous variables feautre engineering technique
# to use with training and validation datasets.
#
# INPUT DATA:
#
# - `data/titanic.csv`
#
# OUTPUT DATA: There is no output data
#
# Notice that I replaced all missing values in `Age` variable by a random value
# between 20 and 50 in the Titanci dataset. I did it to simplify the following
# explanation.

##### Import modules

# checking and changing working directory
import os
cwd = os.getcwd()
cwd

# Changing working directory to current project's directory
os.chdir('C:\\Users\\t93kqi0\\Documents\\Projects\\Credit-Scoring-Toolkit')
cwd = os.getcwd()
cwd

import pandas as pd
import numpy as np
from sklearn.model_selection import train_test_split
import matplotlib.pyplot as plt
%matplotlib inline

# let's load the titanic dataset from Kaggle
# Let's load the continuous variable `Fare`, and then the target `Suvived`.
data = pd.read_csv('data/titanic.csv', usecols=['Fare','Age', 'Survived'])
data.head()

##### Important

# The calculation of the quantiles should be done consedirig ONLY the training set, and then expanded it to the test set. See bellow

# Let's divide into train and test set
X_train, X_test, y_train, y_test = train_test_split(data[['Fare', 'Age']], data.Survived, random_state=1234)

X_train.shape, X_test.shape

##### Quantile-based discretization for training and validation

# Quantile-based discretization function.
# Discretize variable into equal-sized buckets based on rank or based on sample quantiles.
# For example 1000 values for 10 quantiles would produce a Categorical object indicating quantile membership for each data point.

features = [var for var in X_train.columns]

def discretize(train_data, test_data, bins=5):
    '''
    Discretizes the training data using quatiles.
    Then apply the same binning logic derived from the training data
    to the test data.

    Using retbins=True qcut returns a tuple whose second element is the bins.
    So, train is the categorical series and bins are the break points. Now
    you can pass bins to pd.cut to apply the same grouping logic to the test
    data.
    '''

    train, bins = pd.qcut(train_data, bins, retbins = True,  labels=False)

    test = pd.cut(test_data, bins=bins, labels=False, include_lowest = True)

    return train, bins, test

# Let's loop trhugh columns list to apply `discretize()` function to each column:
for feature in features:
    X_train[feature + '_Bin'], bins, X_test[feature + '_Bin']  = discretize(X_train[feature], X_test[feature], 5)

X_train.head()

X_test.head()

# Note that it is possible to include labels using `labels=["good", "medium", "bad"]` instead of `labels=list(range(bins)))`
# See Pandas documentation bellow

# [Applying pandas qcut bins to new data](https://stackoverflow.com/questions/37906210/applying-pandas-qcut-bins-to-new-data)
# [reference](https://pandas.pydata.org/pandas-docs/version/0.23.4/generated/pandas.qcut.html)
# [reference](https://www.analyticsvidhya.com/blog/2016/01/12-pandas-techniques-python-data-manipulation/)

##### Binning and encoding numeric columns with the new `KBinsDiscretizer` in scikit-learn

from sklearn.preprocessing import KBinsDiscretizer
kbd = KBinsDiscretizer(encode='onehot-dense')
fare_transformed = kbd.fit_transform(X_train[['Fare']])

fare_transformed

# By default, each bin contains (approximately) an equal number of observations.
# Let’s sum up each column to verify this.

fare_transformed.sum(axis=0)

# This is the ‘quantile’ strategy. You can choose ‘uniform’ to make the bin edges
# equally spaced or ‘kmeans’ which uses K-means clustering to find the bin edges.

kbd.bin_edges_

##### References

# - [From Pandas to Scikit-Learn — A new exciting workflow](https://medium.com/dunder-data/from-pandas-to-scikit-learn-a-new-exciting-workflow-e88e2271ef62)
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbOTg0MDg4MjJdfQ==
-->