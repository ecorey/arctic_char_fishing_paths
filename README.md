![Layout](./Layout_arctic_charr.pdf)
---

THE PROBLEM

Bub is going camping in the North Maine Woods and has found a campsite on perch pond in Aroostock County. The Deboullie Ecoreserve is close and had four ponds that have arctic charr. Bub is an avid fly fisherman and has always wanted to try his luck for arctic charr but he is going to have to hike to the closest spot. This analysis will determine which pond Bub should hike to taking into account the cost path of the hike, the distance of the hike, and the fishing report (number of artic charr caught) at the various ponds. 
---

THE DATASETS
-	Ponds that contain arctic charr: digitized point feature class based on ponds found to contain arctic charr in this Maine state study:    https://www.maine.gov/ifw/docs/strategic-management-plans/arcticcharr.pdf
-	DEM Elevation Raster Datasets (USGS): https://apps.nationalmap.gov/downloader/#/
-	Fishing Reports: Loosely based off accounts on:
Fishing App and Fishing Tools
https://www.lake-link.com/
---


THE METHODOOLOGY
1)	Create a point feature class for ponds that have arctic charr
2)	Create a point feature class for the campsite and place it
3)	Create a polygon feature class / digitize the lakes in the analysis area (1:65,010)
4)	Download area DEMs from USGS national map
5)	Use mosaic to new raster tool to create one dem from the various ones downloaded
6)	Create a raster layer from the lake/ pond polygons that were digitized
7)	Reclass the lake/ pond raster layer to assign water values to 99
8)	Run a slope analysis on the DEM layer
9)	Reclassify the slope layer with higher values for higher slopes
10)	 Use the mosaic to new raster tool to combine the reclassified lake/ pond raster and the reclassified slope layer together (overlay operation)
11)	 Create a feature class for polygons to cover lakes/ ponds with arctic charr in the area 
12)	 Create a polygon to raster layer from the new polygon layer
13)	 Find the Euclidean distance using the new arctic charr lake/ pond raster  (distance operation)
14)	Create a feature classes to hold destination points and create the points
15)	 Create a cost distance and a backlink using the reclassified dem and the campsite point
16)	Run a cost path analysis using the cost distance raster, the backlink raster, and the various destination points (spatial overlay operation)
17)	 Using the Raster to Polyline tool converts the new cost paths to polylines to find their distances 
18)	In the polyline attribute tables create field length_miles and use the calculate field with the expression (length_miles =  !Shape_Length! / 1609) to find miles (distance operation)
19)	Compare the polyline miles with cost path values for the same paths
20)	Merge Polylines to create a table to display on the layout that includes the fishing reports
21)	Weigh the overlays of the Cost Paths, distances, and fishing reports to determine the best route

---

THE RESULTS

Using the Euclidean Distance tool revealed that Gardner Pond was the closest to the campsite and considering the slope and cost distance, the cost path was also the least for Gardner Pond compared to any other pond. The fishing, however, is not great and compared to Deboullie Pond could be considered dismal. Deboullie Pond had the best fishing and only a slightly higher cost path and distance than Gardner Pond, so it was the overall first choice after the overlay’s weights were taken into consideration. These results demonstrate the influence that weights have on the results and the impact of one dataset can have on the results of several others. 
