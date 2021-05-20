---
layout: default
title: Spatial Analysis
nav_order: 4
---

# Spatial Analysis

We're going to look at two methods for overlaying a raster image and a vector layer: 1) Using the Zonal Statistics tool to overlay a raster layer, 2) Converting the raster to a vector and doing some polygon overlays.  Method 1 is slightly faster and more accurate, but can be applied in a more limited number of circumstances.  Method 2 induces some error when converting between data types (we will discuss more in lecture) and requires more steps, but it is more flexible.

## Method 1) Zonal Statistics

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

## Method 2) Raster to Polygon Conversion

We are going to convert the Classification raster layer to a vector data and select just the Green Vegetation.  We can then overlay the resulting vector layer with the Van_DA_2016 layer using an intersect.

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

Adding new fields to our attribute table allows us to perform calculations or copy a subset of our data to a new column.

**1)** In the Van_DA_2016_Intersect layer, create a Green Veg Area Field.
* Right click on Field in the attribute table.
* Name the field Green_Veg_Area and give it an alias without the underscores.
  * Arc doesn't allow spaces in column names.
* Make sure the data type is Double.
  * Double is a type of data that allows for decimals.
* Make sure to save the field.
* Close the field window and go back to the attribute table.

**2)** Select only the green vegetation areas.
* Choose Select by Attribute: Where gridcode is equal to 3.
  * Select by attribute allows us to select rows/objects with a certain attribute.
  * It relies on something called a Structured Query Language (SQL).
  * We are selecting all rows "Where" our conditions are met.
  * Our condition is that grdicode (attribute from the NDVI layer representing vegetation category) is equal to 3 (green vegetation).

**3)** Calculate the Green Veg Area.
* Right click on Green Veg Area and choose calculate field.
  * This allows us to define a function and apply it.
* Set the expression to: Green_Veg_Area = Shape_Area as the.
  * *Note* you only need to complete the right side of the equation.
  * This will simply copy the shape area for the green vegetation areas, we will work with a mathematical expression on the next page.

**4)** Assign all other shapes a zero.
* We can quickly invert our selection.
* Calculate the field again, but with Green_Veg_Area = 0
  * We have selected girdcode 1 & 2 (Not vegetation) so they all get zeros.


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


## Summary Table

Summarizing by a field (eg. DAUID - the Dissemination Unit ID) allows us to get statistics of interest for specific columns.

**1)** Get the sum of Green Veg Area by DA.
* Right click on DAUID and click Summarize.
* Set Green Veg Area as the Field and choose Sum as the statistic type.
* Make sure DAUID as the Case Field.
* The resulting table will show the total of just the green vegetation area per DA, and can be joined to the Van_DA_2016 layer.

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
Create a scatter plot, with the Mean NDVI value (Output from Method 1) on the X-axis Green Veg Area Sum (Output from Method 2) on the Y-axis.  What is the R2 value? How strongly related are these two measures of greenness? 
<!-- 0.0108 -->

## Question 11)
Change the Y-axis to Income and leave the X-axis as Mean NDVI, note the R2 score.  Now change the X-axis to the Green Veg Area Sum and note the R2 score.  Which variable has a "stronger" relationship with income?

## Question 12) 
Are either of these variables strongly linked to income?  Why?








