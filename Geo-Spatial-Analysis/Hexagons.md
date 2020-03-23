


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

An interesting thing, you can label each hexagon with the number of points inside each one:

![enter image description here](http://www.esri.com/about/newsroom/wp-content/uploads/files/2015/04/3.jpg)
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEyODI1OTMxMzFdfQ==
-->