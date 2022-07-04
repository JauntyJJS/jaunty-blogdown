---
title: "Learning Journey and Reflections on useR! 2022 Conference Part 1"
subtitle: ""
excerpt: "This narrative is a write up on Day 1 and Day 2 of my learning journey in the useR! 2022 Conference."
date: 2022-06-23
author: "Jeremy Selva"
draft: false
images:
series:
  - useR! 2022
tags:
  - useR! 2022
categories:
  - useR! 2022
layout: single-sidebar
editor_options: 
  chunk_output_type: console
bibliography: utils/bibliography.bib
csl: utils/f1000research.csl
---

## Introduction

The [useR! 2022 Virtual Conference](https://user2022.r-project.org/) has provided me to new things about R as well as an opportunity to meet new people along the way. Here is a narrative of my learning journey in the conference for Day 1 and Day 2.

## Day 1

I have attended two workshops this year titled Introduction to Dimensional Reduction in R and Regression Modeling Strategies.

### Introduction To Dimensional Reduction In R

The course was conducted by [Isabella Bicalho-Frazeto](https://twitter.com/bisnotforbella). The materials can be found in this [Github page](https://github.com/bellabf/dimensional-reduction).

I personally enjoyed this course as it was not too technical with equations and the pace was just right with sufficient breaks. The instructor also went the extra mile to create polls to interact with us and check if we wwere doing fine during the course.

Besides learning to use different dimension reduction techniques using base R, I was also lightly introduced to the use of [Tidymodels](https://www.tidymodels.org/) to do Principal Component Analysis ([PCA](https://recipes.tidymodels.org/reference/step_pca.html) ) as well as [reticulate](https://rstudio.github.io/reticulate/) to run T-distributed Stochastic Neighbor Embedding ([tSNE](https://scikit-learn.org/stable/modules/generated/sklearn.manifold.TSNE.html) ) using [Python](https://www.python.org/).

### Regression Modeling Strategies

It was heart warming to be able to attend a course conducted by a well-known biostatistician, [Frank Harrell](https://twitter.com/f2harrell) from Vanderbilt University.

I first saw his presentation [R for Graphical Clinical Trial Reporting](https://www.youtube.com/watch?v=4gXWQxaBbac) during the RStudio Conference 2020 at San Francisco. Here is the [abstract](https://www.fharrell.com/talk/rstudio20/) for that presentation. I was touched by his desire and passion to always learn new things in R. This talk was one of the key morale booster for me to learn [plotly](https://plotly.com/r/) even though its documentation could be quite intimidating.I only got aware of his popularity when I saw him again presenting again at the Why R? 2020 as a keynote speaker titled [Controversies in Predictive Modeling, Machine Learning, and Validation](https://www.youtube.com/watch?v=DF1WsYZ94Es).

In summary, the course was mainly a short summary of his e-book [Regression Modeling Strategies](https://hbiostat.org/rms/) as well as a short introduction of his new e-book [R Workflow](https://hbiostat.org/rflow/) written in [Quarto](https://quarto.org/). Recently, he has also converted his free text [Biostatistics for Biomedical Research](http://hbiostat.org/bbr/) into an e-book as well. There are indeed a lot of useful information and it takes some time for me to digest, understand and reflect.

## Day 2

### First Keynote: R For Geospatial Data Science And Public Health Surveillance

The first keynote in Day 2 of the conference was by [Paula Moraga](https://twitter.com/Paula_Moraga), author of the e-book [Geospatial Health Data: Modeling and Visualization with R-INLA and Shiny](https://www.paulamoraga.com/book-geospatial/).

Even though I am not working with geospatial data, the content from the talk is very resourceful for those who has just started using R and geospatial analysis in general. It is the type of information I wish I had when I first begin to learn about R.

It started with a brief summary of a generic geospatial analysis workflow followed by some real life applications to highlight some challenges faced. Lots of visual examples were used to keep the audience glued to the talk. The presenter also shared how one can start learning geospatial analysis by using open data from [rspatialdata](https://rspatialdata.github.io/) and useful R packages analytical tools like [SpatialEpiApp](https://github.com/Paula-Moraga/SpatialEpiApp) and [epiflows](https://www.repidemicsconsortium.org/epiflows/). R packages from the [R Epidemics Consortium](http://www.repidemicsconsortium.org) were something new to me as well.

The section on communication and dissemination provided a good overview of different R packages used to display and distribute results to others. A gentle introduction of [ggplot2](https://ggplot2.tidyverse.org/), [htmlwidgets](http://gallery.htmlwidgets.org/), [R Markdown](https://rmarkdown.rstudio.com/), [flexdashboard](https://pkgs.rstudio.com/flexdashboard/), [Shiny](https://shiny.rstudio.com/) were mentioned, without being too technical on the code. The presenter also highlighted some R communities ([R Ladies](https://rladies.org/), [R Forwards](https://forwards.github.io/)) for those new to R to be able to seek help or improve themselves.

Overall, I recommended this keynote for those who wants to know more about R and what it can provide.

-   📝[Slides](https://www.paulamoraga.com/presentation-geohealth)

### gittargets For Better Data Version Control

As for the sessions, I first attended the first two talks from Big Data Management followed by next two talks from Building the R Community 1.

In the first talk, I got to view the latest development on the R package [targets](https://docs.ropensci.org/targets/) from [The R Targetopia](https://wlandau.github.io/targetopia/) created by [Will Landau](https://twitter.com/wmlandau).

[targets](https://docs.ropensci.org/targets/) is known to keep a record of pre-processing results in a data analysis pipeline so that it knows when it is able to skip tasks when data analysis pipeline is rerun.

Take a look at [Joel Nitta’s](https://twitter.com/joel_nitta) [presentation](https://www.youtube.com/watch?v=XMvinGSG72k) at an [AsiaR meetup](https://hackmd.io/8HzieKHoSEKLUoQRm9fBYg?view) for a decent introduction and demonstration of the \[targets\]((https://docs.ropensci.org/targets/) R package

Now it is able to have the option to **keep records** of historical data outputs instead of overwriting a previous output with a recent new one as a result of changes in the analysis pipeline.

Two methods were shared to capture version-controlled snapshots of the data store. One is by using a version-aware cloud storage such as [Amazon S3](https://aws.amazon.com/s3/) the other is by using Git, both with the help of the [gittargets](https://docs.ropensci.org/gittargets/).

With the snapshots recorded, the \[targets\]((https://docs.ropensci.org/targets/) workflow is able to recover the pre-processing data that correspond to a **previous** git branch or commit. Thus, should the user needs to roll back the analysis pipeline to a previous stage, it will take less time to rerun the updated code as the set of pre-processing results are updated accordingly.

-   📝[Slides](https://wlandau.github.io/user-conf-2022/)

### bulkAnalyseR: An Interactive Pipeline For Analysing And Sharing Bulk Sequencing Results

The following talk was on [bulkAnalyseR](https://core-bioinformatics.github.io/bulkAnalyseR/) by [Ilias Moutsopoulos](https://github.com/emouts) from the [Cambridge Stem Cell Institute Core Bioinformatics Group](https://github.com/Core-Bioinformatics)

If you are new to bulk sequencing data, take a look at this introductory YouTube [video](https://www.youtube.com/watch?v=bMf1cnttuPk) first.

[bulkAnalyseR](https://core-bioinformatics.github.io/bulkAnalyseR/) ensures analysis of single- and multi-omics bulk-sequencing data follows a certain preprocessing pipeline smoothly and display the results in an interactive [R Shiny](https://shiny.rstudio.com/) application. The analysis pipeline is flexible for users’ to analyse a combination of other sequencing data set like mRNAseq, ChIPseq, sRNAseq/microRNAs.

The results are then distributed online via the [shinyapps.io](https://www.shinyapps.io/) platform. Results includes quality check heatmap, similarity heatmap, principal component analysis scatter plots, volcano plots, gene regulatory networks and so on. Here is the [link](http://bioinf.stemcells.cam.ac.uk:3838/bulkAnalyseR/) of some of bulkAnalyseR results if you are interested.

### R-Ladies Nairobi During COVID-19 Pandemic

After two talks from Big Data Management, I switched to another session Building the R Community 1 for a less technical presentation.

I managed to catch up with the presentation by [Njoki Lucy](https://twitter.com/lucy_njokinjuki) and [Shel Kariuki](https://twitter.com/shel_kariuki) on their story of trying to build [R-Ladies Nairobi](https://twitter.com/rladiesnairobi) during the COVID-19 pandemic.

Despite the challenges faced, they managed to host several [meetings](https://www.youtube.com/channel/UCRth2ImB1T-_saYc5YBTcyA/videos) and even collaborated with the [Nairobi R User Group](https://www.meetup.com/nairobi-r-users-group/) to conduct an R conference called [satRday Nairobi 2021](https://www.youtube.com/hashtag/satrdaynairobi). The slides for all [R-Ladies Nairobi](https://twitter.com/rladiesnairobi) meetings can be found in this [Github page](https://github.com/rladies/meetup-presentations_nairobi).

It is heart warming and encouraging to see their strong passion and desire in community building even though the work can be exhausting and the rewards may be little. Do support the team by attending their meetings and if you can’t attend, do at least share it to someone else.

-   📝[Slides](https://github.com/rladies/meetup-presentations_nairobi/tree/master/useR!%202022%20-%20Regular%20Talk)

### Dev Containers For Easy R Tutorials

The following talk I had attended was provided by [David Smith](https://twitter.com/revodavid), I was thrilled to see the use of [Dev Containers](https://containers.dev/) in [Github Codespaces](https://github.com/features/codespaces) to create interactive R tutorials for teaching. One real life example is this [Microsoft workshop](https://docs.microsoft.com/en-us/learn/paths/machine-learning-with-r/) titled “Create machine learning models with R and tidymodels”.

To my knowledge, I have seen interactive R Tutorials implemented in two ways. One is by [learnR](https://rstudio.github.io/learnr/), for example [A Quick Flight to the Edge of the Tidyverse](https://www.allisonhorst.com/talk/rladies_tunis_saudiarabia_tidyverse_intro/) conducted by Allison Horst in a combined [R-Ladies Tunis](https://twitter.com/rladiestunis) and [R-Ladies Dammam](https://twitter.com/rladiesdammam?lang=en) Workshop. The other is by [Google Colaboratory](https://colab.research.google.com/), for example [Introduction to ggplot2](https://github.com/kuanhoong/ggplot2_workshop) conducted by Kuan Hoong in Malaysia’s [R confeRence 2021](https://www.r-conference.com/).

Seeing more and more options to create interactive R Tutorials definitely will empower more teachers to be able to teach R in more interesting and engaging ways.

Here is a [Github](https://github.com/revodavid/devcontainers-r) introduction of what [Dev Containers](https://containers.dev/) in Github Codespaces is about. (Video introduction may come soon.)

Unfortunately, creating such tutorials are currently only possible with a GitHub Enterprise or GitHub Education account. Hopefully, it could be extended to a personal Github account in the future.

-   📝[Slides](https://github.com/revodavid/devcontainers-r/blob/main/EasyRTutorialsUseR2022.pdf)

### Speed Networking Session

This was my first time attending a speed networking session actually. I had to admit it could be scary to meet someone new in the web. The fact that each meetup lasted for three minutes added to my anxiety. There were times when I started talking only to be realised that I was muted when the other person told me that they can’t hear me. Nevertheless, I managed to get the hang of it halfway and started to feel more comfortable and confident in introducing myself. I had to say the process was quite fruitful for me. I managed to meet new people from Europe and Australia passionate about R and made some connections on Linkedin.

### Converting R function To C++ Function With ast2ast

After the short break from the speed networking session, I attended the session on Containerization and Metaprogramming.

In some cases when optimisation of code running time is necessary, there may be a need to rewrite an R function in a faster programming language like C++. However, as C++ is not an easy programming language to learn, a lot of time and effort is required in this rewriting process. I recall learning C++ on my first year as an undergraduate. It was a tough journey. I usually create infinite loops by mistake and crash the program frequently. Memory management using C++ pointers was a nightmare.

To speed up the rewriting process, [Krämer Konrad](https://twitter.com/kraemer_konrad) introduced the R package [ast2ast](https://github.com/Konrad1991/ast2ast) which is able to convert some simple R function into C++ function automatically, minimising the need for the user to type [Rcpp](https://www.rcpp.org/) related function and C++ code.

I have to say it sounded like magic. I thought it was too good to be truth and slapped my face with both hands like [Naruto](https://twitter.com/abdul_s17/status/1193855247850053634) to check if I was dreaming instead of watching the conference in the middle of the night. However, the session proceeded to the Q and A asking if [ast2ast](https://github.com/Konrad1991/ast2ast) could translate functions from non standard libraries like the [magrittr pipe](https://magrittr.tidyverse.org/reference/pipe.html) and probability density functions. Guess I was not sleeping and agreed with the host that [ast2ast](https://github.com/Konrad1991/ast2ast) had a lot of potential.

### Modeling Marine Ecosystem With gadget3

Marine ecosystem models are needed to better understand the impacts of human related activities and natural events, such as overfishing, pollution and climate change, on the marine food web. Such models are needed for state holders to make wiser decisions and evaluate existing policies meant to protect our marine environment.

The issue is that most of these open source computationally intensive modeling tools are implemented in C++ and lack integration for other programming languages and modern tools to contribute. Thus, [Jamie Lentin](https://github.com/lentinj) shared about how his team managed to bridge this gap for the [Gadget model](https://heima.hafro.is/~bthe/introduction.html) using [gadget3](https://github.com/gadget-framework/gadget3) and other R packages in the [gadget-framework](https://github.com/gadget-framework).

I am afraid that this is all I can share due to my limited understanding in this kind of analysis. While this marine ecology is something that I don’t know much, it is amazing to see how much progress has been made made into this field of research since the UN proclaimed 2021–2030 as the [Decade of Ocean Science for Sustainable Development](https://www.oceandecade.org/)

### Docker For Data Science And Shiny Apps

The talks in relation to Containerization were about [Docker](https://www.docker.com/), so I have summarised both talks in this section.

Today, more research data publications use [Docker](https://www.docker.com/) as a means for others to reproduce the results and graphs created in the published journal paper. Recently, they are also applied on open source web applications as well.

If what I am writing may sound Greek to you, may I suggest [Alex Gold’s](https://twitter.com/alexkgold?lang=en) introductory [talk](https://github.com/akgold/docker4ds) on Docker. In addition, the speaker is also working on an [e-book](https://do4ds.com/) titled DevOps for Data Science. Do give him your support.

For those who are familiar with Docker, [Peter Solymos](https://twitter.com/psolymos) had shared some valuable [advice](https://my.visme.co/view/90rqk0kg-user-2022-talk-shiny-docker) on when and how to apply Docker on [R Shiny](https://shiny.rstudio.com/) Apps. More of such resources can be found in this Hosting Data Apps’ [post](https://hosting.analythium.io/user-2022-best-practicesfor-shiny-apps-with-docker-and-more/).

-   📝[Alex’s Slides](https://github.com/akgold/docker4ds)
-   📝[Peter’s Slides](https://my.visme.co/view/90rqk0kg-user-2022-talk-shiny-docker)

### Second Keynote: How Tools Shape Thinking About Graphics

The second keynote was by [Amanda Cox](https://mobile.twitter.com/amandacox), a well-known American journalist now working in a non-profit organisation [USAFacts](https://usafacts.org/).

In the past when people ask her what tools were used to make great graphics, her response waw used to be “it does not really matters” as great graphics usually depended on how well it communicate its message to the readers rather than how it was made. Her perspective changed when she started her new job and begin to look for people to work for her. During the hiring process as she was looking at portfolios, she realised that she was able to identify which tools were used (this graph looked like it had been made using [reactjs](https://reactjs.org/) but the overall structure was inspired from R related plots) and understand what programming skills the candidate may potentially possess. For example, graphics that showed small multiple plots arranged neatly in a grid squares gave a higher probability that it was inspired from R.
As she started to reflect on why she was able to identify the tools used to make a certain graphic so easily, she started to see that the tools used did restrict or enhance what information could be highlight from the visual graphics, affecting how well it communicated its message to the readers. For example, in this New York Times’ graphics on [Olympics sprinter](http://archive.nytimes.com/www.nytimes.com/interactive/2012/08/05/sports/olympics/the-100-meter-dash-one-race-every-medalist-ever.html), the sound at the end to emphasise the difference in speed between 19-century sprinter and 2012 is three seconds was made using R. R was used at that time because it was the only tool that the team coul find that was able to produce a decent soundtrack that complimented the video at a tight deadline schedule.

She then shared some case studies in which R was the right tool to use and others that were not. Based on what I can understand, here were some of the cases.

One example in which the team felt that R was the right tool to use was when there was a need to report [statistical uncertainty](https://raw.githubusercontent.com/m1arc00/m1arc00.github.io/master/useR/fla5.png) (approximate answers) of the US election voting results over time. The team was grateful that R was able to simulate practice data set for the team to learn how to make such a report in advanced before applying it on the actual data.

On the other hand, graphics needing animation (movement) are harder to implement using R like [The New Science of Sentencing](https://www.themarshallproject.org/2015/08/04/the-new-science-of-sentencing) and [Extensive Data Shows Punishing Reach of Racism for Black Boys](https://www.nytimes.com/interactive/2018/03/19/upshot/race-class-white-and-black-men.html).
For interactive visualisations that is able to provide constant feedback (mimicking a real person) based on the readers’ input of expected data, such as [You Draw It: How Family Income Predicts Children’s College Chances](https://www.nytimes.com/interactive/2015/05/28/upshot/you-draw-it-how-family-income-affects-childrens-college-chances.html), R also still has a long way to go.

Amanda also shared her difficulties in using R to make annotations/labelling in a static graph even though it was simple to do the same thing in other visual making software. She then showed a few examples on the usefulness of annotations like this New York Times’ report [One Report, Diverging Perspectives](https://archive.nytimes.com/www.nytimes.com/interactive/2012/10/05/business/economy/one-report-diverging-perspectives.html). This was something that I fully agree. They were a few times that I had to resolve to Powerpoint after making a plot in R because I did not know how to create a label at the correct place. Resources like Cara Thompson’s [post]((https://www.cararthompson.com/talks/user2022)) on how to make polished annotations in R were truly like gem mines.

Nevertheless, Amanda concluded that despite all these limitations in R for visualisation based on her understanding, it still remained subjective and personal as it depended how much people were willing to push themselves to make effective visuals given the amount of tools and resources that they had. One of the last few examples that she showed was [Coasterplots](https://www.tylermw.com/datacoaster-tycoon/) made by [Tyler Morgan-Wall](https://twitter.com/tylermorganwall). It was an eye-opening experience for me to see how 3D visualisation plots can be viewed in such a unique way using R.

## Conclusion

That marks the end of the first part of this post. Stay tune for a write up on Day 3 and 4.
