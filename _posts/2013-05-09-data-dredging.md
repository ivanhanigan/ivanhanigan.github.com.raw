--- 
name: data-dredging
layout: post
title: Complex Model Selection (or Data Dredging)
date: 2013-05-09
categories: 
- spatial dependence
---
<html xmlns="http://www.w3.org/1999/xhtml" lang="en" xml:lang="en">
<head>
<!--<title>data dredging</title>-->
<meta http-equiv="Content-Type" content="text/html;charset=utf-8"/>
<meta name="title" content="data dredging"/>
<meta name="generator" content="Org-mode"/>
<meta name="generated" content="2013-05-09 "/>
<meta name="author" content="ivan hanigan"/>
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
<h1 class="title">Toward Automated Model Selection</h1>

<!--
<div id="table-of-contents">
<h2>Table of Contents</h2>
<div id="text-table-of-contents">
<ul>
<li><a href="#sec-1">1 Data Dredging</a></li>
<li><a href="#sec-2">2 Compulsory inclusions</a></li>
<li><a href="#sec-3">3 AIC vs BIC vs LRTests</a></li>
</ul>
</div>
</div>
-->
<div id="outline-container-1" class="outline-2">
<!--<h2 id="sec-1"><span class="section-number-2">1</span> Data Dredging</h2>-->
<div class="outline-text-2" id="text-1">

<p><a href="http://www.mendeley.com/research/why-did-bluetongue-spread-the-way-it-did-environmental-factors-influencing-the-velocity-of-blueton">The Bluetongue paper</a> we've been discussing at the <a href="http://gis-forum.github.io/study.html">ANU GIS forum</a>  correctly points out that with the "the large number of candidate variables &hellip; a huge number of models could be considered."
</p>
<p>
They go on to say that:
</p>
<p>
"Thus, for practical reasons, we &hellip; isolate independently for each of  three thematic sets of variables (host-, meteorological- and landscape-related covariates) a combination of variables best fitting the data."
</p>
<p>
I don't really get this.  Why not fit the huge number of models (RAM and disk speed permitting) and let AIC or BIC  sift out any combinations that perform well?  For example in a simple instance with four explanatory variables and no interactions the rich model would be:
</p>


\(Y_{i} = \beta_{0} + \beta_{1} X_{1} + \beta_{2} X_{2} + \beta_{3} X_{3} + \beta_{4} X_{4}\)

<p>
Lu, Sonya and I are working on a function to do all the possible combos (interaction terms are possible to include too).  So far we have this code and a link to an old <a href="https://stat.ethz.ch/pipermail/r-help/2007-January/124023.html">Hadley Wickham quote</a>.
That's from 2007, and still haven't herd about any tool developed that really does this. 
</p>
<p>
So far we have this code:
</p>



<pre class="src src-R"><span style="color: #268bd2;">combos</span>  <span style="color: #268bd2; font-weight: bold;">&lt;-</span> <span style="color: #859900; font-weight: bold;">function</span>(yvar, xvars, compulsory = <span style="color: #b58900;">NA</span>)
  {
    formlas <span style="color: #268bd2; font-weight: bold;">&lt;-</span> <span style="color: #b58900;">NULL</span>
    <span style="color: #859900; font-weight: bold;">for</span>(j <span style="color: #859900; font-weight: bold;">in</span> length(xvars):1)
      {
        combns <span style="color: #268bd2; font-weight: bold;">&lt;-</span> combn(xvars, j)
        <span style="color: #859900; font-weight: bold;">for</span>(i <span style="color: #859900; font-weight: bold;">in</span> 1:ncol(combns))
          {
            terms2include <span style="color: #268bd2; font-weight: bold;">&lt;-</span> combns[,i]
            <span style="color: #859900; font-weight: bold;">if</span>(!is.na(compulsory[1]))
              {
                terms2include  <span style="color: #268bd2; font-weight: bold;">&lt;-</span> c(terms2include, compulsory)
              }
            formla <span style="color: #268bd2; font-weight: bold;">&lt;-</span> reformulate(terms2include,                                  
                                  response = yvar
                                  )
            formlas <span style="color: #268bd2; font-weight: bold;">&lt;-</span> c(formlas,formla)     
          }
      }
    <span style="color: #859900; font-weight: bold;">return</span>(formlas)
  }
</pre>


<p>
The resulting list of candidate models are:
</p>



<pre class="src src-R">formlas <span style="color: #268bd2; font-weight: bold;">&lt;-</span> combos(yvar = <span style="color: #2aa198;">"deaths"</span>,
                  xvars = c(<span style="color: #2aa198;">"x1"</span>, <span style="color: #2aa198;">"x2"</span>, <span style="color: #2aa198;">"x3"</span>, <span style="color: #2aa198;">"x4"</span>)
                  )
paste(formlas)

</pre>



<table border="2" cellspacing="0" cellpadding="6" rules="groups" frame="hsides">
<colgroup><col class="left" />
</colgroup>
<tbody>
<tr><td class="left">deaths ~ x1 + x2 + x3 + x4</td></tr>
<tr><td class="left">deaths ~ x1 + x2 + x3</td></tr>
<tr><td class="left">deaths ~ x1 + x2 + x4</td></tr>
<tr><td class="left">deaths ~ x1 + x3 + x4</td></tr>
<tr><td class="left">deaths ~ x2 + x3 + x4</td></tr>
<tr><td class="left">deaths ~ x1 + x2</td></tr>
<tr><td class="left">deaths ~ x1 + x3</td></tr>
<tr><td class="left">deaths ~ x1 + x4</td></tr>
<tr><td class="left">deaths ~ x2 + x3</td></tr>
<tr><td class="left">deaths ~ x2 + x4</td></tr>
<tr><td class="left">deaths ~ x3 + x4</td></tr>
<tr><td class="left">deaths ~ x1</td></tr>
<tr><td class="left">deaths ~ x2</td></tr>
<tr><td class="left">deaths ~ x3</td></tr>
<tr><td class="left">deaths ~ x4</td></tr>
</tbody>
</table>



</div>

</div>

<div id="outline-container-2" class="outline-2">
<h2 id="sec-2"><span class="section-number-2">2</span> Compulsory inclusions</h2>
<div class="outline-text-2" id="text-2">

<p>In some instances you may want to include a variable in all models so the compulsory option can be used.  For example in spatio-temporal models we could include a term for zone and time while assessing the mix of explanatory variables:
</p>



<pre class="src src-R">formlas <span style="color: #268bd2; font-weight: bold;">&lt;-</span> combos(yvar = <span style="color: #2aa198;">"deaths"</span>,
                  xvars = c(<span style="color: #2aa198;">"x1"</span>, <span style="color: #2aa198;">"x2"</span>, <span style="color: #2aa198;">"x3"</span>, <span style="color: #2aa198;">"x4"</span>),
                  compulsory = c(<span style="color: #2aa198;">"zone"</span>, <span style="color: #2aa198;">"ns(time, df = 3)"</span>)
                  )
paste(formlas)

</pre>



<table border="2" cellspacing="0" cellpadding="6" rules="groups" frame="hsides">
<colgroup><col class="left" />
</colgroup>
<tbody>
<tr><td class="left">deaths ~ x1 + x2 + x3 + x4 + zone + ns(time, df = 3)</td></tr>
<tr><td class="left">deaths ~ x1 + x2 + x3 + zone + ns(time, df = 3)</td></tr>
<tr><td class="left">deaths ~ x1 + x2 + x4 + zone + ns(time, df = 3)</td></tr>
<tr><td class="left">deaths ~ x1 + x3 + x4 + zone + ns(time, df = 3)</td></tr>
<tr><td class="left">deaths ~ x2 + x3 + x4 + zone + ns(time, df = 3)</td></tr>
<tr><td class="left">deaths ~ x1 + x2 + zone + ns(time, df = 3)</td></tr>
<tr><td class="left">deaths ~ x1 + x3 + zone + ns(time, df = 3)</td></tr>
<tr><td class="left">deaths ~ x1 + x4 + zone + ns(time, df = 3)</td></tr>
<tr><td class="left">deaths ~ x2 + x3 + zone + ns(time, df = 3)</td></tr>
<tr><td class="left">deaths ~ x2 + x4 + zone + ns(time, df = 3)</td></tr>
<tr><td class="left">deaths ~ x3 + x4 + zone + ns(time, df = 3)</td></tr>
<tr><td class="left">deaths ~ x1 + zone + ns(time, df = 3)</td></tr>
<tr><td class="left">deaths ~ x2 + zone + ns(time, df = 3)</td></tr>
<tr><td class="left">deaths ~ x3 + zone + ns(time, df = 3)</td></tr>
<tr><td class="left">deaths ~ x4 + zone + ns(time, df = 3)</td></tr>
</tbody>
</table>




</div>

</div>

<div id="outline-container-3" class="outline-2">
<h2 id="sec-3"><span class="section-number-2">3</span> AIC vs BIC vs LRTests</h2>
<div class="outline-text-2" id="text-3">

<p>Well now we get into a sort of philosophical debate on how to rank all these models.  That'll have to wait for another day.
</p></div>
</div>
</div>

</body>
</html>
