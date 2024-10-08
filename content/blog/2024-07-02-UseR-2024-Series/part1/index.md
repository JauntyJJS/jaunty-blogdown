---
title: Learning Journey in the useR! 2024 Conference Part 1
subtitle: ''
excerpt: >-
  This narrative is a write up of my learning journey in the virtual seesion of
  the [useR! 2024 Conference](https://events.linuxfoundation.org/user/).
format: hugo-md
date: 2024-07-07T00:00:00.000Z
author: Jeremy Selva
draft: false
images: null
series:
  - useR! 2024
tags:
  - useR! 2024
categories:
  - useR! 2024
layout: single-sidebar
editor_options:
  chunk_output_type: console
---


<script src="index_files/libs/clipboard-2.0.6/clipboard.min.js"></script>
<link href="index_files/libs/xaringanExtra-clipboard-0.2.6/xaringanExtra-clipboard.css" rel="stylesheet" />
<script src="index_files/libs/xaringanExtra-clipboard-0.2.6/xaringanExtra-clipboard.js"></script>
<script>window.xaringanExtraClipboard(null, {"button":"<i class=\"fa fa-clipboard\"><\/i> Copy Code","success":"<i class=\"fa fa-check\" style=\"color: #90BE6D\"><\/i> Copied!","error":"Press Ctrl+C to Copy"})</script>
<link href="index_files/libs/font-awesome-6.4.2/css/all.min.css" rel="stylesheet" />
<link href="index_files/libs/font-awesome-6.4.2/css/v4-shims.min.css" rel="stylesheet" />


<a name="top"></a>

## Table of Content

-   [Introduction](#introduction)
-   [Decomposition Based Deep Learning Model For Forecasting Agricultural Commodity Prices with decompDL](#decomposition-based-deep-learning-model-for-forecasting-agricultural-commodity-prices-with-decompdl)
-   [Modeling Antimicrobial Resistance Rate Data using DeβARMA](#modeling-antimicrobial-resistance-rate-data-using-deβarma)
-   [Share your R with Quarto](#share-your-r-with-quarto)
-   [Enhancing the R Development Guide](#enhancing-the-r-development-guide)
-   [Making Better Error Messages with cli](#making-better-error-messages-with-cli)
-   [Connecting Shiny Apps to Chemotion-ELN](#connecting-shiny-apps-to-chemotion-eln)
-   [One Container to Rule Them All](#one-container-to-rule-them-all)
-   [Minimum Viable Good Practices for High Quality Statistical Software Packages](#minimum-viable-good-practices-for-high-quality-statistical-software-packages)
-   [How to Quickly Mock-Up and Test Your Application User Interface Designs in Web Application](#how-to-quickly-mock-up-and-test-your-application-user-interface-designs-in-web-application)
-   [hpfilter: An R Implementation of the One- and Two-Sided Hodrick-Prescott Filter](#hpfilter-an-r-implementation-of-the-one--and-two-sided-hodrick-prescott-filter)
-   [Dandelion Hub: A Central Repository For De-central Civil Non-Violent Political Actions (CNPA) For Eco-social Justice](#dandelion-hub-a-central-repository-for-de-central-civil-non-violent-political-actions-cnpa-for-eco-social-justice)
-   [Rix: Reproducible Environments with Nix](#rix-reproducible-environments-with-nix)
-   [SDTM Automation with MINT+ ecosystem](#sdtm-automation-with-mint-ecosystem)
-   [Streamlining Cohort Analysis with cohortBuilder and shinyCohortBuilder](#streamlining-cohort-analysis-with-cohortbuilder-and-shinycohortbuilder)
-   [R-Ladies Paris](#r-ladies-paris)
-   [Tips for Writing Better R Code](#tips-for-writing-better-r-code)
-   [Data Pipeline to Analyse FODESAF's Cash Flow](#data-pipeline-to-analyse-fodesafs-cash-flow)
-   [Learning Together at the Data Science Learning Community (DSLC)](#learning-together-at-the-data-science-learning-community-dslc)
-   [Detection Abnormal Fish Behaviours With Isolation Forest](#detection-abnormal-fish-behaviours-with-isolation-forest)
-   [Overcoming Challenges in Primary School Educational Data Analysis](#overcoming-challenges-in-primary-school-educational-data-analysis)
-   [ExoLabel: Community Detection for Big Biological Networks](#exolabel-community-detection-for-big-biological-networks)
-   [Benchmarking Performance For The data.table Package](#benchmarking-performance-for-the-data.table-package)
-   [WHO's Health Economic Assessment Tool (HEAT)](#whos-health-economic-assessment-tool-heat)
-   [Submission Of Analysis Using R To Health Authority Reviewers](#submission-of-analysis-using-r-to-health-authority-reviewers)
-   [Democratizing Access to Water Treatment Models with tidywater](#democratizing-access-to-water-treatment-models-with-tidywater)

## Introduction

The [useR! 2024 Conference](https://events.linuxfoundation.org/user/) has returned after two years since its last launch in 2022. This year's programme consist of a virtual session on 2nd July 2024 followed by an in-person session from 8th to 11th July 2024.

Here is a small write up of the talks presented during the virtual session on 2nd July 2024.

<a href="#top">Back to top</a>

### Decomposition Based Deep Learning Model For Forecasting Agricultural Commodity Prices with decompDL

Agricultural commodity prices forecasting is useful for farmers to manage price risk of agricultural goods. A stable price of agricultural commodity brings greater welfare for the farmers. However, agricultural commodity prices series tend to behave differently from most financial time series. This is because the price trend tends to be more fluctuating due to seasonality, inelastic demand, production uncertainty and perishability. As artificial neural network (ANN) tend to work poorly with non-stationary time series, it needs to be improved.

Kapil Choudhary proposed a decomposition (smoothing technique) and ensemble method that first decompose a complex time series into a set of simple modes (known as intrinsic mode functions or IMFs) in which each mode contains a simple structure and more important, have a stationary fluctuation. The number of modes to decompose is determined by the minimum number of modes that provides a signal difference average that is close to zero.
These modes are individually predicted using LSTM deep learning model. These predictions are then ensembled to give a final forecasting prediction for the complex time series.

The implementation of the proposed model can be found in the R package [`decompDL`](https://cran.r-project.org/web/packages/decompDL/index.html). Kapil Choudhary is also the maintainer of other decomposition based neural network models implemented as an R package such as [`eemdTDNN`](https://cran.r-project.org/web/packages/eemdTDNN/index.html), [`vmdTDNN`](https://cran.r-project.org/web/packages/vmdTDNN/index.html), [`EEMDelm`](https://cran.r-project.org/web/packages/EEMDelm/index.html) and [`eemdARIMA`](https://cran.r-project.org/web/packages/eemdARIMA/index.html)

-   📹[Video](https://www.youtube.com/watch?v=8obzmBflLyo)

<a href="#top">Back to top</a>

### Modeling Antimicrobial Resistance Rate Data using DeβARMA

The misuse of antimicrobial medications and poor health facilities have led to an increase in antimicrobial resistance (AMR) cases in patients which can lead to an increase in health cost. There is a need of an decent antimicrobial resistance (AMR) model to predict the rate of antimicrobial resistance to assist healthcare providers and policy makers to develop effective and yet cost-effective antimicrobial management policies.

Traditionally, forecasting of AMR rates is done using the autoregressive moving average (ARMA) model, ARMA model with a Transfer function, also called ARMAX, exponential smoothing or logistic regression. However, some bacteria are either susceptible or resistant to the antibiotics, causing the AMR rate to contains a lot of zeros or ones in the time series. This requires the need of very specific ARMA models which is limited in R. Jevitha Lobo presented a novel time series model called Degenerate Beta Auto-regressive moving average or DeβARMA in short, that fits data in unit interval including zeros or ones.

The DeβARMA model is implemented in R and was tested on a real like **E.coli** dataset that is resistant to some antibiotics in blood collected from Jan 2011 to Dec 2019. A [R Shiny Application](https://jevithalobo.shinyapps.io/DBARMA_updated/) is also implemented for other researchers to try out the DeβARMA model for themselves.

-   📹[Video](https://www.youtube.com/watch?v=70u3K1xPzQY)

<a href="#top">Back to top</a>

### Share your R with Quarto

The third presentation in the virtual conference is an application of using [Quarto](https://quarto.org/) to share your R contents to others.

Inspired by the [Data Science Learning Community](https://dslc.io/) group
Jinhwan Kim had created a Quarto website in Korean named [R Education for Clinical Researchers](https://education.zarathu.com/) or R4CR in short.

In clinical research, R has been increasing in popularity as it is able to provide data management, statistical analysis and give outputs like tabular results and plots that is suited for a variety of audiences, like regulators and academics. However, more and more clinical researchers are doing the coding themselves instead of relying on professional statistical programmers or statisticians. To reduce the learning curve of R, [Zarathu](https://www.zarathu.com/), a research support organisation in Korea, had to provide a number of R contents (slides and tutorials) to clinical researchers. The problem is that these R contents existed in several locations (or [GitHub](https://github.com/) repositories) and it can be hard to find where things are.
This provides the motivation to create a learning website using [Quarto](https://quarto.org/) and publish the website using [GitHub Pages](https://pages.github.com/). The fact that [Quarto](https://quarto.org/) is able to work well with RStudio, output presentations, dashboards, short tutorials make it the ideal choice.

Jinhwan Kim then presented some [Quarto](https://quarto.org/)-related information that may not be so intuitive to new users.

The first part shared is that the creation of a small [Quarto](https://quarto.org/) website can be done using Rstudio's "New Project" -\> "Quarto Website". He then shared four essential files that make a [Quarto](https://quarto.org/) website called `index.qmd`, `about.qmd`, `_quarto.yml` and `styles.css`.

The next part is that [Quarto](https://quarto.org/) has a feature that creates a navigation bar in the website. This can be done by typing some `navbar` content in the `_quarto.yml` file. The navigation bar will be useful in organising large amount of content without the need to create a long list of README.

The third part is about ways to embed a slide deck that was created using [Quarto](https://quarto.org/). Suppose we have a slide deck in [Quarto](https://quarto.org/) called `slide.baseR.qmd`. It can be embedded into a [Quarto](https://quarto.org/) webpage using the [iframe frame elements](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/iframe). He also shared how the size of the embedded presentation (slide container) can be modified by adjusting the `.slide-deck` parameters in the `styles.css` file.

The last part to add a [slick](https://github.com/kenwheeler/slick) in the [Quarto](https://quarto.org/) webpage. This is not a trivial task but the key is to create a html file called `slider.html` that contains the slick code and class called `slider`. In the [Quarto](https://quarto.org/) file that requires to display the slick, first set the yaml parameter `include-in-header` to include `slider.html` and in places where the slider needs to be displayed, create a `div` frame element to show the slider.

Jinhwan Kim then showed how [Quarto](https://quarto.org/) can be connected to external services (such as chat service and payment platforms) using some Javascript code as well as some limitations of [Quarto](https://quarto.org/).

-   📝[Slides](https://jhk0530.github.io/useR2024-R4CR)
-   📹[Video](https://www.youtube.com/watch?v=a2InR6nbIuE)

<a href="#top">Back to top</a>

### Enhancing the R Development Guide

In this presentation, Saranjeet Kaur gives an brief introduction about the [R Development Guide](https://contributor.r-project.org/rdevguide/) (R Dev Guide), its current status and progress to make R a better programming language to use.

The [R Development Guide](https://contributor.r-project.org/rdevguide/) started as an initiative from some members from [R Ladies](https://rladies.org/) community after a discussion during the useR! 2020 conference that there is a need to reach out to a wider group of programmers to contribute to base R regardless on how seasoned they are with the programming language. After receiving a seed grant from the [R Foundation](https://www.r-project.org/foundation/), The [R Development Guide](https://contributor.r-project.org/rdevguide/) was born and developed by Saranjeet Kaur under the mentorship of Heather Turner and Michael Lawrence. Subsequently, a community dedicated to the maintenance of [R Development Guide](https://contributor.r-project.org/rdevguide/). During the Google Season of Docs (GSoD) 2022, the [R Development Guide](https://contributor.r-project.org/rdevguide/) gave a [proposal](https://github.com/rstats-gsod/gsod2022/wiki/GSOD-2022-Proposal) to expand the guide by

-   Expanding existing chapter with beginner-friendly examples
-   Adding a chapter on how to install R from source files.
-   Adding a chapter on translation
-   Adding a chapter on how to contribute tests for base R
-   Adding a chapter on how to use a git workflow to submit a new R patch

To date, the following new contents are added.

-   [Introduction](https://contributor.r-project.org/rdevguide/introduction.html)
    -   Quick start guide on how to contribute to base R
    -   The different ways to contribute to base R
    -   How to contribute to the [R Development Guide](https://contributor.r-project.org/rdevguide/) itself
-   [Message Translation](https://contributor.r-project.org/rdevguide/message-translations.html)
    -   How translation work in R with `.pot`, `po` and `mo` files.
    -   How to contribute new translation using [Weblate](https://translate.rx.studio/)
-   [Installing R from source](https://contributor.r-project.org/rdevguide/GetStart.html)

With the current improvements made on the [R Development Guide](https://contributor.r-project.org/rdevguide/), contribution to base R has become more accessible to newcomers, creating a more supportive environment for those who wish to help out.

While there is still a lot of work that needs to be done, the speaker ensures that they will be more opportunities to people to make contributions such as the [R Dev Day @ Paris Lodron University of Salzburg (PLUS), Austria on 12 July 2024](https://contributor.r-project.org/r-dev-day-plus-2024/) and [R Development Hackaton @ RSECon24, UK on 5 Sept 2024](https://rsecon24.society-rse.org/)

-   📹[Video](https://www.youtube.com/watch?v=vit06hXFw3M)

<a href="#top">Back to top</a>

### Making Better Error Messages with cli

Software can be hard for when you are working on it for the first time. It is highly likely that you will come across an error message. More often, we sometimes wish that these error messages could have be more clear, informative, helpful and even kinder.

Emil Hvitfeldt who is working in the development of [`tidymodels`](https://tidymodels.org/) shared how error, warnings and other messages from R packages can be improved using the [`cli`](https://cli.r-lib.org/) and [`rlang`](https://rlang.r-lib.org/) R packages.

One tip is to make use of the`call` parameter in [`cli::cli_abort`](https://cli.r-lib.org/reference/cli_abort.html) function to indicate which function that is available to the user is causing an error, rather than an internal function.

Another tip is to use [`glue`](https://glue.tidyverse.org/) interpolation to capture the user's input and display this input in an error message to indicate that the user's input is invalid. [`cli`](https://cli.r-lib.org/) has inline text formatting which can be useful to indicate which variable is a function parameter and which variable is a user's input.

When writing user-facing functions, it is advised that error messages as a results of a failed validation check should happen as early or fast as possible. Try also to not just indicate the cause of the error but also some suggestions to avoid this error from appearing.

-   📹[Video](https://www.youtube.com/watch?v=uu8KHXgagug)

<a href="#top">Back to top</a>

### Connecting Shiny Apps to Chemotion-ELN

The [NFDI<sub>4</sub>Chem](https://www.nfdi4chem.de/) is a non-commercial consortium that aims to build a national research data infrastructure for the research domain of chemistry in Germany. One of its projects to improve its Electronic Lab Notebook (ELN) workflow by providing a platform to transform decentralised ELN-instances from different working groups into a central (published) data collections on a repository.

[Chemotion-ELN](https://chemotion.net/) is developed by several software developers at different NFDI4Chem sites to facilitate the publication of research data by transferring data from a user's ELN account to a central research data repository. This reduces the scientist's effort in allowing access to research data. It will be nice if [Chemotion-ELN](https://chemotion.net/) is able to communicate with other Third Party Applications (TPA).

Konrad Krämer gave a presentation showing how this could be done using R [Shiny](https://shiny.posit.co/). He then provided an example on how with the use of R [Shiny](https://shiny.posit.co/), [Chemotion-ELN](https://chemotion.net/) is able to send data to another Shiny application called [Biostats](https://github.com/ComPlat/shinychem), which helps scientists perform data wrangling, visualization, and statistical tests on chemistry related data. The results were then sent back to [Chemotion-ELN](https://chemotion.net/).

-   📹[Video](https://www.youtube.com/watch?v=HaG5lRrFQuE)

<a href="#top">Back to top</a>

### One Container to Rule Them All

Magnus Mengelbier gave a brief introduction about containers defined as a cheap and easily accessible virtual machine. The general workflow is that a script file (for example a Docker script) is used to create a container image. A container image is like a big zip file that contains all the operating systems files, files needed to run R and files needed for your R packages. Putting the container image into a host and running it will give a container instance that users can interact with. In a Docker file example, it usually starts with a command to build s base image like Ubuntu. The next set of commands is used to build the container image. The last set of commands will only run once the container image is built and launched as container instance in the host.

In most cases, container images are built one for an interactive development environment (IDE) like Posit workbench and another for web application. If there is a need to validate an R package for both containers, the validation needs to be done individually for each container. The problem comes when certain workflow or applications requires validation of an R package in multiple containers. Magnus showed that there is a more efficient way to this. The key is to make use a technique called container providence.

The idea is to first build a container with contain the R software. Let's call it Container R. Next add the validated packages to a new container that is based on Container R. Let call it Container R Batch. When Container R Batch is verified, it can be use as a source to create new containers of whatever interface is needed like IDE or web applications. Container R Batch can be updated if the list of validated R packages needs to be changed. This approach ensures that the R packages are installed and validated once until a new R version is released.

-   📹[Video](https://www.youtube.com/watch?v=48-cHmKzrhY)

<a href="#top">Back to top</a>

### Minimum Viable Good Practices for High Quality Statistical Software Packages

This presentation is presented by Daniel Bové from [RCONIS](https://www.rconis.com/).

While there are many courses, books and peer review programmes that can help one to create a decent R package, it can be a overwhelming task for many as most of us who started using R do not have software development experience. [openstatsguide](https://www.openstatsware.org/guide.html) aims to provide small, concise and minimal set of recommendations to encourage developers to make better R packages. These recommendations can be used on other functional data science languages like Python and Julia as well.

The content of [openstatsguide](https://www.openstatsware.org/guide.html) revloves around these six principles.

"Documentation, Vignettes, Tests, Functions, Style, Life cycle"

These keywords can be easily remembered with the mnemonic bridge sentence:

"Developers Value Tests For Software Longevity"

The presentation that provides details of these six principles which can also be found in the [openstatsguide](https://www.openstatsware.org/guide.html) link

-   📹[Video](https://www.youtube.com/watch?v=_BKCey-8008)
-   📝[Slides](https://rconis.github.io/openstatsguide-user2024)

<a href="#top">Back to top</a>

### How to Quickly Mock-Up and Test Your Application User Interface Designs in Web Application

In this presentation, Barbara Mikulasova presented some great tip and advice for people who want to start implementing [Shiny](https://shiny.posit.co/) applications in their workflow but have little experience in full stack or web application development.

The general advice is the need to present an initial design/prototype of the Shiny application to users. This is to receive users' feedback on the interactive experience and to have a better understanding of the users needs and what they like or dislike about the user interface (UI). This stage also ensures that the users have a clear idea of how the Shiny application looks like, suppose to work and most importantly, are satisfied with the implementation. After all, we do want to avoid developing features that users will not use in the long run and undo applications which takes a long time to implement and can potentially break the application when removed.

Developing a prototype can be done in three main stages:
- First stage is to work with the users to design the front-end or the user interface (UI) first. This process will help to gather users' feedback quickly on the UI layout, users' experience when they interact with the application. From there, it will be easier to identify essential and nice to have features, conceptualize the end-product and estimate the Shiny application complexity.
- Second stage is to work on adding interactive input elements (like data input and filtering). This is also the stage to discuss the data workflow with the users as this will provide some ideas on which elements should be reactive or non-reactive and what business logic or application needs to be turned into modules.
- Third stage is then to develop the back-end (or the rest) of prototype

It is worth noting that the three main stages may not always be a linear process (Stage 2 can lead back to Stage 1) if not managed well. Thankfully, there exists R packages like [`fakir`](https://thinkr-open.github.io/fakir/) and [`shinipsum`](https://github.com/ThinkR-open/shinipsum) to speed up the Shiny prototyping process.

[`shinipsum`](https://github.com/ThinkR-open/shinipsum) provides an easy way to create random shiny elements like data.frame, ggplot objects and dygraph objects on the front-end for users to view and give their feedback. On the other hand, [`fakir`](https://thinkr-open.github.io/fakir/) provides a quick way to create fake datasets that can be useful to test certain features like table design, filters and plots.

The presentation then proceeds with a use-case example on how [`fakir`](https://thinkr-open.github.io/fakir/) and [`shinipsum`](https://github.com/ThinkR-open/shinipsum) are applied in creating the prototype design. Though the prototype may not look pretty at this point, it is more important at this stage to get the layout right. Once this is done, we can make the prototype look nice with some [CSS](https://unleash-shiny.rinterface.com/beautify-css) code or styling R packages like [`shinythemes`](https://github.com/rstudio/shinythemes) for Shiny.

After finalising the prototype design, it is time to translate the prototype into an actionable minimum viable product (MVP). At this point, it is important to have a good understanding of the users' behaviour and expectations to anticipate potential pain points in the developmental stage. Barbara suggests that it is important to

-   Choose a framework for building production-grade shiny applications (Should I go with [shiny module](https://mastering-shiny.org/scaling-modules.html), [`golem`](https://thinkr-open.github.io/golem/) or [`rhino`](https://appsilon.github.io/rhino/) ?)

-   Decide which feature to develop first and the order in which to develop them. Remember to identify essential and nice to have features

-   Build the application in modules so that it is easier to test and grow the application, assign resources and assess the project's progress. Keep the UI and Server code light.

-   Maintain a concise visual representation of the UI and Server logic workflow to keep track on features and the overall development process. It will also help to see how new features can be added to minimise risk of having an application breakdown.

-   📹[Video](https://www.youtube.com/watch?v=Syu3LlteOfA)

<a href="#top">Back to top</a>

### hpfilter: An R Implementation of the One- and Two-Sided Hodrick-Prescott Filter

Time series fluctuation curve is a common trend seen in finance and economics. The Hodrick--Prescott (HP) filter is a widely used tool for to remove short term fluctuation associated with the business cycle by data-smoothing. The purpose is to be able to reveal underlying long term trends hidden in the fluctuation curve. To date, there is a one-sided and two-sided versions of the Hodrick-Prescott filter.

Alexandru Monahov shared that that implementation of the HP filter in R is limited to the two-sided version. The motivation of creating the R package [`hpfilter`](https://cran.r-project.org/web/packages/hpfilter/index.html) was to fill this gap and allows user to be able to use both the one-sided and two-sided versions of the Hodrick-Prescott filter. In addition, the package uses sparse matrices in its calculations. This ensures that results can be produced in a shorter running time, especially with large datasets. [`hpfilter`](https://cran.r-project.org/web/packages/hpfilter/index.html) is also allow the HP filter to be applied on multiple time series fluctuation curves in a few lines of code. The presentation then proceeds with the use of the [`hpfilter`](https://cran.r-project.org/web/packages/hpfilter/index.html) a case study involving Ireland's Countercyclical Capital Buffer (CCyB).

-   📹[Video](https://www.youtube.com/watch?v=AkEafUs8-R8)

<a href="#top">Back to top</a>

### Dandelion Hub: A Central Repository For De-central Civil Non-Violent Political Actions (CNPA) For Eco-social Justice

It is not surprising to acknowledge that the world had faced multiple crises during last few years. With the lack of political will from major decision makers, environmental/ecological degradation and social injustice continues to be main reason for individuals to conduct non-violent resistance or protests to not only raise awareness but also to persuade policy makers to correct ineffective policies. The [Dandelion Hub](https://dhub.global/) is implemented as a platform to store records of CNPA events from around the world. It is also able to create an action map and summary report of the protests made to better understanding how activist groups behave and spread its influence from one place to another.

Details on how it is implemented using R can be found in the video link below.

-   📹[Video](https://www.youtube.com/watch?v=F1Lrz5mdgeo)

<a href="#top">Back to top</a>

### Rix: Reproducible Environments with Nix

[Nix](https://nixos.org/) is a package manager that allows users to install and manage many kinds of software (from the [Nixpkgs collection](https://github.com/nixos/nixpkgs)) by creating complex project-specific sandbox environments. When installing a software using the Nix package manager, Nix will install all the dependencies required. Once the development environment is successfully built using Nix, it can be deployed in any operating system. Hence, it can be seen as a powerful tool for reproducibility of projects. However, it is not easy to learn and utilise Nix as it comes with its own programming language, which is also called *Nix*. As such, Bruno Rodrigues and his team developed an R package called [`rix`](https://b-rodrigues.github.io/rix/) that provides functions that allows R users to generate *Nix* programming codes to build development environment easily.

In the presentation, Bruno gave a short demonstration on how to use [`rix`](https://b-rodrigues.github.io/rix/) to create a development environment with R, RStudio and some specific R packages and Python libraries installed and later deploy the same environment using the `nix-build` command. Another demonstration was done this time creating a development environment with the [`targets`](https://books.ropensci.org/targets/) pipeline.

Bruno Rodrigues is also the author of the book [Building reproducible analytical pipelines with R](https://raps-with-r.dev/).

-   📹[Video](https://www.youtube.com/watch?v=tM4JrCWZpwA)

<a href="#top">Back to top</a>

### SDTM Automation with MINT+ ecosystem

Created by the Clinical Data Interchange Standards Consortium (CDISC), a global not-for-profit organization that develops data standards for the pharmaceutical industry, a Study Data Tabulation Model (SDTM) is a standard specification for organising and harmonising human clinical trials tabular data prior to it submission to regulatory authorities such as the United States Food and Drug Administration (FDA). This is to make things easier for the reviewers to compare data across different studies. An SDTM dataset usually contains information about the demographic, visits, treatments, observations of the clinical trial patients.

As clinical trials generate large amount of raw data, it can be time-consuming and inefficient to convert the data manually that meets the standards of a SDTM. Therefore, [`MINT+`](https://www.lexjansen.com/phuse/2023/ad/PAP_AD13.pdf) is created as a web application to automate the creation of SDTM datasets from raw clinical data.

In greater detail, the MINT+ frontend is developed with the [ReactJS](https://react.dev/) framework. The backend of MINT+ consists of a REST API application called "rsaffron.api" and an Amazon DocumentDB called "Saffron" for SDTM data storage. "rsaffron.api" is developed using the R package [`plumber`](https://www.rplumber.io/), which does the heavy work of handling any action triggered on the front end, such as fetching from and writing data to the Saffron database.

-   📹[Video](https://www.youtube.com/watch?v=LeG2DM6jH80)

<a href="#top">Back to top</a>

### Streamlining Cohort Analysis with cohortBuilder and shinyCohortBuilder

Cohort analysis comes with many challenges such as the need to work with various data sources like (data.frames and SQL DB) and the need to be robust against complex workflow and requirements that needs multi-stage filtering. This makes it hard to keep on its progress and report the current status or results.

Adam Forys & Krystian Igras presented the R package [`cohortBuilder`](https://r-world-devs.github.io/cohortBuilder/) that is created to ensure the process of reading and filtering cohort data from multiple data sources can be done easily with a few lines of code (instead of using many different R packages like [`dplyr`](https://dplyr.tidyverse.org/), [`dtplyr`](https://dtplyr.tidyverse.org/), [`data.table`](https://rdatatable.gitlab.io/data.table/) to handle data from multiple sources). To ensure that the application is more accessible for people with limited coding experience, the R package [`shinyCohortBuilder`](https://r-world-devs.github.io/shinyCohortBuilder/) is created as a user-friendly Shiny application tool for people to perform cohort analysis using [`cohortBuilder`](https://r-world-devs.github.io/cohortBuilder/) in a point and click fashion. Plots and reproducible code can be exported from the Shiny application tool to update on the cohort's current status and results.

-   📹[Video](https://www.youtube.com/watch?v=i5K4VDLrHIU)

<a href="#top">Back to top</a>

### R-Ladies Paris

The [R-Ladies](https://rladies.org/) organisation is well-known for supporting and empowering minority genders to be able to showcase their R programming expertise and to take on more leadership roles in the R ecosystem, building a more diversified R community in the long term.

Chaima Boughanmi from the [R-Ladies Paris](https://www.meetup.com/rladies-paris/) community presented the progress and achievements that [R-Ladies Paris](https://www.meetup.com/rladies-paris/) have made since its founding in 2016. She then shared some helpful guides in maintaining an R-Ladies Chapter. Below is a small summary

-   Use survey to identify topics that are relevant for your community and to find potential speakers.
-   Use the [R-Ladies Directory](https://rladies.org/directory/) or [R-Ladies Slack](https://guide.rladies.org/comm/slack/) to look for speakers that support the cause of [R-Ladies](https://rladies.org/)
-   Make meetups accessible to attract new members
-   Collect testimonies from speakers to receive authentic feedback about your community
-   Meetup with mentors or people with more experience to gain valuable support and advice on how to run an organisation.
-   Ask for a grant for [R Consortium](https://www.r-consortium.org/) if you need financial support.
-   Share your chapter activites in the [R-Ladies Blogs](https://rladies.org/activities/rladies-blogs/)

Motivated individuals who are interested in starting a new R-Ladies chapter can contact via this email address <chapters@rladies.org>.

-   📹[Video](https://www.youtube.com/watch?v=KqokszC42Uc)
-   📝[Slides](https://rladiesparis.github.io/rladies_paris_talk_useR2024/rladies_paris_talk_useR2024.html)

<a href="#top">Back to top</a>

### Tips for Writing Better R Code

Writing code that is human readable and understandable allows code to be shared easily with others, preventing duplicate work and make work easier to replicate important results. It is also a requirement for some journals for codes to be shared. However, it is always hard for PhD students or someone with a limited programming background to apply good software development practices and avoid writing [spaghetti code](https://en.wikipedia.org/wiki/Spaghetti_code). These individuals usually do not have mentors or supervisors that are able to help them as well and are force to learn things on the job.

Nicola Rennie shared that as learning to write decent R code can be daunting, it is best to do this one step at a time rather than to do everything at once.

Here are the tips to ensure individual scripts are styled and structured well

-   Write comments to explain not what your code does but to explain why the code is implemented or written in a specific way.
-   Use comments to add [section and subsections](https://docs.posit.co/ide/user/ide/guide/code/code-sections.html) to the R scripts, just like writing a paper.
-   Avoid writing codes that are too wide that it requires left and right scrolling.
-   Use a [linting](https://www.perforce.com/blog/qac/what-is-linting) tools like [`lintr`](https://lintr.r-lib.org/) and [`styler`](https://styler.r-lib.org/) to standardise coding style across projects.

Here are the tips to ensure individual projects are styled and structured well

-   Break up a single R script with thousands of lines of code into many files with shorter R scripts instead.

-   Name the R script files based on what the R script is doing (usually one file name is given for one specific data workflow task)

-   Add number as prefix to your file name to tell others the order of the files the R scripts need to run.

-   Remember to also organise the other files as well (data, results and plots) by creating different folders with sensible names.

-   Try out the R package [`targets`](https://books.ropensci.org/targets/) to manage your data workflow.

-   Use code version control tools like [Git](https://git-scm.com/) to keep track of different versions of R scripts

-   Use code repositories like [GitHub](https://github.com/)/[GitLab](https://about.gitlab.com/)/[BitBucket](https://bitbucket.org/product/) to allow people in different locations to work together on the code.

-   📹[Video](https://www.youtube.com/watch?v=wbhWl5-xR10)

-   📝[Slides](https://nrennie.rbind.io/talks/user-spaghetti-code/)

<a href="#top">Back to top</a>

### Data Pipeline to Analyse FODESAF's Cash Flow

[FODESAF](https://fodesaf.go.cr/) is a public financial institution that conduct social programs to address the housing, education, health and social protection needs of Costa Ricans and foreign legal residents of the country, especially minors who are in a situation of poverty or extreme poverty.

Roberto Castro highlighted that FODESAF is in need of a way to
- visualise and follow up a US\$13,000 million cash flow from 2005 to 2022
- consolidate financial, budgetary and social programmatic data in one single ecosystem
- build an online Data Informative Center for public-open consultation

To achieve these tasks, a data pipeline is created with three major parts: Inputs, Processing and Outputs.

For the input, there were three main databases. One to handle financial and budgetary data, one to handle data from social programs and one to handle data from social security institutions. For the Processing stage, R was used to tidy, clean and unify the raw data and then classify the raw data correctly based on the provided requirements. For the Outputs, [Power BI](https://www.microsoft.com/en-us/power-platform/products/power-bi) to then used to output visualisations and relevant processed dataframes for users while [Quarto](https://quarto.org/) is used to create HTML reports. In addition, four data warehouses are created to store different types of outputs. One for Budget (FODESAF's cash flow), Evaluation, Collections (debts from past-due employers) and Trusts.

An example of such a report can be found in this [Quarto Pub link](https://robertodelgadocastro.quarto.pub/cash_flow_fodesaf-2005-2021/)

-   📹[Video](https://www.youtube.com/watch?v=jPgOL6Bu1y8)

<a href="#top">Back to top</a>

### Learning Together at the Data Science Learning Community (DSLC)

Jon Harmon provides an introduction of the [Data Science Learning Community (DSLC)](https://dslc.io/). DSLC is a community that aims to provide tools and resources to create a diverse, friendly and inclusive environment for new data science learners and experts alike. It has conducted many activities such as book clubs, a safe and nurturing platform for asking data science related questions and [`TidyTuesday`](https://github.com/rfordatascience/tidytuesday) to give participants a chance to work on real-world datasets. Currently, they are conducting a [survey](DSLC.io/ttsurvey23) to gather feedback from people who have used [`TidyTuesday`](https://github.com/rfordatascience/tidytuesday) as a teacher or a student to find out ways to increase the usage of #TidyTuesday in Education.

The speaker then encourages others to step up and contribute to DSLC by
- Facilitating book club cohorts
- Answering questions on Slack: dslc.io/mentordash
- Helping out with DSLC-related Shiny apps (contact the speaker <https://fosstodon.org/@jonthegeek> for more information on this)

DSLC is also seeking a new fiscal host so that the organisation can legally accept monetary assistance from donations, grants and sponsorships.

-   📹[Video](https://www.youtube.com/watch?v=8jH5wfuDx-g)
-   📝[Slides](https://dslc-io.github.io/useR2024)

<a href="#top">Back to top</a>

### Detection Abnormal Fish Behaviours With Isolation Forest

Abnormal fish behaviours is critical for marine biologist as it is an indicator used to detect environmental changes caused by pollution or climate change. Fish behaviours are measured by the path they use and time they take to travel from one place to another. This path is called a trajectory consisting of two components: coordinates and time steps. The [Fish4Knowledge](https://github.com/Callmewuxin/fish4konwledge) project ensures that fish trajectories data are measured correctly.

Enrique Ceja introduced how trajectories data are processed using the R package [`trajr`](https://github.com/JimMcL/trajr) and then fitted into an [isolation forest model](https://dl.acm.org/doi/10.1145/2133360.2133363) using [`solitude`](https://talegari.github.io/solitude/index.html) to identify abnormal fish behaviours.

Enrique Ceja is also the author of the book [Behavior Analysis with Machine Learning Using R](https://enriquegit.github.io/behavior-free/).

-   📹[Video](https://www.youtube.com/watch?v=P6f29SskS1g)
-   📝[Slides](https://github.com/enriquegit/fish-behaviors)

<a href="#top">Back to top</a>

### Overcoming Challenges in Primary School Educational Data Analysis

Learning Management Systems (LMS) can generate a lot of raw data in relation to education. However, extracting and converting such raw data into useful information for decision-making is challenging because of the large volume and complex data structure in the LMS and it is in general, difficult to summarize the learning process based on this dataset, especially in a primary school setting which is uncommon.

Despite the challenging task ahead, Natalia da Silva and her team was determined to find ways to

-   monitor/evaluate the use of the LMS in primary school from Uruguay
-   identify key drivers that promote students' engagement with the LMS
-   predict students' performance in English tests based on their engagement with the LMS.

The presentation mainly focus on the techniques to achieve the first and last task.

For the first task, R [Shiny](https://shiny.posit.co/) application is used to create the monitoring system (called LMS Monitor) that is scalable, modular, flexible to changes, produce reproducible results, and can be used my many people at the same time. This is achieved using a [`rhino`](https://appsilon.github.io/rhino/) framework connected to a [PostgreSQL](https://www.postgresql.org/) database.

For the last task, [`tidymodels`](https://www.tidymodels.org/) and [`dbarts`](https://github.com/vdorie/dbarts) are heavily used to generate Bayesian Additive Regression Tree (BART) models to predict numerous outcomes like a student's final test results, average points at class level, if a primary student is able to graduate from school.

-   📹[Video](https://www.youtube.com/watch?v=nm5M4dF9aLs)

<a href="#top">Back to top</a>

### ExoLabel: Community Detection for Big Biological Networks

One aspect that people are interested in large networks analysis is to identify different communities (highly dense nodes) in a given network. From the perspective of geneticists, they are curious to identify a common group of genes that are the same across different organisms or families.

To do this, geneticists calculate how similar each gene sequence are to another and a build a large sequence similarity network (gene as nodes and similarity as edges) out of it. Genes that are highly similar will share a large edge between them. Genes that are highly similar to each other will be clustered/grouped together as a community. A community detection algorithm is then use to isolate one gene community from another. The problem is that there are many community detection algorithm used for different applications and use-cases. This can cause the same dataset to give highly varied results.

Aidan Lakshman from the [Wright Laboratory](https://wrightlabscience.com/) presented how the lab compare popular community detection algorithms in R to measure their accuracy, runtime and memory usage on synthetic and real datasets. The lab discovered that most community detection algorithms for gene analysis used a lot of computational memory and could only be used by analyst who have access to a high performance computer. Hence, they create a community detection algorithm `ExoLabel` that has a decent runtime, works well as other popular community detection algorithms and most importantly, consume a constant amount of memory. `ExoLabel` is available in the Bioconductor package [`SynExtend`](https://github.com/npcooley/SynExtend/).

-   📹[Video](https://www.youtube.com/watch?v=9eRAv-ouJmk)

<a href="#top">Back to top</a>

### Benchmarking Performance For The data.table Package

[`data.table`](https://rdatatable.gitlab.io/data.table/) is a highly popular because it is one of the first few R packages that have the capabilities to read and wrangle large datasets quickly without compromising memory space.

Doris Amoakohene is curious to see how well [`data.table`](https://rdatatable.gitlab.io/data.table/) does when compared to other R packages and Python libraries in performing various data analysis related task. To perform the benchmarking task, she uses the R package [`atime`](https://github.com/tdhock/atime) because the package is able to calculate the runtime and memory usage for a sequence of dataset of increasing size automatically and even plot the results. Here are some results:

-   When writing real numbers to a csv file, [`data.table::fwrite`](https://rdatatable.gitlab.io/data.table/reference/fwrite.html) perform better than [`pandas::to_csv`](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.to_csv.html).It also performed better when compared to other R packages like [`readr::write_csv`](https://readr.tidyverse.org/reference/write_delim.html) or [`arrow::write_csv_arrow`](https://arrow.apache.org/docs/r/reference/write_csv_arrow.html)

-   When converting data from wide to long format, [`data.table::melt`](https://rdatatable.gitlab.io/data.table/reference/melt.data.table.html) did not perform as well as [`tidyr::pivot_longer`](https://tidyr.tidyverse.org/reference/pivot_longer.html)

An interesting observation made is that the function [`data.table::setDT`](https://rdatatable.gitlab.io/data.table/reference/setDT.html) does not work well on wide dataset. This issue was then reported in [data.table GitHub page](https://github.com/Rdatatable/data.table/pull/5427) and was fixed when a new version is released.

In addition, Doris wanted to evaluate the performance of [`data.table`](https://rdatatable.gitlab.io/data.table/) across different versions to better understand the progress made in this highly used R package.

To do this efficiently, a [GitHub action for continuous performance testing](https://github.com/tdhock/atime?tab=readme-ov-file#github-action-for-continuous-performance-testing) using [`atime`](https://github.com/tdhock/atime) was implemented to ensure [`data.table`](https://rdatatable.gitlab.io/data.table/) is properly evaluated for every pull request and the visual results are displayed as a pull request comment.

-   📹[Video](https://www.youtube.com/watch?v=AuuGzUSSjpI)

<a href="#top">Back to top</a>

### WHO's Health Economic Assessment Tool (HEAT)

The WHO's [Health Economic Assessment Tool](https://www.heatwalkingcycling.org/) or HEAT for short is an online calculator to easily quantify, report and conduct economic assessments (like benefit-cost ratio) of the health impacts of walking or cycling for policy makers to make better decisions in urban/transportation planning and healthcare.

The speaker explains that the HEAT ecosystem is mainly made of a data cleaning process, the model and codes to create a user interface (UI).

For the data cleaning process, they use
- [`qs`](https://cran.r-project.org/web/packages/qs/index.html) to read the large data
- [`data.table`](https://rdatatable.gitlab.io/data.table/) to match/standardise countries names
- [`tidyverse`](https://www.tidyverse.org/) to conduct [ETL](https://en.wikipedia.org/wiki/Extract,_transform,_load)
- [`targets`](https://books.ropensci.org/targets/) to create a standardise and reproducible workflow
- [`assertr`](https://docs.ropensci.org/assertr/) to do data validation on processed data

For the UI process, they use the R [Shiny](https://shiny.posit.co/) framework to build the web application. The inheritance feature from the [`R6`](https://r6.r-lib.org/index.html) package was used to simplify the modification process of generic [Shiny](https://shiny.posit.co/) inputs.

During the process of making the web application, they also developed two new R packages called `translator` and `templater`. `translator` is built to resolve common translation problems such as different line-endings from different operating systems. `templater` is meant to create conditioned templates for R, similar to [`Nunjucks`](https://mozilla.github.io/nunjucks/) for JavaScript and [`Jinja`](https://palletsprojects.com/p/jinja/) for Python, to reduce errors as a result of copy and paste of very similar for HTML and PDF export templates. Both packages will be open-sourced in the future.

-   📹[Video](https://www.youtube.com/watch?v=hf92pZ98dlo)

<a href="#top">Back to top</a>

### Submission Of Analysis Using R To Health Authority Reviewers

In order to gain market support for a novel medical treatment, companies, hospitals and/or sponsors need to submit analysis reports, datasets, software codes and programs to the relevant health authorities for evaluation of the treatment's efficacy and safety. The reviewers usually not only review the reports but also rerun the software on the provided dataset to check that the results generated are reproducible. Recently, there has been a large interest on using codes from open source software like [R](https://www.r-project.org/) as part of the submission.

Joel Laxamana from [Genentech](https://www.gene.com/) gave a brief introduction to the [R Consortium R Submission Work Group](https://rconsortium.github.io/submissions-wg/), which was created to promote the use of R in regulatory processes. One of the challenges faced was to provide the reviewers the correct R package versions as they do not have access to [container technologies](https://www.solarwinds.com/resources/it-glossary/container) like [Docker](https://www.docker.com/). Things get harder when the analysis uses an R package that is not publicly available as some submission gateways reserved compressed files to only large datasets. Submission of computer files also needs to follow a strict file structure to ensure relevant documents are accessible to the reviewers.

To date, the [R Consortium R Submission Work Group](https://rconsortium.github.io/submissions-wg/) has completed three pilot submissions and is currently working on a 4th pilot submission. The speaker then proceed to elaborate more on the [Pilot 3](https://github.com/RConsortium/submissions-pilot3-adam) submission. In short, [Pilot 3](https://github.com/RConsortium/submissions-pilot3-adam) is an extension of [Pilot 1](https://rconsortium.github.io/submissions-pilot1/) which uses [R](https://www.r-project.org/) to generate the [ADaM](https://www.cdisc.org/standards/foundational/adam) datasets and then uses the same R codes from [Pilot 1](https://rconsortium.github.io/submissions-pilot1/) to regenerate the tables, listings, and figures (TLFs). The talk then proceeds with a demonstration on how to reproduce the results using the [Analysis Data Reviewer's Guide](https://raw.githubusercontent.com/JauntyJJS/jaunty-blogdown/main/content/blog/2024-07-02-UseR-2024-Series/part1/adrg.pdf).

Taking a look at the [Analysis Data Reviewer's Guide](https://raw.githubusercontent.com/JauntyJJS/jaunty-blogdown/main/content/blog/2024-07-02-UseR-2024-Series/part1/adrg.pdf), there are a lot of things that we can learn in creating a decent user friendly guide for people who are unfamiliar to [R](https://www.r-project.org/).

-   📹[Video](https://www.youtube.com/watch?v=vPmNdHTVYm8)

<a href="#top">Back to top</a>

### Democratizing Access to Water Treatment Models with tidywater

Sierra Johnson from [Brown and Caldwell](https://brownandcaldwell.com/) introduced how water treatment models are useful in helping engineers optimise clean water treatment protocols that are affordable, sustainable and efficient in the long run.

However, doing this was a challenge because
- the data collected were mainly used in one-off studies and lack standardisation and harmonisation.
- current water treatment modelling tools are dispersed (found in different academic papers/websites/software), - current water treatment modelling tools can only run very specific water treatment processes and scenarios
- current water treatment models lacks transparency as most are black box models.
- analysis on model outputs are done manually.

Sierra's goal in creating the R package `tidywater` is to ensure

-   Water treatment models are centralised in one tool.
-   Water treatment models can be applied to different water treatment processes in different scenarios.
-   Model outputs analysis can be done automatically.

Despite her success in convincing her managers and other colleagues that investing in R was the right way forward, Sierra shared that the process needed to reach to this stage was not easy.

She highlighted that because she and most of her team members do not have experience in making software, several time costly mistakes were made. A lot of time was needed to

-   document complicated models in a user friendly way.
-   simplify complex functions that other developers can understand.
-   fix failed test involving complex functions because the team only started to writing codes to test the model only when the package is "more or less complete".
-   rewrite R scripts in different project because they did not tag/record different version of the package used during analysis.

The last part of the talk consist of a small roadmap on how she managed to convince her stakeholders and managers that it is better in the long term to make the R package `tidywater` open source and to get the relevant approvals to make it happen in a risk adverse company.

One nice tip shared is to use clear and exciting terms like "Thought Leadership", "Industry Collaboration", "Access to new research" that help people understand the many opportunities and potential an open source product can bring. Another tip is to be try to more communicative and confidence about the sharing the tool towards people who are less technical or software-savvy than you. This is because they are the ones who usually knows the relevant people in authority that could give you useful advice or the final approval needed to keep the project going.

-   📹[Video](https://www.youtube.com/watch?v=ZF5V4PbvfXQ)

<a href="#top">Back to top</a>
