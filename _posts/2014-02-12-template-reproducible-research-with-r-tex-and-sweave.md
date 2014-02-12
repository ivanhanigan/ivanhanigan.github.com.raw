---
name: template-reproducible-research-with-r-tex-and-sweave
layout: post
title: Template Reproducible Research with R TEX and Sweave
date: 2014-02-12
categories:
- research methods
---

- Last year I wrote to a Professor to let them know some numbers that quantified their effect estimate (computed be exponentiating their beta coefficient) described in their results section was inconsistent with the numbers in their table (the raw coefficients).
- Happily the recalculation showed that they had underestimated the effect size and their conclusions were not wrong, but erroneously conservative.
- Previously I would use Sweave documents to keep track of all my calculations, but I was still copy-and-pasting the key numbers into the text.
- I've become more interested now in using Inline R Outputs (called Sexpr - S expressions)
- This is also the first time I've created a report using the Palatino font, on the advice of a new colleague of mine.
- I popped up a [Github repo with a Sweave template for Reproducible Reports with a few notes I made](https://github.com/ivanhanigan/DataDocumentation).  Which looks like

![/images/sexpr.png](/images/sexpr.png)

- The [PDF output is here](https://github.com/ivanhanigan/DataDocumentation/blob/master/src/sexpr.pdf)

- The [Sweave file is here](https://github.com/ivanhanigan/DataDocumentation/blob/master/src/sexpr.Rnw)
