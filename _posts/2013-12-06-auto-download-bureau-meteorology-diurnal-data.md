---
name: 2013-12-06-auto-download-bureau-meteorology-diurnal-data
layout: post
title: auto-download-bureau-meteorology-diurnal-data
date: 2013-12-06
categories:
- extreme weather events
---
<head>
<title>Excess Heat Indices </title>
<meta http-equiv="Content-Type" content="text/html;charset=iso-8859-1"/>
<meta name="title" content="Excess Heat Indices "/>
<meta name="generator" content="Org-mode"/>
<meta name="generated" content="2013-12-07T23:25+1100"/>
<meta name="author" content="Ivan Hanigan"/>
<meta name="description" content=""/>
<meta name="keywords" content=""/>
<style type="text/css">
 <!--/*--><![CDATA[/*><!--*/
  html { font-family: Times, serif; font-size: 12pt; }
  .title  { text-align: center; }
  .todo   { color: red; }
  .done   { color: green; }
  .tag    { background-color: #add8e6; font-weight:normal }
  .target { }
  .timestamp { color: #bebebe; }
  .timestamp-kwd { color: #5f9ea0; }
  .right  {margin-left:auto; margin-right:0px;  text-align:right;}
  .left   {margin-left:0px;  margin-right:auto; text-align:left;}
  .center {margin-left:auto; margin-right:auto; text-align:center;}
  p.verse { margin-left: 3% }
  pre {
        border: 1pt solid #AEBDCC;
        background-color: #F3F5F7;
        padding: 5pt;
        font-family: courier, monospace;
        font-size: 90%;
        overflow:auto;
  }
  table { border-collapse: collapse; }
  td, th { vertical-align: top;  }
  th.right  { text-align:center;  }
  th.left   { text-align:center;   }
  th.center { text-align:center; }
  td.right  { text-align:right;  }
  td.left   { text-align:left;   }
  td.center { text-align:center; }
  dt { font-weight: bold; }
  div.figure { padding: 0.5em; }
  div.figure p { text-align: center; }
  div.inlinetask {
    padding:10px;
    border:2px solid gray;
    margin:10px;
    background: #ffffcc;
  }
  textarea { overflow-x: auto; }
  .linenr { font-size:smaller }
  .code-highlighted {background-color:#ffff00;}
  .org-info-js_info-navigation { border-style:none; }
  #org-info-js_console-label { font-size:10px; font-weight:bold;
                               white-space:nowrap; }
  .org-info-js_search-highlight {background-color:#ffff00; color:#000000;
                                 font-weight:bold; }
  /*]]>*/-->
</style>
<script type="text/javascript">
/*
@licstart  The following is the entire license notice for the
JavaScript code in this tag.

Copyright (C) 2012-2013 Free Software Foundation, Inc.

The JavaScript code in this tag is free software: you can
redistribute it and/or modify it under the terms of the GNU
General Public License (GNU GPL) as published by the Free Software
Foundation, either version 3 of the License, or (at your option)
any later version.  The code is distributed WITHOUT ANY WARRANTY;
without even the implied warranty of MERCHANTABILITY or FITNESS
FOR A PARTICULAR PURPOSE.  See the GNU GPL for more details.

As additional permission under GNU GPL version 3 section 7, you
may distribute non-source (e.g., minimized or compacted) forms of
that code without the copy of the GNU GPL normally required by
section 4, provided you include this license notice and a URL
through which recipients can access the Corresponding Source.


@licend  The above is the entire license notice
for the JavaScript code in this tag.
*/
<!--/*--><![CDATA[/*><!--*/
 function CodeHighlightOn(elem, id)
 {
   var target = document.getElementById(id);
   if(null != target) {
     elem.cacheClassElem = elem.className;
     elem.cacheClassTarget = target.className;
     target.className = "code-highlighted";
     elem.className   = "code-highlighted";
   }
 }
 function CodeHighlightOff(elem, id)
 {
   var target = document.getElementById(id);
   if(elem.cacheClassElem)
     elem.className = elem.cacheClassElem;
   if(elem.cacheClassTarget)
     target.className = elem.cacheClassTarget;
 }
/*]]>*///-->
</script>

</head>
<body>

<div id="preamble">

</div>

<div id="content">
<h1 class="title">Excess Heat Indices </h1>


<div id="table-of-contents">
<h2>Table of Contents</h2>
<div id="text-table-of-contents">
<ul>
<li><a href="#sec-1">1 auto-download-bureau-meteorology-diurnal-data</a>
<ul>
<li><a href="#sec-1-1">1.1 First the FTP server URL structure</a></li>
<li><a href="#sec-1-2">1.2 table</a></li>
<li><a href="#sec-1-3">1.3 R Code: bom<sub>download</sub>.r</a></li>
<li><a href="#sec-1-4">1.4 R Code: bom<sub>collation</sub>.r</a></li>
<li><a href="#sec-1-5">1.5 BAT file (windoze)</a></li>
<li><a href="#sec-1-6">1.6 check the data</a></li>
<li><a href="#sec-1-7">1.7 Conclusions</a></li>
</ul>
</li>
</ul>
</div>
</div>

<div id="outline-container-1" class="outline-3">
<h3 id="sec-1"><span class="section-number-3">1</span> auto-download-bureau-meteorology-diurnal-data</h3>
<div class="outline-text-3" id="text-1">


<ul>
<li>We;re looking at health impacts of high temperatures at work 
</li>
<li>need to see the highest temperatures during the working hours
</li>
<li>bom provides hourly data for download, but only 3 days at a time
</li>
<li>we build a script and set it on a schedule to run every day, download the data and collate the results
</li>
</ul>



</div>

<div id="outline-container-1-1" class="outline-4">
<h4 id="sec-1-1"><span class="section-number-4">1.1</span> First the FTP server URL structure</h4>
<div class="outline-text-4" id="text-1-1">


<ul>
<li>The URLS are predictable, just need the station id, state and a code if metro or rural
</li>
</ul>


</div>

</div>

<div id="outline-container-1-2" class="outline-4">
<h4 id="sec-1-2"><span class="section-number-4">1.2</span> table</h4>
<div class="outline-text-4" id="text-1-2">

<table border="2" cellspacing="0" cellpadding="6" rules="groups" frame="hsides">
<colgroup><col class="right" /><col class="left" /><col class="right" />
</colgroup>
<tbody>
<tr><td class="right">Station<sub>ID</sub></td><td class="left">State</td><td class="right">City<sub>9</sub><sub>or</sub><sub>regional</sub><sub>8</sub>_</td></tr>
<tr><td class="right">94774</td><td class="left">N</td><td class="right">9</td></tr>
<tr><td class="right">95719</td><td class="left">N</td><td class="right">8</td></tr>
<tr><td class="right">94768</td><td class="left">N</td><td class="right">9</td></tr>
<tr><td class="right">94763</td><td class="left">N</td><td class="right">9</td></tr>
<tr><td class="right">94767</td><td class="left">N</td><td class="right">9</td></tr>
<tr><td class="right">94910</td><td class="left">N</td><td class="right">8</td></tr>
<tr><td class="right">94929</td><td class="left">N</td><td class="right">8</td></tr>
<tr><td class="right">95896</td><td class="left">N</td><td class="right">8</td></tr>
<tr><td class="right">94693</td><td class="left">N</td><td class="right">8</td></tr>
<tr><td class="right">94691</td><td class="left">N</td><td class="right">8</td></tr>
<tr><td class="right">95677</td><td class="left">S</td><td class="right">9</td></tr>
<tr><td class="right">94675</td><td class="left">S</td><td class="right">9</td></tr>
<tr><td class="right">94672</td><td class="left">S</td><td class="right">9</td></tr>
<tr><td class="right">94866</td><td class="left">V</td><td class="right">9</td></tr>
<tr><td class="right">95867</td><td class="left">V</td><td class="right">9</td></tr>
<tr><td class="right">94868</td><td class="left">V</td><td class="right">9</td></tr>
<tr><td class="right">94875</td><td class="left">V</td><td class="right">8</td></tr>
</tbody>
</table>




<ul>
<li>now create a script called "bom<sub>download</sub>.r"
</li>
<li>it takes the station details and paste into the URLs
</li>
<li>downloads the files
</li>
<li>stores in a directory for each days downloads
</li>
</ul>



</div>

</div>

<div id="outline-container-1-3" class="outline-4">
<h4 id="sec-1-3"><span class="section-number-4">1.3</span> R Code: bom<sub>download</sub>.r</h4>
<div class="outline-text-4" id="text-1-3">




<pre class="src src-R">filename = <span style="color: #2aa198;">"~/data/ExcessHeatIndices/inst/doc/weather_stations.csv"</span>
output_directory = <span style="color: #2aa198;">"~/bom-downloads"</span>
setwd(output_directory)

urls <span style="color: #268bd2; font-weight: bold;">&lt;-</span> read.csv(filename)
urls_list <span style="color: #268bd2; font-weight: bold;">&lt;-</span> paste(sep = <span style="color: #2aa198;">""</span>, <span style="color: #2aa198;">"http://www.bom.gov.au/fwo/ID"</span>,
                  urls$State,
                  <span style="color: #2aa198;">"60"</span>, 
                  urls$City_9_or_regional_8_,
                  <span style="color: #2aa198;">"01/ID"</span>,
                  urls$State,
                  <span style="color: #2aa198;">"60"</span>,
                  urls$City_9_or_regional_8_,
                  <span style="color: #2aa198;">"01."</span>,
                  urls$Station_ID,
                  <span style="color: #2aa198;">".axf"</span>)

output_directory <span style="color: #268bd2; font-weight: bold;">&lt;-</span> file.path(output_directory,Sys.Date())
dir.create(output_directory)

<span style="color: #859900; font-weight: bold;">for</span>(url <span style="color: #859900; font-weight: bold;">in</span> urls_list)
{
  output_file <span style="color: #268bd2; font-weight: bold;">&lt;-</span> file.path(output_directory,basename(url))
  download.file(url, output_file, mode = <span style="color: #2aa198;">"wb"</span>)

}
print(<span style="color: #2aa198;">"SUCCESS"</span>)

</pre>




<ul>
<li>Now the data can be combined
</li>
<li>clean up the header and extraneous extra line at the bottom
</li>
</ul>


</div>

</div>

<div id="outline-container-1-4" class="outline-4">
<h4 id="sec-1-4"><span class="section-number-4">1.4</span> R Code: bom<sub>collation</sub>.r</h4>
<div class="outline-text-4" id="text-1-4">





<pre class="src src-R"><span style="color: #586e75;"># </span><span style="color: #586e75;">this takes data in directories from bom_download.r</span>
 
<span style="color: #586e75;"># </span><span style="color: #586e75;">first get list of directories</span>
filelist <span style="color: #268bd2; font-weight: bold;">&lt;-</span> dir(pattern = <span style="color: #2aa198;">"axf"</span>, recursive = T)
filelist
 
<span style="color: #586e75;"># </span><span style="color: #586e75;">next get directories for days we haven't done yet</span>
<span style="color: #859900; font-weight: bold;">if</span>(file.exists(<span style="color: #2aa198;">"complete_dataset.csv"</span>))
{
complete_data <span style="color: #268bd2; font-weight: bold;">&lt;-</span> read.csv(<span style="color: #2aa198;">"complete_dataset.csv"</span>, stringsAsFactors = F)
<span style="color: #586e75;">#</span><span style="color: #586e75;">str(complete_data)</span>
last_collated <span style="color: #268bd2; font-weight: bold;">&lt;-</span> max(as.Date(complete_data$date_downloaded))
<span style="color: #586e75;">#</span><span style="color: #586e75;">max(complete_data$local_hrmin)</span>
 
days_downloaded <span style="color: #268bd2; font-weight: bold;">&lt;-</span> dirname(filelist)
filelist <span style="color: #268bd2; font-weight: bold;">&lt;-</span> filelist[which(as.Date(days_downloaded) &gt; as.Date(last_collated))]
}
 
<span style="color: #586e75;"># </span><span style="color: #586e75;">for these collate them into the complete file</span>
<span style="color: #859900; font-weight: bold;">for</span>(f <span style="color: #859900; font-weight: bold;">in</span> filelist)
{
  <span style="color: #586e75;">#</span><span style="color: #586e75;">f &lt;- filelist[2]</span>
  print(f)
  fin <span style="color: #268bd2; font-weight: bold;">&lt;-</span> read.csv(f, colClasses = c(<span style="color: #2aa198;">"local_date_time_full.80."</span> = <span style="color: #2aa198;">"character"</span>), 
    stringsAsFactors = F, skip = 19)
  fin <span style="color: #268bd2; font-weight: bold;">&lt;-</span> fin[1:(nrow(fin) - 1),]
  fin$date_downloaded <span style="color: #268bd2; font-weight: bold;">&lt;-</span> dirname(f)
  fin$local_year <span style="color: #268bd2; font-weight: bold;">&lt;-</span> substr(fin$local_date_time_full.80., 1, 4)
  fin$local_month <span style="color: #268bd2; font-weight: bold;">&lt;-</span> substr(fin$local_date_time_full.80., 5, 6)
  fin$local_day <span style="color: #268bd2; font-weight: bold;">&lt;-</span> substr(fin$local_date_time_full.80., 7, 8)
  fin$local_hrmin <span style="color: #268bd2; font-weight: bold;">&lt;-</span> substr(fin$local_date_time_full.80., 9, 12)
  fin$local_date <span style="color: #268bd2; font-weight: bold;">&lt;-</span> paste(fin$local_year, fin$local_month, fin$local_day, sep = <span style="color: #2aa198;">"-"</span>)
  <span style="color: #859900; font-weight: bold;">if</span>(file.exists(<span style="color: #2aa198;">"complete_dataset.csv"</span>))
  {
  write.table(fin, <span style="color: #2aa198;">"complete_dataset.csv"</span>, row.names = F, sep = <span style="color: #2aa198;">","</span>, append = T, col.names = F)
  } <span style="color: #859900; font-weight: bold;">else</span> {
  write.table(fin, <span style="color: #2aa198;">"complete_dataset.csv"</span>, row.names = F, sep = <span style="color: #2aa198;">","</span>)
  }
}
</pre>


<ul>
<li>so now let;s automate the process
</li>
<li>make a BAT file
</li>
</ul>


</div>

</div>

<div id="outline-container-1-5" class="outline-4">
<h4 id="sec-1-5"><span class="section-number-4">1.5</span> BAT file (windoze)</h4>
<div class="outline-text-4" id="text-1-5">





<pre class="src src-R"><span style="color: #2aa198;">"C:\Program Files\R\R-2.15.2\bin\Rscript.exe"</span> <span style="color: #2aa198;">"~\bom-downloads\bom_download.r"</span>
</pre>


<ul>
<li>add this  bat file to the scheduled tasks in your control panel
</li>
<li>use chron for a linux version
</li>
</ul>



</div>

</div>

<div id="outline-container-1-6" class="outline-4">
<h4 id="sec-1-6"><span class="section-number-4">1.6</span> check the data</h4>
<div class="outline-text-4" id="text-1-6">




<pre class="src src-R"><span style="color: #586e75;">#### </span><span style="color: #586e75;">name:check the data ####</span>
<span style="color: #268bd2; font-weight: bold;">require</span>(plyr)

setwd(<span style="color: #2aa198;">"~/bom-downloads"</span>)
<span style="color: #268bd2; font-weight: bold;">source</span>(<span style="color: #2aa198;">"bom_download.r"</span>)
dir()
<span style="color: #268bd2; font-weight: bold;">source</span>(<span style="color: #2aa198;">"bom_collation.r"</span>)

complete_data <span style="color: #268bd2; font-weight: bold;">&lt;-</span> read.csv(<span style="color: #2aa198;">"complete_dataset.csv"</span>, stringsAsFactors = F)
str(complete_data)

<span style="color: #586e75;"># </span><span style="color: #586e75;">Quick and dirty de-duplication</span>
table(complete_data$name.80.)
qc <span style="color: #268bd2; font-weight: bold;">&lt;-</span> subset(complete_data, name.80. == <span style="color: #2aa198;">"Broken Hill Airport"</span>)
qc <span style="color: #268bd2; font-weight: bold;">&lt;-</span> ddply(qc, <span style="color: #2aa198;">"local_date_time_full.80."</span>,
  summarise, apparent_temp = mean(apparent_t))

names(qc)
png(<span style="color: #2aa198;">"qc-diurnal-plot.png"</span>)
with(qc,
     plot(apparent_temp, type= <span style="color: #2aa198;">"l"</span>)
     )
dev.off()
</pre>


<p>
<img src="/images/qc-diurnal-plot.png"  alt="qc-diurnal-plot.png" />
</p>
</div>

</div>

<div id="outline-container-1-7" class="outline-4">
<h4 id="sec-1-7"><span class="section-number-4">1.7</span> Conclusions</h4>
<div class="outline-text-4" id="text-1-7">


<ul>
<li>watch the data roll on in
</li>
<li>each day there are about 3 days downloaded
</li>
<li>meaning duplicates will be frequent, need to write a script to de-duplicate
</li>
<li>cheers!
</li>
</ul>


</div>
</div>
</div>
</div>

</body>
</html>
