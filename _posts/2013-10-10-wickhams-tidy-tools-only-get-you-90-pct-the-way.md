---
name: 2013-10-10-wickhams-tidy-tools-only-get-you-90-pct-the-way
layout: post
title: wickhams-tidy-tools-only-get-you-90-pct-the-way
date: 2013-10-10
categories:
- research methods
---

#### Hadley Wickham's tidy tools
In this video at 8 mins 50 seconds he says "these four tools do 90% of the job" 

- subset, 
- transform, 
- summarise, and 
- arrange
- TODO I noticed [at the website for an Rstudio  course](http://www.rstudio.com/training/curriculum/data-manipulation.html) transform has been replaced by mutate as one of the "four basic verbs of data manipulation".

<iframe src="//player.vimeo.com/video/33727555" width="500" height="281" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen></iframe> <p><a href="http://vimeo.com/33727555">Tidy Data</a> from <a href="http://vimeo.com/user2150538">Drew Conway</a> on <a href="https://vimeo.com">Vimeo</a>.</p>

So I thought what's the other 10?  Here's a few contenders for my work:

- merge
- reshape::cast and reshape::melt
- unlist
- t() transpose
- sprintf or paste

<p></p>
#### R-subset
    # Filter rows by criteria
    subset(airquality, Temp > 90, select = c(Ozone, Temp))

    ## NB This is a convenience function intended for use interactively.  For
    ## programming it is better to use the standard subsetting functions like
    ## ‘[’, and in particular the non-standard evaluation of argument
    ## ‘subset’ can have unanticipated consequences.

    with(airquality,
         airquality[Temp > 90, c("Ozone", "Temp")]
         )

    # OR

    airquality[airquality$Temp > 90,  c("Ozone", "Temp")]
#### R-transform
    # New columns that are functions of other columns       
    df <- transform(airquality,
                    new = -Ozone,
                    Temp2 = (Temp-32)/1.8
                    )
    head(df)
#### R-mutate
    require(plyr)
    # same thing as transform
    df <- mutate(airquality, new = -Ozone, Temp = (Temp - 32) / 1.8)    
    # Things transform can't do
    df <- mutate(airquality, Temp = (Temp - 32) / 1.8, OzT = Ozone / Temp)
    
    # mutate is rather faster than transform
    system.time(transform(baseball, avg_ab = ab / g))
    system.time(mutate(baseball, avg_ab = ab / g))
#### R-summarise
    # New data.frame where columns are functions of existing columns
    require(plyr)    
    df <- ddply(.data = airquality,
                .variables = "Month",
                .fun = summarise,
                tmax = max(Temp),
                tav = mean(Temp),
                ndays = length(unique(Day))
                )
    head(df)
#### R-arrange
    # Re-order the rows of a data.frame
    df <- arrange(airquality, Temp, Ozone)
    head(df)
