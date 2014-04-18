---
name: 2014-01-03-tumbarumba-supersite-dem
layout: post
title: tumbarumba-supersite-dem
date: 2014-01-03
categories:
- research methods
---

- The first dataset I downloaded from ASN for playing around with was the Tumba Lidar.
- I had thought it might be better to offer this as a OGC service rather than downloadable geotiff
- just in terms of the size firstly (104MB)
- but I also soon realised it would need some specialised tweaking which non-GIS users might struggle a bit and could avoid if the serverside data is set up by a GIS specialist (although can we assume only GIS specialists will download this kind of data)? 
- kudos to [http://stackoverflow.com/questions/11966503/how-to-replace-nas-in-a-raster-object](http://stackoverflow.com/questions/11966503/how-to-replace-nas-in-a-raster-object)

#### Code:tumbarumba-supersite-dem
    setwd("~/data/supersite/tumba-lidar")
    require(raster)
    fname  <- dir(pattern = "tif$")
    fname
    r  <- raster(fname)
    str(r)
    dfr <- as.data.frame(r)
    summary(dfr)
    # the -1 code looks like it might be missing?  They are around the edge.
    rna <- reclassify(r, cbind(-1, 1197))
    png("tumba-lidar.png")
    plot(rna, col=terrain.colors(100), xlab = "eastings (m)", ylab = "northings (m)")
    title("Tumbarumba Supersite Digital Elevation Model")
    title(sub = "packageId=lloyd.374.2")
    dev.off()

<p></p>

![tumba-lidar.png](/images/tumba-lidar.png)

#### Alternately use a geoserver

- If we use a Geoserver we could set it up so people can view this without downloading the data
- following the instructions [http://suite.opengeo.org/opengeo-docs/processing/contour/setup.html](http://suite.opengeo.org/opengeo-docs/processing/contour/setup.html)
- using the ANU GIS library server

<iframe style="border: none;" height="400" width="600" src="http://brawn.anu.edu.au:8081/geoexplorer/viewer/#maps/1"></iframe>;

- PS the map might take a minute to show up, not sure why, might ask the sysadmin to look at the server performance
