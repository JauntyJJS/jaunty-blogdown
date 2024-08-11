---
title: Learning Journey in the useR! 2024 Conference Part 2
subtitle: ''
excerpt: >-
  This narrative is a write up of my learning journey in the [useR! 2024
  Conference](https://events.linuxfoundation.org/user/).
format: hugo-md
date: 2024-07-07T00:00:00.000Z
author: Jeremy Selva
draft: true
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
-   [Formal Debugging in R](#formal-debugging-in-r)
-   [Building Effective Docker Images: R Edition](#building-effective-docker-images-r-edition)

## Introduction

On the first day of the [useR! 2024 Conference](https://events.linuxfoundation.org/user/), I had attending two tutorial sessions. Here are my thoughts about them.

<a href="#top">Back to top</a>

## Formal Debugging in R

What I have always done when R has an error is to comment everything and run the code one line at a time in a painstaking way. If an error occurs in my custom made functions, I usually copy the source code into my R script and then test them line by line. If an error occurs during the for loop, I usually just `print()/cat()/message()` the output and the iteration number to see where the issue is. I never knew that R has some useful functions that can be used for debugging errors in a less tedious way until I attended this session from [Shannon Pileggi](https://www.pipinghotdata.com/) and [Maëlle Salmon](https://masalmon.eu/)

The tutorial started light with some tips on basic troubleshooting, such as

-   Samantha Csik's [talk](https://www.youtube.com/watch?v=93WsFQUuxvA) and [slides](https://samanthacsik.github.io/teach-me-how-to-google/slides/RLadiesSTL-2022-02-22.html) on how to effectively use search engines like Google to find solutions.

-   Learning how to restarting R in a [blank state](https://rstats.wtf/source-and-blank-slates) without saving the workspace and without restoring a saved workspace.

-   Using a [reprex](https://reprex.tidyverse.org/). The tutorial did not go through how to create one, though I wish they do because I personally find it non-trivial and can be challenging for new R users based on my experience with the [R4DS Book Club Cohort 9 Chapter 8](https://www.youtube.com/watch?v=m3XatUM9qBE). Most of us from the cohort group shared that they have issues creating a minimal reproduce example when trying to run `reprex::reprex()` on the console and it gives an error: `#> Error: attempt to use zero-length variable name` that they don't understand. (The error appeared because they did not run any code in the console before running `reprex::reprex()`) I prefer the reprex demo session by [JD Long](https://www.youtube.com/watch?v=0zNPgGa-Cu0) because the presenter shows how to do this step by step or [1littlecoder](https://www.youtube.com/watch?v=hnzrDLf9anw) who showed how to copy and paste the reprex on Github and Stack Overflow.

Due to the limited time, the tutorial could only the following themes:

### Debugging your code

Below are some tips to debug functions that you have access to the source codes.

#### traceback()

`traceback()` is useful in locating which function, its corresponding R script name and code line number where the error has occurred. This is a good starting point for beginners. The catch is that the users must remember to `source` all the R scripts that contain the functions to get an effective message from `traceback`. If the project contains a lot of R scripts with functions, it is better to organise them as a [R package structure](https://r-pkgs.org/structure.html) and run [`devtools::load_all`](https://devtools.r-lib.org/reference/load_all.html). In addition, if the function contains a variable that is assigned from a long pipe(line) and an error comes from the long pipe(line), it can be hard to identify which code line of the pipeline is causing the issue. This is because `traceback()` will treat code in pipes like

``` r
results <- data |> 
  task1 |> 
  task2
```

as `task2(task1(data))` and will inform you that code line number where the error has occurred is the first line the pipe was utilised.

#### rlang::entrace() and rlang::last_trace()

If the project has many R scripts with custom-made functions, it can be hard to locate the right R script. `options(error = rlang::entrace)` handler with `rlang::last_trace()` can be utilised instead as it not only provides the function, its corresponding R script name and code line number where the error has occurred but also the file path to the R script as well. In RStudio, the file path can be left clicked directly and it brings you to the file and line number where the error happened. This is made possible because `options(error = rlang::entrace)` handler converts the base errors to an `rlang` object. Like `traceback()`, users must remember to `source` all the R scripts that contain the functions to get an effective message.

The main disadvantage of `options(error = rlang::entrace)` handler method, as indicated in this [rlang documentation](https://rlang.r-lib.org/reference/global_entrace.html), is that RStudio could only handle one handler per session. If there is a need to use other handlers like `options(error = recover)` or `options(error = browser)`, you will need to manually switch between `options(error = rlang::entrace)`. Thankfully, there is a workaround function to handle this issue called [`rlang::global_entrace`](https://rlang.r-lib.org/reference/global_entrace.html) for people using R version 4.0 and above.

#### browser()

In some cases, we may need to troubleshoot because the custom-made function is giving a logical error (or NA or +/-Inf) and there may be a need to investigate how the input value changes overtime in the custom-made function. Instead of copy and pasting the source code into and R script to debug, it may be easier to type the `browser()` function as a breakpoint inside the custom-made function where you are interested to find out the status/value of the input value as well as other variables declared before `browser()` function. With the `browser()` function breakpoint in place, running the custom-made function will open an interactive debugging session where we can list all available variables (using `ls.str()`) and print their assigned values.

In the interactive debugger, there are some [reserved commands like n, s, f, c, Q](https://docs.posit.co/ide/user/ide/guide/code/debugging.html#debugging-commands). If there is a need to call a variable that is the same as the reserved commands like `n`, please type `print(n)` instead of `n` in the `Browse[{some_number}]>` prompt.

`browser()` is also useful for creating conditional breakpoints. Here is an example from a [Posit Article](https://docs.posit.co/ide/user/ide/guide/code/debugging.html#stopping-on-a-line) and [Stack Overflow question](https://stackoverflow.com/questions/49008890/how-to-start-debugger-only-when-condition-is-met) showing how to debug after many loop iterations.

However, to use `browser()` within a pipe requires the tee pipe [`%T>%`](https://magrittr.tidyverse.org/reference/tee.html). For a short but detailed use of `browser()` in a complex function with pipes, check out this example [video](https://www.youtube.com/watch?v=ATIl_JlM9ko) from Bruno Rodrigues.

#### RStudio IDE Breakpoints

The RStudio IDE also have some useful features for debugging as well.

One of them is by creating multiple breakpoints (without explicitly typing the `browser()` function) denoted by a red circle on the left of the code line number of an R script containing functions. This can be done by clicking on the left of the code line number, giving a red hollow circle and then clicking on the source button to turn from a red hollow circle to a filled hollow circle. If the project is structured as an R package, `devtools::load_all()` can be used instead of `source()`.

While this feature is convenient, do note that [not all types of R codes support the red circle breakpoints](https://support.posit.co/hc/en-us/articles/200534337-Breakpoint-Troubleshooting-in-the-RStudio-IDE) and the RStudio IDE [does not support conditional breakpoints](https://adv-r.hadley.nz/debugging.html#alternatives).

#### RStudio IDE Error Handler

The RStudio IDE can also allow users to create different error handler options when an error occurred. This is done by clicking `Debug`, `On Error` and users can choose between `Message Only`, `Error Inspector` or `Break in Code`. Do note that RStudio could only handle one handler per session and if there may be a need to manually change the handler like retyping `options(error = rlang::entrace)`.

### Debugging other people's code

Below are some tips to debug functions that you do not have access to the scripts holding the source codes (for example, functions from an R package that you have installed) or are not allowed to modify the body of restricted functions (that does not belong to you) based on your company's code management guidelines. As such, you can no longer use `browser()` to create any breakpoints (because you do not have the files containing the source codes to start out with). For convenience, I will call such functions "inaccessible functions".

#### debug, undebug and debugonce

`debug` and `debugonce` can allow users to at least enter an interactive debugger to view and walkthrough line by line from the beginning (line 1) of source code that runs a given inaccessible function.

The `debug({some_inaccessible_function})` function is equivalence to forcefully run a `broswer()` breakpoint on the first line of the inaccessible function. In another words, when `debug({some_inaccessible_function})` is executed in the console, the interactive debugger will **always be initiated** each time the inaccessible function is called. To resume calling the inaccessible function without starting the interactive debugger, use `undebug({some_inaccessible_function})`.

An alternative is to type `debugonce({some_inaccessible_function})` so that calling the `some_inaccessible_function` will enter the interactive debugger the next time it runs, but not after that.

#### options(error=recover) and trace

However, it the source codes from the inaccessible function is very long or is built with many nested functions (or in R terms have a large [call stack](https://swcarpentry.github.io/r-novice-inflammation/14-supp-call-stack.html)), it can be tedious to always start the interactive debugger from line 1 of the inaccessible function source codes.

One simple way to handle this is to use `options(error=recover)`. When an error occurred, R will let you choose which function in the call stack you want to debug (start from line 1).

A more complicated but flexible option is to use `trace()` which allows users to open the interactive debugger at any location in a function. `trace()` can also be used to [debug methods (in japanese)](https://kohske.wordpress.com/2011/05/14/debug-in-r-6-debug-in-s4r5-classes/) from S4 or R6 classes.

The basic syntax is as follows:

``` r
trace(what = some_inaccessible_function,
      tracer = some_R_expression usually browser, 
      at = code_line_number)
```

Like `debug`, after calling `trace({some_inaccessible_function})` in the console, the interactive debugger will **always be initiated** each time the inaccessible function is called. To resume calling the inaccessible function without starting the interactive debugger, use `untrace({some_inaccessible_function})`.

https://shiny.abdn.ac.uk/Stats/debugging/
https://cosimameyer.com/post/mastering-debugging-in-r/

-   📝[Slides](https://rstats-wtf.github.io/wtf-debugging-slides/)
-   💻[RStudio Session](bit.ly/useR-debugging)
-   👩🏻‍💻[Github Code](https://github.com/rstats-wtf/wtf-debugging)

<a href="#top">Back to top</a>

## Building Effective Docker Images: R Edition

Linux - https://datawookie.dev/blog/2024/06/installing-docker-on-linux/
macOS - https://datawookie.dev/blog/2024/06/installing-docker-on-macos/
Windows - https://datawookie.dev/blog/2024/06/installing-docker-on-windows/

[Andrew Collier](https://www.datawookie.dev/blog/)

https://bit.ly/user-salzburg-building-effective-docker-images.

-   📝[Slides](https://bit.ly/user-salzburg-building-effective-docker-images)

<a href="#top">Back to top</a>

https://www.restaurant-stieglkeller.at/en/eventlocation/raeumlichkeiten-eventlocation/
