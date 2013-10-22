---
name: data-documentation-case-study-reml-and-rfigshare
layout: post
title: data-documentation-case-study-reml-and-rfigshare
date: 2013-10-11
categories:
- Data Documentation
---

#### Case Study: reml-and-rfigshare
First we will look at the work of the ROpenSci team and the reml
package.  In the vignette they show how to publish data to figshare
using rfigshare package.  [figshare](http://figshare.com/) is a site
where scientists can share datasets/figures/code. The goals are to
encourage researchers to share negative results and make reproducible
research efforts user-friendly. It also uses a tagging system for
scientific research discovery. They give you unlimited public space
and 1GB of private space.  

Start by getting the reml package.

#### Code:
    # func
    require(devtools)
    install_github("reml", "ropensci")
    require(reml)
    ?eml_write
<p></p>
This is the Top-level API function for writing eml.  Help page is a bit sparse.  See [This Link](https://github.com/ropensci/reml) for more.  For eg "for convenience, dat could simply be a data.frame and reml will launch it's metadata wizard to assist in constructing the metadata based on the data.frame provided. While this may be helpful starting out, regular users will find it faster to define the columns and units directly in the format above."


#### Code:
    install_github("disentangle", "ivanhanigan") # for the data
                                                 # described in prev post

    # load
    fpath <- system.file(file.path("extdata", "civst_gend_sector.csv"),
                         package = "disentangle"
                         )
    civst_gend_sector <- read.csv(fpath)

    # clean
    str(civst_gend_sector)

    # do
    eml_write(civst_gend_sector,
              creator = "Ivan Hanigan <ivanhanigan@gmail.com>")


              


    # Starts up the wizard, a section is shown below.  The wizard
    # prompts in the console and the user writes the answer.

    # Enter description for column 'civil_status':
    #  marriage status
    # column civil_status appears to contain categorical data.
    #  
    # Categories are divorced/widowed, married, single
    #  Please define each of the categories at the prompt
    # define 'divorced/widowed':
    # was once married
    # define 'married':
    # still married
    # define 'single':
    # never married

    # TODO I don't really know what activity_sector is.  I assumed
    # school because Categories are primary, secondary, tertiary.

    # this created "metadata.xml" and "metadata.csv"
    file.remove(c("metadata.xml","metadata.csv"))
<p></p>  
This was a very minimal data documentation effort.  A bit more detail would look like this.  Because I would now need to re-write all that in the wizard I will take the advice of the help file that "regular users will find it faster to define the columns and units directly in the format"

#### Code:
    ds <- data.set(civst_gend_sector,
                   col.defs = c("Marriage status", "sex", "education", "counts"),
                   unit.defs = list(c("was once married","still married","never married"),
                       c("women", "men"),
                       c("primary school","secondary school","tertiary school"),
                       c("persons"))
                   )
    ds
    # this prints the dataset and the metadata
    # now run the EML function
    eml_write(ds, 
              title = "civst_gend_sector",  
              description = "An example, fictional dataset for Decision Tree Models",
              creator = "Ivan Hanigan <ivanhanigan@gmail.com>",
              file = "civst_gend_sector.xml"
              )
    # this created the xml and csv with out asking anything
    # but returned a
    ## Warning message:
    ## In `[<-.data.frame`(`*tmp*`, , value = list(civil_status = c(2L,  :
    ##   Setting class(x) to NULL;   result will no longer be an S4 object

    # TODO investigate this?

    # now we can access the local EML
    obj <- eml_read("civst_gend_sector.xml")
    obj 
    str(dataTable(obj))
    # returns an error
    ## Error in plyr::compact(lapply(slotNames(from), function(s) if (!isEmpty(slot(from,  (from attribute.R#300) : 
    ##   subscript out of bounds
<p></p>

# Conclusions
So this looks like a useful tool.  Next steps are to:
- look at sending these data to figshare
- describe a really really REALLY simple workflow (3 lines? create metadata, eml_write, push to figshare)
