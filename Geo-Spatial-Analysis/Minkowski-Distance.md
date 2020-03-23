


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

<!--stackedit_data:
eyJoaXN0b3J5IjpbMTYyMjg5MjYyLC0xNjQ0NzQwODUxLDE0NT
A5MzY2NzEsODIxNDcyODk0XX0=
-->