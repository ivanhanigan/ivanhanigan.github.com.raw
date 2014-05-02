---
name: 2014-02-27-yearmon-class-and-interoperability-with-excel-and-access
layout: post
title: yearmon-class-and-interoperability-with-excel-and-access
date: 2014-02-27
categories:
- research methods
- Data Documentation
---


#### Toward a standard and unambiguous format for sharing Year-Month data
  
- I am working in a new job where we are recieving data from a lot of different groups
- we aim to review these datasets and then publish them for a wide audience of potential users
- therefore usability and interoperability is a key concern
- we recieved some data with Month and Year as Apr.12
- I know this is easy to convert to a date/time class with in R but wondered what a better format would be to recommend for our datasets to use to maximise utility downstream (especially for non R users)
- Apr.12 is assumed to be text in excel so need something else
- Apr-12 is assumed to be the twelfth of April this year (ie 12/4/2014)

#### In R the solution might be to use the zoo package
    require(zoo)
    as.yearmon("Apr.12", "%b.%y")
    # [1] "Apr 2012"

    # other options abound
    as.yearmon("apr12", "%b%y")

    # the default is YYYY-MM or similar
    as.yearmon("2012-04")
    as.yearmon("2012-4")

<p></p>

- So I went looking at how Excel and Access deal with this
- found that the best appeard to be MMM-YYYY in terms of how these software assume the data should look

#### R Code:
    as.yearmon("Apr-2012", "%b-%Y")

    # but will need to specify format because otherwise fails
    as.yearmon("Apr-2012")
    # NA

<p></p>

#### Conclusion

- I recommend the MMM-YYYY option
- it is pretty good that in Excel it is assumed 1/04/2012 
- and if MS access is set to date/time and format = mmm-yyyy is ok for data entry (but not importing)
- to import this use a shorttext type, then post-import, change to date/time with mmm-yyyy (the . failed)
