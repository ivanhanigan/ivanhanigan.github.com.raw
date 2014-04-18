---
name: gantting-like-a-hacker
layout: post
title: gantting-like-a-hacker
date: 2014-02-22
categories:
- research methods
---

### Background
- ["Blogging like a Hacker"](http://tom.preston-werner.com/2008/11/17/blogging-like-a-hacker.html) has become a paradigm for programmers who want to link their code to their blogs.
- I've followed this paradigm for a while to support my scientific projects, enhancing their transparency and reproducibility.
- I've started a new project where I need to also manage project management and planning (following [Tomas Aragon's tutorial](http://medepi.com/2012/02/05/project-mgmt/))
- I propose that the same methods I use in scientific programming and blogging like a hacker can be used in "Gantting like a Hacker"  
- The title for this post is also influenced by the poste over at [Geek | Manager](http://blog.geekmanager.co.uk/2007/05/02/using-the-best-plan-format/).
- That post says taht "Premature Gannting" is the act of making a "huge Gantt chart (often in MS Project)."
- Gannting like a Hacker is doing this in a scripted environment, without relying on closed-source proprietry software such as the Windoze options.  
- The community of bloggers (mostly geeks) who are following a style of blogging that originated with the invention of Jekyll, [unveiled in this post by Tom Preston-Werner](http://tom.preston-werner.com/2008/11/17/blogging-like-a-hacker.html); GitHub’s co-founder (aka mojombo).
- This experiment uses Taskjuggler and Emacs Orgmode

### Materials and Methods

- Use Ubuntu 12.04 Long Term Support (LTS)
- with Ruby 

#### Code:install task juggler
    gem install taskjuggler

<p></p>

### Gantt charts with Emacs Orgmode

- I'm using an Emacs tool to use TaskJuggler to handle the task scheduling and creation of Gantt chart suitable for [a Pointy-haired Boss](http://orgmode.org/worg/org-tutorials/org-taskjuggler.html). 
- I hated using the Orgmode script to compile the parts of the Gantt chart so I wrote [this R script](https://raw.github.com/ivanhanigan/disentangle/gh-pages/gantt-tj3/gantt-tj3-build.R) to convert a spreadsheet into an Orgmode script
- the spreadsheet is organised in a fairly simple way shown below.

![alttext](/images/gantt-chart-sheet.png)

### Results
- and executing my script will convert this into a Emacs orgmode file that will export to a taskjuggler file (use C-c C-e j) and viola!

![alttext](/images/gantt-chart.png)

### Conclusions

- This simplifies the Orgmode taskjuggler creation
- A drawback is that it has to go through the Emacs export function.
