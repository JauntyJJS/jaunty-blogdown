---
title: Learning Journey in the useR! 2024 Conference Part 2
subtitle: ''
excerpt: >-
  This narrative is a write up of my learning journey during Day 1 of the [useR!
  2024 Conference](https://events.linuxfoundation.org/user/).
format: hugo-md
date: 2024-08-20T00:00:00.000Z
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
-   [Formal Debugging 🐛 in R](#formal-debugging-in-r)
    -   [Debugging your code](#debugging-your-code)
        -   [traceback](#traceback)
        -   [rlang::entrace and rlang::last_trace](#rlangentrace-and-rlanglast_trace)
        -   [browser](#browser)
        -   [RStudio IDE Breakpoints and Error Handler](#rstudio-ide-breakpoints-and-error-handler)
    -   [Debugging other people's code](#debugging-other-peoples-code)
        -   [debug, undebug and debugonce](#debug-undebug-and-debugonce)
        -   [options(error=recover) and trace](#optionserrorrecover-and-trace)
    -   [Other Debugging Techniques](#other-debugging-techniques)
    -   [Debugging Tutorial Resources](#debugging-tutorial-resources)
-   [Building Effective Docker 🐳 Images: R Edition](#building-effective-docker-images-r-edition)
    -   [Images and Containers Management](#images-and-containers-management)
    -   [Ports and Volumes](#ports-and-volumes)
    -   [Dockerfile](#dockerfile)
    -   [Installing Packages](#installing-packages)
        -   [System Package Management System](#system-package-management-system)
        -   [Posit Pubic Package Manager and littler](#posit-pubic-package-manager-and-littler)
    -   [Metadata](#metadata)
    -   [Docker Registry](#docker-registry)
    -   [Optimising Build Speed](#optimising-build-speed)
    -   [Optimising Image Size](#optimising-image-size)
    -   [Docker Tutorial Resources](#docker-tutorial-resources)

## Introduction

On the first day of the [useR! 2024 Conference](https://events.linuxfoundation.org/user/), I had attending two tutorial sessions. Here are my thoughts about them.

<a href="#top">Back to top</a>

## Formal Debugging 🐛 in R

What I have always done when R has an error is to comment everything and run the code one line at a time in a painstaking way. If an error occurs in my custom made functions, I usually copy the source code into my R script and then test them line by line. If an error occurs during the for loop, I usually just `print()/cat()/message()` the output and the iteration number to see where the issue is.

I never knew that R has some useful functions that can be used for debugging errors in a less tedious way until I attended this morning session from [Shannon Pileggi](https://www.pipinghotdata.com/) and [Maëlle Salmon](https://masalmon.eu/)

The tutorial started light with some tips on basic troubleshooting, such as

-   Samantha Csik's [talk](https://www.youtube.com/watch?v=93WsFQUuxvA) and [slides](https://samanthacsik.github.io/teach-me-how-to-google/slides/RLadiesSTL-2022-02-22.html) on how to effectively use search engines like Google to find solutions.

-   Learning how to restarting R in a [blank state](https://rstats.wtf/source-and-blank-slates) without saving the workspace and without restoring a saved workspace.

-   Using a [reprex](https://reprex.tidyverse.org/).

The tutorial did not go through how to create one, though I wished they did because I personally found the process non-trivial and could be challenging for new R users. Based on my experience with the [R4DS Book Club Cohort 9 Chapter 8](https://www.youtube.com/watch?v=m3XatUM9qBE), most of us from the cohort group shared that they had issues creating a minimal reproduce example when trying to run `reprex::reprex()` on the console and it gave an error that they don't understand:

`#> Error: attempt to use zero-length variable name`

The error appeared because they did not run any code in the console before running [`reprex::reprex()`](https://reprex.tidyverse.org/reference/reprex.html). I prefer the reprex demo session by [JD Long](https://www.youtube.com/watch?v=0zNPgGa-Cu0) because the presenter shows how to do this step by step or [1littlecoder](https://www.youtube.com/watch?v=hnzrDLf9anw) who showed how to copy and paste the reprex on Github and Stack Overflow.

<iframe width="710" height="390" src="https://www.youtube.com/embed/hnzrDLf9anw" frameborder="0" allowfullscreen>
</iframe>

Due to the limited time, the tutorial could only the following themes:

### Debugging your code

Below are some tips to debug functions that you have access to the source codes.

#### traceback

[`traceback()`](https://rdrr.io/r/base/traceback.html) is useful in locating which function, its corresponding R script name and code line number where the error has occurred. This is a good starting point for beginners. The catch is that the users must remember to [`source`](https://rdrr.io/r/base/source.html) all the R scripts that contain the functions to get an effective message from [`traceback`](https://rdrr.io/r/base/traceback.html).

If the project contains a lot of R scripts with functions, it is better to organise them as a [R package structure](https://r-pkgs.org/structure.html) and run [`devtools::load_all`](https://devtools.r-lib.org/reference/load_all.html).

In addition, if the function contains a variable that is assigned from a long pipe(line) and an error comes from the long pipe(line), it can be hard to identify which code line of the pipeline is causing the issue like the following below:

``` r
results <- data |> 
  task1 |> 
  task2
```

This is because [`traceback()`](https://rdrr.io/r/base/traceback.html) will treat code in the above pipe as `task2(task1(data))` and will inform you that code line number where the error has occurred is the first line the pipe was utilised.

<a href="#top">Back to top</a>

#### rlang::entrace and rlang::last_trace

If the project has many R scripts with custom-made functions, it can be hard to locate the right R script. [`options(error = rlang::entrace)`](https://rlang.r-lib.org/reference/entrace.html) handler with [`rlang::last_trace()`](https://rlang.r-lib.org/reference/last_error.html) can be utilised instead as it not only provides the function, its corresponding R script name and code line number where the error has occurred but also the file path to the R script as well. In RStudio, the file path can be left clicked directly and it brings you to the file and line number where the error happened. This is made possible because [`options(error = rlang::entrace)`]((https://rlang.r-lib.org/reference/entrace.html)) handler converts the base errors to an `rlang` object. Like [`traceback()`](https://rdrr.io/r/base/traceback.html), users must remember to [`source`](https://rdrr.io/r/base/source.html) all the R scripts that contain the functions to get an effective message.

The main disadvantage of [`options(error = rlang::entrace)`](https://rlang.r-lib.org/reference/entrace.html) handler method, as indicated in this [rlang documentation](https://rlang.r-lib.org/reference/global_entrace.html), is that RStudio could only handle one handler per session. If there is a need to use other handlers like [`options(error = recover)`](https://rdrr.io/r/utils/recover.html) or [`options(error = browser)`](https://rdrr.io/r/base/browser.html), you will need to manually switch between [`options(error = rlang::entrace)`](https://rlang.r-lib.org/reference/entrace.html). Thankfully, there is a workaround function to handle this issue called [`rlang::global_entrace`](https://rlang.r-lib.org/reference/global_entrace.html) for people using R version 4.0 and above.

<a href="#top">Back to top</a>

#### browser

In some cases, we may need to troubleshoot because the custom-made function is giving a logical error (or `NA` or `+/-Inf`) and there may be a need to investigate how the input value changes overtime in the custom-made function. Instead of copy and pasting the source code into and R script to debug, it may be easier to type the [`browser()`](https://rdrr.io/r/base/browser.html) function as a breakpoint inside the custom-made function where you are interested to find out the status/value of the input value as well as other variables declared before [`browser()`](https://rdrr.io/r/base/browser.html) function. With the [`browser()`](https://rdrr.io/r/base/browser.html) function breakpoint in place, running the custom-made function will open an interactive debugging session where we can list all available variables (using [`ls.str()`](https://rdrr.io/r/utils/ls_str.html)) and print their assigned values.

In the interactive debugger, there are some [reserved commands like n, s, f, c, Q](https://docs.posit.co/ide/user/ide/guide/code/debugging.html#debugging-commands). If there is a need to call a variable that is the same as the reserved commands like `n`, please type `print(n)` instead of `n` in the `Browse[{some_number}]>` prompt.

[`browser()`](https://rdrr.io/r/base/browser.html) is also useful for creating conditional breakpoints. Here is an example from a [Posit Article](https://docs.posit.co/ide/user/ide/guide/code/debugging.html#stopping-on-a-line) and [Stack Overflow question](https://stackoverflow.com/questions/49008890/how-to-start-debugger-only-when-condition-is-met) showing how to debug after many loop iterations.

However, to use [`browser()`](https://rdrr.io/r/base/browser.html) within a pipe requires the tee pipe [`%T>%`](https://magrittr.tidyverse.org/reference/tee.html).

``` r
results <- mtcars |> 
  dplyr::select(dplyr::all_of(c("mpg", "cyl"))) %T>%  
  browser() |> 
  dplyr::pull(.data[["mpg"]]) %T>% 
  browser() |>
  log() %T>%
  browser() |> 
  mean(na.rm = TRUE)
```

<img src="images/pipe-debug.png" data-fig-align="center" data-fig-alt="Debugging in pipe operator." />

For a short but detailed use of [`browser()`](https://rdrr.io/r/base/browser.html) in a complex function with pipes, check out this example [video](https://www.youtube.com/watch?v=ATIl_JlM9ko) from Bruno Rodrigues.

<iframe width="710" height="390" src="https://www.youtube.com/embed/ATIl_JlM9ko" frameborder="0" allowfullscreen>
</iframe>

<a href="#top">Back to top</a>

#### RStudio IDE Breakpoints and Error Handler

The RStudio IDE also have some useful features for debugging as well.

One of them is by creating multiple breakpoints (without explicitly typing the [`browser()`](https://rdrr.io/r/base/browser.html) function) denoted by a red circle on the left of the code line number of an R script containing functions. This can be done by clicking on the left of the code line number, giving a red hollow circle and then clicking on the source button to turn from a red hollow circle to a filled hollow circle.

<img src="images/hollow_circle.png" data-fig-align="center" data-fig-alt="Breakpoint in hollow circle." />

<img src="images/full_circle.png" data-fig-align="center" data-fig-alt="Breakpoint in full circle." />

If the project is structured as an R package, [`devtools::load_all()`]((https://devtools.r-lib.org/reference/load_all.html)) can be used instead of [`source()`](https://rdrr.io/r/base/source.html).

While this feature is convenient, do note that [not all types of R codes support the red circle breakpoints](https://support.posit.co/hc/en-us/articles/200534337-Breakpoint-Troubleshooting-in-the-RStudio-IDE) and the RStudio IDE [does not support conditional breakpoints](https://adv-r.hadley.nz/debugging.html#alternatives).

The RStudio IDE can also allow users to create different error handler options when an error occurred. This is done by clicking `Debug`, `On Error` and users can choose between `Message Only`, `Error Inspector` or `Break in Code`. Do note that RStudio could only handle one handler per session and if there may be a need to manually change the handler like retyping [`options(error = rlang::entrace)`](https://rlang.r-lib.org/reference/entrace.html).

<img src="images/debug_options.png" data-fig-align="center" data-fig-alt="RStudio IDE error handler options: Message Only, Error Inspector and Break in Code." />

<a href="#top">Back to top</a>

### Debugging other people's code

Below are some tips to debug functions that you do not have access to the scripts holding the source codes (for example, functions from an R package that you have installed) or are not allowed to modify the body of restricted functions (that does not belong to you) based on your company's code management guidelines. As such, you can no longer use `browser()` to create any breakpoints (because you do not have the files containing the source codes to start out with). For convenience, I will call such functions "inaccessible functions".

#### debug, undebug and debugonce

[`debug`](https://rdrr.io/r/base/debug.html) and [`debugonce`](https://rdrr.io/r/base/debug.html) can allow users to at least enter an interactive debugger to view and walkthrough line by line from the beginning (line 1) of source code that runs a given inaccessible function.

The `debug({some_inaccessible_function})` function is equivalence to forcefully run a [`browser()`](https://rdrr.io/r/base/browser.html) breakpoint on the first line of the inaccessible function. In another words, when `debug({some_inaccessible_function})` is executed in the console, the interactive debugger will **always be initiated** each time the inaccessible function is called. To resume calling the inaccessible function without starting the interactive debugger, use `undebug({some_inaccessible_function})`.

An alternative is to type `debugonce({some_inaccessible_function})` so that calling the `some_inaccessible_function` will enter the interactive debugger the next time it runs, but not after that.

<a href="#top">Back to top</a>

#### options(error=recover) and trace

However, it the source codes from the inaccessible function is very long or is built with many nested functions (or in R terms have a large [call stack](https://swcarpentry.github.io/r-novice-inflammation/14-supp-call-stack.html)), it can be tedious to always start the interactive debugger from line 1 of the inaccessible function source codes.

One simple way to handle this is to use [`options(error = recover)`](https://rdrr.io/r/utils/recover.html). When an error occurred, R will let you choose which function in the call stack you want to debug (start from line 1).

A more complicated but flexible option is to use [`trace()`](https://rdrr.io/r/base/trace.html) which allows users to open the interactive debugger at any location in a function. [`trace()`](https://rdrr.io/r/base/trace.html) can also be used to [debug methods (in japanese)](https://kohske.wordpress.com/2011/05/14/debug-in-r-6-debug-in-s4r5-classes/) from S4 or R6 classes.

The basic syntax is as follows:

``` r
trace(what = some_inaccessible_function,
      tracer = some_R_expression usually browser, 
      at = code_line_number)
```

Like [`debug`](https://rdrr.io/r/base/debug.html), after calling `trace({some_inaccessible_function})` in the console, the interactive debugger will **always be initiated** each time the inaccessible function is called. To resume calling the inaccessible function without starting the interactive debugger, use `untrace({some_inaccessible_function})`.

<a href="#top">Back to top</a>

### Other Debugging Techniques

As I was visiting the booth from [Cynkra](https://www.cynkra.com/), some of the team members shared that they have used the R package [`flow`](https://moodymudskipper.github.io/flow/index.html) to assist in the debugging process because the R package is able to convert the logic of a given R function into a flow diagram. For a mini summary of how the [`flow`](https://moodymudskipper.github.io/flow/index.html) package is used, check out this [blog post](https://cosimameyer.com/post/mastering-debugging-in-r/) from [Cosima Meyer](https://github.com/cosimameyer).

The tutorial is heavily focused on debugging R functions. A question was raised if there are any useful tips for debugging in a Quarto Document or Shiny Application. Below are some links that can help.

-   Quarto
    -   <https://docs.posit.co/ide/user/ide/guide/code/debugging.html#debugging-in-quarto-documents>
    -   <https://qmd4sci.njtierney.com/common-problems.html>
-   Shiny
    -   <https://docs.posit.co/ide/user/ide/guide/code/debugging.html#debugging-in-shiny-applications>

<a href="#top">Back to top</a>

### Debugging Tutorial Resources

-   📝[Slides](https://rstats-wtf.github.io/wtf-debugging-slides/)
-   💻[RStudio Session](bit.ly/useR-debugging)
-   👩🏻‍💻[Github Code](https://github.com/rstats-wtf/wtf-debugging)

<a href="#top">Back to top</a>

## Building Effective Docker 🐳 Images: R Edition

The afternoon session was conducted by [Andrew Collier](https://www.datawookie.dev/blog/) from [Fathom Data](https://www.fathomdata.dev/), which covered the basics of Docker so that an R user, with limited programming experience, is able to create an image, that contains R, RStudio (if needed), R packages with their corresponding system dependencies installed, such that the image is able to run some R scripts. I have to commend that Andrew's slides are very eye-catching and have a lot of pictorial analogies are used to describe what the docker command actually does.

### Images and Containers Management

Andrew provides a useful analogy that a Docker image is like a cookie cutter which provides a template to create many Docker containers (or cookies of similar shape to the cookie cutter but can come various sizes). The images (cookie cutter) come from a [registry](https://hub.docker.com/search?image_filter=official) (bakery shop).

The command `docker pull <image_name>[:tag]` downloads a copy of the image while `docker run` creates a container from the image and runs it. There are optional commands for `docker run` such as `-d` that tells Docker to run the container in the background, `-it` to run the container in an interactive terminal and `--name <some_container_name>` to give the running container a memorable name. If we forget to give a container name, Docker will give the container a random name.

To stop a running container, we must first identify the running container's name by listing all container (including stopped containers) using the command `docker ps -a`. Once the name is identified, we can stop the container using the command `docker stop <some_container_name>`

A practical session was conducted for users to pull and run different version of the `r-base` Docker image.

<a href="#top">Back to top</a>

### Ports and Volumes

By default, a Docker container is a sealed environment. It is not possible for host files (or other inputs) to enter the container and results (or other outputs) generated in the Docker container to leave the container. We need to create ports (gates) for both the host and containers and map (connect) them so that they can communicate with each other. This can be done using `-p <host port>:<container port>` option in the `docker run` command.

Next, as the Docker container has a different file system from the host, there is a need to mount the host files or folders in order for the Docker container to have access to them. This can be done using `-v <host file>:<container file>` option in the `docker run` command.

A practical session was conducted for users to pull and run an `r-base` Docker image with R package [crayon](https://r-lib.github.io/crayon/).

<a href="#top">Back to top</a>

### Dockerfile

A `Dockerfile` is a text file that contains a list of commands to create Docker images. The command `docker build [-t <image_name>[:tag]] <output_image_file_path>` tries to find the file `Dockerfile` in the directory the command has been called and build a Docker image called `<image_name>[:tag]` in `<output_image_file_path>`. The tutorial also went through some basic `Dockerfile` commands.

| Commands | Description                                |
|----------|--------------------------------------------|
| `FROM`   | Specify the base image.                    |
| `LABEL`  | Add metadata.                              |
| `RUN`    | Execute a command at build time.           |
| `COPY`   | Copy file or directory from host to image. |
| `ENV`    | Create an environment variable.            |
| `CMD`    | Execute a command at run time.             |

A practical session was conducted for users to pull and run an RStudio Docker image.

<a href="#top">Back to top</a>

### Installing Packages

Andrew then highlighted a few ways to install R packages in the Docker command.

#### System Package Management System

According to the [Rocker Project](https://rocker-project.org/use/extending.html#system-package-management-system), there are Linux distributions that allows installation of binary R packages with the system package management system. R packages (like [jsonlite](https://cran.r-project.org/web/packages/jsonlite/index.html)) can be installed with the `apt-get-install` command.

    FROM rocker/r-ver:latest

    RUN apt-get update && \
        apt-get install -y --no-install-recommends \
        r-cran-jsonlite && \
        rm -rf /var/lib/apt/lists/*

    ENV R_LIBS_USER /usr/lib/R/site-library/

A downside is that there is a need to specify an installation folder and the R package installed can lag quite behind its latest version.

#### Posit Pubic Package Manager and littler

Another way is to make use of the [Posit Public Package Manager](https://packagemanager.posit.co/client/) (P3M) as CRAN mirror to install binary version of packages.

    FROM rocker/r-ver:latest

    # If you want to install from source.
    #
    # RUN R -e "options(repos = 'https://cloud.r-project.org/')"

    RUN R -e 'install.packages(c("jsonlite", "remotes"))'
    RUN R -e 'remotes::install_github("datawookie/emayili")'

Another way is to use the [littler](https://eddelbuettel.github.io/littler/) package.

    FROM rocker/r-ver:latest

    RUN install2.r jsonlite remotes

    RUN installGithub.r datawookie/emayili

Do note that some packages (e.g. [rvest](https://rvest.tidyverse.org/) and [Rcpp](https://www.rcpp.org/)) will fail to load if the required additional system prerequisites libraries for the package are not installed.

    FROM rocker/r-base:latest

    RUN apt-get update -q && \ 
        apt-get install -qq -y \ 
        libssl-dev \ 
        libxml2-dev \ 
        libcurl4-openssl-dev
        
    RUN install2.r rvest

A practical session was conducted for users to pull and run an RStudio Docker image that scrape USD exchange rates.

<a href="#top">Back to top</a>

### Metadata

The `LABEL` command (of the form `LABEL <key-string>=<value-string>`) in `Dockerfile` helps to add metadata about the Docker image. Here are some examples.

    LABEL maintainer="Your Name <email_address>"
          version="Version Number"
          description="Your description"

<a href="#top">Back to top</a>

### Docker Registry

The tutorial also teaches users how to push a Docker image into the [Docker Hub](https://hub.docker.com/). The first step is to log into [Docker Hub](https://hub.docker.com/) using the command `docker login [-u USERNAME] [-p PASSWORD]`. Assuming that we have built a Docker image called `<image_name>[:tag]`, [change the image name](https://stackoverflow.com/questions/25211198/docker-how-to-change-repository-name-or-rename-image) of the form `<image_name>[:tag]` to `<user_name/image_name>[:tag]`, using the command `docker image tag <image_name>[:tag] <user_name/image_name>[:tag]`. Lastly, push the image to [Docker Hub](https://hub.docker.com/) using the command `docker push <user_name/image_name>[:tag]`

<a href="#top">Back to top</a>

### Optimising Build Speed

Recall that the command `docker build [-t <image_name>[:tag]] <output_image_file_path>` tries to find the file `Dockerfile` in the directory the command has been called and build a Docker image called `<image_name>[:tag]` in `<output_image_file_path>`. During the building phase, all files in the directory where the command has been called will also be copied into the Docker image. TO reduce the build time, it is recommended to exclude unnecessary files by listing them in the `.dockerignore` file, especially files that contain sensitive information.

Unnecessary files includes

-   data files (*.csv, *.xlsx, \*.rds or data/)
-   documentation (*.doc, *.pdf)
-   hidden files (.Renviron, .Rprofile)
-   session files (.RData, .Rhistory)

Each command in `Dockerfile` creates a new building layer. Though the layers are cached, if a layer needs to be rebuilt, then all subsequent layers will also need to be rebuilt. This means the order of how the layers are built matters. It is advised to start building layers from the most stable (or layers that do not change often) to the least.

    # Base image will hardly change
    FROM alpine:latest

    # System dependecies will seldom change
    RUN apk add --no-cache nginx

    # NINX configuration may change
    COPY default.conf /etc/nginx/http.d/

    # Page content and command will change frequently
    COPY index.html /usr/share/nginx/html/

    CMD ["nginx", "-g", "daemon off;"]

<a href="#top">Back to top</a>

### Optimising Image Size

There are several factors that can affect the image.

The first one is the size of the base image. It is advised to choose a minimal base image and avoid having an image with software, like RStudio or R packages that you do not need.

-   Prefer `rocker/r-base` to `rocker/r-ver`
-   Prefer `rocker/r-ver` to `rocker/rstudio`
-   Prefer `rocker/rstudio` to `rocker/cuda`

The next tip is to consolidate layers that have a similar command.

✅ Do this:

    RUN R -e "install.packages('forcats')" && \
        R -e "install.packages('here')" && \
        R -e "install.packages('httr')"

⛔Avoid this:

    RUN R -e "install.packages('forcats')"
    RUN R -e "install.packages('here')"
    RUN R -e "install.packages('httr')"

The last tip is to avoid installing unnecessary system dependencies and documentations and have code that cleans up after installation of system dependencies and R packages.

Here are some ways on how this can be done in the `RUN` command.

`apt-get install -qq -y --no-install-recommends`

This command skips the installation of [some ubuntu recommended packages](https://ubuntu.com/blog/we-reduced-our-docker-images-by-60-with-no-install-recommends). It is important to note that doing this could result in some missing system libraries that needs to be added back.

`rm -rf /var/lib/apt/lists/*`

This command removes cached package lists.

`rm -rf /tmp/downloaded_packages/`

This command removes downloaded packages.

`strip /usr/local/lib/R/site-library/*/libs/*.so`

This command will [strip the dynamic libraries](https://github.com/rocker-org/rocker-versioned2/issues/340) after installation of binary R packages, reducing the image size.

`"install.packages('plumber', INSTALL_opts = c('--no-docs'))"`

This command will install the R packages without the documentation or vignette files.

A practical session was conducted for users to pull and run an RStudio Docker image that has a simple API that extract text from an uploaded image using Optical Character Recognition.

Here is the difference in image size for the following Docker commands (ocr-api-default vs ocr-api-clean) for this practical session.

#### ocr-api-default

    FROM rocker/r-base

    LABEL maintainer="Jeremy Selva"
    LABEL version="0.1.0"
    LABEL description="An API for Optical Character Recognition (OCR)"

    RUN apt-get update -q && \ 
        apt-get install -qq -y \ 
            libmagick++-dev \ 
            libtesseract-dev \ 
            libpoppler-cpp-dev \
            libsodium-dev \ 
            tesseract-ocr-eng && \
        install2.r -e \ 
          plumber \ 
          tesseract \ 
          magick

    COPY api.R run.R ./

    CMD ["Rscript", "run.R"]

<img src="images/ocr-api-default-size.png" data-fig-align="center" data-fig-alt="Layer size of RUN command is 473.73 MB." />

#### ocr-api-clean

    FROM rocker/r-base

    LABEL maintainer="Jeremy Selva" \
          version="0.1.0" \
          description="An API for Optical Character Recognition (OCR)"

    RUN apt-get update -qq && \ 
        apt-get install -qq -y --no-install-recommends \
            libmagick++-dev \ 
            libtesseract-dev \ 
            libpoppler-cpp-dev \
            libsodium-dev \ 
            tesseract-ocr-eng && \
        rm -rf /var/lib/apt/lists/* && \
        R -q -e "install.packages('plumber', INSTALL_opts = c('--no-docs'))"  && \
        R -q -e "install.packages('tesseract', INSTALL_opts = c('--no-docs'))"  && \
        R -q -e "install.packages('magick', INSTALL_opts = c('--no-docs'))"  && \
        rm -rf /tmp/downloaded_packages/ && \
        strip /usr/local/lib/R/site-library/*/libs/*.so

    COPY api.R run.R ./

    CMD ["Rscript", "run.R"]

<img src="images/ocr-api-clean-size.png" data-fig-align="center" data-fig-alt="Layer size of RUN command is 392.03 MB." />

<a href="#top">Back to top</a>

### Docker Tutorial Resources

-   📝[Slides](https://bit.ly/user-salzburg-building-effective-docker-images)

<a href="#top">Back to top</a>
