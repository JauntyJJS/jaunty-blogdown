---
title: "Reflections on R ConfeRence 2022"
subtitle: ""
excerpt: "This is a write up of what I have learned during the [R ConfeRence 2022](https://www.r-conference.com/home)"
format: hugo
date: 2022-11-28
author: "Jeremy Selva"
draft: false
tags:
  - R ConfeRence 2022
categories:
  - R ConfeRence 2022
layout: single-sidebar
editor_options: 
  chunk_output_type: console
---

<a name="top"></a>

## Table of Content

-   [Introduction](#introduction)
-   [Day 1](#day-1)
    -   [Application of R and Shiny in Digital Marketing Intelligence](#application-of-r-and-shiny-in-digital-marketing-intelligence)
    -   [Data Storytelling in R](#data-storytelling-in-r)
    -   [Contributing to R Packages](#contributing-to-r-packages)
    -   [Univariate Bayesian Approach to Fine-mapping Genes](#univariate-bayesian-approach-to-fine-mapping-genes)
    -   [Web Scraping, Text and Network Analysis in R](#web-scraping-text-and-network-analysis-in-r)
-   [Day 2](#day-2)
    -   [Tidymodels in Medicine](#tidymodels-in-medicine)
    -   [Partial Verification Bias Correction](#partial-verification-bias-correction)
    -   [Integrating R with Web Applications with OpenCPU](#integrating-r-with-web-applications-with-opencpu)
    -   [Bibliometrics Analysis in R](#bibliometrics-analysis-in-r)
    -   [Modeling Longitudinal Health Measurement Trend with `lme4`](#modeling-longitudinal-health-measurement-trend-with-lme4)
    -   [Summarising model-based results with `gtsummary`](#summarising-model-based-results-with-gtsummary)
-   [Conclusion](#conclusion)
    -   [YouTube video links](#youtube-video-links)
    -   [Social media links](#social-media-links)

## Introduction

[R ConfeRence 2022](https://www.r-conference.com/home) is one of the biggest R event in Malaysia conducted by the [Malaysian R User Group](https://www.facebook.com/rusergroupmalaysia/) (MyRUG) and [R-Ladies Malaysia](https://www.facebook.com/groups/myrladies). This year, it is a two days virtual event consisting of workshops and presentations from many talented instructors and speakers.

<a href="#top">Back to top</a>

## Day 1

On the first day of the conference, there was a choice to attend some R related workshops or talks prepared by [R-Ladies Malaysia](https://www.facebook.com/groups/myrladies). For me, I had decided to attend the talks and to learn something new.

### Application of R and Shiny in Digital Marketing Intelligence

In short, digital marketing intelligence is the process of analysing information that is relevant for the business, to understand how the business is doing and help decision makers make wise choices.

[Sailalith Sarupuri](https://github.com/sarupurisailalith) shared how R and [Shiny](https://shiny.rstudio.com/) were incorporated in his digital marketing intelligence architecture. Here is a summary of some useful R packages shared.

With a few lines of code, R package [`httr`](https://httr.r-lib.org/index.html) can be used to facilitate authentication using [OAuth 2.0](https://httr.r-lib.org/reference/oauth2.0_token.html) to ensure the data are imported, using REST API endpoints, by the right users. More information on OAuth 2.0 authentication can be found in this [R-hub blog post](https://blog.r-hub.io/2021/01/25/oauth-2.0/).

R packages [`shinycssloaders`](https://github.com/daattali/shinycssloaders) and [`shinydashboard`](https://rstudio.github.io/shinydashboard/) provides additional widgets for users to quickly create a user interface for the [Shiny](https://shiny.rstudio.com/) application. Custom components can be added using HTML, CSS and JS.

Reactivity in [Shiny](https://shiny.rstudio.com/) applications can be hard to understand, making it hard to debug should an issue occur. R package [`reactlog`](https://rstudio.github.io/reactlog/) is able to display an interactive reactivity workflow to help users see which reactive elements are responsible in causing the issue.

[Firebase](https://firebase.google.com/docs/auth/web/custom-auth) lightweight javascript library can be used in a Shiny application for users to create a customised user authentication system such as registration of new users, user login, reset passwords platforms.

With regards to deploying [Shiny](https://shiny.rstudio.com/) applications, there are a few options such as [shinyapps.io](https://www.shinyapps.io/) and [Shiny Server](https://github.com/rstudio/shiny-server). However, there are limitations in both options when it comes to scaling. Applications deployed in [shinyapps.io](https://www.shinyapps.io/) has a 8GB memory limited while maintainance of [Shiny Server](https://github.com/rstudio/shiny-server) can be laborious. The speaker shared that one solution which is to convert the [Shiny](https://shiny.rstudio.com/) application into a containerized application using [Docker](https://www.docker.com/) and then use [Kubernetes](https://kubernetes.io/) to deploy, scale and manage the containerized application automatically.

It is useful create functions that can be resued in the [Shiny](https://shiny.rstudio.com/) application. Such function are called [`Shiny Modules`](https://mastering-shiny.org/scaling-modules.html). Sailalith gave an example of creating a [`Shiny Module`](https://mastering-shiny.org/scaling-modules.html) that generate dynamic report cards.

As R is a single threaded program, it can only perform one task at a time which can affect the performance of the [Shiny](https://shiny.rstudio.com/) application. It is possible to enable asynchronous programming in R using the R package [`promises`](https://rstudio.github.io/promises/). This is to ensure that the Shiny application can still response to other user interaction events while it is running a time consuming task.

[Caching](https://mastering-shiny.org/performance.html#caching) or storing a temporary copy of a processed data or chart can help to speed up the running process as well. When the [Shiny](https://shiny.rstudio.com/) application refreshes or restarts, the temporary copy will only be recomputed only when the inputs have changed.

Overall, it is a very informative presentation which I will keep watching time after time.

-   📹[Video](https://www.youtube.com/watch?v=XEivnv6qlaU&list=PLqd3IXFKBgD_YP6dFmvKmu8ojtH_wOCLY&index=1)

<a href="#top">Back to top</a>

### Data Storytelling in R

After a content heavy presentation, the following one by Dr. Calyn Tan was thankfully less technical. The speaker shared her R experience when she first learn how to create dashboard using R in 2020. With some guidance and training from her mentors, she is now more confidence in presenting her analysis results using Shiny dashboards to a wide range of audiences. In this presentation, she shared some guidelines on how to present data more effectively using an example to raise awareness on the financial abuse and exploitation of the elderly living in rural Malaysia.

Here are some summarised key points from her talk.

-   It is wise to spend some time to understand the data.
-   Use appropriate keywords if audience comes from a specialised background.
-   Present in simple English or native language if audience comes from a different background.
-   Narrative should bridge the relationship between the analysed data and the domain knowledge or audience interest
-   Interactive dashboard can be useful to build additional data insights but it must not deviate from the dashboard's content main points.
-   Sometimes, a simple but clear dashboard is good enough for a general audience.
-   If the audience is not familiar with the presentation topic, start out first with a brief summary with useful pictures to introduce the topic and get the audience's attention.
-   Use contrasting colours to emphasise the main points.

Calyn concluded her presentation with a few advises when learning R

-   R is not just for programming experts.

-   Success is the sum of small efforts done day in and day out.

-   Try to challenge your limits with motivation ans passion.

-   Don't be afraid to fail. Just keep trying

-   Stories are Data with a Soul - *Brené Brown*

-   📹[Video](https://www.youtube.com/watch?v=MFp8xzDq9Zs&list=PLqd3IXFKBgD_YP6dFmvKmu8ojtH_wOCLY&index=2)

<a href="#top">Back to top</a>

### Contributing to R Packages

R package contributions may be seen as a daunting task for many, especially if it is widely used and have well known maintainers. It can also be a time consuming process. However, Dr. Nurul Ain Toha emphasised that the benefits of contributing to an R package are numerous and it is worth to have the courage to give it a shot.

The talk began with a friendly introduction about R, RStudio and R packages followed by the advantages of creating an R package instead of keeping R scripts of many functions

-   Improve source code organisation.
-   Encourage good documentation.
-   Ensure code Rrusability and accessibility.

and the benefits of contributing to an R package

-   Improve the R package that you are using
-   Gain new R programming coding knowledge and skills
-   A chance to work with new people and expand your network and visibility in the R community

The main body of the talk are some guidelines to make a decent contribution using the speaker's experiences when contributing to the R packages [`mlr3proba`](https://mlr3proba.mlr-org.com/) and [`distr6`](https://alan-turing-institute.github.io/distr6/) as examples. Here is a quick preview of the main points discussed.

-   Ensure your contribution aligns with the objective of the R package.

-   Contributing to R packages is not limited to contributing code. Here are some alternative ways to contribute.

    -   Raise a question
    -   Bug reporting
    -   Improve documentation or vignette.
    -   Proposed a new idea or feature request

-   When contributing code, try to understand the design of the package

    -   Basic file structure of an R package.
    -   Does it use functional programming or object oriented programming like [S3](https://adv-r.hadley.nz/s3.html), [S4](https://adv-r.hadley.nz/s4.html), Reference Classes (RC), [R6](https://r6.r-lib.org/index.html) or [R7](https://rconsortium.github.io/OOP-WG/index.html).

-   Remember to write unit test and documentation if you are creating a new function for the R package.

-   📹[Video](https://www.youtube.com/watch?v=ASUxL4AGZCo&list=PLqd3IXFKBgD_YP6dFmvKmu8ojtH_wOCLY&index=3)

<a href="#top">Back to top</a>

### Univariate Bayesian Approach to Fine-mapping Genes

The next speaker is by Dr. Hannuun Yaacob, giving a presentation on her PhD project on genetic fine-mapping. Here is a short background for those who are unfamiliar with this topic.

Genome-Wide Association Studies or GWAS for short is a research field that identify genomic variants or causal single-nucleotide polymorphism (SNP) that are associated with a risk for a disease or a particular trait. The process usually involves taking the genomic sequence of large numbers of individuals and look for regions with SNPs that occurs more frequently in those with a particular trait than the controls. However, many of these frequently occurring SNPs in the region are usually not the causal SNPs but rather have an indirect relationship with the causal SNPs.

Fine-mapping analysis aims to find out which frequently occurring SNPs are truly causal in the region. However, this task is tricky because these frequently occurring SNPs are usually high in numbers and are correlated with each other. Thus, a brute force approach is impractical. Bayesian fine mapping approach tries to assign reliable probability that a candidate SNP is causal given the GWAS results.

Additional resources can be found in this YouTube video.
- [MPG Primer: Introduction to fine-mapping methods (2020)](https://www.youtube.com/watch?v=S6vfOr336b0)

A common prior used in Bayesian fine-mapping studies is the Normal distribution. Dr. Hannuun Yaacob proposed that changing the prior to a Laplace distribution provides a more accurate calculation of the probability that a candidate SNP is causal using simulated genotype data, [HAPGEN2](https://mathgen.stats.ox.ac.uk/genetics_software/hapgen/hapgen2.html) as an example.

The second part of the presentation is a short code demonstration on how to use R to change haplotype data to genotype data.

-   📝[Paper](https://onlinelibrary.wiley.com/doi/10.1002/gepi.22212)
-   📹[Video](https://www.youtube.com/watch?v=ASUxL4AGZCo&list=PLqd3IXFKBgD_YP6dFmvKmu8ojtH_wOCLY&index=4)

<a href="#top">Back to top</a>

### Web Scraping, Text and Network Analysis in R

The last speaker of the day is by [Dr. Pieter](https://pstek.nl/) on Web Scraping, Content and Network Analysis using R. It consisted of three short but concise demonstrations, using R in Web Scraping, Text and Network Analysis.

Using R packages [`tidyRSS`](https://robertmyles.github.io/tidyRSS/), [`httr`](https://httr.r-lib.org/index.html) and [`rvest`](https://rvest.tidyverse.org/), the first demonstration involved getting paragraphs of news articles from Google News related to Malaysia's most recent prime minister, Anwar Ibrahim. Tips included ways to make search query reproducible and the need to let the system sleep for a few seconds to prevent the search request to be blacklisted. After the data had been collected, R packages [`quanteda`](https://quanteda.io/) and [`quanteda.textplots`](https://github.com/quanteda/quanteda.textplots) were used to do simple Text Analysis such as word frequency and co-word analysis. Results were then plotted as a word cloud and network to find out what topics are closely related to Anwar Ibrahim.

Lastly, a Network Analysis is done on the novel "A Tale of Two Cities" by Charles Dickens to identify important characters in the novel. With the help of R packages [`quanteda`](https://quanteda.io/) and [`igraph`](https://igraph.org/r/), the generated results showed that Javis Lorry had the highest degree centrality but Monsieur Defrage had the highest betweeness centrality score

-   📝[Slides and Codes](https://pstek.nl/2022/r-conference/)
-   📹[Video](https://www.youtube.com/watch?v=ASUxL4AGZCo&list=PLqd3IXFKBgD_YP6dFmvKmu8ojtH_wOCLY&index=5)

<a href="#top">Back to top</a>

## Day 2

Day 2 is the main day of R ConfeRence 2022 consisting of just talks for the whole day.

### Tidymodels in Medicine

It is crucial for physicians to be able to correctly predict a patient's health outcomes based on the patient's past medical information. However, as medical data can be vast and complex, it can be challenging for physicians to achieve this goal. Thankfully, predictive analytics can assist physicians to make more accurate diagnosis on the patient via machine learning and other computationally intensive methods.

In relation to R, [Dr. Kamarul Imran Musa](https://myanalytics.com.my/) showed how to do predictive analysis, more specifically supervised machine learning, using R packages from [`tidymodels`](https://www.tidymodels.org/) on a stroke fatality dataset. He also covered different types of bias in medical machine learning projects and ways to mitigate them.

Dr. Kamarul Imran Musa is also the author of the book titled [Exploring Data Using R](https://shopee.com.my/Exploring-Data-Using-R-i.222767571.13310422273).

-   📹[Video](https://www.youtube.com/watch?v=Gx8kiBcQ3Gs&list=PLqd3IXFKBgD9oYTacAUVf9NauopnYpsGb)

<a href="#top">Back to top</a>

### Partial Verification Bias Correction

In a typical diagnostic accuracy study, a newly developed diagnostic test is usually compared to a gold standard diagnostic test. For example, a new Covid-19 test kit is compared with the results generated from Reverse Transcription Polymerase Chain Reaction (RT-PCR). From there, a confusion matrix is constructed and the sensitivity and specificity are calculated. A test kit is decent when it has high sensitivity and specificity.

However, if the gold standard diagnostic test is too invasive or expensive, it is common that individuals who are tested positive for a disease from a newly developed test kit to be verified with the results from the gold standard diagnostic test. Patients who were test negative are selectively excluded. For example, usually patients who were tested positive for Covid-19 on a new test kit are asked to go for a RT-PCR test for verification. Those who tested negative need not be further verified. This gave rise to partial verification bias (PVB), leading to an inaccurate evaluation of the newly developed test kit.

As a result, [Dr. Wan Nor Ariffin](https://wnarifin.github.io/) created an R package [`PVBcorrect`](https://github.com/wnarifin/PVBcorrect) to allow users to use various PVB correction methods on their dataset during diagnostic accuracy analysis.

-   📹[Video](https://www.youtube.com/watch?v=jkFDk1tdtUo&list=PLqd3IXFKBgD9oYTacAUVf9NauopnYpsGb&index=2)

<a href="#top">Back to top</a>

### Integrating R with Web Applications with OpenCPU

It can be hard to scale up a program in R into a productive enterprise system. This is because to build a tool with modern web application features, R needs to be integrated with other applications which requires a lot of technical knowledge and skills. [Arup Kamal](https://github.com/arupkamal) shared that this conversion process can be made less painful if the functions in R can be converted to REST APIs. To do this, he suggested a program called [OpenCPU](https://www.opencpu.org/).

Examples shown in this presentation are creating a web service that outputs the results from the R function `rnorm` and a simple web based wind turbine management system. Other examples can be found in this [webpage](https://www.opencpu.org/apps.html).

-   📹[Video](https://www.youtube.com/watch?v=jkFDk1tdtUo&list=PLqd3IXFKBgD9oYTacAUVf9NauopnYpsGb&index=3)

<a href="#top">Back to top</a>

### Bibliometrics Analysis in R

While bibliometrics is commonly used in the evaluation the progress of a given research area, it can be used for someone who is new to a broad research topic to identify useful introductory and review papers.

[Tengku Hanis](https://tengkuhanis.netlify.app/) shared a walk through of the R package [`bibliometrix`](https://www.bibliometrix.org/home/) to find relevant information related to Covid-19 research in Malaysia from the [Scopus](https://www.scopus.com/home.uri) database. Information includes highly cited papers, relevant journals, most productive authors, institutions/countries collaborations and trending keywords.

For those that do not want to do bibliometrics analysis in code, they can instead use [`biblioshiny`](https://www.bibliometrix.org/home/index.php/layout/biblioshiny), which is a web interface version of [`bibliometrix`](https://www.bibliometrix.org/home/).

-   📝[Slides](https://tengku-hanis.github.io/bibliometrics_Nov2022/#1)
-   👨‍💻 [Codes](https://github.com/tengku-hanis/bibliometrics_Nov2022)
-   📹[Video](https://www.youtube.com/watch?v=jkFDk1tdtUo&list=PLqd3IXFKBgD9oYTacAUVf9NauopnYpsGb&index=4)

<a href="#top">Back to top</a>

### Modeling Longitudinal Health Measurement Trend with `lme4`

Longitudinal health measurements may contain variables that are correlated due to similar trends over time or clustering effects such as geographical location. As such, these data are not independent from one another. It is recommended to use a linear mixed effects model instead of a standard linear model to give a more accurate predictions. More information can be found in this [visual introduction](https://mfviz.com/hierarchical-models/) by [Michael Freeman](https://twitter.com/mf_viz)

Mohd Azmi Bin Suliman shared that one way to do linear mixed effects model in R is to use the R package [`lme4`](https://github.com/lme4/lme4/). He showcased its use in a sleep study data set and a simulated stroke care giver data set.

One thing that catches my eye is that he uses the R package [`simstudy`](https://kgoldfeld.github.io/simstudy/index.html) to simulate the data, an R package which I have not heard of.

-   📹[Video](https://www.youtube.com/watch?v=jkFDk1tdtUo&list=PLqd3IXFKBgD9oYTacAUVf9NauopnYpsGb&index=5)

<a href="#top">Back to top</a>

### Summarising model-based results with `gtsummary`

The last session by Dr. Che Muhammad Nur Hidayat bin Che Nawi is a brief summary of what the R package [`gtsummary`](https://www.danieldsjoberg.com/gtsummary/) can do. In a nutshell, the [`gtsummary`](https://www.danieldsjoberg.com/gtsummary/) package helps user create publication-ready statistical summary tables that is also flexible for customisation. While SPSS and R is able to display results from regression models, it can be hard to understand for someone looking at it for the first time. [`gtsummary`](https://www.danieldsjoberg.com/gtsummary/) is able to convert these output to something that is more comprehensible with just a few lines of code.

Using a stroke mortality dataset, the speaker showed how [`gtsummary`](https://www.danieldsjoberg.com/gtsummary/) is able to convert tabular raw data to a descriptive summary table and a cross tabulation table. Next, he showed how to create model summary tables from a logistic regression and cox proportional hazards regression (for survival analysis). Dr. Che then shared ways to customised the table and combined multiple tables together. [`gtsummary`](https://www.danieldsjoberg.com/gtsummary/) results can be exported in many forms such as html, pdf and word. During the presentation, Dr Che. suggested using the print engine [`flextable`](https://davidgohel.github.io/flextable/) to export the report in Microsoft Word.

To give an overview report of a [`gtsummary`](https://www.danieldsjoberg.com/gtsummary/) table in a R Markdown or Quarto document, [`inline_text`](https://www.danieldsjoberg.com/gtsummary/reference/inline_text.html) can be used to ensure that the overview report can be updated automatically when the [`gtsummary`](https://www.danieldsjoberg.com/gtsummary/) table changes overtime.

-   📹[Video](https://www.youtube.com/watch?v=jkFDk1tdtUo&list=PLqd3IXFKBgD9oYTacAUVf9NauopnYpsGb&index=6)

<a href="#top">Back to top</a>

## Conclusion

[R ConfeRence 2022](https://www.r-conference.com/home) is made possible by the dedication and hard work from the [organising community](https://www.r-conference.com/about/organizing-committee).

<a href="#top">Back to top</a>

### YouTube video links

The link to the YouTube videos for this conference can be found as follows:

-   📹[R Workshop (26 November 2022)](https://www.youtube.com/watch?v=bsCJI5sxFbw&list=PLqd3IXFKBgD8_Mh0mKcXss-d8appb_Tun)
-   📹[R Ladies (26 November 2022)](https://www.youtube.com/watch?v=XEivnv6qlaU&list=PLqd3IXFKBgD_YP6dFmvKmu8ojtH_wOCLY)
-   📹[R Technical Talk (27 November 2022)](https://www.youtube.com/watch?v=Gx8kiBcQ3Gs&list=PLqd3IXFKBgD9oYTacAUVf9NauopnYpsGb)

<a href="#top">Back to top</a>

### Social media links

If you are curious to find out more about the [Malaysian R User Group](https://www.facebook.com/rusergroupmalaysia/) (MyRUG) or [R-Ladies Malaysia](https://www.facebook.com/groups/myrladies) like their upcoming events or volunteer your time to give a talk or teaching session, they can be contacted via these platforms.

Malaysian R User Group (MyRUG)
- 🌐[Facebook](https://www.facebook.com/groups/MalaysiaRUserGroup/)
- 🌐[Meetup](https://www.meetup.com/malaysia-r-user-group/)
- 🌐[YouTUbe](https://www.youtube.com/@malaysiarusergroup)
- 🌐[Discord](https://discord.com/invite/bsDFvGvMhY)

R-Ladies Malaysia
- 🌐[Facebook](https://www.facebook.com/groups/myrladies)

<a href="#top">Back to top</a>
