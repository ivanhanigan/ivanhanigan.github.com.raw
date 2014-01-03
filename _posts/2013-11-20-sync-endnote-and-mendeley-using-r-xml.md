---
name: 2013-11-20-sync-endnote-and-mendeley-using-r-xml
layout: post
title: sync-endnote-and-mendeley-references-using-r-xml
date: 2013-11-20
categories:
- research methods
---

#### Background
- I use Mendeley (despite them being bought out by Elsevier, who used to sell guns)
- My Colleagues use EndNote 
- Need to sync, they find Endnote better for their workflow
- I tried to export my Mendeley as XML and import to Endnote, but found many duplicates that took time to rectify 
- (and the risk is there that the RefNo they used in the Doc will be the duplicate that I removed)

#### Aims
- test if R and the XML package can help find refs in Endnote that aren't in Mendeley
- If so can I write those into an Mendeley import for seamless integrations
- and what about going from Mendeley to Endnote?

#### Methods
- The R XML package seems an obvious place to start
- before writing a function, just step thru the process

#### Step 1: export XML from Mendeley and Endnote
- In Mendeley Just select the refs in the list and then from the file menu
- In Endnote it is also under File menu

#### Step 2: R Code:
    # func
    # might need sudo apt-get install r-cran-xml?
    require(XML)

    # load
    dir()
    [1] "EndnoteCollection.xml"
        "MendeleyCollection.Data"
    [3] "MendeleyCollection.xml" 
    
    d1 <- xmlTreeParse("EndnoteCollection.xml", useInternal=T)

    # clean
    str(d1)
    # ooooh xml schmexemhel voodoo?

    # do
    top <- xmlRoot(d1)
    str(top)
    names(top)
    # top [[1]] # prints the whole thing
    top [[1]][[1]]
    top [[1]][[2]]
    # prints a record (1 or 2)

    # just messing around
    length(top[[1]])
    top [[1]][[120]]
    names(top [[1]][[120]])
    names(top [[1]][[120]][["contributors"]])
    names(top [[1]][[120]][["contributors"]][["authors"]])
    top [[1]][[120]][["contributors"]][["authors"]][[2]]
    
    i <- 110
    top [[1]][[i]]
    as.matrix(names(top [[1]][[i]]))

#### OK so XML as a list.
- I think if I do a merge of two author-date-title dataframes I can easily find the diffs


#### TRY a square wheel
#### R Code:
    endnote_mendeley_df <- function(input_xml,
                                    nrow_to_try = 1000){
      d1 <- xmlTreeParse(input_xml, useInternal=T)
      top <- xmlRoot(d1)
     
      output <- matrix(ncol = 4, nrow = 0)
      for(i in 1:nrow_to_try)
      {
      # i = 1000
        if(is.na(xmlValue(top [[1]][[i]]))) break
        if(
          !is.na(xmlValue(top [[1]][[i]][["contributors"]][["authors"]][[2]]))
          )
        {
          author <- paste(xmlValue(top [[1]][[i]][["contributors"]][["authors"]][[1]]), "et al", " ")
        } else {
          author <- xmlValue(top [[1]][[i]][["contributors"]][["authors"]][[1]])
        }
        year <- xmlValue(top [[1]][[i]][["dates"]][["year"]])
        title <- xmlValue(top [[1]][[i]][["titles"]][[1]])
        endnoteref <- xmlValue(top [[1]][[i]][["rec-number"]])
        output <- rbind(output, c(author, year, title, endnoteref))
     
      }
      output <- as.data.frame(output)
      return(output)
    }

#### R Test:
    output <- endnote_mendeley_df(
      input_xml = "EndnoteCollection.xml"
      ,
      nrow_to_try = 10
      )

    nrow(output)
    write.csv(output, "EndnoteCollection.csv", row.names = F)
    output  <- read.csv("EndnoteCollection.csv", stringsAsFactors = F)
    str(output)
    output[,1:2]

#### R Do-read:
    endnote <- endnote_mendeley_df(
      input_xml = "EndnoteCollection.xml"
      )
    nrow(endnote)
    mendeley <- endnote_mendeley_df(
      input_xml = "MendeleyCollection.xml"
      )
    nrow(mendeley)

#### R Do-concatenate and lowercase
    # TODO this is a really terrible way to do this.
    # FIXME find out how to compare the two better
    require(stringr)
    mendeley2 <- str_c(mendeley$V1, mendeley$V2, mendeley$V3)
    mendeley2 <- gsub(" ", "", mendeley2)
    mendeley2 <- gsub(",", "", mendeley2)
    mendeley2 <- tolower(mendeley2)
    mendeley2[1:5]
    mendeley$mendeley2 <- mendeley2

    # now do this again from endnote
    endnote2 <- str_c(endnote$V1, endnote$V2, endnote$V3)
    endnote2 <- gsub(" ", "", endnote2)
    endnote2 <- gsub(",", "", endnote2)
    endnote2 <- tolower(endnote2)
    endnote2[1:5]
    endnote$endnote2 <- endnote2

#### R Do-merge:
    endnote_not_in_mendeley <- merge(endnote,
                                     mendeley,
                                     by.x = "endnote2",
                                     by.y = "mendeley2",
                                     all.x = T)
    str(endnote_not_in_mendeley)
    nrow(endnote_not_in_mendeley)
    head(endnote_not_in_mendeley)
    endnote_not_in_mendeley <- endnote_not_in_mendeley[
                                                       is.na(endnote_not_in_mendeley$V1.y),
                                                       ]
    nrow(endnote_not_in_mendeley)
    # 66 refs in endnote are not in mendeley
    write.csv(endnote_not_in_mendeley,
          "endnote_not_in_mendeley.csv", row.names = F)
#### Open this as spreadsheet and cross check
- make a new column for comments
- check off which ones were in AllDocuments and not in the Mendeley group
- this diff was because of when I imported the Endnote XML but had not assigned these to the mendeley group
- once have cleaned up the mendeley group export again and then check which are in mendeley but not in endnote

#### First here is a note
- about a way to speed up the checks, excluding false positives using fuzzy matching
- my method relies on the author, date and title to be written the same in both ie initials then surname or visa verca
- But this is not always true 
- I previously used levenshtein string matching to identify strings that are close but not identical
- [Try this link]( http://wiki.r-project.org/rwiki/doku.php?id=tips:data-strings:levenshtein)
- [OR this link](http://rwiki.sciviews.org/doku.php?id=tips:data-strings:levenshtein)
- TODO I will share this code as a GitHub Gist later!


#### R Code: possibility to speed up Checks
    tmp1 <- mendeley[grep("Walker", mendeley$V1),"mendeley2"]
    tmp2 <- endnote[grep("Walker", endnote$V1),"endnote2"]

    # these differ slightly
    # B. Walker et al vs Walker, Brian et al
    source("~/Dropbox/tools/levenshtein.r")
    levenshtein(
        tmp1
        ,
        tmp2
        )
    # gives 92percent match


#### R Code: Find mendeley refs without endnote
      endnote <- endnote_mendeley_df(
        input_xml = "EndnoteCollection.xml"
        )
      nrow(endnote)
      mendeley <- endnote_mendeley_df(
        input_xml = "MendeleyCollection2.xml"
        )
      nrow(mendeley)
#### R Code: Do-concatenate and lowercase
    require(stringr)
    mendeley2 <- str_c(mendeley$V1, mendeley$V2, mendeley$V3)
    mendeley2 <- gsub(" ", "", mendeley2)
    mendeley2 <- gsub(",", "", mendeley2)
    mendeley2 <- tolower(mendeley2)
    mendeley2[1:5]
    mendeley$mendeley2 <- mendeley2

    # now do this again from endnote
    endnote2 <- str_c(endnote$V1, endnote$V2, endnote$V3)
    endnote2 <- gsub(" ", "", endnote2)
    endnote2 <- gsub(",", "", endnote2)
    endnote2 <- tolower(endnote2)
    endnote2[1:5]
    endnote$endnote2 <- endnote2

#### R Do-merge:
    mendeley_not_in_endnote <- merge(mendeley,
                                     endnote,
                                     by.y = "endnote2",
                                     by.x = "mendeley2",
                                     all.x = T)
    str(mendeley_not_in_endnote)
    nrow(mendeley_not_in_endnote)
    head(mendeley_not_in_endnote)
    mendeley_not_in_endnote <- mendeley_not_in_endnote[
                                                          is.na(mendeley_not_in_endnote$V1.y),
                                                          ]
    nrow(mendeley_not_in_endnote)
    # 92 refs in endnote are not in mendeley
    write.csv(mendeley_not_in_endnote,
          "mendeley_not_in_endnote.csv", row.names = F)
#### Not all these 92 will be true
- so let;s try the string matching
 
#### R Code:
    source("~/Dropbox/tools/levenshtein.r")
    pcnt_threshold <- 0.6
    out_list <- matrix(ncol = 3, nrow = 0)
    #out_list <- read.csv("mendeley_not_in_endnote_fz_match.csv", stringsAsFactors = F)
    for(i in 36:nrow(mendeley_not_in_endnote))
        {
            print(i)
    #        i = 2
    tmp1 <- mendeley_not_in_endnote[i,1]
        for(j in 1:nrow(endnote))
            {
        #        j = 2
        if(exists("out")) rm(out)
        tmp2 <- endnote$endnote2[j]
        pcnt <- levenshtein(
                tmp1
                ,
                tmp2
                )
        #pcnt
        if(pcnt >= pcnt_threshold) out <- tmp2
        if(exists("out"))
            out_list <- rbind(out_list, c(tmp1, tmp2, pcnt))
        if(exists("out")) break
            }
            
        }
    out_list
    write.csv(out_list, "mendeley_not_in_endnote_fz_match.csv", row.names = F)
#### R Code: Do-concatenate and lowercase
    require(stringr)
    out_list <- read.csv("mendeley_not_in_endnote_fz_match.csv", stringsAsFactors = F)
    mendeley2 <- read.csv("mendeley_not_in_endnote.csv", stringsAsFactors=F)
    mendeley2[1,]
    out_list[1,]
    mendeley2 <- merge(mendeley_not_in_endnote, out_list,
                       by.x = "mendeley2",
                       by.y = "V1", all.x = T)
    mendeley2[2,]
    mendeley2 <- mendeley2[is.na(mendeley2$V3),]
    nrow(mendeley2)
    # 48 records
    write.csv(mendeley2, "mendeley_not_in_endnote_best_estimate.csv", row.names=F)
#### Results
- I found that XML package in R can work with the Endnote and Mendeley export Files
- I think I made a lot of bad decisions about the way I went about  doing this!
- It seemed quite difficult to get the XML stuff to make sense to me
- I;ve heard that python has better libraries for working with XML
- the levenshtein string matching code proved useful again.  I should get out of the habit of looping and start using lapply etc to speed this up.
  
#### Conclusions
- This was an interesting if frustrating experiment
- The minor issues with importing from mendeley/endnote and deduplicating using their own tools was probably not worth writing all this half-baked R code.
- But I did learn more about working with XML in R (and realised this is probably not one of R's Strengths -- or mine for that matter!)
