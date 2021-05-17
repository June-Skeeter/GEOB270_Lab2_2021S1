---
layout: default
title: Spatial Analysis
nav_order: 4
---

# Spatial Analysis

## Vector Overlay

We are going to overlay the vector data on the raster data to measure the mean NDVI value for each DA & CT using the Zonal Statistics as Table tool.  Then we will Join the resulting output table to display the mean NDVI values per DA & CT.  

## Mean NDVI

**1)** Calculate the Zonal Statistics
* Find the Zonal Statistics as Table tool in the Geoprocessing pane.
* Choose Van_DA_2016 as the feature zone data.
* Set DAUID as the Zone Field
* Set your NDVI layer as the Input value raster.
* Select All statistics types
* Run

**2)** Join the Zonal Statistics table with the Van_DA_2016
* Right click on Van_DA_2016 and choose Joins and Relates > Add Join
* Set DAUID as the Input Join Field
* Choose the Zonal Statistics table (mine is named ZonalST_Van_DA_1) as your input.
* Make sure DAUID is selected as the Join Table Field as well
* Click OK

**3)** Inspect the Join
* Open the attribute table and note the new columns.
* Change the symbology, and choose Mean as the Field.
* Zoom in, turn Van_DA_2016 layer on/off, compare to the classification, NDVI layer, and base map.  Confirm the values make sense given the inputs.

<div style="overflow: hidden;
  padding-top: 56.25%;
  position: relative">
  <iframe src="ZonalStats.mp4" title="Processes" scrolling="no" frameborder="0"
    style="border: 0;
   height: 100%;
   left: 0;
   position: absolute;
   top: 0;
   width: 100%;">
   <p>Your browser does not support iframes.</p>
 </iframe>
</div>
<a href="ZonalStats.mp4" target="_blank">View Image in New Tab</a>

## Raster to Polygon

We are going to convert the Classification raster layer to a vector data. 

**1)** Use the Raster to Polygon Tool
* Set Classification as the Input raster
* Choose Value as the Field

**2)** Set the Symbology to Unique Values
* Choose gridcode as the Field
* Zoom into somewhere of interest (eg. I chose Trout Lake), toggle the newly created vector layer on and off to see if it makes sense.

<div style="overflow: hidden;
  padding-top: 56.25%;
  position: relative">
  <iframe src="RasterToPoly.mp4" title="Processes" scrolling="no" frameborder="0"
    style="border: 0;
   height: 100%;
   left: 0;
   position: absolute;
   top: 0;
   width: 100%;">
   <p>Your browser does not support iframes.</p>
 </iframe>
</div>
<a href="RasterToPoly.mp4" target="_blank">View Image in New Tab</a>

## Intersect


**1)** 

## Spatial Join


**1)** 

