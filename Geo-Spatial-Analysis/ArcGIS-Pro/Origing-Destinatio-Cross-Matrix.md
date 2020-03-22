


> Written with [StackEdit](https://stackedit.io/).

# Origin Destination Cross Matrix

> Reference: _Creating an Origin-Destination Cost Matrix in ArcGIS Pro  by Esri_ one-hour training by ESRI.

## Introduction

You can use origin-destination cost matrices to obtain information on the best routes from multiple origins to multiple destinations using least-cost paths. This information can help you learn about distances and driving costs and provide data for further analysis.

## Origin-destination cost matrix analysis

An origin-destination (OD) cost matrix analysis can be used to create a matrix showing travel times or distances along a transportation network using a network dataset. You can use the OD cost matrix solver to assign customer locations to the nearest stores, for example, where you do not need the actual route and driving directions. Here are more questions you can answer with an OD cost matrix analysis:

-   Which are the best truck terminals, by driving time, to use for moving freight from multiple distribution centers in a city?
-   Which houses have more parks nearby compared to other houses?
-   How many people live within a certain distance of each voting location?

The OD cost matrix solver uses a network dataset to analyze origins and destinations and return a matrix.

> **Network dataset**: A network dataset contains information about the road system, how roads relate to one another, where turns might be allowed or prohibited, and how long road segments take to traverse. Costs are used to calculate travel time and can include prohibited turns, speed limits, traffic, one-way streets, and temporary road construction. Costs in the network can make a facility or incident that is not the closest be the quickest to drive to.
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTc0MDMxMTUwNV19
-->