---
name: ripping-data-from-georeferenced-images-with-qgis
layout: post
title: Ripping data from georeferenced images with QGIS
date: 2016-08-30
categories:
- drought 
- awap grids
- data operation
---


# Introduction
Drought Declarations are made by government in Australia to determine when and where a drought is occuring.
The Declarations are linked to agricultural and social support policies. We are working on a climatic drought index that should correlate with these Drought Declarations.  The New South Wales Government has provided us with spatial data from 1986 but they also have a graphical visualisation available for earlier times, especially noteworthy is the extreme 1982-1983 drought.
This post is a document of the process I will try to derive spatial data from the image.

# Methods

- Follow instructions on this website [http://www.qgistutorials.com/en/docs/advanced_georeferencing.html](http://www.qgistutorials.com/en/docs/advanced_georeferencing.html)
- Try out the method on a month that is already available as spatial data, to assess precision.
- Then start mapping earlier data with no correlates.

# Data
Download the drought maps. The current maps are at:
[http://www.dpi.nsw.gov.au/content/agriculture/emergency/drought/planning-archive/climate/advance-retreat](http://www.dpi.nsw.gov.au/content/agriculture/emergency/drought/planning-archive/climate/advance-retreat)

But there is a higher resolution map archived at:
[http://pandora.nla.gov.au/pan/120345/20120529-0000/advance-retreat-drought-map-april-2011.pdf](http://pandora.nla.gov.au/pan/120345/20120529-0000/advance-retreat-drought-map-april-2011.pdf)

![drt-nswdpi-raw](images/drt-nswdpi-raw.png)

# Results

## Step 1 - load the reference layer

- Load up the NSW boundaries by selecting "Add PostGIS Layers" > Connect > gislibrary
- Then select a map layer of NSW

## Step 2 - set up the raster data into the Georeferencer

- Launch the Georeferencer from Raster > Georeferencer > Georeferencer.
- If you do not see that menu item, you will need to enable the Georeferencer GDAL plugin from Plugins > Manage and install Plugins > Installed.
- Zoom in on the month of interest
- Now click on the Add Point button on the toolbar and select an easily identifiable location on the image. Corners, intersections, poles etc. make good control points.
- Once you click on the image at a control point location, you will see a pop-up asking you to enter map coordinates. Click the button From map canvas.
- Find the same location in your reference layer and click there. The coordinates are auto-populated from your click on the map canvas. Click Ok. Similarly, choose at least 4 points on the image and add their coordinates from the reference layer.
- Now go to Settings > Transformation settings (yellow cog wheel).
- Choose the settings as shown below. 
- Transformation type = Thin Plate Spline
- output raster = someting
- target EPS = 4283 (match what your reference layer is)
- Make sure the Load in QGIS when done button is checked. Click OK. 
- Back in the Georeferencer window, go to File > Start georeferencing. This will start the process of warping the image using the GCPs and creating the target raster.

## Step 3 - rip the data to a shapefile

- create a new shp (Layer > New)
- type = ploygon
- Specify CRS = EPSG:4283
- attribute = drought, text
- save to a shp like 'drt198610rip' and OK
- right-click, toggle editing, add new feature
- save layer edits

![drt-edit-shapefile](images/drt-edit-shapefile.png)




# Results

## This work

![drt198610rip](images/drt198610rip.png)

## Compared to NSW DPI drought declarations data

![drt198610rip2](images/drt198610rip2.png)

# Conclusion

The process produces data that is very prone to imprecision.  We may be able to use some extra data from before 1986 though.
