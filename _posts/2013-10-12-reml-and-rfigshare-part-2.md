---
name: reml-and-rfigshare-part-2
layout: post
title: reml-and-rfigshare-part-2
date: 2013-10-12
categories:
- Data Documentation
---

In the last post I explored the functionality of reml.
This time I will try to send data to figshare.

- First follow [These Instructions](https://github.com/ropensci/rfigshare) to get rfigshare set up.  In particular store your figshare credentials in ~/.Rprofile

#### Code:reml-and-rfigshare-part-2
    # func
    require(devtools)
    install_github("reml", "ropensci")
    require(reml)
    install_github("rfigshare", "ropensci")
    require(rfigshare)
    install_github("disentangle", "ivanhanigan")
    require(disentangle)
    # load
    fpath <- system.file(file.path("extdata","civst_gend_sector_eml.xml"), package = "disentangle")
    setwd(dirname(fpath))
    obj <- eml_read(fpath)
    # clean
    obj
    # do

    ## STEP 1: find one of the preset categories
    # available. We can ask the API for
    # a list of all the categories:
    list <- fs_category_list()
    list[grep("Survey", list)]

    ## STEP 2: PUBLISH TO FIGSHARE
    id <- eml_publish(fname,
                      description="Example EML
                        A fictional dataset",
                      categories = "Survey results",
                      tags = "EML",
                      destination="figshare"
                      )
    # there are several warnings
    # but go to figshare and it has sent the metadata and data OK

    # make public using either the figshare web interface, the
    # rfigshare package (using fs_make_public(id)) or just by adding
    # the argument visibility = TRUE to the above eml_publish
    fs_make_public(id)

    
<p></p>
# Now these data are on figshare

Now I have published the data they are visible and have a DOI


<iframe src="http://wl.figshare.com/articles/820158/embed?show_title=1" width="568" height="157" frameborder="0"></iframe>
