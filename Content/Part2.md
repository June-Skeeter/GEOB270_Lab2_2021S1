---
layout: default
title: Raster Data
nav_order: 3
---

# Raster Data

## Download Data from Google Earth Engine

Copy and paste this code into the GEE code Explorer

'''javascript
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
'''

## Downloading the NDVI Layer

Go to your [Google Drive](https://drive.google.com/drive/my-drive) and find the Van_Greenest.tif, it should be located in the root folder.  Right click on it and to download.  Put it in your Lab2_Data folder.

## Re-Project the Raster Layer

The NDVI layer needs to be in the same coordinate system as the Census layers for our analysis to be most accurate.


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
