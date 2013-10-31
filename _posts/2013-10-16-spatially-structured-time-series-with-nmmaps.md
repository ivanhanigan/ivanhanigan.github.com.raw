---
name: spatially-structured-time-series-with-nmmaps
layout: post
title: spatially-structured-time-series-with-nmmaps
date: 2013-10-16
categories:
- spatial dependence
---

I will use the NMMAPSlite datasets for a simple example of what I
describe as "Spatially Structured Timeseries" as opposed to
"Spatio-Temporal" which I think more explicitly includes spatial
structure in the model.  [See This Report](http://ivanhanigan.github.io/spatiotemporal-regression-models/) for all the gory details.

# R Codes

<!-- <?xml version="1.0" encoding="utf-8"?> -->
<!-- <!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Strict//EN" -->
<!--                "http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd"> -->
<!-- <html xmlns="http://www.w3.org/1999/xhtml" lang="en" xml:lang="en"> -->
<head>
<title>Spatiotemporal Regression Modelling</title>
<meta http-equiv="Content-Type" content="text/html;charset=utf-8"/>
<meta name="title" content="Spatiotemporal Regression Modelling"/>
<meta name="generator" content="Org-mode"/>
<meta name="generated" content="2013-10-16T15:17+1100"/>
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
<h1 class="title">Spatiotemporal Regression Modelling</h1>


<div id="table-of-contents">
<h2>Table of Contents</h2>
<div id="text-table-of-contents">
<ul>
<li><a href="#sec-1">1 Core Model</a></li>
<li><a href="#sec-2">2 Core Model Plots</a></li>
</ul>
</div>
</div>

<div id="outline-container-1" class="outline-4">
<h4 id="sec-1"><span class="section-number-4">1</span> Core Model</h4>
<div class="outline-text-4" id="text-1">




<pre class="src src-R"><span style="color: #5F7F5F;">################################################################</span>
<span style="color: #5F7F5F;"># </span><span style="color: #7F9F7F;">name:core</span>
<span style="color: #5F7F5F;"># </span><span style="color: #7F9F7F;">func</span>
setwd(<span style="color: #CC9393;">"~/projects/spatiotemporal-regression-models/NMMAPS-example"</span>)
<span style="color: #BFEBBF; font-weight: bold;">require</span>(mgcv)
<span style="color: #BFEBBF; font-weight: bold;">require</span>(splines)

<span style="color: #5F7F5F;"># </span><span style="color: #7F9F7F;">load</span>
analyte <span style="color: #BFEBBF; font-weight: bold;">&lt;-</span> read.csv(<span style="color: #CC9393;">"analyte.csv"</span>)

<span style="color: #5F7F5F;"># </span><span style="color: #7F9F7F;">clean</span>
analyte$yy <span style="color: #BFEBBF; font-weight: bold;">&lt;-</span> substr(analyte$date,1,4)
numYears<span style="color: #BFEBBF; font-weight: bold;">&lt;-</span>length(names(table(analyte$yy)))
analyte$date <span style="color: #BFEBBF; font-weight: bold;">&lt;-</span> as.Date(analyte$date)
analyte$time <span style="color: #BFEBBF; font-weight: bold;">&lt;-</span> as.numeric(analyte$date)
analyte$agecat <span style="color: #BFEBBF; font-weight: bold;">&lt;-</span> factor(analyte$agecat,
                          levels = c(<span style="color: #CC9393;">"under65"</span>,
                              <span style="color: #CC9393;">"65to74"</span>, <span style="color: #CC9393;">"75p"</span>),
                          ordered = <span style="color: #7CB8BB;">TRUE</span>
                          )

<span style="color: #5F7F5F;"># </span><span style="color: #7F9F7F;">do</span>
fit <span style="color: #BFEBBF; font-weight: bold;">&lt;-</span> gam(cvd ~ s(tmax) + s(dptp) +
           city + agecat +
           s(time, k= 7*numYears, fx=T) +
           offset(log(pop)),
           data = analyte, family = poisson
           )

<span style="color: #5F7F5F;"># </span><span style="color: #7F9F7F;">plot of response functions</span>
png(<span style="color: #CC9393;">"images/nmmaps-eg-core.png"</span>, width = 1000, height = 750, res = 150)
par(mfrow=c(2,3))
plot(fit, all.terms = <span style="color: #7CB8BB;">TRUE</span>)
dev.off()


</pre>

</div>

</div>

<div id="outline-container-2" class="outline-4">
<h4 id="sec-2"><span class="section-number-4">2</span> Core Model Plots</h4>
<div class="outline-text-4" id="text-2">

<p><img src="/images/nmmaps-eg-core.png"  alt="/images/nmmaps-eg-core.png" />
</p></div>
</div>
</div>

</body>
</html>