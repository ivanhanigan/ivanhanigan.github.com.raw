---
name: 2014-06-18-data-dictionary-function-needed-upgrade-to-my-misc-package
layout: post
title: data-dictionary-function-needed-upgrade-to-my-misc-package
date: 2014-06-18
categories:
- disentangle
---

- Recently I got a lot of files with columns that are all missing.  I had to modify the 'data\_dictionary' function to cope with these so have released version 1.1
- [Windows Version is Downloadable Here](http://ivanhanigan.github.io/disentangle/lib/disentangle_1.1.zip)
- Linux and Mac users can just run this R code

#### R Code:
    require(devtools)
    install_github("disentangle", "ivanhanigan")

<p></p>

- In my 'disentangle' package of miscellaneous tools, the data\_dictionary function is designed to produce descriptive summary statistics in a familiar way to the FREQUENCIES command for SPSS
- I chose to emulate the SPSS output because I think it is a pretty decent summary statistics table, and there are loads of users who have already been introduced to this style of output
- I wrote it because I had not got exactly what I wanted from the reporttools or stargazer packages which also have similar summary stats functions
- I chose to call it data\_dictionary because I think that the alternatives (like 'frequencise' or 'code\_book' are not as immediately intuitive as to what you get) 
- the function I wrote returns a data.frame with the variable name, a simplified type (character, number or date)

#### Code:data-dictionary-function-needed-upgrade-to-my-misc-package
    # functions
    require(devtools)
    install_github("disentangle", "ivanhanigan")
    require(disentangle)
    require(xtable)

    # load
    fpath <- system.file("extdata/civst_gend_sector.csv", package = "disentangle")
    fpath
    civst_gend_sector <- read.csv(fpath)
    civst_gend_sector$datevar <- as.Date(round(rnorm(nrow(civst_gend_sector), Sys.Date(),10)), origin = "1970-01-01")
    civst_gend_sector$missing_blahblah_variable  <- NA

    # check
    str(civst_gend_sector)

    #do
    data_dict(civst_gend_sector, "civil_status")
    data_dict(civst_gend_sector, "datevar")
    data_dict(civst_gend_sector, "number_of_cases")
    data_dict(civst_gend_sector, "missing_blahblah_variable")
    
    dataDictionary <- data_dictionary(civst_gend_sector,
                                      show_levels = -1)
    
    print(xtable(dataDictionary), type = "html", include.rownames = F)

<p></p>

<!-- html table generated in R 3.1.0 by xtable 1.7-1 package -->
<!-- Wed Jun 18 22:41:49 2014 -->
<TABLE border=1>
<TR> <TH> Variable </TH> <TH> Type </TH> <TH> Attributes </TH> <TH> Value </TH> <TH> Count </TH> <TH> Percent </TH>  </TR>
  <TR> <TD> civil_status </TD> <TD> character </TD> <TD> divorced/widowed </TD> <TD>  </TD> <TD> 6 </TD> <TD align="right"> 33.33 </TD> </TR>
  <TR> <TD>  </TD> <TD>  </TD> <TD> married </TD> <TD>  </TD> <TD> 6 </TD> <TD align="right"> 33.33 </TD> </TR>
  <TR> <TD>  </TD> <TD>  </TD> <TD> single </TD> <TD>  </TD> <TD> 6 </TD> <TD align="right"> 33.33 </TD> </TR>
  <TR> <TD> gender </TD> <TD> character </TD> <TD> female </TD> <TD>  </TD> <TD> 9 </TD> <TD align="right"> 50.00 </TD> </TR>
  <TR> <TD>  </TD> <TD>  </TD> <TD> male </TD> <TD>  </TD> <TD> 9 </TD> <TD align="right"> 50.00 </TD> </TR>
  <TR> <TD> activity_sector </TD> <TD> character </TD> <TD> primary </TD> <TD>  </TD> <TD> 6 </TD> <TD align="right"> 33.33 </TD> </TR>
  <TR> <TD>  </TD> <TD>  </TD> <TD> secondary </TD> <TD>  </TD> <TD> 6 </TD> <TD align="right"> 33.33 </TD> </TR>
  <TR> <TD>  </TD> <TD>  </TD> <TD> tertiary </TD> <TD>  </TD> <TD> 6 </TD> <TD align="right"> 33.33 </TD> </TR>
  <TR> <TD> number_of_cases </TD> <TD> number </TD> <TD> Min. </TD> <TD> 0 </TD> <TD>  </TD> <TD align="right">  </TD> </TR>
  <TR> <TD>  </TD> <TD>  </TD> <TD> 1st Qu. </TD> <TD> 5 </TD> <TD>  </TD> <TD align="right">  </TD> </TR>
  <TR> <TD>  </TD> <TD>  </TD> <TD> Median </TD> <TD> 9 </TD> <TD>  </TD> <TD align="right">  </TD> </TR>
  <TR> <TD>  </TD> <TD>  </TD> <TD> Mean </TD> <TD> 15.17 </TD> <TD>  </TD> <TD align="right">  </TD> </TR>
  <TR> <TD>  </TD> <TD>  </TD> <TD> 3rd Qu. </TD> <TD> 17 </TD> <TD>  </TD> <TD align="right">  </TD> </TR>
  <TR> <TD>  </TD> <TD>  </TD> <TD> Max. </TD> <TD> 50 </TD> <TD>  </TD> <TD align="right">  </TD> </TR>
  <TR> <TD> datevar </TD> <TD> date </TD> <TD> Min. </TD> <TD> 2014-05-26 </TD> <TD>  </TD> <TD align="right">  </TD> </TR>
  <TR> <TD>  </TD> <TD>  </TD> <TD> 1st Qu. </TD> <TD> 2014-06-07 </TD> <TD>  </TD> <TD align="right">  </TD> </TR>
  <TR> <TD>  </TD> <TD>  </TD> <TD> Median </TD> <TD> 2014-06-15 </TD> <TD>  </TD> <TD align="right">  </TD> </TR>
  <TR> <TD>  </TD> <TD>  </TD> <TD> Mean </TD> <TD> 2014-06-14 </TD> <TD>  </TD> <TD align="right">  </TD> </TR>
  <TR> <TD>  </TD> <TD>  </TD> <TD> 3rd Qu. </TD> <TD> 2014-06-18 </TD> <TD>  </TD> <TD align="right">  </TD> </TR>
  <TR> <TD>  </TD> <TD>  </TD> <TD> Max. </TD> <TD> 2014-07-05 </TD> <TD>  </TD> <TD align="right">  </TD> </TR>
  <TR> <TD> missing_blahblah_variable </TD> <TD> missing </TD> <TD> NA's </TD> <TD>  </TD> <TD> 18 </TD> <TD align="right"> 100.00 </TD> </TR>
  </TABLE>
