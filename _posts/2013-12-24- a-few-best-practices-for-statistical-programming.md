---
name:  a-few-best-practices-for-statistical-programming
layout: post
title:  a-few-best-practices-for-statistical-programming
date: 2013-12-24
categories:
- research methods
---

- John Myles White invented the ProjectTemplate R Package
- This is a great application that helps streamline the process of creating a data analysis project
- Recently John posted about some tips for [best practices for statistical programming](http://www.johnmyleswhite.com/notebook/2013/01/24/writing-better-statistical-programs-in-r/)


#### Best Practices for Statistical Programming

- Write Out a Directed Acyclic Graph (DAG)
- Vectorize Your Operations (profile your code and understand where it spends its time)
- Generate Data and Fit Models
- Correctness: always ensure that code infers  parameters of models given simulated data with known parameters.


#### Additional suggestions

- Unit Testing (use testthat)
- Re-factoring - as above, but with extra attention to system.time()
