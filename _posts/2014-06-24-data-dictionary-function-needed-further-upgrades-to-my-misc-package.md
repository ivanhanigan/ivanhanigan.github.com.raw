---
name: 2014-06-24-data-dictionary-function-needed-further-upgrades-to-my-misc-package
layout: post
title: data-dictionary-function-needed-further-upgrades-to-my-misc-package
date: 2014-06-24
categories:
- disentangle
tags:
- software
---t

- I've been enjoying summarising datasets with my data\_dictionary function
- There was a bug when a date variable had any missings.  
- I have modified the function to cope with these so have released version 1.2
- [Windows Version is Downloadable Here](http://ivanhanigan.github.io/disentangle/lib/disentangle_1.2.zip)
- Linux and Mac users can just run this R code

#### R Code:
    require(devtools)
    install_github("disentangle", "ivanhanigan")
