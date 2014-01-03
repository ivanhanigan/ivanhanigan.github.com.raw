---
name: 2013-12-03-non-linear-relationships-vs-non-linear-models-vis-a-vis-curvi-linear-terms
layout: post
title: non-linear-relationships-vs-non-linear-models-vis-a-vis-curvi-linear-terms
date: 2013-12-03
categories:
- research methods
- statistical models
---


<head>
<title>non-linear-model-vs-non-linear-relationship </title>
<meta http-equiv="Content-Type" content="text/html;charset=iso-8859-1"/>
<meta name="title" content="non-linear-model-vs-non-linear-relationship "/>
<meta name="generator" content="Org-mode"/>
<meta name="generated" content="2013-12-03T17:29+1100"/>
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
<h1 class="title">non-linear-model-vs-non-linear-relationship </h1>


<hr/>


<div id="table-of-contents">
<h2>Table of Contents</h2>
<div id="text-table-of-contents">
<ul>
<li><a href="#sec-1">1 non-linear-relationships-vs-non-linear-models</a>
<ul>
<li><a href="#sec-1-1">1.1 Nonlinear Regression vs. Linear Regression</a>
<ul>
<li><a href="#sec-1-1-1">1.1.1 Model 1</a></li>
<li><a href="#sec-1-1-2">1.1.2 Model 2</a></li>
</ul>
</li>
<li><a href="#sec-1-2">1.2 Conclusions</a></li>
</ul>
</li>
</ul>
</div>
</div>

<div id="outline-container-1" class="outline-2">
<h2 id="sec-1"><span class="section-number-2">1</span> non-linear-relationships-vs-non-linear-models</h2>
<div class="outline-text-2" id="text-1">


<ul>
<li>I value precise language very highly
</li>
<li>this is because in multi-disciplinary teams it is easy to talk using the same words and mean different things
</li>
<li>in recent discussion about <a href="http://cran.r-project.org/web/packages/dlnm/index.html">Distributed Lag Non-linear Models</a> I started to reflect on something that has bothered me for a While
</li>
<li>back in 2005 my old mate Prof Keith Dear picked me up on using the term "non-linear model" incorrectly and explained the maths&hellip;
</li>
<li>I kind of understood but promptly forgot and found a lot of people use the term non-linear model a bit carelessly
</li>
<li>Yesterday I was in a discussion about comparing non-linear relationships between different studies in a meta-analysis
</li>
<li>I immediatly felt uncomfortable when we started to discuss these as "non-linear models"
</li>
<li>so here is a quick bit of google fu (with a session at the coffee shop with Steve and Mishka) to remind me about the difference between 
</li>
</ul>



</div>

<div id="outline-container-1-1" class="outline-3">
<h3 id="sec-1-1"><span class="section-number-3">1.1</span> Nonlinear Regression vs. Linear Regression</h3>
<div class="outline-text-3" id="text-1-1">


<ul>
<li>the following comes from
</li>
<li><a href="http://www.ats.ucla.edu/stat/sas/library/SASNLin_os.htm">http://www.ats.ucla.edu/stat/sas/library/SASNLin_os.htm</a>
</li>
<li>verbatim except for my attempt at mathjax notation in latex
</li>
</ul>


<p>
A regression model is called nonlinear, if the derivatives
of the model with respect to the model parameters depends on one or
more parameters. This definition is essential to distinguish nonlinear
from curvilinear regression. A regression model is not necessarily
nonlinear if the graphed regression trend is curved. A polynomial
model such as this:
</p>

</div>

<div id="outline-container-1-1-1" class="outline-4">
<h4 id="sec-1-1-1"><span class="section-number-4">1.1.1</span> Model 1</h4>
<div class="outline-text-4" id="text-1-1-1">




\(Y_{i} = \beta_{0} + \beta_{1} X_{i} + \beta_{2} X_{i}^2 + \epsilon_{i}\)

<ul>
<li>appears curved when y is plotted against x. It is, however, not a nonlinear model. To see this, take derivatives of y with respect to the parameters b0, b1
</li>
<li>dy/db0 = 1 
</li>
<li>dy/db1 = x 
</li>
<li>dy/db2 = x<sup>2</sup> 
</li>
</ul>



<ul>
<li>None of these derivatives depends on a model parameter, the model is linear. In contrast, consider the log-logistic model 
</li>
</ul>


</div>

</div>

<div id="outline-container-1-1-2" class="outline-4">
<h4 id="sec-1-1-2"><span class="section-number-4">1.1.2</span> Model 2</h4>
<div class="outline-text-4" id="text-1-1-2">




\(Y_{i} = d + (a - d)/(1 + e^{b \times log(x/g)}) + \epsilon\)

<ul>
<li>Take derivatives with respect to d, for example: 
</li>
</ul>




\(dy/dd = 1 - 1/(1 + e^{b \times log(x/g)})\)

<ul>
<li>The derivative involves other parameters, hence the model is nonlinear.
</li>
</ul>


</div>
</div>

</div>

<div id="outline-container-1-2" class="outline-3">
<h3 id="sec-1-2"><span class="section-number-3">1.2</span> Conclusions</h3>
<div class="outline-text-3" id="text-1-2">


<ul>
<li>It is probably best to refer to the polynomial as a "non-linear relationship" in a linear model
</li>
<li>reserving "non-linear model" for things like Model 2
</li>
</ul>



</div>
</div>
</div>
</div>

</body>
</html>