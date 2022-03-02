---
title: "Cleaning Lipid Names for Annotation Part 2"
subtitle: ""
excerpt: "This post provides some tips on how to clean lipid names input suited for some current nomenclature tools using R"
date: 2022-03-01
author: "Jeremy Selva"
draft: true
images:
series:
tags:
categories:
output: md_document #needed for flair to work
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
<script src="{{< blogdown/postref >}}index_files/core-js/shim.min.js"></script>
<script src="{{< blogdown/postref >}}index_files/react/react.min.js"></script>
<script src="{{< blogdown/postref >}}index_files/react/react-dom.min.js"></script>
<script src="{{< blogdown/postref >}}index_files/reactwidget/react-tools.js"></script>
<script src="{{< blogdown/postref >}}index_files/htmlwidgets/htmlwidgets.js"></script>
<script src="{{< blogdown/postref >}}index_files/reactable-binding/reactable.js"></script>

## Introduction

In this blog, I will introduce another set of lipid annotations that my workplace uses that require to be cleaned up and modified so that they can be processed by lipid annotations converter tools like [Goslin](https://lifs-tools.org/goslin) (1) and [RefMet](https://metabolomicsworkbench.org/databases/refmet/index.php) (2).

## R Packages Used

``` r
library("rgoslin")
library("reactable")
library("flair")
library("here")
library("readxl")
library("magrittr")
library("stringr")
library("dplyr")
library("report")
```

## Labels to clean

Here are the list of lipid names to clean

| Given Name          | Clean Name For Annotation | Precursor Ion | Product Ion |
|---------------------|---------------------------|---------------|-------------|
| DG 32:0 \[-16:0\]   | DG 16:0_16:0              | 586.5         | 313.3       |
| DG 36:1 \[NL-18:1\] | DG 18:1_18:0              | 640.6         | 341.3       |
| TG 54:3 \[-18:1\]   | TG 18:1_36:2              | 902.8         | 603.5       |
| TG 54:3 \[NL-18:2\] | TG 18:2_36:1              | 902.8         | 605.5       |
| TG 54:3 \[SIM\]     | TG 54:3                   | 902.8         | 902.8       |

Unfortunately lipid annotations converter tools like Goslin and RetMet is unable to parse these given names

``` r
c("DG 32:0 [-16:0]",
  "TG 54:3 [NL-18:2]") %>%
  rgoslin::parseLipidNames()
```

    ## Warning in rcpp_parse_lipid_name(as.character(lipidNames[[i]])): Parsing of
    ## lipid name 'DG 32:0 [-16:0]' caused an exception: Lipid not found

    ## Warning in rcpp_parse_lipid_name(as.character(lipidNames[[i]])): Parsing of
    ## lipid name 'TG 54:3 [NL-18:2]' caused an exception: Lipid not found

    ## data frame with 0 columns and 0 rows

![refmet_negative_results](refmet_negative_results.jpg)

They must be clean up accordingly

``` r
c("DG 16:0_16:0",
  "TG 18:2_36:1") %>%
  rgoslin::parseLipidNames() %>%
  reactable::reactable(defaultPageSize = 5)
```

<div id="htmlwidget-1" class="reactable html-widget" style="width:auto;height:auto;"></div>
<script type="application/json" data-for="htmlwidget-1">{"x":{"tag":{"name":"Reactable","attribs":{"data":{"Normalized.Name":["DG 16:0_16:0","TG 18:2_36:1"],"Original.Name":["DG 16:0_16:0","TG 18:2_36:1"],"Grammar":["Shorthand2020","Shorthand2020"],"Message":["NA","NA"],"Adduct":["NA","NA"],"Adduct.Charge":[0,0],"Lipid.Maps.Category":["GL","GL"],"Lipid.Maps.Main.Class":["DG","TG"],"Species.Name":["DG 32:0","TG 54:3"],"Molecular.Species.Name":["DG 16:0_16:0","TG 18:2_36:1"],"Sn.Position.Name":["NA","NA"],"Structure.Defined.Name":["NA","NA"],"Full.Structure.Name":["NA","NA"],"Functional.Class.Abbr":["[DG]","[TG]"],"Functional.Class.Synonyms":["[DG, DAG]","[TG, TAG]"],"Level":["MOLECULAR_SPECIES","MOLECULAR_SPECIES"],"Total.C":[32,54],"Total.OH":[0,0],"Total.DB":[0,3],"Mass":[568.50667553,870.80402686],"Sum.Formula":["C35H68O5","C57H106O5"],"FA1.Position":[-1,-1],"FA1.C":[16,18],"FA1.OH":[0,0],"FA1.DB":[0,2],"FA1.Bond.Type":["ESTER","ESTER"],"FA1.DB.Positions":["[]","[]"],"FA2.Position":[-1,-1],"FA2.C":[16,36],"FA2.OH":[0,0],"FA2.DB":[0,1],"FA2.Bond.Type":["ESTER","ESTER"],"FA2.DB.Positions":["[]","[]"],"LCB.Position":["NA","NA"],"LCB.C":["NA","NA"],"LCB.OH":["NA","NA"],"LCB.DB":["NA","NA"],"LCB.Bond.Type":[null,null],"LCB.DB.Positions":[null,null],"FA3.Position":[-1,-1],"FA3.C":[0,0],"FA3.OH":[0,0],"FA3.DB":[0,0],"FA3.Bond.Type":["ESTER","ESTER"],"FA3.DB.Positions":["[]","[]"],"FA4.Position":["NA","NA"],"FA4.C":["NA","NA"],"FA4.OH":["NA","NA"],"FA4.DB":["NA","NA"],"FA4.Bond.Type":[null,null],"FA4.DB.Positions":[null,null]},"columns":[{"accessor":"Normalized.Name","name":"Normalized.Name","type":"character"},{"accessor":"Original.Name","name":"Original.Name","type":"character"},{"accessor":"Grammar","name":"Grammar","type":"character"},{"accessor":"Message","name":"Message","type":"character"},{"accessor":"Adduct","name":"Adduct","type":"character"},{"accessor":"Adduct.Charge","name":"Adduct.Charge","type":"numeric"},{"accessor":"Lipid.Maps.Category","name":"Lipid.Maps.Category","type":"character"},{"accessor":"Lipid.Maps.Main.Class","name":"Lipid.Maps.Main.Class","type":"character"},{"accessor":"Species.Name","name":"Species.Name","type":"character"},{"accessor":"Molecular.Species.Name","name":"Molecular.Species.Name","type":"character"},{"accessor":"Sn.Position.Name","name":"Sn.Position.Name","type":"character"},{"accessor":"Structure.Defined.Name","name":"Structure.Defined.Name","type":"character"},{"accessor":"Full.Structure.Name","name":"Full.Structure.Name","type":"character"},{"accessor":"Functional.Class.Abbr","name":"Functional.Class.Abbr","type":"character"},{"accessor":"Functional.Class.Synonyms","name":"Functional.Class.Synonyms","type":"character"},{"accessor":"Level","name":"Level","type":"character"},{"accessor":"Total.C","name":"Total.C","type":"numeric"},{"accessor":"Total.OH","name":"Total.OH","type":"numeric"},{"accessor":"Total.DB","name":"Total.DB","type":"numeric"},{"accessor":"Mass","name":"Mass","type":"numeric"},{"accessor":"Sum.Formula","name":"Sum.Formula","type":"character"},{"accessor":"FA1.Position","name":"FA1.Position","type":"numeric"},{"accessor":"FA1.C","name":"FA1.C","type":"numeric"},{"accessor":"FA1.OH","name":"FA1.OH","type":"numeric"},{"accessor":"FA1.DB","name":"FA1.DB","type":"numeric"},{"accessor":"FA1.Bond.Type","name":"FA1.Bond.Type","type":"character"},{"accessor":"FA1.DB.Positions","name":"FA1.DB.Positions","type":"character"},{"accessor":"FA2.Position","name":"FA2.Position","type":"numeric"},{"accessor":"FA2.C","name":"FA2.C","type":"numeric"},{"accessor":"FA2.OH","name":"FA2.OH","type":"numeric"},{"accessor":"FA2.DB","name":"FA2.DB","type":"numeric"},{"accessor":"FA2.Bond.Type","name":"FA2.Bond.Type","type":"character"},{"accessor":"FA2.DB.Positions","name":"FA2.DB.Positions","type":"character"},{"accessor":"LCB.Position","name":"LCB.Position","type":"numeric"},{"accessor":"LCB.C","name":"LCB.C","type":"numeric"},{"accessor":"LCB.OH","name":"LCB.OH","type":"numeric"},{"accessor":"LCB.DB","name":"LCB.DB","type":"numeric"},{"accessor":"LCB.Bond.Type","name":"LCB.Bond.Type","type":"character"},{"accessor":"LCB.DB.Positions","name":"LCB.DB.Positions","type":"character"},{"accessor":"FA3.Position","name":"FA3.Position","type":"numeric"},{"accessor":"FA3.C","name":"FA3.C","type":"numeric"},{"accessor":"FA3.OH","name":"FA3.OH","type":"numeric"},{"accessor":"FA3.DB","name":"FA3.DB","type":"numeric"},{"accessor":"FA3.Bond.Type","name":"FA3.Bond.Type","type":"character"},{"accessor":"FA3.DB.Positions","name":"FA3.DB.Positions","type":"character"},{"accessor":"FA4.Position","name":"FA4.Position","type":"numeric"},{"accessor":"FA4.C","name":"FA4.C","type":"numeric"},{"accessor":"FA4.OH","name":"FA4.OH","type":"numeric"},{"accessor":"FA4.DB","name":"FA4.DB","type":"numeric"},{"accessor":"FA4.Bond.Type","name":"FA4.Bond.Type","type":"character"},{"accessor":"FA4.DB.Positions","name":"FA4.DB.Positions","type":"character"}],"defaultPageSize":5,"paginationType":"numbers","showPageInfo":true,"minRows":1,"dataKey":"28c45172401b46de1aaa0ffd50952b83","key":"28c45172401b46de1aaa0ffd50952b83"},"children":[]},"class":"reactR_markup"},"evals":[],"jsHooks":[]}</script>

![refmet_positive_results](refmet_positive_results.jpg)
## Read Data

``` r
annotation_data <- readxl::read_excel(
  path = here::here("content", 
                    "blog",
                    "2022-03-01-Clean-Lipid_Names-2",
                    "Annotation.xlsx"),
  sheet = "Transition_Name_Annot"
  )

reactable::reactable(annotation_data, defaultPageSize = 5)
```

<div id="htmlwidget-2" class="reactable html-widget" style="width:auto;height:auto;"></div>
<script type="application/json" data-for="htmlwidget-2">{"x":{"tag":{"name":"Reactable","attribs":{"data":{"Given Name":["DG 32:0 [-16:0]","DG 36:1 [NL-18:1]","TG 54:3  [-18:1]","TG 54:3  [NL-18:2]","TG 54:3  [SIM]","TG(O-50:2) [-18:1]","TG(O-50:2) [NL-18:2]","TG(O-50:2) [SIM]"],"Precursor Ion":[586.5,640.6,902.8,902.8,902.8,834.8,834.8,834.8],"Product Ion":[313.3,341.3,603.5,605.5,902.8,535.5,537.5,834.8]},"columns":[{"accessor":"Given Name","name":"Given Name","type":"character"},{"accessor":"Precursor Ion","name":"Precursor Ion","type":"numeric"},{"accessor":"Product Ion","name":"Product Ion","type":"numeric"}],"defaultPageSize":5,"paginationType":"numbers","showPageInfo":true,"minRows":1,"dataKey":"4ffa8319b24345681656a750f8c1e80e","key":"4ffa8319b24345681656a750f8c1e80e"},"children":[]},"class":"reactR_markup"},"evals":[],"jsHooks":[]}</script>

## The Plan

We can split the task in the following steps

-   Find those transition names that ends with \[SIM\], remove the \[SIM\] and return it

Transition names from here on should only be those that are measuring neutral loss a particular fatty acid chain.

We now need to do the following steps to clean such transition names.

-   Get the acyl class of the transition.

-   Get the total carbon number of the transition.

-   Get the total number of double bond of the transition

-   Get the total carbon number of the measured fatty acid chain.

-   Get the total number of double bond of the measured fatty acid chain.

-   Use the tools above to clean the transition name.

We begin with an empty generic function

``` r
clean_acyl <- function(input_acyl = "DG 30:0 [NL-15:0]") {
  return(input_acyl)
}
```

## Remove \[SIM\] at the end

<pre><code class='language-r'><code>clean_acyl <- function(input_acyl = "DG 30:0 [NL-15:0]") {<br>&nbsp;&nbsp;<br>&nbsp;&nbsp;# If we have a sum composition labelled as [SIM] at the end,<br>&nbsp;&nbsp;# remove it and return the results<br>&nbsp;&nbsp;if (isTRUE(stringr::str_detect(string = input_acyl,<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style='background-color:#ffff7f'>pattern = "\\s*\\[SIM\\]\\s*$"</span>)))<br>&nbsp;&nbsp;{<br>&nbsp;&nbsp;&nbsp;&nbsp;input_acyl <- input_acyl %>%<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;stringr::str_remove(<span style='background-color:#ffff7f'>pattern = "\\s*\\[SIM\\]\\s*$"</span>)<br>&nbsp;&nbsp;&nbsp;&nbsp;<br>&nbsp;&nbsp;&nbsp;&nbsp;return(input_acyl)<br>&nbsp;&nbsp;}<br>&nbsp;&nbsp;<br>&nbsp;&nbsp;return(input_acyl)<br>}</code></code></pre>

Putting it all together, we have the following function and corresponding documentation.

``` r
#' @title Clean Acyl Lipids
#' @description Clean Acyl Lipids for `rgoslin` input
#' @param input_acyl A character string highlighting a lipid,
#' Default: 'DG 30:0 \[NL-15:0\]'
#' @return A acyl lipid that `rgoslin` can accept
#' @details We only accept DG, DAG, TG, TAG for now.
#' Input Acyl Lipid is of the form
#' {acyl_class} {total_C}:{total_DB} \[NL-{measured_C}:{measured_DB}\]
#' where C is carbon and DB is double bond
#' Output Acyl Lipid is of the form
#' {acyl_class} {measured_C}:{measured_DB}_{remaining_C}:{remaining_DB}
#' where {remaining_C} is {total_C - measured_C}
#' and {remaining_DB} is {total_DB - measured_DB}
#' @examples
#' clean_acyl_dynamo(input_acyl = "DG 30:0 -15:0")
#' @rdname clean_acyl
#' @export
clean_acyl <- function(input_acyl = "DG 30:0 [NL-15:0]") {

  # If we have a sum composition labelled as [SIM] at the end
  # after removing the (a\b) and (ISTD)
  if(isTRUE(stringr::str_detect(string = input_acyl,
                         pattern = "\\s*\\[SIM\\]\\s*$"))) {

    input_acyl <- input_acyl %>%
      stringr::str_remove(pattern = "\\s*\\[SIM\\]\\s*$")

    return(input_acyl)

  }

  # If we have no neutral loss labeling
  if(!isTRUE(stringr::str_detect(string = input_acyl,
                                pattern = "\\s*(\\[)?(NL)?-\\s*\\d+:\\d+(\\])?\\s*$"))) {

    return(input_acyl)

  }

  # From here all should end with [NL-XX:X]

  acyl_class <- input_acyl %>%
    stringr::str_extract(pattern = "^[D|T]A?G")

  total_C <- input_acyl %>%
    stringr::str_remove(pattern = stringr::str_glue("{acyl_class}\\s*")) %>%
    stringr::str_extract(pattern = "^\\d+:\\d+") %>%
    stringr::str_extract(pattern = "^\\d+")

  total_DB <- input_acyl %>%
    stringr::str_remove(pattern = stringr::str_glue("{acyl_class}\\s*")) %>%
    stringr::str_extract(pattern = "^\\d+:\\d+") %>%
    stringr::str_extract(pattern = "\\d+$")

  measured_C <- input_acyl %>%
    stringr::str_remove(pattern = stringr::str_glue("{acyl_class}\\s*")) %>%
    stringr::str_extract(pattern = "-\\s*\\d+:\\d+") %>%
    stringr::str_remove(pattern = "-") %>%
    stringr::str_extract(pattern = "^\\d+")

  measured_DB <- input_acyl %>%
    stringr::str_remove(pattern = stringr::str_glue("{acyl_class}\\s*")) %>%
    stringr::str_extract(pattern = "-\\s*\\d+:\\d+") %>%
    stringr::str_remove(pattern = "-") %>%
    stringr::str_extract(pattern = "\\d+$")

  if(!isTRUE(stringr::str_detect(total_C, "^[0-9]+$"))) {
    stop(glue::glue("Extracting total carbon in {input_acyl} has failed"))
  }

  if(!isTRUE(stringr::str_detect(total_DB, "^[0-9]+$"))) {
    stop(glue::glue("Extracting total double bond in {input_acyl} has failed"))
  }

  if(!isTRUE(stringr::str_detect(measured_C, "^[0-9]+$"))) {
    stop(glue::glue("Extracting measured carbon in {input_acyl} has failed"))
  }

  if(!isTRUE(stringr::str_detect(measured_DB, "^[0-9]+$"))) {
    stop(glue::glue("Extracting measured double bond in {input_acyl} has failed"))
  }

  remaining_C <- (as.numeric(total_C) - as.numeric(measured_C)) %>%
    as.character()

  remaining_DB <- (as.numeric(total_DB) - as.numeric(measured_DB)) %>%
    as.character()

  clean_acyl <- stringr::str_glue(
    "{acyl_class} {measured_C}:{measured_DB}_{remaining_C}:{remaining_DB}"
  ) %>%
    as.character()

  return(clean_acyl)

}
```

## References

<div id="refs" class="references csl-bib-body">

<div id="ref-GOSLIN" class="csl-entry">

<span class="csl-left-margin">1. </span><span class="csl-right-inline">Kopczynski D, Hoffmann N, Peng B, Ahrends R. Goslin: A grammar of succinct lipid nomenclature. Analytical Chemistry \[Internet\]. 2020;92(16):10957–60. Available from: <https://doi.org/10.1021/acs.analchem.0c01690></span>

</div>

<div id="ref-Fahy2020" class="csl-entry">

<span class="csl-left-margin">2. </span><span class="csl-right-inline">Fahy E, Subramaniam S. RefMet: A reference nomenclature for metabolomics. Nature Methods \[Internet\]. 2020 Dec 1;17(12):1173–4. Available from: <https://doi.org/10.1038/s41592-020-01009-y></span>

</div>

</div>
