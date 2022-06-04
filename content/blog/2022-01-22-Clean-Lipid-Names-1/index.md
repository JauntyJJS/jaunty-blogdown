---
title: "Cleaning Lipid Names for Annotation Part 1"
subtitle: ""
excerpt: "This post provides some tips on how to clean lipid names input suited for some current nomenclature tools using R"
date: 2022-01-30
author: "Jeremy Selva"
draft: false
images:
series:
tags:
categories:
layout: single-sidebar
bibliography: utils/bibliography.bib
csl: utils/f1000research.csl
---

<script src="{{< blogdown/postref >}}index_files/clipboard/clipboard.min.js"></script>
<link href="{{< blogdown/postref >}}index_files/xaringanExtra-clipboard/xaringanExtra-clipboard.css" rel="stylesheet" />
<script src="{{< blogdown/postref >}}index_files/xaringanExtra-clipboard/xaringanExtra-clipboard.js"></script>
<script>window.xaringanExtraClipboard(null, {"button":"<i class=\"fa fa-clipboard\"><\/i> Copy Code","success":"<i class=\"fa fa-check\" style=\"color: #90BE6D\"><\/i> Copied!","error":"Press Ctrl+C to Copy"})</script>
<link href="{{< blogdown/postref >}}index_files/font-awesome/css/all.css" rel="stylesheet" />
<link href="{{< blogdown/postref >}}index_files/font-awesome/css/v4-shims.css" rel="stylesheet" />
<script src="{{< blogdown/postref >}}index_files/core-js/shim.min.js"></script>
<script src="{{< blogdown/postref >}}index_files/react/react.min.js"></script>
<script src="{{< blogdown/postref >}}index_files/react/react-dom.min.js"></script>
<script src="{{< blogdown/postref >}}index_files/reactwidget/react-tools.js"></script>
<script src="{{< blogdown/postref >}}index_files/htmlwidgets/htmlwidgets.js"></script>
<script src="{{< blogdown/postref >}}index_files/reactable-binding/reactable.js"></script>
<script src="{{< blogdown/postref >}}index_files/core-js/shim.min.js"></script>
<script src="{{< blogdown/postref >}}index_files/react/react.min.js"></script>
<script src="{{< blogdown/postref >}}index_files/react/react-dom.min.js"></script>
<script src="{{< blogdown/postref >}}index_files/reactwidget/react-tools.js"></script>
<script src="{{< blogdown/postref >}}index_files/htmlwidgets/htmlwidgets.js"></script>
<script src="{{< blogdown/postref >}}index_files/reactable-binding/reactable.js"></script>
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
<script src="{{< blogdown/postref >}}index_files/core-js/shim.min.js"></script>
<script src="{{< blogdown/postref >}}index_files/react/react.min.js"></script>
<script src="{{< blogdown/postref >}}index_files/react/react-dom.min.js"></script>
<script src="{{< blogdown/postref >}}index_files/reactwidget/react-tools.js"></script>
<script src="{{< blogdown/postref >}}index_files/htmlwidgets/htmlwidgets.js"></script>
<script src="{{< blogdown/postref >}}index_files/reactable-binding/reactable.js"></script>

## Introduction

Despite efforts made to unified lipids shorthand notations and the rise of software dedicated to standardise lipid annotations, lipid names still remains diverse. This is due to limited ways lipid software may label a lipid and/or researchers’ personal preferences to annotate them.

Here, I would like to highlight some lipid annotations that my workplace uses and show how to modify them in R such that it can be processed by lipid annotations converter tools like [Goslin](https://lifs-tools.org/goslin) (1), (2) and [RefMet](https://metabolomicsworkbench.org/databases/refmet/index.php) (3).

## R Packages Used

``` r
library("rgoslin")
library("reactable")
library("readr")
library("magrittr")
library("stringr")
library("dplyr")
library("purrr")
library("tibble")
library("report")
summary(report::report(sessionInfo()))
```

    ## The analysis was done using the R Statistical language (v4.2.0; R Core Team, 2022) on Windows 10 x64, using the packages rgoslin (v1.0.0), report (v0.5.1), dplyr (v1.0.9), magrittr (v2.0.3), purrr (v0.3.4), reactable (v0.2.3), readr (v2.1.2), stringr (v1.4.0) and tibble (v3.1.7).

## Labels to clean

Here are the list of lipid names to clean

| Given Name              | Clean Name For Annotation | Precursor Ion | Product Ion |
|-------------------------|---------------------------|---------------|-------------|
| LPC 13:0 (ISTD) (a)     | LPC 13:0                  | 454.3         | 184.1       |
| LPC 13:0 (ISTD) (a\\b)  | LPC 13:0                  | 454.3         | 184.1       |
| LPC 13:0 (ISTD) (b)     | LPC 13:0                  | 454.3         | 184.1       |
| LPC 15:0-d5 (IS) (a)    | LPC 15:0                  | 487.4         | 304.3       |
| LPC 15:0-d5 (IS) (a\\b) | LPC 15:0                  | 487.4         | 304.3       |
| LPC 15:0-d5 (IS) (b)    | LPC 15:0                  | 487.4         | 304.3       |
| LPC 17:1 (a)            | LPC 17:1                  | 508.3         | 184.1       |
| LPC 17:1 (a/b/c)        | LPC 17:1                  | 508.3         | 184.1       |
| LPC 17:1 (b)            | LPC 17:1                  | 508.3         | 184.1       |
| LPC 17:1 (c)            | LPC 17:1                  | 508.3         | 184.1       |

The word (IS) or (ISTD) stands for [internal standards](https://en.wikipedia.org/wiki/Internal_standard).

The word -d5 means the compound contains five [deuterium](https://en.wikipedia.org/wiki/Deuterium) instead of hydrogen.

These internal standards can be purchased via these links

-   [LPC 13:0 (ISTD)](https://avantilipids.com/product/855476)

-   [LPC 15:0-d5 (IS)](https://avantilipids.com/product/870309)

The (a\\b) in this case refers to which lipid isomer is integrated. Here is an example with LPC 17:1

![LPC_17_1\_a](LPC_17_1_a.jpg)

![LPC_17_1\_abc](LPC_17_1_abc.jpg)

![LPC_17_1\_b](LPC_17_1_b.jpg)

![LPC_17_1\_c](LPC_17_1_c.jpg)

The identity of such isomers is still an ongoing research process for most lipids. Thankfully for the case of LPC 17:1 in human plasma, the identity can be found in these links.

-   [LPC 17:1 (a)](https://metabolomics.baker.edu.au/method/mrm/LPC171sn2a)

-   [LPC 17:1 (b)](https://metabolomics.baker.edu.au/method/mrm/LPC171sn1aLPC171sn2b)

-   [LPC 17:1 (c)](https://metabolomics.baker.edu.au/method/mrm/LPC171sn1b)

Unfortunately lipid annotations converter tools like [Goslin](https://lifs-tools.org/goslin) and [RefMet](https://metabolomicsworkbench.org/databases/refmet/index.php) are unable to parse these given names

``` r
c("LPC 13:0 (ISTD) (a\\b)",
  "LPC 15:0-d5 (IS) (a\\b)",
  "LPC 17:1 (a/b/c) ") %>%
  rgoslin::parseLipidNames() %>%
  reactable::reactable(defaultPageSize = 5)
```

<div id="htmlwidget-1" class="reactable html-widget" style="width:auto;height:auto;"></div>
<script type="application/json" data-for="htmlwidget-1">{"x":{"tag":{"name":"Reactable","attribs":{"data":{"Normalized.Name":[null,null,null],"Original.Name":["LPC 13:0 (ISTD) (a\\b)","LPC 15:0-d5 (IS) (a\\b)","LPC 17:1 (a/b/c) "],"Grammar":["NOT_PARSEABLE","NOT_PARSEABLE","NOT_PARSEABLE"],"Message":["Expecting a single string value: [type=character; extent=4].","Expecting a single string value: [type=character; extent=4].","Expecting a single string value: [type=character; extent=4]."]},"columns":[{"accessor":"Normalized.Name","name":"Normalized.Name","type":"logical"},{"accessor":"Original.Name","name":"Original.Name","type":"character"},{"accessor":"Grammar","name":"Grammar","type":"character"},{"accessor":"Message","name":"Message","type":"character"}],"defaultPageSize":5,"paginationType":"numbers","showPageInfo":true,"minRows":1,"dataKey":"9a32536c2445fd6fb2d8c9a085cb7c77","key":"9a32536c2445fd6fb2d8c9a085cb7c77"},"children":[]},"class":"reactR_markup"},"evals":[],"jsHooks":[]}</script>

They must be clean up accordingly

``` r
c("LPC 13:0","LPC 15:0","LPC 17:1") %>%
  rgoslin::parseLipidNames() %>%
  reactable::reactable(defaultPageSize = 5)
```

<div id="htmlwidget-2" class="reactable html-widget" style="width:auto;height:auto;"></div>
<script type="application/json" data-for="htmlwidget-2">{"x":{"tag":{"name":"Reactable","attribs":{"data":{"Normalized.Name":["LPC 13:0","LPC 15:0","LPC 17:1"],"Original.Name":["LPC 13:0","LPC 15:0","LPC 17:1"],"Grammar":["Shorthand2020","Shorthand2020","Shorthand2020"],"Message":["NA","NA","NA"],"Adduct":["NA","NA","NA"],"Adduct.Charge":[0,0,0],"Lipid.Maps.Category":["GP","GP","GP"],"Lipid.Maps.Main.Class":["LPC","LPC","LPC"],"Species.Name":["LPC 13:0","LPC 15:0","LPC 17:1"],"Molecular.Species.Name":["LPC 13:0","LPC 15:0","LPC 17:1"],"Sn.Position.Name":["NA","NA","NA"],"Structure.Defined.Name":["NA","NA","NA"],"Full.Structure.Name":["NA","NA","NA"],"Functional.Class.Abbr":["[LPC]","[LPC]","[LPC]"],"Functional.Class.Synonyms":["[LPC, LysoPC, lysoPC]","[LPC, LysoPC, lysoPC]","[LPC, LysoPC, lysoPC]"],"Level":["MOLECULAR_SPECIES","MOLECULAR_SPECIES","MOLECULAR_SPECIES"],"Total.C":[13,15,17],"Total.OH":[0,0,0],"Total.DB":[0,0,1],"Mass":[453.28553995,481.31684009,507.33249016],"Sum.Formula":["C21H44NO7P","C23H48NO7P","C25H50NO7P"],"FA1.Position":[-1,-1,-1],"FA1.C":[13,15,17],"FA1.OH":[0,0,0],"FA1.DB":[0,0,1],"FA1.Bond.Type":["ESTER","ESTER","ESTER"],"FA1.DB.Positions":["[]","[]","[]"],"FA2.Position":[-1,-1,-1],"FA2.C":[0,0,0],"FA2.OH":[0,0,0],"FA2.DB":[0,0,0],"FA2.Bond.Type":["ESTER","ESTER","ESTER"],"FA2.DB.Positions":["[]","[]","[]"],"LCB.Position":["NA","NA","NA"],"LCB.C":["NA","NA","NA"],"LCB.OH":["NA","NA","NA"],"LCB.DB":["NA","NA","NA"],"LCB.Bond.Type":[null,null,null],"LCB.DB.Positions":[null,null,null],"FA3.Position":["NA","NA","NA"],"FA3.C":["NA","NA","NA"],"FA3.OH":["NA","NA","NA"],"FA3.DB":["NA","NA","NA"],"FA3.Bond.Type":[null,null,null],"FA3.DB.Positions":[null,null,null],"FA4.Position":["NA","NA","NA"],"FA4.C":["NA","NA","NA"],"FA4.OH":["NA","NA","NA"],"FA4.DB":["NA","NA","NA"],"FA4.Bond.Type":[null,null,null],"FA4.DB.Positions":[null,null,null]},"columns":[{"accessor":"Normalized.Name","name":"Normalized.Name","type":"character"},{"accessor":"Original.Name","name":"Original.Name","type":"character"},{"accessor":"Grammar","name":"Grammar","type":"character"},{"accessor":"Message","name":"Message","type":"character"},{"accessor":"Adduct","name":"Adduct","type":"character"},{"accessor":"Adduct.Charge","name":"Adduct.Charge","type":"numeric"},{"accessor":"Lipid.Maps.Category","name":"Lipid.Maps.Category","type":"character"},{"accessor":"Lipid.Maps.Main.Class","name":"Lipid.Maps.Main.Class","type":"character"},{"accessor":"Species.Name","name":"Species.Name","type":"character"},{"accessor":"Molecular.Species.Name","name":"Molecular.Species.Name","type":"character"},{"accessor":"Sn.Position.Name","name":"Sn.Position.Name","type":"character"},{"accessor":"Structure.Defined.Name","name":"Structure.Defined.Name","type":"character"},{"accessor":"Full.Structure.Name","name":"Full.Structure.Name","type":"character"},{"accessor":"Functional.Class.Abbr","name":"Functional.Class.Abbr","type":"character"},{"accessor":"Functional.Class.Synonyms","name":"Functional.Class.Synonyms","type":"character"},{"accessor":"Level","name":"Level","type":"character"},{"accessor":"Total.C","name":"Total.C","type":"numeric"},{"accessor":"Total.OH","name":"Total.OH","type":"numeric"},{"accessor":"Total.DB","name":"Total.DB","type":"numeric"},{"accessor":"Mass","name":"Mass","type":"numeric"},{"accessor":"Sum.Formula","name":"Sum.Formula","type":"character"},{"accessor":"FA1.Position","name":"FA1.Position","type":"numeric"},{"accessor":"FA1.C","name":"FA1.C","type":"numeric"},{"accessor":"FA1.OH","name":"FA1.OH","type":"numeric"},{"accessor":"FA1.DB","name":"FA1.DB","type":"numeric"},{"accessor":"FA1.Bond.Type","name":"FA1.Bond.Type","type":"character"},{"accessor":"FA1.DB.Positions","name":"FA1.DB.Positions","type":"character"},{"accessor":"FA2.Position","name":"FA2.Position","type":"numeric"},{"accessor":"FA2.C","name":"FA2.C","type":"numeric"},{"accessor":"FA2.OH","name":"FA2.OH","type":"numeric"},{"accessor":"FA2.DB","name":"FA2.DB","type":"numeric"},{"accessor":"FA2.Bond.Type","name":"FA2.Bond.Type","type":"character"},{"accessor":"FA2.DB.Positions","name":"FA2.DB.Positions","type":"character"},{"accessor":"LCB.Position","name":"LCB.Position","type":"numeric"},{"accessor":"LCB.C","name":"LCB.C","type":"numeric"},{"accessor":"LCB.OH","name":"LCB.OH","type":"numeric"},{"accessor":"LCB.DB","name":"LCB.DB","type":"numeric"},{"accessor":"LCB.Bond.Type","name":"LCB.Bond.Type","type":"character"},{"accessor":"LCB.DB.Positions","name":"LCB.DB.Positions","type":"character"},{"accessor":"FA3.Position","name":"FA3.Position","type":"numeric"},{"accessor":"FA3.C","name":"FA3.C","type":"numeric"},{"accessor":"FA3.OH","name":"FA3.OH","type":"numeric"},{"accessor":"FA3.DB","name":"FA3.DB","type":"numeric"},{"accessor":"FA3.Bond.Type","name":"FA3.Bond.Type","type":"character"},{"accessor":"FA3.DB.Positions","name":"FA3.DB.Positions","type":"character"},{"accessor":"FA4.Position","name":"FA4.Position","type":"numeric"},{"accessor":"FA4.C","name":"FA4.C","type":"numeric"},{"accessor":"FA4.OH","name":"FA4.OH","type":"numeric"},{"accessor":"FA4.DB","name":"FA4.DB","type":"numeric"},{"accessor":"FA4.Bond.Type","name":"FA4.Bond.Type","type":"character"},{"accessor":"FA4.DB.Positions","name":"FA4.DB.Positions","type":"character"}],"defaultPageSize":5,"paginationType":"numbers","showPageInfo":true,"minRows":1,"dataKey":"b0e2e9c2ce2e3c49fa0940bd12bb4903","key":"b0e2e9c2ce2e3c49fa0940bd12bb4903"},"children":[]},"class":"reactR_markup"},"evals":[],"jsHooks":[]}</script>

The task is to remove the variations of (ISTD), (a\\b) and the -d5

## Read Data

``` r
annotation_data <- readr::read_csv("https://raw.github.com/JauntyJJS/jaunty-blogdown/main/content/blog/2022-01-22-Clean-Lipid-Names-1/Annotation.csv")

reactable::reactable(annotation_data, defaultPageSize = 5)
```

<div id="htmlwidget-3" class="reactable html-widget" style="width:auto;height:auto;"></div>
<script type="application/json" data-for="htmlwidget-3">{"x":{"tag":{"name":"Reactable","attribs":{"data":{"Given Name":["LPC 13:0 (ISTD) (a)","LPC 13:0 (ISTD) (a\\b)","LPC 13:0 (ISTD) (b)","LPC 15:0-d5 (IS) (a)","LPC 15:0-d5 (IS) (a\\b)","LPC 15:0-d5 (IS) (b)","LPC 17:1 (a)","LPC 17:1 (a/b/c)","LPC 17:1 (b)","LPC 17:1 (c)"],"Precursor Ion":[454.3,454.3,454.3,487.4,487.4,487.4,508.3,508.3,508.3,508.3],"Product Ion":[184.1,184.1,184.1,304.3,304.3,304.3,184.1,184.1,184.1,184.1]},"columns":[{"accessor":"Given Name","name":"Given Name","type":"character"},{"accessor":"Precursor Ion","name":"Precursor Ion","type":"numeric"},{"accessor":"Product Ion","name":"Product Ion","type":"numeric"}],"defaultPageSize":5,"paginationType":"numbers","showPageInfo":true,"minRows":1,"dataKey":"e26c2bb649e9fe5d80bb5851114b88c6","key":"e26c2bb649e9fe5d80bb5851114b88c6"},"children":[]},"class":"reactR_markup"},"evals":[],"jsHooks":[]}</script>

## The Plan

We will do the following in order

1.  Remove the -d5

2.  Remove the ISTD and its variations

3.  Remove the (a\\b\\c) and its variations

The idea is to first use `stringr::str_view` to check what the matched pattern is. Once the matched pattern is correct, we can use `stringr::str_remove` function to clean up the matched pattern.

## Remove -d5

Here is an example to remove the -d5 using `stringr::str_view`. Simply just set the pattern as “-d5”

``` r
stringr::str_view("LPC 15:0-d5 (IS) (a)", pattern = "-d5")
```

<div id="htmlwidget-4" style="width:960px;height:100%;" class="str_view html-widget"></div>
<script type="application/json" data-for="htmlwidget-4">{"x":{"html":"<ul>\n  <li>LPC 15:0<span class='match'>-d5<\/span> (IS) (a)<\/li>\n<\/ul>"},"evals":[],"jsHooks":[]}</script>

``` r
stringr::str_remove("LPC 15:0-d5 (IS) (a)", pattern = "-d5")
```

    ## [1] "LPC 15:0 (IS) (a)"

## Remove the ISTD variation

The first challenge is to create a pattern that is able to remove variations of ISTD such as `(ISTD)` and `(IS)`

### Detect the word ISTD

To detect the word ISTD, we can do this in R

``` r
stringr::str_view("LPC 13:0 (ISTD) (a)", pattern = "ISTD")
```

<div id="htmlwidget-5" style="width:960px;height:100%;" class="str_view html-widget"></div>
<script type="application/json" data-for="htmlwidget-5">{"x":{"html":"<ul>\n  <li>LPC 13:0 (<span class='match'>ISTD<\/span>) (a)<\/li>\n<\/ul>"},"evals":[],"jsHooks":[]}</script>

Unfortunately, this will not work with the word IS

``` r
stringr::str_view("LPC 15:0-d5 (IS) (a)", pattern = "ISTD")
```

<div id="htmlwidget-6" style="width:960px;height:100%;" class="str_view html-widget"></div>
<script type="application/json" data-for="htmlwidget-6">{"x":{"html":"<ul>\n  <li>LPC 15:0-d5 (IS) (a)<\/li>\n<\/ul>"},"evals":[],"jsHooks":[]}</script>

Alternatively to detect the word IS, we can do this in R

``` r
stringr::str_view("LPC 15:0-d5 (IS) (a)", pattern = "IS")
```

<div id="htmlwidget-7" style="width:960px;height:100%;" class="str_view html-widget"></div>
<script type="application/json" data-for="htmlwidget-7">{"x":{"html":"<ul>\n  <li>LPC 15:0-d5 (<span class='match'>IS<\/span>) (a)<\/li>\n<\/ul>"},"evals":[],"jsHooks":[]}</script>

This time, this will not work with the word ISTD

``` r
stringr::str_view("LPC 13:0 (ISTD) (a)", pattern = "IS")
```

<div id="htmlwidget-8" style="width:960px;height:100%;" class="str_view html-widget"></div>
<script type="application/json" data-for="htmlwidget-8">{"x":{"html":"<ul>\n  <li>LPC 13:0 (<span class='match'>IS<\/span>TD) (a)<\/li>\n<\/ul>"},"evals":[],"jsHooks":[]}</script>

To detect words of the form IS and ISTD, we can make use of the fact that the group “TD” in “ISTD” appear zero or one time. Referring to the cheat sheet of `stringr`, we can make use of parentheses to create a group.

Hence, adding the group to the existing pattern, we have the form `IS(TD)`.

Next, we inform `stringr` that the group `(TD)` can appear zero or one time. Referring to the cheat sheet of `stringr`, we can make use of the `?` symbol

This give our updated pattern to `IS(TD)?`

Putting this to our existing list of words, we have

``` r
stringr::str_view(annotation_data$`Given Name`, pattern = "IS(TD)?")
```

<div id="htmlwidget-9" style="width:960px;height:100%;" class="str_view html-widget"></div>
<script type="application/json" data-for="htmlwidget-9">{"x":{"html":"<ul>\n  <li>LPC 13:0 (<span class='match'>ISTD<\/span>) (a)<\/li>\n  <li>LPC 13:0 (<span class='match'>ISTD<\/span>) (a\\b)<\/li>\n  <li>LPC 13:0 (<span class='match'>ISTD<\/span>) (b)<\/li>\n  <li>LPC 15:0-d5 (<span class='match'>IS<\/span>) (a)<\/li>\n  <li>LPC 15:0-d5 (<span class='match'>IS<\/span>) (a\\b)<\/li>\n  <li>LPC 15:0-d5 (<span class='match'>IS<\/span>) (b)<\/li>\n  <li>LPC 17:1 (a)<\/li>\n  <li>LPC 17:1 (a/b/c)<\/li>\n  <li>LPC 17:1 (b)<\/li>\n  <li>LPC 17:1 (c)<\/li>\n<\/ul>"},"evals":[],"jsHooks":[]}</script>

### Detect Parenthesis

The way to detect `(` and `)` is unfortunately not as simple as `stringr::str_view_all("LPC 13:0 (ISTD) (a)", pattern = "(")`, giving rise to this error message.

``` r
stringr::str_view_all("LPC 13:0 (ISTD) (a)", pattern = "(")
```

    ## Error in stri_locate_all_regex(string, pattern, omit_no_match = TRUE, : Incorrectly nested parentheses in regex pattern. (U_REGEX_MISMATCHED_PAREN, context=`(`)

This is because `(` and `)` fall under a group called “meta characters” that have other functions in regular expression. In fact, we have just explained what it does earlier which is to group characters together.

To inform that we want to search for the pattern `(` and `)` explicitly. We need to add two escape character `\\` as indicated in the stringr cheat sheet.

![parenthesis](parenthesis.jpg)

``` r
stringr::str_view_all("LPC 13:0 (ISTD) (a)", pattern = "\\(")
```

<div id="htmlwidget-10" style="width:960px;height:100%;" class="str_view html-widget"></div>
<script type="application/json" data-for="htmlwidget-10">{"x":{"html":"<ul>\n  <li>LPC 13:0 <span class='match'>(<\/span>ISTD) <span class='match'>(<\/span>a)<\/li>\n<\/ul>"},"evals":[],"jsHooks":[]}</script>

``` r
stringr::str_view_all("LPC 13:0 (ISTD) (a)", pattern = "\\)")
```

<div id="htmlwidget-11" style="width:960px;height:100%;" class="str_view html-widget"></div>
<script type="application/json" data-for="htmlwidget-11">{"x":{"html":"<ul>\n  <li>LPC 13:0 (ISTD<span class='match'>)<\/span> (a<span class='match'>)<\/span><\/li>\n<\/ul>"},"evals":[],"jsHooks":[]}</script>

Putting it all together, we have the pattern `\\(IS(TD)?\\)`

``` r
stringr::str_view_all(annotation_data$`Given Name`, pattern = "\\(IS(TD)?\\)")
```

<div id="htmlwidget-12" style="width:960px;height:100%;" class="str_view html-widget"></div>
<script type="application/json" data-for="htmlwidget-12">{"x":{"html":"<ul>\n  <li>LPC 13:0 <span class='match'>(ISTD)<\/span> (a)<\/li>\n  <li>LPC 13:0 <span class='match'>(ISTD)<\/span> (a\\b)<\/li>\n  <li>LPC 13:0 <span class='match'>(ISTD)<\/span> (b)<\/li>\n  <li>LPC 15:0-d5 <span class='match'>(IS)<\/span> (a)<\/li>\n  <li>LPC 15:0-d5 <span class='match'>(IS)<\/span> (a\\b)<\/li>\n  <li>LPC 15:0-d5 <span class='match'>(IS)<\/span> (b)<\/li>\n  <li>LPC 17:1 (a)<\/li>\n  <li>LPC 17:1 (a/b/c)<\/li>\n  <li>LPC 17:1 (b)<\/li>\n  <li>LPC 17:1 (c)<\/li>\n<\/ul>"},"evals":[],"jsHooks":[]}</script>

## Remove (a\\b\\c) and its variations

The second challenge is to create a pattern to remove variations of (a\\b\\c).

Things that are consistent is that they are written in small letters.

However, the main issue I faced when dealing with this variation

-   The letter does not always start with `a`

-   The list of letters can be separated by `\` or `/`

-   The list can expand indefinitely. For example, it can be

    -   (a\\b\\…\\f)

    -   (b\\d\\f)

Here is what I have done to resolve the above issues.

### Letter does not always start with `a`

To create a pattern that matches small letters from a to z, we can use the square brackets `[` and `]` and hyphen `-` as indicated in the stringr cheat sheet.

![range](range.jpg)

Applying what we have learnt, we have the pattern `\\([a-z]\\)`. The `a-z` means the range from a to z. The square brackets `[` and `]` means one of. Hence `[a-z]` is telling the software to look for one of the letters ranging from a to z.

``` r
stringr::str_view_all(annotation_data$`Given Name`, pattern = "\\([a-z]\\)")
```

<div id="htmlwidget-13" style="width:960px;height:100%;" class="str_view html-widget"></div>
<script type="application/json" data-for="htmlwidget-13">{"x":{"html":"<ul>\n  <li>LPC 13:0 (ISTD) <span class='match'>(a)<\/span><\/li>\n  <li>LPC 13:0 (ISTD) (a\\b)<\/li>\n  <li>LPC 13:0 (ISTD) <span class='match'>(b)<\/span><\/li>\n  <li>LPC 15:0-d5 (IS) <span class='match'>(a)<\/span><\/li>\n  <li>LPC 15:0-d5 (IS) (a\\b)<\/li>\n  <li>LPC 15:0-d5 (IS) <span class='match'>(b)<\/span><\/li>\n  <li>LPC 17:1 <span class='match'>(a)<\/span><\/li>\n  <li>LPC 17:1 (a/b/c)<\/li>\n  <li>LPC 17:1 <span class='match'>(b)<\/span><\/li>\n  <li>LPC 17:1 <span class='match'>(c)<\/span><\/li>\n<\/ul>"},"evals":[],"jsHooks":[]}</script>

### The list of letters can be separated by `\` or `/`

Matching `/` is easy.

``` r
stringr::str_view_all("LPC 17:1 (a/b/c)", pattern = "/")
```

<div id="htmlwidget-14" style="width:960px;height:100%;" class="str_view html-widget"></div>
<script type="application/json" data-for="htmlwidget-14">{"x":{"html":"<ul>\n  <li>LPC 17:1 (a<span class='match'>/<\/span>b<span class='match'>/<\/span>c)<\/li>\n<\/ul>"},"evals":[],"jsHooks":[]}</script>

but not so for `\`

``` r
stringr::str_view_all("LPC 13:0 (ISTD) (a\\b)", pattern = "\\")
```

    ## Error in stri_locate_all_regex(string, pattern, omit_no_match = TRUE, : Unrecognized backslash escape sequence in pattern. (U_REGEX_BAD_ESCAPE_SEQUENCE, context=`\`)

`\` also fall under a group called “meta characters”. Referring to the stringr cheat sheet, to search for the pattern `/` explicitly. We use four escape characters `\\\\`

![backslash](backslash.jpg)

``` r
stringr::str_view_all("LPC 13:0 (ISTD) (a\\b)", pattern = "\\\\")
```

<div id="htmlwidget-15" style="width:960px;height:100%;" class="str_view html-widget"></div>
<script type="application/json" data-for="htmlwidget-15">{"x":{"html":"<ul>\n  <li>LPC 13:0 (ISTD) (a<span class='match'>\\<\/span>b)<\/li>\n<\/ul>"},"evals":[],"jsHooks":[]}</script>

The question now is how do we incorporate “or” into the pattern. Referring again to the stringr cheat sheet, it is `|`

![or](or.jpg)

The pattern therefore is `[\\\\|/]` as we are looking for one of `/` or `\`

``` r
stringr::str_view_all(c("LPC 13:0 (ISTD) (a\\b)", "LPC 17:1 (a/b/c)"), pattern = "[\\\\|/]")
```

<div id="htmlwidget-16" style="width:960px;height:100%;" class="str_view html-widget"></div>
<script type="application/json" data-for="htmlwidget-16">{"x":{"html":"<ul>\n  <li>LPC 13:0 (ISTD) (a<span class='match'>\\<\/span>b)<\/li>\n  <li>LPC 17:1 (a<span class='match'>/<\/span>b<span class='match'>/<\/span>c)<\/li>\n<\/ul>"},"evals":[],"jsHooks":[]}</script>

### List can expand indefinitely

This one is a bit tricky. The pattern (a\\b\\…\\f) and (a/b/c) can be viewed as

(\[some small letter\]`[\ or /][some small letter]`)

where the whole pattern `[\ or /][some small letter]` appears zero or more times.

To add the element of zero or more times, we use the `*` character

![zero_or_more](zero_or_more.jpg)

This gives the pattern `([\\\\|/][a-z])*`. The parenthesis `()` is to ensure the whole pattern `{\ or /}{some small letter}` appears zero or more times.

Putting the three solution altogether, we have the pattern `\\([a-z]([\\\\|/][a-z])*\\)`

``` r
stringr::str_view_all(annotation_data$`Given Name`, pattern = "\\([a-z]([\\\\|/][a-z])*\\)")
```

<div id="htmlwidget-17" style="width:960px;height:100%;" class="str_view html-widget"></div>
<script type="application/json" data-for="htmlwidget-17">{"x":{"html":"<ul>\n  <li>LPC 13:0 (ISTD) <span class='match'>(a)<\/span><\/li>\n  <li>LPC 13:0 (ISTD) <span class='match'>(a\\b)<\/span><\/li>\n  <li>LPC 13:0 (ISTD) <span class='match'>(b)<\/span><\/li>\n  <li>LPC 15:0-d5 (IS) <span class='match'>(a)<\/span><\/li>\n  <li>LPC 15:0-d5 (IS) <span class='match'>(a\\b)<\/span><\/li>\n  <li>LPC 15:0-d5 (IS) <span class='match'>(b)<\/span><\/li>\n  <li>LPC 17:1 <span class='match'>(a)<\/span><\/li>\n  <li>LPC 17:1 <span class='match'>(a/b/c)<\/span><\/li>\n  <li>LPC 17:1 <span class='match'>(b)<\/span><\/li>\n  <li>LPC 17:1 <span class='match'>(c)<\/span><\/li>\n<\/ul>"},"evals":[],"jsHooks":[]}</script>

## Plan Execution

With the three removal plan set, we can clean the transition name as follows.

``` r
Clean_Name <- annotation_data[["Given Name"]] %>%
  stringr::str_remove(pattern = "-d5") %>%
  stringr::str_remove(pattern = "\\(IS(TD)?\\)") %>%
  stringr::str_remove(pattern = "\\([a-z]([\\\\|/][a-z])*\\)") %>%
  stringr::str_trim()

annotation_data %>%
  # Create a new column with the Clean Names
  dplyr::mutate(`Clean Name For Annotation` = Clean_Name) %>%
  # Make Given Name and Clean Name the first two columns
  dplyr::relocate(
    dplyr::any_of(c("Given Name","Clean Name For Annotation"))
    ) %>%
  reactable::reactable(defaultPageSize = 5)
```

<div id="htmlwidget-18" class="reactable html-widget" style="width:auto;height:auto;"></div>
<script type="application/json" data-for="htmlwidget-18">{"x":{"tag":{"name":"Reactable","attribs":{"data":{"Given Name":["LPC 13:0 (ISTD) (a)","LPC 13:0 (ISTD) (a\\b)","LPC 13:0 (ISTD) (b)","LPC 15:0-d5 (IS) (a)","LPC 15:0-d5 (IS) (a\\b)","LPC 15:0-d5 (IS) (b)","LPC 17:1 (a)","LPC 17:1 (a/b/c)","LPC 17:1 (b)","LPC 17:1 (c)"],"Clean Name For Annotation":["LPC 13:0","LPC 13:0","LPC 13:0","LPC 15:0","LPC 15:0","LPC 15:0","LPC 17:1","LPC 17:1","LPC 17:1","LPC 17:1"],"Precursor Ion":[454.3,454.3,454.3,487.4,487.4,487.4,508.3,508.3,508.3,508.3],"Product Ion":[184.1,184.1,184.1,304.3,304.3,304.3,184.1,184.1,184.1,184.1]},"columns":[{"accessor":"Given Name","name":"Given Name","type":"character"},{"accessor":"Clean Name For Annotation","name":"Clean Name For Annotation","type":"character"},{"accessor":"Precursor Ion","name":"Precursor Ion","type":"numeric"},{"accessor":"Product Ion","name":"Product Ion","type":"numeric"}],"defaultPageSize":5,"paginationType":"numbers","showPageInfo":true,"minRows":1,"dataKey":"55f339c5c4c45dcbde21e5ace5a0de73","key":"55f339c5c4c45dcbde21e5ace5a0de73"},"children":[]},"class":"reactR_markup"},"evals":[],"jsHooks":[]}</script>

## Package References

``` r
get_citation <- function(package_name) {
  transform_name <- package_name %>% 
    citation() %>% 
    format(style="text")
  return(transform_name)
} 

packages <- c("base","rgoslin", "reactable",
              "readr", "magrittr", "stringr", 
              "dplyr", "report",
              "tibble", "purrr")

table <- tibble::tibble(Packages = packages)

table %>%
  dplyr::mutate(
    transform_name = purrr::map_chr(.data[["Packages"]],
                                    get_citation)
  ) %>% 
  dplyr::pull(.data[["transform_name"]]) %>% 
  report::as.report_parameters()
```

-   R Core Team (2022). *R: A Language and Environment for Statistical
    Computing*. R Foundation for Statistical Computing, Vienna, Austria.
    <https://www.R-project.org/>.
-   Kopczynski D, Hoffmann N, Peng B, Ahrends R (2020). “Goslin: A Grammar
    of Succinct Lipid Nomenclature.” *Analytical Chemistry*, *92*(16),
    10957-10960. <https://pubs.acs.org/doi/10.1021/acs.analchem.0c01690>.
-   Lin G (2020). *reactable: Interactive Data Tables Based on ‘React
    Table’*. R package version 0.2.3,
    <https://CRAN.R-project.org/package=reactable>.
-   Wickham H, Hester J, Bryan J (2022). *readr: Read Rectangular Text
    Data*. R package version 2.1.2,
    <https://CRAN.R-project.org/package=readr>.
-   Bache S, Wickham H (2022). *magrittr: A Forward-Pipe Operator for R*. R
    package version 2.0.3, <https://CRAN.R-project.org/package=magrittr>.
-   Wickham H (2019). *stringr: Simple, Consistent Wrappers for Common
    String Operations*. R package version 1.4.0,
    <https://CRAN.R-project.org/package=stringr>.
-   Wickham H, François R, Henry L, Müller K (2022). *dplyr: A Grammar of
    Data Manipulation*. R package version 1.0.9,
    <https://CRAN.R-project.org/package=dplyr>.
-   Makowski D, Ben-Shachar M, Patil I, Lüdecke D (2021). “Automated
    Results Reporting as a Practical Tool to Improve Reproducibility and
    Methodological Best Practices Adoption.” *CRAN*.
    <https://github.com/easystats/report>.
-   Müller K, Wickham H (2022). *tibble: Simple Data Frames*. R package
    version 3.1.7, <https://CRAN.R-project.org/package=tibble>.
-   Henry L, Wickham H (2020). *purrr: Functional Programming Tools*. R
    package version 0.3.4, <https://CRAN.R-project.org/package=purrr>.

## References

<div id="refs" class="references csl-bib-body">

<div id="ref-GOSLIN" class="csl-entry">

<span class="csl-left-margin">1. </span><span class="csl-right-inline">Kopczynski D, Hoffmann N, Peng B, Ahrends R. Goslin: A grammar of succinct lipid nomenclature. Analytical Chemistry \[Internet\]. 2020;92(16):10957–60. Available from: <https://doi.org/10.1021/acs.analchem.0c01690></span>

</div>

<div id="ref-GOSLIN2" class="csl-entry">

<span class="csl-left-margin">2. </span><span class="csl-right-inline">Kopczynski D, Hoffmann N, Peng B, Liebisch G, Spener F, Ahrends R. Goslin 2.0 implements the recent lipid shorthand nomenclature for MS-derived lipid structures. Analytical Chemistry \[Internet\]. 2022;94(16):6097–101. Available from: <https://doi.org/10.1021/acs.analchem.1c05430></span>

</div>

<div id="ref-Fahy2020" class="csl-entry">

<span class="csl-left-margin">3. </span><span class="csl-right-inline">Fahy E, Subramaniam S. RefMet: A reference nomenclature for metabolomics. Nature Methods \[Internet\]. 2020 Dec 1;17(12):1173–4. Available from: <https://doi.org/10.1038/s41592-020-01009-y></span>

</div>

</div>
