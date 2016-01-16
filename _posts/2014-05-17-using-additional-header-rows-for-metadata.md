---
name: 2014-05-17-using-additional-header-rows-for-metadata
layout: post
title: using-additional-header-rows-for-metadata
date: 2014-05-17
categories:
- Data Documentation
---


<body>
<div id="toc">
<div id="toc_header">Table of Contents</div>
<ul>
<li>
<a href="#toc_0">Comment on eMast recommendations</a>
<ul>
<li>
<ul>
<li>
<a href="#toc_1">Introduction</a>
</li>
<li>
<a href="#toc_2">R code</a>
<ul>
<li>
<a href="#toc_3">Construct some fake data</a>
</li>
<li>
<a href="#toc_4">Run the aggregation of trait data program provided in eMast doc</a>
</li>
<li>
<a href="#toc_5">Minor modifications to make it work</a>
</li>
<li>
<a href="#toc_6">Now finish off with the example code</a>
</li>
</ul>
</li>
</ul>
</li>
</ul>
</li>
</ul>
</div>


<h1 id="toc_0">Comment on eMast recommendations</h1>

<p><a href="mailto:ivan.hanigan@anu.edu.au">ivan.hanigan@anu.edu.au</a></p>

<h3 id="toc_1">Introduction</h3>

<ul>
<li>I was lucky to be forwarded a copy of the document &ldquo;DRAFT Best practices for collecting, processing and collating plant trait data&rdquo; (V0.0).</li>
<li>What I like most about this is the statement on page nine under &ldquo;3. Best practice collection techniques&rdquo; 
that &ldquo;Datasets should be maintained following two simple practices of formatting and cataloguing&rdquo;.</li>
<li>I think the recomendations are very sensible but I have the following comment regarding the proposed file structure shown in the table </li>
</ul>

<p><img src="data:image/png;base64,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" alt="emast-format.png"/></p>

<ul>
<li>I have not used the second row for the units before, but rather have encoded this information in a second metadata file that I keep with the main data file.</li>
<li>This second row does seem attractive </li>
<li>BUT  as this might be interpreted as the first row of data after the header row of column names this needs extra code to be written to allow importation to statistics packages.</li>
<li>While this can be easily handled by writing extra code to treat this first row separately,  this does seem a bit risky to expect ordinary data users to do so.</li>
<li>I wonder if the intention of the authors is to include this in the column NAME rather than just in the column as the statement currently reads (&ldquo;the units of measurement and an expanded definition of the data recorded in each column&rdquo;) and the table shows?</li>
<li>For example the R code given in the Appendix &ldquo;R script to aggregate unprocessed trait data into summary statistics ready for the EMP DATABASE&rdquo;</li>
</ul>

<h3 id="toc_2">R code</h3>

<ul>
<li>The eMast Document provides an interesting appendix with R codes.<br/></li>
<li>The following is an attempt to make a vignette that will run with the example data provided. </li>
</ul>

<h4 id="toc_3">Construct some fake data</h4>

<pre><code class="r">
dat &lt;- read.csv(textConnection(&quot;Date    ,Latitude,Longitude,Genus,Species,Tree No.,Meas. No.,Photosynthesis,Air Temp.,Height\n         ,      oS,       oE,          ,       ,   , ,umol m-2 s-1, oC, m\n1/10/2004,-43.4444,140.1453 ,Eucalyptus,Saligna,  1,1,15.043,25.56,15\n1/10/2004,-43.4444,140.1453 ,Eucalyptus,Saligna,  1,2,15.998,25.56,15\n1/10/2004,-43.4444,140.1453 ,Eucalyptus,Saligna,  1,3,15.584,25.56,15\n&quot;))
# write a couple of fake data files
for (i in 1:2) {
    write.csv(dat, paste(&quot;Book&quot;, i, &quot;.csv&quot;, sep = &quot;&quot;), row.names = F)
}
# show me the data
print(xtable(dat), type = &quot;html&quot;)
</code></pre>

<!-- html table generated in R 3.1.0 by xtable 1.7-1 package -->

<!-- Wed May  7 16:19:23 2014 -->

<TABLE border=1>
<TR> <TH>  </TH> <TH> Date </TH> <TH> Latitude </TH> <TH> Longitude </TH> <TH> Genus </TH> <TH> Species </TH> <TH> Tree.No. </TH> <TH> Meas..No. </TH> <TH> Photosynthesis </TH> <TH> Air.Temp. </TH> <TH> Height </TH>  </TR>
  <TR> <TD align="right"> 1 </TD> <TD>           </TD> <TD>       oS </TD> <TD>        oE </TD> <TD>            </TD> <TD>         </TD> <TD align="right">  </TD> <TD align="right">  </TD> <TD> umol m-2 s-1 </TD> <TD>  oC </TD> <TD>  m </TD> </TR>
  <TR> <TD align="right"> 2 </TD> <TD> 1/10/2004 </TD> <TD> -43.4444 </TD> <TD> 140.1453  </TD> <TD> Eucalyptus </TD> <TD> Saligna </TD> <TD align="right">   1 </TD> <TD align="right">   1 </TD> <TD> 15.043 </TD> <TD> 25.56 </TD> <TD> 15 </TD> </TR>
  <TR> <TD align="right"> 3 </TD> <TD> 1/10/2004 </TD> <TD> -43.4444 </TD> <TD> 140.1453  </TD> <TD> Eucalyptus </TD> <TD> Saligna </TD> <TD align="right">   1 </TD> <TD align="right">   2 </TD> <TD> 15.998 </TD> <TD> 25.56 </TD> <TD> 15 </TD> </TR>
  <TR> <TD align="right"> 4 </TD> <TD> 1/10/2004 </TD> <TD> -43.4444 </TD> <TD> 140.1453  </TD> <TD> Eucalyptus </TD> <TD> Saligna </TD> <TD align="right">   1 </TD> <TD align="right">   3 </TD> <TD> 15.584 </TD> <TD> 25.56 </TD> <TD> 15 </TD> </TR>
   </TABLE>

<h4 id="toc_4">Run the aggregation of trait data program provided in eMast doc</h4>

<pre><code class="r">
library(stringr)
# This function summarises the data, one just needs to past the parameter of
# interest and the quantities by which it varies around.
do.sumy &lt;- function(pars, lab, dat) {
    epars &lt;- as.formula(pars)
    mu &lt;- aggregate(epars, data = dat, mean)
    md &lt;- aggregate(epars, data = dat, median)
    se &lt;- aggregate(epars, data = dat, sd)
    mx &lt;- aggregate(epars, data = dat, min)
    mn &lt;- aggregate(epars, data = dat, max)
    NN &lt;- aggregate(epars, data = dat, length)
    drp0 &lt;- unlist(strsplit(pars, &quot;\\+&quot;))
    drp &lt;- -length(drp0):-1
    df1 &lt;- cbind(mu, md[, drp], se[, drp], mx[, drp], mn[, drp], NN[, drp])
    df2 &lt;- cbind(df1, Parameter = lab)
    hd1 &lt;- gsub(&quot;^\\w.*.~&quot;, &quot;&quot;, drp0)
    names(df2) &lt;- c(hd1, &quot;Mean&quot;, &quot;Median&quot;, &quot;Std&quot;, &quot;Min&quot;, &quot;Max&quot;, &quot;N&quot;, &quot;Parameter&quot;)
    return(df2)
}

# Not Required setwd(&#39;~/where/is/the/data/?&#39;)
files &lt;- list.files(pattern = &quot;*.csv&quot;)
# files
data &lt;- lapply(files, read.csv, header = T, stringsAsFactors = F, strip.white = T)
</code></pre>

<h4 id="toc_5">Minor modifications to make it work</h4>

<ul>
<li>I needed to write the following to read the csv with metadata row</li>
</ul>

<pre><code class="r">
#### Notes str(data) as expected, these are sometimes imported as character due
#### to the second row so need to fix it also because the data object is a list
#### of data.frames, it is easier to run the example if we will just create
#### individual data frames
read_metadata_csv &lt;- function(filename) {
    dat &lt;- read.csv(filename, skip = 1)
    col.defs &lt;- names(read.csv(filename, nrow = 0))
    unit.defs &lt;- read.csv(filename, nrow = 1, stringsAsFactors = F)
    attributes(dat)$unit.defs &lt;- unit.defs[1, ]
    names(dat) &lt;- col.defs
    return(dat)
}
# files
data &lt;- read_metadata_csv(files[1])
# str(data)
</code></pre>

<h4 id="toc_6">Now finish off with the example code</h4>

<pre><code class="r">#### NOTE this is not relevant here so commented out If the Genus and Species
#### is not separate, then split it up split.spp &lt;- strsplit( data$Spp.Name, &#39;
#### &#39; ) data$Genus &lt;- sapply( split.spp, &#39;[[&#39;, 1 ) data$Species &lt;- sapply(
#### split.spp, &#39;[[&#39;, 2 )



# Get the summary stats for each interesting trait
Height &lt;- do.sumy(&quot;Height~Photosynthesis+Genus+Species&quot;, &quot;Height&quot;, data)
# show me the data
print(xtable(Height), type = &quot;html&quot;)
</code></pre>

<!-- html table generated in R 3.1.0 by xtable 1.7-1 package -->

<!-- Wed May  7 16:19:23 2014 -->

<TABLE border=1>
<TR> <TH>  </TH> <TH> Photosynthesis </TH> <TH> Genus </TH> <TH> Species </TH> <TH> Mean </TH> <TH> Median </TH> <TH> Std </TH> <TH> Min </TH> <TH> Max </TH> <TH> N </TH> <TH> Parameter </TH>  </TR>
  <TR> <TD align="right"> 1 </TD> <TD align="right"> 15.04 </TD> <TD> Eucalyptus </TD> <TD> Saligna </TD> <TD align="right"> 15.00 </TD> <TD align="right">  15 </TD> <TD align="right">  </TD> <TD align="right">  15 </TD> <TD align="right">  15 </TD> <TD align="right">   1 </TD> <TD> Height </TD> </TR>
  <TR> <TD align="right"> 2 </TD> <TD align="right"> 15.58 </TD> <TD> Eucalyptus </TD> <TD> Saligna </TD> <TD align="right"> 15.00 </TD> <TD align="right">  15 </TD> <TD align="right">  </TD> <TD align="right">  15 </TD> <TD align="right">  15 </TD> <TD align="right">   1 </TD> <TD> Height </TD> </TR>
  <TR> <TD align="right"> 3 </TD> <TD align="right"> 16.00 </TD> <TD> Eucalyptus </TD> <TD> Saligna </TD> <TD align="right"> 15.00 </TD> <TD align="right">  15 </TD> <TD align="right">  </TD> <TD align="right">  15 </TD> <TD align="right">  15 </TD> <TD align="right">   1 </TD> <TD> Height </TD> </TR>
   </TABLE>

<pre><code class="r">#### not available Vcmax &lt;- do.sumy( &#39;Vcmax25~CO2.treatment+Genus+Species&#39;,
#### &#39;VCMAXM25&#39;, data ) Jmax &lt;- do.sumy( &#39;Jmax25~CO2.treatment+Genus+Species&#39;,
#### &#39;JMAXM25&#39;, data ) VjVn &lt;- do.sumy( &#39;J.V~CO2.treatment+Genus+Species&#39;,
#### &#39;VJVN&#39;, data ) Tleaf &lt;- do.sumy(
#### &#39;Tleaf_avg~CO2.treatment+Genus+Species&#39;,&#39;TLEAF&#39;, data ) all.Y &lt;- rbind(
#### Vcmax, Jmax, VjVn, Tleaf )

## # Re-arrange the columns to the correct order exp.dat1 &lt;- subset( all.Y,
## select=c(&#39;Genus&#39;,&#39;Species&#39;,&#39;Parameter&#39;,&#39;Mean&#39;,&#39;Median&#39;,&#39;Std&#39;,&#39;Min&#39;,&#39;Max&#39;,&#39;N&#39;,&#39;CO2.treatment&#39;)
## )

## # save it somewhere write.table( exp.dat1, &#39;choose/folder/to/save/to.csv&#39;,
## sep=&#39;,&#39;, row.names=F, col.names=T, na=&#39;&#39; )

</code></pre>

</body>