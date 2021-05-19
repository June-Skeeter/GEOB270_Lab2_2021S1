---
layout: default
title: Vector Data
nav_order: 2
---

# Vector Data

## Setting up your GeoDatabase
By default, ArcPro creates a geodatabase when you start a new project.  We're going to create a Feature Dataset within this geodatabase and add the census data to it.  Feature Datasets are collections of Feature Classes that are all in the same coordinate system.  Data that comes from Stats Canada is by default in the Lambert Conformal Conic Projection.  We're going to use a Universal Transverse Mercator projection instead since we are working with a small area (Vancouver).

**1)** Create the CensusData Feature Dataset
* Right click on the Lab2_Project.gdb and chose New>Feature Dataset
* Name it CensusData
* Set the Coordinate System to NAD 1983 UTM Zone 10N
	* NAD 1983 is the name of the datum (North American Datum 1983)
	* UTM Zone 10N is the name of the projection (Universal Transverse Mercator, Zone 10 N)
	* You can set this coordinate system to your favorites by right clicking and selecting add to favorites.  This will make it easier to find in the future.

**2)** Import the census layers
* Right click CensusData and choose Import > Feature Class(es)
* Add Van_DA_2016.shp and and VanCMS_CT_2016.shp from the Lab2_Data folder.

<div style="overflow: hidden;
  padding-top: 56.25%;
  position: relative">
  <iframe src="FeatureDataset.mp4" title="Processes" scrolling="no" frameborder="0"
    style="border: 0;
   height: 100%;
   left: 0;
   position: absolute;
   top: 0;
   width: 100%;">
   <p>Your browser does not support iframes.</p>
 </iframe>
</div>
<a href="FeatureDataset.mp4" target="_blank">View Image in New Tab</a>


## Get Project Boundary File
We need to create a simple boundary file to upload to Google Earth Engine so we can download satellite for the study area.  We can do this quickly using the dissolve tool.

**1)** Use the Dissolve tool to create the boundary file.
* In the Geoprocessing pane, find the Dissolve tool.
* Set VanCMA_CT_2016 as the input
* **Note** Geoprocessing results are by default saved to your Lab2_Project.gdb, but files in .gdb are saved in a format that can't be read by Google Earth Engine.
	* Instead, save the Output in Lab2_Data and name it Boundary.
* Remove this layer from your table of contents.  We don't need it in this map project.	

<div style="overflow: hidden;
  padding-top: 56.25%;
  position: relative">
  <iframe src="Dissolve.mp4" title="Processes" scrolling="no" frameborder="0"
    style="border: 0;
   height: 100%;
   left: 0;
   position: absolute;
   top: 0;
   width: 100%;">
   <p>Your browser does not support iframes.</p>
 </iframe>
</div>
<a href="Dissolve.mp4" target="_blank">View Image in New Tab</a>
