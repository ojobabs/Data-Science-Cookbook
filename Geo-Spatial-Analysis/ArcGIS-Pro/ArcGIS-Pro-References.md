


> Written with [StackEdit](https://stackedit.io/).

# ArcGIS Pro References

### Installation

- [Installing Business Analyst 2019 U.S. Data](https://doc.arcgis.com/en/business-analyst/desktop/installing-business-analyst-data.htm)
- [Authorize and start ArcGIS Pro with a Single Use license](https://pro.arcgis.com/en/pro-app/get-started/authorize-and-start-arcgis-pro-with-a-single-use-license.htm)
- [Authorizing your software and data](https://doc.arcgis.com/en/business-analyst/desktop/authorizing-your-software.htm)
- [How To: Download and install Esri software from My Esri](https://support.esri.com/en/technical-article/000018698)

### Business Analyst

- [What is Business Analyst for ArcGIS Pro?](https://pro.arcgis.com/en/pro-app/help/analysis/business-analyst/what-is-business-analyst-pro.htm)
- [Business Analyst Tools in ArcGIS Pro](https://community.esri.com/community/commercial/blog/2019/06/04/business-analyst-tools-in-arcgis-pro)

### Service Areas

- [Service area analysis layer](https://pro.arcgis.com/en/pro-app/help/analysis/networks/service-area-analysis-layer.htm)

### Spatial Outliers Detection

- [Identifying patterns in spatial information: a survey of methods](https://www-users.cs.umn.edu/~shekhar/talk/2011/sdm_wiley2011.pdf)

### Density-Based Clustering

- [This is the most clear video: DBSCAN:  ](https://www.youtube.com/watch?v=6jl9KkmgDIw)
- [DBSCAN: Part 1](https://www.youtube.com/watch?v=sKRUfsc8zp4)
- [How Dpro.arcgis.com/en/pro-app/tool-reference/spatial-statistics/how-density-based C-clustering works](https://ensity-basedlustering-works.htm)
- [HDBSCAN, Fast Density Based Clustering, the How and the Why - John Healy - Pydata 2019](https://www.youtube.com/watch?v=dGsxd67IFiU)
- [DBSCAN Clustering in ML | Density based clustering](https://www.geeksforgeeks.org/dbscan-clustering-in-ml-density-based-clustering/)
- [Density-Based Clustering - Domino Blog]([https://blog.dominodatalab.com/topology-and-density-based-clustering/](https://blog.dominodatalab.com/topology-and-density-based-clustering/))
- [Brian Kent: Density Based Clustering in Python](https://www.youtube.com/watch?v=5cOhL4B5waU)

### [Does Y mean latitude and X mean longitude in every GIS software?](https://gis.stackexchange.com/questions/11626/does-y-mean-latitude-and-x-mean-longitude-in-every-gis-software)

For ESRI its almost always going to be:

Lat = Y Long = X

### Measuring distance between to points using Python

- [https://python-forum.io/Thread-Formula-works-for-one-row-does-not-for-two](https://python-forum.io/Thread-Formula-works-for-one-row-does-not-for-two) If you you Pandas dataframe you need to change the math library by the numpy library. 
- [Pandas: calculate haversine distance within each group of rows](https://stackoverflow.com/questions/43577086/pandas-calculate-haversine-distance-within-each-group-of-rows)

Determines whether to calculate the distance using a planar (flat earth) or a geodesic (ellipsoid) method.

-   **Planar**—Planar measurements use 2D Cartesian mathematics to calculate length and area. The option is only available when measuring in a projected coordinate system and the 2D plane of that coordinate system will be used as the basis for the measurements.
-   **Geodesic** (Harversine)—The shortest line between two points on the earth's surface on a spheroid (ellipsoid). Therefore, regardless of input or output projection, the results do not change.

>##### Note:
>
> One use for a geodesic line is when you want to determine the shortest distance between two cities for an airplane's flight path. This is also known as a great circle line if based on a > sphere rather than an ellipsoid.

- [How can I quickly estimate the distance between two (latitude, longitude) points?](https://stackoverflow.com/questions/15736995/how-can-i-quickly-estimate-the-distance-between-two-latitude-longitude-points)
- [Haversine Formula in Python (Bearing and Distance between two GPS points)](https://stackoverflow.com/questions/4913349/haversine-formula-in-python-bearing-and-distance-between-two-gps-points)
- [https://community.esri.com/groups/coordinate-reference-systems/blog/2017/10/05/haversine-formula](https://community.esri.com/groups/coordinate-reference-systems/blog/2017/10/05/haversine-formula)
- [https://community.esri.com/groups/coordinate-reference-systems/blog/2014/09/01/geodetic-distances-how-long-is-that-line-again](https://community.esri.com/groups/coordinate-reference-systems/blog/2014/09/01/geodetic-distances-how-long-is-that-line-again)
- [https://www.esri.com/arcgis-blog/products/arcgis-desktop/analytics/calculating-geodesic-distance-between-points/](https://www.esri.com/arcgis-blog/products/arcgis-desktop/analytics/calculating-geodesic-distance-between-points/)
- [Pandas: calculate haversine distance within each group of rows](https://stackoverflow.com/questions/43577086/pandas-calculate-haversine-distance-within-each-group-of-rows)
- [Vectorised Haversine formula with a pandas dataframe](https://stackoverflow.com/questions/25767596/vectorised-haversine-formula-with-a-pandas-dataframe)

### How to select the symbology you want to show?

If you use Python language you can use the following code to show up only the labels corresponding to the selected GOs:

If you want to show the label corresponding the GO = V65 then you can use this code:
```python
def FindLabel ([USER_GO_CD_1], [USER_go_ou_nm]):
    if [USER_GO_CD_1] == "V65":
        return [USER_go_ou_nm]
```
If you can to show the label corresponding to the follo

```python
def FindLabel ([USER_GO_CD_1], [USER_go_ou_nm]):
    if [USER_GO_CD_1] == "D54":
        return [USER_go_ou_nm]
    elif [USER_GO_CD_1] == "D56":
        return [USER_go_ou_nm]
    elif [USER_GO_CD_1] == "D57":
        return [USER_go_ou_nm]
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTIxMzMxMjcwNDAsLTIwMDM2OTc0MzgsNj
AxMDM4NjkxLC01NzkzNjk5OTYsLTE4NTU4NTQ3MDgsMTg0MjY1
NDU5MCwtMTkwMTc2ODE4NSwxNzU5NzY3OTAyLC0xMTc1NDQ1OT
MyXX0=
-->