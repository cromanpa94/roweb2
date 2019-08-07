---
slug: "software-peer-review-guidelines-for-teaching"
title: Using rOpenSci Software Peer Review Guidelines for Teaching
authors:
  - Tiffany Timbers
date: 2010-08-12
categories: blog
topicid:
tags:
- Software Peer Review
- R
- software
- packages
- teaching
- education
---

In the [University of British Columbia's Master of Data Science program](https://ubc-mds.github.io/about/) one of the courses we teach is called [DSCI 524 Collaborative Software Development](https://github.com/UBC-MDS/DSCI_524_collab-sw-dev). In this course we focus on teaching how to exploit practices from collaborative software development techniques in data scientific workflows. This includes appropriate use of the software life cycle, unit testing and continuous integration, as well as packaging code for use by others. 

This is a project-based course where students are required to work together in teams of three or four. Here the project involves developing a Python and an R software package. The two packages are expected to do essentially the same thing. They are asked to make one in each language so that they can learn how to do both, and learn to generalize about software pacakges. For the project, the students are guided to choose the package topic from one of the following themes: 1) functions that are entirely new to the R or Python ecosystem, 2) improve upon pre-existing functions in either language or 3) re-implement existing code/functions that they wish to deepen their understanding of (*e.g.,* write a linear regression package from scratch). Students are asked to place emphasis in their work on robust software engineering (*e.g.,* continuous integration, testing, documentation, licensing) and collaboration (*e.g.,* advanced version control control).

For courses in the Master of Data Science program we work hard to find and curate high quality and current resources for our students to help them in their coursework. For this collaborative software development course, one of the best resources we recommend for the R package part of their project is the [rOpenSci Packages: Development, Maintenance, and Peer Review](https://devguide.ropensci.org/) guide. In particular, we encourage the students to go through the [Review template](https://devguide.ropensci.org/reviewtemplate.html) in the appendix of that guide before they hand in their R package for final grading. We recommend this, as by its design and use in the wild, it is a comprehensive checklist to review if an R package is of high quality and complete (in regards to software development). Instructors and Teaching Assistants for this course also use this [Review template](https://devguide.ropensci.org/reviewtemplate.html) to help give both formative feedback and guide summative assessment. Currently we are not aware of such a checklist for Python packages, and thus this rOpenSci guide also helps the Instructors and Teaching Assistants consider what should be considered for formative feedback and summative assessment for the Python packages. We hope the Python community builds an equivalent package review system and guide that we can leverage in the future. 

We think that by using the [rOpenSci Packages: Development, Maintenance, and Peer Review](https://devguide.ropensci.org/) guide in our [DSCI 524 Collaborative Software Development](https://github.com/UBC-MDS/DSCI_524_collab-sw-dev) course in the [University of British Columbia's Master of Data Science program](https://ubc-mds.github.io/about/) we can better teach our students how to create high quality software packages, and expose them to the idea of package review in hopes that they will embrace this culture when they create their own Data Science software packages out in the wild in their future careers.



