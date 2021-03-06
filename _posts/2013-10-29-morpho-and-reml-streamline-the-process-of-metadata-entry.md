---
name: morpho-and-reml-boilerplate-streamline-the-process-of-metadata-entry
layout: post
title: morpho-and-reml-boilerplate-streamline-the-process-of-metadata-entry
date: 2013-10-29
categories:
- Data Documentation
tags:
- morpho
---


<body>

<div id="preamble">

</div>

<div id="content">
<h1 class="title">Disentangle Things</h1>


<div id="table-of-contents">
<h2>Table of Contents</h2>
<div id="text-table-of-contents">
<ul>
<li><a href="#sec-1">1 morpho-and-reml-boilerplate-streamline-the-process-of-metadata-entry</a>
<ul>
<li><a href="#sec-1-1">1.1 Background</a></li>
<li><a href="#sec-1-2">1.2 Speed and Rigour</a></li>
<li><a href="#sec-1-3">1.3 Analysts can often trade-off completeness of documentation for speed</a></li>
<li><a href="#sec-1-4">1.4 Librarians produce gold plated documentation and can take longer to produce this</a></li>
<li><a href="#sec-1-5">1.5 An example</a></li>
<li><a href="#sec-1-6">1.6 Embracing Inaccuracy and Incompleteness</a></li>
<li><a href="#sec-1-7">1.7 Aim</a></li>
<li><a href="#sec-1-8">1.8 Step 1: load a simple example dataset</a></li>
<li><a href="#sec-1-9">1.9 Step 2 create a function to deliver the minimal metadata object</a></li>
<li><a href="#sec-1-10">1.10 reml<sub>boilerplate</sub>-code</a></li>
<li><a href="#sec-1-11">1.11 reml<sub>boilerplate</sub>-test-code</a></li>
<li><a href="#sec-1-12">1.12 Results: This loads into Morpho with some errors</a></li>
<li><a href="#sec-1-13">1.13 Conclusions</a></li>
</ul>
</li>
</ul>
</div>
</div>

<div id="outline-container-1" class="outline-3">
<h3 id="sec-1"><span class="section-number-3">1</span> morpho-and-reml-boilerplate-streamline-the-process-of-metadata-entry</h3>
<div class="outline-text-3" id="text-1">


</div>

<div id="outline-container-1-1" class="outline-4">
<h4 id="sec-1-1"><span class="section-number-4">1.1</span> Background</h4>
<div class="outline-text-4" id="text-1-1">


<ul>
<li>The Morpho/Metacat system is great for a data repository
</li>
<li>Morpho also claims to be suitable for Ecologists to document their data
</li>
<li>But in my experience it leaves a little to be desired in ease of use for both purposes
</li>
<li>Specifically the speed that documentation can be entered into Morpho is slow
</li>
<li>This post is a first attempt to create some boilerplate code to quickly generate EML metadata using REML.
</li>
</ul>


</div>

</div>

<div id="outline-container-1-2" class="outline-4">
<h4 id="sec-1-2"><span class="section-number-4">1.2</span> Speed and Rigour</h4>
<div class="outline-text-4" id="text-1-2">

<p>As I noted in a previous post, there are [two types of data documentation workflow](<a href="http://ivanhanigan.github.io/2013/10/two-main-types-of-data-documentation-workflow/">http://ivanhanigan.github.io/2013/10/two-main-types-of-data-documentation-workflow/</a>).  
</p>
<ul>
<li>GUI
</li>
<li>Programatic
</li>
</ul>


<p>  
I also think there are two types of users with different motivations and constraints:
</p>
<ul>
<li>1) Data Analysts
</li>
<li>2) Data Librarians
</li>
</ul>


</div>

</div>

<div id="outline-container-1-3" class="outline-4">
<h4 id="sec-1-3"><span class="section-number-4">1.3</span> Analysts can often trade-off completeness of documentation for speed</h4>
<div class="outline-text-4" id="text-1-3">

<p>In my view the Analysts group of users need a tool that will very rapidly document their data and workflow steps and can live with a bit less rigour in the quality of documentation.  Obviously this is not ideal but seems an inevitable trade-off needed to enable analysts to keep up the momentum of the data processing and modelling without getting distracted by tedious (and potentially unnecessary) data documentation tasks.
</p>
</div>

</div>

<div id="outline-container-1-4" class="outline-4">
<h4 id="sec-1-4"><span class="section-number-4">1.4</span> Librarians produce gold plated documentation and can take longer to produce this</h4>
<div class="outline-text-4" id="text-1-4">

<p>On the other hand the role of the Librarian group is to produce documentation to the best level possible (given time and resource constraints) the datasets and methodologies that lead to the creation of the datasets.  For that group Rigour will take precedence and there will be a trade-off in terms of the amount of time needed to produce the documentation.
</p>
</div>

</div>

<div id="outline-container-1-5" class="outline-4">
<h4 id="sec-1-5"><span class="section-number-4">1.5</span> An example</h4>
<div class="outline-text-4" id="text-1-5">

<p>As an example of the two different groups, an analyst working with weather data in Australia may want to specify that their variable "temperature" is the average of the daily maxima and minima, but might not need to specify that the observations were taken inside a Stevenson Screen, or even if they are in Celsius, Farenhiet or Kelvin.  They will be very keen to start the analysis to identify any associations between weather variables and the response variable they are investigating.   The data librarian on the other hand will be more likely to need to include this information so that the users of the temperature data do not mis-interpret it.
</p>
</div>

</div>

<div id="outline-container-1-6" class="outline-4">
<h4 id="sec-1-6"><span class="section-number-4">1.6</span> Embracing Inaccuracy and Incompleteness</h4>
<div class="outline-text-4" id="text-1-6">


<ul>
<li>I've been talking about this for a while got referred to this document by Ben Davies at the ANUSF
</li>
</ul>

<p>[http://thedailywtf.com/Articles/Documentation-Done-Right.aspx](<a href="http://thedailywtf.com/Articles/Documentation-Done-Right.aspx">http://thedailywtf.com/Articles/Documentation-Done-Right.aspx</a>)
</p><ul>
<li>It has this bit:
</li>
</ul>




<pre class="src src-R">  
   
Embracing Inaccuracy and Incompleteness 
    
The immediate answer to what&#8217;s the right way to do documentation is
clear: produce the least amount of documentation needed to facilitate
the most understanding, and be very explicit about which documentation
is to be maintained and which is to be archived (i.e., read-only and
left to rot).
</pre>


<ul>
<li>Roughly speaking, a full EML document produced by Morpho is a bit like a whole bunch of cruft that isnt needed and gets in the way (and is more confusing)
</li>
<li>Whereas a minimal version Im thinking of covers almost all the generic entries providing the "minimum amount of stuff to make it work right".
</li>
</ul>


</div>

</div>

<div id="outline-container-1-7" class="outline-4">
<h4 id="sec-1-7"><span class="section-number-4">1.7</span> Aim</h4>
<div class="outline-text-4" id="text-1-7">


<ul>
<li>This experiment aims to speed up the creation of a minimal "skeleton" of metadata to a level that both the groups above can be comfortable with AS A FIRST STEP.
</li>
<li>It is assumed that additional steps will then need to be taken to complete the documentation, but the automation of the first part of the process should shave off enough time to suit the purposes of both groups
</li>
<li>It is an imperative that the quick-start creation of the metadata does not end up costing the documentor more time later on down the track if they need to go back to many of the elements for additional editing.
</li>
</ul>





</div>

</div>

<div id="outline-container-1-8" class="outline-4">
<h4 id="sec-1-8"><span class="section-number-4">1.8</span> Step 1: load a simple example dataset</h4>
<div class="outline-text-4" id="text-1-8">

<p>I've been using a [fictitious dataset from a Statistics Methodology paper by Ritschard 2006](<a href="http://ivanhanigan.github.io/2013/10/test-data-for-classification-trees/">http://ivanhanigan.github.io/2013/10/test-data-for-classification-trees/</a>).  It will do as a first cut but when it comes to actually test this out it would be good to have something that would take a bit longer (so that the frustrations of using Morpho become very apparent).
</p>



<pre class="src src-R">  <span style="color: #586e75;">#### </span><span style="color: #586e75;">R Code:</span>
      <span style="color: #586e75;"># </span><span style="color: #586e75;">func</span>
      <span style="color: #268bd2; font-weight: bold;">require</span>(devtools)
      install_github(<span style="color: #2aa198;">"disentangle"</span>, <span style="color: #2aa198;">"ivanhanigan"</span>)
      <span style="color: #268bd2; font-weight: bold;">require</span>(disentangle)
      <span style="color: #586e75;"># </span><span style="color: #586e75;">load</span>
      fpath <span style="color: #268bd2; font-weight: bold;">&lt;-</span> system.file(
          file.path(<span style="color: #2aa198;">"extdata"</span>, <span style="color: #2aa198;">"civst_gend_sector_full.csv"</span>),
          package = <span style="color: #2aa198;">"disentangle"</span>
          )
      data_set <span style="color: #268bd2; font-weight: bold;">&lt;-</span> read.csv(fpath)
      summary(data_set)
      <span style="color: #586e75;"># </span><span style="color: #586e75;">store it in the current project workspace</span>
      write.csv(data_set, <span style="color: #2aa198;">"data/civst_gend_sector_full.csv"</span>, row.names = F)
      



<span style="color: #586e75;">## </span><span style="color: #586e75;">| divorced/widowed: 33 | female:132 | primary  :116 | Min.   : 128.9 |</span>
<span style="color: #586e75;">## </span><span style="color: #586e75;">| married         :120 | male  :141 | secondary: 99 | 1st Qu.: 768.3 |</span>
<span style="color: #586e75;">## </span><span style="color: #586e75;">| single          :120 | nil        | tertiary : 58 | Median : 922.8 |</span>
<span style="color: #586e75;">## </span><span style="color: #586e75;">| nil                  | nil        | nil           | Mean   : 908.4 |</span>
<span style="color: #586e75;">## </span><span style="color: #586e75;">| nil                  | nil        | nil           | 3rd Qu.:1079.1 |</span>
<span style="color: #586e75;">## </span><span style="color: #586e75;">| nil                  | nil        | nil           | Max.   :1479.4 |</span>

</pre>




</div>

</div>

<div id="outline-container-1-9" class="outline-4">
<h4 id="sec-1-9"><span class="section-number-4">1.9</span> Step 2 create a function to deliver the minimal metadata object</h4>
<div class="outline-text-4" id="text-1-9">

<ul>
<li>the package REML will create a EML metadata document quite easily
</li>
<li>I will assume that a lot of the data elements are self explanatory and take column names and factor levels as the descriptions
</li>
</ul>


</div>

</div>

<div id="outline-container-1-10" class="outline-4">
<h4 id="sec-1-10"><span class="section-number-4">1.10</span> reml<sub>boilerplate</sub>-code</h4>
<div class="outline-text-4" id="text-1-10">




<pre class="src src-R"><span style="color: #586e75;">################################################################</span>
<span style="color: #586e75;"># </span><span style="color: #586e75;">name:reml_boilerplate</span>
 
<span style="color: #586e75;"># </span><span style="color: #586e75;">func</span>
<span style="color: #859900; font-weight: bold;">if</span>(!<span style="color: #268bd2; font-weight: bold;">require</span>(reml)) {
  <span style="color: #268bd2; font-weight: bold;">require</span>(devtools)
  install_github(<span style="color: #2aa198;">"reml"</span>, <span style="color: #2aa198;">"ropensci"</span>)
  } 
<span style="color: #268bd2; font-weight: bold;">require</span>(reml)

<span style="color: #268bd2;">reml_boilerplate</span> <span style="color: #268bd2; font-weight: bold;">&lt;-</span> <span style="color: #859900; font-weight: bold;">function</span>(data_set, created_by = <span style="color: #2aa198;">"Ivan Hanigan &lt;<a href="mailto:ivanhanigan&#64;gmail.com">ivanhanigan&#64;gmail.com</a>&gt;"</span>, data_dir = getwd(), titl = <span style="color: #b58900;">NA</span>, desc = <span style="color: #2aa198;">""</span>)
{

  <span style="color: #586e75;"># </span><span style="color: #586e75;">essential</span>
  <span style="color: #859900; font-weight: bold;">if</span>(is.na(titl)) <span style="color: #859900; font-weight: bold;">stop</span>(print(<span style="color: #2aa198;">"must specify title"</span>))
  <span style="color: #586e75;"># </span><span style="color: #586e75;">we can get the col names easily</span>
  col_defs <span style="color: #268bd2; font-weight: bold;">&lt;-</span> names(data_set)
  <span style="color: #586e75;"># </span><span style="color: #586e75;">next create a list from the data</span>
  unit_defs <span style="color: #268bd2; font-weight: bold;">&lt;-</span> list()
  <span style="color: #859900; font-weight: bold;">for</span>(i <span style="color: #859900; font-weight: bold;">in</span> 1:ncol(data_set))
    {
      <span style="color: #586e75;"># </span><span style="color: #586e75;">i = 4</span>
      <span style="color: #859900; font-weight: bold;">if</span>(is.numeric(data_set[,i])){
        unit_defs[[i]] <span style="color: #268bd2; font-weight: bold;">&lt;-</span> <span style="color: #2aa198;">"numeric"</span>
      } <span style="color: #859900; font-weight: bold;">else</span> {
        unit_defs[[i]] <span style="color: #268bd2; font-weight: bold;">&lt;-</span> names(table(data_set[,i]))          
      }
    }
  <span style="color: #586e75;"># </span><span style="color: #586e75;">unit_defs</span>
  
  ds <span style="color: #268bd2; font-weight: bold;">&lt;-</span> data.set(data_set,
                 col.defs = col_defs,
                 unit.defs = unit_defs
                 )
  <span style="color: #586e75;">#</span><span style="color: #586e75;">str(ds)</span>

  metadata  <span style="color: #268bd2; font-weight: bold;">&lt;-</span> metadata(ds)
  <span style="color: #586e75;"># </span><span style="color: #586e75;">needs names</span>
  <span style="color: #859900; font-weight: bold;">for</span>(i <span style="color: #859900; font-weight: bold;">in</span> 1:ncol(data_set))
    {
      <span style="color: #586e75;"># </span><span style="color: #586e75;">i = 4</span>
      <span style="color: #859900; font-weight: bold;">if</span>(is.numeric(data_set[,i])){
        names(metadata[[i]][[3]]) <span style="color: #268bd2; font-weight: bold;">&lt;-</span> <span style="color: #2aa198;">"number"</span>
      } <span style="color: #859900; font-weight: bold;">else</span> {
        names(metadata[[i]][[3]]) <span style="color: #268bd2; font-weight: bold;">&lt;-</span> metadata[[i]][[3]]
      }
    }
  <span style="color: #586e75;"># </span><span style="color: #586e75;">metadata</span>
  oldwd <span style="color: #268bd2; font-weight: bold;">&lt;-</span> getwd()
  setwd(data_dir)
  eml_write(data_set, metadata,
            title = titl,  
            description = desc,
            creator = created_by
            )
  setwd(oldwd)
  sprintf(<span style="color: #2aa198;">"your metadata has been created in the '%s' directory"</span>, data_dir)
  }
</pre>

</div>

</div>

<div id="outline-container-1-11" class="outline-4">
<h4 id="sec-1-11"><span class="section-number-4">1.11</span> reml<sub>boilerplate</sub>-test-code</h4>
<div class="outline-text-4" id="text-1-11">




<pre class="src src-R"><span style="color: #586e75;">################################################################</span>
<span style="color: #586e75;"># </span><span style="color: #586e75;">name:reml_boilerplate-test</span>

analyte <span style="color: #268bd2; font-weight: bold;">&lt;-</span> read.csv(<span style="color: #2aa198;">"data/civst_gend_sector_full.csv"</span>)
reml_boilerplate(
  data_set = analyte,
  created_by = <span style="color: #2aa198;">"Ivan Hanigan &lt;<a href="mailto:ivanhanigan&#64;gmail.com">ivanhanigan&#64;gmail.com</a>&gt;"</span>,
  data_dir = <span style="color: #2aa198;">"data"</span>,
  titl = <span style="color: #2aa198;">"civst_gend_sector_full"</span>,
  desc = <span style="color: #2aa198;">"An example, fictional dataset"</span>
  )

dir(<span style="color: #2aa198;">"data"</span>)
</pre>

</div>

</div>

<div id="outline-container-1-12" class="outline-4">
<h4 id="sec-1-12"><span class="section-number-4">1.12</span> Results: This loads into Morpho with some errors</h4>
<div class="outline-text-4" id="text-1-12">

<ul>
<li>Notably unable to import the data file
</li>
</ul>


<p>
<img src="/images/morpho-reml-boilerplate.png" alt = "morpho-reml-boilerplate.png">
</p>
<ul>
<li>Also "the saved document is not valid for some reason"
</li>
</ul>


<p>
<img src="/images/morpho-reml-boilerplate2.png" alt = "morpho-reml-boilerplate2.png">
</p></div>

</div>

<div id="outline-container-1-13" class="outline-4">
<h4 id="sec-1-13"><span class="section-number-4">1.13</span> Conclusions</h4>
<div class="outline-text-4" id="text-1-13">

<ul>
<li>This needs testing
</li>
<li>A real deal breaker is if the EML is not valid 
</li>
<li>In some cases not having the data table included will be a deal breaker (ie KNB repositories designed for downloading complete data packs
</li>
<li>A definite failure would be that even if it is quicker to get started if it takes a long time and is difficult to fix up it might increase the risk of misunderstandings.
</li>
</ul>


</div>
</div>
</div>
</div>

</body>
</html>
