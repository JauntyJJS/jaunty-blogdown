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

# Introduction

Despite efforts made to unified lipids shorthand notations and the rise of software dedicated to standardise lipid annotations, lipid names still remains diverse. This is due to limited ways lipid software may label a lipid and/or researchers’ personal preferences to annotate them.

Here, I would like to highlight some lipid annotations that my workplace uses and show how to modify them in R such that it can be processed by lipid annotations converter tools.

# Labels to clean

Here are the list of lipid names to clean

| Given Name             | Clean Name | Precursor Ion | Product Ion |
|------------------------|------------|---------------|-------------|
| LPC 13:0 (ISTD) (a)    | LPC 13:0   | 454.3         | 184.1       |
| LPC 13:0 (ISTD) (a\\b) | LPC 13:0   | 454.3         | 184.1       |
| LPC 13:0 (ISTD) (b)    | LPC 13:0   | 454.3         | 184.1       |
| LPC 17:1 (a)           | LPC 17:1   | 468.3         | 184.1       |
| LPC 17:1 (a/b/c)       | LPC 17:1   | 468.3         | 184.1       |
| LPC 17:1 (b)           | LPC 17:1   | 468.3         | 184.1       |
| LPC 17:1 (c)           | LPC 17:1   | 468.3         | 184.1       |

<https://metabolomics.baker.edu.au/method/mrm/TG566NL225>

Selected Ion Monitoring (SIM)

# References
