---
name: 2014-06-15-my-feed-filesize-is-larger-than-512k-need-to-reduce-its-size-in-order-for-feedburner-to-process-it
layout: post
title: my-feed-filesize-is-larger-than-512k-need-to-reduce-its-size-in-order-for-feedburner-to-process-it
date: 2014-06-15
categories:
- Data Documentation
---

- I am not sure but I suspect [this post](http://ivanhanigan.github.com/2014/05/using-additional-header-rows-for-metadata.html) caused my feedburner xml to become too big and stop the updates to my feedly account
- Found this out by logging in to [http://feedburner.google.com](http://feedburner.google.com) and trying to re-sync my feed (under troubleshootize)
- I may have tipped the size over the edge with [this post](http://ivanhanigan.github.com/2014/06/testing-aekos-data-portal.html) 
- the issue is probably due to me starting to use knitr (see [this post](/2014/05/reproducible-research-reports-using-emacs-orgmode-export-to-knitr/) ) to produce the HTML reports which encodes the images inline, whereas I used to use the old school orgmode approach of referencing the png in the images directory
- looking at the feed/index.xml I saw that this includes every post I ever wrote
- I fixed it by going back to [the instructions I used to set up the feed](http://www.daveperrett.com/articles/2010/09/14/integrating-jekyll-with-feedburner/)
- and adding limit:10 to the line of the loop 'for post in site.posts'
