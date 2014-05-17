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
- You need to install both the 32 and 64 bit executables
- Assuming you use the 32 bit windows office suite (recommended) then use the command below to open the ODBC connections tool and add a DSN for your postgres database

#### Code:
    Go to Start -> Run (or Press Windows+R keys) and enter 
    %WINDIR%\SysWOW64\odbcad32.exe
    
<p></p>

- On either the User DSN (DSNs available for only that user) or System DSN (DSNs available to every user) tab, click the Add button.
Scroll down the list and find the PostgreSQL ODBC Driver. 
- You may select ANSI or UNICODE (For future support I personally prefer UNICODE), and click Finish.
- Data Source refers to the programmable name of the DSN Entry. Stick to lower-case letters and underscores. Ex: psql_server
- Specify the Database, Server, User Name and Password to your PostgreSQL server.
- Click the Test button to ensure everything has been specified correctly.
- Click the Save button to create the DSN.
