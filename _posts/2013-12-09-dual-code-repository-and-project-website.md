---
name: 2013-12-09-dual-code-repository-and-project-website
layout: post
title: dual-code-repository-and-project-website
date: 2013-12-09
categories:
- research methods
---

- I really like the idea of using github or bitbucket for a dual code repository and project website
- in Github I set up the master branch with the R package code
- and set up the website using the gh-pages branch 
- it has to be called gh-pages, and add an index.html, it will appear at your-username.github.com/repo-name

#### Github

- The best bit about doing this on github is that the R package "devtools" can be used to install the package (so long as you can compile the package)
- on windows you may need to install Rtools and configure the path

#### R Code: install_github
    require(devtools)
    install_github("repo-name", "github-account-name")

#### Bitbucket

- I recently took these notes about setting up a website on Bitbucket
- I am not sure about how this would work for R packages (the devtools installer mentioned above is a great tool for developing)
- but with unlimited private repositories this seems like a good platform for my "open notebook - selected content" (I need to be selective about what I share and what I keep restricted access only)  
- the page is available for "your-account".bitbucket.org
- create a new repo on the web UI 
- I kept the repo private, but the pages will be public,
- added issue tracking and Wiki

#### using git shell
    mkdir ~/projects/your-account.bitbucket.org
    cd ~/projects/your-account.bitbucket.org
    git init
    git remote add origin ssh://git@bitbucket.org/your-account/your-account.bitbucket.org.git
    touch index.org
    # use emacs to make changes and publish the html (C-c C-e h)
     
    git commit -m "First commit"
    git push -u origin master

- now it is online at http://your-account.bitbucket.org/

- More info at:
[https://confluence.atlassian.com/display/BITBUCKET/Publishing+a+Website+on+Bitbucket](https://confluence.atlassian.com/display/BITBUCKET/Publishing+a+Website+on+Bitbucket)
