
> Written with [StackEdit](https://stackedit.io/).

# Origin Destination Cost Matrix

> **References**:
> - [Generate Origin Destination Cost Matrix (Ready To Use)](https://pro.arcgis.com/en/pro-app/tool-reference/ready-to-use/itemdesc-generateorigindestinationcostmatrix.htm)
> - [Output from Origin Destination Cost Matrix](https://pro.arcgis.com/en/pro-app/tool-reference/ready-to-use/output-generateorigindestinationcostmatrix.htm)

Summary

- The Generate Origin Destination Cost Matrix service tool creates an origin-destination (OD) cost matrix from multiple origins to multiple destinations.
- OD cost matrix is a table that contains the **travel time** and **travel distance** from each origin to each destination.
- Additionally, it ranks the destinations that each origin connects to in ascending order based on the minimum time or distance required to travel from that origin to each destination.
- The best path on the street network is discovered for each origin-destination pair, and the travel times and travel distances are stored as attributes of the output lines.
- Even though the lines are straight for performance reasons, they always store the travel time and travel distance along the street network, not straight-line distance.

Usage

- You need to specify at least one origin and one destination to successfully execute the tool. You can load up to 1000 origins and 1000 destinations.
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE0OTUwMjI0MSwtNzcxMjQ4ODk2XX0=
-->