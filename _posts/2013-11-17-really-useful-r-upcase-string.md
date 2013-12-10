---
name: 2013-11-17-really-useful-r-upcase-string
layout: post
title: really-useful-r-upcase-string
date: 2013-11-17
categories:
- research methods
---

Here is a really useful R snippet from  [http://stackoverflow.com/a/6364905](http://stackoverflow.com/a/6364905) with a minor modification to allow differnt splits

#### Code:r-upcase-string
    x <- c("The", "quick", "Brown", "fox/lazy dog")
     
    simpleCap <- function(x, tosplit = " ") {
      s <- strsplit(x, tosplit)[[1]]
      paste(toupper(substring(s, 1,1)), substring(s, 2),
          sep="", collapse=tosplit)
    }
    sapply(x, simpleCap)
    sapply(x, simpleCap, tosplit = "/")
