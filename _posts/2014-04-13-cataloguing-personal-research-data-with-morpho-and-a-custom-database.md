---
name: 2014-04-13-cataloguing-personal-research-data-with-morpho-and-a-custom-database
layout: post
title: Cataloguing Personal Research Data with Morpho And A Custom Database
date: 2014-04-13
categories:
- Data Documentation
---

#### Introduction

The collection of scientific data is undertaken at an individual level
by everybody in their own way. The layout of data collections that I
have seen is incredibly varied; spread across multiple files and folders which can
be difficult to navigate or search through. In some cases
these collections are incomprehensible to all but the individual themselves. Given
that a lot of projects are collaborative in nature and require
extensive sharing, it is important that scientists maintain their
data collection by some form of system that allows easy data extraction and
use in other projects. Therefore, the maintenance of a personal catalogue of datasets is an
important activity for scientists.

By cataloguing I mean that a file or database is kept that stores all the
information about the names of the datasets (and any other files the
data may be spread across), where the datasets are located, any
references (papers) that were developed from it and finally
important information regarding the conditions it
was formed under.

While this may seem laborious, it keeps track of all the data that one
has collected over time and gives one a reference system to find a
dataset of interest when sharing with collaborators. Datasets can be
saved in any filing system the scientist chooses, but with the help of
their personal data catalogue they will always know the status of
their data collection.

#### Cataloguing Personal Research Data with Morpho

[Metacat](https://knb.ecoinformatics.org/knb/docs/intro.html) is an
online repository for data and metadata. It is a great resource for
the publication of data, but not very useful for an individual
scientist to use on their personal computer.  However
[Morpho](https://knb.ecoinformatics.org/#tools/morpho) the Metadata
Editor used by Metacat may be used locally by a researcher to
catalogue their collection (and ultimately this will make publishing
elements of the collection easier.)  Morpho uses the Ecological
Metadata Language (EML) to author metadata with a graphical user
interface wizard.

#### How Morpho Works

When you install Morpho it creates a directory where you can run the
program from, and another hidden directory called ".morpho" for it's
database of all your metadata (and optionally any data you import to
it).  Below is an image of mine, with a couple of test records I
played around with (the XMLs/HTMLs) and a dataset I imported (the text
file).

- ~/.morpho/profiles/hanigan/data/hanigan/

![morphodir1](/images/morphodir1.png)

Every time a modification is made to the metadata a new XML is saved here, with the major number being the ID of the package and incremented minor number to reflect the change.

### Adding a dataset from my collection

I have already got a good amount of metadata I generated when I published [the drought data](http://dx.doi.org/10.4225/13/50BBFD7E6727A)

#### the drought dataset:
    Hanigan, Ivan (2012): Monthly drought data for Australia 1890-2008
    using the Hutchinson Drought Index. Australian National University Data Commons.
    DOI: 10.4225/13/50BBFD7E6727A. 

<p></p>

### Step One: define the project that I will keep locally

- This is the Github repo https://github.com/swish-climate-impact-assessment/DROUGHT-BOM-GRIDS
- I store this locally at ~/data/DROUGHT-BOM-GRIDS

### Contextual Metadata

#### Abstract

I originally wrote the abstract as the description for a RIF-CS metadata object to publish for the ANU library.

I got the following instructions from a Librarian: The "informative abstract" method.

- The abstract should be a descriptive of the data, not the research.
- Briefly outline the relevant project or study and describe the contents of the data package. 
- Include geographic location, the primary objectives of the study, what data was collected (species or phenomena), the year range the data was collected in, and collection frequency if applicable.
- Describe methodology techniques or approaches only to the degree necessary for comprehension – don’t go into any detail.
- Cite references and/or links to any publications that are related to the data package.
- Single paragraph
- 200-250 words
- Use active voice and past tense.
- Use short complete sentences.
- Express terms in both their abbreviated and spelled out form for search retrieval purposes.

#### Australian FOR codes
ANZSRC-FOR Codes: Australian and New Zealand Standard Research Classification – Fields of Research codes allow R&D activity to be categorised according to the methodology used in the R&D, rather than the activity of the unit performing the R&D or the purpose of the R&D.  
http://www.abs.gov.au/Ausstats/abs@.nsf/Latestproducts/4AE1B46AE2048A28CA25741800044242?opendocument

#### GCMD Keywords
Olsen, L.M., G. Major, K. Shein, J. Scialdone, S. Ritz, T. Stevens, M. Morahan, A. Aleman, R. Vogel, S. Leicester, H. Weir, M. Meaux, S. Grebas, C.Solomon, M. Holland, T. Northcutt, R. A. Restrepo, R. Bilodeau, 2013. NASA/Global Change Master Directory (GCMD) Earth Science Keywords. Version 8.0.0.0.0 
http://gcmd.nasa.gov/learn/keyword_list.html

#### Geographic coverage
    # I developed the following function to take a spatial object and convert it to the bounding box
    > require(devtools)
    > install_github("disentangle", "ivanhanigan")
    > require(disentangle)
    > morpho_bounding_box(d)
                      X1                 X2                 X3
    1               <NA> 10.1356954574585 S               <NA>
    2 112.907211303711 E               <NA> 158.960372924805 E
    3               <NA> 54.7538909912109 S               <NA>



#### Save the metadata

- the metadata is now ready to save to my .morpho catalogue
- without importing any data

![morphoimg2.png](/images/morphoimg2.png)

- this appears as a new XML

![morphoimg3.png](/images/morphoimg3.png)

- which looks like this

![morphoimg4.png](/images/morphoimg4.png)

### Additional Metadata 

As this is metadata only about the dataset, it is innapropriate to refer to related publications etc in these elements.  Luckily EML has the additionalMetadata and additionalLinks fields.  Just open the XML and paste the following in the bottom.

    <additionalMetadata>
      <metadata>
        <additionalLinks>
          <url name="Hanigan, IC, Butler, CD, Kokic, PN, Hutchinson, MF. Suicide and Drought in New South Wales, Australia, 1970-2007. Proceedings of the National Academy of Science USA 2012, vol. 109 no. 35 13950-13955, doi: 10.1073/pnas.1112965109">http://dx.doi.org/10.1073/pnas.1112965109</url>
        </additionalLinks>
      </metadata>
    </additionalMetadata>

You can see this if you then open it up again in morpho and then under the documentation menu go to Add/Edit Documentation.

![morphoimg5.png](/images/morphoimg5.png)

### Additional Metadata regarding the Data Location and Backups

These data are quite large and also geospatial, so I store these 
on a PostGIS server at the ANU library. The original data are stored
on a PostGIS server at NCEPH and the code I used to compute the
indices is on github.  So all I want to do with Morpho is document the
data, not import it.
