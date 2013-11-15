---
name: handling-survey-data-with-r
layout: post
title: handling-survey-data-with-r
date: 2013-11-06
categories:
- Data Documentation
- surveys
---

R is generally very good for handling many different data types but

### R has problems with survey data

This post is a stub about what packages Ive found with methods allowing to handle efficiently survey data: handle variable labels, values labels, and retrieve information about missing values

#### Base R:
    ## Not run:
    require(foreign)
    analyte  <- read.spss(filename, to.data.frame=T) 
    varslist <- as.data.frame(attributes(analyte)$variable.labels)
    # this gives a pretty useful thing to use
<p></p>

While I was digging around in [TraMineR](http://mephisto.unige.ch/traminer) I found this link to Dataset, Emmanuel Rousseaux's package for handling, documenting and describing data sets of survey data. 

#### Code:Dataset, a package for handling-survey-data-with-r
    if(!require(Dataset)) install.packages("Dataset", repos="http://R-Forge.R-project.org");
    require(Dataset)
    data(dds)
    str(dds)
    # cool
    description(dds$sexe)
    # excellent!

<p></p>

### Conclusions

I'm sure there are plenty of other approaches.  I'll add them as I find them'
