---
name: 2013-11-25-setting-up-a-workflow-with-code-chunks
layout: post
title: Setting Up A Workflow Script With Code Chunks
date: 2013-11-25
categories:
- research methods
---

This post describes some ideas and techniques I use to set up a "workflow script".  I use this term to refer to the structured combination of code, data and narrative that make an executable Reproducible Research Report (RRR).

A lot of these ideas are inpsired by  a great paper by Kieran Healy called  "Choosing Your Workflow Applications" available at [https://github.com/kjhealy/workflow-paper](https://github.com/kjhealy/workflow-paper) to accompany [his Emacs Starter Kit](http://kieranhealyo.org/resources/emacs-starter-kit.html). My shortened version of his main points are:

- 1 use a good code editor
- 2 analyse data with scripts
- 3 store your work simply and document it properly
- 4 use a version control system
- 5 Automate back ups 
- 6 Avoid distracting gadgets

#### Here's my current approach in each of these categories
- 1 use Emacs with Orgmode (and kjhealy's drop-in set of useful defaults)
- 2 Scripts that utilise the literate programming technique of mixing Code Chunks in with descriptive prose
- 3 John Myles White's ProjectTemplate R Package and Josh Riech's LCFD paradigm 
- 4 git and GitHub for version control

5 Automated Backups and 6 Avoiding Gadgets are still somethings I find challenging

#### 1 Use a good code editor
I like using Emacs with Orgmode.

- I have previously tried a variety of code editors from Tinn-r, NppToR, Rstudio and Eclipse.  
- Emacs with Orgmode suits me the most because it has a great number of features especially the linkage with LaTeX or HTML export
- A key reference to look at for reasons why Emacs is so good for scientific work is Eric Schulte et al ["A Multi-Language Computing Environment for Literate Programming"](www.jstatsoft.org/v46/i03‎) 
- Here is a [link to a great orgmode description](http://doc.norang.ca/org-mode.html)
- (this guy spends a lot of time on tweaking his set up)

#### 2 Analyse data with Scripts (stitch together code chunks)
I use Scripts but prefer to think of them as stitched together Code Chunks with prose into Compendia.

- Compendia are documents that weave together Code and Prose into an executable report
- The underlying philosophy is called Reproducible Research Reports
- A very useful tool is a keyboard shortcut to quickly create a chunk for code
- so you can be writing parts of the report like this: "Blah Blah Blah as shown in Figure X and Table Y"
- then just hit the correct keys and WHAMM-O there is a new chunk ready for the code that creates Figure X and Table Y to be written.
- Here is how I use Emacs to achieve this (the other editors I mentioned above also have the abiltiy to do this too).  The IPython Notebook does this stuff too but calls chunks "cells" for some reason.

#### Emacs Code: Put this into the ~/.emacs.d/init.el file
    (define-skeleton chunk-skeleton
      "Info for a code chunk."
      "Title: "
      "*** " str "-code\n"
      "#+name:" str "\n"
      "#+begin_src R :session *R* :tangle src/" str ".r :exports reports :eval no\n"
      "#### name:" str " ####\n"
      "\n"
      "#+end_src\n"
    )
    (global-set-key [?\C-x ?\C-\\] 'chunk-skeleton)

#### Using the Emacs Shortcut
- now whenever you type Control-x control-\ a new code chunk will appear
- you'll be typing "blah blah blah" and think I need a figure or table, just hit it.
- move into the empty section and add some code
- you can hit C-c ' to enter a org-babel code execution session that will be able to send these line by line to an R session
- or within the main org buffer if your eval flag is set to yes then you can run the entire chunk (and return tabular output to the doc) using C-c C-c
- To export the code chunks and create the modular code scripts without the narrative prose use C-c C-v t
- this is called "tangling" and the chunks will be written out to the file specified in the chunk header ":tangle" flag

#### Compiling the resulting Compendium
- Emacs uses LaTeX or HTML to produce the Report
- I find both of these outputs very pleasing
- to compile to TEX use C-c C-e d
- for HTML use C-c C-e h (FOR CODE HIGHLIGHTING INSTALL htmlize.el)
- these commands will also evaluate all the chunks where ":eval" = yes to load the data and calculate the results fresh. 
- AWESOME!
    
#### 3 Store your work simply and document it properly
- I use the [ProjectTemplate R package](http://www.johnmyleswhite.com/notebook/2010/08/26/projecttemplate/) to organise my code sections into modules
- These modules are organised into the Reichian LCFD paradigm described first [on StackOverflow here](http://stackoverflow.com/a/1434424), and encoded into [the makeProject R package](http://cran.r-project.org/web/packages/makeProject/makeProject.pdf)
- documentation is within the main orgmode script
- data documentation is a whole other universe that I will deal with in a separate post

#### 4 use a version control system using git and github
    # once you have the project via R
    R
    require(ProjectTemplate)
    create.project("AwesomeProject", minimal = T)
    q()
    # use the shell to start a git repo
    cd AwesomeProject
    git init
    # and commit the TODO
    git add TODO
    git commit -m "first commit"
    # tada!

- Emacs can now be used to manage the git repo using the C-x g command
- Rstudio has a really nice GUI for doing this inside it;s Project management interface too.

#### Using Github or another Git Server
- You can easily set up a Github repo for this now but it will be public
- Alternatative is to set up your own private Git server.  I followed [these instructions to Running a Simple Git Server Using SSH](http://blog.goosoftware.co.uk/2012/02/07/quick-git-server/)
- Either way once you have set up your remote git repo you need to set the remote tracking

#### Git Code:
    cd /path/to/local/git/repo
    git remote add origin git@github-or-other-server:myname/myproject.git
    git push origin master

#### 5 Automate back ups AND 6 Avoid distracting gadgets
- OMG backups stress me out
- ideally I would follow [this advice because "when it comes to losing your data the universe tends toward maximum irony. Don't push it."](http://www.jwz.org/blog/2007/09/psa-backups/)
- But I don;t fully comply
- Instead I generally use Dropbox for  basic project management admin stuff
- I use github for code projects I am happy to share, I also pay for 10 private repos 
- I Set up a git server at my workplace for extra projects but this is on a test server that is not backed up, and I am not really happy about this
- In terms of Distracting Gadgets, I think that with the current tempo of new innovations related to new software tools for this type of work I should keep trying new things but I have pretty much settled into a comfortable zone with the gadgets I described here. 

#### Conclusions
- This is how I've worked for a couple of years
- I find it very enjoyable, mostly productive but prone to the distractions of "distractions by gadgets"
- The main thing I want to point out is the usage of Code Chunks in RRR scripts.
- These things are awesome.
