


> Written with [StackEdit](https://stackedit.io/).

# Using hexagons

References:
- [[1] Why hexagons?](https://pro.arcgis.com/en/pro-app/tool-reference/spatial-statistics/h-whyhexagons.htm)
- [[2] Using a binning technique for point-based multiscale web maps](https://www.esri.com/arcgis-blog/products/arcgis-online/mapping/using-a-binning-technique-for-point-based-multiscale-web-maps/)
- [[3] Thematic Mapping with Hexagons](https://www.esri.com/about/newsroom/insider/thematic-mapping-with-hexagons/)

From [3]:
**_Want to be “in” the cool club? Use hexagons to visualize your data._**  
Over the last few years we’ve seen more and more maps that use hexagons. They have become “cool”. Why is that? Well, hexagons and other regularly shaped features allow you to normalize geography for thematic mapping rather than be constrained to using irregular shaped polygons created from a political process (for example, county boundaries, census tracts, zip codes, etc.). And this is VERY useful because of the massive disparity in some of these shapes.

For instance, if you create a thematic map using US counties, [the county where I live](http://en.wikipedia.org/wiki/San_Bernardino_County,_California) disproportionately stands out as it the largest county in the US and is 20,105 square miles (52,070 km2), or slightly larger than the states of New Jersey, Connecticut, Delaware, and Rhode Island combined. Using appropriately sized regularly spaced shapes helps solve this disparity of perception.

![enter image description here](http://www.esri.com/about/newsroom/wp-content/uploads/files/2015/04/1_640.jpg)
> Left: Population Density show with Counties. Right: Population Density shown with Hexagons.

**But why hexagons?**  
Simply put, hexagons are good for visualization because they nest together perfectly and look good. Rectangles are also a good way to show data, and we do it all the time with rasters and imagery data, but the linear patterns of the rectangles are very apparent when zoomed far enough in to see them. The linear patterns in the hexagons are not as apparent and the shapes “softer”, making them more attractive when you are able to see the shape outline. (Note: if you are zoomed out to a small scale, rectangles and hexagons look the same, so the scale at which the data will be used is important).

![enter image description here](http://www.esri.com/about/newsroom/wp-content/uploads/files/2015/04/2_640.jpg)
> Left: 20 km hexagons showing density of bridges. Right: 20 km rectangles showing density of bridges.

**How do you assign data to hexagons?**  
Assigning data to hexagons is pretty easy. You just need more detailed data than the scale of your hexagons and then you aggregate that data into your hexagons. You simply overlay your source data (for example, a set of points representing bridge locations) and a layer of hexagons, and then summarize the values that intersect your hexagons. This is very easy for point data, as you take all the points within a single hexagon and specify how you want to aggregate each field in the point data (maximum, minimum, average, count, etc.). If your data is represented as lines or polygons you can also overlay the data, but you should be aware that you are introducing some interpolated data into your results. (Use the “Summarize within” analysis tool in [ArcGIS Desktop](http://pro.arcgis.com/en/pro-app/tool-reference/analysis/summarize-within.htm) or [ArcGIS Online](https://doc.arcgis.com/en/arcgis-online/use-maps/perform-analysis.htm) to aggregate the data.)  
Depending on the extent or your source data, you may want to do this aggregation at a couple of different scales. Then you can create multi-scale hexagons that turn on as you zoom in or out on the map, giving your end users a more dynamic experience. They only see data appropriate at the given scale and never struggle to discern the data.

**Obscuring the source.**  
An interesting aspect of this data aggregation is that you can use it to obscure the source of the data for privacy reasons. For instance, if you have a list of conference attendees and you want to show a map of where the attendees came from, you probably don’t want to show their actual location due to privacy issues. And you may not want to use zip codes for similar reasons. But you could use multi-scale hexagons to show an approximate area of the people and even filter the results so you only show hexagons that have more than 10 people.

An interesting thing, you can label each hexagon with the number of points inside each one:

![enter image description here](http://www.esri.com/about/newsroom/wp-content/uploads/files/2015/04/3.jpg)
> Showing conference attendees at multiple scales. Top: 500 km hexagons; Middle: 100 km hexagons; Bottom: 20 km hexagons.
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE5NzQ2NzQ4NDJdfQ==
-->