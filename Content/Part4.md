---
layout: default
title: Spatial Analysis
nav_order: 4
---

# Spatial Analysis

We're going to look at two methods for overlaying a raster image and a vector layer: 1) Using the Zonal Statistics tool to overlay a raster layer, 2) Converting the raster to a vector and doing some polygon overlays.  Method 1 is slightly faster and more accurate, but can be applied in a more limited number of circumstances.  Method 2 induces some error when converting between data types (we will discuss more in lecture) and requires more steps, but it is more flexible.

## Zonal Statistics: Mean NDVI

We are going to overlay the vector data on the raster data to measure the mean NDVI value for each DA & CT using the Zonal Statistics as Table tool.  Then we will Join the resulting output table to display the mean NDVI values per DA & CT.  

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

## Question 7)
What is the DAUID of the DA with the highest Mean NDVI value?  *Hint* Double clicking on Green Veg Area in the attribute table allows you to sort in ascending/descending order.
<!-- 59151219 -->

## Raster to Polygon Conversion:

We are going to convert the Classification raster layer to a vector data and select just the Green Vegetation.  Then we can add it to the Van_DA_2016 layers so that 

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
The [Intersect tool](https://pro.arcgis.com/en/pro-app/latest/tool-reference/analysis/intersect.htm) is one of the most useful vector - vector overlay operations.  It will combine the feature classes where they overlap and exclude all other areas 

**1)** Run the Intersect.

**2)** Change the symbology and open the attribute table to confirm the results look like what we'd expect.

<div style="overflow: hidden;
  padding-top: 56.25%;
  position: relative">
  <iframe src="Intersect.mp4" title="Processes" scrolling="no" frameborder="0"
    style="border: 0;
   height: 100%;
   left: 0;
   position: absolute;
   top: 0;
   width: 100%;">
   <p>Your browser does not support iframes.</p>
 </iframe>
</div>
<a href="Intersect.mp4" target="_blank">View Image in New Tab</a>

## Add & Calculate Field

<div style="overflow: hidden;
  padding-top: 56.25%;
  position: relative">
  <iframe src="AddField.mp4" title="Processes" scrolling="no" frameborder="0"
    style="border: 0;
   height: 100%;
   left: 0;
   position: absolute;
   top: 0;
   width: 100%;">
   <p>Your browser does not support iframes.</p>
 </iframe>
</div>
<a href="AddField.mp4" target="_blank">View Image in New Tab</a>


## Summary Table: Area of Green Vegetation


<div style="overflow: hidden;
  padding-top: 56.25%;
  position: relative">
  <iframe src="SummaryTable.mp4" title="Processes" scrolling="no" frameborder="0"
    style="border: 0;
   height: 100%;
   left: 0;
   position: absolute;
   top: 0;
   width: 100%;">
   <p>Your browser does not support iframes.</p>
 </iframe>
</div>
<a href="SummaryTable.mp4" target="_blank">View Image in New Tab</a>


## Join Summary Table
Do a Join to add the Summary Table output to Van_DA_2016.  Following the same steps as above but use the Summary Table you just generated as the Join Table.

## Question 8)
What is the DAUID of the DA with the highest Green Veg Area?
<!-- 59153586 -->

## Question 9)
Is the DA with the highest mean NDVI value the same as the DA with the greatest area of green vegetation? Y/N
<!-- N -->

## Question 10)
How strongly related are these two measures of greenness? Create a scatter plot, with the Mean NDVI value (Output from Method 1) on the X-axis Green Veg Area Sum (Output from Method 2) on the Y-axis.  What is the R2 value?
<!-- 0.0108 -->

## Question 11)
Does this indicate a strong relationship between the two variables?
<!-- No -->

## Question 12)
Change the Y-axis to Income and leave the X-axis as Mean NDVI, not the R2 score.  Now change the X-axis to the Green Veg Area Sum and note the R2 score.  Which variable has a "stronger" relationship with income?

## Question 13) 
Do either of these variables seem to be strongly linked to income?  Why or why not?








