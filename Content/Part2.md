---
layout: default
title: Raster Data
nav_order: 3
---

# Raster Data

## Calculating NDVI with Google Earth Engine
We're going to use [LANDSAT8]() data to calculate [NDVI]() and download the layer.

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

## Question A1)
What happens?

## Question A2)
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
