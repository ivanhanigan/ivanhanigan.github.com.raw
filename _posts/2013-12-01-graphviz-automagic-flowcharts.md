---
name: 2013-12-01-graphviz-automagic-flowcharts
layout: post
title: graphviz-automagic-flowcharts
date: 2013-12-01
categories:
- research methods 
- workflow
---

- Back in 2009 Joseph Guillaume worked with me on a complicated workflow
- He came up with this python script to help keep track of the steps
- The simple text file is a list of transformations, inputs and output
- It is converted to the right format and graphviz creates a html page with pop-outs

#### Simple text list
    Transformation
            description
                    the thing 
            inputs
                    the thing before
                    another thing
            output
                    the next thing
            notes
                    the thing is this other thing   this is a really long description 
                    blah blah asdfasdfasdfasdfasdfa 
     
    Transformation
            description
                    yet another thing
            inputs
                    the next thing
            output
                    a final thing
            notes
                    this is a note

<p></p>

- keep this in your work directory and update it whenever you add a step to the workflow
- the list can be as big as you like (hundreds of steps), and entered in any order, the inputs/output relationships determine how the graph looks at the end
- to run the script just do the one line

#### Python code: run
    python transformations.py workflow_steps.txt index

<p></p>
- open the html page and click on a square box to bring up the pop-out
- short text is shown, long text is replaced by an ellipse and only shown in pop-out

#### Conclusions  
- I've popped the script up as a [Github repo](https://github.com/ivanhanigan/transformations)
- The example is in the [gh-pages branch](http://ivanhanigan.github.io/transformations/)
