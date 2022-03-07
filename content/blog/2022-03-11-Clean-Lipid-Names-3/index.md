---
title: "Cleaning Lipid Names for Annotation Part 3"
subtitle: ""
excerpt: "This post provides some tips on how to clean lipid names input suited for some current nomenclature tools using R"
date: 2022-03-07
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

## Package References

``` r
report::cite_packages(sessionInfo())
```

-   Greg Lin (2020). reactable: Interactive Data Tables Based on ‘React Table.’ R package version 0.2.3. https://CRAN.R-project.org/package=reactable
-   Hadley Wickham (2019). stringr: Simple, Consistent Wrappers for Common String Operations. R package version 1.4.0. https://CRAN.R-project.org/package=stringr
-   Hadley Wickham and Jennifer Bryan (2019). readxl: Read Excel Files. R package version 1.3.1. https://CRAN.R-project.org/package=readxl
-   Hadley Wickham, Romain François, Lionel Henry and Kirill Müller (2021). dplyr: A Grammar of Data Manipulation. R package version 1.0.7. https://CRAN.R-project.org/package=dplyr
-   Kelly Bodwin and Hunter Glanz (2020). flair: Highlight, Annotate, and Format your R Source Code. R package version 0.0.2. https://CRAN.R-project.org/package=flair
-   Kirill Müller (2020). here: A Simpler Way to Find Your Files. R package version 1.0.1. https://CRAN.R-project.org/package=here
-   Makowski, D., Ben-Shachar, M.S., Patil, I. & Lüdecke, D. (2020). Automated Results Reporting as a Practical Tool to Improve Reproducibility and Methodological Best Practices Adoption. CRAN. Available from https://github.com/easystats/report. doi: .
-   Nils Hoffmann and Dominik Kopczynski (2022). rgoslin: Lipid Shorthand Name Parsing and Normalization. R package version 0.99.3. https://github.com/lifs-tools/rgoslin
-   R Core Team (2021). R: A language and environment for statistical computing. R Foundation for Statistical Computing, Vienna, Austria. URL https://www.R-project.org/.
-   Stefan Milton Bache and Hadley Wickham (2022). magrittr: A Forward-Pipe Operator for R. R package version 2.0.2. https://CRAN.R-project.org/package=magrittr

## References

<div id="refs" class="references csl-bib-body">

<div id="ref-GOSLIN" class="csl-entry">

<span class="csl-left-margin">1. </span><span class="csl-right-inline">Kopczynski D, Hoffmann N, Peng B, Ahrends R. Goslin: A grammar of succinct lipid nomenclature. Analytical Chemistry \[Internet\]. 2020;92(16):10957–60. Available from: <https://doi.org/10.1021/acs.analchem.0c01690></span>

</div>

<div id="ref-Fahy2020" class="csl-entry">

<span class="csl-left-margin">2. </span><span class="csl-right-inline">Fahy E, Subramaniam S. RefMet: A reference nomenclature for metabolomics. Nature Methods \[Internet\]. 2020 Dec 1;17(12):1173–4. Available from: <https://doi.org/10.1038/s41592-020-01009-y></span>

</div>

</div>
