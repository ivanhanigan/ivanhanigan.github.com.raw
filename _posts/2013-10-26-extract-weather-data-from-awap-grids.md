---
name: extract-weather-data-from-awap-grids
layout: post
title: Daintree Rainforest Observatory Climate Data from AWAP-GRIDS
date: 2013-10-26
categories:
- awap grids
- extreme weather events
---

<body>

<div id="preamble">

</div>

<div id="content">
<h1 class="title">AWAP GRIDS </h1>


<div id="table-of-contents">
<h2>Table of Contents</h2>
<div id="text-table-of-contents">
<ul>
<li><a href="#sec-1">1 Introduction and Methods</a>
<ul>
<li><a href="#sec-1-1">1.1 Authors</a></li>
<li><a href="#sec-1-2">1.2 Background</a></li>
<li><a href="#sec-1-3">1.3 Material and Methods</a></li>
</ul>
</li>
<li><a href="#sec-2">2 R-code-for-extraction</a></li>
<li><a href="#sec-3">3 Results</a></li>
<li><a href="#sec-4">4 R-code-for-comparison</a></li>
<li><a href="#sec-5">5 Discussion</a></li>
</ul>
</div>
</div>

<div id="outline-container-1" class="outline-3">
<h3 id="sec-1"><span class="section-number-3">1</span> Introduction and Methods</h3>
<div class="outline-text-3" id="text-1">


<p>
This is a work in progress.  It is a stub of an article I want to put together which shows how to use several online data repositories together as a showcase of the [Scientific Workflow and Integration Software for Health (SWISH) Climate Impact Assessments](<a href="https://github.com/swish-climate-impact-assessment">https://github.com/swish-climate-impact-assessment</a>) project.
</p>

</div>

<div id="outline-container-1-1" class="outline-4">
<h4 id="sec-1-1"><span class="section-number-4">1.1</span> Authors</h4>
<div class="outline-text-4" id="text-1-1">

<ul>
<li>Ivan Hanigan and [Markus Nolf](<a href="http://www.thinkoholic.com">http://www.thinkoholic.com</a>)
</li>
</ul>


</div>

</div>

<div id="outline-container-1-2" class="outline-4">
<h4 id="sec-1-2"><span class="section-number-4">1.2</span> Background</h4>
<div class="outline-text-4" id="text-1-2">


<ul>
<li>Markus Nolf offers this use case of the [SWISH EWEDB](<a href="http://swish-climate-impact-assessment.github.io/">http://swish-climate-impact-assessment.github.io/</a>)
</li>
<li>Markus is pulling together his  Daintree Rainforest Observatory (DRO) data into a manuscript for publication, and was looking for climate data from 2012 as well as long-term. 
</li>
<li>More specifically, the annual precipitation and mean annual temperature for both 2012 and the 30-year mean.
</li>
<li>The Australian Bureau of Meteorology has a nice rainfall dataset available at <a href="http://www.bom.gov.au/climate/data/">http://www.bom.gov.au/climate/data/</a> ("Cape Trib Store" weather station), but it seems like the temperature records are patchy.
</li>
<li>So it is advised to use the data the DRO collects its self
</li>
<li>You need to apply through the [ASN SuperSite data portal](<a href="http://www.tern-supersites.net.au/knb/">http://www.tern-supersites.net.au/knb/</a>) for access to the daily data for the DRO.
</li>
<li>Note the use of the DRO met data will need to be properly cited as it is harder to keep
</li>
</ul>

<p>an AWS station running in the tropics for years than it is to collect most other data. 
The citation information is provided when you make a request to access the data.
</p><ul>
<li>The long term mean used by most DRO researchers is from the BOM station as we only have a short record from the station itself.  The offset is around 1000mm.
</li>
<li>However what we want is mean annual temperatures but the BOM website seems to focus more on mean minimum and maximum temperatures.
</li>
</ul>


</div>

</div>

<div id="outline-container-1-3" class="outline-4">
<h4 id="sec-1-3"><span class="section-number-4">1.3</span> Material and Methods</h4>
<div class="outline-text-4" id="text-1-3">


<ul>
<li id="sec-1-3-1">Baseline Climate Data 2012, Far North Queensland Rainforest Supersite, Cape Tribulation Node<br/>

<ul>
<li>We can use the data portal too see [the data file in question](<a href="http://www.tern-supersites.net.au/knb/metacat/lloyd.238.13/html">http://www.tern-supersites.net.au/knb/metacat/lloyd.238.13/html</a>)
</li>
<li>Application for access is via email
</li>
</ul>


</li>
</ul>
<ul>
<li id="sec-1-3-2">Extract mean annual temperatures at the BOM website<br/>

<ul>
<li>SWISH uses BoM data a fair bit and aims to streamline access to BoM data for extreme weather event analysis (which require long term average climatology to provide the baseline that extremes are measured against).
</li>
<li>WRT to temperature most daily averages from BoM are calculated as average of maximum<sub>temperature</sub><sub>in</sub><sub>24</sub><sub>hours</sub><sub>after</sub><sub>9am</sub><sub>local</sub><sub>time</sub><sub>in</sub><sub>degrees</sub> and minimum<sub>temperature</sub><sub>in</sub><sub>24</sub><sub>hours</sub><sub>before</sub><sub>9am</sub><sub>local</sub><sub>time</sub><sub>in</sub><sub>degree</sub> (only couple of hundred AWS provide hourly data to get the proper mean of 24 obs).
</li>
<li>The Bureau of Meteorology has generated a range of gridded meteorological datasets for Australia as a contribution to the Australian Water Availability Project (AWAP). These include daily max and min temperature which you could use to generate daily averages, then calculate your long term averages from those?  
</li>
<li><a href="http://www.bom.gov.au/jsp/awap/">http://www.bom.gov.au/jsp/awap/</a>
</li>
<li>Documentation is at <a href="http://www.bom.gov.au/amm/docs/2009/jones.pdf">http://www.bom.gov.au/amm/docs/2009/jones.pdf</a>
</li>
</ul>


</li>
</ul>
<ul>
<li id="sec-1-3-3">A workflow to download and process the public BoM weather grids.<br/>
<div id="outline-container-1" class="outline-3">
<h3 id="sec-1"><span class="section-number-3">1</span> R-depends</h3>
<div class="outline-text-3" id="text-1">




<pre class="src src-R"><span style="color: #7f9f7f;"># </span><span style="color: #7f9f7f;">depends</span>
install.packages(c(<span style="color: #cc9393;">'raster'</span>, <span style="color: #cc9393;">'rgdal'</span>, <span style="color: #cc9393;">'plyr'</span>, <span style="color: #cc9393;">'RODBC'</span>, <span style="color: #cc9393;">'RCurl'</span>, <span style="color: #cc9393;">'XML'</span>, <span style="color: #cc9393;">'ggmap'</span>, <span style="color: #cc9393;">'maptools'</span>, <span style="color: #cc9393;">'spdep'</span>))

</pre>

</div>
</div>

<ul>
<li>This workflow uses the open source R software with some of our custom written packages:
</li>
</ul>



</li>
</ul>
</div>
</div>

</div>

<div id="outline-container-2" class="outline-3">
<h3 id="sec-2"><span class="section-number-3">2</span> R-code-for-extraction</h3>
<div class="outline-text-3" id="text-2">




<pre class="src src-R"><span style="color: #93a1a1;">################################################################</span>
<span style="color: #93a1a1;"># </span><span style="color: #93a1a1;">name:r-code</span>



<span style="color: #93a1a1;"># </span><span style="color: #93a1a1;">aim daily weather for any point location from online BoM weather grids</span>

<span style="color: #93a1a1;"># </span><span style="color: #93a1a1;">depends on some github packages</span>
<span style="color: #268bd2; font-weight: bold;">require</span>(awaptools)
<span style="color: #93a1a1;">#</span><span style="color: #93a1a1;">http://swish-climate-impact-assessment.github.io/tools/awaptools/awaptools-downloads.html</span>
<span style="color: #268bd2; font-weight: bold;">require</span>(swishdbtools)
<span style="color: #93a1a1;">#</span><span style="color: #93a1a1;">http://swish-climate-impact-assessment.github.io/tools/swishdbtools/swishdbtools-downloads.html</span>
<span style="color: #268bd2; font-weight: bold;">require</span>(gisviz)
<span style="color: #93a1a1;"># </span><span style="color: #93a1a1;">http://ivanhanigan.github.io/gisviz/</span>

<span style="color: #93a1a1;"># </span><span style="color: #93a1a1;">and this from CRAN</span>
<span style="color: #859900; font-weight: bold;">if</span>(!<span style="color: #268bd2; font-weight: bold;">require</span>(raster)) install.packages(<span style="color: #2aa198;">'raster'</span>); <span style="color: #268bd2; font-weight: bold;">require</span>(raster)

<span style="color: #93a1a1;"># </span><span style="color: #93a1a1;">get weather data, beware that each grid is a couple of megabytes</span>
vars <span style="color: #268bd2; font-weight: bold;">&lt;-</span> c(<span style="color: #2aa198;">"maxave"</span>,<span style="color: #2aa198;">"minave"</span>,<span style="color: #2aa198;">"totals"</span>,<span style="color: #2aa198;">"vprph09"</span>,<span style="color: #2aa198;">"vprph15"</span>) <span style="color: #93a1a1;">#</span><span style="color: #93a1a1;">,"solarave") </span>
<span style="color: #93a1a1;"># </span><span style="color: #93a1a1;">solar only available after 1990</span>
<span style="color: #859900; font-weight: bold;">for</span>(measure <span style="color: #859900; font-weight: bold;">in</span> vars)
{
  <span style="color: #93a1a1;">#</span><span style="color: #93a1a1;">measure &lt;- vars[1]</span>
  get_awap_data(start = <span style="color: #2aa198;">'1960-01-01'</span>,end = <span style="color: #2aa198;">'1960-01-02'</span>, measure)
}

<span style="color: #93a1a1;"># </span><span style="color: #93a1a1;">get location</span>
locn <span style="color: #268bd2; font-weight: bold;">&lt;-</span> geocode(<span style="color: #2aa198;">"daintree rainforest"</span>)
<span style="color: #93a1a1;"># </span><span style="color: #93a1a1;">this uses google maps API, better check this</span>
<span style="color: #93a1a1;"># </span><span style="color: #93a1a1;">lon       lat</span>
<span style="color: #93a1a1;"># </span><span style="color: #93a1a1;">1 145.4185 -16.17003</span>
<span style="color: #93a1a1;">## </span><span style="color: #93a1a1;">Treat data frame as spatial points</span>
epsg <span style="color: #268bd2; font-weight: bold;">&lt;-</span> make_EPSG()
shp <span style="color: #268bd2; font-weight: bold;">&lt;-</span> SpatialPointsDataFrame(cbind(locn$lon,locn$lat),locn,
                              proj4string=CRS(epsg$prj4[epsg$code %<span style="color: #859900; font-weight: bold;">in</span>% <span style="color: #2aa198;">'4283'</span>]))
<span style="color: #93a1a1;"># </span><span style="color: #93a1a1;">now loop over grids and extract met data</span>
cfiles <span style="color: #268bd2; font-weight: bold;">&lt;-</span>  dir(pattern=<span style="color: #2aa198;">"grid$"</span>)

<span style="color: #859900; font-weight: bold;">for</span> (i <span style="color: #859900; font-weight: bold;">in</span> seq_len(length(cfiles))) {
  <span style="color: #93a1a1;">#</span><span style="color: #93a1a1;">i &lt;- 1 ## for stepping thru</span>
  gridname <span style="color: #268bd2; font-weight: bold;">&lt;-</span> cfiles[[i]]
  r <span style="color: #268bd2; font-weight: bold;">&lt;-</span> raster(gridname)
  <span style="color: #93a1a1;">#</span><span style="color: #93a1a1;">image(r) # plot to look at</span>
  e <span style="color: #268bd2; font-weight: bold;">&lt;-</span> extract(r, shp, df=T)
  <span style="color: #93a1a1;">#</span><span style="color: #93a1a1;">str(e) ## print for debugging</span>
  e1 <span style="color: #268bd2; font-weight: bold;">&lt;-</span> shp
  e1@data$values <span style="color: #268bd2; font-weight: bold;">&lt;-</span> e[,2]
  e1@data$gridname <span style="color: #268bd2; font-weight: bold;">&lt;-</span> gridname
  <span style="color: #93a1a1;"># </span><span style="color: #93a1a1;">write to to target file</span>
  write.table(e1@data,<span style="color: #2aa198;">"output.csv"</span>,
    col.names = i == 1, append = i&gt;1 , sep = <span style="color: #2aa198;">","</span>, row.names = <span style="color: #b58900;">FALSE</span>)
}

<span style="color: #93a1a1;"># </span><span style="color: #93a1a1;">further work is required to format the column with the gridname to get out the date and weather paramaters.</span>
</pre>

</div>

</div>

<div id="outline-container-3" class="outline-3">
<h3 id="sec-3"><span class="section-number-3">3</span> Results</h3>
<div class="outline-text-3" id="text-3">

<ul>
<li id="sec-3-1">Results<br/>

<ul>
<li>Markus reports:
</li>
<li>"The R-script worked great once i had set a working directory that did not include spaces. (It may have been a different problem that got solved by changing the wd, but the important thing is it's running now.)"
</li>
<li>Markus downloaded 70+ GB of gridded weather data from the BoM website to his local computer
</li>
<li>Also note there is another set of gridded data available from the BOM, which contains pre-computed longterm mean temps, [ready to be extracted with the script](<a href="http://reg.bom.gov.au/jsp/ncc/climate_averages/temperature/index.jsp?maptype=6&amp;period=#maps">http://reg.bom.gov.au/jsp/ncc/climate_averages/temperature/index.jsp?maptype=6&amp;period=#maps</a>)
</li>
<li>"Using this file, I only needed to get the 2012 temp grids for a comparison of 2012 vs. 30-year data. I'm going to run the extraction of 1961-1990 data, just to be sure."
</li>
<li>"When we finished analysis of the long-term temperature from daily means found:
</li>
<li>While the official, pre-computed long-term mean (i.e. 30-year grid file, analysed with your script) was 22.29 °C for the DRO coordinates (145.4494, -16.1041), the new value from daily means (i.e. daily minave and maxave averaged) is 24.91 °C.
</li>
<li>We're not sure what causes this discrepancy, but thought we'd note that there is one.
</li>
<li>For the manuscript, we ended up using the means obtained via BOM's method* to compare 1961-1990 values to 2012, both computed with the above script.
</li>
<li>(* average of daily min/max temperature for each year, then averaged across the entire 30 year period)
</li>
</ul>


</li>
</ul>
<ul>
<li id="sec-3-2">Dataset discrepancy<br/>

<ul>
<li>Following up on the interesting a difference between the two BoM datasets. 
</li>
<li>One thing that might cause this might be if you are calculating the average of the annual averages ie sum(annavs)/30 or the average of all the daily averages as sum(dailyavs)/(30 * 365 or 366)?  the variance will differ by these methods.
</li>
<li>looks like the 30 year dataset is the former:
</li>
<li>"Average annual temperatures (maximum, minimum or mean) are calculated by adding daily temperature values each year, dividing by the number of days in that year to get an average for that particular year. The average values for each year in a specified period (1961 to 1990) are added together and the final value is calculated by dividing by the number of years in the period (30 years in this case)."
</li>
</ul>

<p>[metadata](<a href="http://reg.bom.gov.au/jsp/ncc/climate_averages/temperature/index.jsp?maptype=6&amp;period=#maps">http://reg.bom.gov.au/jsp/ncc/climate_averages/temperature/index.jsp?maptype=6&amp;period=#maps</a>)
</p><ul>
<li>Markus followed the BOM calculation method, and just compared it with two other approaches.
</li>
<li>average of all 21914 values
</li>
<li>average of yearly sum(min and max values per year)/(ndays*2)
</li>
<li>average of yearly sum(daily average)/ndays)
</li>
<li>where ndays = number of days per year.
</li>
<li>Differences between these methods show only in the 6th decimal place, far from 2.62 degrees.
</li>
</ul>



</li>
</ul>
</div>

</div>

<div id="outline-container-4" class="outline-3">
<h3 id="sec-4"><span class="section-number-3">4</span> R-code-for-comparison</h3>
<div class="outline-text-3" id="text-4">




<pre class="src src-R"><span style="color: #93a1a1;">################################################################</span>
<span style="color: #93a1a1;"># </span><span style="color: #93a1a1;">This is Markus' comparison script </span>
<span style="color: #93a1a1;"># </span><span style="color: #93a1a1;">also see the formatted table csv, as well as the SWISH script's raw output csv</span>

setwd(<span style="color: #2aa198;">"E:\\markus\\ph.d\\aus-daintree\\data-analysis\\climate"</span>)
climate <span style="color: #268bd2; font-weight: bold;">&lt;-</span> read.csv(<span style="color: #2aa198;">"minmaxave-30year-daily.csv"</span>, sep=<span style="color: #2aa198;">","</span>, dec=<span style="color: #2aa198;">"."</span>)

climate$year <span style="color: #268bd2; font-weight: bold;">&lt;-</span> substr(climate$file,1,4)
climate$dailymean <span style="color: #268bd2; font-weight: bold;">&lt;-</span> (climate$maxave+climate$minave)/2
head(climate)


<span style="color: #93a1a1;">#</span><span style="color: #93a1a1;">total average across all days and values</span>
annmean <span style="color: #268bd2; font-weight: bold;">&lt;-</span> mean(c(climate$maxave,climate$minave))
annmean


<span style="color: #93a1a1;">#</span><span style="color: #93a1a1;">daily means averaged by year, then total average</span>
annmean1 <span style="color: #268bd2; font-weight: bold;">&lt;-</span> c(1,2)
<span style="color: #859900; font-weight: bold;">for</span>(i <span style="color: #859900; font-weight: bold;">in</span> 1:30) {
        annmean1[i] <span style="color: #268bd2; font-weight: bold;">&lt;-</span> mean(climate[climate$year==(i+1960),]$dailymean)
        <span style="color: #93a1a1;">#</span><span style="color: #93a1a1;">print(annmean1[i])</span>
}
annmean1
mean(annmean1)


<span style="color: #93a1a1;">#</span><span style="color: #93a1a1;">mean of all values per year, then total average</span>
annmean2 <span style="color: #268bd2; font-weight: bold;">&lt;-</span> c(1,2)
<span style="color: #859900; font-weight: bold;">for</span>(i <span style="color: #859900; font-weight: bold;">in</span> 1:30) {
        tmpdata <span style="color: #268bd2; font-weight: bold;">&lt;-</span> climate[climate$year==(i+1960),]
        annmean2[i] <span style="color: #268bd2; font-weight: bold;">&lt;-</span> (sum(tmpdata$maxave) + sum(tmpdata$minave))/(length(tmpdata$maxave)+length(tmpdata$minave))
        <span style="color: #93a1a1;">#</span><span style="color: #93a1a1;">print(annmean2[i])</span>
}
annmean2; mean(annmean2)


<span style="color: #93a1a1;">#</span><span style="color: #93a1a1;">differences</span>
annmean - mean(annmean1)
annmean - mean(annmean2)
mean(annmean1) - mean(annmean2)


</pre>


</div>

</div>

<div id="outline-container-5" class="outline-3">
<h3 id="sec-5"><span class="section-number-3">5</span> Discussion</h3>
<div class="outline-text-3" id="text-5">


<ul>
<li>Principal findings: Very convenient automated extraction of location-based time series data for the precise period that is requested.
</li>
<li>Weaknesses (whole method, not your script): very long download time for daily grids (~11.000 grids = huge dataset, took several days in my case). Yearly grids would be beneficial (and I believe most others are also looking mainly for data on a yearly (or larger) scale).
</li>
</ul>


<ul>
<li id="sec-5-1">Conclusion<br/>

<ul>
<li>Take home message: Seems like a perfect case of "double-check the data using one and the same method".
</li>
</ul>


</li>
</ul>
</div>
</div>
</div>

</body>
</html>
