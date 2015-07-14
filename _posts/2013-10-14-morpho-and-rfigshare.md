---
name: morpho-and-rfigshare
layout: post
title: morpho-and-rfigshare
date: 2013-10-14
categories:
- Data Documentation
tags:
- morpho
---

In this Case Study I will use Morpho to compare directly with reml.

# Step one: Set up morpho

- Follow the instructions at the ASN SuperSite website and install Morpho 1.8 rather than latest version because it has technical issues that stop it from setting permissions.    
- [Configure morpho](http://www.tern-supersites.net.au/index.php/data/repository-tutorial).  (I will follow the ASN SuperSite instructions as a future Case Study will be to use their KNB Metacat service).
- Do not configure to connect to the Metacat repository, will need a password to be assigned by ASN data manager.

# Step 2: Look at the REML created metadata using Morpho

- Morpho offers to open existing sets for modification.

#### Code: get location of my example dataset
    require(disentangle)
    fpath <- system.file(file.path("extdata", "civst_gend_sector.csv"), package="disentangle")
    fpath
    dirname(fpath)
    # [1] "/home/ivan_hanigan/Rlibs/disentangle/extdata"

- Morpho > File > import = civst_gend_sector_eml.xml
- (not the figshare_civst_gend_sector_eml.xml that was created when sending to figshare)
- Error encountered.  could not open metadata, open empty data package.  Offered to upgrade (unable to edit > accepted)
- unable to display data, empty data package will be shown
- top menu > Documentation > Add/Edit ion
# Step 3: Create new datasets with Morpho
