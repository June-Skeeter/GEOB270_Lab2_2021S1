---
layout: default
title: Raster Data
nav_order: 3
---

# Raster Data

## Calculating NDVI with Google Earth Engine
We're going to use GEE to download [LANDSAT8](https://developers.google.com/earth-engine/datasets/catalog/landsat-8) data.  LANDSAT8 is one of a large number of satellites that orbit the earth continuously collecting multi-spectral (visible light & other wavelengths) imagery.  We can use multi-spectral imagery for a number of different applications like estimating vegetation health.

The lines on the chart below are referred to as a spectral reflectance curves. They show reflectance (amount of light) on the y-axis, defined as the percent of incident radiation reflected by different earth features, and wavelength on the x-axis. As you can see, the spectral reflectance curves for different features look very different. Specifically, you can see that healthy green vegetation has very high reflectance in the near-infrared wavelengths (0.7-1.4 µm) and lower reflectance in the visible part of the spectrum (0-0.7 µm), while water absorbs almost all incoming infrared radiation and thus has very low infrared reflectance. Soil has relatively higher reflectance in the visible wavelengths, and intermediate reflectance in the near infrared.
 
<div style="overflow: hidden;
  padding-top: 56.25%;
  position: relative">
  <iframe src="NDVI.png" title="Processes" scrolling="no" frameborder="0"
    style="border: 0;
   height: 100%;
   left: 0;
   position: absolute;
   top: 0;
   width: 100%;">
   <p>Your browser does not support iframes.</p>
 </iframe>
</div>
<a href="NDVI.png" target="_blank">View Image in New Tab</a>

These differences are the basis for the normalized difference vegetation index (NDVI), one of the most commonly used spectral indices for vegetation monitoring. NDVI is calculated as:
<a href="https://www.codecogs.com/eqnedit.php?latex=NDVI&space;=&space;\frac{(NIR-&space;RED)}{(NIR&plus;&space;RED)}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?NDVI&space;=&space;\frac{(NIR-&space;RED)}{(NIR&plus;&space;RED)}" title="NDVI = \frac{(NIR- RED)}{(NIR+ RED)}" /></a>
where NIR is reflectance in the near-infrared wavelengths, and RED is reflectance in the red wavelengths. This index can range from -1 to 1, with higher values indicating more/greener/healthier vegetation. Look at the graph above and make sure you understand why green vegetation would have a high value of NDVI.
The gray shaded areas indicate regions of the electromagnetic spectrum that are measured by a satellite. These regions are referred to as “spectral bands.” When you work with satellite imagery, you will have one raster for each band. The values for each raster contain the reflectance measured by the satellite in that band. (This will make more sense in a minute, when you start working with the satellite data).


**1)** Go to the [GEE code Explorer](https://code.earthengine.google.com/), log in if you need to, and create a new Repository called "Lab2_NDVI_Download".

<div style="overflow: hidden;
  padding-top: 56.25%;
  position: relative">
  <iframe src="NewRepo.png" title="Processes" scrolling="no" frameborder="0"
    style="border: 0;
   height: 100%;
   left: 0;
   position: absolute;
   top: 0;
   width: 100%;">
   <p>Your browser does not support iframes.</p>
 </iframe>
</div>
<a href="NewRepo.png" target="_blank">View Image in New Tab</a>

**2)** Now create an new File, make sure its located within the Repository you just created, and name it Landsat8_NDIV_Download.

<div style="overflow: hidden;
  padding-top: 56.25%;
  position: relative">
  <iframe src="NewFile.png" title="Processes" scrolling="no" frameborder="0"
    style="border: 0;
   height: 100%;
   left: 0;
   position: absolute;
   top: 0;
   width: 100%;">
   <p>Your browser does not support iframes.</p>
 </iframe>
</div>
<a href="NewFile.png" target="_blank">View Image in New Tab</a>


**3)** Copy and past the following Javascrpt code below in the grey window, paste it into the code window (top middle pane), then click run.

```javascript
// Coordinates for Vancouver
var Cent = ee.Geometry.Point([-123,49.25]);

// Center Map on Vancouver
Map.centerObject(Cent, 10);

// Import the Landsat 8 TOA image collection.
var Collection = ee.ImageCollection('LANDSAT/LC08/C01/T1_TOA').filter(ee.Filter.lt('CLOUD_COVER_LAND', 10));

// Get the number of images.
var count = Collection.size();
print('Count: ', count);

// Define NDVI Function
var addNDVI_Landsat = function(image) {
  var ndvi = image.normalizedDifference(['B5', 'B4']).rename('NDVI');
  return image.addBands(ndvi);
};

// Apply Function to all Images
var withNDVI_Landsat = Collection.map(addNDVI_Landsat);

// Make a "greenest" pixel composite.
var greenest = withNDVI_Landsat.qualityMosaic('NDVI');
var ndvi = greenest.select('NDVI')

// Define Color Scheme for Visualization
var ndviParams = {min: -.5, max: 1, palette: ['blue', 'white', 'green']};

// Display the result.
Map.addLayer(ndvi, ndviParams, 'Greenest pixel composite');

// // Export to Google drive
// Export.image.toDrive({
//   image: ndvi,
//   description: 'Van_Greenest',
//   scale: 30,
//   region: Boundary
// });
```


## Question 1)
How many images have been retrieved to create this NDVI layer? *Hint* Look at lines 10-12 of code and the corresponding console output.
<!-- 466405 -->

## Request the NDVI Layer

**1)** Upload the Boundary file.
* Go to the Assets tab
* Click New > Shape files
* Navigate to your Lab2_Data folder and upload the Boundary file you created.
  * Try to upload all the files named Boundary.  GEE will tell you which (eg. .sbx) file types it won't accept.  Exclude them and upload the rest
* Click refresh to see your upload
  * It may take a few minutes to show up, the video has been edited for brevity

**2)** Import the Boundary file into the code.
* Click on the boundary file you uploaded, and select import.
* It will import in the top of the code window.
  * By default it names it "table", change the name to Boundary.

**3)** Run the download.
* Scroll to the bottom of the code.
* In Javascript the double backslash "//" will "comment out" code or text so that it is ignored by the processor.
  * Highlight the commented out section of code and hit "ctrl + /" to get rid of the double back slashes.
  * Alternatively, you can just manual delete the double back slashes.
* Click Run
* Switch to the Task pane in the top right.  Run the Van_Greenest task to export this layer to your Google Drive.
  * Google Drive is a free (15GB) file storage service that comes with a Google account.  

<div style="overflow: hidden;
  padding-top: 56.25%;
  position: relative">
  <iframe src="GEE.mp4" title="Processes" scrolling="no" frameborder="0"
    style="border: 0;
   height: 100%;
   left: 0;
   position: absolute;
   top: 0;
   width: 100%;">
   <p>Your browser does not support iframes.</p>
 </iframe>
</div>
<a href="GEE.mp4" target="_blank">View Image in New Tab</a>

## Download the NDVI Layer.

Go to your [Google Drive](https://drive.google.com/drive/my-drive) and find the Van_Greenest.tif, it should be located in the root folder.  It could take 5/10 minutes for GEE to process your request, the task pane will show you when your request is complete.  Right click on it to download.  Put it in your Lab2_Data folder.

## Re-Project the Raster Layer

The Van_Greenest Raster needs to be in the same coordinate system as the Census layers for our analysis to be accurate.

**1)** Reproject the Van_Greenest layer.
* In the Geoprocessing pane, search for the Project tool.
* Set the projection to UTM Zone 10N (find in your favorites for quick access)
* After running, the Van_Greenest_ProjectRaste should show up on your map.

<div style="overflow: hidden;
  padding-top: 56.25%;
  position: relative">
  <iframe src="ProjectRaster.mp4" title="Processes" scrolling="no" frameborder="0"
    style="border: 0;
   height: 100%;
   left: 0;
   position: absolute;
   top: 0;
   width: 100%;">
   <p>Your browser does not support iframes.</p>
 </iframe>
</div>
<a href="ProjectRaster.mp4" target="_blank">View Image in New Tab</a>
