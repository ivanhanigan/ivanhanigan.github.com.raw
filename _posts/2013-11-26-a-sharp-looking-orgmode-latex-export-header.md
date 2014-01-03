---
name: 2013-11-26-a-sharp-looking-orgmode-latex-export-header
layout: post
title: a-sharp-looking-orgmode-latex-export-header
date: 2013-11-26
categories:
- research methods
---

- I got this header for a nice looking report from Bull, G. (2011). Example Sweave Document. SharpStatistics.co.uk.
- This has a bunch of useful parameters, but I just really like the header and footer on pages 2 onward
- The original was a Sweave file.  I really like Sweave but orgmode allows other languages as well as R to be inter-woven into the script
- An alternative to Sweave is knitr and is still on my todo list, but this works well at the moment
- I also like how you can quickly change this to a Beamer presentation style.
- Once this is in your file use C-c C-e d to export and compile the PDF
- This example is available at [this link](/pdfs/SharpReportTemplate.pdf)

#### Emacs orgmode Code: Put this into your .org file
    #+TITLE: Sharp Report Template
    #+AUTHOR: Ivan Hanigan
    #+email: ivan.hanigan@anu.edu.au
    #+LaTeX_CLASS: article
    #+LaTeX_CLASS_OPTIONS: [a4paper]
    #+LaTeX_HEADER: \usepackage{amssymb,amsmath}
    #+LaTeX_HEADER: \usepackage{fancyhdr} %For headers and footers
    #+LaTeX_HEADER: \pagestyle{fancy} %For headers and footers
    #+LaTeX_HEADER: \usepackage{lastpage} %For getting page x of y
    #+LaTeX_HEADER: \usepackage{float} %Allows the figures to be positioned and formatted nicely
    #+LaTeX_HEADER: \floatstyle{boxed} %using this
    #+LaTeX_HEADER: \restylefloat{figure} %and this command
    #+LaTeX_HEADER: \usepackage{url} %Formatting of yrls
    #+LaTeX_HEADER: \lhead{ivanhanigan.github.com}
    #+LaTeX_HEADER: \chead{}
    #+LaTeX_HEADER: \rhead{\today}
    #+LaTeX_HEADER: \lfoot{Draft}
    #+LaTeX_HEADER: \cfoot{}
    #+LaTeX_HEADER: \rfoot{\thepage\ of \pageref{LastPage}}
    #+LATEX: \tableofcontents
    
    * Introduction
    This is a sharp looking report template I got from an R blogger \cite{Bull2011}.
    
    The pages after the first page have a nice looking header, footer and page number.
    \clearpage
    
    * Section 1
    In the Org file you can see some hidden R code that computes a linear regression and returns the results shown in Table \ref{ATable}.
    \input{ATable.tex}
    \clearpage
    *** COMMENT some-code
    #+name:some-code
    #+begin_src R :session *R* :tangle no :exports none :eval yes
    #### name:some-code ####
    x<-rnorm(100,10,5)
    y<-rnorm(100,20,15)
    fit <- lm(y~x)
    library(xtable)
    sink("ATable.tex")
    xtable(fit, caption="Example Table",digits=4,table.placement="H",label="ATable")
    sink()
    #+end_src
    
    #+RESULTS: some-code
    
    
    
    * References
    \bibliographystyle{apalike}
    \bibliography{/home/ivan_hanigan/references/library}
