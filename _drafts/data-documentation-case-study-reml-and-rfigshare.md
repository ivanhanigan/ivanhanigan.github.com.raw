---
name: two-main-types-of-data-documentation-workflow
layout: post
title: two-main-types-of-data-documentation-workflow
categories:
- Data Documentation
---

#### Case Study
First we will look at the work of the ROpenSci team and the reml
package.  In the vignette they show how to publish data to figshare
using rfigshare package.  [figshare](http://figshare.com/) is a site
where scientists can share datasets/figures/code. The goals are to
encourage researchers to share negative results and make reproducible
research efforts user-friendly. It also uses a tagging system for
scientific research discovery. They give you unlimited public space
and 1GB of private space.  


#### Code:
    # document
    require(devtools)
    install_github("reml", "ropensci")
    require(reml)
    eml_write(civst_gend_sector, 
              title = "reml example",  
              description = "An example, intended for
                                  illustrative purposes only.",
              creator = "Ivan Hanigan <ivanhanigan@gmail.com>",
              file = "reml_example.xml")
    obj <- eml_read("reml_example.xml")
    obj 
    str(dataTable(obj))
    head(dataTable(obj))
