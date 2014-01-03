---
name: 2013-12-16-links-to-useful-data-munging-posts
layout: post
title: links-to-useful-data-munging-posts
date: 2013-12-16
categories:
- research methods
- Data Documentation
---

Here are a few links to some recent data munging tips I picked up last week:

#### Database Relationships

1. [This is a a very quick way to look at the relationships in a database](http://pirategrunt.com/2013/12/13/24-days-of-r-day-13/)

#### MS Access field (column) descriptions:

- I'm looking for methods to access the metadata related to the columns.
- In general MS Access seems to hide these:
- http://blogannath.blogspot.com.au/2010/03/microsoft-access-tips-tricks-list-table.html
- "Field descriptions can be entered by the user when creating the table in design view. It is a highly encouraged practice since the description can provided valuable documentation about the purpose of each field in a table. The inability to extract the field descriptions as part of the table documentation using Access's built-in documenter is therefore quite inconvenient."
- I can see there is [a C# method, but I'd need visual studio or someone to compile this I suppose?](http://stackoverflow.com/questions/7041824/retrieve-msaccess-database-column-description)
- My mate Francis said: "you'll have to use a script that uses the Microsoft OLE-DB, as in the stackoverflow answers. However, you don't need Visual Studio or C# to do this, just any language that can interface with Windows COM objects. Python can do this, so this might be your excuse to finally learn it. I imagine there might even by a R library out there somewhere, although it would probably be more convenient to go the python route here."
- To get started with COM and python, you [could do worse than to start with](http://timgolden.me.uk/pywin32-docs/html/com/win32com/HTML/QuickStartClientCom.html)

#### Data manipulation

1. [This guy has created some custom functions that look helpful](http://christophergandrud.blogspot.com.au/2013/12/three-quick-and-simple-data-cleaning.html)
1. [Revolutions Blog links to several Data Wrangling resources](http://blog.revolutionanalytics.com/2013/12/tutorial-basic-data-processing-with-r.html)

#### Code editor / IDE

1. [Updates to Rstudio server are always worth checking out](http://www.r-bloggers.com/new-version-of-rstudio-v0-98/)
