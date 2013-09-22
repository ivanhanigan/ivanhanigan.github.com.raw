---
name: using-orgmode-and-jekyll-for-open-notebook
layout: post
title: using-orgmode-and-jekyll-for-open-notebook
date: 2013-09-22
categories:
- orgmode
---

# Using Orgmode and Jekyll for Open Notebook
Orgmode is a great notebook tool because it allows the coding, evaluation and documentation all in one.  I also want to use it to send the documentation to my blog as an Open Notebook.

If starting again I'd look into this:
- http://orgmode.org/worg/org-tutorials/org-jekyll.html

But as it is I already put a lot of work into configuring a jekyll blog I cloned from Scott Chamberlain over at ROpenSci and I will just use orgmode to publish the posts related to each project, tagged as 'categories'.

But here is a problem I just found out how to solve.  For a long time I thought that because github disabled ruby plugins that the automatic generate categories index pages was broken.  Luckily Charlie Park has written up the following solution and this seems to have worked for me today:    
- http://charliepark.org/tags-in-jekyll/
- http://charliepark.org/jekyll-with-plugins/

Cheers!
