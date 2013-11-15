---
name: quantum-gis-visualisations 
layout: post
title: quantum-gis-visualisations
date: 2013-10-31
categories:
- gisviz
- concordance
---

- This is a quick post on Quantum GIS for spatial data visualisation
- it is also a follow up on [this post about area concordance](http://swish-climate-impact-assessment.github.io/2013/06/test-gislibrary/)
- Quantum GIS is getting pretty good but is still a bit tricky to make good looking maps
- QGIS can use [remote PostGIS geodatabases on the Cloud as the backend](http://swish-climate-impact-assessment.github.io/2013/04/quantumgis-and-postgis/)

#### R Code: use postgis to create area-concordance
    require(devtools)
    install_github("gisviz", "ivanhanigan")
    require(gisviz)
    require(swishdbtools)
    ch <- connect2postgres2("gislibrary")
    # make a temporary tablename, to avoid clobbering
    temp_table <- swish_temptable("gislibrary")
    temp_table <- paste("public", temp_table$table, sep = ".")
    temp_table
    # this is going to be public.foo11c7673416ea
     
    sql <- postgis_concordance(conn = ch, source_table = "abs_sla.nswsla91",
       source_zones_code = 'sla_id', target_table = "abs_sla.nswsla01",
       target_zones_code = "sla_code",
       into = temp_table, tolerance = 0.01,
       subset_target_table = "cast(sla_code as text) like '105%'", 
       eval = F) 
    cat(sql)
    dbSendQuery(ch, sql)

<p></p>

- now connect to PostGIS using QGIS [as described in this tute](http://swish-climate-impact-assessment.github.io/2013/04/quantumgis-and-postgis/)
- and add the layer to the map
- Style it how you like, I also added NSWSLA1991 over the top
- go into the "new print composer"

![qgis-new-print-composer.png](/images/qgis-new-print-composer.png)

![qgis-add-new-map.png](/images/qgis-add-new-map.png)

### Results
- hit the export to image and viola

![qgis-export-image.png](/images/qgis-export-image.png)

### Don't forget to clean up the database!
#### R Code:
    dbSendQuery(ch, sprintf("drop table %s", temp_table))
