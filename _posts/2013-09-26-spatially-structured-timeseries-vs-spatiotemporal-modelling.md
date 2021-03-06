---
name: spatially-structured-timeseries-vs-spatiotemporal-modelling
layout: post
title: spatially-structured-timeseries-vs-spatiotemporal-modelling
date: 2013-09-26
categories:
- spatial dependence
---
    
<head>
<title>Spatiotemporal Regression Modelling</title>
<meta http-equiv="Content-Type" content="text/html;charset=iso-8859-1"/>
<meta name="title" content="Spatiotemporal Regression Modelling"/>
<meta name="generator" content="Org-mode"/>
<meta name="generated" content="2013-09-26T10:18+1000"/>
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
<script type="text/javascript" src="http://orgmode.org/mathjax/MathJax.js">
/**
 *
 * @source: http://orgmode.org/mathjax/MathJax.js
 *
 * @licstart  The following is the entire license notice for the
 *  JavaScript code in http://orgmode.org/mathjax/MathJax.js.
 *
 * Copyright (C) 2012-2013  MathJax
 *
 * Licensed under the Apache License, Version 2.0 (the "License");
 * you may not use this file except in compliance with the License.
 * You may obtain a copy of the License at
 *
 *     http://www.apache.org/licenses/LICENSE-2.0
 *
 * Unless required by applicable law or agreed to in writing, software
 * distributed under the License is distributed on an "AS IS" BASIS,
 * WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
 * See the License for the specific language governing permissions and
 * limitations under the License.
 *
 * @licend  The above is the entire license notice
 * for the JavaScript code in http://orgmode.org/mathjax/MathJax.js.
 *
 */

/*
@licstart  The following is the entire license notice for the
JavaScript code below.

Copyright (C) 2012-2013 Free Software Foundation, Inc.

The JavaScript code below is free software: you can
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
for the JavaScript code below.
*/
<!--/*--><![CDATA[/*><!--*/
    MathJax.Hub.Config({
        // Only one of the two following lines, depending on user settings
        // First allows browser-native MathML display, second forces HTML/CSS
        //  config: ["MMLorHTML.js"], jax: ["input/TeX"],
            jax: ["input/TeX", "output/HTML-CSS"],
        extensions: ["tex2jax.js","TeX/AMSmath.js","TeX/AMSsymbols.js",
                     "TeX/noUndefined.js"],
        tex2jax: {
            inlineMath: [ ["\\(","\\)"] ],
            displayMath: [ ['$$','$$'], ["\\[","\\]"], ["\\begin{displaymath}","\\end{displaymath}"] ],
            skipTags: ["script","noscript","style","textarea","pre","code"],
            ignoreClass: "tex2jax_ignore",
            processEscapes: false,
            processEnvironments: true,
            preview: "TeX"
        },
        showProcessingMessages: true,
        displayAlign: "center",
        displayIndent: "2em",

        "HTML-CSS": {
             scale: 100,
             availableFonts: ["STIX","TeX"],
             preferredFont: "TeX",
             webFont: "TeX",
             imageFont: "TeX",
             showMathMenu: true,
        },
        MMLorHTML: {
             prefer: {
                 MSIE:    "MML",
                 Firefox: "MML",
                 Opera:   "HTML",
                 other:   "HTML"
             }
        }
    });
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
<li><a href="#sec-1">1 Spatially Structured Timeseries Vs Spatiotemporal Modelling</a>
<ul>
<li><a href="#sec-1-1">1.1 Spatially Structured Time Series</a></li>
<li><a href="#sec-1-2">1.2 Spatiotemporal modelling</a></li>
</ul>
</li>
</ul>
</div>
</div>

<div id="outline-container-1" class="outline-3">
<h3 id="sec-1"><span class="section-number-3">1</span> Spatially Structured Timeseries Vs Spatiotemporal Modelling</h3>
<div class="outline-text-3" id="text-1">

<p>In my last post about <a href="http://ivanhanigan.github.io/2013/09/reflections-bob-haining-update">spatiotemporal regression modelling</a> I mentioned that I am mostly interested in "spatially structured time-series models" rather than spatial models at a single point in time. By this I mean that we have several neighbouring areal units observed over a period of time. In this framework the general methods of time series modelling are used to control for temporal autocorrelation. However this makes the methods of spatial error and spatial lag models tricky because the spatial autocorrelation needs to be assessed at many points in time.
</p>
<p>
I want to expand more on this topic because I want to be clear that the organisation of the material I am aiming to bring to this notebook topic is not aimed at purely spatial regression models <a href="https://geodacenter.asu.edu/spatial-lag-and">(there is a lot of material and tools out there already for that)</a>.  I am trying with these notes to document my learning steps toward integrating spatial methods with time-series methods to allow me to practice (and understand) spatiotemporal regression modelling.
</p>

</div>

<div id="outline-container-1-1" class="outline-4">
<h4 id="sec-1-1"><span class="section-number-4">1.1</span> Spatially Structured Time Series</h4>
<div class="outline-text-4" id="text-1-1">

<p>In <a href="http://www.pnas.org/content/early/2012/08/08/1112965109.full.pdf+html">my most successful previous attempt to conduct a spatiotemporal analysis of Suicide and Droughts</a> I built on my knowledge of time-series regression models from single-city air pollution studies where the whole city is the unit of analysis and the temporal variation is modelled with controlling techniques for temporal autocorrelation.  These techniques are also valid for multi-city studies because it is pretty safe to assume the cities are all independent at each time point.  I structured my study by Eleven large zones (Census Statistical Divisions) of NSW and assumed each of these would vary over time independent of each other, and I fitted a zone-specific time trend and cycle. This is what I call "spatially structured time-series" modelling.  
</p>
<p>
I justify using this model in this case because aggregating up to these very large regions will diminish the possibility of spatial autocorrelation and because Droughts vary over large spatial zones too, we will not suffer from exposure misclassificaiton bias.
</p>
<p>
So this model is a simple time-series regression (with trend and seasonality) and an additional term for spatial Zone.
</p>


\begin{eqnarray*}
        log({\color{red} O_{ijk}})  & = & s({\color{red}ExposureVariable})  + {\color{blue} OtherExplanators}  \\
        & &   + AgeGroup_{i} + Sex_{j} \\
        & &   + {\color{blue} SpatialZone_{k}}  \\
        & &  + sin(Time \times 2 \times \pi) + cos(Time \times 2 \times \pi) \\
        & &  + Trend \\
        & &   + offset({\color{blue} log(Pop_{ijk})})\\
\end{eqnarray*}

<p>
Where:<br/>
</p>
<ul>
<li>\({\color{red}O_{ijk}}\) = Outcome (counts) by Age\(_{i}\), Sex\(_{j}\) and SpatialZone\(_{k}\) <br/>
</li>
<li>{\color{red}ExposureVariable} = Data with {\color{red}Restrictive Intellectual Property~(IP)} <br/>
</li>
<li>{\color{blue}OtherExplanators} = Other {\color{blue}Less Restricted}  Explanatory variables <br/>
</li>
<li>s( ) = penalized regression splines <br/>
</li>
<li>\({\color{blue} SpatialZone_{k}}\)  = {\color{blue} Less Restricted} data representing the \(SpatialZone_{k}\)  <br/>
</li>
<li>Trend = Longterm smooth trend(s) <br/>
</li>
<li>\({\color{blue}Pop_{ijk}}\) = interpolated Census populations, by time in each group<br/>
</li>
</ul>


</div>

</div>

<div id="outline-container-1-2" class="outline-4">
<h4 id="sec-1-2"><span class="section-number-4">1.2</span> <span class="todo TODO">TODO</span> Spatiotemporal modelling</h4>
<div class="outline-text-4" id="text-1-2">

<p>In contrast to the above model for modelling exposures that have fine resolution spatial variation (such as air pollution) the exposure misclassification effect of aggregating up to very large spatial zones will conteract the benefits of avoiding spatially autocorrelated errors and this might be unacceptable for certain research questions.  Therefore it is important to move toward a spatiotemporal regression model that replaces the \(SpatialZone_{k}\) term with a more spatial error or spatial lag approach.
</p></div>
</div>
</div>
</div>

</body>
</html>
