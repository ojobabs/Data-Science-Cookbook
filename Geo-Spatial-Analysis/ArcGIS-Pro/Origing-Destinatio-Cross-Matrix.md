


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

## Settings and constraints

You can set many constraints when setting up an origin-destination cost matrix analysis.

> **Mode:** Mode refers to the way that you want the OD matrix to be created—the type of transportation and distance versus time. The modes are configured in the network dataset, and these settings can be changed at the time of analysis.

> **Cutoff**: Cutoff refers to a maximum time or distance within which you would like the analysis to search for destinations. For example, if the mode is based on driving time, a cutoff of 5 will yield only the destinations that are within five minutes of an origin. If the mode is based on distance, the units will be miles, meters, or whatever unit you have set in the network dataset.

> **Destinations**: The number of destinations to find should also be set. A setting of 1 means that your analysis will find the one closest destination for each origin. Leaving Destinations blank or setting it to a number higher than the actual number of destinations imported will result in the matrix containing a path from every origin to every destination.

> **Barriers**: Barriers allow you to model a road or area blocked by an obstruction, such as road construction or another temporary closure. Barriers can be modeled and added to your analysis to get more realistic results by temporarily adding to the cost of reaching certain parts of a network. Barriers in ArcGIS Network Analyst must be imported from a feature class or digitized on-screen.

> **Arrive/Depart Time**: Arrive/Depart Time is a setting that allows you to add information about the date, day, or time of day to better reflect reality, if desired for the analysis. This option can be useful if your network dataset contains traffic data and you want to target or avoid high-traffic times of day in your scenario.

> **Output Geometry:** The Output Geometry parameter allows you to display the results of the analysis as either lines from origins to destinations or no lines at all. For performance reasons, when analysis results are displayed as lines, the lines are straight. The lines always store the travel time and travel distance along the street network, not the straight-line distance. This is why the table, or matrix, behind the lines output is the most useful part of the analysis results.

## Output and other uses

The output of an origin-destination cost matrix analysis is the table containing the travel times or distances from origins to destinations. You can use this table, or matrix, to show ranked locations—that is, which locations are the shortest driving times or distances from other locations.

![Destination 2 is closest in driving time to both Origin 1 and 2.](https://raw.githubusercontent.com/markeyser/Data-Science-Cookbook/master/imgs/OD-Cost-Matrix.png?_sm_au_=iVVH555w0LFMV6sHjfc06K6ttCjRt)

> Destination 2 is closest in driving time to both Origin 1 and 2.

An OD cost matrix can also be used as input for many other spatial analyses where the network cost is needed instead of simple straight-line cost, including many location or supply-chain problems. Here are some examples:

-   Using the Summary Statistics tool, you can report how many people live within a certain distance of each of your stores, setting store locations as the Origins and census tracts with population as the Destinations.
-   The Hot Spot Analysis tool uses the results of an OD cost matrix analysis to show statistically significant spatial clustering.
-   The Generate Network Spatial Weights calls the OD cost matrix solver to create an SWM (spatial weights matrix) file, which can be input to other tools like Spatial Autocorrelation.

Tools that use OD cost matrix output
  
> **You can use the OD cost matrix as input to external processes or tools.**
>For example, some linear programming problems require an origin-destination matrix as input. This tool is an example of an external tool using an OD cost matrix and a Python script used to solve common allocation problems having capacity constraints, such as allocating stores to warehouses or allocating students to schools.
>[Determine Optimum Allocation tool![](https://www.esri.com/training/courses/shared/images/newWindow.png "Opens in new window")](http://www.arcgis.com/home/item.html?id=c5ae481f25604d1bb050d9bd1d6e3c06 "Opens in new window")
>This tool solves the classic transportation problem by first generating a travel cost matrix between the given origins and destinations using the OD cost matrix solver provided by Network Analyst. The tool then formulates and solves a linear programming (LP) problem using an LP solver. It allocates origins having a supply to destinations having demand where the supply is consumed, the demands are met, and the overall transportation cost is minimized.


<!--stackedit_data:
eyJoaXN0b3J5IjpbMTQwNjMyMzM2MywxMzE4MjUzMzA5XX0=
-->