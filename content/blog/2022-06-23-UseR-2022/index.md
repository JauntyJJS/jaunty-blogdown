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

### Poster Presentation

#### renderthis

I first entered the Dissemination of Information room because I was curious about the [`renderthis`](https://jhelvy.github.io/renderthis/) presented by [John Paul Helveston](https://twitter.com/JohnHelveston). It was formally called `xaringanBuilder`, one of the extension of [`Xaringan`](https://github.com/yihui/xaringan). For those who are new to `Xaringan`, it is an alternative way to create presentation slides in html. A decent quick start guide can be found in Silvia Canelón’s blog post [Deploying xaringan Slides with GitHub Pages](https://www.silviacanelon.com/blog/2021-deploying-xaringan-slides/). Here is a link to the [Xaringan gallery](https://xaringan.gallery/) for other examples. To my knowledge, the other extension packages are [`xaringanthemer`](https://pkg.garrickadenbuie.com/xaringanthemer/) and [`xaringanExtra`](https://pkg.garrickadenbuie.com/xaringanExtra/).

It is eye opening to see how many different ways `Xaringan` slides can be converted to using `renderthis`. It goes from the usual html file, pdf file to even png images. Currently, I was following the instructions in Garrick Aden-Buie’s blog post [Printing xaringan slides with chromote](https://www.garrickadenbuie.com/blog/print-xaringan-chromote/) to output the `Xaringan` slides into pdf. Maybe I should try to see if I can do the same with `renderthis`. With `renderthis`, users can also specify which `Xaringan` slides to be converted to. Future work involves able to output the `Xaringan` slides as a Micosoft Powerpoint [3 slides per page handout](https://answers.microsoft.com/en-us/msoffice/forum/all/how-do-i-save-a-powerpoint-presentation-with/e93ec638-8ad1-4002-8c1c-78cc90f097a6).

#### animate

I jumped to Data Visualisation room later after that.

I was looking forward for the presentation on the R package [`animate`](https://kcf-jackson.github.io/animate/index.html) by Jackson Kwok. You see, I was reading the poster in Micosoft Powerpoint beforehand and my jaws dropped when I see that the animation featured in this article titled [The New Science of Sentencing](https://www.themarshallproject.org/2015/08/04/the-new-science-of-sentencing) could be replicated using R. While reading the documentation of `animate`, I found out Jackson also made some `Xaringan` [slides](https://rawcdn.githack.com/kcf-jackson/animate/0f3e8211f063e832b3b83288b4834329d491f4da/man/slides/SVI_presentation.html) introducing the R package `animate`. Do take a look if you need a more visual information. Unfortunately, when I entered the virtual longue. It just ended…

#### Polished annotations

Putting this aside, the next presentation was by [Cara Thompson](https://twitter.com/cararthompson) sharing useful tips and trick to make polished annotations in `ggplot`. Making annotations in `ggplot` has always been really challenging for me. I usually spend a lot of time tweaking fixed parameters to move the annotations from one place to another. Most of the time I just gave up and use Microsoft Powerpoint to add these extra text boxes. Cara’s success in finding several clever strategies to make polished annotations, using `ggtext`, `glue`, CSS formatting and a filtered tibble with unique arrow curvature information, does makes me smile. Her tips can also be found in this [talk post](https://www.cararthompson.com/talks/user2022). One of her blog post [Alignment cheatsheet](https://www.cararthompson.com/posts/2021-09-02-alignment-cheat-sheet/) may be useful for those who need a little help on the alignment parameters.

#### Two-Sample Corrgram

The last presentation in the Data Visualisation room is by Rohan Tummala. This visualisation is a unique way to optimise the correlation results of dichotomous data within the space of a 2D heatmap matrix. More information can be found in this [project webpage](https://rithikatummala8.wixsite.com/sigmaxisrs2021/).

It definitely has a lot of potential to be improved by the R community. Here are my “5-cent” suggestions. The team may wish to use the R package [`correlation`](https://easystats.github.io/correlation/) from the [easystats](https://easystats.github.io/easystats/) team, to expand their current correlation methods of Pearson, Kendall and Spearman. As for the question raised on extending the static plot to multichotomous data (or k-sample corrgram), one idea I can think of currently is to adopt the [scatter plot matrix](http://www.sthda.com/english/wiki/scatter-plot-matrices-r-base-graphs) style where the diagonal are the groups and the scatter plots are replaced with the two sample corrgrams instead. However, this in turn creates the same redundant space which the two-sample corrgram is supposed to prevent. Regardless, if this visualisation continue to receive good feedback, someone will create an interactive two-sample corrgram and push it as a web tool.

#### R in Production

I next entered the R in Production room where I am first introduced to the R package [`pacs`]((https://polkas.github.io/pacs/)) by [Maciej Nasinski](https://github.com/polkas). It contains a set of useful utility functions for helping R package developers life easier such as, automating validation of a [`renv`](https://rstudio.github.io/renv/articles/renv.html) lock file, finding out packages which are not from CRAN and many more. More information can be found in its [documentation](https://polkas.github.io/pacs/).

The second sharing is from Konrad Oberwimmer who introduced the R package [`svgtools`](https://cran.r-project.org/web/packages/svgtools/index.html) that is able to key in statistical results onto charts template made in [SVG file format](https://commons.wikimedia.org/wiki/Template:SVG_Chart). This is helpful if there is a need to create graphs that needs to follow a certain layout based on corporate needs.

The next showcase is about `data.validator`(https://appsilon.github.io/data.validator/) by [Marcin Dubel](https://twitter.com/DubelMarcin). Honestly, this is an R package that I wish I knew earlier how to use it. While it is great to have tools that validate the data but it is even better when a validation report, highlighting the possible issues of a given dataset clearly and explicitly, can be created and distributed to others. `data.validator` not only uses [`assertr`](https://github.com/ropensci/assertr) to do the validation but is able to create an interactive report in html as well. More details can also be found in this [youtube video](https://www.youtube.com/watch?v=U1-j7c_8LFQ) as well as this [R-bloggers post](https://www.r-bloggers.com/2022/05/data-cleaning-in-r-2-r-packages-to-clean-and-validate-datasets/)

Lastly, it is a workflow presented by [Cody Marquart](https://twitter.com/cody_marquart) on how to manage R packages automatically using [GitLab](https://about.gitlab.com/) Continuous Integration (CI). [GitLab CI](https://docs.gitlab.com/ee/ci/introduction/index.html#continuous-integration) was first introduced from an [April 2020 GitLab meetup](https://www.youtube.com/watch?v=l5705U8s_nQ&t=397s). It is nice to know that CI is possible to be applied on R packages management in GitLab. Usually, CI was done using [Github Actions](https://github.com/features/actions) from [Github](https://github.com/) because of many [useful resources](https://github.com/r-lib/actions) available to help users create CI tasks easily. Thus, [Github Actions](https://github.com/features/actions) became a popular choice for R package management. Nevertheless, as it is unwise not to have a backup plan, being aware of that an alternative workflow exists is critical. Take a look at one of GitLab CI examples used in the R package [`shinyLogger`](https://gitlab.com/clmarquart/shinyLogger/-/blob/main/.gitlab-ci.yml)
Hopefully, I will get to witness a similar workflow for managing R packages in [Bitbucket](https://bitbucket.org/product/) in the future.

### Clinical Data Review Reporting Tool

Day 3 for me was filled with many sessions that I was interested in like Data Visualization, Publishing and Reproducibility as well as Web Frameworks. Unfortunately, I could not join all at the same time. After some thoughts, I had decided to attend the session on Publishing and Reproducibility.

The first talk was from Laure Cougnaud from [OpenAnalytics](https://www.openanalytics.eu) introducing an R package [`clinDataReview`](https://cran.r-project.org/web/packages/clinDataReview/index.html) used to provide a medical report in [`bookdown`](https://bookdown.org/), filled with interactive plots to understand how patients are doing during a clinical study. An example of this report can be found in this [link](https://medical-monitoring.openanalytics.io/) The report is created as a folder of mainly HTML (and [other](https://cran.r-project.org/web/packages/clinDataReview/vignettes/clinDataReview-reporting.html)) files which is then distributed to the clinicians. The key to making this possible is the use of a standard template report in R markdown as well as a configuration file in YAML for users to set specific parameters to make the report customisable and flexible to their needs.

I was first introduced to Rmarkdown report templates during my attendance in the RStudio Conference 2020 at San Francisco. It was presented by [Sharla Gelfand](https://twitter.com/sharlagelfand) titled [Don’t repeat yourself, talk to yourself! Reporting with R](https://www.youtube.com/watch?v=JThd3YYQXGg&ab_channel=RStudio). I highly recommend watching as it is really down to Earth and funny at the same time. Sharla also provided a [blog post](https://sharla.party/post/usethis-for-reporting/) showing step by step how to produce an introductory R package with Rmarkdown report templates. The work done by Laure Cougnaud and her team is bringing this workflow to the next level by extending from Rmarkdown to `bookdown` reports. Definitely a job well done.

### knitr engines and blogdown troubleshooting

The next talk is by [Christophe Dervieux](https://twitter.com/chrisderv) giving a [introductory tour](https://cderv.rbind.io/talk/2022-user-knitr-engines/) on the different [`knitr`](https://github.com/yihui/knitr) engines. The `knitr` engines can be listed in R using the command `names(knitr::knit_engines$get())`. More information of commonly used engines can be found in the \[Rmarkdown e-book\](https://bookdown.org/yihui/rmarkdown/language-engines.html. The talk also introduced the latest `knitr` engine called `exec` which allow command lines to be executed in the Rmarkdown code chunk. The talk also inform users how to create custom `knitr` engines as well. One major takeaway for me on this talk is the that there is actually a [Github link](https://github.com/yihui/knitr-examples) showing Rmarkdown examples of many different `knitr` engine, including the latest `exec` engine found [here](https://github.com/yihui/knitr-examples/blob/master/124-exec-engine.Rmd).

After enjoying the tour on `knitr` engines, the session proceeds with [Yihui Xie](https://twitter.com/xieyihui) sharing some [helpful summary](https://yihui.org/en/2022/06/user-blogdown/) on how to create a blog using [`blogdown`](https://pkgs.rstudio.com/blogdown/) with minimal issues using `blogdown::serve_site()` and `blogdown::check_site()`. Hopefully the `blogdown::check_site()` could be part of the RStudio Addins for `blogdown` in the future.

For me, I started to learn how to create this [Hugo Apéro](https://hugo-apero-docs.netlify.app/) theme `blogdown` site from watching a YouTube video of a [lesson](https://www.youtube.com/watch?v=RksaNh5Ywbo&ab_channel=R-LadiesTunis) conducted by Alison Hill’s in R Ladies Tunis. However, if a two hours lesson is too long, may I direct you to Alison Hill’s [Day 09: Hugo Apéro from scratch \|\| rmarkdown + blogdown + Netlify](https://www.youtube.com/watch?v=yXFu_upDL2o&ab_channel=AlisonHill) from the \#12DaysOfDusting [series](https://www.youtube.com/playlist?list=PLzxicn7kBeazI9Niimsth81iWn4mvCmu0) instead.

### Reliable Scientific Software Development

The last

### Clinical Data Review

\[https://twitter.com/M_Steinhilber\]
\[https://twitter.com/janithcwanni\]
[Using R to Create Reproducible Engineering Test Reports](https://www.youtube.com/watch?v=9GmXuOi4nhk&list=PL9HYL-VRX0oTL2P7FK3854-X6kfLTb4fJ&index=33)

## Conclusion

## References
