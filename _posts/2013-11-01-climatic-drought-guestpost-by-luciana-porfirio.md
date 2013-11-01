---
name: climatic-drought-guestpost-by-luciana-porfirio
layout: post
title: climatic-drought-guestpost-by-luciana-porfirio
date: 2013-11-01
categories:
- climatic and agricultural drought
---

### Guest post by Luciana Porfirio with code contributions by Francis Markham

- Recently I encountered a student doing an analysis who was doing everything in excel, and I couldn't contain my mouth and say R would be better... but it isn't a simple task. So any here are some tips.
- There is a table with 62 years * 12 months of rain data in mm. We calculated the cumulative distribution using ecdf: empirical cumulative distribution function. So the table looks like this: Year Jan Feb Mach (...) each cell contains the cum dist.
- We also got the number of months per year with less than X mm of rain. But he needs to know how many months  are between the drought months, regardless the year. So, I thought that converting the data into a ts was going to facilitate the task, but it doesn't, because now I don't' have columns and rows any longer.
- But I struggled to handle a ts object to do for example an ifelse.
- Luckily there are many many tricks about R, and with the code below we solved all his problems (and many months of work in excel).
- [Get the example data here](/data/raj_rain_data.csv)
- This is how it looks like:

#### R Code:
     
    ###############################################
    ###############################################
    #read csv file with rain BoM data
    dat = read.csv('raj_rain_data.csv')
     
    fn <- apply(dat[,2:13], 2, ecdf) # equivalent to Excel's percentrank function, only for cols 2 to 13 but you need to apply the function to each month
     
    #this fun does all the months at once
    fn2 = data.frame(t(do.call("rbind", sapply(1:12, FUN = function(i) fn[[i]](dat[,i+1]), simplify = FALSE))))
    colnames(fn2) = colnames(dat[,2:13])
    fn2$year = dat$Year
     
    #if the value is lower than 0.4, retrieves a 1, otherwise 0 fn2$drought = rowSums(ifelse(apply(fn2[,1:12], 2, FUN= function (x) x < 0.4)==TRUE, 1,0))
     
    #if the value is lower than 0.1, retrieves a 1, otherwise 0 fn2$extreme = rowSums(ifelse(apply(fn2[,1:12], 2, FUN= function (x) x < 0.1)==TRUE, 1,0))
     
    str(fn2)
    names(fn2)
     
    #ts didn't work - Francis suggested to melt the data.frame # Melt fn2 to tall data set fn2.tall <- melt(fn2, id.vars="year")
     
    # Get the year-month into date format
    fn2.tall$date <- with(fn2.tall,
                                 as.Date(paste("1", variable, year), "%d %b %Y"))
     
    # Convert dates into months since 0 BC/AD (arbitrary, but doesn't matter) #I'm not using the month.idx with Ivan's solution (remove) fn2.tall$mnth.idx <- sapply(fn2.tall$date, function(x){
      12*as.integer(format(x, "%Y")) + (as.integer(format(x, "%m")) - 1)
    })
     
    # Sort by date
    fn2.tall <- fn2.tall[order(fn2.tall$date),]
     
     
    #Ivan's solution
     
    x<-fn2.tall$value<0.4
    xx <- (cumsum(!x) + 1) * x
    x2<-(seq_along(x) - match(xx, xx) + 1) * x
    fn2.tall$count<-x2
     
    #counts the number of cases of drought
    as.data.frame(table(fn2.tall$count))
    ###############################################
    ###############################################
