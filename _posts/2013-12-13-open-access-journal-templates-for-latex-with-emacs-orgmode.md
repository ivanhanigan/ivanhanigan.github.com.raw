---
name: 2013-12-13-open-access-journal-templates-for-latex-with-emacs-orgmode
layout: post
title: open-access-journal-templates-for-latex-with-emacs-orgmode
date: 2013-12-13
categories:
- research methods
---

- I appreciate all the arguments for using OA journals
- Using a LaTeX template is also attractive
- This post is a record of some experiences with the BioMedCentral (BMC) template and the Public Library of Science (PLOS) templates
- implemented with my favourite editor for everything Emacs Orgmode.

#### BMC seemed like a good option

- I started this journey 6 months ago with the BMC template
- because I pitch my work mostly at the health science community BMC seemed logical
- It turns out I downloaded their old LaTeX template and it SUCKED
- If you Download [the template and bibliography stuff](http://www.biomedcentral.com/authors/tex) now it looks better
- But I am suspicious now because of the last little while I've been struggling so I've got a skeptical approach
- First copy the stuff to a test dir
- then use TexWorks to test compiling it
- try deleting the provided BBL file, this reveales that the BIB file has to be compiled with bibtex to work
- orgmode produces BBL files when evaluated but I don't know if it'll be smooth with the template

#### PLOS seems like a smoother option

- Download from [the LaTeX template site](http://www.plosone.org/static/latexGuidelines)
- First thing I notice is there is no BIB file, Yay!
- just make sure  bibliographystyle and bibliography are set
- Looks like it isn't trying so hard
