---
name: two-main-types-of-data-documentation-workflow
layout: post
title: two-main-types-of-data-documentation-workflow
date: 2013-10-11
categories:
- Data Documentation
---

This post introduces a new series of blog posts in which I want to experiment with a few tools for data documentation, which I'll present as Case Studies.  This series of posts will be pitched to an audience mixture of data librarians and data analysts.
  
Data documentation occurs in a spectrum from simple notes through to elaborate systems.  I've been working on a conceptual framework about how the actual process can be done in two distinct ways:

- Graphical User Interface (GUI) solutions
- Programmatic (Scripted/Automagic) solutions
 
I think the GUI tools are in general pretty user friendly and useful
for simple projects with only a small number of datasets, but have a
major drawback for the challenge of heterogeneous data integration.  I
think the problem is expressed nicely [In This Post By Carl Boettiger](http://carlboettiger.info/2013/06/23/notes-on-leveraging-the-ecological-markup-language.html)  in reference to Morpho:

- "looks like a rather useful if tedious tool for generating EML
files. Unfortunately, without the ability to script inputs or
automatically detect existing data structures, we are forced through
the rather arduous process of adding all metadata annotation each
time...."
- "...A package could also provide utilities to generate EML from R objects, leveraging the metadata implicit in R objects that is not present in a CSV (in which there is no built-in notion of whether  a column is numeric or character string, what missing value characters it uses, or really if it is consistent at all. Avoiding manual specification of these things makes the metadata annotation less tedious as well."
  
# Centralised Repository, Distributed Users
A key aspect of current approaches is the existence of a centralised data management system.  All the examples I consider include at least a metadata catalogue and some also include a data repository.  An additional feature sometimes exists for managing users permissions.

The relationship between users and centralised services is a really complicated space, but essentially consists of the ability for users to create the documentation and push it (perhaps along with the data) to the metadata catalogue  and/or repository.  So given these assumptions I propose the following types of arrangement:

- user sends metadata to metadata catalogue
- user sends metadata and data to metadata catalogue and data repository 
- user sends metadata and data and permissions information to metadata catalogue and data repository and permissions system.
  
The Case Studies I've identified that I want to explore are listed below, names follow the format 'client tool'-and-'data repository or metadata catalogue'-and-optionally-'permissions system':

#### Programmatic solutions
- reml-and-rfigshare
- reml-and-knb (when/if this becomes available)
- make_ddixml-and-ddiindex-and-orapus
- r2ddi-ddiindex
- dc-uploader-and-ANU-DataCommons
- dc-uploader-and-RDA

#### Graphical User Interface solutions
- morpho-and-knb-metacat
- nesstar-publisher-and-nesstar-and-whatever-Steve-calls-the-ADA-permissions-system
- xmet-and-Australian-Spatial-Data-Directory
- sdmx-editor-and-sdmx-registry
