---
name: 2014-04-20-using-morpho-for-cataloguing-personal-research-data
layout: post
title: Using Morpho for Cataloguing Personal Research Data
date: 2014-04-20
categories:
- Data Documentation
---
  
  

<div id="table-of-contents">
<h2>Table of Contents</h2>
<div id="text-table-of-contents">
<ul>
<li><a href="#sec-1">1 2014-04-20-using-morpho-orgmode</a>
<ul>
<li><a href="#sec-1-1">1.1 Introduction</a></li>
<li><a href="#sec-1-2">1.2 Cataloguing Personal Research Data with Morpho</a></li>
<li><a href="#sec-1-3">1.3 How Morpho Works</a></li>
<li><a href="#sec-1-4">1.4 Adding a dataset from my collection</a></li>
<li><a href="#sec-1-5">1.5 the drought dataset:</a></li>
<li><a href="#sec-1-6">1.6 Step One: define the project that I will keep locally</a></li>
<li><a href="#sec-1-7">1.7 Contextual Metadata</a></li>
<li><a href="#sec-1-8">1.8 Abstract</a></li>
<li><a href="#sec-1-9">1.9 Australian FOR codes</a></li>
<li><a href="#sec-1-10">1.10 GCMD Keywords</a></li>
<li><a href="#sec-1-11">1.11 Geographic coverage</a></li>
<li><a href="#sec-1-12">1.12 Save the metadata</a></li>
<li><a href="#sec-1-13">1.13 Additional Metadata</a></li>
</ul>
</li>
</ul>
</div>
</div>
 
<div id="outline-container-1" class="outline-3">
<h3 id="sec-1"><span class="section-number-3">1</span> 2014-04-20-using-morpho-orgmode</h3>
<div class="outline-text-3" id="text-1">
  
<?xml version="1.0" encoding="utf-8"?>
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Strict//EN"
               "http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd">
<html xmlns="http://www.w3.org/1999/xhtml" lang="en" xml:lang="en">
<head>
<meta http-equiv="Content-Type" content="text/html;charset=utf-8"/>
<meta name="generator" content="Org-mode"/>
<meta name="generated" content="2014-04-19T22:38+1000"/>
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
  
  
</div>

<div id="outline-container-1-1" class="outline-4">
<h4 id="sec-1-1"><span class="section-number-4">1.1</span>Introduction</h4>
<div class="outline-text-4" id="text-1-1">


<p>
The collection of scientific data is undertaken at an individual level
by everybody in their own way. The layout of data collections that I
have seen is incredibly varied; spread across multiple files and folders which can
be difficult to navigate or search through. In some cases
these collections are incomprehensible to all but the individual themselves. Given
that a lot of projects are collaborative in nature and require
extensive sharing, it is important that scientists maintain their
data collection by some form of system that allows easy data extraction and
use in other projects. Therefore, the maintenance of a personal catalogue of datasets is an
important activity for scientists.
</p>
<p>
By cataloguing I mean that a file or database is kept that stores all the
information about the names of the datasets (and any other files the
data may be spread across), where the datasets are located, any
references (papers) that were developed from it and finally
important information regarding the conditions it
was formed under.
</p>
<p>
While this may seem laborious, it keeps track of all the data that one
has collected over time and gives one a reference system to find a
dataset of interest when sharing with collaborators. Datasets can be
saved in any filing system the scientist chooses, but with the help of
their personal data catalogue they will always know the status of
their data collection.
</p>
</div>

</div>

<div id="outline-container-1-2" class="outline-4">
<h4 id="sec-1-2"><span class="section-number-4">1.2</span> Cataloguing Personal Research Data with Morpho</h4>
<div class="outline-text-4" id="text-1-2">


<p>
[Metacat](<a href="https://knb.ecoinformatics.org/knb/docs/intro.html">https://knb.ecoinformatics.org/knb/docs/intro.html</a>) is an
online repository for data and metadata. It is a great resource for
the publication of data, but not very useful for an individual
scientist to use on their personal computer.  However
[Morpho](<a href="https://knb.ecoinformatics.org/#tools/morpho">https://knb.ecoinformatics.org/#tools/morpho</a>) the Metadata
Editor used by Metacat may be used locally by a researcher to
catalogue their collection (and ultimately this will make publishing
elements of the collection easier.)  Morpho uses the Ecological
Metadata Language (EML) to author metadata with a graphical user
interface wizard.
</p>
<p>
I am using morpho 1.8 due to my group using older metacat server.
</p>
</div>

</div>

<div id="outline-container-1-3" class="outline-4">
<h4 id="sec-1-3"><span class="section-number-4">1.3</span> How Morpho Works</h4>
<div class="outline-text-4" id="text-1-3">


<p>
When you install Morpho it creates a directory where you can run the
program from, and another hidden directory called ".morpho" for it's
database of all your metadata (and optionally any data you import to
it).  Below is an image of mine, with a couple of test records I
played around with (the XMLs/HTMLs) and a dataset I imported (the text
file).
</p>
<ul>
<li>~/.morpho/profiles/hanigan/data/hanigan/
</li>
</ul>

<p>
<img src="/images/morphodir1.png" alt="morphodir1.png">
</p>
<p>  
Every time a modification is made to the metadata a new XML is saved here, with the major number being the ID of the package and incremented minor number to reflect the change.
</p>
<p>
The GUI is tedious.
</p>

</div>

</div>

<div id="outline-container-1-4" class="outline-4">
<h4 id="sec-1-4"><span class="section-number-4">1.4</span> Adding a dataset from my collection</h4>
<div class="outline-text-4" id="text-1-4">


<p>
I have already got a good amount of metadata I generated when I published [the drought data](<a href="http://dx.doi.org/10.4225/13/50BBFD7E6727A">http://dx.doi.org/10.4225/13/50BBFD7E6727A</a>)
</p>
</div>

</div>

<div id="outline-container-1-5" class="outline-4">
<h4 id="sec-1-5"><span class="section-number-4">1.5</span> the drought dataset:</h4>
<div class="outline-text-4" id="text-1-5">

<p>    Hanigan, Ivan (2012): Monthly drought data for Australia 1890-2008
    using the Hutchinson Drought Index. Australian National University Data Commons.
    DOI: 10.4225/13/50BBFD7E6727A. 
</p>
<p>
&lt;p&gt;&lt;/p&gt;
</p>
</div>

</div>

<div id="outline-container-1-6" class="outline-4">
<h4 id="sec-1-6"><span class="section-number-4">1.6</span> Step One: define the project that I will keep locally</h4>
<div class="outline-text-4" id="text-1-6">


<ul>
<li>This is the Github repo <a href="https://github.com/swish-climate-impact-assessment/DROUGHT-BOM-GRIDS">https://github.com/swish-climate-impact-assessment/DROUGHT-BOM-GRIDS</a>
</li>
<li>I store this locally at ~/data/DROUGHT-BOM-GRIDS
</li>
</ul>


</div>

</div>

<div id="outline-container-1-7" class="outline-4">
<h4 id="sec-1-7"><span class="section-number-4">1.7</span> Contextual Metadata</h4>
<div class="outline-text-4" id="text-1-7">


</div>

</div>

<div id="outline-container-1-8" class="outline-4">
<h4 id="sec-1-8"><span class="section-number-4">1.8</span> Abstract</h4>
<div class="outline-text-4" id="text-1-8">


<p>
I originally wrote the abstract as the description for a RIF-CS metadata object to publish for the ANU library.
</p>
<p>
I got the following instructions from a Librarian: The "informative abstract" method.
</p>
<ul>
<li>The abstract should be a descriptive of the data, not the research.
</li>
<li>Briefly outline the relevant project or study and describe the contents of the data package. 
</li>
<li>Include geographic location, the primary objectives of the study, what data was collected (species or phenomena), the year range the data was collected in, and collection frequency if applicable.
</li>
<li>Describe methodology techniques or approaches only to the degree necessary for comprehension – don’t go into any detail.
</li>
<li>Cite references and/or links to any publications that are related to the data package.
</li>
<li>Single paragraph
</li>
<li>200-250 words
</li>
<li>Use active voice and past tense.
</li>
<li>Use short complete sentences.
</li>
<li>Express terms in both their abbreviated and spelled out form for search retrieval purposes.
</li>
</ul>


</div>

</div>

<div id="outline-container-1-9" class="outline-4">
<h4 id="sec-1-9"><span class="section-number-4">1.9</span> Australian FOR codes</h4>
<div class="outline-text-4" id="text-1-9">

<p>ANZSRC-FOR Codes: Australian and New Zealand Standard Research Classification – Fields of Research codes allow R&amp;D activity to be categorised according to the methodology used in the R&amp;D, rather than the activity of the unit performing the R&amp;D or the purpose of the R&amp;D.  
<a href="http://www.abs.gov.au/Ausstats/abs@.nsf/Latestproducts/4AE1B46AE2048A28CA25741800044242?opendocument">http://www.abs.gov.au/Ausstats/abs@.nsf/Latestproducts/4AE1B46AE2048A28CA25741800044242?opendocument</a>
</p>
</div>

</div>

<div id="outline-container-1-10" class="outline-4">
<h4 id="sec-1-10"><span class="section-number-4">1.10</span> GCMD Keywords</h4>
<div class="outline-text-4" id="text-1-10">

<p>Olsen, L.M., G. Major, K. Shein, J. Scialdone, S. Ritz, T. Stevens, M. Morahan, A. Aleman, R. Vogel, S. Leicester, H. Weir, M. Meaux, S. Grebas, C.Solomon, M. Holland, T. Northcutt, R. A. Restrepo, R. Bilodeau, 2013. NASA/Global Change Master Directory (GCMD) Earth Science Keywords. Version 8.0.0.0.0 
<a href="http://gcmd.nasa.gov/learn/keyword_list.html">http://gcmd.nasa.gov/learn/keyword_list.html</a>
</p>
</div>

</div>

<div id="outline-container-1-11" class="outline-4">
<h4 id="sec-1-11"><span class="section-number-4">1.11</span> Geographic coverage</h4>
<div class="outline-text-4" id="text-1-11">

<p>    &gt; require(devtools)
    &gt; install<sub>github</sub>("disentangle", "ivanhanigan")
    &gt; require(disentangle)
    &gt; morpho<sub>bounding</sub><sub>box</sub>(d)
                      X1                 X2                 X3
    1               &lt;NA&gt; 10.1356954574585 S               &lt;NA&gt;
    2 112.907211303711 E               &lt;NA&gt; 158.960372924805 E
    3               &lt;NA&gt; 54.7538909912109 S               &lt;NA&gt;
</p>

</div>

</div>

<div id="outline-container-1-12" class="outline-4">
<h4 id="sec-1-12"><span class="section-number-4">1.12</span> Save the metadata</h4>
<div class="outline-text-4" id="text-1-12">


<ul>
<li>the metadata is now ready to save to my .morpho catalogue
</li>
<li>without importing any data
</li>
</ul>


<p>
<img src="/images/morphoimg2.png" alt="morphoimg2.png">
</p>
<ul>
<li>this appears as a new XML
</li>
</ul>


<p>
<img src="/images/morphoimg3.png" alt="morphoimg3.png">
</p>
<ul>
<li>which looks like this
</li>
</ul>


<p>
<img src="/images/morphoimg4.png" alt="morphoimg4.png">
</p>
</div>

</div>

<div id="outline-container-1-13" class="outline-4">
<h4 id="sec-1-13"><span class="section-number-4">1.13</span> Additional Metadata</h4>
<div class="outline-text-4" id="text-1-13">


<p>
As this is metadata only about the dataset, it is innapropriate to refer to related publications etc in these elements.  Luckily EML has the additionalMetadata and additionalLinks fields.  Just open the XML and paste the following in the bottom.
</p>
<p>
    &lt;additionalMetadata&gt;
      &lt;metadata&gt;
        &lt;additionalLinks&gt;
          &lt;url name="Hanigan, IC, Butler, CD, Kokic, PN, Hutchinson, MF. Suicide and Drought in New South Wales, Australia, 1970-2007. Proceedings of the National Academy of Science USA 2012, vol. 109 no. 35 13950-13955, doi: 10.1073/pnas.1112965109"&gt;<a href="http://dx.doi.org/10.1073/pnas.1112965109">http://dx.doi.org/10.1073/pnas.1112965109</a>&lt;/url&gt;
        &lt;/additionalLinks&gt;
      &lt;/metadata&gt;
    &lt;/additionalMetadata&gt;
</p>
<p>
You can see this if you then open it up again in morpho and then under the documentation menu go to Add/Edit Documentation.
</p>
<p>
<img src="/images/morphoimg5.png" alt="morphoimg5.png">
</p></div>
</div>
</div>
</div>

</body>
</html>
