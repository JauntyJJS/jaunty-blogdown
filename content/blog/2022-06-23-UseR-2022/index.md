---
title: "Reflections on useR! 2022 Conference"
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

## Introduction to Dimensional Reduction in R

The course was conducted by [Isabella](https://twitter.com/bisnotforbella). The materials can be found in this [Github page](https://github.com/bellabf/dimensional-reduction).

I personally enjoyed this course as it is not too technical with equations and the pace is just right with sufficient breaks. The instructor also goes the extra mile to create polls to interact with us and check if we are doing fine during the course.

Besides learning to use different dimension reduction techniques using base R, I was also lightly introduced to the use of [Tidymodels](https://www.tidymodels.org/) to do Principal Component Analysis ([PCA](https://recipes.tidymodels.org/reference/step_pca.html) ) as well as [reticulate](https://rstudio.github.io/reticulate/) to run T-distributed Stochastic Neighbor Embedding ([tSNE](https://scikit-learn.org/stable/modules/generated/sklearn.manifold.TSNE.html) ) using [Python](https://www.python.org/).

## Regression Modeling Strategies

It is heart warming to be able to attend a course conducted by a well-known biostatistician, [Frank Harrell](https://twitter.com/f2harrell) from Vanderbilt University.

I first saw his presentation [R for Graphical Clinical Trial Reporting](https://www.youtube.com/watch?v=4gXWQxaBbac) during the RStudio Conference 2020 at San Francisco. Here is the [abstract](https://www.fharrell.com/talk/rstudio20/) for this talk. I was touched by his desire and passion to always learn new things in R. This talk was one of the key morale booster for me to learn [plotly](https://plotly.com/r/) even though its documentation can be quite intimidating.I only got aware of his popularity when I saw him again presenting again at the Why R? 2020 as a keynote speaker titled [Controversies in Predictive Modeling, Machine Learning, and Validation](https://www.youtube.com/watch?v=DF1WsYZ94Es)

In summary, the course was mainly a short summary of his ebook [Regression Modeling Strategies](https://hbiostat.org/rms/) as well as a short introduction of his new ebook [R Workflow](https://hbiostat.org/rflow/) written in [Quarto](https://quarto.org/).

There are indeed a lot of useful information and it takes some time for me to digest, understand and reflect.

## Day 2

### Speed Networking Session

The event that will stick to my mind for a long time is the speed networking session. This is my first time attending one actually. I have to admit it can be scary to meet someone new in the web. The fact that each meetup lasts for three minutes adds to my anxiety. There are times when I started talking only to be realised that I was muted when the other person tells me that they can’t hear me. Nevertheless, I managed to get the hang of it halfway and started to feel more comfortable and confident in introducing myself. I have to say it is quite fruitful for me. I managed to meet new people from Europe and Australia passionate about R and made some connections on Linkedin.

### gittargets

As for the talks, I get to view the latest development on the R package [`targets`](https://docs.ropensci.org/targets/) from [The R Targetopia](https://wlandau.github.io/targetopia/) created by [Will Landau](https://twitter.com/wmlandau). `targets` is known to keep a record of pre-processing results in a data analysis pipeline so that it knows when it is able to skip tasks when data analysis pipeline is rerun.

Take a look at [Joel Nitta’s](https://twitter.com/joel_nitta) [presentation](https://www.youtube.com/watch?v=XMvinGSG72k) at an [AsiaR meetup](https://hackmd.io/8HzieKHoSEKLUoQRm9fBYg?view) for a decent introduction and demonstration of the `targets` R package

Now it is able to have the option to **keep records** of historical data outputs instead of overwriting a previous output with a recent new one as a result of changes in the analysis pipeline. Two methods were shared to capture version-controlled snapshots of the data store. One is by using a version-aware cloud storage such as [Amazon S3](https://aws.amazon.com/s3/) the other is with the help of the R package [`gittargets`](https://docs.ropensci.org/gittargets/).

With the snapshots recorded, the `targets` workflow is able to recover the pre-processing data that correspond to a **precious** git branch or commit. Thus, should the user needs to roll back the analysis pipeline to a previous stage, it will take less time to rerun the updated code as the set of pre-processing results are updated accordingly.

### Dev Containers for Easy R Tutorials

Another talk that excites me is the one provided by [David Smith](https://twitter.com/revodavid/status/1539256109722222592?cxt=HHwWgIC-5djRxNwqAAAA), I was thrilled to see the use of [`Dev Containers`](https://containers.dev/) in [Github Codespaces](https://github.com/features/codespaces) to create interactive R tutorials for teaching. One real life example is this [Microsoft workshop](https://docs.microsoft.com/en-us/learn/paths/machine-learning-with-r/) titled “Create machine learning models with R and tidymodels”.

To my knowledge, I have seen interactive R Tutorials implemented in two ways. One is by [learnR](https://rstudio.github.io/learnr/), for example [A Quick Flight to the Edge of the Tidyverse](https://www.allisonhorst.com/talk/rladies_tunis_saudiarabia_tidyverse_intro/) conducted by Allison Horst in a combined [R-Ladies Tunis](https://twitter.com/rladiestunis) and [R-Ladies Dammam](https://twitter.com/rladiesdammam?lang=en) Workshop. The other is by [Google Colaboratory](https://colab.research.google.com/), for example [Introduction to ggplot2](https://github.com/kuanhoong/ggplot2_workshop) conducted by Kuan Hoong in Malaysia’s [R confeRence 2021](https://www.r-conference.com/).

Seeing more and more options to create interactive R Tutorials definitely will empower more teachers to be able to teach R in more interesting and engaging ways.

Here is a [Github](https://github.com/revodavid/devcontainers-r) introduction of what `Dev Containers` in Github Codespaces is about. (Video introduction may come soon.)

Unfortunately, creating such tutorials are currently only possible with a GitHub Enterprise or GitHub Education account. Hopefully, it could be extended to a personal Github account in the future.

### Docker for Data Science and Shiny Apps

Today, more research data publications use [Docker](https://www.docker.com/) as a means for others to reproduce the results and graphs created in the published journal paper. Recently, they are also applied on open source web applications as well.

If what I am writing may sound Greek to you, may I suggest [Alex Gold’s](https://twitter.com/alexkgold?lang=en) introductory [talk](https://github.com/akgold/docker4ds) on Docker. In addition, the speaker is also working on an [ebook](https://do4ds.com/) titled DevOps for Data Science. Do give him your support.

For those who are familiar with Docker, [Peter Solymos](https://twitter.com/psolymos) has shared some valuable [advice](https://my.visme.co/view/90rqk0kg-user-2022-talk-shiny-docker) on when and how to apply Docker on [R Shiny](https://shiny.rstudio.com/) Apps. More of such resources can be found in this Hosting Data Apps [webpage](https://hosting.analythium.io/).

## Day 3

Day 3 for me was filled with many sessions that I was interested in like Data Visualization, Publishing and Reproducibility and Web Frameworks as well as the poster presentations. Unfortunately, I could not join all at the same time but here is what I have attended.

### Speed Networking Session

### Clinical Data Review

\[https://twitter.com/M_Steinhilber\]
\[https://twitter.com/janithcwanni\]

## Conclusion

## References
