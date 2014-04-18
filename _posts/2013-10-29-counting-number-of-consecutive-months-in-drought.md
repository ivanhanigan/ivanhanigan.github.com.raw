---
name: counting-number-of-consecutive-months-in-drought
layout: post
title: counting-number-of-consecutive-months-in-drought
date: 2013-10-29
categories:
- extreme weather events
---

I got this question today from a Drought researcher:

#### Question:
    There a table with 62 years * 12 months of rain data in mm. We
    calculated the cumulative distribution using ecdf: empirical
    cumulative distribution function. So the table looks like this:
    Year Jan Feb Mach (…) each cell contains the cum dist.
      
    We also got the number of months per year with less than X mm of
    rain. But he needs to know how many months are between the
    drought months, regardless the year. So, I thought that
    converting the data into a ts was going to facilitate the task,
    but it doesn’t, because now I don’t’ have columns and rows any
    longer.
     
    How do I handle a ts object to do for example an ifelse?

<p></p>
I answered:

This looks a lot like the Hutchinson Drought Index which I've coded up here

- [https://github.com/ivanhanigan/HutchinsonDroughtIndex](https://github.com/ivanhanigan/HutchinsonDroughtIndex)
- [https://github.com/ivanhanigan/HutchinsonDroughtIndex/blob/master/src/HutchinsonDroughtIndex_tools_droughtIndex.r](https://github.com/ivanhanigan/HutchinsonDroughtIndex/blob/master/src/HutchinsonDroughtIndex_tools_droughtIndex.r)
- Also there is a completely reproducible example with BoM rainfall data at [https://github.com/ivanhanigan/SuicideAndDroughtInNSW](https://github.com/ivanhanigan/SuicideAndDroughtInNSW)

This is the key bit for counting consecutive months below a threshold
#### R Code:
    x<-data$index<=-1
    xx <- (cumsum(!x) + 1) * x
    x2<-(seq_along(x) - match(xx, xx) + 1) * x
    data$count<-x2
<p></p>  
I got it from [https://stat.ethz.ch/pipermail/r-help/2007-June/134594.html](https://stat.ethz.ch/pipermail/r-help/2007-June/134594.html)
and looked in wonder at the structure and am amazed it works.

I also really like the cumulative summing version a lot

#### R Code:
    data$sums<-as.numeric(0)
    y <- ifelse(data$index >= -1, 0, data$index)
    f <- data$index < -1
    f <- (cumsum(!f) + 1) * f
    z <- unsplit(lapply(split(y,f),cumsum),f)
    data$sums <- z
<p></p>  
Several things I'd like to change.

- I like the idea of using a wide dataset and ecdf rather than my loop thru months
- I'd like to look into Joe Wheatley;s approach [http://joewheatley.net/20th-century-droughts/](]http://joewheatley.net/20th-century-droughts/)
- I was defeated by Mike's request to make a different threshold for breaking a drought than starting a drought.  went back to a for loop
