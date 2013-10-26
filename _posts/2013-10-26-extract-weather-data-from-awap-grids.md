---
name: extract-weather-data-from-awap-grids
layout: post
title: extract-weather-data-from-awap-grids
date: 2013-10-26
categories:
- extreme weather events
---

### extract mean annual temperatures at the BOM website

I use BoM data a fair bit and work on a project that tried to streamline access to BoM data for extreme weather event analysis (which require long term average climatology to provide the baseline that extremes are measured against).

WRT to temperature most daily averages from BoM are calculated as average of maximum_temperature_in_24_hours_after_9am_local_time_in_degrees and minimum_temperature_in_24_hours_before_9am_local_time_in_degree (only couple of hundred AWS provide hourly data to get the proper mean of 24 obs).

The Bureau of Meteorology has generated a range of gridded meteorological datasets for Australia as a contribution to the Australian Water Availability Project (AWAP). These include daily max and min temperature which you could use to generate daily averages, then calculate your long term averages from those?  

http://www.bom.gov.au/jsp/awap/

Documentation is at http://www.bom.gov.au/amm/docs/2009/jones.pdf


I’m working on a workflow to download and process the public BoM weather grids.
It uses the open source R software with some of our custom written packages:
<!-- <?xml version="1.0" encoding="utf-8"?> -->
<!-- <!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Strict//EN" -->
<!--                "http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd"> -->
<!-- <html xmlns="http://www.w3.org/1999/xhtml" lang="en" xml:lang="en"> -->
<!-- <head> -->
<!-- <title>AWAP GRIDS </title> -->
<!-- <meta http-equiv="Content-Type" content="text/html;charset=utf-8"/> -->
<!-- <meta name="title" content="AWAP GRIDS "/> -->
<!-- <meta name="generator" content="Org-mode"/> -->
<!-- <meta name="generated" content="2013-10-26T22:31+1100"/> -->
<!-- <meta name="author" content="Ivan Hanigan"/> -->
<!-- <meta name="description" content=""/> -->
<!-- <meta name="keywords" content=""/> -->
<!-- <style type="text/css"> -->
<!--  <\!--/*-\-><![CDATA[/*><\!--*/ -->
<!--   html { font-family: Times, serif; font-size: 12pt; } -->
<!--   .title  { text-align: center; } -->
<!--   .todo   { color: red; } -->
<!--   .done   { color: green; } -->
<!--   .tag    { background-color: #add8e6; font-weight:normal } -->
<!--   .target { } -->
<!--   .timestamp { color: #bebebe; } -->
<!--   .timestamp-kwd { color: #5f9ea0; } -->
<!--   .right  {margin-left:auto; margin-right:0px;  text-align:right;} -->
<!--   .left   {margin-left:0px;  margin-right:auto; text-align:left;} -->
<!--   .center {margin-left:auto; margin-right:auto; text-align:center;} -->
<!--   p.verse { margin-left: 3% } -->
<!--   pre { -->
<!--    border: 1pt solid #AEBDCC; -->
<!--    background-color: #F3F5F7; -->
<!--    padding: 5pt; -->
<!--    font-family: courier, monospace; -->
<!--         font-size: 90%; -->
<!--         overflow:auto; -->
<!--   } -->
<!--   table { border-collapse: collapse; } -->
<!--   td, th { vertical-align: top;  } -->
<!--   th.right  { text-align:center;  } -->
<!--   th.left   { text-align:center;   } -->
<!--   th.center { text-align:center; } -->
<!--   td.right  { text-align:right;  } -->
<!--   td.left   { text-align:left;   } -->
<!--   td.center { text-align:center; } -->
<!--   dt { font-weight: bold; } -->
<!--   div.figure { padding: 0.5em; } -->
<!--   div.figure p { text-align: center; } -->
<!--   div.inlinetask { -->
<!--     padding:10px; -->
<!--     border:2px solid gray; -->
<!--     margin:10px; -->
<!--     background: #ffffcc; -->
<!--   } -->
<!--   textarea { overflow-x: auto; } -->
<!--   .linenr { font-size:smaller } -->
<!--   .code-highlighted {background-color:#ffff00;} -->
<!--   .org-info-js_info-navigation { border-style:none; } -->
<!--   #org-info-js_console-label { font-size:10px; font-weight:bold; -->
<!--                                white-space:nowrap; } -->
<!--   .org-info-js_search-highlight {background-color:#ffff00; color:#000000; -->
<!--                                  font-weight:bold; } -->
<!--   /*]]>*/-\-> -->
<!-- </style> -->
<!-- <script type="text/javascript"> -->
<!-- /* -->
<!-- @licstart  The following is the entire license notice for the -->
<!-- JavaScript code in this tag. -->

<!-- Copyright (C) 2012-2013 Free Software Foundation, Inc. -->

<!-- The JavaScript code in this tag is free software: you can -->
<!-- redistribute it and/or modify it under the terms of the GNU -->
<!-- General Public License (GNU GPL) as published by the Free Software -->
<!-- Foundation, either version 3 of the License, or (at your option) -->
<!-- any later version.  The code is distributed WITHOUT ANY WARRANTY; -->
<!-- without even the implied warranty of MERCHANTABILITY or FITNESS -->
<!-- FOR A PARTICULAR PURPOSE.  See the GNU GPL for more details. -->

<!-- As additional permission under GNU GPL version 3 section 7, you -->
<!-- may distribute non-source (e.g., minimized or compacted) forms of -->
<!-- that code without the copy of the GNU GPL normally required by -->
<!-- section 4, provided you include this license notice and a URL -->
<!-- through which recipients can access the Corresponding Source. -->


<!-- @licend  The above is the entire license notice -->
<!-- for the JavaScript code in this tag. -->
<!-- */ -->
<!-- <\!--/*-\-><![CDATA[/*><\!--*/ -->
<!--  function CodeHighlightOn(elem, id) -->
<!--  { -->
<!--    var target = document.getElementById(id); -->
<!--    if(null != target) { -->
<!--      elem.cacheClassElem = elem.className; -->
<!--      elem.cacheClassTarget = target.className; -->
<!--      target.className = "code-highlighted"; -->
<!--      elem.className   = "code-highlighted"; -->
<!--    } -->
<!--  } -->
<!--  function CodeHighlightOff(elem, id) -->
<!--  { -->
<!--    var target = document.getElementById(id); -->
<!--    if(elem.cacheClassElem) -->
<!--      elem.className = elem.cacheClassElem; -->
<!--    if(elem.cacheClassTarget) -->
<!--      target.className = elem.cacheClassTarget; -->
<!--  } -->
<!-- /*]]>*///-\-> -->
<!-- </script> -->

<!-- </head> -->
<body>

<div id="preamble">

</div>

<div id="content">
<h1 class="title">AWAP GRIDS </h1>


<div id="table-of-contents">
<h2>Table of Contents</h2>
<div id="text-table-of-contents">
<ul>
<li><a href="#sec-1">1 r-code-code</a></li>
</ul>
</div>
</div>

<div id="outline-container-1" class="outline-3">
<h3 id="sec-1"><span class="section-number-3">1</span> r-code-code</h3>
<div class="outline-text-3" id="text-1">




<pre class="src src-R"><span style="color: #586e75;">################################################################</span>
<span style="color: #586e75;"># </span><span style="color: #586e75;">name:r-code</span>



<span style="color: #586e75;"># </span><span style="color: #586e75;">aim daily weather for any point location from online BoM weather grids</span>

<span style="color: #586e75;"># </span><span style="color: #586e75;">depends on some github packages</span>
<span style="color: #268bd2; font-weight: bold;">require</span>(awaptools)
<span style="color: #586e75;">#</span><span style="color: #586e75;">http://swish-climate-impact-assessment.github.io/tools/awaptools/awaptools-downloads.html</span>
<span style="color: #268bd2; font-weight: bold;">require</span>(swishdbtools)
<span style="color: #586e75;">#</span><span style="color: #586e75;">http://swish-climate-impact-assessment.github.io/tools/swishdbtools/swishdbtools-downloads.html</span>
<span style="color: #268bd2; font-weight: bold;">require</span>(gisviz)
<span style="color: #586e75;"># </span><span style="color: #586e75;">http://ivanhanigan.github.io/gisviz/</span>

<span style="color: #586e75;"># </span><span style="color: #586e75;">and this from CRAN</span>
<span style="color: #859900; font-weight: bold;">if</span>(!<span style="color: #268bd2; font-weight: bold;">require</span>(raster)) install.packages(<span style="color: #2aa198;">'raster'</span>); <span style="color: #268bd2; font-weight: bold;">require</span>(raster)

<span style="color: #586e75;"># </span><span style="color: #586e75;">get weather data, beware that each grid is a couple of megabytes</span>
vars <span style="color: #268bd2; font-weight: bold;">&lt;-</span> c(<span style="color: #2aa198;">"maxave"</span>,<span style="color: #2aa198;">"minave"</span>,<span style="color: #2aa198;">"totals"</span>,<span style="color: #2aa198;">"vprph09"</span>,<span style="color: #2aa198;">"vprph15"</span>) <span style="color: #586e75;">#</span><span style="color: #586e75;">,"solarave") </span>
<span style="color: #586e75;"># </span><span style="color: #586e75;">solar only available after 1990</span>
<span style="color: #859900; font-weight: bold;">for</span>(measure <span style="color: #859900; font-weight: bold;">in</span> vars)
{
  <span style="color: #586e75;">#</span><span style="color: #586e75;">measure &lt;- vars[1]</span>
  get_awap_data(start = <span style="color: #2aa198;">'1960-01-01'</span>,end = <span style="color: #2aa198;">'1960-01-02'</span>, measure)
}

<span style="color: #586e75;"># </span><span style="color: #586e75;">get location</span>
locn <span style="color: #268bd2; font-weight: bold;">&lt;-</span> geocode(<span style="color: #2aa198;">"daintree rainforest"</span>)
<span style="color: #586e75;"># </span><span style="color: #586e75;">this uses google maps API, better check this</span>
<span style="color: #586e75;"># </span><span style="color: #586e75;">lon       lat</span>
<span style="color: #586e75;"># </span><span style="color: #586e75;">1 145.4185 -16.17003</span>
<span style="color: #586e75;">## </span><span style="color: #586e75;">Treat data frame as spatial points</span>
epsg <span style="color: #268bd2; font-weight: bold;">&lt;-</span> make_EPSG()
shp <span style="color: #268bd2; font-weight: bold;">&lt;-</span> SpatialPointsDataFrame(cbind(locn$lon,locn$lat),locn,
                              proj4string=CRS(epsg$prj4[epsg$code %<span style="color: #859900; font-weight: bold;">in</span>% <span style="color: #2aa198;">'4283'</span>]))
<span style="color: #586e75;"># </span><span style="color: #586e75;">now loop over grids and extract met data</span>
cfiles <span style="color: #268bd2; font-weight: bold;">&lt;-</span>  dir(pattern=<span style="color: #2aa198;">"grid$"</span>)

<span style="color: #859900; font-weight: bold;">for</span> (i <span style="color: #859900; font-weight: bold;">in</span> seq_len(length(cfiles))) {
  <span style="color: #586e75;">#</span><span style="color: #586e75;">i &lt;- 1 ## for stepping thru</span>
  gridname <span style="color: #268bd2; font-weight: bold;">&lt;-</span> cfiles[[i]]
  r <span style="color: #268bd2; font-weight: bold;">&lt;-</span> raster(gridname)
  <span style="color: #586e75;">#</span><span style="color: #586e75;">image(r) # plot to look at</span>
  e <span style="color: #268bd2; font-weight: bold;">&lt;-</span> extract(r, shp, df=T)
  <span style="color: #586e75;">#</span><span style="color: #586e75;">str(e) ## print for debugging</span>
  e1 <span style="color: #268bd2; font-weight: bold;">&lt;-</span> shp
  e1@data$values <span style="color: #268bd2; font-weight: bold;">&lt;-</span> e[,2]
  e1@data$gridname <span style="color: #268bd2; font-weight: bold;">&lt;-</span> gridname
  <span style="color: #586e75;"># </span><span style="color: #586e75;">write to to target file</span>
  write.table(e1@data,<span style="color: #2aa198;">"output.csv"</span>,
    col.names = i == 1, append = i&gt;1 , sep = <span style="color: #2aa198;">","</span>, row.names = <span style="color: #b58900;">FALSE</span>)
}

<span style="color: #586e75;"># </span><span style="color: #586e75;">further work is required to format the column with the gridname to get out the date and weather paramaters.</span>
</pre>


</div>
</div>
</div>

</body>
<!-- </html> -->
