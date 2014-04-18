---
name: 2013-12-21-add-2d-plots-of-trend-and-wiggle-to-catastrophic-regime-shifts-plot
layout: post
title: add-2d-plots-of-trend-and-wiggle-to-catastrophic-regime-shifts-plot
date: 2013-12-21
categories:
- ecosocial tipping points
---

<head>
<title>Catastrophic Regime Shifts Visualisation  </title>
<meta http-equiv="Content-Type" content="text/html;charset=utf-8"/>
<meta name="title" content="Catastrophic Regime Shifts Visualisation  "/>
<meta name="generator" content="Org-mode"/>
<meta name="generated" content="2013-12-21T11:39+1100"/>
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
<h1 class="title">Catastrophic Regime Shifts Visualisation  </h1>


<hr/>

<div id="table-of-contents">
<h2>Table of Contents</h2>
<div id="text-table-of-contents">
<ul>
<li><a href="#sec-1">1 Try adding 2D plot of the trend overtime and the variation within basins of attraction</a>
<ul>
<li><a href="#sec-1-1">1.1 figure</a></li>
<li><a href="#sec-1-2">1.2 code</a></li>
</ul>
</li>
</ul>
</div>
</div>

<div id="outline-container-1" class="outline-2">
<h2 id="sec-1"><span class="section-number-2">1</span> Try adding 2D plot of the trend overtime and the variation within basins of attraction</h2>
<div class="outline-text-2" id="text-1">

<ul>
<li>Following on from the previous work I now want to calculate the 2D paths.
</li>
<li>This will then form the basis for a "walk through" animation 
</li>
<li>Either with recorded narration or annotations that appear at the right time to describe each transition
</li>
<li>This is most of what I want to include except I have not added the wiggly variations around the main trend line, that show the system varying within the basin of attraction
</li>
<li>I got advice that Blender3d was the best way to finish this off.  Any other suggestions?
</li>
</ul>


</div>

<div id="outline-container-1-1" class="outline-3">
<h3 id="sec-1-1"><span class="section-number-3">1.1</span> figure</h3>
<div class="outline-text-3" id="text-1-1">

<p><img src="/images/TrendsAndTriggers-v2.1.gif"  alt="/images/TrendsAndTriggers-v2.1.gif" />
</p>

</div>

</div>

<div id="outline-container-1-2" class="outline-3">
<h3 id="sec-1-2"><span class="section-number-3">1.2</span> code</h3>
<div class="outline-text-3" id="text-1-2">




<pre class="src src-R"><span style="color: #586e75;"># </span><span style="color: #586e75;">functions</span>
x <span style="color: #268bd2; font-weight: bold;">&lt;-</span> seq(from=-2.5, to=2.5, by=0.1)

<span style="color: #586e75;"># </span><span style="color: #586e75;">load</span>
data_out <span style="color: #268bd2; font-weight: bold;">&lt;-</span> read.csv(<span style="color: #2aa198;">"TrendsAndTriggers-v2.csv"</span>)

<span style="color: #586e75;">## </span><span style="color: #586e75;">do</span>
x2d  <span style="color: #268bd2; font-weight: bold;">&lt;-</span> matrix(<span style="color: #b58900;">NA</span>, ncol = 3, nrow = 0)
xindex  <span style="color: #268bd2; font-weight: bold;">&lt;-</span> c(rep(-1.9, 5), 
             -1.7, -1.5 , -1.3, -1.1, 0, 1.1, 1.3, 1.5, 1.7
             , rep(2, 4))
j  <span style="color: #268bd2; font-weight: bold;">&lt;-</span> 1
xind  <span style="color: #268bd2; font-weight: bold;">&lt;-</span> xindex[j]
<span style="color: #859900; font-weight: bold;">for</span>(index <span style="color: #859900; font-weight: bold;">in</span> c(1:5,rep(5,8), 6:10)){
x2d <span style="color: #268bd2; font-weight: bold;">&lt;-</span> rbind(x2d, subset(data_out, y == index &amp; x == xind))
j <span style="color: #268bd2; font-weight: bold;">&lt;-</span> j + 1
xind <span style="color: #268bd2; font-weight: bold;">&lt;-</span> xindex[j]
}
<span style="color: #586e75;">#  </span><span style="color: #586e75;">x2d</span>

<span style="color: #586e75;">#</span><span style="color: #586e75;">png("/images/TrendsAndTriggers-v2.1.gif")</span>
setwd(<span style="color: #2aa198;">"images"</span>)
saveGIF(
{
ani.options(interval = 0.2)  
<span style="color: #859900; font-weight: bold;">for</span>(ith <span style="color: #859900; font-weight: bold;">in</span> 100:140){
layout(matrix(c(1,2,1,3,1,4), 3, 2, byrow = <span style="color: #b58900;">TRUE</span>), widths=c(2,1), heights=c(2,2,2))
<span style="color: #586e75;"># </span><span style="color: #586e75;">layout.show(4)</span>
res <span style="color: #268bd2; font-weight: bold;">&lt;-</span>  persp(x, 1:10, matrix(data_out$z, ncol = 10, nrow = length(x)),
               ylab= <span style="color: #2aa198;">"y"</span>,  xlab= <span style="color: #2aa198;">"x"</span>, zlab = <span style="color: #2aa198;">"z"</span>,  
               theta = ith, 
               phi = 42, ltheta = 120, shade = 0.75,
               expand = 0.5, col = <span style="color: #2aa198;">"lightgrey"</span>)
lines (trans3d(x2d$x, x2d$y, x2d$z, pmat = res), col = <span style="color: #2aa198;">"red"</span>, lwd = 4)
plot(x2d$x, x2d$y, type = <span style="color: #2aa198;">"l"</span>, xlab=<span style="color: #2aa198;">"x"</span>, ylab=<span style="color: #2aa198;">"y"</span>)
plot(x2d$x, x2d$z, type = <span style="color: #2aa198;">"l"</span>, xlab=<span style="color: #2aa198;">"x"</span>, ylab=<span style="color: #2aa198;">"z"</span>)
plot(x2d$y, x2d$z, type = <span style="color: #2aa198;">"l"</span>, xlab=<span style="color: #2aa198;">"y"</span>, ylab=<span style="color: #2aa198;">"z"</span>)
}
}

outdir = getwd(), movie.name = <span style="color: #2aa198;">"TrendsAndTriggers-v2.1.gif"</span>
)
setwd(<span style="color: #2aa198;">".."</span>)

<span style="color: #586e75;">#  </span><span style="color: #586e75;">dev.off()</span>
</pre>


</div>
</div>
</div>
</div>

</body>
