---
name: 2013-12-20-animation-illustrating-catastrophic-regime-shifts
layout: post
title: Animation Illustrating Catastrophic Regime Shifts
date: 2013-12-20
categories:
- ecosocial tipping points
---

<head>
<title>Trends and Triggers Figure </title>
<meta http-equiv="Content-Type" content="text/html;charset=utf-8"/>
<meta name="title" content="Trends and Triggers Figure "/>
<meta name="generator" content="Org-mode"/>
<meta name="generated" content="2013-12-20T00:18+1100"/>
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
<h1 class="title">Trends and Triggers Figure </h1>


<hr/>


<div id="table-of-contents">
<h2>Table of Contents</h2>
<div id="text-table-of-contents">
<ul>
<li><a href="#sec-1">1 Introduction</a></li>
<li><a href="#sec-2">2 The History</a></li>
<li><a href="#sec-3">3 3D surface</a>
<ul>
<li><a href="#sec-3-1">3.1 figure</a></li>
<li><a href="#sec-3-2">3.2 code</a></li>
</ul>
</li>
<li><a href="#sec-4">4 Try an animation</a>
<ul>
<li><a href="#sec-4-1">4.1 figure</a></li>
<li><a href="#sec-4-2">4.2 code</a></li>
</ul>
</li>
<li><a href="#sec-5">5 Next Steps</a></li>
</ul>
</div>
</div>

<div id="outline-container-1" class="outline-2">
<h2 id="sec-1"><span class="section-number-2">1</span> Introduction</h2>
<div class="outline-text-2" id="text-1">

<p>This work toward a enhanced figure that might be used to tell a detailed story about the mixture of trend, triggers and wiggles.
</p></div>

</div>

<div id="outline-container-2" class="outline-2">
<h2 id="sec-2"><span class="section-number-2">2</span> The History</h2>
<div class="outline-text-2" id="text-2">

<p>The original image I base my imagination on is:
</p>
<ul>
<li>Scheffer, M., &amp; Carpenter, S. R. (2003). Catastrophic regime shifts in ecosystems: linking theory to observation [Review]. TRENDS in Ecology and Evolution, 18(12), 648–656. Retrieved from <a href="http://eaton.math.rpi.edu/csums/papers/Ecostability/scheffercatastrophe.pdf">http://eaton.math.rpi.edu/csums/papers/Ecostability/scheffercatastrophe.pdf</a>
</li>
</ul>


<p>
Which was based on 
</p>
<ul>
<li>Scheffer, M., Carpenter, S., Foley, J. a, Folke, C., &amp; Walker, B. (2001). Catastrophic shifts in ecosystems. Nature, 413(6856), 591–6. <i>&lt;doi:10.1038/35098000&gt;</i>
</li>
</ul>


<p>
<img src="/images/catastrophe.png"  alt="/images/catastrophe.png" />
</p>


</div>

</div>

<div id="outline-container-3" class="outline-2">
<h2 id="sec-3"><span class="section-number-2">3</span> 3D surface</h2>
<div class="outline-text-2" id="text-3">

<p>First I want to generate a 3d computer image to play with perspective and shading.
</p>
</div>

<div id="outline-container-3-1" class="outline-3">
<h3 id="sec-3-1"><span class="section-number-3">3.1</span> figure</h3>
<div class="outline-text-3" id="text-3-1">


<p>
<img src="/images/TrendsAndTriggers-v2.png"  alt="/images/TrendsAndTriggers-v2.png" />
</p></div>

</div>

<div id="outline-container-3-2" class="outline-3">
<h3 id="sec-3-2"><span class="section-number-3">3.2</span> code</h3>
<div class="outline-text-3" id="text-3-2">




<pre class="src src-R"><span style="color: #586e75;">#### </span><span style="color: #586e75;">name:generate-surface ####</span>
x <span style="color: #268bd2; font-weight: bold;">&lt;-</span> seq(from=-2.5, to=2.5, by=0.1)
zid <span style="color: #268bd2; font-weight: bold;">&lt;-</span> .1
<span style="color: #859900; font-weight: bold;">for</span>(y <span style="color: #859900; font-weight: bold;">in</span> 1:10)
{    
  z <span style="color: #268bd2; font-weight: bold;">&lt;-</span> x^4 - zid * x^3 - 7 * x^2 + x + 6
  <span style="color: #859900; font-weight: bold;">if</span>(y == 1)
  {
    data_out <span style="color: #268bd2; font-weight: bold;">&lt;-</span> cbind(x,y,z)  
  } <span style="color: #859900; font-weight: bold;">else</span> {
    data_out <span style="color: #268bd2; font-weight: bold;">&lt;-</span> rbind(data_out, cbind(x,y,z))
  }
  zid <span style="color: #268bd2; font-weight: bold;">&lt;-</span> zid + 0.1
}

data_out <span style="color: #268bd2; font-weight: bold;">&lt;-</span> as.data.frame(data_out)
write.csv(data_out, <span style="color: #2aa198;">"TrendsAndTriggers-v2.csv"</span>, row.names = F)

png(<span style="color: #2aa198;">"/images/TrendsAndTriggers-v2.png"</span>)
persp(x, 1:10, matrix(data_out$z, ncol = 10, nrow = length(x)), ylab= <span style="color: #2aa198;">""</span>,  xlab= <span style="color: #2aa198;">""</span>, zlab = <span style="color: #2aa198;">""</span>,  
      theta = 140, 
      phi = 42, 
      expand = 0.5, col = <span style="color: #2aa198;">"lightgrey"</span>)
dev.off()
</pre>



</div>
</div>

</div>

<div id="outline-container-4" class="outline-2">
<h2 id="sec-4"><span class="section-number-2">4</span> Try an animation</h2>
<div class="outline-text-2" id="text-4">

<p>I'd like to move the ball through the surface.  First need to calculate the path.
</p>
</div>

<div id="outline-container-4-1" class="outline-3">
<h3 id="sec-4-1"><span class="section-number-3">4.1</span> figure</h3>
<div class="outline-text-3" id="text-4-1">

<p><img src="/images/animation.gif"  alt="/images/animation.gif" />
</p></div>

</div>

<div id="outline-container-4-2" class="outline-3">
<h3 id="sec-4-2"><span class="section-number-3">4.2</span> code</h3>
<div class="outline-text-3" id="text-4-2">




<pre class="src src-R"><span style="color: #586e75;"># </span><span style="color: #586e75;">functions</span>
<span style="color: #859900; font-weight: bold;">if</span>(!<span style="color: #268bd2; font-weight: bold;">require</span>(animation)) install.packages(<span style="color: #2aa198;">"animation"</span>);
<span style="color: #268bd2; font-weight: bold;">require</span>(animation)

<span style="color: #586e75;"># </span><span style="color: #586e75;">load</span>
data_out <span style="color: #268bd2; font-weight: bold;">&lt;-</span> read.csv(<span style="color: #2aa198;">"TrendsAndTriggers-v2.csv"</span>)

<span style="color: #586e75;">## </span><span style="color: #586e75;">do</span>
setwd(<span style="color: #2aa198;">"images"</span>)
saveGIF(
{
  ani.options(interval = 0.2)
  xindex  <span style="color: #268bd2; font-weight: bold;">&lt;-</span> c(0, -1, rep(-1.9, 6), -1, 0, 1, rep(2, 6), 1, 0 , 0)
  j  <span style="color: #268bd2; font-weight: bold;">&lt;-</span> 1
  xind  <span style="color: #268bd2; font-weight: bold;">&lt;-</span> xindex[j]
  <span style="color: #859900; font-weight: bold;">for</span>(index <span style="color: #859900; font-weight: bold;">in</span> c(1:10, 9:1)){
  with(subset(data_out, y == index),
       plot(x, z, type = <span style="color: #2aa198;">"l"</span>, ylim = c(-15,15))
       )
  with(subset(data_out, y == index &amp; x == xind),
       points(x,z,pch=16,cex = 3)
       )
  j <span style="color: #268bd2; font-weight: bold;">&lt;-</span> j + 1
  xind <span style="color: #268bd2; font-weight: bold;">&lt;-</span> xindex[j]
  }
},
outdir = getwd()
)
setwd(<span style="color: #2aa198;">".."</span>)
</pre>


</div>
</div>

</div>

<div id="outline-container-5" class="outline-2">
<h2 id="sec-5"><span class="section-number-2">5</span> Next Steps</h2>
<div class="outline-text-2" id="text-5">

<ul>
<li>the polynomials should move up and down to give the height of originals
</li>
<li>the hump in the middle needs to change, so the ball flips more easily
</li>
<li>I'd like the ball to wiggle, add a random walk 
</li>
<li>the time series dimension needs to be shown
</li>
<li>It'd be great to combine this with 2D line plots as well
</li>
</ul>





</div>
</div>
</div>

</body>
