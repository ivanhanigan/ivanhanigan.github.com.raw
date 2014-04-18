---
name: aggregation-of-statistical-local-areas
layout: post
title: Aggregation Of Statistical Local Areas
date: 2014-02-18
categories:
- spatial
---

## Reproducibility 

- A subset of the data and code used for this blog post is available at [https://github.com/ivanhanigan/aggregation-of-slas-or-sa2s](https://github.com/ivanhanigan/aggregation-of-slas-or-sa2s)
- Some parts of the data I used are not available due to shared Intellectual Property 
- The spatial data and SEIFA Socioeconomic index data are publicly available from the Australian Bureau of Statistics
- The New Groups categories were generously contributed by John Glover of the Public Health Information Development Unit, The University of Adelaide.

## Introduction

The Aim is to aggregate Statistical Local Areas (SLAs, recently relabelled SA2) Australian Standard Geographical Classification (ASGC, recently relabelled ASGS) to achieve a greater level of privacy protection.
The rules to achieve a geography amenable to statistical comparisons are:

- similar populations (around 20,000 to 30,000)
- homogenous Index of Relative Socioeconomic Disadvantage
- nested within the next level up in the ASGC/ASGS
- so that SSD (recently relabelled SA3) are not split.
- the SA2s can be aggregated through a process of assigning alike areas to groups, and reviewing/adjusting these assignments
- This document contains some suggestions for adjusting groupings to better reflect differences in the level of disadvantage, while still adhering to the rules outlined.

## Results

### Data Prep

- The data were prepared as spatial files

![alttext](/images/aggregation-of-sa2s.png)



### Assess proposed split in Belconnen

- the proposed split in belconnen looks good
- This involves splitting Belconnen West (old SLA group) into two regions. The first generally has much higher proportion of individuals in a bottom quintile SES score
- Group 1 =  Belconnen/ Charnwood/ Florey/ Higgins/ Holt/ Latham
- Group 2 =  Flynn (ACT)/ Fraser/ Melba/ Spence

![alttext](/images/belco-split.png)

### Assess the outliers 

- this can be done by identifying their component CCD SEIFA within new groups
- the seifa of CCD in outliers are compared to the others within their new groups

![alttext](/images/seifa-by-newgroups1.png)

- zoom in on croweded areas

![alttext](/images/seifa-by-newgroups1-2.png)

<!-- html table generated in R 3.0.2 by xtable 1.7-1 package -->
<!-- Tue Feb 18 22:03:04 2014 -->
<TABLE border=1>
<TR> <TH>  </TH> <TH> sa2_name.x </TH> <TH> new_sa2_group </TH> <TH> notes </TH>  </TR>
  <TR> <TD align="right"> 12 </TD> <TD> Bruce </TD> <TD> Bruce/ Evatt/ Giralang/ Kaleen/ Lawson/ McKellar </TD> <TD> higher than neighbours </TD> </TR>
  <TR> <TD align="right"> 14 </TD> <TD> Campbell </TD> <TD> Acton/ Braddon/ Campbell/ Civic/ Reid/ Turner </TD> <TD> ok </TD> </TR>
  <TR> <TD align="right"> 20 </TD> <TD> Civic </TD> <TD> Acton/ Braddon/ Campbell/ Civic/ Reid/ Turner </TD> <TD> ok </TD> </TR>
  <TR> <TD align="right"> 31 </TD> <TD> Fadden </TD> <TD> Fadden/ Gowrie (ACT)/ Macarthur/ Monash </TD> <TD> ok </TD> </TR>
  <TR> <TD align="right"> 32 </TD> <TD> Farrer </TD> <TD> Farrer/ Isaacs/ Mawson/ Pearce/ Torrens </TD> <TD> higher than neighbours bar one ccd </TD> </TR>
  <TR> <TD align="right"> 37 </TD> <TD> Forrest </TD> <TD> Forrest/ Griffith (ACT)/ Kingston - Barton/ Narrabundah/ Red Hill (ACT) </TD> <TD> higher than neighbours </TD> </TR>
  <TR> <TD align="right"> 60 </TD> <TD> Isaacs </TD> <TD> Farrer/ Isaacs/ Mawson/ Pearce/ Torrens </TD> <TD> higher than neighbours bar one ccd </TD> </TR>
  <TR> <TD align="right"> 64 </TD> <TD> Kingston - Barton </TD> <TD> Forrest/ Griffith (ACT)/ Kingston - Barton/ Narrabundah/ Red Hill (ACT) </TD> <TD> higher than neighbours </TD> </TR>
  <TR> <TD align="right"> 71 </TD> <TD> Macarthur </TD> <TD> Fadden/ Gowrie (ACT)/ Macarthur/ Monash </TD> <TD> ok </TD> </TR>
  <TR> <TD align="right"> 73 </TD> <TD> Macquarie </TD> <TD> Aranda/ Cook/ Hawker/ Macquarie/ Page/ Scullin/ Weetangera </TD> <TD> ok </TD> </TR>
  <TR> <TD align="right"> 87 </TD> <TD> O'Malley </TD> <TD> Chifley/ Lyons (ACT)/ O'Malley/ Phillip </TD> <TD> higher than neighbours </TD> </TR>
  <TR> <TD align="right"> 89 </TD> <TD> Page </TD> <TD> Aranda/ Cook/ Hawker/ Macquarie/ Page/ Scullin/ Weetangera </TD> <TD> ok </TD> </TR>
  <TR> <TD align="right"> 98 </TD> <TD> Scullin </TD> <TD> Aranda/ Cook/ Hawker/ Macquarie/ Page/ Scullin/ Weetangera </TD> <TD> ok </TD> </TR>
   </TABLE>
   
### Investigating areas: eg the Kingston - Barton area 

- we can zoom in on some of these areas
  
![alttext](/images/kingston-barton.png)
  
## Conclusions

Basically, the problem comes from public housing policies in Canberra which distorts the effect of the housing market and land values in segregating rich from poor. Essentially, there are highly advantaged suburbs with pockets of disadvantaged public housing.  

Other 'problematic' features re this are:
    
- proximity to ornamental lakes
- proximity to urban green space
- proximity to rural residential hubs (walaroo road?  hall?).  This is a bit of a reverse statement -- but different to 'distance from urban centre'
- elevation, especially with a view.

Potentially the issue is going to be that this can't be solved if you want to maintain SA2 as the base level - the distinctions are going to be at an SA1 or even mesh block level.
