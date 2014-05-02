---
name: tweaking-r-eml-package-outputs-with-morpho-and-failing-that-with-emacs
layout: post
title: Tweaking R Eml Package Outputs With Morpho And Failing That With Emacs
date: 2014-04-25
categories:
- Data Documentation
tags: 
- morpho
- R-eml
---

I realised that the work I did yesterday had an error in it.  I'd
created a list of unit.defs with one less than I needed.  So the
variable V100 was given the definition of NA!  I can fix this by open
that package in Morpho and go to the column and select it, then under
the Data menu, choose Edit Column Documentation.  There we can change
all the definitions.  Now I start thinking about changing the type
from count to ArealDensity, numberPerMeterSquared.  To change all
these new variables I don't want to go thru the GUI 95 times!  Change
the first one and then look at the EML

#### EML Code:
    <attribute id="1398382425052">
      <attributeName>V99</attributeName>
      <attributeDefinition>count stuff</attributeDefinition>
      <measurementScale>
        <ratio>
          <unit><standardUnit>number</standardUnit></unit>
          <numericDomain><numberType>real</numberType></numericDomain>
        </ratio>
      </measurementScale>
    </attribute>
    <attribute id="1398382385863">
      <attributeName>V100</attributeName>
      <attributeDefinition>A random variable</attributeDefinition>
      <measurementScale>
        <ratio>
          <unit><standardUnit>numberPerMeterSquared</standardUnit></unit>
          <numericDomain><numberType>real</numberType></numericDomain>
        </ratio>
      </measurementScale>
    </attribute>

<p></p>

So this looks like I can do a find and replace in Emacs so go to the
"~/.morpho" database and make a copy of the appropriate EML (number was in the morpho saved) and rename it with the increment up one of the minor version. Open this and run the find and replace.

#### Code:
    <standardUnit>number<
    to
    <standardUnit>numberPerMeterSquared<

<p></p>

Which was a much quicker way to redefine all these.  Save to our Metacat Network and it shows up as I wanted it to.

![morpho-wide3.png](/images/morpho-wide3.png)

## Conclusions
- Morpho and a code editor can be used in conjunction to edit EML quite well
- I suspect edits to the EML directly with a code editor are pretty dangerous
- For eg if you do the wrong change then that EML will likely not be valid and Morpho will complain.
- But the advantage of quickly modifying things like 100 variables unit definitions rather than opening every one in the GUI seems to be a worthwhile risk to me.
