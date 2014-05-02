---
name: morpho-has-an-issue-with-zero-length-strings-as-missing-data
layout: post
title: morpho-has-an-issue-with-zero-length-strings-as-missing-data
date: 2014-05-02
categories:
- Data Documentation
tags: 
- morpho
- bugs
---

We encountered a strange issue Morpho 1.8 has when ingesting a CSV with zero length strings as missing data.  An example of what this looks like is given below in the mulgara example dataset I;ve shown before.  I have added some rows with missing data as zero length strings (these are the ",," after the fictional value Treat = 0.5).

#### R Code:
    datatext <- 'Treat, Before, After1, After2
    a,,-9999,9999
    a,,-9999,9999
    a,,-9999,9999
    a,,-9999,9999
    a,,-9999,9999
    a,,-9999,9999
    a,,-9999,9999
    a,,-9999,9999
    0,  2.833213344,    1.609437912,    2.48490665
    0,  1.791759469,    2.197224577,    2.079441542
    0,  3.044522438,    2.708050201,    3.135494216
    0,  2.772588722,    1.791759469,    2.197224577
    0,  1.098612289,    1.609437912,    2.63905733
    1,  2.944438979,    0.693147181,    1.791759469
    1,  2.564949357,    0.693147181,    1.791759469
    1,  2.564949357,    1.609437912,    1.609437912
    1,  0.693147181,    1.098612289,    1.098612289
    1,  1.609437912,    0,      1.098612289'
    analyte <- read.csv(textConnection(datatext))
    write.csv(analyte, "inst/extdata/morpho-bug-empty-na.csv", row.names = F, na= "", quote=F)

<p></p>

- Unfortunately for this blog entry, the example above doesn;t exhibit the problem!
- you can see what happens by selecting the "treat consecutive delimiters as as one" option
- showing that the data from the 3rd and 4th cols shifts to the right
- this is what happened to us but we were not able to modify this behaviour by changing that option!
- The problem only occurred when we had a file big file (200+ columns)
- the problem occured at col 23, shown in the image below

![morpho-bug-empty-na3.png](/images/morpho-bug-empty-na3.png)

- this column is ftyp[12] which has 62 rows of missing and then some text codes.
- the next 24th column is  aerial[10] and it is this one that is then read incorrectly by morpho.  The importer makes the error of reading blanks for the first few rows and then *, even though in reality it is * and then date 1/06/2006 (shown in the image below)

![morpho-bug-empty-na2.1.png](/images/morpho-bug-empty-na2.1.png)

- and finally col 25 fire[13] now appears as * and the date 1/06/2006 but it should be a different number of *s and the date 2/04/2007 further down

![morpho-bug-empty-na2.png](/images/morpho-bug-empty-na2.png)

### Workaround

- to deal with this in this case we replaced all zero length strings as "NA"
- this is probably a good idea in most cases, except when NA is not an appropriate value and so in those cases we replaced with the word "blank"

### Conclusions

- This issue is probably rare and might be fixed in the newer version of Morpho
- We don;t use new morpho because we are still using the old metacat
- I thought it worth reporting here
