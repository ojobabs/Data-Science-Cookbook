


> Written with [StackEdit](https://stackedit.io/).

# Minkowski Distance Estimation

The following notes summarizes the article:  ["Comparison of distance measures in spatial analytical modeling for health service planning"](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC2781002/).

> **Summary*8: The Minkowski metric is optimized, to approximate travel time and road distance, respectively.

- Distances estimated with each metric are contrasted with road distance and travel time measurements, and an optimized Minkowski distance is implemented in spatial analytical modeling.

## Methods

- **Road distance** and **travel time** are calculated from the postal code of residence of each patient undergoing cardiac catheterization to the pertinent hospital.
- The Minkowski metric is optimized, to approximate travel time and road distance, respectively.
- Distance estimates and distance measurements are then compared using descriptive statistics and visual mapping methods.

## Results

- The Minkowski coefficient that best approximates road distance is 1.54; 1.31 best approximates travel time.
- Euclidean distance tends to underestimate road distance and travel time; Manhattan distance tends to overestimate both.
- The optimized Minkowski distance partially overcomes their shortcomings; it provides a single model of travel over the network.
- The method is flexible, suitable for analytical modeling, and more accurate than the traditional metrics; its use ultimately increases the reliability of spatial analytical models.

## Distance Metric Calculation

- One of the reasons for using Euclidean and/or Manhattan distance is the relative ease of their implementation; in contrast, it is more problematic to design algorithms implementing actual road network distance in spatial analytical models.
- In order to reduce the error associated with the Euclidean and Manhattan metrics while maintaining the computational simplicity of a single, intuitive mathematical formula, the general Minkowski metric is examined, to devise a single method that best approximates the average pattern of an empirical road network.
- Optimizing values of the Minkowski formula are calculated for road distance as well as travel time; the results are compared with more traditional distance measures in the context of assessing geographic accessibility to cardiac facilities.
- The Minkowski distance has the potential to provide a more accurate estimate of road network distance and travel time than the Euclidean and Manhattan metrics.

<!--stackedit_data:
eyJoaXN0b3J5IjpbODg2MzA3MjE5LC0xNjQ0NzQwODUxLDE0NT
A5MzY2NzEsODIxNDcyODk0XX0=
-->