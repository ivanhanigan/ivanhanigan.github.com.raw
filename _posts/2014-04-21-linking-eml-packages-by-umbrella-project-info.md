---
name: linking-eml-packages-by-umbrella-project-info
layout: post
title: linking-eml-packages-by-umbrella-project-info
date: 2014-04-21
categories:
- Data Documentation
tags:
- morpho
---

In Eml the optional "project" module provides an overall description
of the larger-scale project or research context with which that
dataset is associated. For the examples in our work the "project" will
most often be an LTER (Longterm Ecological Research Network) site that
directed the research.  Accordingly, the "title" here consists of the
name of the LTER site. The "personnel" group contains the same
elements as "creator" and "contact", with the addition of a mandatory
"role" element, and it is used to identify the lead PI and/or
information manager on the site. Other optional elements in the
"project" module include "abstract", "funding",
"studyAreaDescription", and "designDescription", each of which can be
used to provide a richer textual description of the LTER site
responsible for the research project being documented.  If used, the
"abstract" includes basic information about the LTER site, such as its
general history and administration, while "studyAreaDescription" is
more of a physical description of the area where the site is
located. This description may also include the "coverage" module,
which is fully discussed on page XX of this handbook, or the
"citation" module, covered on page XX. The "funding" tag is textual
and self-explanatory, but "designDescription" is best used for a
description of the site’s database information and availability.

Morpho doesn't give all these options so you need to go to the EML file found in the "~/.morpho/..." directory and edit this with a text editor
I think the order of the tags here might make a difference so I always put thye "abstract" tag after the "/personnel" tag.  I also think you might need this "para" tag:

#### Code:linking-eml-packages-by-umbrella-project-inf
    <abstract> 
      <para>Prof McMichael set up this group to develop new methods of researching Environmental (especially Climate Change) and Health
      </para>
    </abstract>

<p></p>

So this gives the overarching project a valid reference, but how to provde the links for interested readers to find out more?  First we can include a link to the project homepage from the eml/dataset/abstract node, but also we can provide URLs in a machine-readable way by inserting an "additionalLinks" node at the bottom of the EML:

#### Code:linking-eml-packages-by-umbrella-project-info
    <additionalMetadata>
      <metadata>
        <additionalLinks>
          <url name="The name of the homepage">http://...</url>
        </additionalLinks>
      </metadata>
    </additionalMetadata>
