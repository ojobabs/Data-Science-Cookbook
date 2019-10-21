> Written with [StackEdit](https://stackedit.io/).

# Quantile-based discretization implemented in Python

## Discretisation
Discretisation is the process of transforming continuous variables into discrete variables by creating a set of contiguous intervals that spans the range of the variable's values.

## Discretisation helps handle outliers and highly skewed variables
Discretisation helps handle outliers by placing these values into the lower or higher intervals together with the remaining inlier values of the distribution. Thus, these outlier observations no longer differ from the rest of the values at the tails of the distribution, as they are now all together in the same interval / bucket. In addition, by creating appropriate bins or intervals, discretisation can help spread the values of a skewed variable across a set of bins with equal number of observations.

## Discretisation approaches
There are several approaches to transform continuous variables into discrete ones. This process is also known as **binning**, with each bin being each interval. Discretisation methods fall into 2 categories: **supervised** and **unsupervised**. Unsupervised methods do not use any information, other than the variable distribution, to create the contiguous bins in which the values will be placed. Supervised methods typically use target information in order to create the bins or intervals.

## Unsupervised discretisation methods
- Equal width binning
- Equal frequency binning

## Supervised discretisation methods
- Discretisation using decision trees

## Equal frequency discretisation or Quantile-based discretization
Equal frequency binning divides the scope of possible values of the variable into N bins, where each bin carries the same amount of observations. This is particularly useful for skewed variables as it spreads the observations over the different bins equally. Typically, we find the interval boundaries by determining the quantiles.

Equal frequency discretisation using quantiles consists of dividing the continuous variable into N quantiles, N to be defined by the user. There is no rule of thumb to define N. However, if we think of the discrete variable as a categorical variable, where each bin is a category, we would like to keep N (the number of categories) low (typically no more than 10).

Equal frequency binning is straightforward to implement and by spreading the values of the observations more evenly it may help boost the algorithm's performance. On the other hand, this arbitrary binning may also disrupt the relationship with the target on occasions. Therefore, whenever possible, it will bring value to examine whether this type of binning is the right strategy, and it will depend on the variable and the algorithm that we want to use to make the predictions.

### Some references:

- [12 Useful Pandas Techniques in Python for Data Manipulation](https://www.analyticsvidhya.com/blog/2016/01/12-pandas-techniques-python-data-manipulation/)
- [Pandas documentation](https://pandas.pydata.org/pandas-docs/version/0.23.4/generated/pandas.qcut.html)
- [Binning a pandas column based on quantiles](https://stackoverflow.com/questions/52207582/binning-a-pandas-column-based-on-quantiles)
- [What is the difference between pandas.qcut and pandas.cut?](https://stackoverflow.com/questions/30211923/what-is-the-difference-between-pandas-qcut-and-pandas-cut/30214901)
- [Bucketing Continuous Variables in pandas](http://benalexkeen.com/bucketing-continuous-variables-in-pandas/)
- [Quantile and Decile rank of a column in pandas python](http://www.datasciencemadesimple.com/quantile-decile-rank-column-pandas-python-2/)
- [Continuous variable to categorical by quartiles?](https://datascience.stackexchange.com/questions/29093/continuous-variable-to-categorical-by-quartiles)

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTExNDg0MDQyNDFdfQ==
-->