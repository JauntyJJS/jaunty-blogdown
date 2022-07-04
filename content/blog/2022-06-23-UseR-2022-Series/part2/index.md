---
title: "Learning Journey and Reflections on useR! 2022 Conference Part 2"
subtitle: ""
excerpt: "This narrative is a write up on Day 3 of my learning journey in the [useR! 2022 Conference](https://user2022.r-project.org/)."
date: 2022-07-01
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
---



## Introduction

In this narrative, I will continue sharing my learning journey during Day 3 of [useR! 2022 Virtual Conference](https://user2022.r-project.org/).

## Day 3

### First Keynote: afrimapr

The first keynote was by the [afrimapr](https://afrimapr.github.io/afrimapr.website/) project team. The project aims is to use R as a building block for many things such as better management of data realted to Africa, creation of open source analytical tools to analyse and provide insights across Africa, providing teaching resources and training for those interested in this novel work and building a strong community with this common interest.

[Anelda van der Walt](https://twitter.com/aneldavdw) shared the progress the team had made since it was first launched in 2020 such as [R packages](https://afrimapr.github.io/afrimapr.website/code/), [interactive apps](https://afrimapr.github.io/afrimapr.website/interactive-apps/), [teaching materials](https://afrimapr.github.io/afrimapr.website/training/) and even [publications of data](https://afrimapr.github.io/afrimapr.website/publications/) in journals.

The next phase of the talk was a sharing from [Clinton Nkolokosa](https://twitter.com/clintymw) about his experiences as a geospatial researcher doing projects such as [malaria incident](https://rpubs.com/Clinty/786191), [flood incidence](https://nkolokosa.shinyapps.io/FloodMapper/) and [covid 19 cases](https://rpubs.com/Clinty/705819). Such meaningful accomplishments were hard to obtain as he highlighted the challenges faced such as difficulties in getting up-to-date data (Clinton ended up having to update the data on his own) and finding local talented people (R gurus) doing similar work for help and consultation due to lack of funding and opportunities. He stressed the importance of more individuals from the African R community to step out of their comfort zones and be drivers of innovative ideas and resources.  

The following phase of the keynote was mainly focus on effective teaching. [Anne Treasure](https://twitter.com/annemtreasure) presented the usefulness of [learnr](https://rstudio.github.io/learnr/) to create [online tutorials](https://afrimapr.github.io/afrilearnr/) to support novice learners of R. She then showed how the team went one step further by making these material more accessible such as 

* Teaching them in French, besides English.
* Use of [RStudio Cloud](https://rstudio.cloud/) so that more people could participate on the courses simultaneously.
* Making materials downloadable for local use.
* Pre and post course survey to understand the attendee's concern for improvement of future teaching sessions.

[Nono Gueye](https://twitter.com/gueyenono) then showed how having teaching resources in other language such as French can benefit more people in multilingual Africa and gave some existing R resources in French such as [tidyverse](https://juba.github.io/tidyverse/index.html).

The last phase of the keynote was about the status of R communities in Africa. Anelda showed some statistics that the R communities in Africa when compared to North America was not doing as well with a significantly lower number of active groups and organised events. This implied that the knowledge transmission of R from one individual to another in Africa was quite low. 

Anelda then gave a few reasons to explain why it was hard to build and sustain an R community. One reason was that building one requires a lot of skills and hard work which was daunting if the organising team just have a few people. Another reason was that the people who built such communities were mainly volunteers who may be overburdened by work and/or family commitments to run regular events. Low participate rate in such organised event did bring a mental toll on the organisers as well. The last reason was a lack of funding and resources.

The keynote concluded first by appealing to the African R community to support more new R users locally, collaborate locally and internationally and try to experiment new established approaches to see if it helped or not. It then appealed towards the global (funding) community to find ways to reward people for their time to run events, invest more in multilingual materials as well as to identify and support locally-led, custom-developed initiatives that worked in emerging regions. 

* 📝[Slides](https://docs.google.com/presentation/d/1ResuITjWSs6shKT0wtyyWzR1llTIu-t4cOcPh1BsIII/edit#slide=id.g131a1a79661_0_0)

### Poster Presentation

#### renderthis

I first entered the Dissemination of Information room because I was curious about the [renderthis](https://jhelvy.github.io/renderthis/) presented by [John Paul Helveston](https://twitter.com/JohnHelveston). It was formally called xaringanBuilder, one of the extension of [Xaringan](https://github.com/yihui/xaringan). 

For those who are new to [Xaringan](https://github.com/yihui/xaringan), it is an alternative way to create presentation slides in html. A decent quick start guide can be found in Silvia Canelón's blog post [Deploying xaringan Slides with GitHub Pages](https://www.silviacanelon.com/blog/2021-deploying-xaringan-slides/). Here is a link to the [Xaringan gallery](https://xaringan.gallery/) for other examples. To my knowledge, the other extension packages are [xaringanthemer](https://pkg.garrickadenbuie.com/xaringanthemer/) and [xaringanExtra](https://pkg.garrickadenbuie.com/xaringanExtra/).

It was eye opening to see how many different ways [Xaringan](https://github.com/yihui/xaringan) slides can be converted to using [renderthis](https://jhelvy.github.io/renderthis/). It went from the usual html file, pdf file to even png images. Currently, I was following the instructions in Garrick Aden-Buie's blog post [Printing xaringan slides with chromote](https://www.garrickadenbuie.com/blog/print-xaringan-chromote/) to output the [Xaringan](https://github.com/yihui/xaringan) slides into pdf. Maybe I should try to see if I could do the same with [renderthis](https://jhelvy.github.io/renderthis/). 

With [renderthis](https://jhelvy.github.io/renderthis/), users could also specify which [Xaringan](https://github.com/yihui/xaringan) slides to be converted to. Future work involved able to output the [Xaringan](https://github.com/yihui/xaringan) slides as a Microsoft Powerpoint [3 slides per page handout](https://answers.microsoft.com/en-us/msoffice/forum/all/how-do-i-save-a-powerpoint-presentation-with/e93ec638-8ad1-4002-8c1c-78cc90f097a6).

#### animate

I jumped to Data Visualisation room later after that. 

I was looking forward for the presentation on the R package [animate](https://kcf-jackson.github.io/animate/index.html) by Jackson Kwok. You see, I was reading the poster in Micosoft Powerpoint beforehand and my jaws dropped when I see that the animation featured in this article titled [The New Science of Sentencing](https://www.themarshallproject.org/2015/08/04/the-new-science-of-sentencing) could be replicated using R. While reading the documentation of [animate](https://kcf-jackson.github.io/animate/index.html), I found out Jackson also made some [Xaringan](https://github.com/yihui/xaringan) [slides](https://rawcdn.githack.com/kcf-jackson/animate/0f3e8211f063e832b3b83288b4834329d491f4da/man/slides/SVI_presentation.html) introducing the R package [animate](https://kcf-jackson.github.io/animate/index.html). Do take a look if you need a more information. Unfortunately, when I entered the virtual longue. It just ended...

#### Polished Annotations

Putting this aside, the next presentation was by [Cara Thompson](https://twitter.com/cararthompson) sharing useful tips and trick to make polished annotations in [ggplot](https://ggplot2.tidyverse.org/index.html). Making annotations in [ggplot](https://ggplot2.tidyverse.org/index.html) had always been really challenging for me. I usually spent a lot of time tweaking fixed parameters to move the annotations from one place to another. Most of the time I just gave up and used Microsoft Powerpoint to add these extra text boxes. 

Cara's success in finding several clever strategies to make polished annotations, using [ggtext](https://wilkelab.org/ggtext/), [glue](https://glue.tidyverse.org/), CSS formatting and a filtered tibble with unique arrow curvature information, did make me smile. Her tips could also be found in this [talk post](https://www.cararthompson.com/talks/user2022). One of her blog post [Alignment cheatsheet](https://www.cararthompson.com/posts/2021-09-02-alignment-cheat-sheet/) may be useful for those who need a little help on the alignment parameters.

#### Two-Sample Corrgram

The last presentation in the Data Visualisation room was by Rohan Tummala. This visualisation is a unique way to optimise the correlation results of dichotomous data within the space of a 2D heatmap matrix. More information could be found in this [project webpage](https://rithikatummala8.wixsite.com/sigmaxisrs2021/). 

It definitely has a lot of potential to be improved by the R community. Here are my "5-cent" suggestions. The team may wish to use the R package [correlation](https://easystats.github.io/correlation/) from the [easystats](https://easystats.github.io/easystats/) team, to expand their current correlation methods of Pearson, Kendall and Spearman. 

As for the question raised on extending the static plot to multichotomous data (or k-sample corrgram), one idea I can think of currently is to adopt the [scatter plot matrix](http://www.sthda.com/english/wiki/scatter-plot-matrices-r-base-graphs) style where the diagonal are the groups and the scatter plots are replaced with the two sample corrgrams instead. However, this in turn creates the same redundant space which the two-sample corrgram is supposed to prevent. 

Regardless, if this visualisation continue to receive good feedback, someone will create an interactive two-sample corrgram and push it as a web tool.

#### pacs

I next entered the R in Production room where I was first introduced to the R package [pacs]((https://polkas.github.io/pacs/)) by [Maciej Nasinski](https://github.com/polkas). It contained a set of useful utility functions for helping R package developers life easier such as, automating validation of a [renv](https://rstudio.github.io/renv/articles/renv.html) lock file, finding out packages which are not from CRAN. More information could be found in its [documentation](https://polkas.github.io/pacs/).

#### svgtools

The second sharing was from Konrad Oberwimmer who introduced the R package [`svgtools`](https://cran.r-project.org/web/packages/svgtools/index.html) that was able to key in statistical results onto charts template made in [SVG file format](https://commons.wikimedia.org/wiki/Template:SVG_Chart). This is helpful if there is a need to create graphs that needs to follow a certain layout based on corporate needs.

#### data.validator

The next showcase was about [data.validator](https://appsilon.github.io/data.validator/) by [Marcin Dubel](https://twitter.com/DubelMarcin). Honestly, this is an R package that I wish I knew earlier how to use it. While it is great to have tools that validate the data but it is even better when a validation report, highlighting the possible issues of a given dataset clearly and explicitly, can be created and distributed to others.

[data.validator](https://appsilon.github.io/data.validator/) not only used [assertr](https://github.com/ropensci/assertr) to do the validation but is able to create an interactive report in html as well. More details could also be found in this [youtube video](https://www.youtube.com/watch?v=U1-j7c_8LFQ) as well as this [R-bloggers post](https://www.r-bloggers.com/2022/05/data-cleaning-in-r-2-r-packages-to-clean-and-validate-datasets/)

#### Continuous Integration In GitLab For R

Lastly, it was a workflow presented by [Cody Marquart](https://twitter.com/cody_marquart) on how to manage R packages automatically using [GitLab](https://about.gitlab.com/) Continuous Integration (CI). [GitLab CI](https://docs.gitlab.com/ee/ci/introduction/index.html#continuous-integration) was first introduced from an [April 2020 GitLab meetup](https://www.youtube.com/watch?v=l5705U8s_nQ&t=397s). It was nice to know that CI is possible to be applied on R packages management in GitLab. Usually, CI was done using [Github Actions](https://github.com/features/actions) from [Github](https://github.com/) because of many [useful resources](https://github.com/r-lib/actions) available to help users create CI tasks easily. Thus, [Github Actions](https://github.com/features/actions) became a popular choice for R package management. Nevertheless, as it is unwise not to have a backup plan, being aware of that an alternative workflow exists is critical. Take a look at one of GitLab CI examples used in the R package [shinyLogger](https://gitlab.com/clmarquart/shinyLogger/-/blob/main/.gitlab-ci.yml) 
Hopefully, I would get to witness a similar workflow for managing R packages using [Bitbucket](https://bitbucket.org/product/) in the future. 

### Clinical Data Review Reporting Tool

Day 3 for me was filled with many sessions that I was interested in like Data Visualization, Publishing and Reproducibility as well as Web Frameworks. Unfortunately, I could not join all at the same time. After some thoughts, I had decided to attend the session on Publishing and Reproducibility.

The first talk was from Laure Cougnaud from [OpenAnalytics](https://www.openanalytics.eu) introducing an R package [clinDataReview](https://cran.r-project.org/web/packages/clinDataReview/index.html) used to provide a medical report in [bookdown](https://bookdown.org/), filled with interactive plots to understand how patients were doing during a clinical study. An example of this report could be found in this [link](https://medical-monitoring.openanalytics.io/) The report was created as a folder of mainly HTML (and [other](https://cran.r-project.org/web/packages/clinDataReview/vignettes/clinDataReview-reporting.html)) files which was then distributed to the clinicians. The key to making this possible was the use of a standard template report in R markdown as well as a configuration file in YAML for users to set specific parameters to make the report customisable and flexible to their needs.

I was first introduced to Rmarkdown report templates during my attendance in the RStudio Conference 2020 at San Francisco. It was presented by [Sharla Gelfand](https://twitter.com/sharlagelfand) titled [Don’t repeat yourself, talk to yourself! Reporting with R](https://www.youtube.com/watch?v=JThd3YYQXGg&ab_channel=RStudio). I highly recommend watching as it is really down to Earth and funny at the same time. Sharla also provided a [blog post](https://sharla.party/post/usethis-for-reporting/) showing step by step how to produce an introductory R package with Rmarkdown report templates. 

The work done by Laure Cougnaud and her team was bringing this workflow to the next level by extending from Rmarkdown to [bookdown](https://bookdown.org/) reports. Definitely a job well done.

* 📝[Slides](https://medical-monitoring.openanalytics.io/)

### knitr engines And blogdown Troubleshooting

The next talk was by [Christophe Dervieux](https://twitter.com/chrisderv) giving a [introductory tour](https://cderv.rbind.io/talk/2022-user-knitr-engines/) on the different [knitr](https://github.com/yihui/knitr) engines. The [knitr](https://github.com/yihui/knitr) engines can be listed in R using the command `names(knitr::knit_engines$get())`. More information of commonly used engines can be found in the [Rmarkdown e-book](https://bookdown.org/yihui/rmarkdown/language-engines.html). 

I was then introduced the latest [`knitr`](https://github.com/yihui/knitr) engine called `exec` which allow command lines to be executed in the Rmarkdown code chunk. The talk also guided users on how to create custom [knitr](https://github.com/yihui/knitr) engines as well. 

One major takeaway for me on this talk was the that there was actually a [Github link](https://github.com/yihui/knitr-examples) showing Rmarkdown examples of many different [knitr](https://github.com/yihui/knitr) engine, including the latest `exec` engine found [here](https://github.com/yihui/knitr-examples/blob/master/124-exec-engine.Rmd). 

After enjoying the tour on [knitr](https://github.com/yihui/knitr) engines, the session proceeded with [Yihui Xie](https://twitter.com/xieyihui) sharing some [helpful summary](https://yihui.org/en/2022/06/user-blogdown/) on how to create a blog using [blogdown](https://pkgs.rstudio.com/blogdown/) with minimal issues using `blogdown::serve_site()` and `blogdown::check_site()`. Hopefully the `blogdown::check_site()` could be part of the RStudio Addins for [blogdown](https://pkgs.rstudio.com/blogdown/) in the future. 

For me, I started to learn how to create this [Hugo Apéro](https://hugo-apero-docs.netlify.app/) theme [blogdown](https://pkgs.rstudio.com/blogdown/) site from watching a YouTube video of a [lesson](https://www.youtube.com/watch?v=RksaNh5Ywbo&ab_channel=R-LadiesTunis) conducted by Alison Hill's in R Ladies Tunis. However, if a two hours lesson is too long, may I direct you to Alison Hill's [Day 09: Hugo Apéro from scratch || rmarkdown + blogdown + Netlify](https://www.youtube.com/watch?v=yXFu_upDL2o&ab_channel=AlisonHill) from the #12DaysOfDusting [series](https://www.youtube.com/playlist?list=PLzxicn7kBeazI9Niimsth81iWn4mvCmu0) instead.

* 📝[Christophe's Slides](https://cderv.rbind.io/talk/2022-user-knitr-engines/)
* 📝[Yihui's Slides](https://yihui.org/en/2022/06/user-blogdown/)

### Reliable Scientific Software Development

The last presentation of this session was by [Meike Steinhilber](https://twitter.com/M_Steinhilber), developer of the R packages [sprtt](https://meikesteinhilber.github.io/sprtt/)(Sequential Probability Ratio Tests Using The Associated t-statistic) and its Shiny counterpart [sprit](https://meike-steinhilber.shinyapps.io/spirit/). The talk focused on ways to develop reliable scientific software using some best practices for software development. 

In summary, the best practices were having clean and refactored code, software testing, continuous integration, version control and extended documentation. Examples used were from her R package [sprtt](https://meikesteinhilber.github.io/sprtt/). 

This is great advice for someone who has just started to have many long R scripts and wish to make them more manageable and sustainable. As this is also the speaker's [first conference presentation](https://twitter.com/M_Steinhilber/status/1539705226319564802?cxt=HHwWhMC4mdzvkN4qAAAA), do show her some love and support if you like the presentation.

The presentation gave me a nostalgia feeling as I had [presented](https://jeremy-selva.netlify.app/talk/2021-10-29-pydata-global-2021/) something similar in the [PyData Global 2021](https://pydata.org/global2021/) conference using a Python-made software [MSOrganiser](https://github.com/SLINGhub/MSOrganiser) as an example. That conference was also my first as well. Instead of reliability, the focus of my presentation however was tips to make the software more user friendly, less intimidating for new users and ways to deal with the angry ones as well.

* 📝[Slides](https://www.dropbox.com/s/dv80062qo0rbhd3/useR_MeikeSteinhilber_2022_V2.pdf?dl=0)

### Second Keynote: Applied Machine Learning With tidymodels

Day 3 of the conference ended with a keynote from [Julia Silge](https://twitter.com/juliasilge), author of [Supervised Machine Learning for Text Analysis in R](https://smltar.com/). She also posted a lot of [tidymodels-related lessons](https://www.youtube.com/c/JuliaSilge/videos) on YouTube as well as the online tutorial [Text mining with tidy data principles](https://juliasilge.shinyapps.io/learntidytext/).

The keynote consisted of a brief introduction of [machine learning](https://vas3k.com/blog/machine_learning/), followed by the e-book [Tidy Modeling with R](https://www.tmwr.org/) which she is working on. Julia then presented three things that made the job of a machine learning practitioner challenging and showed how [tidymodels](https://www.tidymodels.org/) was able to help the practitioner cope with those challenges.

The first challenge for a machine learning practitioner is to decide how much data should be used as training data to train the model and how much is used as test data to evaluate the model. If we allocate too much on training data, we will have a model that is unable to generalize well on new, unseen data. On the other hand, allocating too much on the test data will give an unoptimised model that gives inconsistent predictions on input data with similar properties. The [tidymodels](https://www.tidymodels.org/) package best suited for is [rsample](https://rsample.tidymodels.org/) which provides not just data splitting between training and testing data but also resampling of the training data (simulated versions of training data) by cross validation or bootstrapping for the optimisation of the model's complex parameters.

Another tough decision a machine learning practitioner has to make is to determine when does the model building process starts and ends. To do this, a proper model building workflow is required. A common misconception is the belief that the model building process starts only when we started using a given model to fit the training data. Julia warned that such a workflow is susceptible to [data leakage](https://machinelearningmastery.com/data-leakage-machine-learning/). Instead, the model building workflow should include any preprocessing steps, feature engineering processes, the model fit itself and post-processing activities. However, managing such a complex workflow can be hard, especially when many [different kinds of models](https://towardsdatascience.com/all-machine-learning-models-explained-in-6-minutes-9fe30ff6776a) are used. As such, the [recipes](https://recipes.tidymodels.org/) and [workflows](https://workflows.tidymodels.org) R packages from [tidymodels](https://www.tidymodels.org/) are created to assist machine learning practitioners to better organise their machine learning related projects.

After finalising the machine learning model, the machine learning practitioner can now deploy the model into the external clients system. However, the work does not end here. Overtime, the deployed model may decrease its effectiveness in making good predictions because the properties of input data have changed. The machine learning practitioner must monitor the model and wisely determine when it is the time to collect new data to create an updated model that performs better than the previous one. As many versions of models are created, a report may be required from the external clients to give transparency on how well different models are doing when compared to its predecessor. This process of model maintenance is also called Machine Learning Operations or MLOps for short.

To facilitate a smooth MLOps process for the programming language of Python and R, the last R package that Julia introduced is [vetiver](https://vetiver.rstudio.com/). 
[vetiver](https://vetiver.rstudio.com/) automatically generates [Dockerfiles](https://www.simplilearn.com/tutorials/docker-tutorial/what-is-dockerfile) so that the trained model can be deployed easily. Moreover, [vetiver](https://vetiver.rstudio.com/) is able to create APIs for the machine learning practitioner to monitor how well the trained model as well as the option to provide a [report card](https://vetiver.rstudio.com/learn-more/model-card.html) to summarise how the model is doing over time. In suumary, [vetiver](https://vetiver.rstudio.com/) is an open source tool created to provide a decent framework to version, share, deploy, and monitor a trained model.

The keynote was indeed rich in content regarding the best practices for machine learning. 

* 📝[Slides](https://www.dropbox.com/s/3ds01k9hdtn2ghb/user2022.pdf?dl=0)

## Conclusion

That is all I have learnt from Day 3. It has been a long one. Only one more day to go.
