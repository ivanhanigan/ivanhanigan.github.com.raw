---
name: dc-uploader-and-ANU-DataCommons
layout: post
title: dc-uploader-and-ANU-DataCommons
date: 2013-10-13
categories:
- Data Documentation
---

In this post I use the tool produced at the ANU by the DataCommons team.  This requires Python3.

# What does it do?
The script only creates new collection records. The functionality to edit records didn’t make it into the script as the expectation is that automated ingests will only require creation of new datasets to which files will be uploaded. 

Users can feel free to tweak the collection parameter file to their liking in the development environment until happy with the results.

# Create the metadata.txt

You need to get the python scripts and conf file from the ANU DataCommons team.  Store these somewhere handy and move to that directory.

change the anudc.conf: to test out the scripts by creating some sample records, please uncomment the “host” field in the file that points to dc7-dev2.anu.edu.au:8443 , and comment out the one that points to datacommons.anu.edu.au:8443.

Also you get a different token in dev and prod servers for security reasons you cannot use the same token. Also, storing your username and password in plain text is not recommended and is to be used only for debugging purposes. Also, in my case I had to change the owner group to ‘5’ when creating records in dev. In prod, it’s 6.

You can look int the "Keys.txt" file that contains the full list of values that can be specified in this metadata.txt file.     

#### Code:
    setwd("~/tools/dcupload")
    sink("metadata.txt")
    cat("
    # This file, referred to as a collection parameter file, consists of
    # data in key=value pairs. This data is sent to the ANU Data Commons
    # to create a collection, establish relations with other records,
    # and/or upload files to those collections.
     
    # The metadata section consists of metadata for use in creation (not
    # for modification) of record metadata in ANU Data Commons. The
    # following fields are required for the creation of a record. The file
    # Keys.txt contains the full list of values that can be specified in
    # this file. Based on this information below, a collection record of
    # type databaset with the title "Test Collection 6/05/2013" will be
    # created owned by Meteorology and Health group.
    [metadata]
    type = Collection
    subType = dataset
    ownerGroup = 5
    # 6 on production, 5 on dev
    name = Civil Status, Gender and Activity Sector
    briefDesc = An example, fictional dataset for Decision Tree Models
    citationCreator = Ritschard, G. (2006). Computing and using the deviance with classification trees. In Compstat 2006 - Proceedings in Computational Statistics 17th Symposium Held in Rome, Italy, 2006.
    email = ivan.hanigan@anu.edu.au
    anzforSubject = 1601
     
    # The relations section allows you to specify the relation this record
    # has with other records in the system.  Currently relations with NLA
    # identifiers is not supported.
    [relations]
    isOutputOf = anudc:123
     
    # This section contains a line of the form 'pid = anudc:123' once a
    # record has been created so executing the uploader script with the
    # same collection parameter file doesnt create a new record with the
    # same metadata.
    [pid]
    ")
    sink()

    # run the dcload
    system("python3 dcuploader.py -c metadata.txt")

<p></p>
# What happened?

- Looking in the metadata.txt file it now has a pid like "pid = test:3527"        
- And we have created a new record in our account on the DataCommons server.

    
# go to the website
Now go to [the dev site](https://dc7-dev2.anu.edu.au:8443/DataCommons/) and you can continue editing the record manually in the browser.
    
Or if we have ironed out the wrinkles you could go straight to the production server at [This Link](https://datacommons.anu.edu.au:8443/DataCommons)


# Uploading the data
The dataset gets sent using a Java applet in the browser while you are manually editing the record using the browser.

# Notes

- After the records get created, the script tries to relate the record to other records as you’ve specified in the collection parameter file in the relations section. If you’re creating a record in dev2, you cannot relate it to a record in production because that record doesn’t exist in dev2. Remember that IDs for records in dev environments have the prefix “test:” while those in production have “anudc:”.
 
- Also, when you ran the script against production the created records were linked with the record with the ID anudc:123. I have now removed those relations. You might want to change that value in your metadata.txt file so the links are established to records that created records actually can be related to. Or for testing purposes, simply delete the entire [relations] section.
