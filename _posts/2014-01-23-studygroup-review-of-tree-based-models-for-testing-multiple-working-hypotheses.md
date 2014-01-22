---
name: 2014-01-23-studygroup-review-of-tree-based-models-for-testing-multiple-working-hypotheses
layout: post
title: studygroup-review-of-tree-based-models-for-testing-multiple-working-hypotheses
date: 2014-01-23
categories:
- research methods
- overview
---

Yesterday I had the opportunity to review the Tree based modelling methods we are implementing in a study I'm working on at the moment.
I based the discussion on [a paper from 2012](http://www.tandfonline.com/doi/abs/10.1080/00330124.2012.724347), along with [some notes I have made related to the use of these methods in our context](/pdfs/TreeModelNotes.pdf).
I had an hour and a half with a couple of senior statisticians and a bunch of sociologists at the study group yesterday.

#### My main question for the group was:

- What do you think of the proposition that these models are suitable for "studies that test hypotheses generated from multiple theories"?

The statisticians where underwhelmed by the Cutts study, but thought the stats method was "neat" and one had not heard of tree models before (!).

#### Key outcomes of that session were:

- First stage PCA  
    - Q: did they need to do the PCA first stage to either a) reduce the the large number of potentially collinear variables or b) to control for measurement error?
    - A: No they didn't need the PCA.  The large number, collinearity and measurement efficacy are dealt with by the tree based methods (ie cross-validation on steroids, grouping primary and surrogate splits, etc).  Also the trees have an advantage with the large number of predictors in that they are non-parametric and able to automatically detect interactions whereas PCA is parametric and typically assumes linearity. (Note that I saw Steve afterward and he is still not convinced.  Maybe he will respond to this with some description of the reason why not?)

- Rescaling the variables
    - Q: Did they need to centre each variable on the grand sample mean so that the relative weight of each variable was even?
    - A: No the tree models are not effected by this, and it reduced the interpret-ability of the decision tree graphic.  The PCA is effected, however, and maybe that is why they did it.

- Multiple working hypotheses
    - Q: What do you think of the Cutts et al proposition that these models are suitable for "studies that test hypotheses generated from multiple theories"?
    - A: It is a promising approach.  Not clear from this study if it is successful but the proposition is plausible.  It has more of a chance than the General Linear Model approach which cannot (this point was made categorically by one of the statisticians).  It will be important to be very clear about what exactly each of the "Theories" are predicting, so that the explanatory power attributable to those variables from one "theory" can be compared with that of the other theories.  The ability to uncover complex interactions is very attractive (extrovert/introvert personality type interacting with group demographics etc) but it also increases the potential for spurious results (and 'chasing the noise') ergo the need to base inferences on what the theories predict, not just on what the data reveal.

- In general we thought that authors had overdone the stats.  It showed what 'could' be done with trees and forests, but possibly not what 'should' be done.

- Is the A3 variable really missing from ctree output but dominant in the randomForest in Figure3?
    - when another group I'm in reviewed it last year it was noted as odd that fig3 has A3 most important in randomforest but does not appear in ctree. At the time I thought this might be due to the cross validation like in the rpart or tree package, but it turns out that ctree does not do that.... 
    - Mislabelling is a possibility as these graphics appear to be edited from the default produced by the 'party' package.
    - However, it also reasonable that these results could be correct. ctree (and rpart, tree, etc.) use greedy algorithms, meaning that the best local split is used even if this is suboptimal globally.  
    - Basically there are algorithmic reasons that this might be a true difference between ctree and randomforest.  It might just have been the way the cookie crumbled for the ctree's best local split which may not have survived through the randomForest's  thousands of iterations.
    - But on page 569 they do say "total knowledge is lowest among those whod do not think that they are empowered and are unaware of information sources" which implies to me that the top or left-most node might be mis-labelled I3 when it is actually A3.
    - this would give the appropriate left most box plot (ie I3 <= -0.22 & A3 <= -0.64 gives lowest total knowledge??)
    - at the group yesterday people also generally suspected mislabelling, given the dominance of A3 in randomforest.
