---
title: "Cleaning Lipid Names Part 1"
subtitle: ""
excerpt: "This post provides some tips on how to clean lipid names input suited for some current nomenclature tools using R"
date: 2022-01-22
author: "Jeremy Selva"
draft: true
images:
series:
tags:
categories:
layout: single
bibliography: utils/bibliography.bib
csl: utils/f1000research.csl
---

<script src="{{< blogdown/postref >}}index_files/core-js/shim.min.js"></script>
<script src="{{< blogdown/postref >}}index_files/react/react.min.js"></script>
<script src="{{< blogdown/postref >}}index_files/react/react-dom.min.js"></script>
<script src="{{< blogdown/postref >}}index_files/reactwidget/react-tools.js"></script>
<script src="{{< blogdown/postref >}}index_files/htmlwidgets/htmlwidgets.js"></script>
<script src="{{< blogdown/postref >}}index_files/reactable-binding/reactable.js"></script>
<script src="{{< blogdown/postref >}}index_files/htmlwidgets/htmlwidgets.js"></script>
<link href="{{< blogdown/postref >}}index_files/str_view/str_view.css" rel="stylesheet" />
<script src="{{< blogdown/postref >}}index_files/str_view-binding/str_view.js"></script>
<script src="{{< blogdown/postref >}}index_files/htmlwidgets/htmlwidgets.js"></script>
<link href="{{< blogdown/postref >}}index_files/str_view/str_view.css" rel="stylesheet" />
<script src="{{< blogdown/postref >}}index_files/str_view-binding/str_view.js"></script>
<script src="{{< blogdown/postref >}}index_files/htmlwidgets/htmlwidgets.js"></script>
<link href="{{< blogdown/postref >}}index_files/str_view/str_view.css" rel="stylesheet" />
<script src="{{< blogdown/postref >}}index_files/str_view-binding/str_view.js"></script>
<script src="{{< blogdown/postref >}}index_files/htmlwidgets/htmlwidgets.js"></script>
<link href="{{< blogdown/postref >}}index_files/str_view/str_view.css" rel="stylesheet" />
<script src="{{< blogdown/postref >}}index_files/str_view-binding/str_view.js"></script>
<script src="{{< blogdown/postref >}}index_files/htmlwidgets/htmlwidgets.js"></script>
<link href="{{< blogdown/postref >}}index_files/str_view/str_view.css" rel="stylesheet" />
<script src="{{< blogdown/postref >}}index_files/str_view-binding/str_view.js"></script>
<script src="{{< blogdown/postref >}}index_files/htmlwidgets/htmlwidgets.js"></script>
<link href="{{< blogdown/postref >}}index_files/str_view/str_view.css" rel="stylesheet" />
<script src="{{< blogdown/postref >}}index_files/str_view-binding/str_view.js"></script>
<script src="{{< blogdown/postref >}}index_files/htmlwidgets/htmlwidgets.js"></script>
<link href="{{< blogdown/postref >}}index_files/str_view/str_view.css" rel="stylesheet" />
<script src="{{< blogdown/postref >}}index_files/str_view-binding/str_view.js"></script>
<script src="{{< blogdown/postref >}}index_files/htmlwidgets/htmlwidgets.js"></script>
<link href="{{< blogdown/postref >}}index_files/str_view/str_view.css" rel="stylesheet" />
<script src="{{< blogdown/postref >}}index_files/str_view-binding/str_view.js"></script>
<script src="{{< blogdown/postref >}}index_files/htmlwidgets/htmlwidgets.js"></script>
<link href="{{< blogdown/postref >}}index_files/str_view/str_view.css" rel="stylesheet" />
<script src="{{< blogdown/postref >}}index_files/str_view-binding/str_view.js"></script>

# Introduction

Despite efforts made to unified lipids shorthand notations and the rise of software dedicated to standardise lipid annotations, lipid names still remains diverse. This is due to limited ways lipid software may label a lipid and/or researchers’ personal preferences to annotate them.

Here, I would like to highlight some lipid annotations that my workplace uses and show how to modify them in R such that it can be processed by lipid annotations converter tools.

# Labels to clean

Here are the list of lipid names to clean

| Given Name              | Clean Name | Precursor Ion | Product Ion |
|-------------------------|------------|---------------|-------------|
| LPC 13:0 (ISTD) (a)     | LPC 13:0   | 454.3         | 184.1       |
| LPC 13:0 (ISTD) (a\\b)  | LPC 13:0   | 454.3         | 184.1       |
| LPC 13:0 (ISTD) (b)     | LPC 13:0   | 454.3         | 184.1       |
| LPC 15:0-d5 (IS) (a)    | LPC 15:0   | 487.4         | 304.3       |
| LPC 15:0-d5 (IS) (a\\b) | LPC 15:0   | 487.4         | 304.3       |
| LPC 15:0-d5 (IS) (b)    | LPC 15:0   | 487.4         | 304.3       |
| LPC 17:1 (a)            | LPC 17:1   | 508.3         | 184.1       |
| LPC 17:1 (a/b/c)        | LPC 17:1   | 508.3         | 184.1       |
| LPC 17:1 (b)            | LPC 17:1   | 508.3         | 184.1       |
| LPC 17:1 (c)            | LPC 17:1   | 508.3         | 184.1       |

The task is to remove the variations of (ISTD), (a\\b\\c\\d) and the -d5

### Libraries Used

``` r
library("flair")
library("reactable")
library("here")
library("readxl")
library("magrittr")
library("stringr")
```

### Read Data

``` r
annotation_data <- readxl::read_excel(
  path = here::here("content", 
                    "blog",
                    "2022-01-22-Clean-Lipid-Names-1",
                    "Annotation.xlsx"),
  sheet = "Transition_Name_Annot"
  )

reactable::reactable(annotation_data, defaultPageSize = 5)
```

<div id="htmlwidget-1" class="reactable html-widget" style="width:auto;height:auto;"></div>
<script type="application/json" data-for="htmlwidget-1">{"x":{"tag":{"name":"Reactable","attribs":{"data":{"Transition_Name":["LPC 13:0 (ISTD) (a)","LPC 13:0 (ISTD) (a\\b)","LPC 13:0 (ISTD) (b)","LPC 15:0-d5 (IS) (a)","LPC 15:0-d5 (IS) (a\\b)","LPC 15:0-d5 (IS) (b)","LPC 17:1 (a)","LPC 17:1 (a/b/c)","LPC 17:1 (b)","LPC 17:1 (c)"],"Precursor Ion":[454.3,454.3,454.3,487.4,487.4,487.4,508.3,508.3,508.3,508.3],"Product Ion":[184.1,184.1,184.1,304.3,304.3,304.3,184.1,184.1,184.1,184.1]},"columns":[{"accessor":"Transition_Name","name":"Transition_Name","type":"character"},{"accessor":"Precursor Ion","name":"Precursor Ion","type":"numeric"},{"accessor":"Product Ion","name":"Product Ion","type":"numeric"}],"defaultPageSize":5,"paginationType":"numbers","showPageInfo":true,"minRows":1,"dataKey":"735619341f0c70cc6c36cf6011d0831c","key":"735619341f0c70cc6c36cf6011d0831c"},"children":[]},"class":"reactR_markup"},"evals":[],"jsHooks":[]}</script>

# The Plan

We will do the following in order

1.  Remove the -d5

2.  Remove the ISTD and its variations

3.  Remove the (a\\b\\c) and its variations

The idea is to first use `stringr::str_view` to check what the matched pattern is. Once the matched pattern is correct, we can use `stringr::str_remove` function to clean up the matched pattern.

# Remove -d5

Here is an example to remove the -d5 using `stringr::str_view`. Simply just set the pattern as “-d5”

``` r
stringr::str_view("LPC 15:0-d5 (IS) (a)", pattern = "-d5")
```

<div id="htmlwidget-2" style="width:960px;height:100%;" class="str_view html-widget"></div>
<script type="application/json" data-for="htmlwidget-2">{"x":{"html":"<ul>\n  <li>LPC 15:0<span class='match'>-d5<\/span> (IS) (a)<\/li>\n<\/ul>"},"evals":[],"jsHooks":[]}</script>

``` r
stringr::str_remove("LPC 15:0-d5 (IS) (a)", pattern = "-d5")
```

    ## [1] "LPC 15:0 (IS) (a)"

# Remove the ISTD variation

The first challenge is to create a pattern that is able to remove variations of ISTD such as `(ISTD)` and `(IS)`

## Detect the word ISTD

To detect the word ISTD, we can do this in R

``` r
stringr::str_view("LPC 13:0 (ISTD) (a)", pattern = "ISTD")
```

<div id="htmlwidget-3" style="width:960px;height:100%;" class="str_view html-widget"></div>
<script type="application/json" data-for="htmlwidget-3">{"x":{"html":"<ul>\n  <li>LPC 13:0 (<span class='match'>ISTD<\/span>) (a)<\/li>\n<\/ul>"},"evals":[],"jsHooks":[]}</script>

Unfortunately, this will not work with the word IS

``` r
stringr::str_view("LPC 15:0-d5 (IS) (a)", pattern = "ISTD")
```

<div id="htmlwidget-4" style="width:960px;height:100%;" class="str_view html-widget"></div>
<script type="application/json" data-for="htmlwidget-4">{"x":{"html":"<ul>\n  <li>LPC 15:0-d5 (IS) (a)<\/li>\n<\/ul>"},"evals":[],"jsHooks":[]}</script>

Alternatively to detect the word IS, we can do this in R

``` r
stringr::str_view("LPC 15:0-d5 (IS) (a)", pattern = "IS")
```

<div id="htmlwidget-5" style="width:960px;height:100%;" class="str_view html-widget"></div>
<script type="application/json" data-for="htmlwidget-5">{"x":{"html":"<ul>\n  <li>LPC 15:0-d5 (<span class='match'>IS<\/span>) (a)<\/li>\n<\/ul>"},"evals":[],"jsHooks":[]}</script>

This time, this will not work with the word ISTD

``` r
stringr::str_view("LPC 13:0 (ISTD) (a)", pattern = "IS")
```

<div id="htmlwidget-6" style="width:960px;height:100%;" class="str_view html-widget"></div>
<script type="application/json" data-for="htmlwidget-6">{"x":{"html":"<ul>\n  <li>LPC 13:0 (<span class='match'>IS<\/span>TD) (a)<\/li>\n<\/ul>"},"evals":[],"jsHooks":[]}</script>

To detect words of the form IS and ISTD, we can make use of the fact that the group “TD” in “ISTD” appear zero or one time. Referring to the cheat sheet of `stringr`, we can make use of parentheses to create a group.

Hence, adding the group to the existing pattern, we have the form `IS(TD)`.

Next, we inform `stringr` that the group `(TD)` can appear zero or one time. Referring to the cheat sheet of `stringr`, we can make use of the `?` symbol

This give our updated pattern to `IS(TD)?`

Putting this to our existing list of words, we have

``` r
stringr::str_view(annotation_data$Transition_Name, pattern = "IS(TD)?")
```

<div id="htmlwidget-7" style="width:960px;height:100%;" class="str_view html-widget"></div>
<script type="application/json" data-for="htmlwidget-7">{"x":{"html":"<ul>\n  <li>LPC 13:0 (<span class='match'>ISTD<\/span>) (a)<\/li>\n  <li>LPC 13:0 (<span class='match'>ISTD<\/span>) (a\\b)<\/li>\n  <li>LPC 13:0 (<span class='match'>ISTD<\/span>) (b)<\/li>\n  <li>LPC 15:0-d5 (<span class='match'>IS<\/span>) (a)<\/li>\n  <li>LPC 15:0-d5 (<span class='match'>IS<\/span>) (a\\b)<\/li>\n  <li>LPC 15:0-d5 (<span class='match'>IS<\/span>) (b)<\/li>\n  <li>LPC 17:1 (a)<\/li>\n  <li>LPC 17:1 (a/b/c)<\/li>\n  <li>LPC 17:1 (b)<\/li>\n  <li>LPC 17:1 (c)<\/li>\n<\/ul>"},"evals":[],"jsHooks":[]}</script>

## Detect Parenthesis

The way to detect `(` and `)` is unfortunately not as simple as `stringr::str_view_all("LPC 13:0 (ISTD) (a)", pattern = "(")`, giving rise to this error message.

This is because `(` and `)` fall under a group called “meta characters” that have other functions in regular expression. In fact, we have just explained what it does earlier which is to group characters together.

``` r
stringr::str_view_all("LPC 13:0 (ISTD) (a)", pattern = "\\(")
```

<div id="htmlwidget-8" style="width:960px;height:100%;" class="str_view html-widget"></div>
<script type="application/json" data-for="htmlwidget-8">{"x":{"html":"<ul>\n  <li>LPC 13:0 <span class='match'>(<\/span>ISTD) <span class='match'>(<\/span>a)<\/li>\n<\/ul>"},"evals":[],"jsHooks":[]}</script>

``` r
stringr::str_view_all(annotation_data$Transition_Name, pattern = "\\)")
```

<div id="htmlwidget-9" style="width:960px;height:100%;" class="str_view html-widget"></div>
<script type="application/json" data-for="htmlwidget-9">{"x":{"html":"<ul>\n  <li>LPC 13:0 (ISTD<span class='match'>)<\/span> (a<span class='match'>)<\/span><\/li>\n  <li>LPC 13:0 (ISTD<span class='match'>)<\/span> (a\\b<span class='match'>)<\/span><\/li>\n  <li>LPC 13:0 (ISTD<span class='match'>)<\/span> (b<span class='match'>)<\/span><\/li>\n  <li>LPC 15:0-d5 (IS<span class='match'>)<\/span> (a<span class='match'>)<\/span><\/li>\n  <li>LPC 15:0-d5 (IS<span class='match'>)<\/span> (a\\b<span class='match'>)<\/span><\/li>\n  <li>LPC 15:0-d5 (IS<span class='match'>)<\/span> (b<span class='match'>)<\/span><\/li>\n  <li>LPC 17:1 (a<span class='match'>)<\/span><\/li>\n  <li>LPC 17:1 (a/b/c<span class='match'>)<\/span><\/li>\n  <li>LPC 17:1 (b<span class='match'>)<\/span><\/li>\n  <li>LPC 17:1 (c<span class='match'>)<\/span><\/li>\n<\/ul>"},"evals":[],"jsHooks":[]}</script>

``` r
stringr::str_view_all(annotation_data$Transition_Name, pattern = "\\s*\\(IS(TD)?\\)\\s*")
```

<div id="htmlwidget-10" style="width:960px;height:100%;" class="str_view html-widget"></div>
<script type="application/json" data-for="htmlwidget-10">{"x":{"html":"<ul>\n  <li>LPC 13:0<span class='match'> (ISTD) <\/span>(a)<\/li>\n  <li>LPC 13:0<span class='match'> (ISTD) <\/span>(a\\b)<\/li>\n  <li>LPC 13:0<span class='match'> (ISTD) <\/span>(b)<\/li>\n  <li>LPC 15:0-d5<span class='match'> (IS) <\/span>(a)<\/li>\n  <li>LPC 15:0-d5<span class='match'> (IS) <\/span>(a\\b)<\/li>\n  <li>LPC 15:0-d5<span class='match'> (IS) <\/span>(b)<\/li>\n  <li>LPC 17:1 (a)<\/li>\n  <li>LPC 17:1 (a/b/c)<\/li>\n  <li>LPC 17:1 (b)<\/li>\n  <li>LPC 17:1 (c)<\/li>\n<\/ul>"},"evals":[],"jsHooks":[]}</script>

# References
