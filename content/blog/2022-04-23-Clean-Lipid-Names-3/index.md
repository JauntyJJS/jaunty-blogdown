---
title: "Cleaning Lipid Names for Annotation Part 3"
subtitle: ""
excerpt: "This post provides some tips on how to clean lipid names input suited for some current nomenclature tools using R"
date: 2022-04-23
author: "Jeremy Selva"
draft: true
images:
series:
tags:
categories:
output: md_document #needed for flair to work
layout: single-sidebar
bibliography: utils/bibliography.bib
csl: utils/f1000research.csl
editor_options: 
  chunk_output_type: console
---

<script src="{{< blogdown/postref >}}index_files/core-js/shim.min.js"></script>
<script src="{{< blogdown/postref >}}index_files/react/react.min.js"></script>
<script src="{{< blogdown/postref >}}index_files/react/react-dom.min.js"></script>
<script src="{{< blogdown/postref >}}index_files/reactwidget/react-tools.js"></script>
<script src="{{< blogdown/postref >}}index_files/htmlwidgets/htmlwidgets.js"></script>
<script src="{{< blogdown/postref >}}index_files/reactable-binding/reactable.js"></script>

## Introduction

Our last function below is able to remove the \[SIM\] at the end of the transition name

``` r
clean_acyl <- function(input_acyl = "DG 32:0 [NL-16:0]") {
  
  # If we have a sum composition labelled as [SIM] at the end,
  # remove it and return the results
  if (isTRUE(stringr::str_detect(string = input_acyl,
                                 pattern = "\\s*\\[SIM\\]\\s*$")))
  {
    input_acyl <- input_acyl %>%
      stringr::str_remove(pattern = "\\s*\\[SIM\\]\\s*$")
    
    return(input_acyl)
  }
  
  return(input_acyl)
}
```

``` r
clean_acyl("TG 54:3 [SIM]")
```

    ## [1] "TG 54:3"

We continue the cleaning task for these transitions.

| Given Name          | Clean Name For Annotation | Precursor Ion | Product Ion |
|---------------------|---------------------------|---------------|-------------|
| DG 32:0 \[-16:0\]   | DG 16:0_16:0              | 586.5         | 313.3       |
| DG 36:1 \[NL-18:1\] | DG 18:1_18:0              | 640.6         | 341.3       |
| TG 54:3 \[-18:1\]   | TG 18:1_36:2              | 902.8         | 603.5       |
| TG 54:3 \[NL-18:2\] | TG 18:2_36:1              | 902.8         | 605.5       |

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

## The plan

We recall the following steps needed to clean such transition names.

-   Get the acyl class of the transition.

-   Get the total carbon number of the transition.

-   Get the total number of double bond of the transition

-   Get the total carbon number of the measured fatty acid chain.

-   Get the total number of double bond of the measured fatty acid chain.

-   Use the tools above to clean the transition name.

## Read Data

``` r
annotation_data <- readxl::read_excel(
  path = here::here("content", 
                    "blog",
                    "2022-04-23-Clean-Lipid-Names-3",
                    "Annotation.xlsx"),
  sheet = "Transition_Name_Annot"
  )

reactable::reactable(annotation_data, defaultPageSize = 5)
```

<div id="htmlwidget-1" class="reactable html-widget" style="width:auto;height:auto;"></div>
<script type="application/json" data-for="htmlwidget-1">{"x":{"tag":{"name":"Reactable","attribs":{"data":{"Given Name":["DG 32:0 [-16:0]","DG 36:1 [NL-18:1]","TG 54:3  [-18:1]","TG 54:3  [NL-18:2]","TG 54:3  [SIM]"],"Precursor Ion":[586.5,640.6,902.8,902.8,902.8],"Product Ion":[313.3,341.3,603.5,605.5,902.8]},"columns":[{"accessor":"Given Name","name":"Given Name","type":"character"},{"accessor":"Precursor Ion","name":"Precursor Ion","type":"numeric"},{"accessor":"Product Ion","name":"Product Ion","type":"numeric"}],"defaultPageSize":5,"paginationType":"numbers","showPageInfo":true,"minRows":1,"dataKey":"4e317afefcf906ebc6a3b0b6ceb3ac38","key":"4e317afefcf906ebc6a3b0b6ceb3ac38"},"children":[]},"class":"reactR_markup"},"evals":[],"jsHooks":[]}</script>

## Get the acyl class

To extract the (DG or DAG) or (TG or TAG) in the front of the transition name, we first add the `^` to indicate the software to look at the beginning of the string. Next, as the first letter can only be a D or T, we use the pattern `[D|T]`. Recall that `|` means or. As A is optional (appear zero or one time), we add a `?` add the end of the pattern `A`. Finally we simply add the G at the end.

This gives the final pattern to be `^[D|T]A?G`

``` r
acyl_class <- "TG 54:3" %>%
    stringr::str_extract(pattern = "^[D|T]A?G")

acyl_class
```

    ## [1] "TG"

## Labels to clean

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
#' clean_acyl_dynamo(input_acyl = "DG 32:0 [-16:0]")
#' @rdname clean_acyl
#' @export
clean_acyl <- function(input_acyl = "DG 32:0 [NL-16:0]") {

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

## Package References

``` r
report::cite_packages(sessionInfo())
```

-   Greg Lin (2020). reactable: Interactive Data Tables Based on ‘React Table.’ R package version 0.2.3. https://CRAN.R-project.org/package=reactable
-   Hadley Wickham (2019). stringr: Simple, Consistent Wrappers for Common String Operations. R package version 1.4.0. https://CRAN.R-project.org/package=stringr
-   Hadley Wickham and Jennifer Bryan (2022). readxl: Read Excel Files. R package version 1.4.0. https://CRAN.R-project.org/package=readxl
-   Hadley Wickham, Romain François, Lionel Henry and Kirill Müller (2022). dplyr: A Grammar of Data Manipulation. R package version 1.0.8. https://CRAN.R-project.org/package=dplyr
-   Kelly Bodwin and Hunter Glanz (2020). flair: Highlight, Annotate, and Format your R Source Code. R package version 0.0.2. https://CRAN.R-project.org/package=flair
-   Kirill Müller (2020). here: A Simpler Way to Find Your Files. R package version 1.0.1. https://CRAN.R-project.org/package=here
-   Makowski, D., Ben-Shachar, M.S., Patil, I. & Lüdecke, D. (2020). Automated Results Reporting as a Practical Tool to Improve Reproducibility and Methodological Best Practices Adoption. CRAN. Available from https://github.com/easystats/report. doi: .
-   Nils Hoffmann and Dominik Kopczynski (2022). rgoslin: Lipid Shorthand Name Parsing and Normalization. R package version 0.99.3. https://github.com/lifs-tools/rgoslin
-   R Core Team (2022). R: A language and environment for statistical computing. R Foundation for Statistical Computing, Vienna, Austria. URL https://www.R-project.org/.
-   Stefan Milton Bache and Hadley Wickham (2022). magrittr: A Forward-Pipe Operator for R. R package version 2.0.3. https://CRAN.R-project.org/package=magrittr

## References
