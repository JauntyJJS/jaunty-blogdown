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

## Introduction

In this blog, I will introduce another set of lipid annotations that my workplace uses that require to be cleaned up and modified so that they can be processed by lipid annotations converter tools like [Goslin](https://lifs-tools.org/goslin) (1) and [RefMet](https://metabolomicsworkbench.org/databases/refmet/index.php) (2).

## R Packages Used

``` r
library("rgoslin")
library("reactable")
library("here")
library("readxl")
library("magrittr")
library("stringr")
library("dplyr")
library("report")
```

## Labels to clean

Here are the list of lipid names to clean

| Given Name             | Clean Name For Annotation | Precursor Ion | Product Ion |
|------------------------|---------------------------|---------------|-------------|
| DG 32:0 \[-16:0\]      | DG 16:0_16:0              | 586.5         | 313.3       |
| DG 36:1 \[NL-18:1\]    | LPC(O-18:1)               | 640.6         | 341.3       |
| TG 54:3 \[-18:1\]      | LPC(P-18:1)               | 902.8         | 603.5       |
| TG 54:3 \[NL-18:2\]    | LPE 18:1                  | 902.8         | 605.5       |
| TG 54:3 \[SIM\]        | LPE(P-18:1)               | 902.8         | 902.8       |
| TG(O-50:2) \[-18:1\]   | PC 32:0                   | 834.8         | 535.5       |
| TG(O-50:2) \[NL-18:2\] | PC(O-32:0)                | 834.8         | 537.5       |
| TG(O-50:2) \[SIM\]     | PC(P-32:0)                | 834.8         | 834.8       |

Unfortunately lipid annotations converter tools like Goslin and RetMet is unable to parse these given names

``` r
c("DG 32:0 [-16:0]",
  "TG 54:3 [NL-18:2]",
  "TG(O-50:2) [NL-18:2]") %>%
  rgoslin::parseLipidNames()
```

    ## Warning in rcpp_parse_lipid_name(as.character(lipidNames[[i]])): Parsing of
    ## lipid name 'DG 32:0 [-16:0]' caused an exception: Lipid not found

    ## Warning in rcpp_parse_lipid_name(as.character(lipidNames[[i]])): Parsing of
    ## lipid name 'TG 54:3 [NL-18:2]' caused an exception: Lipid not found

    ## Warning in rcpp_parse_lipid_name(as.character(lipidNames[[i]])): Parsing of
    ## lipid name 'TG(O-50:2) [NL-18:2]' caused an exception: Lipid not found

    ## data frame with 0 columns and 0 rows

They must be clean up accordingly

``` r
c("DG 16:0_16:0",
  "TG 18:2_36:1",
  "TG (O-18:0_36:0)") %>%
  rgoslin::parseLipidNames() %>%
  reactable::reactable(defaultPageSize = 5)
```

    ## Warning in rcpp_parse_lipid_name(as.character(lipidNames[[i]])): Parsing of
    ## lipid name 'TG (O-18:0_36:0)' caused an exception: Lipid not found

<div id="htmlwidget-1" class="reactable html-widget" style="width:auto;height:auto;"></div>
<script type="application/json" data-for="htmlwidget-1">{"x":{"tag":{"name":"Reactable","attribs":{"data":{"Normalized.Name":["DG 16:0_16:0","TG 18:2_36:1"],"Original.Name":["DG 16:0_16:0","TG 18:2_36:1"],"Grammar":["Shorthand2020","Shorthand2020"],"Message":["NA","NA"],"Adduct":["NA","NA"],"Adduct.Charge":[0,0],"Lipid.Maps.Category":["GL","GL"],"Lipid.Maps.Main.Class":["DG","TG"],"Species.Name":["DG 32:0","TG 54:3"],"Molecular.Species.Name":["DG 16:0_16:0","TG 18:2_36:1"],"Sn.Position.Name":["NA","NA"],"Structure.Defined.Name":["NA","NA"],"Full.Structure.Name":["NA","NA"],"Functional.Class.Abbr":["[DG]","[TG]"],"Functional.Class.Synonyms":["[DG, DAG]","[TG, TAG]"],"Level":["MOLECULAR_SPECIES","MOLECULAR_SPECIES"],"Total.C":[32,54],"Total.OH":[0,0],"Total.DB":[0,3],"Mass":[568.50667553,870.80402686],"Sum.Formula":["C35H68O5","C57H106O5"],"FA1.Position":[-1,-1],"FA1.C":[16,18],"FA1.OH":[0,0],"FA1.DB":[0,2],"FA1.Bond.Type":["ESTER","ESTER"],"FA1.DB.Positions":["[]","[]"],"FA2.Position":[-1,-1],"FA2.C":[16,36],"FA2.OH":[0,0],"FA2.DB":[0,1],"FA2.Bond.Type":["ESTER","ESTER"],"FA2.DB.Positions":["[]","[]"],"LCB.Position":["NA","NA"],"LCB.C":["NA","NA"],"LCB.OH":["NA","NA"],"LCB.DB":["NA","NA"],"LCB.Bond.Type":[null,null],"LCB.DB.Positions":[null,null],"FA3.Position":[-1,-1],"FA3.C":[0,0],"FA3.OH":[0,0],"FA3.DB":[0,0],"FA3.Bond.Type":["ESTER","ESTER"],"FA3.DB.Positions":["[]","[]"],"FA4.Position":["NA","NA"],"FA4.C":["NA","NA"],"FA4.OH":["NA","NA"],"FA4.DB":["NA","NA"],"FA4.Bond.Type":[null,null],"FA4.DB.Positions":[null,null]},"columns":[{"accessor":"Normalized.Name","name":"Normalized.Name","type":"character"},{"accessor":"Original.Name","name":"Original.Name","type":"character"},{"accessor":"Grammar","name":"Grammar","type":"character"},{"accessor":"Message","name":"Message","type":"character"},{"accessor":"Adduct","name":"Adduct","type":"character"},{"accessor":"Adduct.Charge","name":"Adduct.Charge","type":"numeric"},{"accessor":"Lipid.Maps.Category","name":"Lipid.Maps.Category","type":"character"},{"accessor":"Lipid.Maps.Main.Class","name":"Lipid.Maps.Main.Class","type":"character"},{"accessor":"Species.Name","name":"Species.Name","type":"character"},{"accessor":"Molecular.Species.Name","name":"Molecular.Species.Name","type":"character"},{"accessor":"Sn.Position.Name","name":"Sn.Position.Name","type":"character"},{"accessor":"Structure.Defined.Name","name":"Structure.Defined.Name","type":"character"},{"accessor":"Full.Structure.Name","name":"Full.Structure.Name","type":"character"},{"accessor":"Functional.Class.Abbr","name":"Functional.Class.Abbr","type":"character"},{"accessor":"Functional.Class.Synonyms","name":"Functional.Class.Synonyms","type":"character"},{"accessor":"Level","name":"Level","type":"character"},{"accessor":"Total.C","name":"Total.C","type":"numeric"},{"accessor":"Total.OH","name":"Total.OH","type":"numeric"},{"accessor":"Total.DB","name":"Total.DB","type":"numeric"},{"accessor":"Mass","name":"Mass","type":"numeric"},{"accessor":"Sum.Formula","name":"Sum.Formula","type":"character"},{"accessor":"FA1.Position","name":"FA1.Position","type":"numeric"},{"accessor":"FA1.C","name":"FA1.C","type":"numeric"},{"accessor":"FA1.OH","name":"FA1.OH","type":"numeric"},{"accessor":"FA1.DB","name":"FA1.DB","type":"numeric"},{"accessor":"FA1.Bond.Type","name":"FA1.Bond.Type","type":"character"},{"accessor":"FA1.DB.Positions","name":"FA1.DB.Positions","type":"character"},{"accessor":"FA2.Position","name":"FA2.Position","type":"numeric"},{"accessor":"FA2.C","name":"FA2.C","type":"numeric"},{"accessor":"FA2.OH","name":"FA2.OH","type":"numeric"},{"accessor":"FA2.DB","name":"FA2.DB","type":"numeric"},{"accessor":"FA2.Bond.Type","name":"FA2.Bond.Type","type":"character"},{"accessor":"FA2.DB.Positions","name":"FA2.DB.Positions","type":"character"},{"accessor":"LCB.Position","name":"LCB.Position","type":"numeric"},{"accessor":"LCB.C","name":"LCB.C","type":"numeric"},{"accessor":"LCB.OH","name":"LCB.OH","type":"numeric"},{"accessor":"LCB.DB","name":"LCB.DB","type":"numeric"},{"accessor":"LCB.Bond.Type","name":"LCB.Bond.Type","type":"character"},{"accessor":"LCB.DB.Positions","name":"LCB.DB.Positions","type":"character"},{"accessor":"FA3.Position","name":"FA3.Position","type":"numeric"},{"accessor":"FA3.C","name":"FA3.C","type":"numeric"},{"accessor":"FA3.OH","name":"FA3.OH","type":"numeric"},{"accessor":"FA3.DB","name":"FA3.DB","type":"numeric"},{"accessor":"FA3.Bond.Type","name":"FA3.Bond.Type","type":"character"},{"accessor":"FA3.DB.Positions","name":"FA3.DB.Positions","type":"character"},{"accessor":"FA4.Position","name":"FA4.Position","type":"numeric"},{"accessor":"FA4.C","name":"FA4.C","type":"numeric"},{"accessor":"FA4.OH","name":"FA4.OH","type":"numeric"},{"accessor":"FA4.DB","name":"FA4.DB","type":"numeric"},{"accessor":"FA4.Bond.Type","name":"FA4.Bond.Type","type":"character"},{"accessor":"FA4.DB.Positions","name":"FA4.DB.Positions","type":"character"}],"defaultPageSize":5,"paginationType":"numbers","showPageInfo":true,"minRows":1,"dataKey":"28c45172401b46de1aaa0ffd50952b83","key":"28c45172401b46de1aaa0ffd50952b83"},"children":[]},"class":"reactR_markup"},"evals":[],"jsHooks":[]}</script>

## References

<div id="refs" class="references csl-bib-body">

<div id="ref-GOSLIN" class="csl-entry">

<span class="csl-left-margin">1. </span><span class="csl-right-inline">Kopczynski D, Hoffmann N, Peng B, Ahrends R. Goslin: A grammar of succinct lipid nomenclature. Analytical Chemistry \[Internet\]. 2020;92(16):10957–60. Available from: <https://doi.org/10.1021/acs.analchem.0c01690></span>

</div>

<div id="ref-Fahy2020" class="csl-entry">

<span class="csl-left-margin">2. </span><span class="csl-right-inline">Fahy E, Subramaniam S. RefMet: A reference nomenclature for metabolomics. Nature Methods \[Internet\]. 2020 Dec 1;17(12):1173–4. Available from: <https://doi.org/10.1038/s41592-020-01009-y></span>

</div>

</div>
