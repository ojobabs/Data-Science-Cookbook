


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

> **OD cost matrix solver**: Because it uses a network dataset, an OD cost matrix analysis can find the shortest road distances and quickest travel times between locations. It gives you this information from the possible network paths, from multiple origins to multiple destinations. Using network paths instead of straight-line distances is better for analyzing how people move about in a city. This is because people usually travel on a transportation network, such as roads, train lines, and sidewalks.
> **The matrix**: The best path on the street network is discovered for each OD pair, and the travel times and travel distances are stored as attributes of the output lines. You can display the paths as straight lines on a map or, more commonly, you can view the table of the attributes of the paths. The paths are also ranked in ascending order based on the travel time or distance.

### Settings and constraints

You can set many constraints when setting up an origin-destination cost matrix analysis.

> **Mode:** Mode refers to the way that you want the OD matrix to be created—the type of transportation and distance versus time. The modes are configured in the network dataset, and these settings can be changed at the time of analysis.

> **Cutoff**: Cutoff refers to a maximum time or distance within which you would like the analysis to search for destinations. For example, if the mode is based on driving time, a cutoff of 5 will yield only the destinations that are within five minutes of an origin. If the mode is based on distance, the units will be miles, meters, or whatever unit you have set in the network dataset.

> **Destinations**: The number of destinations to find should also be set. A setting of 1 means that your analysis will find the one closest destination for each origin. Leaving Destinations blank or setting it to a number higher than the actual number of destinations imported will result in the matrix containing a path from every origin to every destination.

> **Barriers**: Barriers allow you to model a road or area blocked by an obstruction, such as road construction or another temporary closure. Barriers can be modeled and added to your analysis to get more realistic results by temporarily adding to the cost of reaching certain parts of a network. Barriers in ArcGIS Network Analyst must be imported from a feature class or digitized on-screen.

> **Arrive/Depart Time**: Arrive/Depart Time is a setting that allows you to add information about the date, day, or time of day to better reflect reality, if desired for the analysis. This option can be useful if your network dataset contains traffic data and you want to target or avoid high-traffic times of day in your scenario.

> ****
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTk0NjgxMTE0OF19
-->