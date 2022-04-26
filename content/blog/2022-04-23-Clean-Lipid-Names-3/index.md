---
title: "Cleaning Lipid Names for Annotation Part 3"
subtitle: ""
excerpt: "This post provides some tips on how to clean lipid names input suited for some current nomenclature tools using R"
date: 2022-04-23
author: "Jeremy Selva"
draft: false
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

Just to recall, these transition names measure the amount of fatty acyl chain attached to the given DG or TG. For example, TG 54:3 \[NL-18:1\] measures the amount of fatty acyl chain 18:1 attached to TG 54:3 while TG 54:3 \[-18:2\] measures the amount of fatty acyl chain 18:2 attached to TG 54:3 instead.

In general, they are in the form
- {acyl_class} {total_C}:{total_DB} \[NL-{measured_C}:{measured_DB}\].

We need to transform into the form

-   {acyl_class} {measured_C}:{measured_DB}\_{remaining_C}:{remaining_DB}

where

-   {remaining_C} is {total_C - measured_C}
-   {remaining_DB} is {total_DB - measured_DB}

## R packages used

``` r
library("rgoslin")
library("reactable")
library("flair")
library("here")
library("readxl")
library("magrittr")
library("stringr")
library("dplyr")
library("purrr")
library("report")
```

## The plan

We recall the following steps needed to clean such transition names.

-   Get the acyl class of the transition. {acyl_class}

-   Get the total carbon number of the transition. {total_C}

-   Get the total number of double bond of the transition {total_DB}

-   Get the total carbon number of the measured fatty acid chain. {measured_C}

-   Get the total number of double bond of the measured fatty acid chain. {measured_DB}

-   Use the tools above to clean the transition name.

## Read data

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

## Get the acyl class {acyl_class}

We now try to get {acyl_class} from {acyl_class} {total_C}:{total_DB} \[NL-{measured_C}:{measured_DB}\].

To extract the (DG or DAG) or (TG or TAG) in the front of the transition name, we first add the `^` to indicate the software to look at the beginning of the string. Next, as the first letter can only be a D or T, we use the pattern `[D|T]`. Recall that `|` means or. As A is optional (appear zero or one time), we add a `?` add the end of the pattern `A`. Finally we simply add the G at the end.

This gives the final pattern to be `^[D|T]A?G`

<pre><code class='language-r'><code>acyl_class <- "TG 54:3 [NL-18:1]" %>%<br>&nbsp;&nbsp;&nbsp;&nbsp;stringr::str_extract(<span style='background-color:#d2f8d2'>pattern = "^[D|T]A?G"</span>)<br><br>acyl_class</code></code></pre>


    ## [1] "TG"

## Get the total carbon number of the transition {total_C}

The next step is to extract the total carbon number of the given transition or to get {total_C} from {acyl_class} {total_C}:{total_DB} \[NL-{measured_C}:{measured_DB}\]. In the case of TG 54:3 \[NL-18:1\], the total carbon number to 54. The key is to remove the {acyl_class} on the front first and then extract the total carbon.

To do this, we will need to make use of the {acyl_class} extracted earlier as a pattern and remove them using [`stringr::str_remove`](https://stringr.tidyverse.org/reference/str_remove.html).

For me, I use [`stringr::str_glue`](https://stringr.tidyverse.org/reference/str_glue.html) to achieve this pattern. `\\s*` is just a pattern to find white spaces and remove them.

<pre><code class='language-r'><code>total_C_step_1 <- "TG 54:3 [NL-18:1]" %>%<br>&nbsp;&nbsp;&nbsp;&nbsp;stringr::str_remove(<span style='background-color:#d2f8d2'>pattern = stringr::str_glue("{acyl_class}\\s*")</span>)<br><br>total_C_step_1</code></code></pre>


    ## [1] "54:3 [NL-18:1]"

After removing the {acyl_class} on the front, we will extract the pattern {total_C}:{total_DB} with using the pattern `^\\d+:\\d+`. This works when the digits are the first character of the string. Remember that `^` tells the software to look at the start of the string.

<pre><code class='language-r'><code>total_C_step_2 <- "TG 54:3 [NL-18:1]" %>%<br>&nbsp;&nbsp;&nbsp;&nbsp;stringr::str_remove(pattern = stringr::str_glue("{acyl_class}\\s*")) %>%<br>&nbsp;&nbsp;&nbsp;&nbsp;stringr::str_extract(<span style='background-color:#d2f8d2'>pattern = "^\\d+:\\d+"</span>)<br><br>total_C_step_2</code></code></pre>


    ## [1] "54:3"

From {total_C}:{total_DB}, we can then extract {total_C} using the pattern `^\\d+`

<pre><code class='language-r'><code>total_C <- "TG 54:3 [NL-18:1]" %>%<br>&nbsp;&nbsp;&nbsp;&nbsp;stringr::str_remove(pattern = stringr::str_glue("{acyl_class}\\s*")) %>%<br>&nbsp;&nbsp;&nbsp;&nbsp;stringr::str_extract(pattern = "^\\d+:\\d+") %>%<br>&nbsp;&nbsp;&nbsp;&nbsp;stringr::str_extract(<span style='background-color:#d2f8d2'>pattern = "^\\d+"</span>)<br><br>total_C</code></code></pre>


    ## [1] "54"

## Get the total number of double bond of the transition {total_DB}

The next step is to extract the total double bond number of the given transition or to get {total_DB} from {acyl_class} {total_C}:{total_DB} \[NL-{measured_C}:{measured_DB}\]. In the case of TG 54:3 \[NL-18:1\], the total number of double bonds is 3.

The extraction process is similar to the previous task. The only difference is that during the stage when we have obtained {total_C}:{total_DB}, we can extract {total_DB} using the pattern `\\d+$` instead. Recall that `$` tells the software to look at the end of the string.

<pre><code class='language-r'><code>total_DB <- "TG 54:3 [NL-18:1]" %>%<br>&nbsp;&nbsp;&nbsp;&nbsp;stringr::str_remove(pattern = stringr::str_glue("{acyl_class}\\s*")) %>%<br>&nbsp;&nbsp;&nbsp;&nbsp;stringr::str_extract(pattern = "^\\d+:\\d+") %>%<br>&nbsp;&nbsp;&nbsp;&nbsp;stringr::str_extract(<span style='background-color:#d2f8d2'>pattern = "\\d+$"</span>)<br><br>total_DB</code></code></pre>


    ## [1] "3"

## Get the total carbon number of the measured fatty acid chain {measured_C}

We now try to get {measured_C} from {acyl_class} {total_C}:{total_DB} \[NL-{measured_C}:{measured_DB}\]. To do this, first, we again remove the acyl class on the front, giving us {total_C}:{total_DB} \[NL-{measured_C}:{measured_DB}\]. In the case of TG 54:3 \[NL-18:1\], the total number of measured carbon bonds is 18.

<pre><code class='language-r'><code>measured_C_step1 <- "TG 54:3 [NL-18:1]" %>%<br>&nbsp;&nbsp;stringr::str_remove(<span style='background-color:#d2f8d2'>pattern = stringr::str_glue("{acyl_class}\\s*")</span>)<br>&nbsp;&nbsp;<br>measured_C_step1</code></code></pre>


    ## [1] "54:3 [NL-18:1]"

As the measured fatty acid chain comes with a `-`, we extract -{measured_C}:{measured_DB} from {total_C}:{total_DB} \[NL-{measured_C}:{measured_DB}\]. This is done by using the pattern `-\\s*\\d+:\\d+`

<pre><code class='language-r'><code>measured_C_step2 <- "TG 54:3 [NL-18:1]" %>%<br>&nbsp;&nbsp;stringr::str_remove(pattern = stringr::str_glue("{acyl_class}\\s*")) %>%<br>&nbsp;&nbsp;stringr::str_extract(<span style='background-color:#d2f8d2'>pattern = "-\\s*\\d+:\\d+"</span>)<br>&nbsp;&nbsp;<br>measured_C_step2</code></code></pre>


    ## [1] "-18:1"

We proceed to remove the `-` from -{measured_C}:{measured_DB}, giving us {measured_C}:{measured_DB}

<pre><code class='language-r'><code>measured_C_step3 <- "TG 54:3 [NL-18:1]" %>%<br>&nbsp;&nbsp;stringr::str_remove(pattern = stringr::str_glue("{acyl_class}\\s*")) %>%<br>&nbsp;&nbsp;stringr::str_extract(pattern = "-\\s*\\d+:\\d+") %>%<br>&nbsp;&nbsp;stringr::str_remove(<span style='background-color:#d2f8d2'>pattern = "-"</span>)<br>&nbsp;&nbsp;<br>measured_C_step3</code></code></pre>


    ## [1] "18:1"

Finally, we again use the pattern `^\\d+` to extract the {measured_C}

<pre><code class='language-r'><code>measured_C <- "TG 54:3 [NL-18:1]" %>%<br>&nbsp;&nbsp;stringr::str_remove(pattern = stringr::str_glue("{acyl_class}\\s*")) %>%<br>&nbsp;&nbsp;stringr::str_extract(pattern = "-\\s*\\d+:\\d+") %>%<br>&nbsp;&nbsp;stringr::str_remove(pattern = "-") %>%<br>&nbsp;&nbsp;stringr::str_extract(<span style='background-color:#d2f8d2'>pattern = "^\\d+"</span>)<br><br>measured_C</code></code></pre>


    ## [1] "18"

## Get the total number of double bond of the measured fatty acid chain {measured_DB}

We now try to get {measured_DB} from {acyl_class} {total_C}:{total_DB} \[NL-{measured_C}:{measured_DB}\]. In the case of TG 54:3 \[NL-18:1\], the total number of measured double bonds is 1.

The process is similar to the previous section, the difference is that during the stage when we have obtained {measured_C}:{measured_DB}, we can extract {measured_DB} using the pattern `\\d+$` instead.

<pre><code class='language-r'><code>measured_DB <- "TG 54:3 [NL-18:1]" %>%<br>&nbsp;&nbsp;&nbsp;&nbsp;stringr::str_remove(pattern = stringr::str_glue("{acyl_class}\\s*")) %>%<br>&nbsp;&nbsp;&nbsp;&nbsp;stringr::str_extract(pattern = "-\\s*\\d+:\\d+") %>%<br>&nbsp;&nbsp;&nbsp;&nbsp;stringr::str_remove(pattern = "-") %>%<br>&nbsp;&nbsp;&nbsp;&nbsp;stringr::str_extract(<span style='background-color:#d2f8d2'>pattern = "\\d+$"</span>)<br><br>measured_DB</code></code></pre>


    ## [1] "1"

## Check if extraction is successful

There will be situation when the extraction will fail due to a new input of transitions that the function has not encountered before. To check for this issue, we have the following.

<pre><code class='language-r'><code>input_acyl <- "TG 54:3 [NL-18:1]"<br><br>if (!<span style='background-color:#d2f8d2'>isTRUE</span>(stringr::str_detect(total_C, <span style='background-color:#d2f8d2'>"^[0-9]+$"</span>))) {<br>&nbsp;&nbsp;stop(glue::glue("Extracting total carbon in {input_acyl} has failed"))<br>}<br><br>if (!<span style='background-color:#d2f8d2'>isTRUE</span>(stringr::str_detect(total_DB, <span style='background-color:#d2f8d2'>"^[0-9]+$"</span>))) {<br>&nbsp;&nbsp;stop(glue::glue("Extracting total double bond in {input_acyl} has failed"))<br>}<br><br>if (!<span style='background-color:#d2f8d2'>isTRUE</span>(stringr::str_detect(measured_C, <span style='background-color:#d2f8d2'>"^[0-9]+$"</span>))) {<br>&nbsp;&nbsp;stop(glue::glue("Extracting measured carbon in {input_acyl} has failed"))<br>}<br><br>if (!<span style='background-color:#d2f8d2'>isTRUE</span>(stringr::str_detect(measured_DB, <span style='background-color:#d2f8d2'>"^[0-9]+$"</span>))) {<br>&nbsp;&nbsp;stop(glue::glue("Extracting measured double bond in {input_acyl} has failed"))<br>}</code></code></pre>

The pattern `^[0-9]+$` means the software will try to detect digits 0 to 9 (indicated by `[0-9]`). The digits can appear one or more times (indicated by `+`) and the start (indicated by `^`) and the end (indicated by `$`) of the string must contain only these digits.

The reason we use `isTRUE` is to ensure that only logicals `TRUE` and `FALSE` are returned. It is possible for `stringr::str_detect` to return `NA`. Take a look at this [Win Vector LLC blog post](https://win-vector.com/2018/06/11/r-tip-use-istrue) for more information.

## Use the tools above to clean the transition name

With the {acyl_class}, {total_C}, {total_DB}, {measured_C} and {measured_DB} extracted successfully, we can proceed to calculate

-   {remaining_C} as {total_C - measured_C}
-   {remaining_DB} as {total_DB - measured_DB}

``` r
remaining_C <- (as.numeric(total_C) - as.numeric(measured_C)) %>%
    as.character()

remaining_C
```

    ## [1] "36"

``` r
remaining_DB <- (as.numeric(total_DB) - as.numeric(measured_DB)) %>%
  as.character()

remaining_DB
```

    ## [1] "2"

Lastly, we use [`stringr::str_glue`](https://stringr.tidyverse.org/reference/str_glue.html) to construct {acyl_class} {measured_C}:{measured_DB}\_{remaining_C}:{remaining_DB}

``` r
clean_acyl <- stringr::str_glue(
    "{acyl_class} {measured_C}:{measured_DB}_{remaining_C}:{remaining_DB}"
  ) %>%
    as.character()

clean_acyl
```

    ## [1] "TG 18:1_36:2"

## Putting it all together

Combining what we have accomplished from the previous and this section, we have the following function and corresponding documentation.

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
#' clean_acyl(input_acyl = "DG 32:0 [-16:0]")
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

  output_acyl <- stringr::str_glue(
    "{acyl_class} {measured_C}:{measured_DB}_{remaining_C}:{remaining_DB}"
  ) %>%
    as.character()

  return(output_acyl)

}
```

## Plan execution

Here is how it looks like when the function is utilised.

``` r
cleaned_data <- annotation_data %>% 
  dplyr::mutate(
    `Clean Name For Annotation` = purrr::map(.data[["Given Name"]],
                                             clean_acyl
                                             ) )%>% 
  # Make Given Name and Clean Name the first two columns
  dplyr::relocate(
    dplyr::any_of(c("Given Name","Clean Name For Annotation"))
    ) 

cleaned_data %>%
  reactable::reactable(defaultPageSize = 5)
```

<div id="htmlwidget-2" class="reactable html-widget" style="width:auto;height:auto;"></div>
<script type="application/json" data-for="htmlwidget-2">{"x":{"tag":{"name":"Reactable","attribs":{"data":{"Given Name":["DG 32:0 [-16:0]","DG 36:1 [NL-18:1]","TG 54:3  [-18:1]","TG 54:3  [NL-18:2]","TG 54:3  [SIM]"],"Clean Name For Annotation":[["DG 16:0_16:0"],["DG 18:1_18:0"],["TG 18:1_36:2"],["TG 18:2_36:1"],["TG 54:3"]],"Precursor Ion":[586.5,640.6,902.8,902.8,902.8],"Product Ion":[313.3,341.3,603.5,605.5,902.8]},"columns":[{"accessor":"Given Name","name":"Given Name","type":"character"},{"accessor":"Clean Name For Annotation","name":"Clean Name For Annotation","type":"list"},{"accessor":"Precursor Ion","name":"Precursor Ion","type":"numeric"},{"accessor":"Product Ion","name":"Product Ion","type":"numeric"}],"defaultPageSize":5,"paginationType":"numbers","showPageInfo":true,"minRows":1,"dataKey":"05f036ebe49957979dc6b5b9ee5f590d","key":"05f036ebe49957979dc6b5b9ee5f590d"},"children":[]},"class":"reactR_markup"},"evals":[],"jsHooks":[]}</script>

``` r
cleaned_data[["Clean Name For Annotation"]] %>% 
  rgoslin::parseLipidNames() %>%
  reactable::reactable(defaultPageSize = 5)
```

<div id="htmlwidget-3" class="reactable html-widget" style="width:auto;height:auto;"></div>
<script type="application/json" data-for="htmlwidget-3">{"x":{"tag":{"name":"Reactable","attribs":{"data":{"Normalized.Name":["DG 16:0_16:0","DG 18:1_18:0","TG 18:1_36:2","TG 18:2_36:1","TG 54:3"],"Original.Name":["DG 16:0_16:0","DG 18:1_18:0","TG 18:1_36:2","TG 18:2_36:1","TG 54:3"],"Grammar":["Shorthand2020","Shorthand2020","Shorthand2020","Shorthand2020","Shorthand2020"],"Message":["NA","NA","NA","NA","NA"],"Adduct":["NA","NA","NA","NA","NA"],"Adduct.Charge":[0,0,0,0,0],"Lipid.Maps.Category":["GL","GL","GL","GL","GL"],"Lipid.Maps.Main.Class":["DG","DG","TG","TG","TG"],"Species.Name":["DG 32:0","DG 36:1","TG 54:3","TG 54:3","TG 54:3"],"Molecular.Species.Name":["DG 16:0_16:0","DG 18:1_18:0","TG 18:1_36:2","TG 18:2_36:1","NA"],"Sn.Position.Name":["NA","NA","NA","NA","NA"],"Structure.Defined.Name":["NA","NA","NA","NA","NA"],"Full.Structure.Name":["NA","NA","NA","NA","NA"],"Functional.Class.Abbr":["[DG]","[DG]","[TG]","[TG]","[TG]"],"Functional.Class.Synonyms":["[DG, DAG]","[DG, DAG]","[TG, TAG]","[TG, TAG]","[TG, TAG]"],"Level":["MOLECULAR_SPECIES","MOLECULAR_SPECIES","MOLECULAR_SPECIES","MOLECULAR_SPECIES","SPECIES"],"Total.C":[32,36,54,54,54],"Total.OH":[0,0,0,0,0],"Total.DB":[0,1,3,3,3],"Mass":[568.50667553,622.55362574,870.80402686,870.80402686,884.78329142],"Sum.Formula":["C35H68O5","C39H74O5","C57H106O5","C57H106O5","C57H104O6"],"FA1.Position":[-1,-1,-1,-1,"NA"],"FA1.C":[16,18,18,18,"NA"],"FA1.OH":[0,0,0,0,"NA"],"FA1.DB":[0,1,1,2,"NA"],"FA1.Bond.Type":["ESTER","ESTER","ESTER","ESTER",null],"FA1.DB.Positions":["[]","[]","[]","[]",null],"FA2.Position":[-1,-1,-1,-1,"NA"],"FA2.C":[16,18,36,36,"NA"],"FA2.OH":[0,0,0,0,"NA"],"FA2.DB":[0,0,2,1,"NA"],"FA2.Bond.Type":["ESTER","ESTER","ESTER","ESTER",null],"FA2.DB.Positions":["[]","[]","[]","[]",null],"LCB.Position":["NA","NA","NA","NA","NA"],"LCB.C":["NA","NA","NA","NA","NA"],"LCB.OH":["NA","NA","NA","NA","NA"],"LCB.DB":["NA","NA","NA","NA","NA"],"LCB.Bond.Type":[null,null,null,null,null],"LCB.DB.Positions":[null,null,null,null,null],"FA3.Position":[-1,-1,-1,-1,"NA"],"FA3.C":[0,0,0,0,"NA"],"FA3.OH":[0,0,0,0,"NA"],"FA3.DB":[0,0,0,0,"NA"],"FA3.Bond.Type":["ESTER","ESTER","ESTER","ESTER",null],"FA3.DB.Positions":["[]","[]","[]","[]",null],"FA4.Position":["NA","NA","NA","NA","NA"],"FA4.C":["NA","NA","NA","NA","NA"],"FA4.OH":["NA","NA","NA","NA","NA"],"FA4.DB":["NA","NA","NA","NA","NA"],"FA4.Bond.Type":[null,null,null,null,null],"FA4.DB.Positions":[null,null,null,null,null]},"columns":[{"accessor":"Normalized.Name","name":"Normalized.Name","type":"character"},{"accessor":"Original.Name","name":"Original.Name","type":"character"},{"accessor":"Grammar","name":"Grammar","type":"character"},{"accessor":"Message","name":"Message","type":"character"},{"accessor":"Adduct","name":"Adduct","type":"character"},{"accessor":"Adduct.Charge","name":"Adduct.Charge","type":"numeric"},{"accessor":"Lipid.Maps.Category","name":"Lipid.Maps.Category","type":"character"},{"accessor":"Lipid.Maps.Main.Class","name":"Lipid.Maps.Main.Class","type":"character"},{"accessor":"Species.Name","name":"Species.Name","type":"character"},{"accessor":"Molecular.Species.Name","name":"Molecular.Species.Name","type":"character"},{"accessor":"Sn.Position.Name","name":"Sn.Position.Name","type":"character"},{"accessor":"Structure.Defined.Name","name":"Structure.Defined.Name","type":"character"},{"accessor":"Full.Structure.Name","name":"Full.Structure.Name","type":"character"},{"accessor":"Functional.Class.Abbr","name":"Functional.Class.Abbr","type":"character"},{"accessor":"Functional.Class.Synonyms","name":"Functional.Class.Synonyms","type":"character"},{"accessor":"Level","name":"Level","type":"character"},{"accessor":"Total.C","name":"Total.C","type":"numeric"},{"accessor":"Total.OH","name":"Total.OH","type":"numeric"},{"accessor":"Total.DB","name":"Total.DB","type":"numeric"},{"accessor":"Mass","name":"Mass","type":"numeric"},{"accessor":"Sum.Formula","name":"Sum.Formula","type":"character"},{"accessor":"FA1.Position","name":"FA1.Position","type":"numeric"},{"accessor":"FA1.C","name":"FA1.C","type":"numeric"},{"accessor":"FA1.OH","name":"FA1.OH","type":"numeric"},{"accessor":"FA1.DB","name":"FA1.DB","type":"numeric"},{"accessor":"FA1.Bond.Type","name":"FA1.Bond.Type","type":"character"},{"accessor":"FA1.DB.Positions","name":"FA1.DB.Positions","type":"character"},{"accessor":"FA2.Position","name":"FA2.Position","type":"numeric"},{"accessor":"FA2.C","name":"FA2.C","type":"numeric"},{"accessor":"FA2.OH","name":"FA2.OH","type":"numeric"},{"accessor":"FA2.DB","name":"FA2.DB","type":"numeric"},{"accessor":"FA2.Bond.Type","name":"FA2.Bond.Type","type":"character"},{"accessor":"FA2.DB.Positions","name":"FA2.DB.Positions","type":"character"},{"accessor":"LCB.Position","name":"LCB.Position","type":"numeric"},{"accessor":"LCB.C","name":"LCB.C","type":"numeric"},{"accessor":"LCB.OH","name":"LCB.OH","type":"numeric"},{"accessor":"LCB.DB","name":"LCB.DB","type":"numeric"},{"accessor":"LCB.Bond.Type","name":"LCB.Bond.Type","type":"character"},{"accessor":"LCB.DB.Positions","name":"LCB.DB.Positions","type":"character"},{"accessor":"FA3.Position","name":"FA3.Position","type":"numeric"},{"accessor":"FA3.C","name":"FA3.C","type":"numeric"},{"accessor":"FA3.OH","name":"FA3.OH","type":"numeric"},{"accessor":"FA3.DB","name":"FA3.DB","type":"numeric"},{"accessor":"FA3.Bond.Type","name":"FA3.Bond.Type","type":"character"},{"accessor":"FA3.DB.Positions","name":"FA3.DB.Positions","type":"character"},{"accessor":"FA4.Position","name":"FA4.Position","type":"numeric"},{"accessor":"FA4.C","name":"FA4.C","type":"numeric"},{"accessor":"FA4.OH","name":"FA4.OH","type":"numeric"},{"accessor":"FA4.DB","name":"FA4.DB","type":"numeric"},{"accessor":"FA4.Bond.Type","name":"FA4.Bond.Type","type":"character"},{"accessor":"FA4.DB.Positions","name":"FA4.DB.Positions","type":"character"}],"defaultPageSize":5,"paginationType":"numbers","showPageInfo":true,"minRows":1,"dataKey":"7eb2a118539df235d064c56020cc9937","key":"7eb2a118539df235d064c56020cc9937"},"children":[]},"class":"reactR_markup"},"evals":[],"jsHooks":[]}</script>

## Package references

``` r
get_citation <- function(package_name) {
  transform_name <- package_name %>% 
    citation() %>% 
    format(style="text")
  return(transform_name)
} 

packages <- c("base","rgoslin", "reactable", "flair",
              "here", "readxl", "magrittr",
              "stringr", "dplyr", "report", "purrr")

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
-   Bodwin K, Glanz H (2020). *flair: Highlight, Annotate, and Format your
    R Source Code*. R package version 0.0.2,
    <https://CRAN.R-project.org/package=flair>.
-   Müller K (2020). *here: A Simpler Way to Find Your Files*. R package
    version 1.0.1, <https://CRAN.R-project.org/package=here>.
-   Wickham H, Bryan J (2022). *readxl: Read Excel Files*. R package
    version 1.4.0, <https://CRAN.R-project.org/package=readxl>.
-   Bache S, Wickham H (2022). *magrittr: A Forward-Pipe Operator for R*. R
    package version 2.0.3, <https://CRAN.R-project.org/package=magrittr>.
-   Wickham H (2019). *stringr: Simple, Consistent Wrappers for Common
    String Operations*. R package version 1.4.0,
    <https://CRAN.R-project.org/package=stringr>.
-   Wickham H, François R, Henry L, Müller K (2022). *dplyr: A Grammar of
    Data Manipulation*. R package version 1.0.8,
    <https://CRAN.R-project.org/package=dplyr>.
-   Makowski D, Ben-Shachar M, Patil I, Lüdecke D (2021). “Automated
    Results Reporting as a Practical Tool to Improve Reproducibility and
    Methodological Best Practices Adoption.” *CRAN*.
    <https://github.com/easystats/report>.
-   Henry L, Wickham H (2020). *purrr: Functional Programming Tools*. R
    package version 0.3.4, <https://CRAN.R-project.org/package=purrr>.
