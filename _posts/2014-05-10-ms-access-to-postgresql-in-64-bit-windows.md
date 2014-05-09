---
name: ms-access-to-postgresql-in-64-bit-windows
layout: post
title: ms-access-to-postgresql-in-64-bit-windows
date: 2014-05-10
categories:
- research methods
---

- In 2011 we published a paper on "Creating an integrated historical record of extreme particulate air pollution events in australian cities from 1994 to 2007".
- I used a PostGIS/PostgreSQL server to host the database and MS Access clients for data entry by my co-author's at their own institutions (thousands of kms away) 
- This worked great but recently I realised that updating to windows 64 bit has broken the ODBC connection
- to fix it I followed the instructions [here](http://www.youlikeprogramming.com/2011/09/postgresql-and-odbc-in-64-bit-windows/)
