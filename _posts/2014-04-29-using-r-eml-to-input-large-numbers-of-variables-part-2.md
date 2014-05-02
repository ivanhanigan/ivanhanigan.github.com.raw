---
name: using-r-eml-to-input-large-numbers-of-variables-part-2
layout: post
title: using-r-eml-to-input-large-numbers-of-variables-part-2
date: 2014-04-29
categories:
- Data Documentation
tags: 
- morpho
- R-eml
---

In my [previous post](/2014/04/using-reml-to-input-large-number-of-column-descriptions) I showed a workaround to input large number of variabels than Morpho could handle.  I have found out an interesting thing about the R EML package data.set approach.  The unit.defs depends on the type of the column in the data frame (R knows if you try to trick it).  Rather than describe all the levels of the factor vars, I wanted to just have simple descriptions for numeric or character type columns.  If numeric it should be number and if character it can be the name of the column.  Because I am just trying to sidestep the issue with morpho failing to input the 200 plus variables I just need to create a dataframe with either number or character (not factor).

For an example:

#### R Code:
    require(EML)
    fname <- dir("myData", full.names=T, pattern = 'csv')
    fname
    fname  <- "myData/paper_data.csv"  
    dat  <- read.csv(fname, stringsAsFactor=F)
    # the variable names include special characters such as % and [ so need to do some extra work
    names_dat  <- read.csv(fname, nrow=1, header=F, stringsAsFactor=F)
    names(dat) <- names_dat
    head(dat)
    nrow(dat)
    # the first 46 variables are nominal, thereafter they are all numeric
    str(dat[,1:46])
    str(dat[,47:49])
    # but these numerics are character for some reason
    table(dat[ , 47])
    # it is because the raw data had * instead of NA...  I could use na.strings when I call read.table above, or deal with it here
    # I'll just convert them to numerics now
    dat1 <- dat[,1:46]
    dat2 <- dat[,47:ncol(dat)]
    dat2[dat2 == "*"] <- NA
    for(i in 1:ncol(dat2)){
      dat2[,i]  <- as.numeric(dat2[ , i])
    }
    str(dat2)
    # good that has set them up properly, also make sure all the text are character type
    for(i in 1:ncol(dat1)){
      dat1[,i]  <- as.character(dat1[ , i])
    }
    # recombine
    dat <- cbind(dat1,dat2)
    str(dat)
    # then I add to it the definition for the constructed variables
    unit_defs <- list()
    for(i in 1:46){
        unit_defs[[i]] <- names(dat[i])
    }
    for(i in 47:ncol(dat)){
        unit_defs[[i]] <- "number"
    }
    unit_defs[1:20]
    col_defs <- names(dat)
    col_defs
    #names(dat)
    dat <- data.set(dat,
                   col.defs = col_defs,
                   unit.defs = unit_defs
                   )
    str(dat)
    
    eml_config(creator="Ivan Charles Hanigan <ivan.hanigan@gmail.com>")
    dir()
    oldwd <- getwd()
    setwd("myData")
    eml_write(dat, file = "test_eml.xml", title = "test_eml")
    setwd(oldwd)


<p></p>

### Use Morpho to tidy up the Results

- The result can be imported to Morpho and then edited from there
- or you can use a code editor like emacs or notepad++ to do bulk find-and-replace operations to fix up issues

### Conclusions

- Morpho failed with 200 plus variables
- the R EML package succeeded to write the file
- I needed to pay careful attention to the type of the variables in the data.frame before running the R EML functions
