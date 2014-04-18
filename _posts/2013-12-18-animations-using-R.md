---
name: 2013-12-18-animations-using-R
layout: post
title: animations-using-R
date: 2013-12-18
categories:
- research methods
---

- following on from my previous posts about [animated maps](http://ivanhanigan.github.io/2013/07/animated-maps/), [spatio-temporal animations](http://ivanhanigan.github.io/2013/06/spatio-temporal-animations/) and animations [with buttons for go, stop and reverse](http://ivanhanigan.github.io/button/index.html)
- Here is a quick note about how to do a simple animation with R to create a movie file (GIF)
- To create this movie

![animation.gif](/animation/animation.gif)


#### Code:animations-using-R
    if(!require(animation)) install.packages("animation");
    require(animation)
    saveGIF(
    {
    ani.options(nmax = 100, interval = 0.5)
    par(mar = c(3, 2.5, 0.5, 0.2), pch = 20, mgp = c(1.5, 0.5,0))
    buffon.needle(mat = matrix(c(1, 2, 1, 3), 2))
    },
    outdir = getwd()
    )
