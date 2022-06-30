---
title: "Journey and Reflections on useR! 2022 Conference"
subtitle: ""
excerpt: "This post is a write up on my learning journey in the useR! 2022 Conference."
date: 2022-06-23
author: "Jeremy Selva"
draft: true
images:
series:
tags:
categories:
layout: single-sidebar
editor_options: 
  chunk_output_type: console
bibliography: utils/bibliography.bib
csl: utils/f1000research.csl
---

## Introduction

The useR! 2022 Virtual Conference is a great opportunity for me to learn new things about R as well as to meet new people along the way.

Here is a list of things that inspire me to be a better programmer and analyst.

## Day 1

I have attended two workshops this year titled Introduction to Dimensional Reduction in R and Regression Modeling Strategies.

### Introduction to Dimensional Reduction in R

The course was conducted by [Isabella Bicalho-Frazeto](https://twitter.com/bisnotforbella). The materials can be found in this [Github page](https://github.com/bellabf/dimensional-reduction).

I personally enjoyed this course as it is not too technical with equations and the pace is just right with sufficient breaks. The instructor also goes the extra mile to create polls to interact with us and check if we are doing fine during the course.

Besides learning to use different dimension reduction techniques using base R, I was also lightly introduced to the use of [Tidymodels](https://www.tidymodels.org/) to do Principal Component Analysis ([PCA](https://recipes.tidymodels.org/reference/step_pca.html) ) as well as [reticulate](https://rstudio.github.io/reticulate/) to run T-distributed Stochastic Neighbor Embedding ([tSNE](https://scikit-learn.org/stable/modules/generated/sklearn.manifold.TSNE.html) ) using [Python](https://www.python.org/).

### Regression Modeling Strategies

It is heart warming to be able to attend a course conducted by a well-known biostatistician, [Frank Harrell](https://twitter.com/f2harrell) from Vanderbilt University.

I first saw his presentation [R for Graphical Clinical Trial Reporting](https://www.youtube.com/watch?v=4gXWQxaBbac) during the RStudio Conference 2020 at San Francisco. Here is the [abstract](https://www.fharrell.com/talk/rstudio20/) for this talk. I was touched by his desire and passion to always learn new things in R. This talk was one of the key morale booster for me to learn [plotly](https://plotly.com/r/) even though its documentation can be quite intimidating.I only got aware of his popularity when I saw him again presenting again at the Why R? 2020 as a keynote speaker titled [Controversies in Predictive Modeling, Machine Learning, and Validation](https://www.youtube.com/watch?v=DF1WsYZ94Es).

In summary, the course was mainly a short summary of his ebook [Regression Modeling Strategies](https://hbiostat.org/rms/) as well as a short introduction of his new e-book [R Workflow](https://hbiostat.org/rflow/) written in [Quarto](https://quarto.org/).

There are indeed a lot of useful information and it takes some time for me to digest, understand and reflect.

## Day 2

### First Keynote

The first keynote in Day 2 of the conference is by [Paula Moraga](https://twitter.com/Paula_Moraga), author of the e-book [Geospatial Health Data: Modeling and Visualization with R-INLA and Shiny](https://www.paulamoraga.com/book-geospatial/).

Even though I am not working with geospatial data, the content from the talk is very resourceful for those who has just started using R and geospatial analysis in general. It is the type of information I wish I had when I first begin to learn about R.

It started with a brief summary of a generic geospatial analysis workflow followed by some real life applications to highlight some challenges faced. Lots of visual examples were used to keep the audience glued to the talk. The presenter also shared how one can start learning geospatial analysis by using open data from [rspatialdata](https://rspatialdata.github.io/) and useful R packages analytical tools like [SpatialEpiApp](https://github.com/Paula-Moraga/SpatialEpiApp) and [epiflows](https://www.repidemicsconsortium.org/epiflows/). R packages from the [R Epidemics Consortium](http://www.repidemicsconsortium.org) were something new to me as well.

The section on communication and dissemination provides a good overview of different R packages used to display and distribute results to others. A gentle introduction of [ggplot2](https://ggplot2.tidyverse.org/), [htmlwidgets](http://gallery.htmlwidgets.org/), [R Markdown](https://rmarkdown.rstudio.com/), [flexdashboard](https://pkgs.rstudio.com/flexdashboard/), [Shiny](https://shiny.rstudio.com/) were mentioned, without being too technical on the code. The presenter also highlighted some R communities ([R Ladies](https://rladies.org/), [R Forwards](https://forwards.github.io/)) for those new to R to be able to seek help or improve themselves.

Overall, I recommended this keynote for those who wants to know more about R and what it can provide.

### Speed Networking Session

The event that will stick to my mind for a long time is the speed networking session. This is my first time attending one actually. I have to admit it can be scary to meet someone new in the web. The fact that each meetup lasts for three minutes adds to my anxiety. There are times when I started talking only to be realised that I was muted when the other person tells me that they can’t hear me. Nevertheless, I managed to get the hang of it halfway and started to feel more comfortable and confident in introducing myself. I have to say it is quite fruitful for me. I managed to meet new people from Europe and Australia passionate about R and made some connections on Linkedin.

### gittargets for better data version control

As for the sessions, I first attended the first two talks from Big Data Management followed by next two talks from Building the R Community 1.

In the first talk, I get to view the latest development on the R package [targets](https://docs.ropensci.org/targets/) from [The R Targetopia](https://wlandau.github.io/targetopia/) created by [Will Landau](https://twitter.com/wmlandau). \[targets\]((https://docs.ropensci.org/targets/) is known to keep a record of pre-processing results in a data analysis pipeline so that it knows when it is able to skip tasks when data analysis pipeline is rerun.

Take a look at [Joel Nitta’s](https://twitter.com/joel_nitta) [presentation](https://www.youtube.com/watch?v=XMvinGSG72k) at an [AsiaR meetup](https://hackmd.io/8HzieKHoSEKLUoQRm9fBYg?view) for a decent introduction and demonstration of the \[targets\]((https://docs.ropensci.org/targets/) R package

Now it is able to have the option to **keep records** of historical data outputs instead of overwriting a previous output with a recent new one as a result of changes in the analysis pipeline. Two methods were shared to capture version-controlled snapshots of the data store. One is by using a version-aware cloud storage such as [Amazon S3](https://aws.amazon.com/s3/) the other is by using Git, both with the help of the [gittargets](https://docs.ropensci.org/gittargets/).

With the snapshots recorded, the \[targets\]((https://docs.ropensci.org/targets/) workflow is able to recover the pre-processing data that correspond to a **previous** git branch or commit. Thus, should the user needs to roll back the analysis pipeline to a previous stage, it will take less time to rerun the updated code as the set of pre-processing results are updated accordingly.

### An interactive pipeline for analysing and sharing bulk sequencing results

The following talk is on [bulkAnalyseR](https://core-bioinformatics.github.io/bulkAnalyseR/) by [Ilias Moutsopoulos](https://github.com/emouts) from the [Cambridge Stem Cell Institute Core Bioinformatics Group](https://github.com/Core-Bioinformatics)

If you are new to bulk sequencing data, take a look at this introductory YouTube [video](https://www.youtube.com/watch?v=bMf1cnttuPk) first.

[bulkAnalyseR](https://core-bioinformatics.github.io/bulkAnalyseR/) ensures analysis of single- and multi-omics bulk-sequencing data follows a certain preprocessing pipeline smoothly and display the results in an interactive [R Shiny](https://shiny.rstudio.com/) application. The analysis pipeline is flexible for users’ to analyse a combination of other sequencing data set like mRNAseq, ChIPseq, sRNAseq/microRNAs.

The results are then distributed online via the [shinyapps.io](https://www.shinyapps.io/) platform. Results includes quality check heatmap, similarity heatmap, principal component analysis scatter plots, volcano plots, gene regulatory networks and so on. Here is the [link](http://bioinf.stemcells.cam.ac.uk:3838/bulkAnalyseR/) of some of bulkAnalyseR results if you are interested.

### R-Ladies Nairobi during COVID-19 pandemic

After two talks from Big Data Management, I switched to another session Building the R Community 1 for a less technical presentation.

I managed to catch up with the presentation by [Njoki Lucy](https://twitter.com/lucy_njokinjuki) and [Shel Kariuki](https://twitter.com/shel_kariuki) on their story of trying to build [R-Ladies Nairobi](https://twitter.com/rladiesnairobi) during the COVID-19 pandemic.

Despite the challenges faced, they managed to host several [meetings](https://www.youtube.com/channel/UCRth2ImB1T-_saYc5YBTcyA/videos) and even collaborated with the [Nairobi R User Group](https://www.meetup.com/nairobi-r-users-group/) to conduct an R conference called [satRday Nairobi 2021](https://www.youtube.com/hashtag/satrdaynairobi). The slides for all [R-Ladies Nairobi](https://twitter.com/rladiesnairobi) meetings can be found in this [Github page](https://github.com/rladies/meetup-presentations_nairobi).

It is heart warming and encouraging to see their strong passion and desire in community building even though the work can be exhausting and the rewards may be little. Do support the team by attending their meetings and if you can’t attend, do at least share it to someone else.

### Dev Containers for Easy R Tutorials

The following talk I have attended is provided by [David Smith](https://twitter.com/revodavid), I was thrilled to see the use of [Dev Containers](https://containers.dev/) in [Github Codespaces](https://github.com/features/codespaces) to create interactive R tutorials for teaching. One real life example is this [Microsoft workshop](https://docs.microsoft.com/en-us/learn/paths/machine-learning-with-r/) titled “Create machine learning models with R and tidymodels”.

To my knowledge, I have seen interactive R Tutorials implemented in two ways. One is by [learnR](https://rstudio.github.io/learnr/), for example [A Quick Flight to the Edge of the Tidyverse](https://www.allisonhorst.com/talk/rladies_tunis_saudiarabia_tidyverse_intro/) conducted by Allison Horst in a combined [R-Ladies Tunis](https://twitter.com/rladiestunis) and [R-Ladies Dammam](https://twitter.com/rladiesdammam?lang=en) Workshop. The other is by [Google Colaboratory](https://colab.research.google.com/), for example [Introduction to ggplot2](https://github.com/kuanhoong/ggplot2_workshop) conducted by Kuan Hoong in Malaysia’s [R confeRence 2021](https://www.r-conference.com/).

Seeing more and more options to create interactive R Tutorials definitely will empower more teachers to be able to teach R in more interesting and engaging ways.

Here is a [Github](https://github.com/revodavid/devcontainers-r) introduction of what [Dev Containers](https://containers.dev/) in Github Codespaces is about. (Video introduction may come soon.)

Unfortunately, creating such tutorials are currently only possible with a GitHub Enterprise or GitHub Education account. Hopefully, it could be extended to a personal Github account in the future.

### Converting R function to C++ function and back with ast2ast

After the second keynote of the day, I attended the session on Containerization and Metaprogramming.

In some cases when optimisation of code running time is necessary, there may be a need to rewrite an R function in a faster programming language like C++. However, as C++ is not an easy programming language to learn, a lot of time and effort is required in this rewriting process. I recall learning C++ on my first year as an undergraduate. It was a tough journey. I usually create infinite loops by mistake and crash the program frequently. Memory management using C++ pointers was a nightmare.

To speed up the rewriting process, [Krämer Konrad](https://twitter.com/kraemer_konrad) introduced the R package [ast2ast](https://github.com/Konrad1991/ast2ast) which is able to convert some simple R function into C++ function automatically, minimising the need for the user to type [Rcpp](https://www.rcpp.org/) related function and C++ code.

I have to say it sounds like magic. I thought it was too good to be truth and slapped my face with both hands like [Naruto](https://twitter.com/abdul_s17/status/1193855247850053634) to check if I was dreaming instead of watching the conference in the middle of the night. However, the session proceeded to the Q and A asking if [ast2ast](https://github.com/Konrad1991/ast2ast) can translate functions from non standard libraries like the [magrittr pipe](https://magrittr.tidyverse.org/reference/pipe.html) and probability density functions. Guess I am not sleeping and agreed with the host that [ast2ast](https://github.com/Konrad1991/ast2ast) has a lot of potential.

### Modeling marine ecosystem with gadget3

Marine ecosystem models are needed to better understand the impacts of human related activities and natural events, such as overfishing, pollution and climate change, on the marine food web. Such models are needed for state holders to make wiser decisions and evaluate existing policies meant to protect our marine environment.

The issue is that most of these open source computationally intensive modeling tools are implemented in C++ and lack integration for other programming languages and modern tools to contribute. Thus, [Jamie Lentin](https://github.com/lentinj) shared about how his team managed to bridge this gap for the [Gadget model](https://heima.hafro.is/~bthe/introduction.html) using [gadget3](https://github.com/gadget-framework/gadget3) and other R packages in the [gadget-framework](https://github.com/gadget-framework).

I am afraid that this is all I can share due to my limited understanding in this kind of analysis. While this marine ecology is something that I don’t know much, it is amazing to see how much progress has been made made into this field of research since the UN proclaimed 2021–2030 as the [Decade of Ocean Science for Sustainable Development](https://www.oceandecade.org/)

### Docker for Data Science and Shiny Apps

The talks in relation to Containerization were about [Docker](https://www.docker.com/), so I have summarised both talks in this section.

Today, more research data publications use [Docker](https://www.docker.com/) as a means for others to reproduce the results and graphs created in the published journal paper. Recently, they are also applied on open source web applications as well.

If what I am writing may sound Greek to you, may I suggest [Alex Gold’s](https://twitter.com/alexkgold?lang=en) introductory [talk](https://github.com/akgold/docker4ds) on Docker. In addition, the speaker is also working on an [e-book](https://do4ds.com/) titled DevOps for Data Science. Do give him your support.

For those who are familiar with Docker, [Peter Solymos](https://twitter.com/psolymos) has shared some valuable [advice](https://my.visme.co/view/90rqk0kg-user-2022-talk-shiny-docker) on when and how to apply Docker on [R Shiny](https://shiny.rstudio.com/) Apps. More of such resources can be found in this Hosting Data Apps [webpage](https://hosting.analythium.io/).

### Second Keynote

The second keynote is by [Amanda Cox](https://mobile.twitter.com/amandacox), a well-known American journalist now working in a non-profit organisation [USAFacts](https://usafacts.org/).

In the past when people ask her what tools were used to make great graphics, her response were used to be “it does not really matters” as great graphics usually depends on how well it communicate its message to the readers rather than how it is made. Her perspective changes when she started her new job and begin to look for people to work for her. During the hiring process as she was looking at portfolios, she realised that she was able to identify which tools were used (this graph looks like it has been made using [reactjs](https://reactjs.org/) but the overall structure is inspired from R related plots) and understand what programming skills the candidate may potentially possess. For example, graphics that shows small multiple plots arranged neatly in a grid squares give a higher probability that it is inspired from R.

As she started to reflect on why she was able to identify the tools used to make a certain graphic so easily, she started to see that the tools used does restrict or enhance what information can be highlight from the visual graphics, affecting how well it communicate its message to the readers. For example, in this New York Times’ graphics on [Olympics sprinter](http://archive.nytimes.com/www.nytimes.com/interactive/2012/08/05/sports/olympics/the-100-meter-dash-one-race-every-medalist-ever.html), the sound at the end to emphasise the difference in speed between 19-century sprinter and 2012 is three seconds is made using R. R was used at that time because it was the only tool that the team can find that is able to produce a decent soundtrack that compliments the video at a tight deadline schedule.

She then shared some case studies in which R was the right tool to use and others that were not. Based on what I can understand, here are some of the cases.

One example in which R was the right tool to use is when there is a need to report [statistical uncertainty](https://raw.githubusercontent.com/m1arc00/m1arc00.github.io/master/useR/fla5.png) (approximate answers) of the US election voting results over time. The team was grateful that R was able to simulate practice data set for the team to learn how to make such a report in advanced before applying it on the actual data.

On the other hand, graphics needing animation (movement) are harder to implement using R like [The New Science of Sentencing](https://www.themarshallproject.org/2015/08/04/the-new-science-of-sentencing) and [Extensive Data Shows Punishing Reach of Racism for Black Boys](https://www.nytimes.com/interactive/2018/03/19/upshot/race-class-white-and-black-men.html).
For interactive visualisations that is able to provide constant feedback (mimicking a real person) based on the readers’ input of expected data, such as [You Draw It: How Family Income Predicts Children’s College Chances](https://www.nytimes.com/interactive/2015/05/28/upshot/you-draw-it-how-family-income-affects-childrens-college-chances.html), R also still has a long way to go.

Amanda also shared her difficulties in using R to make annotations/labelling in a static graph even though it is simple to do the same thing in other visual making software. She then show a few examples on how annotations are useful like this New York Times’ report [One Report, Diverging Perspectives](https://archive.nytimes.com/www.nytimes.com/interactive/2012/10/05/business/economy/one-report-diverging-perspectives.html). This is something that I fully agree. They are a few times that I had to resolve to Powerpoint after making a plot in R because I do not know how to create a label at the correct place. Resources like Cara Thompson’s [post]((https://www.cararthompson.com/talks/user2022)) on how to make polished annotations in R are truly like gem mines.

Nevertheless, Amanda concludes that despite all these limitations in R for visualisation based on her understanding, it still remains subjective and personal as it depends how much people are willing to push themselves to make effective visuals given the amount of tools and resources that they have. One of the last few examples that she showed was [Coasterplots](https://www.tylermw.com/datacoaster-tycoon/) made by [Tyler Morgan-Wall](https://twitter.com/tylermorganwall). It was an eye-opening experience for me to see how 3D visualisation plots can be viewed in such a unique way using R.

## Day 3

### First Keynote

The first keynote is by the [afrimapr](https://afrimapr.github.io/afrimapr.website/) project team. The project aims is to use R as a building block for many things such as better management of data realted to Africa, creation of open source analytical tools to analyse and provide insights across Africa, providing teaching resources and training for those interested in this novel work and building a strong community with this common interest.

[Anelda van der Walt](https://twitter.com/aneldavdw) shared the progress the team have made since it was first launched in 2020 such as [R packages](https://afrimapr.github.io/afrimapr.website/code/), [interactive apps](https://afrimapr.github.io/afrimapr.website/interactive-apps/), [teaching materials](https://afrimapr.github.io/afrimapr.website/training/) and even [publications of data](https://afrimapr.github.io/afrimapr.website/publications/) in journals.

The next phase of the talk was a sharing from [Clinton Nkolokosa](https://twitter.com/clintymw) about his experiences as a geospatial researcher doing projects such as [malaria incident](https://rpubs.com/Clinty/786191), [flood incidence](https://nkolokosa.shinyapps.io/FloodMapper/) and [covid 19 cases](https://rpubs.com/Clinty/705819). Such meaningful accomplishments were hard to obtain as he highlighted the challenges faced such as difficulties in getting up-to-date data (Clinton ended up having to update the data on his own) and finding local talented people (R gurus) doing similar work for help and consultation due to lack of funding and opportunities. He stressed the importance of more individuals from the African R community to step out of their comfort zones and be drivers of innovative ideas and resources.

The following phase of the keynote is mainly focus on effective teaching. [Anne Treasure](https://twitter.com/annemtreasure) presented the usefulness of [learnr](https://rstudio.github.io/learnr/) to create [online tutorials](https://afrimapr.github.io/afrilearnr/) to support novice learners of R. She then showed how the team goes one step further by making these material more accessible such as

-   Teaching them in French, besides English.
-   Use of [RStudio Cloud](https://rstudio.cloud/) so that more people can participate on the courses simultaneously.
-   Making materials downloadable for local use.
-   Pre and post course survey to understand the attendee’s concern for improvement of future teaching sessions.

[Nono Gueye](https://twitter.com/gueyenono) then showed how having teaching resources in other language such as French can benefit more people in multilingual Africa and gave some existing R resources in French such as [tidyverse](https://juba.github.io/tidyverse/index.html).

The last phase of the keynote is about the status of R communities in Africa. Anelda showed some statistics that the R communities in Africa when compared to North America is not doing as well with a significantly lower number of active groups and organised events. This implies that the knowledge transmission of R from one individual to another in Africa is quite low. Anelda then gave a few reasons to explain why it is hard to build and sustain an R community. One reason is that building one requires a lot of skills and hard work which is daunting if the organising team just have a few people. Another reason is that the people who build such communities are mainly volunteers who may be overburdened by work and/or family commitments to run regular events. Low participate rate in such organised event does bring a mental toll on the organisers as well. The last reason is a lack of funding and resources.

The keynote concluded first by appealing to the African R community to support more new R users locally, collaborate locally and internationally and try to experiment new established approaches to see if it helps or not. It then appeal towards the global (funding) community to find ways to reward people for their time to run events, invest more in multilingual materials as well as to identify and support locally-led, custom-developed initiatives that works in emerging regions.

### Poster Presentation

#### renderthis

I first entered the Dissemination of Information room because I was curious about the [renderthis](https://jhelvy.github.io/renderthis/) presented by [John Paul Helveston](https://twitter.com/JohnHelveston). It was formally called xaringanBuilder, one of the extension of [Xaringan](https://github.com/yihui/xaringan). For those who are new to [Xaringan](https://github.com/yihui/xaringan), it is an alternative way to create presentation slides in html. A decent quick start guide can be found in Silvia Canelón’s blog post [Deploying xaringan Slides with GitHub Pages](https://www.silviacanelon.com/blog/2021-deploying-xaringan-slides/). Here is a link to the [Xaringan gallery](https://xaringan.gallery/) for other examples. To my knowledge, the other extension packages are [xaringanthemer](https://pkg.garrickadenbuie.com/xaringanthemer/) and [xaringanExtra](https://pkg.garrickadenbuie.com/xaringanExtra/).

It is eye opening to see how many different ways [Xaringan](https://github.com/yihui/xaringan) slides can be converted to using [renderthis](https://jhelvy.github.io/renderthis/). It goes from the usual html file, pdf file to even png images. Currently, I was following the instructions in Garrick Aden-Buie’s blog post [Printing xaringan slides with chromote](https://www.garrickadenbuie.com/blog/print-xaringan-chromote/) to output the [Xaringan](https://github.com/yihui/xaringan) slides into pdf. Maybe I should try to see if I can do the same with [renderthis](https://jhelvy.github.io/renderthis/). With [renderthis](https://jhelvy.github.io/renderthis/), users can also specify which [Xaringan](https://github.com/yihui/xaringan) slides to be converted to. Future work involves able to output the [Xaringan](https://github.com/yihui/xaringan) slides as a Micosoft Powerpoint [3 slides per page handout](https://answers.microsoft.com/en-us/msoffice/forum/all/how-do-i-save-a-powerpoint-presentation-with/e93ec638-8ad1-4002-8c1c-78cc90f097a6).

#### animate

I jumped to Data Visualisation room later after that.

I was looking forward for the presentation on the R package [animate](https://kcf-jackson.github.io/animate/index.html) by Jackson Kwok. You see, I was reading the poster in Micosoft Powerpoint beforehand and my jaws dropped when I see that the animation featured in this article titled [The New Science of Sentencing](https://www.themarshallproject.org/2015/08/04/the-new-science-of-sentencing) could be replicated using R. While reading the documentation of [animate](https://kcf-jackson.github.io/animate/index.html), I found out Jackson also made some [Xaringan](https://github.com/yihui/xaringan) [slides](https://rawcdn.githack.com/kcf-jackson/animate/0f3e8211f063e832b3b83288b4834329d491f4da/man/slides/SVI_presentation.html) introducing the R package [animate](https://kcf-jackson.github.io/animate/index.html). Do take a look if you need a more visual information. Unfortunately, when I entered the virtual longue. It just ended…

#### Polished annotations

Putting this aside, the next presentation was by [Cara Thompson](https://twitter.com/cararthompson) sharing useful tips and trick to make polished annotations in [ggplot](https://ggplot2.tidyverse.org/index.html). Making annotations in [ggplot](https://ggplot2.tidyverse.org/index.html) has always been really challenging for me. I usually spend a lot of time tweaking fixed parameters to move the annotations from one place to another. Most of the time I just gave up and use Microsoft Powerpoint to add these extra text boxes. Cara’s success in finding several clever strategies to make polished annotations, using [ggtext](https://wilkelab.org/ggtext/), [glue](https://glue.tidyverse.org/), CSS formatting and a filtered tibble with unique arrow curvature information, does makes me smile. Her tips can also be found in this [talk post](https://www.cararthompson.com/talks/user2022). One of her blog post [Alignment cheatsheet](https://www.cararthompson.com/posts/2021-09-02-alignment-cheat-sheet/) may be useful for those who need a little help on the alignment parameters.

#### Two-Sample Corrgram

The last presentation in the Data Visualisation room is by Rohan Tummala. This visualisation is a unique way to optimise the correlation results of dichotomous data within the space of a 2D heatmap matrix. More information can be found in this [project webpage](https://rithikatummala8.wixsite.com/sigmaxisrs2021/).

It definitely has a lot of potential to be improved by the R community. Here are my “5-cent” suggestions. The team may wish to use the R package [correlation](https://easystats.github.io/correlation/) from the [easystats](https://easystats.github.io/easystats/) team, to expand their current correlation methods of Pearson, Kendall and Spearman. As for the question raised on extending the static plot to multichotomous data (or k-sample corrgram), one idea I can think of currently is to adopt the [scatter plot matrix](http://www.sthda.com/english/wiki/scatter-plot-matrices-r-base-graphs) style where the diagonal are the groups and the scatter plots are replaced with the two sample corrgrams instead. However, this in turn creates the same redundant space which the two-sample corrgram is supposed to prevent. Regardless, if this visualisation continue to receive good feedback, someone will create an interactive two-sample corrgram and push it as a web tool.

#### R in Production

I next entered the R in Production room where I am first introduced to the R package [pacs]((https://polkas.github.io/pacs/)) by [Maciej Nasinski](https://github.com/polkas). It contains a set of useful utility functions for helping R package developers life easier such as, automating validation of a [renv](https://rstudio.github.io/renv/articles/renv.html) lock file, finding out packages which are not from CRAN and many more. More information can be found in its [documentation](https://polkas.github.io/pacs/).

The second sharing is from Konrad Oberwimmer who introduced the R package [`svgtools`](https://cran.r-project.org/web/packages/svgtools/index.html) that is able to key in statistical results onto charts template made in [SVG file format](https://commons.wikimedia.org/wiki/Template:SVG_Chart). This is helpful if there is a need to create graphs that needs to follow a certain layout based on corporate needs.

The next showcase is about [data.validator](https://appsilon.github.io/data.validator/) by [Marcin Dubel](https://twitter.com/DubelMarcin). Honestly, this is an R package that I wish I knew earlier how to use it. While it is great to have tools that validate the data but it is even better when a validation report, highlighting the possible issues of a given dataset clearly and explicitly, can be created and distributed to others. [data.validator](https://appsilon.github.io/data.validator/) not only uses [assertr](https://github.com/ropensci/assertr) to do the validation but is able to create an interactive report in html as well. More details can also be found in this [youtube video](https://www.youtube.com/watch?v=U1-j7c_8LFQ) as well as this [R-bloggers post](https://www.r-bloggers.com/2022/05/data-cleaning-in-r-2-r-packages-to-clean-and-validate-datasets/)

Lastly, it is a workflow presented by [Cody Marquart](https://twitter.com/cody_marquart) on how to manage R packages automatically using [GitLab](https://about.gitlab.com/) Continuous Integration (CI). [GitLab CI](https://docs.gitlab.com/ee/ci/introduction/index.html#continuous-integration) was first introduced from an [April 2020 GitLab meetup](https://www.youtube.com/watch?v=l5705U8s_nQ&t=397s). It is nice to know that CI is possible to be applied on R packages management in GitLab. Usually, CI was done using [Github Actions](https://github.com/features/actions) from [Github](https://github.com/) because of many [useful resources](https://github.com/r-lib/actions) available to help users create CI tasks easily. Thus, [Github Actions](https://github.com/features/actions) became a popular choice for R package management. Nevertheless, as it is unwise not to have a backup plan, being aware of that an alternative workflow exists is critical. Take a look at one of GitLab CI examples used in the R package [shinyLogger](https://gitlab.com/clmarquart/shinyLogger/-/blob/main/.gitlab-ci.yml)
Hopefully, I will get to witness a similar workflow for managing R packages in [Bitbucket](https://bitbucket.org/product/) in the future.

### Clinical Data Review Reporting Tool

Day 3 for me was filled with many sessions that I was interested in like Data Visualization, Publishing and Reproducibility as well as Web Frameworks. Unfortunately, I could not join all at the same time. After some thoughts, I had decided to attend the session on Publishing and Reproducibility.

The first talk was from Laure Cougnaud from [OpenAnalytics](https://www.openanalytics.eu) introducing an R package [clinDataReview](https://cran.r-project.org/web/packages/clinDataReview/index.html) used to provide a medical report in [bookdown](https://bookdown.org/), filled with interactive plots to understand how patients are doing during a clinical study. An example of this report can be found in this [link](https://medical-monitoring.openanalytics.io/) The report is created as a folder of mainly HTML (and [other](https://cran.r-project.org/web/packages/clinDataReview/vignettes/clinDataReview-reporting.html)) files which is then distributed to the clinicians. The key to making this possible is the use of a standard template report in R markdown as well as a configuration file in YAML for users to set specific parameters to make the report customisable and flexible to their needs.

I was first introduced to Rmarkdown report templates during my attendance in the RStudio Conference 2020 at San Francisco. It was presented by [Sharla Gelfand](https://twitter.com/sharlagelfand) titled [Don’t repeat yourself, talk to yourself! Reporting with R](https://www.youtube.com/watch?v=JThd3YYQXGg&ab_channel=RStudio). I highly recommend watching as it is really down to Earth and funny at the same time. Sharla also provided a [blog post](https://sharla.party/post/usethis-for-reporting/) showing step by step how to produce an introductory R package with Rmarkdown report templates. The work done by Laure Cougnaud and her team is bringing this workflow to the next level by extending from Rmarkdown to [bookdown](https://bookdown.org/) reports. Definitely a job well done.

### knitr engines and blogdown troubleshooting

The next talk is by [Christophe Dervieux](https://twitter.com/chrisderv) giving a [introductory tour](https://cderv.rbind.io/talk/2022-user-knitr-engines/) on the different [knitr](https://github.com/yihui/knitr) engines. The [knitr](https://github.com/yihui/knitr) engines can be listed in R using the command `names(knitr::knit_engines$get())`. More information of commonly used engines can be found in the \[Rmarkdown e-book\](https://bookdown.org/yihui/rmarkdown/language-engines.html. The talk also introduced the latest [`knitr`](https://github.com/yihui/knitr) engine called `exec` which allow command lines to be executed in the Rmarkdown code chunk. The talk also inform users how to create custom [knitr](https://github.com/yihui/knitr) engines as well. One major takeaway for me on this talk is the that there is actually a [Github link](https://github.com/yihui/knitr-examples) showing Rmarkdown examples of many different [knitr](https://github.com/yihui/knitr) engine, including the latest `exec` engine found [here](https://github.com/yihui/knitr-examples/blob/master/124-exec-engine.Rmd).

After enjoying the tour on [knitr](https://github.com/yihui/knitr) engines, the session proceeds with [Yihui Xie](https://twitter.com/xieyihui) sharing some [helpful summary](https://yihui.org/en/2022/06/user-blogdown/) on how to create a blog using [blogdown](https://pkgs.rstudio.com/blogdown/) with minimal issues using `blogdown::serve_site()` and `blogdown::check_site()`. Hopefully the `blogdown::check_site()` could be part of the RStudio Addins for [blogdown](https://pkgs.rstudio.com/blogdown/) in the future.

For me, I started to learn how to create this [Hugo Apéro](https://hugo-apero-docs.netlify.app/) theme [blogdown](https://pkgs.rstudio.com/blogdown/) site from watching a YouTube video of a [lesson](https://www.youtube.com/watch?v=RksaNh5Ywbo&ab_channel=R-LadiesTunis) conducted by Alison Hill’s in R Ladies Tunis. However, if a two hours lesson is too long, may I direct you to Alison Hill’s [Day 09: Hugo Apéro from scratch \|\| rmarkdown + blogdown + Netlify](https://www.youtube.com/watch?v=yXFu_upDL2o&ab_channel=AlisonHill) from the \#12DaysOfDusting [series](https://www.youtube.com/playlist?list=PLzxicn7kBeazI9Niimsth81iWn4mvCmu0) instead.

### Reliable Scientific Software Development

The last presentation of this session is by [Meike Steinhilber](https://twitter.com/M_Steinhilber), developer of the R packages [sprtt](https://meikesteinhilber.github.io/sprtt/)(Sequential Probability Ratio Tests Using The Associated t-statistic) and its Shiny counterpart [sprit](https://meike-steinhilber.shinyapps.io/spirit/). The [talk](https://www.dropbox.com/s/dv80062qo0rbhd3/useR_MeikeSteinhilber_2022_V2.pdf?dl=0) focuses on ways to develop reliable scientific software using some best practices for software development.

In summary, the best practices are having clean and refactored code, software testing, continuous integration, version control and extended documentation. Examples used were from her R package [sprtt](https://meikesteinhilber.github.io/sprtt/). This is great advice for someone who has just started to have many long R scripts and wish to make them more manageable and sustainable. As this is also the speaker’s [first conference presentation](https://twitter.com/M_Steinhilber/status/1539705226319564802?cxt=HHwWhMC4mdzvkN4qAAAA), do show her some love and support if you like the presentation.

This presentation gives me a nostalgia feeling as I have [presented](https://jeremy-selva.netlify.app/talk/2021-10-29-pydata-global-2021/) something similar in the [PyData Global 2021](https://pydata.org/global2021/) conference using a Python-made software [MSOrganiser](https://github.com/SLINGhub/MSOrganiser) as an example. That conference was also my first as well. Instead of reliability, the focus of my presentation however was tips to make the software more user friendly, less intimidating for new users and ways to deal with the angry ones as well.

### Clinical Data Review

\[https://twitter.com/M_Steinhilber\]
\[https://twitter.com/janithcwanni\]
[Using R to Create Reproducible Engineering Test Reports](https://www.youtube.com/watch?v=9GmXuOi4nhk&list=PL9HYL-VRX0oTL2P7FK3854-X6kfLTb4fJ&index=33)

## Day 4

For Day 4,

After the keynote session, I attended the first two talks in the Package Development session followed by the last two talks in Building the R Community 2.

### Package dependencies

The first talk on Package Development is from [Zuguang Gu](https://twitter.com/jokergoo_gu), developer of many packages such as [ComplexHeatmap](https://github.com/jokergoo/ComplexHeatmap) and [spiralize](https://github.com/jokergoo/spiralize). The presentation is about an R package called [pkgndep](https://jokergoo.github.io/pkgndep/) used to calculate the dependency heaviness of an R package and display the results in a heatmap.

When developing R packages, it is advisable to keep it [lightweight](https://tinyverse.netlify.app/) (depend on a low number of external R packages). This is mainly to allow users to install R packages easily by reducing the chances of failure due to an unsuccessful dependency installation. Thus, [pkgndep](https://jokergoo.github.io/pkgndep/) is helpful for R package developers who wish to optimise their R package dependencies.

This is kind of similar to the R package [dstr](https://github.com/falo0/dstr). The difference is that [pkgndep](https://jokergoo.github.io/pkgndep/) provides a more detailed result in a heatmap rather than a network graph. On the other hand, [dstr](https://github.com/falo0/dstr) provides clearer advise to the R developers on what they can do next to reduce the dependencies. Perhaps, the teams of [pkgndep](https://jokergoo.github.io/pkgndep/) and [dstr](https://github.com/falo0/dstr) can collaborate and build on each other strengths to further improve on the usefulness of their current creations.

### pre-commits

The second talk conducted by [Lorenz Walthert](https://twitter.com/lorenzwalthert) is an eye-opener for me as I am unfamiliar with git pre-commit hooks. From my understanding, pre-commit hooks are widely used for Python developers due to the availability of of the Python package [pre-commit](https://pre-commit.com/) to do all the heavy lifting.
Motivated by how useful git pre-commit hooks are in improving code quality, Lorenz created a R package [precommit](https://lorenzwalthert.github.io/precommit/index.html) in hopes that more R package developers are able to adapt this workflow easily.

### Transitioning to R

After the second talk, I jumped to the session on Building the R Community 2. Luckily, this time when I got in, the third talk of the session has just begun. It was a presentation by [Kieran Martin](https://twitter.com/kjmartinstats) from [Roche](https://twitter.com/Roche). I have watched a previous R Consortium conducted by his team before in YouTube titled [Package Management at Roche]((https://www.youtube.com/watch?v=A8ePOTOSGg0&ab_channel=RConsortium)) and find it very informative and educational.

It is delightful to see him again presenting for useR! 2022. This time Kieran shared his experience on his large Product Development team’s ongoing journey to using R as one of the core data science tool, when there is a need to report results of clinical trials in the most efficient way. Best practices were shared like using [Docker](https://www.docker.com/) to fix the operating system, [renv](https://rstudio.github.io/renv/index.html) and internal package repositories to control the R packages used and the [R Validation Hub](https://www.pharmar.org/) to validate R packages. He also provided some useful advice and mistakes to avoid to help people grow into R.

What is very touching is their desire in conjunction with like-minded pharmaceutical companies to create a shared set of high quality R packages for clinical reporting related analysis, plotting table and graphs via the [pharmaverse](https://pharmaverse.org/) and [Insights Engineering](https://github.com/insightsengineering). At least we do not have to see multiple R packages solving the same problem. Definitely something great to look into.

### Reflections of a Research Software Engineer

This is followed by a presentation by [Nicholas Tierney](https://twitter.com/nj_tierney), a [research software engineer](https://researchsoftware.org/) at the [Telethon Kids Institute](https://www.telethonkids.org.au/). Nicholas is also the developer of the two data visualisation R packages [visdat](https://docs.ropensci.org/visdat/) and [naniar](https://naniar.njtierney.com/index.html).

The talk is consist of three parts: what kind of work he does as a \[research software engineer\]((https://researchsoftware.org/), a small summary of how he tries to maintain the [greta](https://greta-stats.org/) R package (as part of his job scope) and the future of [research software engineer](https://researchsoftware.org/) in Australia.

I do gain some useful knowledge in package management such as creating better snapshot test, efficient pull request using `pr_feteh` and `pr_finish` from the [usethis](https://usethis.r-lib.org/reference/pull-requests.html) R package and using [glue](https://glue.tidyverse.org/) to make better command line messages to users.

Despite being busy with his research software engineer role, Nicholas is also active in the [rOpenSci Social Coworking and Office Hours](https://ropensci.org/events/coworking-2022-06/) (Asia Pacific Edition) helping people with R related issues. It is actually from this online event when I first met him. He is really a nice and approachable R enthusiast.

### Synthetic Data Generation

Honestly the last set of sessions was another hard choice for me as it covers topics that I am unfamiliar with. I took a leap of faith and attended the session on Synthetic Data and Text Analysis.

The first talk is about a small introduction of the [simPop](https://github.com/statistikat/simPop) R package by Alexander Kowarik. It is an R package used to create synthetic data. Synthetic data generation is useful when there is a need to transform sensitive but complex original data to into privacy-compliant data that still retains the complex structure of the original data. The transformed data can then be used for train machine learning models, software testing and simulation studies. This is actually my first time getting to know about synthetic data and what it is used for. I am grateful for the speaker for giving such a clear presentation for me to understand.

### textrecipes to improve preprocessing of textual data

The second one switches to the topic of Text Analysis with the R package [textrecipes](https://textrecipes.tidymodels.org/). It is presented by [Emil Hvitfeldt](https://twitter.com/Emil_Hvitfeldt) one of the authors of the e-book [Supervised Machine Learning for Test Analysis in R](https://smltar.com/). While I am new to text data analysis, I am able to understand the unique properties of such dataset and why is it so hard to transform such a dataset into meaningful numbers that a machine learning model can use to learn. The presentation then shows step by step how [textrecipes](https://textrecipes.tidymodels.org/) is able to make this transformation process less painful and yet flexible to user’s different needs.

As someone who has attended a [book club](https://www.youtube.com/watch?v=cXjTKOoN6aU&list=PL3x6DOfs2NGisLSs09v1NQUQaxuE8nbOO) on [An Introduction to Statistical Learning with Applications in R](https://www.statlearning.com/)(ISLR) conducted by the [R4DS Online Learning Community](https://www.rfordatasci.com/), Emil’s [ISLR tidymodels Labs](https://emilhvitfeldt.github.io/ISLR-tidymodels-labs/index.html) notes have been very helpful to our cohort group’s learning journey to use [tidymodels](https://www.tidymodels.org/) to better understand some of the statistical learning methods.

### Bivariate Data Generation using Scagnostics

The next presentation is led by [Janith Wanniarachchi](https://mobile.twitter.com/janithcwanni) regarding his R package called [scatteR](https://github.com/janithwanni/scatteR). [scatteR](https://github.com/janithwanni/scatteR) is used to generate a bivariate data set based on a given [scagnostics](https://en.wikipedia.org/wiki/Scagnostics) measurement.

I enjoyed the flow of the presentation as it is like telling a story. The protagonist who faced a stumbling block along the way managed to overcome it after being inspired by ice-cream sprinkles. I won’t spoil the plot any further.

Janith is another [first time](https://mobile.twitter.com/janithcwanni/status/1540053289089519616?cxt=HHwWgMDS9dGTr98qAAAA) presenter at an international conference. Do show him your support if you like his presentation.

### Making better forecasting models by integrating sentiment analysis with topic modeling of textual data.

The last talk of the session is quite hard for me to understand because I am unfamiliar with textual data analysis as mentioned before. Nevertheless, to the best of my knowledge, I try to explain what is going on.

Oliver Delmarcelle shows how the R package [sentopics](https://github.com/odelmarcelle/sentopics) can be used to integrating sentiment analysis and topic modeling of textual data to potentially make better forecasting models. In this presentation, the [press conferences](https://www.ecb.europa.eu/press/key/html/index.en.html) documents of the European Central Bank is used as an example.

If you are unfamiliar with the term topic modeling and sentiment analysis, take a look at these two Youtube videos by [Julia Silge](https://twitter.com/juliasilge)
[Data Centric Inc.](https://www.datacentriccorp.com/) to know what they are.

-   [Topic modeling with R and tidy data principles](https://www.youtube.com/watch?v=evTuL-RcRpc)
-   [A Tutorial on Sentiment Analysis in R](https://www.youtube.com/watch?v=c7YSyCofH3o)

The [press conferences](https://www.ecb.europa.eu/press/key/html/index.en.html) documents of the European Central Bank are first grouped into different dominant topics/themes, like inflation, economic growth and so on. Separately, sentiment analysis is applied on the [press conferences](https://www.ecb.europa.eu/press/key/html/index.en.html) documents to obtain two sentiment time series data, the sentiment of the Economic Condition and Monetary Policy over time.

With that, two forecasting models were constructed to see which one better predict the [European Central Bank’s decision](https://www.ecb.europa.eu/press/govcdec/html/index.en.html) on the interest rate and monthly targets of the asset purchase program. They ar a forecasting model using only the two sentiment predictors (Economic Condition and Monetary Policy) and another one with an additional topic-specific sentiment predictor. The result shows that the additional topic-specific sentiment predictor improves the forecasting model.

In addition, Oliver also showed how [sentopics](https://github.com/odelmarcelle/sentopics) is able to create time series plots showing how each topic/theme contributed to the sentiment of the Economic Condition.

## Conclusion

## References
